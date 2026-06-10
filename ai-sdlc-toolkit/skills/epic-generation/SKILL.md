---
name: epic-generation
description: Generate consistent epic artifacts from initiative history with GitHub Issues as source of truth. Use when drafting a new epic or refreshing an existing epic from prior decisions.
---

# Epic Generation Skill

## Purpose

Create epics that are structurally consistent, historically grounded, and traceable to ADRs and GitHub issues.

## When to Use

- Creating a new epic under an initiative
- Rewriting an epic from issue history after drift
- Normalizing epic format before issue creation/update

## Required Inputs

- Initiative context: `initiative.md` and `product-brief.md`
- Related prior epics/features in the same initiative
- ADR source: `adrs/adr-list.md` and specific ADR files when present
- Related GitHub issues (if available).

## Required Workflow

1. Collect context from initiative docs, ADRs, and related issues.
   - If `graphify-out/GRAPH_REPORT.md` exists, read it to identify god nodes, surprising connections, and structural relationships relevant to the epic scope.
   - Use `/graphify query "<epic topic>"` to discover cross-cutting dependencies and related components.
2. Define epic scope in one sentence (in-scope and out-of-scope).
3. Write Problem, Value, and Acceptance Criteria with measurable language.
4. Build Features table with stable IDs and slugs (`<EPIC-ID>-F01`, `-F02`, ...).
5. Add only cross-cutting ADR links in the epic ADR section.
6. Link each feature row to its feature doc path.
7. Create/update the GitHub epic issue from the epic markdown file.

## Epic Rules

- Epic ID is stable and uppercase (e.g., `EDI-MCP-CORE`).
- Acceptance criteria are testable and non-ambiguous.
- Features in the table are implementation slices, not goals.
- Epic ADR section must not duplicate feature-specific ADR detail.

## GitHub Source of Truth

- Epic issue body must be updated from the epic markdown file.
- If epic doc and issue differ, reconcile and re-sync immediately.

## Verification

- [ ] Epic has stable ID and GitHub issue link
- [ ] Problem/Value/ACs are present and measurable
- [ ] Features table includes IDs, slugs, and links
- [ ] ADRs listed are cross-cutting only
- [ ] GitHub epic issue body matches the markdown file
