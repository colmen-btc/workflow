---
name: product-brief-generation
description: Author a consistent product brief (product-brief.md) for an initiative, including a stable-ID Epic Index that feeds epic generation. Use when defining the capability under an initiative or refreshing an existing brief.
---

# Product Brief Generation Skill

## Purpose

Define the capability an initiative delivers and register its epics at a glance, so the Epic Index can be consumed downstream by the epic-generation and epics-from-product-brief skills.

## When to Use

- Defining the product brief for a new initiative
- Rewriting an existing `product-brief.md` to a consistent format
- Establishing or normalizing the Epic Index before scaffolding epics

## Required Inputs

- The sibling `initiative.md` (charter) for scope and outcomes
- Organization context: `mission.md` / `platform-brief.md` when present
- Known epic-level scope (capabilities to slice into the Epic Index)
- Template: [`ai-sdlc-toolkit/templates/product-brief.md`](../../templates/product-brief.md)

## Required Workflow

1. Read [`ai-sdlc-toolkit/templates/product-brief.md`](../../templates/product-brief.md) and treat every `<!-- AGENT: ... -->` block as authoring rules — not as text to copy.
2. Read the sibling `initiative.md` to align the brief with the charter's What and Success Criteria.
3. Draft in fill order: Title + tagline -> Initiative pointer -> What This Capability Delivers -> Who It's For -> Components -> Epic Index.
4. Set the Initiative pointer to link `initiative.md`.
5. Build the Epic Index with stable IDs, one row per epic.
6. Strip every `<!-- AGENT: ... -->` and `<!-- REPLACE: ... -->` block; the shipped file must contain no template scaffolding.
7. Present the draft for review before writing the file.

## Epic Index Rules

- Each epic ID is stable, uppercase, and shaped `<INITIATIVE_PREFIX>-<SLUG>` (e.g. `EDI-AGT-ARCH`, `EDI-MCP-CORE`).
- The ID must match the intended epic doc filename stem `epics/<id>.md` (lowercase) so [`epic-generation`](../epic-generation/SKILL.md) and the `epics-from-product-brief` scaffolder can consume it.
- Outcome is one line describing what "done" enables; Description is a scope hint only.
- Do NOT paste full acceptance criteria, full feature lists, or raw issue tables into the Epic Index — that detail belongs in `epics/<id>.md`.
- Track aligns to a phase in `roadmap.md` (or a GitHub milestone name — one convention per repo).
- Set the Epic doc column to `epics/<id>.md` only when that file exists, otherwise `—`.

## Document Rules

- Components table lists the moving parts and their role, not implementation detail.
- Who It's For names target users/roles.
- No placeholder template text is allowed in the shipped file.

## Reference Examples

- [`initiatives/edi-ai-agents/product-brief.md`](../../../initiatives/edi-ai-agents/product-brief.md)
- [`initiatives/edi-mcp-server/product-brief.md`](../../../initiatives/edi-mcp-server/product-brief.md)

## Verification

- [ ] File written to `initiatives/<name>/product-brief.md`
- [ ] Title, Initiative pointer, What This Capability Delivers, Who It's For, Components, Epic Index present
- [ ] Initiative pointer links the sibling `initiative.md`
- [ ] Epic Index uses stable `<PREFIX>-<SLUG>` IDs that map to `epics/<id>.md`
- [ ] No full acceptance criteria or feature lists in the Epic Index
- [ ] No `<!-- AGENT -->` or `<!-- REPLACE -->` text remains
