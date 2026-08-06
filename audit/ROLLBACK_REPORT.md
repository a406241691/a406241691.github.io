# ROLLBACK REPORT

**Date**: 2026-08-06
**Rolled back from**: fc7e591 (v3.0 — breaking)
**Restored to**: 06e1f2f (v2.0 — last known working)
**Backup branch**: backup-broken-v3 (preserves fc7e591 for reference)

---

## Rollback Method

```
cd D:\studio-demos\showcase
git fetch origin
git status                                 # clean working tree confirmed
git branch backup-broken-v3 fc7e591        # preserve broken commit
git reset --hard 06e1f2f                   # restore working commit
git push --force-with-lease origin main    # deploy
```

---

## Restored Commit

| Field | Value |
|-------|-------|
| SHA | 06e1f2f7c600ced360cedd445e256dd1a073123a |
| Message | "Central catalogue: verified 18-demo portfolio with audit documentation" |
| Date | 2026-08-06 |
| Branch | main |

---

## Deployment Verification

| Check | Result |
|-------|--------|
| https://studio-public-demos.github.io/ returns HTTP 200 | PASS (39435 bytes) |
| catalogue.json loads (18 demos) | PASS |
| 15 live demos in catalogue | PASS |
| hero canvas renders | PASS |
| Pages build status | built |
| Deployed SHA matches restored | YES |

---

## Live Link Verification (5 sampled)

| Demo | URL | Status |
|------|-----|--------|
| Open London 3D Drive | open-london-3d-showcase | 200 OK (9155 bytes) |
| NexusTwin | nexustwin-industrial-digital-twin | 200 OK (75026 bytes) |
| Stadium Digital Twin | stadium-digital-twin | 200 OK (41972 bytes) |
| Guntur Change Detection | guntur-change-detection-dashboard | 200 OK (890693 bytes) |
| VLM Aerodynamics | vlm-aerodynamics-demo | 200 OK (618714 bytes) |

---

## Restored File State

| File | Status at 06e1f2f |
|------|-------------------|
| index.html | v2.0 — 9 categories, 4 discovery paths, detail pages, Three.js hero |
| catalogue.json | 18 verified demos with pagesUrl, repoUrl, classification |
| demo-inventory-legacy.json | Preserved (47 speculative entries) |
| audit/CURRENT_SHOWCASE_AUDIT.md | Full org scan |
| audit/REPOSITORY_INVENTORY.csv | 29 repos |
| audit/PROJECT_CLASSIFICATION_MATRIX.csv | 18 demos classified |
| audit/DEPLOYMENT_AND_LINK_AUDIT.csv | 15 live URLs |
| audit/TARGET_INFORMATION_ARCHITECTURE.md | 9-category model |
| audit/IMPLEMENTATION_PLAN.md | 5-phase plan |
| templates/* | 6 standardisation templates |

---

## Files NOT Restored (from v3.0)

| File | Disposition |
|------|-------------|
| audit/PREVIEW_REGRESSION_REPORT.md | Lost in rollback (v3.0-only) |

---

## What v2.0 Contains

- 18 verified demos in catalogue.json
- 9 primary technology categories
- 4 discovery paths: Categories, By Technology, By Industry, Browse All
- Search with real-time filtering
- Category + maturity filter chips
- Project detail pages at `/?demo={repo-name}`
- 15 verified live URLs
- All 6 audit documents
- Legacy speculative inventory preserved
- Three.js wireframe icosahedron hero globe (exact nebulacloud.studio replica)
- Per-section wireframe geometry backgrounds

---

## Breaker Commit Analysis

Commit fc7e591 ("v3.0: Corrected catalogue model") introduced:
- catalogue.json schema change (projects[] vs demos[], new field names)
- 6 solution families replacing 9 categories
- repositoryType field with public grid filtering
- Changed card rendering (subtitle instead of summary, new badge system)
- New detail page sections (business problem, validation, etc.)
- Static hero HTML + updateHeroStats()
- buildHome() restructured

The changes were too many to isolate the specific failure. Safe recovery path = complete rollback.

---

## Next Steps (after approval)

Make only small, separately tested changes — one change per commit — with a preview branch before touching main.
