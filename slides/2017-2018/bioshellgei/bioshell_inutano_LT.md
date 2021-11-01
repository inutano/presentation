![twitter.com/inut](images/diesel.jpg)

## tw: inut, gh: inutano

---

# 宣伝: 国内版バイオハッカソン BH17.11

- http://wiki.lifesciencedb.jp/mw/BH17.11
- 11/26 - 12/1 @ 熊本県熊本市 菊南温泉ユウベルホテル

---

# pfastq-dump

- github.com/inutano/pfastq-dump
  - 鈍足fastq-dumpをspot指定で部分展開 + 並列実行
  - pure bash

![pfastq-dump center](images/pfastq-dump.png)

---

# Bioinformatics :heart: シェル芸

---

# Bioinformatics :hatching_chick:

1. 生命科学の問題を解くための情報科学の道具を作る
2. 情報科学の道具を使って生命科学の問題を解く
    - シェル芸はこっち

---

# ゲノム科学 :heart: シェル芸

- ゲノム: 生物のソースコード
- ゲノム情報はどのように生物の機能をコードしているか？
  - ゲノム多型
  - 遺伝子発現
  - 遺伝子発現制御
  - etc.
- 何ができればゲノムを理解したと言えるのか
  - 任意の表現型を示す生物のゲノムを設計する

---

# シェル芸でヒトゲノムを構築する

---

# FASTQを生成するワンライナー

```
READLENGTH=100
seq 400000000 | awk -v rlength="${READLENGTH}" '
  BEGIN{
    base[0]="A"; base[1]="T"; base[2]="G"; base[3]="C";
  } NR%4==1 {
    print "@read." int(NR/4)+1
  } NR%4==2 {
    seq=""; for(i=1;i<rlength;i++){
      seq=seq sprintf("%c", base[int(rand()*100%4)])
    }; print seq
  } NR%4==3 {
    print "+"
  } NR%4==0 {
    ql=""; for(i=1;i<rlength;i++){
      ql=ql sprintf("%c", substr(rand(), 3) % 93 + 33)
    }; print ql
  }'
```

- 好きな数だけリード吐いてくれるので便利
- これをリファレンスにマップできたらヒトゲノム出来たことにする

---

![https://en.wikipedia.org/wiki/Infinite_monkey_theorem](images/monkey.jpg)

# The Infinite Monkey Theorem

###### ランダムな文字列を生成し続ければいつかは任意の文章を生成できる

---

# 無限にFASTQを生成する

```
READLENGTH=100
yes | awk -v rlength="${READLENGTH}" '
  BEGIN{
    base[0]="A"; base[1]="T"; base[2]="G"; base[3]="C";
  } NR%4==1 {
    print "@read." int(NR/4)+1
  } NR%4==2 {
    seq=""; for(i=1;i<rlength;i++){
      seq=seq sprintf("%c", base[int(rand()*100%4)])
    }; print seq
  } NR%4==3 {
    print "+"
  } NR%4==0 {
    ql=""; for(i=1;i<rlength;i++){
      ql=ql sprintf("%c", substr(rand(), 3) % 93 + 33)
    }; print ql
  }'
```

- hashtag: #yes

---

# 無限に生成されるFASTQを延々とmapする

```
READLENGTH=100
yes | awk -v rlength="${READLENGTH}" '
  BEGIN{
    base[0]="A"; base[1]="T"; base[2]="G"; base[3]="C";
  } NR%4==1 {
    print "@read." int(NR/4)+1
  } NR%4==2 {
    seq=""; for(i=1;i<rlength;i++){
      seq=seq sprintf("%c", base[int(rand()*100%4)])
    }; print seq
  } NR%4==3 {
    print "+"
  } NR%4==0 {
    ql=""; for(i=1;i<rlength;i++){
      ql=ql sprintf("%c", substr(rand(), 3) % 93 + 33)
    }; print ql
  }' | bwa mem genome.fa - > onelinehuman.sam
```

- 永遠に結果が返ってこないので生成できたかどうか分からない

---

# 無限にFASTQをmapしつつdepthをカウントし続ける

```
READLENGTH=100
yes | awk -v rlength="${READLENGTH}" 'BEGIN{ base[0]="A"; base[1]="T"; base[2]="G"; base[3]="C" } NR%4==1 { print "@read." int(NR/4)+1 } NR%4==2 { seq=""; for(i=1;i<rlength;i++){ seq=seq sprintf("%c", base[int(rand()*100%4)]) }; print seq } NR%4==3 { print "+" } NR%4==0 { ql=""; for(i=1;i<rlength;i++){ ql=ql sprintf("%c", substr(rand(), 3) % 93 + 33) }; print ql }' \
  | awk 'NR%4!=0 { printf $0 "\t" } NR%4==0 { print $0 }' \
\
  | while read seq; do
    bwa mem genome.fa <(echo $seq | tr '\t' '\n') \
    | samtools view -b - \
    > $(echo $seq | awk '{ sub("@",""); print $1 }').bam
    samtools cat *bam | samtools sort \
    | samtools depth -a - \
    | awk '{ sum += $3 }END{ print sum/NR }'
  done
```

- そのうちヒトゲノムが完成します
- 待っている間に研究をしましょう

---

# 寒い冬に暖を取るためのバイオワンライナー

###### for [シェル芸勉強会 meets バイオインフォマティクス vol.1](https://bio-shell.connpass.com/event/66089/), 2017/10/18

Tazro Ohta / @inutano

![dbcls](images/dbcls.png)

---

# おまけ: コピペ用一行野郎

`READLENGTH=100; yes | awk -v rlength="${READLENGTH}" 'BEGIN{ base[0]="A"; base[1]="T"; base[2]="G"; base[3]="C" } NR%4==1 { print "@read." int(NR/4)+1 } NR%4==2 { seq=""; for(i=1;i<rlength;i++){ seq=seq sprintf("%c", base[int(rand()*100%4)]) }; print seq } NR%4==3 { print "+" } NR%4==0 { ql=""; for(i=1;i<rlength;i++){ ql=ql sprintf("%c", substr(rand(), 3) % 93 + 33) }; print ql }' | awk 'NR%4!=0 { printf $0 "\t" } NR%4==0 { print $0 }' | while read seq; do bwa mem genome.fa <(echo $seq | tr '\t' '\n') | samtools view -b - > $(echo $seq | awk '{ sub("@",""); print $1 }').bam; samtools cat *bam | samtools sort | samtools depth -a - | awk '{ sum += $3 }END{ print sum/NR }'; done
`