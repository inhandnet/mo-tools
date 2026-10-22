# mo-tools

English | [简体中文](README.zh-CN.md)

Mo Studio and toolchain usage examples for InHand Mo series single-board computers.

This repository will hold Mo Studio, the desktop companion application for Mo boards, and worked examples that show how to use the Mo toolchain (compilers, debuggers, flashing and board bring-up utilities) from a development host.

Related repositories:

- [Mo62A](https://github.com/inhandnet/Mo62A) — board support package, OS image build and device-side runtime for the Mo 62A board.
- [mo-docs](https://github.com/inhandnet/mo-docs) — product documentation for the Mo series.

## Status

The directory layout, contribution rules and the CI and release pipelines are in place. `toolchain/` holds the pinned TI edgeai-tidl-tools baseline (`versions.json`) and the x86 host setup scripts; `board-test/` holds the Mo62A desktop board test tool migrated from the Mo62A repository. `studio/` is still a placeholder. No release has been published yet; nothing here is ready for production use until one is.

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

Every pull request must pass the `commit-message` and `ci` checks before it can be merged. Questions about using Mo boards belong in the [community forum](https://community.inhand.com); use GitHub issues for bugs and feature requests in this repository.

## Releases and tags

Releases are created by pushing an annotated tag that exactly matches `V<major>.<minor>.<patch>` or, for a release candidate, `V<major>.<minor>.<patch>-rc<n>`. The tag must point to a commit on `master`. The [release workflow](.github/workflows/release.yml) validates the tag, generates English and Chinese changelogs from the bilingual commit messages, packages a source archive with an SPDX SBOM and SHA-256 checksums, and publishes a GitHub Release titled with the tag name. A release candidate is published as a prerelease.

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
