# Changelog

All notable changes to CDF will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.1] - 2026-06-08

First publicly tagged release of CDF (Agent 开发工作站).

### Highlights

CDF is an offline-first desktop Agent development workstation. You talk to a
Master Agent in natural language; the Master Agent plans tasks, calls tools,
and orchestrates workflows — all on your machine, all under your control.

### What's in this build

#### 🧠 Master Agent
- Multi-step reasoning with LangGraph / `deepagents` runtime
- Streaming responses with reasoning / text / tool-call event stream
- Per-session goal / `/goal` judge that auto-decides when to stop iterating
- Pluggable LLM providers: Anthropic, OpenAI, Ollama, plus any OpenAI-compatible
  endpoint (provider normalization abstracts base URL + auth header quirks)
- Built-in Anthropic roundtrip + video-passthrough adapters

#### 🛠️ Tools available to the Agent
- **Bash** — `bash-tool` with timeout, output truncation, dangerous-pattern blocklist
- **Files** — read / write / edit / search with project-scope awareness
- **Fetch** — HTTP GET / POST with HTML → Markdown conversion (jsdom +
  @mozilla/readability + turndown)
- **Web search** — pluggable provider with built-in default
- **arXiv** — paper search and abstract retrieval for research workflows
- **Skills** — loadable `.cdf/skills/*/SKILL.md` with project / global scope
- **MCP servers** — stdio / SSE / HTTP transports via `@langchain/mcp-adapters`

#### 💬 Chat experience
- Slash commands — `/help`, `/goal`, `/clear`, `/context`, and MCP-server
  commands exposed via the popup (`/mcp:<server>`)
- `@` file mention — type `@` to fuzzy-search project files and folders,
  results render as pills in the input
- Streaming message list with tool-call / tool-result grouping, file
  attachments, and message-level error display
- Per-session model override (provider + model) with welcome-screen picker
- Markdown rendering with code blocks (assistant-ui)

#### 🗂️ Projects & sessions
- Multi-project workspace with sidebar tree
- Session history per project; switch sessions without losing state
- Goal system: each session has a user-defined goal; judge auto-runs after
  each iteration
- Task panel with delegated sub-tasks and pending approvals

#### ⚙️ Workflows
- Visual workflow editor (React Flow) — drag-and-drop nodes + edges
- Multiple node types: LLM, Tool, Condition, Sub-workflow
- Save / load / run / history with per-execution node traces
- Streaming node status into the execution panel

#### 🔌 Settings
- Model providers (Anthropic / OpenAI / Ollama / custom) with per-provider
  API key + base URL
- MCP server registry (add / remove / test connection)
- Skill library (project + global scope)
- System: language (中文 / English), theme (light / dark / system)

#### 🤖 Agent Library
- Per-project custom agents with system prompt, default provider, MCP
  bindings, skill bindings
- Edit / create / set-as-default, scoped to a project

#### 🖥️ Desktop platform
- Cross-platform: macOS, Windows, Linux
- Native window management, OS notifications (sonner), file dialogs
- Local SQLite database (better-sqlite3) for projects / sessions / agents /
  workflows / providers / MCP servers / execution history
- electron-store for app preferences (theme, last project, etc.)

#### 🌐 Internationalization
- Full UI in **English** (`en-US`) and **简体中文** (`zh-CN`)
- Language switchable in settings, no restart required

### Quality baseline

- ✅ **422 / 422** unit tests passing across 56 test files
- ✅ **0** TypeScript errors (main + web tsconfigs)
- ✅ Cross-platform CI on Ubuntu / macOS / Windows
- ✅ Cross-platform release pipeline producing 6 build targets:
  - `CDF-0.1.0-mac-x64.dmg` (Intel)
  - `CDF-0.1.0-mac-arm64.dmg` (Apple Silicon)
  - `CDF.Setup.0.1.0-win-x64.exe` (NSIS installer)
  - `CDF.Setup.0.1.0-win-arm64.exe` (NSIS installer)
  - `CDF-0.1.0-linux-x64.AppImage`
  - `CDF-0.1.0-linux-arm64.AppImage`
- ✅ `latest-*.yml` sidecars for `electron-updater`-based in-app updates

### Known limitations

- macOS / Windows installers are **not code-signed** in this build. Users
  will need to right-click → Open (macOS) or accept the SmartScreen prompt
  (Windows) on first launch.
- Linux AppImage runs as unsigned (no AppImage signing key configured).
- No auto-update channel yet — releases are manual.

### How to use

1. Download the installer for your platform from the
   [Releases page](https://github.com/suntianc/CDF/releases/tag/v0.1.1).
2. Install and launch CDF.
3. Open Settings → Model Providers → add your Anthropic / OpenAI / Ollama
   credentials.
4. (Optional) Settings → MCP Servers → register any external MCP servers
   you want the Agent to use.
5. Create a project, start a session, and describe what you want built.

### Changes vs internal development

There is no public release before 0.1.0. This is the **first** tagged
release. The `0.x` version line signals an early-development API: things
will change, but the data model and core Agent loop are stable enough
to start using.

[0.1.1]: https://github.com/suntianc/CDF/releases/tag/v0.1.1
