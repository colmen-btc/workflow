---
name: roadmap-generation
description: Author a consistent initiative roadmap (roadmap.md) that phases and prioritizes the epic backlog, aligned to the product brief Epic Index. Use when sequencing epics into milestones or refreshing an existing roadmap.
---

# Roadmap Generation Skill

## Purpose

Express the intent order and priorities for an initiative's epic backlog — phasing only, not a schedule — so the team knows what each phase proves and which epics come first.

## When to Use

- Sequencing the epics from a product brief into phased milestones
- Rewriting an existing `roadmap.md` to a consistent format
- Re-prioritizing the backlog after the Epic Index changes

## Required Inputs

- The sibling `product-brief.md` (Epic Index) for epic names and IDs
- The sibling `initiative.md` (Timeline) for phase intent
- Template: [`ai-sdlc-toolkit/templates/roadmap.md`](../../templates/roadmap.md)

## Required Workflow

1. Read [`ai-sdlc-toolkit/templates/roadmap.md`](../../templates/roadmap.md) and treat every `<!-- AGENT: ... -->` block as authoring rules — not as text to copy.
2. Read the sibling `product-brief.md` Epic Index and `initiative.md` Timeline.
3. Build the Milestones & Epics table: each phase states the goal it proves, the epics in it, and a priority (P1/P2/P3).
4. Use epic names that match the product-brief Epic Index exactly.
5. Write the Prioritization Criteria section describing how priorities are ranked.
6. Strip every `<!-- AGENT: ... -->` and `<!-- REPLACE: ... -->` block; the shipped file must contain no template scaffolding.
7. Present the draft for review before writing the file.

## Roadmap Rules

- Epic names must align with the `product-brief.md` Epic Index — no drift, no invented epics.
- Phases should align with the `initiative.md` Timeline phases where present.
- Capture intent order and priorities only; do NOT duplicate long schedules — link a GitHub Project or milestone view when ready.
- Each phase has a clear goal (what it proves/expands/enables).
- No placeholder template text is allowed in the shipped file.

## Reference Examples

- [`initiatives/edi-ai-agents/roadmap.md`](../../../initiatives/edi-ai-agents/roadmap.md)
- [`initiatives/edi-mcp-server/roadmap.md`](../../../initiatives/edi-mcp-server/roadmap.md)

## Verification

- [ ] File written to `initiatives/<name>/roadmap.md`
- [ ] Milestones & Epics table present with phases, epics, and priorities
- [ ] Epic names match the product-brief Epic Index
- [ ] Prioritization Criteria section present
- [ ] No duplicated schedule/dates beyond phase intent
- [ ] No `<!-- AGENT -->` or `<!-- REPLACE -->` text remains
