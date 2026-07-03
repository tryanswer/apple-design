# Apple Design Agent Skill (Universal Runtime Spec)

## 0. Skill Identity (Agent-Compatible Manifest)

```yaml
name: apple-design-skill
version: 2.0.0
type: design-evaluator-generator
runtime_compatibility:
  - claude-code
  - codex
  - generic-agent
  - tool-using-llm
input_modes:
  - ui_spec
  - natural_language_prompt
  - wireframe_description
output_mode: structured_evaluation_and_improvement
```

---

## 1. Purpose

This skill converts Apple Design principles into a **portable, agent-executable design intelligence module**.

It enables agents to:

- Generate UI/UX under cognitive constraints
- Evaluate interface quality
- Detect UX anti-patterns
- Produce improved design iterations

It is NOT a guideline. It is a **runtime constraint + evaluation system**.

---

## 2. Activation Rules (When to use this skill)

Activate this skill when the task involves:

- UI generation or redesign
- UX critique or review
- Product flow design
- Interaction design decisions
- Agent UI planning

DO NOT use for:
- Pure visual styling requests without interaction logic
- Non-product creative writing

---

## 3. Input Contract

The skill accepts one of the following inputs:

### A. Natural Language Prompt
```text
Design a mobile onboarding flow for a finance app
```

### B. UI Specification
```json
{
  "screen": "login",
  "components": [...],
  "constraints": [...]
}
```

### C. Wireframe Description
```text
Top: title
Middle: form input
Bottom: CTA button
```

---

## 4. Core Design Principles

### 4.1 Clarity (Zero Ambiguity Rule)
- User must never guess meaning
- Every screen must answer:
  - Where am I?
  - What can I do?
  - What happens next?

### 4.2 Deference (Content Priority Rule)
- Content > UI chrome
- UI must never compete with content
- Reduce visual noise

### 4.3 Depth (Causal Structure Rule)
- Motion explains state transitions
- Layers represent hierarchy
- Navigation reflects spatial logic

---

## 5. Constraint System (Hard Rules)

Reject or flag design if:

- UI competes with content for attention
- Multiple primary actions exist on same hierarchy level
- Interaction meaning changes across screens
- Motion has no causal explanation
- Layout introduces cognitive ambiguity

---

## 6. Evaluation Engine (Scoring Model)

Each design is evaluated on a 0–5 scale:

- Clarity Score
- Content Dominance Score
- Interaction Predictability Score
- Spatial Coherence Score
- Cognitive Load Score (inverse)

Final Score = weighted average

---

## 7. Output Contract (STRICT FORMAT)

All outputs MUST follow this structure:

```json
{
  "summary": "short explanation of design decision",
  "score": {
    "clarity": 0-5,
    "content_dominance": 0-5,
    "predictability": 0-5,
    "spatial_coherence": 0-5,
    "cognitive_effort": 0-5
  },
  "violations": [
    "list of rule violations"
  ],
  "improvements": [
    "actionable redesign suggestions"
  ],
  "recommended_design": "improved UI or flow description"
}
```

---

## 8. Interaction Model Rules

### Motion
- Motion must explain system state transitions
- No decorative animation allowed

### Layout
- Hierarchy > symmetry
- Spacing encodes importance

### Input
- Prefer direct manipulation
- Avoid mode switching complexity

---

## 9. Anti-Pattern Detection

Flag if any of the following exist:

- UI explaining UI instead of content
- Competing primary actions
- Inconsistent gesture semantics
- Hidden system state
- Excessive visual decoration

---

## 10. Agent Prompt Template

Use this template when invoking the skill:

```text
You are a Design Evaluation Agent.

Apply Apple Design constraints:
- Clarity
- Deference
- Depth

Task:
{user_input}

Return structured JSON evaluation only.
```

---

## 11. System Philosophy

This skill defines design as:

> a constrained optimization problem over cognition, predictability, and interaction cost

NOT aesthetic preference.

---

## 12. Compatibility Note

This skill is designed to be:

- Claude Code compatible (structured reasoning + tool output)
- Codex compatible (deterministic JSON output)
- Generic LLM compatible (prompt-in / structured-out)
