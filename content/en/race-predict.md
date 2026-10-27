---
entityId: tool:race-predict
locale: en
title: "Race time prediction: the Riegel formula and its 1.06 exponent"
summary: Use one known road race result to estimate the finish time and pace at another distance from 5 km to the marathon under the Riegel model. An empirical estimate, not a promise.
aliases: ["race time prediction", "Riegel formula", "finish time"]
authors:
  - runmap-editorial
reviewers:
  - runmap-editorial
translationStatus: reviewed
---

## What this tool answers

Enter the **distance** and **finish time** of a known road race, then enter a target distance. The tool applies the Riegel formula to estimate the target finish time and converts it to pace per kilometre, pace per mile and average speed.

For example, estimate a 10 km time from a 5 km result, or a half marathon from a 10 km result. This is useful for a rough conversion between race distances and for checking whether a target time is broadly in line with current performance. It does not predict what you will definitely run on race day.

## Formula and units

The tool uses:

`target time = known time × (target distance ÷ known distance)^1.06`

Distances are converted to metres internally and time is handled in seconds; conversion to pace per kilometre, pace per mile and km/h happens only for display. Both the known and target distance must be between 5,000 and 42,195 metres, covering common road distances such as 5 km, 10 km, the half marathon and the marathon.

The exponent 1.06 is a fixed product default, not a law that holds for every runner and every distance. The Riegel formula fits a constant to each runner; this tool does not refit anything to your personal data and simply treats 1.06 as a common empirical simplification.

## Scope and limits

- Road races only. Do not use it for trail races, ultramarathons or courses with substantial climbing.
- Assumes the known result and the target race are broadly comparable in training, pacing and conditions.
- No confidence interval and no probability of hitting the target time.
- Weather, heat, altitude, course profile, start congestion and fuelling are not modelled.
- Not a training plan. Do not use the estimate to prescribe training intensity or a race goal on its own.

If the two races are far apart in time, or your training volume, body weight or injury status has changed significantly, the estimate is less useful. Pacing decay over long races is usually more complex than the formula suggests, especially in the second half of a marathon.

## Reading the result

Look at the estimated time first, then the corresponding average pace. If the target pace is much faster than a pace you can currently sustain in training, the goal is more likely too aggressive than the formula being "all that stands between you" and the time. Treat the estimate as a starting point and test it with a shorter race or a tempo effort rather than adopting it as a race goal unexamined.

To turn the estimated time into a segment plan, use the [split table](/en/tools/splits/). To check distance, time and pace conversions, use the [pace calculator](/en/tools/pace/). For background on the marathon distance, read [why the marathon is 42.195 km](https://learn.paobu.org/en/articles/marathon-distance/).

## Verification cases

- Known 5,000 m in 1,200 s, target 10,000 m: distance ratio 2, estimate 1,200 × 2^1.06 = 2,501.918 s, displayed as 2,502 s; about 250 s/km, 403 s/mi and 14.39 km/h.
- Known 10,000 m in 3,000 s, target 21,097.5 m: distance ratio 2.10975, estimate 6,619.209 s, displayed as 6,619 s; about 314 s/km, 505 s/mi and 11.47 km/h.
- Known 21,097.5 m in 5,700 s, target 42,195 m: distance ratio 2, estimate 11,884.110 s, displayed as 11,884 s; about 282 s/km, 453 s/mi and 12.78 km/h.

These values were checked by independent arithmetic, not by the page script itself.

## Privacy and data

All calculations happen locally in your browser; inputs are not sent to an application database and no account is required. To restore inputs after a refresh and to support sharing, values are written into the page URL query string. Opening or refreshing that URL sends it to the static host and leaves it in browser history. File contents are never written into the URL. Clear the address-bar parameters after using a shared device.

## Sources and limitations

The formula and the 1.06 exponent are documented in Blythe and Király, "Prediction and Quantification of Individual Athletic Performance of Runners", PLoS One, 2016, which describes the Riegel formula as fitting a constant to each runner while fixing the exponent at 1.06. The standard marathon distance follows World Athletics. This article and tool were checked on 2026-10-27; the model limits are part of the published scope.
