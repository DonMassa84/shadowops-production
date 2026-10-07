# ShadowOps Repository Map

Status: CANONICAL

## Repository roles

| Current repository | Canonical role | Target name | Lifecycle |
|---|---|---|---|
| `shadowops-production` | release / production control plane | `shadowops-production` | PRODUCTION |
| `shadowops` | active application development | `shadowops-development` | ACTIVE / MIGRATE |
| `shadowops-mission-control-v2` | Mission Control UI, i7 kiosk display, prioritized sanitized status projection | `shadowops-mission-control` | ACTIVE / REVIEW-NAME |
| `shadowops-ollama-aio-setup` | local AI runtime, Ollama orchestration and deployment tooling | `shadowops-ollama-runtime` | ACTIVE / MIGRATE |
| `shadowops-logs` | generated reports, audit/evidence and operational snapshots | `shadowops-evidence` | REFERENCE / MIGRATE |
| `shadowops-knowledge` | runbooks, known issues, reviews, templates and reusable operational knowledge | `shadowops-knowledge` | ACTIVE |

## Canonical responsibility boundaries

### shadowops-production
Contains only production/release-facing material: release manifests, deployment definitions, production CI/CD, architecture contracts, governance, acceptance evidence pointers and release documentation. It must not become a dumping ground for experiments or generated logs.

### shadowops-development
Contains application source, agents, adapters, APIs, backend code, tests and development automation. Current `shadowops` is the source repository for this role.

### shadowops-mission-control
Contains the Phoenix/LiveView operations console, mission boards, i7 kiosk display routes, display control and sanitized priority/status projections. Runtime secrets and private source data stay outside this repository. Current source repository: `shadowops-mission-control-v2`.

Known display/application routes include:
- `/mission`
- `/mission/projects`
- `/mission/career`
- `/mission/ihk`
- `/mission/infrastructure`
- `/mission/display`
- `/mission/display/control`

The repository is a consumer/presentation layer, not the canonical store for sensitive raw Gmail, financial, legal or personal case data.

### shadowops-ollama-runtime
Contains Ollama/local-AI deployment and orchestration assets, runtime scripts, model setup, prompts required by the runtime and runtime-specific documentation. Current `shadowops-ollama-aio-setup` is the source repository for this role.

### shadowops-evidence
Contains generated reports, audit exports, verification snapshots and historical operational evidence. It must not contain authoritative application source.

### shadowops-knowledge
Contains curated human-readable knowledge: runbooks, infrastructure notes, known issues, reviews, templates and knowledge-ingestion material. Generated runtime logs belong in `shadowops-evidence`, not here.

## i7 / kiosk data flow

```text
private sources (Gmail / Calendar / case archives)
                     |
                     v
             sanitize + prioritize
                     |
                     v
       shadowops-mission-control-v2
                     |
                     v
             Git / sync worker
                     |
                     v
                i7 kiosk
```

A GitHub commit is not proof of a successful physical i7 synchronization. Success requires consumer acknowledgement / verified display state.

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
3. Preserve production, development, presentation and evidence separation.
4. Move generated reports out of source repositories into the evidence role where practical.
5. Keep curated runbooks and knowledge separate from generated evidence.
6. Rename repositories only after references, workflows and deployment dependencies have been inventoried.
7. After a rename, update remotes, badges, Actions references, documentation and service configuration before declaring migration complete.
8. Do not create another Kiosk/Mission-Control repository while `shadowops-mission-control-v2` remains the active implementation unless an independently deployable lifecycle is proven.

## Current assessment

- `shadowops` is materially the development/source repository and already uses `main`.
- `shadowops-production` holds governance/release scaffolding and is suitable as the canonical production repository.
- `shadowops-mission-control-v2` is the active Mission Control / i7 kiosk UI. Earliest currently verified commit: 2026-10-02.
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
