---
layout: post
title: Tulip Stage A Initial Measurements
date: '2026-11-07 15:50:17 -0400'
categories: [Tulip, Hardware]
tags: [stagea]     # TAG names should always be lowercase
---

# Time-lapse camera measurements

Every sharpness, focus, exposure, timing, file-size and reliability measurement found in the project notes for the battery-powered Feather and Arducam Mega camera, gathered in one place. Charts are images; each one has a table view with the exact values.

> Powered time per photo is now less than half of where it started. The reliability charts cover what is still being worked on: blurred starts, truncated JPEGs and retakes.

## Headline numbers

- **Picture size:** 2592×1944. 5 MP JPEG; every Stage A and later run saved at this size.
- **Sharpest edge width:** 4.59 px. Flat target at 40 cm with autofocus, 10–90 % edge width. A truly sharp 5 MP image measures 2–3 px.
- **Stage A 100-cycle run:** 100 of 100. One early run, saved at full size with no failure, unexpected reset or SD error. Camera and SD stayed powered (power was not switched); later switched-power runs lost cycles, see Reliability.
- **Sharp-sized frames, best recipes:** 97 %. 25 cm, warm camera, autofocus right after the warm-up and 2 s in all (two recipes, about 35 cycles each).
- **Powered time per photo:** 10.8 s. `tl_cycle` v12b on the board, no retake; Stage A took 25.9 s.
- **Mean JPEG size:** 2.84 MB. Stage A indoor scene; 43,200 photos (one per minute for 30 days) would be about 123 GB.

## Contents

