# Source and license of this directory

These three files are copied unchanged in behaviour from the Mo62A warehouse
zone-occupancy tutorial package published by the `mo-docs` repository
(`static/downloads/ai/zone-demo/`, archive `mo62a-zone-demo.tar.gz`):

| File | Purpose |
| --- | --- |
| `setup_host.sh` | Creates an isolated x86 Python 3.10 environment, clones the pinned TI source, installs the pinned TI wheel and downloads/checks the AM62A compiler archive. |
| `activate_host.sh` | Sourced in every new shell; activates the environment and exports `SOC`, `TIDL_TOOLS_PATH` and the library search path. |
| `requirements-host.txt` | Pinned host packages, including the TI ONNX Runtime 1.23.0 wheel with its SHA-256. |

The only edit is a `# shellcheck source=/dev/null` directive in
`activate_host.sh` so that the repository's shellcheck job accepts the dynamic
`source` of the virtual environment.

The tutorial package is licensed under Creative Commons Attribution-ShareAlike
4.0 International; see the accompanying `LICENSE`. That license applies to the
files in this directory and differs from the Apache-2.0 license of the rest of
this repository.
