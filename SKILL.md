---
name: hr-grilling
description: Stress-test an HR-related plan, diagnosis, or decision through a dependency-aware interview. Separate facts, assumptions, and decisions; investigate retrievable facts instead of asking for them; challenge unsupported assumptions; and continue until the material decision space is explicit.
---

# HR Grilling

Sharpen an HR-related plan, diagnosis, or decision before action.

Do not rush from a vague request to a solution.

Map the subject as a **Decision Tree（决策树）** and work through it according to dependencies.

This skill owns the reasoning and interview method.

It does not own HR domain expertise.

# Activation

Activate when:

1. the user explicitly asks to grill, challenge, pressure-test, diagnose, or clarify an HR-related plan or decision; or
2. another HR Domain Skill（HR领域技能）calls this skill because material decisions, assumptions, or uncertainties must be resolved.

Do not activate merely because an HR topic exists.

Do not turn simple factual questions into interviews.

# Input Contract

When called by another skill, accept an optional **Context Package（上下文包）**.

Recommended fields:

```yaml
objective:
current_state:
facts:
assumptions:
current_proposal:
decisions_needed:
constraints:
evidence:
stakeholders:
```

Fields may be incomplete or omitted.

Do not reject an invocation because the package is incomplete.

Use available context first, then determine what truly requires investigation or human clarification.

When invoked directly by a user in natural language, construct the Context Package internally rather than requiring the user to fill a form.

# Core Principle

**Facts are the agent's job. Decisions belong to the responsible human.**

If information can reasonably be retrieved from available:

- documents;
- data;
- policies;
- systems;
- research;
- supplied context;

investigate it instead of asking the user.

Ask the user only when:

- a genuine human decision must be made;
- first-hand context is unavailable elsewhere;
- available evidence conflicts;
- ambiguity materially affects the decision.

Never disguise a decision as a factual question.

# Evidence Retrieval Rule

Use:

> **Retrieve when available. Surface when unavailable.**

When required evidence is directly accessible in the current environment, retrieve it.

Do not ask the user to manually provide information the agent can reasonably obtain itself.

When evidence cannot be accessed:

- do not invent it;
- do not block unnecessarily;
- record it explicitly as missing evidence;
- assess whether the decision can still proceed.

Do not require this skill to know which HRIS, spreadsheet, database, knowledge base, or external system contains the evidence.

Tool and system expertise may be supplied by the calling Domain Skill or runtime environment.

# Build the Decision Tree

Identify:

- the outcome being pursued;
- established facts;
- assumptions being relied upon;
- decisions that must be made;
- dependencies between decisions;
- material risks and trade-offs;
- evidence that could change the decision.

Do not use a fixed HR questionnaire.

The tree must emerge from the specific problem.

# Work the Frontier

The **Frontier（决策前沿）** contains unresolved decisions whose prerequisites are sufficiently settled.

Ask only frontier questions.

Questions in the same round must not depend on one another.

Ask a maximum of **3 questions per round**.

If the frontier contains more than 3 questions, prioritize by:

1. downstream impact;
2. irreversibility;
3. risk;
4. uncertainty.

After each round:

1. record what is settled;
2. update facts, assumptions, and decisions;
3. identify contradictions;
4. identify weak causal assumptions;
5. update missing evidence;
6. recompute the Decision Tree;
7. generate the next Frontier.

Later questions should become possible because earlier questions were answered.

# Separate Facts, Assumptions, and Decisions

## Fact

A claim supported by available evidence.

## Assumption

A claim currently treated as true but insufficiently supported.

## Decision

A choice an accountable human must make.

Never silently convert an assumption into a fact.

If a material decision depends on an assumption, expose that dependency.

# Evidence Basis

When reasoning toward a recommendation, distinguish:

## [Fact]

Evidence directly supported by data, documents, observed events, policy, systems, or another reliable source.

## [Principle]

A relevant professional, organizational, analytical, or design principle.

## [Inference]

A conclusion derived from facts and/or principles but not directly observed.

Never present an inference as a fact.

A recommendation may combine multiple evidence types.

Example:

**Recommended direction**

Consider segmenting customers by value and service complexity rather than geography alone.

**Basis**

- [Fact] High-value customers account for a disproportionate share of revenue.
- [Fact] Service workload differs materially across customer groups.
- [Principle] Large workload variation weakens uniform resource allocation.
- [Inference] Value plus service complexity is therefore likely to be more useful than geography alone as the primary segmentation dimension.

# Recommendation Gate

A recommendation must have an identifiable rationale.

## Evidence sufficient

Provide a provisional recommended direction and show its basis.

## Evidence incomplete but directional reasoning is possible

Provide a tentative recommendation.

Explicitly identify important assumptions and uncertainty.

## Evidence insufficient

State:

**No evidence-backed recommendation yet.**

Then specify:

- what evidence is missing; or
- what management choice cannot be made by the agent.

## Value or management choice

When reasonable alternatives depend primarily on:

- strategy;
- management preference;
- risk appetite;
- organizational values;

explain the trade-off without deciding for the responsible human.

# Professional Challenge

Default to **Professional Challenge（专业挑战）**.

Do not merely validate the user's current explanation.

Challenge:

- unsupported assumptions;
- premature solutions;
- weak causal claims;
- proxy metrics;
- contradictory objectives;
- hidden trade-offs;
- missing stakeholders;
- unclear success criteria.

Examples:

> Current evidence shows performance declined, but does not yet establish capability as the cause.

