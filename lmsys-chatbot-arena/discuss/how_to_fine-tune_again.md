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

