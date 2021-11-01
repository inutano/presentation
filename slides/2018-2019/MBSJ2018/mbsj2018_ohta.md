# 公共データベースに登録されたNGSデータを検索・活用する

大田達郎, 仲里猛留, 坊農秀雅
ライフサイエンス統合データベースセンター (DBCLS)

[]()
[]()

2018/11/29 MBSJ2018 ワークショップ
「いかにして公共データベースを生命科学研究に活用するか？」

![DBCLS logo](images/dbcls.png) 

---

# 来場者アンケート :bowing_man:

- NGS使ってますか
  - DDBJにNGSデータを登録したことがありますか
- データの解析を自分でやりますか、人に任せますか
- 公共のNGSデータを
  - 検索したことがありますか
  - 使って解析したことがありますか
    - それで論文書けましたか

---

# まとめ

- DDBJ/DBCLS で公共NGSデータ検索エンジンを作っています
  - https://sra.dbcls.jp
  - 2019年度DDBJにて正式稼働予定
  - 是非フィードバックを
- 解析済み公共NGSデータを提供するDBをどんどん活用しましょう

---

# Agenda

- Sequence Read Archive (SRA) について
- SRAデータ検索の問題点
- DDBJ Search の実装
- SRAデータを用いたアプリケーションの紹介
- まとめ

---

# Sequence Read Archive (SRA) について

何がどれくらい入っているのか

---

# Sequence Read Archive (SRA) について

- いわゆる NGS データを収載する公共データレポジトリ
- INSDC が運用
  - INSDC: International Nucleotide Sequence Database Collaboration
  - 米国NCBI + 欧州EBI + 日本DDBJ
- 研究者が登録するもの
  - 配列データ (FASTQ, BAM, etc.)
  - 実験やサンプルについての記述 (メタデータ)

![INSDC center 45%](images/insdc.gif)

---

# SRAのデータ量と伸び

20PB!

![SRA growth center 90%](images/sragrowth.png)

https://www.ncbi.nlm.nih.gov/sra/docs/sragrowth/

---

# Open access bytes per quarter

![open access bytes per quarter center](images/open_access_bytes_per_quarter.png)

---

# Controlled access bytes per quarter

![controlled access bytes per quarter center](images/controlled_access_bytes_per_quarter.png)

---

# Statistics: Library source

![source center](images/submission_by_source.png)

---

# Statistics: Library strategy (application)

![app center](images/submission_by_application.png)

---

# Statitsitcs: Platform

![platform center](images/submission_by_platform.png)

---

# Statistics: Organisms (Top50)

![top50 center](images/submission_by_organisms_1-50.png)

---

# Statistics: Organisms (51-100)

![51-100 center](images/submission_by_organisms_51-100.png)

---


# SRAデータ検索の問題点

こんなにあるのに何故欲しいデータが見つからないのか

---

# SRAデータ検索の問題点

たくさんあるが…

1. メタデータオブジェクトの関係性が複雑である
2. メタデータに記載された情報が検索に不十分である
3. 検索の仕方が悪いのか、そもそもアーカイブにないのか？

---

# メタデータオブジェクトの関係性

![40% center](images/sra_object.png)

- 個別の情報のアップデートや削除に対応するために情報の単位ごとに分割されIDが振られる
- 知らないと検索するときに混乱する

---

# メタデータに含まれる情報の不足

![omg-seq](images/omg-seq.biosample.png)

