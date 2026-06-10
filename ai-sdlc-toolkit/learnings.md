## ADR Organization
- ADRs live at product-workspace level
- ADR structure mirrors repo organization (edi-mcp-server, agent, UI)
- Atleast a high level ADR's need to be created first (see adr-list)

## Epic Requirements
- Link to applicable ADRs in additional context section
- Track status against GitHub issues
- Use templates or skills to generate new epics for consistency

## Feature Requirements
- Link the ADR's to the realted features

## Workflow Skills
- Review available relavent ADRs before starting
- Reference agent model during GitHub PRs and branch pushes

## Source of Truth
- GitHub is the single source of truth for stable context and execution decisions.
- Keep epic, feature, and task context current in GitHub issues so collaboration is easy and centralized.

## Knowledge Graph (Graphify)
- Run `graphify .` at project root after setting up an initiative to build the knowledge graph.
- Agents should read `graphify-out/GRAPH_REPORT.md` during the Explore phase before grepping files.
- After creating or updating ADRs, run `graphify . --update` to keep graph context current.
- The graph surfaces cross-cutting relationships (god nodes, surprising connections) that are hard to discover by reading files linearly.
- Commit `graphify-out/` to the repo; exclude `manifest.json` and `cost.json` via `.gitignore`.
