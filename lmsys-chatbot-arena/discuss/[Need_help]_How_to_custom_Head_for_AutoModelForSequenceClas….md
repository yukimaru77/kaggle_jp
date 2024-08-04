# [Need help] How to custom Head for AutoModelForSequenceClassification with LoRA?

**Bao Loc Pham** *Sat Jul 20 2024 13:52:51 GMT+0900 (日本標準時)* (2 votes)

I've a model look like this

```
Gemma2ForSequenceClassification(
  (model): Gemma2Model(
    (embed_tokens): Embedding(256000, 3584, padding_idx=0)
    (layers): ModuleList(
      (0-41): 42 x Gemma2DecoderLayer(
        (self_attn): Gemma2SdpaAttention(
          (q_proj): Linear4bit(in_features=3584, out_features=4096, bias=False)
          (k_proj): Linear4bit(in_features=3584, out_features=2048, bias=False)
          (v_proj): Linear4bit(in_features=3584, out_features=2048, bias=False)
          (o_proj): Linear4bit(in_features=4096, out_features=3584, bias=False)
          (rotary_emb): Gemma2RotaryEmbedding()
        )
        (mlp): Gemma2MLP(
          (gate_proj): Linear4bit(in_features=3584, out_features=14336, bias=False)
          (up_proj): Linear4bit(in_features=3584, out_features=14336, bias=False)
          (down_proj): Linear4bit(in_features=14336, out_features=3584, bias=False)
          (act_fn): PytorchGELUTanh()
        )
        (input_layernorm): Gemma2RMSNorm()
        (post_attention_layernorm): Gemma2RMSNorm()
        (pre_feedforward_layernorm): Gemma2RMSNorm()
        (post_feedforward_layernorm): Gemma2RMSNorm()
      )
    )
    (norm): Gemma2RMSNorm()
  )
  (score): Linear(in_features=3584, out_features=3, bias=False)
)

```

After applied LoRA, the model look like this

```
PeftModelForSequenceClassification(
  (base_model): LoraModel(
    (model): Gemma2ForSequenceClassification(
      (model): Gemma2Model(
        (embed_tokens): Embedding(256000, 3584, padding_idx=0)
        (layers): ModuleList(
         ....
            )
            (mlp): Gemma2MLP(
              ....
            )
            ...
          )
        )
        (norm): Gemma2RMSNorm()
      )
      (score): ModulesToSaveWrapper(
        (original_module): Linear(in_features=3584, out_features=3, bias=False)
        (modules_to_save): ModuleDict(
          (default): Linear(in_features=3584, out_features=3, bias=False)
        )
      )
    )
  )
)

```

Because of score module is just a simple fully connected layer, I want to make it more complex,

I tried to replace the head like this

```
CustomGemmaForSequenceClassification(
  (model): GemmaModel(
    (embed_tokens): Embedding(256000, 3584, padding_idx=0)
    (layers): ModuleList(
      (0-41): 42 x GemmaDecoderLayer(
        ...
        )
        (mlp): GemmaMLP(
        ...
        )
        (input_layernorm): GemmaRMSNorm()
        (post_attention_layernorm): GemmaRMSNorm()
      )
    )
    (norm): GemmaRMSNorm()
  )
  **(score): Sequential(
    (0): Linear4bit(in_features=7168, out_features=3584, bias=True)
    (1): Linear(in_features=3584, out_features=3, bias=False)
  )**
)

```

But after applied peft and LoRA, there is an error 

```
p.requires_grad_(requires_grad)
RuntimeError: only Tensors of floating point dtype can require gradients

```

I already put lora module_to_save=["score"] like this [huggingface tutorial](https://huggingface.co/docs/peft/en/developer_guides/custom_models) but seem not working yet



---

 # Comments from other users

> ## CPMP
> 
> Why use LORA on a matrix of rank 3?
> 
> The classification head linear layer has a rank of at most 3 because its dimension is 3584x3. 
> 
> TL;DR it does not make sense to apply LORA to the classification head.
> 
> 
> 
> > ## Bao Loc PhamTopic Author
> > 
> > [@cpmpml](https://www.kaggle.com/cpmpml) 
> > 
> > thank for your comment, the rank 3 you mean is the number of class.
> > 
> > - Yes, I don't want to apply LORA to the classification head.
> > 
> > I just apply these code like the huggingface tutorial
> > 
> > ```
> > lora_config = LoraConfig(
> >     r=config.lora_r,
> >     lora_alpha=config.lora_alpha,
> >     # only target self-attention
> >     target_modules=config.target_modules,
> >     layers_to_transform=[i for i in range(42) if i >= config.freeze_layers],
> >     lora_dropout=config.lora_dropout,
> >     bias=config.lora_bias,
> >     task_type=TaskType.SEQ_CLS,
> > )
> > model = AutoModelForSequenceClassification.from_pretrained(
> >     config.checkpoint,
> >     num_labels=3,
> >     torch_dtype=torch.float16,
> >     device_map="auto",
> >     quantization_config=quantization_config
> > )
> > model.config.use_cache = False
> > model = prepare_model_for_kbit_training(model)
> > model = get_peft_model(model, lora_config)
> > print(model)
> > 
> > print(model.print_trainable_parameters())
> > 
> > ```
> > 
> > the AutoModelForSequenceClassification class will create a simple neural network with 3 output.
> > 
> > but I want to replace with CustomModelForSequenceClassification with my custom head.
> > 
> > 
> > 
> > > ## Ashwani
> > > 
> > > you can specify the target_modules in which you want to apply LoRA. target_modules=["query", "key", "value"] specifies that LoRA should only be applied to the attention modules, effectively excluding the classification head.
> > > 
> > > 
> > > 
> > > ## CPMP
> > > 
> > > 
> > > the rank 3 you mean is the number of class.
> > > 
> > > The rank is  the rank of the matrix. LoRA is about approximating a high rank matrix with a low rank matrix. That's the lora_r parameter of LoRA. 
> > > 
> > > What I am saying is that applying LoRA to the classification head only makes sense with lora_r smaller than 3.
> > > 
> > > 
> > > 


---

