# Buildability Framework

Public methodology for the Buildable Report scoring system.

Published by [NXLV](https://nxlv.ai). Authored by Lucio Amorim.

---

## What this repository contains

- Scoring philosophy and public rubric definitions
- Score-band interpretations
- Evidence policy and standards
- Versioning model and changelog
- Public glossary

This repository exposes enough of the methodology to make it **credible,
auditable and comparable across reports** — without exposing private prompt
chains, agent instructions or proprietary calibration pipelines.

---

## Framework v1.1 — Current

**Status:** Shipped and live on [buildable.report](https://buildable.report)

### The three dimensions

Every Buildable Report produces three independent scores:

| Dimension | What it measures | Scale |
|-----------|-----------------|-------|
| **Buildability Index** | How legible and reconstructible the visible product surface is under current AI-native development conditions | 0–100 |
| **Moat Density** | What survives after the visible surface is understood or reconstructed | 0–100 |
| **Lovability Fit** | How cleanly the product or workflow translates into a Lovable-native build path | 0–100 |

The three scores are **independent**. Do not collapse them into a single verdict.
The analytical value lives in the relationship between the three.

### How scores are produced (v1.1)

In Framework v1.1, scores are produced by a language model acting as a
structured evaluator. The model receives:

- The product's public URL and name
- Scraped public surface data (landing page, public feature descriptions,
  pricing page, public integrations)
- A system prompt specifying the three dimensions, their definitions, scoring
  orientation and evidence rigor requirements

The model returns:
- A numeric score (0–100) for each dimension
- Verdict band classification
- Classified evidence: observed / inferred / speculated
- Moat category breakdown
- Narrative for each dimension
- A seed prompt / build brief

Weights used for v1.1 were derived through operator elicitation across real
Lovable build sessions. **Specific weights are not published** (private
calibration). The classification rubric for each dimension is described in the
sections below.

> **Transparency note:** v1.1 asks the model to produce scores directly,
> using its internal representation of the rubric. This is reliable for
> consistent band-level verdicts but introduces model-level variance at the
> exact-score level. Framework v1.2 (see roadmap) will replace this with
> atomic evidence classification and mechanical score derivation to reduce
> that variance and make the scoring fully auditable criterion by criterion.

### Score bands

#### Buildability Index

| Band | Range | Label |
|------|-------|-------|
| ONE SHOT | 85–100 | Highly legible, standard stack, AI-native by default |
| SHIP IT | 70–84 | Clear surface, achievable with one strong AI-native sprint |
| READY | 50–69 | Reconstructible with meaningful effort |
| RETHINK | 20–49 | Complex surface, significant build challenges |
| WRONG TOOL | 0–19 | Out of scope (hardware, biotech, regulated infra, data-plane businesses) |

#### Moat Density

| Band | Range | Label |
|------|-------|-------|
| Very High | 80–100 | Multiple compounding moats; distribution + data + trust |
| High | 60–79 | Clear defensibility; at least two strong moat categories |
| Moderate | 40–59 | Some moat; defensibility exists but narrow |
| Low | 20–39 | Thin moat; mostly surface; switching costs minimal |
| Minimal | 0–19 | Surface only; fully substitutable |

#### Lovability Fit

| Band | Range | Label |
|------|-------|-------|
| Strong Fit | 80–100 | Translates cleanly; standard stack; AI-native by default |
| Good Fit | 60–79 | Translates well with known effort |
| Partial Fit | 40–59 | Achievable but requires significant iteration |
| Weak Fit | 20–39 | Difficult translation; complex integrations or non-standard stack |
| No Fit | 0–19 | Out of scope for Lovable-native build |

### Evidence policy

Reports separate evidence into three tiers:

- **Observed** — directly visible from public product surface (landing page,
  published pricing, public feature list, public integrations)
- **Inferred** — reasonably derived from observed signals (funding stage →
  likely team size; stated enterprise clients → likely compliance requirements)
- **Speculated** — plausible but not derivable from public evidence

Rules:
- Observed evidence may directly affect scoring.
- Inferred evidence affects scoring only where the rubric permits inference.
- Speculation must not materially raise a score.
- External research (funding, headcount, news, market position) is used when
  scoring depends on it. Sources are cited.
- Stale information is excluded or marked.

### Evidence basis declaration

Every report declares its evidence basis from:

```text
Landing page only
Landing page + public sources
Authenticated product access
Founder-provided material
Operator test build
```

### Moat categories tracked (v1.1)

```text
proprietary data          distribution
trust and brand           switching costs
workflow entrenchment     network effects
regulatory / compliance   integrations
accumulated ops context   enterprise procurement friction
service / implementation depth
```

---

## Framework v1.2 — Roadmap

**Status:** Planned. Not yet implemented.

### What changes in v1.2

v1.2 introduces **deterministic rubric scoring** to replace the direct
model-estimated scores of v1.1.

The model's role changes from "estimate a score" to "classify evidence."
The score is then **derived mechanically** from those classifications.

```text
v1.1: LLM → score (direct)
v1.2: LLM → evidence classifications → score (derived mechanistically)
```

### Atomic scale (v1.2)

Each rubric criterion is scored on:

```text
0 = Not evidenced / absent
1 = Partial / weak / inferred
2 = Strong / observed / structurally relevant
```

Use a 0–3 scale only where a two-level scale cannot capture the criterion.
Avoid 1–10 scoring at criterion level.

Score normalization:
```text
dimension_score = raw_points_obtained / raw_points_possible * 100
```

### Backtest plan (v1.2)

When v1.2 ships, a backtest will run:

```text
companies: 12 initial products
models:    ≥3
runs/model: ≥3
temperature: controlled and documented
outputs:
  - exact score variance per company
  - verdict-band stability
  - criterion-level variance
  - model disagreement map
  - unstable criteria list
  - confidence calibration
```

Target stability thresholds:

```text
±20 pts = unstable / research-only
±15 pts = acceptable for early v0
±10 pts = publishable
±5  pts = excellent / rare
```

Verdict-band stability is more important than exact-score stability.

Goal: operational reliability and methodological transparency, not scientific
certainty. Uncertainty is logged, not hidden.

---

## Versioning model

Every report declares a framework version. Scores are comparable only within
the same major framework version unless a migration or recalibration note
exists.

Version format: `v<major>.<minor>` (e.g. `v1.1`, `v1.2`).

When deterministic rubrics replace looser scoring, treat it as a minor version
bump within a major. Breaking changes to score bands or dimension definitions
are major version bumps.

---

## Glossary

| Term | Definition |
|------|-----------|
| **Buildable Report** | The full name of the project and publication. |
| **Buildability Index** | The primary score measuring surface legibility and reconstructibility. High ≠ weak company. |
| **Moat Density** | The defensibility score. What survives after the surface is reconstructed. |
| **Lovability Fit** | The Lovable-translation score. An NXLV methodology, not an official Lovable certification. |
| **Evidence Basis** | The stated source tier for a report's analysis. |
| **Confidence Band** | The qualitative verdict range (e.g. ONE SHOT, SHIP IT, READY). |
| **Seed Prompt** | A sanitized AI-native build brief derived from a public report. |
| **Build Brief** | Synonym for Seed Prompt. Preferred in some contexts. |
| **Framework Version** | The versioned rubric under which a report was scored. |
| **Observed** | Evidence directly visible from public product surface. |
| **Inferred** | Evidence reasonably derived from observed signals. |
| **Speculated** | Plausible but not derivable from public evidence. |

---

## Disclaimer

Buildability Framework is published by NXLV.

Lovability Fit is an NXLV methodology. It is not an official Lovable product,
certification, endorsement or audit.

This repository discloses methodology for transparency and comparability. It
does not expose private prompt chains, proprietary calibration weights or
agent instructions.
