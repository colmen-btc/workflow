---
name: feature-generation
description: Generate consistent feature artifacts from epic requirements and history with GitHub Issues as source of truth. Use when deriving new features or refining existing feature docs.
---

# Feature Generation Skill

## Purpose

Create features that map directly to epic acceptance criteria with clear dependencies, ADR scope, and delivery tasks.

## When to Use

- Deriving features from a new or existing epic
- Refactoring feature docs to a consistent format
- Syncing feature docs and GitHub feature issues

## Required Inputs

- Parent epic markdown file
- Existing features under the same epic
- Relevant ADRs (`adrs/adr-list.md` and ADR files)
- Related feature/implementation issues and PR context

## Required Workflow

1. Select one or more epic criterian the feature will satisfy.
2. If `graphify-out/GRAPH_REPORT.md` exists, query the knowledge graph for the feature topic to discover related components, ADRs, and surprising connections.
3. Assign stable feature ID and slug (`<EPIC-ID>-Fxx`, kebab-case slug).
4. Draft What and Why in one short paragraph each.
5. Write 2 to 10 verifiable acceptance criteria.
6. Add Depends On entries (features/infra/ADRs as needed).
7. Add feature-specific ADR links (avoid repeating epic-level cross-cutting ADRs unless required).
8. Build task table with dependency-aware ordering.
9. Create/update the GitHub feature issue from the feature markdown file.

## Feature Rules

- Every feature maps to at least one explicit epic acceptance criterion.
- Feature scope is a shippable increment, not an umbrella epic.
- IDs/slugs remain stable after issue creation.
- No placeholder template text is allowed.

## ADR Scope Rules

- Cross-cutting decisions belong at epic level.
- Feature-level design/security/behavior decisions belong in the feature ADR section.
- Link to specific ADR files when available; otherwise link to ADR index.

## GitHub Source of Truth

- Feature issue body must be updated from the feature markdown file.
- If feature doc and issue differ, reconcile and re-sync immediately.

## Verification

- [ ] Feature links to parent epic and has stable ID/slug
- [ ] Acceptance criteria are verifiable and tied to epic criteria
- [ ] Depends On and ADR sections are present and scoped correctly
- [ ] Task table is dependency-ordered
- [ ] GitHub feature issue body matches the markdown file
