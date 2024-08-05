# 要約 
ディスカッションでは、LLM（大規模言語モデル）の評価とその設定に関する情報が提供されています。主に以下の点が議論されています。

1. **Gemmaの評価と問題点**:
   - Gemma 7bの量子化モデルは、指示に従うのが苦手であり、競争力のあるパフォーマンスを発揮できていないと指摘されています。

2. **推奨される評価方法**:
   - LMSYS Arenaリーダーボードを用いたモデル評価が推奨されており、このシステムはユーザーが質問を投げかけ、2つのモデルからの回答を比較する方式です。これにより、ユーザーのニーズを一貫して満たすモデルを特定しやすくなっています。

3. **現在のトップモデル**:
   - GPT-4やGemini 1.5 Proといったモデルが具体的なEloスコアとともに評価されています。

4. **代替モデルの提案**:
   - LLaMA 3 8B Instructが強力な選択肢として挙げられ、量子化がまだ必要であることが指摘されています。また、llama.cppを利用することで推論を高速化することが可能とされています。

5. **他のユーザーからのフィードバック**:
   - 他のユーザーからは、llama-cpp-pythonの依存関係解決に関する問題についての質問が寄せられ、具体的な解決アドバイスを求めています。

全体として、Gemmaを含むさまざまなLLMの性能と評価方法が検討され、より競争力のあるモデルの開発への道筋が示されています。また、実際の実装における課題も共有されています。

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

# LLM overview and Llama 3 setup

**Raki** *Sat May 18 2024 21:29:56 GMT+0900 (日本標準時)* (6 votes)

## Evaluation of Gemma and Other LLMs

### Issues with Gemma

Gemma 7b it quant, which is used in the starting notebook, struggles with following instructions and doesn't achieve state-of-the-art performance for its size. 

### Recommended LLM Evaluation: LMSYS Arena Leaderboard

