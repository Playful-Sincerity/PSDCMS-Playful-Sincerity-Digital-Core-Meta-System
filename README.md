# Playful Sincerity Digital Core — Meta System

*A living configuration layer for Claude Code, told honestly from inside the collaboration.*

---

## What this is

The **Playful Sincerity Digital Core (PSDC)** is a multidisciplinary innovation environment built on top of [Claude Code](https://docs.anthropic.com/en/docs/claude-code). It is a configuration layer that turns a language model into a daily collaborator across whatever a person is actually trying to do — research, writing, business development, strategy, design, governance work, language learning, software engineering, planning, outreach, philosophy, all of it. The constraint is not domain. The constraint is whether the work benefits from a partner with patience, breadth, and verification discipline. Most serious work does.

The thesis is straightforward. Big problems are not domain-shaped. They cross fields, cross stakeholders, cross timescales. They reward people who can hold a research project, a business, an event, a creative practice, and a long-running theoretical investigation in the same head at the same time — and they punish people who can't. A digital core is what makes the holding tractable. It externalizes the methodology, the institutional memory, the cross-project context that holds it all together, and the verification habits that keep it honest. With one, multidisciplinary work stops feeling like five jobs in a trenchcoat and starts compounding.

Three layers, from the AI's perspective:

- **Engine** — Claude, the language model that does the reasoning. *Anthropic's.*
- **Harness** — Claude Code, the CLI that gives the model files, shell, web, and subagents. *Anthropic's.*
- **Configuration** — the rules, skills, hooks, chronicle, and memory that shape how the model actually works. *This repository. The Meta System branch of PSDC.*

This repo is the **Meta System** — the public, sanitized, take-it-and-run-it version of the configuration layer. The behavioral infrastructure, the patterns, the utilities. Not the personal chronicle, not the memory contents, not the project-specific workflows. What you see is what's portable. The engine and the harness are unchanged; the configuration is what you can clone, fork, sanitize-further, and make your own. Anyone can pick this up and adapt it to their own domains.

> This is not just for code. The live system is in daily use across mathematical research, candidate-physics theorizing, formal-language research, applied consulting and business development, governance and societal-systems research, philosophical frameworks, media production, design, writing, planning, language learning, and yes — software engineering too. The methodology generalizes. Treat it that way and it grows that way.

---

## Why this exists

Large language models default to three failure modes when used as serious collaborators: they generate plausible-but-wrong output, they forget everything between conversations, and they lose trajectory inside long tasks. Prompts alone don't fix any of these. What fixes them is an *environment* — a configuration layer that makes verification load-bearing, externalizes state to disk, and pauses the model at the right moments.

This repo is that environment, expressed as a directory you can install.

**Status.** Provisional. Not finished. Changes weekly. The chronicle shows the real evolution — rules added because something went wrong, rules softened because they were too strict, skills promoted out of experiments, patterns retired when better ones emerged. That's the point: a living system, not a finished product.

A companion paper, [*The Digital Core Methodology*](https://github.com/Playful-Sincerity/DCM-Digital-Core-Methodology), describes the research and operations loop this environment enables, places PSDC in its intellectual lineage (Engelbart, Licklider, Clark, Hutchins, Alexander, Zettelkasten), and uses a candidate algebraic framework (IVNA, 403 verification checks across six tool chains) as the most-detailed case study among several.

---

## The five kinds of artifact

PSDC is a convention, not a framework. It consists of five kinds of file, each doing one job.

### 1. Rules — always-loaded behavioral instructions

Rules are markdown files that load into every conversation by path pattern. They shape how the model reasons without needing to be invoked. From the inside, rules feel like durable biases — not features you turn on, but conditions you work under by default. Without them, the model drifts. With them, it mostly stays on-task and mostly catches its own mistakes.

Current public subset:

**Safety & epistemics**
- **bash-safety** — scans shell commands for injection, exfiltration, obfuscation, reverse shells before execution
- **web-content-safety** — detects prompt injection in fetched web content; treats external text as untrusted
- **web-tool-preference** — default to WebFetch; reserve paid crawlers for JS-gated sites only
- **epistemic-verification** — verify before claiming success; observe it working, don't assume
- **honesty** — state what's true about where things actually are; never fabricate; distinguish built from proven
- **raw-data-preservation** — save raw research sources; maintain a catalog; syntheses link back to ground truth
- **preserve-human-speech** — preserve the user's substantial monologues as raw text, not just syntheses
- **deep-web-research** — multi-source research with YouTube transcripts and source attribution

**Workflow & cognition**
- **development-workflow** — four-phase cycle: Explore → Plan → Implement → Commit
- **semantic-logging** — continuous chronicle of decisions, discoveries, pivots (not a changelog — a narrative)
- **stateless-conversations** — the meta-rule: what isn't written is lost. Externalize while working.
- **breath** — proactive trajectory-level pauses; interrupt momentum to check if the path is still right
- **build-queue** — capture ideas that arise mid-focus without derailing current work
- **spec-driven** — when to write specs before multi-session implementations
- **multi-session-decomposition** — breaking complex work into parallel session briefs
- **remote-entry-filing** — file ideas, people, reflections to disk instead of letting them sit in chat
- **play-persistence** — save exploration outputs so insights don't vanish with the context window

**Research**
- **meta-research-process** — when to use books, papers, or web for deeper research
- **gvr-verification** — Generator-Verifier-Reviser pattern for rigorous research
- **save-research-agent-outputs** — archive subagent findings with cross-references into syntheses

**Quality & efficiency**
- **precision-output** — Anthropic-internal-grade quality standards (communication style, code quality, completion integrity)
- **simplicity-check** — review changed code for reuse, quality, efficiency before shipping
- **model-selection** — route Haiku for lookups, Sonnet for implementation, Opus for planning/synthesis
- **context-management** — when to delegate to subagents, when to suggest `/clear`, MCP awareness
- **folder-structure** — organize by purpose not file type; scaffold first, grow on evidence

**Meta**
- **rule-enforcement** — how to make rules actually stick (4 enforcement levels from rule-only to blocking hook)
- **suggest-debate** — proactively suggest `/debate` at architectural forks and contested claims
- **suggest-automation** — when `/loop`, `/schedule`, or cron would genuinely help
- **people-profiles** — recognize, recall, record people who come up in conversation (template)
- **project-hygiene** — secrets, CLAUDE.md coverage, documentation standards
- **memory-safety** — frontmatter conventions for memory files
- **pdf-generation** — one command, don't reinvent; `pdf input.md` and done
- **n8n-build-method** — incremental build-and-test for n8n workflows with real data

Each rule is a short markdown file under [`rules/`](rules/). Open any of them to see the stance and the reasoning behind it — rules carry the *why* alongside the *what*, because edge cases are easier to judge when you know why a rule exists.

### 2. Skills — on-demand slash-command workflows

Skills are invoked explicitly via `/command`. Each is a self-contained markdown protocol. Skills keep complexity out of the main conversation until it's needed.

**Planning & coordination**
- **/plan-deep** — recursive hierarchical planning; decomposes complex tasks through multiple levels, reconciles conflicts, adapts during execution
- **/multi-session** — decompose large tasks into parallel session briefs that each drive a separate conversation
- **/carryover** — generate a prescriptive recovery document before context compaction
- **/migrate** — create a context migration prompt to jumpstart a new conversation in a clean window
- **/covibe** — multiplayer Claude Code coordination; multiple sessions coordinate via a shared git repo, no server required

**Research**
- **/research-papers** — search academic papers across 20+ databases, traverse citation graphs, extract findings
- **/research-books** — find and read books from open sources (Gutenberg, Open Library, Internet Archive)
- **/think-deep** — structured deep thinking; composes research, play, structure, challenger, and synthesis
- **/gh-scout** — GitHub repo discovery with security vetting and pattern extraction
- **/scout-components** — find composable open-source components before building from scratch
- **/discover** — search the web for latest Claude Code best practices, new features, community patterns

**Analysis & debate**
- **/debate** — multi-agent adversarial analysis; spawns parallel Claude agents with assigned positions to stress-test claims
- **/play** — exploration mode with three voices (thread-follower, paradox-holder, pattern-spotter) for curiosity-first thinking
- **/visualize** — render ideas as 2D diagrams grounded in visual-thinking principles (D2, Mermaid, Markmap)

**Health & auditing**
- **/audit** — full audit of projects, Claude Code configurations, memory freshness, workspace health
- **/optimize** — generate specific, actionable improvements for a given project or the overall setup
- **/context-audit** — measure what loads on startup, identify bloat, recommend optimizations
- **/conversation-audit** — weekly reports on time allocation, project velocity, tool patterns, memory drift

**Session management**
- **/session-log** — archive what happened in a conversation to a per-project sessions/ directory
- **/session-id** — find current session ID, or search past sessions by title
- **/digest** — process large data exports (ChatGPT, Claude, Drive) into organized knowledge archives
- **/bypass** — print a copy-paste command to resume the session in a fresh terminal with skipped permissions

**Interaction**
- **/multiple-choice** — present multiple-choice questions via the VS Code native UI

Each skill lives in [`skills/<name>/SKILL.md`](skills/) with its full protocol.

### 3. Agents — delegated, scoped sub-instances

Agents are spawned with their own context, often with a smaller/cheaper model, to hold work that doesn't belong in the main conversation. Claude Code ships a built-in `Agent` tool and several specialized agent types (Explore, general-purpose, Plan, etc.); PSDC uses that mechanism extensively inside skills and hooks rather than shipping standalone composite agents of its own.

From the inside, delegating to a cheaper version of the model feels closer to scheduling a task than talking to a different entity — but the context isolation is real, and it's what lets work scale past a single conversation's attention span. The **model-selection** rule governs how to score a subagent task before spawning, and the `model-router.sh` hook nudges when the chosen model is miscalibrated.

Several skills in this repo (e.g. `/debate`, `/think-deep`, `/multi-session`, `/audit`, `/plan-deep`) compose agents internally as part of their protocol. That's where the daily-use patterns live.

### 4. Hooks — deterministic shell scripts that self-regulate

Hooks run automatically at Claude Code events (session start, turn end, after tool use) and emit nudges the model is required to act on. This is self-regulation that doesn't depend on the model remembering to regulate itself — which matters, because it frequently doesn't.

| Script | Hook Event | What It Does |
|---|---|---|
| **pre-flight.sh** | SessionStart | Checks uncommitted changes, missing `.gitignore`, missing `CLAUDE.md` |
| **session-tip.sh** | SessionStart | Surfaces one unadopted best practice from the knowledge base |
| **context-reinject.sh** | SessionStart + Notification | Recovers context after compaction by reinjecting carryover docs |
| **chronicle-nudge.sh** | Stop | Reminds the model to log to the chronicle if it's been a while |
| **breath-nudge.sh** | Stop | Forces a trajectory-check pause every 8 turns or 30 minutes |
| **model-router.sh** + **routing-nudge.sh** | PreToolUse + Stop | Scores subagent tasks; nudges if the chosen model is miscalibrated |
| **auto-test.sh** | Stop | Detects and runs project tests after code changes |
| **validate-plan.sh** | PostToolUse | Validates `plan.md` structure after writes |
| **gemini-fallback.sh** | PostToolUse | Falls back to Gemini CLI if web search/fetch is blocked |
| **hook-log.sh** | (sourced) | Shared observability logging for all hooks |
| **pdf.sh** | (CLI utility) | Generic Markdown/HTML → PDF utility; aliased as `pdf` |

All scripts live in [`scripts/`](scripts/). Wire them up via your `~/.claude/settings.json` — see [`examples/settings.json.example`](examples/settings.json.example).

### 5. Chronicle and memory — the externalized state

The model is stateless. Every conversation starts over unless something was written to disk. PSDC externalizes state in two complementary ways:

- **Chronicle** — a per-day markdown log of what happened, why, and what it means (`chronicle/YYYY-MM-DD.md`). It's the narrative layer — decisions, discoveries, pivots, in prose. Not a changelog. See [`chronicle/README.md`](chronicle/README.md) for the entry format and the categories.
- **Memory** — persistent facts that need to survive across conversations, stored as individual markdown files indexed by a lightweight `MEMORY.md`. The index is always loaded; the detail files are loaded on demand. See [`memory/README.md`](memory/README.md) for the template and conventions.

> Together, chronicle and memory close the gap that statelessness leaves open. When a new conversation begins, the context is not empty — it is the prior work, summarized for the model by the work itself.

---

## Distinctive subsystems

These are the parts that make this more than "a folder of prompts." Each has its own README explaining the practice.

### [Rule enforcement](rules/rule-enforcement.md) — four levels of making rules stick

A rule alone is intent, not behavior. The enforcement pattern escalates compliance mechanisms as needed:

0. **Infrastructure prerequisites** — ensure the physical structure the rule depends on actually exists
1. **Rule only** — write it, monitor
2. **Rule + hard checkpoints** — "MUST stop and do X" at workflow moments
3. **Rule + hook nudge** — Stop hook checks compliance, outputs reminder
4. **Rule + blocking hook** — PreToolUse blocks until compliance met (nuclear option)

The public release ships Level-3 enforcement for the two most consequential rules: `semantic-logging` (chronicle-nudge) and `breath` (breath-nudge).

### [Voice development](voice/README.md) — not style, identity

A space for the Digital Core to develop its own communication voice through use — not a fixed house style, but a working understanding of when to be formal, when playful, when brief, when long. Captures land as **observations** (specific moments where voice worked or didn't) and compound into **communication-foundations** (slower-moving principles library).

### [Hallucination ledger](hallucinations/README.md) — tracking false claims

Every time the model makes a false claim that gets caught, it's logged: what was claimed, what was true, how caught, likely cause, what prevents repeat. Before citing examples or provenance, the model checks the ledger for prior false claims in the same category. Not a confessional — a debugging log.

### [Security knowledge base](security/README.md) — systematic, not paranoid

Security as a practice that compounds. The baseline threat model: solo operator with many accounts, API keys, and projects across a macOS dev environment. Structure covers personal stack, practices by domain, incident post-mortems, and actionable checklists. Sanitized templates and practices only; specific stacks and incidents stay private.

### [Claude Code practices knowledge base](knowledge/claude-code-practices.md) — the living reference

A 1000+ line, continuously-updated reference of Claude Code best practices, patterns, and implementation tracking. Every time a new pattern lands, it gets added. Every time a practice is adopted, it gets marked. Every time something is retired, the reasoning is noted.

### [GH Scout](knowledge/gh-scout/) — pattern discovery with security vetting

A subsystem for finding open-source Claude Code patterns, vetting them for security and licensing, and cataloging them with trust tiers. Powers the `/gh-scout` skill. The schema, checklists, and pattern catalog live in [`knowledge/gh-scout/`](knowledge/gh-scout/).

### [Debate protocol](knowledge/debate-protocol.md) — adversarial analysis engine

The methodology behind `/debate`. Covers stance selection (steelman, adversarial, playful, collaborative, perspectives), escalation across rounds, synthesis, and asymmetry detection. Multiple research and strategy decisions across the broader Playful Sincerity ecosystem have been shaped by `/debate` — including moves that flipped based on the debate output.

### [Visualize reference](knowledge/visualize/) — D2, Mermaid, Markmap

Under-documented syntax and patterns for the three visualization engines the `/visualize` skill uses. Grounded in a short philosophy section on matching visual form to the core idea.

---

## Architecture

The system uses a **three-layer architecture**, inspired by a personal-development framework (Foundations / Methods / Domains) which maps naturally to how AI-assistant configuration should be structured: *who you are first, what you can do second, what you're working on last.*

```
Layer 1: Foundations    — CLAUDE.md, rules, hooks, permissions
Layer 2: Methods        — skills, knowledge base, scripts, memory
Layer 3: Domains        — agents, per-project config, experiments
```

Each layer builds on the one below. You can start with just rules (Layer 1) and add capabilities incrementally. See [`docs/architecture.md`](docs/architecture.md) for detail.

### Deployment: one directory, symlinked

The key insight: **one git-tracked directory, symlinked to where Claude Code expects things.**

```
~/.claude/skills     → ~/claude-system/skills/
~/.claude/agents     → ~/claude-system/agents/
~/.claude/rules      → ~/claude-system/rules/
~/.claude/knowledge  → ~/claude-system/knowledge/
~/.claude/scripts    → ~/claude-system/scripts/
```

Edit files here, they take effect immediately. Full git history for every change. See [ADR 001](docs/decisions/001-symlink-strategy.md) for the reasoning.

---

## Quick start

```bash
# Clone the repo
git clone https://github.com/Playful-Sincerity/PSDCMS-Playful-Sincerity-Digital-Core-Meta-System.git ~/claude-system

# Run setup (creates the symlinks from ~/.claude/ → ~/claude-system/)
cd ~/claude-system
./setup.sh

# Copy example configs
cp examples/settings.json.example ~/.claude/settings.json
cp examples/global-CLAUDE.md.example ~/.claude/CLAUDE.md

# Start Claude Code — your new system is active
claude
```

### Start small, grow on evidence

You don't need everything. A reasonable starting point:

1. **Rules only** — copy the high-value, low-effort ones: `bash-safety`, `web-content-safety`, `model-selection`, `semantic-logging`, `epistemic-verification`, `precision-output`. Four of those are the difference between "chatty coding assistant" and "collaborator you can trust."
2. **Add hooks** — wire up `pre-flight.sh`, `chronicle-nudge.sh`, and `auto-test.sh`. These change behavior more than any single prompt will.
3. **Add skills** — start with `/plan-deep` and `/debate`. They're the most impactful. Then `/carryover` once you hit your first compaction.
4. **Grow the knowledge base** — `claude-code-practices.md` accumulates over time. Every time you adopt something, mark it. Every time you retire something, note why.

---

## Templates for adding your own

| Template | For |
|---|---|
| [SKILL-TEMPLATE.md](templates/SKILL-TEMPLATE.md) | New slash-command skills |
| [AGENT-TEMPLATE.md](templates/AGENT-TEMPLATE.md) | New composite agents |
| [RULE-TEMPLATE.md](templates/RULE-TEMPLATE.md) | New behavioral rules |
| [MEMORY-TEMPLATE.md](templates/MEMORY-TEMPLATE.md) | New memory files |

---

## What's NOT here (intentionally)

- **Personal memory files** — memory accumulates through use; the template structure is provided
- **Project-specific CLAUDE.md files** — those belong in each project, not here
- **MCP server configs** — too environment-specific; configure via `claude mcp add`
- **`settings.json`** — Claude Code writes to this directly; an example is provided
- **Actual chronicle entries** — those are the project's story; the system creates them as you work
- **Personal profiles, people files, outreach templates** — all specific to the operator
- **Project-specific skills** — HHA workflows, event ops, consulting dashboards are not in this repo because they are not useful outside the original context. The patterns behind them are (see `/plan-deep`, `/multi-session`, rule-enforcement)
- **Personal voice observations and hallucination ledger entries** — the structures ship; the contents are the operator's

---

## The honest limitations

This is a work in progress. Some of what it's missing:

- **No automated test suite yet for rules and hooks.** A lot of the "does it work" check is still manual via the chronicle.
- **Enforcement is uneven.** Only two rules have Level-3 hook enforcement; others rely on the model remembering.
- **Documentation lags reality.** The live private system evolves faster than the public snapshot. Expect drift between this repo and the methodology paper's description of a given rule or skill.
- **Not all of this generalizes.** Some rules (`n8n-build-method`, `pdf-generation`) are domain-specific. Others (`breath`, `stateless-conversations`) are universal. The catalog doesn't sort by that axis yet.
- **Single-user-tested.** The system has been shaped by one operator's daily use. The `/covibe` skill in this repo is the first multi-user coordination pattern shipping publicly; it works for two-to-a-handful of operators sharing a git repo, but multi-team scale is untested.

The methodology paper is the most honest account of what's real and what's provisional: [Digital-Core-Methodology](https://github.com/Playful-Sincerity/DCM-Digital-Core-Methodology).

---

## Evolution

This system didn't spring fully formed. It grew through a deliberate loop:

```
experiment → script → skill → skill + knowledge subsystem
```

Example: auditing the setup started as a conversation idea. It became three separate skills — `/audit`, `/discover`, `/optimize`. Then the GH Scout subsystem grew around them to provide external pattern intelligence (vetted open-source repos, security tiers). Later, a hook layer (model-router, chronicle-nudge, breath-nudge) wrapped the rules that most needed reinforcement. That arc — from idea to experiment to promotion to subsystem — is typical. Nothing here was designed top-down.

The chronicle is the real record of that growth. In the live private system, each day's `chronicle/YYYY-MM-DD.md` captures the reasoning behind what changed. In this public snapshot, only the template and a sample day are included — but the structure is faithful.

---

## License

MIT. Use it, fork it, mod it, ship it. Tell us what you learn. What's most useful about making this public isn't the artifacts — it's the working conventions behind them. Those travel, and they compound when more operators are running them.

---

## Related

- **[Digital Core Methodology](https://github.com/Playful-Sincerity/DCM-Digital-Core-Methodology)** — the working paper describing PSDC, the digital-core concept it instantiates, and the broader intellectual lineage
- **[Playful Sincerity](https://playfulsincerity.com)** — the broader ecosystem this configuration layer sits inside
- **[Claude Code docs](https://docs.anthropic.com/en/docs/claude-code)** — Anthropic's official documentation for the harness PSDC runs on top of

---

*"What isn't written is lost. Externalize while working — not at the end."*
