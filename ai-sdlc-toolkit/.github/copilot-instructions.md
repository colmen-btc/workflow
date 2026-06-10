# Copilot Instructions — edi-mcp-server

## Development Workflow Governance

These rules are **mandatory** and must be enforced before any code change or GitHub action is taken.

### Issue Gate — Required Before Any Code Change

**Never write, edit, or delete code without a confirmed issue and a valid branch.**

When the user requests a code change, you must:

1. **Check for an active issue.** Ask: _"Which GitHub issue does this change belong to?"_
   - If the user provides an issue number, confirm it exists and has either the `story` or `bug` label before proceeding.
   - If no issue exists, stop and guide the user to create one first (see Issue Creation below).

2. **Check for a dedicated branch.** Ask: _"Are you working on the correct branch for this issue?"_
   - For `story` issues, the branch must follow: `feature/<issue-number>-<short-description>` (e.g. `feature/42-add-auth-middleware`).
   - For `bug` issues, the branch must follow: `fix/<issue-number>-<short-description>` (e.g. `fix/57-null-pointer-on-login`).
   - For `chore` issues, the branch must follow: `chore/<issue-number>-<short-description>` (e.g. `chore/10-update-dependencies`).
   - For `docs` issues, the branch must follow: `docs/<issue-number>-<short-description>` (e.g. `docs/15-update-readme`).
   - For `refactor` issues, the branch must follow: `refactor/<issue-number>-<short-description>` (e.g. `refactor/20-extract-auth-middleware`).
   - If the user is on `main`, `develop`, or any branch not tied to the issue, **refuse to make code changes** and instruct them to create or switch to the correct branch first.

