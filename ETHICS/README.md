# Ethics — PYMMCORE

**Project:** PYMMCORE  
**Category:** SCIENTIFIC_LAB  
**Upstream:** see BENCH.json  
**Pinned commit:** `4bb2d63cd7926faaeea901c1de5d1b28a3912587`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `bcebdb1f0443644c9c1190d11a12416fc5e0fc23d51cea7f35c67784d102a0a2`  
**Date:** October 2026

## Position

PYMMCORE is packaged for offline deployment with a verifiable audit trail. The
ethical questions this raises are answered by making the system's behaviour
checkable rather than by policy statements.

## The four commitments

1. **No hidden egress.** The deployment has no external API dependency; this is
   testable by running it with the network disconnected.
2. **Attributable output.** Every artifact is recorded in a hash chain, so what
   the system produced can be reconstructed.
3. **Operator control.** The institution owns the hardware and the keys.
4. **Refusal to overclaim.** Where a certification is not held, the project says
   so rather than implying it.

## Dual use

This project is packaged for civilian and public-sector deployment. Where an
upstream has dual-use characteristics, the licence gate and the reference-only
marking in `BENCH.json` record that.
