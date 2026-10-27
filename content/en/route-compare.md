---
entityId: tool:route-compare
locale: en
title: "Route comparison: distance, elevation basis and technicality across published versions"
summary: "Compare two to four published route versions field by field: distance, elevation basis, surface and technicality. Missing values stay unknown, and no safety or difficulty ranking is generated."
aliases: ["route comparison", "course comparison", "elevation comparison"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool does

Route comparison places two to four **published** route versions in one table and shows:

- the course distance and how it was recorded;
- elevation gain, when recorded, and its stated basis;
- surface type, when recorded;
- technicality, when recorded.

It does not sort the routes, and it does not interpret a longer distance, more elevation or a particular technicality value as "harder" or "more dangerous". Whether a course suits you depends on training, weather, fuelling, access rules and race-day conditions; a field table cannot derive that.

## Why published versions only

Course data can change before publication is complete, so unpublished versions do not take part. The tool reads only fixed versions whose status is published and shows the version identifier, so you are looking at reviewed records rather than a draft.

If the site does not have enough published versions (fewer than two), the page shows an empty state explaining that nothing is comparable yet. That is a content state, not a page failure.

## Missing values and measurement basis

A missing elevation, surface or technicality field is shown as **unknown**. It is never filled with zero, and a value is not inferred for one route because another route has it. Distance may come from different official descriptions or measurement methods, and elevation may come from official gain, map estimates or track statistics. The table keeps each route's stated basis so numbers from different sources are not treated as one ruler.

Whether track geometry is public or redistributable is separate from whether fields can be compared. A visible route page does not mean its track may be republished; follow the official link and licence note recorded for that route.

## Verification case

A synthetic acceptance case contains two routes. The first has a distance of 42,195 m, 300 m of gain, surface "road" and no technicality. The second has a distance of 21,097.5 m and no elevation, surface or technicality. The comparison must keep both distance values, show the second route's missing fields as unknown and produce no ranking field. This case tests field handling only and does not represent a real race.

## Privacy and data

All calculations happen locally in your browser; inputs are not sent to an application database and no account is required. To restore inputs after a refresh and to support sharing, values are written into the page URL query string. Opening or refreshing that URL sends it to the static host and leaves it in browser history. File contents are never written into the URL. Clear the address-bar parameters after using a shared device.

## Sources and scope

The standard marathon distance follows World Athletics; example fields for UTMB and the Boston Marathon come from their official pages. The tool displays recorded fields only, does not certify course distance and does not judge race safety. This article and tool were checked on 2026-10-27.
