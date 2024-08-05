# 要約 
以下はコンペティション「LLM 20 Questions」に関するディスカッションの要約です。

---

**トピックタイトル: Llama3の推論が遅いのですが、改善方法はありますか？**

ユーザーのyamitomoが、Llama3を使用して応答を生成する際に1分以上かかると報告し、速度を向上させる方法を尋ねました。

### 主なコメント

1. **torinoの提案**:
   - 8ビットまたは4ビットの量子化を利用することで、処理速度が向上する可能性があると述べました。torinoは4ビットを使用した場合、1つのT4 GPUで20ラウンドのシミュレーションに約4〜6分を要すると報告しました。

2. **Matthew S Farmerの指摘**:
   - yamitomoに対して、応答生成が遅い理由はモデルの初期化方法やトークン生成処理の違いによる可能性があるとし、具体的な初期化コードやトークン生成コードを提示するよう求めました。yamitomoは自分の初期化コードを公開しました。

3. **yamitomoの実装確認**:
   - 提示された初期化コードや設定に基づいて、出力トークンの生成における設定が正しいかどうかの関連性を検討しました。

---

ディスカッションでは、Llama3の応答速度改善のための具体的な手法や設定についての情報交換が行われ、他のユーザーからの技術的アドバイスが共有されています。

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

# Llama3 inference is slow. Is there any way to improve it?

**yamitomo** *Sun Jul 21 2024 03:18:13 GMT+0900 (日本標準時)* (0 votes)

It takes more than a minute to generate a single response in Llama3. Is there any way to speed it up?



---

 # Comments from other users

> ## torino
> 
> you can use 8 bits or 4 bits quant, i use 4bits then it need about 4-6 minutes in simulation all 20 round on 1 t4 gpu.
> 
> 
> 
> > ## yamitomoTopic Author
> > 
> > Thank you, I will try that.
> > 
> > 
> > 


---

