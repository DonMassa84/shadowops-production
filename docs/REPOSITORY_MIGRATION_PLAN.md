# Repository Migration Plan

This plan normalizes the current repository landscape without deleting history.

## Priority A — canonical active repositories

| Current repository | Canonical target name | Lifecycle | Action |
|---|---|---|---|
| `shadowops-production` | `shadowops-production` | PRODUCTION | Keep; canonical release repository |
| `shadowops` | `shadowops-development` | ACTIVE/MIGRATE | Use as development source until production migration is complete |
| `shadowops-logs` | `shadowops-evidence` | ACTIVE | Rename conceptually; keep only sanitized operational evidence/log tooling |
| `shadowops-ollama-aio-setup` | `shadowops-ollama-runtime` | ACTIVE | Normalize name and scope |
| `ihk-operative-professionals-2024-25` | `ihk-operative-professionals` | ACTIVE | Remove date from active name |
| `auto_bewerbungen` | `career-application-automation` | ACTIVE | Normalize language and separators |
| `generate_customized_cover_letter` | `career-cover-letter-generator` | REFERENCE/ACTIVE | Normalize name |
| `daniel-massa-portfolio` | `daniel-massa-portfolio` | ACTIVE | Keep as canonical personal portfolio |
| `foodsharing-control-center` | `community-foodsharing-control-center` | ACTIVE | Add domain prefix |
| `shadow-ai-lab` | `lab-shadow-ai` | ACTIVE | Experimental/lab namespace |
| `n8n-workflows` | `shadowmaker-n8n-workflows` | ACTIVE | Clarify ownership/domain |

## Priority B — consolidate duplicates

### EVA family
Canonical namespace should be `eva-*`.

Candidates to consolidate or archive after content comparison:
- `EVA`
- `EVA2`
- `EVA-Mirror`
- `eva-os-ultimate`
- `BlackOps-EVA`
- `spiegelkern-eva`
- `EVA_IntelligentAgent`
- `eva-video-analysis`
- `eva-multiagent-workflows`
- `eva-skill3-informationsverarbeitung`
- `eva-agent-template`

Target model:
- `eva-core`
- `eva-agents`
- `eva-workflows`
- `eva-video-analysis`
- `eva-archive` (historical snapshots only)

### Portfolio family
Keep one canonical personal portfolio:
- canonical: `daniel-massa-portfolio`
- compare/migrate then archive: `massa-portfolio`, `schattenmacher-portfolio`, `Skalierungs-Portfolio`

### Foodsharing/community family
Canonical implementation: `community-foodsharing-control-center`.
Compare and migrate useful content from:
- `Lebensmittelretter-Stuttgart-Ost`
- `Lebensmittelretter-Stuttgart-Ost2`
- `-Foodsharing-Initiative`
- `Foodsharing-Initiative_2`
- `Foodsharing-Initiative_3`

Do not keep numbered repository variants after migration.

### Shadowmaker platform family
Review overlap between:
- `ShadowHub-Core`
- `shadowmaker-core`
- `shadowmaker-system`
- `SchattenSystem`
- `shadowmaker-suite`
- `shadow-command-hub`
- `shadowmaker-ultimate-control`
- `shadowmaker-agent-system`
- `shadowmaker-agents`

Target topology should normally be:
- `shadowmaker-core`
- `shadowmaker-agents`
- `shadowmaker-automation`
- `shadowmaker-archive`

Only retain additional repos when they have an independently deployable lifecycle.

## Priority C — names that violate the standard

Recommended normalization:

| Current | Target |
|---|---|
| `SmartContacts` | `smart-contacts` |
| `Csharp-by-DonMassa84-` | `lab-csharp` |
| `2022CODEandMySQLdataDLL` | `archive-code-mysql-2022` |
| `parkingLotGUI` | `lab-parking-lot-gui` |
| `InterNetX-GmbH` | `archive-internetx-project` |
| `-RFID_Trustworth1984` | `lab-rfid-trust` |
| `CampResidentManager` | `camp-resident-manager` |
| `IBOGA-TOKEN-Projekt` | `archive-iboga-token-project` |
| `universellesZugangskontrollsystem` | `universal-access-control` |
| `MY-GPT-PROFILE.md` | `shadowmaker-gpt-profile` |
| `-ehs-it-support-doku` | `archive-ehs-it-support-docs` |
| `Operation_KI_Hub` | `eva-operation-ai-hub` |
| `Operation_KI_Hub_Full_Bundle` | archive after merge into canonical hub |
| `EmotionAgent-Neurostatus-Analytiker` | `eva-emotion-agent` |
| `AGENTENKORPS-ARCHIV-SPIEGEL` | `archive-agent-corps-mirror` |
| `ki-telefonagent-deep-shadow` | `shadowmaker-phone-agent` |
| `new` | inspect; migrate or archive immediately |
| `matrixchatroom_domain_suite` | `matrix-chatroom-domain-suite` |
| `Schattenmacher_Kapitalstrategie` | `shadowmaker-capital-strategy` |
| `PH-NIX-KERN` | `phoenix-core` |
| `agent-training-center-` | `agent-training-center` |
| `tactic_prompt_core` | `tactic-prompt-core` |
| `Fiverr-Gig-Creator` | `career-fiverr-gig-creator` |
| `YouTubePythonScraper` | `youtube-python-scraper` |
| `architekt_production` | `architect-production` |
| `-shadowmaker-fiverr-gig` | `career-shadowmaker-fiverr-gig` |

## Execution order

1. Freeze new ad-hoc repository creation.
2. Keep `shadowops-production` as the first fully governed repository.
3. Compare duplicate families before moving or archiving anything.
4. Migrate active code into canonical repositories.
5. Update references, CI, remotes and documentation.
6. Archive old repositories only after successful verification.
7. Rename remaining canonical repositories to lowercase kebab-case.
8. Standardize default branch to `main`.
9. Add README contract and CI/security baseline to every maintained repository.

## Safety rule

No repository is deleted as part of this migration. Historical repositories are archived only after canonical content has been verified.
