# OpenIFS Skill

Progressive-disclosure skill for [OpenIFS](https://github.com/ecmwf-ifs/openifs), the ECMWF Integrated Forecast System released for research and education.

> **Skill author:** Koutian Wu (ktwu01@gmail.com)
> **Skill version:** 0.1.0-scaffold

> ⚠️ **Disclaimer — please read before using this skill.**
> This skill is **not a gold-standard reference**. It is a helper that lowers
> the barrier for new users to **get their hands dirty** with the model. AI
> agents (and the humans drafting this material) make mistakes; commands, file
> paths, namelist options, and physics explanations here can be wrong,
> incomplete, or out of date. **Always cross-check with the official model
> documentation, the source code, and a human expert before trusting any
> output for research, publication, or operational use.**

## What This Is

A guide to OpenIFS for atmospheric research and education. Covers license scope (research/education only), the ecbundle dependency manifest, per-machine `arch/` configs, experiment setup, and pointers to ECMWF Confluence for the deep operational docs.

## Status

Scaffold. Layout and license model verified against the cloned `ecmwf-ifs/openifs` tree. The most authoritative how-to documentation lives on ECMWF Confluence; this skill is a reference and routing layer.

## Acknowledgments

**Gold-standard references for OpenIFS** (use these to cross-check anything in this skill):
- ecmwf-ifs/openifs repository: https://github.com/ecmwf-ifs/openifs
- OpenIFS documentation on ECMWF Confluence: https://confluence.ecmwf.int/display/OIFS
- OpenIFS user support: https://confluence.ecmwf.int/display/OIFS/OpenIFS+Home
- ECMWF IFS documentation: https://www.ecmwf.int/en/publications/ifs-documentation

This scaffold exists only because of the work of other people, and any value
it has is borrowed from theirs.

- **ECMWF** for developing and maintaining
  [ecmwf-ifs/openifs](https://github.com/ecmwf-ifs/openifs), the research /
  education licensed snapshot of the Integrated Forecast System, plus the
  ecbundle dependency manifest and `arch/` configuration scaffolding this
  skill teaches.
- The **OpenIFS user community** at universities and national met services
  whose research and feedback shape what ECMWF releases publicly.
- The maintainers of **ECMWF Confluence** documentation, which is the
  authoritative how-to source this skill routes users toward.
- **Zesen Huang** for [laps-skill](https://github.com/huangzesen/laps-skill),
  the progressive-disclosure layout this repo borrows.

Any errors, oversimplifications, or out-of-date claims in this skill are the
skill author's responsibility, not the upstream community's. This is a
scaffold; operational depth is being filled in iteratively. Respect the
OpenIFS research/education licence terms when using anything you learn here.

## License

MIT (skill content). OpenIFS is **not** open source, its `LICENSE` restricts to research and education, with no operational use or redistribution. Read upstream terms.
