# 要約 
このディスカッションは、Kaggleで公開されているLlama 3モデルの8b-chat-hfバージョンについてです。

Dylan Liuは、Llama 3には通常のバージョンとインストラクトバージョンがあることを確認し、8b-chat-hfが何なのか、インストラクトバージョンはどこにあるのかを質問しています。

Weirenは、8b-chat-hfが対話ユースケース向けにファインチューニングされたHugging Face形式のモデルであると説明し、インストラクトモデルはHugging FaceからダウンロードしてKaggleにアップロードできるだろうと回答しています。

Cristóbal Mackenzieは、8b-chat-hfが実際にはHugging Faceのインストラクトモデルと同じであると指摘し、Weirenはそれを確認しています。

つまり、8b-chat-hfはLlama 3のインストラクトバージョンであり、Hugging FaceからダウンロードしてKaggleで使用することができます。


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

# What is 8b-chat-hf in kaggle's llama3 models? 

**Dylan Liu** *Thu Jul 11 2024 18:38:03 GMT+0900 (日本標準時)* (0 votes)

If I'm right, Llama 3 has a normal version and an instruct version. 

In [https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1](https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1), I see 8b-chat-hf, what's that? And where is the instruct version?



---

 # Comments from other users

> ## Weiren
> 
> I think the 8b-chat-hf one is fine-tuned for dialogue use cases and in huggingface format. 
> 
> The instruct model I think you can download from hugging face then upload to kaggle.
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > I actually think the 8b-chat-hf is the same as the instruct model in huggingface.
> > 
> > 
> > 
> > > ## Weiren
> > > 
> > > Yea, should be the same. thanks~
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# KaggleのLlama 3モデルにおける8b-chat-hfとは？

**Dylan Liu** *木曜日 7月 11日 2024 18:38:03 GMT+0900 (日本標準時)* (0票)

もし私が正しければ、Llama 3には通常のバージョンとインストラクトバージョンがあります。
[https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1](https://www.kaggle.com/models/metaresearch/llama-3/Transformers/8b-chat-hf/1) で、8b-chat-hf を見ましたが、これは何ですか？ インストラクトバージョンはどこにありますか？
---
# 他のユーザーからのコメント
> ## Weiren
> 
> 8b-chat-hf は、対話ユースケース向けにファインチューニングされており、Hugging Face形式です。
> 
> インストラクトモデルは、Hugging FaceからダウンロードしてKaggleにアップロードできると思います。
> 
> 
> 
> > ## Cristóbal Mackenzie
> > 
> > 実は、8b-chat-hf はHugging Faceのインストラクトモデルと同じだと思います。
> > 
> > 
> > 
> > > ## Weiren
> > > 
> > > はい、同じはずです。ありがとう〜
> > > 
> > > 
> > > 
--- 



</div>