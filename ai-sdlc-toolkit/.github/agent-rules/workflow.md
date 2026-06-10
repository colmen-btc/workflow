# Agent Workflow

## Explore → Plan → Implement

For any change touching 2+ files or an unfamiliar area:

1. Explore — read relevant files, understand the current state; make no changes
   - If `graphify-out/GRAPH_REPORT.md` exists, read it first for god nodes, surprising connections, and structural context
   - Use `/graphify query "<topic>"` to find relationships between components before grepping through files
2. Plan — write out what files change and why; confirm with user if scope is large
3. Implement — execute against the plan; stop if reality diverges from the plan

For a single-file or obvious fix: skip to implement directly.

## Brownfield Changes (existing systems)

When the work changes, re-platforms, or retires an existing system, do the reverse phase before forward planning:

1. Context acquisition — gather evidence from every reachable source (code via graphify, git, and Jira/Confluence/Slack via their MCP servers) into `assessments/<system>/source-inventory.md` + `evidence-ledger.md`. Log unreachable sources as gaps.
2. AS-IS extraction — recover the system as `system-overview.md`, extracted epics/features, and discovered ADRs (`Status: Discovered`).
3. Forward delta — express the target as keep/change/add/retire against the AS-IS; never plan a re-platform without the recovered baseline.

Every extracted artifact must cite evidence ids and carry a confidence level (High/Medium/Low). Code wins for "what exists"; tickets/docs/Slack supply rationale and may be stale — log contradictions, don't resolve them silently.

## Verification

- After implementing, run the relevant test, lint, or build command
- If no automated check exists, state what manual step would confirm correctness
- IMPORTANT: Never claim work is complete without evidence it works

## Scope Creep Guard

- If exploration reveals a larger problem than asked, surface it before touching it
- One PR / one concern — don't bundle unrelated fixes

## Context Hygiene

- Start a fresh task with clean context when switching topics
- If the same mistake happens twice, stop and restate the goal more precisely before retrying
- When `graphify-out/` exists, prefer graph queries over brute-force file searches for cross-cutting context
- After significant code or doc changes, run `graphify . --update` to keep the graph current
