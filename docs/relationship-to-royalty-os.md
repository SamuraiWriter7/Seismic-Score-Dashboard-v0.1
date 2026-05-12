# Relationship to Royalty OS

## Purpose

この文書は、**Seismic Score Dashboard v0.1** と **Royalty OS** の関係を整理するための接続文書です。

Seismic Score Dashboard は、それ自体が分配を実行するOSではありません。  
また、Royalty OS は、観測なしに成立する分配OSでもありません。

両者は役割が異なります。

- **Seismic Score Dashboard** は、価値循環を観測する
- **Royalty OS** は、観測結果をもとに還元を制度化する

本書の目的は、この役割分担を明確にし、  
両者を競合概念ではなく、**前段と後段のレイヤー**として接続することです。

---

## Short answer

ひとことで言えば、

**Seismic Score Dashboard は「観測の計器盤」、Royalty OS は「還元の制度OS」である。**

前者は何が起きているかを見る。  
後者は見えたものをどう返すかを決める。

---

## Why this distinction matters

AI時代の価値循環では、しばしば次の2つが混同されます。

### 1. 価値が発生したこと
ある知が利用され、引用され、派生を生み、共鳴したこと。

### 2. 価値を返すべきこと
その知に対し、どのような還元や配分を行うべきかを制度として決めること。

この2つは同じではありません。

価値が発生していても、

- 起点が曖昧
- 証拠が弱い
- dispute が未解決
- 寄与が分離できない
- 分配ポリシーが存在しない

という状態なら、還元はまだ制度化できません。

だからこそ、  
**観測レイヤー**と**制度レイヤー**を分ける必要があります。

---

## Layered relationship

両者の関係は、次のように整理できます。

