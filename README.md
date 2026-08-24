# ShadowOps Production

Canonical production/release repository for ShadowOps.

## Repository portfolio governance

This repository also hosts the canonical repository-governance documents for the DonMassa84 portfolio:

- `docs/REPOSITORY_GOVERNANCE.md` — naming, lifecycle and structure standard
- `docs/REPOSITORY_MIGRATION_PLAN.md` — portfolio-wide migration plan
- `docs/SHADOWOPS_REPOSITORY_MAP.md` — ShadowOps repository family
- `docs/CORE_REPOSITORY_MAP.md` — IHK, Career, Portfolio, Community and AI-Lab classification

## Production scope

Only production/release-facing ShadowOps assets belong here: release manifests, deployment definitions, production CI/CD, architecture contracts, governance and production acceptance material.

Development experiments, generated logs and general knowledge are intentionally kept in separate repositories.

## Naming standard

Maintained repositories use lowercase kebab-case and `main` as the default branch. Duplicate/version-suffix repositories are migration sources, not new canonical products.

## Safety

No repository is deleted during normalization. A predecessor is archived only after unique content, references and deployment behavior have been verified in its canonical target.
