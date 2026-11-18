# Co-run observation — Sogni + disNet (Nov 17–18, 2026)

A 24-hour observation window, **Nov 17 7:00 PM → Nov 18 7:00 PM Toronto time**,
during which the Sogni-priority gates on all three Novacore rigs are in
observe mode and the Dispersed (disNet) nodes co-run with the Sogni workers
instead of being parked.

**Learning goal:** for every Sogni error and every disNet failed job, identify
which Sogni model/workflow was running on that rig at that moment, and which
hours carry the heavy video models. No gate policy changes during the window.

## Files

- `corun-24h-state.json` — the sampler state, refreshed hourly:
  - `samples` — every 5 minutes: per-rig disNet busy flags and per-worker
    Sogni completion/error counters (workers 462 = x870, 463 = x570,
    478 = adam5070; rigs keyed 870 / 570 / 5070).
  - `jobs` — the per-rig Sogni job timeline from the workers' own timing
    records: timestamp, rig, workflow/model name, class (image / video /
    audio) and inference seconds. This is what ties an error or a failed
    disNet job to the exact model that was co-running.
  - `baseline`, `eta_watermark_ms`, window start/end.
- `media-split-hourly.csv` — one row per worker per hour (backfilled from
  Nov 15 7:00 PM Toronto): image / video / audio job counts and inference
  seconds, and total busy seconds.

Data is read-only observation output. The timing records are a sample of
jobs, not a complete ledger.

Last upload: 2026-11-18T03:54:32Z
