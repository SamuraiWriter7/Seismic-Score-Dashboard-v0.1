# Relationship to Dispute Registry

## Purpose

この文書は、**Seismic Score Dashboard v0.1** と **Dispute Registry** の関係を整理するための接続文書です。

Seismic Score Dashboard は、異議の存在を見える化し、  
score や readiness に反映する観測層です。  
一方、Dispute Registry は、異議そのものを記録・追跡・更新するための制度寄りレイヤーです。

両者は役割が異なります。

- **Seismic Score Dashboard** は dispute を観測上どう扱うかを示す
- **Dispute Registry** は dispute そのもののライフサイクルを記録する

この違いを明確にするのが本書の目的です。

---

## Short answer

ひとことで言えば、

**Dispute Registry は「異議の台帳」、Seismic Score Dashboard は「異議を反映する観測面」である。**

前者は争点の記録層。  
後者は争点の影響表示層です。

---

## Why this distinction matters

もし Dashboard が dispute の詳細まで抱え込みすぎると、

- record が肥大化する
- 異議管理の履歴が不明瞭になる
- 状態遷移が雑になる
- score 表示と異議処理が混線する

逆に、Dispute Registry がないと、

- dispute の継続管理ができない
- いつ、誰が、何に異議を出したか追えない
- resolved / superseded の意味が曖昧になる
- Dashboard 側が「ただ揉めてる」表示で止まる

そのため、両者を分けることが重要です。

---

## Layered relationship

両者の関係は、次のように整理できます。

