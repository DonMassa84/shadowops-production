# EVA vs EVA-Mirror Comparison

Status: PARTIAL_COMPARISON_COMPLETE

## Findings

1. `EVA` and `EVA-Mirror` share substantial commit history. Several commits are byte-identical by SHA in both repositories, including `72ae34fa...`, `f1e8976c...`, `8835e5ec...` and `26bedb5d...`.
2. Their current `README.md` files are byte-identical (`57f29906...`) and explicitly describe `DonMassa84/EVA` as the central repository.
3. The histories later diverged.
   - `EVA-Mirror` contains later mirror-side commits such as `1cd0e093...`, `1b4abc6a...`, `98cf9854...`, `0c3633f6...`, `0ae6b281...`, `7b6a0ddf...`, `61640d8c...`, `b780be76...`, `dac39584...` and `463b42df...`.
   - `EVA` later contains independent commits including `1a5c9d3d...` and latest inspected commit `678709b0...` from 2025-07-26.
4. The latest inspected `EVA-Mirror` commit (`463b42df...`) is heavily polluted by committed `.venv`, `site-packages` and Python cache artifacts. These artifacts must not be imported into a canonical core repository.
5. The latest inspected `EVA` commit adds a GitHub Actions workflow for n8n deployment discovery. It is real source/configuration material rather than environment cache data, but the filename itself (`.github/workflows/debug-workflow yml`) should be normalized before production use.

## Decision

### Canonical core base
`DonMassa84/EVA` is the preferred **base repository for future `eva-core`** because:
- both READMEs identify it as the central repository;
- it contains later independent development after the common history;
- its latest inspected change is source/workflow material rather than virtual-environment cache pollution.

### Mirror status
`DonMassa84/EVA-Mirror` is **NOT safe to archive yet**. It contains a divergent commit sequence after the shared history and therefore may contain unique functional changes.

It is reclassified as:

`MIGRATION_SOURCE_UNIQUE_CHANGES -> eva-core/eva-archive`

## Required migration filter

Never migrate from `EVA-Mirror` blindly. Exclude at minimum:

```
.venv/
venv/
__pycache__/
*.pyc
*.pyo
.pytest_cache/
.cache/
logs/
```

Also inspect generated ZIP/export/archive files before migration.

## Next comparison work

For each mirror-only commit after the common history:
1. inspect changed filenames;
2. classify each change as SOURCE / CONFIG / DOC / GENERATED / CACHE / SECRET-RISK;
3. migrate only SOURCE, CONFIG and relevant DOC changes into the canonical EVA base;
4. reject generated/cache artifacts;
5. run tests/build after migration;
6. only then mark `EVA-Mirror` as `ARCHIVE_READY`.

## Current lifecycle

| Repository | Status |
|---|---|
| `EVA` | CANONICAL_BASE / target rename `eva-core` |
| `EVA-Mirror` | MIGRATION_SOURCE_UNIQUE_CHANGES |
| `EVA2` | ARCHIVE_CANDIDATE |
| `BlackOps-EVA` | ARCHIVE_CANDIDATE |
| `eva-os-ultimate` | ARCHIVE_CANDIDATE |

No destructive action has been taken.