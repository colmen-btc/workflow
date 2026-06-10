You are doing a production-grade PR review. Review PR: <https://github.com/47lining/edi-mcp-server/pull/77> in repo <edi-mcp-server>.
you can find adr/epics over here <C:\Projects\DataOps\product-workspace\initiatives\edi-mcp-server> or in GH issues <https://github.com/47lining/edi-mcp-server/issues>.

Review objectives:
1. Perform a code-review-first assessment (findings first, severity ordered).
2. Cross-check alignment with:
   - linked issue(s) (story/bug/chore/docs/refactor),
   - epic requirements,
   - ADR references mentioned in PR/issue/body/comments.
3. Validate behavior, not just style:
   - regressions, edge cases, retry/error handling, logging, security implications.
4. Evaluate tests:
   - coverage of changed behavior,
   - missing negative-path and integration scenarios.
5. Check CI/readiness:
   - status checks, review requirements, merge blockers.

Output format (strict):
- Findings
  - Critical: ...
  - High: ...
  - Medium: ...
  - Low: ...
  For each finding include:
  - file and line reference (if available),
  - why it matters,
  - concrete fix.
- Cross-check Matrix
  - Requirement | Source (Issue/Epic/ADR) | PR Evidence | Status (Met/Partial/Missing)
- Open Questions / Assumptions
- Merge Recommendation
  - Approve / Request Changes / Comment-only
  - short rationale
- Optional follow-ups (non-blocking)

Review rules:
- If no defects are found, explicitly say “No blocking findings found.”
- Do not give generic praise without evidence.
- Distinguish blocking issues from nice-to-have improvements.
- If ADRs/issues are referenced but not present, flag as “traceability gap” and propose exact follow-up.
- Keep conclusions concise and actionable.
