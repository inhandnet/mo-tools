# mo-tools

English | [简体中文](README.zh-CN.md)

Mo Studio and toolchain usage examples for InHand Mo series single-board computers.

This repository will hold Mo Studio, the desktop companion application for Mo boards, and worked examples that show how to use the Mo toolchain (compilers, debuggers, flashing and board bring-up utilities) from a development host.

Related repositories:

- [Mo62A](https://github.com/inhandnet/Mo62A) — board support package, OS image build and device-side runtime for the Mo 62A board.
- [mo-docs](https://github.com/inhandnet/mo-docs) — product documentation for the Mo series.

## Status

The directory layout, contribution rules and the CI and release pipelines are in place. `toolchain/` holds the pinned TI edgeai-tidl-tools baseline (`versions.json`) and the x86 host setup scripts; `board-test/` holds the Mo62A desktop board test tool migrated from the Mo62A repository. `studio/` is still a placeholder. Published archives are listed under GitHub Releases; their existence does not establish hardware or production qualification.

## Repository layout

| Path | Purpose |
| --- | --- |
| `toolchain/` | Pinned TI toolchain versions, official download links and host setup scripts. |
| `board-test/` | Mo62A board test tool (PySide6 GUI over SSH, HTML reports). |
| `studio/` | Mo Studio (placeholder). |
| `scripts/` | Repository maintenance scripts (commit message check, changelog generation). |
| `.githooks/` | Git hooks that run the commit message check locally. |
| `.github/` | Issue forms, pull request template and GitHub Actions workflows. |
| `release-notes/` | Changelog baseline used by the release workflow. |

## Contributing

Contributions are welcome through pull requests to `master`. Read [CONTRIBUTING.md](CONTRIBUTING.md) for the commit message convention, the pull request process and how to enable the local Git hooks:

```bash
git config core.hooksPath .githooks
```

Every pull request must pass the `commit-message` and `ci` checks before it can be merged. Use GitHub issues for bugs, reproducible problems and feature requests in this repository.

## Releases and tags

New releases use annotated ordinary `V<major>.<minor>.<patch>` tags on checked `master` commits. Only developer publishes website release candidates. The release workflow validates catalogs, packages source with SPDX SBOM, records the source commit and catalog hashes in `release.json`, writes SHA-256 checksums, then publishes a complete GitHub Release. Historical RCs remain unchanged. Changelog headings are bilingual; entries retain their English commit summaries.

```bash
git switch master
git pull --ff-only
git tag -a V1.0.0 -m "V1.0.0"
git push origin V1.0.0
```

## Security

Do not report security vulnerabilities in public issues. Follow [SECURITY.md](SECURITY.md).

## License

This repository is licensed under the terms in [LICENSE](LICENSE). Third-party content added later keeps its own license, stated next to the content.

## Unified website integration

`toolchain/versions.json` owns the selected TI toolchain versions and official download references. It includes the documented MCU+ SDK / Arm Clang / SysConfig combination; Linux/A53 cross-compilation remains explicitly unverified. SDK installers stay with TI. Developer reads a pinned source revision, validates the combined data, and renders the website; this repository has no documentation-site frontend or website deployment.

Run `node scripts/check-catalog.mjs` and `node --test tests/*.test.mjs` with Node 22. `validation/` is exported from a committed developer contract and checked by hash; do not edit it locally. For integrated preview, run developer's `npm run preview -- --source mo-tools=/path/to/mo-tools`.
