# 要約 
## LLM 20 QuestionsコンペティションにおけるLLM選択とセットアップに関するディスカッション要約

このディスカッションは、LLM 20 QuestionsコンペティションにおけるLLMの選択とセットアップに関するものです。投稿者は、初期のノートブックで使用されているGemma 7b it quantモデルが指示に従うことに苦労し、そのサイズに対して最先端のパフォーマンスを達成していないことを指摘しています。

代わりに、投稿者はLMSYS Arena Leaderboardを用いてLLMを評価することを推奨しています。このリーダーボードは、Eloレーティングシステムを用いて、さまざまなトピックにわたるユーザーのクエリに対するLLMのパフォーマンスを評価します。

投稿者は、GPT-4、Gemini 1.5 Pro、Anthropicの最良モデル、LLaMA 3 70B InstructがLMSYS Arena Leaderboardで上位にランクインしていることを示しています。Gemma 7b-ITと量子化バージョンは、これらのモデルよりもパフォーマンスが劣っています。

投稿者は、LLaMA 3 8B Instructが、サイズとパフォーマンスのバランスが取れた優れた選択肢であると提案しています。このモデルは、コンペティションで使用できるT4 GPUのVRAM容量に適しており、llama.cppを用いて量子化して実行することができます。

投稿者は、量子化されたLLaMA 3 8B Instructモデルを含むデータセットと、その使用方法を示すノートブックを提供しています。

コメント欄では、別のユーザーが、llama-cpp-pythonとllama-3-8b-instructを提出物用にパッケージ化する際に依存関係解決エラーが発生していることを報告しています。投稿者は、この問題に対する具体的な解決策を提供していませんが、この問題に対するヒントを求めています。

**要約:**

* Gemma 7b it quantモデルは、コンペティションに適していない。
* LMSYS Arena Leaderboardを用いてLLMを評価することを推奨。
* LLaMA 3 8B Instructが、サイズとパフォーマンスのバランスが取れた優れた選択肢。
* llama.cppを用いて量子化して実行可能。
* 提出物用にパッケージ化する際に依存関係解決エラーが発生する可能性がある。

**結論:**

このディスカッションは、LLM 20 Questionsコンペティションに参加する際に、LLMの選択とセットアップについて重要な情報を提供しています。特に、LMSYS Arena Leaderboardを用いたLLM評価と、LLaMA 3 8B Instructモデルの使用は、コンペティション参加者にとって有益な情報です。


---
# LLMの概要とLlama 3のセットアップ

**Raki** *2024年5月18日土曜日 21:29:56 GMT+0900 (日本標準時)* (6票)

## Gemmaと他のLLMの評価
### Gemmaの問題点
Gemma 7b it quantは、初期のノートブックで使用されているモデルですが、指示に従うことに苦労し、そのサイズに対して最先端のパフォーマンスを達成していません。
### 推奨されるLLM評価: LMSYS Arena Leaderboard
堅牢な汎用LLMを特定するために、[LMSYS Arena Leaderboard](https://chat.lmsys.org/) をお勧めします。このEloレーティングシステムでは、ユーザーが質問を行い、2つの異なるモデル（ブラインド）からの回答を比較して、どちらの回答を好むかを判断します。この評価方法は、さまざまなトピックにわたってユーザーのクエリを常に満たすことが成功の鍵となるため、「ゲーム」をするのが難しいです。他の指標は、トレーニングセットへのベンチマークリークの影響を受けやすく、多くの場合、より狭いタスクに焦点を当てているため、汎用性よりも特定のパフォーマンスを最適化しやすくなります。
### 現在のトップモデル
- GPT-4: 1287 Elo
- Gemini 1.5 Pro (Google): 1248 Elo
- Anthropicの最良モデル: 1246 Elo
- LLaMA 3 70B Instruct (Meta): 1203 Elo（最良のオープンソースモデルですが、大きすぎる）
### Gemmaのパフォーマンス（スターターのような）
- Gemma 7B-IT: 1043 Elo
- 量子化バージョン: わずかに悪い（量子化は、FP32などの形式からINT8に重みを減らし、VRAMと計算要件を大幅に削減しますが、品質が低下します）
### 代替案: LLaMA 3 8B Instruct
- LLaMA 3 8B Instruct: 1155 Elo（全体としてはるかに強力なモデル）
提出のために使用できるT4には16 GiBのVRAMがあるため、量子化して実行する必要があります。
### 推論を実行する最良の方法: llama.cpp
私の知る限り、非独自量子化LLMで推論を実行する最良の方法は、llama.cppです。このツールは、量子化やKVキャッシングなどのさまざまなテクニックを使用して、推論を高速化します。
### LLaMA 3 8B Instructのリソース
以前、量子化されたLLaMA 3 8B Instructモデルを含むデータセットをセットアップしました。
- [データセット](https://www.kaggle.com/datasets/raki21/meta-llama-3-8b-gguf)
- [ノートブック](https://www.kaggle.com/code/raki21/llama-3-gguf-with-llama-cpp) は、その使用方法を示しています。チャット全体で永続性を備えたQ20の例を追加しています。
8ビット量子化バリアントを使用することをお勧めします。現在のエージェント設定に統合する時間はありませんが、この書き込みが誰かのスタートに役立つことを願っています！
AI注記: テキストは自分で書きましたが、GPT4oで実行して、より良いマークダウン構造にフォーマットし、タイプミスを修正しました。
---
# 他のユーザーからのコメント
> ## Melinda
> 
> このノートブックを投稿してくれてありがとう！ 私は自分の提出物でllama-cpp-pythonを動作させようとしていますが、あなたのノートブックのコピーを作成すると、その中でpip installコマンドを実行できます。 しかし、"-t /kaggle/working/submission/lib"オプションを使用して、パッケージ化できるようにフォルダにpip installしようとすると、依存関係解決エラーが大量に発生します。 ("ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts. (etc - a huge list)")
> 
> 提出物用にllama-cpp-pythonとllama-3-8b-instructをパッケージ化する方法について、何かヒントがあれば教えてください。
> 
> 
> 
---

