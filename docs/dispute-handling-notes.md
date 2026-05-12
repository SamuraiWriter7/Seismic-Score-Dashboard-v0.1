# Dispute Handling Notes — Seismic Score Dashboard v0.1

## Purpose

この文書は、**Seismic Score Dashboard v0.1** において  
異議申し立て（dispute）が発生した場合に、どのような考え方で扱うべきかを整理するための設計メモです。

本書は、法的裁定の完全仕様ではありません。  
また、単独で dispute 解決を完結させる制度文書でもありません。

ここで扱うのは、あくまで次の問いです。

- dispute が起きたとき、Dashboard は何をどう表示すべきか
- どの状態を penalty や readiness に反映すべきか
- どこから先を governance / Royalty OS / 外部審査へ渡すべきか

言い換えれば、これは  
**観測層における異議処理の取り扱いメモ**です。

---

## Why this matters

震源スコアは、起点・利用・共鳴・純度・還元準備性を観測する仕組みです。  
しかし、価値循環の観測は、しばしば争点を生みます。

典型例は次の通りです。

- その知の起点は本当にその人か
- その派生は正当な再解釈か、単なる複製か
- その citation は意味のある参照か、表面的な言及か
- その allocation readiness は早すぎないか
- 複数人が同じ震源を主張していないか

こうした争点を無視したままスコアだけを流通させると、  
Dashboard は計器盤ではなく、**誤配分の拡声器**になります。

そのため、v0.1 の段階から dispute を  
**見えるものとして扱う姿勢**が必要です。

---

## Core Principle

本仕様における基本原則は、次の一文に要約できます。

> 異議がある状態では、スコアを消すのではなく、不確実性を見える形で残す。

つまり、

- dispute が起きたから即ゼロにする、ではない
- dispute があるのに通常状態として見せる、でもない

という中間の扱いが重要です。

---

## What counts as a dispute

ここで言う dispute とは、単なる感想の違いではなく、  
**スコア・帰属・派生・還元候補性に影響しうる異議**を指します。

典型的には以下が含まれます。

### 1. Origin dispute
「その知の起点は別にある」という異議。

### 2. Attribution dispute
「その成果の寄与者が他にもいる」という異議。

### 3. Derivative dispute
「これは正当な派生ではなく、過度な複製である」という異議。

### 4. Citation dispute
「この citation は意味のある参照として数えるべきではない」という異議。

### 5. Allocation dispute
「この record を分配候補とするのは早い、または不適切である」という異議。

### 6. Record integrity dispute
「ログ、timestamp、revision、provenance chain などの記録自体に疑義がある」という異議。

---

## What is not necessarily a dispute

逆に、以下は即 dispute とは限りません。

- 単なる評価の好み
- 思想的賛否
- popularity の高低
- 文章の好き嫌い
- 影響を受けた気がする、というだけの曖昧な感覚

これらは重要な周辺情報にはなりえますが、  
直ちに governance status を変える dispute とは区別されるべきです。

---

## Dashboard posture toward disputes

Seismic Score Dashboard は、dispute を**裁定する装置**ではありません。  
ただし、dispute を**表示しない装置**でもありません。

役割は次の通りです。

### Dashboard should
- dispute の存在を可視化する
- dispute status を保持する
- return readiness に反映する
- 必要に応じて penalty をかける
- downstream の governance や Royalty OS に注意信号を渡す

### Dashboard should not
- 最終法的判断を下す
- 一方の主張だけで ownership を確定する
- dispute があることを隠して高スコアだけを前面表示する
- 異議処理そのものを完結させたかのように装う

---

## Recommended dispute statuses

v0.1 では、少なくとも以下の状態を扱えると自然です。

### `none`
異議なし。  
少なくとも現在の観測範囲では dispute が確認されていない状態。

### `pending`
異議が提起されたが、まだ整理・確認・予備審査中の状態。

### `disputed`
争点が明示され、スコアや allocation readiness に影響を与える状態。

### `resolved`
争点が一定の形で整理され、観測上の状態が落ち着いた状態。

### `superseded`
元の記録や主張が、後続の記録・証拠・裁定により上書きされた状態。

---

## Recommended lifecycle

dispute の流れは、概ね次のように考えると整理しやすいです。

