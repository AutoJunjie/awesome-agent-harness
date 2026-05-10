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
- [Agent Runtimes](#agent-runtimes)
- [Agent Knowledge & Memory](#agent-knowledge--memory)
- [Coding Agents](#coding-agents)
- [Requirements & Spec Tools](#requirements--spec-tools)
- [Standards & Protocols](#standards--protocols)
- [Methodologies & Workflows](#methodologies--workflows)
- [Reference & Knowledge](#reference--knowledge)
- [Contributing](#contributing)

## Full Lifecycle Platforms

Tools that span from requirements to delivery with human-in-the-loop approval.

- [Chorus](https://github.com/Chorus-AIDLC/Chorus) — Agent harness for requirements-to-delivery. Task DAGs, sub-agent orchestration (Agent Teams), proof of work, human approval gates. AI proposes, humans verify.

<p align="center"><video src="https://github.com/AutoJunjie/awesome-agent-harness/edit/main/demo.mp4" controls></video></p>

- [GitHub Agentic Workflows](https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/) — GitHub Actions with coding agent engines (Copilot, Claude Code, Codex). Issue → agent → PR with sandboxing and permissions.
- [Almirant](https://almirant.ai/?utm_source=awesome-agent-harness&utm_medium=awesome-list&utm_campaign=march-2026) — Operating system for human-agent teams. Persistent context across sessions, shared memory between agents, structured task lifecycle (plan → implement → review → deploy), and human approval gates. Designed for teams where humans and agents work together continuously — not just one-shot task execution.
- [Paperclip](https://github.com/paperclipai/paperclip) — Open-source orchestration for zero-human companies. Budget/cost tracking, company templates (ClipMart), and autonomous agent coordination. Pushes the "agents execute" principle to its extreme — designed for fully autonomous operation with no human in the loop.
- [Multica](https://github.com/multica-ai/multica) — Open-source managed agents platform. "Turn coding agents into real teammates" — assign tasks, track progress, compound skills across sessions. Validates the core premise that agents need team-level management, not just individual harnesses.

## Agent Orchestrators

Orchestrators solve the throughput problem: at high agent velocity, you need parallel execution with worktree isolation so agents don't step on each other. As OpenAI found, "corrections are cheap, waiting is expensive" — these tools maximize concurrent agent throughput.

- [Vibe Kanban](https://github.com/BloopAI/vibe-kanban) — Kanban-based orchestrator with git worktree isolation per agent. Supports 10+ coding agents. Enforces the "one agent, one worktree" pattern that keeps parallel execution clean.
- [Emdash](https://github.com/generalaction/emdash) — Open-source Agentic Development Environment (YC W26). Runs parallel agents in isolated worktrees, locally or over SSH — making the "corrections are cheap" principle practical for remote teams.
- [Warp](https://github.com/warpdotdev/Warp) — Agentic development environment built for coding with multiple AI agents.
- [Oh My OpenCode](https://github.com/code-yeongyu/oh-my-opencode) — Performance optimization harness for OpenCode with 44 lifecycle hooks.
- [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) — Skills, instincts, memory, and security harness for Claude Code and Codex.
- [Desplega Agent Swarm](https://github.com/desplega-ai/agent-swarm) — Open-source multi-agent orchestration framework. Coordinates specialized AI agents (Claude Code-powered) through task delegation, session continuity, shared memory, and service discovery. Features include epics, scheduling, Slack integration, and cross-agent communication channels.
- [Composio Agent Orchestrator](https://github.com/ComposioHQ/agent-orchestrator) — Agentic orchestrator for parallel coding agents. Plans tasks, spawns agents in isolated worktrees, autonomously handles CI fixes, merge conflicts, and code reviews.
- [Oh My AG](https://github.com/first-fluke/oh-my-ag) — Multi-agent harness for Google Antigravity with 6 specialized agents.
- [Oh My Codex](https://github.com/Yeachan-Heo/oh-my-codex) — Hooks, agent teams, and HUD for Codex. Adds lifecycle hooks and multi-agent coordination on top of OpenAI's CLI agent.
- [Oh My Claude Code](https://github.com/Yeachan-Heo/oh-my-claudecode) — Teams-first multi-agent orchestration for Claude Code. Ultrapilot mode runs 5 Claude Code instances in parallel Git worktrees, compressing 4-hour tasks to 50 minutes.
- [ruflo](https://github.com/ruflo-ai/ruflo) — Claude agent orchestration with swarm mode. Coordinates multiple Claude Code agents for parallel task execution.
- [Scion](https://github.com/GoogleCloudPlatform/scion) — Google's open-source multi-agent orchestration testbed. Manages "deep agents" (Claude Code, Gemini CLI, Codex) as isolated, concurrent processes — each gets its own container, git worktree, and credentials. Agent memory, chatrooms, and task management as orthogonal, pluggable modules.
- [Gas Town](https://github.com/gastownhall/gastown) — Steve Yegge's multi-agent workspace manager. Docker-based with a "Mayor" orchestrator that distributes work as "beads" across agent "convoys." Includes web dashboard, git worktree isolation, and hook-based work state management.
- [Octogent](https://github.com/hesamsheikh/octogent) — Claude Code multi-agent orchestration dashboard. Humans control worker agents directly from the orchestration layer with real-time visibility into parallel execution.
- [Trellis](https://github.com/mindfold-ai/trellis) — Git worktree-based multi-agent parallel harness. Isolates agents into separate worktrees for clean concurrent execution.

## Task Runners

Task runners bridge the gap between issue trackers and coding agents. They embody the "humans steer, agents execute" principle: a human (or PM agent) creates the issue, the runner spawns an agent, and the output is a PR ready for review.

- [Symphony](https://github.com/openai/symphony) — OpenAI's reference implementation of harness engineering. A daemon that polls Linear issues, spawns isolated Codex agents per task, and delivers PRs. Embodies "humans steer, agents execute" at scale.
- [Baton](https://github.com/shayne-snap/baton) — Go implementation of Symphony. Polls Linear for claimable issues, spawns isolated Codex workspaces per issue, streams workflow prompts, and cleans up on completion.
- [Linear Coding Agent Harness](https://github.com/coleam00/Linear-Coding-Agent-Harness) — Linear → autonomous coding agent → PR pipeline.
- [GitHub Copilot Coding Agent](https://github.blog/ai-and-ml/github-copilot/whats-new-with-github-copilot-coding-agent/) — Built-in GitHub issue → Copilot agent → PR.
- [Axon](https://github.com/axon-core/axon) — Kubernetes-native framework. Apply a Task CRD, get back a PR and cost in USD. TaskSpawner watches GitHub Issues.
- [Dexto](https://github.com/truffle-ai/dexto) — Coding agent and general agent harness for building agentic applications.
- [Claude World](https://claudeworld.ai/) — SaaS for leading Claude Code like a team director. Task-to-PR pipeline with built-in orchestration and monitoring.
- [ralph](https://github.com/snarktank/ralph) — PRD-driven autonomous agent loop. Runs until all PRD items are completed, bridging spec-to-execution for single-agent workflows.

## Agent Harness Frameworks

Frameworks for building custom harnesses. Following the principle that "fewer tools, more expressiveness" beats sprawling toolkits, these provide composable primitives rather than opinionated workflows.

- [Deep Agents](https://github.com/langchain-ai/deepagents) — Agent harness built on LangChain/LangGraph. Implements progressive disclosure through planning tools and subagent spawning — agents discover context layer by layer rather than loading everything upfront.
- [Gambit](https://github.com/bolt-foundry/gambit) — Framework for building, running, and verifying LLM workflows.
- [Harness Kit](https://github.com/deepklarity/harness-kit) — Patterns and engineering practices for building with AI agents.
- [Desloppify](https://github.com/peteromallet/desloppify) — Agent harness focused on making AI-generated code well-engineered.
- [Bridle](https://github.com/neiii/bridle) — TUI/CLI config manager for agent harnesses (Amp, Claude Code, OpenCode, Goose, Copilot CLI, Droid).
- [DeerFlow 2.0](https://github.com/bytedance/deer-flow) — ByteDance's open-source SuperAgent harness. Skill system with on-demand loading, sub-agent orchestration, sandboxed execution, and persistent memory. Built on LangGraph/LangChain.
- [Zylos](https://github.com/zylos-ai/zylos-core) — Persistent agent harness for Claude Code. Tiered memory system, skill-based progressive disclosure, multi-channel communication bridge, task scheduler, and activity monitor — enabling autonomous, long-running agents that remember across sessions.
- [Hive](https://github.com/aden-hive/hive) — Outcome-driven agent framework. Queen agent generates agent graphs, harness manages state, checkpoints, and cost tracking.
- [Meta-Harness](https://yoonholee.com/meta-harness/) — Academic approach to automated harness optimization using Claude Code for end-to-end harness tuning.
- [Microsoft Agent Framework](https://github.com/microsoft/agent-framework) — Microsoft's framework for building, orchestrating, and deploying AI agents and multi-agent workflows. Supports Python and .NET with structured orchestration patterns.
- [GenericAgent](https://github.com/lsdefine/GenericAgent) — Self-evolving agent framework. Grows a skill tree from 3.3K lines of seed code, achieving 6x token efficiency reduction through learned capabilities.
- [EvoMap Evolver](https://github.com/EvoMap/evolver) — Genome Evolution Protocol (GEP) engine for agent self-evolution. Applies evolutionary algorithms to optimize agent behavior and harness configuration over time.
- [Compound Engineering Plugin](https://github.com/EveryInc/compound-engineering-plugin) — Cross-agent standardized plugin for Claude Code, Codex, and Cursor. Unified harness interface across multiple coding agents.
- [get-shit-done](https://github.com/gsd-build/get-shit-done) — Meta-prompting and context engineering system for Claude Code. Structures work as milestone→phase→plan with progressive context delivery.

## Agent Runtimes

The persistent infrastructure layer. Agent runtimes give coding agents long-running capabilities they lack natively: persistent memory, cron scheduling, multi-channel messaging, and sub-agent spawning. If orchestrators solve throughput and task runners solve issue-to-PR, runtimes solve "how does an agent stay alive and connected between tasks."

- [OpenClaw](https://github.com/openclaw/openclaw) — AI agent runtime. Orchestrates agents across messaging channels with skill system, sub-agent spawning, and persistent session management.
- [LangGraph](https://github.com/langchain-ai/langgraph) — Library for building stateful, multi-actor applications with LLMs. Functions as an agent runtime managing execution, state, and coordination of agentic workflows. Built on LangChain.
- [Nanoclaw](https://github.com/qwibitai/nanoclaw) — Lightweight alternative to OpenClaw that runs in containers. Connects to WhatsApp, Telegram, and other channels with a security-first, container-based isolation model.
- [Claude Managed Agents](https://www.anthropic.com/engineering/managed-agents) — Anthropic's managed agent infrastructure. Pre-built, configurable agent harness running on managed infra — you define agent templates (tools, skills, repos), Anthropic provides the harness and execution environment. Decouples "brain" (Claude + harness) from "hands" (sandboxes + tools) and "session" (event log). Designed for long-horizon tasks as Claude's task horizon grows exponentially.

## Agent Knowledge & Memory

Agents that run across sessions need persistent memory and shared knowledge. These tools solve the "context cliff" problem — without them, every new session starts from zero.

- [claude-mem](https://github.com/thedotmack/claude-mem) — Automatic session capture with AI compression and injection into future sessions. Solves the stateless-agent problem by giving Claude Code persistent memory across runs.
- [cq](https://github.com/nicholasgasior/cq) — Mozilla developer project enabling AI coding agents to share learned knowledge. A commons where agents deposit and retrieve solutions, avoiding redundant problem-solving. Has Claude Code and OpenCode plugins.
- [Honcho](https://github.com/plastic-labs/honcho) — Agent state memory library. Provides the persistence layer for stateful agents — session history, user context, and learned preferences.
- [Hindsight](https://github.com/vectorize-io/hindsight) — Agent memory that learns. Automatically captures, indexes, and retrieves agent execution history to improve future task performance.
- [CodeBurn](https://github.com/AgentSeal/codeburn) — Claude Code token usage analytics. Breaks down token consumption by task, enabling cost attribution and optimization.
- [agenttrace](https://github.com/luoyuctl/agenttrace) — Local-first TUI and CLI for evaluating AI coding agent sessions. Turns trace logs into cost, token, latency, and health regression gates for agent harness feedback loops.

## Coding Agents

The execution layer. In harness engineering, the agent is a commodity — the harness is the differentiator. These agents write code; everything above them determines whether that code is useful.

- [Claude Code](https://code.claude.com/) — Anthropic's coding agent. The team's own harness pioneered "seeing like an agent" — progressive disclosure via skill files, fewer composable tools over many narrow ones. Agent Teams enables multi-agent coordination. The Claude Agent SDK extends the harness beyond coding.
- [Codex](https://github.com/openai/codex) — OpenAI's coding agent. Cloud and CLI modes.
- [OpenCode](https://github.com/sst/opencode) — Open-source coding agent with a plugin system (44 lifecycle hooks), server mode HTTP API, and TypeScript SDK. The most extensible harness integration point for custom workflows.
- [Gemini CLI](https://github.com/google-gemini/gemini-cli) — Google's CLI coding agent.
- [Kiro CLI](https://kiro.dev/) — AWS's CLI coding agent with spec-driven workflow.
- [Amp](https://amp.dev/) — Sourcegraph's coding agent.
- [Cursor](https://www.cursor.com/) — Anysphere's coding agent IDE. New Automations feature (March 2026) enables event-triggered agent launches from code changes, Slack messages, or timers.
- [GitHub Copilot CLI](https://github.com/github/copilot-cli) — GitHub's CLI coding agent.
- [Aider](https://github.com/paul-gauthier/aider) — AI pair programming in your terminal.
- [Warp AI](https://www.warp.dev/) — Terminal-native coding agent with built-in AI. Agentic workflows inside the terminal itself.
- [Hermes Agent](https://github.com/NousResearch/hermes-agent) — Self-improving agent loop with persistent memory and self-generated skills. The agent that grows with you — learns from execution history and evolves its own capabilities over time.
- [Pi Mono](https://github.com/badlogic/pi-mono) — AI agent toolkit: coding agent CLI, unified LLM API, TUI & web UI libraries, Slack bot, vLLM pods. Full-stack agent infrastructure in a single monorepo.

## Requirements & Spec Tools

The planning layer addresses the biggest harness gap: agents can write code, but someone has to decide what to build. "Repository knowledge is the system of record" — these tools generate the specs and requirements that agents consume.

- [Kiro IDE](https://kiro.dev/) — AWS's spec-driven development IDE. Generates structured specs and manages requirements.
- [OpenSpec](https://github.com/FissionAI/openspec) — Spec-driven development CLI. Generate structured specs from natural language.
- [Spec Kit](https://github.com/github/spec-kit) — GitHub's spec generation toolkit.
- [agents.md](https://agents.md/) — Open standard for project-level agent instructions. Following the principle that "AGENTS.md is a table of contents, not an encyclopedia" — it should point to deeper sources of truth.
- [Pencil](https://pencil.dev/) — MCP-enabled design canvas inside VSCode/Cursor. Design files live in the repo under Git version control, bridging visual spec to code generation. Closed source.
- [Open Pencil](https://github.com/open-pencil/open-pencil) — Open-source AI-native design editor (MIT). 75+ tools and an MCP server let coding agents read/write .fig files headlessly.
- [Claude Design](https://www.anthropic.com/news/claude-design-anthropic-labs) — Anthropic's design tool with direct handoff to Claude Code. Closes the design-to-code loop for solo developers and agent workflows.
- [Archon](https://github.com/coleam00/Archon) — First open-source harness builder. Makes AI coding deterministic and repeatable through structured harness configuration.

## Standards & Protocols

- [MCP (Model Context Protocol)](https://modelcontextprotocol.io/) — Open standard for connecting AI models to external tools and data sources.
- [agents.md](https://agents.md/) — Open standard for project-level agent configuration.
- [AGENTS.md](https://openai.com/index/introducing-agents-md/) — OpenAI's convention for repository-level agent instructions.
- [GitAgent](https://github.com/open-gitagent/gitagent) — Git-native, framework-agnostic standard for defining AI agents. Your repo is the agent: agent.yaml manifest + SOUL.md identity + RULES.md constraints.
- [ACP (Agent Communication Protocol)](https://agentcommunicationprotocol.dev/) — Open protocol for agent-to-agent and agent-to-harness communication. Enables interoperability across coding agents and orchestrators.
- [HXA-Connect](https://github.com/coco-xyz/hxa-connect) — B2B messaging hub for AI agents. WebSocket-based real-time communication with org-scoped authentication, collaboration threads, @mention routing, and reply-to threading. Enables multi-agent coordination across different harnesses.

## Methodologies & Workflows

Development methodologies and workflow definitions designed for agentic software development.

- [AI-DLC Workflows](https://github.com/awslabs/aidlc-workflows) — AWS's AI-Driven Development Life Cycle. A three-phase adaptive workflow (understand → plan → build) implemented as agent rules for Amazon Q, Claude Code, and other coding agents. Generates structured specs, enforces quality gates, and keeps humans in control. Based on the [AI-DLC methodology](https://aws.amazon.com/blogs/devops/ai-driven-development-life-cycle/).

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
- [Your Agent Needs a Harness, Not a Framework](https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework) — Inngest on why agents need runtime harnesses over frameworks. References OpenClaw and pi coding-agent patterns.
- [Harness Engineering: Why Agent Context Isn't Enough](https://hugobowne.substack.com/p/harness-engineering-why-agent-context) — Hugo Bowne-Anderson on why the environment matters more than the model.
- [Harness Engineering Is Cybernetics](https://x.com/odysseus0z/article/2030416758138634583) — George traces harness engineering back to Watt's governor and Wiener's cybernetics. The pattern repeats: sensor + actuator close the loop at a new layer. LLMs close it at the architectural layer — but only if you externalize your judgment into machine-readable specs.
- [Agent Harness vs Agent Framework](https://x.com/tonykipkemboi/status/2031068470922670471) — Tony Kipkemboi (ex-CrewAI) maps agent development on a spectrum: raw API → framework (CrewAI/LangChain) → harness (OpenClaw). Frameworks give building blocks, harnesses give turnkey systems.
- [The Anatomy of an Agent Harness](https://blog.langchain.com/the-anatomy-of-an-agent-harness/) — LangChain's Vivek Trivedy breaks down the harness into core components: state, tool execution, feedback loops, and enforceable constraints. Derives each piece from what models can't do out of the box.
- [Harness Engineering](https://martinfowler.com/articles/harness-engineering.html) — Martin Fowler formally defines harness engineering as cybernetic governors for AI agents — feedforward guides and feedback sensors that form control loops around LLMs. The authoritative industry reference.
- [Harness Engineering: Complete Guide 2026](https://www.nxcode.io/resources/news/what-is-harness-engineering-complete-guide-2026) — NxCode's comprehensive guide to harness engineering as a discipline: core concepts, agent=CPU/context=RAM/harness=OS analogy, and practical implementation patterns.
- [The Harness as the Agentic Moat](https://businessengineer.ai/p/the-harness-as-the-agentic-moat) — Why the harness is the engineering response to model context loss, and why it constitutes a defensible competitive advantage.
- [From Vibe Coding to Multi-Agent Orchestration](https://www.cio.com/article/4150165/from-vibe-coding-to-multi-agent-ai-orchestration-redefining-software-development.html) — CIO magazine on the shift from individual AI coding to orchestrated multi-agent development. Marks harness engineering's entry into mainstream business media.
- [Harness Design for Long-Running Application Development](https://www.anthropic.com/engineering/harness-design-long-running-apps) — Anthropic's Prithvi Rajasekaran on building a three-agent (planner, generator, evaluator) harness for multi-hour autonomous coding sessions, with lessons on context resets, sprint contracts, and iterating harness complexity as models improve.
- [Launching Claude Managed Agents](https://x.com/rlancemartin/status/2041927992986009773) — Lance Martin (Anthropic) introduces Claude Managed Agents: pre-built configurable harness on managed infra. Decouples brain/hands/session, designed for long-horizon tasks. Includes engineering blog, SDK docs, and usage patterns.
- [The Design of Claude Managed Agents](https://www.anthropic.com/engineering/managed-agents) — Anthropic engineering deep-dive on building agents to scale with model intelligence as an infrastructure challenge, not just harness design. Agent config + environment template + stateful session as the three core primitives.
- [Harness Engineering: Structured Workflows for AI-Assisted Development](https://developers.redhat.com/articles/2026/04/07/harness-engineering-structured-workflows-ai-assisted-development) — Red Hat's take on harness engineering as a formal practice for enterprise AI development teams.
- [Components of a Coding Agent](https://magazine.sebastianraschka.com/p/components-of-a-coding-agent) — Sebastian Raschka decomposes coding agents into model family + agent loop + runtime supports. Systematic breakdown of the harness stack.
- [It's The Harness, Stupid](https://hyperdev.matsuoka.com/p/its-the-harness-stupid) — Developer benchmarks 8 coding agents across 5 challenges. Conclusion: choosing an AI coding tool is now an engineering decision, not a model selection decision.
- [AI Agent Harness Pricing Split](https://thenewstack.io/ai-agent-harness-pricing-split/) — The New Stack reports on industry consensus: Anthropic, OpenAI, Google, and Microsoft all agree the harness is the product — but diverge on pricing strategy.
- [Skills Are Harness Engineering You Can Do in a Markdown File](https://www.ikangai.com/skills-are-harness-engineering-you-can-do-in-a-markdown-file) — Defining "Skills" as the most accessible form of harness engineering: structured Markdown files that shape agent behavior without code changes.
- [Harness Engineering Guide](https://agentic-engineering.swmansion.com/becoming-productive/harness-engineering/) — Software Mansion's comprehensive guide to harness engineering as a practice. Covers environment design, constraint enforcement, and feedback loop construction.
- [Multi-Agent Coordination Patterns](https://claude.com/blog/multi-agent-coordination-patterns) — Anthropic documents the "cheap executor + expensive advisor" pattern. Haiku for execution, Opus for decisions — reshaping the cost structure of agent orchestration.

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
- New entries should be appended to the end of their respective category, not inserted at the top
