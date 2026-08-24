# Repository Governance Standard

Status: ACTIVE
Owner: DonMassa84
Scope: All repositories under the account

## 1. Naming convention

All maintained repositories use lowercase kebab-case only.

Allowed pattern:

`^[a-z0-9]+(?:-[a-z0-9]+)*$`

Do not use:
- underscores
- spaces
- leading/trailing hyphens
- CamelCase or ALL CAPS
- personal names inside technical repo names unless the repository is explicitly a personal portfolio
- dates in active product names
- suffixes such as `new`, `2`, `3`, `final`, `ultimate`, `full-bundle`

## 2. Canonical domain prefixes

- `shadowops-*` — ShadowOps production, integrations, runtime, evidence, tooling
- `shadowmaker-*` — personal platform/tooling not part of ShadowOps runtime
- `eva-*` — EVA-specific agents, workflows, research
- `ihk-*` — IHK learning/project/evidence repositories
- `career-*` — applications, CV tooling, job automation
- `community-*` — civic/community projects
- `lab-*` — experiments and proofs of concept
- `archive-*` — frozen historical repositories

A project should have one canonical active repository. Historical variants are archived, not versioned by creating `-2`, `-3`, `new`, `ultimate`, etc.

## 3. Lifecycle states

Every repository is assigned exactly one lifecycle state:

- `PRODUCTION` — deployable or operational system
- `ACTIVE` — maintained development project
- `REFERENCE` — useful knowledge/data, not deployed
- `ARCHIVE` — frozen historical content
- `MIGRATE` — temporary state while content is moved to canonical repo

## 4. Standard branches

- default branch: `main`
- feature: `feat/<short-name>`
- fix: `fix/<short-name>`
- hardening: `hardening/<short-name>`
- docs: `docs/<short-name>`
- release: `release/vX.Y.Z`

No repository should use a feature branch or `gh-pages` as its canonical source branch.

## 5. Standard repository layout

```text
README.md
LICENSE                 # when distributable
.gitignore
.github/
  workflows/
docs/
src/ or apps/           # implementation
scripts/                 # operational scripts
tests/ or test/          # automated tests
config/                  # non-secret config only
```

Optional:

```text
evidence/                # generated/curated acceptance evidence
infra/                   # IaC/deployment definitions
examples/
```

Never commit runtime secrets, private raw exports, tokens, credentials, local databases, generated caches or personal source data.

## 6. README contract

Every active repository README should state:

1. Purpose
2. Lifecycle status
3. Canonical repository / predecessor if relevant
4. Architecture or main components
5. Setup
6. Test / quality command
7. Security and data-handling note
8. Release/deployment method when applicable

## 7. Consolidation rules

- One product = one canonical repo.
- Duplicate/v2/v3 repos are merged or archived.
- Experimental code moves under `lab-*` or into a `labs/` directory of the canonical project.
- Documentation-only mirrors should point to the canonical implementation instead of creating another competing product identity.
- Production repositories must not depend on unpinned mutable branches from experimental repositories.

## 8. ShadowOps canonical topology

- `shadowops-production` — canonical production/release repository
- `shadowops` — development/integration repository until migration is complete
- `shadowops-logs` — operational evidence/log tooling only; no raw secrets or private message contents
- `shadowops-ollama-aio-setup` — local AI runtime setup component; candidate for `shadowops-ollama-runtime`

After migration, production releases originate only from `shadowops-production`.
