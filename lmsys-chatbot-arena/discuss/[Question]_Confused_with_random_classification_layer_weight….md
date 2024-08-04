# [Question] Confused with random classification layer weight(score.weight) for LlamaForSequenceClassification

**Xuhang_CN** *Sat Jul 20 2024 19:07:52 GMT+0900 (日本標準時)* (0 votes)

Hi , I am a freshman for llm. I want to SFT llama3 in my GPU.

When I check for the same train environment, I find classification layer weight is initialized randomly(maybe?):

When I run below code first time and second time, I get different score.weight.

model_raw = LlamaForSequenceClassification.from_pretrained(
    model_name,
    quantization_config=quantization_config,
    num_labels=3,
    device_map='auto'
model = prepare_model_for_kbit_training(model)
config = PeftConfig.from_pretrained(finetune_model_name)
model = PeftModel.from_pretrained(model, finetune_model_name,is_trainable=False)
)

Even if I load saved adapter weight, weight is still not the same.

So I want to know how to make sure I train llama3 in my GPU and upload adapter in kaggle to make sure I get the same model.

Thanks!



---

 # Comments from other users

> ## Valentin Werner
> 
> You could set the seed for the run. That way you always get the same initial values. Make sure versions are similar / identical between kaggle notebook and local. There are plenty of "seed all" functions on kaggle and google that you can use
> 
> 
> 


---

> ## hn
> 
> You may need to do a custom save LoRA as some combinations may render the LoRA saving the wrong weights.
> 
> 
> 


---

