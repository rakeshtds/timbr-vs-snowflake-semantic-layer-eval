# Findings

A balanced summary of the evaluation. Ratings referenced here are the
qualitative scorecard ratings in `scorecard.csv`; no benchmark percentages
were produced or are claimed.

## Where Timbr's ontology layer is stronger

- **Explicit relationships and hierarchies.** Concepts, class hierarchies
  and relationships are first-class, named parts of the model. For domains
  where the relationship structure *is* the business semantics — parties,
  policies, producers and their hierarchies — the ontology states directly
  what a semantic view expresses indirectly through joins.
- **SQL-native querying.** The ontology is queried in SQL, so the same
  semantic definitions serve BI tools, notebooks and applications, not
  only LLM interfaces.
- **Cross-domain reuse.** A shared ontology amortises its modeling cost
  when many domains query the same concepts; metrics and relationships are
  defined once, enterprise-wide.

## Where Snowflake semantic views are stronger

- **Zero additional platform.** Semantic views are native Snowflake
  objects: nothing extra to deploy, secure, patch or license-manage, and
  they inherit the platform's governance and release cadence.
- **Native Cortex fit.** Semantic views are the direct input to Cortex
  Analyst and Cortex Agents, so governed natural-language querying and
  agent experiences work out of the box.
- **Incremental adoption.** A semantic view can be built for one use case
  and extended; there is no up-front enterprise modeling programme to
  complete before value appears.

## Where both performed comparably

- **Concept and metric definition.** Both paradigms covered the agreed
  concept list and defined the metric set once, with reuse through their
  respective query interfaces.
- **LLM query accuracy on the shared question set.** Both produced
  structurally correct queries for the clear majority of questions.
  Reviewing the failures, the dominant cause on both sides was ambiguity
  in the question itself, not a modeling gap in either layer — a reminder
  that question governance (verified queries, synonyms, clear concept
  names) matters as much as layer choice.

## The real trade-off

The evaluation did not produce a universal winner; it produced a decision
rule:

- Choose the **ontology layer** when the enterprise's semantics are
  relationship-heavy, shared across many domains, and queried from many
  SQL surfaces — and the organisation will fund the up-front modeling.
- Choose **semantic views** when the priority is governed LLM/agent
  querying inside Snowflake with the least platform footprint and the
  fastest path to value per domain.

## Caveats

- Snapshot in time: both products evolve quickly, and the versions
  evaluated are those available during the evaluation.
- The question set reflects regulated financial-services governance and
  analytics use cases; other workloads may weight the criteria
  differently.