> This proposal assumes the workload problem is caused by headcount. What evidence rules out process or allocation problems?

The goal is not to oppose the user.

The goal is to improve decision quality.

# Red Team Escalation

Selected branches may escalate into **Red Team（红队压力测试）**.

Red Team can be triggered by:

1. an explicit user request; or
2. material risk indicators identified during the grilling process.

Risk indicators include:

- high impact;
- difficult or costly reversibility;
- weak supporting evidence;
- major stakeholder consequences;
- fairness concerns;
- compliance exposure;
- significant implementation risk.

## Automatic Trigger

Normally escalate a branch when **two or more material risk indicators** are present.

A single indicator may trigger escalation when it involves:

- material compliance or legal exposure;
- a decision that is especially difficult to reverse;
- another clearly severe consequence where the cost of error is unusually high.

Do not Red Team the entire conversation by default.

Apply it only to branches where the cost of being wrong justifies deeper scrutiny.

Red Team questions may include:

- If this decision fails, which assumption was most likely wrong?
- What evidence contradicts the preferred solution?
- Who could be disadvantaged by this design?
- How could this mechanism be gamed?
- What second-order behavior could this create?
- Which alternative explanation are we underweighting?
- What would make us reverse this decision later?

# Question Format

Use:

**Q<n> — <decision title>**

Explain briefly:

- what needs to be decided;
- why it matters;
- relevant options or trade-offs;
- current evidence and uncertainty.

When permitted by the Recommendation Gate:

**Recommended direction**

<recommendation>

**Basis**

- [Fact] ...
- [Principle] ...
- [Inference] ...

Questions in the same round must be independently answerable.

The user should be able to respond:

`1A; 2 agree; 3 disagree because...`

# Stop Condition

Continue until no material branch remains silently assumed.

Stop when:

- important decisions are settled or explicitly open;
- critical assumptions are visible;
- missing evidence is visible;
- major risks and trade-offs are understood;
- additional questioning is unlikely to materially change the decision.

Do not continue asking questions merely to appear thorough.

# Final Output

End with an **HR Decision Brief（人力决策摘要）**.

## Objective

What outcome is being pursued.

## Facts

What is currently supported.

## Assumptions

What remains unverified.

## Decisions

What has been decided.

## Open Decisions

What still requires a human choice.

## Evidence Needed

What information could materially change the decision.

## Risks & Trade-offs

The important consequences and tensions.

## Validation

How the decision will later be evaluated.

# Return Status

When called by another skill, return one primary machine-readable status:

```text
READY
NEEDS_EVIDENCE
NEEDS_HUMAN_DECISION
```

## READY

The calling skill has enough clarity to continue its workflow.

This does not mean uncertainty is zero.

It means remaining uncertainty is not material enough to block the next step.

## NEEDS_EVIDENCE

A material decision cannot responsibly proceed until additional evidence is obtained.

## NEEDS_HUMAN_DECISION

The required next step is a genuine management, HR, business, strategic, or value judgment that should not be made by the agent.

# Blockers

A case may contain multiple blockers at the same time.

When called by another skill, return a `blockers` list alongside the primary status.

Example:

```yaml
status: NEEDS_EVIDENCE

blockers:
  - type: evidence
    item: Customer service workload by segment

  - type: human_decision
    item: Whether growth or profitability is the primary business priority
```

Allowed blocker types should remain simple:

```text
evidence
human_decision
```

Do not create a complex workflow state machine unless a later use case demonstrates a real need.

## Primary Status Selection

When several blockers coexist, choose the primary status according to what most directly blocks responsible progress.

Do not hide secondary blockers merely because a primary status has been selected.

The `blockers` list is the complete visible record of material blockers.

# Human vs Skill Output

## Direct human use

When the user directly invokes `hr-grilling`, prioritize a natural conversational experience.

Return:

- the grilling dialogue;
- the final HR Decision Brief.

Do not expose machine-oriented state unless it materially helps the user.

## Skill-to-Skill use

When another Domain Skill invokes `hr-grilling`, return:

1. the HR Decision Brief;
2. `status`;
3. `blockers`.

Example:

```yaml
status: NEEDS_HUMAN_DECISION

blockers:
  - type: human_decision
    item: Define whether the role prioritizes short-term revenue or strategic account development
```

This enables the calling skill to decide whether to:

- continue;
- retrieve more evidence;
- pause for human judgment;
- re-enter `hr-grilling`.

# Scope Boundary

This skill owns:

- dependency-aware questioning;
- assumption exposure;
- evidence classification;
- evidence-gap detection;
- professional challenge;
- selective Red Team testing;
- decision clarification;
- decision summarization;
- readiness signalling;
- blocker identification.

This skill does not own:

- recruiting methodology;
- organization design methodology;
- talent development methodology;
- performance methodology;
- employee-relations expertise;
- compensation expertise;
- workforce-planning expertise;
- employment-law interpretation;
- persistent project documentation.

Domain Skills should supply relevant professional context and call this skill when structured decision clarification is required.

Persistent documentation belongs in a separate skill such as `hr-grilling-with-docs`.

# Design Principle

Keep this skill thin.

Do not add domain-specific checklists merely because a particular HR case exposed a new question.

Before modifying this skill, ask:

> Is this a reusable decision-reasoning rule, or does it belong to a Domain Skill?

If it belongs to a domain, keep it out of `hr-grilling`.

The purpose of this skill is not to know every HR answer.

Its purpose is to make weak assumptions, missing evidence, unresolved decisions, and hidden trade-offs difficult to ignore.
