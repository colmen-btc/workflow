# AI-SDLC Toolkit

A git-native, human-controlled, AI-assisted software delivery lifecycle. Everything you need to run an initiative — templates, checklists, agent rules, CI/CD, and GitHub Issue forms.

## Start Here

- **New to the AI-SDLC?** Read [The AI-SDLC: How It Works](standard/guide.md)
- **Why is it designed this way?** Read [Design Rationale](standard/design-rationale.md)
- **Just joined the team?** Read [Onboarding Guide](standard/onboarding.md)
- **Starting a new initiative?** Follow [SETUP.md](SETUP.md)
- **Want to improve the toolkit?** Read [CONTRIBUTING.md](CONTRIBUTING.md)

## What's Inside

| Folder | Contents |
|--------|----------|
| `standard/` | The SDLC lifecycle, vocabulary, roles, and design rationale |
| `templates/` | Fill-in-the-blank artifacts; top-of-file `<!-- AGENT: ... -->` blocks are **scaffolding instructions only** — strip them when copying into `initiatives/` (see [CONTRIBUTING.md](CONTRIBUTING.md)) |
| `samples/` | Completed examples using a reference product |
| `checklists/` | Gate checklists for stage transitions |
| `skills/` | Reusable agent skills for repeatable workflows (for example ADR maintenance, epic generation, feature generation) |
| `agent-rules/` | IDE-agnostic agent behavior rules |
| `ide/` | Pre-packaged agent rules per IDE |
| `.github/` | Issue forms, PR template, CI/CD workflows |

## Using Skills

Skills are reusable agent workflows packaged as markdown files under `skills/<skill-name>/SKILL.md`. Each skill has a YAML front-matter block (`name`, `description`) and a structured body with purpose, trigger conditions, and step-by-step instructions.

**How to invoke a skill in your IDE:**

| IDE | How to invoke |
|-----|---------------|
| GitHub Copilot | Copy the SKILL.md into your repo as `.github/instructions/<skill-name>.instructions.md` — Copilot auto-discovers it. Optionally add `applyTo` front-matter to scope activation to specific files. |
| Cursor | Add the skills directory to your agent rules, then call the skill by name in chat |
| Claude Code | Reference the skill file path in your prompt: `Follow skills/adr-maintenance/SKILL.md` |

**Copilot example:**
```bash
cp skills/adr-maintenance/SKILL.md your-repo/.github/instructions/adr-maintenance.instructions.md
```

**When to use vs. when to skip:**
- Use a skill when a workflow repeats across epics (e.g., every ADR, every spec review).
- Skip a skill for one-off actions that don't fit an existing skill — just work directly.

**Adding a new skill:**
1. Create `skills/<your-skill-name>/SKILL.md`
2. Include YAML front-matter with `name` and `description`
3. Follow the structure: Purpose → When to Use → Required Workflow → Examples
4. Add a row to the `skills/` table in this README

**Available Skills:**

| Skill | Description |
|-------|-------------|
| [`skills/initiative-generation/`](skills/initiative-generation/SKILL.md) | Author an initiative charter (initiative.md) grounded in mission and platform context |
| [`skills/product-brief-generation/`](skills/product-brief-generation/SKILL.md) | Author a product brief (product-brief.md) with a stable-ID Epic Index that feeds epic generation |
| [`skills/roadmap-generation/`](skills/roadmap-generation/SKILL.md) | Author a roadmap (roadmap.md) that phases and prioritizes the epic backlog, aligned to the product brief |
| [`skills/adr-maintenance/`](skills/adr-maintenance/SKILL.md) | Create, update, supersede, and close ADRs with GitHub Issues as the source of truth |
| [`skills/epic-generation/`](skills/epic-generation/SKILL.md) | Generate epics consistently from initiative history, ADRs, and issue context |
| [`skills/feature-generation/`](skills/feature-generation/SKILL.md) | Generate features consistently from epic criteria, ADR scope, dependencies, and issue context |
| [`skills/context-acquisition/`](skills/context-acquisition/SKILL.md) | Brownfield: gather evidence from code, git, Jira, Confluence, Slack (via MCP) into a source inventory + evidence ledger |
| [`skills/current-state-assessment/`](skills/current-state-assessment/SKILL.md) | Brownfield: recover the AS-IS system as a descriptive `system-overview.md` |
| [`skills/adr-recovery/`](skills/adr-recovery/SKILL.md) | Brownfield: recover de-facto decisions as ADRs with `Status: Discovered` |
| [`skills/epic-extraction/`](skills/epic-extraction/SKILL.md) | Brownfield: recover AS-IS capability areas as epics |
| [`skills/feature-extraction/`](skills/feature-extraction/SKILL.md) | Brownfield: recover AS-IS deliverables as features (the parity inventory) |
| [`skills/migration-planning/`](skills/migration-planning/SKILL.md) | Brownfield: author the AS-IS -> TO-BE migration plan as a delta |
| [`skills/parity-baseline/`](skills/parity-baseline/SKILL.md) | Brownfield: turn the AS-IS feature inventory into a no-regression gate |
| [`skills/decommission-planning/`](skills/decommission-planning/SKILL.md) | Brownfield: plan safe retirement of replaced AS-IS components |

