---
entityId: tool:track-convert
locale: en
title: "Track conversion: GPX and GeoJSON lines"
summary: Convert a GPX or GeoJSON line to the other format in your browser, preserving coordinate order and available elevation while stripping times, devices, names and original metadata.
aliases: ["track conversion", "GPX to GeoJSON", "format conversion"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool does

The track converter reads a line and writes it again in the format you choose, then offers the result as a download. It is useful for turning a watch or app GPX export into GeoJSON, or a GeoJSON line into GPX for another tool, without carrying the original file's personal information across.

The output contains the line geometry, the coordinate order, the separation between segments and, where a point has reliable elevation, an `<ele>` element or a third coordinate value. The tool does not write timestamps, device names, person names, file names or other original metadata. It also does not replace missing elevation with zero.

## Accepted input

- **GPX**: reads `trkseg` elements under `trk`; if there is no `trkseg`, it reads route `rte` elements instead. Every `trkseg` or `rte` becomes an independent segment; endpoints of different segments are not joined.
- **GeoJSON**: accepts `LineString`, `MultiLineString`, and `FeatureCollection` or `Feature` wrappers containing only those types. Coordinates are longitude, latitude, with an optional third elevation value.

Point sets, polygons and other non-line geometry types are rejected with an error rather than silently turned into a fake line. Files are limited to 20 MB and 200,000 points and are read locally; nothing is uploaded.

## Output and privacy

The output is re-serialized, so even when the output format matches the input the bytes may differ from the original: indentation, number formatting or element order can change. Keep your original file if you need it; the tool never modifies or overwrites it.

The download is generated locally by the browser. Its content is not uploaded, written to server logs or retained after a refresh. On a shared device, think twice before opening a track that reveals a home address.

## Verification case

A GeoJSON line with three points: `[0, 0, 10]`, `[0.001, 0]`, `[0.002, 0, 15]`. After conversion it must still have one segment and three positions, two of which carry elevation (10 and 15) while the middle point has none. Coordinate order and values must not change; missing elevation must not be replaced by `null` or zero. This case was checked by an independent round trip, not by the page's display output.

## What it cannot answer

The converter does not decide whether a line is an official course, whether access is permitted or whether it is suitable for a race, and it does not certify distance. It only changes the file format. To read distance, point count and endpoints, use the [track viewer](/en/tools/track-view/). To reduce the number of points, use [track simplification](/en/tools/track-simplify/) and check the reported points and distance change.

## Sources and scope

The file structure follows the GPX 1.1 specification and RFC 7946 for GeoJSON. This article and tool were checked on 2026-10-27.
