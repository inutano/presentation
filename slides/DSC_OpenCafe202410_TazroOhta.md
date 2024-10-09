---
title       : データサイエンス教育・研究の効率をX倍にするにはどうすればよいか
author      : Tazro Ohta
description : 第2回 千葉大学データサイエンスコア オープンカフェ
keywords    : data science, education, research
marp        : true
paginate    : true
footer      : dsc.chiba-u.jp
---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
img[alt~="right"] {
  display: block;
  margin-top: auto;
  margin-bottom: auto;
  margin-right: 0;
  margin-left: auto;
}
</style>

<!-- _paginate: false -->

<!-- 
_footer: "2024/10/09 @ 千葉大学西千葉キャンパス BiZCAFE"
-->
<style scoped>
footer {
  color: black;
}
</style>


# データサイエンス教育・研究の効率をX倍にするにはどうすればよいか

#### 第2回 千葉大学データサイエンスコア オープンカフェ

大田達郎
千葉大学 国際高等研究基幹 / 大学院医学研究院
千葉大学データサイエンスコア 副ダイレクター

![right w:700](images/dsc-logo-w-uni.png)

---

# 自己紹介

- 1986 福岡県福岡市生まれ
- 2009 神戸大学農学部卒
- 2011 東京大学大学院農学生命科学研究科修了
- 2011-2023 ライフサイエンス統合データベースセンター
  - 2019 総研大にて論文博士取得
- 2023- 千葉大学 国際高等研究基幹 / 医学研究院 人工知能医学 所属
  - 2024/7- 千葉大学データサイエンスコア 副ダイレクター
- 専門: バイオインフォマティクス
  - バイオデータベース構築, ゲノムデータ解析システム開発

![bg fit right:17%](images/logo.extent.png)

<!-- _footer: "https://github.com/inutano/cv" -->

---

データベース統合

---

![](images/togo2024-bg-top.png)



<!-- _footer: https://biosciencedbc.jp/event/symposium/togo2024/ -->

---

> パネルディスカッション「生命科学の未来を予想する――データベースはもう要らなくなる...ってコト?!」

<!-- _footer: https://biosciencedbc.jp/event/symposium/togo2024/ -->

---

# AIがあればデータベースはもういらない？

![center w:500](images/irukamo.png)

<!-- _footer: データむしり検定5級 -->

---

# 心配事の多い時代

- AIによって研究者はお払い箱になるのか？
- 自我を持つAIの出現、シンギュラリティの可能性は？

---

# What if

つよつよAI「私が研究しますからあなたは研究費の申請書を書き続けてください」

---

# 現実

- まだそうはなってない
- 早く無駄で退屈な仕事を奪ってほしい

![bg right:45% fit](images/machine_learning_2x.png)

<!-- _footer: https://xkcd.com/1838/ -->

---

AIに奪われるのを待っていられない、奪ってもらえないならこちらから仕事を手放してやる

---

「データサイエンス教育・研究の効率をX倍にするにはどうすればよいか」

---

![bg fit](images/leafret.png)

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# データサイエンス教育・研究の効率をX倍にするにはどうすればいいかみんなで考えよう会議

---

# なんでこんな話をするのか

- DSCができたおかげで私の `(教育|研究)` の `(速度|質)` が急上昇！となるのが理想。主役は学生・教員・事務職員のみなさん。DSCはそれを全力でサポート。
- 自分の目の前の困りごとには気付きやすいが、本質的に解決すべき問題は人と話し合わないとわからない
- 「何を解決すべきか」を見誤らないための議論をしましょう

---

# 研究・教育の効率とはなにか、それは測定できるのか

---

![bg fit](images/kenkyujikan.png)

<!-- _footer: 教員の研究時間割合　02年度より13.6ポイント減 東大新聞オンライン 2019年7月9日号 https://www.todaishimbun.org/research_time20190711/ -->

---

# 目的関数の候補

- 授業の準備時間
- 学会発表のための資料作成時間
- 実験に着手してからデータが出るまでの時間
- データを手渡されてから解析が完了するまでの時間
- 期間あたりの論文数
- 事務的な手続きに必要な書類を作成する時間
- 特定ドメインの問題解決能力を会得するために必要な授業時間数
- 人類が新たな知識を得るまでにかかった金銭的コスト
- 人類誕生から新技術の発明まで何年かかったか

これらを `X` 倍にできるか？ `X` のオーダーをどれくらい変化させられるか？

---

# 変数

