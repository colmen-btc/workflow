# Setup: Start a New Initiative

This guide scaffolds everything you need to run an initiative through the AI-SDLC.

> **Prerequisite:** `mission.md` and `platform-brief.md` must already exist at the repo root. These are read-only context — you reference them, you don't create them here.

---

## 1. Create the Initiative Folder

```bash
mkdir -p initiatives/<initiative-name>/epics
```

Copy from `templates/`:

```bash
cp templates/initiative.md  initiatives/<initiative-name>/initiative.md
cp templates/product-brief.md  initiatives/<initiative-name>/product-brief.md
cp templates/roadmap.md  initiatives/<initiative-name>/roadmap.md
```

**Strip template scaffolding:** each file under `templates/` may start with a `<!-- AGENT: ... -->` HTML block (instructions for humans and agents). **Delete that entire comment** from the copies in `initiatives/<initiative-name>/` before you treat the docs as the product artifact — it does not belong in the initiative folder long-term.

## 2. Fill In Initiative Documents

1. `initiative.md` — why this initiative exists, success criteria, timeline, deployment variants
2. `product-brief.md` — what this capability delivers, who it's for, epic index
3. `roadmap.md` — phasing and priorities for the epics

Reference `mission.md` and `platform-brief.md` when filling these in — they provide the strategic context.

## 3. Set Up GitHub

### Create Milestones

One milestone per roadmap phase:
- `Phase 1 — <name>`
- `Phase 2 — <name>`
- `Phase 3 — <name>`

### Create Labels (if not already present)

```
epic
feature
task
adr
priority-p1
priority-p2
priority-p3
```

### Create GitHub Project

1. Go to your repo → Projects → New Project
2. Select **Board** layout
3. Configure status columns: `Backlog` → `Ready for Dev` → `Ready for Spec` → `Approved` → `In Progress` → `Done`
4. Add a **Roadmap** view for executive-level visibility

### Copy Issue Templates (if not already present)

```bash
cp -r .github/ISSUE_TEMPLATE <your-repo>/.github/
cp .github/PULL_REQUEST_TEMPLATE.md <your-repo>/.github/
```

## 4. Set Up Agent Rules (if not already present)

Copy rules for your IDE into your repo. See `ide/<your-ide>/INSTALL.md` for details.

| IDE | Command |
|-----|---------|
| Cursor | `cp -r ide/cursor/cursor-rules/ <your-repo>/.cursor/rules/` |
| Claude Code | `cp ide/claude-code/CLAUDE.md <your-repo>/CLAUDE.md` |
| Copilot | `cp ide/copilot/copilot-instructions.md <your-repo>/.github/copilot-instructions.md` |

## 5. Build the Knowledge Graph (Graphify)

[Graphify](https://github.com/safishamsi/graphify) maps your code, docs, and ADRs into a knowledge graph that agents query when building specs.

### Install Graphify

```bash
uv tool install graphifyy
```

### Register with your IDE

| IDE | Command |
|-----|---------|
| Copilot (VS Code) | `graphify vscode install` |
| Claude Code | `graphify claude install` |
| Cursor | `graphify cursor install` |
| Gemini CLI | `graphify gemini install` |

### Generate the graph

Run once from your project root:

```bash
graphify .
```

This creates `graphify-out/` with three files:
- `graph.html` — interactive visualization (open in a browser)
- `GRAPH_REPORT.md` — highlights: god nodes, surprising connections, suggested questions
- `graph.json` — the full graph for agent queries

### Keep the graph current

```bash
graphify hook install   # auto-rebuild on git commit (AST only, no API cost)
```

After doc or ADR changes, refresh semantic nodes:

```bash
graphify . --update     # re-extract only changed files
```

### Commit and share

Commit `graphify-out/` to the repo so every team member's agent starts with the graph. Add to `.gitignore`:

```
graphify-out/manifest.json
graphify-out/cost.json
```

### Add a `.graphifyignore`

Create `.graphifyignore` in your project root to exclude noise:

```
node_modules/
dist/
*.generated.*
.venv/
```

## 6. Foundation (before writing code)

1. Create Tier 1 ADRs using [templates/adr.md](templates/adr.md) — see [checklists/foundation-readiness.md](checklists/foundation-readiness.md)
2. Document architecture in `docs/architecture/`
3. Verify CI/CD pipeline runs green
4. Confirm branch protection rules are enforced
5. Rebuild the knowledge graph after ADRs are created: `graphify . --update`

## 7. Start the Lifecycle

1. Create your first epic in `initiatives/<initiative-name>/epics/` using [templates/epic.md](templates/epic.md)
2. Create a GitHub Issue from the epic — the delivery cycle begins
