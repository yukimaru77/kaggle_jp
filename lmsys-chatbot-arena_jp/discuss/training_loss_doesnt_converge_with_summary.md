# 要約 
このディスカッションは、KaggleのLMSYS - Chatbot Arena Human Preference Predictionsコンペティションに参加しているユーザー、ivan_c2004が、DeBERTa XSmallモデルをPEFTを使って学習させた際に、学習損失が収束しない問題に直面していることから始まります。

ivan_c2004は、バッチサイズ8、学習率1e-4で、40,000から56,000のデータを使って学習させていますが、損失は約1.01で、6〜7エポック後も減少しません。GPUがRTX 3060のため、10エポック以上学習させるには時間がかかりすぎるため、学習を止めています。

他のユーザーからのコメントでは、以下の解決策が提案されています。

* **yechenzhi1**: バッチサイズを大きくする（gradient_accumulation_stepsを100に増やす）ことで、学習がうまくいくようになったと報告しています。
* **Valentin Werner**: モデルが小さすぎる可能性があり、Baseモデルやより大きな実効バッチサイズ、より低い学習率で学習させることを提案しています。また、XSmallモデルでPEFTを使用するよりも、KaggleのGPUで小さなモデルを完全にファインチューニングすることを推奨しています。さらに、Hugging Faceのトークンがコードに漏れていることを指摘し、削除することを勧めています。

ivan_c2004は、これらのコメントに対して感謝の意を表し、提案された解決策を試すことを表明しています。

このディスカッションは、コンペティション参加者が直面する課題や解決策を共有し、互いに助け合うための場として機能していることがわかります。


---
# 学習損失が収束しない

**ivan_c2004** *2024年6月8日 土曜日 22:15:28 JST* (1票)

皆さん、こんにちは。私はDeBERTa XSmallモデルをPEFTを使って学習させています。バッチサイズは8、学習率は1e-4で、学習データは40,000から56,000の範囲です。モデルを学習させるたびに、損失は約1.01で、6〜7エポック後も減少しません。私のGPUはRTX 3060のみで、10エポック以上学習させると1日以上かかります。オンラインのウェブサイトで読んだところ、LoRAによるファインチューニングは数エポックで済むはずなので、それ以上学習させていません。この問題を解決する方法、または損失が0.2や0.3などの特定の数値に達するまで、さらにエポックを学習させてみるべきでしょうか？どうもありがとうございます。

学習コードは以下の通りです。ありがとうございます。

