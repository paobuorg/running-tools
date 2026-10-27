---
entityId: tool:splits
locale: en
title: "Split table: break a target time into segments"
summary: Enter total distance, total time and split distance, then choose an even or negative-split strategy to build a printable table. The final segment may be short, and all whole seconds add up exactly to the total.
aliases: ["split table", "negative split", "pace splits"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What it is for

A split table breaks a target performance into equal-distance segments. It is useful for writing a pace band before a race, printing a note for an aid-station bag, or comparing actual splits afterwards. It offers two explicit arithmetic strategies: **even** and **negative split**. Both are planning tools, not predictions of how a race will unfold.

For example: 10 km in 50 minutes with 1 km even splits gives 5 minutes per segment and cumulative times of 5, 10, 15 … 50 minutes. For 5 km with 2 km splits, the first two segments take 10 minutes each and the final 1 km takes 5 minutes.

## The two strategies

**Even**: every metre uses the same pace, total time ÷ total distance.

**Negative split**: the first half of the distance is slower and the second half is faster. The difference `delta` defaults to 0.02 and is limited to 0 to 0.10. The first half uses `(1 + delta) ÷ 2` of total time and the second half uses `(1 − delta) ÷ 2`. For 10 km in 3000 seconds with delta = 0.02, the first 5 km take 1530 seconds (306 s/km) and the second 5 km take 1470 seconds (294 s/km).

A segment that crosses the halfway point is integrated over its actual metres in each half; the whole segment is never given a single pace by mistake.

## The algorithm

1. Split count = total distance ÷ split distance, rounded up.
2. Segment i covers `[(i−1) × split distance, min(i × split distance, total distance)]`.
3. Under the even strategy, exact time = segment metres × total seconds ÷ total metres.
4. Under the negative strategy, each part before or after the halfway distance is multiplied by its own pace, then the parts are added.
5. Take the floor of every exact time, then distribute the remaining whole seconds by **largest remainder**: the segments with the largest fractional parts receive one extra second each, with ties going to the earlier segment.
6. The final segment may still be shorter than a full unit, but every segment time adds up exactly to the total and no segment is negative.

Largest-remainder allocation can put a segment one second away from its exact value, but the total does not drift. Cumulative times are built from the allocated whole seconds, so the last segment cannot turn negative and the total cannot disagree with the input.

## Inputs and limits

- Total distance, total time and split distance must all be greater than zero; total time is entered as whole seconds.
- `delta` applies only to the negative strategy and must be between 0 and 0.10; setting it to 0 produces the same table as the even strategy.
- If the split distance is greater than the total distance, the table has one segment equal to the total time.
- Distance units can be kilometres or miles; the table uses the unit you entered, with one mile equal to 1,609.344 metres.
- The tool does not adjust for hills, aid stations or weather. Those are training and racing decisions, not arithmetic the table should make for you.

## How to use it

Treat the table as a **reference or ceiling**, not a command. Start corrals, aid stations, hills and weather will move actual splits. If the first half is clearly faster than the table, the second half may pay for it. A negative-split table describes a deliberate pace distribution; it does not guarantee that the second half will feel easier.

To convert an average pace first, use the [pace calculator](/en/tools/pace/). To understand the standard marathon distance, read [why the marathon is 42.195 km](https://learn.paobu.org/en/articles/marathon-distance/).

## Verification cases

- 10 km, 3000 seconds, 1 km even splits: 10 segments of 300 seconds, cumulative from 300 to 3000 seconds.
- 5 km, 1500 seconds, 2 km even splits: 3 segments of 2, 2 and 1 km, taking 600, 600 and 300 seconds, totalling 1500 seconds.
- 5 miles, 2400 seconds, 1 mile even splits: 5 segments of 480 seconds, totalling 2400 seconds.
- 10 km, 3000 seconds, 4 km negative splits, delta = 0.02: 1224, 1188 and 588 seconds, totalling 3000 seconds; the second segment crosses halfway.
- 10 km, 3000 seconds, 5 km negative splits, delta = 0.02: 1530 seconds for the first half and 1470 seconds for the second half.

All cases were checked by independent arithmetic.

## Privacy and data

All calculations happen locally in your browser; inputs are not sent to an application database and no account is required. To restore inputs after a refresh and to support sharing, values are written into the page URL query string. Opening or refreshing that URL sends it to the static host and leaves it in browser history. File contents are never written into the URL. Clear the address-bar parameters after using a shared device.

## Sources and scope

Distance units and the standard marathon value follow World Athletics' description. This article and tool were checked on 2026-10-27. A split table is not a finish-time promise.
