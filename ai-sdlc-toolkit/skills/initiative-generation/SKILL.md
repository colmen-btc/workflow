---
name: initiative-generation
description: Author a consistent initiative charter (initiative.md) for a new program of work, grounded in mission and platform context. Use when starting a new initiative or rewriting an existing charter for consistency.
---

# Initiative Generation Skill

## Purpose

Create the top-tier initiative charter that frames why a program of work exists, what it delivers, and how success is measured — the north-star document that epics, features, and ADRs trace back to.

## When to Use

- Starting a new initiative under `initiatives/<name>/`
- Rewriting an existing `initiative.md` to a consistent format
- Normalizing a charter before drafting the product brief and roadmap

## Required Inputs

- The idea/why for the initiative (problem, motivation, "why now")
- Organization context: `mission.md` (goals, portfolio) and `platform-brief.md` when present
- Related initiatives this one depends on (for the Depends On table)
- Template: [`ai-sdlc-toolkit/templates/initiative.md`](../../templates/initiative.md)

## Required Workflow

1. Read [`ai-sdlc-toolkit/templates/initiative.md`](../../templates/initiative.md) and treat every `<!-- AGENT: ... -->` block as authoring rules — not as text to copy.
2. Read `mission.md` (and `platform-brief.md` if present) to ground the charter; identify the mission goal this initiative advances.
3. Choose the initiative slug and create `initiatives/<name>/` if it does not exist.
4. Draft the charter in fill order: Status -> Why -> What -> Success Criteria -> Depends On -> Deployment Variants -> Timeline.
5. Write Success Criteria as measurable, testable checkboxes.
6. Add a Reference table linking the sibling artifacts: [`product-brief.md`](product-brief.md) and [`roadmap.md`](roadmap.md) (these may not exist yet — link them as the intended path).
7. Strip every `<!-- AGENT: ... -->` and `<!-- REPLACE: ... -->` block; the shipped file must contain no template scaffolding.
8. Present the draft for review before writing the file.

## Initiative Rules

- Status is one of: `Proposed`, `Active`, `Completed`, `Cancelled`.
- The Why section must name which mission goal the initiative advances and why now.
- Success Criteria are measurable outcomes, not task lists.
- What describes capability and outcome — keep technical design in ADRs/architecture, not the charter.
- Timeline captures intent and phases only; execution tracking lives in GitHub.
- Product detail belongs in `product-brief.md`; phasing detail in `roadmap.md` — do not duplicate them here.
- No placeholder template text is allowed in the shipped file.

## Reference Examples

- [`initiatives/edi-ai-agents/initiative.md`](../../../initiatives/edi-ai-agents/initiative.md)
- [`initiatives/edi-mcp-server/initiative.md`](../../../initiatives/edi-mcp-server/initiative.md)

## Verification

- [ ] File written to `initiatives/<name>/initiative.md`
- [ ] Status, Why, What, Success Criteria, Depends On, Deployment Variants, Timeline present
- [ ] Why names a mission goal; Success Criteria are measurable checkboxes
- [ ] Reference/links point to sibling `product-brief.md` and `roadmap.md`
- [ ] No `<!-- AGENT -->` or `<!-- REPLACE -->` text remains
