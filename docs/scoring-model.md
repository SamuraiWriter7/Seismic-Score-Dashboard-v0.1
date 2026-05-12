# Scoring Model — Seismic Score Dashboard v0.1

## Purpose

この文書は、**Seismic Score Dashboard v0.1** における  
震源スコア算定モデルの考え方、構成、重み付け、減点、解釈指針を定義するものです。

本モデルの目的は、単純な人気指標を作ることではありません。  
目的は、知の価値循環を次の5層で観測し、**説明可能な形で可視化すること**です。

- Origin
- Trace
- Resonance
- Purity
- Return

---

## Design Goal

本スコアモデルが目指すものは、次の3点です。

### 1. 観測可能性
知の起点、利用、派生、構造品質、還元準備性を観測できること。

### 2. 説明可能性
なぜその総合点になったかを、各層の内訳として説明できること。

### 3. ガバナンス接続性
将来的な監査、異議処理、分配判断へ接続できる構造を持つこと。

---

## Scoring Philosophy

Seismic Score は、**「どれだけ目立ったか」**ではなく、  
**「どれだけ起点として成立し、どれだけ使われ、どれだけ響き、どれだけ返せる状態にあるか」**  
を測るためのモデルです。

したがって、以下の立場を明確に取ります。

- 閲覧数だけでは高得点にしない
- 引用数だけでも高得点にしない
- バズだけでは高得点にしない
- 起点が曖昧なら伸びにくくする
- 構造が崩れていれば伸びにくくする
- 未解決の異議がある場合は減衰させる

---

## Score Layers

総合震源スコアは、5つの観測層から構成されます。

---

### 1. Origin Score

## What it measures
その知が、どれだけ**起点として明確か**を示します。

## Typical signals
- first publication timestamp
- first publication platform
- originality delta
- structure consistency
- provenance chain strength
- origin confidence

## Interpretation
高い Origin Score は、  
その知が単なる派生や再包装ではなく、**震源候補としての強さ**を持つことを意味します。

## Non-goal
これは法的な著作権確定ではありません。  
あくまで、起点性の観測上の強さを示すものです。

---

### 2. Trace Score

## What it measures
その知が、どれだけ**利用・参照・取り込み**されたかを示します。

## Typical signals
- input tokens consumed
- output tokens generated
- cache tokens reused
- search reference count
- citation count
- RAG ingestion count
- agent task count

## Interpretation
高い Trace Score は、  
その知が広く実際に使われていることを示します。

## Important caution
ただし、利用量が多いこと自体は、起点性や純度の高さを保証しません。  
Trace は「消費量」であって、「正統性」や「深度」そのものではありません。

---

### 3. Resonance Score

## What it measures
その知が、どれだけ**次の知や派生構造を生んだか**を示します。

## Typical signals
- derivative count
- reinterpretation count
- cross-platform count
- continued reference rate
- downstream depth score

## Interpretation
高い Resonance Score は、  
その知が一度読まれて終わるのではなく、**派生・再定義・再実装の起点**になっていることを示します。

## Why it matters
AI時代の価値は、単純な閲覧よりも、  
**再利用と再生成の連鎖**の中で増幅されやすいためです。

---

### 4. Purity Score

## What it measures
その知が、どれだけ**構造的に明快で再利用しやすいか**を示します。

## Typical signals
- heading-body alignment
- definition clarity
- redundancy score
- Q&A decomposability
- diagrammability
- terminology stability
- structure_id presence

## Interpretation
高い Purity Score は、  
AIにも人間にも扱いやすい、**構造純度の高い知**であることを示します。

## Why it matters
同じ内容でも、構造が整理されている知ほど

- 引用しやすい
- 再要約しやすい
- 誤読されにくい
- 派生展開しやすい

という利点があります。

---

### 5. Return Score

## What it measures
その知が、どれだけ**還元候補として制度的に扱いやすいか**を示します。

## Typical signals
- attribution confidence
- evidence strength
- trace continuity
- dispute status
- allocation readiness

## Interpretation
高い Return Score は、  
その知が単に優れているだけでなく、**返す理由を制度的に持ちやすい状態**にあることを示します。

## Important caution
Return Score は、実際の支払いを意味しません。  
これは、分配や還元へ接続しやすい準備状態の観測です。

---

## Default Weight Model

v0.1 における初期重みは以下です。

| Layer | Weight |
|---|---:|
| Origin | 0.25 |
| Trace | 0.20 |
| Resonance | 0.20 |
| Purity | 0.20 |
| Return | 0.15 |

---

## Why these weights

### Origin = 0.25
最も重いのは Origin です。  
理由は、震源スコアが単なる人気スコアではなく、**起点性を中核に置くモデル**だからです。

### Trace = 0.20
使われていない知は循環しません。  
そのため Trace は重要ですが、起点性よりは一段軽くしています。

### Resonance = 0.20
AI時代では、派生を生む力そのものが価値になります。  
そのため Resonance も Trace と同等に扱います。

### Purity = 0.20
再利用しやすい構造は、今後さらに重要になります。  
そのため Purity は利用量や共鳴と同格です。

### Return = 0.15
Return は重要ですが、これは観測後段の層です。  
そのため、初期版では少し軽めに設定しています。

---

## Composite Formula

総合震源スコアは、以下の基礎式で算出します。