To identify a robust general LLM, I recommend the [LMSYS Arena Leaderboard](https://chat.lmsys.org/). This Elo rating system involves users asking questions and comparing answers from two different models (blind) to determine which one they prefer. This evaluation method is challenging to "game" as success depends on consistently satisfying user queries across various topics. Other metrics can suffer from benchmark leakage into the training set and often focus on narrower tasks, making them easier to optimize for specific performance rather than general utility.

### Current Top Models

- GPT-4: 1287 Elo

- Gemini 1.5 Pro (Google): 1248 Elo

- Best Anthropic Model: 1246 Elo

- LLaMA 3 70B Instruct (Meta): 1203 Elo (best open-source model, but too large)

### Gemma's Performance (like in starter)

- Gemma 7B-IT: 1043 Elo

- Quantized Version: Slightly worse (Quantization reduces weights from formats like FP32 to INT8, significantly lowering VRAM and compute requirements at the cost of some quality)

### Alternative: LLaMA 3 8B Instruct

- LLaMA 3 8B Instruct: 1155 Elo (a much stronger model overall)

We still need to quantize it to run it on the T4 available for submission, which has 16 GiB of VRAM.

### Best Way to Run Inference: llama.cpp

As far as I know, the best way to run inference on a non-proprietary quantized LLM is with llama.cpp. This tool employs various techniques to speed up inference, such as quantization and KV caching.

### Resources for LLaMA 3 8B Instruct

I have previously set up a dataset with some quantized LLaMA 3 8B Instruct models:

- [Dataset](https://www.kaggle.com/datasets/raki21/meta-llama-3-8b-gguf)

- [Notebook](https://www.kaggle.com/code/raki21/llama-3-gguf-with-llama-cpp) demonstrating its use, I'm in the process of adding a Q20 example, with persistence across the chat.

I recommend using the 8-bit quantized variant. Although I don't have the time to integrate it with the current agent setup, I hope this writeup helps some people get started! 

AI Note: I wrote the text myself, but ran it through GPT4o to format it into a nicer markdown structure and correct typos.



---

 # Comments from other users

> ## Melinda
> 
> Hi, and thanks for posting this notebook! I am trying to get llama-cpp-python working in my submission, and if I make a copy of your notebook, I'm able to run the pip install command in it. However, if I try to pip install it into a folder with the "-t /kaggle/working/submission/lib" option so that I can package it up, I get all kinds of dependency resolver errors. ("ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts. (etc - a huge list)")
> 
> I'm curious if you have any tips for how to get llama-cpp-python with llama-3-8b-instruct packaged for a submission? 
> 
> 
> 


---



</div>
<div class="column-right">

# 日本語訳

# LLMの概要とLlama 3の設定
**Raki** *2024年5月18日 21:29:56 (日本標準時)* (6票)
## Gemmaとその他のLLMの評価
### Gemmaの問題点
Gemma 7bの量子化版は、スタートノートブックで使用されているものですが、指示に従うのが苦手で、サイズに対して最先端のパフォーマンスを達成できていません。
### 推奨するLLM評価方法: LMSYS Arenaリーダーボード
強力な汎用LLMを特定するために、[LMSYS Arenaリーダーボード](https://chat.lmsys.org/)をお勧めします。このEloレーティングシステムは、ユーザーが質問を投げかけ、異なる2つのモデルからの回答を比較することで、どちらが好ましいかを判断します（ブラインド方式）。この評価方法は、さまざまなトピックにわたってユーザーの要求を一貫して満たすことに依存するため、「ゲーム化」するのが難しいです。他の指標は、ベンチマークがトレーニングセットに漏れる可能性があり、特定のパフォーマンスを最適化しやすい狭いタスクに焦点を当てることが多いです。
### 現在のトップモデル
- GPT-4: 1287 Elo
- Gemini 1.5 Pro（Google）: 1248 Elo
- 最良のAnthropicモデル: 1246 Elo
- LLaMA 3 70B Instruct（Meta）: 1203 Elo（最良のオープンソースモデルですが、大きすぎます）
### Gemmaのパフォーマンス（スタートと同様）
- Gemma 7B-IT: 1043 Elo
- 量子化版: わずかに劣ります（量子化はFP32などの形式からINT8に重みを減少させ、VRAMと計算要件を大幅に削減しますが、品質に対しては妥協が生じます）
### 代替案: LLaMA 3 8B Instruct
- LLaMA 3 8B Instruct: 1155 Elo（全体的にかなり強力なモデルです）
T4での実行に必要な量子化をまだ行う必要がありますが、T4には16 GiBのVRAMがあります。
### 推論を実行する最良の方法: llama.cpp
私が知る限り、非独自の量子化されたLLMで推論を行う最良の方法は、llama.cppです。このツールは、量子化やKVキャッシングなど、推論を高速化するためのさまざまな技術を採用しています。
### LLaMA 3 8B Instruct用のリソース
以前にいくつかの量子化されたLLaMA 3 8B Instructモデルのデータセットを設定しました：
- [データセット](https://www.kaggle.com/datasets/raki21/meta-llama-3-8b-gguf)
- [Notebook](https://www.kaggle.com/code/raki21/llama-3-gguf-with-llama-cpp) 使用法を示したものです。チャット全体で継続性を持つQ20の例を追加するプロセスにあります。
8ビット量子化バリアントの使用をお勧めします。現在のエージェント設定に統合する時間はありませんが、この書き込みが何らかの形でスタートする手助けになることを願っています！
AIノート: テキストは自分で書きましたが、より良いマークダウン構造に整形し、誤字を修正するためにGPT4oを通しました。
---
# 他のユーザーからのコメント
> ## Melinda
> 
> こんにちは、このノートブックを投稿してくれてありがとう！ 私は自分の提出物に対してllama-cpp-pythonを動作させようとしていますが、あなたのノートブックをコピーすると、pip installコマンドを実行できます。しかし、「-t /kaggle/working/submission/lib」オプションを指定してフォルダーにpip installを試みると、さまざまな依存関係解決エラーが発生します。 （「ERROR: pipの依存関係解決機能は、現在すべてのインストールパッケージを考慮に入れていません。この動作が原因で、次の依存関係の衝突が発生しています。（etc - 大量のリスト）」）
> 
> あなたはllama-cpp-pythonとllama-3-8b-instructを提出用にパッケージ化する方法について何かアドバイスがありますか？ 
> 
> ---


</div>