# Core Repository Map

Status: CANONICAL PORTFOLIO CLASSIFICATION

This document defines Phase 2 canonical repositories and migration sources. No repository is deleted by this plan.

## IHK

| Repository | Role | Target | Lifecycle |
|---|---|---|---|
| `ihk-projektarbeit-zero-trust` | authoritative project-work repository | keep | ACTIVE / PRIMARY |
| `ihk-operative-professionals-2024-25` | course/exam knowledge and learning material | `ihk-operative-professionals` | ACTIVE / RENAME |
| `ihk-document-ai` | mixed integration/development repository; contains historical ShadowOps integration work | retain temporarily | MIGRATE / REVIEW |
| `ihk-schattenarchiv` | historical material | keep name until archive review | ARCHIVE CANDIDATE |
| `zero-trust-github-integration` | reusable/public Zero-Trust implementation/reference | keep | REFERENCE |

Decision: Do not merge the IHK project-work repository into the course repository. Project evidence and course-learning material have different lifecycles.

## Career / Applications

| Repository | Role | Target | Lifecycle |
|---|---|---|---|
| `auto_bewerbungen` | application automation source | `career-application-automation` | ACTIVE / RENAME |
| `generate_customized_cover_letter` | cover-letter component/tooling | `career-cover-letter-generator` | ACTIVE / REFERENCE |
| `bewerbung-daniel-massa-2025-` | historical application documents | `archive-career-applications-2025` | ARCHIVE CANDIDATE |
| `karriere-shadow` | inspect for unique career data/workflows | TBD after content review | MIGRATE / REVIEW |

Decision: automation code and historical application documents stay separate.

## Personal Portfolio

| Repository | Role | Target | Lifecycle |
|---|---|---|---|
| `daniel-massa-portfolio` | canonical target name | keep | ACTIVE / TARGET |
| `massa-portfolio` | current code-rich portfolio implementation | migrate into `daniel-massa-portfolio` after comparison | MIGRATION SOURCE |
| `schattenmacher-portfolio` | alternate/legacy portfolio | compare then archive | MIGRATE / ARCHIVE |
| `Skalierungs-Portfolio` | strategy/legacy portfolio variant | compare then archive | MIGRATE / ARCHIVE |

Decision: `massa-portfolio` must not be archived before its application code, assets and deployment behavior are verified in `daniel-massa-portfolio`.

## Community / Foodsharing

| Repository | Role | Target | Lifecycle |
|---|---|---|---|
| `foodsharing-control-center` | canonical implementation source | `community-foodsharing-control-center` | ACTIVE / RENAME |
| `-Foodsharing-Initiative` | predecessor | migrate unique content | MIGRATE / ARCHIVE |
| `Foodsharing-Initiative_2` | numbered predecessor | migrate unique content | MIGRATE / ARCHIVE |
| `Foodsharing-Initiative_3` | numbered predecessor | migrate unique content | MIGRATE / ARCHIVE |
| `Lebensmittelretter-Stuttgart-Ost` | related community implementation | compare scope | REVIEW |
| `Lebensmittelretter-Stuttgart-Ost2` | duplicate/variant | compare scope | REVIEW / ARCHIVE |

Decision: no numbered Foodsharing repositories remain active after verified consolidation.

## AI Lab

| Repository | Role | Target | Lifecycle |
|---|---|---|---|
| `shadow-ai-lab` | large experimental AI workspace | `lab-shadow-ai` | ACTIVE / RENAME |
| `agent-apps` | empty/near-empty agent app target | inspect before use | REVIEW |
| `agent-apps-v3` | archived historical agent-app experiment | keep archived | ARCHIVE |

Decision: keep lab/experimental work explicitly outside production repositories.

## Required standard for maintained repositories

Every maintained repository must converge on:

- lowercase kebab-case repository name;
- default branch `main`;
- clear README purpose statement;
- lifecycle classification;
- documented source-of-truth role;
- `.gitignore` appropriate to its stack;
- no committed secrets/runtime credentials;
- CI only when the repository contains executable/buildable code;
- `docs/` for maintained documentation;
- `scripts/` for operational helper scripts;
- generated artifacts excluded unless the repository is explicitly an evidence/archive repository.

## Migration gates

A source repository may become ARCHIVE only when:

1. unique content has been inventoried;
2. canonical target has received required content;
3. build/deploy behavior has been verified where applicable;
4. references and remotes have been updated;
5. secrets and personal data exposure have been reviewed;
6. rollback information exists.
