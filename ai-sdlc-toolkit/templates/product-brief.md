<!--
AGENT: Product brief — defines one capability under an initiative and registers epics at a glance.

Fill order: (1) Title + tagline, (2) Initiative pointer, (3) What This Capability Delivers,
(4) Who It's For, (5) Components, (6) Epic Index rows.

Epic Index columns:
- ID: stable code <INITIATIVE_PREFIX>-<SLUG> (e.g. EDI-MCP-CORE). Must match the epic doc filename stem in epics/<ID>.md when that file exists.
- Epic: short human-readable name.
- Outcome: one line — what "done" enables for users or the business (not a task list).
- Description: scope hint only; not acceptance criteria.
- Track: phase from initiatives/<name>/roadmap.md (or your GitHub milestone name — pick one convention per repo).
- GitHub: milestone URL, Project link, saved issue query, or TBD.
- Epic doc: relative path epics/<ID>.md or — if not created yet.

Do NOT paste full acceptance criteria, full feature lists, or raw issue tables into Epic Index — use epics/<ID>.md and GitHub for detail.

Cross-links: initiative.md (charter), roadmap.md (phasing), epics/ (deep dive).

Strip this entire HTML comment when writing to initiatives/ or anywhere outside ai-sdlc-toolkit/templates/ — scaffolding only; not part of the product artifact.
-->

# <!-- REPLACE: Capability Name -->

> <!-- REPLACE: One-sentence description of this capability -->

## Initiative

> Part of: <!-- REPLACE: Initiative Name -->
> See: `initiatives/<name>/initiative.md`

## What This Capability Delivers

<!-- REPLACE: 2-3 sentences describing what this capability enables and who it's for -->

## Who It's For

<!-- REPLACE: Target users or roles -->

## Components

| Component | Role |
|-----------|------|
| <!-- REPLACE --> | <!-- REPLACE --> |

## Epic Index

| ID | Epic | Outcome | Description | Track | GitHub | Epic doc |
|----|------|---------|-------------|-------|--------|----------|
| <!-- REPLACE --> | <!-- REPLACE --> | <!-- REPLACE --> | <!-- REPLACE --> | <!-- REPLACE --> | <!-- REPLACE: URL or TBD --> | <!-- REPLACE: epics/<ID>.md or — --> |

> Phasing and priorities: see `roadmap.md`
