# 生命科学DB構築におけるRDF化の実践

###### IIBMP 2017 BoF: SemWeb時代におけるバイオデータベースとデータ解析の融合

ライフサイエンス統合データベースセンター (DBCLS)
大田達郎 @inutano

![dbcls logo](images/dbcls.png)

---

## 話すこと

- 「データをRDF化する」とは、技術的に何をするのか

## 伝えたいこと

- 使いやすいデータを共有してみんなで科学をやっていきましょう
- RDFはそれを助ける1つの有力な選択肢だが、真に大事なのは作法

## 伝えたい人

- 測定/解析したデータを公開する人、DBを作る人
- 生物学的解釈が付与される余地のあるデータを出力するソフトウェアを作っている人

---

# 宣伝

第2回 RDF 講習会「RDFの作り方」
10/6 (金) @ JST 東京本部別館 (市ヶ谷)
"RDF講習会" で検索

---

# 問題: 公開されたデータを使うと捗らない

---

### 公開DBを使うときに何をしますか

- 理想
  - URL叩くと即、自分の欲しい形でデータが落ちてくる
- 現実
  - ウェブサイトを探す (が見つからないもしくは落ちている)
  - とりあえずダウンロード (サイトにそれ以外何もないので)
  - 謎の.tar.gzが落ちてくる (一晩かかる)
  - 雑に展開してみる (たまに開かない)
  - 何かが入っている (が何かよくわからない)
  - READMEを読んでデータ構造を調べる (が何も書いてない)
  - パーサーを書いて必要な部分を取り出す (何度も例外で落ちる)
  - データの意味を調べるのに再度ドキュメントを読む (つらい)

---

# つらい

別ドメインのデータをさらに結合するなんて考えたくもない

---

## データ作る方もつらい

- ユースケースは10^n人10^n色
- マニアックな使い方をされてこその研究資源
  - その全てを予測することはできない
  - 「自分でやれ」ラインの見極めの難しさ
- なるべく柔軟なインターフェース、柔軟な形式で用意したい
  - と、少なくとも思ってはいる

---

# 解決策: データ提供者が守るべきN個のお作法

---

# どうあってほしいのか

- ウェブサイトに情報を載せてくれ
- ドキュメント書いてくれ
- エントリIDを体系的に管理してくれ
- 関連リソースへのリンクを張ってくれ
- 変な略語使うのをやめろ
- 文字コードちゃんとしろ
- 特殊すぎる(圧縮|通信)プロトコルを使うな
- データ扱うのに特殊なソフトウェアを要求するな

**=> どうすればデータ提供者は従ってくれるのか？**

---

