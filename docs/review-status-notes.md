## `docs/review-status-notes.md`

```markdown
# Review Status Notes — Seismic Score Dashboard v0.1

## Purpose

この文書は、**Seismic Score Dashboard v0.1** における  
`review status` の考え方と、観測・審査・監査の関係を整理するための設計メモです。

Seismic Score Dashboard はスコアを表示しますが、  
そのスコアがどの程度レビューされたものかまで見えなければ、  
数値は過剰に信頼されやすくなります。

そのため v0.1 では、  
**「この record はどの程度レビューされたか」** を示す層が重要です。

---

## One-line definition

**Review status** とは、  
ある record または score が、どの程度機械的確認・人手確認・混合確認を経ているかを示す観測信頼状態である。

---

## Why this matters

同じ seismic_score でも、

- 完全自動集計の暫定値
- 人手監査を通過した値
- dispute を経て再確認された値

では、重みが違います。

もし review status が見えなければ、  
ユーザーはそれらを同列に見てしまいます。

その結果、

- 暫定値が確定値のように流通する
- dispute 中なのに安全に見える
- audit 未実施なのに権威づけされる

という問題が起きます。

だからこそ、  
score だけでなく **review status** を見える化する必要があります。

---

## Core idea

review status は、  
「この score が正しい」と保証するものではありません。

示すのは、

**この score が、どの程度の確認プロセスを通過したか**

です。

つまり、これは真理の証明ではなく、  
**確認の履歴を示すラベル**です。

---

## Relationship to other fields

review status は、以下の fields と特に近い関係にあります。

- `audit_status`
- `dispute_status`
- `attribution_confidence`
- `evidence_strength`
- `allocation_status`

ただし、それぞれ役割は異なります。

### audit_status
監査の種類・実施状態に近い

### dispute_status
争点の有無・進行状態に近い

### review_status
その record をどの程度レビュー済みと見なせるかの表示に近い

---

## Recommended statuses

v0.1 では、少なくとも以下の状態を使うと自然です。

### `unreviewed`
レビュー未実施。  
自動生成または初期集計のままの状態。

### `machine_reviewed`
機械的ルールや schema、異常検知などを通過した状態。

### `human_reviewed`
人手による確認・審査・判断を受けた状態。

### `mixed_reviewed`
機械確認と人手確認の両方を経た状態。

必要なら将来拡張として、

- `peer_reviewed`
- `governance_reviewed`
- `dispute_reviewed`

なども考えられますが、v0.1 では上記4種で十分です。

---

## What each status means

### `unreviewed`
意味:
- まだ誰も十分に確認していない
- 暫定観測値に近い

UI上の読み:
- 参考値
- 確定的に扱わない

---

### `machine_reviewed`
意味:
- schema validation
- anomaly detection
- required field checks
- basic consistency checks

などの自動確認を通過した

UI上の読み:
- 最低限の整合性はある
- ただし意味解釈は未成熟の可能性あり

---

### `human_reviewed`
意味:
- 人手による読み直し
- 帰属確認
- note / repo / revision の目視検証
- dispute 文脈の確認

などが行われた

UI上の読み:
- 一定の社会的・文脈的確認が入っている
- ただし最終制度判断とは限らない

---

### `mixed_reviewed`
意味:
- 自動確認と人手確認の両方が入っている
- v0.1 では最もバランスの良い確認状態

UI上の読み:
- 比較的信頼しやすい
- 後段の governance に渡しやすい

---

## Review status is not final truth

ここは重要です。

**review status が高いことは、最終真実の保証ではありません。**

それはあくまで、

- どの程度確認されたか
- どのような確認を経たか

を示すだけです。

したがって、

- `human_reviewed` でも dispute は起こりうる
- `mixed_reviewed` でも superseded はありうる
- `unreviewed` でも内容が正しいことはありうる

という理解が必要です。

---

## Recommended interpretation

### High score + unreviewed
→ 値は高いが、まだ慎重に読むべき

### Medium score + mixed_reviewed
→ 地味でも比較的安定した record の可能性

### High score + disputed + human_reviewed
→ 重要だが争点あり。慎重な扱いが必要

### Low score + human_reviewed
→ 単に価値が小さいのではなく、静かな一次震源かもしれない

---

## Relationship to allocation readiness

review status は allocation readiness に強く影響します。

一般に、

- `unreviewed` は readiness を上げにくい
- `machine_reviewed` は暫定候補を支える
- `human_reviewed` は review friction を下げる
- `mixed_reviewed` は最も readiness に接続しやすい

ただし、review status が高くても、

- dispute が強い
- attribution が弱い
- evidence が薄い

なら readiness は低いままです。

---

## Relationship to dispute handling

dispute がある場合、review status の意味はさらに重要になります。

### Example
- `dispute_status = pending`
- `review_status = unreviewed`

→ かなり危うい。観測は仮状態。

### Example
- `dispute_status = disputed`
- `review_status = mixed_reviewed`

→ 少なくとも争点は可視化され、確認も進んでいる。

つまり review status は、  
争いの有無だけでなく、**争いにどう向き合われたか** の手がかりになります。

---

## Review dimensions

review と一口に言っても、実際には複数の層があります。

### 1. Structural review
schema 整合、required fields、型、整合性など。

### 2. Trace review
ログ、時系列、引用、trace continuity の確認。

### 3. Attribution review
誰が起点か、共創か、寄与分離可能かの確認。

### 4. Governance review
dispute、保留、監査メモ、再計算要否などの確認。

v0.1 では、これらを細分化しすぎず、  
status label と note で扱うのが現実的です。

---

## Example cases

### Case A: Auto-generated first pass
- score は生成済み
- schema は通過
- 人手確認なし

推奨状態:
`machine_reviewed`

---

### Case B: Manual source inspection completed
- 初出URL確認済み
- revision確認済み
- disputeなし
- 人手確認あり

推奨状態:
`human_reviewed`

---

### Case C: Fully checked candidate for governance handoff
- schema通過
- anomaly確認済み
- attribution確認済み
- human review 済み

推奨状態:
`mixed_reviewed`

---

### Case D: Early-stage draft record
- 仮入力
- evidence未整備
- 自動チェックも未通過

推奨状態:
`unreviewed`

---

## Recommended UI posture

review status は、ダッシュボード上で  
総合点ほど大きくなくてもよいですが、必ず見えるべきです。

### Recommended visible elements
- review status badge
- last reviewed timestamp
- reviewer type
- evidence linked indicator
- dispute presence indicator

### Recommended display principle
- `unreviewed` は控えめだが明確に表示
- `mixed_reviewed` は最上位保証のように見せすぎない
- score のすぐ近くに status を置く
- allocation readiness と並べて誤読を防ぐ

---

## Suggested note fields

将来的には、review status に加えて  
以下のような補助 field があると強いです。

- `reviewed_at`
- `reviewed_by_type`
- `review_scope`
- `review_note`
- `review_version`

v0.1 では必須ではありませんが、  
運用上かなり役立ちます。

---

## What this document does not do

この文書は、以下を定義しません。

- 審査機関の正式制度
- 査読者資格
- 人手確認の詳細手順
- 監査プロトコル全文
- 法的確定の基準

ここで扱うのは、  
あくまで **review の見える化** です。

---

## Summary

review status の役割は、  
score の権威づけではありません。

本質は、

**この値が、どの程度確認されたものかを、誤解なく示すこと**

にあります。

より短く言えば、

**score shows the observation.  
review status shows how much that observation was checked.**

この区別があることで、  
Dashboard は見た目の強さではなく、  
観測の信頼段階まで伝えられるようになります。

---

## Next recommended document

次に自然につながる文書は、たとえば以下です。

- `docs/dispute-registry-relationship.md`
- `docs/allocation-readiness.md`
- `docs/audit-status-notes.md`
