# EVA-Mirror Recovery Classification

Status: RECOVERY_SET_CREATED

## Decision

`DonMassa84/EVA` remains the canonical source for future `eva-core`.
`DonMassa84/EVA-Mirror` is treated as a migration source with divergent history, not as a second active core.

## Mirror-only commit classification

### 1cd0e09 — EVA v1.1 Agent upgrade
- `eva_loader.py` — SOURCE — RECOVERED_FOR_REVIEW

### 1b4abc6 — ShadowSync / dashboard / token
- `dashboard_phase5.py` — SOURCE/UI — RECOVERED_FOR_REVIEW
- `shadow_sync.py` — SOURCE — RECOVERED_FOR_REVIEW
- `get_eva_token.sh` — SECURITY_REJECT_AS_IS
  - password variables in script
  - Resource Owner Password grant pattern
  - not suitable for hardened core without redesign

### 0c3633f — EVA AutoSync workflow
- `.github/workflows/eva-sync.yml` — CONFIG/CI — REJECT_AS_IS
  - appends text bytes to PDF files
  - commits/pushes mutations from scheduled CI
  - unsafe and non-deterministic for canonical core

### 0ae6b28 — Shadowmind export workflow
- `.github/workflows/shadowmind_export.yml` — INVALID_CONFIG — REJECT
  - content consists of shell commands rather than a valid Actions workflow definition

### b780be7 — EVA autonomy mode
- `modules/run_prompt.py` — SOURCE/PROTOTYPE — RECOVERED_FOR_REVIEW
- `agents/decision_core.ts` — SOURCE candidate — requires separate content review
- `agents/observer_agent.ts` — SOURCE candidate — requires separate content review
- `modules/autonomous_loop.py` — SOURCE candidate — requires separate content review
- `modules/executor_module.py` — SOURCE candidate — requires separate content review

### 7b6a0dd — AutoPush bundle
Mixed commit; do not cherry-pick wholesale.
- `__pycache__`, `venv/pyvenv.cfg`, logs — CACHE/GENERATED — REJECT
- `Makefile` — CONFIG — REVIEW; contains auto-commit/push and hard-coded webhook behavior
- `watch_sorter.py` — SOURCE/LOCAL_AUTOMATION — HOLD; hard-coded user filesystem paths
- `EVA_agents_backup.yml` — BACKUP/CONFIG — HOLD; not authoritative while active agent config exists
- `shadowmind.json` — RUNTIME_STATE — DO_NOT_PROMOTE_TO_CORE

### 61640d8 — Reload + ZIP export
Mixed generated/export/prompt material. Do not cherry-pick wholesale.
- `eva_autostart_prompt.sh` / prompt selector — local tooling; HOLD/SEPARATE_TOOLING
- prompt JSON examples — content library; move only if a canonical prompt-library role is created
- `eva_gitlog.txt` and daily logs — GENERATED — REJECT

### 463b42d — QA commit
Heavily contaminated with `.venv`, `site-packages`, `__pycache__` and compiled Python artifacts. Do not cherry-pick.

## Recovery branch

A safe recovery branch was created in `DonMassa84/EVA`:

`migration/eva-mirror-unique-source`

Recovered into `legacy/mirror-recovered/`:
- `eva_loader.py`
- `dashboard_phase5.py`
- `shadow_sync.py`
- `run_prompt.py`
- recovery README with explicit rejection list

These files are isolated and are not active runtime code.

## Remaining gate before EVA-Mirror can be archived

1. Inspect four source candidates with missing patches from `b780be7`.
2. Search mirror-only history for other source/config files not already in EVA.
3. Decide whether prompt JSON material belongs in `eva-workflows`, `eva-agents`, or a separate prompt library.
4. Review current EVA `.gitignore` against `.venv`, `venv`, `__pycache__`, `*.pyc`, logs and ZIP exports.
5. Merge only reviewed recovery material.
6. Record final archive decision.
