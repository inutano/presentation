### 次世代シーケンサーによるメタゲノム解析：桜の花びらに付着した環境DNAを分析する

![]()
![]()

大田達郎
ライフサイエンス統合データベースセンター (DBCLS)
2018/12/26 JSTグローバルサイエンスキャンパス 講演会

![dbcls_logo](images/dbcls.png)

---

# 背景: Next-generation sequencing の登場

- この10年でDNA配列解読技術は劇的に進歩した
- 昔: サンガー法によるゲノムシーケンス
  - そこそこの長さの塩基配列を時間かけて解読する
- 2008年ごろ: 次世代シーケンス技術 (NGS) の登場
  - 短い長さの塩基配列を大量に解読する
  - すごく長い塩基配列をある程度の量だけ解読する
- 解読が難しかった塩基配列が読める
  - できなかったことができるように

---

# サンガー法の原理

![140% center](images/sanger.png)

<font size=2>Mitochondrial DNA in Sensitive Forensic Analysis https://www.researchgate.net/figure/Principle-of-Sanger-sequencing-Incorporation-of-ddNTPs-terminates-the-elongation-of-the_fig4_265264877</font>

---

# NGS: Sequencing by Synthesis (Illumina)

![60%](images/illumina.png)

<font size=2>https://bitesizebio.com/13546/sequencing-by-synthesis-explaining-the-illumina-sequencing-technology/</font>

---

# NGS: Nanopore technology

![center](images/nanopore.png)

<font size=2>An ace in the hole for DNA sequencing https://www.nature.com/articles/550285a</font>

---

# Omics: NGS が可能にした測定手法

- Genome
  - Variant Analysis
  - Whole Genome Sequence
- Exome
- Transcriptome
  - RNA-Seq
- Epigenome
  - ChIP-Seq
  - DNase-Seq
  - ATAC-Seq
  - Methyl-Seq
- Metagenome

---

# Metagenome

- サンプル中に含まれるDNAをまるごと全部解析する
- 特定の領域をPCRで増やして読むことも
  - e.g. meta 16S sequencing
- DBに問い合わせることでどんな生物が存在していたかがわかる

---

# メタゲノム研究の事例

- ヒト腸内細菌叢の解析
- ヒト皮膚常在菌の解析
- 環境DNA = 特定の環境に存在するDNAをサンプリングして解析
  - 土壌
  - 水中
  - 空気中

---

# 環境DNA解析の事例

- 美ら海水族館の水槽の中の配列を解析する
- 空気中に存在する微生物の配列を解析する
- 地下鉄構内に存在する微生物の配列を解析する

---

# 海水中の塩基配列解析

![150% center](images/tyuraumi.jpg)

- 海水を汲んでメタゲノム解析することで存在する魚の種類と数を同定する
- https://www.jst.go.jp/pr/announce/20150722-4/index.html

<font size=2>Miya M, et.al. MiFish, a set of universal PCR primers for metabarcoding environmental DNA from fishes: detection of more than 230 subtropical marine species. Royal Society open science. 2015 Jul 1;2(7):150088. https://doi.org/10.1098/rsos.150088</font>

---

# 空気中の塩基配列解析

![center 20%](images/airborne.png)

- 空気中に存在する微生物の種類を同定し、公衆衛生施策に反映

<font size=2>Tringe SG, et.al. The airborne metagenome in an indoor urban environment. PloS one. 2008 Apr 2;3(4):e1862. https://doi.org/10.1371/journal.pone.0001862</font>

---

# MetaSUB Project

![center](images/metasub.jpg)

- 世界中の地下鉄構内 = 多数の人が利用する公共の閉鎖空間にどのような微生物が存在するか調査

<font size=2>MetaSUB International Consortium. The metagenomics and metadesign of the subways and urban biomes (MetaSUB) international consortium inaugural meeting report. https://doi.org/10.1186/s40168-016-0168-z</font>

---

# 桜の花びらに付着した環境DNAを分析する

---

# 背景と目的

- 日本中に自生するソメイヨシノは単一の株に由来するクローン
  - 南は鹿児島、北は北海道南部まで
- 気象条件が揃うと開花
  - 一週間から10日ほどで散ってしまう
- 短い期間だけ外界に晒される花びらの上にはどんな環境DNAが存在するのか

---

# サンプリング手法と取得したサンプル

- クラウドソーシングを利用
  - プロジェクトを宣伝、参加者を募る
  - キットを送ってサンプリングしてもらい、サンプルを送り返してもらう
- バッファで湿らせた綿棒状のキットで花びら表面を拭ってサンプリング
- 149名の参加者、594サンプルを回収

---

# サンプルの回収

![20% center](images/omg_00.png)

- 赤丸がサンプリング拠点
- サンプルを取り違えないようにバーコードで管理

---

# DNAシーケンスの手順

![80% center](images/sakura_seq_01.png)

- boiling法によってDNAを一括で抽出
- Illuminaのシーケンサーで16S rRNA 領域をシーケンス

---

# 16S rRNA Sequence

![center](images/sakura_seq_02.png)

- 16S rRNA をコードするDNA領域をシーケンス
- 原核生物の種同定に用いられる

---

# 解析結果1

![center](images/omg_01.png)

- シーケンサから読み出された塩基配列断片の由来を門レベルで解析
- サンプル (= 拠点) ごとに同定された断片の数の分布
- どこでも見つかるもの、特定の拠点でしか見つからないものがある

---

# 解析結果2

![center](images/omg_02.png)

- 配列解析の結果、どの生物種由来と思われるDNAが見つかったか
- 桜そのものに由来すると思われるDNAの他に様々な植物が見つかる

---

# 結論と考察

- 短い開花期間、小さな花びらでも多数の環境DNAが付着している
- 地域差は存在するが、それが樹木の位置レベルのものかエリアレベルのものかは判断できない
- 16S rRNA 解析は簡便で安価だが正確な生物種の同定には情報が不足
- 3月初旬から5月初旬までの数ヶ月という短い期間で、全国規模のサンプリングを行ったのは国内初 (おそらく世界でも初)

---

# 参考文献/ウェブサイト

- 論文
  - Ohta T, Kawashima T, et. al. Collaborative environmental DNA sampling from petal surfaces of flowering cherry Cerasus× yedoensis ‘Somei-yoshino’across the Japanese archipelago. Journal of plant research. 2018 Feb 19:1-9. https://link.springer.com/content/pdf/10.1007/s10265-018-1017-x.pdf
  - SharedIt http://rdcu.be/HmdX
- 日本語解説記事
  - 全国のソメイヨシノの花びらに付着したDNAを解析し、環境中に存在するDNAの由来を調査 https://www.nig.ac.jp/nig/ja/2018/03/research-highlights_ja/20180312-3.html