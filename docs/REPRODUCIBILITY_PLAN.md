# Reproducibility plan

## Gates and outputs

| Gate | Input | Required output |
|---|---|---|
| Provenance | Original firmware, ELF/MAP, model export, raw logs | File inventory and SHA-256 hashes |
| Configuration | Build settings and clock evidence | Verified core frequency, CAN rate and compiler flags |
| Decode | Verified C structs and raw dumps | Normalized records with consistency checks |
| Aggregate | Validated runs | Per-run summaries and six configuration summaries |
| Compare | Tables/figures from the reference manuscript | A result-by-result comparison with explained differences |

## Planned consistency checks

1. Verify the raw format before interpreting byte offsets or alignment.
2. Preserve the 32-bit timestamp wrap semantics stated by the measurement implementation.
3. Check sequence, record count, score/sign, padding and metadata totals.
4. Keep all valid runs, and retain an exclusion log for invalid runs.
5. Use run-level replication for aggregate variation; do not relabel dependent records as independent trials.
6. Record input/model/timer configuration explicitly. The reference design has no attack-input timer-on runs.

## Sharing scope

This preparation repository contains documentation and a manifest header. It does not yet
contain the original firmware, model arrays, raw observations, manuscript PDF or vendor SDK.
Import each original artifact with provenance and its applicable redistribution terms.

## Release condition

A reproducible release needs actual execution commands, the required accessible inputs,
successful comparison output, and a limitations section. A documentation-only revision
must remain labeled as preparation.
