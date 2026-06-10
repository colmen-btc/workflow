# Release Gate Checklist

> Must pass before deploying to production.

## Quality

- [ ] All features in release scope pass integration tests
- [ ] Regression suite passes
- [ ] Staging deployment verified with smoke tests

## Security

- [ ] No critical/high CVEs unresolved
- [ ] Security review completed (scope-dependent)

## Compliance

- [ ] SBOM generated for this release
- [ ] Change log approved by PM
- [ ] Full traceability verified: every PR → task → feature → epic

## Observability

- [ ] Dashboards live for this release
- [ ] Alert thresholds configured
- [ ] Rollback criteria defined

## Release

- [ ] Release notes reviewed by PM
- [ ] Monitoring window defined (duration, escalation contact)
- [ ] Rollback plan documented
