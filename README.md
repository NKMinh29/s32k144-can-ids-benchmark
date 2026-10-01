# S32K144 CAN IDS Processing-Time Benchmark

**Status: repository preparation.** This draft describes an existing research project.
Firmware, raw logs, and reproduction scripts have not yet been imported into this starter.
Conference acceptance and publication metadata are not asserted here.

## Research question

How do a single-threshold detector (D3) and an integer MLP (D4) differ in deployed
per-frame processing time, and how does a periodic interrupt affect the measured path?

## Reference manuscript

*Processing-Time Characterization of Single-Threshold and Integer-MLP CAN Intrusion Detectors on the S32K144*.
The reference used for this draft is the manuscript revision dated 16 September 2026.

## Measurement boundary

The measured helper includes feature construction, runtime dispatch, inference,
result publication, and LED action. RX waiting, record writes, and receiver rearming
are outside the interval. Measurements include interrupt execution occurring inside
the boundary. They are processing times, not pure model inference times or end-to-end latency.

## Results reported in the manuscript

These numbers have **not been independently regenerated from raw logs in this starter**.

| Item | Reported configuration/result |
|---|---|
| Platform | S32K144, 48 MHz, bare-metal |
| Build | One ELF; GCC 6.3.1; `-O1` |
| Data | 18 runs × 128 records = 2,304 observations |
| D3, timer off | 275 cycles / 5.729 µs |
| D4, timer off | 23,322 cycles / 485.875 µs |
| D4 normal, timer on | 26/384 records with an observed timer entry |
| Maximum D4 normal, timer on | 2,365.271 µs |

The experiment contains three replicates of six configurations:
D3/D4 × normal-off, attack-off, and normal-on. Attack inputs were not measured with the timer enabled.

## Reproduction plan

1. Identify the exact source, ELF, MAP, model export, raw logs, and environment.
2. Record hashes and run metadata in `docs/ARTIFACTS.md`.
3. Implement the decoder against the verified C record layout.
4. Validate each run and export normalized CSV.
5. Regenerate run-level summaries and figures.
6. Compare every reported result with the manuscript; document differences.

There is no reproduction command yet because the required original artifacts have not been imported.

## Interpretation and limitations

- D3 collapsed to the threshold `ID <= 1` on the selected data. This is a comparison of these exports, not a general ranking of model families.
- D4 is a compiled integer MLP; the measured firmware does not deploy TensorFlow Lite Micro.
- The audited dataset split contains repeated vectors and a strong identifier shortcut. Perfect test accuracy does not establish attack generalization.
- Processing counts after application reception do not quantify earlier frame loss.
- The low-rate traffic experiment is not a saturation test; observed maxima are not WCET bounds.
- Host arithmetic parity and the four hardware probes provide different levels of evidence.

## Sharing and attribution

Only files with confirmed sharing rights should be imported. Vendor SDK/toolchain
components should be obtained through their original distribution channels when redistribution
is not permitted. Code, data, and manuscript licensing must be recorded separately.

Author contributions and publication/citation details will be completed from confirmed project records.
