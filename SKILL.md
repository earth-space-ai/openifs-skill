---
name: openifs
description: >
  Progressive-disclosure skill for OpenIFS, the ECMWF Integrated Forecast
  System released for research and education. Covers OpenIFS license
  scope (research/education only), bundle.yml layout, build system,
  experiment setup, and the documentation under docs/. NOT a substitute
  for the operational IFS; it's a frozen research-friendly snapshot.
version: 0.1.0-scaffold
tags:
  - earth-science
  - atmospheric-model
  - nwp
  - spectral
  - openifs
  - ifs
  - ecmwf
  - fortran
  - mpi
---

# OpenIFS Guide

> **OpenIFS** = the ECMWF Integrated Forecast System released for research and education.
> Maintainer: ECMWF
> Source: https://github.com/ecmwf-ifs/openifs
> License: see `LICENSE` in repo (research/education use)
> Docs: shipped under `docs/` (build options, env vars, run howto, test options)
> ECMWF Confluence: https://confluence.ecmwf.int/display/OIFS
> Skill author: Koutian Wu (ktwu01@gmail.com)
> Skill version: 0.1.0-scaffold

**What OpenIFS does:** Research-friendly snapshot of the ECMWF IFS atmospheric model, including the spectral dynamical core, semi-Lagrangian advection, the IFS physics package (radiation, convection, cloud, turbulence, surface), and a single-column model. Used for atmospheric process studies, education, idealized experiments, and as the atmospheric component of EC-Earth and AWI-CM.

**Important license + access note:** OpenIFS is **not fully open source**. The repo at `github.com/ecmwf-ifs/openifs` requires a signed ECMWF license and an active GitHub invitation; you cannot just `git clone` it as a stranger. The license restricts use to research and education and prohibits operational use or redistribution. Read `LICENSE` and the ECMWF terms before using or sharing.

**Who this skill is for:** Researchers and students using OpenIFS for atmospheric research, with appropriate ECMWF licensing.

---

## Quick Decision Tree

```
"What do I need?"
│
├─ 🆕 What is OpenIFS, what's the difference from operational IFS?
│  └─ Read: reference/overview.md
│
├─ 📜 License, am I allowed to use/redistribute this?
│  └─ Read: reference/license.md
│
├─ 🛠️ Build OpenIFS (see docs/oifs_build_options.md upstream)
│  └─ Read: reference/build.md
│
├─ 🌎 Set up an experiment (see docs/oifs_howto_run_experiments.md upstream)
│  └─ Read: reference/experiment-setup.md
│
├─ 🔧 Environment variables (see docs/oifs_env_vars.md upstream)
│  └─ Read: reference/env-vars.md
│
├─ ✅ Test infrastructure (see docs/oifs_test_options.md upstream)
│  └─ Read: reference/testing.md
│
└─ 🐛 Common build/run failures
   └─ Read: reference/debugging.md
```

---

## Repo Layout (verified from clone)

```
openifs/
├── arch/                                # Per-machine architecture configs
├── bundle.yml                           # ecbundle dependency manifest
├── docs/                                # Top-level docs (small, see Confluence for more)
│   ├── oifs_build_options.md
│   ├── oifs_env_vars.md
│   ├── oifs_howto_run_experiments.md
│   ├── oifs_howto_setup_central_source.md
│   └── oifs_test_options.md
├── ifs-source/                          # IFS source tree
├── ifs-test/                            # Tests
├── LICENSE                              # ECMWF research/education license
├── NOTICE
└── oifs-config.edit_me.sh               # Per-site config template
```

OpenIFS uses `ecbundle` (ECMWF's bundle system), `bundle.yml` lists the dependencies that need to be present in the source tree alongside `ifs-source/`.

---

## Critical Rules

1. **License is restrictive.** Research and education only. Do not redistribute build artifacts or use operationally without ECMWF agreement. Check current terms on ECMWF Confluence.
2. **`ecbundle` is the dependency tool.** `bundle.yml` lists what other ECMWF code (Atlas, FCKit, ECTrans, etc.) must be checked out alongside.
3. **Per-machine `arch/` configs** define toolchain, libraries, and flags. Adapt an existing one rather than starting from scratch.
4. **`oifs-config.edit_me.sh`** is a template, copy and edit for your site.
5. **The most authoritative how-to guides live on ECMWF Confluence**, not in this repo. The repo's `docs/` is a quick reference; depth lives upstream.
6. **OpenIFS is not the operational IFS.** Cycle / version may lag the operational system. Don't assume bug-for-bug compatibility.

---

## Reference Index

| File | Topic |
|---|---|
| reference/overview.md | OpenIFS vs operational IFS |
| reference/license.md | Use, redistribution, citation |
| reference/build.md | ecbundle, arch configs |
| reference/experiment-setup.md | Run an experiment |
| reference/env-vars.md | OIFS environment variables |
| reference/testing.md | Test infrastructure |
| reference/debugging.md | Common errors |

## Critical agent gotchas (Gemini-reviewed)

- **Two build eras coexist.** Cycle 43r3 and earlier use a `make`-based system with `arch/` files and `oifs-config.edit_me.sh`. Cycle 48r1+ uses `ecbundle` + CMake (`bundle.yml`). They are not compatible. Identify your cycle first.
- **`ecbundle` needs `ecbuild`** (ECMWF's CMake wrapper) to actually build. Not always preinstalled.
- **Climate / fix files and initial state files are required and external.** OpenIFS will crash at startup without topography/land-sea mask climate files and a GRIB initial state. These are multi-GB and downloaded separately from the source.
- **`fort.4` is the namelist file.** Massive Fortran namelist controlling resolution, time steps, physics. Editing this is unavoidable.
- **GRIB output requires `eccodes`** (ECMWF's GRIB library + CLI). Without it you cannot inspect or process model output.
- **Spectral dycore needs FFTW or Intel MKL DFTI.** Per-machine `arch/` files often need manual library paths on modern Linux distros.
- **Single-column model needs experiment-specific input data** (GABLS, GATE, etc.), not shipped with source.

## Status

Scaffold (v0.1.0-scaffold). Layout and license model verified against the cloned tree, with Gemini critique pass on 2026-05-09 to add access caveat, build-system disambiguation, and required-input notes. Operational depth being filled in. Always cross-check with ECMWF Confluence.