```text
dispute claims / objections / evidence updates
        ↓
Dispute Registry
        ↓
status and reference signals
        ↓
Seismic Score Dashboard

より短く言えば、

Dispute is registered there.
Dispute impact is shown here.

です。

What Dispute Registry does

Dispute Registry が担うのは、主に次のような機能です。

1. Dispute intake

異議の受付と登録。

2. Dispute identity

どの source / claim / record に関する異議かを識別する。

3. Lifecycle tracking

異議の進行状態を追跡する。

例:

submitted
pending
disputed
resolved
superseded
withdrawn
4. Evidence linkage

証拠、反証、revision、関連レコードを紐づける。

5. Governance handoff

必要に応じて review / audit / allocation decision に接続する。

つまり、Dispute Registry は
異議処理の台帳兼進行管理レイヤーです。

What Seismic Score Dashboard does

Seismic Score Dashboard は、Dispute Registry の代わりにはなりません。
担うのは次の役割です。

1. dispute_status を表示する

現在その record がどの状態かを示す。

2. readiness を慎重化する

未解決 dispute がある場合、allocation readiness を下げる。

3. penalty を適用する

必要に応じて return_score や総合 score へ減衰を反映する。

4. attention signal を送る

後段の governance / Royalty OS に注意喚起を行う。

つまり、Dashboard は
異議を観測へ反映するための翻訳面です。

The key difference

最も重要な違いはここです。

Dispute Registry

dispute そのものを記録し、追跡する

Seismic Score Dashboard

dispute が score や readiness にどう影響するかを示す

前者は台帳。
後者は計器盤。

前者は事件簿。
後者は警告表示。

Why Dashboard should not absorb the registry

Dashboard が registry 的役割まで抱えないほうがよい理由は明確です。

1. Separation of concerns

異議そのものの管理と、スコア観測は責務が違う。

2. Auditability

争点の履歴を独立に追えるほうが監査しやすい。

3. Reusability

Dispute Registry は、Dashboard 以外の systems にも使える。

4. Governance clarity

「異議が存在すること」と「その影響をどう表示するか」を切り分けられる。

Recommended connection model

自然な接続は、以下のような形です。

From Dispute Registry to Dashboard
dispute_id
related source_id
dispute_type
current status
severity hint
last_updated_at
linked evidence presence
superseded flag
From Dashboard perspective
dispute badge を表示
readiness を調整
penalty を適用
review を促す
allocation_status を慎重化

つまり、Dashboard は registry を
参照する側であるのが自然です。

Example flow
Step 1: Objection is raised

ある source に対して起点異議や寄与異議が提起される。

Step 2: Dispute Registry records it

dispute_id が発行され、type、status、evidence が記録される。

Step 3: Dashboard consumes the status

関連 source_id に対して dispute_status を反映する。

Step 4: Scores and readiness are adjusted

必要に応じて return_score や allocation_status が見直される。

Step 5: Resolution flows back

resolved / superseded 等の状態更新があれば、Dashboard も再反映する。

Example cases
Case A: Pending origin dispute

Registry:

dispute_type = origin
status = pending

Dashboard:

dispute badge 表示
allocation_status を pending_review
origin 解釈を慎重化
Case B: Resolved shared-attribution dispute

Registry:

status = resolved
note = shared contribution accepted

Dashboard:

dispute 履歴は残す
return_score を再計算
allocation note を更新
Case C: Superseded source claim

Registry:

status = superseded
linked new source record present

Dashboard:

旧 record の readiness を停止または減衰
新 record 側へ主な起点性を移す
Relationship to score layers

Dispute Registry の状態は、Dashboard 上では主に以下へ影響します。

Origin

起点争いがある場合、最も強く影響。

Resonance

派生の正当性争いがある場合に影響。

Return

ほぼ常に強く影響。特に unresolved dispute 時。

Trace

通常は値そのものを消さないが、二重計上や citation dispute があれば補正対象。

Relationship to readiness

Dashboard 上の allocation readiness は、
Registry の状態をかなり強く受けます。

none

通常フローへ進みやすい

pending

慎重化

disputed

原則として review 優先

resolved

内容に応じて通常化可能

superseded

旧対象は停止・修正対象

このように、Registry の状態は
Dashboard の readiness 制御にとって重要な upstream signal です。

Relationship to review status

review status と dispute registry も関連します。

dispute があるのに unreviewed なら危うい
dispute を経て mixed_reviewed なら安定度が増す
resolved 後の再レビュー有無は重要

したがって、Dashboard 側では
dispute_status と review_status を近く表示するのが自然です。

Recommended repository posture

もし Dispute Registry が独立リポジトリなら、
Seismic Score Dashboard 側では依存関係を次のように書くのが自然です。

Seismic Score Dashboard may consume dispute status signals from a dispute registry
Dispute Registry manages the lifecycle of objections and supersessions
The dashboard reflects dispute impact but does not replace dispute registration

この書き方なら、責務分離が明快です。

What Dispute Registry should not assume

Registry 側も、以下を前提にしすぎてはいけません。

dispute 登録 = score 低下の自動確定
pending = guilty
registry が ownership を即決できる
すべての異議が同じ重さを持つ

Registry はまず記録層であり、
影響の反映は Dashboard や governance 側で段階的に行うのが自然です。

What Dashboard should not assume

逆に Dashboard 側も、

dispute badge = 価値否定
resolved = 完全無謬
superseded = 履歴不要
registry 不在でも dispute を適当に埋めてよい

とは考えるべきではありません。

Practical summary

実務的に言えば、役割分担はこうです。

Dispute Registry
登録する
追跡する
状態更新する
証拠を紐づける
履歴を保持する
Seismic Score Dashboard
表示する
慎重化する
penalty を反映する
readiness を下げる
governance に橋渡しする

つまり、

Registry keeps the dispute alive as a record.
Dashboard makes its impact visible.

Summary

Dispute Registry と Seismic Score Dashboard の関係は、
ひとことで言えば次の通りです。

Dispute Registry は異議を記録する。
Seismic Score Dashboard は、その異議が観測にどう影響するかを示す。

より短く言えば、

Registry tracks the dispute.
Dashboard reflects the dispute.

この分離があることで、

異議は履歴として失われず
score は文脈を失わず
readiness は早計にならず
governance は後追いしやすくなる

ようになります。
