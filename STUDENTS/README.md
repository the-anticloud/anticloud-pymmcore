# Students — PYMMCORE

**Project:** PYMMCORE  
**Category:** SCIENTIFIC_LAB  
**Upstream:** see BENCH.json  
**Pinned commit:** `4bb2d63cd7926faaeea901c1de5d1b28a3912587`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `bcebdb1f0443644c9c1190d11a12416fc5e0fc23d51cea7f35c67784d102a0a2`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `4bb2d63cd7926faaeea901c1de5d1b28a3912587`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `bcebdb1f0443644c9c1190d11a12416fc5e0fc23d51cea7f35c67784d102a0a2`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.
