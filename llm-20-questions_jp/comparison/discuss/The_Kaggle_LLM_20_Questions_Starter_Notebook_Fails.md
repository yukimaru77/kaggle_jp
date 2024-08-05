# 要約 
ディスカッションでは、ユーザーのmarketneutralがKaggleの「LLM 20 Questionsスタートノートブック」をクローンして保存した後、提出に失敗したことを報告しています。彼はその原因がわからず助けを求めています。Ryan Holbrookは、提出する際にノートブック自体ではなく、その出力を提出する必要があるとアドバイスしています。

marketneutralはそのアドバイスに従ったものの、まだエラーが発生していると報告し、エラーログを共有しました。内容を確認すると、エラーはモデルのトークナイザーに関連していることが示されています。彼は他のユーザーにKaggleのベースラインエージェントを提出できたかどうかも尋ねています。

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

# The Kaggle "LLM 20 Questions Starter Notebook" Fails

**marketneutral** *Thu May 16 2024 08:03:39 GMT+0900 (日本標準時)* (5 votes)

All I did was clone the notebook; save it; and hit submit. And it fails… Any ideas why?

[fail.PNG](https://storage.googleapis.com/kaggle-forum-message-attachments/2815506/20702/fail.PNG)

---

 # Comments from other users

> ## Ryan Holbrook
> 
> Hi [@marketneutral](https://www.kaggle.com/marketneutral), You'll need to submit the output of the notebook instead of the notebook itself. Check out the first cell of the notebook for more details.
> 
> 
> 
> > ## marketneutralTopic Author
> > 
> > Ok. Got it. Thank you. I tried that. It still errors. The log file:
> > 
> > ```
> > [[{"duration": 0.077924, "stdout": "Initializing model\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 130, in callable_agent\n    agent(*args) \\\n  File \"/kaggle_simulations/agent/main.py\", line 245, in agent_fn\n    response = get_agent('answerer')(obs)\n  File \"/kaggle_simulations/agent/main.py\", line 229, in get_agent\n    agent = GemmaAnswererAgent(\n  File \"/kaggle_simulations/agent/main.py\", line 187, in __init__\n    super().__init__(*args, **kwargs)\n  File \"/kaggle_simulations/agent/main.py\", line 106, in __init__\n    model = GemmaForCausalLM(model_config)\n  File \"/kaggle_simulations/agent/lib/gemma/model.py\", line 400, in __init__\n    self.tokenizer = tokenizer.Tokenizer(config.tokenizer)\n  File \"/kaggle_simulations/agent/lib/gemma/tokenizer.py\", line 24, in __init__\n    assert os.path.isfile(model_path), model_path\nAssertionError: /kaggle_simulations/agent/gemma/py"}]]
> > 
> > ```
> > 
> > 
> > 
> > > ## marketneutralTopic Author
> > > 
> > > Has anyone been able to submit the Kaggle baseline agents?
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# Kaggleの「LLM 20 Questionsスタートノートブック」が失敗する
**marketneutral** *2024年5月16日 08:03:39 JST* (5票)
ノートブックをクローンして保存し、提出ボタンを押しただけなんですが、それが失敗します…何が原因か分かりますか？
[fail.PNG](https://storage.googleapis.com/kaggle-forum-message-attachments/2815506/20702/fail.PNG)
---
# 他のユーザーからのコメント
> ## Ryan Holbrook
> 
> こんにちは[@marketneutral](https://www.kaggle.com/marketneutral)、ノートブック自体ではなく、ノートブックの出力を提出する必要があります。ノートブックの最初のセルで詳細を確認してみてください。
> 
> > ## marketneutral トピックの著者
> > 
> > わかりました。ありがとうございます。それを試してみましたが、まだエラーが出ます。ログファイル：
> > 
> > ```
> > [[{"duration": 0.077924, "stdout": "モデルを初期化中\n", "stderr": "Traceback (most recent call last):\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 159, in act\n    action = self.agent(*args)\n  File \"/opt/conda/lib/python3.10/site-packages/kaggle_environments/agent.py\", line 130, in callable_agent\n    agent(*args) \\\n  File \"/kaggle_simulations/agent/main.py\", line 245, in agent_fn\n    response = get_agent('answerer')(obs)\n  File \"/kaggle_simulations/agent/main.py\", line 229, in get_agent\n    agent = GemmaAnswererAgent(\n  File \"/kaggle_simulations/agent/main.py\", line 187, in __init__\n    super().__init__(*args, **kwargs)\n  File \"/kaggle_simulations/agent/main.py\", line 106, in __init__\n    model = GemmaForCausalLM(model_config)\n  File \"/kaggle_simulations/agent/lib/gemma/model.py\", line 400, in __init__\n    self.tokenizer = tokenizer.Tokenizer(config.tokenizer)\n  File \"/kaggle_simulations/agent/lib/gemma/tokenizer.py\", line 24, in __init__\n    assert os.path.isfile(model_path), model_path\nAssertionError: /kaggle_simulations/agent/gemma/py"}]]
> > 
> > 
> > 
> > > ## marketneutral トピックの著者
> > > > 
> > > 誰かKaggleのベースラインエージェントを提出できた人はいませんか？
> > > 
> > > > 



</div>