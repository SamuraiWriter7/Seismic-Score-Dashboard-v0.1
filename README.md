# Seismic Score Dashboard v0.1

A draft specification for observing origin, trace, resonance, structural purity, and return readiness in one shared coordinate system.

Seismic Score Dashboard is a governance-ready observation layer for value circulation in the AI era.  
It is designed to help creators, users, and platforms see the same structure from different viewpoints.

---

## Overview

**Seismic Score Dashboard v0.1** は、  
知の起点性・利用痕跡・共鳴・構造純度・還元可能性を、  
同一座標系で観測するための観測仕様です。

単なる人気ランキングではありません。  
これは、次の問いに答えるための**価値循環の計器盤**です。

- その知は、どこから始まったのか
- どれだけ使われたのか
- どれだけ次の知を生んだのか
- どれだけ再利用しやすい構造を持つのか
- どれだけ還元対象として扱えるのか

---

## One-line Definition

**震源スコア・ダッシュボード**とは、  
知の震源性・利用痕跡・共鳴・構造純度・還元可能性を同一座標系で観測し、  
価値循環の判断材料を提供するための観測UI仕様である。

---

## Triadic Circulation View

Seismic Score Dashboard は、発信者・利用者・プラットフォームの三者を、  
同じ価値地図の上で観測するための仕様です。

<p align="center">
  <img src="docs/triadic-circulation.svg" alt="発信者・利用者・プラットフォームの三者循環図" width="100%">
</p>

この図は、

- 発信者が震源を置き、
- 利用者がそれを選び、使い、共鳴し、
- プラットフォームが利用痕跡を保持し、
- Dashboard がその循環を読み取り、
- 後段の governance / Royalty OS が還元判断へ接続する

という全体の流れを示しています。

---

## Why This Exists

AI時代では、価値は「作品そのもの」だけでなく、  
**どの知が起点となり、どのように消費され、どこまで派生したか**によっても生まれます。

しかし現状の多くのシステムでは、見えているのは主に以下の一部だけです。

- 閲覧数
- クリック数
- 単純な引用数
- プラットフォーム側の内部消費量

それだけでは不十分です。  
必要なのは、**震源・痕跡・共鳴・分配可能性**をつなぐ観測構造です。

Seismic Score Dashboard は、そのための最小仕様として設計されています。

---

## Design Principles

本仕様は、以下の設計原則に基づきます。

### 1. Structure over Surface
表層的な人気や瞬間的なバズより、  
構造の明確性・再利用性・追跡可能性を重視します。

### 2. Trace before Reward
分配を先に決めるのではなく、  
まず利用痕跡と帰属信頼度を整えます。

### 3. Resonance over Raw Volume
単純な消費量だけでなく、  
再定義・再実装・継続参照などの深い共鳴を見ます。

### 4. Explainable Scoring
総合スコアは内訳に分解でき、  
なぜその点数なのかを説明可能でなければなりません。

### 5. Governance Ready
異議申し立て・監査・再計算・保留処理に耐えうる構造を前提とします。

---

## Scope

### This specification is for
- 知の震源性を観測すること
- 利用量と引用・派生を可視化すること
- 構造純度を定量化すること
- 将来的な還元・分配の準備状態を示すこと
- 発信者・利用者・プラットフォームが共通座標を持つこと

### This specification is not for
- 法的著作権判定の自動確定
- 真偽判定や思想の優劣判定
- 単純な人気投票
- 単一指標だけによる絶対評価

---

## Score Layers

震源スコアは、1つの数字だけでなく、  
**5つの観測層**として扱います。

### 1. Origin
その知が、どれだけ起点として明確か。

例:
- 初出日時
- 初出媒体
- 独自性差分
- 構造の一貫性
- provenance chain の強さ
- 起点信頼度

### 2. Trace
どれだけ利用・参照・取り込みが発生したか。

例:
- input tokens
- output tokens
- cache tokens
- search reference count
- citation count
- RAG ingestion count

### 3. Resonance
その知が次の知や派生構造をどれだけ生んだか。

例:
- derivative count
- reinterpretation count
- cross-platform count
- continued reference rate
- downstream depth score

