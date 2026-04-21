# Claude Code: The Complete Technical Guide

---

## Table of Contents

### Part I: Foundations
- [TLDR (Abstract)](#tldr-abstract)
- [Chapter 1: Introduction — What is Claude Code?](#chapter-1-introduction----what-is-claude-code)
  - 1.1 Beyond the Chatbot: An Agentic Coding Assistant
  - 1.2 Available Surfaces
  - 1.3 The Key Differentiator: Agency
  - 1.4 High-Level Architecture
  - 1.5 Installation
  - 1.6 System Requirements
  - 1.7 Authentication
  - 1.8 Your First Session
- [Chapter 2: How Claude Code Works — The Agentic Loop](#chapter-2-how-claude-code-works----the-agentic-loop)
  - 2.1 The Three Phases
  - 2.2 Real-World Example: Fixing a Bug Step by Step
  - 2.3 Available Models
  - 2.4 Built-in Tools
  - 2.5 The Context Window
  - 2.6 Permission System: 6 Modes
  - 2.7 Sessions
- [Chapter 3: The CLI — Your Primary Interface](#chapter-3-the-cli----your-primary-interface)
  - 3.1 Starting and Continuing Sessions
  - 3.2 Key CLI Flags
  - 3.3 System Prompt Customization
  - 3.4 Unix Composability
- [Chapter 4: Interactive Mode — Keyboard Shortcuts & Input](#chapter-4-interactive-mode----keyboard-shortcuts--input)
  - 4.1 General Controls
  - 4.2 Text Editing
  - 4.3 Multiline Input
  - 4.4 Quick Commands
  - 4.5 Vim Editor Mode
  - 4.6 Background Commands & Side Questions

### Part II: Core Concepts
- [Chapter 5: Memory — CLAUDE.md & Auto Memory](#chapter-5-memory----claudemd-and-auto-memory)
  - 5.1 Two Memory Systems
  - 5.2 CLAUDE.md Locations and Scopes
  - 5.3 Writing Effective CLAUDE.md
  - 5.4 Modular Rules with .claude/rules/
  - 5.5 Auto Memory
- [Chapter 6: Context Window Management](#chapter-6-context-window-management)
  - 6.1 Startup Token Costs
  - 6.2 Auto-Compaction
  - 6.3 Manual Compaction
  - 6.4 What Survives Compaction
- [Chapter 7: Permissions & Security](#chapter-7-permissions--security)
  - 7.1 Six Permission Modes
  - 7.2 Permission Rules Syntax
  - 7.3 Sandboxing
  - 7.4 Auto Mode Classifier
- [Chapter 8: Checkpointing — Undo Anything](#chapter-8-checkpointing----undo-anything)
  - 8.1 How Checkpoints Work
  - 8.2 Rewind Menu
  - 8.3 Limitations

### Part III: Extensibility
- [Chapter 9: Skills — Reusable Workflows & Knowledge](#chapter-9-skills----reusable-workflows--knowledge)
  - 9.1 SKILL.md Files
  - 9.2 Frontmatter Reference
  - 9.3 Invocation Control
  - 9.4 Dynamic Context Injection
  - 9.5 Skills vs CLAUDE.md
- [Chapter 10: Hooks — Event-Driven Automation](#chapter-10-hooks----event-driven-automation)
  - 10.1 Lifecycle Events
  - 10.2 Four Handler Types
  - 10.3 Matcher Patterns
  - 10.4 Exit Codes & JSON Output
- [Chapter 11: MCP — Model Context Protocol](#chapter-11-mcp----model-context-protocol)
  - 11.1 Transport Types
  - 11.2 Installation Scopes
  - 11.3 OAuth Authentication
  - 11.4 Resources, Prompts & Channels
- [Chapter 12: Sub-agents — Isolated Specialists](#chapter-12-sub-agents----isolated-specialists)
  - 12.1 Built-in Sub-agents
  - 12.2 Custom Sub-agents
  - 12.3 Foreground vs Background
  - 12.4 Persistent Memory
- [Chapter 13: Agent Teams — Parallel Collaboration](#chapter-13-agent-teams----parallel-collaboration)
  - 13.1 Architecture
  - 13.2 Sub-agents vs Agent Teams
  - 13.3 Quality Gates & Hooks

### Part IV: Ecosystem & Integrations
- [Chapter 14: Plugins — Bundled Extensions](#chapter-14-plugins----bundled-extensions)
  - 14.1 Plugin Manifest & Structure
  - 14.2 LSP Servers & Monitors
  - 14.3 Marketplaces
- [Chapter 15: IDE Integrations — VS Code & JetBrains](#chapter-15-ide-integrations----vs-code-and-jetbrains)
  - 15.1 VS Code Extension
  - 15.2 JetBrains Plugin
- [Chapter 16: Desktop App, Web & Mobile](#chapter-16-desktop-app-web-and-mobile)
  - 16.1 Desktop App
  - 16.2 Claude Code on the Web
  - 16.3 Remote Control
- [Chapter 17: CI/CD Integrations](#chapter-17-cicd-integrations)
  - 17.1 GitHub Actions
  - 17.2 GitLab CI/CD
  - 17.3 Code Review
  - 17.4 Slack Integration
- [Chapter 18: Scheduling & Automation](#chapter-18-scheduling-and-automation)
  - 18.1 Routines (Cloud)
  - 18.2 Desktop Scheduled Tasks
  - 18.3 /loop (Session-Scoped)
  - 18.4 Headless Mode

### Part V: Mastery
- [Chapter 19: Settings & Configuration](#chapter-19-settings--configuration)
  - 19.1 Four Configuration Scopes
  - 19.2 Settings Precedence
  - 19.3 Key Settings Categories
  - 19.4 Enterprise Managed Settings
- [Chapter 20: Model Configuration & Performance](#chapter-20-model-configuration--performance)
  - 20.1 Model Aliases
  - 20.2 Effort Levels
  - 20.3 Extended Thinking & Fast Mode
  - 20.4 Cost Management
- [Chapter 21: Common Workflows & Best Practices](#chapter-21-common-workflows--best-practices)
  - 21.1 Core Workflows
  - 21.2 Plan Mode (4 Phases)
  - 21.3 Eight Best Practices
- [Chapter 22: Advanced Topics & Agent SDK](#chapter-22-advanced-topics--agent-sdk)
  - 22.1 Chrome Integration
  - 22.2 Channels
  - 22.3 Agent SDK
  - 22.4 Environment Variables
  - 22.5 Data Usage & Privacy
- [Chapter 23: Conclusion & References](#chapter-23-conclusion--references)
  - 23.1 Feature Maturity
  - 23.2 Learning Path
  - 23.3 References

---

**Part 1 -- Foundations: Understanding Claude Code from the Ground Up**


---

## TLDR (Abstract)

Claude Code is Anthropic's **agentic coding tool** -- not a chatbot, but an autonomous agent that reads your codebase, edits files, runs shell commands, and integrates with your entire development toolchain. It is available across every surface a developer touches: **Terminal CLI, VS Code, JetBrains, Desktop App, Web (claude.ai/code), Slack, GitHub Actions, GitLab CI/CD, and Chrome**.

The core insight behind Claude Code is its **agentic loop**: a repeating cycle of **Gather Context, Take Action, and Verify Results** that continues until a task is complete. Unlike traditional autocomplete tools that suggest the next line, Claude Code plans multi-step implementations, executes them across files, runs tests, reads error output, and iterates -- the same way a senior engineer works through a problem.

Key capabilities include: **persistent memory** via CLAUDE.md files and auto-memory, **custom skills** (reusable prompt-based workflows), **lifecycle hooks** (shell commands that fire before/after Claude actions), **MCP server integrations** (connecting to external tools like Jira, Slack, databases), **sub-agents** (spawning focused workers for parallel tasks), **agent teams** (multiple Claude instances coordinating on a project), and **6 permission modes** ranging from manual approval to fully autonomous execution with safety classifiers.

Claude Code runs on **Claude Opus 4.7** (most capable), **Sonnet 4.6** (daily coding), and **Haiku 4.5** (fast/simple), with context windows of **200K tokens by default and up to 1M tokens** for long sessions.

**Who should use it**: Software engineers who want an AI pair-programmer that understands their entire codebase, teams automating code review and CI/CD, and anyone building AI-powered developer workflows.

---

## Chapter 1: Introduction -- What is Claude Code?

### 1.1 Beyond the Chatbot: An Agentic Coding Assistant

If you have used AI coding assistants before, you have probably experienced the pattern: you paste a code snippet into a chat window, get a suggestion back, copy it, paste it into your editor, realize it does not quite fit, go back to the chat, provide more context, and repeat. That workflow treats AI as a consultant you brief over email.

Claude Code works differently. It is an **agentic** coding assistant, meaning it does not wait for you to feed it context one snippet at a time. Instead, it reads your entire codebase, plans a multi-step approach, executes changes across multiple files, runs your tests, reads the output, and iterates until the task is done. The difference is like the difference between emailing a contractor a description of a bug and having a senior engineer sit down at your desk, pull up the repo, and fix it.

Here is a concrete example. You type:

```bash
claude "The auth module returns 401 after token refresh. Fix it."
```

Claude Code will:

1. **Search** your codebase for auth-related files using `Grep` and `Glob`
2. **Read** the relevant source files (`src/api/auth.ts`, `src/lib/tokens.ts`)
3. **Analyze** the token refresh logic and identify the bug
4. **Edit** the broken file with a targeted fix (not a full rewrite)
5. **Run** your test suite (`npm test`) to verify the fix
6. **Read** the test output, and if tests fail, iterate on the fix
7. **Report** what it did and why

That entire sequence happens autonomously. You approve actions at permission prompts (or let auto mode handle it), but you do not have to manually feed context or copy-paste code.

### 1.2 Available Surfaces

One of Claude Code's design principles is meeting developers where they already work. It is available across virtually every surface in a modern development workflow:

| Surface | Description | Best For |
|:--------|:------------|:---------|
| **Terminal CLI** | Full-featured command-line interface | Power users, scripting, CI/CD pipelines |
| **VS Code Extension** | Inline diffs, @-mentions, plan review | Developers who live in VS Code |
| **JetBrains Plugin** | Native plugin for IntelliJ, PyCharm, WebStorm | Java/Python/web developers on JetBrains |
| **Desktop App** | Standalone native app (macOS, Windows) | Visual diff review, multiple sessions side-by-side |
| **Web (claude.ai/code)** | Browser-based, no local setup | Remote work, cloud-only environments |
| **Slack** | `@Claude` mentions in channels | Bug reports to PRs from team chat |
| **GitHub Actions** | CI/CD integration | Automated PR review, issue triage |
| **GitLab CI/CD** | CI/CD integration | Same as above for GitLab users |
| **Chrome Extension** | Browser automation and debugging | Debugging live web applications |
| **Remote Control** | Control terminal sessions from browser/mobile | Working from phone or another device |

All of these surfaces connect to the same underlying engine. Your CLAUDE.md files, settings, and MCP server configurations work across all of them.

### 1.3 The Key Differentiator: Agency

The word "agentic" is critical. Traditional AI coding tools operate in a **request-response** pattern: you ask, they answer. Claude Code operates in an **agentic loop**: it observes the environment, decides what to do, acts, observes the result, and decides what to do next.

Think of it this way:

> **Real-world analogy**: Traditional AI coding tools are like having a very smart friend on the phone -- you describe the problem, they suggest a fix, and you implement it. Claude Code is like having a senior engineer sit down at your workstation -- they pull up the repo, read the code, make changes, run the tests, and keep going until it works. They ask you before doing anything risky, but they drive the process.

### 1.4 High-Level Architecture

![Claude Code Architecture](diagrams/claude-code-architecture.png)

At its core, Claude Code follows this architecture:

```
                        +-----------------------+
                        |    User Interface     |
                        | (CLI / IDE / Desktop  |
                        |  / Web / Slack / CI)  |
                        +-----------+-----------+
                                    |
                                    v
                    +-------------------------------+
                    |       Context Window           |
                    |  +-------------------------+   |
                    |  | System Prompt  (~4,200t)|   |
                    |  | Auto Memory     (~680t) |   |
                    |  | Env Info        (~280t) |   |
                    |  | MCP Tools       (~120t) |   |
                    |  | Skill Descs     (~450t) |   |
                    |  | CLAUDE.md     (~2,100t) |   |
                    |  | Conversation History    |   |
                    |  +-------------------------+   |
                    +-------------------------------+
                                    |
                                    v
                    +-------------------------------+
                    |        Claude Model            |
                    |  (Opus 4.7 / Sonnet 4.6 /     |
                    |        Haiku 4.5)              |
                    +---------------+---------------+
                                    |
                    +---------------v---------------+
                    |       Built-in Tools           |
                    | Read | Edit | Write | Bash     |
                    | Glob | Grep | Agent | WebSearch|
                    | WebFetch | NotebookEdit | ...  |
                    +---------------+---------------+
                                    |
                                    v
                            +-------+-------+
                            |    Results    |
                            +-------+-------+
                                    |
                        +-----------v-----------+
                        |   Agentic Loop:       |
                        |   "Is task complete?" |
                        |   No -> Loop back to  |
                        |   Context Window      |
                        +-----------------------+
```

The key insight in this architecture is the **feedback loop**. Every tool result -- every file read, every command output, every test result -- flows back into the context window and informs the next decision. This is what makes Claude Code agentic rather than merely conversational.

### 1.5 Installation

Getting started is a one-line install. Choose the method that fits your platform:

**macOS / Linux / WSL (recommended):**

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

**Windows PowerShell:**

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Homebrew (macOS/Linux):**

```bash
brew install --cask claude-code
```

**WinGet (Windows):**

```powershell
winget install Anthropic.ClaudeCode
```

**npm (all platforms, requires Node.js 18+):**

```bash
npm install -g @anthropic-ai/claude-code
```

> **Note**: Native installations auto-update in the background. Homebrew and WinGet installs require manual updates (`brew upgrade claude-code` or `winget upgrade Anthropic.ClaudeCode`).

### 1.6 System Requirements

| Requirement | Minimum |
|:------------|:--------|
| **macOS** | 13.0 (Ventura) or later |
| **Windows** | 10 version 1809+ or Windows Server 2019+ |
| **Linux** | Ubuntu 20.04+, Debian 10+, Alpine 3.19+ |
| **RAM** | 4 GB |
| **Processor** | x64 or ARM64 |
| **Shell** | Bash, Zsh, PowerShell, or CMD |
| **Network** | Internet connection required |
| **Windows extra** | Git for Windows (native installs) |

### 1.7 Authentication

Claude Code requires one of the following:

- **Claude Subscription**: Pro, Max, Team, or Enterprise plan (the free plan does not include Claude Code)
- **Anthropic Console**: API account with pay-per-token billing
- **Third-party Providers**: Amazon Bedrock, Google Vertex AI, or Microsoft Foundry

Log in on first launch:

```bash
cd your-project
claude
# Follow the browser prompts to authenticate
```

### 1.8 Your First Session

Once authenticated, starting a session is as simple as:

```bash
cd your-project
claude
```

Claude Code reads your project structure, loads any CLAUDE.md instructions, and presents an interactive prompt. From here you can type natural language requests, use slash commands (`/help`, `/model`, `/cost`), run bash commands with `!`, or reference files with `@`.

> **Try This**: Navigate to any project on your machine and run `claude "explain the architecture of this project"`. Watch how Claude reads your files, identifies patterns, and produces a comprehensive overview -- without you pointing it at any specific file.

### 1.9 Key Takeaway

Claude Code is fundamentally different from chat-based AI coding assistants. It is an **autonomous agent** that reads, writes, executes, and verifies -- operating in a continuous loop until your task is complete. It runs everywhere you code (terminal, IDE, browser, CI/CD) and requires minimal setup: one install command and a login. The rest of this paper explores exactly how it works under the hood.

---

## Chapter 2: How Claude Code Works -- The Agentic Loop

### 2.1 The Three Phases

Every interaction with Claude Code follows the same fundamental pattern, repeated until the task is complete. Understanding this loop is the single most important concept for using Claude Code effectively.

```
    +------------------+
    |                  |
    |  1. GATHER       |    Read files, search code, check git status,
    |     CONTEXT      |    load CLAUDE.md, read test output
    |                  |
    +--------+---------+
             |
             v
    +--------+---------+
    |                  |
    |  2. TAKE         |    Edit files, run commands, create files,
    |     ACTION       |    spawn sub-agents, call MCP tools
    |                  |
    +--------+---------+
             |
             v
    +--------+---------+
    |                  |
    |  3. VERIFY       |    Run tests, read output, check for errors,
    |     RESULTS      |    validate behavior, compare with intent
    |                  |
    +--------+---------+
             |
             |   Task complete? ---> YES ---> Report to user
             |        |
             |        NO
             |        |
             +--------+  (loop back to Gather Context)
```

**Phase 1: Gather Context** -- Claude reads your codebase to understand what exists. It uses tools like `Read` (read files), `Glob` (find files by pattern), `Grep` (search content with regex), and `WebSearch`/`WebFetch` (look up documentation online). This is equivalent to a developer opening a project for the first time and exploring the file tree, reading key files, and understanding the architecture.

**Phase 2: Take Action** -- Based on context, Claude decides what to do. It uses tools like `Edit` (make targeted changes to files), `Write` (create new files), `Bash` (run shell commands), and `Agent` (spawn sub-agents for parallel work). This is the equivalent of the developer actually writing code, running scripts, and making changes.

**Phase 3: Verify Results** -- After acting, Claude checks its work. It runs tests, reads compiler output, checks for lint errors, and validates that the changes match the original intent. If something is wrong, it loops back to Phase 1 with the new information (e.g., "test X failed because of Y") and iterates.

### 2.2 Real-World Example: Fixing a Bug Step by Step

Let us trace through a complete agentic loop. You type:

```
Fix the bug where users get a 401 error after token refresh
```

**Turn 1 -- Gather Context:**
- Claude uses `Grep` to search for "token refresh" across the codebase
- Finds references in `src/api/auth.ts`, `src/lib/tokens.ts`, `src/middleware/auth.ts`
- Uses `Read` to load all three files into context

**Turn 2 -- Analyze & Act:**
- Claude identifies that `refreshToken()` in `tokens.ts` updates the access token in memory but the auth middleware reads it from a stale cache
- Uses `Edit` to modify `src/middleware/auth.ts` to invalidate the cache after refresh

**Turn 3 -- Verify:**
- Claude runs `Bash` with `npm test -- --grep "token"` to run auth-related tests
- Reads the output: 14 tests pass, 1 fails -- "expected header Authorization to contain new token"
- The fix was incomplete

**Turn 4 -- Iterate (Gather + Act):**
- Claude reads the failing test to understand the expectation
- Identifies that the response interceptor also needs updating
- Edits `src/lib/tokens.ts` to propagate the new token to pending requests

**Turn 5 -- Verify again:**
- Runs the full test suite: all 15 tests pass
- Reports the fix and what was changed

That is five agentic turns, each one autonomously decided by Claude. You approved two file edits (or had auto mode handle them), but you did not have to manually debug, find files, or figure out the fix.

### 2.3 Available Models

Claude Code supports three model tiers, each suited to different tasks:

| Model | Alias | Strengths | Best For | Context |
|:------|:------|:----------|:---------|:--------|
| **Claude Opus 4.7** | `opus` | Most capable reasoning, complex planning | Architecture decisions, multi-step refactoring, hard bugs | 200K (auto-upgrades to 1M on Max/Team/Enterprise) |
| **Claude Sonnet 4.6** | `sonnet` | Excellent balance of capability and speed | Day-to-day coding, feature development, code review | 200K (1M available) |
| **Claude Haiku 4.5** | `haiku` | Fastest, most efficient | Simple tasks, sub-agent work, quick lookups | 200K |

**Special aliases:**
- `opusplan` -- Uses Opus during plan mode for reasoning, then switches to Sonnet for execution (best of both worlds)
- `best` -- Always maps to the most capable model (currently Opus)
- `sonnet[1m]` / `opus[1m]` -- Explicitly requests the 1M context window variant

Switch models mid-session with `/model sonnet` or at startup with `claude --model opus`.

> **Default model by plan**: Max and Team Premium default to Opus 4.7. Pro, Team Standard, Enterprise, and API default to Sonnet 4.6. Bedrock/Vertex/Foundry default to Sonnet 4.5.

### 2.4 Built-in Tools

Claude Code comes with a comprehensive toolkit. Every tool in this table is available out of the box -- no configuration required:

| Tool | What It Does | Real-World Analogy |
|:-----|:-------------|:-------------------|
| **Read** | Read any file on disk | Opening a file in your editor |
| **Edit** | Make targeted edits to existing files (not full rewrites) | Find-and-replace with intelligence |
| **Write** | Create new files from scratch | Creating a new file in your editor |
| **Bash** | Execute any shell command | Your terminal |
| **Glob** | Find files by name pattern (e.g., `**/*.ts`) | `find` command, but faster |
| **Grep** | Search file content with regex | `ripgrep` / `grep` |
| **WebSearch** | Search the web for documentation, answers | Googling something |
| **WebFetch** | Fetch and process a specific URL | Opening a documentation page |
| **Agent** | Spawn a sub-agent for focused work | Delegating a task to a teammate |
| **NotebookEdit** | Edit Jupyter notebook cells | Working in Jupyter |

Additionally, **plugins** can add tools like:
- **LSP** (Language Server Protocol) -- Code intelligence: go-to-definition, find-references, type checking
- **Monitor** -- Watch background processes

Each tool is designed to be composable. Claude chains them naturally: `Glob` to find files, `Read` to understand them, `Edit` to change them, `Bash` to test the changes.

### 2.5 The Context Window: What Claude Sees

The context window is Claude's working memory -- everything it can "see" at any point in the conversation. Understanding what fills it helps you use Claude Code effectively.

**At startup, the context window loads (in order):**

| Component | Approximate Tokens | Description |
|:----------|:-------------------|:------------|
| System prompt | ~4,200 | Core instructions for behavior, tool use, response formatting. You never see it. |
| Auto memory (MEMORY.md) | ~680 | Claude's notes to itself from previous sessions (first 200 lines or 25KB). |
| Environment info | ~280 | Working directory, platform, shell, OS version, git status. |
| MCP tools (deferred) | ~120 | Names of available MCP tools. Full schemas load on demand. |
| Skill descriptions | ~450 | One-line descriptions of available skills. Full content loads only when invoked. |
| User CLAUDE.md | ~320 | Your global preferences (`~/.claude/CLAUDE.md`). |
| Project CLAUDE.md | ~1,800 | Project conventions and instructions (`./CLAUDE.md`). |
| **Total startup** | **~7,850** | **Less than 4% of the 200K window** |

That leaves **~192,000 tokens** for your conversation, file reads, command outputs, and Claude's responses.

**Context window sizes:**
- **200K tokens** -- Default for all models
- **1M tokens** -- Available for Opus 4.7, Opus 4.6, and Sonnet 4.6 (auto-enabled for Opus on Max/Team/Enterprise plans; opt-in for others)

When the context window approaches its limit, Claude Code automatically triggers **compaction** -- it summarizes the conversation history to free up space while preserving key information. Project-root CLAUDE.md files survive compaction (they are re-read from disk), but conversation-only context is summarized.

> **Real-world analogy**: The context window is like a desk. At the start of the day, you have your reference materials laid out (CLAUDE.md, environment info). As you work, you pile on files, test results, and notes. When the desk gets full, you organize and file away older materials (compaction), keeping the most important items within reach.

### 2.6 Permission System: 6 Modes

Claude Code gives you fine-grained control over how much autonomy to grant. Six permission modes trade off convenience against oversight:

| Mode | What Runs Without Asking | Best For |
|:-----|:-------------------------|:---------|
| **`default`** | Reads only | Getting started, sensitive work |
| **`acceptEdits`** | Reads, file edits, common filesystem commands (`mkdir`, `touch`, `mv`, `cp`, etc.) | Iterating on code you review after |
| **`plan`** | Reads only (Claude proposes but does not edit) | Exploring a codebase before changing it |
| **`auto`** | Everything, with background safety classifier checks | Long tasks, reducing prompt fatigue |
| **`dontAsk`** | Only pre-approved tools (everything else denied) | Locked-down CI/CD and scripts |
| **`bypassPermissions`** | Everything except protected paths | Isolated containers/VMs only |

Switch modes mid-session with `Shift+Tab`, or start with a specific mode:

```bash
claude --permission-mode auto
```

**Protected paths are never auto-approved** regardless of mode: `.git/`, `.claude/` (config files), shell profiles (`.bashrc`, `.zshrc`), and similar sensitive locations.

Auto mode deserves special mention: it uses a separate **classifier model** that reviews each action before execution, blocking anything that escalates beyond your request, targets unrecognized infrastructure, or appears driven by hostile content. It blocks dangerous patterns by default (e.g., `curl | bash`, production deploys, force pushes to `main`) while allowing routine operations (local file edits, installing declared dependencies, read-only HTTP requests).

### 2.7 Sessions: Persistent and Resumable

Every Claude Code session is saved locally as a **JSONL file**. This means you can:

- **Continue the last session**: `claude --continue` or `claude -c`
- **Resume a specific session**: `claude --resume auth-refactor`
- **Resume from a PR**: `claude --from-pr 123`
- **Name sessions** for easy reference: `claude --name "feature-login"`
- **Fork a session** to try a different approach: `claude --resume abc123 --fork-session`

Sessions persist across terminal restarts. You can close your terminal, reboot your machine, and pick up right where you left off.

> **Try This**: Start a session with `claude --name "my-first-session"`, do some work, exit with Ctrl+D, then resume it with `claude --resume my-first-session`. Notice how Claude remembers the full conversation history.

### 2.8 Key Takeaway

The agentic loop -- Gather Context, Take Action, Verify Results -- is the fundamental operating principle of Claude Code. Everything else (tools, permissions, models, sessions) serves this loop. When you understand that Claude Code is *autonomously iterating* rather than *passively responding*, you can structure your prompts and workflows to take full advantage of it. Tell Claude *what* you want done, give it enough permission to work, and let the loop run.

---

## Chapter 3: The CLI -- Your Primary Interface

### 3.1 Starting Sessions

The CLI is Claude Code's most powerful and flexible interface. Every capability available in the GUI surfaces is also available (and often more accessible) from the command line.

**Three ways to start:**

```bash
# 1. Interactive mode -- opens a REPL where you type prompts
claude

# 2. Interactive with an initial prompt -- starts working immediately
claude "add input validation to the signup form"

# 3. Non-interactive (print) mode -- outputs result and exits
claude -p "explain the architecture of this project"
```

The distinction between interactive (`claude` / `claude "query"`) and non-interactive (`claude -p "query"`) is important. Interactive mode gives you a full REPL with permission prompts, follow-up questions, and session management. Non-interactive mode runs the task to completion (or until `--max-turns` is reached) and outputs the result -- perfect for scripts and CI pipelines.

### 3.2 Continuing and Resuming Sessions

```bash
# Continue the most recent session in this directory
claude -c
claude --continue

# Continue most recent session in non-interactive mode
claude -c -p "now add tests for the validation"

# Resume a specific session by name or ID
claude --resume "auth-refactor"
claude -r "auth-refactor" "Finish the PR"

# Resume sessions linked to a specific PR
claude --from-pr 123
claude --from-pr https://github.com/org/repo/pull/123
```

### 3.3 Key CLI Flags Reference

This table covers the flags you will use most often. Claude Code has many more (run `claude --help` for the complete list), but these cover 90% of daily use:

| Flag | Description | Example |
|:-----|:------------|:--------|
| `--model` | Choose the model (alias or full name) | `claude --model opus` |
| `--permission-mode` | Set permission mode at startup | `claude --permission-mode auto` |
| `--allowedTools` | Pre-approve specific tools (no prompts) | `claude --allowedTools "Bash(git *)" "Read"` |
| `--disallowedTools` | Remove tools from Claude's access | `claude --disallowedTools "Bash(rm *)"` |
| `--output-format` | Output format: `text`, `json`, `stream-json` | `claude -p --output-format json "query"` |
| `--max-turns` | Limit agentic turns (print mode only) | `claude -p --max-turns 5 "query"` |
| `--max-budget-usd` | Cap API spend for a single run | `claude -p --max-budget-usd 2.00 "query"` |
| `--worktree`, `-w` | Isolated git worktree at `.claude/worktrees/<name>` | `claude -w feature-auth` |
| `--bare` | Minimal mode -- skip hooks, skills, plugins, MCP, CLAUDE.md | `claude --bare -p "query"` |
| `--append-system-prompt` | Add custom instructions to the system prompt | `claude --append-system-prompt "Use TypeScript"` |
| `--system-prompt` | Replace the entire system prompt | `claude --system-prompt "You are a Python expert"` |
| `--chrome` | Enable Chrome browser integration | `claude --chrome` |
| `--remote-control` | Enable control from browser/mobile | `claude --remote-control "My Project"` |
| `--name`, `-n` | Name the session for easy resuming | `claude -n "auth-refactor"` |
| `--continue`, `-c` | Continue most recent session | `claude -c` |
| `--resume`, `-r` | Resume a specific session by name or ID | `claude -r auth-refactor` |
| `--print`, `-p` | Non-interactive mode (output and exit) | `claude -p "explain this code"` |
| `--verbose` | Show full turn-by-turn output | `claude --verbose` |
| `--effort` | Set reasoning effort (`low`/`medium`/`high`/`xhigh`/`max`) | `claude --effort high` |
| `--fallback-model` | Auto-fallback model when primary is overloaded | `claude -p --fallback-model sonnet "query"` |
| `--json-schema` | Get structured JSON output matching a schema | `claude -p --json-schema '{...}' "query"` |
| `--tmux` | Create a tmux session for the worktree | `claude -w feature-auth --tmux` |
| `--add-dir` | Add extra directories for Claude to access | `claude --add-dir ../shared-lib` |
| `--teleport` | Resume a web session in your local terminal | `claude --teleport` |

### 3.4 System Prompt Customization

Four flags let you customize what Claude "knows" before you even ask a question:

| Flag | Behavior | When to Use |
|:-----|:---------|:------------|
| `--system-prompt` | Replaces the entire default prompt | Full control -- building custom agents |
| `--system-prompt-file` | Replaces with file contents | Same, but instructions live in a file |
| `--append-system-prompt` | Appends to the default prompt | Adding rules while keeping built-in capabilities |
| `--append-system-prompt-file` | Appends file contents | Same, but from a file |

For most use cases, use `--append-system-prompt`. It preserves all of Claude Code's built-in capabilities (tools, formatting, safety) while adding your custom rules on top. Only use `--system-prompt` when you need complete control, like when building custom agents with the Agent SDK.

### 3.5 Unix Composability: Piping and Scripting

Claude Code follows the Unix philosophy: it reads from stdin, writes to stdout, and composes with other tools via pipes. This makes it a first-class citizen in shell scripts and CI pipelines.

**Piping input:**

```bash
# Analyze a log file
tail -200 app.log | claude -p "summarize errors and suggest fixes"

# Explain a diff
git diff main | claude -p "review this diff for security issues"

# Process a list of files
git diff main --name-only | claude -p "review these changed files"

# Translate content
cat src/i18n/en.json | claude -p "translate to French, output JSON"
```

**Scripting with JSON output:**

```bash
# Get structured output for further processing
result=$(claude -p --output-format json "list all TODO comments in src/")
echo "$result" | jq '.result'

# Stream JSON events for real-time processing
claude -p --output-format stream-json "refactor auth module" | \
  while read -r line; do
    echo "$line" | jq -r '.type // empty'
  done
```

**CI pipeline integration (GitHub Actions example):**

```yaml
name: AI Code Review
on: [pull_request]
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install Claude Code
        run: curl -fsSL https://claude.ai/install.sh | bash
      - name: Review PR
        run: |
          git diff origin/main...HEAD | \
          claude -p \
            --permission-mode dontAsk \
            --max-turns 3 \
            --output-format text \
            "Review this diff for bugs, security issues, and style violations. 
             Output a markdown summary."
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
```

### 3.6 Real-World Example: Auto-Review PRs in CI

Here is a practical CI pipeline that uses Claude Code to automatically review pull requests and post comments:

```bash
#!/bin/bash
# review-pr.sh -- Run Claude Code as an automated PR reviewer

PR_NUMBER=$1

# Fetch the diff
gh pr diff "$PR_NUMBER" > /tmp/pr-diff.txt

# Run Claude Code with strict constraints
cat /tmp/pr-diff.txt | claude -p \
  --permission-mode dontAsk \
  --max-turns 5 \
  --max-budget-usd 1.00 \
  --allowedTools "Read" "Grep" "Glob" \
  --output-format text \
  --append-system-prompt "You are a code reviewer. Focus on:
    1. Security vulnerabilities
    2. Performance issues  
    3. Missing error handling
    4. Test coverage gaps
    Output your review as a markdown checklist." \
  "Review this pull request diff."
```

Key design decisions:
- `--permission-mode dontAsk` prevents any interactive prompts in CI
- `--max-turns 5` caps the agent loop to prevent runaway execution
- `--max-budget-usd 1.00` sets a hard cost ceiling
- `--allowedTools "Read" "Grep" "Glob"` gives read-only access (Claude cannot modify files)
- `--output-format text` gives clean output for posting as a PR comment

> **Try This**: Create a shell script that pipes `git log --oneline -20` into Claude Code and asks it to generate release notes. Use `claude -p --output-format text` so the output is clean markdown you can paste into a release.

### 3.7 Key Takeaway

The CLI is Claude Code's most versatile interface. Interactive mode (`claude`) gives you a full AI pair-programming session. Non-interactive mode (`claude -p`) makes Claude Code a composable Unix tool you can pipe, script, and automate. The combination of `--permission-mode`, `--allowedTools`, `--max-turns`, and `--max-budget-usd` gives you precise control over what Claude can do, how long it runs, and how much it costs -- making it safe for everything from local development to production CI pipelines.

---

## Chapter 4: Interactive Mode -- Keyboard Shortcuts and Input

### 4.1 Why Interactive Mode Matters

Interactive mode (`claude` or `claude "query"`) is where most developers spend their time with Claude Code. It is a full-featured terminal application with keyboard shortcuts, multiple input modes, vim emulation, image support, and more. Mastering these controls is like mastering keyboard shortcuts in your IDE -- it dramatically speeds up your workflow.

### 4.2 General Controls

These are the shortcuts you will use in every session:

| Shortcut | Description | When to Use |
|:---------|:------------|:------------|
| `Ctrl+C` | Cancel current generation or clear input | Stop Claude mid-response |
| `Ctrl+D` | Exit Claude Code session | Done for the day |
| `Ctrl+L` | Clear input and redraw screen | Display gets garbled |
| `Ctrl+O` | Toggle transcript viewer | See detailed tool usage, expand collapsed MCP calls |
| `Ctrl+R` | Reverse search command history | Find a previous prompt |
| `Ctrl+B` | Background running tasks | Long-running builds, dev servers |
| `Ctrl+T` | Toggle task list | Track multi-step work progress |
| `Shift+Tab` | Cycle permission modes | Switch between default/acceptEdits/plan/auto |
| `Alt+P` (or `Option+P`) | Switch model | Change from Sonnet to Opus without clearing prompt |
| `Alt+T` (or `Option+T`) | Toggle extended thinking | Enable/disable deep reasoning |
| `Alt+O` (or `Option+O`) | Toggle fast mode | Enable/disable fast mode |
| `Esc` + `Esc` | Rewind or summarize | Restore code/conversation to previous point |

> **macOS Note**: Option/Alt key shortcuts require configuring Option as Meta in your terminal. In iTerm2: Settings, Profiles, Keys, set Left/Right Option to "Esc+". In VS Code: set `"terminal.integrated.macOptionIsMeta": true`.

### 4.3 Text Editing Shortcuts

Claude Code supports standard readline-style text editing:

| Shortcut | Description |
|:---------|:------------|
| `Ctrl+A` | Move cursor to start of line |
| `Ctrl+E` | Move cursor to end of line |
| `Ctrl+K` | Delete to end of line (stores for paste) |
| `Ctrl+U` | Delete from cursor to line start (stores for paste) |
| `Ctrl+W` | Delete previous word (stores for paste) |
| `Ctrl+Y` | Paste deleted text |
| `Alt+Y` | Cycle through paste history (after `Ctrl+Y`) |
| `Alt+B` | Move cursor back one word |
| `Alt+F` | Move cursor forward one word |

These work exactly like they do in bash/zsh, so your existing muscle memory transfers directly.

### 4.4 Multiline Input

For prompts that span multiple lines (describing complex tasks, pasting code, etc.):

| Method | Shortcut | Notes |
|:-------|:---------|:------|
| Backslash escape | `\` + `Enter` | Works in all terminals |
| macOS default | `Option+Enter` | Default on macOS |
| Shift+Enter | `Shift+Enter` | Works out of the box in iTerm2, WezTerm, Ghostty, Kitty |
| Control sequence | `Ctrl+J` | Line feed character, works everywhere |
| Paste mode | Paste directly | For code blocks and logs -- just paste multi-line content |

If `Shift+Enter` does not work in your terminal (VS Code, Alacritty, Zed, Warp), run `/terminal-setup` inside Claude Code to install the binding.

### 4.5 Quick Commands

Three special prefixes give you rapid access to common actions:

| Prefix | What It Does | Example |
|:-------|:-------------|:--------|
| `/` | Access commands and skills | `/model sonnet`, `/clear`, `/help` |
| `!` | Bash mode -- run shell commands directly | `! npm test`, `! git status` |
| `@` | File path mention with autocomplete | `@src/auth.ts can you explain this?` |

**Bash mode** (`!`) is particularly useful. It runs the command, adds the output to conversation context (so Claude can see it), and shows real-time progress. It supports `Ctrl+B` backgrounding for long-running commands and Tab completion based on your command history.

**File mentions** (`@`) trigger autocomplete for file paths, making it easy to reference specific files in your prompts without typing full paths.

### 4.6 Vim Mode

For developers who think in vim, Claude Code has a full vim emulation mode. Enable it via `/config` and select "Editor mode".

**Mode switching:**

| Command | Action | From Mode |
|:--------|:-------|:----------|
| `Esc` | Enter NORMAL mode | INSERT |
| `i` / `I` | Insert before cursor / at line start | NORMAL |
| `a` / `A` | Insert after cursor / at line end | NORMAL |
| `o` / `O` | Open line below / above | NORMAL |

**Navigation (NORMAL mode):**

| Command | Action |
|:--------|:-------|
| `h`/`j`/`k`/`l` | Left/down/up/right |
| `w`/`e`/`b` | Next word / end of word / previous word |
| `0` / `$` / `^` | Line start / line end / first non-blank |
| `gg` / `G` | Beginning / end of input |
| `f{char}` / `F{char}` | Jump to next/previous occurrence of character |
| `t{char}` / `T{char}` | Jump to just before/after next/previous character |

**Editing (NORMAL mode):**

| Command | Action |
|:--------|:-------|
| `x` | Delete character |
| `dd` / `D` | Delete line / delete to end of line |
| `dw`/`de`/`db` | Delete word/to-end/back |
| `cc` / `C` | Change line / change to end of line |
| `yy` / `Y` | Yank (copy) line |
| `p` / `P` | Paste after/before cursor |
| `>>` / `<<` | Indent/dedent line |
| `.` | Repeat last change |

**Text objects** work with operators (`d`, `c`, `y`): `iw`/`aw` (inner/around word), `i"`/`a"` (inner/around quotes), `i(`/`a(` (inner/around parens), `i{`/`a{` (inner/around braces).

### 4.7 Image Input

Claude Code supports image input for visual debugging, UI review, and screenshot analysis:

- **Paste from clipboard**: `Ctrl+V` (or `Cmd+V` in iTerm2, `Alt+V` on Windows)
- **Drag and drop**: Drag an image file into the terminal
- **Provide a path**: Reference an image file by path

Images appear as `[Image #N]` chips in your prompt, and Claude can analyze them -- useful for "here is a screenshot of the bug, fix it" workflows.

### 4.8 Side Questions with `/btw`

One of the most underrated features in Claude Code. When you are deep in a debugging session and need to check something quickly without derailing the main conversation:

```
/btw what was the name of that config file we looked at earlier?
```

`/btw` questions:
- Have full visibility into the current conversation (Claude can reference anything it has already seen)
- **Do not add to conversation history** -- the question and answer are ephemeral
- **Work while Claude is processing** -- you can ask side questions during a long-running task
- Have no tool access (answers only from what is already in context)
- Are dismissed with `Space`, `Enter`, or `Escape`

> **Real-world analogy**: `/btw` is like leaning over to a colleague and whispering "hey, what was that file called?" while they are in the middle of explaining something. They answer, and the main conversation continues uninterrupted.

### 4.9 Task List

For complex, multi-step work, Claude creates a task list that tracks progress. Tasks appear in the terminal status area with indicators for pending, in-progress, and complete:

- Press `Ctrl+T` to toggle the task list view (shows up to 10 tasks)
- Ask Claude to "show me all tasks" or "clear all tasks"
- Tasks persist across context compactions
- Share task lists across sessions with `CLAUDE_CODE_TASK_LIST_ID=my-project claude`

### 4.10 Session Recap

When you return to the terminal after stepping away (minimum 3 minutes), Claude Code shows a one-line recap of what happened in the session. This generates in the background while the terminal is unfocused, so it is ready when you switch back. You can also run `/recap` to generate a summary on demand.

### 4.11 Prompt Suggestions

When you open a session, a grayed-out suggestion appears in the prompt based on your project's git history (reflecting files you have recently changed). After Claude responds, suggestions continue based on conversation context -- like a natural follow-up step.

- Press **Tab** or **Right arrow** to accept the suggestion
- Press **Enter** to accept and submit immediately
- Start typing to dismiss it

Suggestions reuse the parent conversation's prompt cache, so additional cost is minimal.

### 4.12 Background Bash Commands

Long-running processes (dev servers, builds, test suites) do not have to block your session:

- Press `Ctrl+B` to move a running command to the background
- Claude can read background task output later using the `Read` tool
- Background tasks get unique IDs for tracking
- They auto-terminate if output exceeds 5GB
- They auto-clean up when Claude Code exits

Common use case: start a dev server in the background, then ask Claude to test against it:

```
! npm run dev
# Press Ctrl+B to background it
Now test the /api/auth endpoint against the running server
```

### 4.13 PR Review Status

When working on a branch with an open pull request, Claude Code displays a clickable PR link in the footer (e.g., "PR #446") with a colored underline:

| Color | State |
|:------|:------|
| Green | Approved |
| Yellow | Pending review |
| Red | Changes requested |
| Gray | Draft |
| Purple | Merged |

`Cmd+click` (Mac) or `Ctrl+click` (Windows/Linux) opens the PR in your browser. Status updates automatically every 60 seconds. Requires the `gh` CLI to be installed and authenticated.

### 4.14 External Editor Integration

Press `Ctrl+G` (or `Ctrl+X Ctrl+E`) to open your current prompt in your default text editor (`$EDITOR` or `$VISUAL`). This is invaluable for composing complex, multi-paragraph prompts or pasting large blocks of context. When you save and close the editor, the content returns to the Claude Code prompt.

Enable "Show last response in external editor" in `/config` to also see Claude's previous reply as `#`-commented context above your prompt -- helpful for crafting precise follow-ups.

### 4.15 Voice Input

For hands-free operation, enable voice dictation in `/config`:

- Hold `Space` for push-to-talk dictation
- Transcript inserts at cursor position
- Rebindable to a different key

> **Try This**: Open Claude Code in a project, press `Ctrl+O` to open the transcript viewer, then ask Claude to do something that involves multiple tool calls (e.g., "find all files that import the auth module"). Watch the transcript viewer to see exactly which tools Claude uses and in what order. This is the best way to build intuition for how the agentic loop works in practice.

### 4.16 Key Takeaway

Interactive mode is a full-featured terminal application, not just a chat prompt. The combination of vim mode, multiline input, bash mode (`!`), file mentions (`@`), side questions (`/btw`), background tasks (`Ctrl+B`), and the transcript viewer (`Ctrl+O`) makes it a complete development environment. Investing time in learning these shortcuts pays off quickly -- especially `Shift+Tab` for permission modes, `Ctrl+B` for backgrounding, and `/btw` for quick lookups without losing context.

---

## References

1. **Claude Code Documentation**: [code.claude.com/docs](https://code.claude.com/docs/en/overview) -- Official documentation covering all features, setup, and configuration.
2. **Claude Code Overview**: [code.claude.com/docs/en/overview](https://code.claude.com/docs/en/overview) -- Product overview and installation guide.
3. **CLI Reference**: [code.claude.com/docs/en/cli-reference](https://code.claude.com/docs/en/cli-reference) -- Complete reference for all CLI commands and flags.
4. **Interactive Mode**: [code.claude.com/docs/en/interactive-mode](https://code.claude.com/docs/en/interactive-mode) -- Keyboard shortcuts, input modes, and interactive features.
5. **Permission Modes**: [code.claude.com/docs/en/permission-modes](https://code.claude.com/docs/en/permission-modes) -- Detailed guide to all six permission modes.
6. **Model Configuration**: [code.claude.com/docs/en/model-config](https://code.claude.com/docs/en/model-config) -- Model aliases, effort levels, and extended context.
7. **Memory System**: [code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory) -- CLAUDE.md files, auto memory, and project rules.
8. **Context Window**: [code.claude.com/docs/en/context-window](https://code.claude.com/docs/en/context-window) -- Interactive visualization of context window usage.
9. **Cost Management**: [code.claude.com/docs/en/costs](https://code.claude.com/docs/en/costs) -- Token tracking, team cost management, and optimization strategies.
10. **Advanced Setup**: [code.claude.com/docs/en/setup](https://code.claude.com/docs/en/setup) -- System requirements, platform installation, and binary integrity.

---

*Part 1 covers Chapters 1-4. Part 2 will continue with: Chapter 5 (Memory System: CLAUDE.md and Auto Memory), Chapter 6 (Custom Skills and Commands), Chapter 7 (Hooks: Lifecycle Automation), Chapter 8 (MCP Server Integrations), Chapter 9 (Sub-Agents and Agent Teams), and Chapter 10 (Putting It All Together: Real-World Workflows).*

---

# Part II: Core Concepts

# Chapter 5: Memory -- CLAUDE.md and Auto Memory

*What you will learn: how to give Claude persistent instructions across sessions and how Claude accumulates its own knowledge automatically.*

---

## 5.1 The Problem Memory Solves

Every Claude Code session starts with a fresh context window. Without memory, you would re-explain your project's build command, coding standards, file layout, and preferences every single time. Memory is the bridge between sessions.

> **Real-world analogy:** CLAUDE.md is the onboarding doc you would hand a new hire on day one. Auto Memory is the personal notebook that new hire keeps -- full of "gotchas I learned," "commands that work," and "things the team actually does versus what the wiki says."

---

## 5.2 Two Memory Systems

Claude Code has two complementary memory systems. Both load at the start of every conversation.

| Aspect | CLAUDE.md Files | Auto Memory |
|--------|----------------|-------------|
| **Who writes it** | You | Claude |
| **What it contains** | Instructions and rules | Learnings and patterns |
| **Scope** | Project, user, or org | Per working tree (git repo) |
| **Loaded into** | Every session | Every session (first 200 lines or 25 KB) |
| **Best for** | Coding standards, workflows, architecture | Build commands, debugging insights, discovered preferences |

Use CLAUDE.md when you want to **guide** Claude's behavior. Auto Memory lets Claude **learn** from your corrections without manual effort.

---

## 5.3 CLAUDE.md -- Locations and Scopes

CLAUDE.md files can live in several locations, each with a different reach. More specific locations take precedence.

| Scope | Location | Purpose | Shared with |
|-------|----------|---------|-------------|
| **Managed policy** | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`; Linux: `/etc/claude-code/CLAUDE.md` | Org-wide standards enforced by IT | All users in the organization |
| **Project** | `./CLAUDE.md` or `./.claude/CLAUDE.md` | Team-shared conventions checked into source control | Team members via git |
| **User** | `~/.claude/CLAUDE.md` | Personal preferences across all projects | Just you (all projects) |
| **Local** | `./CLAUDE.local.md` (add to `.gitignore`) | Personal project-specific overrides | Just you (this project) |

**How loading works:** Claude Code walks up the directory tree from your current working directory. If you run Claude in `foo/bar/`, it loads CLAUDE.md from `foo/bar/`, then `foo/`, and so on up to the root. Within each directory, `CLAUDE.local.md` is appended after `CLAUDE.md`, so your personal notes are the last thing Claude reads at that level.

CLAUDE.md files in **subdirectories** do not load at startup. They load on demand when Claude reads files in those subdirectories.

---

## 5.4 Writing Effective CLAUDE.md

The golden rules:

1. **Keep it under 200 lines.** Longer files consume more context and reduce adherence. If it grows, split it.
2. **Be specific and verifiable.** Claude follows concrete instructions far more reliably than vague ones.
3. **Use markdown structure.** Headers and bullet points help Claude parse the document the same way humans do.
4. **Avoid contradictions.** If two rules conflict, Claude picks one arbitrarily. Audit periodically.

```markdown
# Bad -- vague, unverifiable
- Format code properly
- Test your changes
- Keep files organized

# Good -- specific, actionable
- Use 2-space indentation in all TypeScript files
- Run `npm test` before committing; all tests must pass
- API handlers live in `src/api/handlers/`; one file per resource
- Use named exports, not default exports
```

### Import Additional Files

Use `@path/to/file` syntax anywhere in a CLAUDE.md to pull in external content:

```markdown
See @README.md for project overview and @package.json for available npm commands.

# Additional Instructions
- Git workflow: @docs/git-instructions.md
```

Relative paths resolve relative to the file containing the import. Imports can be recursive (up to five levels deep).

### AGENTS.md Compatibility

If your repo already has an `AGENTS.md` for other coding agents, create a CLAUDE.md that imports it:

```markdown
@AGENTS.md

## Claude-Specific
Use plan mode for changes under `src/billing/`.
```

---

## 5.5 Modular Rules with `.claude/rules/`

For larger projects, break instructions into topic-specific files:

```
your-project/
+-- .claude/
|   +-- CLAUDE.md               # Main project instructions
|   +-- rules/
|       +-- code-style.md       # Code style guidelines
|       +-- testing.md          # Testing conventions
|       +-- api-conventions.md  # API design rules
|       +-- security.md         # Security requirements
```

Rules without `paths` frontmatter load at startup with the same priority as `.claude/CLAUDE.md`.

### Path-Specific Rules

Scope rules to particular files using YAML frontmatter:

```markdown
---
paths:
  - "src/api/**/*.ts"
---

# API Development Rules

- All API endpoints must include input validation
- Use the standard error response format from `src/api/errors.ts`
- Include OpenAPI documentation comments
```

These conditional rules **only load when Claude reads files matching the pattern**, saving context space and reducing noise.

| Pattern | Matches |
|---------|---------|
| `**/*.ts` | All TypeScript files in any directory |
| `src/**/*` | All files under `src/` |
| `*.md` | Markdown files in the project root only |
| `src/components/*.tsx` | React components in one specific directory |

---

## 5.6 Auto Memory

Auto Memory lets Claude accumulate knowledge across sessions without you writing anything. Claude saves notes -- build commands, debugging insights, code style preferences -- when it discovers information that would be useful in a future conversation.

### Storage

Each project gets its own directory at `~/.claude/projects/<project>/memory/`:

```
~/.claude/projects/<project>/memory/
+-- MEMORY.md          # Concise index loaded every session
+-- debugging.md       # Detailed notes on debugging patterns
+-- api-conventions.md # API design decisions
+-- ...
```

The first **200 lines** (or 25 KB, whichever comes first) of `MEMORY.md` are loaded at the start of every session. Topic files like `debugging.md` load on demand -- Claude reads them when it needs the information.

### Controlling Auto Memory

- **Toggle on/off:** Open `/memory` in a session, or set `"autoMemoryEnabled": false` in project settings.
- **Browse and edit:** Run `/memory` to see all loaded files; select any file to open it in your editor.
- **Direct Claude:** Say "remember that the API tests require a local Redis instance" and Claude saves it to auto memory. Say "add this to CLAUDE.md" if you want it in the instruction file instead.

---

## 5.7 The `/init` Command

Run `/init` to auto-generate a starter CLAUDE.md. Claude analyzes your codebase and creates a file with build commands, test instructions, and project conventions it discovers. If a CLAUDE.md already exists, `/init` suggests improvements rather than overwriting it.

Set `CLAUDE_CODE_NEW_INIT=1` for an interactive multi-phase flow that asks which artifacts to set up (CLAUDE.md files, skills, hooks), explores your codebase with a sub-agent, and presents a reviewable proposal before writing anything.

---

## 5.8 Real-World Example: A React Project CLAUDE.md

```markdown
# Acme Dashboard -- Project Instructions

## Build & Test
- `pnpm install` to set up dependencies
- `pnpm dev` starts the dev server on port 3000
- `pnpm test` runs Vitest; all tests must pass before committing
- `pnpm lint` runs ESLint + Prettier checks

## Code Conventions
- Use TypeScript strict mode; no `any` types
- Use 2-space indentation
- React components: functional with hooks, no class components
- Named exports only (`export function Foo`, not `export default`)
- CSS: Tailwind utility classes; no inline styles, no CSS modules

## File Layout
- `src/components/` -- reusable UI components, one per file
- `src/pages/` -- route-level pages
- `src/api/` -- API client functions (one file per resource)
- `src/hooks/` -- custom React hooks
- `src/utils/` -- pure utility functions with unit tests

## Git
- Branch from `main`, use `feat/`, `fix/`, `chore/` prefixes
- Squash-merge PRs; write conventional commit messages
- Never force-push to `main`
```

---

> ### Try This
>
> 1. Run `/init` in one of your projects. Read the generated CLAUDE.md and refine it.
> 2. Create a `.claude/rules/testing.md` with a `paths:` frontmatter scoped to your test files. Add a rule like "Always use `describe`/`it` blocks, never standalone `test()`."
> 3. Ask Claude a question, then correct it. Check `~/.claude/projects/<project>/memory/MEMORY.md` to see if Claude remembered your correction.

---

> **Key Takeaway:** Memory is the difference between Claude as a stateless chatbot and Claude as a team member who knows your project. Invest 30 minutes writing a good CLAUDE.md, and every future session starts smarter. Let Auto Memory handle the rest.

---

# Chapter 6: Context Window Management

*What you will learn: how Claude's working memory fills up during a session, what consumes space, and how to manage it so Claude stays sharp throughout long tasks.*

---

## 6.1 What Is the Context Window?

The context window is Claude's working memory for a single session. Everything Claude knows right now -- your instructions, the files it has read, its own responses, tool outputs, and invisible system content -- lives here. The default window is **200,000 tokens** (roughly 150,000 words). Extended thinking models can use up to 1,000,000 tokens.

> **Real-world analogy:** The context window is your desk. Everything Claude reads goes on the desk. When it fills up, older papers get filed away (compacted) to make room. The desk has a fixed size, so what you put on it matters.

---

## 6.2 What Loads at Startup

Before you type a single character, Claude Code has already consumed roughly 7,000-8,000 tokens:

| Component | Approx. Tokens | Notes |
|-----------|----------------|-------|
| System prompt | ~4,200 | Core instructions for behavior, tool use, response formatting. Invisible to you. |
| Auto memory (MEMORY.md) | ~680 | Claude's notes from previous sessions. First 200 lines or 25 KB. |
| Environment info | ~280 | Working directory, platform, shell, OS version, git status. |
| MCP tools (deferred) | ~120 | Tool names only. Full schemas load on demand when Claude needs them. |
| Skill descriptions | ~450 | One-line descriptions so Claude knows what skills exist. NOT re-injected after compaction. |
| `~/.claude/CLAUDE.md` | ~320 | Your global personal preferences. |
| Project CLAUDE.md | ~1,800 | Varies widely by project. This is the most important file you can create. |

**That leaves roughly 192,000 tokens for actual work** -- which sounds like a lot until Claude starts reading files.

---

## 6.3 How Files Consume Context

Every file Claude reads adds its **full content** to the context window. A typical source file is 500-3,000 tokens. Read ten files and you have consumed 5,000-30,000 tokens.

```
Session start:         ████░░░░░░░░░░░░░░░░  ~8K tokens (startup)
After reading 5 files: ████████░░░░░░░░░░░░  ~20K tokens
After 20 tool calls:   ████████████████░░░░  ~80K tokens
Getting full:          ██████████████████░░  ~170K tokens -- compaction soon
```

Path-scoped rules also consume context. When Claude reads a file matching a rule's `paths:` pattern, that rule's content silently enters context.

**Tip:** Be specific in your prompts. "Fix the bug in `src/auth/login.ts`" makes Claude read one file. "Fix the login bug" might make Claude read ten files searching for it.

---

## 6.4 Auto-Compaction

When the context window reaches approximately **95% capacity**, Claude Code triggers auto-compaction:

1. A summarization model reads the full conversation.
2. It produces a structured summary preserving: your requests and intent, key technical concepts, files examined or modified, errors and how they were fixed, pending tasks.
3. The summary **replaces** the original conversation messages.
4. Startup content is re-injected from disk.

The summary is typically about **12% the size** of the original conversation. A session that was using 170K tokens might drop to 25-30K tokens after compaction.

### What Survives Compaction

This is critical to understand:

| Mechanism | After Compaction |
|-----------|-----------------|
| System prompt and output style | Unchanged (not part of message history) |
| Project-root CLAUDE.md and unscoped rules | Re-injected from disk |
| Auto memory (MEMORY.md) | Re-injected from disk |
| Rules with `paths:` frontmatter | **Lost** until a matching file is read again |
| Nested CLAUDE.md in subdirectories | **Lost** until a file in that subdirectory is read again |
| Invoked skill bodies | Re-injected (capped at 5,000 tokens per skill, 25,000 total; oldest dropped first) |
| Skill descriptions listing | **NOT** re-injected. Only skills you actually invoked are preserved. |
| Hooks | Not applicable (hooks run as code, not as context) |

**This is why persistent rules belong in CLAUDE.md**, not in conversation messages. Instructions you typed in chat will be summarized away.

---

## 6.5 Manual Compaction: `/compact`

You do not have to wait for auto-compaction. Run `/compact` at any time to summarize the conversation so far. You can add a focus hint:

```
/compact focus on the API refactoring changes
```

This tells the summarizer to prioritize retaining information about the API refactoring in the compressed output.

### Targeted Summarization: Esc+Esc

Press `Esc` twice to open the rewind menu, then select a message and choose **"Summarize from here."** This keeps all messages before the selected point in full detail and only compresses everything after it. This is more surgical than `/compact`, which summarizes the entire conversation.

---

## 6.6 Other Context Management Tools

### `/context` -- Live Visualization

Run `/context` for a live breakdown of what is consuming your context window, categorized by type, with optimization suggestions. This is your diagnostic tool when things feel "slow" or Claude starts forgetting instructions.

### `/clear` -- Fresh Start

Run `/clear` to wipe the conversation and start a new session in the same terminal. Use this between unrelated tasks. The previous session is preserved and can be resumed with `/resume`.

### `/btw` -- Zero-Context Side Questions

Use `/btw` to ask a quick question without adding to conversation history:

```
/btw what was the name of that config file again?
```

The question and answer appear in a dismissible overlay and never enter the context window. Works even while Claude is processing a response. No tool access -- Claude can only answer from what is already in context.

### Sub-Agents for Context Isolation

When Claude needs to research something that requires reading many files, delegate to a sub-agent. The sub-agent gets its own fresh context window. It can read dozens of files without consuming a single token of your main session's context. Only the final summary (typically 200-500 tokens) returns to your window.

```
Use a subagent to research how session timeout handling works in this codebase
```

Think of it this way: `/btw` sees your full conversation but has no tools. A sub-agent has full tools but starts with an empty context. Use `/btw` for what Claude already knows; use a sub-agent to go find out something new.

---

## 6.7 Real-World Example: A Debugging Session

Here is how context management plays out in practice:

```
[Session Start]                                ~8K tokens
You: "Debug why /api/orders returns 500"       ~8K tokens
Claude reads: routes.ts, orders.ts, db.ts      ~15K tokens
Claude reads: middleware.ts, auth.ts            ~22K tokens
Claude runs: npm test (output)                  ~28K tokens
Claude explains the bug, proposes fix           ~30K tokens

You: "Try that fix"
Claude edits orders.ts, runs tests              ~38K tokens
Tests fail, Claude reads error logs             ~45K tokens
Claude tries a different approach               ~55K tokens

You: "Also fix the related issue in /api/users"
Claude reads: users.ts, user-service.ts         ~65K tokens
Claude reads: 5 more related files              ~85K tokens
                                                -- getting full --

You: /compact focus on the orders and users API fixes
[Context drops from ~85K to ~15K tokens]

You: "Now write tests for both fixes"
Claude works with fresh context space           ~35K tokens
```

**When to use what:**

| Situation | Action |
|-----------|--------|
| Starting an unrelated task | `/clear` |
| Context getting full mid-task | `/compact` with a focus hint |
| Need a quick answer about current work | `/btw your question` |
| Need Claude to research something large | Ask Claude to use a sub-agent |
| Want to keep early context, compress recent work | `Esc+Esc` then "Summarize from here" |

---

> ### Try This
>
> 1. Start a session and run `/context` immediately. Note the startup token usage.
> 2. Ask Claude to read 5 files, then run `/context` again. Compare the numbers.
> 3. Run `/compact` and check `/context` a third time. See how much space was freed.
> 4. Try `/btw how many tokens am I using?` -- notice it does not add to your context.

---

> **Key Takeaway:** Context is your most precious resource. Every file read, every tool output, every conversation turn consumes it. Be deliberate: use `/compact` before context runs low, delegate large research to sub-agents, and run `/clear` between unrelated tasks. The developers who get the most out of Claude Code are the ones who manage context like a budget.

---

# Chapter 7: Permissions and Security

*What you will learn: how to control what Claude can and cannot do, from conservative read-only mode to fully autonomous execution, and how OS-level sandboxing provides defense in depth.*

---

## 7.1 Why Permissions Matter

Claude Code runs real commands on your real machine. It can edit files, run shell scripts, make network requests, and interact with external services. The permission system ensures you stay in control of what actually executes.

> **Real-world analogy:** Permission modes are like security clearance levels at a building. `default` is a visitor badge -- you can look around but need an escort to touch anything. `acceptEdits` is a contractor badge -- you can work on the building but someone checks your plans. `auto` is a full-time employee badge -- you move freely with security cameras watching. `bypassPermissions` is the building owner's master key -- use it only when you are the only person in the building.

---

## 7.2 Permission Modes

| Mode | What Runs Without Asking | Best For |
|------|-------------------------|----------|
| `default` | Reads only | Getting started, sensitive work |
| `acceptEdits` | Reads + file edits + filesystem commands (`mkdir`, `touch`, `mv`, `cp`, etc.) | Active coding with post-hoc review |
| `plan` | Reads only (Claude proposes changes but does not execute them) | Safe exploration, architecture review |
| `auto` | Everything, with background safety classifier checks | Long unattended tasks, reducing prompt fatigue |
| `dontAsk` | Only pre-approved tools (everything else auto-denied) | Locked-down CI pipelines |
| `bypassPermissions` | Everything except protected paths | Isolated containers and VMs **only** |

### Switching Modes

**During a session:** Press `Shift+Tab` to cycle through `default` -> `acceptEdits` -> `plan` (and `auto`/`bypassPermissions` if enabled).

**At startup:**

```bash
claude --permission-mode plan
```

**As a persistent default (in settings):**

```json
{
  "permissions": {
    "defaultMode": "acceptEdits"
  }
}
```

### Protected Paths

Regardless of mode, writes to these paths **always** require confirmation:

- `.git`, `.vscode`, `.idea`, `.husky`
- `.claude` (except `.claude/commands`, `.claude/agents`, `.claude/skills`, `.claude/worktrees`)
- Shell config files: `.bashrc`, `.zshrc`, `.profile`, etc.
- `.gitconfig`, `.gitmodules`

---

## 7.3 Permission Rules Syntax

Fine-grained rules use the format `Tool` or `Tool(specifier)`:

| Rule | Effect |
|------|--------|
| `Bash` | Matches all Bash commands |
| `Bash(npm run build)` | Matches the exact command `npm run build` |
| `Bash(npm run *)` | Matches any command starting with `npm run ` |
| `Bash(git commit *)` | Matches git commit with any arguments |
| `Read(./.env)` | Matches reading the `.env` file |
| `Edit(/src/**/*.ts)` | Matches editing TypeScript files under `src/` |
| `WebFetch(domain:example.com)` | Matches fetch requests to example.com |
| `mcp__puppeteer__puppeteer_navigate` | Matches a specific MCP tool |

Rules are evaluated in order: **deny -> ask -> allow**. The first matching rule wins. Deny rules always take precedence.

### Example Settings Configuration

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run *)",
      "Bash(git commit *)",
      "Bash(git status *)",
      "Bash(* --version)",
      "Bash(* --help *)"
    ],
    "deny": [
      "Bash(git push --force *)",
      "Bash(rm -rf *)",
      "Read(./.env.production)"
    ]
  }
}
```

---

## 7.4 Settings Files Hierarchy

Permission rules (and all settings) follow a strict precedence. Higher levels cannot be overridden by lower ones:

| Priority | Source | Location |
|----------|--------|----------|
| 1 (highest) | Managed settings | OS-level policy files (deployed by IT) |
| 2 | CLI arguments | `--permission-mode`, `--allowedTools`, etc. |
| 3 | Local project | `.claude/settings.local.json` |
| 4 | Shared project | `.claude/settings.json` |
| 5 (lowest) | User | `~/.claude/settings.json` |

If a tool is denied at any level, no lower level can allow it. A managed settings deny cannot be overridden by `--allowedTools`.

---

## 7.5 Sandboxing: OS-Level Isolation

Permissions control what Claude **decides** to do. Sandboxing controls what Claude's commands **can physically access**, enforced by the operating system.

### Filesystem Isolation

- **Default writes:** Read/write access to the current working directory and subdirectories only.
- **Default reads:** Read access to the entire filesystem (useful for system libraries and dependencies).
- **Enforcement:** macOS uses **Seatbelt**; Linux uses **bubblewrap**. All child processes inherit the same restrictions.

### Network Isolation

Network access is controlled through a proxy server running **outside** the sandbox:

- Only approved domains can be accessed.
- New domain requests trigger permission prompts.
- Applies to all scripts, programs, and subprocesses.

### Enable Sandboxing

```
/sandbox
```

This opens a menu where you choose between:

1. **Auto-allow mode:** Sandboxed Bash commands run without prompts. Commands that need access outside the sandbox fall back to the regular permission flow.
2. **Regular permissions mode:** All Bash commands go through standard permission prompts, even when sandboxed.

### Configure Sandbox Paths

```json
{
  "sandbox": {
    "enabled": true,
    "filesystem": {
      "allowWrite": ["~/.kube", "/tmp/build"],
      "denyRead": ["~/"],
      "allowRead": ["."]
    }
  }
}
```

---

## 7.6 Auto Mode: The Background Safety Classifier

`auto` mode is the most sophisticated permission mode. A separate classifier model reviews every action before it runs, blocking anything that:

- Escalates beyond your request (e.g., you asked to fix a bug, Claude tries to deploy)
- Targets unrecognized infrastructure (pushing to unknown repos, writing to unknown cloud buckets)
- Appears driven by hostile content Claude read (prompt injection defense)

**Blocked by default in auto mode:**

- `curl | bash` patterns (download-and-execute)
- Sending sensitive data to external endpoints
- Production deploys and database migrations
- Force push or pushing directly to `main`
- Mass deletion, IAM permission grants

**Allowed by default:**

- Local file operations in working directory
- Installing declared dependencies
- Read-only HTTP requests
- Pushing to the current branch

If the classifier blocks an action 3 times consecutively or 20 times total, auto mode pauses and resumes normal prompting.

---

## 7.7 Real-World Example: CI Pipeline Permissions

Setting up Claude Code for a CI pipeline that runs automated code review:

```json
{
  "permissions": {
    "defaultMode": "dontAsk",
    "allow": [
      "Read",
      "Bash(npm run lint *)",
      "Bash(npm run test *)",
      "Bash(git diff *)",
      "Bash(git log *)",
      "Bash(gh pr comment *)"
    ],
    "deny": [
      "Edit",
      "Write",
      "Bash(git push *)",
      "Bash(git commit *)",
      "Bash(rm *)",
      "Bash(curl *)",
      "Bash(wget *)"
    ]
  }
}
```

This configuration:
- Uses `dontAsk` mode so no human is needed for prompts
- Allows reading files, running lint/test, viewing git history
- Allows posting PR comments via the GitHub CLI
- Denies all file modifications, pushes, commits, and network tools
- Any tool not explicitly allowed is automatically denied by `dontAsk`

---

> ### Try This
>
> 1. Start Claude Code and press `Shift+Tab` three times. Watch the mode indicator cycle through `default` -> `acceptEdits` -> `plan`.
> 2. Run `/sandbox` and enable auto-allow mode. Ask Claude to run `ls /etc/` (allowed read) and then `touch /etc/test` (blocked write). Observe the difference.
> 3. Add `"Bash(npm test *)"` to your project's `.claude/settings.json` allow list. Notice that `npm test` no longer prompts for permission.

---

> **Key Takeaway:** Layer your defenses. Permission modes set the baseline. Permission rules fine-tune specific tools. Sandboxing enforces OS-level boundaries that no amount of prompt injection can bypass. For solo development, `acceptEdits` with sandbox is the sweet spot. For CI, use `dontAsk` with explicit allow/deny lists. Reserve `bypassPermissions` for throwaway containers.

---

# Chapter 8: Checkpointing -- Undo Anything

*What you will learn: how Claude Code's automatic checkpoint system lets you safely experiment with code changes and rewind when things go wrong.*

---

## 8.1 The Safety Net

Every time you send a prompt, Claude Code quietly snapshots the state of every file it is about to edit. This happens automatically -- no configuration, no commands, no git staging. If Claude breaks something, you rewind. If you want to try two approaches, you rewind between them. The checkpoint system turns risky experiments into safe ones.

> **Real-world analogy:** Checkpoints are like save points in a video game. You are about to fight the boss (refactor the auth system). Save first. If you die (tests break horribly), reload your save and try a different strategy. No progress is permanently lost.

---

## 8.2 How Checkpoints Work

### Automatic Tracking

- **Every user prompt** creates a new checkpoint automatically.
- Claude Code tracks all changes made by its **file editing tools** (Read, Edit, Write).
- Checkpoints **persist across sessions** -- you can access them in resumed conversations.
- Automatically **cleaned up after 30 days** (configurable).

### What Gets Tracked

Checkpoints cover **file edits made through Claude's built-in tools**. This includes:

- Files created by Claude
- Files edited by Claude
- Files deleted by Claude's file tools

### What Does NOT Get Tracked

Checkpoints do **not** cover:

- **Bash command side effects:** `rm file.txt`, `mv old.txt new.txt`, `sed -i 's/foo/bar/' file.txt` -- these are invisible to the checkpoint system.
- **External edits:** Changes you make manually in your editor while Claude is running.
- **Remote side effects:** Database writes, API calls, deployments, git pushes -- anything that affects systems outside your local filesystem.

This is why Claude asks before running commands with external side effects and why `bypassPermissions` mode should only be used in disposable environments.

---

## 8.3 The Rewind Menu

Press `Esc` twice (`Esc+Esc`) or run `/rewind` to open the rewind menu. You see a scrollable list of every prompt from the session. Select one and choose an action:

| Action | What It Does |
|--------|-------------|
| **Restore code + conversation** | Full rewind: reverts files AND conversation to that exact point. As if everything after never happened. |
| **Restore conversation only** | Rewinds the conversation to that message but keeps your current code on disk unchanged. Useful when Claude went down a rabbit hole but the code is fine. |
| **Restore code only** | Reverts files to that point but keeps the full conversation. Useful when the code is broken but the conversation has valuable context. |
| **Summarize from here** | Keeps all messages before this point in full detail; compresses everything after into a summary. Frees context space without losing information. |
| **Never mind** | Returns to the message list. |

After restoring conversation or summarizing, the original prompt from the selected message is restored into the input field so you can re-send or edit it.

---

## 8.4 VS Code Integration

In VS Code, checkpoints integrate with the editor's UI:

- **Hover over any message** in the Claude Code panel to reveal rewind buttons.
- **Fork:** Create a new session branch from that point (preserves the original session).
- **Rewind code:** Revert files to that checkpoint while keeping the conversation.
- **Fork + Rewind:** Create a new branch AND revert code -- the safest way to try alternatives.

---

## 8.5 Checkpoints vs. Git

Checkpoints and git serve different purposes and complement each other:

| Aspect | Checkpoints | Git |
|--------|------------|-----|
| **Scope** | Single session, local only | Permanent, shared history |
| **Granularity** | Every prompt (dozens per session) | Every commit (intentional saves) |
| **What's tracked** | File edits by Claude's tools | All staged changes |
| **Persistence** | 30 days | Forever |
| **Collaboration** | Just you | Entire team |
| **Recovery** | Instant rewind in session | `git checkout`, `git revert` |

**Best practice workflow:**

1. Start a session -- checkpoints begin automatically.
2. Claude makes changes -- experiment freely.
3. If something breaks -- rewind with `Esc+Esc`.
4. When things work -- commit with git.
5. Start the next task -- checkpoints cover the new work.

Think of checkpoints as "local undo" and git as "permanent history."

---

## 8.6 Real-World Example: Trying Two Approaches to a Refactor

You need to refactor the authentication system. There are two plausible approaches: extracting a middleware layer versus using a decorator pattern. Here is how checkpoints let you try both safely:

```
[Session Start -- Checkpoint 0 (automatic)]

You: "Refactor the auth system to use a middleware pattern.
      Extract auth logic from each route handler into middleware."

Claude edits 8 files, creates 2 new files.

[Checkpoint 1 created automatically]

You run tests: 3 failures.

You: "Fix those test failures."

Claude edits 3 more files.

[Checkpoint 2 created]

You run tests: all pass, but the code feels over-engineered.

  ------- Decision point: try the other approach -------

Press Esc+Esc -> select Checkpoint 0 -> "Restore code + conversation"

  All 10 file changes are reverted. Conversation rewinds to start.

You: "Refactor the auth system using a decorator pattern instead.
      Each route handler should be wrapped with an @authenticate decorator."

Claude takes a completely different approach, edits 5 files.

[Checkpoint 3 created]

You run tests: all pass. Code is cleaner.

You: "This is the approach I want. Let me commit this."
```

You explored two fundamentally different designs in the same session without touching git, without stashing, without creating branches. The checkpoint system made it trivial.

---

## 8.7 Tips for Effective Checkpointing

1. **Commit before big refactors.** Checkpoints are great for session-level recovery, but a git commit before starting gives you a permanent safety net.
2. **Be careful with Bash commands.** If you ask Claude to `rm -rf node_modules` and then rewind, `node_modules` stays deleted. Only file-tool edits are reversible.
3. **Use "Restore code only" when debugging.** If Claude's analysis was good but the fix was wrong, keep the conversation (it has valuable context about the bug) and just revert the code.
4. **Use "Summarize from here" to free context.** If you spent 50 messages debugging and found the fix, summarize the debugging from the midpoint forward. Keep your initial instructions intact, compress the verbose back-and-forth.
5. **Fork sessions for parallel exploration.** When you want to preserve the original session completely (not just the code state), use `claude --continue --fork-session` to create a new session branch.

---

> ### Try This
>
> 1. Ask Claude to make a significant edit to a file (e.g., "Rewrite this function to use async/await").
> 2. Press `Esc+Esc` to open the rewind menu. Explore the options -- try "Restore code only" to revert the file while keeping the conversation.
> 3. Now ask Claude to try a different approach. The conversation still has the context of what you tried before, but the code is back to its original state.
> 4. When you like the result, commit with git for permanent history.

---

> **Key Takeaway:** Checkpoints remove the fear from experimentation. With automatic snapshots on every prompt, you can ask Claude to try anything -- aggressive refactors, risky optimizations, complete rewrites -- knowing that reverting is two keypresses away. The developers who get the most out of Claude Code are the ones who are not afraid to say "try it" because they know they can always say "undo."

---

## References

- [Claude Code Memory Documentation](https://code.claude.com/docs/en/memory)
- [Claude Code Context Window](https://code.claude.com/docs/en/context-window)
- [Claude Code Permissions](https://code.claude.com/docs/en/permissions)
- [Claude Code Permission Modes](https://code.claude.com/docs/en/permission-modes)
- [Claude Code Sandboxing](https://code.claude.com/docs/en/sandboxing)
- [Claude Code Security](https://code.claude.com/docs/en/security)
- [Claude Code Checkpointing](https://code.claude.com/docs/en/checkpointing)
- [Claude Code Interactive Mode](https://code.claude.com/docs/en/interactive-mode)
- [Claude Code How It Works](https://code.claude.com/docs/en/how-claude-code-works)
- [Anthropic Trust Center](https://trust.anthropic.com)

---

# Part III: Extensibility

# Chapter 9: Skills -- Reusable Workflows & Knowledge

**Skills are prompt playbooks that load into Claude Code on demand, giving it specialized knowledge or step-by-step workflows without cluttering every session.**

## 9.1 What Is a Skill?

Think of skills like recipe cards in a kitchen. A chef does not memorize every recipe -- they pull the card when they need it. Skills work the same way: a `SKILL.md` file contains instructions that Claude loads only when relevant, keeping your context window lean the rest of the time.

A skill is a directory containing a `SKILL.md` file (required) plus optional supporting files:

```
fix-issue/
  SKILL.md           # Main instructions (required)
  template.md        # Template for Claude to fill in
  examples/
    sample.md        # Example output
  scripts/
    validate.sh      # Script Claude can execute
```

## 9.2 Where Skills Live

Where you store a skill determines who can use it:

| Location | Path | Applies To |
|----------|------|------------|
| Enterprise | Managed settings directory | All users in your organization |
| Personal | `~/.claude/skills/<skill-name>/SKILL.md` | All your projects |
| Project | `.claude/skills/<skill-name>/SKILL.md` | This project only |
| Plugin | `<plugin>/skills/<skill-name>/SKILL.md` | Where the plugin is enabled |

When multiple skills share the same name, higher-priority locations win: enterprise > personal > project. Plugin skills use a `plugin-name:skill-name` namespace, so they never conflict with other levels.

Claude Code watches skill directories for file changes. Edits take effect within the current session without restarting. In monorepo setups, skills in `packages/frontend/.claude/skills/` are automatically discovered when you work on files in that subdirectory.

## 9.3 Anatomy of a SKILL.md

Every skill has two parts: YAML frontmatter (between `---` markers) and markdown content.

```yaml
---
name: fix-issue
description: Fix a GitHub issue by number. Use when asked to fix, resolve, or address a GitHub issue.
disable-model-invocation: true
allowed-tools: Bash(git add *) Bash(git commit *) Bash(gh *)
---

Fix GitHub issue $ARGUMENTS following our coding standards.

1. Read the issue with `gh issue view $ARGUMENTS`
2. Find the relevant code using Grep and Glob
3. Implement the fix
4. Write or update tests
5. Run the test suite
6. Create a commit with a descriptive message
7. Open a PR linking the issue
```

### Frontmatter Reference

| Field | Required | Description |
|-------|----------|-------------|
| `name` | No | Display name (defaults to directory name). Lowercase, hyphens, max 64 chars. |
| `description` | Recommended | What the skill does. Claude uses this to decide when to load it. Truncated at 1,536 chars. |
| `disable-model-invocation` | No | `true` = only the user can invoke. Default: `false`. |
| `user-invocable` | No | `false` = hidden from `/` menu, only Claude invokes. Default: `true`. |
| `allowed-tools` | No | Tools Claude can use without permission prompts while the skill is active. |
| `model` | No | Override the session model while this skill runs. |
| `effort` | No | Override effort level: `low`, `medium`, `high`, `xhigh`, `max`. |
| `context` | No | Set to `fork` to run in an isolated sub-agent context. |
| `agent` | No | Which sub-agent type to use when `context: fork` is set. |
| `paths` | No | Glob patterns limiting auto-activation to matching files. |
| `hooks` | No | Hooks scoped to this skill's lifecycle. |
| `shell` | No | `bash` (default) or `powershell` for inline shell commands. |

## 9.4 Invocation: User vs. Claude

There are two ways a skill gets loaded:

1. **You type it**: `/fix-issue 1234` -- you explicitly invoke the skill.
2. **Claude auto-loads it**: You say "fix the bug in issue 1234" and Claude matches the description to your request.

Two frontmatter fields control this behavior:

| Setting | You Invoke | Claude Invokes | When Loaded Into Context |
|---------|-----------|---------------|--------------------------|
| (default) | Yes | Yes | Description always visible; full content loads on invoke |
| `disable-model-invocation: true` | Yes | No | Description hidden; full content loads only when you invoke |
| `user-invocable: false` | No | Yes | Description always visible; full content loads when Claude invokes |

**Real-world analogy**: `disable-model-invocation: true` is like a fire alarm pull station -- only a human should trigger a deployment. `user-invocable: false` is like background knowledge a doctor carries -- you would not run `/medical-school` as a command, but the knowledge is there when the doctor needs it.

## 9.5 $ARGUMENTS Substitution

When you run `/fix-issue 1234`, the string `1234` replaces every `$ARGUMENTS` placeholder in the skill content. You can also access individual arguments by index:

```yaml
---
name: migrate-component
description: Migrate a component from one framework to another
---

Migrate the $0 component from $1 to $2.
Preserve all existing behavior and tests.
```

Running `/migrate-component SearchBar React Vue` makes `$0` = `SearchBar`, `$1` = `React`, `$2` = `Vue`. Shell-style quoting works: `/my-skill "hello world" second` passes `"hello world"` as a single argument.

Other available substitutions include `${CLAUDE_SESSION_ID}` (current session ID) and `${CLAUDE_SKILL_DIR}` (directory containing the SKILL.md file).

## 9.6 Dynamic Context Injection

The `` !`command` `` syntax runs shell commands *before* the skill content reaches Claude. This is preprocessing, not something Claude executes.

```yaml
---
name: pr-summary
description: Summarize changes in a pull request
context: fork
agent: Explore
---

## Pull request context
- PR diff: !`gh pr diff`
- PR comments: !`gh pr view --comments`
- Changed files: !`gh pr diff --name-only`

## Your task
Summarize this pull request concisely.
```

When this skill runs: (1) each `` !`command` `` executes immediately, (2) its output replaces the placeholder, (3) Claude receives the fully-rendered prompt with actual PR data. For multi-line commands, use a fenced code block opened with ` ```! `.

## 9.7 Pre-Approving Tools

The `allowed-tools` field grants automatic permission for listed tools while the skill is active. It does not *restrict* tools -- every tool remains callable. Your permission settings still govern tools not listed.

```yaml
---
name: commit
description: Stage and commit the current changes
disable-model-invocation: true
allowed-tools: Bash(git add *) Bash(git commit *) Bash(git status *)
---
```

## 9.8 Running Skills in Sub-agents

Add `context: fork` to run a skill in isolation. The skill content becomes the prompt that drives the sub-agent. It does not have access to your conversation history.

```yaml
---
name: deep-research
description: Research a topic thoroughly
context: fork
agent: Explore
---

Research $ARGUMENTS thoroughly:
1. Find relevant files using Glob and Grep
2. Read and analyze the code
3. Summarize findings with specific file references
```

The `agent` field specifies which sub-agent configuration to use: built-in (`Explore`, `Plan`, `general-purpose`) or any custom sub-agent from `.claude/agents/`. If omitted, defaults to `general-purpose`.

## 9.9 Skill Content Lifecycle

Once invoked, the rendered `SKILL.md` content enters the conversation as a single message and stays there for the rest of the session. Claude Code does not re-read the file on later turns.

During auto-compaction, Claude Code re-attaches the most recent invocation of each skill, keeping the first 5,000 tokens of each. Re-attached skills share a combined budget of 25,000 tokens, filled starting from the most recently invoked skill. Older skills may be dropped entirely if you have invoked many in one session.

## 9.10 Skills vs. CLAUDE.md

| | CLAUDE.md | Skills |
|---|-----------|--------|
| **Loads when** | Every session, automatically | On demand (invoked or auto-matched) |
| **Best for** | Always-on rules, conventions, facts | Reference material, multi-step procedures |
| **Context cost** | Constant overhead | Near-zero until invoked |
| **Editability** | Watched for live changes | Watched for live changes |

**Rule of thumb**: if a section of CLAUDE.md has grown into a procedure rather than a fact, move it to a skill.

## 9.11 Real-World Example: The `/fix-issue` Skill

Here is a complete skill that reads a GitHub issue, finds the relevant code, implements a fix, runs tests, and creates a PR:

```yaml
---
name: fix-issue
description: Fix a GitHub issue by number. Reads the issue, finds code, implements a fix, runs tests, and creates a PR.
disable-model-invocation: true
allowed-tools: Bash(git *) Bash(gh *) Bash(npm test *) Read Grep Glob Edit Write
---

## Context
- Issue: !`gh issue view $ARGUMENTS --json title,body,labels`
- Repo structure: !`find . -name "*.ts" -not -path "*/node_modules/*" | head -30`

## Instructions
Fix GitHub issue #$ARGUMENTS:

1. **Understand**: Read the issue description above carefully
2. **Locate**: Find the relevant source files using Grep and Glob
3. **Implement**: Make the minimal fix that addresses the issue
4. **Test**: Run `npm test` and fix any failures
5. **Commit**: Stage changes and create a descriptive commit
6. **PR**: Run `gh pr create --title "Fix #$ARGUMENTS" --body "Closes #$ARGUMENTS"`
```

Usage: `/fix-issue 1234`

> **Try This**: Create a personal skill at `~/.claude/skills/explain-code/SKILL.md` with a description like "Explains code with visual diagrams and analogies." Test it by asking Claude "How does this code work?" and see if it auto-loads, then try invoking it directly with `/explain-code src/auth/login.ts`.

**Key Takeaway**: Skills are the bridge between one-off prompts and permanent CLAUDE.md rules. They load on demand, support argument passing and dynamic context injection, and can run in isolated sub-agents. If you keep pasting the same multi-step procedure into chat, it belongs in a skill.

---

# Chapter 10: Hooks -- Event-Driven Automation

**Hooks are shell commands, HTTP calls, prompt evaluations, or agent spawns that execute deterministically at specific lifecycle points in Claude Code.**

## 10.1 Why Hooks Exist

CLAUDE.md instructions are *advisory* -- Claude might follow them, might not. Hooks are *deterministic*: if you configure a `PostToolUse` hook to run Prettier after every file edit, it **will** run. Every time. No exceptions.

Think of hooks like Git hooks (`pre-commit`, `post-merge`) but for the entire Claude Code lifecycle. They fire at predictable points, receive structured input, and can block, modify, or enhance tool calls.

## 10.2 Lifecycle Events

Hooks are organized by how frequently they fire:

**Once per session:**

| Event | When It Fires |
|-------|--------------|
| `SessionStart` | Session begins (startup, resume, clear, compact) |
| `SessionEnd` | Session ends |

**Once per turn:**

| Event | When It Fires |
|-------|--------------|
| `UserPromptSubmit` | After you press Enter, before Claude processes your message |
| `Stop` | When Claude finishes responding |
| `StopFailure` | When Claude stops due to an error (rate limit, auth failure) |

**Every tool call:**

| Event | When It Fires |
|-------|--------------|
| `PreToolUse` | Before a tool executes (can block or modify) |
| `PostToolUse` | After successful tool execution |
| `PostToolUseFailure` | After a tool call fails |
| `PermissionRequest` | When a tool needs user approval |
| `PermissionDenied` | When a permission request is denied |

**Async events:**

| Event | When It Fires |
|-------|--------------|
| `Notification` | When Claude sends a notification (permission prompt, idle) |
| `SubagentStart` / `SubagentStop` | When a sub-agent begins or completes |
| `FileChanged` | When a watched file changes |
| `WorktreeCreate` / `WorktreeRemove` | When git worktrees are created or removed |
| `TaskCreated` / `TaskCompleted` | When agent team tasks change state |
| `TeammateIdle` | When an agent team teammate goes idle |
| `PreCompact` / `PostCompact` | Before and after context compaction |

## 10.3 The Four Handler Types

| Type | What It Does | Example Use |
|------|-------------|-------------|
| `command` | Runs a shell command with JSON input on stdin | Auto-format after file edit |
| `http` | POSTs JSON to a URL | Notify a webhook when Claude stops |
| `prompt` | Single-turn LLM yes/no evaluation | Smart filtering of tool calls |
| `agent` | Spawns a sub-agent for complex logic | Deep validation of generated code |

### Command handler example:

```json
{
  "type": "command",
  "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/format.sh",
  "timeout": 600
}
```

### HTTP handler example:

```json
{
  "type": "http",
  "url": "http://localhost:8080/hooks/post-tool-use",
  "headers": {
    "Authorization": "Bearer $MY_TOKEN"
  }
}
```

### Prompt handler example:

```json
{
  "type": "prompt",
  "prompt": "Is this command safe to run? $ARGUMENTS",
  "model": "claude-haiku"
}
```

## 10.4 Matcher Patterns

Matchers filter *when* hooks fire. They match differently depending on the event:

| Event | Matches On | Example |
|-------|-----------|---------|
| `PreToolUse`, `PostToolUse` | Tool name | `Bash`, `Edit\|Write`, `mcp__memory__.*` |
| `SessionStart` | Session source | `startup`, `resume`, `clear` |
| `Notification` | Notification type | `permission_prompt`, `idle_prompt` |
| `SubagentStart/Stop` | Agent type | `Explore`, `Plan` |
| `FileChanged` | Literal filenames | `.envrc\|.env` |

**Matching rules:**
- `"*"`, `""`, or omitted = match everything
- Letters/digits/`_`/`|` only = exact string or `|`-separated list (e.g., `"Edit|Write"`)
- Any other characters = treated as a JavaScript regex (e.g., `"mcp__.*__write.*"`)

## 10.5 Exit Codes and Output

Exit codes determine what happens after a hook runs:

| Exit Code | Meaning | Behavior |
|-----------|---------|----------|
| `0` | Success | Parse stdout for JSON; continue normally |
| `2` | Blocking error | Stderr is fed to Claude; action is blocked |
| Other | Non-blocking error | Stderr shown in transcript; action continues |

**What exit code 2 blocks, per event:**

| Event | What Gets Blocked |
|-------|-------------------|
| `PreToolUse` | The tool call is prevented entirely |
| `UserPromptSubmit` | Your prompt is erased |
| `Stop` | Claude continues (does not stop) |
| `PermissionRequest` | Permission is denied |
| `PostToolUse` | Error shown only (tool already ran) |

## 10.6 JSON Output Format

A hook that exits with code 0 can emit JSON to stdout for structured control:

```json
{
  "continue": true,
  "stopReason": "Build failed",
  "suppressOutput": false,
  "systemMessage": "Warning: lint errors detected"
}
```

For `PreToolUse` specifically, hooks can allow, deny, or modify tool inputs:

```json
{
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "permissionDecision": "deny",
    "permissionDecisionReason": "Destructive command blocked",
    "updatedInput": { "command": "safe alternative" },
    "additionalContext": "The user is on the production branch"
  }
}
```

The `permissionDecision` field accepts `allow`, `deny`, `ask` (show prompt to user), or `defer`.

## 10.7 Configuration Locations

| Location | Scope | Shareable |
|----------|-------|-----------|
| `~/.claude/settings.json` | All your projects | No |
| `.claude/settings.json` | This project | Yes (commit to repo) |
| `.claude/settings.local.json` | This project | No (gitignored) |
| Managed policy settings | Organization-wide | Yes (admin-deployed) |
| Plugin `hooks/hooks.json` | When plugin is enabled | Yes (bundled) |
| Skill/agent frontmatter | While skill/agent is active | Yes (component-scoped) |

## 10.8 Example: Block Dangerous Commands

This `PreToolUse` hook prevents `rm -rf` commands:

**`.claude/settings.json`:**
```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/block-rm.sh"
          }
        ]
      }
    ]
  }
}
```

**`.claude/hooks/block-rm.sh`:**
```bash
#!/bin/bash
COMMAND=$(jq -r '.tool_input.command')

if echo "$COMMAND" | grep -q 'rm -rf'; then
  jq -n '{
    hookSpecificOutput: {
      hookEventName: "PreToolUse",
      permissionDecision: "deny",
      permissionDecisionReason: "Destructive rm -rf command blocked by policy"
    }
  }'
else
  exit 0
fi
```

## 10.9 Example: Auto-Format After Every Edit

This `PostToolUse` hook runs Prettier after any file edit:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$(jq -r '.tool_input.file_path')\" 2>/dev/null || true"
          }
        ]
      }
    ]
  }
}
```

## 10.10 Example: Desktop Notifications

This `Notification` hook sends an OS notification when Claude needs your attention:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "permission_prompt",
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude needs your approval\" with title \"Claude Code\"'"
          }
        ]
      }
    ]
  }
}
```

## 10.11 Hooks vs. CLAUDE.md

```
CLAUDE.md:    "Please format code with Prettier"     --> Advisory (might be ignored)
Hook:         PostToolUse -> run prettier             --> Deterministic (always runs)
```

Use CLAUDE.md for *preferences*. Use hooks for *guarantees*.

> **Try This**: Add a `PostToolUse` hook to your `.claude/settings.json` that runs `eslint --fix` on any `.js` or `.ts` file after an `Edit` or `Write` tool call. Test it by asking Claude to create a file with intentional style issues and verify the hook auto-fixes them.

**Key Takeaway**: Hooks give you deterministic control over Claude Code's behavior at every lifecycle point. They are the enforcement mechanism that CLAUDE.md cannot be -- use them for formatting, security gates, notifications, and any workflow where "always" means always.

---

# Chapter 11: MCP -- Model Context Protocol

**MCP is an open standard that connects Claude Code to external data sources -- issue trackers, databases, monitoring tools -- so you stop copy-pasting data into chat.**

## 11.1 The Problem MCP Solves

Without MCP, your workflow looks like this:

```
You: *opens Jira* *copies issue description*
You: *pastes into Claude Code* "Fix this issue"
You: *opens Sentry* *copies stack trace*
You: *pastes into Claude Code* "Here's the error"
```

With MCP:

```
You: "Fix the bug described in JIRA-4521, check Sentry for the stack trace"
Claude: *reads Jira directly* *reads Sentry directly* *fixes the bug*
```

MCP is like USB for AI tools. Just as USB provides a standard interface for connecting peripherals to a computer, MCP provides a standard interface for connecting data sources to AI assistants.

## 11.2 Three Transport Types

| Type | Command | Best For |
|------|---------|----------|
| HTTP (recommended) | `claude mcp add --transport http <name> <url>` | Cloud services (Notion, Jira, Sentry, GitHub) |
| SSE (deprecated) | `claude mcp add --transport sse <name> <url>` | Legacy servers only |
| stdio | `claude mcp add <name> -- <command> [args]` | Local tools (database CLIs, file processors) |

### HTTP example (connecting to Notion):
```bash
claude mcp add --transport http notion https://mcp.notion.com/mcp
```

### stdio example (connecting to PostgreSQL):
```bash
claude mcp add --transport stdio db -- npx -y @bytebase/dbhub \
  --dsn "postgresql://readonly:pass@prod.db.com:5432/analytics"
```

## 11.3 Installation Scopes

| Scope | Loads In | Shared With Team | Stored In |
|-------|---------|-----------------|-----------|
| Local (default) | Current project only | No | `~/.claude.json` |
| Project | Current project only | Yes, via version control | `.mcp.json` in project root |
| User | All your projects | No | `~/.claude.json` |

```bash
# Local scope (default)
claude mcp add --transport http stripe https://mcp.stripe.com

# Project scope (shared via .mcp.json)
claude mcp add --transport http stripe --scope project https://mcp.stripe.com

# User scope (available everywhere)
claude mcp add --transport http hubspot --scope user https://mcp.hubspot.com/anthropic
```

When the same server is defined in multiple places, higher-precedence sources win: local > project > user > plugin > claude.ai connectors.

## 11.4 OAuth Authentication

Many cloud MCP servers require OAuth. The flow is simple:

```bash
# Step 1: Add the server
claude mcp add --transport http sentry https://mcp.sentry.dev/mcp

# Step 2: Authenticate (inside Claude Code)
/mcp
# Follow the browser login flow
```

Tokens are stored securely and refreshed automatically. For servers requiring pre-configured OAuth credentials, use `--client-id` and `--client-secret` flags.

## 11.5 Managing Servers

```bash
# List all configured servers
claude mcp list

# Get details for a specific server
claude mcp get github

# Remove a server
claude mcp remove github

# Check status inside Claude Code
/mcp
```

Claude Code supports MCP `list_changed` notifications, so servers can dynamically update their available tools without reconnection. HTTP/SSE servers auto-reconnect with exponential backoff (up to 5 attempts).

## 11.6 Environment Variable Expansion in .mcp.json

Team-shared `.mcp.json` files support variable expansion:

```json
{
  "mcpServers": {
    "api-server": {
      "type": "http",
      "url": "${API_BASE_URL:-https://api.example.com}/mcp",
      "headers": {
        "Authorization": "Bearer ${API_KEY}"
      }
    }
  }
}
```

Supported syntax:
- `${VAR}` -- expands to the value of `VAR`
- `${VAR:-default}` -- uses `default` if `VAR` is not set

Variables expand in `command`, `args`, `env`, `url`, and `headers` fields.

## 11.7 MCP Resources

MCP servers can expose resources you reference with `@` mentions:

```
Can you analyze @github:issue://123 and suggest a fix?
Compare @postgres:schema://users with @docs:file://database/user-model
```

Resources are fetched and included as attachments when referenced. Type `@` to see available resources from all connected servers.

## 11.8 MCP Prompts as Commands

MCP servers can expose prompts that become slash commands:

```
/mcp__github__list_prs
/mcp__github__pr_review 456
/mcp__jira__create_issue "Bug in login flow" high
```

The format is `/mcp__servername__promptname`. Arguments are passed space-separated after the command.

## 11.9 Tool Search

Tool search is enabled by default and keeps MCP context usage low. Only tool *names* load at session start; full schemas load on demand when Claude needs them.

| `ENABLE_TOOL_SEARCH` Value | Behavior |
|---------------------------|----------|
| (unset) | All MCP tools deferred, loaded on demand |
| `true` | All MCP tools deferred (even with custom base URL) |
| `auto` | Upfront if tools fit within 10% of context; deferred otherwise |
| `auto:5` | Same as `auto` but with 5% threshold |
| `false` | All MCP tools loaded upfront, no deferral |

## 11.10 Output Limits

| Threshold | Default | Override |
|-----------|---------|----------|
| Warning displayed | 10,000 tokens | (informational only) |
| Maximum output | 25,000 tokens | `MAX_MCP_OUTPUT_TOKENS=50000` |
| Per-tool annotation | N/A | `anthropic/maxResultSizeChars` in tool metadata (up to 500K chars) |

## 11.11 Claude Code AS an MCP Server

Claude Code can itself serve as an MCP server for other clients:

```bash
claude mcp serve
```

Add to Claude Desktop's config:
```json
{
  "mcpServers": {
    "claude-code": {
      "type": "stdio",
      "command": "claude",
      "args": ["mcp", "serve"]
    }
  }
}
```

This exposes Claude Code's tools (Read, Edit, Glob, Grep, etc.) to any MCP-compatible client.

## 11.12 Channels: MCP Servers That Push Events

An MCP server can also push messages *into* your session, so Claude reacts to external events. Enable with the `--channels` flag at startup. Channels can connect Claude Code to Telegram messages, Discord chats, CI results, or monitoring alerts.

## 11.13 Real-World Example: The Three-Source Workflow

Connect three MCP servers for a complete development workflow:

```bash
# Product specs from Notion
claude mcp add --transport http notion https://mcp.notion.com/mcp

# Error monitoring from Sentry
claude mcp add --transport http sentry https://mcp.sentry.dev/mcp

# Database access via PostgreSQL
claude mcp add --transport stdio db -- npx -y @bytebase/dbhub \
  --dsn "postgresql://readonly:pass@analytics.db.com:5432/main"
```

Now you can ask:

```
Read the spec for the user dashboard redesign from Notion.
Check Sentry for the top errors on the dashboard page.
Query the database for the most common user actions on the current dashboard.
Then implement the redesign based on all this context.
```

Claude reads the spec, checks error patterns, queries real usage data, and implements the feature -- all without you switching tabs or copying data.

> **Try This**: Add the GitHub MCP server (`claude mcp add --transport http github https://api.githubcopilot.com/mcp/`), authenticate with `/mcp`, then ask Claude to "Review PR #123 and suggest improvements." Experience the difference between pasting a diff and having Claude read it directly.

**Key Takeaway**: MCP eliminates the copy-paste loop between your tools and Claude Code. HTTP transport is recommended for cloud services, stdio for local tools. Use project-scoped `.mcp.json` to share configurations with your team, and environment variables to keep secrets out of version control.

---

# Chapter 12: Sub-agents -- Isolated Specialists

**Sub-agents are specialized AI assistants with their own context window, tool restrictions, and permissions, keeping verbose operations out of your main conversation.**

## 12.1 The Context Problem Sub-agents Solve

Imagine you ask Claude to "run the full test suite and tell me what fails." Without sub-agents, 500 lines of test output flood your conversation, consuming precious context window space. With sub-agents, a specialist runs the tests in its own context and returns only: "3 tests failed in `auth.test.ts`: login timeout, token refresh, and session expiry."

Sub-agents are like delegating to a colleague. You say "go research this and give me a summary" -- they do the deep work in their own notebook and hand you a one-page brief.

## 12.2 Built-in Sub-agents

| Agent | Model | Tools | Purpose |
|-------|-------|-------|---------|
| **Explore** | Haiku (fast) | Read-only (no Write/Edit) | Fast codebase search and analysis |
| **Plan** | Inherits from session | Read-only (no Write/Edit) | Research during plan mode |
| **general-purpose** | Inherits from session | All tools | Complex multi-step tasks requiring both reading and writing |

Additional built-in helpers include `statusline-setup` (Sonnet, for configuring status lines) and `Claude Code Guide` (Haiku, for answering questions about Claude Code features).

When invoking Explore, Claude specifies a thoroughness level: **quick** for targeted lookups, **medium** for balanced exploration, or **very thorough** for comprehensive analysis.

## 12.3 Custom Sub-agents

Create a `.claude/agents/<name>.md` file (project-scoped) or `~/.claude/agents/<name>.md` (user-scoped) with YAML frontmatter and a markdown body that becomes the system prompt:

```markdown
---
name: security-reviewer
description: Reviews code for security vulnerabilities. Use proactively after code changes.
tools: Read, Grep, Glob, Bash
model: sonnet
memory: project
---

You are a senior security engineer. When invoked:

1. Run `git diff` to see recent changes
2. Check for:
   - SQL injection vulnerabilities
   - XSS attack vectors
   - Exposed secrets or API keys
   - Missing input validation
   - Insecure deserialization
3. Rate each finding: Critical / High / Medium / Low
4. Provide specific fix recommendations with code examples

Update your agent memory with patterns you discover.
```

### Frontmatter Fields Reference

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Unique identifier (lowercase, hyphens) |
| `description` | Yes | When Claude should delegate to this sub-agent |
| `tools` | No | Allowlisted tools. Inherits all if omitted |
| `disallowedTools` | No | Tools to deny (removed from inherited set) |
| `model` | No | `sonnet`, `opus`, `haiku`, full model ID, or `inherit` |
| `permissionMode` | No | `default`, `acceptEdits`, `auto`, `dontAsk`, `bypassPermissions`, `plan` |
| `maxTurns` | No | Maximum agentic turns before stopping |
| `skills` | No | Skills to preload at startup (full content injected, not just available) |
| `mcpServers` | No | MCP servers scoped to this sub-agent |
| `hooks` | No | Lifecycle hooks scoped to this sub-agent |
| `memory` | No | Persistent memory scope: `user`, `project`, or `local` |
| `background` | No | `true` = always run as a background task |
| `effort` | No | Override effort level: `low` through `max` |
| `isolation` | No | `worktree` = run in a temporary git worktree (isolated repo copy) |
| `color` | No | Display color: `red`, `blue`, `green`, `yellow`, `purple`, `orange`, `pink`, `cyan` |
| `initialPrompt` | No | Auto-submitted first turn when running as main agent via `--agent` |

### Scope Priority

| Location | Scope | Priority |
|----------|-------|----------|
| Managed settings | Organization-wide | 1 (highest) |
| `--agents` CLI flag | Current session only | 2 |
| `.claude/agents/` | Current project | 3 |
| `~/.claude/agents/` | All your projects | 4 |
| Plugin `agents/` directory | Where plugin is enabled | 5 (lowest) |

## 12.4 Invoking Sub-agents

Three approaches, from light-touch to session-wide:

**Natural language** -- name the sub-agent and Claude decides whether to delegate:
```
Use the security-reviewer to check my auth changes
```

**@-mention** -- guarantees the sub-agent runs for one task:
```
@"security-reviewer (agent)" audit the authentication module
```

**Session-wide** -- the entire session uses that sub-agent:
```bash
claude --agent security-reviewer
```

Or make it the default for a project:
```json
// .claude/settings.json
{ "agent": "security-reviewer" }
```

## 12.5 Foreground vs. Background

- **Foreground** (default): blocks the main conversation; permission prompts pass through to you.
- **Background**: runs concurrently; permissions are pre-approved at launch. Press **Ctrl+B** to background a running task.

Set `background: true` in frontmatter to always run in background. If a background sub-agent fails due to missing permissions, start a new foreground instance for the same task.

## 12.6 Worktree Isolation

Set `isolation: worktree` to give a sub-agent its own copy of the repository via git worktrees. Each sub-agent works on its own branch without interfering with your working directory. The worktree is automatically cleaned up if the sub-agent makes no changes.

```yaml
---
name: experimental-refactor
description: Tries risky refactors in an isolated copy
isolation: worktree
tools: Read, Edit, Write, Bash, Grep, Glob
---
```

## 12.7 Persistent Memory

The `memory` field gives sub-agents a directory that survives across conversations:

| Scope | Location | Use When |
|-------|----------|----------|
| `user` | `~/.claude/agent-memory/<name>/` | Learnings should apply across all projects |
| `project` | `.claude/agent-memory/<name>/` | Knowledge is project-specific and shareable via VCS |
| `local` | `.claude/agent-memory-local/<name>/` | Project-specific but should not be committed |

When enabled, the sub-agent's system prompt includes the first 200 lines (or 25KB) of `MEMORY.md` in the memory directory, plus instructions to curate the file. The Read, Write, and Edit tools are automatically enabled.

## 12.8 Scoped MCP Servers

Attach MCP servers that only exist while a sub-agent runs:

```yaml
---
name: browser-tester
description: Tests features in a real browser using Playwright
mcpServers:
  - playwright:
      type: stdio
      command: npx
      args: ["-y", "@playwright/mcp@latest"]
  - github  # reference an already-configured server by name
---
```

Inline definitions are connected at sub-agent start and disconnected at finish. This keeps the parent conversation free of tools it does not need.

## 12.9 Preloading Skills

The `skills` field injects the full content of named skills at startup. Sub-agents do not inherit skills from the parent -- you must list them explicitly:

```yaml
---
name: api-developer
description: Implement API endpoints following team conventions
skills:
  - api-conventions
  - error-handling-patterns
---
```

## 12.10 Auto-Compaction

Sub-agents support automatic compaction with the same logic as the main conversation. By default, it triggers at approximately 95% capacity. Override with `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` (e.g., `50` for 50%).

## 12.11 Sub-agents vs. /btw

| | Sub-agents | `/btw` (Side Questions) |
|---|-----------|------------------------|
| **Context** | Own window (empty), returns summary | Sees full main conversation context |
| **Tools** | Full tool access (configurable) | No tool access |
| **Result** | Returns to main conversation | Discarded after answering |
| **Best for** | Tasks producing verbose output | Quick clarifying questions |

## 12.12 Real-World Example: Security Reviewer

A sub-agent that checks every PR for vulnerabilities, with persistent project memory:

```markdown
---
name: security-reviewer
description: Reviews code changes for security vulnerabilities. Use proactively after any code modifications.
tools: Read, Grep, Glob, Bash
model: sonnet
memory: project
color: red
---

You are a senior security engineer performing code review.

## On every invocation:
1. Check your memory for known patterns in this codebase
2. Run `git diff HEAD~1` to see recent changes
3. Analyze each changed file for:
   - Injection vulnerabilities (SQL, XSS, command injection)
   - Authentication/authorization bypasses
   - Secrets or credentials in code
   - Insecure cryptographic usage
   - Missing input validation
   - Race conditions
4. Rate findings: CRITICAL / HIGH / MEDIUM / LOW
5. For each finding, provide the exact vulnerable line and a fix
6. Update your memory with new patterns discovered

## Output format:
### Security Review Summary
- **Files reviewed**: (list)
- **Findings**: (count by severity)
- **Details**: (one section per finding with line number, risk, and fix)
```

> **Try This**: Create a `~/.claude/agents/test-runner.md` sub-agent with `tools: Bash, Read, Grep` and `model: haiku` that runs your project's test suite and reports only failures. Then tell Claude: "Use test-runner to check if the auth module tests pass." Notice how the 200-line test output stays in the sub-agent's context while your main conversation receives only the summary.

**Key Takeaway**: Sub-agents are context-preserving specialists. They keep verbose operations out of your main conversation, enforce tool restrictions, and can accumulate knowledge across sessions through persistent memory. Use them for any task where the *process* is noisy but the *result* is concise.

---

# Chapter 13: Agent Teams -- Parallel Collaboration (Experimental)

**Agent teams coordinate multiple independent Claude Code instances working in parallel, with shared task lists and direct inter-agent messaging.**

## 13.1 Why Agent Teams?

Sub-agents are like sending one assistant at a time to research something. Agent teams are like assembling a war room: multiple specialists work simultaneously, challenge each other's findings, and coordinate through a shared task board.

This feature is experimental and disabled by default:

```json
// settings.json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

Or in your shell: `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude`

## 13.2 Architecture

An agent team consists of four components:

```
+------------------+
|    Team Lead     |  <-- Your main Claude Code session
|  (coordinates)   |
+--------+---------+
         |
    +----+----+----+----+
    |         |         |
+---v---+ +---v---+ +---v---+
| Team- | | Team- | | Team- |
| mate 1| | mate 2| | mate 3|
| (sec) | | (perf)| | (test)|
+---+---+ +---+---+ +---+---+
    |         |         |
    +----+----+----+----+
         |         |
    +----v----+ +--v------+
    |  Shared | | Mailbox |
    |Task List| | (msgs)  |
    +---------+ +---------+
```

| Component | Role |
|-----------|------|
| **Team Lead** | Main session that creates the team, spawns teammates, coordinates work |
| **Teammates** | Separate Claude Code instances working on assigned tasks |
| **Task List** | Shared list of work items with states: pending, in-progress, completed |
| **Mailbox** | Messaging system for direct inter-agent communication |

Teams and tasks are stored locally at `~/.claude/teams/{team-name}/config.json` and `~/.claude/tasks/{team-name}/`.

## 13.3 When to Use Agent Teams

Best use cases:
- **Parallel investigation**: multiple teammates explore different aspects simultaneously
- **Independent modules**: each teammate owns a separate piece without conflicts
- **Competing hypotheses**: teammates test different theories and debate findings
- **Cross-layer coordination**: frontend, backend, and tests each owned by a different teammate

## 13.4 Sub-agents vs. Agent Teams

| | Sub-agents | Agent Teams |
|---|-----------|-------------|
| **Context** | Own window; results return to caller | Fully independent windows |
| **Communication** | Report to main agent only | Message each other directly |
| **Coordination** | Main agent manages all work | Shared task list with self-coordination |
| **Best for** | Focused tasks where only the result matters | Complex work requiring discussion |
| **Token cost** | Lower (results summarized back) | Higher (each teammate is a separate instance) |

**Rule of thumb**: if workers need to *talk to each other*, use agent teams. If they just need to *report back*, use sub-agents.

## 13.5 Starting a Team

Tell Claude what you need in natural language:

```
Create an agent team to review PR #142. Spawn three reviewers:
- One focused on security implications
- One checking performance impact
- One validating test coverage
Have them each review and report findings.
```

Claude creates the team, spawns teammates, assigns tasks, and coordinates work. You stay in control -- Claude will not create a team without your approval.

## 13.6 Display Modes

| Mode | How It Works | Requirements |
|------|-------------|--------------|
| **In-process** (default) | All teammates in main terminal. `Shift+Down` to cycle. | Any terminal |
| **Split panes** | Each teammate gets its own pane. Click to interact. | tmux or iTerm2 |

Configure in `~/.claude.json`:
```json
{ "teammateMode": "in-process" }
```

Or per session:
```bash
claude --teammate-mode in-process
```

The default `"auto"` mode uses split panes if you are already in a tmux session, and in-process otherwise.

## 13.7 Team Control

### Specify teammates and models:
```
Create a team with 4 teammates to refactor these modules in parallel.
Use Sonnet for each teammate.
```

### Require plan approval:
```
Spawn an architect teammate to refactor the auth module.
Require plan approval before they make any changes.
```

The teammate works in read-only plan mode until the lead approves the approach. Rejected plans go back for revision.

### Talk to teammates directly:
- **In-process**: `Shift+Down` to cycle, type to message. `Ctrl+T` toggles task list.
- **Split panes**: Click into a pane to interact.

### Task management:
Tasks have three states: pending, in-progress, completed. Tasks can depend on other tasks. The lead assigns tasks explicitly, or teammates self-claim unblocked tasks. File locking prevents race conditions when multiple teammates try to claim simultaneously.

## 13.8 Hooks for Quality Gates

Three hook events enforce rules on agent teams:

| Hook Event | When It Fires | Exit 2 Behavior |
|------------|--------------|-----------------|
| `TeammateIdle` | Teammate about to go idle | Sends feedback, keeps teammate working |
| `TaskCreated` | New task being created | Prevents creation, sends feedback |
| `TaskCompleted` | Task being marked complete | Prevents completion, sends feedback |

## 13.9 Best Practices

1. **Start with 3-5 teammates.** Coordination overhead increases faster than throughput.
2. **Aim for 5-6 tasks per teammate.** Keeps everyone productive without excessive context switching.
3. **Avoid file conflicts.** Break work so each teammate owns different files.
4. **Monitor and steer.** Check in on progress; redirect approaches that are not working.
5. **Give enough context.** Teammates load CLAUDE.md and skills but do NOT inherit the lead's conversation history. Include task-specific details in the spawn prompt.
6. **Start with research/review tasks.** If new to teams, start with non-coding tasks that have clear boundaries.
7. **Tell the lead to wait.** If the lead starts implementing instead of delegating, say: "Wait for your teammates to complete their tasks before proceeding."

## 13.10 Permissions and Context

- Teammates start with the lead's permission settings. If the lead uses `--dangerously-skip-permissions`, all teammates do too.
- Each teammate loads the same project context as a regular session (CLAUDE.md, MCP servers, skills) but NOT the lead's conversation history.
- Messages are delivered automatically. The lead does not need to poll for updates.
- Task dependencies unblock automatically when prerequisite tasks complete.

## 13.11 Using Sub-agent Definitions for Teammates

When spawning a teammate, reference a sub-agent definition by name:

```
Spawn a teammate using the security-reviewer agent type to audit the auth module.
```

The teammate honors the definition's `tools` allowlist and `model`. The definition body is appended to the teammate's system prompt as additional instructions. Team coordination tools (`SendMessage`, task management) are always available regardless of `tools` restrictions.

## 13.12 Limitations

- **No session resumption**: `/resume` does not restore in-process teammates
- **One team per session**: clean up the current team before starting a new one
- **No nested teams**: teammates cannot spawn their own teams
- **Lead is fixed**: the session that creates the team stays the lead
- **Permissions set at spawn**: can be changed after, but not at spawn time
- **Task status can lag**: teammates sometimes fail to mark tasks as completed
- **Split panes**: not supported in VS Code terminal, Windows Terminal, or Ghostty
- **Shutdown can be slow**: teammates finish their current request before shutting down

## 13.13 Real-World Example: Parallel PR Review

Three reviewers analyze a PR simultaneously, each with a different lens:

```
Create an agent team to review PR #142. Spawn three reviewers:

- **security-reviewer**: Focus on authentication, authorization, injection attacks,
  and secret exposure. Check every input path and database query.

- **performance-reviewer**: Focus on algorithmic complexity, unnecessary allocations,
  N+1 queries, and missing caching opportunities. Run benchmarks if applicable.

- **test-reviewer**: Focus on test coverage for new code paths, edge cases,
  error handling, and regression risks. Check that mocks are realistic.

Have them each review independently, then share and challenge each other's
findings before synthesizing a final review.
```

The debate structure is key. Sequential review suffers from anchoring: once one issue category is explored, subsequent review is biased toward it. With multiple independent reviewers actively challenging each other, the final review is more thorough.

### Cleanup

When done, tell the lead to clean up:
```
Clean up the team
```

This removes shared team resources. Shut down teammates first -- cleanup fails if any are still running. Always use the lead for cleanup, not teammates.

> **Try This**: Enable agent teams with `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`, then ask Claude: "Create an agent team to investigate why our API response times increased. Spawn 3 teammates: one checking database queries, one reviewing recent code changes, one analyzing infrastructure logs." Watch them work in parallel and challenge each other's hypotheses.

**Key Takeaway**: Agent teams are the heavyweight option for parallel AI work. They are best for tasks where multiple specialists need to communicate, debate, and coordinate -- like code reviews, investigations with competing hypotheses, and cross-layer implementations. Start with 3-5 teammates, avoid file conflicts, and monitor progress actively. Remember: sub-agents are cheaper and simpler for tasks that do not require inter-agent communication.

---

## References

1. [Claude Code Skills Documentation](https://code.claude.com/docs/en/skills) -- Official Anthropic documentation on creating, managing, and sharing skills.
2. [Claude Code Hooks Documentation](https://code.claude.com/docs/en/hooks) -- Official reference for event-driven automation with lifecycle hooks.
3. [Claude Code MCP Documentation](https://code.claude.com/docs/en/mcp) -- Guide to connecting Claude Code to external tools via Model Context Protocol.
4. [Claude Code Sub-agents Documentation](https://code.claude.com/docs/en/sub-agents) -- Creating and using specialized AI sub-agents.
5. [Claude Code Agent Teams Documentation](https://code.claude.com/docs/en/agent-teams) -- Experimental multi-agent parallel collaboration.
6. [Model Context Protocol Specification](https://modelcontextprotocol.io/introduction) -- The open standard for AI-tool integrations.
7. [Agent Skills Standard](https://agentskills.io) -- Open standard for cross-tool AI skills, which Claude Code extends.

---

# Part IV: Ecosystem & Integrations

# Chapter 14: Plugins -- Bundled Extensions

**Plugins are the package manager for Claude Code: they bundle skills, hooks, agents, MCP servers, LSP servers, monitors, and settings into a single distributable unit.**

## 14.1 Why Plugins Exist

Think of Claude Code's standalone configuration (everything in `.claude/`) as writing a script that only lives on one machine. It works perfectly for personal workflows, but the moment you want three teammates to use your custom code-review skill, you are copy-pasting Markdown files and hoping everyone keeps them in sync.

Plugins solve this the same way npm solved JavaScript dependency sharing. A plugin is a self-contained directory with a manifest that Claude Code can install, version, update, and namespace so nothing collides.

| Approach | Skill Name Format | Best For |
|----------|------------------|----------|
| **Standalone** (`.claude/`) | `/hello` | Personal workflows, quick experiments |
| **Plugin** (`.claude-plugin/`) | `/plugin-name:hello` | Team sharing, marketplace distribution, versioned releases |

The namespacing is key. If two plugins both define a `review` skill, they live peacefully as `/security-plugin:review` and `/style-plugin:review`.

## 14.2 Plugin Manifest

Every plugin starts with a manifest at `.claude-plugin/plugin.json`:

```json
{
  "name": "code-review-pro",
  "description": "Security-focused code review with OWASP checks",
  "version": "2.1.0",
  "author": {
    "name": "Your Security Team"
  },
  "homepage": "https://github.com/yourorg/code-review-pro",
  "license": "MIT"
}
```

The `name` field doubles as the namespace prefix -- all skills in this plugin are invoked as `/code-review-pro:skill-name`. Version follows semantic versioning so teams can pin dependencies.

## 14.3 Directory Structure

Here is the complete anatomy of a plugin:

```
code-review-pro/
+-- .claude-plugin/
|   +-- plugin.json            # Manifest (ONLY file in this dir)
+-- skills/
|   +-- security-scan/
|   |   +-- SKILL.md           # Auto-invoked security scanner
|   +-- owasp-check/
|       +-- SKILL.md
+-- commands/
|   +-- quick-review.md        # Legacy format, use skills/ for new plugins
+-- agents/
|   +-- security-reviewer.md   # Custom sub-agent definition
+-- hooks/
|   +-- hooks.json             # Event handlers (PostToolUse, etc.)
+-- .mcp.json                  # MCP server configurations
+-- .lsp.json                  # LSP server configurations
+-- monitors/
|   +-- monitors.json          # Background process watchers
+-- bin/
|   +-- scan-deps              # Executables added to PATH
+-- settings.json              # Default settings when plugin is active
```

A critical mistake newcomers make: putting skills or hooks *inside* the `.claude-plugin/` directory. Only `plugin.json` goes there. Everything else lives at the plugin root.

## 14.4 LSP Servers: Code Intelligence

LSP (Language Server Protocol) plugins give Claude precise symbol navigation -- go-to-definition, find-references, type-checking -- which dramatically reduces the number of file reads Claude needs.

```json
// .lsp.json
{
  "go": {
    "command": "gopls",
    "args": ["serve"],
    "extensionToLanguage": {
      ".go": "go"
    }
  }
}
```

Without LSP, Claude must grep and read files to understand where a function is defined. With LSP, Claude gets the exact file and line number in one call. For large codebases, this reduces token consumption significantly.

For common languages (TypeScript, Python, Rust), pre-built LSP plugins exist in the official marketplace. Create custom LSP plugins only for languages not already covered.

## 14.5 Background Monitors

Monitors watch long-running processes and stream events to Claude in real time:

```json
// monitors/monitors.json
[
  {
    "name": "error-log",
    "command": "tail -F ./logs/error.log",
    "description": "Application error log"
  }
]
```

Each stdout line from the command is delivered to Claude as a notification. This is the "push" counterpart to `/loop`'s "pull" model -- instead of polling for errors, Claude hears about them the instant they happen.

## 14.6 Installation and Testing

**Development testing:**

```bash
# Load plugin directly from a local directory
claude --plugin-dir ./code-review-pro

# Load multiple plugins simultaneously
claude --plugin-dir ./plugin-one --plugin-dir ./plugin-two
```

**Hot reload during development:** Run `/reload-plugins` inside a session to pick up changes without restarting. This reloads skills, agents, hooks, MCP servers, and LSP servers.

**Marketplace installation:**

```bash
# Install from a configured marketplace
/plugin install code-review-pro

# Or from the CLI
claude plugin install code-review-pro
```

Installation scopes: **user** (all projects), **project** (shared with collaborators), or **local** (just you, just this repo).

## 14.7 Plugin Marketplaces

Plugins can be distributed from multiple source types:

- **GitHub repositories** -- a repo with a `.claude-plugin/plugin.json` at its root
- **npm packages** -- published to the npm registry
- **URLs** -- direct links to plugin archives
- **Local directories** -- file paths on disk
- **Official Anthropic marketplace** -- submit at [claude.ai/settings/plugins/submit](https://claude.ai/settings/plugins/submit)

## 14.8 Migration from Standalone

Converting existing `.claude/` configurations to a plugin:

| Standalone (`.claude/`) | Plugin Equivalent |
|------------------------|-------------------|
| `.claude/commands/` | `plugin-name/commands/` |
| `.claude/skills/` | `plugin-name/skills/` |
| `.claude/agents/` | `plugin-name/agents/` |
| Hooks in `settings.json` | `hooks/hooks.json` |

The hooks format is identical -- copy the `hooks` object from your `settings.json` directly into `hooks/hooks.json`.

## 14.9 Real-World Example: Building a Code-Review Plugin

Let us build a security-scanning code review plugin from scratch:

```bash
mkdir -p sec-review/.claude-plugin sec-review/skills/scan sec-review/hooks
```

**Manifest** (`sec-review/.claude-plugin/plugin.json`):
```json
{
  "name": "sec-review",
  "description": "Security-focused code review with dependency scanning",
  "version": "1.0.0"
}
```

**Skill** (`sec-review/skills/scan/SKILL.md`):
```markdown
---
description: Scan code changes for security vulnerabilities. Use when reviewing PRs or before commits.
---

When scanning code for security issues, check for:
1. SQL injection vectors (unsanitized user input in queries)
2. XSS vulnerabilities (unescaped output in templates)
3. Hardcoded secrets (API keys, passwords, tokens)
4. Insecure dependencies (known CVEs)
5. Authentication/authorization bypass

Report findings with severity: CRITICAL, HIGH, MEDIUM, LOW.
For each finding, show the file, line, vulnerable code, and remediation.
```

**Hook** (`sec-review/hooks/hooks.json`):
```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [{
          "type": "command",
          "command": "jq -r '.tool_input.file_path' | xargs grep -n 'password\\|secret\\|api_key' || true"
        }]
      }
    ]
  }
}
```

Test it:
```bash
claude --plugin-dir ./sec-review
# Then invoke: /sec-review:scan
```

> **Try This:** Create a plugin with a single skill that enforces your team's commit message format. Add a `PreToolUse` hook that validates commit messages match `type(scope): description` before allowing `git commit`.

**Key Takeaway:** Plugins transform Claude Code from a personal tool into a team platform. Start with standalone configuration for rapid iteration, then package into a plugin when you are ready to share. The namespace-based isolation ensures multiple plugins coexist without conflicts.

---

# Chapter 15: IDE Integrations -- VS Code and JetBrains

**IDE integrations bring Claude Code directly into your editor, eliminating context-switching between terminal and code.**

## 15.1 VS Code Extension

The VS Code extension is the recommended graphical interface for Claude Code. It provides a native panel inside VS Code with capabilities that complement the CLI.

### Installation

```bash
# From the command line
code --install-extension anthropic.claude-code

# Or from VS Code: Cmd+Shift+X, search "Claude Code", click Install
```

Requires VS Code 1.98.0 or higher.

### Core Features

**Inline diffs:** When Claude proposes a file edit, VS Code shows a side-by-side diff. You can accept, reject, or modify the proposed content directly in the diff view before accepting -- Claude is told that you modified it and does not assume the file matches its original proposal.

**@-mentions with fuzzy matching:** Type `@` followed by a partial name. Claude uses fuzzy matching:

```
@auth     -> matches auth.js, AuthService.ts, middleware/auth.go
@src/comp -> matches src/components/ (trailing slash for folders)
```

Select text in the editor and press `Option+K` (Mac) / `Alt+K` (Windows/Linux) to insert an @-mention with the exact file path and line range, like `@app.ts#5-10`.

**Permission modes:** Click the mode indicator at the bottom of the prompt box to switch between:
- **Normal** -- Claude asks before each action
- **Plan** -- Claude describes its plan and waits for approval (opens as a full Markdown document for inline comments)
- **Auto-accept** -- Claude makes edits without asking

**Session history:** AI-generated titles for each conversation. Browse by time period (Today, Yesterday, Last 7 days). Hover to rename or remove sessions.

**Multiple conversations:** Use "Open in New Tab" from the Command Palette for parallel conversations. Each maintains independent history and context. Colored dots on tab icons indicate status: blue = permission pending, orange = Claude finished while tab was hidden.

### The Built-in IDE MCP Server

The extension runs a local MCP server that exposes two model-visible tools:

| Tool | What It Does | Writes? |
|------|-------------|---------|
| `mcp__ide__getDiagnostics` | Returns errors/warnings from VS Code's Problems panel | No |
| `mcp__ide__executeCode` | Runs Python code in the active Jupyter notebook kernel | Yes |

The server binds to `127.0.0.1` on a random port with a fresh auth token per activation, so only the local user can connect.

For Jupyter execution, every call inserts a new cell and shows a native Quick Pick dialog asking you to **Execute** or **Cancel**. The tool refuses if there is no active notebook or the Jupyter extension is not installed.

### Key Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd+Esc` / `Ctrl+Esc` | Toggle focus between editor and Claude |
| `Cmd+Shift+Esc` / `Ctrl+Shift+Esc` | Open new conversation tab |
| `Option+K` / `Alt+K` | Insert @-mention reference for current selection |
| `Cmd+N` / `Ctrl+N` | New conversation (requires `enableNewConversationShortcut`) |

### Checkpoints and Rewind

Hover over any message to reveal the rewind button with three options:
- **Fork conversation from here** -- new branch, code unchanged
- **Rewind code to here** -- revert files, keep conversation
- **Fork conversation and rewind code** -- both

### Chrome Integration

With the Claude in Chrome extension (v1.0.36+), type `@browser` in the prompt:

```
@browser go to localhost:3000 and check the console for errors
```

Claude opens new tabs and shares your browser's login state.

## 15.2 JetBrains Plugin

The JetBrains plugin supports IntelliJ IDEA, PyCharm, WebStorm, GoLand, PhpStorm, and Android Studio.

### Features

| Feature | Description |
|---------|-------------|
| **Quick launch** | `Cmd+Esc` (Mac) / `Ctrl+Esc` (Windows/Linux) |
| **Diff viewing** | Code changes displayed in IDE's native diff viewer |
| **Selection sharing** | Current selection/tab automatically shared with Claude |
| **File references** | `Cmd+Option+K` (Mac) / `Alt+Ctrl+K` inserts `@File#L1-99` |
| **Diagnostic sharing** | Lint, syntax, and type errors automatically shared |

### The `/ide` Command

When running Claude from an external terminal (not the JetBrains integrated terminal), use `/ide` to connect:

```bash
claude     # Start Claude Code
/ide       # Connect to JetBrains IDE
```

This activates all integration features -- diffs open in JetBrains, diagnostics flow automatically, and file references work correctly.

## 15.3 VS Code Extension vs CLI Comparison

| Feature | CLI | VS Code Extension |
|---------|-----|-------------------|
| All commands and skills | Yes | Subset (type `/` to see available) |
| MCP server config | Yes | Partial (add via CLI; manage via `/mcp`) |
| Checkpoints | Yes | Yes |
| `!` bash shortcut | Yes | No |
| Tab completion | Yes | No |
| Inline diffs | Terminal-based | Native VS Code diff viewer |
| Multiple conversations | Separate terminals | Tabbed within VS Code |
| Chrome integration | No | Yes (with extension) |

The extension and CLI share conversation history. Continue an extension conversation in the CLI with `claude --resume`.

## 15.4 Real-World Example: React Component Refactor

Imagine you need to refactor a class component to a functional component with hooks.

1. **Open the file** in VS Code and select the class component
2. **Press `Option+K`** to insert `@UserProfile.tsx#15-87` into the prompt
3. **Type your request:**
   ```
   Refactor this class component to a functional component using hooks.
   Preserve all lifecycle behavior and state management.
   ```
4. **Review the inline diff** -- VS Code shows the before/after side by side
5. **Click a line** in the diff to leave a comment: "Keep the error boundary as a class component"
6. **Submit comments** with `Cmd+Enter` -- Claude revises its proposal
7. **Accept** the final diff

The entire workflow happens without leaving VS Code. Claude sees your selection, proposes changes in the native diff viewer, reads your inline comments, and iterates.

> **Try This:** Install the VS Code extension, open a project, select a function, and ask Claude to add TypeScript types. Review the inline diff and leave a comment asking for stricter types on one parameter.

**Key Takeaway:** IDE integrations eliminate the context-switch tax between terminal and editor. The VS Code extension adds visual diff review, @-mention fuzzy matching, and the IDE MCP server (diagnostics + Jupyter), while the JetBrains plugin provides native diff viewing and automatic diagnostic sharing. Both complement rather than replace the CLI.

---

# Chapter 16: Desktop App, Web, and Mobile

**Claude Code runs on three surfaces -- desktop, web, and mobile -- with sessions that can move between them.**

## 16.1 Desktop App (macOS + Windows)

The Desktop app is not a standalone application but the **Code tab** within the Claude Desktop app. It adds a graphical layer on top of the standard Claude Code experience.

### Parallel Sessions with Git Worktree Isolation

Click **+ New session** (or `Cmd+N`) and each session gets its own Git worktree automatically. Changes in one session do not affect others until you commit. Worktrees live in `<project-root>/.claude/worktrees/` by default.

This is like having multiple developers working on separate branches simultaneously -- except they are all Claude instances running on your machine.

### Visual Diff Review

After Claude makes changes, a diff stats indicator (`+12 -1`) appears. Click to open a file-by-file diff viewer. Click any line to leave a comment. Submit all comments with `Cmd+Enter`, and Claude reads them and revises.

### Live App Preview

Claude can start a dev server and open an embedded browser to verify its changes. Configuration lives in `.claude/launch.json`:

```json
{
  "version": "0.0.1",
  "configurations": [
    {
      "name": "my-app",
      "runtimeExecutable": "npm",
      "runtimeArgs": ["run", "dev"],
      "port": 3000
    }
  ]
}
```

Auto-verify is on by default: after each edit, Claude takes screenshots, inspects the DOM, clicks elements, and fixes issues it finds.

### Computer Use (Research Preview)

Computer use lets Claude open apps, control your screen, and interact with GUIs. Available on macOS and Windows with Pro/Max plans.

Claude follows a precision hierarchy:
1. **Connector** for a service (e.g., Slack MCP) -- used first
2. **Bash** for shell commands
3. **Chrome extension** for browser tasks
4. **Computer use** for everything else (native apps, simulators, proprietary tools)

App access tiers:
| Tier | Capability | Applies To |
|------|-----------|------------|
| View only | See the app in screenshots | Browsers, trading platforms |
| Click only | Click and scroll, no typing | Terminals, IDEs |
| Full control | Click, type, drag, shortcuts | Everything else |

### Side Chats

Press `Cmd+;` to open a side chat. It reads the main thread's context but does not add anything back. Think of it as a "whisper" conversation -- ask Claude to explain a concept without derailing the main task.

### PR Monitoring

After opening a PR, a CI status bar appears with toggles:
- **Auto-fix**: Claude reads CI failure output and pushes fixes automatically
- **Auto-merge**: squash-merges when all checks pass
- **Auto-archive**: archives the session when the PR merges or closes

### Dispatch: Phone to Desktop

Dispatch lives in the Cowork tab. Message a task from the Claude mobile app ("fix the login bug in auth.py"), and Dispatch spawns a Code session on your desktop. You get a push notification when it finishes or needs your approval.

### Environments

| Environment | Where Claude Runs | Best For |
|------------|------------------|----------|
| **Local** | Your machine | Full filesystem access |
| **SSH** | Remote machine you manage | Server-side development |
| **Remote** | Anthropic cloud | Long-running tasks, close laptop |

## 16.2 Claude Code on the Web (claude.ai/code)

Cloud sessions run on Anthropic-managed VMs with:
- **4 vCPUs, 16 GB RAM, 30 GB disk**
- **Sessions persist** even if you close the browser
- **Pre-installed tools:**

| Category | Included |
|----------|----------|
| Python | 3.x with pip, poetry, uv, black, mypy, pytest, ruff |
| Node.js | 20, 21, 22 via nvm; npm, yarn, pnpm, bun |
| Ruby | 3.1, 3.2, 3.3 with bundler, rbenv |
| PHP | 8.4 with Composer |
| Java | OpenJDK 21 with Maven, Gradle |
| Go | Latest stable |
| Rust | rustc, cargo |
| C/C++ | GCC, Clang, cmake, ninja |
| Docker | docker, dockerd, docker compose |
| Databases | PostgreSQL 16, Redis 7.0 |

### GitHub Authentication

Two methods:
- **GitHub App**: Install during web onboarding, access scoped per repository
- **`/web-setup`**: Sync your local `gh` CLI token to your Claude account

### Setup Scripts

Bash scripts that run before Claude launches. Results are cached (snapshotted) so dependencies install once and persist:

```bash
#!/bin/bash
apt update && apt install -y gh
pip install -r requirements.txt
```

### Network Access Levels

| Level | Outbound Connections |
|-------|---------------------|
| **None** | No outbound network |
| **Trusted** (default) | Allowlisted domains: package registries, GitHub, cloud SDKs |
| **Full** | Any domain |
| **Custom** | Your own allowlist, optionally including defaults |

### Teleport: Pull Web Sessions to Your Terminal

```bash
# Interactive session picker
claude --teleport

# Resume a specific session
claude --teleport <session-id>
```

Teleport verifies you are in the correct repository, fetches the cloud session's branch, and loads the full conversation history locally. It is the inverse of `--remote` (which pushes a task to the cloud).

### Auto-Fix PRs

Claude can watch a PR and automatically respond to CI failures and review comments:
- **Clear fixes**: Claude pushes the fix and explains what was done
- **Ambiguous requests**: Claude asks you before acting
- **Duplicate events**: Claude notes them and moves on

## 16.3 Remote Control

Remote Control connects claude.ai or the mobile app to a locally running Claude Code session. All code execution stays local -- web/mobile is just a display window.

```bash
# Server mode: dedicated process waiting for connections
claude remote-control

# Add to existing session
claude --remote-control
# or inside a session:
/remote-control
```

Server mode supports multiple concurrent sessions (up to 32 by default) with `--spawn worktree` for Git isolation per connection.

### Mobile Push Notifications

Claude decides when to notify you -- typically when a long task finishes or when it needs a decision. You can also request notifications: "notify me when the tests finish."

## 16.4 Real-World Example: Cross-Device Workflow

1. **At your desk** (Desktop app): Start refactoring the auth module in a local session
2. **Heading out**: Run `/remote-control` before leaving
3. **On your phone** (Claude mobile app): Open the session, review Claude's progress, type "looks good, now add the migration script"
4. **On the couch** (laptop browser): Open claude.ai/code, leave inline comments on the diff
5. **Back at desk**: Continue in the terminal with `claude --resume`

The session never moved to the cloud. Your phone and browser were windows into the local process running on your desktop machine.

> **Try This:** Start a Claude Code session, run `/remote-control`, then open claude.ai/code on your phone. Send a message from your phone and watch it execute on your computer.

**Key Takeaway:** Desktop, web, and mobile are not separate products -- they are surfaces for the same underlying session. Remote Control keeps everything local while letting you interact from anywhere. Teleport and `--remote` move sessions between local and cloud when you need persistent execution.

---

# Chapter 17: CI/CD Integrations -- GitHub Actions and GitLab

**CI/CD integrations embed Claude into your team's automated workflows, from PR reviews to scheduled automation.**

## 17.1 GitHub Actions

### Quick Setup

The fastest path:

```bash
# Inside a Claude Code session:
/install-github-app
```

This installs the Claude GitHub App, adds the `ANTHROPIC_API_KEY` secret, and creates the workflow file.

### Basic Workflow

```yaml
# .github/workflows/claude.yml
name: Claude Code
on:
  issue_comment:
    types: [created]
  pull_request_review_comment:
    types: [created]
jobs:
  claude:
    runs-on: ubuntu-latest
    steps:
      - uses: anthropics/claude-code-action@v1
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          # Responds to @claude mentions in comments
```

Once deployed, any comment containing `@claude` on a PR or issue triggers Claude to analyze context and respond.

### Using Skills in Actions

```yaml
- uses: anthropics/claude-code-action@v1
  with:
    anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
    prompt: "Review this PR for security and correctness"
    claude_args: "--max-turns 5 --model claude-sonnet-4-6"
```

The `claude_args` parameter accepts any CLI flag: `--max-turns`, `--model`, `--allowedTools`, `--mcp-config`, `--append-system-prompt`, and more.

### Scheduled Automation

```yaml
name: Daily Report
on:
  schedule:
    - cron: "0 9 * * *"  # 9 AM UTC daily
jobs:
  report:
    runs-on: ubuntu-latest
    steps:
      - uses: anthropics/claude-code-action@v1
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          prompt: "Generate a summary of yesterday's commits and open issues"
```

### AWS Bedrock Workflow (OIDC)

```yaml
- name: Configure AWS Credentials (OIDC)
  uses: aws-actions/configure-aws-credentials@v4
  with:
    role-to-assume: ${{ secrets.AWS_ROLE_TO_ASSUME }}
    aws-region: us-west-2

- uses: anthropics/claude-code-action@v1
  with:
    github_token: ${{ steps.app-token.outputs.token }}
    use_bedrock: "true"
    claude_args: '--model us.anthropic.claude-sonnet-4-6 --max-turns 10'
```

### Google Vertex AI Workflow (Workload Identity Federation)

```yaml
- name: Authenticate to Google Cloud
  uses: google-github-actions/auth@v2
  with:
    workload_identity_provider: ${{ secrets.GCP_WORKLOAD_IDENTITY_PROVIDER }}
    service_account: ${{ secrets.GCP_SERVICE_ACCOUNT }}

- uses: anthropics/claude-code-action@v1
  with:
    github_token: ${{ steps.app-token.outputs.token }}
    use_vertex: "true"
    claude_args: '--model claude-sonnet-4-5@20250929 --max-turns 10'
  env:
    ANTHROPIC_VERTEX_PROJECT_ID: ${{ steps.auth.outputs.project_id }}
    CLOUD_ML_REGION: us-east5
```

## 17.2 GitLab CI/CD

GitLab integration is maintained by GitLab (currently in beta). The pattern is similar: add a masked CI/CD variable, add a Claude job to `.gitlab-ci.yml`, and Claude responds to `@claude` mentions.

```yaml
stages:
  - ai

claude:
  stage: ai
  image: node:24-alpine3.21
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
  before_script:
    - apk add --no-cache git curl bash
    - curl -fsSL https://claude.ai/install.sh | bash
  script:
    - /bin/gitlab-mcp-server || true
    - >
      claude
      -p "${AI_FLOW_INPUT:-'Review this MR and implement requested changes'}"
      --permission-mode acceptEdits
      --allowedTools "Bash Read Edit Write mcp__gitlab"
```

GitLab uses a `gitlab-mcp-server` for MR interaction (reading comments, creating MRs, posting responses). It supports Bedrock and Vertex via OIDC, just like GitHub Actions.

## 17.3 GitHub Code Review (Research Preview)

Code Review is a managed service -- a fleet of specialized agents analyze your PRs in parallel on Anthropic infrastructure.

### How It Works

```
PR Opened/Pushed
      |
      v
+---------------------+
| Multiple Agents     |  (parallel on Anthropic infra)
| - Logic errors      |
| - Security vulns    |
| - Edge cases        |
| - Regressions       |
+---------------------+
      |
      v
  Verification Step (filter false positives)
      |
      v
  Inline Comments on PR (severity-tagged)
```

### Severity Levels

| Marker | Severity | Meaning |
|--------|----------|---------|
| Red circle | Important | Bug that should be fixed before merging |
| Yellow circle | Nit | Minor issue, worth fixing but not blocking |
| Purple circle | Pre-existing | Bug in the codebase not introduced by this PR |

### Metrics and Cost

- **Average completion time**: ~20 minutes
- **Average cost**: $15-25 per review (scales with PR size)
- **Billing**: Separate from plan usage via extra usage

### Setup

1. Go to [claude.ai/admin-settings/claude-code](https://claude.ai/admin-settings/claude-code)
2. Install the Claude GitHub App
3. Select repositories and trigger modes

### Trigger Modes

| Mode | When Reviews Run |
|------|-----------------|
| **Once after PR creation** | When PR is opened or marked ready |
| **After every push** | On every push to the PR branch |
| **Manual** | Only when someone comments `@claude review` |

### REVIEW.md Customization

Place a `REVIEW.md` at your repo root to override review behavior:

```markdown
# Review Instructions

## What Important means here
Reserve Important for findings that would break behavior, leak data,
or block a rollback. Style and naming suggestions are Nit at most.

## Cap the nits
Report at most five Nits per review. Say "plus N similar items" in
the summary for the rest.

## Do not report
- Anything CI already enforces: lint, formatting, type errors
- Generated files under src/gen/ and any *.lock file

## Always check
- New API routes have an integration test
- Log lines don't include PII
- Database queries are scoped to the caller's tenant
```

## 17.4 Slack Integration

The Claude Slack app routes coding requests to Claude Code on the web:

1. **@Claude** in a channel with a coding task
2. Claude detects coding intent and creates a web session
3. Status updates post to the Slack thread
4. Completion notification with "View Session" and "Create PR" buttons

**Routing modes:**
- **Code only**: All mentions route to Claude Code sessions
- **Code + Chat**: Claude intelligently routes between Code (development) and Chat (writing, analysis, general questions)

If Claude misroutes, click "Retry as Code" or "Retry as Chat" to correct.

## 17.5 Real-World Example: Automated PR Reviews

Here is a complete setup for automated PR reviews with GitHub Actions:

**Step 1:** Install the GitHub app and add the API key:
```bash
claude
/install-github-app
```

**Step 2:** Create the workflow (`.github/workflows/claude-review.yml`):
```yaml
name: Claude PR Review
on:
  pull_request:
    types: [opened, synchronize]
  issue_comment:
    types: [created]
  pull_request_review_comment:
    types: [created]

jobs:
  review:
    runs-on: ubuntu-latest
    if: |
      github.event_name == 'pull_request' ||
      contains(github.event.comment.body, '@claude')
    steps:
      - uses: anthropics/claude-code-action@v1
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          prompt: |
            Review this PR for:
            1. Correctness and logic errors
            2. Security vulnerabilities
            3. Performance regressions
            4. Test coverage gaps
            Post findings as review comments with severity.
          claude_args: "--max-turns 5"
```

**Step 3:** Add a `CLAUDE.md` to your repo with coding standards Claude should enforce.

Now every PR gets an automatic review, and team members can ask `@claude` follow-up questions in PR comments.

> **Try This:** Set up the basic Claude GitHub Action workflow in a test repository. Open a PR with a deliberate bug (e.g., an off-by-one error) and see if Claude catches it.

**Key Takeaway:** CI/CD integrations make Claude a team member, not just an individual tool. GitHub Actions and GitLab CI let Claude respond to @mentions and review PRs. Code Review provides a managed multi-agent analysis service. Slack integration meets developers where they already communicate. The key to all of them: `CLAUDE.md` guides Claude to follow your team's standards.

---

# Chapter 18: Scheduling and Automation

**Four scheduling options cover the spectrum from quick session polling to cloud automation that runs while your laptop is closed.**

## 18.1 The Scheduling Landscape

| Option | Runs On | Requires Machine On | Best For |
|--------|---------|---------------------|----------|
| **Routines** | Anthropic cloud | No | Tasks that should run reliably without your machine |
| **Desktop tasks** | Your machine | Yes (Desktop app open) | Local file access on a recurring schedule |
| **GitHub Actions cron** | CI pipeline | No | Repo event triggers and scheduled automation |
| **`/loop`** | Current CLI session | Yes (session open) | Quick polling during a session |

Think of it as a spectrum from lightweight to heavyweight:

```
/loop          Desktop tasks       Routines        GitHub Actions
(session)      (machine)           (cloud)         (CI pipeline)
<---------- increasing durability and independence ---------->
```

## 18.2 Routines (Cloud Scheduling)

A routine is a saved configuration: a prompt + repositories + connectors, packaged once and triggered automatically. Routines run on Anthropic cloud infrastructure -- they keep working when your laptop is closed.

### Three Trigger Types

**Scheduled:** Run on a recurring cadence.
```bash
# From the CLI:
/schedule daily PR review at 9am
```

Presets: hourly, daily, weekdays, weekly. Custom intervals via cron expressions (minimum 1 hour).

**API:** An HTTP endpoint that starts a run on demand.
```bash
curl -X POST https://api.anthropic.com/v1/claude_code/routines/trig_01ABC.../fire \
  -H "Authorization: Bearer sk-ant-oat01-xxxxx" \
  -H "anthropic-beta: experimental-cc-routine-2026-04-01" \
  -H "anthropic-version: 2023-06-01" \
  -H "Content-Type: application/json" \
  -d '{"text": "Sentry alert SEN-4521 fired in prod."}'
```

Wire this into your monitoring system: when an alert fires, Claude investigates and opens a fix PR.

**GitHub:** React to pull request or release events.
```
pull_request.opened -> Run review routine
release.published   -> Run changelog routine
```

Filter by author, title, body, base branch, head branch, labels, draft status, or merge status.

### Branch Permissions

By default, routines can only push to `claude/`-prefixed branches. This prevents accidental modification of protected branches. Enable "Allow unrestricted branch pushes" per repository if needed.

### Creating Routines

Three surfaces, same result:
- **Web**: [claude.ai/code/routines](https://claude.ai/code/routines) -- New routine
- **CLI**: `/schedule` command (scheduled triggers only)
- **Desktop**: Schedule page -- New task -- New remote task

## 18.3 Desktop Scheduled Tasks

Local recurring tasks that run on your machine. The Desktop app must be open.

| Frequency | Behavior |
|-----------|----------|
| Manual | Run only when you click "Run now" |
| Hourly | Every hour |
| Daily | Once per day at a set time |
| Weekdays | Monday through Friday |
| Weekly | Once per week |

**Missed runs:** If you were away, Desktop runs one catch-up run for the most recent missed time when it resumes. It does not run multiple catch-up runs.

Desktop tasks have full access to local files, MCP servers, and tools -- unlike cloud routines which start from a fresh clone.

## 18.4 /loop (Session-Scoped Scheduling)

The lightest scheduling option. Runs within the current session and stops when you start a new one.

### Fixed Interval

```bash
/loop 5m check if the deployment finished and tell me what happened
```

Supported units: `s` (seconds, rounded up to 1 minute), `m` (minutes), `h` (hours), `d` (days).

### Dynamic Interval (Claude Chooses)

```bash
/loop check whether CI passed and address any review comments
```

Without an interval, Claude picks a delay between 1 minute and 1 hour based on what it observed -- short waits during active CI, longer waits when things are quiet.

### Built-in Maintenance Prompt

```bash
/loop
```

With no arguments, Claude runs a built-in maintenance loop:
1. Continue unfinished work
2. Tend to the current branch's PR (review comments, failed CI, merge conflicts)
3. Cleanup passes (bug hunts, simplification)

Customize by placing a `.claude/loop.md` or `~/.claude/loop.md` file.

### Under the Hood

`/loop` uses three tools:

| Tool | Purpose |
|------|---------|
| `CronCreate` | Schedule a task with a 5-field cron expression |
| `CronList` | List all scheduled tasks with IDs and schedules |
| `CronDelete` | Cancel a task by ID |

Limits: **50 tasks per session**, **7-day auto-expiry** for recurring tasks, tasks fire only while Claude is idle (not mid-response).

### Stopping a Loop

Press `Esc` to stop a running `/loop`. This clears the pending wakeup but does not affect tasks scheduled through direct `CronCreate` calls.

## 18.5 Headless Mode (Agent SDK via CLI)

For scripts and CI pipelines, `claude -p` runs non-interactively:

```bash
# Basic non-interactive query
claude -p "Find and fix the bug in auth.py" --allowedTools "Read,Edit,Bash"
```

### Bare Mode: Fastest Startup

```bash
claude --bare -p "Summarize this file" --allowedTools "Read"
```

`--bare` skips auto-discovery of hooks, skills, plugins, MCP servers, CLAUDE.md, and memory. Only flags you pass explicitly take effect. Ideal for CI where you want deterministic behavior.

### Structured Output

```bash
# JSON with metadata
claude -p "Extract function names from auth.py" \
  --output-format json \
  --json-schema '{"type":"object","properties":{"functions":{"type":"array","items":{"type":"string"}}},"required":["functions"]}'
```

The response includes session metadata with the structured output in the `structured_output` field.

### Streaming

```bash
claude -p "Explain recursion" \
  --output-format stream-json \
  --verbose \
  --include-partial-messages
```

Each line is a JSON event. Filter for text deltas:
```bash
... | jq -rj 'select(.type == "stream_event" and .event.delta.type? == "text_delta") | .event.delta.text'
```

### Continue Conversations

```bash
# First request
claude -p "Review this codebase for performance issues"

# Continue the most recent conversation
claude -p "Now focus on the database queries" --continue

# Resume a specific session
session_id=$(claude -p "Start a review" --output-format json | jq -r '.session_id')
claude -p "Continue that review" --resume "$session_id"
```

## 18.6 Real-World Example: Morning PR Review Routine

Set up a routine that reviews all open PRs every morning at 9 AM:

**Step 1:** Create the routine from the CLI:
```bash
claude
/schedule
```

Claude walks you through the setup interactively.

**Step 2:** Or create from the web at [claude.ai/code/routines](https://claude.ai/code/routines):

- **Name**: "Morning PR Review"
- **Prompt**:
  ```
  List all open pull requests in this repository.
  For each PR:
  1. Read the diff and check for bugs, security issues, and style violations
  2. Leave a summary comment with findings categorized by severity
  3. If the PR is approved and CI is green, note it as ready to merge
  Post a summary of all PRs to the #dev channel via Slack connector.
  ```
- **Repository**: Select your main repo
- **Environment**: Default (Trusted network access)
- **Trigger**: Scheduled -- Daily at 9:00 AM
- **Connectors**: GitHub (for PR access), Slack (for posting summaries)

**Step 3:** Verify by clicking "Run now" on the routine's detail page.

Each run creates a session you can review at claude.ai/code. The routine uses your GitHub identity, so PR comments appear under your username (labeled as from Claude Code).

For quick one-off polling during a session, combine with `/loop`:

```bash
# After opening a PR, poll CI status every 5 minutes
/loop 5m check CI status on PR #42, if it fails read the logs and push a fix
```

> **Try This:** Create a `/loop` that checks `git status` every 2 minutes and reports uncommitted changes. Then create a one-shot reminder: "remind me in 30 minutes to push the branch." Verify both with "what scheduled tasks do I have?"

**Key Takeaway:** Match your scheduling choice to your durability needs. Use `/loop` for quick in-session polling, Desktop tasks for local recurring work, Routines for cloud automation that survives closed laptops, and GitHub Actions cron for CI pipeline triggers. Headless mode (`claude -p`) bridges Claude Code into any script or pipeline with structured output and conversation continuation.

---

# Part V: Mastery

# Chapter 19: Settings & Configuration

## TLDR

Claude Code uses a four-scope configuration hierarchy (Managed > CLI args > Local project > Shared project > User) that lets organizations enforce security policies at the top while individuals customize at the bottom. Settings files are JSON with a published schema, covering permissions, sandboxing, model selection, auto mode, attribution, hooks, and environment variables. Enterprise administrators can deploy managed settings via MDM tools, file-based configs, or Anthropic's server-managed delivery. The `/config` command provides an interactive interface, while `/status` shows which settings are active and where they originate.

---

Think of Claude Code's configuration system like a corporate building's access control. The building management (Managed settings) sets fire codes and security policies that nobody can override. Individual tenants (Project settings) define their own office rules. And each person (User settings) has personal desk preferences. When there is a conflict, the higher authority always wins.

### The Four Configuration Scopes

Claude Code organizes settings into four distinct scopes, each serving a different audience:

| Scope | Location | Who It Affects | Shared with Team? |
|:------|:---------|:---------------|:-------------------|
| **Managed** | Server-managed, plist/registry, or `managed-settings.json` | All users on the machine | Yes (deployed by IT) |
| **User** | `~/.claude/` directory | You, across all projects | No |
| **Project** | `.claude/` in repository | All collaborators on this repository | Yes (committed to git) |
| **Local** | `.claude/settings.local.json` | You, in this repository only | No (gitignored) |

### Settings Precedence Hierarchy

When the same setting appears in multiple scopes, Claude Code follows a strict precedence order. This is the single most important concept in configuration:

```
1. Managed settings     (highest — cannot be overridden)
2. Command line arguments
3. Local project settings (.claude/settings.local.json)
4. Shared project settings (.claude/settings.json)
5. User settings         (lowest — ~/.claude/settings.json)
```

For **array settings** (like permission rules or sandbox paths), arrays are **concatenated and deduplicated** across scopes rather than replaced. This means a lower-priority scope can add entries without overriding higher-priority ones.

### Key Settings Categories

#### Permissions: allow, deny, ask

Permission rules control what tools Claude can use. Rules follow the format `Tool` or `Tool(specifier)` and are evaluated in order: deny first, then ask, then allow.

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run lint)",
      "Bash(npm run test *)",
      "Read(~/.zshrc)"
    ],
    "deny": [
      "Bash(curl *)",
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)"
    ],
    "ask": [
      "Bash(git push *)"
    ],
    "defaultMode": "default"
  }
}
```

#### Sandbox: Filesystem and Network Isolation

The sandbox isolates bash commands at the OS level:

```json
{
  "sandbox": {
    "enabled": true,
    "autoAllowBashIfSandboxed": true,
    "excludedCommands": ["docker *"],
    "filesystem": {
      "allowWrite": ["/tmp/build", "~/.kube"],
      "denyRead": ["~/.aws/credentials"]
    },
    "network": {
      "allowedDomains": ["github.com", "*.npmjs.org"],
      "deniedDomains": ["uploads.github.com"],
      "allowLocalBinding": true
    }
  }
}
```

#### Model and Effort Level

```json
{
  "model": "opus",
  "effortLevel": "xhigh",
  "availableModels": ["sonnet", "opus", "haiku"]
}
```

#### Auto Mode: Classifier Rules

Auto mode uses a separate classifier to approve or block actions. Configure it with prose rules:

```json
{
  "autoMode": {
    "environment": ["Trusted repo: github.example.com/acme"],
    "allow": ["npm and yarn commands are safe in this project"],
    "soft_deny": ["Never deploy to production without approval"]
  }
}
```

#### Attribution: Git Commit Customization

```json
{
  "attribution": {
    "commit": "Generated with AI\n\nCo-Authored-By: AI <ai@example.com>",
    "pr": ""
  }
}
```

#### Hooks and Environment Variables

```json
{
  "hooks": {
    "Notification": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "osascript -e 'display notification \"Claude needs attention\" with title \"Claude Code\"'"
      }]
    }]
  },
  "env": {
    "CLAUDE_CODE_ENABLE_TELEMETRY": "1",
    "OTEL_METRICS_EXPORTER": "otlp"
  }
}
```

### Managed Settings for Enterprise

Enterprise administrators have three delivery mechanisms for managed settings that cannot be overridden:

**MDM / OS-Level Policies:**
- **macOS**: `com.anthropic.claudecode` managed preferences domain (Jamf, Kandji)
- **Windows**: `HKLM\SOFTWARE\Policies\ClaudeCode` registry key (Group Policy, Intune)

**File-Based:**
- macOS: `/Library/Application Support/ClaudeCode/managed-settings.json`
- Linux/WSL: `/etc/claude-code/managed-settings.json`
- Windows: `C:\Program Files\ClaudeCode\managed-settings.json`

File-based settings also support a `managed-settings.d/` drop-in directory for composability. Use numeric prefixes like `10-telemetry.json` and `20-security.json` to control merge order.

**Server-Managed**: Delivered from Anthropic's servers via the Claude.ai admin console.

### Worktree and Auto-Update Settings

```json
{
  "worktree": {
    "symlinkDirectories": ["node_modules", ".cache"],
    "sparsePaths": ["packages/my-app", "shared/utils"]
  },
  "autoUpdatesChannel": "stable",
  "minimumVersion": "2.1.100"
}
```

Set `DISABLE_AUTOUPDATER=1` as an environment variable to prevent background updates entirely.

### Interactive Configuration

- **`/config`**: Opens a tabbed Settings interface for viewing and modifying configuration options interactively.
- **`/status`**: Displays which settings sources are active and where they come from — including labels like "Enterprise managed settings (remote)" or "Enterprise managed settings (plist)".

### Complete Settings File Example

```json
{
  "$schema": "https://json.schemastore.org/claude-code-settings.json",
  "permissions": {
    "allow": [
      "Bash(npm run lint)",
      "Bash(npm run test *)",
      "Bash(git diff *)",
      "Bash(git log *)",
      "Bash(git status)"
    ],
    "deny": [
      "Bash(curl *)",
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)"
    ],
    "defaultMode": "default"
  },
  "model": "sonnet",
  "effortLevel": "high",
  "sandbox": {
    "enabled": true,
    "network": {
      "allowedDomains": ["github.com", "*.npmjs.org"]
    }
  },
  "hooks": {
    "Notification": [{
      "matcher": "idle_prompt",
      "hooks": [{
        "type": "command",
        "command": "osascript -e 'display notification \"Claude is done\" with title \"Claude Code\"'"
      }]
    }]
  },
  "env": {
    "CLAUDE_CODE_EFFORT_LEVEL": "high"
  },
  "attribution": {
    "commit": "Generated with Claude Code\n\nCo-Authored-By: Claude <noreply@anthropic.com>",
    "pr": "Generated with Claude Code"
  }
}
```

> **Try This**: Create a `.claude/settings.json` in your project with permission rules that allow your test runner and deny access to `.env` files. Run `/status` to confirm the rules are active.

### Key Takeaway

Claude Code's settings hierarchy provides a powerful layered system where organizations enforce policies at the top and individuals customize at the bottom. The `$schema` property enables autocomplete in your editor, `/config` makes changes interactively, and `/status` verifies what is active. Always start with project-level settings (`.claude/settings.json`) and commit them to git so your entire team benefits from consistent configuration.

---

# Chapter 20: Model Configuration & Performance

## TLDR

Claude Code supports multiple models through aliases (`default`, `best`, `sonnet`, `opus`, `haiku`, `opusplan`) with defaults varying by account type. Effort levels (`low` through `max`) control adaptive reasoning depth, while extended thinking is enabled by default and dynamically allocates tokens. Fast mode provides 2.5x faster Opus 4.6 responses at higher cost. Extended context (1M tokens) is available on Max, Team, Enterprise, and API plans. The average cost is approximately $13 per developer per active day, manageable through context strategies, model selection, and the `/cost` command.

---

Choosing the right model for a task is like choosing the right vehicle for a trip. A bicycle (Haiku) is fast and cheap for quick errands. A sedan (Sonnet) handles most daily commutes perfectly. A truck (Opus) is what you need when hauling heavy loads of complex reasoning. And `opusplan` is like using the truck to navigate a route, then switching to the sedan for the actual drive.

### Model Aliases

Model aliases abstract away version numbers so you can refer to capabilities instead of specific releases:

| Alias | Behavior |
|:------|:---------|
| `default` | Clears any override, reverts to recommended model for your account |
| `best` | Most capable model available (currently equivalent to `opus`) |
| `sonnet` | Latest Sonnet for daily coding tasks |
| `opus` | Latest Opus for complex reasoning |
| `haiku` | Fast, efficient model for simple tasks |
| `sonnet[1m]` | Sonnet with 1M token context window |
| `opus[1m]` | Opus with 1M token context window |
| `opusplan` | Opus during plan mode, auto-switches to Sonnet for execution |

On the Anthropic API, `opus` resolves to Opus 4.7 and `sonnet` to Sonnet 4.6. On Bedrock, Vertex, and Foundry, `opus` resolves to Opus 4.6 and `sonnet` to Sonnet 4.5.

### Default Models by Account Type

| Account Type | Default Model |
|:-------------|:-------------|
| Max, Team Premium | Opus 4.7 |
| Pro, Team Standard, Enterprise, Anthropic API | Sonnet 4.6 |
| Bedrock, Vertex, Foundry | Sonnet 4.5 |

You can set your model in several ways (listed by priority): `/model` during a session, `--model` at startup, `ANTHROPIC_MODEL` environment variable, or the `model` field in settings.

### Effort Levels: Controlling Thinking Depth

Effort levels control adaptive reasoning, letting the model decide how much to think on each step:

| Level | When to Use |
|:------|:-----------|
| `low` | Short, scoped, latency-sensitive tasks that are not intelligence-sensitive |
| `medium` | Cost-sensitive work that can trade off some intelligence |
| `high` | Balances token usage and intelligence; minimum for intelligence-sensitive work |
| `xhigh` | Best results for most coding/agentic tasks; recommended default on Opus 4.7 |
| `max` | Deepest reasoning with no constraint on token spend; current session only |

Model-specific availability:

| Model | Available Levels |
|:------|:----------------|
| Opus 4.7 | `low`, `medium`, `high`, `xhigh`, `max` |
| Opus 4.6 / Sonnet 4.6 | `low`, `medium`, `high`, `max` |

Set effort via: `/effort` (interactive slider), arrow keys in `/model`, `--effort` flag, `CLAUDE_CODE_EFFORT_LEVEL` env var, or `effortLevel` in settings.

### Extended Thinking

Extended thinking is **enabled by default**, giving Claude space to reason through complex problems before responding. Models with effort support (Opus 4.7, Opus 4.6, Sonnet 4.6) use **adaptive reasoning** — dynamically allocating thinking tokens based on task complexity.

| Configuration | Method |
|:-------------|:-------|
| Toggle on/off | `Option+T` (macOS) / `Alt+T` (Windows/Linux) |
| Set effort level | `/effort`, `/model`, `CLAUDE_CODE_EFFORT_LEVEL` |
| Global default | `/config` to toggle thinking mode |
| Limit budget | `MAX_THINKING_TOKENS=10000` environment variable |
| Deep reasoning one-off | Include "ultrathink" in your prompt |

The "ultrathink" keyword adds an in-context instruction telling the model to reason more on that specific turn. It does not change the effort level setting.

Opus 4.7 always uses adaptive reasoning. On Opus 4.6 and Sonnet 4.6, set `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING=1` to revert to the fixed thinking budget.

### Extended Context (1M Tokens)

Opus 4.7, Opus 4.6, and Sonnet 4.6 support a 1 million token context window:

| Plan | Opus 1M | Sonnet 1M |
|:-----|:--------|:----------|
| Max, Team, Enterprise | Included | Requires extra usage |
| Pro | Requires extra usage | Requires extra usage |
| API / Pay-as-you-go | Full access | Full access |

Enable with the `[1m]` suffix: `/model opus[1m]` or `/model sonnet[1m]`.

### Fast Mode (Research Preview)

Fast mode provides **2.5x faster** Opus 4.6 responses at higher per-token cost:

| Mode | Input (MTok) | Output (MTok) |
|:-----|:-------------|:--------------|
| Fast mode Opus 4.6 | $30 | $150 |

- Toggle with `/fast`
- Available to all subscription plans and Console API users via **extra usage only**
- Has separate rate limits; auto-falls back to standard Opus 4.6 when rate-limited
- Not available on Opus 4.7 or other models
- The `lightning bolt` icon appears next to your prompt when active

### Model Overrides and Custom Models

For enterprise deployments using Bedrock, Vertex, or Foundry, map Anthropic model IDs to provider-specific IDs:

```json
{
  "modelOverrides": {
    "claude-opus-4-7": "arn:aws:bedrock:us-east-2:123456789012:application-inference-profile/opus-prod",
    "claude-sonnet-4-6": "arn:aws:bedrock:us-east-2:123456789012:application-inference-profile/sonnet-prod"
  }
}
```

Add a custom entry to the model picker with:

```bash
export ANTHROPIC_CUSTOM_MODEL_OPTION="my-gateway/claude-opus-4-7"
export ANTHROPIC_CUSTOM_MODEL_OPTION_NAME="Opus via Gateway"
```

### Prompt Caching

Prompt caching is auto-enabled and significantly reduces costs for repeated content. Disable selectively:

| Variable | Effect |
|:---------|:-------|
| `DISABLE_PROMPT_CACHING` | Disable for all models |
| `DISABLE_PROMPT_CACHING_HAIKU` | Disable for Haiku only |
| `DISABLE_PROMPT_CACHING_SONNET` | Disable for Sonnet only |
| `DISABLE_PROMPT_CACHING_OPUS` | Disable for Opus only |

### Cost Management

The average enterprise cost is **~$13 per developer per active day** and **$150-250 per month**, with 90% of users under $30 per active day.

**Track costs**: Use `/cost` for session token usage and cost estimates.

**Reduce costs with these strategies:**

1. **Manage context proactively**: `/clear` between tasks, use `/compact` with instructions
2. **Choose the right model**: Sonnet for most tasks, Opus for complex reasoning, `model: haiku` for subagents
3. **Reduce MCP overhead**: CLI tools (`gh`, `aws`) are more context-efficient than MCP servers
4. **Use plan mode**: Prevents expensive rework from wrong implementation direction
5. **Delegate verbose operations**: Use subagents for test runs and log analysis

**Agent teams** use approximately **7x more tokens** than standard sessions. Keep teams small and tasks focused.

> **Try This**: Start a session, run `/effort` and set it to `low`. Ask Claude a simple question, then check `/cost`. Change to `xhigh`, ask a complex architecture question, and check `/cost` again. Compare the token usage difference.

### Key Takeaway

Model selection and effort level are the two biggest levers for balancing quality, speed, and cost. Use `opusplan` for complex features (Opus plans, Sonnet executes), `sonnet` with `high` effort for daily work, and `haiku` for simple subagent tasks. Monitor costs with `/cost`, manage context aggressively with `/clear`, and consider fast mode when interactive latency matters more than cost.

---

# Chapter 21: Common Workflows & Best Practices

## TLDR

Claude Code excels at exploring codebases, fixing bugs, refactoring, writing tests, creating PRs, and handling git operations through natural language. The recommended four-phase workflow is Explore (Plan Mode) then Plan then Implement (Normal Mode) then Commit. Unix composability lets you pipe data through Claude in scripts and CI. Parallel sessions with git worktrees enable concurrent work without conflicts. The eight official best practices center on one principle: give Claude a way to verify its work, manage context aggressively, and course-correct early.

---

### Core Workflows

#### Exploring Codebases

When joining a new project, start broad and narrow down:

```
> give me an overview of this codebase
> explain the main architecture patterns used here
> trace the login process from front-end to database
> find the files that handle user authentication
```

#### Fixing Bugs

Share the error, get recommendations, apply the fix:

```
> I'm seeing an error when I run npm test
> suggest a few ways to fix the @ts-ignore in user.ts
> update user.ts to add the null check you suggested
```

Always tell Claude the command to reproduce the issue. A stack trace is worth a thousand words.

#### Refactoring

Find legacy code, get recommendations, apply safely, verify:

```
> find deprecated API usage in our codebase
> suggest how to refactor utils.js to use modern JavaScript features
> refactor utils.js to use ES2024 features while maintaining the same behavior
> run tests for the refactored code
```

#### Writing Tests

Identify gaps, scaffold, add edge cases, run:

```
> find functions in NotificationsService.swift that are not covered by tests
> add tests for the notification service
> add test cases for edge conditions in the notification service
> run the new tests and fix any failures
```

Claude examines your existing test files to match the style, frameworks, and assertion patterns already in use.

#### Creating PRs

```
> summarize the changes I've made to the authentication module
> create a pr
> enhance the PR description with more context about the security improvements
```

When you create a PR using `gh pr create`, the session is automatically linked. Resume later with `claude --from-pr <number>`.

#### Git Operations

Claude handles commits, branches, and even merge conflicts:

```
> commit these changes with a descriptive message
> create a new branch called feature/oauth-integration
> help me resolve the merge conflicts in auth.ts
```

#### Documentation

```
> find functions without proper JSDoc comments in the auth module
> add JSDoc comments to the undocumented functions in auth.js
> check if the documentation follows our project standards
```

#### Working with Images

You can paste screenshots, drag-and-drop images, or provide file paths. Claude analyzes UI elements, generates CSS from design mockups, and identifies visual issues:

```
> [paste screenshot] Here's the error. What's causing it?
> Generate CSS to match this design mockup
```

### File References with @

Use `@` to include files and directories directly without waiting for Claude to discover them:

```
> Explain the logic in @src/utils/auth.js
> What's the structure of @src/components?
> Show me the data from @github:repos/owner/repo/issues
```

### Plan Mode Workflow (4 Phases)

This is the official recommended workflow for complex features:

```
Phase 1: EXPLORE (Plan Mode)
┌──────────────────────────────┐
│  Enter Plan Mode (Shift+Tab) │
│  Claude reads files, answers  │
│  questions, no changes made   │
└──────────┬───────────────────┘
           │
Phase 2: PLAN (Plan Mode)
┌──────────────────────────────┐
│  Ask for implementation plan  │
│  Press Ctrl+G to edit plan    │
│  in your text editor          │
└──────────┬───────────────────┘
           │
Phase 3: IMPLEMENT (Normal Mode)
┌──────────────────────────────┐
│  Switch to Normal Mode        │
│  Claude codes, tests, fixes   │
│  Verify against the plan      │
└──────────┬───────────────────┘
           │
Phase 4: COMMIT (Normal Mode)
┌──────────────────────────────┐
│  Ask Claude to commit + PR    │
│  "commit with a descriptive   │
│   message and open a PR"      │
└──────────────────────────────┘
```

Start a session in Plan Mode directly:

```bash
claude --permission-mode plan
```

Or run headless queries in Plan Mode:

```bash
claude --permission-mode plan -p "Analyze the authentication system and suggest improvements"
```

### Unix Composability

Claude Code integrates into your existing Unix toolchain:

```bash
# Pipe build errors through Claude
cat build-error.txt | claude -p "concisely explain the root cause" > output.txt

# Use as a linter in package.json
{
  "scripts": {
    "lint:claude": "claude -p 'look at the changes vs. main and report any typos'"
  }
}

# Structured output for scripts
claude -p "List all API endpoints" --output-format json

# Streaming for real-time processing
claude -p "Analyze this log file" --output-format stream-json

# Code review in CI
git diff | claude -p "review these changes for potential issues"
```

### Parallel Sessions with Git Worktrees

Run multiple Claude sessions concurrently, each in an isolated working directory:

```bash
# Start Claude in an isolated worktree
claude --worktree feature-auth

# Start another session in a separate worktree
claude --worktree bugfix-123

# Auto-generate a name
claude --worktree
```

Worktrees are created at `<repo>/.claude/worktrees/<name>` and branch from the default remote branch.

#### .worktreeinclude: Copy Gitignored Files

Git worktrees are fresh checkouts without untracked files. Create a `.worktreeinclude` file in your project root to copy essential files:

```
.env
.env.local
config/secrets.json
```

Only files matching a pattern that are also gitignored get copied.

### Desktop Notifications

Set up a Notification hook so you know when Claude finishes or needs input:

```json
{
  "hooks": {
    "Notification": [{
      "matcher": "",
      "hooks": [{
        "type": "command",
        "command": "osascript -e 'display notification \"Claude Code needs your attention\" with title \"Claude Code\"'"
      }]
    }]
  }
}
```

Matchers: `permission_prompt`, `idle_prompt`, `auth_success`, `elicitation_dialog`.

### Asking Claude About Itself

Claude has built-in access to its own documentation:

```
> can Claude Code create pull requests?
> how do I use MCP with Claude Code?
> what skills are available?
> how do I configure Claude Code for Amazon Bedrock?
```

---

### The Eight Best Practices

#### 1. Give Claude a Way to Verify Its Work

This is the single highest-leverage thing you can do. Include tests, screenshots, or expected outputs.

| Strategy | Weak Prompt | Strong Prompt |
|:---------|:------------|:--------------|
| Verification criteria | "implement email validation" | "write validateEmail. Test: user@example.com is true, invalid is false. Run tests after implementing" |
| Visual verification | "make the dashboard look better" | "[paste screenshot] implement this design, take a screenshot, compare, fix differences" |
| Root cause focus | "the build is failing" | "the build fails with [error]. fix it and verify the build succeeds. address the root cause" |

#### 2. Explore First, Then Plan, Then Code

Use Plan Mode to separate research from execution. Skip planning only when the scope is clear and the fix is small.

#### 3. Provide Specific Context

Reference files with `@`, paste images, give URLs, pipe data. The more precise your instructions, the fewer corrections you need.

#### 4. Course-Correct Early

- **`Esc`**: Stop Claude mid-action
- **`Esc + Esc`** or `/rewind`: Restore previous conversation and code state
- **`/clear`**: Reset context between unrelated tasks

If you have corrected Claude more than twice on the same issue, run `/clear` and start fresh with a better prompt.

#### 5. Manage Context Aggressively

- `/clear` frequently between tasks
- `/compact <instructions>` for targeted summarization
- `/btw` for side questions that do not enter history
- Subagents for investigation (separate context, only summary returns)

#### 6. Use Sub-Agents for Investigation

```
> Use subagents to investigate how our authentication system handles
  token refresh, and whether we have any existing OAuth utilities.
```

The subagent explores in its own context window and reports back a summary, keeping your main conversation clean.

#### 7. Let Claude Interview You

For larger features, start with a minimal prompt and let Claude ask you questions:

```
I want to build [brief description]. Interview me in detail using
the AskUserQuestion tool. Ask about technical implementation, UI/UX,
edge cases, and tradeoffs. Keep interviewing until we've covered
everything, then write a complete spec to SPEC.md.
```

Then start a fresh session to execute the spec with clean context.

#### 8. Avoid Common Failures

- **Kitchen-sink sessions**: Tasks pile up, context polluted. Fix: `/clear` between unrelated tasks.
- **Correcting repeatedly**: Failed attempts pollute context. Fix: After two failures, `/clear` and write a better initial prompt.
- **Over-specified CLAUDE.md**: Claude ignores half of long instructions. Fix: Ruthlessly prune; if Claude already does it correctly, delete the rule.
- **Trust-then-verify gap**: Plausible code that misses edge cases. Fix: Always provide verification.
- **Infinite exploration**: Unscoped investigation fills context. Fix: Use subagents.

---

### Real-World Example: Bug Report to PR

Here is a complete workflow from bug report to merged PR:

```bash
# 1. Start Claude in Plan Mode for the project
claude --permission-mode plan

# 2. In Plan Mode: Explore the bug
> Users report that login fails after session timeout.
  Check the auth flow in src/auth/, especially token refresh.

# 3. Still in Plan Mode: Create a plan
> Create a detailed plan to fix the session timeout bug.
  Include which files to change and what tests to add.

# [Press Ctrl+G to review/edit the plan in your editor]

# 4. Accept the plan, switch to Normal Mode (Shift+Tab twice)
> Implement the fix from your plan. Write a failing test
  that reproduces the issue first, then fix it.

# 5. Verify
> Run the full test suite and make sure everything passes.

# 6. Ship
> Commit with a descriptive message and open a PR.
  Highlight the security improvement in the description.
```

> **Try This**: Find a bug in one of your projects. Use the four-phase workflow (Explore, Plan, Implement, Commit) to fix it. Time yourself and compare to your usual approach.

### Key Takeaway

The four-phase workflow (Explore, Plan, Implement, Commit) is the backbone of effective Claude Code usage. Always give Claude a way to verify its work, manage context aggressively with `/clear`, and course-correct early rather than repeatedly. When in doubt, use subagents for investigation to keep your main context clean, and let Claude interview you for larger features to surface requirements you might have missed.

---

# Chapter 22: Advanced Topics & Agent SDK

## TLDR

Claude Code extends beyond the terminal with Chrome browser integration (live debugging and web testing), Channels (push events from Telegram/Discord/iMessage into sessions), Computer Use (control native apps and screen), and Voice Dictation (push-to-talk input). The Agent SDK (`pip install claude-agent-sdk` / `npm install @anthropic-ai/claude-agent-sdk`) lets you build production AI agents with the same tools, loop, and context management that power Claude Code. Key environment variables cover authentication, cloud providers, model selection, performance tuning, and thinking configuration. Data privacy separates consumer (opt-in/out training) from commercial (never trained on) with 30-day default retention.

---

### Chrome Browser Integration (Beta)

Claude Code can connect to your Chrome browser for tasks that require a real browser environment. Think of it as giving Claude a pair of eyes and hands for web interaction.

**Setup:**

```bash
# Start with Chrome integration
claude --chrome

# Or enable mid-session
/chrome
```

**Capabilities:**

- **Live debugging**: Read console errors and DOM state, then fix the code that caused them
- **Design verification**: Build UI from a Figma mock, open in browser to verify it matches
- **Web app testing**: Test form validation, check for visual regressions, verify user flows
- **Authenticated apps**: Interact with Google Docs, Gmail, Notion — any app you are logged into
- **Data extraction**: Pull structured information from web pages and save locally
- **GIF recording**: Record browser interactions as shareable GIF files

Claude opens new tabs and shares your browser's login state. When it encounters a login page or CAPTCHA, it pauses and asks you to handle it manually.

**Requirements**: Google Chrome or Microsoft Edge, the Claude in Chrome extension (v1.0.36+), Claude Code v2.0.73+, and a direct Anthropic plan (Pro, Max, Team, or Enterprise).

```
> I just updated the login form validation. Can you open localhost:3000,
  try submitting with invalid data, and check if error messages appear?

> Draft a project update based on recent commits and add it to my
  Google Doc at docs.google.com/document/d/abc123
```

### Channels (Research Preview)

A channel is an MCP server that **pushes events** into your running Claude Code session, enabling two-way communication. Unlike MCP servers that Claude queries on demand, channels deliver messages while you are away from the terminal.

**Supported Channels:**

| Channel | Setup | Authentication |
|:--------|:------|:---------------|
| **Telegram** | Create bot via BotFather, install plugin, configure token | Pairing code |
| **Discord** | Create bot in Developer Portal, install plugin, configure token | Pairing code |
| **iMessage** | macOS only, reads Messages database directly | Self-chat auto-approved |
| **fakechat** | Localhost demo, no external service | None needed |

**Install and run a channel:**

```bash
# Install the Telegram plugin
/plugin install telegram@claude-plugins-official

# Configure with your bot token
/telegram:configure <bot-token>

# Restart with channels enabled
claude --channels plugin:telegram@claude-plugins-official
```

**Security model**: Every channel maintains a sender allowlist. Pair senders with a pairing code, then lock access:

```
/telegram:access pair <code>
/telegram:access policy allowlist
```

**Enterprise controls**: On Team and Enterprise plans, channels are off by default. Admins enable them via managed settings:

```json
{
  "channelsEnabled": true,
  "allowedChannelPlugins": [
    { "marketplace": "claude-plugins-official", "plugin": "telegram" }
  ]
}
```

### Computer Use (Research Preview, macOS)

Computer Use lets Claude control native apps on your screen — open windows, click, type, scroll, and screenshot. It is the fallback when MCP, Bash, and Chrome cannot reach a GUI-only application.

**Enable in an interactive session:**

```
/mcp
# Select computer-use > Enable
```

**Permission tiers:**

| Tier | Applies To | Capabilities |
|:-----|:-----------|:-------------|
| View only | Browsers, trading platforms | See the screen, no interaction |
| Click only | Terminals, IDEs | Click and navigate, limited typing |
| Full control | All other apps | Click, type, scroll, drag |

**Safety guardrails:**
- Per-app approval each session
- Terminal window excluded from screenshots (prevents feedback loops)
- Apps with broad reach (Terminal, Finder, System Settings) show extra warnings
- Global `Esc` key aborts computer use from anywhere
- Machine-wide lock ensures only one session controls the screen at a time

```
> Build the MenuBarStats target, launch it, open preferences,
  and verify the interval slider updates the label. Screenshot when done.

> The settings modal clips on narrow windows. Resize to reproduce it,
  screenshot the bug, patch the CSS, and verify the fix.
```

### Voice Dictation

Hold a key and speak to dictate prompts. Your speech is transcribed live into the prompt input.

```bash
# Enable voice dictation
/voice

# Hold Space to record, release to stop
# Mix typing and dictation in the same message
```

Transcription is tuned for coding vocabulary (regex, OAuth, JSON, localhost). Your project name and git branch are added as recognition hints automatically.

Rebind the push-to-talk key in `~/.claude/keybindings.json`:

```json
{
  "bindings": [{
    "context": "Chat",
    "bindings": {
      "meta+k": "voice:pushToTalk",
      "space": null
    }
  }]
}
```

### Agent SDK: Build Custom Agents

The Agent SDK gives you Claude Code's capabilities as a library for building production AI agents.

**Installation:**

```bash
# Python
pip install claude-agent-sdk

# TypeScript
npm install @anthropic-ai/claude-agent-sdk
```

**Basic usage — an agent that finds and fixes bugs:**

```python
import asyncio
from claude_agent_sdk import query, ClaudeAgentOptions

async def main():
    async for message in query(
        prompt="Find and fix the bug in auth.py",
        options=ClaudeAgentOptions(
            allowed_tools=["Read", "Edit", "Bash"]
        ),
    ):
        if hasattr(message, "result"):
            print(message.result)

asyncio.run(main())
```

```typescript
import { query } from "@anthropic-ai/claude-agent-sdk";

for await (const message of query({
  prompt: "Find and fix the bug in auth.ts",
  options: { allowedTools: ["Read", "Edit", "Bash"] }
})) {
  if ("result" in message) console.log(message.result);
}
```

**Built-in Tools:**

| Tool | What It Does |
|:-----|:-------------|
| Read | Read any file in the working directory |
| Write | Create new files |
| Edit | Make precise edits to existing files |
| Bash | Run terminal commands, scripts, git operations |
| Monitor | Watch a background script and react to output |
| Glob | Find files by pattern |
| Grep | Search file contents with regex |
| WebSearch | Search the web for current information |
| WebFetch | Fetch and parse web page content |
| AskUserQuestion | Ask clarifying questions with multiple choice |

**SDK Hooks:**

```python
from claude_agent_sdk import query, ClaudeAgentOptions, HookMatcher

async def log_file_change(input_data, tool_use_id, context):
    file_path = input_data.get("tool_input", {}).get("file_path", "unknown")
    with open("./audit.log", "a") as f:
        f.write(f"{datetime.now()}: modified {file_path}\n")
    return {}

async for message in query(
    prompt="Refactor utils.py to improve readability",
    options=ClaudeAgentOptions(
        permission_mode="acceptEdits",
        hooks={
            "PostToolUse": [
                HookMatcher(matcher="Edit|Write", hooks=[log_file_change])
            ]
        },
    ),
):
    pass
```

Available hooks: `PreToolUse`, `PostToolUse`, `Stop`, `SessionStart`, `SessionEnd`, `UserPromptSubmit`.

**Sessions — resume later:**

```python
session_id = None

# First query: capture session ID
async for message in query(
    prompt="Read the authentication module",
    options=ClaudeAgentOptions(allowed_tools=["Read", "Glob"]),
):
    if isinstance(message, SystemMessage) and message.subtype == "init":
        session_id = message.data["session_id"]

# Resume with full context
async for message in query(
    prompt="Now find all places that call it",
    options=ClaudeAgentOptions(resume=session_id),
):
    if isinstance(message, ResultMessage):
        print(message.result)
```

**SDK vs CLI:**

| Use Case | Best Choice |
|:---------|:-----------|
| Interactive development | CLI |
| CI/CD pipelines | SDK |
| Custom applications | SDK |
| One-off tasks | CLI |
| Production automation | SDK |

### Key Environment Variables

**Authentication:**

| Variable | Purpose |
|:---------|:--------|
| `ANTHROPIC_API_KEY` | API key for Anthropic API requests |
| `ANTHROPIC_AUTH_TOKEN` | Custom Authorization header value |

**Cloud Providers:**

| Variable | Purpose |
|:---------|:--------|
| `CLAUDE_CODE_USE_BEDROCK` | Enable Amazon Bedrock (`1`) |
| `CLAUDE_CODE_USE_VERTEX` | Enable Google Vertex AI (`1`) |
| `CLAUDE_CODE_USE_FOUNDRY` | Enable Microsoft Foundry (`1`) |

**Model:**

| Variable | Purpose |
|:---------|:--------|
| `ANTHROPIC_MODEL` | Default model to use |
| `ANTHROPIC_DEFAULT_SONNET_MODEL` | Override what `sonnet` alias resolves to |
| `ANTHROPIC_DEFAULT_OPUS_MODEL` | Override what `opus` alias resolves to |
| `ANTHROPIC_DEFAULT_HAIKU_MODEL` | Override what `haiku` alias resolves to |

**Performance:**

| Variable | Default |
|:---------|:--------|
| `API_TIMEOUT_MS` | 600000 (10 min) |
| `BASH_DEFAULT_TIMEOUT_MS` | 120000 (2 min) |

**Thinking:**

| Variable | Purpose |
|:---------|:--------|
| `CLAUDE_CODE_EFFORT_LEVEL` | Effort level (`low`/`medium`/`high`/`xhigh`/`max`/`auto`) |
| `MAX_THINKING_TOKENS` | Limit thinking budget |
| `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING` | Revert to fixed budget (Opus 4.6/Sonnet 4.6 only) |

**Context:**

| Variable | Purpose |
|:---------|:--------|
| `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` | Auto-compaction trigger threshold (e.g., `50` = 50%) |

**Features:**

| Variable | Purpose |
|:---------|:--------|
| `CLAUDE_CODE_DISABLE_CRON` | Disable scheduled tasks |
| `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` | Enable agent teams (`1`) |

### Data Usage & Privacy

**Training policy:**

| Account Type | Used for Training? |
|:------------|:-------------------|
| Free, Pro, Max (consumer) | Opt-in/out via settings at claude.ai/settings/data-privacy-controls |
| Team, Enterprise, API (commercial) | **Not used** unless opted into Developer Partner Program |

**Data retention:**

| Scenario | Retention |
|:---------|:---------|
| Consumer, training ON | 5 years |
| Consumer, training OFF | 30 days |
| Commercial (standard) | 30 days |
| Commercial (zero data retention) | Available for Enterprise |
| Local cache (`~/.claude/projects/`) | 30 days (configurable via `cleanupPeriodDays`) |

**Telemetry:**

| Service | Default on Claude API | Default on Bedrock/Vertex/Foundry | Disable Variable |
|:--------|:---------------------|:----------------------------------|:-----------------|
| Statsig (metrics) | On | Off | `DISABLE_TELEMETRY=1` |
| Sentry (errors) | On | Off | `DISABLE_ERROR_REPORTING=1` |
| Feedback (`/feedback`) | On | Off | `DISABLE_FEEDBACK_COMMAND=1` |

Set `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1` to disable everything at once.

> **Try This**: Install the Agent SDK (`pip install claude-agent-sdk`), set your `ANTHROPIC_API_KEY`, and write a 10-line Python script that uses the SDK to search your codebase for TODO comments and print a summary. Compare the experience to running the same query interactively in Claude Code.

### Key Takeaway

Claude Code's advanced features extend its reach far beyond the terminal: Chrome for browser testing, Channels for real-time event streams, Computer Use for GUI automation, and Voice for hands-free input. The Agent SDK unlocks the same capabilities for production systems and CI/CD pipelines. When deploying in enterprise environments, pin your model versions, configure managed settings for policy enforcement, understand the data retention policies for your account type, and disable telemetry if required by your security posture.

---

# Chapter 23: Conclusion & References

## TLDR

Claude Code is a comprehensive agentic coding environment that spans from a simple CLI tool to a full-featured development platform with IDE integration, desktop and web apps, CI/CD automation, scheduled routines, browser control, and an SDK for building custom agents. This chapter summarizes all features by maturity status, provides a recommended learning path from beginner to master, and collects all references to official documentation.

---

### Feature Maturity Overview

Understanding feature maturity helps you decide what to adopt today versus what to experiment with:

| Feature | Status |
|:--------|:-------|
| Core CLI | Stable |
| VS Code Extension | Stable |
| JetBrains Plugin | Beta |
| Desktop App (macOS/Windows) | Stable |
| Web (claude.ai/code) | Research Preview |
| Agent Teams | Experimental |
| Chrome Integration | Beta |
| Channels (Telegram/Discord/iMessage) | Research Preview |
| Code Review | Research Preview |
| Computer Use (Desktop) | Research Preview |
| Fast Mode | Research Preview |
| Routines (Scheduled Cloud Tasks) | Research Preview |
| Voice Dictation | Stable |
| Agent SDK | Stable |

"Stable" means production-ready with backward compatibility commitments. "Beta" means functional but the interface may change. "Research Preview" means experimental, and the feature, pricing, and availability may change based on feedback. "Experimental" means enabled via feature flag and not recommended for production.

### Recommended Learning Path

We have structured the 23 chapters of this paper into a progressive learning path:

```
LEVEL 1: START (Chapters 1-4)
├── Install Claude Code
├── Complete the Quickstart
├── Learn Interactive Mode (commands, shortcuts)
└── Understand the Agentic Loop

LEVEL 2: CUSTOMIZE (Chapters 5-8)
├── Write effective CLAUDE.md files
├── Understand context window management
├── Configure permission modes
└── Set up sandboxing

LEVEL 3: EXTEND (Chapters 9-13)
├── Create Skills and Slash Commands
├── Write Hooks for lifecycle automation
├── Connect MCP servers
├── Build custom Sub-Agents
└── Coordinate Agent Teams

LEVEL 4: SCALE (Chapters 14-18)
├── Install and manage Plugins
├── Use VS Code Extension and JetBrains Plugin
├── Run in Desktop App and Web interface
├── Integrate into CI/CD with GitHub Actions
└── Schedule tasks with Routines and /loop

LEVEL 5: MASTER (Chapters 19-22)
├── Configure settings hierarchy
├── Optimize model selection and effort levels
├── Master workflows and best practices
└── Explore advanced features (Chrome, Channels, SDK)
```

**For the absolute beginner**: Start by installing Claude Code (`npm install -g @anthropic-ai/claude-code`), launching it in a project directory, and asking "give me an overview of this codebase." That single interaction teaches you more about how Claude Code works than any amount of documentation.

**For the intermediate user**: Focus on writing an effective CLAUDE.md, setting up permission rules in `.claude/settings.json`, and learning the four-phase workflow (Explore, Plan, Implement, Commit). These three investments yield the highest return.

**For the advanced user**: Explore the Agent SDK for CI/CD integration, create custom subagents for specialized tasks, set up hooks for deterministic automation, and use managed settings for enterprise deployment. Agent teams and channels open new paradigms for autonomous and collaborative AI-assisted development.

### Summary of Core Concepts

Across all 23 chapters, several principles recur:

1. **Context is your most precious resource.** Everything Claude reads consumes context tokens. Manage aggressively with `/clear`, `/compact`, and subagents.

2. **Configuration flows downward.** Managed settings cannot be overridden. Project settings override user settings. This hierarchy enables both organizational control and personal customization.

3. **Verification beats instruction.** Giving Claude a test suite to run is more effective than explaining what "correct" means in prose.

4. **Layered extension model.** CLAUDE.md for instructions, Skills for domain knowledge, Hooks for deterministic automation, MCP for external tools, Subagents for delegation, Plugins for distribution.

5. **The agentic loop is the engine.** Claude reads your prompt, decides which tool to use, executes it, observes the result, and repeats. Understanding this loop helps you craft better prompts and debug unexpected behavior.

### References

#### Official Documentation

All documentation URLs follow the pattern `https://code.claude.com/docs/en/<page>`.

**Getting Started:**
- Quickstart: https://code.claude.com/docs/en/quickstart
- Interactive Mode: https://code.claude.com/docs/en/interactive-mode
- CLI Reference: https://code.claude.com/docs/en/cli-reference

**Core Concepts:**
- How Claude Code Works: https://code.claude.com/docs/en/how-claude-code-works
- Context Window: https://code.claude.com/docs/en/context-window
- Memory (CLAUDE.md): https://code.claude.com/docs/en/memory
- Permissions: https://code.claude.com/docs/en/permissions
- Permission Modes: https://code.claude.com/docs/en/permission-modes
- Sandboxing: https://code.claude.com/docs/en/sandboxing

**Extension System:**
- Features Overview: https://code.claude.com/docs/en/features-overview
- Skills: https://code.claude.com/docs/en/skills
- Hooks: https://code.claude.com/docs/en/hooks
- Hooks Guide: https://code.claude.com/docs/en/hooks-guide
- MCP (Model Context Protocol): https://code.claude.com/docs/en/mcp
- Sub-Agents: https://code.claude.com/docs/en/sub-agents
- Agent Teams: https://code.claude.com/docs/en/agent-teams

**Platforms:**
- Plugins: https://code.claude.com/docs/en/plugins
- Plugin Marketplaces: https://code.claude.com/docs/en/plugin-marketplaces
- VS Code: https://code.claude.com/docs/en/vs-code
- JetBrains: https://code.claude.com/docs/en/jetbrains
- Desktop App: https://code.claude.com/docs/en/desktop
- Claude Code on the Web: https://code.claude.com/docs/en/claude-code-on-the-web
- GitHub Actions: https://code.claude.com/docs/en/github-actions
- Routines: https://code.claude.com/docs/en/routines

**Configuration:**
- Settings: https://code.claude.com/docs/en/settings
- Model Configuration: https://code.claude.com/docs/en/model-config
- Environment Variables: https://code.claude.com/docs/en/env-vars
- Server-Managed Settings: https://code.claude.com/docs/en/server-managed-settings

**Workflows & Best Practices:**
- Common Workflows: https://code.claude.com/docs/en/common-workflows
- Best Practices: https://code.claude.com/docs/en/best-practices
- Costs: https://code.claude.com/docs/en/costs

**Advanced:**
- Chrome Integration: https://code.claude.com/docs/en/chrome
- Channels: https://code.claude.com/docs/en/channels
- Computer Use: https://code.claude.com/docs/en/computer-use
- Voice Dictation: https://code.claude.com/docs/en/voice-dictation
- Fast Mode: https://code.claude.com/docs/en/fast-mode
- Agent SDK Overview: https://code.claude.com/docs/en/agent-sdk/overview
- Headless Mode: https://code.claude.com/docs/en/headless

**Security & Privacy:**
- Data Usage: https://code.claude.com/docs/en/data-usage
- Security: https://code.claude.com/docs/en/security
- Authentication: https://code.claude.com/docs/en/authentication

**Cloud Providers:**
- Amazon Bedrock: https://code.claude.com/docs/en/amazon-bedrock
- Google Vertex AI: https://code.claude.com/docs/en/google-vertex-ai
- Microsoft Foundry: https://code.claude.com/docs/en/microsoft-foundry

**Full documentation index (LLM-friendly):** https://code.claude.com/docs/llms.txt

#### Agent SDK Repositories

- TypeScript SDK: https://github.com/anthropics/claude-agent-sdk-typescript
- Python SDK: https://github.com/anthropics/claude-agent-sdk-python
- Example Agents: https://github.com/anthropics/claude-agent-sdk-demos
- Official Plugins: https://github.com/anthropics/claude-plugins-official

#### Additional Resources

- Claude Platform Documentation: https://platform.claude.com/docs
- Anthropic API Models Overview: https://platform.claude.com/docs/en/about-claude/models/overview
- Claude Pricing: https://claude.com/pricing
- Anthropic Trust Center: https://trust.anthropic.com
- Anthropic Privacy Center: https://privacy.anthropic.com
- JSON Schema for Settings: https://json.schemastore.org/claude-code-settings.json

#### Community Resources

- Claude Code GitHub Issues: https://github.com/anthropics/claude-code/issues
- MDM Deployment Templates: https://github.com/anthropics/claude-code/tree/main/examples/mdm
- Development Container Reference: https://github.com/anthropics/claude-code/tree/main/.devcontainer
- luongnv89/claude-howto: https://github.com/luongnv89/claude-howto (Community-maintained guide; useful as supplementary reference, though it may lag behind official docs and some sections may be outdated or incomplete)

> **Try This**: Pick one feature from this paper that you have not tried yet. It could be setting up a Hook, installing a Plugin, connecting an MCP server, or writing a Skill. Implement it in your current project and evaluate whether it improves your workflow. The best way to learn Claude Code is to use Claude Code.

### Key Takeaway

Claude Code is not just a chatbot in a terminal — it is a comprehensive agentic development platform that spans from interactive coding assistance to production CI/CD automation. The layered configuration system lets organizations enforce policies while individuals customize their experience. The extension model (Skills, Hooks, MCP, Sub-Agents, Plugins) makes it infinitely adaptable. And the Agent SDK opens it up as a building block for custom applications. Start simple, add complexity only when you need it, and always give Claude a way to verify its work.

---