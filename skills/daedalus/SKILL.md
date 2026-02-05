---
name: daedalus
description: Plan and orchestrate coding work using the Daedalus CLI and Talos daemon. Daedalus is an AI planning CLI that creates structured beans (task files) for coding agents to execute autonomously. Use when planning features, breaking down work into tasks, or running autonomous agent workflows with beans.
license: MIT
compatibility: Requires Node.js >= 20 and the beans CLI (brew install hmans/beans/beans)
metadata:
  author: internet-development
  version: "1.0"
---

# Daedalus

## Overview

Daedalus is an AI planning CLI that creates structured tasks (beans) for coding agents to execute autonomously. Instead of babysitting agents, you plan the work with Daedalus and let Talos (the daemon) execute it.

- **Repository**: [internet-development/daedalus](https://github.com/internet-development/daedalus)
- **npm**: `npm install -g @internet-dev/daedalus`
- **Philosophy**: [A Beans Based AI Workflow](https://caidan.dev/blog/2026-01-29-a-beans-based-ai-workflow/)

The core insight: the bottleneck isn't agents — it's having clear enough tasks for them to work on.

```
You (planning) ──→ Daedalus ──→ Beans (.beans/) ──→ Talos ──→ Coding Agents
     ↑                                                              │
     └──────────── review PRs, iterate on plan ─────────────────────┘
```

## Prerequisites

- **Node.js** >= 20
- **beans CLI**: `brew install hmans/beans/beans` (or `go install github.com/hmans/beans@latest`)
- One of:
  - **Claude Code CLI** (recommended) — uses subscription, no API key
  - `ANTHROPIC_API_KEY` — direct Anthropic API
  - `OPENAI_API_KEY` — OpenAI alternative

## Quick Start

```bash
npm install -g @internet-dev/daedalus
cd your-project
beans init
daedalus
```

## The `daedalus` CLI

Interactive AI-assisted planning agent. Start a planning session:

```bash
daedalus                       # Session selector
daedalus --new                 # Fresh session
daedalus --continue            # Resume most recent
daedalus --mode brainstorm     # Start in brainstorm mode
daedalus tree                  # Show bean dependency tree
```

### Planning Modes

| Mode | Purpose |
|------|---------|
| `new` | Create new beans through guided conversation |
| `refine` | Improve and clarify existing draft beans |
| `critique` | Run expert review on draft beans |
| `sweep` | Check consistency across related beans |
| `brainstorm` | Explore design options with Socratic questioning |
| `breakdown` | Decompose work into actionable child beans (2-5 min each) |

### In-Session Commands

| Command | Action |
|---------|--------|
| `/help` | Show all commands |
| `/mode [name]` | Switch planning mode |
| `/prompt [name]` | Select a built-in prompt |
| `/edit` | Open `$EDITOR` for multi-line input |
| `/sessions` | List and switch sessions |
| `/new` | Start a new session |
| `/tree` | Display bean tree |
| `/start` / `/stop` | Start/stop Talos daemon |
| `/status` | Show daemon status |
| `/quit` | Exit |

### Expert Advisors

Daedalus can consult 9 expert personas for multi-perspective analysis:

| Expert | Focus |
|--------|-------|
| Pragmatist | Ship fast, avoid over-engineering |
| Architect | Scalability, maintainability, long-term health |
| Skeptic | Edge cases, failure modes, what could go wrong |
| Simplifier | Reduce complexity, find simpler alternatives |
| Security | Auth, data exposure, input validation, attack vectors |
| Researcher | Papers, docs, best practices |
| Codebase Explorer | Patterns, dependencies, existing architecture |
| UX Reviewer | User experience, discoverability, interface design |
| Critic | Synthesize multiple perspectives into actionable feedback |

## The `talos` CLI

Talos is the daemon that watches `.beans/` and spawns coding agents to work on todo beans. Named after the bronze automaton that protected Crete.

```bash
talos start              # Start daemon (background)
talos start --no-detach  # Start in foreground
talos stop               # Stop daemon
talos stop --force       # Force kill
talos status             # Show daemon status
talos logs               # View recent logs
talos logs -f            # Follow logs
talos config             # Show configuration
talos config --validate  # Validate talos.yml
```

### The Ralph Loop

Talos runs a [ralph loop](https://www.humanlayer.dev/blog/brief-history-of-ralph):

1. **Pick a bean** — Query todo/in-progress beans, filter blocked ones, sort by priority
2. **Mark in-progress** — Update bean status
3. **Generate prompt** — Implementation prompt for tasks/bugs, review prompt for epics
4. **Run agent** — Claude Code, OpenCode, or Codex
5. **Handle result** — On success, check status. On failure, retry up to 3 times
6. **Pick next** — Repeat until no beans remain

## Configuration

Create `talos.yml` in your project root:

```yaml
agent:
  backend: claude
  claude:
    model: claude-sonnet-4-20250514

planning_agent:
  provider: claude_code
  model: claude-sonnet-4-20250514

planning:
  skills_directory: ./skills
  modes:
    brainstorm:
      skill: beans-brainstorming
    breakdown:
      skill: beans-breakdown
```

### Agent Backends

| Backend | Command | API Key Required |
|---------|---------|-----------------|
| `claude` | Claude Code CLI | No (uses subscription) |
| `opencode` | OpenCode CLI | No (uses subscription) |
| `codex` | OpenAI Codex CLI | Yes (`OPENAI_API_KEY`) |

### Planning Providers

| Provider | Description |
|----------|-------------|
| `claude_code` | Claude Code CLI (recommended, no API key) |
| `claude` | Anthropic API (requires `ANTHROPIC_API_KEY`) |
| `openai` | OpenAI API (requires `OPENAI_API_KEY`) |
| `opencode` | OpenCode CLI |

## Beans

Beans are plain markdown files with YAML front matter, stored in `.beans/` and tracked in git.

```markdown
---
id: daedalus-abc123
title: Add user authentication
type: feature
status: todo
priority: high
parent: daedalus-parent-id
blockedBy:
  - daedalus-other-id
---

## Problem

Users can't log in...

## Solution

Implement email + password auth...

## Files

- `src/auth/login.ts` - Login handler
- `src/auth/session.ts` - Session management
```

### Bean Types

| Type | Use For |
|------|---------|
| `milestone` | Release target with deadline |
| `epic` | Thematic group of related work |
| `feature` | User-facing capability |
| `bug` | Something broken to fix |
| `task` | Concrete implementation work |

### Bean Statuses

| Status | Meaning |
|--------|---------|
| `draft` | Not ready for execution |
| `todo` | Ready to be picked up |
| `in_progress` | Currently being worked on |
| `done` | Completed |

### Bean Commands

```bash
beans create "Title" -t task -s todo -d "Description..."
beans update <id> --status done
beans update <id> --parent <parent-id>
beans update <id> --blocking <other-id>
beans query '{ beans { id title status } }'
```

## Workflow

The recommended workflow with Daedalus:

1. **Plan** — `daedalus --mode brainstorm` to explore the design space
2. **Break down** — `daedalus --mode breakdown` to decompose into small beans
3. **Critique** — `daedalus --mode critique` to get expert feedback
4. **Execute** — `talos start` to let agents work autonomously
5. **Review** — Check agent output, refine beans, plan next batch

## Runtime Data

The `.talos/` directory (gitignored) stores:

| Path | Contents |
|------|----------|
| `.talos/output/` | Agent execution logs |
| `.talos/chat-history.json` | Planning chat persistence |
| `.talos/prompts/` | Custom planning prompts |
| `.talos/daemon.pid` | Daemon process ID |
| `.talos/daemon-status.json` | Daemon state |