### 4. Purity
AIや人間が扱いやすい構造純度をどれだけ持つか。

例:
- heading-body alignment
- definition clarity
- redundancy score
- Q&A decomposability
- diagrammability
- terminology stability

### 5. Return
分配対象として制度的に扱いやすいか。

例:
- attribution confidence
- evidence strength
- trace continuity
- dispute status
- allocation readiness

---

## Score Formula

v0.1 では、総合震源スコアは以下の基本式を採用します。

```text
seismic_score =
  (origin * 0.25) +
  (trace * 0.20) +
  (resonance * 0.20) +
  (purity * 0.20) +
  (return * 0.15) -
  penalty_total
Important note

総合点だけを見るのではなく、
各層スコアの内訳を必ず併記することを推奨します。

Penalty Model

スコアの不自然な膨張や不完全な帰属を防ぐため、
以下のような減点要因を想定しています。

ambiguous attribution
weak provenance
duplication excess
structural breakage
short-term buzz bias
unresolved dispute
self-loop inflation

この仕様は、人気の過剰評価ではなく、
説明可能な観測を目指します。

Repository Structure
.
├── README.md
├── LICENSE
├── spec/
│   └── seismic-score-dashboard-v0.1.yaml
├── schemas/
│   └── seismic-score-dashboard-v0.1.schema.json
├── examples/
│   └── seismic-score-dashboard.sample.json
├── docs/
│   ├── allocation-readiness.md
│   ├── anti-gaming-rules.md
│   ├── dispute-handling-notes.md
│   ├── dispute-registry-relationship.md
│   ├── governance-bridge-notes.md
│   ├── one-page-overview.md
│   ├── relationship-to-royalty-os.md
│   ├── relationship-to-trace-architecture.md
│   ├── review-status-notes.md
│   ├── scoring-model.md
│   ├── triadic-circulation.dot
│   └── triadic-circulation.svg
└── .github/
    └── workflows/
        └── validate-specs.yml
File guide
spec/seismic-score-dashboard-v0.1.yaml
人間が読むための原仕様です。
概念定義、設計原則、観測層、スコア構造、record model をまとめています。
schemas/seismic-score-dashboard-v0.1.schema.json
1件の seismic-score record を検証するための JSON Schema です。
実装・交換・自動検証の基準になります。
examples/seismic-score-dashboard.sample.json
Schema に適合するサンプルレコードです。
最小限の運用イメージを確認できます。
docs/one-page-overview.md
本仕様の全体像を短く把握するための概要文書です。
docs/scoring-model.md
Origin / Trace / Resonance / Purity / Return の5層スコアと、
合成式・解釈指針・補助指標を整理した中核文書です。
docs/anti-gaming-rules.md
自己循環引用、burst、copy-derivative、二重計上などへの防御原則を整理した文書です。
docs/relationship-to-royalty-os.md
Seismic Score Dashboard を、Royalty OS の前段にある観測層として位置づける接続文書です。
docs/relationship-to-trace-architecture.md
Trace Architecture を記録層、Dashboard を読解層として分離するための接続文書です。
docs/dispute-handling-notes.md
dispute を score と readiness にどう反映するかを整理した異議処理メモです。
docs/allocation-readiness.md
record がどの程度「返せる状態」にあるかを示す readiness の考え方を整理した文書です。
docs/review-status-notes.md
score がどの程度レビュー済みかを示す review status の設計メモです。
docs/dispute-registry-relationship.md
Dispute Registry を異議の台帳、Dashboard を影響表示層として切り分ける接続文書です。
docs/governance-bridge-notes.md
score / readiness / dispute / review を後段の制度判断へ安全に渡すための橋渡しメモです。
docs/triadic-circulation.dot
発信者・利用者・プラットフォームの三者循環図を定義する Graphviz ソースです。
docs/triadic-circulation.svg
README 表示用に出力した三者循環図です。
.github/workflows/validate-specs.yml
YAML spec の読込確認と、JSON Schema / sample record の自動検証を行う GitHub Actions workflow です。
Start Here

はじめて読む場合は、次の順番がいちばん分かりやすいです。

1. Quick entry

最初に全体像をつかみたい場合:

docs/one-page-overview.md
README.md

ここで、このリポジトリが
「価値循環を観測する仕様」 であり、
「分配そのものを実行するOSではない」
ことが分かります。

2. Core specification

仕様の中核を読みたい場合:

spec/seismic-score-dashboard-v0.1.yaml
docs/scoring-model.md
docs/anti-gaming-rules.md

ここで、

何を観測するのか
どうスコア化するのか
どう不正膨張を抑えるのか

が分かります。

3. Implementation entry

実装や検証から入りたい場合:

schemas/seismic-score-dashboard-v0.1.schema.json
examples/seismic-score-dashboard.sample.json
.github/workflows/validate-specs.yml

ここで、

record の形
検証対象
GitHub Actions 上での validation flow

を確認できます。

4. Governance-oriented reading path

制度接続や運用面を深く見たい場合:

docs/dispute-handling-notes.md
docs/allocation-readiness.md
docs/review-status-notes.md
docs/governance-bridge-notes.md
docs/dispute-registry-relationship.md

ここで、

異議がある場合どう扱うか
readiness をどう読むか
review 状態をどう見せるか
score をどう制度判断へ渡すか
dispute registry とどう接続するか

がつながります。

5. Relationship reading path

他のOSや記録層との接続を見たい場合:

docs/relationship-to-trace-architecture.md
docs/relationship-to-royalty-os.md
docs/dispute-registry-relationship.md
docs/governance-bridge-notes.md

ここで、Seismic Score Dashboard が

Trace Architecture の上に立つ観測層であり
Royalty OS の前段にある pre-allocation layer であり
Dispute Registry と接続する影響表示層であり
Governance Bridge を通って制度判断へ渡される

ことが整理できます。

6. Visual entry

最初に図から入りたい場合:

docs/triadic-circulation.svg
docs/one-page-overview.md
docs/scoring-model.md

この順番なら、
三者循環の全体像を見てから、仕様の骨格へ自然に入れます。

7. Minimal practical route

最短で仕様の雰囲気だけ掴みたい場合:

docs/one-page-overview.md
examples/seismic-score-dashboard.sample.json
docs/scoring-model.md

この3つだけでも、
「何を観測し、どんな record を持ち、どう読むのか」がだいたい見えます。

Specification Files
spec/seismic-score-dashboard-v0.1.yaml

人間が読める仕様の原本です。
概念、設計思想、観測層、スコア構造、レコードモデルを記述します。

schemas/seismic-score-dashboard-v0.1.schema.json

1件の震源レコードを検証するための JSON Schema です。
実装、交換、バリデーションの基準点になります。

examples/seismic-score-dashboard.sample.json

Schema に適合するサンプルレコードです。
最小限の運用イメージを確認するための例です。

.github/workflows/validate-specs.yml

GitHub Actions 上で spec / schema / sample を自動検証するワークフローです。

Record Model

1件の震源対象は、概ね以下の構造を持ちます。

source_id
source_type
title
origin
metrics
scores
governance
allocation
Origin

起点情報を記録します。

例:

author
first_published_at
platform
url
provenance hash
revision id
Metrics

利用・引用・派生・純度に関する観測値を記録します。

Scores

各層スコアと総合震源スコアを記録します。

Governance

帰属信頼度、証拠強度、異議状態、監査状態を記録します。

Allocation

将来的な還元対象としての準備状態や推定配分値を記録します。

Schema Usage

このリポジトリでは、
JSON Schema Draft 2020-12 を使用してサンプルレコードを検証します。

Requirements
Python 3.10+
jsonschema
Install
pip install jsonschema
Validate the sample locally
python - <<'PY'
import json
from pathlib import Path
from jsonschema import Draft202012Validator

schema_path = Path("schemas/seismic-score-dashboard-v0.1.schema.json")
sample_path = Path("examples/seismic-score-dashboard.sample.json")

with schema_path.open("r", encoding="utf-8") as f:
    schema = json.load(f)

with sample_path.open("r", encoding="utf-8") as f:
    sample = json.load(f)

Draft202012Validator.check_schema(schema)
validator = Draft202012Validator(schema)
errors = sorted(validator.iter_errors(sample), key=lambda e: e.path)

if errors:
    print("Validation failed:")
    for err in errors:
        path = ".".join(str(p) for p in err.path) or "(root)"
        print(f"- {path}: {err.message}")
    raise SystemExit(1)

print("OK: Seismic Score Dashboard sample is valid.")
PY
Render the triadic diagram locally
dot -Tsvg docs/triadic-circulation.dot -o docs/triadic-circulation.svg
What this validates

この検証では主に以下を確認します。

必須フィールドが存在するか
型が正しいか
enum 値が正しいか
数値範囲が妥当か
URI / date-time 形式が正しいか
余計なフィールドが混入していないか
GitHub Actions Validation

validate-specs.yml では、
spec / schema / sample を GitHub Actions 上で自動検証できます。

これにより、少なくとも以下を継続的に確認できます。

spec の読込破損
schema の破損
sample の不整合
誤ったフィールド追加
enum や required 定義の崩れ

ローカルで通ることと、リポジトリ上で通ることを揃えることで、
仕様の信頼性を高めます。

Minimum Viable Profile

v0.1 の最小構成として、以下の項目があれば
1件の震源レコードとして観測を開始できます。

source_id
title
origin.author
origin.first_published_at
origin.platform
origin.url
metrics.token_usage.input_tokens_consumed
metrics.token_usage.output_tokens_generated
metrics.citations.citation_count
metrics.resonance.derivative_count
scores.seismic_score
governance.attribution_confidence
allocation.allocation_status
Anti-Gaming Considerations

震源スコアは、設計を誤ると
「自作自演で膨らませた数値」にもなりえます。

そのため v0.1 の時点で、少なくとも以下を原則化します。

同一主体による自己循環引用は逓減加点とする
短時間大量参照は異常値として扱う
キャッシュ再利用は重みを下げる
単純複製は共鳴として過大評価しない
未解決異議がある場合は return 系を減衰させる
総合点には内訳と減点要因を添付する
Intended Views

同じデータでも、見る主体によって焦点は異なります。

Creator View
どの定義や記事が震源化しているか
どの構造がAIに消費されやすいか
どこで派生や共鳴が起きているか
User View
どの震源が一次情報に近いか
どのソースが明快か
どのソースがコスト効率に優れるか
Platform View
どの起点へどれだけ返すべきか
どのレコードが監査対象か
異常検知や二重計上防止をどう処理するか
Status
Version: 0.1.0
Status: draft

この仕様は初期段階の観測モデルです。
現時点では、制度の最終形ではなく、制度へ向かうための観測基盤として位置づけられます。

Roadmap

次に追加すると自然なもの:

複数レコード用の collection schema
可視化用ダッシュボード定義
allocation simulation 層の拡張
review / audit 補助フィールドの拡張
governance bridge と downstream handoff の明文化強化
Relationship to Royalty OS

Seismic Score Dashboard は、
直接分配を実行する OS ではありません。

これはむしろ、

何が震源か
どこまで痕跡が続いているか
どれだけ共鳴が起きたか
還元候補としてどれだけ準備が整っているか

を観測するための前段レイヤーです。

言い換えれば、

Trace 系仕様が「痕跡を記録する」
Seismic Score Dashboard が「痕跡を観測・整理する」
Governance Bridge が「制度判断へ整流する」
Royalty OS が「還元を制度化する」

という接続が想定されます。

License

この仕様書そのものの公開ライセンスは、
CC-BY-4.0 を想定しています。

リポジトリ全体の正式なライセンス運用は、
LICENSE ファイルで最終確定してください。

Closing Note

Seismic Score Dashboard は、
単なる分析画面の仕様ではありません。

これは、

問いを残し、痕跡を追い、震源を見つけ、利用を測り、還元へ接続するための観測層です。

人気の可視化ではなく、
価値循環の可視化へ。

その最小の一歩として、v0.1 をここに置きます。
