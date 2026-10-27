---
entityId: tool:pace
locale: en
title: "Pace calculator: distance, time, pace and speed"
summary: Choose any two of distance, time and pace to solve the third, with pace per kilometre, pace per mile and average speed shown together. A road-running arithmetic tool that does not model hills, stops or wind.
aliases: ["pace calculator", "pace per kilometre", "speed conversion", "pace chart"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool answers

The pace calculator works with three quantities and lets you supply any two:

- **Distance + time**: get pace per kilometre, pace per mile and average speed.
- **Distance + pace**: get the total time needed to cover the distance.
- **Time + pace**: get the distance covered at that pace in the given time.

The page always shows pace per kilometre, pace per mile, speed, distance and total time together, so you can check the conversion across units. For example, 10 km in 50 minutes is an average pace of 5:00 per kilometre and a speed of 12 km/h. In reverse, 10 km at 5:00 per kilometre takes 50 minutes.

## Formula and units

The calculation uses metres and seconds internally and converts units only at the input and output boundaries.

- Kilometres to metres: distance × 1000.
- Miles to metres: distance × 1,609.344.
- Distance + time: `pace per kilometre = total seconds ÷ distance in kilometres`.
- Distance + pace: `total seconds = pace seconds × distance in metres ÷ metres per pace unit`.
- Time + pace: `distance in metres = total seconds ÷ pace seconds × metres per pace unit`.
- `pace per mile = pace per kilometre × 1.609344`.
- `speed in km/h = distance in kilometres ÷ (total seconds ÷ 3600)`.

Pace is rounded to the nearest whole second, speed to two decimal places, and distance to three decimal places. A pace input means the time per kilometre or per mile in the selected unit. The result is always an **average**.

## Inputs and limits

Each calculation needs two finite values greater than zero: distance and time, distance and pace, or time and pace. The tool does not judge whether an input is realistic and gives no training advice for fast or slow results. A marathon is 42.195 km and a half marathon is 21.0975 km; if you enter 42.2 km, you get the result for 42.2 km, not the standard marathon distance.

Enter pace as `hh:mm:ss` or `mm:ss`; `05:00` means five minutes per kilometre or per mile. When you change the unit, the meaning of the pace changes with it. Do not treat a per-mile pace as a per-kilometre pace.

## Reading the result

Average pace is useful for pre-race target conversion and post-race review, but it does not describe the race itself. Start corrals, aid-station stops, hills and weather all push actual splits away from the average. For a segment-by-segment plan, use the [split table](/en/tools/splits/). To understand the marathon distance, read [why the marathon is 42.195 km](https://learn.paobu.org/en/articles/marathon-distance/).

Pace and speed are not synonyms for training intensity. The same 6:00 per kilometre means different things in an easy run and a tempo run; judge intensity with breathing, perceived effort and the purpose of the session.

## Verification cases

- 10 km, 3000 seconds: 300 s/km (5:00/km), 482.8032 → 483 s/mi, 12.00 km/h.
- 5 miles, 2400 seconds: 480 s/mi (8:00/mi), 298.258 → 298 s/km, 12.07008 → 12.07 km/h.
- 10 km at 300 s/km: total time 3000 seconds and speed 12 km/h.
- 2400 seconds at 480 s/mi: distance 5 miles, or 8.04672 km, with pace 298.258 → 298 s/km.

These cases were checked by independent arithmetic, not by the page script itself.

## Privacy and data

All calculations happen locally in your browser; inputs are not sent to an application database and no account is required. To restore inputs after a refresh and to support sharing, values are written into the page URL query string. Opening or refreshing that URL sends it to the static host and leaves it in browser history. File contents are never written into the URL. Clear the address-bar parameters after using a shared device.

## Sources and scope

The standard marathon distance follows World Athletics' discipline description; mile conversion uses the exact international mile. This article and tool were checked on 2026-10-27.
