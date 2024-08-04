# training loss doesnt converge

**ivan_c2004** *Sat Jun 08 2024 22:15:28 GMT+0900 (日本標準時)* (1 votes)

Hello guys, i am using deberta xsmall with peft for training. the batch size is 8 and the learning rate is 1e-4, data for training is the range 40k to 56k , everytime i train the model the loss keeps at about 1.01, doesnt decrease after 6-7 epoches. my gpu is rtx 3060 only and training for ten or more epoches would take me more than a day and that i read from online websites lora finertuning llm should take only a few epoches so i didnt try for more epoches. Does anyone know how to solve this issue, or just try training for more epoches until the loss reaches a certain number like 0.2 0.3? thank you so much

My codes for training can be found below. Thank you 

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

 # Comments from other users

> ## yechenzhi1
> 
> larger batch size helped for me( I just increased gradient_accumulation_steps to 100)
> 
> 
> 
> > ## ivan_c2004Topic Author
> > 
> > yah gradient accumulation can help! thx. 
> > 
> > how long does the training take? what is the suggested epoch and batch size?
> > 
> > 
> > 
> > > ## yechenzhi1
> > > 
> > > Training time is up to your GPUs and model size. And I simply tried 1 epoch and 400 batch size( I didn't do much experiments, this is just my personal choice)
> > > 
> > > 
> > > 
> > > ## ivan_c2004Topic Author
> > > 
> > > I see. Thank you so much!
> > > 
> > > 
> > > 


---

> ## Valentin Werner
> 
> model might be too small. took me Base model, Higher effective batch size and lower lr with all data for some epochs to her ANY convergence
> 
> Using PEFT with XSmall model might not be preferrable either, training on kaggle GPU can easily handle full finetune of the small models.
> 
> Also you leaked your huggingface token, I recommend to remove that.
> 
> 
> 
> > ## ivan_c2004Topic Author
> > 
> > i see. 
> > 
> > thank you so much for reminding me the leak 
> > 
> > 
> > 


---

