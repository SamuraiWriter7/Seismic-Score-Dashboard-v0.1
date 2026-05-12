# Relationship to Trace Architecture

## Purpose

この文書は、**Seismic Score Dashboard v0.1** と **Trace Architecture** の関係を整理するための接続文書です。

Seismic Score Dashboard は、痕跡を自力で生み出す仕組みではありません。  
一方、Trace Architecture は、痕跡を記録することに強いが、それ自体では価値の意味づけや観測の要約を完結しません。

両者は役割が異なります。

- **Trace Architecture** は、痕跡を記録する
- **Seismic Score Dashboard** は、記録された痕跡を読んで整理する

本書の目的は、この二つを競合概念ではなく、**下層の記録層と上層の観測層**として明確に接続することです。

---

## Short answer

ひとことで言えば、

**Trace Architecture は「痕跡の記録層」、Seismic Score Dashboard は「痕跡の読解層」である。**

前者は何が起きたかを残す。  
後者は残されたものから、何が起点で、どこで共鳴し、どこまで還元準備が整っているかを読む。

---

## Why this distinction matters

AI時代の価値循環では、しばしば次の二つが混同されます。

### 1. 痕跡が存在すること
ある知が参照され、検索され、引用され、再利用され、派生の中に組み込まれたこと。

### 2. 痕跡の意味が読めること
その痕跡が、震源・共鳴・構造純度・還元可能性の観点からどういう意味を持つかを判断できること。

この二つは同じではありません。

ログが大量に残っていても、

- どの痕跡が重要か分からない
- どの利用が新規で、どれが再利用か分からない
- どの派生が深い共鳴で、どれが単純複製か分からない
- 誰が起点か見えない

という状態なら、観測としてはまだ不十分です。

だからこそ、  
**痕跡を記録する層**と**痕跡を読む層**を分ける必要があります。

---

## Layered relationship

両者の関係は、次のように整理できます。