```
from peft import get_peft_config, PeftModel, PeftConfig, get_peft_model, LoraConfig, TaskType
import torch
import sklearn
import numpy as np
import pandas as pd
import time
from tqdm import tqdm
from torch.nn import CrossEntropyLoss
from torch.utils.data import DataLoader, Dataset
from sklearn.model_selection import train_test_split
import matplotlib.pyplot as plt
from transformers import AutoTokenizer, LlamaModel, LlamaForSequenceClassification, BitsAndBytesConfig,get_linear_schedule_with_warmup,AutoModelForSequenceClassification,DebertaTokenizerFast
from torch.cuda.amp import autocast
torch.backends.cuda.enable_mem_efficient_sdp(False)
torch.backends.cuda.enable_flash_sdp(False)
if (not torch.cuda.is_available()): print("Sorry - GPU required!")
print(torch.__version__)
if torch.cuda.is_available(): print('gpu available')
from huggingface_hub import login
login(token="")
class CustomDataset(Dataset):
    def __init__(self, df, tokenizer):
        self.df = df
        self.tokenizer = tokenizer
    def __len__(self):
        return len(self.df)
    def __getitem__(self, idx):
        text = self.df.loc[idx, 'text']
        labels_a = self.df.loc[idx, 'winner_model_a']
        labels_b = self.df.loc[idx, 'winner_model_b']
        labels_tie = self.df.loc[idx, 'winner_tie']
        max_length = 1024
        inputs = self.tokenizer(
            text,
            max_length=max_length,
            truncation=True,
            padding="max_length",
            return_tensors="pt"
        )
        input_ids = inputs['input_ids'].squeeze()
        attention_mask = inputs['attention_mask'].squeeze()
        labels = torch.tensor([labels_a, labels_b, labels_tie]) 
        return {
            'input_ids': input_ids,
            'attention_mask': attention_mask,
            'labels': labels  
        }
bnb_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_use_double_quant=True,
    bnb_4bit_quant_type="nf4",
    bnb_4bit_compute_dtype=torch.float16
)
print(torch.cuda.get_device_name(0))
model_id = "microsoft/deberta-v3-xsmall"
tokenizer_id = "microsoft/deberta-v3-xsmall"
tokenizer = AutoTokenizer.from_pretrained(tokenizer_id)
model = AutoModelForSequenceClassification.from_pretrained(
    model_id,
    num_labels=3,
    torch_dtype=torch.float16,
    quantization_config=bnb_config,
    device_map='cuda:0')
model.config.pad_token_id = tokenizer.pad_token_id
tokenizer.pad_token = tokenizer.eos_token
peft_config = LoraConfig(
    r=16,
    lora_alpha=32,
    lora_dropout=0.10,
    bias='none',
    task_type=TaskType.SEQ_CLS,
    )
device = torch.device('cuda:0')
baseline_model = get_peft_model(model, peft_config).to(device)
baseline_model.print_trainable_parameters()
baseline_model.eval()
lr = 1e-4
num_epochs = 16
batch_size = 8
kaggle = False
train_df = pd.read_csv('./lmsys-chatbot-arena/train.csv')
print('number of training data: ',len(train_df))
train_df = train_df.iloc[:]
def process(input_str):
    stripped_str = input_str.strip('[]')
    sentences = [s.strip('"') for s in stripped_str.split('","')]
    return ' '.join(sentences)
train_df.loc[:, 'prompt'] = train_df['prompt'].apply(process)
train_df.loc[:, 'response_a'] = train_df['response_a'].apply(process)
train_df.loc[:, 'response_b'] = train_df['response_b'].apply(process)
train_df['text'] = 'User prompt: ' + train_df['prompt'] + '\n\nModel A :\n' + train_df['response_a'] + '\n\n--------\n\nModel B:\n' + train_df['response_b']
train_df = train_df.reset_index(drop=True)
if kaggle:
    print(f'number of training data {len(train_df)}')
else:
    train_df, val_df = train_test_split(train_df, test_size=0.2, random_state=42)
    train_df = train_df.reset_index(drop=True)
    val_df = val_df.reset_index(drop=True)
    print(f'number of training data after spliting: {len(train_df)} number of testing data: {len(val_df)}')
    val_dataset = CustomDataset(val_df, tokenizer)
    val_dataloader = DataLoader(val_dataset, batch_size=batch_size, shuffle=False)
train_dataset = CustomDataset(train_df, tokenizer)
train_dataloader = DataLoader(train_dataset, batch_size=batch_size, shuffle=False)
import gc
gc.collect()
torch.cuda.empty_cache()
criterion = CrossEntropyLoss()
optimizer = torch.optim.AdamW(baseline_model.parameters(), lr=lr)
lr_scheduler = torch.optim.lr_scheduler.StepLR(optimizer, step_size=5, gamma=0.1)
training_losses = []  
validation_losses = []  
for epoch in range(num_epochs):
    baseline_model.train()
    epoch_training_loss = 0  
    for step, batch in enumerate(tqdm(train_dataloader)):
        batch = {k: v.to(device) for k, v in batch.items()} 
        inputs = {
            'input_ids': batch['input_ids'],
            'attention_mask': batch['attention_mask'],
        }
        outputs = baseline_model(**inputs)
        labels = batch['labels'].float()
        loss = criterion(outputs.logits, labels)
        loss.backward()
        optimizer.zero_grad()
        epoch_training_loss += loss.item() 
    epoch_training_loss /= len(train_dataloader)  
    training_losses.append(epoch_training_loss) 
    baseline_model.eval()
    if not kaggle:
        total_validation_loss = 0
        total_samples = 0
        correct_predictions = 0
        with torch.no_grad():
            for step, batch in enumerate(tqdm(val_dataloader)):
                batch = {k: v.to(device) for k, v in batch.items()}  
                inputs = {
                    'input_ids': batch['input_ids'],
                    'attention_mask': batch['attention_mask'],
                }
                outputs = baseline_model(**inputs)
                predictions = outputs.logits.argmax(dim=-1)
                labels = batch['labels'].float().argmax(dim=1)
                loss = criterion(outputs.logits, labels)
                total_validation_loss += loss.item()
                total_samples += len(labels)
                correct_predictions += (predictions == labels).sum().item()
        epoch_validation_loss = total_validation_loss / len(val_dataloader)
        validation_losses.append(epoch_validation_loss)  
        accuracy = correct_predictions / total_samples
        print(f"Validation Loss: {epoch_validation_loss:.4f}, Accuracy: {accuracy:.4f}")
    print(f"Epoch {epoch+1}: Training Loss: {epoch_training_loss:.4f}")
plt.plot(training_losses, label='Training Loss')
plt.plot(validation_losses, label='Validation Loss')
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.legend()
plt.show()
torch.save(baseline_model.state_dict(), 'model.pt')
```

---
# 他のユーザーからのコメント

> ## yechenzhi1
> 
> バッチサイズを大きくすると、私の場合はうまくいきました（gradient_accumulation_stepsを100に増やしただけです）。
> 
> 
> 
> > ## ivan_c2004トピック作成者
> > 
> > ええ、勾配累積は役立ちます！ありがとう。
> > 
> > 学習にはどれくらい時間がかかりますか？推奨されるエポック数とバッチサイズは？
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > 学習時間は、GPUとモデルのサイズによって異なります。私は単に1エポックと400のバッチサイズを試しました（あまり実験していません。これは単なる個人的な選択です）。
> > > 
> > > 
> > > 
> > > ## ivan_c2004トピック作成者
> > > 
> > > わかりました。どうもありがとうございます！
> > > 
> > > 
> > > 
---
> ## Valentin Werner
> 
> モデルが小さすぎるかもしれません。私はBaseモデル、より大きな実効バッチサイズ、より低い学習率で、すべてのデータを使って数エポック学習させたところ、収束が見られました。
> 
> XSmallモデルでPEFTを使用することも、必ずしも良い選択ではありません。KaggleのGPUなら、小さなモデルを完全にファインチューニングできます。
> 
> また、Hugging Faceのトークンが漏れています。削除することをお勧めします。
> 
> 
> 
> > ## ivan_c2004トピック作成者
> > 
> > わかりました。
> > 
> > 漏洩を教えていただきありがとうございます。
> > 
> > 
> > 
---


