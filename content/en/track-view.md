---
entityId: tool:track-view
locale: en
title: "Track viewer: read your GPX and GeoJSON"
summary: Inspect a track's point count, start and end, distance and available elevation locally in your browser, without uploading the file. Missing elevation is shown as unknown, never filled with zero.
aliases: ["track viewer", "GPX viewer", "elevation view"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What the tool does

The track viewer reads a GPX or GeoJSON file you select and performs parsing and statistics locally. It shows:

- The number of coordinate points.
- The WGS84 geodesic distance when the points are connected in order.
- The latitude and longitude of the start and end.
- Cumulative elevation gain if the file contains elevation; otherwise it clearly marks it as unknown.

It does not judge your pace, compare the track against an official race course, or claim that the track has been authoritatively verified.

## Supported files

- **GPX 1.1**: reads track points (trkpt) first; if there is no trkseg, it reads route points (rtept). Separate segments are measured individually; their endpoints are not joined.
- **GeoJSON**: reads LineString coordinates. Coordinate order is longitude, latitude, with optional elevation.

Other geometry types, such as point collections or polygons, are not silently treated as a running line. Files are limited to 20 MB and 200,000 coordinate points. The tool explains in its warnings what it could not parse.

## Distance and elevation conventions

Distance is the sum of WGS84 ellipsoidal geodesic distances between consecutive points. It is not planar Pythagoras, and the tool does no smoothing, simplification or drift correction. GPS noise, tunnels and signal loss all affect the result, so the distance is informational, not a certified course measurement.

Cumulative gain is the sum of positive changes between consecutive elevations. If the file has no elevation at all, gain is unknown and must not be written as 0 — zero reads as "flat throughout". If only some points have elevation, the tool warns and explains what the calculation covers.

## Privacy

The file is read in your browser only. It is not uploaded to this site's server or written to server logs, and its contents are not retained after a refresh. Do not open files containing a home address on a shared computer; if you share a track, remove private locations near the start and unnecessary timestamps first.

## Questions it can and cannot answer

It can tell you how many points a file has, where it starts and ends, roughly how long it is, and the cumulative gain when elevation exists.

It cannot tell you the official certified distance of a course, whether the route is open on race day, whether the surface is safe, or whether your pace is appropriate. A GPX file is a sequence of coordinates; it carries no race rules, access permission or live conditions.

To turn a track into pace segments, use the [split table](/en/tools/splits/). To understand training load, combine your logs and recovery, not a single track.

## Verification cases

- A three-point track from longitude 0 to 0.02 degrees on the equator with no elevation: about 2226.3898 metres, rounded to 2226 m; 3 points; elevation gain unknown.
- A three-point track from longitude 0 to 0.002 degrees with elevations 10, 20 and 15 m: about 222.639 metres, rounded to 223 m; positive gain 10 m.

Both cases were checked by independent WGS84 arithmetic.

## Sources and scope

File formats follow the GPX 1.1 specification and RFC 7946. This article and tool were checked on 2026-10-27.
