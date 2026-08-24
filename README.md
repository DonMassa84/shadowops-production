# ShadowOps Production

Production-focused repository for ShadowOps.

## Purpose

This repository contains the production-hardened ShadowOps control plane, Mission Control UI, governance controls, recovery tooling, and production acceptance evidence.

## Production principles

- Feature freeze until production acceptance is green
- Real data only for production evidence
- Zero Trust / fail-closed write paths
- Human approval for external effects
- Auditable operations
- Deterministic backup and restore validation
- Reproducible CI acceptance
- No secrets or private raw data in the repository

## Source baseline

Initial production baseline is derived from `DonMassa84/ihk-document-ai` branch `hardening/shadowops-production-ready`.

## Target acceptance

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
