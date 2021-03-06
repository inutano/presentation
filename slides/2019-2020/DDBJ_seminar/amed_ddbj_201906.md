---
marp: true
---

# DDBJ Workflow Execution Service 

June 2019
大田達郎
ライフサイエンス統合データベースセンター

---

# 背景

- DDBJ では生命科学研究者向けのスパコンを提供しています
  - 2019年3月にハードウェアをアップグレード
  - ヒト個人データを解析するために必要なセキュリティ要件を満たす閉鎖環境の提供を開始
- 従来のスパコンの問題を解決できるプラットフォームに向けて
  - 従来のスパコンを使った解析で起こる問題
  - ヒトデータをスパコンで扱う際に起こる問題

---

# 問題

### 従来のスパコンを使った解析で起こる問題

- 手元で動いているワークフローがスパコンで動かない
- Nヶ月前に動いていたワークフローが動かない
- 担当者が異動しワークフローが何故動いているかわからない

### ヒトデータをスパコンで扱う際に起こる問題

- 他グループの解析済みデータと比較してもよいか？
  - 他のグループのワークフローとの整合性の検証が難しい
- 解析担当者が間違ってデータを外に出してしまわないか？

---

# 解決策 (1)


### ワークフローの可搬性の問題: コンテナ仮想化
  - バージョン管理と配布を容易に
  - ソフトウェアの実行環境が固定されることで反復が容易に
### ワークフローの記述と可読性の問題: ワークフロー言語
  - 実行時引数の指定やソフトウェアの組み合わせの指定が容易に
  - Common Workflow Language (CWL) を採用

---

# 解決策 (2)

### 他グループデータとの比較の問題: 標準ワークフローの策定
  - TMM, 理研などによる 10k 日本人ゲノムのワークフローをCWL化
### データ流出の問題: 閉鎖環境で動作するワークフロー実行システム
  - ユーザが指定したワークフローが、指定したデータを入力に、個人ゲノム解析環境で動いて、結果だけを返す

---

# DDBJ Workflow Execution Service (WES)

- DDBJスパコンでの提供に向けて現在テスト中
　　- code: Sapporo
- オープンソース (MITライセンス)
- 既存のフレームワークを活用
  - Docker, Singularity
  - Common Workflow Language (CWL)
  - GA4GH workflow execution service API standard

---

![bg 50%](images/sapporo_components.png)

---

![bg 60%](images/sapporo-server.png)

---

![bg 60%](images/sapporo-wf.png)

---

![bg 60%](images/sapporo-wf-run.png)

---

# 特徴/他システムとの差別化

- 「ワークフロー遠隔実行システム」は多数存在する
  - Galaxy, nextflow, etc.
- ユーザはワークフローを実行にあたって直接データを操作できない
  - 入力: データの場所 (URL) とそれを解析するワークフロー
  - 出力: 解析結果の場所 (URL)
- Adminが指定したワークフローのみ実行可能
  - ユーザが任意のワークフローを実行できるわけではない
  - 個人ゲノムデータの流出や意図しないソフトウェアの実行を防ぐ
- 既存OSSフレームワークの利用
  - コミュニティの資産 (公開されたワークフロー) が利用可

---

# 今後

- システムの運用
  - 諸事情あり公開日は未定
  - 閉鎖環境だけでなく公開領域でヒト以外のデータも
  - 他拠点の計算機にもワークフローを実行できるように
    - TMM など。調整中
- 利用可能ワークフローの拡大
  - 各国機関で公開されているCWLの検証と導入
- 可搬性、再現性のさらなる向上
  - データ、ワークフロー管理における継続的インテグレーション (CI) の導入
  - ワークフロー評価・検証コスト削減のためのシステム
    - CWL-metrics の導入