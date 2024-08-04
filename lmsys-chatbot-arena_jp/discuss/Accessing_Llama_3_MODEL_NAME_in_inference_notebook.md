# Llama 3 モデルの MODEL_NAME にアクセスする

**JamshaidSohail** *2024年7月15日 月曜日 00:07:29 GMT+0900 (日本標準時)* (1票)

こんにちは。私は [@kishanvavdara](https://www.kaggle.com/kishanvavdara) さんの素晴らしい [TPU Llama 3 トレーニングノートブック](https://www.kaggle.com/code/kishanvavdara/lmsys-llama-3-tpu-train) を正常に実行することができました。そして今、推論ノートブックを実行しようとしています。私はすでに Hugging Face と Meta の公式ページの両方で Llama 3 の使用許可を得ており、対応する Hugging Face トークンと重みファイルも持っています。[推論ノートブック](https://www.kaggle.com/code/kishanvavdara/inference-llama-3-8b) を実行しようとすると、以下のエラーが発生します。

```
OSError: Incorrect path_or_model_id: '/kaggle/input/llama-3/transformers/8b-chat-hf/1'. Please provide either the path to a local folder or the repo_id of a model on the Hub.
```

推論ノートブックではインターネットアクセスが無効になっています。そのため、トレーニングノートブックで行ったように、Hugging Face ハブからモデルをダウンロードする `MODEL_NAME="meta-llama/Meta-Llama-3-8B-Instruct"` を使用することはできません。何か助けがあれば幸いです。 [@valentinwerner](https://www.kaggle.com/valentinwerner) 

---
# 他のユーザーからのコメント

> ## Valentin Werner
> 
> まず、Kaggle で Llama アクセスをリクエストする必要があります。モデルのリンクに従ってリクエストできます。次に、ノートブックに Llama モデルがモデルとして追加されていることを確認してください。そうすれば、パスは正しくなります。
> 
> 
> 
> > ## JamshaidSohailトピック作成者
> > 
> > 私はすでに Meta の公式ページを使用して Llama モデルへのアクセスを取得しており、Kaggle を通じてフォームを送信しました。それがすぐに承認されることを願っています。そうすれば、すぐに進めることができます :D。改めてありがとうございます。
> > 
> > 
> > 
> > > ## JamshaidSohailトピック作成者
> > > 
> > > [@valentinwerner](https://www.kaggle.com/valentinwerner) さん、ありがとうございます。アクセス権を取得し、推論を実行することができました :D
> > > 
> > > 
> > > 
> > > ## Valentin Werner
> > > 
> > > 土曜日に1時間以内にアクセス権を取得できたなんて素晴らしいですね！24時間以上待ったという報告もありました。トレーニング頑張ってください - toi toi toi 😉
> > > 
> > > 
> > > 
---