> ## Matthew S Farmer
> 
> Not my experience… Mind posting your code for initiating the model? Are you generating thousands of tokens? Do you have the end token and proper pipeline or chat template loaded? 
> 
> 
> 
> > ## yamitomoTopic Author
> > 
> > The initialization code is as follows:
> > 
> > ```
> > torch.backends.cuda.enable_mem_efficient_sdp(False)
> > torch.backends.cuda.enable_flash_sdp(False)
> > 
> > model_id = "/kaggle/input/llama-3/transformers/8b-chat-hf/1"
> > 
> > if debug:
> >     llm_model = None
> > else:
> >     llm_model = AutoModelForCausalLM.from_pretrained(model_id, torch_dtype=torch.bfloat16, device_map="auto")
> > 
> > questioner_agent = None
> > answerer_agent = None
> > guesser_agent = None
> > 
> > def initialize_agent(obs):
> >     global questioner_agent, answerer_agent, guesser_agent
> >     global llm_model
> > 
> >     match obs.turnType:
> >         case "ask":
> >             questioner_agent = Questioner(llm_model, debug)
> >         case "answer":
> >             answerer_agent = Answerer(llm_model, debug)
> >         case "guess":
> >             guesser_agent = Guesser(llm_model, debug)
> > 
> > def my_agent_fn(obs, cfg):
> >     match obs.turnType:
> >         case "ask":
> >             if questioner_agent is None:
> >                 initialize_agent(obs)
> >             return questioner_agent.get_question(obs)
> >         case "answer":
> >             if answerer_agent is None:
> >                 initialize_agent(obs)
> >             return answerer_agent.get_answer(obs)
> >         case "guess":
> >             if guesser_agent is None:
> >                 initialize_agent(obs)
> >             return guesser_agent.get_guess(obs)
> > 
> > ```
> > 
> > The output token generation code is as follows.
> > 
> > ```
> > from transformers import AutoTokenizer, AutoModelForCausalLM
> > from logging import getLogger
> > 
> > logger = getLogger(__name__)
> > 
> > def get_formatted_prompt(prompt, desc=None):
> >     prefix = "| "
> >     modified_prompt = "\n".join(prefix + line for line in prompt.split("\n"))
> > 
> >     formatted_prompt = ""
> >     if desc is None:
> >         formatted_prompt += ("-" * 30) + "\n"
> >     else:
> >         formatted_prompt += ("-" * 15) + f" {desc} " + ("-" * 15) + "\n"
> >     formatted_prompt += modified_prompt + "\n"
> >     formatted_prompt += "-" * 30
> > 
> >     return formatted_prompt
> > 
> > class Questioner:
> >     def __init__(self, llm_model, debug=False) -> None:
> >         print("Initializing model (Questioner 004)")
> > 
> >         self.debug = debug
> > 
> >         # 提出時変更必要！！！！！！！
> >         model_id = "/kaggle/input/llama-3/transformers/8b-chat-hf/1"
> > 
> >         self.tokenizer = AutoTokenizer.from_pretrained(model_id)
> >         self.model = llm_model
> >         self.id_eot = self.tokenizer.convert_tokens_to_ids(["<|eot_id|>"])[0]
> > 
> >     def get_question(self, obs):
> >         sys_prompt = """You are a helpful AI assistant, and your are very smart in playing 20 questions game,
> >         the user is going to think of a word, it can be only one of the following 3 categories:
> >         1. a place
> >         2. a person
> >         3. a thing
> >         So focus your area of search on these options. and give smart questions that narrows down the search space\n"""
> > 
> >         ask_prompt = sys_prompt + """your role is to find the word by asking him up to 20 questions, your questions to be valid must have only a 'yes' or 'no' answer.
> >         to help you, here's an example of how it should work assuming that the keyword is Morocco:
> >         examle:
> >         <you: is it a place?
> >         user: yes
> >         you: is it in europe?
> >         user: no
> >         you: is it in africa?
> >         user: yes
> >         you: do most people living there have dark skin?
> >         user: no
> >         user: is it a country name starting by m ?
> >         you: yes
> >         you: is it Morocco?
> >         user: yes.>
> > 
> >         the user has chosen the word, ask your first question!
> >         please be short and not verbose, give only one question, no extra word!"""
> > 
> >         chat_template = f"""<|begin_of_text|><|start_header_id|>system<|end_header_id|>\n\n{ask_prompt}<|eot_id|>"""
> > 
> >         chat_template += "<|start_header_id|>assistant<|end_header_id|>\n\n"
> > 
> >         if len(obs.questions) >= 1:
> >             for q, a in zip(obs.questions, obs.answers):
> >                 chat_template += f"{q}<|eot_id|><|start_header_id|>user<|end_header_id|>\n\n"
> >                 chat_template += f"{a}<|eot_id|><|start_header_id|>assistant<|end_header_id|>\n\n"
> > 
> >         question = self._call_llm(chat_template)
> > 
> >         return question
> > 
> >     def _call_llm(self, prompt):
> >         # print_prompt(prompt=prompt, desc="prompt to generate QUESTION")
> >         logger.debug("\n\n" + get_formatted_prompt(prompt=prompt, desc="prompt to generate QUESTION"))
> > 
> >         if self.debug:
> >             return "Is it a bug?"
> > 
> >         inp_ids = self.tokenizer(prompt, return_tensors="pt").to("cuda")
> > 
> >         # max_new_tokens必要か？？？？
> >         out_ids = self.model.generate(**inp_ids, max_new_tokens=15).squeeze()
> > 
> >         start_gen = inp_ids.input_ids.shape[1]
> >         out_ids = out_ids[start_gen:]
> > 
> >         if self.id_eot in out_ids:
> >             stop = out_ids.tolist().index(self.id_eot)
> >             out = self.tokenizer.decode(out_ids[:stop])
> >         else:
> >             out = self.tokenizer.decode(out_ids)
> > 
> >         return out
> > 
> > ```
> > 
> > 
> > 
> > > ## yamitomoTopic Author
> > > 
> > > I get output like this, is it relevant?
> > > 
> > > ```
> > > Setting `pad_token_id` to `eos_token_id`:128001 for open-end generation.
> > > 
> > > ```
> > > 
> > > 
> > > 


