# ヘルプ！Kaggleでのファイルインポートで行き詰まりました

**Andres H. Zapke** *金 6月 7 2024 18:40:39 GMT+0900 (日本標準時)* (1 票)

チュートリアルに従って、ノートブックと以下のファイル構造を作成しました（画像参照）。このグラフィカルインターフェースは少し誤解を招く可能性がありますが、`main.py`は`submission`フォルダ内にあり、`lib`フォルダ内にはありません。

そのため、`game_output = env.run(agents=[simple_agent, simple_agent, simple_agent , "/kaggle/working/submission/main.py"])`を使ってKaggleノートブックからゲームを実行すると、今のところすべて正常に動作しています。

しかし、今`main.py`は`gemma`モジュールのいくつかのメソッドを必要としています。`sys.path.insert(0, "/kaggle/working/submission/lib")`、`sys.path.insert(0, "./lib")`、`from gemma.config import *`を使ってインポートしようとしましたが、常に`"No module named 'gemma.config'"`というエラーが発生します。

`gemma`に`__init__.py`ファイルがあることは確認済みですが、そのメソッドを`main`にインポートする方法がわかりません。何かヒントがあれば教えてください！

[Captura de pantalla 2024-06-07 a las 11.34.58.png](https://storage.googleapis.com/kaggle-forum-message-attachments/2859842/20789/Captura de pantalla 2024-06-07 a las 11.34.58.png)

> `gemma`モジュールを`main.py`からインポートするには、`main.py`と同じディレクトリに`gemma`モジュールがあることを確認する必要があります。`gemma`モジュールが`lib`フォルダ内にある場合、`main.py`から`gemma`モジュールをインポートするには、次のコードを使用できます。

```python
import sys
sys.path.append('/kaggle/working/submission/lib')
from gemma.config import *
```

> このコードは、`sys.path`に`lib`フォルダへのパスを追加します。これにより、`main.py`は`lib`フォルダ内のモジュールをインポートできるようになります。

> また、`gemma`モジュールが`__init__.py`ファイルを含むパッケージであることを確認してください。`__init__.py`ファイルは、`gemma`モジュールがパッケージであることをPythonに通知します。

> これらの手順を実行しても問題が解決しない場合は、`gemma`モジュールの構造と`main.py`からのインポート方法について、さらに詳しく説明してください。

