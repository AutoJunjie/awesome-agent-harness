# Awesome Agent Harness [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of tools, frameworks, and resources for agent harness engineering — the discipline of orchestrating AI coding agents to plan, execute, and deliver software with human oversight.

## Contents

- [How These Tools Fit Together](#how-these-tools-fit-together)
- [Full Lifecycle Platforms](#full-lifecycle-platforms)
- [Agent Orchestrators](#agent-orchestrators)
- [Task Runners](#task-runners)
- [Agent Harness Frameworks](#agent-harness-frameworks)
- [Coding Agents](#coding-agents)
- [Requirements & Spec Tools](#requirements--spec-tools)
- [Standards & Protocols](#standards--protocols)
- [Reference & Knowledge](#reference--knowledge)
- [Contributing](#contributing)

## How These Tools Fit Together

```
┌─────────────────────────────────────────────────────────┐
│                   Human Oversight                        │
├─────────────────────────────────────────────────────────┤
│  Planning & Requirements    │  Review & Approval         │
│  (Idea → Spec → Task DAG)  │  (PR Review → Merge)       │
├─────────────────────────────────────────────────────────┤
│              Orchestration & Scheduling                   │
│  (Parallel execution, worktree isolation, CI feedback)   │
├─────────────────────────────────────────────────────────┤
│              Coding Agents (Execution)                    │
│  (Claude Code, Codex, Gemini CLI, OpenCode, ...)        │
└─────────────────────────────────────────────────────────┘
```

Most tools cover one layer. The challenge is connecting them.

## Full Lifecycle Platforms

Tools that span from requirements to delivery with human-in-the-loop approval.

- [Chorus](https://github.com/Chorus-AIDLC/Chorus) — AI-DLC platform: idea → elaboration → proposal → task DAG → agent execution → human verification. Agents propose, humans approve. Works with any MCP-compatible agent.
- [GitHub Agentic Workflows](https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/) — GitHub Actions with coding agent engines (Copilot, Claude Code, Codex). Issue → agent → PR with sandboxing and permissions.

## Agent Orchestrators

Tools for running multiple coding agents in parallel with isolation.

- [Vibe Kanban](https://github.com/BloopAI/vibe-kanban) — Kanban board for AI agents. Git worktree isolation, 10+ agent support, built-in diff review. Cloud team version available.
- [Emdash](https://github.com/generalaction/emdash) — Open-source Agentic Development Environment (YC W26). Parallel agents in isolated worktrees, local or SSH remote.
- [Warp](https://github.com/warpdotdev/Warp) — Agentic development environment built for coding with multiple AI agents.
- [VibeHQ](https://github.com/VibeHQ/vibehq) — Orchestrate multiple CLI agents (Claude Code, Codex, Gemini CLI) as a company team. Contract-driven development with API spec sign-offs.
- [Beehive](https://github.com/mbezhanov/beehive) — Multi-workspace agent orchestrator for parallel issue resolution.
- [Agent Orchestrator](https://github.com/pkarnal/agent-orchestrator) — Lightweight orchestrator: `ao init --tracker github --agent claude-code --runtime tmux`.
- [Oh My OpenCode](https://github.com/code-yeongyu/oh-my-opencode) — Performance optimization harness for OpenCode with 44 lifecycle hooks.
- [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) — Skills, instincts, memory, and security harness for Claude Code and Codex.
- [Oh My AG](https://github.com/first-fluke/oh-my-ag) — Multi-agent harness for Google Antigravity with 6 specialized agents.

## Task Runners

Tools that automate the issue → code → PR pipeline.

- [Symphony](https://github.com/openai/symphony) — OpenAI's daemon that polls Linear, spawns Codex agents per issue, and opens PRs. The reference implementation of harness engineering.
- [Linear Coding Agent Harness](https://github.com/coleam00/Linear-Coding-Agent-Harness) — Linear → autonomous coding agent → PR pipeline.
- [GitHub Copilot Coding Agent](https://github.blog/ai-and-ml/github-copilot/whats-new-with-github-copilot-coding-agent/) — Built-in GitHub issue → Copilot agent → PR.
- [Axon](https://github.com/axon-ai/axon) — Kubernetes-native framework. Apply a Task CRD, get back a PR and cost in USD. TaskSpawner watches GitHub Issues.
- [Dexto](https://github.com/truffle-ai/dexto) — Coding agent and general agent harness for building agentic applications.

## Agent Harness Frameworks

Frameworks and kits for building your own agent harness.

- [Deep Agents](https://github.com/langchain-ai/deepagents) — Agent harness built on LangChain/LangGraph with planning tool, filesystem backend, and subagent spawning.
- [Gambit](https://github.com/bolt-foundry/gambit) — Framework for building, running, and verifying LLM workflows.
- [Harness Kit](https://github.com/deepklarity/harness-kit) — Patterns and engineering practices for building with AI agents.
- [Desloppify](https://github.com/peteromallet/desloppify) — Agent harness focused on making AI-generated code well-engineered.
- [Bridle](https://github.com/neiii/bridle) — TUI/CLI config manager for agent harnesses (Amp, Claude Code, OpenCode, Goose, Copilot CLI, Droid).

## Coding Agents

The execution layer — these are the agents that actually write code.

- [OpenCode](https://github.com/sst/opencode) — Open-source coding agent with plugin system, server mode, and SDK.
- [Claude Code](https://code.claude.com/) — Anthropic's agentic coding tool. Supports Agent Teams (multi-agent), hooks, skills, and MCP.
- [Codex](https://github.com/openai/codex) — OpenAI's coding agent. Cloud and CLI modes.
- [Gemini CLI](https://github.com/google-gemini/gemini-cli) — Google's CLI coding agent.
- [Amp](https://amp.dev/) — Sourcegraph's coding agent.
- [Cursor Agent CLI](https://www.cursor.com/) — Cursor's command-line agent mode.
- [GitHub Copilot CLI](https://github.com/github/copilot-cli) — GitHub's CLI coding agent.
- [OpenClaw](https://github.com/openclaw/openclaw) — AI agent runtime. Orchestrates agents across messaging channels with skill system and sub-agent spawning.
- [Kiro CLI](https://kiro.dev/) — AWS's CLI coding agent with spec-driven workflow.
- [Aider](https://github.com/paul-gauthier/aider) — AI pair programming in your terminal.

## Requirements & Spec Tools

Tools for the "what to build" layer — specs, requirements, and task planning.

- [OpenSpec](https://github.com/FissionAI/openspec) — Spec-driven development CLI. Generate structured specs from natural language.
- [Spec Kit](https://github.com/github/spec-kit) — GitHub's spec generation toolkit.
- [Kiro IDE](https://kiro.dev/) — AWS's spec-driven development IDE. Generates structured specs and manages requirements.
- [agents.md](https://agents.md/) — Open standard for guiding AI coding agents with project-specific instructions.

## Standards & Protocols

- [MCP (Model Context Protocol)](https://modelcontextprotocol.io/) — Open standard for connecting AI models to external tools and data sources.
- [Kiro IDE](https://kiro.dev/) — AWS's spec-driven development IDE. Generates structured specs and manages requirements.
- [agents.md](https://agents.md/) — Open standard for project-level agent configuration.
- [AGENTS.md](https://openai.com/index/introducing-agents-md/) — OpenAI's convention for repository-level agent instructions.

## Reference & Knowledge

Articles, talks, and guides on harness engineering practices.

### Articles

- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — OpenAI's seminal blog post. How they built 1M+ lines of code with zero human-written code.
- [Building an AI-Native Engineering Team](https://developers.openai.com/codex/guides/build-ai-native-engineering-team/) — OpenAI's guide to structuring teams around AI-first workflows.
- [The Emerging "Harness Engineering" Playbook](https://www.ignorance.ai/p/the-emerging-harness-engineering) — How OpenAI is retooling engineering teams.
- [Harness Engineering: How to Supervise Code You Can't Read](https://decision.substack.com/p/harness-engineering-how-to-supervise) — Practical supervision patterns.
- [Conductors to Orchestrators: The Future of Agentic Coding](https://www.oreilly.com/radar/conductors-to-orchestrators-the-future-of-agentic-coding/) — O'Reilly overview of the orchestration landscape.
- [My LLM Coding Workflow Going into 2026](https://medium.com/@addyosmani/my-llm-coding-workflow-going-into-2026-52fe1681325e) — Addy Osmani's specs-first approach.

### Talks

- [The Future of Coding is Agents — Andrej Karpathy (YC)](https://www.youtube.com/watch?v=fqVLjtvWgq8) — Landmark talk on the trajectory from assistants to agents.
- [Agentic Coding — Armin Ronacher](https://www.youtube.com/watch?v=nfOVgz_omlU) — Creator of Flask on adopting agentic workflows in practice.
- [12 Rules of Harness Engineering](https://www.youtube.com/watch?v=BabEnt6VjtE) — Practical rules derived from OpenAI's approach.

### Documentation Patterns

- [agent-harness](https://github.com/MattMagg/agent-harness) — Principles, checklists, and invariants for AI coding workflows.
- [harness-kit](https://github.com/deepklarity/harness-kit) — Engineering patterns for building with AI agents.

## Contributing

Contributions welcome! Please read the [contributing guidelines](CONTRIBUTING.md) before submitting a PR.

When suggesting additions, include:
- A one-line description of what the tool does
- Why it belongs in this list (which layer of the stack it addresses)