---



</div>
<div class="column-right">

# 日本語訳

# Llama3の推論が遅いのですが、改善方法はありますか？
**yamitomo** *2024年7月21日（日）03:18:13 JST* (0票)
Llama3での1回の応答生成に1分以上かかっています。速度を上げる方法はあるのでしょうか？

---
# 他のユーザーからのコメント
> ## torino
> 
> 8ビットや4ビットの量子化を使うことができます。私は4ビットを使用していますが、1つのT4 GPUで20ラウンドのシミュレーションを行うのに約4〜6分かかります。
> 
> > ## yamitomoトピック作成者
> > 
> > ありがとうございます、試してみます。
> > 
> > 
> > 
---
> ## Matthew S Farmer
> 
> 私の経験とは異なります… モデルを初期化するためのコードを投稿できますか？ 数千トークンを生成していますか？ 終了トークンや適切なパイプライン、チャットテンプレートは読み込まれていますか？
> 
> > ## yamitomoトピック作成者
> > 
> > 初期化コードは以下の通りです：
> > 
> > ```
> > torch.backends.cuda.enable_mem_efficient_sdp(False)
> > torch.backends.cuda.enable_flash_sdp(False)
> > 
> > model_id = "/kaggle/input/llama-3/transformers/8b-chat-hf/1"
> > 
> > if debug:
> >     llm_model = None
> > else:
> >     llm_model = AutoModelForCausalLM.from_pretrained(model_id, torch_dtype=torch.bfloat16, device_map="auto")
> > 
> > questioner_agent = None
> > answerer_agent = None
> > guesser_agent = None
> > 
> > def initialize_agent(obs):
> >     global questioner_agent, answerer_agent, guesser_agent
> >     global llm_model
> > 
> >     match obs.turnType:
> >         case "ask":
> >             questioner_agent = Questioner(llm_model, debug)
> >         case "answer":
> >             answerer_agent = Answerer(llm_model, debug)
> >         case "guess":
> >             guesser_agent = Guesser(llm_model, debug)
> > 
> > def my_agent_fn(obs, cfg):
> >     match obs.turnType:
> >         case "ask":
> >             if questioner_agent is None:
> >                 initialize_agent(obs)
> >             return questioner_agent.get_question(obs)
> >         case "answer":
> >             if answerer_agent is None:
> >                 initialize_agent(obs)
> >             return answerer_agent.get_answer(obs)
> >         case "guess":
> >             if guesser_agent is None:
> >                 initialize_agent(obs)
> >             return guesser_agent.get_guess(obs)
> > 
> > ```
> > 
> > 出力トークン生成のコードは以下の通りです。
> > 
> > ```
> > from transformers import AutoTokenizer, AutoModelForCausalLM
> > from logging import getLogger
> > 
> > logger = getLogger(__name__)
> > 
> > def get_formatted_prompt(prompt, desc=None):
> >     prefix = "| "
> >     modified_prompt = "\n".join(prefix + line for line in prompt.split("\n"))
> > 
> >     formatted_prompt = ""
> >     if desc is None:
> >         formatted_prompt += ("-" * 30) + "\n"
> >     else:
> >         formatted_prompt += ("-" * 15) + f" {desc} " + ("-" * 15) + "\n"
> >     formatted_prompt += modified_prompt + "\n"
> >     formatted_prompt += "-" * 30
> > 
> >     return formatted_prompt
> > 
> > class Questioner:
> >     def __init__(self, llm_model, debug=False) -> None:
> >         print("モデルを初期化中（Questioner 004）")
> > 
> >         self.debug = debug
> > 
> >         # 提出時変更必要！！！！！！！
> >         model_id = "/kaggle/input/llama-3/transformers/8b-chat-hf/1"
> > 
> >         self.tokenizer = AutoTokenizer.from_pretrained(model_id)
> >         self.model = llm_model
> >         self.id_eot = self.tokenizer.convert_tokens_to_ids(["<|eot_id|>"])[0]
> > 
> >     def get_question(self, obs):
> >         sys_prompt = """あなたは役に立つAIアシスタントで、20の質問ゲームをするのがとても得意です。
> >         ユーザーは言葉を考えています。それは以下の3つのカテゴリのうちの1つである必要があります：
> >         1. 場所
> >         2. 人
> >         3. 物
> >         そのため、これらのオプションの範囲に集中し、検索空間を狭めるための賢い質問をしてください。\n"""
> > 
> >         ask_prompt = sys_prompt + """あなたの役割は、彼に20の質問以内でその言葉を見つけることです。あなたの質問は、'はい'または'いいえ'の回答が必要です。
> >         助けるために、キーワードがモロッコの場合の動作例を示します：
> >         例：
> >         <あなた: それは場所ですか？
> >         ユーザー: はい
> >         あなた: ヨーロッパにありますか？
> >         ユーザー: いいえ
> >         あなた: アフリカにありますか？
> >         ユーザー: はい
> >         あなた: そこに住んでいる大多数の人は肌の色が暗いですか？
> >         ユーザー: いいえ
> >         ユーザー: mで始まる国名ですか？
> >         あなた: はい
> >         あなた: それはモロッコですか？
> >         ユーザー: はい。>
> > 
> >         ユーザーが言葉を選びました。最初の質問をしてください！
> >         短く簡潔にしてください。1つの質問のみを提供し、余計な言葉は不要です！"""
> > 
> >         chat_template = f"""<|begin_of_text|><|start_header_id|>system<|end_header_id|>\n\n{ask_prompt}<|eot_id|>"""
> > 
> >         chat_template += "<|start_header_id|>assistant<|end_header_id|>\n\n"
> > 
> >         if len(obs.questions) >= 1:
> >             for q, a in zip(obs.questions, obs.answers):
> >                 chat_template += f"{q}<|eot_id|><|start_header_id|>user<|end_header_id|>\n\n"
> >                 chat_template += f"{a}<|eot_id|><|start_header_id|>assistant<|end_header_id|>\n\n"
> > 
> >         question = self._call_llm(chat_template)
> > 
> >         return question
> > 
> >     def _call_llm(self, prompt):
> >         # プロンプトを表示する必要がありますか？（適切な質問生成プロンプト）
> >         logger.debug("\n\n" + get_formatted_prompt(prompt=prompt, desc="質問生成のためのプロンプト"))
> > 
> >         if self.debug:
> >             return "それはバグですか？"
> > 
> >         inp_ids = self.tokenizer(prompt, return_tensors="pt").to("cuda")
> > 
> >         # max_new_tokensが必要か確認してください。？
> >         out_ids = self.model.generate(**inp_ids, max_new_tokens=15).squeeze()
> > 
> >         start_gen = inp_ids.input_ids.shape[1]
> >         out_ids = out_ids[start_gen:]
> > 
> >         if self.id_eot in out_ids:
> >             stop = out_ids.tolist().index(self.id_eot)
> >             out = self.tokenizer.decode(out_ids[:stop])
> >         else:
> >             out = self.tokenizer.decode(out_ids)
> > 
> >         return out
> > 
> > ```
> > 
> > > ## yamitomoトピック作成者
> > > 
> > > このような出力を得ましたが、関連性はありますか？
> > > 
> > > ```
> > > `pad_token_id`を`eos_token_id`:128001に設定しました：オープンエンド生成のために。
> > > ```
> > > 
> > > 
> > > 
---


</div>