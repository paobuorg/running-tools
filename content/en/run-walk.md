---
entityId: tool:run-walk
locale: en
title: "Run-walk planner: cycles or total duration"
summary: Plan run-walk intervals. Enter a run and walk duration, then lay out the intervals by number of cycles or by total time, marking any truncated final segment. Time arithmetic only; no distance, pace or fitness estimate.
aliases: ["run walk", "run-walk intervals", "walk break"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool answers

The run-walk planner turns "how long do I run, how long do I walk, and how many rounds" into a segment-by-segment schedule you can follow. It has two input modes:

- **Cycles mode**: given a run duration, a walk duration and a number of cycles, it lists the run and walk segments for every cycle. The walk in the final cycle is part of the plan and is not dropped.
- **Duration mode**: given a run duration, a walk duration and a total time, it starts at cycle one and keeps adding segments until the total is used up. If the total lands in the middle of a segment, that final segment is cut at the boundary and marked incomplete.

The output includes the requested duration, scheduled duration, number of full cycles, every segment, total running time, total walking time and whether the plan was truncated. It does not infer how far you travelled and does not estimate calories.

## How the two modes work

**Cycles mode**: each cycle is exactly "run then walk". For example, running 2 minutes and walking 1 minute for 3 cycles gives a total of 3 × (2 + 1) = 9 minutes, with 6 minutes of running and 3 minutes of walking across 6 segments. If the walk duration is zero, no empty walk rows are produced and the plan contains only runs.

**Duration mode**: the tool repeats run and walk until the requested total is reached. Take a 2-minute run, 1-minute walk and a total of 6 minutes 40 seconds. The first two full cycles use 6 minutes, leaving 40 seconds, which is not enough for the third run; the plan ends with a 40-second partial run. Running totals 4 minutes 40 seconds and walking totals 2 minutes.

Neither mode rounds up to a tidy number of cycles. Duration mode ends exactly at the entered total; cycles mode ends exactly at cycles multiplied by the cycle length.

## Inputs and limits

- The run duration must be a positive whole number of seconds.
- The walk duration may be zero but must be a non-negative whole number of seconds.
- The number of cycles must be a whole number from 1 to 1000.
- The total duration must be a positive whole number of seconds and no more than 7 days (604,800 seconds).
- A plan generates at most 3,000 segments; a very short segment combined with a very long total will hit this limit. The scheduled total in cycles mode is also limited to 7 days.

These limits only keep the arithmetic bounded. They do not mean the plan suits your fitness, injury history or training stage. The tool does not judge whether a run-walk ratio is reasonable and does not add or remove training load.

## Using the result

A segment list is useful for run-walk intervals, returning to running after a break, or breaking a longer outing into manageable pieces. It can also serve as a draft for manual watch entry. All times are **clock time** and exclude warm-up, cool-down, aid stops and travel; arrange those outside the plan if you need them.

For pace, distance and time conversion, use the [pace calculator](/en/tools/pace/). To plan per-kilometre or per-mile splits for a target time, use the [split table](/en/tools/splits/). The NHS Couch to 5K beginner plan is a public example whose first week uses 1-minute runs with 1-minute-30-second walks; this tool cites it to show a common run-walk structure, not to copy its training prescription or to claim that any ratio suits everyone.

## Verification cases

- Run 120 seconds, walk 60 seconds, 3 cycles: 540 seconds across 6 segments; running totals 360 seconds, walking totals 180 seconds, and the final segment is complete.
- Run 120 seconds, walk 60 seconds, total 400 seconds: two full cycles use 360 seconds, leaving a 40-second partial run; running totals 280 seconds and walking totals 120 seconds.
- Run 90 seconds, walk 0 seconds, 2 cycles: 180 seconds in two run segments with no zero-length walk rows.

These values were checked by independent arithmetic, not by the page script itself.

## Privacy and data

All calculations happen locally in your browser; inputs are not sent to an application database and no account is required. To restore inputs after a refresh and to support sharing, values are written into the page URL query string. Opening or refreshing that URL sends it to the static host and leaves it in browser history. File contents are never written into the URL. Clear the address-bar parameters after using a shared device.

## Sources and scope

The run-walk structure follows the NHS Couch to 5K beginner plan page. That source documents a public example of alternating short runs and walks; it is not a training recommendation for a particular person. This article and tool were checked on 2026-10-27. If you feel unwell, are injured or have cardiovascular risk factors, consult a qualified medical or sports professional.
