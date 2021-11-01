# DBCLSでのコンテナ・クラウド活用紹介

ライフサイエンス統合データベースセンター (DBCLS)
大田達郎 @inutano

![dbcls logo](images/dbcls.png)

---

## 誰

- ゲノムデータの共有促進のための技術開発をしています
- twitter.com/iNut
- github.com/inutano
- speakerdeck.com/inutano

## 所属

- ライフサイエンス統合データベースセンター (DBCLS)
  - 生命科学研究に資する研究開発
  - データリソース、インフラ

---

## 話すこと

- 話題提供
  - 科学研究の現場におけるインフラについて
  - 広く浅く

## キーワード

- オンプレ (and|or) クラウド
- HPCをクラウドで拡張する
- コンテナによるアプリケーションの可搬性と再現性の向上

---

## Topics

1. **WebApp hosting**: オンプレとクラウドの間
2. **HPC x Cloud**: 前処理から可視化まで
3. **HPC x Container**: セキュリティの問題と環境選択

---

# WebApp hosting

---

## WebApp hosting on DBCLS

- [約30ほどのウェブアプリケーション](http://dbcls.rois.ac.jp/services)
  - 従来は全て自前のウェブサーバで
- 計算機の管理コスト削減、停電対策のため商用クラウド利用を開始
- 課題
  - コスト
    - 長期に維持するならオンプレの方が安い場合も
    - 特にストレージと転送料金が高い
  - セキュリティ
  - クラウド扱える人材
  - ベンダーロックイン
- 何をクラウドで、何をオンプレでホストするか？

---

## 事例: ChIP-Atlas

- 世界中から集まる公開済み実験データを統一基準で再解析
  - http://chip-atlas.org
- 再解析したデータを使ったデータ分析ツールを提供
  - ユーザデータとの比較
  - 関連するデータの検索
- データサイズが巨大
  - FTPサーバのファイル合計20TB程度
  - 毎月更新
    - 現在70,000件ほどの実験データを公開
  - [NBDC](https://biosciencedbc.jp)の[DBアーカイブ](https://dbarchive.biosciencedbc.jp/index.html)を利用
    - 研究データ公開用アーカイブサービス

---

## 事例: ChIP-Atlas

![chip-atlas-architecture center](images/chipatlas.png)

- 毎月更新の処理とオンデマンド解析 in silico ChIP を NIG SC で
- bedデータ (20TB) は NBDC DB Archive から配信


---

# HPC x Cloud

---

## HPC x Cloud

- [遺伝学研究所スーパーコンピューターシステム](https://sc.ddbj.nig.ac.jp)
- スパコン？
  - でかいクラスタマシン
  - 分散ジョブ実行システム (Univa Grid Engine)
  - 大型共有ストレージ (lustre) と 共有メモリ (max 10TB)
- 商用クラウドと接続
  - 混雑時に分散できる
  - ウェブサーバが建てられる
    - ゲノムブラウザ
    - Jupyter notebook
  - クラウドの料金はユーザが負担 (請求書払いが可能)
  - 興味のあるユーザの方は問い合わせを

---

## NIG SC to Cloud

![nig2cloud center](images/nig2cloud.png)

1. ユーザが reseller に登録すると IAM ユーザが作成される
2. ユーザはNIGスパコンにログインしスクリプトを実行
3. データのコピーとEC2へのログインが実行される

---

# HPC x Container

---

## Which container?

- 遺伝研スパコンテスト環境でdockerを試験
  - OSやドライバの問題があり本番環境には反映していない
- docker/udocker/shifter/singularity?
- 最終的な結論は出ていない
  - 事例の少なさ
  - OSやドライバの制約
  - セキュリティ

---

## Container metrics

- コンテナによる可搬性の向上により環境の選択肢が増える
  - アプリケーションごとに必要なスペックを知る必要がある
- github.com/inutano/docker-metrics-collector
  - Telegraf/Fluentd/Elasticsearch+Kibana
  - `git clone && docker-compose up`
  - [Common Workflow Language](http://www.commonwl.org) との接続を実装中

---

## Container metrics

![containermetrics center](images/containermetrics.png)

1. Telegraf が同一ホスト上のコンテナによるリソース消費を記録
2. fluentd が elasticsearch にログを貯める
3. CWL のワークフローメタデータをelasticsearchにロード
4. kibanaで可視化、elasticsearchでメタデータの全文検索が可能

---

# 科学研究のためのインフラは何であるべきか

---

## アカデミアにおけるインフラ開発整備のモチベーション

- 世の研究者は時間がない
  - 計算機をメンテする時間がない
    - それクラウドで…
  - ソフトウェアを都度インストールするのが面倒
    - それコンテナで…
- 新しい技術は導入のハードルが高い
  - 研究者はインフラのことを1秒も考えずに研究したい
  - 「気がついたら使っていた」がベスト
    - 研究者に時間を作ることの価値は計り知れない

---

## Monthly Meetup の勧め

- 研究者の数に対してインフラを(やりたい|やれる|やる)人は少ない
  - 結託すべし
  - 既に誰かが悩んだことで悩んではいけない
- 月に一度、組織の垣根を超えて共同作業する日があるとよい
  - [SPARQLthon](http://wiki.lifesciencedb.jp/mw/SPARQLthon)
  - [Galaxy meetup](http://wiki.pitagora-galaxy.org/wiki/index.php/Events)
  - [Workflow meetup](https://github.com/manabuishii/workflow-meetup/wiki)
- 研究は競争かもしれないが、インフラはオープンに

---

## まとめ

- オンプレとクラウドの使い分け、その見極めが重要
- HPCとクラウドの接続をユーザに意識させない
- HPCにおけるコンテナ利用の事例を積み上げて普及を
- 開発者同士の情報交換の場をつくる