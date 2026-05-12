# Anti-Gaming Rules — Seismic Score Dashboard v0.1

## Purpose

この文書は、**Seismic Score Dashboard v0.1** における  
スコア不正膨張・誤認誘導・自己増幅・見せかけの共鳴を抑制するための基本原則を定義します。

震源スコアは、設計を誤ると簡単に壊れます。  
なぜなら、価値を測る指標は、公開された瞬間から**操作対象**にもなるからです。

そのため本仕様では、スコアリングと同じくらい、  
**アンチゲーミング設計**を重視します。

---

## Why this matters

震源スコアが危険なのは、  
一見すると「知の価値」を見ているようで、実際には以下のような擬似シグナルに汚染されやすい点です。

- 自作自演の引用
- 短時間集中の不自然な参照
- コピーや言い換えを派生に見せかける行為
- 出典の曖昧化
- キャッシュや再取得の二重計上
- 異議の存在を隠したまま点数だけを流通させること

これを放置すると、Seismic Score Dashboard は  
観測装置ではなく、**虚飾の増幅器**になります。

---

## Core Principle

**高スコアであること**よりも、  
**高スコアが説明可能であること**を優先します。

本仕様におけるアンチゲーミングの基本姿勢は、次の一文に集約されます。

> スコアは盛れるものではなく、監査に耐えるものでなければならない。

---

## Threat Model

本仕様が想定する主要な操作リスクは、以下の6類型です。

### 1. Self-Loop Inflation
同一主体が自分自身を繰り返し引用・参照し、  
人工的に trace や resonance を膨らませる行為。

### 2. Burst Manipulation
短時間に不自然なアクセスや参照を集中させ、  
人気や利用量があるように見せる行為。

### 3. Copy-Derivative Abuse
単純な複製、表層的な言い換え、並べ替えを  
「派生」や「再解釈」と偽装する行為。

### 4. Attribution Blur
起点を曖昧にし、実際の震源を見えにくくする行為。

### 5. Double Counting
同一利用を重複して計上し、  
trace や allocation readiness を不当に高く見せる行為。

### 6. Dispute Masking
異議申し立てや帰属争いがあるにもかかわらず、  
スコア流通上はそれを反映させない行為。

---

## Defensive Philosophy

アンチゲーミングは、単に「ズルを防ぐ」ためだけのものではありません。  
その本質は、**観測の品位を守ること**にあります。

そのため v0.1 では、以下の姿勢を採用します。

- 疑わしい値は、いきなり禁止せず**減衰**させる
- 不確実性は隠さず、**フラグとして可視化**する
- 高得点の裏には、常に**説明責任**を要求する
- popularity と provenance を混同しない
- 数値だけでなく、**履歴と文脈**を見る

---

## Rule Set

以下は v0.1 における基本防御ルールです。

---

### Rule 1: Self-Citation Decay

## Definition
同一主体による自己循環引用は、逓減加点とします。

## Rationale
自己参照そのものは不正ではありません。  
しかし、無制限に加点すると、自己増殖ループだけでスコアが膨張します。

## Recommended handling
- 初回自己引用: 通常の一部加点
- 2回目以降: 逓減
- 極端な自己循環群: anomaly flag 付与

## Suggested implementation posture
- same author
- same repo owner
- same publishing identity
- tightly linked identity cluster

これらが一致する場合は、自己循環の可能性を考慮します。

---

### Rule 2: Burst Anomaly Detection

## Definition
短時間に集中した不自然な参照や引用を異常値候補として扱います。

## Rationale
自然な共鳴は、多くの場合ある程度の時間幅を持ちます。  
極端な集中は、誘導・操作・キャンペーン的増幅の可能性があります。

## Recommended signals
- short-time spike ratio
- repeated same-source access
- same-network burst
- identical pattern retrieval burst

## Suggested handling
- 即時排除ではなく anomaly flag 付与
- trace_score への重み減衰
- 必要に応じて human review 対象化

---

### Rule 3: Cache Double Count Prevention

## Definition
キャッシュ再利用は、通常利用と同等には扱わず、低い重みで計上します。

## Rationale
キャッシュは再利用効率を示しますが、  
新規消費そのものと同じ価値ではありません。

## Recommended handling
- input token: 標準重み
- output token: 中程度重み
- cache token: 低重み

v0.1 の推奨補助式では、cache は以下のように軽く扱います。

