# 要約 
このディスカッションは、Kaggleコンペティション「LMSYS - Chatbot Arena 人間による好み予測チャレンジ」における、Gemma2モデルのファインチューニングに関するものです。

Mukataiさんは、公開ノートブックでGemma2モデルのファインチューニング方法が紹介されているものの、すでにファインチューニングされたモデルを再度ファインチューニングする方法が分からず、質問を投稿しました。

Darshan Patelさんは、Mukataiさんの質問に回答し、Gemma2-9b-it-4bitの事前学習済みモデルを読み込み、`/kaggle/input/73zap2gx/checkpoint-5600` からLoRAアダプターを適用することで、新しいベースモデルを作成し、そのモデルを独自のデータセットとハイパーパラメータを使ってファインチューニングすれば良いと説明しました。

つまり、すでにファインチューニングされたモデルを再度ファインチューニングするには、事前学習済みモデルとLoRAアダプターを組み合わせた新しいベースモデルを作成し、そのモデルをさらにファインチューニングする必要があるということです。


---


<style>
.column-left{
  float: left;
  width: 47.5%;
  text-align: left;
}
.column-right{
  float: right;
  width: 47.5%;
  text-align: left;
}
.column-one{
  float: left;
  width: 100%;
  text-align: left;
}
</style>


<div class="column-left">

# original

# how to fine-tune again?

**Mukatai** *Tue Jul 16 2024 01:09:47 GMT+0900 (日本標準時)* (0 votes)

In the public notebook, there is information about fine-tuning the Gemma2 model. Do you know how to fine-tune a model that has already been fine-tuned again?

`@dataclass

class Config:

    gemma_dir = '/kaggle/input/gemma-2/transformers/gemma-2-9b-it-4bit/1/gemma-2-9b-it-4bit'

    lora_dir = '/kaggle/input/73zap2gx/checkpoint-5600'

    max_length = 2048

    batch_size = 4

    device = torch.device("cuda")    

    tta = False  # test time augmentation. --

    spread_max_length = False  # whether to apply max_length//3 on each input or max_length on the concatenated input

cfg = Config()`

I am trying to load a pre-trained model with lora_dir = '/kaggle/input/73zap2gx/checkpoint-5600', but the final results suggest that it has only trained on the additional data.



---

 # Comments from other users

> ## Darshan Patel
> 
> [@mukatai](https://www.kaggle.com/mukatai) You load the pre-trained model Gemma-2-9b-it-4bit and apply the LoRA adapter from /kaggle/input/73zap2gx/checkpoint-5600. This combined model becomes your new base model, which you then fine-tune using your own dataset and hyperparameters.
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# 再度ファインチューニングする方法

**Mukatai** *2024年7月16日 火曜日 01:09:47 日本標準時* (0票)

公開ノートブックには、Gemma2モデルのファインチューニングに関する情報があります。すでにファインチューニングされたモデルを再度ファインチューニングする方法をご存知ですか？

```python
@dataclass
class Config:
    gemma_dir = '/kaggle/input/gemma-2/transformers/gemma-2-9b-it-4bit/1/gemma-2-9b-it-4bit'
    lora_dir = '/kaggle/input/73zap2gx/checkpoint-5600'
    max_length = 2048
    batch_size = 4
    device = torch.device("cuda")    
    tta = False  # test time augmentation. --
    spread_max_length = False  # whether to apply max_length//3 on each input or max_length on the concatenated input
cfg = Config()
```

私は `lora_dir = '/kaggle/input/73zap2gx/checkpoint-5600'` を使って事前学習済みモデルを読み込もうとしていますが、最終的な結果は追加データでのみトレーニングされたことを示唆しています。

---
# 他のユーザーからのコメント

> ## Darshan Patel
> 
> [@mukatai](https://www.kaggle.com/mukatai) Gemma-2-9b-it-4bit の事前学習済みモデルを読み込み、`/kaggle/input/73zap2gx/checkpoint-5600` から LoRA アダプターを適用します。この組み合わせたモデルが新しいベースモデルとなり、そのモデルを独自のデータセットとハイパーパラメータを使ってファインチューニングします。
> 
> 
> 
---



</div>