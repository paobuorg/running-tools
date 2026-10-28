---
entityId: tool:route-elevation
locale: en
title: "Route elevation profile: read a GPX file locally"
summary: "Read GPX or GeoJSON, calculate distance, gain, loss, elevation range and maximum grade, and show a downsampled profile. Missing elevation stays unknown rather than becoming zero."
aliases: ["Route elevation profile: read a GPX file locally"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool does

Choose a local GPX or GeoJSON file. The tool reads the track in this browser, calculates total distance, cumulative gain and loss, minimum and maximum elevation, the largest absolute point-to-point grade, and draws an elevation profile. The file is not uploaded and no account is required.

It is useful for understanding the shape of a route before heading out or reviewing the elevation structure of a recorded activity. It is not race certification, a safety assessment or a navigation tool.

## How distance, gain and grade are defined

Distance is the sum of WGS84 great-circle distances between consecutive points within each segment. Segments are measured independently and their endpoints are not joined. Gain is the sum of all positive elevation differences; loss is the sum of the absolute negative differences.

Grade is `Δelevation / horizontal distance × 100%`. To avoid amplifying noise from points that are very close together, grade is calculated only for pairs at least 5 metres apart. The maximum grade is therefore a point-pair estimate, not a road-design grade or a whole-climb average.

## Missing elevation and GPS noise

If the file has no elevation, or only some points have it, the tool shows gain, loss and profile as unknown instead of treating missing values as zero; otherwise it would undercount climbing. GPS elevation also drifts, and different devices, barometers and correction algorithms can produce different totals.

When comparing two routes, prefer the same source and the same elevation method. Do not mix corrected and uncorrected numbers without saying so.

## Using the result

Start with the distance and climb magnitude, then look for steep climbs, descents and long gradients in the profile. Read them alongside aid stations, surface and weather. For a race, the organiser's route, mandatory kit and technical notes remain authoritative; a GPX file alone cannot establish safety.

Parsing happens locally. Results are not saved after the page closes. Oversized or malformed files return an error rather than a partial result.

## What this tool does not provide

This tool does not verify that a track is the official course, that access is permitted or that the route is suitable for a race. It does not assess rockfall, traffic, weather or technical difficulty. Technical trails, glaciers or roped routes require specific training and local information.

## Sources and scope

GPX and GeoJSON format boundaries follow the public specifications; uphill and downhill mechanics follow a sports-biomechanics review. Elevation values come from the file; the tool does not guarantee device accuracy or route safety.
