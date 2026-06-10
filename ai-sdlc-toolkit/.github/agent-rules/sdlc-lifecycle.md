# AI-SDLC Lifecycle Enforcement

## Artifact Rules

- Every artifact follows its template from `templates/`
- Use the locked vocabulary from `standard/glossary.md` — Initiative, Product Brief, Epic, Feature, Task, Spec, ADR
- Every spec must reference applicable ADRs
- Every PR must link to a task issue
- Every PR must use `templates/pull-request.md` as its description template — populate the AI Attribution table with the exact model slug (e.g. `claude-sonnet-4-5`) and tool name (e.g. `GitHub Copilot` / `Cursor` / `Claude Code`); use `—` for human-only roles

## Stage Gates

- NEVER advance work past a gate without human approval
- Gates are GitHub Issue status transitions — only humans make them
- If a gate checklist exists in `checklists/`, reference it before asking for approval

## Hierarchy

```
Initiative → Product Brief → Epic → Feature → Task → Spec → Code → PR
```

- Initiatives add capabilities to the platform — each has its own product brief, roadmap, and epics
- Epics are product areas within an initiative — they contain features and never close
- Features are deliverables — they ship in a phase
- Tasks are engineering units — independently testable
- Specs are implementation detail — attached to task issues

## Brownfield Track

For initiatives that change/re-platform/retire an existing system, run the reverse phase first:

```
Existing system → Evidence Ledger → AS-IS (system-overview + epics + features + Discovered ADRs) → Forward delta (initiative → migration-plan → parity-baseline → decommission-plan)
```

- AS-IS reference model lives in `assessments/<system>/` — it is descriptive (no Status/Timeline) and reusable across initiatives
- The AS-IS feeds the forward delta; target epics are keep/change/add/retire against it
- Discovered ADRs (`Status: Discovered`) are superseded by forward (`Accepted`) migration ADRs
- Every extracted artifact cites evidence ids (provenance) and a confidence level; code wins for "what exists"

## Workload Budget

| Task size | Approach |
|-----------|----------|
| Single function / config change | Do it directly, no plan needed |
| 2–5 file changes | Brief inline reasoning, then execute |
| 6+ files or cross-cutting concern | Write a plan first, get approval |
