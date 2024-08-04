# 2枚のGPUでモデルを実行する方法

**KeShuang Liu** *2024年6月17日 月曜日 17:22:30 JST* (0票)

CPUにモデルをロードしたところ、19GBのメモリを使用しました。一方、GPU p100は16GBしかありませんでした。しかし、2つのt4ブロックを使用すると合計30GBになることがわかりました。この場合、モデルを2つのt4ブロックに展開できますか？どうすればよいですか？

---
# 他のユーザーからのコメント

> ## Minato Ryan
> 
> transformersライブラリを使用している場合は、`device_map="auto"`を使用してください。
> 
> 例えば、
> 
> ```
> AutoModelForCausalLM.from_pretrained("google-bert/bert-base-cased", device_map="auto")
> 
> ```
> 
> 
> 
> > ## KeShuang Liuトピック作成者
> > 
> > ご回答ありがとうございます。この方法で成功しました。
> > 
> > 
> > 
---