```text
Trace / Provenance Layer
        ↓
Seismic Score Dashboard
        ↓
Royalty OS

より丁寧に書けば、こうです。

origin / trace / provenance records
        ↓
score interpretation and dashboard observation
        ↓
allocation policy / royalty logic / governance decision

つまり、

Trace系が「痕跡を記録する」
Seismic Score Dashboard が「痕跡を読んで整理する」
Royalty OS が「何をどのように返すかを決める」

という役割分担です。

What Seismic Score Dashboard does

Seismic Score Dashboard が担うのは、次のような機能です。

1. Origin を見る

その知がどれだけ震源として明確かを見る。

2. Trace を見る

どれだけ消費・参照・取り込みが起きたかを見る。

3. Resonance を見る

どれだけ派生・再定義・横断共鳴が生まれたかを見る。

4. Purity を見る

どれだけ構造純度が高く、再利用しやすいかを見る。

5. Return Readiness を見る

制度的に返しやすい状態かどうかを見る。

つまり、Seismic Score Dashboard は
価値循環の状態を観測し、可視化し、整理するところまでを担います。

What Royalty OS does

Royalty OS が担うのは、次のような機能です。

1. Allocation policy

誰に、どの比率で、どの条件で返すかを決める。

2. Governance

異議、監査、保留、再計算、承認の流れを扱う。

3. Distribution logic

Qコイン、内部ポイント、金銭、クレジットなど、
どの形式で還元するかを決める。

4. Attribution handling

単一震源だけでなく、共創・共鳴・複数寄与の扱いを決める。

5. Settlement or record finalization

最終的な分配実行、もしくは分配記録の確定を行う。

つまり、Royalty OS は
観測結果を制度判断へ変換するOSです。

The key difference

最も重要な違いはここです。

Seismic Score Dashboard

「どんな価値循環が起きているか」を観測する

Royalty OS

「その価値循環にどう返すか」を制度化する

前者は認識。
後者は判断。

前者は可視化。
後者は配分。

前者は計器。
後者は制度。

この違いを曖昧にすると、

スコアがそのまま支払額のように誤読される
観測値が法的結論のように扱われる
高スコア＝即分配と誤認される
dispute や attribution の不確実性が無視される

という問題が起きます。

Why Seismic Score should not directly become payment

Seismic Score は重要ですが、
そのまま支払額や印税額に直結させるべきではありません。

理由は単純です。

スコアは観測値であり、制度判断そのものではないからです。

たとえば、ある対象が

高い Trace を持つ
高い Resonance を持つ
しかし Attribution が弱い
しかも dispute が pending

という場合、観測としては重要でも、
分配としてはまだ保留が妥当です。

つまり、

score ≠ payment

です。

より正確には、

score → input for governance → allocation decision

という順番になります。

Seismic Score as a pre-allocation layer

Seismic Score Dashboard は、Royalty OS にとって
**pre-allocation layer（分配前観測層）**として機能します。

この位置づけが自然です。

Why pre-allocation matters

分配を始める前に、少なくとも以下を見ておく必要があるからです。

震源がどこか
どれくらい利用されたか
どれくらい共鳴したか
出典信頼度が十分か
異議が残っていないか
二重計上の疑いがないか

これらを飛ばしていきなり返そうとすると、
Royalty OS は制度ではなく、ただの早押し装置になります。

Data flow between the two

両者のデータ接続は、次のように考えるのが自然です。

Upstream inputs into Seismic Score Dashboard
trace logs
provenance records
citation logs
ingestion records
derivative links
dispute metadata
audit status
Outputs from Seismic Score Dashboard to Royalty OS
seismic_score
layer breakdown
attribution_confidence
evidence_strength
trace_continuity
anomaly_flags
dispute_status
allocation_readiness
proposed allocation ratio
qcoin_estimate (optional)

つまり、Seismic Score Dashboard は
Royalty OS に対して観測済みの整理データを渡す立場にあります。

Example interpretation flow

典型的な接続フローは、次のようになります。

Step 1: Trace is recorded

ある知がAIに参照される。
トークン消費、引用、派生、再利用の痕跡が残る。

Step 2: Seismic Score Dashboard reads the traces

その痕跡を整理し、

起点性
利用量
共鳴
構造純度
還元準備性

をスコア化・可視化する。

Step 3: Governance checks the readiness

dispute 状態や attribution の強さを確認する。

Step 4: Royalty OS decides allocation logic

その対象を

分配候補にするか
保留するか
共創配分にするか
後続審査へ回すか

を決める。

Step 5: Distribution is executed or recorded

Qコイン、内部記録、金銭、クレジット等の形で還元処理を行う。

Example cases
Case A: High score, ready for allocation
Origin: 高い
Trace: 高い
Resonance: 高い
Purity: 高い
Return: 高い
dispute: none

この場合、Seismic Score Dashboard は
強い分配候補として Royalty OS に引き渡せます。

Royalty OS は比較的素直に allocation decision を下せます。

Case B: High resonance, low attribution confidence
Origin: 中程度
Trace: 高い
Resonance: 高い
Purity: 高い
Return: 低い
dispute: pending

この場合、Seismic Score Dashboard は
「重要だが制度判断にはまだ危うい」と示すべきです。

Royalty OS は、即分配ではなく

pending_review
withheld
shared allocation hypothesis

などの扱いを選ぶ可能性があります。

Case C: Quiet but clean origin
Origin: 高い
Trace: 低い
Resonance: 低い
Purity: 高い
Return: 中程度

この場合、まだ大きな利用はないが、
起点としての質は高いことが示されます。

Royalty OS の観点では、今すぐ大きな分配は発生しなくても、
将来の高価値候補としてマークする意義があります。

Governance bridge

Seismic Score Dashboard と Royalty OS のあいだには、
通常 governance bridge が必要です。

この橋渡しで扱うべきものは、たとえば以下です。

dispute status
audit status
attribution confidence threshold
anomaly handling
human review requirement
shared-source handling
superseded record handling

つまり、
Seismic Score Dashboard から Royalty OS へは
直接ジャンプするのではなく、
governance を経由して接続するのが健全です。

Conceptual formula

両者の関係を簡単な式で書くなら、こうです。

Observed value circulation
        ↓
Seismic interpretation
        ↓
Governance judgment
        ↓
Royalty allocation

あるいは、より短く書けば、

Trace → Score → Govern → Return

この4段が揃うことで、
印税OSはようやく制度として落ち着きます。

What Royalty OS should not assume

Royalty OS 側が前提にしてはいけないこともあります。

1. High score means final ownership

高スコアは最終所有権を意味しません。

2. High trace means clean attribution

利用量が多いからといって、起点が明確とは限りません。

3. High resonance means single-author claim

派生が多い場合、むしろ複数寄与の可能性があります。

4. No visible dispute means no uncertainty

異議が見えていなくても、観測範囲外の不確実性は残りえます。

What Seismic Score Dashboard should not assume

逆に、Dashboard 側も越権してはいけません。

1. It should not finalize payment

支払いを確定してはいけません。

2. It should not replace governance

異議審査や監査の代わりになってはいけません。

3. It should not collapse value into one number

すべての価値を総合点ひとつに還元してはいけません。

4. It should not pretend certainty where evidence is incomplete

証拠が弱いのに、確定的に見せてはいけません。

Why this relationship is important in the AI era

AI時代では、
「使われたこと」と「返すべきこと」のあいだに大きな空白があります。

従来の制度では、この空白はしばしばブラックボックスでした。

どこから学習したか分からない
どれだけ使われたか見えない
誰に返すべきか整理されていない
返す仕組み自体が存在しない

この空白を埋めるには、いきなり印税制度だけを作っても足りません。

まず必要なのは、
観測の地図です。

Seismic Score Dashboard は、その地図を与えます。
Royalty OS は、その地図をもとに道を作ります。

Practical summary

実務的に言えば、両者の役割はこうです。

Seismic Score Dashboard
観測する
比較する
可視化する
異常を示す
還元準備性を示す
Royalty OS
判断する
配分する
保留する
異議処理と接続する
分配記録を残す
Recommended repository posture

もし Seismic Score Dashboard を独立リポジトリとして置くなら、
Royalty OS との関係は「依存」ではなく「接続」として書くのが自然です。

推奨表現は次の通りです。

Seismic Score Dashboard is compatible with Royalty OS
Seismic Score Dashboard is designed as a pre-allocation observation layer
Royalty OS may consume dashboard outputs as governance-ready input signals

この書き方なら、
Seismic Score Dashboard が単独でも意味を持ちつつ、
Royalty OS とも自然につながります。

Summary

Seismic Score Dashboard と Royalty OS の関係は、
ひとことで言えば次の通りです。

Seismic Score Dashboard は価値循環を観測する。
Royalty OS は観測された価値循環を還元制度へ変換する。

より簡潔に言えば、

Dashboard sees.
Royalty OS decides.

この順序があるからこそ、

スコアは制度を急がせすぎず
制度は観測を無視しすぎず
価値循環はブラックボックスのまま放置されず

AI時代の還元構造に、最低限の秩序が生まれます。
