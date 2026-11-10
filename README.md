# kilocode_agents

A collection of ready-to-use agent definitions for [Kilo Code](https://kilocode.ai). Each agent is a single `.md` file that can be dropped into your project's `.kilo/agent/` directory (or the global `~/.config/kilo/agent/` directory) to extend Kilo Code with a specialized role.

## Agents

| Agent | Description |
| ----- | ----------- |
| `architect` | Turns a requirement brief into an implementation-ready plan (architecture, components, file layout, tradeoffs, ordered steps). Call BEFORE implementation of any non-trivial feature or refactor. Read-only: produces plans, never code. |
| `ask-subagent` | Answers codebase questions ("how does X work", "where is Y implemented", "what does Z do") with file:line evidence, and can web-search for external context. Read-only: never changes anything. |
| `agent-creator` | Creates new Kilo agent files (`.md` in `.kilo/agent/` or `~/.config/kilo/agent/`) with correct frontmatter and least-privilege permissions. Requires a self-contained brief (name, purpose, mode, tools). |
| `code-reviewer` | Inspects diffs, PRs, or recent changes for correctness, bugs, security, convention violations, and test gaps, returning actionable findings ranked by severity. Read-only: findings, never edits. |
| `code-agent` | Writes, edits, and deletes code and files according to a given brief, then verifies the result (compile/tests where available). Use for ANY coding task or file write. |
| `debug-agent` | Reproduces, root-causes, and fixes bugs, runtime errors, failing tests, broken builds, and regressions. Call when something is broken and the cause is unknown. |
| `main` | Strategic coordinator that decomposes tasks and dispatches each to the matching subagent (architect, code-agent, debug-agent, ask-subagent, code-reviewer, pull-request-manager, vision-analyst, security-inspector, rule-maker, agent-creator), then integrates their results into one deliverable. Read-only itself: never writes files or runs write-capable commands — all writes are dispatched to subagents. |
| `pull-request-manager` | Generates a PR title (conventional-commit format, under 50 chars) and a structured description (What Changed / Why / How to Test / Checklist) from a diff or change summary. Read-only: produces text, never code changes. |
| `rule-maker` | Creates, updates, and merges rule files (`.kilo/rules/*.md`, global or project-scoped) with proper frontmatter. Read-only outside rule directories. |
| `security-inspector` | Performs read-only security audits of code, dependencies, config, secrets, and infra, producing a severity-classified report (critical/high/medium/low). |
| `vision-analyst` | Inspects screenshots, UI mockups, diagrams, design files, and images to extract layout, text, colors, and visual requirements. Read-only: analysis, never edits. |

## Usage

1. Copy the agent file(s) you need into your project's `.kilo/agent/` directory.
2. Invoke the agent by name (e.g. `@architect`) or let Kilo Code dispatch it automatically when a task matches its trigger.

> **Note:** `main.md` overrides the default primary orchestrator for the whole project — install it only if you want mandatory subagent dispatch everywhere.

## License

MIT — see LICENSE