- 1つの教育プログラム・研究プロジェクトに関わる人間の数 (労働集約・人的並列化)
- 決断・アイディアに至るまでの思考の速さ・深さ
- 試行錯誤のイテレーションを回すスピードと回数
- ミスのない作業 or 手戻りによるロス
- DX・自動化
- 外注 (時間・知識・技術を金で買う)

---

# 何が一番手っ取り早い？

---

「人間を研究のプロセスから排除する」

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# 研究フローからの人間排除の事例

1. ラボラトリー・オートメーション
2. データ解析ワークフローシステム
3. 大規模言語モデルによるテキストアノテーション

---

# 1. ラボラトリー・オートメーション

![center w:700](images/la.avif)

<!-- _footer: 日本経済新聞 ラボラトリーオートメーション　AI活用し研究を自動化 https://www.nikkei.com/article/DGXZQOUC2770H0X20C23A2000000/ -->

---

# ご利益

- 人間には難しい細かすぎるパラメータチューニングが可能
- 労働基準法が適用されない

---

![](images/robotbiology.png)

<!-- _footer: 再生医療用細胞レシピをロボットとAIが自律的に試行錯誤 https://www.riken.jp/press/2022/20220628_2/ -->

---

# 課題

- ロボットが高価
- 人間は安い

---

# 実際はこう

![center w:700](images/ai_pet_family.png)

<!-- _footer: AIに支配される人達のイラスト https://www.irasutoya.com/2016/08/ai.html?m=1 -->

---

# 2. データ解析ワークフローシステム

![center w:800](images/sarek_subway.png)

<!-- _footer: nf-core/sarek https://nf-co.re/sarek/3.4.4/ -->

---

# ご利益

- レビューワーに「このパラメータも試してみたら」と言われても動じない強い心が得られる
- 先輩からもらうコードが「読めないし動かない」から「読めないがちゃんと動く」になる

---

# 課題

- 組み上げた自動化パイプラインは色々な理由で壊れる
- メンテナンスやアップデートで結局コストゼロにはならない

---

# 3. 大規模言語モデルによるテキストアノテーション

---

# 文献や自然言語テキストからの情報抽出

![center](images/existing_ontology_mapping.png)

<!-- _footer: https://biosciencedbc.jp/event/symposium/togo2024/files/poster01_togo2024.pdf -->

---

# 一度LLMに投げて抽出させるステップを挟むことで改善

![center](images/llm-assisted-annnotation.png)

<!-- _footer: https://biosciencedbc.jp/event/symposium/togo2024/files/poster01_togo2024.pdf -->

---

![center](images/prompt-tuning.png)

<!-- _footer: https://biosciencedbc.jp/event/symposium/togo2024/files/poster01_togo2024.pdf -->

---

# ご利益

- 人間の業の深さに魂を削られることがなくなる

---

![center](images/kusometadata1.png)

<!-- _footer: https://www.ncbi.nlm.nih.gov/biosample/?term=SAMD00009749 -->

---

![center](images/kusometadata2.png)

<!-- _footer: https://www.ncbi.nlm.nih.gov/biosample/?term=SAMEA2024666 -->

---

# 課題

- 「抽出させたものが正しいか」は判断できるが「正しく抽出できたか」の評価には人間が読まなくてはならない = カバレッジ100%達成の判断ができない
- 商用LLMは強力だが、大量のデータを処理させるにはAPI利用の値段が高すぎる
- オープンなLLMは小型のものだとレスポンスが速いが非力、大型のものは計算機パワーが必要な上レスポンスが遅くなるので大量データの処理が難しい
- 今月の電気代がやばい

---

確かにまだ課題はあるが、便利な時代はもうとっくに来ている

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# 機械が全部勝手にやってくれる！

---

![center w:800](images/netero.jpg)

<!-- _footer: Hunter X Hunter25 (ジャンプコミックス) 冨樫 義博 (2008) -->

---

:thinking: 全部自動化されると我々はハッピーなのか？

---

# あなたの研究はどこから？

- キュリオシティ・ドリブン
  - 探索の過程がなくなるのは味気ない
- ミッション・ドリブン
  - 省力化できるに越したことはない

---

# 大学教育の意義

- 大学とは最先端の学問が実施され、それを学ぶことができる場所
- インターネットでアクセスできるAIが最先端になったとき、大学教育は必要なのか？

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# みんなで考えよう会議

今の我々に足りない「X倍効率化」を実現するもの

---

Google Maps がなかったときにどうやって目的地まで行っていたか、覚えていますか？
Google Maps がなかったときに、Google Maps が想像できましたか？

---

