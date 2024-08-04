# TF-IDF + Word2Vec = FTW [LB 1.026]
**Rich Olson** *木曜日 5月 9日 2024 15:54:49 GMT+0900 (日本標準時)* (4 votes)

TF-IDFとWord2Vecを組み合わせた新しいノートブックを公開しました。これにより、LB 1.026を達成しました。

[https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw-lb-1-026](https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw-lb-1-026)

これは、以前のTF-IDFのみのノートブック（LB 1.038）をベースにしています。

[https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees](https://www.kaggle.com/code/richolson/lmsys-tf-idf-boosted-trees)

以前と同様に、LGBMClassifierを使用して分析を行っています。

ノートブックの1つのバージョンでは、Word2Vecのみを使用しました。これだけでもLB 1.038（TF-IDFと同じ）を達成しました。

[https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw?scriptVersionId=176534641](https://www.kaggle.com/code/richolson/tf-idf-word2vec-ftw?scriptVersionId=176534641)

（これは実際にはより興味深い部分かもしれません。なぜなら、このコンペティションでWord2Vecを使用したノートブックを共有した人はいないと思います。）

TF-IDFとWord2VecはそれぞれLBで1.038を達成していますが、一緒に1.026を達成しています。これは、両者がそれぞれ独自の機能を生成していることを示唆しています。

他のノートブックでは、TF-IDFと他の単純な機能（テキストの長さなど）を組み合わせてスコアを向上させているのを見ました。Word2Vecを追加することで、さらにスコアを向上させることができるかもしれません。 

