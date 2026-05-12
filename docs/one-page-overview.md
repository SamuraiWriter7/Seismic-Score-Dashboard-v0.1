# Seismic Score Dashboard v0.1 — One-Page Overview

## What this is

**Seismic Score Dashboard v0.1** is a draft specification for observing how knowledge:

- originates
- gets consumed
- resonates across platforms
- maintains structural purity
- becomes ready for return or allocation

It is not a payment engine itself.  
It is an **observation layer** that makes value circulation visible before distribution is decided.

---

## One-line definition

**Seismic Score Dashboard** is a governance-ready observation specification that measures origin, trace, resonance, structural purity, and return readiness in one shared coordinate system.

---

## Why it matters

In the AI era, value does not emerge only from finished works.

Value also emerges from:

- where an idea began
- how often it is consumed
- how deeply it propagates
- how clearly it can be reused
- how confidently it can be attributed

Most current systems only expose fragments of this picture:

- views
- clicks
- basic citations
- platform-side usage metrics

That is not enough.

What is needed is a shared observation model that connects:

**origin → trace → resonance → purity → return**

Seismic Score Dashboard is a minimal draft for that purpose.

---

## Core idea

The dashboard is built around five score layers.

### 1. Origin
Measures how clearly a piece of knowledge functions as a source point.

Examples:
- first publication timestamp
- first publication platform
- originality delta
- structure consistency
- provenance chain strength
- origin confidence

### 2. Trace
Measures how much consumption, referencing, or ingestion has occurred.

Examples:
- input tokens consumed
- output tokens generated
- cache tokens reused
- search reference count
- citation count
- RAG ingestion count

### 3. Resonance
Measures whether the knowledge generated further knowledge.

Examples:
- derivative count
- reinterpretation count
- cross-platform count
- continued reference rate
- downstream depth score

### 4. Purity
Measures how reusable and structurally clear the content is for humans and AI.

Examples:
- heading-body alignment
- definition clarity
- redundancy score
- Q&A decomposability
- diagrammability
- terminology stability

### 5. Return
Measures whether the record is ready to be treated as a distribution candidate.

Examples:
- attribution confidence
- evidence strength
- trace continuity
- dispute status
- allocation readiness

---

## Score formula

The draft composite score is:

```text
seismic_score =
  (origin * 0.25) +
  (trace * 0.20) +
  (resonance * 0.20) +
  (purity * 0.20) +
  (return * 0.15) -
  penalty_total

Important:

the total score should never stand alone
the breakdown of all five layers should be shown together
penalty factors should remain explainable
What makes this different

This specification does not treat value as simple popularity.

It is designed to distinguish between:

raw attention and deep resonance
temporary buzz and structural reuse
citation count and attribution confidence
consumption volume and return readiness

That makes it suitable as a pre-distribution observation layer for future governance or royalty-oriented systems.

Typical record shape

A seismic-score record contains:

source_id
source_type
title
origin
metrics
scores
governance
allocation

This allows one source object—such as an article, spec, repository, diagram, GPT instruction set, or book—to be observed in a consistent format.

Intended users
Creators

Use it to see:

which definitions or works have become origins
which structures are most reusable by AI
where resonance is actually occurring
Users

Use it to see:

which sources are closest to primary origins
which sources are clearer and more efficient
which sources offer better signal per cost
Platforms

Use it to see:

which records are strong distribution candidates
where attribution is weak
where disputes or anomalies may exist
how to avoid double counting and self-inflation
Governance posture

Seismic Score Dashboard is designed to be governance-ready, not governance-complete.

That means it assumes the need for:

auditability
anomaly detection
dispute handling
explainable scoring
anti-gaming controls

But it does not itself finalize legal ownership or execute payment.

It prepares the ground for those layers.

Anti-gaming principles

At minimum, the model should resist:

self-citation inflation
bursty artificial traffic
cache double counting
shallow copy derivatives
unresolved dispute masking
opaque score calculation

Without these controls, the system degrades into a vanity metric.
With them, it begins to function as a serious observation instrument.

Relationship to other systems

Seismic Score Dashboard fits naturally as a middle layer:

Trace systems record usage and provenance events
Seismic Score Dashboard organizes and interprets them
Royalty / allocation systems use that organized view to make return decisions

In other words:

trace records the movement
seismic score reads the movement
allocation decides what to do with it

Current repository contents

This repository currently defines:

a human-readable YAML specification
a JSON Schema for a single record
a sample JSON record
a GitHub Actions validation workflow

These files make the draft not only conceptual, but already validation-ready.

Current status
Version: 0.1.0
Status: draft

This is an early observation model.
It should be read as a foundation for future value-circulation infrastructure, not as a final institutional standard.

Next steps

Recommended next documents:

docs/scoring-model.md
docs/anti-gaming-rules.md
examples/seismic-score-dashboard.sample.yaml
collection-level schema for multiple records
visualization layer for dashboard rendering
allocation simulation model
Closing

Seismic Score Dashboard is not just a dashboard concept.

It is an attempt to make the following chain observable:

origin → trace → resonance → purity → return

That is the minimum structure needed if AI-era value circulation is to become measurable, explainable, and eventually governable.
