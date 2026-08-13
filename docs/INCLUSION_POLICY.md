# DSH Inclusion Policy / DSH 收录规范

English | [简体中文](#简体中文)

## What belongs here

A project belongs in a plugin category only when its repository provides **source-level evidence** that it extends the official [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) runtime.

At least one of the following must be true:

1. The repository contains an installable DSH repository-plugin manifest, such as `.dsh-plugin/manifest.json`, `.dsh-plugin/package.json`, or a current equivalent documented by DSH.
2. The repository contains a DSH plugin package (for example `dsh.plugin.json` plus a package entry) whose source registers or consumes a documented DSH/Cordis extension seam.
3. It is an official DSH package, example, or documentation page in `deepseek-ai/deepseek-harness`.
4. It is a client, launcher, or development resource with explicit, inspectable DSH integration. Such entries are placed outside the plugin categories and labelled accordingly.

## What does not qualify

- A `dsh-plugin` GitHub topic, `dsh-` name, or README sentence alone.
- A generic DeepSeek model adapter, an unrelated agent tool, a fork/mirror, or a directory of links.
- A repository that cannot be inspected, has no source, or whose claimed DSH integration cannot be found.

## Daily discovery procedure

1. Search public GitHub repositories created or updated in the past 48 hours for `dsh-plugin`, `DeepSeek Harness`, and DSH manifest filenames.
2. Exclude repositories already listed, mirrors, and index-only repositories.
3. Inspect the tree and manifest/package files; confirm the DSH extension seam against the official source/docs.
4. Perform static security triage before inclusion: inspect install/build scripts, dependencies and lockfiles, plugin entrypoints, workflows, and network/process/file-system/credential operations. Reject unresolved risks such as secret exfiltration, opaque payloads, unsafe remote-code execution, approval/sandbox bypasses, or suspicious credential collection. Never execute candidate code or run its install/build scripts.
5. Add only candidates that pass both DSH verification and this basic security triage, with a neutral bilingual description and a compatibility note when supplied.
6. Commit and push only when there is a real change; otherwise leave the repository untouched.

This is static security triage, **not** a complete malware review, reliability certification, or endorsement.

## 简体中文

### 什么可以收录

只有当仓库能提供**源码级证据**，证明它扩展了官方 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 运行时，项目才能进入插件分类。

至少满足以下一项：

1. 仓库含有可安装的 DSH repository-plugin 清单，例如 `.dsh-plugin/manifest.json`、`.dsh-plugin/package.json`，或官方文档规定的当前等价格式。
2. 仓库含有 DSH 插件包（例如 `dsh.plugin.json` 与对应的 package 入口），且源码注册或使用了已文档化的 DSH/Cordis 扩展接缝。
3. 它是 `deepseek-ai/deepseek-harness` 中的官方包、示例或文档。
4. 它是明确可检查 DSH 集成的客户端、启动器或开发资源；这类项目必须置于“非插件”分类并标明身份。

### 不可作为收录依据

- 只有 `dsh-plugin` GitHub topic、`dsh-` 命名，或 README 的单方面描述。
- 通用 DeepSeek 模型适配器、无关 Agent 工具、fork/mirror，或仅链接目录。
- 无法检查源码、没有源码，或找不到所声称 DSH 集成的项目。

### 每日发现流程

1. 搜索过去 48 小时新建或更新的公开 GitHub 仓库：`dsh-plugin`、`DeepSeek Harness` 与 DSH 清单文件名。
2. 排除已收录项目、镜像与纯目录仓库。
3. 检查文件树及清单/package，按官方源码和文档确认 DSH 扩展接缝。
4. 收录前进行静态安全初筛：检查安装/构建脚本、依赖及 lockfile、插件入口、工作流，以及网络/进程/文件/凭据操作。若发现密钥外传、混淆 payload、不安全的远程代码执行、绕过审批/沙箱或可疑凭据收集等未解决风险，直接拒绝；绝不执行候选代码，也不运行其安装或构建脚本。
5. 只有同时通过 DSH 验证与基础安全初筛的条目才会加入；使用中英双语中性描述，若项目提供则写明兼容版本。
6. 仅有实际变更时才提交和推送；没有合格候选则不改仓库。

这属于静态安全初筛，**不代表**完整恶意代码审计、稳定性认证或官方背书。
