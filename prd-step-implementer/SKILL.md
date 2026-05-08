---
name: prd-step-implementer
description: Implement a product requirements document step by step with PRD-grounded verification after each step. Use when the user provides or references a PRD, spec, requirements document, issue brief, or feature plan and expects Codex to design or code the implementation while repeatedly checking each completed step against the source requirements.
---

# PRD Step Implementer

## Overview

Use this skill to turn a PRD into an implementation workflow with explicit requirement traceability. Treat the PRD as the source of truth, implement in small coherent steps, and after each step verify the changed behavior against the corresponding PRD requirements before continuing.

## Workflow

### 1. Load and Normalize the PRD

- Read the PRD file before editing code.
- Extract functional requirements, non-functional requirements, constraints, user flows, edge cases, acceptance criteria, and explicit out-of-scope items.
- If the PRD references designs, APIs, schemas, tickets, or other files, read only the referenced material needed for the next implementation step.
- If requirements conflict or a blocking detail is missing, ask one concise question. Otherwise make a conservative assumption and record it.

### 2. Build a Requirement Checklist

Create a checklist with stable requirement IDs:

```text
R1 - Requirement summary - PRD section/source
R2 - Requirement summary - PRD section/source
```

Group requirements into implementation steps that can be independently designed, coded, and checked. Prefer thin vertical slices when the PRD describes user-facing behavior.

### 3. Plan the Next Step Only in Detail

Before each implementation step, state:

- PRD requirements covered by this step
- Files or modules likely to change
- Verification method for those requirements
- Any assumptions introduced for this step

Keep later steps at a higher level until earlier checks pass, because discoveries during implementation may change the plan.

### 4. Implement the Step

- Follow the existing codebase architecture and style.
- Keep the edit scope aligned with the current requirement IDs.
- Do not implement unrelated PRD sections early unless required by the current step.
- Update tests, fixtures, docs, migrations, or configuration when the PRD requirement depends on them.

### 5. PRD Checkpoint After Every Step

After each step, return to the PRD and produce a checkpoint:

```text
Checkpoint: Step N
Covered requirements: R1, R2
Evidence: files changed, tests run, UI/browser checks, command output, or code references
PRD match: pass / partial / fail
Gaps: remaining mismatch or missing evidence
Next action: continue / fix gap before continuing / ask user
```

Do not mark a requirement complete only because code was written. Mark it complete when behavior, tests, or inspection evidence matches the PRD.

### 6. Maintain Traceability

Keep a live checklist in updates or notes during the task:

```text
[done] R1 - implemented and verified
[partial] R2 - implemented, missing mobile check
[todo] R3 - not started
[blocked] R4 - needs API contract clarification
```

When a PRD requirement is intentionally deferred or changed, say that it diverges from the PRD and explain why.

## Verification Guidance

- Prefer automated tests for business logic, data transformations, APIs, and regression-prone behavior.
- Use browser or UI verification for visual and interaction requirements.
- Use static inspection only when runtime verification is impractical, and label it as inspection evidence.
- Run the narrowest useful verification after each step; run broader checks before final delivery.
- If verification fails, fix the gap before moving to unrelated PRD requirements.

## Final Response

End with:

- Requirements completed and verified
- Requirements partially complete or blocked
- Tests/checks run
- PRD deviations, assumptions, or residual risks
