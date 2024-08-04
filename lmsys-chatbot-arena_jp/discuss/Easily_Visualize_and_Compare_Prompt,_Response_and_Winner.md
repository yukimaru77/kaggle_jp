# プロンプト、応答、勝者を簡単に視覚化して比較する

**Nazim Cherpanov** *2024年5月27日月曜日 18:42:02 GMT+0900 (日本標準時)* (2 votes)

## はじめに:

会話型AIのデータセットを扱う際には、さまざまなモデルによって生成された応答の質を把握することが重要です。この会話では、特定のプロンプトに対する応答と、最もパフォーマンスの高いモデルを簡単に視覚化して比較できる便利な関数を紹介します。

## 関数の概要:

関数 `get_info_by_id(index)` は、インデックスを入力として受け取り、対応するプロンプト、2つのモデル（モデルAとモデルB）からの応答、Kaggleデータセットからの勝者を取得します。そして、読みやすい形式で情報を表示します。

## コードスニペット:

```python
train_path = '/kaggle/input/lmsys-chatbot-arena/train.csv'
train = pd.read_csv(train_path, index_col='id').reset_index(drop=True)

def get_info_by_id(index):
    if index not in list(train.index):
        display("index not in train")
    else:
        print(f"\n{'*'*10} Prompt {'*'*10}\n")
        display(train.iloc[index]['prompt'])
        print(f"\n\n{'*'*10} response A {'*'*10}\n")
        display(train.iloc[index]['response_a'])
        print(f"\n\n{'*'*10} response B {'*'*10}\n")
        display(train.iloc[index]['response_b'])
        print(f"\n\n{'*'*10} Winner {'*'*10}\n")
        if train.iloc[index]['winner_model_a'] == 1:
            display('Model A')
        elif train.iloc[index]['winner_model_b'] == 1:
            display('Model B')
        else:
            display('Tie')

get_info_by_id(3)
```

## 使い方:

この関数を使用するには、`get_info_by_id()` を呼び出し、trainデータセットから目的のインデックスを渡します。例えば、`get_info_by_id(3)` は、インデックスが3の行のプロンプト、応答、勝者を表示します。

## Kaggleを楽しんで！

