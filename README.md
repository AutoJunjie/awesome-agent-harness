# Awesome Agent Harness [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of tools, frameworks, and resources for **agent harness engineering** — the discipline of designing environments, constraints, and feedback loops that make AI coding agents reliable at scale.

## What is an Agent Harness?

An agent harness is the infrastructure that wraps around an LLM coding agent. It's everything except the model itself: session management, context delivery, tool design, architectural enforcement, failure recovery, and human oversight.

OpenAI's [Harness Engineering](https://openai.com/index/harness-engineering/) blog defined the term: *"When a software engineering team's primary job is no longer to write code, but to design environments, specify intent, and build feedback loops that allow agents to do reliable work."* Their team built 1M+ lines of production code with zero human-written lines using this approach.

Anthropic's Claude Code team [discovered the same principles](https://x.com/trq212/status/2027463795355095314) from the tool design side: the harness matters more than the model. Fewer, more expressive tools beat a long menu of narrow ones. Progressive disclosure — letting the agent recursively discover context across layers — outperforms loading everything upfront. *"Designing an agent's action space is as much an art as it is a science."*

## Core Principles

From the two seminal references above:

1. **Humans steer, agents execute** — Engineers design environments and review outcomes, not write code
2. **Repository knowledge is the system of record** — If it's not in the repo, it doesn't exist to the agent. Slack threads, Google Docs, and tribal knowledge are invisible
3. **AGENTS.md is a table of contents, not an encyclopedia** — Point to deeper sources of truth; don't dump everything in one file
4. **Enforce architecture mechanically** — Custom linters, structural tests, and CI checks replace code review for invariants
5. **Agent legibility is the goal** — Optimize code for agent readability first, human readability second
6. **Fewer tools, more expressiveness** — Progressive disclosure and composable primitives beat sprawling toolkits
7. **See like an agent** — Read the model's outputs, watch where it struggles, and evolve the harness accordingly
8. **Corrections are cheap, waiting is expensive** — At high agent throughput, fix-forward beats blocking merge gates

## Contents

