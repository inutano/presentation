![center](images/tw1.png)

---

# こんにちは BioSample

---

# こんにちは


- 大田達郎, DBCLS
- BioSample が飯の種

---

![center](images/tw2.png)

---

# BioSample の検索を作った

- DDBJ Search https://sra.dbcls.jp (ベータ版)
- 元の構造を無視して検索に特化した構造の JSON を ElasticSearch に入れている
- 爆速な全文検索を実現(できる予定)

---

# 人は BioSample で何がしたいのか

- 研究に使ったサンプルの情報を記録したい
- 公開データのサンプル情報を取得したい
- サンプル情報を手がかりに公開された計測データを取得したい
  - 類似したサンプルのデータが欲しい
  - 関連するサンプルのデータが欲しい
- 計測データとメタデータを組み合わせて解析したい
  - グラフ解析, ML

---

# 本当なのか

---

# 人は BioSample で本当は何がしたいのか

- 何もしたくない
- BioSampleのことなんか考えたくない
- さっさとデータを登録して論文サブミットして実験のことを忘れて飲みに行きたい

---

![center](images/tw3.png)

---

# どうすれば

- 何もしたくない人には何もしないでもらいたい
- 「何もしない」をしてもらいたい

---

# 何もしないをするを阻む問題

- 記述コストの問題
- BioSample DB設計の問題
- BioSample DB運用の問題

---

![center](images/tw5.png)

---

# 記述コストの問題

- 人間は怠惰なので情報を記述しない
  - 必須のフィールドを埋めて終わり
    - 必須をNAで逃げる輩の存在が明らかになり人間への怒りが増した
  - 「ないがある」なのか「ない」のか
    - "not applicable" なのか単に書いてないのかは他者にはわからない
  - 「本当にNAなのか」「面倒で書いてないだけでは」「BioSampleのせいで人間不信に」
- 勝手に書いてほしい
  - 計測データから推測する
  - 実験室でセンサーで読んで自動的に記述する
  - 実験ごと外注する

---

# BioSample DB設計の問題

- DBの要件が「サンプル情報のDB」とふわっとしすぎ
  - 結果「なんでも入れられる箱」でありただのkv storeになってしまった
  - Packageでカバーしようとしているが未だ十分ではない
- 設計を変えるのは現実的ではない
  - 既に規模がでかすぎる
  - 3極での折衝が必要
- 適切な Package を登録者に強制する運用上の仕組みが必要

---

# BioSample DB運用の問題

- QC のコストが高い
  - Sample validator は素晴らしい
  - しかし書かれないことに対しては無力
- データ登録者に対して要求がしづらい
  - これも構造上の問題
  - レポジトリにジャーナルと同等かそれ以上の権力が必要
- マンパワーが全然足りていない
  - 金がほしい
  - 間接経費みたいに獲得科研費のXX%を召し上げたい
  - BioSampleが科研費配るようになりたい

---

# 問題は結局のところなんなのか

- 記述コストの問題
  - 人間の知性
- BioSample DB設計の問題
  - 手遅れ
- BioSample DB運用の問題
  - 政治

---

![center](images/tw4.png)

---

# 人間と向き合う

- 記述コストをなんとかする
- 最終的には「なんか知らんが勝手に正しいサンプル情報が書かれていた」を目指す

---

# NCBI CEDAR OnDemand

- これすごくないですか？
- Chrome Extension
  - 55 users
  - https://chrome.google.com/webstore/detail/cedar-ondemand/bbllhpbnjiddckppfdheoignbnmngmfm?hl=en
- GitHub repo
  - 1Star 
    - 今僕がstarしたから
  - https://github.com/ahmadchan/CEDAROnDemand
- もっと頑張れよ…！
- 目指すのはこれのもっと凄い版

---

# オントロジーマッピングしなければならない

- DBCLS では色々のデータリソースを RDF/Linked Data 化している
  - URIの付与
  - オントロジーの付与
  - 適切なモデルの設計
  - フォーマット変換
- BioSample は様々なリソースを繋ぐ重要なDBなのでやっていきましょう
  - **BioSample+構想**
  - EBI Cleaninghouse と基本的には同じ

---

# 方針

- 既存のプロジェクトと協働
  - 沖さんの ChIP-Atlas
  - 森さんたちの microbedb.jp
- ドメインやAttributeを限定しない
  - たとえば Env とか Cell line とかに限定するとやりようはあるが横にスケールしない
- 極力自動化する
  - BioSampleエントリは数が多い
  - 全てのエントリと向き合っていると人生が破滅する
- カバレッジより精度を優先する
  - 同じく人生が破滅するのでコーナーケースは無視する
  - 「精度は微妙だが全てのエントリをカバー」より「ついてるものは正しいがついてないものも多い」が理想
- 正気を保つ

---

![center](images/tw6.png)


---

![70% center](images/bsplus.png)

<!-- *footer: credit: DBCLS池田さん -->

---

# 手順

- BioSample から attribuetes を取得
- EBI Zooma API に全部当てる
- 返ってきた suggested ontology terms を選別し明らかに間違っているものを自動的に落とす
- 人間が目で見てチェックして間違っているものを全部削除する
  - 機械的に作業できるよう工夫する
  - そのための専用appを作ってもいいのではと考えている

---

# EBI SPOT Zooma がすごい

![center](images/cellline_zooma.png)

<!-- *footer: credit: DBCLS池田さん -->

---

# ここがすごいぜ Zooma

- https://www.ebi.ac.uk/spot/zooma/
- タームを投げるとオントロジーをマップしてくれる
- APIもある
- 「どれくらい自信を持ってマップしたか」を教えてくれる
  - High: 既存のマニュアルキュレーションによってマップされた記録がある
  - Good: 既存のマニュアルキュレーションによってマップされた記録があるが複数の候補がある
  - Medium: マニュアルキュレーションのログがなく文字列比較のみで推薦された
- キュレーション結果をZoomaに送ると検索結果に反映してくれる


---

# まとめ

- BioSampleは永遠に終わらない撤退戦
- Zooma saves the Queen