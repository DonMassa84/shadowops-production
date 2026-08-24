# Duplicate Repository Family Map

Status: PHASE_3_CLASSIFIED

No repository is deleted by this plan. `ARCHIVE_CANDIDATE` means compare/verify first, then archive using repository settings.

## EVA family

Canonical topology:
- `eva-core` — primary EVA platform/core
- `eva-agents` — independently reusable agents/templates
- `eva-workflows` — multi-agent/workflow definitions
- `eva-video-analysis` — independently deployable video-analysis component
- `eva-archive` — historical snapshots/mirrors only

Classification:

| Current | Evidence | Target role | Status |
|---|---:|---|---|
| `EVA` | ~199 MB | source for `eva-core` | MIGRATION_SOURCE |
| `EVA-Mirror` | ~221 MB | mirror/snapshot | COMPARE_WITH_EVA |
| `spiegelkern-eva` | ~1.9 MB | specialized/legacy core candidate | REVIEW_FOR_CORE |
| `eva-agent-template` | small template | `eva-agents` input | MIGRATE |
| `EVA_IntelligentAgent` | small agent repo | `eva-agents` input | MIGRATE |
| `eva-multiagent-workflows` | workflow repo | `eva-workflows` input | MIGRATE |
| `eva-video-analysis` | dedicated component | keep canonical name | ACTIVE |
| `eva-skill3-informationsverarbeitung` | skill-specific | agents/workflows or archive | REVIEW |
| `EVA2` | tiny numbered variant | archive after verification | ARCHIVE_CANDIDATE |
| `BlackOps-EVA` | tiny variant | archive after verification | ARCHIVE_CANDIDATE |
| `eva-os-ultimate` | tiny variant | archive after verification | ARCHIVE_CANDIDATE |

Rule: `EVA` and `EVA-Mirror` must be content-compared before either is archived. Size alone is not proof of canonicality.

## Shadowmaker family

Canonical topology:
- `shadowmaker-core`
- `shadowmaker-agents`
- `shadowmaker-automation`
- `shadowmaker-archive`

Classification:

| Current | Target | Status |
|---|---|---|
| `shadowmaker-core` | `shadowmaker-core` | ACTIVE_CANONICAL |
| `shadowmaker-agents` | `shadowmaker-agents` | ACTIVE_CANONICAL |
| `shadowmaker-talk-workflows` | `shadowmaker-automation` input | MIGRATE/REVIEW |
| `shadowmaker-real-api-integration` | core or automation input | MIGRATE/REVIEW |
| `shadowmaker-utils` | core shared utilities input | MIGRATE/REVIEW |
| `shadowmaker-suite` | compare for unique integration code | MIGRATION_SOURCE |
| `shadowmaker` | inspect tiny root repo | ARCHIVE_CANDIDATE |
| `shadowmaker-system` | inspect tiny variant | ARCHIVE_CANDIDATE |
| `shadowmaker-ultimate-control` | inspect tiny variant | ARCHIVE_CANDIDATE |
| `shadowmaker-archiv` | `shadowmaker-archive` | ARCHIVE_SOURCE |
| `shadowmaker-archivierung` | `shadowmaker-archive` input | MIGRATE/ARCHIVE |
| `shadowmaker-audit-suite` | keep only if independently deployable; otherwise core/evidence | REVIEW |
| `shadowmaker-it` | domain-specific; inspect before consolidation | REVIEW |
| `-shadowmaker-fiverr-gig` | career namespace, not platform | MOVE_FAMILY |

## Portfolio family

Canonical target: `daniel-massa-portfolio`.

- `massa-portfolio` — **primary migration source**; contains substantial application assets/code.
- `daniel-massa-portfolio` — canonical target name/identity.
- `schattenmacher-portfolio` — compare unique assets, then archive candidate.
- `Skalierungs-Portfolio` — compare unique assets, then archive candidate.

Do not archive `massa-portfolio` until its code/assets are migrated and the target builds successfully.

## Foodsharing/community family

Canonical target: `community-foodsharing-control-center` (current source repo: `foodsharing-control-center`).

Migration candidates:
- `-Foodsharing-Initiative`
- `Foodsharing-Initiative_2`
- `Foodsharing-Initiative_3`
- `Lebensmittelretter-Stuttgart-Ost`
- `Lebensmittelretter-Stuttgart-Ost2`

Numbered variants are never canonical. Compare unique content first, migrate useful material, then archive.

## Execution gates

A duplicate repository may become ARCHIVED only when all are true:
1. top-level inventory captured;
2. unique source/assets identified;
3. useful content migrated or explicitly rejected;
4. target repository builds/tests where applicable;
5. CI/workflow references updated;
6. local git remotes and runtime references checked;
7. archive decision recorded in the portfolio tracker.

Physical repository archive/rename operations remain GitHub-settings actions and are not emulated by deleting content.