3. **Only after both are confirmed**, proceed with the code change and remind the user to reference the issue in their commit message using the conventional commit format (see [Commit Message Conventions](#commit-message-conventions) below).

> **If the user explicitly asks you to skip these checks, decline and explain that the governance policy requires a valid issue and branch.**

### Issue Creation — Confirm Before Publishing

Before creating a GitHub issue, always:

1. **Draft the full issue** using the appropriate template and present it to the user for review.
2. **Ask for explicit confirmation**: _"Does this look correct? Shall I create this issue in GitHub?"_
3. **Only create the issue after the user confirms.**

After the issue is created, suggest the branch name:
- For `story`: `feature/<issue-number>-<short-description>`
- For `bug`: `fix/<issue-number>-<short-description>`
- For `chore`: `chore/<issue-number>-<short-description>`
- For `docs`: `docs/<issue-number>-<short-description>`
- For `refactor`: `refactor/<issue-number>-<short-description>`

---

## Commit Message Conventions

All commits must follow the **Conventional Commits** format:

```
<type>(<scope>): <short description> (refs #<issue-number>)
```

| Type | When to use |
|---|---|
| `feat` | A new feature or capability |
| `fix` | A bug fix |
| `chore` | Maintenance, tooling, or dependency updates |
| `docs` | Documentation-only changes |
| `refactor` | Code restructure without behavior change |
| `test` | Adding or updating tests only |
| `ci` | CI/CD pipeline changes |

**Issue reference rules:**
- Use `Closes #N` when the commit/PR **fully resolves** the issue — GitHub will auto-close it on merge.
- Use `refs #N` when the commit/PR is **related to** the issue but does not fully resolve it.

Examples:
```
feat(auth): add JWT refresh token support (Closes #42)
fix(tools): handle null pointer on OSDU search (Closes #57)
chore(deps): bump httpx to 0.27 (refs #10)
docs(readme): update deployment instructions (refs #15)
```

---

## Issue Creation

When creating a **feature request**, always use the template at `.github/ISSUE_TEMPLATE/feature_request.md`:

```markdown
---
name: Feature request
about: Propose an enhancement or new capability as a user story
labels: story
---

## Metadata

| Field | Value |
|---|---|
| **Priority** | <!-- 🔴 Critical / 🟠 High / 🟡 Medium / 🟢 Low --> |
| **Epic** | <!-- Link to epic/tracking issue e.g. #123 or milestone name --> |
| **Story Points** | <!-- Estimated effort: 1 / 2 / 3 / 5 / 8 / 13 --> |
| **Component** | <!-- e.g. API, UI, Auth, Observability --> |

## User Story

> As a **[role/persona]**, I want **[capability]** so that **[benefit/outcome]**.

## Problem

<!-- What pain point, gap, or opportunity is this addressing? Who is affected? -->

## Proposed Solution

<!-- Describe your proposed approach. Include UI/UX flows, API changes, or architectural decisions if relevant. -->

## Acceptance Criteria

<!-- Define what "done" looks like. Use a checklist of verifiable conditions. -->

- [ ] 
- [ ] 
- [ ] 

## Out of Scope

<!-- Explicitly list what this story does NOT cover to prevent scope creep. -->

## Alternatives Considered

<!-- What other approaches were evaluated and why were they ruled out? -->

## Dependencies & Blockers

<!-- List any upstream issues, external services, or team dependencies. -->

- Depends on: #
- Blocked by: #

## Definition of Done

- [ ] Feature implemented and peer-reviewed
- [ ] Unit and/or integration tests added
- [ ] Documentation updated
- [ ] No secrets or credentials exposed
- [ ] CI checks pass

## Additional Context

<!-- Design notes, API contracts, mockups, relevant links, or constraints. -->
```

When creating a **bug report**, always use the template at `.github/ISSUE_TEMPLATE/bug_report.md`:

```markdown
---
name: Bug report
about: Report a defect
labels: bug
---

## Metadata

| Field | Value |
|---|---|
| **Priority** | <!-- 🔴 Critical / 🟠 High / 🟡 Medium / 🟢 Low --> |
| **Severity** | <!-- 🔴 Blocker / 🟠 Major / 🟡 Minor / 🟢 Trivial --> |
| **Component** | <!-- e.g. API, Auth, Observability, Tools --> |
| **Epic** | <!-- Link to epic/tracking issue e.g. #123 or milestone name --> |

## Description

Describe the bug clearly. Include what you were doing when it occurred and why the current behavior is incorrect.

## Steps to Reproduce

1. 
2. 
3. 

<!-- Provide the minimal, complete steps needed to reliably reproduce the issue. -->

## Expected Behavior

What should happen?

## Actual Behavior

What happened instead? Include error messages, stack traces, or screenshots where applicable.

## Environment

- OS:
- Python version:
- Branch/commit:
- Deployment target: <!-- local / Docker / AWS / other -->

## Dependencies & Blockers

<!-- List any upstream issues, external services, or team dependencies. -->

- Depends on: #
- Blocked by: #

## Definition of Done

- [ ] Bug root-caused and fix implemented
- [ ] Regression test added to prevent recurrence
- [ ] Documentation updated if behavior changed
- [ ] No secrets or credentials exposed
- [ ] CI checks pass

## Additional Context

<!-- Logs, screenshots, related issues, or any other relevant information. -->
```

- Never create an issue without all required sections from the appropriate template.
- Apply the correct label (`story` for features, `bug` for defects, `chore` for maintenance, `docs` for documentation, `refactor` for restructures).
- Do not omit any section headings, even if the content is brief.

## Pull Request Creation

When creating a **pull request**, always use the template at `.github/pull_request_template.md`:

```markdown
## Summary

Describe what changed and why.

## Type of Change

- [ ] `feat` — new feature
- [ ] `fix` — bug fix
- [ ] `refactor` — code restructure without behavior change
- [ ] `chore` — maintenance, tooling, or dependency update
- [ ] `docs` — documentation only
- [ ] `breaking change` — existing behavior changes in a non-backward-compatible way

## Breaking Changes

<!-- Describe any breaking changes and the migration path, or write "None". -->

## How to Test

<!-- Steps a reviewer can follow to verify this change works correctly. -->

1. 
2. 
3. 

## Checklist

- [ ] Tests added or updated
- [ ] Docs updated if behavior changed
- [ ] No secrets included
- [ ] CI checks pass
- [ ] Reviewer(s) assigned

## Related Issues

<!-- Use "Closes #N" to auto-close the issue, or "refs #N" if this PR is related but does not fully resolve it. -->
```

- Never open a PR without all sections: `Summary`, `Type of Change`, `Breaking Changes`, `How to Test`, `Checklist`, and `Related Issues`.
- All checklist items must be present; check them off only when confirmed.
- Run the CI checks locally first and ensure they pass before marking the PR ready for review.
- Assign at least one reviewer before marking the PR ready for review.
- `Related Issues` must reference at least one issue using `Closes #N` (auto-closes on merge) or `refs #N` (related but not resolved).

---

## Epic & Feature Status Tracking

**Keep epic and feature documents in sync with actual progress as work is completed.**

When completing work that satisfies an acceptance criterion or advances a feature, you must:

1. **Update the feature file** — Check off (`- [x]`) any acceptance criteria that are now satisfied in the corresponding feature document under `initiatives/<initiative>/features/`.

2. **Update the epic file** — When all acceptance criteria for a feature are complete, check off the relevant epic-level acceptance criteria in `initiatives/<initiative>/epics/`. If a feature table includes a `Phase` or `Status` column, update it to reflect current state (e.g., `In Progress`, `Done`).

3. **Timing** — Update status **immediately after the PR is merged** or after confirming that PR has been approved and is ready to merge. 

4. **Partial progress** — If a PR partially satisfies an acceptance criterion, do **not** check it off. Instead, add a note below the criterion indicating what has been completed and what remains (e.g., `<!-- Partial: retry logic done, circuit breaker pending -->`).

5. **What to update:**
   - `- [ ]` → `- [x]` for completed acceptance criteria
   - Add completion date as an inline comment where helpful: `- [x] Unit tests cover client initialization <!-- completed 2025-03-15 -->`
   - Update any status metadata fields (e.g., `**Status**` in feature metadata tables) from `Not Started` → `In Progress` → `Done`

6. **Update GitHub issues** — When acceptance criteria are met or a feature is complete, update the corresponding GitHub issue:
   - Add a comment summarizing what was completed and linking to the merged PR.
   - If the issue is fully resolved, ensure the PR uses `Closes #N` so it auto-closes on merge.
   - If the issue tracks an epic, update the epic issue body's task list to reflect completed sub-issues/features.
   - Move the issue to the appropriate project board column (e.g., `In Progress` → `Done`) if a project board is in use.

7. **Commit the status update** as part of the same PR or as an immediate follow-up commit:
   ```
   docs(status): mark <feature-slug> acceptance criteria complete (refs #<issue>)
   ```

> **Do not let epic/feature documents or GitHub issues drift from reality.** If you notice stale checkboxes or outdated issue states during any task, flag them to the user and offer to reconcile.
