# VMark · 中英双语说明 / Bilingual README

让人与 AI 在同一份本地文档上协作的纯文本工作空间。

A plain-text workspace where people and AI collaborate on the same local documents.

本文依据当前检出的项目源码和随附文档编写，适合初次接触项目的用户。版本与要求以本仓库的 `package.json`、`src-tauri/Cargo.toml` 和原始 [README](README.md) 为准。

This guide is based on the checked-out source and bundled documentation. For authoritative version and dependency requirements, see `package.json`, `src-tauri/Cargo.toml`, and the original [README](README.md).

## 1. 项目介绍 / Project overview

VMark 是一个以本地文件为中心的桌面编辑器，可用于写笔记、整理资料、编辑 Markdown 和查看结构化文档。Markdown 是一种使用简单文字标记表达标题、列表和链接的文档格式，例如 `# 标题`。

VMark is a desktop editor centered on local files. Use it to write notes, organize information, edit Markdown, and inspect structured documents. Markdown uses simple text markers for headings, lists, and links, such as `# Heading`.

应用基于 Tauri、Rust、React 和 TypeScript 构建。Tauri 将网页界面与桌面能力结合，因此 VMark 应通过桌面窗口使用，而不是作为普通网站运行。macOS 是主要支持平台；Windows 和 Linux 的支持以项目说明为准。

The app uses Tauri, Rust, React, and TypeScript. Tauri combines a web-based interface with native desktop capabilities, so VMark is intended to run in a desktop window rather than as a standalone website. macOS is the primary platform; consult the project documentation for Windows and Linux support.

日常文档编辑围绕本地文件进行。可选的 AI 集成需要另外配置；是否联网、使用什么服务及是否产生费用，取决于所连接的 AI 工具和服务。

Everyday editing centers on local files. Optional AI integrations require separate configuration; network access, service usage, and any associated costs depend on the connected AI tools and providers.

## 2. 功能列表 / Features

| 功能 / Feature | 中文说明 | English description |
| --- | --- | --- |
| Markdown 编辑 / Editing | 支持所见即所得编辑、源码预览和源码模式。所见即所得就是直接看到排版效果。 | Visual editing, source peek, and source mode. Visual editing shows the formatted result as you work. |
| 多格式支持 / Multiple formats | 支持 Markdown、JSON/JSONL、YAML、TOML、Mermaid、SVG、HTML 和纯文本。 | Work with Markdown, JSON/JSONL, YAML, TOML, Mermaid, SVG, HTML, and plain text. |
| 代码查看 / Code viewing | 代码文件支持语法高亮，并可切换为就地编辑。 | View code with syntax highlighting and switch to in-place editing. |
| 结构化预览 / Structured previews | 部分配置文件可显示工作流图或依赖树；通用结构化文件可显示树状视图。 | Supported configuration files receive workflow or dependency views; generic structured files have navigable tree views. |
| 工作区 / Workspaces | 打开文件夹，集中管理项目文档。 | Open a folder to work with related project documents. |
| 多光标 / Multiple cursors | 同时编辑多处文字，提高重复修改效率。 | Edit multiple text locations at once. |
| 中日韩排版 / CJK formatting | 提供面向中文、日文和韩文的排版规则。 | Formatting rules designed for Chinese, Japanese, and Korean text. |
| 外观与语言 / Appearance and languages | 支持多种界面语言和主题，主题可用范围因平台而异。 | Multiple interface languages and themes, with theme availability varying by platform. |
| 快捷键 / Shortcuts | 可在设置中调整快捷键。 | Customize keyboard shortcuts in settings. |
| AI 集成 / AI integration | 通过 MCP 连接兼容助手，支持围绕文档的协作。MCP 是工具与 AI 助手之间的一种通信方式。 | Connect compatible assistants through MCP, a protocol for communication between tools and AI assistants. |

## 3. 安装步骤 / Installation

### 3.1 直接使用发布版 / Install a release