```text
issue raised
   ↓
pending
   ↓
disputed
   ↓
resolved or superseded

より丁寧に書けば、こうです。

claim / objection submitted
        ↓
intake and registration
        ↓
preliminary review
        ↓
dispute status applied
        ↓
evidence update / review / governance handling
        ↓
resolved or superseded

この流れの中で、Dashboard は
「どの段階にあるか」を表示し、
「その状態をどこまで score / readiness に反映するか」を扱います。

Minimal dispute record elements

v0.1 の段階でも、dispute を扱うなら最低限以下は持ちたいです。

dispute identifier
related source_id
dispute type
raised_at
raised_by
short description
current status
linked evidence references
review note
last_updated_at

これがないと、単なる「揉めてます」表示になってしまい、
後から追えません。

Recommended handling by score layer

dispute は、全スコアに同じように効かせるべきではありません。
層ごとに扱いを分けるほうが自然です。

Origin

起点争いがある場合、もっとも影響を受けやすい層です。
Origin dispute が発生したときは、origin_score の確信度解釈を弱めるべきです。

Trace

Trace は「使われた量」の観測なので、dispute があっても値自体は消さない場合があります。
ただし、二重計上や citation count の正当性争いがある場合は一部再評価が必要です。

Resonance

派生の正当性争いがある場合、resonance の過大評価を抑える必要があります。
特に copy-derivative dispute とは強く結びつきます。

Purity

Purity は通常 dispute の直接対象ではありませんが、
構造の分解や独自性に関する異議がある場合、補助的に読み直し対象になります。

Return

もっとも強く影響を受ける層です。
未解決 dispute がある場合、return_score は積極的に減衰させるのが自然です。

Recommended handling by readiness

allocation_status への反映は特に重要です。

If dispute_status = none

通常の readiness 判定へ進めます。

If dispute_status = pending

allocation は慎重扱いが望ましく、
少なくとも pending_review に近い運用が自然です。

If dispute_status = disputed

allocation は原則として強く慎重化され、
pending_review または withheld が推奨されます。

If dispute_status = resolved

解決内容に応じて通常フローへ戻せます。
ただし、履歴として dispute が存在した事実は残すべきです。

If dispute_status = superseded

元レコードの allocation は通常停止または大幅修正が必要です。

Penalty guidance

dispute は、即ゼロ化ではなく、
penalty と readiness 制御の組み合わせで扱うのが自然です。

Recommended posture
pending: 軽度〜中程度 penalty
disputed: 中程度〜強い penalty
resolved: 原則 penalty 解消可能。ただし履歴は保持
superseded: 元レコード側に強い制限
Important note

Penalty は、異議を出された側への「罰」ではなく、
未確定性の表現として扱うべきです。

ここを間違えると、dispute 制度そのものが攻撃手段になります。

Evidence posture

dispute handling では、
「誰が強く言ったか」よりも「何が示されたか」を優先すべきです。

そのため、少なくとも以下を意識します。

timestamp evidence
publication history
revision history
provenance chain
linked citations
derivative comparisons
audit notes
archived records

異議があるときほど、
言葉よりも痕跡が重要になります。

Human review posture

v0.1 の段階では、すべてを自動で処理しようとしないことが重要です。

特に以下の場合は、human review が自然です。

起点争いが強い
複数の有力寄与者がいる
copy か reinterpretation かが微妙
主要 record の allocation readiness に直結する
superseded の可能性がある

自動処理だけで片づけると、
きれいに見えても中身は泥沼、という状態になりがちです。

Example cases
Case A: Competing origin claim

ある概念について、別の著者が「自分のほうが先に定義した」と主張した。

推奨対応:

dispute_type = origin
dispute_status = pending → disputed
origin_score の解釈を慎重化
return_score を減衰
allocation_status を pending_review
Case B: Derivative or copy?

ある派生記事が、再解釈ではなく実質コピーだと指摘された。

推奨対応:

dispute_type = derivative
resonance を再評価対象にする
derivative_count の扱いを見直す
copy-like flag を付与
必要に応じて withheld
Case C: Citation counted but not meaningful

言及はあるが、実質的に内容へ寄与していない citation が大量に計上されている。

推奨対応:

dispute_type = citation
citation quality の見直し
trace / resonance の一部補正
penalty を限定的に付与
Case D: Resolved attribution dispute

共著者や寄与者の整理がつき、shared-source として扱うことが決まった。

推奨対応:

dispute_status = resolved
allocation note を更新
return_score を再計算
history を保持したまま通常状態へ復帰
UI recommendations

Dashboard 上では、dispute を隠さないことが重要です。

Recommended visible elements
dispute badge
dispute_status
dispute type
last updated timestamp
evidence linked indicator
review status
allocation warning state
Recommended display posture
高スコアでも dispute badge を消さない
disputed のときは readiness を別表示する
「高スコア」と「今すぐ返せる」は分けて見せる
resolved 後も履歴参照の導線を残す
Governance bridge

Seismic Score Dashboard 単体で dispute を完結させるのではなく、
必要に応じて downstream の governance layer へ渡すのが自然です。

接続先の候補は、たとえば以下です。

dispute registry
signed attestation layers
audit workflows
royalty allocation review
human adjudication process

つまり、この文書は
dispute をどう表示し、どう保留し、どこへ渡すかのためのメモです。

Practical summary

実務的には、dispute handling において Dashboard がやるべきことは次の通りです。

異議の存在を記録する
状態を見える化する
score 解釈を慎重化する
return readiness を減衰させる
governance に橋渡しする

逆に、やりすぎてはいけないことは次の通りです。

ownership を最終確定する
法的裁定を代行する
dispute を隠したままスコアだけを流通させる
一時的な異議だけで全価値をゼロ扱いする
Summary

Seismic Score Dashboard における dispute handling の本質は、
争いを消すことではありません。

本質は、

争点を可視化し
未確定性を隠さず
readiness を慎重に扱い
downstream governance へ正しく渡す

ことにあります。

より短く言えば、

dispute is not a signal to erase value.
It is a signal to slow certainty.

この姿勢があることで、
Dashboard はスコアの飾り棚ではなく、
制度に接続できる観測面として機能しやすくなります。