```text
Observed events / provenance records
        ↓
Trace Architecture
        ↓
Seismic Score Dashboard

より丁寧に書けば、こうです。

access events / citation logs / provenance chains / derivative links
        ↓
structured trace recording
        ↓
score interpretation / dashboard observation / readiness reading

つまり、

イベントが起きる
Trace Architecture がそれを構造化して記録する
Seismic Score Dashboard がその構造化痕跡を読み、価値循環の形を観測する

という流れです。

What Trace Architecture does

Trace Architecture が担うのは、主に次のような機能です。

1. Access Trace

どの知が、いつ、どこで、どのようにアクセス・参照されたかを記録する。

例:

request event
retrieval event
ingestion event
cache reuse event
search reference event
2. Influence Trace

どの知が、どの派生物や後続表現に影響したかを記録する。

例:

citation links
derivative relationships
reinterpretation links
composition references
multi-source influence chains
3. Audit Trace

後から検証するための監査情報を記録する。

例:

provenance chain
event timestamp
source identifiers
confidence marks
review annotations
dispute metadata

つまり、Trace Architecture は
何が起きたかを痕跡として残す基盤です。

What Seismic Score Dashboard does

Seismic Score Dashboard が担うのは、主に次のような機能です。

1. Origin を読む

記録された痕跡から、どの知が起点として強いかを観測する。

2. Trace を読む

利用量・参照量・再利用量を可視化する。

3. Resonance を読む

どこで派生や横断的な共鳴が起きたかを整理する。

4. Purity を読む

その知がどれだけ再利用しやすい構造を持っているかを示す。

5. Return Readiness を読む

制度的な還元候補としてどれだけ整っているかを観測する。

つまり、Seismic Score Dashboard は
痕跡に意味の輪郭を与える観測面です。

The key difference

最も重要な違いはここです。

Trace Architecture

「何が起きたか」を残す

Seismic Score Dashboard

「起きたことが何を意味するか」を読む

前者は記録。
後者は観測。

前者は履歴。
後者は要約と解釈。

前者は材料。
後者は計器盤。

この違いを曖昧にすると、

ログがあるだけで観測できている気になる
痕跡量と価値の意味づけを混同する
記録の粒度不足をスコアでごまかす
ダッシュボードの見やすさだけが先行して根拠が弱くなる

という問題が起きます。

Why the dashboard depends on trace quality

Seismic Score Dashboard は、見た目は上位レイヤーですが、
実際には Trace Architecture の質に強く依存します。

理由は単純です。
入力される痕跡が粗いと、観測も粗くなるからです。

If trace is weak:
起点判定が曖昧になる
利用量が過少または過大に見える
派生深度が正しく読めない
cache と新規消費を区別できない
dispute 状態を観測に反映できない
If trace is strong:
Origin の推定が強くなる
Trace の信頼性が上がる
Resonance の深さを測りやすくなる
Return readiness を制度的に扱いやすくなる

つまり、

bad traces produce decorative dashboards
good traces produce meaningful dashboards

です。

Trace as upstream dependency

Seismic Score Dashboard は、Trace Architecture を
**upstream dependency（上流依存層）**として持つのが自然です。

Upstream examples
access trace logs
citation records
provenance statements
derivative relationship graphs
ingestion logs
audit notes
anomaly metadata
dispute metadata

Dashboard はこれらを消費して、
各スコア層へ変換します。

Data flow between the two

両者のデータ接続は、次のように整理できます。

Inputs from Trace Architecture into Seismic Score Dashboard
source identifiers
event timestamps
citation events
ingestion events
derivative edges
provenance chain strength
cache reuse records
anomaly hints
dispute tags
Outputs from Seismic Score Dashboard
origin_score
trace_score
resonance_score
purity_score
return_score
seismic_score
anomaly flags
readiness signals
creator / user / platform view summaries

つまり、Trace Architecture は
生の痕跡または半構造化痕跡を渡し、
Dashboard はそれを観測可能な座標へ整形して返します。

Example flow

典型的な流れは、次のようになります。

Step 1: Event occurs

ある記事、仕様書、図、GPT instruction、リポジトリなどがAIや人間に参照される。

Step 2: Trace Architecture records it

アクセス、検索、引用、派生、再利用、監査情報が記録される。

Step 3: Seismic Score Dashboard aggregates the traces

記録された痕跡を集約し、

起点性
利用量
共鳴度
構造純度
還元準備性

を観測可能なスコアへ変換する。

Step 4: Governance / Allocation layers may use the output

必要であれば、その観測結果が後続の governance や Royalty OS に引き渡される。

Example cases
Case A: Rich traces, clear dashboard
access logs: 十分
citation links: 明確
provenance chain: 強い
derivative edges: 整っている

この場合、Dashboard は比較的信頼性の高い観測を行えます。

Case B: Many accesses, poor provenance
access logs: 多い
provenance chain: 弱い
derivative metadata: 不完全

この場合、Trace Score は高く見えても、Origin や Return は不安定になります。

Case C: Strong provenance, little usage
provenance chain: 強い
access logs: 少ない
derivative links: 少ない

この場合、Dashboard は「静かな震源候補」として読めます。
記録が少ないのではなく、利用がまだ少ないだけかもしれません。

Case D: High derivative count, copy-like structure
derivative edges: 多い
semantic transformation: 小さい
repeated structural similarity: 高い

この場合、Trace Architecture は派生リンクを記録し、
Dashboard 側で copy-derivative discount をかける、という役割分担が自然です。

Conceptual formula

関係を短く書けば、こうです。

Event → Trace → Observe

もう少し拡張して書くなら、

Access / Influence / Audit
        ↓
Trace Architecture
        ↓
Seismic Interpretation

さらに後段を含めるなら、

Event → Trace → Score → Govern → Return

となります。

What Trace Architecture should not assume

Trace Architecture 側が前提にしてはいけないこともあります。

1. More logs means more value

ログ量が多いこと自体は価値を意味しません。

2. Every derivative edge is meaningful resonance

派生リンクがあるからといって、深い共鳴とは限りません。

3. Recording equals interpretation

記録しただけで意味が読めたことにはなりません。

4. Provenance completeness is always available

完全な provenance が常に取れるとは限りません。

What Seismic Score Dashboard should not assume

逆に、Dashboard 側も越権してはいけません。

1. It should not invent traces that do not exist

存在しない痕跡を推測で補ってはなりません。

2. It should not treat incomplete traces as certainty

記録不足なのに確定的に見せてはいけません。

3. It should not replace audit logs

ダッシュボード表示は監査記録そのものの代わりではありません。

4. It should not collapse trace diversity into one crude score

複数種の痕跡を雑に一数字へ押し込んではなりません。

Governance implications

Trace Architecture と Dashboard の分離は、
ガバナンス上も重要です。

理由は、後から争いが起きたときに、

何が記録されていたか
どう観測されたか
どのスコアにどう反映されたか

を切り分けて検証できるからです。

この切り分けがないと、

ログの誤り
解釈の誤り
UIの誤誘導
分配の誤り

がすべて一塊になり、修正が難しくなります。

Practical summary

実務的に言えば、両者の役割はこうです。

Trace Architecture
記録する
識別する
紐づける
時系列を残す
監査可能にする
Seismic Score Dashboard
読む
集約する
比較する
可視化する
readiness を示す

つまり、

Trace Architecture builds the memory.
Seismic Score Dashboard reads the memory.

Recommended repository posture

もし Seismic Score Dashboard を独立リポジトリとして置くなら、
Trace Architecture との関係は「内包」ではなく「互換的接続」として表現するのが自然です。

推奨表現例:

Seismic Score Dashboard consumes trace-oriented inputs from trace architectures
Trace Architecture provides structured event and provenance records
The dashboard interprets traces but does not replace trace capture

この書き方なら、Trace 側の仕様が独立していても、
上流接続先として自然に読めます。

Summary

Seismic Score Dashboard と Trace Architecture の関係は、
ひとことで言えば次の通りです。

Trace Architecture は痕跡を記録する。
Seismic Score Dashboard は記録された痕跡を観測し、意味の形を与える。

より簡潔に言えば、

Trace records.
Dashboard reads.

この順序があるからこそ、

観測は根拠を失わず
記録は意味を失わず
後続の governance や Royalty OS も土台を持てる

ようになります。
