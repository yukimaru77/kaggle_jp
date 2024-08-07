# 要約 
このディスカッションは、Kaggleコンペティションで、AutoModelForSequenceClassificationモデルのカスタムヘッドにLoRAを適用しようとしているユーザーの質問と、他のユーザーからの回答で構成されています。

**質問:**

ユーザーは、Gemma2ForSequenceClassificationモデルのカスタムヘッドにLoRAを適用しようとしています。カスタムヘッドは、2つの線形層からなるシーケンシャルモジュールです。しかし、LoRAを適用すると、`RuntimeError: only Tensors of floating point dtype can require gradients`というエラーが発生します。

**回答:**

* **CPMP:** LoRAは、高ランク行列を低ランク行列で近似する手法です。分類ヘッドの線形層は、ランクが最大3なので、LoRAを適用しても効果は期待できません。
* **Ashwani:** LoRAを適用するターゲットモジュールを指定することができます。`target_modules=["query", "key", "value"]`のように指定することで、LoRAを注意モジュールにのみ適用し、分類ヘッドは除外することができます。
* **CPMP:** LoRAを分類ヘッドに適用する場合は、`lora_r`パラメータが3より小さい場合にのみ意味があります。

**結論:**

このディスカッションでは、LoRAをカスタムヘッドに適用する際の注意点が議論されています。LoRAは、高ランク行列を低ランク行列で近似する手法であり、分類ヘッドのような低ランク行列には効果が期待できません。また、LoRAを適用するターゲットモジュールを指定することで、分類ヘッドへの適用を回避することができます。

**ユーザーは、LoRAを注意モジュールにのみ適用し、分類ヘッドは除外することで、エラーを解決できる可能性があります。**


---
# [ヘルプが必要] AutoModelForSequenceClassification のカスタムヘッドを LoRA でどのように作成するか

**Bao Loc Pham** *2024年7月20日(土) 13:52:51 JST* (2票)

このようなモデルがあります。

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

LoRA を適用すると、モデルは次のようになります。

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

スコアモジュールは単純な全結合層なので、もっと複雑にしたいと思っています。

次のようにヘッドを置き換えてみました。

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

しかし、peft と LoRA を適用すると、エラーが発生します。

```
p.requires_grad_(requires_grad)
RuntimeError: only Tensors of floating point dtype can require gradients
```

[huggingface のチュートリアル](https://huggingface.co/docs/peft/en/developer_guides/custom_models)のように、lora module_to_save=["score"] を設定しましたが、まだうまくいきません。

---
# 他のユーザーからのコメント

> ## CPMP
> 
> なぜランク3の行列にLoRAを使うのですか？
> 
> 分類ヘッドの線形層は、その次元が3584x3なので、ランクが最大3です。
> 
> TL;DR 分類ヘッドにLoRAを適用するのは意味がありません。
> 
> 
> 
> > ## Bao Loc Phamトピック作成者
> > 
> > [@cpmpml](https://www.kaggle.com/cpmpml) 
> > 
> > コメントありがとうございます。ランク3というのは、クラスの数のことですね。
> > 
> > - はい、分類ヘッドにLoRAを適用したくありません。
> > 
> > huggingfaceのチュートリアルのように、このコードを適用しました。
> > 
> > ```
> > lora_config = LoraConfig(
> >     r=config.lora_r,
> >     lora_alpha=config.lora_alpha,
> >     # 自己注意のみをターゲットとする
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
> > AutoModelForSequenceClassificationクラスは、3つの出力を持つ単純なニューラルネットワークを作成します。
> > 
> > しかし、私はCustomModelForSequenceClassificationを私のカスタムヘッドで置き換えたいのです。
> > 
> > 
> > 
> > > ## Ashwani
> > > 
> > > LoRAを適用したいターゲットモジュールを指定することができます。target_modules=["query", "key", "value"] は、LoRA を注意モジュールにのみ適用し、分類ヘッドは除外することを指定します。
> > > 
> > > 
> > > 
> > > ## CPMP
> > > 
> > > 
> > > ランク3というのは、クラスの数のことですね。
> > > 
> > > ランクは行列のランクです。LoRAは、高ランク行列を低ランク行列で近似することです。それがLoRAのlora_rパラメータです。
> > > 
> > > 私が言いたいのは、分類ヘッドにLoRAを適用するのは、lora_rが3より小さい場合にのみ意味があるということです。
> > > 
> > > 
> > > 
---

