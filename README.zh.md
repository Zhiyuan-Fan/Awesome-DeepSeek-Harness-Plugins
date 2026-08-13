# Awesome DeepSeek Harness Plugins [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[English](README.md) | 简体中文

> 面向 [DeepSeek Harness（DSH）](https://github.com/deepseek-ai/deepseek-harness) 的插件、插件起步项目、工具与一手资料精选索引。

DeepSeek Harness 是 DeepSeek AI 开源的插件优先 Agent Harness：模型、工具、技能、会话、沙箱、文件系统、循环、编排和界面都可以作为插件组合。完整英文目录见 [README.md](README.md)；两个入口维护同一套严格收录标准。

> **开发者预览版**：DSH 迭代很快，可能出现破坏性变更。本仓库是独立社区整理，不代表 DeepSeek AI 或 walkinglabs 的背书。安装第三方插件前请审查源码，并固定 DSH 版本或 commit。

## 快速教程：安装 DSH 并写出第一个插件

### 1. 安装并运行 DeepSeek Harness

先安装当前版本的 [Node.js](https://nodejs.org/)，然后执行：

```sh
npx @deepseek-ai/dsh web
```

打开 `http://127.0.0.1:3080`。在 **Settings → Models** 中填写 DeepSeek API Key；再选择一个工作区，即可开始会话。更多步骤见官方 [Web UI 使用指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/guide/index.md)。

### 2. 从源码创建最小插件

当前官方插件开发流程需要先获得 DSH 源码：

```sh
git clone https://github.com/deepseek-ai/deepseek-harness.git
cd deepseek-harness
pnpm install
pnpm run build
mkdir -p scratch-plugin/src
```

创建 `scratch-plugin/src/hello-plugin.ts`：

```ts
import type { Context } from '@deepseek-ai/cordis'

export const name = 'hello-plugin'

export function apply(ctx: Context) {
  console.log('[hello-plugin] loaded')
}
```

再创建 `scratch-plugin/cordis.yml`。把下方路径替换成在 DSH 源码目录执行 `pwd` 后得到的绝对路径：

```yaml
- insert:
    - id: hello
      name: '/absolute/path/to/deepseek-harness/scratch-plugin/src/hello-plugin.ts'
```

使用这个 overlay 启动：

```sh
pnpm dsh web --patch ./scratch-plugin/cordis.yml
```

DSH 启动后，终端应显示 `[hello-plugin] loaded`。这就是最小的 DSH 插件：导出 `apply(ctx)`，并通过 Cordis 上下文注册能力。若要添加 Agent 可调用的工具，请声明 `export const inject = ['tools']`，再通过官方 DSH 工具 API 注册。完整且随版本更新的写法请查看官方[第一个插件教程](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/develop/basic/index.md)和 [Tool 插件教程](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/user/develop/basic/tool.md)。

## 快速开始：官方 DSH 资料

- [DeepSeek Harness 官方源码](https://github.com/deepseek-ai/deepseek-harness) - 版本、issue 与兼容性的唯一首要依据。
- [官方文档指南](https://deepseek-harness.github.io/deepseek-harness/guide) - DSH 官方文档入口。
- [运行 DSH](https://github.com/deepseek-ai/deepseek-harness#run) - 通过 `npx @deepseek-ai/dsh web` 启动本地 Web UI。
- [架构](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/architecture.md) - 了解插件优先运行时的结构。
- [能力接缝](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/capability-seams.md) - 官方定义的扩展边界。
- [Cordis 入门](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/cordis-primer.md) - DSH 所依赖的可组合框架。
- [开发指南](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/development.md) - 从源码构建及贡献官方项目。
- [防御性模式](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/defensive-patterns.md) - 更安全地扩展 DSH 的官方建议。
- [测试](https://github.com/deepseek-ai/deepseek-harness/blob/master/docs/testing.md) - 官方测试方式。
- [官方示例](https://github.com/deepseek-ai/deepseek-harness/tree/master/examples) - Headless、JSON-RPC、MCP Memory、定时 Web、Cordis 示例。

## 如何找插件

- [GitHub `dsh-plugin` topic](https://github.com/topics/dsh-plugin) - 官方建议用于 DSH 插件发现的 topic；**仅用于发现，不构成收录证据**。
- [插件注册表](https://github.com/vlln/plugin-registry) - Repository-plugin 控制台和 `make-dsh-plugin` 开发指导。
- [插件工作坊](https://github.com/omdsh-dev/dsh-hub-workshop) - 社区插件市场和注册表实践。

## 收录保证

我们不因为名称、topic 或 README 自称 DSH 插件就收录。每个新插件都必须通过[源码级收录规范](docs/INCLUSION_POLICY.md)：存在真实 DSH 清单/插件包，或能在官方 DSH 扩展接缝中验证的实现。每日检索只加入通过验证的新项目；没有合格候选就不修改仓库。

## 完整目录 / Full index

[英文完整目录](README.md) 按下列分类维护项目的英文说明；每一类均只收录符合上述 DSH 规则的项目：

- 生产力与 Agent 工作流 / Productivity & Agent Workflow
- 上下文、记忆与可观测性 / Context, Memory & Observability
- 工具、集成与自动化 / Tools, Integrations & Automation
- 浏览器、计算机操作与远程执行 / Browser, Computer Use & Remote Execution
- 终端与 Web 界面 / Interfaces & Web UI
- 开发工具 / Developer Tooling
- 实用工具 / Utilities
- 创意与个性化 / Creative & Personal
- 启动器与客户端（不是插件）/ Launchers & Clients (not plugins)
- 生态目录（不是插件）/ Ecosystem Indexes (not plugins)

## 贡献

请阅读[中文贡献指南](CONTRIBUTING.zh.md)或[English guide](CONTRIBUTING.md)。提交条目时，请提供源码中 DSH 集成的具体证据。

## 许可证

本仓库采用 [CC0 1.0](LICENSE)。