### Brownfield initiatives

When an initiative changes, re-platforms, or retires an **existing** system, run the reverse phase before forward planning — you cannot define the future without first recovering the past.

**Reverse (extract AS-IS into `assessments/<system>/`), in order:**

1. `context-acquisition` — gather multi-source evidence into `source-inventory.md` + `evidence-ledger.md`
2. `current-state-assessment` — `system-overview.md`
3. `adr-recovery` — discovered ADRs
4. `epic-extraction` — AS-IS epics
5. `feature-extraction` — AS-IS features

**Forward (define the TO-BE delta in `initiatives/<name>/`):** the usual `initiative-generation` -> `product-brief-generation` -> `roadmap-generation` (target epics as keep/change/add/retire against the AS-IS), plus `migration-planning`, `parity-baseline`, and `decommission-planning`. Forward (`Accepted`) migration ADRs supersede the discovered ADRs.

**Reverse derivation chain:**

```
multi-source evidence (code, git, Jira, Confluence, Slack)
    ↓  context-acquisition (via MCP)
evidence-ledger.md  (provenance + confidence)
    ↓  assessment + extraction
assessments/<system>/  (system-overview + epics + features + Discovered ADRs)
    ↓  feeds as input
forward delta  (initiative → migration-plan → parity-baseline → decommission-plan)
```

**MCP prerequisites:** full-context assessments use MCP servers connected in your IDE — Atlassian MCP (Jira + Confluence) and Slack MCP. If a server is not connected, `context-acquisition` records it as a gap and lowers confidence rather than failing; code, git, and graphify still provide ground truth.

## Quick Start

1. Read `mission.md` and `platform-brief.md` at the repo root for context
2. Follow `SETUP.md` to scaffold your initiative
3. Fill in `initiatives/<name>/initiative.md` — why, success criteria, timeline (**omit** the template’s `<!-- AGENT: ... -->` block in the initiative copy)
4. Fill in `initiatives/<name>/product-brief.md` — capability, epic index (same: **no** AGENT block in the shipped file)
5. Fill in `initiatives/<name>/roadmap.md` — phasing and priorities (same)
6. Create your first epic and start the delivery cycle

## Derivation Chain

Every file in this toolkit traces back to a source:

```
standard/   (defines what each artifact IS)
    ↓
templates/  (structure + optional AGENT scaffolding comments — strip AGENT blocks when materializing outside this folder)
    ↓
samples/    (fills the template with a realistic example)
```

## IDE Support

Agent rules are authored once in `agent-rules/` and distributed per IDE:

| IDE | Copy From | Copy To |
|-----|-----------|---------|
| Cursor | `ide/cursor/` | `.cursor/rules/` in your repo |
| Claude Code | `ide/claude-code/` | Root of your repo (`CLAUDE.md`) |
| GitHub Copilot | `ide/copilot/` | `.github/` in your repo |

## Storage Rules

| Purpose | Where |
|---------|-------|
| Mission and platform scope | `mission.md` and `platform-brief.md` at repo root (read-only context) |
| Initiative artifacts | `initiatives/<name>/` — initiative.md, product-brief.md, roadmap.md, epics/ (brownfield adds migration-plan.md, parity-baseline.md, decommission-plan.md) |
| Brownfield AS-IS reference model | `assessments/<system>/` — source-inventory.md, evidence-ledger.md, system-overview.md, epics/, features/, adrs/ (Discovered) |
| Architecture decisions | `docs/adrs/` |
| Implementation specs | Code repo `docs/specs/` |
| Track work | GitHub Issues + Projects |
| Discuss decisions | GitHub Discussions |
| Publish documentation | GitHub Pages |
| Never | GitHub Wiki |
