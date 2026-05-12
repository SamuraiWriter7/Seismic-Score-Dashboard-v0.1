# Allocation Readiness — Seismic Score Dashboard v0.1

## Purpose

この文書は、**Seismic Score Dashboard v0.1** における  
`allocation readiness` の意味、判定観点、状態遷移、注意点を整理するための設計文書です。

Seismic Score Dashboard は分配そのものを実行するOSではありません。  
しかし、観測結果を後段の Royalty OS や governance layer に渡す以上、  
**「どの記録が、どの程度“返せる状態”に近いか」** を示す必要があります。

allocation readiness とは、まさにそのための概念です。

---

## One-line definition

**Allocation readiness** とは、  
ある record が、観測・証拠・帰属・異議状態の観点から、  
どの程度還元候補として扱える状態にあるかを示す準備度指標である。

---

## Why this matters

AI時代の価値循環では、  
「価値が発生していること」と「返せる状態にあること」は同じではありません。

たとえば、ある source が

- 多く使われている
- 多く引用されている
- 派生も多い

としても、

- 誰が起点か曖昧
- 共創か単独か未整理
- dispute が継続中
- evidence が弱い
- 二重計上の疑いがある

なら、分配候補としてはまだ危うい状態です。

そのため、Seismic Score Dashboard では  
スコアの高さとは別に、**allocation readiness** を扱います。

---

## Core idea

allocation readiness は、  
「どれだけ価値があるか」を示すものではありません。

示すのは、

**その価値を、今どれだけ制度的に返しやすいか**

です。

つまり、これは人気指標ではなく、  
**制度接続準備度**です。

---

## Relationship to other layers

allocation readiness は、以下の中間に位置します。