只想使用软件时，下载适合电脑系统的安装包最简单。请前往项目的 [Releases 页面](https://github.com/xiaolai/vmark/releases)。

For everyday use, the simplest route is a prebuilt installer for your operating system from the project's [Releases page](https://github.com/xiaolai/vmark/releases).

- Apple Silicon Mac（M 系列芯片）选择 `aarch64.dmg`；Intel Mac 选择 `x64.dmg`。打开 DMG 后按安装窗口提示操作。
- On Apple Silicon Macs, choose `aarch64.dmg`; on Intel Macs, choose `x64.dmg`. Open the DMG and follow the installer window instructions.

### 3.2 从源码运行 / Run from source

源码是程序的原始文件；编译是把这些文件转换成可以运行的应用。只有需要学习、调试或修改项目时，才需要走这条路线。

Source code consists of the original program files; compilation turns them into a runnable application. Use this route when you want to study, debug, or modify the project.

**准备环境 / Prerequisites**

| 工具 / Tool | 要求 / Requirement |
| --- | --- |
| Git | 用于下载和管理代码 / For cloning and version control |
| Node.js | 22 或更高 / 22 or newer |
| pnpm | 10.x；本检出版本固定为 10.33.0 / 10.x; this checkout pins 10.33.0 |
| Rust | 稳定版，至少 1.89；建议使用当前稳定版以满足依赖要求 / Stable, at least 1.89; use current stable to satisfy dependency requirements |
| 系统开发工具 / System tooling | 安装对应平台的 [Tauri v2 prerequisites](https://v2.tauri.app/start/prerequisites/)，macOS 需要 Apple 开发工具 / Install the platform prerequisites; macOS requires Apple development tools |

先安装上面的工具，确认终端能识别 `git`、`node`、`pnpm` 和 `cargo`，再执行下列命令。已有本地项目时，直接进入该目录，不必重复克隆。

Install these tools and confirm that `git`, `node`, `pnpm`, and `cargo` are available in your terminal before continuing. If you already have a clone, enter that directory instead of cloning again.

```bash
# 下载项目 / Clone the repository
git clone https://github.com/xiaolai/vmark.git
cd vmark

# 按锁定版本安装依赖 / Install locked dependencies
pnpm install --frozen-lockfile

# 首次运行前生成必需的辅助程序 / Build the required sidecar before first launch
pnpm --dir server/mcp build:sidecar

# 启动桌面开发版 / Launch the desktop development app
pnpm tauri dev
```

辅助程序（sidecar）是主应用随附的小程序。新克隆的仓库没有它的编译结果，因此不要跳过构建步骤。首次安装与编译需要联网、一定的磁盘空间和等待时间。

The sidecar is a companion executable bundled with the app. A fresh clone does not contain its compiled output, so do not skip the build step. Initial installation and compilation require network access, disk space, and time.

安装依赖时，项目的 `prepare` 脚本会设置仓库本地 Git hooks 等配置；已有自定义配置时应先备份。开发版使用独立应用标识 `app.vmark.dev`，设置和会话与正式版分开。

During installation, the project's `prepare` script configures repository-local Git hooks and related settings; back up any existing custom configuration first. Development uses the separate identifier `app.vmark.dev`, with settings and sessions separate from the release app.

### 3.3 当前电脑的快捷启动 / Shortcut on this computer

本地环境另有一个启动文件，位于项目文件夹的上一级：`启动VMark开发版.command`。可在访达中双击它，或在本项目目录运行：

This local setup also has a launcher one directory above the project: `启动VMark开发版.command`. Double-click it in Finder, or run this from the project directory:

```bash
../启动VMark开发版.command
```

这个文件使用相邻 `vmark-local-tools` 目录中的工具，不需要改动系统 PATH。它只属于当前电脑的配套环境，不是克隆上游仓库后自动存在的文件。使用时保持终端运行；停止前先保存文档，再在启动终端按 `Control + C`。

The launcher uses tools in the adjacent `vmark-local-tools` directory without changing the system PATH. It is specific to this local setup and is not included in a fresh upstream clone. Keep its terminal running while using the app. To stop, save your documents and press `Control + C` in that terminal.

## 4. 使用说明 / Usage

### 创建和保存文档 / Create and save a document

1. 启动 VMark，在欢迎页点击“新建文件”。 / Launch VMark and choose **New File** on the welcome screen.
2. 输入标题、正文或列表。 / Write a heading, paragraph, or list.
3. 使用“文件”菜单中的保存功能，选择位置并保存为 `.md` 文件。 / Use **Save** in the File menu, choose a location, and save as a `.md` file.
4. 通过“打开文件”再次打开，确认内容已保存。 / Reopen it using **Open File** to confirm the content was saved.

可试着输入以下内容 / Try this content:

```markdown
# 我的第一篇笔记 / My first note

今天开始使用 VMark。 / Today I started using VMark.

- 记录想法 / Capture ideas
- 整理资料 / Organize information
- 制定计划 / Make a plan
```

### 打开文件或工作区 / Open files or a workspace

- 点击“打开文件”，选择已有文档；也可将支持的文件拖入窗口。
- Choose **Open File** and select a document, or drag a supported file into the window.
- 点击“打开工作区”，选择存放相关文档的文件夹。
- Choose **Open Workspace** and select a folder containing related documents.

### 编辑模式与外观 / Editing modes and appearance

Markdown 支持所见即所得、源码预览（默认 `F5`）和源码模式（默认 `F6`）。部分 Mac 键盘需同时按 `Fn`；若已自定义快捷键，请以设置中的绑定为准。主题、字体和快捷键也可在设置中调整。

Markdown supports visual editing, source peek (`F5` by default), and source mode (`F6` by default). Some Mac keyboards require `Fn`; use the bindings shown in settings if shortcuts have been customized. Themes, fonts, and shortcuts can also be adjusted in settings.

### 可选 AI 集成 / Optional AI integration

打开“设置 → 集成”，按照兼容助手的说明配置连接。基础编辑不需要先连接 AI。详情见 [MCP 设置指南](https://vmark.app/guide/mcp-setup)。

Open **Settings → Integrations** and follow the instructions for your compatible assistant. Basic editing does not require an AI connection. See the [MCP setup guide](https://vmark.app/guide/mcp-setup).

### 本地访问地址 / Local development URL

开发界面服务默认使用 `http://localhost:1420`。它是桌面应用加载界面的地址，不是功能完整的独立网站。直接用普通浏览器打开可能显示空白或报错；请使用 `pnpm tauri dev` 启动的桌面窗口。

The frontend development service defaults to `http://localhost:1420`. This is the interface URL used by the desktop app, not a fully functional standalone website. An ordinary browser may show a blank page or errors; use the desktop window launched by `pnpm tauri dev`.

## 5. 常见问题 / Troubleshooting

| 情况 / Symptom | 处理方法 / What to do |
| --- | --- |
| 找不到 pnpm 或 cargo / Command not found | 检查工具安装；当前电脑可使用上述快捷启动文件。 / Check tool installation; on this computer, use the local launcher. |
| pnpm 版本不兼容 / Unsupported pnpm | 使用项目要求的 10.x，不要直接换成 11 或更高版本。 / Use the required 10.x major version. |
| 提示缺少 sidecar / Missing sidecar | 在项目目录执行 `pnpm --dir server/mcp build:sidecar`。 / Run the sidecar build command from the project root. |
| 下载失败 / Download failure | 检查网络与完整错误信息，区分网络问题和执行环境的权限限制。 / Inspect network connectivity and the full error; distinguish network issues from execution restrictions. |
| 1420 端口被占用 / Port 1420 in use | 检查是否已启动一份开发服务，避免重复运行。 / Check whether a development instance is already running. |
| 编译空间不足 / Insufficient disk space | 先检查硬盘剩余空间，保留文档和备份后再规划清理。 / Check available storage and preserve documents and backups before planning cleanup. |

## 6. 项目资料 / Project resources

- [上游仓库 / Upstream repository](https://github.com/xiaolai/vmark)
- [原始说明 / Original README](README.md)
- [贡献指南 / Contribution guide](CONTRIBUTING.md)
- [安全说明 / Security policy](SECURITY.md)
- [ISC 许可证 / ISC license](LICENSE)

根据本检出版本的贡献指南，上游接受问题报告与功能建议（Issues），不合并外部 Pull Requests。提交反馈前请阅读贡献指南。

According to the contribution guide in this checkout, upstream accepts bug reports and feature requests through Issues and does not merge external pull requests. Read the contribution guide before submitting feedback.
