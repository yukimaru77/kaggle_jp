# スターターノートブック 34B LLM すごい！ - Nvidia が KDD Cup 2024 で優勝！すごい！
**Chris Deotte** *2024年7月20日 土曜日 10:19:17 JST* (151票)

皆さん、こんにちは。9時間以内に25,000件のテストサンプルを推論するために、34B LLM を推論する方法を示すスターターノートブックを共有したいと思います [こちら](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm)。残り2週間半しかないので、あまり多くは共有しませんが、いくつかアイデアを共有します。

# 量子化 4bit AWQ を使用する
このコンペティションでは、2xT4 GPU 16GB VRAM で推論する必要があります。そのため、合計32GB VRAM があります。34B LLM は fp16 で 70GB のサイズですが、4bit を使用すると 20GB のサイズになります（つまり、X 億パラメータモデルは 4bit で 0.6X GB のサイズになります）。34B LLM を 20GB に削減すると、32GB VRAM に収まります！やった！

# vLLM を使用して推論する
テストデータは 25,000 件のサンプルなので、高速に推論する必要があります。サンプルごとに平均 1.3 秒で推論する必要があります！ライブラリ vLLM [こちら](https://docs.vllm.ai/en/latest/) は、Hugging Face や純粋な PyTorch コードよりも高速です！サンプルごとに 1 秒以下で簡単に推論できます！

# スターターノートブック
[こちら](https://www.kaggle.com/code/cdeotte/infer-34b-with-vllm) に、Kaggle の LMSYS コンペティションで 34B LLM を推論して、9 時間以内に 25,000 件のテスト予測を完了する方法を示すスターターノートブックを公開しました！私のスターターノートブックは、いくつかのトリックを示しています。

- Kaggle ノートブックに vLLM をインストールする方法
- モデルが "A"、"B"、"tie" のみを出力するように、logits プロセッサを使用する方法
- これらの 3 つのトークンから確率を抽出する方法
- 入力トークンの長さ、出力トークンの長さを最適化する方法
- LLM プロンプトのフォーマット方法

# KDD Cup 2024
今年は、KDD Cup 2024 で 5 人の NVIDIA 同僚 [@aerdem4](https://www.kaggle.com/aerdem4) [@titericz](https://www.kaggle.com/titericz) [@sorokin](https://www.kaggle.com/sorokin) [@simjeg](https://www.kaggle.com/simjeg) [@benediktschifferer](https://www.kaggle.com/benediktschifferer) とチームを組む機会がありました。課題は、4xT4 を使用して推論を行い、2 時間以内に 11,000 件の電子商取引に関する質問に答える LLM を構築することでした。コンペティションページ [こちら](https://www.aicrowd.com/challenges/amazon-kdd-cup-2024-multi-task-online-shopping-challenge-for-llms)。NVIDIA Kaggle グランドマスター（KGMON [こちら](https://www.nvidia.com/en-us/ai-data-science/kaggle-grandmasters/)）の同僚から多くのことを学びました。ありがとうございました！私たちの共同のアイデアが、KDD Cup 2024 の 5 つのトラックすべてで 1 位を獲得しました！すごい！（LB [こちら](https://www.aicrowd.com/challenges/amazon-kdd-cup-2024-multi-task-online-shopping-challenge-for-llms/leaderboards))

# ソリューション
私たちのソリューションには、次の 3 つの主要なコンポーネントが含まれていました。

- 多くのトレーニングデータを作成する
- QLoRA を使用して可能な限り最大のモデルを微調整する
- 時間制限内で、限られたハードウェアで可能な限り高速に推論する

8 月下旬には、スペインのバルセロナで開催される KDD Cup 2024 カンファレンスで、KDD Cup ソリューションをライブで発表し、論文を公開します。詳細をお楽しみに！

---
 # 他のユーザーからのコメント
> ## Anish Vijay
> 
> 素晴らしい！
> 
> 
> 
---
> ## hwz13
> 
> とても分かりやすいです！very clear
> 
> 
> 
---
> ## kaggk
> 
> 素晴らしい！Brilliant！
> 
> 
> 
---
> ## Timmy Juicehouse
> 
> Chris、ここに来てくれてありがとう。そして、あなたの Nvidia チームにおめでとうございます。私たちのチームも上位にランクインしましたが、あなたたちは私たちよりもはるかに強いです。来月は結婚式の準備があるので、バルセロナには行けません。Kdd2024 であなたのソリューションを楽しみにしています。
> 
> 
> 
---
> ## Metin Meki Abullrahman
> 
> 素晴らしい仕事！N!ce Work 😍
> 
> 
> 
---
> ## Cindy Y
> 
> 素晴らしい！Very good! 
> 
> 
> 
---
> ## Kid Liu
> 
> 素晴らしい仕事！Nice work!
> 
> 
> 
---
> ## Sanket Pramod Bhure
> 
> わあ、素晴らしい仕事！wow Great work!
> 
> 
> 
---
> ## Liuyanfen166
> 
> 素晴らしい仕事！Nice work!
> 
> 
> 
---
> ## Rise_Hand
> 
> いつも素晴らしい仕事ですね！小さな質問があります。私の見解では、異なるモデルは、その構造とハイパーパラメータに基づいて、異なるトリックを持っています。過去の経験からコストを削減するにはどうすればよいでしょうか？つまり、過去の経験に基づいて、新しい異なるモデルからコストと最高の結果をどのようにトレードオフすればよいでしょうか？
> 
> 
> 
---
> ## YingxiZhang
> 
> わあ~~~素晴らしい仕事！wow~~~nice work
> 
> 
> 
---
> ## Cody_Null
> 
> データ生成について話しているのを見ました。これは、このようなもので行われていますか？それとも、テンプレートのようなものがありますか？
> 
> ```
> %pip install -q -U ipywidgets
> %pip install -q -U transformers
> %pip install -q -U tokenizers
> %pip install -q -U bitsandbytes
> %pip install -q -U torch
> 
> import pandas as pd
> from tqdm import tqdm
> import torch
> from huggingface_hub import login
> from transformers import AutoModelForCausalLM, AutoTokenizer, BitsAndBytesConfig
> import random
> 
> # 基本プロンプトとパラメータを定義する
> base_prompts = [
>     "返信に値する可能性のある単一の応答を生成し、返信に値する可能性を 1 から 10 のスコアで示します。例: '今日は何かお困りですか？' - 10, 'あなたの名前は？' - 10, 'それについてもっと教えてください。' - 9. フォーマット: '応答' - スコア。",
>     "返信に値する可能性のある単一の応答を生成し、返信に値する可能性を 1 から 10 のスコアで示します。例: 'こんにちは！' - 6, 'おはようございます。' - 7. フォーマット: '応答' - スコア。",
>     "返信に値しない可能性のある単一の応答を生成し、返信に値する可能性を 1 から 10 のスコアで示します。例: 'わかりません。' - 5, 'たぶんあなたは正しいです。調べてみます。' - 4. フォーマット: '応答' - スコア。",
>     "返信に値する可能性が低い単一の応答を生成し、返信に値する可能性を 1 から 10 のスコアで示します。例: 'はい。' - 3, 'いいえ。' - 2, 'うーん' - 1. フォーマット: '応答' - スコア。"
> ]
> num_convos = 10000
> batch_size = 128  # GPU メモリに合わせて調整する
> max_length = 512  # 必要な応答の長さに合わせて調整する
> 
> # モデルとトークナイザーの設定
> model_name = "google/gemma-2-9b"   #"mistralai/Mistral-7B-Instruct-v0.3"  #"meta-llama/Meta-Llama-3-8B-Instruct"
> bnb_config = BitsAndBytesConfig(
>     load_in_4bit=True,
>     bnb_4bit_compute_dtype=torch.float16
> )
> 
> # Hugging Face にログインする
> login(token="hf_JB")
> 
> # モデルとトークナイザーをロードする
> model = AutoModelForCausalLM.from_pretrained(
>     model_name,
>     quantization_config=bnb_config,
>     device_map="auto",
>     token="hf_JB"
> )
> tokenizer = AutoTokenizer.from_pretrained(model_name, token="hf_JB")
> 
> # pad_token を eos_token に設定する
> tokenizer.pad_token = tokenizer.eos_token
> 
> # デバイスを設定し、GPU の可用性を確認する
> torch.backends.cuda.enable_mem_efficient_sdp(False)
> torch.backends.cuda.enable_flash_sdp(False)
> if not torch.cuda.is_available():
>     raise EnvironmentError("申し訳ありません - GPU が必要です！")
> DEVICE = torch.device("cuda")
> 
> # データ抽出を指定する
> def extract_data(outputs, base_prompt):
>     convos = []
>     labels = []
>     for output in outputs:
>         response = tokenizer.decode(output, skip_special_tokens=True).strip()
> 
>         # 応答から基本プロンプトを削除する
>         if response.startswith(base_prompt):
>             response = response[len(base_prompt):].strip()
> 
>         # 応答とスコアを抽出する
>         if " - " not in response:
>             print('出力に - がありません')
>             continue
> 
>         try:
>             response_text = response.split(' - ')[0].strip().strip('"')
>             score = int(response.split(' - ')[1][:2].strip())
> 
>             # スコアが期待される範囲内にあることを確認する
>             if score < 1 or score > 10:
>                 print('無効なスコア')
>                 continue
> 
>         except (IndexError, ValueError):
>             print('壊れた出力')
>             continue
> 
>         convos.append(response_text)
>         labels.append(score)
> 
>     return convos, labels
> 
> # バッチで会話応答を生成する
> convos_df_lst = []
> labels_df_lst = []
> 
> for i in tqdm(range(0, num_convos, batch_size)):
>     # 多様な応答を促すために、基本プロンプトをランダムに選択する
>     base_prompt = random.choice(base_prompts)
>     batch_prompts = [base_prompt] * batch_size
>     encoding = tokenizer(batch_prompts, return_tensors="pt", padding=True, truncation=True, max_length=max_length)
>     input_ids = encoding["input_ids"].to(DEVICE)
>     attention_mask = encoding["attention_mask"].to(DEVICE)
> 
>     outputs = model.generate(input_ids, attention_mask=attention_mask, max_length=max_length, pad_token_id=tokenizer.eos_token_id, do_sample=True, temperature=0.7)
>     convos_batch, labels_batch = extract_data(outputs, base_prompt)
> 
>     convos_df_lst.extend(convos_batch)
>     labels_df_lst.extend(labels_batch)
> 
> # 重複する応答をフィルターする
> unique_responses = list(set(zip(convos_df_lst, labels_df_lst)))
> convos_df_lst, labels_df_lst = zip(*unique_responses) if unique_responses else ([], [])
> 
> # CSV に保存する
> df = pd.DataFrame({'convo': convos_df_lst, 'label': labels_df_lst})
> df['label'] = df['label'] >= 7
> display(df)
> output_path = "/mnt/batch/tasks/shared/LS_root/mounts/clusters/cn1/code/Users/CN/Output/dataset.csv"
> df.to_csv(output_path, index=False)
> 
> print(f"データセットが生成され、{output_path} に保存されました。")
> 
> ```
> 
> 
> 
---
> ## Waqar Ali
> 
> バルセロナでの発表、おめでとうございます！OAG チャレンジで全トラック優勝できたことを共有できて嬉しいです。あなたの提出はわずかでしたが、このコンペティションでのトップランクの成績は本当に印象的です。あなたの功績に敬意を表します。🎁
> 
> 
> 
---
> ## WoNiu666
> 
> わあ~~~素晴らしい仕事！wow~~~great work
> 
> 
> 
---
> ## Yixiao Yuan
> 
> 共有してくれてありがとう。トレーニングと推論における量子化について質問があります。推論に int4 を使用する場合、トレーニング中に LoRA ではなく QLoRA を使用した方が良いでしょうか？これにより、トレーニングと推論の条件がより良く一致する可能性がありますが、QLoRA は LoRA ほど性能が良くないのではないかと懸念しています。ここでのトレードオフは何ですか？
> 
> 
> 
---
> ## sayoulala
> 
> おめでとうございます！バルセロナでの発表を楽しみにしています。私たちは、別のコンペティション（OAG-challenge）でも全トラック優勝しました。
> 
> このコンペティションで非常に少ないエントリーを提出したにもかかわらず、トップランクにランクインしているのを見て、私はあなたをとても尊敬しています。
> 
> 
> 
> > ## Chris Deotteトピック作成者
> > 
> > ありがとう [@sayoulala](https://www.kaggle.com/sayoulala) ここで素晴らしい成績を収めたことに、おめでとうございます！
> > 
> > 私は 1 週間前にこのコンペティションに参加し、KDD Cup 2024 で学んだ洞察を試しています。これまでのところ、アイデアはうまく移行し、ここでうまくいくのに役立っています！
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > vllm を使用すると、精度の低下につながりますか？
> > > 
> > > 
> > > 
> > > ## sayoulala
> > > 
> > > ところで、私の友人 [@chizhu2018](https://www.kaggle.com/chizhu2018) はあなたの熱心なファンです。バルセロナの KDD に行くなら、彼のためにあなたのサインをもらえますか？
> > > 
> > > 
> > > 
> > ## yechenzhi1
> > 
> > lmsys コンペティションで 9B よりも大きいモデルを使用していますか？
> > 
> > 
> > 
> > > ## sayoulala
> > > 
> > > 申し訳ありませんが、コンペティションが終了するまでは公開しません。
> > > 
> > > 
> > > 
> > > ## yechenzhi1
> > > 
> > > 全く問題ありません！自分で大きなモデルを試してみます😁 
> > > 
> > > 
> > > 
> > > ## Ilia Zaitsev
> > > 
> > > これまでのところ、モデルが大きければ大きいほど、損失が低くなるように見えます…
> > > 
> > > 
> > > 
---
> ## HinePo
> 
> ここに来てくれてありがとう、[@cdeotte](https://www.kaggle.com/cdeotte)。コンペティションが終了したら、あなたから再び多くのことを学べると期待しています。
> 
> vLLM は、生成ではなくシーケンス分類に使用できますか？
> 
> 少し検索しましたが、何も見つかりませんでした。
> 
> 
> 
> > ## Chris Deotteトピック作成者
> > 
> > vLLM をシーケンス分類に使用することはできないと思います。そのため、私のノートブックまたは Llama3-8B スターターノートブック [こちら](https://www.kaggle.com/code/shelterw/sft-llama-3-8b-inference) を使用して vLLM を使用する必要があります。これはテキスト生成を使用しています。
> > 
> > 
> > 
---
> ## Valentin Werner
> 
> これは、このチャレンジの勝利ソリューション投稿のように感じます。2 週間早すぎませんか？KDD Cup のパフォーマンス、おめでとうございます。あなたから、このチャレンジに合わせて調整された、このような投稿がもう 1 つ投稿されるのを楽しみにしています 😉
> 
> 編集: また、34B モデルをトレーニングする必要があるのでしょうか？
> 
> 
> 
> > ## yechenzhi1
> > 
> > 
> > 34B モデルをトレーニングする必要があるのでしょうか？
> > 
> > そうだと思います😂 ただ、上位のソリューションが現在、より大きなモデルを使用しているかどうかはわかりません。
> > 
> > 
> > 
> > > ## hn
> > > 
> > > 一部のソリューションはそうだと思います…私の現在の LB スコアは、実際にはこれまで小さな LM に基づいています。
> > > 
> > > 
> > > 
---
> ## Rishan Hasan Tenis
> 
> おめでとうございます。共有してくれてありがとう！[@cdeotte](https://www.kaggle.com/cdeotte) 
> 
> 
> 
---
> ## S J Moudry
> 
> AWQ は qlora と一緒に使用できますか？私が見たところ、SequenceClassification モデルタイプは、AutoAWQ/PEFT ではまだサポートされていません。完全な微調整を実行してから AWQ に変換しますか？
> 
> 
> 
> > ## Chris Deotteトピック作成者
> > 
> > 私たちは、あらゆる種類の 4bit 量子化で QLoRA を微調整します。微調整後、LoRA アダプターをマージし、AWQ で量子化します（推論の準備）。
> > 
> > 
> > 
---
> ## dexterxin
> 
> KDD Cup、おめでとうございます！
> 

> 限られたハードウェアで時間制限内に、9B 以上の事前学習済みモデルを微調整して推論できるようです。十分なコンピューティングリソースがない参加者にとっては朗報です。
> 
> ありがとうございました。今後のアイデアも楽しみにしています！
> 
> 
> 
---
> ## Ched Martin
> 
> おめでとうございます！
> 
> 
> 
---
> ## superferg
> 
> gemma2 27B を試したことはありますか？
> 
> 
> 
> > ## Yichuan Gao
> > 
> > 残念ながら、AutoAWQ はまだ Gemma-2 をサポートしていません。私も gemma-2 27b を試したかったのですが :(
> > 
> > 
> > 
---
> ## yechenzhi1
> 
> すごいですね！このコンペティションでは、9b が使用できる最大のモデルだと思っていました。
> 
> 
> 
> > ## Chris Deotteトピック作成者
> > 
> > いいえ。Kaggle の 2xT4 GPU で 34B を高速に推論できることがわかって嬉しいです。そのため、すべての Kaggle コンペティションで 34B を使用できます。[こちら](https://www.kaggle.com/competitions/kaggle-llm-science-exam/discussion/440620) でも示されているように、Kaggle で 70B を使用できますが、カスタマイズにより、vLLM と 34B を使用した場合よりも遅くなります。（そして、そのノートブックは、Kaggle の LMSYS コンペティションでは遅すぎます）。
> > 
> > 
> > 
---
> ## Harshit Sharma
> 
> 印象的な勝利と、これらの貴重な洞察を共有してくれてありがとうございます、[@cdeotte](https://www.kaggle.com/cdeotte)！あなたの革新的なアプローチとリソースの効率的な使用は、本当に刺激的です。バルセロナでの KDD Cup ソリューションのプレゼンテーションを見るのが待ちきれません！🌟🚀
> 
> 
> 
---


