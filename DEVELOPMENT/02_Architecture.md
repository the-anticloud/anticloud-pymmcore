# Technical Architecture — PYMMCORE

**Upstream:** [https://github.com/sksuzuki/pymmcore](https://github.com/sksuzuki/pymmcore)
**License:** Apache 2.0
**Category:** SCIENTIFIC_LAB
**Anticloud Integration:** PAX L5 Narrow L2 General 27B + AIOSS + Offline-First

## Upstream Description

Python bindings for Micro-Manager microscope control

## Anticloud Architectural Changes

1. PAX L5 Narrow L2 General 27B hypothesis generation and literature synthesis — fully local
2. AIOSS cryptographic audit chain for all experimental records (FDA 21 CFR Part 11 aligned)
3. AES-256 encryption for raw data files, notebook checkpoints, and results
4. Single-binary lab management system with embedded instrument drivers
5. Offline data analysis pipeline: replaces cloud compute with local GPU/CPU inference
6. Version-controlled experiment ledger: immutable record of parameters and outcomes
7. Zero-telemetry: removes all upstream usage analytics and phoning-home
8. CLI pipeline runner replacing web-only workflow interfaces

## Integration Points

- **PAX Inference Socket:** Local HTTP endpoint at `127.0.0.1:11434/v1/chat` — same OpenAI-compatible API, zero cloud
- **AIOSS Hook:** Every write operation calls `aioss_append(event, payload)` before commit
- **Encryption Layer:** All file I/O routed through `anticloud_crypto.encrypt_at_rest()`
- **Single Binary Build:** `pyinstaller anticloud_pymmcore.spec` or `go build -o pymmcore`

## Deployment Modes

| Mode | Hardware | Notes |
| --- | --- | --- |
| Edge CPU | Raspberry Pi 4 / Intel NUC | Full feature set, PAX on CPU |
| Desktop GPU | RTX 3060 / A10 | PAX GPU inference, <1s latency |
| Server | 2× A100 | Full batch throughput |
| Air-gapped | Any x86/ARM | Zero network dependency |