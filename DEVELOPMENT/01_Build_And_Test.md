# Build and Test

**Project:** `PYMMCORE`
**Upstream:** https://github.com/sksuzuki/pymmcore
**License:** Apache 2.0

## Quick Start

```bash
git clone https://github.com/sksuzuki/pymmcore
cd pymmcore
pip install -r requirements-anticloud.txt
python anticloud_main.py --offline --pax-local
```

## Anticloud Improvements Applied

1. PAX L5 Narrow L2 General 27B hypothesis generation and literature synthesis — fully local
2. AIOSS cryptographic audit chain for all experimental records (FDA 21 CFR Part 11 aligned)
3. AES-256 encryption for raw data files, notebook checkpoints, and results
4. Single-binary lab management system with embedded instrument drivers
5. Offline data analysis pipeline: replaces cloud compute with local GPU/CPU inference
6. Version-controlled experiment ledger: immutable record of parameters and outcomes
7. Zero-telemetry: removes all upstream usage analytics and phoning-home
8. CLI pipeline runner replacing web-only workflow interfaces

## Benchmark Targets

| Metric | Target |
| --- | --- |
| Latency | Primary inference task: <5s on CPU, <1s on GPU |
| Throughput | Batch processing: >100 items/hour on single CPU server |
| Memory | <8GB RAM for standard deployment |
| Accuracy | Task-specific accuracy within 5% of cloud-API baseline |

## Build Status

Not yet measured. Run verified build and record actual figures above.
