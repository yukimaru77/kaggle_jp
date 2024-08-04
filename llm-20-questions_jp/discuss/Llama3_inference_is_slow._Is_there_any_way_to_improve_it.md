# Llama3 の推論が遅い。改善する方法はある？
**yamitomo** *Sun Jul 21 2024 03:18:13 GMT+0900 (日本標準時)* (0 votes)
Llama3 で単一の応答を生成するのに 1 分以上かかります。速度を上げる方法はありますか？
---
# 他のユーザーからのコメント
> ## torino
> 
> 8 ビットまたは 4 ビットの量子化を使用できます。私は 4 ビットを使用していますが、1 つの T4 GPU で 20 ラウンドすべてをシミュレートするのに約 4 ～ 6 分かかります。
> 
> 
> 
> > ## yamitomoTopic Author
> > 
> > ありがとうございます。試してみます。
> > 
> > 
> > 
---
> ## Matthew S Farmer
> 
> 私の経験ではそうではありません… モデルの初期化コードを投稿してもらえますか？何千ものトークンを生成していますか？終了トークンと適切なパイプラインまたはチャットテンプレートはロードされていますか？
> 
> 
> 
> > ## yamitomoTopic Author
> > 
> > 初期化コードは以下のとおりです。
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
> > 出力トークン生成コードは以下のとおりです。
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
> > > 以下のような出力が得られますが、関連していますか？
> > > 
> > > ```
> > > Setting `pad_token_id` to `eos_token_id`:128001 for open-end generation.
> > > 
> > > ```
> > > 
> > > 
> > > 
---

このスレッドでは、ユーザーが Llama3 の推論速度の遅さについて質問しています。他のユーザーは、量子化を使用してモデルのサイズを小さくすることで速度を上げられる可能性があると提案しています。また、モデルの初期化コードや出力トークン生成コードが共有され、問題の原因を特定しようとしています。

このスレッドからわかることは、Llama3 は非常に強力なモデルですが、推論速度が遅いという課題があるということです。量子化やその他の最適化技術を使用して、速度を向上させることができます。
