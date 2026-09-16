---
name: ai-development-docs
description: Use when adding features, fixing non-trivial defects, refactoring important code, changing architecture, or reviewing development work that needs traceable requirements, design, milestones, AI participation, verification evidence, and delivery records under docs.
---

# AI Development Docs

## Purpose

Keep code changes maintainable by recording the decisions and evidence a future maintainer needs. Every in-scope code change gets at least one concise AI development record; larger changes add only the documents justified by their risk.

## Workflow

1. Inspect the repository's existing `docs/` layout, naming, contribution rules, and linked issue/PR conventions. Preserve them unless the user asks to reorganize.
2. Classify the change using [references/document-standard.md](references/document-standard.md): small, standard, major, or architectural.
3. Before implementation, create or update the required requirement, design, and milestone sections. Unknowns must be labelled as assumptions or open questions.
4. During implementation, maintain the AI development record with decisions, affected files, deviations, and milestone status. Summarize useful conclusions; never save hidden reasoning or raw chat transcripts.
5. Before claiming completion, record the commands or procedures actually run, their results, remaining risks, rollback notes when relevant, and links to code/issue/PR artifacts.
6. Update the relevant document in the same task as the code. If evidence is unavailable, state `未验证` and do not present the item as complete.

## Required Output by Change Class

| Class | Required records |
|---|---|
| Small fix/change | One AI development record containing scope, files, verification, and remaining risks |
| Standard feature | Requirement analysis, AI development record, verification record |
| Major/high-risk feature | Requirement analysis, technical design, milestones, AI development record, verification, delivery summary |
| Architecture/interface/data ownership change | Major set plus ADR-style decision record, migration, compatibility, observability, and rollback |

Use the templates in `assets/templates/`. Combine sections into one file for small work; do not create empty documents merely to satisfy the matrix.

## Evidence Contract

- Distinguish planned work from completed work.
- List actual affected paths, stable contracts, and material decisions.
- Capture verification command/method, environment when relevant, result, and unresolved failures.
- Record AI participation as task/input constraints/output summary/human review; omit secrets, personal data, credentials, and full prompts containing sensitive context.
- A completed record must let another developer understand why the change exists, how it works, how it was verified, and what remains.

## Common Mistakes

- Treating a generated document as evidence that tests ran.
- Copying long AI conversations instead of decisions and outcomes.
- Writing `测试通过` without commands, scope, or results.
- Reorganizing an established `docs/` tree without authorization.
- Marking milestones complete while open risks or unverified items are hidden.