```text
SCI =
  input_tokens_consumed +
  (output_tokens_generated * 0.5) +
  (cache_tokens_reused * 0.2)
Rule 4: Copy-Derivative Discount
Definition

単純複製や表層的な言い換えは、共鳴として過大評価しません。

Rationale

派生が多く見えても、その中身が単なるコピー群であれば、
それは真の resonance ではありません。

Suspicious patterns
title only changed
wording only lightly altered
paragraph order shuffled only
synonym replacement without structural transformation
no added definition, frame, or interpretation
Suggested handling
derivative_count のそのまま加算を避ける
reinterpretation_count と区別する
downstream_depth_score への寄与を抑制する
必要なら copy-like flag を付与する
Rule 5: Attribution Confidence Gate
Definition

起点帰属の信頼度が低い場合、総合スコアの伸びを抑制します。

Rationale

trace や resonance が大きくても、
誰が震源か曖昧なままでは return 層へ接続できません。

Suggested handling
attribution_confidence が低い場合は return_score を減衰
一定以下では allocation_status を not_ready に固定
provenance 不足時は penalty を加算
Rule 6: Unresolved Dispute Penalty
Definition

未解決の異議がある場合、return 系および総合点を減衰させます。

Rationale

争点が残っている状態で高スコアだけが独り歩きすると、
制度的な誤配分を招きやすくなります。

Suggested handling
dispute_status = pending | disputed の場合は penalty 加算
allocation_status は pending_review または withheld を推奨
UI上で dispute 状態を明示する
Rule 7: Transparency over Black Box
Definition

総合スコアだけを表示してはならず、
内訳・減点・主要根拠を併記することを原則とします。

Rationale

不透明なスコアは、必ず操作されるか、不信を招きます。

Required visibility
seismic_score
5 layer breakdown
penalty_total
anomaly_flags
dispute_status
attribution_confidence
Severity Levels

v0.1 では、不自然な挙動をすべて同一に扱うのではなく、
次の3段階で考えることを推奨します。

Level 1 — Noise

軽微な不自然さ。
誤差や偶然の可能性が高い。

対応:

flag のみ
スコア維持または軽微な減衰
Level 2 — Suspicious

一定の操作性が疑われる。
機械的処理だけでは不十分。

対応:

減衰
human review 候補
allocation 保留候補
Level 3 — Manipulative

不自然性が明確で、スコア汚染の可能性が高い。

対応:

強い減衰
allocation withheld
audit 対象
必要に応じて無効扱い
Penalty Guidance

Penalty は、制裁ではなく不確実性の表現です。
そのため、v0.1 では以下の姿勢を推奨します。

penalty は説明可能な理由に紐づける
penalty は複数の小要因に分解できるようにする
一発退場型より、減衰型を優先する
不確実性と不正を混同しない
Example penalty buckets
attribution penalty
provenance penalty
dispute penalty
duplication penalty
anomaly penalty
self-loop penalty
Example Cases
Case A: Self-citation spiral

同一著者が、自分の記事群・リポジトリ群・派生投稿群を相互に参照し、
大量の citation_count を作っている。

推奨対応:

self-citation decay を適用
anomaly flag を付与
resonance ではなく internal loop として別扱い
Case B: Sudden burst with no downstream depth

短時間で急増したが、その後の継続参照も派生深度もない。

推奨対応:

burst anomaly detection
trace の一部減衰
resonance 加点は抑制
Case C: Many derivatives, little transformation

派生数は多いが、実際には文言差分しかない。

推奨対応:

copy-derivative discount
reinterpretation_count と分離
downstream_depth_score を低く維持
Case D: Strong source, unresolved dispute

起点性も純度も高いが、帰属争いが継続中。

推奨対応:

origin / purity は維持可能
return を強く減衰
allocation_status を pending_review or withheld
UI Recommendations

ダッシュボードUI上では、異常や不確実性を隠さないことが重要です。

Recommended visible elements
anomaly flags
dispute badge
attribution confidence meter
penalty breakdown
review status
allocation readiness state
Recommended anti-misleading posture
総合点だけを大きく見せすぎない
問題のあるレコードには視覚的注意表示をつける
“high score” と “distribution ready” を分離して表示する
Governance Connection

アンチゲーミングは、単独では完結しません。
これは governance 層への橋渡しです。

自然な接続先:

dispute registry
signed attestation layers
trace architecture
royalty allocation logic
audit workflows

つまり、anti-gaming rules は
単なるフィルタではなく、制度に耐える観測をつくるための前室です。

Minimum Requirements for v0.1

v0.1 で最低限必要な防御は以下です。

self-citation decay
burst anomaly detection
cache double count prevention
copy-derivative discount
dispute-aware penalty
visible scoring transparency

この6つがなければ、
Seismic Score Dashboard はまだ本格運用に耐えません。

What this document does not do

この文書は、以下を直接は定義しません。

法的違反の断定
不正の最終認定
ペナルティ係数の厳密数学化
審査機関の設計
分配実行そのもの

それらは将来の governance / dispute / allocation 文書で扱うべきです。

Summary

Seismic Score Dashboard におけるアンチゲーミングの目的は、
単にズルを防ぐことではありません。

目的は、

震源を見失わないこと
共鳴を見せかけにしないこと
利用量を二重化しないこと
帰属不確実性を隠さないこと
分配判断を早まらせないこと

です。

言い換えれば、これは
スコアを守るための防御ではなく、
観測の信頼を守るための防御です。