- [お花見メタゲノムプロジェクト](http://www.ngs-sakura.jp) で取られたメタデータ
  - plant-associate metagenome の package に従っている
- 登録者が記載する情報と検索者が記載してほしい情報は一致しない

---

# 検索の仕方が悪いのか、そもそもアーカイブにないのか

- なんでも入っているわけではない
  - 世界のどこかでシーケンスされ、登録されたものだけ
- メタ情報が適切に書かれていない = 存在しないのと同じ
- 対策
  - 論文を探す
  - 統計情報を活用する
  - 効率よく検索するプログラムを書く

---

# DDBJ Search の実装

---

# DDBJ Search の実装

- メタデータの全文検索インデックス構築
- プログラムからアクセス可能なAPIサーバの構築
- Graphical User Interface (WebUI) の構築
- 停電知らずのクラウド環境

---

# システム構成

![center](images/ddbj-search-data-source.png)

---

# DDBJ Search

twitterでのフィードバックお待ちしてます https://sra.dbcls.jp

![center](images/ddbj-search-01.png)

---

# SRAデータを用いたアプリケーションの紹介

その公共データ、既に誰かが解析している (かも)

---

# SRAデータを用いたアプリケーションの紹介


|Name        |Org         |SeqApp                                  |Organisms|
|------------|------------|----------------------------------------|--------|
|Quanto      |DBCLS       |FastQC                                  |All|
|RefEx       |DBCLS       |RNA-Seq                                 |Human, Mouse, Rat|
|ARCHS4      |Mount Sinai |RNA-Seq                                 |Human, Mouse                    |
|ChIP-Atlas  |Kyushu-Univ.|ChIP-Seq, DNase-Seq                     |Human, Mouse, Rat, Fluit fly, Roundworm, Yeast|
|MicrobeDB.jp|NIG         |Metagenome, Meta-16S, Meta-transcriptome||

---

# Quanto

![Qunato ss 40% center](images/quanto.png)

- SRAデータのクオリティ統計値
- 詳しくは BioDB2 (統合DB DBCLS) のブースへ
- http://data.dbcls.jp/~inutano/fastqc/
- https://doi.org/10.1093/gigascience/gix029


---

# RefEx

![RefEx ss 40% center](images/refex.png)

- 公共遺伝子発現データから作られた "reference transcriptome"
- 詳しくは BioDB2 (統合DB DBCLS) のブースへ
- http://refex.dbcls.jp

---

# ARCHS4

![ARCHS4 ss 40% center](images/archs4.png)

- kallisto による human/mouse RNA-Seq の発現定量
- 結果は全てDL可能
- https://amp.pharm.mssm.edu/archs4/
- https://doi.org/10.1038/s41467-018-03751-6

---

# ChIP-Atlas

![ChIP-Atlas ss 40% center](images/chipatlas.png)

- SRAのChIP-Seq/DNase-Seqを解析、Enrichment analysis も
- 詳しくは BioDB9 (統合DB九州大学) のブースへ
- https://chip-atlas.org
- https://doi.org/10.15252/embr.201846255

---

# Microbedb.jp

![MicrobeDB.jp ss 40% center](images/microbedbjp.png)

- SRAのメタゲノム・メタ16S・メタトランスクリプトームが解析済み
- 詳しくは BioDB7 (統合DB 微生物統合 遺伝研他) のブースへ
- http://microbedb.jp/

---

# まとめ

- DDBJ/DBCLS で公共NGSデータ検索エンジンを作っています
  - https://sra.dbcls.jp
  - 2019年度DDBJにて正式稼働予定
  - 是非フィードバックを
- 解析済み公共NGSデータを提供するDBをどんどん活用しましょう


---

# おまけ：NCBI, EBI, DDBJ の検索サービス

どうやって探すか

---

# NCBI でSRAデータを検索する

http://ncbi.nlm.nih.gov/sra

![NCBI SRA top page 100% center](images/ncbi_sra1.png)

---

# NCBI でSRAデータを検索する

SRA Advanced Search Builder

![NCBI SRA advanced search center](images/ncbi_sra2.png)

---

# EBI でSRAデータを検索する

https://www.ebi.ac.uk/ena

![EBI ENA top page center](images/ebi_ena1.png)

---

# EBI でSRAデータを検索する

Advanced Search

![EBI ENA advanced search center](images/ebi_ena2.png)

---

# EBI でSRAデータを検索する

インクリメンタルサーチも可能

![EBI ENA incremental search center](images/ebi_ena3.png)

---

# DDBJ でSRAデータを検索する

http://ddbj.nig.ac.jp/DRASearch/

![DDBJ DRA search center](images/ddbj_dra1.png)

---

# DDBJ でSRAデータを検索する

インクリメンタルサーチ

![DDBJ DRA incremental search center](images/ddbj_dra2.png)

---

# DDBJ でSRAデータを検索する


![DDBJ DRA search project list center](images/ddbj_dra3.png)

