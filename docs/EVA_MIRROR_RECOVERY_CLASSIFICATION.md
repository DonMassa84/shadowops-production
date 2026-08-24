# EVA-Mirror Recovery Classification

Status: ARCHIVE_READY_AFTER_RECOVERY_REVIEW

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
- `agents/decision_core.ts` — EMPTY_FILE — REJECT
- `agents/observer_agent.ts` — EMPTY_FILE — REJECT
- `modules/autonomous_loop.py` — EMPTY_FILE — REJECT
- `modules/executor_module.py` — EMPTY_FILE — REJECT

All four previously unresolved autonomy candidates resolve to the Git empty-blob SHA `e69de29bb2d1d6434b8b29ae775ad8c2e48c5391`; they contain no source to preserve.

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

A safe recovery branch exists in `DonMassa84/EVA`:

`migration/eva-mirror-unique-source`

Recovered into `legacy/mirror-recovered/`:
- `eva_loader.py`
- `dashboard_phase5.py`
- `shadow_sync.py`
- `run_prompt.py`
- recovery README with explicit rejection list

These files are isolated and are not active runtime code. Draft PR: `DonMassa84/EVA#1`.

## Archive decision

`EVA-Mirror` is now technically `ARCHIVE_READY`, subject to one operational condition: keep Draft PR #1 or otherwise retain the isolated recovered source candidates before archiving the mirror.

The mirror is not required as an active core repository because:
1. canonical development continues from `EVA`;
2. shared history is already present in `EVA`;
3. identified unique source candidates have been isolated for review;
4. unresolved autonomy candidates were verified as empty files;
5. unsafe CI, caches, environments, generated logs and runtime state were explicitly rejected.

## Optional follow-up, not an archive blocker

- decide whether prompt JSON examples deserve a dedicated `eva-prompts`/knowledge location;
- harden and selectively promote recovered prototypes only after tests/security review;
- ensure canonical EVA `.gitignore` excludes `.venv/`, `venv/`, `__pycache__/`, `*.pyc`, logs and generated ZIPs.

No repository content should be deleted as a substitute for GitHub's archive setting.