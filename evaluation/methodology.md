# Evaluation Methodology

How the Timbr ontology semantic layer and Snowflake semantic views were
compared, designed so that neither approach was tested on its own demo data
or its own favourite questions.

## Shared foundations

- **Same data.** Both layers were built over the same set of enterprise
  tables in the same Snowflake account — the same schemas, the same row
  content, the same naming problems.
- **Same concept list.** A fixed set of business concepts (party/customer,
  account, policy, producer, and the relationships among them) was agreed
  before modeling began. Each approach had to model all of them.
- **Same metric set.** A fixed list of business metrics (counts, balances,
  activity measures) was defined in each layer from the same written
  definitions.
- **Same question set.** Natural-language questions were written from real
  governance and analytics use cases *before* either layer was queried, and
  the identical set was put to both.

## Exercises

### 1. Concept and relationship modeling

Each concept and relationship on the agreed list was modeled in both
paradigms:

- Timbr: as ontology concepts with explicit hierarchies and relationship
  definitions, queried in SQL.
- Snowflake: as semantic views with tables, dimensions, facts and
  relationships.

Scored on: expressiveness (can the relationship be stated directly?),
modeling effort, and how the model reads to a new team member.

### 2. Reusable semantic metrics

Each metric from the agreed set was defined once per layer, then exercised
through questions that reuse it in different combinations (filtered,
grouped, time-shifted).

Scored on: define-once behaviour, composability across questions, and
whether the LLM/agent interface actually reused the governed definition
rather than re-deriving the calculation.

### 3. LLM / agent query accuracy

The identical question set was submitted to each layer through its
natural-language interface (Timbr's LLM interface; Cortex Analyst over the
semantic views). For each answer, reviewers checked:

- Was the generated query structurally correct (right concepts, joins,
  filters)?
- Did the answer match the governed expected result?
- On failure, was the failure a modeling gap, a language-understanding gap,
  or an ambiguity in the question itself?

## Scoring approach

- Ratings are **qualitative** — Strong / Adequate / Weak — per criterion,
  each backed by written evidence in the scorecard.
- No synthetic benchmark percentages were produced: the question set was
  sized for architectural decision-making, not for publishing accuracy
  statistics, and inventing precision the sample cannot support would
  mislead the decision.
- Reviewers scored both layers against the same rubric, and disagreements
  were resolved by re-running the underlying question or modeling step.

## Limitations

- The question set reflects one enterprise's governance and analytics use
  cases; results should not be generalised to unrelated workloads (e.g.
  pure BI dashboarding or operational reporting).
- Both products evolve quickly; the evaluation is a snapshot of the
  versions tested, recorded in the findings.
