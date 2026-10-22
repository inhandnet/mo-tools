# mo-tools

[English](README.md) | 简体中文

InHand Mo 系列单板计算机的 Mo Studio 与工具链使用示例。

相关仓库：[Mo62A](https://github.com/inhandnet/Mo62A)（Mo 62A 板级支持与系统镜像）、[mo-docs](https://github.com/inhandnet/mo-docs)（产品文档）。

## 状态

目录结构、贡献规范以及 CI 与发布流水线已就绪。`toolchain/` 存放钉定的 TI edgeai-tidl-tools 版本（`versions.json`）与 x86 主机环境脚本；`board-test/` 存放从 Mo62A 仓库迁入的整机测试工具；`studio/` 仍为占位。尚未发布任何版本，发布前的内容不用于生产。

## 目录结构

- `toolchain/` — 钉定的 TI 工具链版本、官方下载链接与主机环境脚本
- `board-test/` — Mo62A 整机测试工具（PySide6 图形界面，经 SSH 执行，输出 HTML 报告）
- `studio/` — Mo Studio（占位）
- `scripts/` — 仓库维护脚本（提交信息检查、变更记录生成）
- `.githooks/` — 本地提交信息检查钩子
- `.github/` — Issue 表单、PR 模板与 GitHub Actions 工作流

## 参与贡献

通过 PR 提交到 `master`。提交信息规范、PR 流程与本地钩子启用方法见 [CONTRIBUTING.md](CONTRIBUTING.md)（`git config core.hooksPath .githooks`）。PR 必须通过 `commit-message` 与 `ci` 两项检查后才能合并。产品使用问题请到[社区论坛](https://community.inhand.com)提问。

## 发布与标签

推送形如 `V<major>.<minor>.<patch>` 或 `V<major>.<minor>.<patch>-rc<n>` 的附注标签即触发发布工作流：校验标签、根据双语提交信息生成中英文变更记录、打包源码归档（含 SPDX SBOM 与 SHA-256 校验和）并创建以标签命名的 GitHub Release；`-rc` 标签发布为预发布版本。

## 安全

请勿在公开 Issue 中报告安全漏洞，见 [SECURITY.md](SECURITY.md)。

## 许可证

见 [LICENSE](LICENSE)。