```text
seismic_score =
  (origin * 0.25) +
  (trace * 0.20) +
  (resonance * 0.20) +
  (purity * 0.20) +
  (return * 0.15) -
  penalty_total
Score Range
最小値: 0
最大値: 100

各層スコアは、合成前に 0–100 に正規化される前提です。

Penalty Model

総合点は、加点だけでなく減点も持ちます。
これは、スコアの不自然な膨張や誤認を抑えるためです。

Typical penalty factors
ambiguous attribution
weak provenance
duplication excess
structural breakage
short-term buzz bias
unresolved dispute
self-loop inflation
Why penalties matter

減点がないスコアモデルは、
簡単に人気投票や自己増幅ゲームへ崩れます。

Seismic Score は、観測指標であると同時に、
将来的な制度接続を想定するため、
不確実性と異常性を見える化する減点構造が必要です。

Recommended Interpretation Rules
Rule 1: Never read the total score alone

総合点だけを見て判断しないこと。
必ず 5 層の内訳と penalty をあわせて読むこと。

Rule 2: High trace does not equal high origin

たくさん使われていても、震源とは限りません。

Rule 3: High origin with low trace may indicate undeveloped potential

起点性が高いのに利用量が少ない場合、
未発見の震源である可能性があります。

Rule 4: High resonance with low purity may indicate unstable propagation

共鳴はしていても構造純度が低い場合、
誤読や劣化した派生が広がっている可能性があります。

Rule 5: High purity with low resonance may indicate reusable but undiscovered structure

構造は良いのに響いていない場合、
発見経路や接続面の不足が疑われます。

Rule 6: Low return with high other scores means governance friction

起点性・利用・共鳴が高くても Return が低い場合、
制度的な返し先の確定や証拠整備が追いついていない状態です。

Example Reading Patterns
Pattern A: Strong source origin
Origin: 高い
Trace: 中程度
Resonance: 中程度
Purity: 高い
Return: 中程度

解釈:
起点として強く、構造も良い。
まだ大規模循環には至っていないが、育つ震源候補。

Pattern B: Popular but weakly attributable
Origin: 低い
Trace: 高い
Resonance: 中程度
Purity: 中程度
Return: 低い

解釈:
広く使われてはいるが、起点や帰属が曖昧。
拡散物・まとめ・二次消費物の可能性が高い。

Pattern C: Quiet but structurally powerful
Origin: 高い
Trace: 低い
Resonance: 低い
Purity: 高い
Return: 中程度

解釈:
まだ注目は小さいが、構造的には強い。
今後の発見や引用で一気に伸びる可能性がある。

Pattern D: Resonant but unstable
Origin: 中程度
Trace: 高い
Resonance: 高い
Purity: 低い
Return: 低い

解釈:
派生は多いが、構造が粗く、帰属も弱い。
誤差やノイズを含んだ広がり方をしている可能性がある。

Derived Metrics

総合スコアのほかに、補助指標を併用することを推奨します。

1. SCI — Source Consumption Index
SCI =
  input_tokens_consumed +
  (output_tokens_generated * 0.5) +
  (cache_tokens_reused * 0.2)

用途:

消費量の概算把握
Trace層の補助指標
2. CFS — Citation Frequency Score
CFS = citation_count * source_quality_weight

用途:

質補正後の引用頻度把握
3. RDS — Resonance Depth Score
RDS =
  depth_1 * 1 +
  depth_2 * 2 +
  depth_3 * 3

用途:

派生の深さ把握
単発引用と多層派生の区別
4. PCS — Purity Composite Score
PCS =
  (
    heading_body_alignment +
    definition_clarity +
    qa_decomposability +
    diagrammability +
    terminology_stability
  ) / 5

用途:

構造純度の概観把握
Normalization Guidance

各層スコアは、元データの単位が異なるため、
そのままでは比較できません。

そのため、各指標は以下のいずれかで正規化することを推奨します。

fixed threshold normalization
percentile normalization
logarithmic scaling
capped weighted scaling
Recommended posture for v0.1

v0.1 では、まず単純で説明しやすい正規化を優先します。
精密さよりも、透明性と再現性を重視します。

Confidence and Uncertainty

スコアは、真理そのものではありません。
観測条件、収集範囲、参照可能ログ、プラットフォーム差異に依存します。

したがって、将来的には各スコアに対して

confidence band
uncertainty note
incomplete data flag

などを添える拡張が望まれます。

v0.1 では、これらは主に governance 側で補助的に扱います。

Anti-Overfitting Guidance

スコアモデルは、複雑にしすぎると誰も理解できなくなります。
一方で、単純すぎると簡単に悪用されます。

そのため v0.1 では、以下の姿勢を推奨します。

層構造は明快に保つ
重みは固定で始める
penalty は説明可能なものに限定する
派生指標は補助として扱う
総合点より内訳を重視する
Recommended UI Expression

ダッシュボード上では、次の表示が推奨されます。

Required
seismic_score
5 layer breakdown
penalty_total
dispute_status
attribution_confidence
Strongly recommended
trend over time
layer-by-layer history
anomaly flags
allocation readiness state
What this model should not become

このスコアモデルは、以下のようなものになってはなりません。

バズ競争のための数値
名声の序列化装置
単純なSEO代替指標
法的判定の代用品
自己引用ゲームの燃料

本モデルは、
価値循環の観測基盤であり、
制度的判断の補助線であるべきです。

Summary

Seismic Score Dashboard v0.1 のスコアモデルは、
知の価値を次の順で観測します。

起点として明確か
実際に使われたか
次の知を生んだか
再利用しやすい構造か
返せる状態にあるか

この5層を分解して見ることで、
「人気」と「価値循環」を混同せずに観測することが可能になります。