あなたが「これは自分の教育・研究スタイルを変えた(これがなかったら今の自分の研究はない)！」と思った知識や技術、ツールはなんですか？

---

それは研究や教育におけるどんなボトルネックを解決したと思いますか？

---

今抱えているボトルネックはなんですか？

---

それを解決するものはどんな姿をしていますか、誰が作りますか、いつごろできますか？

---

# 生命科学のボトルネックとその解消に必要なもの

- 賢く誠実で献身的な科学者 (教育 :mortar_board: )
- 新たな現象の発見と観察・仮説構築 (資金 :moneybag: 時間 :stopwatch: 知識 :brain: )
- 新たな計測技術の開発 (資金 :moneybag: 時間 :stopwatch:)
- 生体試料のサンプリング (資金 :moneybag: 社会的合意 :speaking_head: )
- 再現可能な実験とその結果 (資金 :moneybag: 時間 :stopwatch: 技術 :microscope: )
- 論文の出版・およびサイエンスというゲームのルール (社会的合意 :speaking_head: )
- 人類社会における需要 (予測・制御が難しい :thinking: )

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# まとめ

- DSCでは継続的にこういった機会を設けますのでぜひご発言ください
- DSCをうまく使ってください

---

---


# 前提: 生成AIは凄いが、解決すべき問題もある

### SaaSでの提供
- 強力なプロプライエタリ・モデルへの依存 => 透明性・セキュリティ・データ保護

### 計算機
- 高性能GPU計算機への依存 => 特定企業による供給の寡占・膨大な電力消費

### 応用可能性
  - 医療応用における事実誤認など正確性に関するリスク
  - 人間とAIの価値観の相違について（倫理）

<!--
_footer: Yu et al. (2024) Medical Artificial Intelligence and Human Values. 10.1056/NEJMc2408971 / World Health Organization (2024) Ethics and governance of artificial intelligence for health: guidance on large multi-modal models.
-->

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# 実応用への障壁: 出力の正確さの担保

---

# Retrieval Augmented Generation (RAG): データベースを基盤にLLMを「強化」

![](images/rag.png)

<!-- _footer: "Lewis et al. (2020) Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks https://arxiv.org/pdf/2005.11401" -->

一般にはドキュメントを蓄積したベクトルDBが用いられるが **知識グラフでもRAGは可能**

---

# LLMは人における"直感"？

- Daniel Kahneman の著書に曰く、人の思考は「直感的・感情的な速い思考」システム1と「時間のかかる論理的な思考」システム2との組み合わせによって成立している
- 膨大な学習データからパターンを見出すLLMは **「AIにおけるシステム1」** と見なせる
- **論理的な推論を行うシステム2にあたるのは、本来データベースが担う機能**ではないか

![bg fit right:40%](images/fast-and-slow.jpg)

<!-- _footer: "Kahneman. (2017) Thinking, fast and slow." -->

---

![bg fit 40%](images/muller-lyer.png)

<!-- _footer: "Müller-Lyer illusion. Fibonacci, CC BY-SA 3.0 <http://creativecommons.org/licenses/by-sa/3.0/>, via Wikimedia Commons" -->

---

<!-- 
_backgroundColor: steelblue
_color: ivory
_footer: ""
-->

# 近い将来の生成AIは「幻覚」を見ない
完璧になったAIが解消できる「生命科学のボトルネック」は何なのか？

---

# 生命科学のボトルネックとその解消に必要なもの

- 賢く誠実で献身的な科学者 (教育 :mortar_board: )
- 新たな現象の発見と観察・仮説構築 (資金 :moneybag: 時間 :stopwatch: 知識 :brain: )
- 新たな計測技術の開発 (資金 :moneybag: 時間 :stopwatch:)
- 生体試料のサンプリング (資金 :moneybag: 社会的合意 :speaking_head: )
- 再現可能な実験とその結果 (資金 :moneybag: 時間 :stopwatch: 技術 :microscope: )
- 論文の出版・およびサイエンスというゲームのルール (社会的合意 :speaking_head: )
- 人類社会における需要 (予測・制御が難しい :thinking: )

---

# 将来の生命科学を左右するもの

- 観測・予測
  - 既にあるものはAIがなんとかしてくれる。今ないもの・これから起きることは？
- インフラ・データ
  - ハードウェア・計算機・ストレージ・ネットワークの維持はますます困難に
  - 100年後、1000年後に残すべきデータは何か、どうやって残すべきか？
- プログラム・AIの自律性
  - 人間が監督すべきか、人間が監督されるべきか
  - 真に強いAI研究者が現れたとき、人間がサイエンスをやる必要があるのか？


