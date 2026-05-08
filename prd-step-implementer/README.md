# PRD Step Implementer

Turn a PRD into shipped code without losing the requirements along the way.

`prd-step-implementer` is a Codex skill for implementation work driven by product requirements documents. It makes Codex read the PRD first, break it into traceable requirements, implement one coherent step at a time, and check each step back against the original PRD before moving on.

## Why This Exists

Most AI-assisted builds fail in the same quiet way: the code looks plausible, but nobody can tell which PRD requirement it actually satisfies.

This skill changes the loop:

```text
PRD -> requirement checklist -> scoped implementation step -> PRD checkpoint -> next step
```

The result is a workflow where every implementation decision stays tied to the source requirement.

## What It Does

- Reads the PRD before touching code
- Extracts functional requirements, edge cases, constraints, and acceptance criteria
- Assigns stable requirement IDs like `R1`, `R2`, `R3`
- Groups requirements into implementation steps
- Plans only the next step in detail
- Implements the step using the existing codebase style
- Runs targeted verification after each step
- Reports whether the implementation matches the PRD: `pass`, `partial`, or `fail`
- Keeps a live traceability checklist until the work is done

## The Core Loop

After every implementation step, Codex produces a checkpoint like this:

```text
Checkpoint: Step N
Covered requirements: R1, R2
Evidence: files changed, tests run, UI/browser checks, command output, or code references
PRD match: pass / partial / fail
Gaps: remaining mismatch or missing evidence
Next action: continue / fix gap before continuing / ask user
```

That checkpoint is the point: code is not considered complete just because it was written. It is complete when there is evidence that it satisfies the PRD.

## Example Use

```text
Use prd-step-implementer with docs/checkout-redesign-prd.md.
Implement the PRD step by step. After each step, check the result against the PRD before continuing.
```

Codex will:

1. Read `docs/checkout-redesign-prd.md`
2. Build a requirement checklist
3. Pick the first coherent implementation slice
4. Make the code change
5. Verify that slice against the PRD
6. Continue only after the checkpoint is clear

## Best For

- Feature PRDs
- Product specs
- Engineering implementation plans
- Design-to-code requirements
- Multi-step application changes
- Work where acceptance criteria matter
- Tasks where regressions or requirement drift are expensive

## Not For

- One-line code edits with no product requirement
- Exploratory brainstorming
- Pure code review with no implementation request
- Vague feature ideas that have not been written into requirements yet

## Install

Copy this folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R prd-step-implementer ~/.codex/skills/
```

Then start a new Codex session and reference a PRD. The skill should trigger when you ask Codex to implement from that PRD.

## Skill File

The actual skill instructions live in:

```text
prd-step-implementer/SKILL.md
```

Keep `SKILL.md` focused on the agent workflow. Use this README for GitHub presentation, onboarding, and examples.
