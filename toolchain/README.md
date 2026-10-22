# Toolchain

English-first. Machine-readable pins live in [`versions.json`](versions.json).

## Policy

Mo boards use TI's current AI toolchain as published by TI. This repository
does not wrap, repackage or mirror it. Every download link below points to the
official TI location; the only files kept here are the pinned versions and the
host environment scripts that reproduce the tested setup.

## Pinned baseline (Mo62A, image V1.1.0)

| Item | Pinned value |
| --- | --- |
| TI source repository | [TexasInstruments/edgeai-tidl-tools](https://github.com/TexasInstruments/edgeai-tidl-tools), tag `11_02_17_00`, commit `d2be7203e5680298d7f54bcbd38e299d1bc22bfd` |
| AM62A compiler archive | [`tidl_tools.tar.gz`](https://software-dl.ti.com/jacinto7/esd/tidl-tools/11_02_17_00/TIDL_TOOLS/AM62A/tidl_tools.tar.gz); `version.txt` reports `BRANCH=REL.TIDL.11.02.17.00` |
| Host | x86_64, Python 3.10 in an isolated virtual environment, TI ONNX Runtime 1.23.0 wheel |
| AM62A SDK compatibility baseline | 11.01.07.05 (`11_02_17_00` is listed by TI as a backward-compatible patch for it) |
| Target firmware and libraries | AM62A `edgeai/11_1`: [firmware.tar.gz](https://software-dl.ti.com/jacinto7/esd/tidl-tools/11_02_17_00/FIRMWARES/AM62A/edgeai/11_1/firmware.tar.gz), [tidl_lib.tar.gz](https://software-dl.ti.com/jacinto7/esd/tidl-tools/11_02_17_00/FIRMWARES/AM62A/edgeai/11_1/tidl_lib.tar.gz) |
| TI references | [SDK compatibility table](https://github.com/TexasInstruments/edgeai-tidl-tools/blob/11_02_17_00/docs/sdk_version_compatibility_table.md), [target update script](https://github.com/TexasInstruments/edgeai-tidl-tools/blob/11_02_17_00/scripts/setup/update_target.sh), [Docker reference environment](https://github.com/TexasInstruments/edgeai-tidl-tools/blob/11_02_17_00/scripts/docker/README.md) |

These values come from the measured
[Mo62A version map](https://github.com/inhandnet/mo-docs/blob/master/docs/mo-62a/resource-download/version-map.mdx)
and the
[toolchain setup page](https://github.com/inhandnet/mo-docs/blob/master/docs/mo-62a/application-development/ai/toolchain.mdx)
in `mo-docs`. They describe the V1.1.0 development installation that was
audited; they are not a manifest for every later image.

## One tested combination

Treat the x86 compiler, the model graph, the compiled artifacts, the target
runtime and provider libraries and the C7x firmware as one deployment set.
Updating a single component can break loading or inference even when every
package imports successfully. The board's own Python (3.13.5 on V1.1.0),
NumPy and ONNX Runtime differ from the host environment on purpose: do not
install the host requirements on the board, and do not run TI's target
updater on Mo OS without reviewing what it replaces.

## Host setup

[`host-setup/`](host-setup/) contains the scripts used by the Mo62A tutorials:

```bash
cd host-setup
bash setup_host.sh ./host          # clones TI source, creates venv, downloads compiler
source ./activate_host.sh ./host   # in every new shell
python -m pip check
```

`setup_host.sh` refuses to reuse an existing `host` directory, does not use
sudo and does not touch the board. It verifies the TI source commit, the
compiler archive SHA-256 and the compiler `version.txt` before finishing.
Read the scripts before running downloaded code. Their origin and license are
described in [`host-setup/SOURCE.md`](host-setup/SOURCE.md).

## Tracking a newer TI release

Keep the pinned tag for day-to-day work. Evaluate a new TI release in a
separate host directory against its AM62A compatibility table, the required
target updates and regressions, then update `versions.json` together with the
firmware and runtime change on the board image. A version-number match alone
is not evidence that a graph compiles or runs.
