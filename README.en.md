# RunMap · Running tools

[中文](README.md) · English

This repository holds the tool descriptions, input/output contracts, formula assumptions, sources and worked cases used by `tools.paobu.org`. It is a content-only repository: it contains no site components, browser calculation code, `package.json`, `node_modules` or build output. The implementation lives in `site-tools`.

## Status

- Twelve tools: pace, splits, run-walk, race prediction, fueling planner, track view, format conversion, track simplification, elevation analysis, shoe mileage, race checklist and route-field comparison. Each has Chinese and English documentation.
- All twelve tools were **AI-assisted editorially reviewed** and published on 2026-10-28 (`published`, with bilingual `approve` records and matching digests). The reviewer is `runmap-editorial`, explicitly AI-assisted, not independent professional review. Physical-device performance remains unverified.
- Twenty-six independent cases live in `data/cases/`. They cover the three pace modes, negative splits, truncated run-walk schedules, Riegel predictions, track elevation and simplification offsets, fueling durations, missing elevation, shoe-mileage summaries and a trail checklist.
- The only author/review identity is `runmap-editorial`, shown as “RunMap editorial desk (AI-assisted draft and review)”. There is no personal qualification claim; the approval is an AI-assisted editorial review, not professional review.
- The six repositories are published under `paobuorg`, and the tools site is live at `https://tools.paobu.org/`.

## Tools and methods

| Tool | Version | Method summary |
|---|---|---|
| Pace `pace` | 1.1.0 | Distance-time, distance-pace and time-pace modes; kilometres or miles; exactly two positive inputs |
| Splits `splits` | 1.1.0 | Even or negative splits; default 2% half-marathon difference, limited to 0–10%; whole seconds allocated by largest remainder and conserved exactly |
| Run-walk `run-walk` | 1.0.0 | Schedule by cycles or total duration; duration mode cuts at the boundary and marks the partial segment; total duration capped at 7 days, cycles at 1000 |
| Race prediction `race-predict` | 1.0.0 | Riegel formula with a fixed 1.06 exponent; known and target distances limited to 5000–42195 m; not for trail or ultramarathon |
| Fueling planner `fueling-planner` | 1.0.0 | 30–60 g/h carbohydrate estimate above 60 minutes; rounds up product servings; does not judge personal tolerance or race strategy |
| Elevation `route-elevation` | 1.0.0 | GPX/GeoJSON line geometry; WGS84 distance; cumulative gain/loss and maximum grade; missing elevation reported as unknown and short segments excluded from grade |
| Shoe mileage `shoe-mileage` | 1.0.0 | Initial plus logged distance; remaining distance against the user's own reminder threshold; no universal replacement interval |
| Race checklist `race-checklist` | 1.0.0 | Items derived from road/trail, duration, weather, terrain and travel conditions; a rule-based list, not medical or mandatory advice |
| Track view `track-view` | 1.0.0 | GPX or GeoJSON line geometry; WGS84 geodesic distance; missing elevation is reported as unknown, never zero |
| Track conversion `track-convert` | 1.0.0 | GPX and GeoJSON conversion; line geometry only; strips timestamps, device and personal metadata |
| Track simplification `track-simplify` | 1.0.0 | Per-segment Ramer–Douglas–Peucker; 1–100 m tolerance; segments are not joined; endpoints and original coordinates are kept |
| Route comparison `route-compare` | 1.0.0 | Compares 2–4 published routes only; shows distance, elevation basis, surface and technicality field by field; missing values stay unknown and no ranking is produced |

The full formula description, constraints and rounding rules live in each `data/entities/{slug}.json` under `formulaDescription`, `assumptions` and `rounding`. Articles explain purpose and limits only. Changing a calculation requires a higher `specVersion` and matching case updates.

## Layout

```text
data/entities/{slug}.json          Contract, formula description, assumptions, rounding and source refs
data/cases/{caseId}.json           Independent case: inputs, expected output and boundary notes
data/sources/{sourceId}.json       Standards, papers and public guidance
data/contributors/{personId}.json  Public author and reviewer identities
data/reviews/{slug}.{locale}.json  Content digest and decision after review
content/zh-CN/{slug}.md            Chinese documentation and frontmatter
content/en/{slug}.md               English documentation and frontmatter
assets/                            Small reusable material
```

Entity IDs look like `tool:pace`; slugs use lowercase English hyphens. The two languages are paired by `entityId`, and the calculation contract lives only in `data/entities/`. Articles do not use MDX, inline scripts or dynamic imports.

## Browser boundaries

The implementation lives in `site-tools` and runs within these limits:

- Track files are read locally in the browser. They are not uploaded, written to analytics logs or committed to this repository.
- One file may contain at most 20,000,000 bytes and 200,000 coordinate points. Larger input is rejected rather than truncated and processed.
- Parsing and geometry work run in a Worker. After 10 seconds the interface offers cancellation; after 30 seconds the job is terminated and no incomplete download is offered.
- DTDs, external entities, non-line geometry, invalid coordinates and non-finite numbers are rejected.
- Track distance is a WGS84 geodesic distance. It is informational and is not a certified course measurement.
- Conversion re-serializes geometry, so output is not byte-identical to the input. Missing elevation stays missing.
- Simplification tolerance is measured in a local projected plane; the resulting WGS84 distance change is reported separately.

## Local use

The content is read by `site-tools` at build time. When the six projects sit in the same parent directory, the build finds this repository automatically; `TOOLS_CONTENT_DIR` can override the path, and `PAOBU_REPOS_DIR` can relocate the parent directory. This repository has no install or build command of its own.

The build validates bilingual pairing, tool contracts, case references, sources, licences, review dates and content digests. The search index is produced by the site build and is not a second copy of the documentation.

## Licence and corrections

- New documentation and cases: CC BY 4.0, attributed to “RunMap 跑地图”.
- Quoted standards, papers and guidance keep their own terms and are cited only within them.
- Site code: MIT, in the three `site-*` repositories.

Once the repository is hosted, report formula, case or source problems through an issue or pull request that names the specific item. No public issue URL or email address exists yet, and none is invented here. See [CONTRIBUTING.md](CONTRIBUTING.md), whose second half is in English.

Last checked: 2026-10-28.
