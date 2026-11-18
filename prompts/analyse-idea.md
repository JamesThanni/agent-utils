# Idea Analysis

Convert idea intent documents into structured project requirements specs ready for engineering handoff.

---

## Soft Rules

- **Assumptions block**: Open every spec with a brief `> **Assumptions:** ...` blockquote listing inferred decisions so the user can correct them.

- **No placeholders**: Fill every section completely. If unknown, document as a question — never write "TBD".

- **Policy alignment**: Call out explicitly where existing code style, security policies, or brand guidelines apply. Describe any conflicts in "Areas of Concern."

- **Depth scales with complexity**: Simple projects get concise sections; complex ones get detail where it matters.

- **YAGNI**: Don't invent features not mentioned or implied by the intent document.

- **POC development plan**: Always 4 epics — AI feature + user management mandatory. Add post-launch epics after.

- **Reduce token usage**: Speak concisely when thinking. This helps the user's token budget. However, when adding notes to markdown files, writing them out in full English.

- **Code-aware**: Reference existing services, models, APIs by name. Show how the spec integrates with what's already there.

## Hard Rules
- Do NOT generate the spec until you have:
  1. Read any attached intent.md or project documentation or idea notes
  2. Explored the codebase, if there is one, for existing context (stack, architecture, conventions)
  3. Interviewed the user enough (one question at a time) until sufficient understanding is reached

- Your ONLY output after the hard-gate is the spec document — no summaries, commentary, or content outside the spec structure.

- Speak concisely: drop filler, articles, and pleasantries while keeping full technical accuracy.


## Workflow

### Step 1: Parse & Explore

Extract available context from the intent document:

- Read attached intent.md if provided
- Explore codebase instead of asking: stack, architecture, existing integrations, conventions
- Identify gaps requiring user input

### Step 2: Interview

Ask **up to 3 targeted clarifying questions** (one at a time, with a recommended answer).

Skip questions you can reasonably infer from code/docs. Only ask if genuinely unknown and important.

**Priority order:**

- **Users** — roles, permissions, access control model?
- **Success metric** — what does "done" look like? Primary objective?
- **Constraints** — tech stack, integrations, compliance, timeline?

### Step 3: Generate Spec

Output full spec using the structure below. No TBD placeholders — unknown items go in Questions section.

### Step 4: Save

Ask: "Save as `spec.md` in project root, or output as markdown?"

---

## Spec Output Format

```markdown
# Spec: [Feature Name]

From: intent.md (Author, Role). Status: [draft|ready for review|approved].
Skills applied: [list of applicable company skills].

> **Assumptions:** [List inferred decisions the user can correct. E.g., "Existing MongoDB schema unchanged," "No new user roles," "60-second cache is acceptable latency."]

## Summary

Project purpose, key objectives, high-level description in 1–2 paragraphs. Identify stakeholders.

## Requirements

Numbered, concise functional + non-functional requirements. Format: `Rn. [Description].`

**Functional:**

- R1. [Core behaviour]
- R2. [Core behaviour]
- R3. [Integration or constraint]

**Non-Functional:**

- R4. [Performance/security/compliance]
- R5. [Scalability/usability]

## Design

Wireframe descriptions, UI/UX flow, component layout. How it aligns with existing brand guidelines and company standards.

**Architecture:**

- New/modified API endpoints with methods and paths
- Data flow: which services read/write where
- Frontend components and their state

## How Each Constraint Is Met

For each constraint, use this format of subheadings and list the corresponding details beneath them:
'''
### Constraint (from intent)

- [Requirement Number] -  Solution that satisfies it

### Notes

- [Brief explanation of each solution]

'''

## Open Questions from the Intent

- Q1. [Question not answered by the intent document]. Not addressed. Carried forward as concern.
- Q2. [Question]. Assumed [answer]. Confirm?

## Areas of Concern

Explicit list of risks, contradictions, feasibility risks, or policy conflicts that cannot be resolved without further input. **Assign an owner for each.**

1. [Description]. Breaks [constraint/requirement]. Workaround: [proposal]. **Owner:** [team/role].
2. [Description]. May impact [area]. Requires [input/approval]. **Owner:** [team/role].
3. [Description]. Feasibility risk. Needs load testing or design review. **Owner:** [team/role].

## Testing Plan

Testing strategy: unit, integration, end-to-end, UAT. Key scenarios and acceptance tests.

## Appendices & References

Glossary, external references, company frameworks.
```

---

## Tips for Effective Interviewing

- **Explore before asking**: Search codebase, docs, README for answers about stack, architecture, existing patterns.
- **Ask one at a time**: Each question should be specific and have a recommended answer.
- **Listen for scope creep**: User's answer to one question often informs the others — stop early if patterns emerge.
- **Call out assumptions**: After each answer, reflect back: "So you're saying [X]?" to confirm.
- **End decisively**: Once you have critical inputs, stop — don't over-interview. Move to spec generation.
