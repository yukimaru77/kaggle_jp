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