[![fair paper](images/fair_header.png)](https://www.nature.com/articles/sdata201618)

**FAIR principles** www.force11.org/group/fairgroup/fairprinciples

- be Findable
- be Accessible
- be Interoperable
- be Reusable

=> これらを突き詰めると Linked Data になる💡

---

**Linked Data**: is a method of publishing structured data built upon standard Web technologies such as HTTP, RDF and URIs to share information in a way that can be read automatically by computers, *from [Wikipedia](https://en.wikipedia.org/wiki/Linked_data)*

---

## Linked Data: お行儀の良いデータ養成ギプス

- URIを使え
- データはRDFで表現しろ
- URIにHTTPでアクセスされたらRDFも返せ

---

## RDF化の機運が高まる

- みんなやってるよ、怖くないよ :relieved:
  - NBDC/DBCLS/DDBJ/PDBj
  - SIB
  - EBI RDF
  - NCBI PubChem/MeSH
- でもRDF化って実際何をするの :confused:

![Dark Ritual from http://gatherer.wizards.com/Pages/Card/Details.aspx?multiverseid=19592 center](images/darkritual.jpg)

---

## パターンA: RDBに入った表形式のDBから作る

1. 行ごとにURIで一意なIDを付与する
2. 列のキーワードを標準的な語彙 (predicates) に置き換える
3. 機械的に変換する

便利: [D2RQ](http://d2rq.org) and [D2RQ Mapper](http://d2rq.dbcls.jp)

---

## パターンB: NoSQLに入ったドキュメント型DBから作る

1. エントリごとにURIで一意なIDを付与する
2. 適切なモデルを設計する
3. 必要な語彙を既存のオントロジーから選ぶ、なければ作る
4. コンバータ書いて変換する

---

# 実例: BioSamples w/ EBI-RDF @ BH17

- 配列データをDDBJに登録する際にサンプルの情報を書くアレ
  - DDBJ, EBI, NCBI で交換されている
  - 登録ユーザが独自に key-value を設定できる
- 元データはXML
- RDFモデルは[EBI BioSamples API](http://www.ebi.ac.uk/biosamples/help/api.html) JSONの構造を流用
  - key-value については適切な構造を設計した
- 語彙を決める
  - ないものについては新規に作る
- [コンバータ](https://github.com/LLTommy/REST_to_RDF)を書く
  - API -> JSON -> RDF Turtle

---

![biosmaples schema slide centre](images/biosamples_schema.png)

http://tinyurl.com/bh17final

---

# 実例: Quanto

Available at [inutano/sra-quanto](https://github.com/inutano/sra-quanto) and [RDF Portal](https://integbio.jp/rdf/?view=detail&id=quanto)

- エントリ単位は FASTQ ファイル単位
- 元データは [FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/) の出力とそこから計算した値
  - テーブルを内包するオブジェクト
- データモデルを作る
  - [bioruby-fastqc](https://github.com/inutano/bioruby-fastqc) で設計したオブジェクトの構造のままJSONに
- 必要な語彙を既存のオントロジーから選び、ないものは[作った](https://github.com/inutano/sos)
- [コンバータ](https://github.com/inutano/bioruby-fastqc/)を書く
  - JSONにcontextを追加してJSON-LDに
  - JSON-LDからrdf/turtleに自動変換
  - txt -> JSON -> JSON-LD -> RDF Turtle
  - [biogem](https://rubygems.org/gems/bio-fastqc) になっています

---

**元データ** はただのテキストファイルなのでこれをパースしてJSONオブジェクトに変換し、contextを付与して JSON-LD にする

![FastQC raw data](images/fastqc_raw_data.png)

---

**RDFモデル** made with draw.io

![Quanto schema](images/quanto_schema.png)

---

**Quanto in RDF Portal** bulk RDF data download, SPARQL endpoint

![Quanto in RDF portal screen shot](images/quanto_ss.png)

---

# ね、簡単でしょ？

- 全然簡単じゃない
  - 特に語彙を探す/選ぶ/作るところがつらい
  - [BioPortal](http://bioportal.bioontology.org), [EBI OLS](http://www.ebi.ac.uk/ols/index) 等があるが、結局人に聞いている
- 独りでは難しい
  - グループで取り掛かることでかなりコストを下げられる
  - [BioHackathon](http://www.biohackathon.org), [SPARQLthon](http://wiki.lifesciencedb.jp/mw/index.php/SPARQLthon), etc..
- いずれにせよ筋力の問題なのでやっていくしかない

---

# RDFにすることで全ての問題が解決したか

- ウェブサイトに情報を載せてくれ: *筋力*
- ドキュメント書いてくれ: *筋力*
- エントリIDを体系的に管理してくれ: *URIを使う*
- 関連リソースへのリンクを張ってくれ: *RDFでリンクを張る*
- 変な略語使うのをやめろ: *適切な語彙を使う*
- 文字コードちゃんとしろ: *UTF-8 or フォーマットの指定に従う*
- 特殊すぎる(圧縮|通信)プロトコルを使うな: *HTTP GET*
- **!!! データ扱うのに特殊なソフトウェアを要求するな !!!**

*No Silver Bullet: RDFにすれば何もかも解決するとは誰も言ってない*

---

## 特殊なソフトウェアを要求するな

- TripleStore, SPARQL は特殊か否か 🤔
  - 依然扱える人は少ない
- 派閥
  - W3C標準なんだからSPARQL使おうよ派
  - いいからJSON返せ、あとはこっちでなんとかするから派
  - Neo4Jではあかんのか派

---

### コストが十分下げられるなら提供する選択肢は増やすべき

- 元データ -> JSON -> JSON-LD -> RDF の流れは比較的容易
- JSON-LD は @context を無視すればただの JSON
- エンドポイント
  - SPARQL
  - RESTful API
    - smart API that returns JSON-LD
    - Elasticsearch
- バルクダウンロード

作法に則ったデータとこれらが揃えば別ドメインのデータと繋ぐことも難しくない（はず）

---

### 繋がったその先: グラフ解析手法にそのまま入力できるのか

- Heterogenous Network: ノード、エッジにバリエーションがある
  - 異なるDB間で同じ概念を表すために別の ontology term が使われている場合がある
  - => 別DBのRDFデータを混ぜたグラフを作る際に、語の使われ方の違いが解析の精度に影響を及ぼすのでは？
- RDF化されたデータベースはあらゆるものが繋がっている
  - 不要なメタデータ (登録の日付, データ登録者の所属, 文献ID, etc.) なども
  - => 解析に必要なサブグラフをいかに簡単に取り出すか？
- そのデータはグラフ化に向いているか
  - bigBedをRDFにすることは技術的には可能だが…

---

# まとめ

- 作法に則ってデータを作りましょう
  - コミュニティに参加して協調すると捗る
  - データ元がやってくれないなら自分でやる
- RDF化とはすなわち「ちゃんとする」こと
  - あなたとFAIR、今すぐ実装
- RDFとJSON-LD, 目的に合ったものを使えるように
- データ解析にとっては異なる種類の前処理が必要になる可能性

