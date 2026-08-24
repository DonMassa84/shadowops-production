# ShadowOps Production Acceptance

ShadowOps may only be labelled `PRODUCTION_READY` when every required gate is PASS.

## Required gates

- Runtime health and readiness
- Format / compile / test
- Real-data connector verification
- Zero-Trust and privacy controls
- Audit-chain verification
- Secret scanning / no credential leakage
- Deterministic backup and restore
- Observability (`/health`, `/ready`, `/metrics`, logs)
- UI end-to-end validation
- Restart/recovery validation
- Clean release tree
- Reproducible build

## Final status

```text
RUNTIME=PASS
FORMAT=PASS
COMPILE=PASS
TESTS=PASS
REAL_DATA=PASS
CONNECTORS=PASS
ZERO_TRUST=PASS
PRIVACY=PASS
AUDIT_CHAIN=PASS
SECRETS=PASS
BACKUP_RESTORE=PASS
OBSERVABILITY=PASS
UI_E2E=PASS
RESTART_RECOVERY=PASS
CLEAN_WORKTREE=PASS
REPRODUCIBLE_BUILD=PASS

FINAL_STATUS=PRODUCTION_READY
```

Until all gates pass, use `NOT_PRODUCTION_READY` or `CODE_PRODUCTION_READY` as applicable.
