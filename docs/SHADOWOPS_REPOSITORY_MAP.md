# ShadowOps Repository Map

Status: CANONICAL

## Repository roles

| Current repository | Canonical role | Target name | Lifecycle |
|---|---|---|---|
| `shadowops-production` | release / production control plane | `shadowops-production` | PRODUCTION |
| `shadowops` | active application development | `shadowops-development` | ACTIVE / MIGRATE |
| `shadowops-ollama-aio-setup` | local AI runtime, Ollama orchestration and deployment tooling | `shadowops-ollama-runtime` | ACTIVE / MIGRATE |
| `shadowops-logs` | generated reports, audit/evidence and operational snapshots | `shadowops-evidence` | REFERENCE / MIGRATE |
| `shadowops-knowledge` | runbooks, known issues, reviews, templates and reusable operational knowledge | `shadowops-knowledge` | ACTIVE |

## Canonical responsibility boundaries

### shadowops-production
Contains only production/release-facing material: release manifests, deployment definitions, production CI/CD, architecture contracts, governance, acceptance evidence pointers and release documentation. It must not become a dumping ground for experiments or generated logs.

### shadowops-development
Contains application source, agents, adapters, APIs, UI/backend code, tests and development automation. Current `shadowops` is the source repository for this role.

### shadowops-ollama-runtime
Contains Ollama/local-AI deployment and orchestration assets, runtime scripts, model setup, prompts required by the runtime and runtime-specific documentation. Current `shadowops-ollama-aio-setup` is the source repository for this role.

### shadowops-evidence
Contains generated reports, audit exports, verification snapshots and historical operational evidence. It must not contain authoritative application source.

### shadowops-knowledge
Contains curated human-readable knowledge: runbooks, infrastructure notes, known issues, reviews, templates and knowledge-ingestion material. Generated runtime logs belong in `shadowops-evidence`, not here.

## Standard top-level layout

Application repositories should converge on:

```
.github/
docs/
src/ or native application source directories
tests/
scripts/
config/
ops/
README.md
LICENSE (when appropriate)
.gitignore
```

Specialized repositories may omit irrelevant directories, but must not invent duplicate synonyms such as `script/`, `tools-scripts/`, `documentation/` when `scripts/` or `docs/` already serve the purpose.

## Migration rules

1. Never delete source history as part of normalization.
2. Do not copy secrets, generated credentials, local state, caches or runtime databases.
3. Preserve production and development separation.
4. Move generated reports out of source repositories into the evidence role where practical.
5. Keep curated runbooks and knowledge separate from generated evidence.
6. Rename repositories only after references, workflows and deployment dependencies have been inventoried.
7. After a rename, update remotes, badges, Actions references, documentation and service configuration before declaring migration complete.

## Current assessment

- `shadowops` is materially the development/source repository and already uses `main`.
- `shadowops-production` currently holds governance/release scaffolding and is suitable as the canonical production repository.
- `shadowops-logs` contains reports and repo snapshots, therefore `shadowops-evidence` describes its function more accurately.
- `shadowops-ollama-aio-setup` contains deployment/orchestration scripts and runtime documentation, therefore `shadowops-ollama-runtime` is the canonical name.
- `shadowops-knowledge` already has a coherent knowledge/runbook structure and keeps its name.

## Gate for repository renames

A repository is READY_TO_RENAME only when:
- dependency/reference search completed;
- GitHub Actions references checked;
- local deployment/service references checked;
- replacement name is unoccupied;
- rollback procedure recorded;
- no destructive content migration is pending.
