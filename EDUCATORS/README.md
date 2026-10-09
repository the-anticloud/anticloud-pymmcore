# Educators — PYMMCORE

**Project:** PYMMCORE  
**Category:** SCIENTIFIC_LAB  
**Upstream:** see BENCH.json  
**Pinned commit:** `4bb2d63cd7926faaeea901c1de5d1b28a3912587`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `bcebdb1f0443644c9c1190d11a12416fc5e0fc23d51cea7f35c67784d102a0a2`  
**Date:** October 2026

## Teaching with PYMMCORE

The project is usable as a worked example of offline-first packaging with a
cryptographic audit chain. It ships with the assurance suite, the evidence
register and the ledger, so students can verify claims rather than take them on
faith.

## Suggested exercises

1. Run `python tools/run_bench.py --out BENCH.json` and read the 16 results.
2. Recompute the SHA3-256 of a row's evidence file and compare to the register.
3. Walk the AIOSS chain from genesis to head `bcebdb1f0443644c9c1190d11a12416fc5e0fc23d51cea7f35c67784d102a0a2` and confirm every link.
4. Break one artifact and observe the chain fail to verify.

## Licence for teaching

Apache 2.0 terms apply to academic and teaching use. See `24_ANTICOMMONS_LICENSE`.