- [What is an Agent Harness?](#what-is-an-agent-harness)
- [Core Principles](#core-principles)
- [Full Lifecycle Platforms](#full-lifecycle-platforms)
- [Agent Orchestrators](#agent-orchestrators)
- [Task Runners](#task-runners)
- [Agent Harness Frameworks](#agent-harness-frameworks)
- [Coding Agents](#coding-agents)
- [Requirements & Spec Tools](#requirements--spec-tools)
- [Standards & Protocols](#standards--protocols)
- [Reference & Knowledge](#reference--knowledge)
- [Contributing](#contributing)

## Full Lifecycle Platforms

Tools that span from requirements to delivery with human-in-the-loop approval.

- [Chorus](https://github.com/Chorus-AIDLC/Chorus) — Agent harness that wraps around LLM agents to manage session lifecycle, task state, sub-agent orchestration (Claude Code Agent Teams), and proof of work. Multiple AI agents (PM, Developer, Admin) and humans collaborate through the full workflow from requirements to delivery. Inspired by [AI-DLC](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/). Core philosophy: *Reversed Conversation* — AI proposes, humans verify.
- [GitHub Agentic Workflows](https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/) — GitHub Actions with coding agent engines (Copilot, Claude Code, Codex). Issue → agent → PR with sandboxing and permissions.

## Agent Orchestrators

Orchestrators solve the throughput problem: at high agent velocity, you need parallel execution with worktree isolation so agents don't step on each other. As OpenAI found, "corrections are cheap, waiting is expensive" — these tools maximize concurrent agent throughput.

- [Vibe Kanban](https://github.com/BloopAI/vibe-kanban) — Kanban-based orchestrator with git worktree isolation per agent. Supports 10+ coding agents. Enforces the "one agent, one worktree" pattern that keeps parallel execution clean.
- [Emdash](https://github.com/generalaction/emdash) — Open-source Agentic Development Environment (YC W26). Runs parallel agents in isolated worktrees, locally or over SSH — making the "corrections are cheap" principle practical for remote teams.
- [Warp](https://github.com/warpdotdev/Warp) — Agentic development environment built for coding with multiple AI agents.
- [VibeHQ](https://github.com/VibeHQ/vibehq) — Orchestrate multiple CLI agents (Claude Code, Codex, Gemini CLI) as a company team.
- [Beehive](https://github.com/mbezhanov/beehive) — Multi-workspace agent orchestrator for parallel issue resolution.
- [Agent Orchestrator](https://github.com/pkarnal/agent-orchestrator) — Lightweight orchestrator: `ao init --tracker github --agent claude-code --runtime tmux`.
- [Oh My OpenCode](https://github.com/code-yeongyu/oh-my-opencode) — Performance optimization harness for OpenCode with 44 lifecycle hooks.
- [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) — Skills, instincts, memory, and security harness for Claude Code and Codex.
- [Oh My AG](https://github.com/first-fluke/oh-my-ag) — Multi-agent harness for Google Antigravity with 6 specialized agents.

## Task Runners

Task runners bridge the gap between issue trackers and coding agents. They embody the "humans steer, agents execute" principle: a human (or PM agent) creates the issue, the runner spawns an agent, and the output is a PR ready for review.

- [Symphony](https://github.com/openai/symphony) — OpenAI's reference implementation of harness engineering. A daemon that polls Linear issues, spawns isolated Codex agents per task, and delivers PRs. Embodies "humans steer, agents execute" at scale.
- [Linear Coding Agent Harness](https://github.com/coleam00/Linear-Coding-Agent-Harness) — Linear → autonomous coding agent → PR pipeline.
- [GitHub Copilot Coding Agent](https://github.blog/ai-and-ml/github-copilot/whats-new-with-github-copilot-coding-agent/) — Built-in GitHub issue → Copilot agent → PR.
- [Axon](https://github.com/axon-ai/axon) — Kubernetes-native framework. Apply a Task CRD, get back a PR and cost in USD. TaskSpawner watches GitHub Issues.
- [Dexto](https://github.com/truffle-ai/dexto) — Coding agent and general agent harness for building agentic applications.

## Agent Harness Frameworks

Frameworks for building custom harnesses. Following the principle that "fewer tools, more expressiveness" beats sprawling toolkits, these provide composable primitives rather than opinionated workflows.

- [Deep Agents](https://github.com/langchain-ai/deepagents) — Agent harness built on LangChain/LangGraph. Implements progressive disclosure through planning tools and subagent spawning — agents discover context layer by layer rather than loading everything upfront.
- [Gambit](https://github.com/bolt-foundry/gambit) — Framework for building, running, and verifying LLM workflows.
- [Harness Kit](https://github.com/deepklarity/harness-kit) — Patterns and engineering practices for building with AI agents.
- [Desloppify](https://github.com/peteromallet/desloppify) — Agent harness focused on making AI-generated code well-engineered.
- [Bridle](https://github.com/neiii/bridle) — TUI/CLI config manager for agent harnesses (Amp, Claude Code, OpenCode, Goose, Copilot CLI, Droid).

## Coding Agents

The execution layer. In harness engineering, the agent is a commodity — the harness is the differentiator. These agents write code; everything above them determines whether that code is useful.

- [Claude Code](https://code.claude.com/) — Anthropic's coding agent. The team's own harness pioneered "seeing like an agent" — progressive disclosure via skill files, fewer composable tools over many narrow ones. Agent Teams enables multi-agent coordination. The Claude Agent SDK extends the harness beyond coding.
- [Codex](https://github.com/openai/codex) — OpenAI's coding agent. Cloud and CLI modes.
- [OpenCode](https://github.com/sst/opencode) — Open-source coding agent with a plugin system (44 lifecycle hooks), server mode HTTP API, and TypeScript SDK. The most extensible harness integration point for custom workflows.
- [Gemini CLI](https://github.com/google-gemini/gemini-cli) — Google's CLI coding agent.
- [Kiro CLI](https://kiro.dev/) — AWS's CLI coding agent with spec-driven workflow.
- [Amp](https://amp.dev/) — Sourcegraph's coding agent.
- [Cursor Agent CLI](https://www.cursor.com/) — Cursor's command-line agent mode.
- [GitHub Copilot CLI](https://github.com/github/copilot-cli) — GitHub's CLI coding agent.
- [OpenClaw](https://github.com/openclaw/openclaw) — AI agent runtime. Orchestrates agents across messaging channels with skill system and sub-agent spawning.
- [Aider](https://github.com/paul-gauthier/aider) — AI pair programming in your terminal.

## Requirements & Spec Tools

The planning layer addresses the biggest harness gap: agents can write code, but someone has to decide what to build. "Repository knowledge is the system of record" — these tools generate the specs and requirements that agents consume.

- [Kiro IDE](https://kiro.dev/) — AWS's spec-driven development IDE. Generates structured specs and manages requirements.
- [OpenSpec](https://github.com/FissionAI/openspec) — Spec-driven development CLI. Generate structured specs from natural language.
- [Spec Kit](https://github.com/github/spec-kit) — GitHub's spec generation toolkit.
- [agents.md](https://agents.md/) — Open standard for project-level agent instructions. Following the principle that "AGENTS.md is a table of contents, not an encyclopedia" — it should point to deeper sources of truth.

## Standards & Protocols

- [MCP (Model Context Protocol)](https://modelcontextprotocol.io/) — Open standard for connecting AI models to external tools and data sources.
- [agents.md](https://agents.md/) — Open standard for project-level agent configuration.
- [AGENTS.md](https://openai.com/index/introducing-agents-md/) — OpenAI's convention for repository-level agent instructions.

## Reference & Knowledge

### Seminal References

- [Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — OpenAI's defining blog post. How they built 1M+ lines with zero human-written code. Introduced the concepts of repository knowledge as system of record, progressive context disclosure, and mechanical architecture enforcement.
- [Lessons from Building Claude Code: Seeing Like an Agent](https://x.com/trq212/status/2027463795355095314) — Thariq (Claude Code lead) on designing agent action spaces. Fewer tools beat more tools. Progressive disclosure outperforms upfront loading. The harness must evolve with the model.
- [Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — Anthropic's guide: simple, composable patterns beat complex frameworks.

### Articles

- [Building an AI-Native Engineering Team](https://developers.openai.com/codex/guides/build-ai-native-engineering-team/) — OpenAI's guide to structuring teams around AI-first workflows.
- [The Emerging "Harness Engineering" Playbook](https://www.ignorance.ai/p/the-emerging-harness-engineering) — How OpenAI is retooling engineering teams.
- [Conductors to Orchestrators: The Future of Agentic Coding](https://www.oreilly.com/radar/conductors-to-orchestrators-the-future-of-agentic-coding/) — O'Reilly overview of the orchestration landscape.
- [My LLM Coding Workflow Going into 2026](https://medium.com/@addyosmani/my-llm-coding-workflow-going-into-2026-52fe1681325e) — Addy Osmani's specs-first approach.
- [How the Claude Code Team Designs Agent Tools](https://www.anup.io/how-the-claude-code-team-designs-agent-tools/) — Analysis of progressive disclosure and tool subtraction in agent design.

### Talks

- [The Future of Coding is Agents — Andrej Karpathy (YC)](https://www.youtube.com/watch?v=fqVLjtvWgq8) — Landmark talk on the trajectory from assistants to agents.
- [Agentic Coding — Armin Ronacher](https://www.youtube.com/watch?v=nfOVgz_omlU) — Creator of Flask on adopting agentic workflows in practice.
- [12 Rules of Harness Engineering](https://www.youtube.com/watch?v=BabEnt6VjtE) — Practical rules derived from OpenAI's approach.

### Documentation Patterns

- [agent-harness](https://github.com/MattMagg/agent-harness) — Principles, checklists, and invariants for AI coding workflows.
- [harness-kit](https://github.com/deepklarity/harness-kit) — Engineering patterns for building with AI agents.

## Contributing

Contributions welcome! When suggesting additions, include:
- A one-line description of what the tool does
- Why it belongs in this list (which layer of the stack it addresses)
