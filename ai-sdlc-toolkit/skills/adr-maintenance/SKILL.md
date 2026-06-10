---
name: adr-maintenance
description: Maintain ADR lifecycle using GitHub Issues as the source of truth. Use when creating, updating, superseding, or closing architecture decisions.
---

# ADR Maintenance Skill

## Purpose

Keep architecture decisions clear, discoverable, and collaborative by managing ADR status and discussion in GitHub Issues.

## Source of Truth Rule

- GitHub Issues are the source of truth for ADR status, rationale updates, and decision discussions.
- ADR markdown files store the durable decision record, but issue state is authoritative for workflow.

## When to Use

- New architectural decision is needed.
- Existing ADR needs clarification or scope update.
- A decision is being superseded.
- Teams disagree on architecture and need a traceable decision log.

## Required Workflow

1. Create or update a GitHub Issue for the ADR decision.
2. Capture context, options, decision, and consequences in the issue.
3. Link the ADR markdown file path in the issue body.
4. Link the GitHub issue URL in the ADR markdown header.
5. Keep ADR issue status current (`Draft`, `Proposed`, `Accepted`, `Superseded`, `Deprecated`).
6. When superseding, open a new ADR issue and cross-link old and new ADRs.
7. New ADRs default to `Proposed` status.
8. Always draft the full ADR using the template at `templates/adr.md` and present it for review before creating or modifying any files.
9. **Validate the draft** against the Quality Checklist below. Present the checklist results (pass/fail/pending per item) alongside the draft so the reviewer can see completeness at a glance. Flag any items that cannot pass until a later step (e.g. cross-links pending issue creation).
10. After approval, create the ADR markdown file using the naming convention below.
11. **Create the GitHub Issue from the ADR file.** The issue body must match the ADR content exactly. Use the ADR markdown file as the source:
    ```bash
    gh issue create --title "ADR-NNN: Decision Title" --body-file <path-to-adr-file>.md --label adr
    ```
    **Never use `--body` for issue creation** — it does not reliably handle UTF-8 characters, tables, or multi-line markdown. Always use `--body-file` with the ADR file path.
12. After the issue is created, update the ADR file's `GitHub Issue:` header with the returned issue URL to complete the bidirectional link.

## GitHub Issue Content Rule

The GitHub Issue body **must be the ADR markdown file itself** — not a summary, not a reformatted subset. This ensures:

- One authoritative version of the decision text (no drift between file and issue).
- Full fidelity of tables, code blocks, and special characters.
- Reviewers see the complete decision record in the issue thread.

When updating an ADR, update the markdown file first, then update the issue body from the file.

## GitHub Issue Template (ADR)

The ADR file used as `--body-file` must contain these sections (per `templates/adr.md`):

- Decision Title (H1 heading)
- Status
- Context
- Decision Drivers
- Decision
- Consequences
  - Becomes Easier
  - Becomes Harder
- Applies To
- Links
  - ADR markdown path
  - Related PRs
  - Related issues

## ADR Status Policy

- `Draft`: discussion started, no recommendation yet.
- `Proposed`: recommendation ready for review.
- `Accepted`: approved and active.
- `Superseded`: replaced by another ADR.
- `Deprecated`: no longer relevant.

## Cross-Link Policy

Every ADR must have bidirectional links:

- In ADR markdown: `GitHub Issue: <url>`
- In GitHub Issue: `ADR File: <repo path>`

For superseded decisions:

- Old ADR issue: `Superseded by #<new-issue>`
- New ADR issue: `Supersedes #<old-issue>`

## Naming Convention

ADR files must be named `<adr-number>-<short-title>.md` (e.g. `005-use-event-sourcing.md`).

## Applies To Rules

The `Applies To` section lists **specs, features, systems, and related ADRs** that must conform to this decision. Do **not** reference source files or implementation paths — those belong in commits and PRs, not in the decision record.

## Quality Checklist

- [ ] Decision is in one sentence and testable.
- [ ] Decision Drivers trace the reasoning from evidence to decision.
- [ ] At least two rejected alternatives with explicit rejection reasons.
- [ ] Consequences include at least one downside.
- [ ] Affected epics/features/tasks are linked.
- [ ] Issue and ADR file links are bidirectional.
- [ ] Status in issue matches status in ADR file.
- [ ] `Applies To` references only specs, systems, or related ADRs — not source files.

## Anti-Patterns

- Updating ADR markdown without updating the GitHub ADR issue.
- Marking ADR accepted without recording rejected alternatives.
- Recording a decision without documenting the drivers that led to it.
- Superseding an ADR without linking both records.
- Duplicating discussion in multiple places instead of centralizing in one issue thread.
- Listing source file paths in `Applies To` instead of specs, systems, or related ADRs.
- Using `gh issue create --body "..."` instead of `--body-file` — causes encoding issues with UTF-8 characters, tables, and multi-line content.
- Writing a different or abbreviated version of the ADR in the issue body instead of using the file directly.