- [Sharpness and focus](#sharpness-and-focus)
- [Exposure and colour](#exposure-and-colour)
- [Timing and powered time](#timing-and-powered-time)
- [File size and storage](#file-size-and-storage)
- [Reliability](#reliability)
- [Evidence and caveats](#evidence-and-caveats)

## Sharpness and focus

How sharp the photos are and how well autofocus holds. Edge width and the line-pair, checkerboard and small-text scores are direct measurements; JPEG size and the sharp-sized share are the proxy used on long runs.

### Edge width by distance

Width of a measured edge in pixels, so smaller is sharper. A missing autofocus-off bar means the edge was too blurred to measure.

![Edge width by distance](assets/camera-report/ch-af-distance.png)

<details markdown="1">
<summary>Table view</summary>

| Distance | Autofocus on, px | Autofocus off, px | Note |
| :--- | ---: | ---: | :--- |
| 15 cm | 4.95 | — | No-autofocus frame too blurred to measure |
| 40 cm | 4.59 | 7.08 | — |
| 1.5 m | 6.16 | 6.14 | — |
| 5 m | 5.88 | 6.34 | — |
| Far, outdoors | 5.16 | 5.17 | — |

</details>

### JPEG size against sharpness

Each dot is a photo scored with the line-pair test. The dashed lines mark the largest size seen for a blurred photo and the smallest seen for a sharp one, which is why file size can stand in for sharpness on long runs.

![JPEG size against sharpness](assets/camera-report/ch-size-sharp.png)

<details markdown="1">
<summary>Table view</summary>

| Photo | Run | Recipe | JPEG, MB | Line pairs | Checker | Small text | Class |
| :--- | :--- | :--- | ---: | ---: | ---: | ---: | :--- |
| c373 | Overnight run 1 | No AF | 2.095 | 82 | 151 | 69 | blurred |
| c4 | Overnight run 1 | 2 s | 2.102 | 97 | 182 | 81 | blurred |
| c3 | Overnight run 1 | 3 s | 2.115 | 102 | 188 | 80 | blurred |
| c298 | Overnight run 1 | 4 s | 2.12 | 76 | 97 | 82 | blurred |
| c1 | Overnight run 1 | 12 s | 2.132 | 113 | 211 | 83 | blurred |
| c37 | Overnight run 1 | No AF | 2.139 | 86 | 158 | 74 | blurred |
| c111 | Overnight run 1 | 5 s | 2.147 | 144 | 244 | 71 | blurred |
| c356 | Overnight run 1 | 12 s | 2.168 | 104 | 218 | 79 | blurred |
| c374 | Overnight run 1 | 12 s | 2.173 | 111 | 239 | 72 | blurred |
| c11 | Overnight run 1 | 5 s | 2.193 | 375 | 541 | 140 | partial |
| c130 | Overnight run 1 | 5 s | 2.21 | 108 | 192 | 73 | blurred |
| c358 | Overnight run 1 | 3 s | 2.226 | 281 | 459 | 114 | partial |
| c240 | Overnight run 1 | 3 s | 2.256 | 352 | 515 | 134 | partial |
| c5 | Overnight run 1 | 2 s | 2.258 | 741 | 695 | 271 | partial |
| c378 | Overnight run 1 | 2 s | 2.307 | 1127 | 755 | 436 | sharp |
| c29 | Overnight run 1 | 12 s | 2.329 | 1187 | 784 | 496 | sharp |
| N6 c2 | Night 6 | 1+1 s / 1+2 s | 2.12 | 99 | 183 | — | blurred |
| N6 c100 | Night 6 | 1+1 s / 1+2 s | 2.12 | 84 | 153 | — | blurred |
| New card c20 | Card check | 1+1 s | 2.357 | 949 | 739 | — | sharp |
| `T04_001` | v12b part b | 1+1 s | 2.356 | 516 | 664 | 155 | not classed |
| `T05_001` | v12b part c | 1+1 s | 2.347 | 490 | 663 | 146 | not classed |

</details>

### Close-range autofocus recipes

Sharpness scores at close range for each autofocus recipe, from three test patterns. Higher is sharper. The table view has the verdict, JPEG size and powered time.

![Close-range autofocus recipes](assets/camera-report/ch-close-af.png)

<details markdown="1">
<summary>Table view</summary>

| Recipe | Photo | Wait, s | Powered, s | JPEG, MB | Line pairs | Checker | Small text | Verdict | Sharp cycles | Cycles scored |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | :--- | ---: | ---: |
| AF at once 1+4 s | `T20_028` | 5 | 17.4 | 2.31 | 1272 | 930 | 494 | sharp | 3 | 4 |
| AF at once 1+2 s | `T20_022` | 3 | 15.2 | 2.29 | 1071 | 905 | 393 | sharp | 4 | 4 |
| AF at once 0.5+1.5 s | `T20_023` | 2 | 14.1 | 2.26 | 925 | 878 | 328 | sharp | 3 | 4 |
| AF at once 0.5+0.5 s | `T20_024` | 1 | 12.1 | 2.02 | 51 | 65 | 56 | blurred | 0 | 4 |
| 7 s, then AF 1+4 s (today) | `T20_026` | 12 | 23.3 | 2.07 | 63 | 83 | 64 | blurred | 2 | 3 |
| 2 s, then AF 1+4 s | `T20_027` | 7 | 18.6 | 2.11 | 85 | 169 | 71 | blurred | 0 | 4 |
| No AF, 2 s | `T20_025` | 2 | 13.1 | 2.06 | 79 | 155 | 70 | blurred | 0 | 4 |

</details>

### Frame sharpness class by recipe

How each autofocus recipe's frames split into blurred-sized, partial and sharp-sized JPEGs during the first night run.

![Frame sharpness class by recipe](assets/camera-report/ch-recipes-stack.png)

<details markdown="1">
<summary>Table view</summary>

| Id | Recipe | Wait, s | Blurred | Partial | Sharp | Failed | Sharp, % | Powered, s |
| ---: | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | Today: 7 s, then AF 1+4 s | 12 | 2 | 5 | 28 | 1 | 80 | 23.2 |
| 1 | AF at once 1+4 s | 5 | 1 | 6 | 29 | 0 | 81 | 16.3 |
| 2 | AF at once 1+2 s | 3 | 0 | 10 | 20 | 5 | 67 | 14.2 |
| 3 | AF at once 0.5+1.5 s | 2 | 0 | 1 | 32 | 2 | 97 | 13.3 |
| 4 | AF at once 1+1 s | 2 | 0 | 1 | 33 | 1 | 97 | 13.4 |
| 5 | 1+2 s, twice | 6 | 0 | 18 | 15 | 2 | 45 | 17.1 |
| 6 | 0.5+1.5 s, twice | 4 | 2 | 11 | 22 | 0 | 63 | 15.3 |
| 7 | 1 s, then AF 1+2 s | 4 | 0 | 10 | 24 | 1 | 71 | 15.3 |
| 8 | 2 s, then AF 1+2 s | 5 | 0 | 12 | 23 | 0 | 66 | 16.2 |
| 9 | No autofocus (control) | 2 | 35 | 0 | 0 | 0 | 0 | 12 |

</details>

### Sharpness against powered time

Each circle is a recipe, labelled by its number. Further left costs less battery; higher gives more sharp-sized frames. The hollow circle is the control.

![Sharpness against powered time](assets/camera-report/ch-recipes-tradeoff.png)

<details markdown="1">
<summary>Table view</summary>

| Id | Recipe | Sharp, % | Powered, s | Wait, s |
| ---: | :--- | ---: | ---: | ---: |
| 0 | Today: 7 s, then AF 1+4 s | 80 | 23.2 | 12 |
| 1 | AF at once 1+4 s | 81 | 16.3 | 5 |
| 2 | AF at once 1+2 s | 67 | 14.2 | 3 |
| 3 | AF at once 0.5+1.5 s | 97 | 13.3 | 2 |
| 4 | AF at once 1+1 s | 97 | 13.4 | 2 |
| 5 | 1+2 s, twice | 45 | 17.1 | 6 |
| 6 | 0.5+1.5 s, twice | 63 | 15.3 | 4 |
| 7 | 1 s, then AF 1+2 s | 71 | 15.3 | 4 |
| 8 | 2 s, then AF 1+2 s | 66 | 16.2 | 5 |
| 9 | No autofocus (control) | 0 | 12 | 2 |

</details>

### Blurred phase after a start

How long the camera keeps producing blurred-sized frames after a start. Faded bars were still blurred when the run ended, so the true length is longer.

![Blurred phase after a start](assets/camera-report/ch-blur-phase.png)

<details markdown="1">
<summary>Table view</summary>

| Run | Interval, s | Cycles | Minutes | Phase ended |
| :--- | ---: | ---: | ---: | :--- |
| Overnight run 1, cold start | 25 | 28 | 12 | yes |
| Night 6, cold start | 18 | 120 | 36 | yes |
| Night 7, after a 40 min rest | 18 | 15 | 4.5 | yes |
| v12b smoke test and part a | 60 | 170 | 170 | no |

</details>

## Exposure and colour

Brightness, colour and how long the camera waits for exposure to settle before it shoots.

### Powered time by settle window

The settle window is the pause before the shot so exposure and colour can stabilise. A longer window keeps the camera powered longer.

![Powered time by settle window](assets/camera-report/ch-window-awake.png)

<details markdown="1">
<summary>Table view</summary>

| Window | Window, s | Powered, s | JPEG, MB | Brightness, % | Red | Green | Blue | Sharpness, % |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 12 s | 12 | 23.8 | 2.254 | 0 | 1 | 1 | 1 | 0 |
| 4 s | 4 | 15.9 | 2.252 | -0.9 | 0.987 | 0.996 | 0.996 | 0.7 |
| 2 s | 2 | 13.7 | 2.237 | -0.3 | 0.995 | 0.997 | 1.004 | -2.3 |
| 1 s | 1 | 12.7 | 2.232 | -1.5 | 0.953 | 0.996 | 1.002 | -3.8 |
| 0.5 s | 0.5 | 12.4 | 2.271 | -3.4 | 0.877 | 1.007 | 1.011 | 0.3 |

</details>

### Colour channels by settle window

Each channel's level relative to the longest window. Below the dashed line means weaker than at the longest window.

![Colour channels by settle window](assets/camera-report/ch-window-red.png)

<details markdown="1">
<summary>Table view</summary>

| Window | Red | Green | Blue |
| :--- | ---: | ---: | ---: |
| 12 s | 1 | 1 | 1 |
| 4 s | 0.987 | 0.996 | 0.996 |
| 2 s | 0.995 | 0.997 | 1.004 |
| 1 s | 0.953 | 0.996 | 1.002 |
| 0.5 s | 0.877 | 1.007 | 1.011 |

</details>

### Brightness and sharpness change

Percent change against the longest window, for each shorter window.

![Brightness and sharpness change](assets/camera-report/ch-window-deltas.png)

<details markdown="1">
<summary>Table view</summary>

| Window | Brightness, % | Sharpness, % |
| :--- | ---: | ---: |
| 12 s | 0 | 0 |
| 4 s | -0.9 | 0.7 |
| 2 s | -0.3 | -2.3 |
| 1 s | -1.5 | -3.8 |
| 0.5 s | -3.4 | 0.3 |

</details>

### Far-scene autofocus timing

Sharpness of the face, torso and a background pumpkin as a percentage of today's recipe, for each autofocus timing tried. The table view has powered time and the red shift on the stone wall.

![Far-scene autofocus timing](assets/camera-report/ch-far-af.png)

<details markdown="1">
<summary>Table view</summary>

| Condition | Wait, s | Powered, s | Face, % | Torso, % | Pumpkin, % | Red, % |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| 7 s, then AF 1+4 s (today) | 12 | 23.8 | 100 | 100 | 100 | 0 |
| 2 s, then AF 1+4 s | 7 | 18.9 | 100 | 102 | 100 | -1.1 |
| AF at once 1+4 s | 5 | 16.7 | 100 | 100 | 102 | -1.1 |
| AF at once 1+2 s | 3 | 14.7 | 100 | 100 | 98 | -1.1 |
| AF at once 0.5+1.5 s | 2 | 13.8 | 99 | 100 | 98 | -1.8 |
| AF at once 0.5+0.5 s | 1 | 12.8 | 101 | 100 | 93 | -5.4 |
| No AF, 2 s | 2 | 13.7 | 99 | 100 | 93 | -1.8 |

</details>

### Measured image properties

Each property with what was measured, the evidence for it and the project note it came from.

| Property | Measured | Evidence | Source |
| :--- | :--- | :--- | :--- |
| Output size | 2592×1944 (5 MP) JPEG | verified | stage-a-findings |
| Sharpest edge (10–90 % width) | 4.59 px at 40 cm with autofocus; a truly sharp 5 MP image is 2–3 px, so roughly half the linear detail | verified | stage-a-findings |
| Noise | Low in good light; grainy in evening room light | verified | stage-a-findings |
| Highlight clipping | 15–16 % of the frame pure white (bright windows, sky); EV −2 only lowers that to about 14 % | verified | stage-a-findings |
| Exposure control | Automatic exposure beat every manual setting in low light; manual saturates between 2,000 and 8,000 lines; gain 240 stayed darker than auto at dusk | verified | stage-a-findings |
| EV compensation | About 10–15 brightness levels per step in steady light; settings reset on every photo | verified | stage-a-findings |
| Evening room light | Dark, green in the middle, purple/pink in the corners, grainy (subject at about 1 m) | verified; fails the charter bar for room scenes | stage-a-findings |
| Colour settling | Red channel about 5 % low after 1 s and 12 % low after 0.5 s; indistinguishable from 12 s at 2 s | verified (one frame per window) | settle-window-sweep |
| Autofocus range | Essential under about 1 m; little or no difference beyond about 1.5 m (the lens rests near far focus) | verified | stage-a-findings |
| Field of view on focus | Sharp frames are shifted 12 px (0.5 % of the width) sideways compared with blurred ones | inference (likely lens movement) | settle-window-sweep |
| Wrong picture size | After a power cycle the camera can return 1600×1200 (about 0.9 MB) instead of full size; a retry fixed it every time | verified | stage-a-findings |
| Truncated JPEG | Reported length normal but no end marker: 3.2 % of cycles in the first overnight run, 14 % in the A/B night, up to 34 % of first attempts in the late v12b session | verified; cause open | settle-window-sweep, v12b-hardware-results |
| Camera SPI clock | 8 MHz maximum (manufacturer specification) | documented | settle-window-sweep |
| Night scenes | Out of scope; dark frames averaged about 2 of 255 in brightness and held no usable edges | verified | stage-a-findings |

## Timing and powered time

How long the camera stays powered for each photo, and where that time goes.

### Powered time along the optimisation path

Powered seconds per photo at each step. Faded bars are estimates rather than hardware measurements.

![Powered time along the optimisation path](assets/camera-report/ch-awake-path.png)

<details markdown="1">
<summary>Table view</summary>

| Step | Powered, s | Range, s | Basis |
| :--- | ---: | :--- | :--- |
| Stage A: `tl_cycle` v2, AF on, 12 s window | 25.9 | 22.7–27.0 | measured (100 cycles) |
| Window sweep baseline: 12 s window, AF off | 23.8 | — | measured (5 cycles) |
| 2 s window, AF off, library read | 13.7 | — | measured (5 cycles) |
| 2 s window, burst read, 32 KB, SD 16 MHz, with read-back | 12.5 | — | measured (6 cycles); read-back costs about 3.2 s |
| Same path without read-back | 9.3 | — | estimate from log timestamps |
| `tl_cycle` v12b on the board, 60 s interval, no retake | 10.8 | 10.4–11.1 | measured (459 cycles) |
| `tl_cycle` v12b with one retake | — | 19.3–21.4 | measured; +8.7 s per retake |

</details>

### Where the powered seconds go

Start-up, settle window, transfer to the SD card and everything else, for each configuration.

![Where the powered seconds go](assets/camera-report/ch-time-budget.png)

<details markdown="1">
<summary>Table view</summary>

| Configuration | Start-up, s | Window, s | Transfer, s | Other, s | Total, s | Basis |
| :--- | ---: | ---: | ---: | ---: | ---: | :--- |
| `tl_cycle` v11 (today) | 1.2 | 12 | 7.4 | 0.6 | 21.2 | split estimated from code and logs; measured total 21.0 s |
| Best path tested (estimate) | 0.8 | 2 | 5.9 | 0.6 | 9.3 | estimate from log timestamps; SD 16 MHz, no read-back |

</details>

### Transfer path timing

Time to move one photo from the camera to the SD card for each data path, split into camera read, SD write and everything else.

![Transfer path timing](assets/camera-report/ch-transfer.png)

<details markdown="1">
<summary>Table view</summary>

| Path | Camera, ms | SD, ms | Other, ms | Transfer, ms | Powered, s |
| :--- | ---: | ---: | ---: | ---: | ---: |
| Library read, 8 KB, SD 8 MHz (today) | 4380 | 5100 | 566 | 10046 | 18 |
| Library read, 8 KB, SD 16 MHz | 4365 | 3816 | 565 | 8746 | 15.4 |
| Burst read, 8 KB, SD 8 MHz | 2279 | 5083 | 371 | 7733 | 15.7 |
| Burst read, 32 KB, SD 8 MHz | 2273 | 4553 | 368 | 7194 | 15.2 |
| Burst read, 32 KB, SD 16 MHz | 2273 | 3239 | 367 | 5879 | 12.5 |

</details>

### Start-up times by SD card

Milliseconds after power-on until the SD card is ready, the camera is ready and the first full-size frame arrives.

![Start-up times by SD card](assets/camera-report/ch-startup.png)

<details markdown="1">
<summary>Table view</summary>

| Card | SD ready, ms | Camera ready, ms | First frame, ms |
| :--- | ---: | ---: | ---: |
| 16 GB card | 452 | 705 | 830 |
| 128 GB card | 557 | 809 | — |

</details>

### Measured stage timings

Timings for individual stages of a capture cycle, with the project note each came from.

| Stage | Value | Source |
| :--- | :--- | :--- |
| SD card ready after power-on | 450 ms (16 GB card), 557 ms (128 GB card) | stage-a-findings, settle-window-sweep |
| Camera ready after power-on | 700 ms (16 GB card), 809 ms (128 GB card) | stage-a-findings, settle-window-sweep |
| First full-size warm-up frame | about 830 ms after power-on (16 GB card) | stage-a-findings |
| Settle window (warm-up to photo) | 12 s in `tl_cycle` v11; 2 s in v12b | settle-window-sweep, tl-cycle-12-draft |
| Capture call | median 105 ms in good cycles, 89 ms in failed ones (night run 6) | settle-window-sweep |
| Camera to controller read, 2.15 MB | 4.38 s with the library; 2.27 s with burst reads (0.94 MB/s) | settle-window-sweep |
| Write to SD, 2.15 MB | 5.1 s (8 MHz, 8 KB writes) down to 3.2 s (16 MHz, 32 KB writes); 4.7 s median on the 128 GB card at 8 MHz | settle-window-sweep |
| Wake to power-off, whole photo | 25.9 s in Stage A; 10.8 s in v12b (no retake) | stage-a-findings, v12b-hardware-results |
| Cost of one retake | +8.7 s powered per retaken photo in v12b (+1.3 s for the earlier wrong-size retry) | v12b-hardware-results, stage-a-findings |

## File size and storage

How big the photos are and what a long run needs from the card.

### JPEG size by scene

Smallest to largest file seen in each scene. The tick marks the mean or typical size.

![JPEG size by scene](assets/camera-report/ch-jpeg.png)

<details markdown="1">
<summary>Table view</summary>

| Scene | Smallest, MB | Largest, MB | Typical, MB | Note |
| :--- | ---: | ---: | ---: | :--- |
| Dark spot, 100-cycle run (session 14) | 0.49 | 0.84 | — | Mean brightness about 2 of 255 |
| Dark spot, 15 cm (sessions 10–12) | 0.7 | 0.84 | — | AF and no-AF about 0.79 vs 0.80 MB |
| Wrong default size 1600×1200 | 0.9 | 0.9 | 0.9 | About 0.9 MB |
| Bright room scene (v11 baseline) | 1.54 | 1.67 | 1.62 | Cycles 7 to 10 |
| 25 cm focus page, blurred frames | 2.03 | 2.18 | — | Night runs and v12b |
| Two studio lights, 15 cm (session 12) | 2.2 | 2.2 | 2.2 | About 2.2 MB |
| Window-sweep still life (window means) | 2.232 | 2.271 | — | 25 cycles, good lighting |
| 25 cm focus page, sharp frames | 2.28 | 2.37 | — | Night runs, night 6 and the new card |
| Stage A indoor scene (100 cycles) | 2.18 | 3 | 2.84 | Mean 2.84 MB |

</details>

### Storage for a long run

Gigabytes needed at several JPEG sizes, with dashed lines at the capacity of common cards. Solid bars use the measured Stage A mean; grey bars use sizes from the plan table.

![Storage for a long run](assets/camera-report/ch-storage.png)

<details markdown="1">
<summary>Table view</summary>

| JPEG, MB | Run total, GB | Basis |
| ---: | ---: | :--- |
| 1 | 43 | plan table |
| 2 | 86 | plan table |
| 2.84 | 123 | measured Stage A mean |
| 3 | 130 | plan table |
| 4 | 173 | plan table |
| 5 | 216 | plan table |

| Card | Capacity, GB |
| :--- | ---: |
| 256 GB (planned, not bought) | 256 |
| 128 GB (in use) | 128 |
| 16 GB (original) | 16 |

</details>

## Reliability

Truncated files, retakes, wrong-size captures and SD read-back failures.

### Photo outcomes in the latest firmware build

Each session's photos split into good on the first try, good after a retake, and failed. The table view has the retake rate.

![Photo outcomes in the latest firmware build](assets/camera-report/ch-v12b-outcomes.png)

<details markdown="1">
<summary>Table view</summary>

| Session | Cycles | First try | Rescued | Failed | Retake, % | Battery low, mV | Battery high, mV |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 2 (smoke test) | 20 | 20 | 0 | 0 | 0 | 4004 | 4024 |
| 3 (part a) | 150 | 150 | 0 | 0 | 0 | 4016 | 4084 |
| 4 (part b) | 150 | 133 | 14 | 3 | 11.3 | 4076 | 4140 |
| 5 (part c) | 139 | 92 | 31 | 16 | 33.8 | 4132 | 4188 |

</details>

### Retakes through the late session

Retaken photos per block of cycles, to show whether retakes cluster late in a session.

![Retakes through the late session](assets/camera-report/ch-retake-v12b.png)

<details markdown="1">
<summary>Table view</summary>

| Cycles | Cycles in block | Retakes |
| :--- | ---: | ---: |
| 1–30 | 30 | 4 |
| 31–60 | 30 | 12 |
| 61–90 | 30 | 11 |
| 91–120 | 30 | 11 |
| 121–139 | 19 | 9 |

</details>

### Truncated JPEGs through the A/B night

Truncated files per block of cycles across the night of the A/B test.

![Truncated JPEGs through the A/B night](assets/camera-report/ch-trunc-n6.png)

<details markdown="1">
<summary>Table view</summary>

| Cycles | Minutes | Truncated |
| :--- | ---: | ---: |
| 1–30 | 9 | 5 |
| 31–60 | 18 | 9 |
| 61–90 | 27 | 11 |
| 91–120 | 36 | 16 |
| 121–150 | 45 | 19 |
| 151–180 | 54 | 7 |
| 181–210 | 63 | 1 |
| 211–240 | 72 | 4 |
| 241–270 | 81 | 1 |
| 271–300 | 90 | 0 |
| 301–330 | 99 | 2 |
| 331–360 | 108 | 0 |
| 361–390 | 117 | 0 |
| 391–420 | 126 | 0 |
| 421–450 | 135 | 2 |
| 451–480 | 144 | 0 |
| 481–510 | 153 | 0 |
| 511–540 | 162 | 0 |

</details>

### Truncated JPEGs by condition

Truncated files per condition, split by whether the file length was still growing when read or had stopped without an end marker.

![Truncated JPEGs by condition](assets/camera-report/ch-trunc-ab.png)

<details markdown="1">
<summary>Table view</summary>

| Condition | Kind | Cycles | Truncated | Growing | Steady | Powered, s |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: |
| 0: AF 1+1 s, poll on | condition | 135 | 19 | 1 | 18 | 11.7 |
| 1: AF 1+1 s, poll off | condition | 135 | 13 | 0 | 13 | 11.5 |
| 2: AF 1+2 s, poll on | condition | 135 | 26 | 18 | 8 | 12 |
| 3: AF 1+2 s, poll off | condition | 135 | 19 | 9 | 10 | 12.2 |
| Poll on, pooled | pooled | 270 | 45 | 19 | 26 | 11.84 |
| Poll off, pooled | pooled | 270 | 32 | 9 | 23 | 11.85 |

</details>

### Wrong-size photos

Share of cycles whose first capture came out at the default size instead of the one requested, by test and autofocus setting.

![Wrong-size photos](assets/camera-report/ch-wrong-size.png)

<details markdown="1">
<summary>Table view</summary>

| Test | Autofocus | Wrong size | Cycles | Rate, % |
| :--- | :--- | ---: | ---: | ---: |
| v4, evening room light | not stated | 7 | 20 | 35 |
| v5, autofocus on | on | 8 | 8 | 100 |
| v5, autofocus off | off | 1 | 10 | 10 |
| Midday, bright, AF | on | 0 | 10 | 0 |
| Midday, dimmed, AF | on | 0 | 10 | 0 |
| Midday, dimmed, no AF | off | 0 | 10 | 0 |
| Dark spot, AF (session 10) | on | 5 | 10 | 50 |
| Dark spot, no AF (session 11) | off | 0 | 10 | 0 |
| Two studio lights, AF (session 12) | on | 0 | 10 | 0 |
| Dark spot, AF (sessions 13 and 14) | on | 110 | 110 | 100 |

</details>

### Failed SD read-backs

Share of verified photos whose read-back differed from what was written, by clock setting.

![Failed SD read-backs](assets/camera-report/ch-readback.png)

<details markdown="1">
<summary>Table view</summary>

| Condition | Clocks | Verified | Failed | Rate, % |
| :--- | :--- | ---: | ---: | ---: |
| Night run 1, autofocus cycles 1–200 | write 16 / read 16 MHz | 171 | 5 | 2.9 |
| Night run 1, autofocus cycles 201–380 | write 16 / read 16 MHz | 159 | 32 | 20.1 |
| Night run 1, no-AF control | write 16 / read 16 MHz | 38 | 14 | 36.8 |
| Night run 2, write 8 / read 8 MHz | 41-cycle run before the hang | 12 | 0 | 0 |
| Night run 2, write 16 / read 8 MHz | 41-cycle run before the hang | 9 | 0 | 0 |
| Night run 2, write 16 / read 16 MHz | 41-cycle run before the hang | 10 | 2 | 20 |

</details>

## Evidence and caveats

### How to read these numbers

Sharpness on long runs is judged from JPEG file size. The size classes were calibrated against photos scored directly with the line-pair, checkerboard and small-text tests, so a size class is a proxy rather than a measurement.

Faded bars on the powered-time path are estimates, and so is the stage split in the powered-seconds chart; the basis column says how each was worked out. The other powered-time bars were measured on hardware.

One step on the path, the latest firmware with a retake, only has a range, so it appears in that chart's table but not on the chart.

Storage bars drawn in grey use sizes from the plan table where no measurement exists.

### Headline facts

| Headline fact | Value | Note |
| :--- | :--- | :--- |
| Picture size | 2592×1944 | 5 MP JPEG; every Stage A and later run saved at this size |
| Sharpest edge width | 4.59 px | Flat target at 40 cm with autofocus, 10–90 % edge width. A truly sharp 5 MP image measures 2–3 px |
| Stage A 100-cycle run | 100 of 100 | One early run, saved at full size with no failure, unexpected reset or SD error. Camera and SD stayed powered (power was not switched); later switched-power runs lost cycles, see Reliability |
| Sharp-sized frames, best recipes | 97 % | 25 cm, warm camera, autofocus right after the warm-up and 2 s in all (two recipes, about 35 cycles each) |
| Powered time per photo | 10.8 s | `tl_cycle` v12b on the board, no retake; Stage A took 25.9 s |
| Mean JPEG size | 2.84 MB | Stage A indoor scene; 43,200 photos (one per minute for 30 days) would be about 123 GB |
| Blurred-sized below | 2.18 MB | Photos under this size were blurred in 9 of 9 measured (night run 1) |
| Sharp-sized from | 2.28 MB | Photos from this size were sharp in 3 of 3 measured; sizes between are mixed |

*Numbers come from the project's test notes and brief: the Stage A findings, settle-window sweep, hardware results, A/B test plan, test runner, build notes and USB photo transfer notes.*
