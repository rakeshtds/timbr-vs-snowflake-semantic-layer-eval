# Timbr Ontology Semantic Layer vs Snowflake Semantic Views — Evaluation

**A structured, criteria-based evaluation of two ways to give LLMs and agents a governed semantic layer over enterprise data: Timbr.ai's SQL ontology layer, and Snowflake's native semantic views.**

## Overview

This repository holds the evaluation of Timbr — an ontology-based semantic layer that models concepts and relationships in SQL over the warehouse — against Snowflake semantic views, the native semantic layer used with Cortex Analyst and Cortex Agents. Both approaches aim at the same goal: let business users, LLMs and agents query enterprise data through governed business concepts instead of raw tables. The evaluation compared them on concept and relationship modeling, reusable semantic metrics, and LLM/agent query accuracy, using the same enterprise data and the same question sets against both layers.

## Problem

Choosing a semantic layer is a long-lived architectural commitment:

- It defines how business concepts (customer, policy, account) and their relationships are modeled once and reused everywhere.
- It is the contract every LLM and agent experience will query through — a weak layer cannot be fixed by a better model.
- The two candidate approaches differ fundamentally: an **ontology layer** (explicit concepts, hierarchies and relationships, queried in SQL) versus **semantic views** (metrics, dimensions and relationships defined natively inside Snowflake, consumed by Cortex Analyst/Agents).

The decision needed evidence on the same data and the same questions, not vendor demos.

## Architecture

```
            Enterprise data (same Snowflake estate)
                    │                       │
                    ▼                       ▼
        Timbr ontology layer      Snowflake semantic views
        (concepts, hierarchies,   (metrics, dimensions,
         relationships in SQL)     relationships, synonyms)
                    │                       │
                    └───────┬───────────────┘
                            ▼
              Evaluation harness (this repo)
        ├─ Modeling exercise: same concepts built both ways
        ├─ Metric reuse exercise: same metrics, defined once
        └─ Question set: identical NL questions to both layers
           via their LLM/agent interfaces; answers compared
           against governed expected results
```

- **Methodology** — how the comparison was designed so neither layer got home-field advantage (see `evaluation/methodology.md`).
- **Scorecard** — criterion-by-criterion qualitative ratings with the reasoning recorded (see `evaluation/scorecard.csv`).
- **Findings** — the balanced summary and the decision context (see `evaluation/findings.md`).

## Tech Stack

- Timbr.ai (SQL ontology semantic layer)
- Snowflake semantic views, Cortex Analyst, Cortex Agents
- SQL
- LLM/agent natural-language querying as the accuracy test surface

## Key Components

| Component | Description |
|---|---|
| `evaluation/methodology.md` | Evaluation design: shared data, shared question set, modeling and metric-reuse exercises, scoring approach. |
| `evaluation/scorecard.csv` | Criterion-by-criterion qualitative ratings for both approaches. |
| `evaluation/findings.md` | Balanced findings: where each approach is stronger, where each is weaker, and the resulting recommendation context. |

## How It Works

1. **Same data** — both layers were built over the same enterprise tables in Snowflake.
2. **Same concepts** — a fixed concept list (parties, accounts, policies, relationships between them) was modeled in both paradigms.
3. **Same metrics** — a set of business metrics was defined in each layer and checked for reuse across questions.
4. **Same questions** — an identical set of natural-language questions was put to both layers through their LLM/agent interfaces; generated SQL and answers were compared against governed expected results.
5. **Scoring** — each criterion was rated qualitatively (Strong / Adequate / Weak) with the evidence written down — deliberately no invented benchmark percentages.

## Outcomes

- A defensible, evidence-based comparison instead of competing vendor claims: the scorecard records *why* each criterion was rated as it was.
- The evaluation clarified the real trade-off: ontology-first modeling (richer explicit relationships, an extra governed layer to run) versus platform-native semantics (simpler operations inside Snowflake, relationships expressed within Snowflake's model).
- The findings fed directly into the semantic-layer standard for subsequent Cortex Analyst/Agent work, whichever layer a given domain adopted.

## Repo Structure

```
timbr-vs-snowflake-semantic-layer-eval/
├── README.md
└── evaluation/
    ├── methodology.md   # how the comparison was designed and run
    ├── scorecard.csv    # qualitative ratings per criterion
    └── findings.md      # balanced summary and decision context
```

## Note

Portfolio project based on production work in regulated financial services; code is a clean-room representative implementation with sample/synthetic metadata only.
