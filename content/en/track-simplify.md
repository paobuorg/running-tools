---
entityId: tool:track-simplify
locale: en
title: "Track simplification: projected tolerance, point and distance comparison"
summary: Simplify each segment independently with a local metric projection and iterative RDP, keeping endpoints and segment breaks while reporting the change in points and WGS84 distance. The original file is never modified.
aliases: ["track simplification", "RDP", "point reduction"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool does

The simplifier reads a GPX or GeoJSON line, removes points that contribute little to its shape within a chosen tolerance, and produces a new simplified file for download. It reports the number of points before and after, the WGS84 geodesic distance before and after, and a per-segment comparison. It does not modify or overwrite the original file.

Simplification is **lossy**: removed points and their elevation values do not appear in the output; retained points keep their original coordinates and elevation. The tool does not smooth or resample the line and does not join separate segments.

## Method

1. For each segment, compute its mean latitude and project longitude and latitude to local metres around that latitude.
2. Run an iterative Ramer–Douglas–Peucker (RDP) pass in the projected plane: keep the first and last points, repeatedly find the point farthest from the current chord, keep it when the distance exceeds the tolerance, and continue on both sides.
3. Output the retained points in their original order and recompute the distance before and after using WGS84 geodesic inverse distances.

The tolerance is a number of **projected metres**, not a geodesic distance. Because the projection is a local approximation, the tolerance and ground distance can differ slightly away from the projection centre; the page reports the WGS84 distance change separately so you can judge whether the shape change is acceptable. RDP constrains the deviation of points from a chord; it does not guarantee that the total distance changes by the same amount.

## Tolerance and refusal conditions

The tolerance is required, must be between 1 and 100 metres, and the page starts at 10 metres. Files are limited to 20 MB and 200,000 coordinate points. This version **refuses to simplify** a segment, and names the segment, when:

- its projected bounding-box diagonal exceeds 500 km;
- its longitude span exceeds 180 degrees, which may indicate an antimeridian crossing;
- any point lies beyond 85 degrees latitude.

These limits apply only to simplification. The same file can still be read with the [track viewer](/en/tools/track-view/) or converted with the [track converter](/en/tools/track-convert/). The output keeps the input format: GPX stays GPX and GeoJSON stays GeoJSON.

## Verification case

Three points near the equator: `[0, 0]`, `[0.001, 0.00005]`, `[0.002, 0]`, with a tolerance of 10 metres. The middle point deviates from the chord by about 0.00005 degrees of latitude, roughly 5.56 metres, which is below 10 metres, so it is removed and the endpoints remain. At a 1-metre tolerance the middle point is kept. This case was checked by independent arithmetic, not by the page script itself.

## Privacy and limits

The file is read and processed only in your browser. It is not uploaded and is not retained after a refresh. The tool does not decide whether a track is an official course, safe or suitable for a race, and the simplified distance is not a certified measurement. Before sharing a file, check whether it reveals sensitive locations such as a home address.

## Sources and scope

The RDP method follows Ramer (1972) and Douglas–Peucker (1973); coordinate and distance handling follow WGS84 and the GeographicLib implementation used by core. This article and tool were checked on 2026-10-27.
