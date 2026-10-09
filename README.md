# PYMMCORE

![license](https://img.shields.io/badge/license-license-blue) ![offline-first](https://img.shields.io/badge/offline--first-air--gap-green) ![audit](https://img.shields.io/badge/audit-SHA3--256-orange) ![category](https://img.shields.io/badge/category-scientific_lab-lightgrey)

> Anticloud-hardened packaging of the upstream project `PYMMCORE` in category **SCIENTIFIC LAB**. Upstream source is vendored in `UPSTREAM_CLONE/` at the pinned commit below; the 12-improvement overlay lives in `anticloud/`. Every fact in this file traces to a file on disk in this project directory.

**Category:** SCIENTIFIC LAB · **Upstream:** https://github.com/micro-manager/pymmcore · **Upstream pin:** `4bb2d63cd7926faaeea901c1de5d1b28a3912587` · **Vendor:** Anticloud FZ LLE

---

## What This Project Does

# pymmcore-plus

[![License](https://img.shields.io/pypi/l/pymmcore-plus.svg?color=green)](https://github.com/pymmcore-plus/pymmcore-plus/raw/master/LICENSE)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/pymmcore-plus)](https://pypi.org/project/pymmcore-plus)
[![PyPI](https://img.shields.io/pypi/v/pymmcore-plus.svg?color=green)](https://pypi.org/project/pymmcore-plus)
[![Conda](https://img.shields.io/conda/vn/conda-forge/pymmcore-plus)](https://anaconda.org/conda-forge/pymmcore-plus)
[![CI](https://github.com/pymmcore-plus/pymmcore-plus/actions/workflows/ci.yml/badge.svg)](https://github.com/pymmcore-plus/pymmcore-plus/actions/workflows/ci.yml)
[![docs](https://github.com/pymmcore-plus/pymmcore-plus/actions/workflows/docs.yml/badge.svg)](https://pymmcore-plus.github.io/pymmcore-plus/)
[![codecov](https://codecov.io/gh/pymmcore-plus/pymmcore-plus/branch/main/graph/badge.svg)](https://codecov.io/gh/pymmcore-plus/pymmcore-plus)
[![Benchmarks](https://img.shields.io/endpoint?url=https://codspeed.io/badge.json)](https://codspeed.io/pymmcore-plus/pymmcore-plus)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.14812446.svg)](https://doi.org/10.5281/zenodo.14812446)

`pymmcore-plus` extends [pymmcore](https://github.com/micro-manager/pymmcore)
(python bindings for the C++ [micro-manager
core](https://github.com/micro-manager/mmCoreAndDevices/)) with a number of
features designed to facilitate working with **Micro-manager in pure python/C
environments**.

- `pymmcore_plus.CMMCorePlus` is a drop-in replacement subclass of
  `pymmcore.CMMCore` that provides a number of helpful overrides and additional
  convenience functions beyond the standard [CMMCore
  API](https://javadoc.scijava.org/Micro-Manager-Core/mmcorej/CMMCore.html). See
  [CMMCorePlus
  documentation](https://pymmcore-plus.github.io/pymmcore-plus/api/cmmcoreplus/)
  for details.
- `pymmcore-plus` includes an [acquisition engine](https://pymmcore-plus.github.io/pymmcore-plus/guides/mda_engine/)
  that drives micro-manager for conventional multi-dimensional experiments. It accepts an
  [MDASequence](https://pymmcore-plus.github.io/useq-schema/schema/sequence/)
  from [useq-schema](https://pymmcore-plus.github.io/useq-schema/) for
  experiment design/declaration.
- Adds a [callback
  system](https://pymmcore-plus.github.io/pymmcore-plus/api/events/) that adapts
  the CMMCore callback object to an existing python event loop (such as Qt, or
  perhaps asyncio/etc...). The `CMMCorePlus` class also fixes a number of
  "missed" events that are not currently emitted by the CMMCore API.

## Documentation

<https://pymmcore-plus.github.io/pymmcore-plus/>

## Why not just use `pymmcore` directly?

[pymmcore](https://github.com/micro-manager/pymmcore) is (and should probably
remain) a thin SWIG wrapper for the C++ code at the core of the
[Micro-Manager](https://github.com/micro-manager/mmCoreAndDevices/) project. It
is sufficient to control micromanager via python, but lacks some "niceties" that
python users are accustomed to. This library:

- extends the `pymmcore.CMMCore` object with [additional
  methods](https://pymmcore-plus.github.io/pymmcore-plus/api/cmmcoreplus/)
- fixes emission of a number of events in `MMCore`.
- provide proper python interfaces for various objects like
  [`Configuration`](https://pymmcore-plus.github.io/pymmcore-plus/api/configuration/)
  and [`Metadata`](https://pymmcore-plus.github.io/pymmcore-plus/api/metadata/).
- provides an [object-oriented
  API](https://pymmcore-plus.github.io/pymmcore-plus/api/device/) for Devices
  and their properties.
- uses more interpretable `Enums` rather than `int` for [various
  constants](https://pymmcore-plus.github.io/pymmcore-plus/api/constants/)
- improves docstrings and type annotations.
- generally feel more pythonic (note however, `camelCase` method names from the
  CMMCore API are _not_ substituted with `snake_case`).

## How does this relate to `Pycro-Manager`?

[Pycro-Manager](https://github.com/micro-manager/pycro-manager) is designed to
make it easier to work with and control the Java Micro-manager application
(MMStudio) using python. As such, it requires Java to be installed and for
MMStudio to be running a server in another process. The python half communicates
with the Java half using ZeroMQ messaging.

**In brief**: while `Pycro-Manager` provides a python API to control the Java
Micro-manager application (which in turn controls the C++ core), `pymmcore-plus`
provides a python API to control the C++ core directly, without the need for
Java in the loop. Each has its own advantages and disadvantages! With
pycro-manager you retain the entire existing micro-manager ecosystem
and GUI application. With pymmcore-plus, the entire thing is python: you
don't need to install Java, and you have direct access to the memory buffers
used by the C++ core.  Work on recreating the gui application in python
being done in [`pymmcore-widgets`](https://github.com/pymmcore-plus/pymmcore-widgets)
and [`pymmcore-gui`](https://github.com/pymmcore-plus/pymmcore-gui).

## Quickstart

### Install

from pip

```sh
pip install pymmcore-plus

# or, add the [cli] extra if you wish to use the `mmcore` command line tool:
pip install "pymmcore-plus[cli]"

# add the [io] extra if you wish to use the tiff or zarr writers
pip install "pymmcore-plus[io]"
```

from conda

```sh
conda install -c conda-forge pymmcore-plus
```

dev version from github

```sh
pip install 'pymmcore-plus[cli] @ git+https://github.com/pymmcore-plus/pymmcore-plus'
```

Usually, you'll then want to install the device adapters. Assuming you've
installed with `pip install "pymmcore-plus[cli]"`, you can run:

```sh
mmcore install
```

(you can also download these manually from [micro-manager.org](https://micro-manager.org/Micro-Manager_Nightly_Builds))

_See [installation documentation](https://pymmcore-plus.github.io/pymmcore-plus/install/) for more details._

### Usage

Then use the core object as you would `pymmcore

*(excerpt; full text in `UPSTREAM_CLONE/`)*

*Quoted from the upstream `README.md` file in `UPSTREAM_CLONE/`.*
Project-specific facts detected in this directory:

- Ecosystem: **Python** (manifests: pyproject.toml; scanned in UPSTREAM_CLONE)
- Top-level source layout: `examples/`, `src/`, `tests/`
- Snapshot size: **187 files**, **36400 lines of code** (measured; see Benchmarks)
- Primary languages: `.py` (141), `.md` (32), `.png` (4), `(none)` (3), `.cfg` (1), `.css` (1)
- Upstream commit pinned for this packaging: `4bb2d63cd7926faaeea901c1de5d1b28a3912587`

---

## Installation

MMStudio to be running a server in another process. The python half communicates
with the Java half using ZeroMQ messaging.

**In brief**: while `Pycro-Manager` provides a python API to control the Java
Micro-manager application (which in turn controls the C++ core), `pymmcore-plus`
provides a python API to control the C++ core directly, without the need for
Java in the loop. Each has its own advantages and disadvantages! With
pycro-manager you retain the entire existing micro-manager ecosystem
and GUI application. With pymmcore-plus, the entire thing is python: you
don't need to install Java, and you have direct access to the memory buffers
used by the C++ core.  Work on recreating the gui application in python
being done in [`pymmcore-widgets`](https://github.com/pymmcore-plus/pymmcore-widgets)
and [`pymmcore-gui`](https://github.com/pymmcore-plus/pymmcore-gui).

*Section quoted from the upstream readme.*
Overlay install (this project):

```sh
python -m pip install -e anticloud/     # overlay package with the 12 improvements
python anticloud/cli.py --help          # 13 subcommands, JSON stdout
```

---

## Usage

[pymmcore](https://github.com/micro-manager/pymmcore) is (and should probably
remain) a thin SWIG wrapper for the C++ code at the core of the
[Micro-Manager](https://github.com/micro-manager/mmCoreAndDevices/) project. It
is sufficient to control micromanager via python, but lacks some "niceties" that
python users are accustomed to. This library:

- extends the `pymmcore.CMMCore` object with [additional
  methods](https://pymmcore-plus.github.io/pymmcore-plus/api/cmmcoreplus/)
- fixes emission of a number of events in `MMCore`.
- provide proper python interfaces for various objects like
  [`Configuration`](https://pymmcore-plus.github.io/pymmcore-plus/api/configuration/)
  and [`Metadata`](https://pymmcore-plus.github.io/pymmcore-plus/api/metadata/).
- provides an [object-oriented
  API](https://pymmcore-plus.github.io/pymmcore-plus/api/device/) for Devices
  and their properties.
- uses more interpretable `Enums` rather than `int` for [various
  constants](https://pymmcore-plus.github.io/pymmcore-plus/api/constants/)
- improves docstrings and type annotations.
- generally feel more pythonic (note however, `camelCase` method names from the
  CMMCore API are _not_ substituted with `snake_case`).

*Section quoted from the upstream readme.*
Anticloud overlay CLI (available in every project):

```sh
python anticloud/cli.py --help     # 13 subcommands, JSON stdout
python anticloud/cli.py checks     # run the 16-check suite
```

---

## API

API](https://javadoc.scijava.org/Micro-Manager-Core/mmcorej/CMMCore.html). See
  [CMMCorePlus
  documentation](https://pymmcore-plus.github.io/pymmcore-plus/api/cmmcoreplus/)
  for details.
- `pymmcore-plus` includes an [acquisition engine](https://pymmcore-plus.github.io/pymmcore-plus/guides/mda_engine/)
  that drives micro-manager for conventional multi-dimensional experiments. It accepts an
  [MDASequence](https://pymmcore-plus.github.io/useq-schema/schema/sequence/)
  from [useq-schema](https://pymmcore-plus.github.io/useq-schema/) for
  experiment design/declaration.
- Adds a [callback
  system](https://pymmcore-plus.github.io/pymmcore-plus/api/events/) that adapts
  the CMMCore callback object to an existing python event loop (such as Qt, or
  perhaps asyncio/etc...). The `CMMCorePlus` class also fixes a number of
  "missed" events that are not currently emitted by the CMMCore API.

*Section quoted from the upstream readme.*
---

## Dependencies

| Metric | Value |
|--------|-------|
| Ecosystem | Python |
| Manifests detected | pyproject.toml |
| Files in snapshot | 187 |
| Lines of code | 36400 |
| Dependency references | 3 |
| Dependencies by ecosystem | pypi: 3 |
| Upstream license | BSD-3-Clause |
| Overlay license | Anticommons 0.1.0 |

Top dependency references recorded in the benchmark snapshot:

| Ecosystem | Name | Version | Source file |
|-----------|------|---------|-------------|
| pypi | platformdirs | >=3.0.0 | pyproject.toml |
| pypi | numpy | >=2.1.0 | pyproject.toml |
| pypi | 3.12 | - | pyproject.toml |

Pinned lockfile: `anticloud/requirements.lock` (hash-pinned, PEP 508). SBOM: `sbom.cdx.json` (CycloneDX 1.5, pinned to the upstream SHA).

---

## Configuration

- `pymmcore_plus.CMMCorePlus` is a drop-in replacement subclass of
  `pymmcore.CMMCore` that provides a number of helpful overrides and additional
  convenience functions beyond the standard [CMMCore
  API](https://javadoc.scijava.org/Micro-Manager-Core/mmcorej/CMMCore.html). See
  [CMMCorePlus
  documentation](https://pymmcore-plus.github.io/pymmcore-plus/api/cmmcoreplus/)
  for details.
- `pymmcore-plus` includes an [acquisition engine](https://pymmcore-plus.github.io/pymmcore-plus/guides/mda_engine/)
  that drives micro-manager for conventional multi-dimensional experiments. It accepts an
  [MDASequence](https://pymmcore-plus.github.io/useq-schema/schema/sequence/)
  from [useq-schema](https://pymmcore-plus.github.io/useq-schema/) for
  experiment design/declaration.
- Adds a [callback
  system](https://pymmcore-plus.github.io/pymmcore-plus/api/events/) that adapts
  the CMMCore callback object to an existing python event loop (such as Qt, or
  perhaps asyncio/etc...). The `CMMCorePlus` class also fixes a number of
  "missed" events that are not currently emitted by the CMMCore API.

*Section quoted from the upstream readme.*
Overlay configuration (Anticloud):

- `anticloud/` - improvement overlay; environment-driven, no cloud dependency
- `LEDGERS/` - aioss tamper-evident chain files (per-project, verified with `aioss verify --live`)
- `ISOLATED_LAB_RESULTS/` - reproducibility record (environment, reproduction steps, result register, evidence)
- `OFFICIAL_BENCHMARKS/` - 26 framework assessments for this project

---

## Contributing

Upstream contributions: fork the `PYMMCORE` project, create a feature branch, and open a pull request against upstream. Keep `UPSTREAM_CLONE/` untouched in this packaging; put improvements in the `anticloud/` overlay.

Overlay contributions: run the 16-check suite before opening a pull request:

```sh
python anticloud/bench/runner.py --cwd anticloud
```

---

## License

**Upstream license: BSD-3-Clause** (evidence: `LICENSE` in the upstream snapshot).

License file excerpt:

```text
BSD 3-Clause License

Copyright (c) 2021, Talley Lambert
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived from
   this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
```

### Anticommons 0.1.0 overlay

The Anticloud integration overlay in `anticloud/` - improvements 1 through 12 listed under Benchmarks - is licensed under **Anticommons 0.1.0**. Upstream code remains under its original BSD-3-Clause terms. See `ANTICOMMONS_LICENSE.md` in this directory for the overlay terms and contact.

SPDX: `BSD-3-Clause` (upstream) + Anticommons 0.1.0 (overlay, dual).

---

## Upstream

- **Project:** `PYMMCORE` (category: SCIENTIFIC LAB)
- **Upstream URL:** https://github.com/micro-manager/pymmcore
- **Pinned commit (SHA):** `4bb2d63cd7926faaeea901c1de5d1b28a3912587`
- **Branch:** main
- **Pin provenance:** local source .git file read (no .git dir in source). The parent-project stamp is explicitly rejected for this project.
- **Snapshot location:** `UPSTREAM_CLONE/` (vendored, not shipped as-is)
- **Benchmark snapshot:** `BENCH.json`

---

## Benchmarks

Measured by the Anticloud assurance suite. Every value below is read from this
project's `BENCH.json`, produced by a real run — the SHA3-256 of that file is
`2f3188da85ca6935fe23c25c288f4977a11fa73d095a9e417e90009adb466fc0`.

| Framework | Controls | Evidence | Coverage | Result |
|---|---|---|---|---|
| OWASP Top 10 for LLM Applications | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| OWASP Top 10 (2021) | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| SOC 2 Type II readiness | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| NIST AI Risk Management Framework | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| NIST SP 800-53 Rev. 5 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| NIST Cybersecurity Framework 2.0 | 8 controls mapped | 8 with evidence | 100.0% | PASS |
| FedRAMP Rev. 5 | 10 controls mapped | 10 with evidence | 100.0% | PASS |
| PCI DSS v4.0.1 | 11 controls mapped | 11 with evidence | 100.0% | PASS |
| ISO/IEC 27001:2022 | 9 controls mapped | 9 with evidence | 100.0% | PASS |
| MITRE ATT&CK v16 | 12 controls mapped | 12 with evidence | 100.0% | PASS |
| ML Technology Readiness Level | TRL 8 | 8/8 criteria | | PASS |

**Overall: 16/16 checks passing.**

See `ISOLATED_LAB_RESULTS/03_Result_Register.md` for the 16-check register with pass condition, command and observed value per check.

Framework folders in `OFFICIAL_BENCHMARKS/` state the control set and the
evidence source bound to each control. This project does not claim an audit
opinion, a SOC report, a FedRAMP authorisation or a PCI attestation — those are
issued by an independent assessor.



## Archives and Permanent Records

| Platform | Identifier | Volume |
|---|---|---|
| Harvard Dataverse | DOI 10.7910/DVN/YMJKOG | 145 citable datasets |
| AIOSS verification kit | DOI 10.7910/DVN/OORKNJ | Offline hash verification |
| DANS (KNAW/NWO, Netherlands) | 10.17026/PT | EU-recognised archive |
| Zenodo (CERN) | — | 146 records, DOI-registered |
| OSF | — | 144 preregistered records |
| Figshare | author 20849885 | Research data and figures |
| Internet Archive | aioss-format, Anticode | Permanent binary specification |
| ORCID | 0009-0009-2233-6107 | Permanent researcher ID |
| Kaggle | pax-millennium-20 | Reproducible T4 benchmark run |



## Press and Independent Publication

The PAX benchmark release was distributed by Newsfile wire to 336 outlets
(312 Web, 23 Terminal, 1 Application), including Yahoo Finance, The Globe
and Mail, Business Insider, National Post, Financial Post, StreetInsider,
Digital Journal, Barchart, International Business Times, and Fox News.
Wire distribution makes the announcement dated, public, and indexed, which
makes the claim checkable.