```text
observed traces
    ↓
seismic score interpretation
    ↓
allocation readiness
    ↓
governance / royalty decision

より短く言えば、

Trace → Score → Readiness → Govern → Return

です。

Seismic Score Dashboard が担うのは、
このうち Readiness まで を整えるところです。

What allocation readiness is based on

v0.1 では、allocation readiness は主に次の観点から判断します。

1. Attribution clarity

誰に返すべきかが、どの程度明確か。

2. Evidence strength

その判断を支える証拠が、どの程度十分か。

3. Trace continuity

利用痕跡が断片的ではなく、ある程度つながって見えているか。

4. Dispute status

異議が存在するか、未解決か、解消済みか。

5. Governance friction

監査・見直し・保留が必要な要因がどれだけあるか。

6. Allocation interpretability

分配比率や候補の考え方を、どの程度説明しやすいか。

What it is not based on alone

allocation readiness は、以下だけでは決めません。

高い閲覧数
高い citation_count
高い seismic_score
話題性
バズ
単一の主張だけ

これらは参考にはなりますが、
readiness を単独で支える根拠にはなりません。

Recommended readiness states

v0.1 では、少なくとも以下の状態を持つと自然です。

not_ready

まだ分配候補として扱うのは早い状態。

典型例:

attribution 不明瞭
evidence 不足
trace が断片的
dispute が強い
anomaly が多い
proposed

分配候補として仮提示できる状態。

典型例:

起点はある程度見えている
trace も一定量ある
大きな dispute はない
ただし governance の最終確認は未了
pending_review

候補としては見えているが、審査や確認が必要な状態。

典型例:

軽微〜中程度の dispute
attribution が複数候補にまたがる
anomaly flag が存在
比率算定の再確認が必要
approved

後段の制度レイヤーで分配候補として承認できる状態。

注意:
Dashboard 単体で “approved” を最終確定するのではなく、
governance を経た結果として扱うのが自然です。

distributed

実際に分配が実行された、または分配記録が確定した状態。

これは通常、Seismic Score Dashboard 単体よりも
Royalty OS 側の状態に近いものです。

withheld

価値は観測されているが、分配は意図的に留保されている状態。

典型例:

unresolved dispute
strong anomaly
evidence insufficiency
superseded possibility
Readiness is not ownership

最重要の注意点はこれです。

allocation readiness は ownership ではありません。

readiness が高いとは、

誰かが最終所有者である
法的に確定している
そのまま支払ってよい

という意味ではありません。

意味するのは、

制度上の判断に進みやすい
保留条件が少ない
説明可能な候補になりやすい

ということです。

Relationship to return score

Return Score と allocation readiness は近いですが、同じではありません。

Return Score

返しやすさを数値的に観測したもの。

Allocation Readiness

その観測結果を、状態としてどう扱うかを示したもの。

つまり、

Return Score は measurement
Allocation Readiness は operational state

です。

Recommended interpretation logic

v0.1 では、たとえば次のような読み方が自然です。

High return score + no dispute + strong evidence

→ proposed または approved に近い

Medium return score + some uncertainty

→ pending_review

Low return score + attribution weakness

→ not_ready

High overall score + unresolved dispute

→ withheld または pending_review

ここで重要なのは、
総合スコアが高くても readiness は低くなりうる
という点です。

Typical readiness factors
Positive factors
attribution_confidence が高い
evidence_strength が高い
trace_continuity が高い
dispute_status が none or resolved
anomaly_flags が少ない
source boundary が明確
allocation note が説明可能
Negative factors
attribution_confidence が低い
dispute_status が pending or disputed
provenance chain が弱い
self-loop inflation の疑い
copy-derivative ambiguity
source overlap が強い
superseded possibility
Example cases
Case A: Strong single-source candidate
origin_score: 高い
trace_score: 高い
return_score: 高い
dispute_status: none
attribution_confidence: 高い

推奨状態:
proposed

理由:
観測上かなり整っており、後段制度へ渡しやすい。

Case B: Strong value, weak readiness
seismic_score: 高い
trace_score: 高い
resonance_score: 高い
dispute_status: disputed
evidence_strength: 中程度

推奨状態:
pending_review または withheld

理由:
価値は見えているが、返すにはまだ危うい。

Case C: Quiet but clean source
origin_score: 高い
purity_score: 高い
trace_score: 低い
dispute_status: none

推奨状態:
not_ready または低強度の proposed

理由:
将来候補ではあるが、まだ十分な循環が観測されていない。

Case D: Superseded candidate
過去は高評価
新証拠で別 source が上位起点と判明
dispute_status: superseded

推奨状態:
withheld または旧配分停止

理由:
元レコードの readiness は維持できない。

Recommended UI posture

Dashboard 上では、allocation readiness を
総合点とは別に表示することが重要です。

Recommended visible elements
allocation_status badge
attribution confidence meter
dispute badge
evidence strength indicator
anomaly flag summary
allocation note
Recommended display principle
高スコアでも readiness が低ければ明示する
readiness が高くても ownership のようには見せない
withheld を失敗扱いせず、「慎重状態」として表現する
Governance connection

allocation readiness は、Royalty OS や governance layer への橋渡しです。

そのため、Dashboard 側では
次のような signal を渡せると自然です。

allocation_status
attribution_confidence
evidence_strength
trace_continuity
dispute_status
anomaly_flags
allocation_note
proposed allocation ratio

これにより、後段制度は
“生ログ”ではなく、整理済みの観測判断材料を受け取れます。

What this document does not do

この文書は、以下を直接定義しません。

支払ルールそのもの
法的権利確定
分配比率アルゴリズムの最終版
審査機関の制度設計
通貨やQコインの清算方法

ここで定義するのは、
あくまで 「返しやすい状態とは何か」 です。

Summary

allocation readiness の本質は、
価値そのものを測ることではなく、

観測された価値を、今どれだけ安全かつ説明可能に返しうるか

を示すことにあります。

より短く言えば、

score measures value signals.
readiness measures return preparedness.

この区別があることで、
Seismic Score Dashboard は
“高得点＝即分配” という危うい短絡を避けられます。
