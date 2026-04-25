# Playful Sincerity Digital Core — Meta System (Public Edition)

Project instructions for working on **this repository** — the sanitized public subset of the Digital Core. If you are inside a Claude Code session editing the Meta System itself, this is the file that tells you how.

This is a git-tracked configuration system. `~/.claude/` directories (skills, agents, rules, knowledge, scripts) are symlinks pointing here after you run `./setup.sh`.

## What this repo contains

- **`rules/`** — ~32 behavioral rules (safety, workflow, methodology, research, voice, quality). Each is a short markdown file with a path-scoped YAML frontmatter.
- **`skills/`** — ~23 slash-command skills. Each lives in `skills/<name>/SKILL.md`.
- **`knowledge/`** — Best-practices KB, GH Scout subsystem, debate protocol, visualization references, research-domain profiles, testing practices, research-paper writing guide.
- **`scripts/`** — Hook scripts (pre-flight, session-tip, context-reinject, auto-test, chronicle-nudge, breath-nudge, model-router, routing-nudge, hook-log, validate-plan, gemini-fallback, pdf).
- **`security/`** — Security knowledge base (README + practices templates).
- **`voice/`** — Voice development practice (README + communication-foundations + empty observations template).
- **`hallucinations/`** — Hallucination-tracking ledger (README + empty ledger template).
- **`chronicle/`** — Chronicle pattern documentation (README + one sanitized sample day).
- **`memory/`** — Memory system template and conventions.
- **`docs/`** — Architecture docs (three-layer model, ADRs).
- **`templates/`** — Starter templates for creating new skills, agents, rules, memory files.
- **`examples/`** — Example `settings.json` and global `CLAUDE.md`.

## What this repo does NOT contain

The Meta System is a subset of the live Digital Core. Not included here:

- Personal chronicle entries, memory content, voice observations, hallucination-ledger entries
- Project-specific skills (HHA workflows, event ops, consulting dashboards, calendar ops)
- Operator-specific rules (personal-voice rules, language-learning rules, specific-tool-integration rules)
- MCP server configurations (environment-specific)
- Actual `~/.claude/settings.json` (Claude Code writes to it directly; an example is provided)
- Personal people profiles, outreach templates, project maps

If a file references `~/Playful Sincerity/...` or uses personal context, it was removed or sanitized before public release.

## Working on this repo

### Adding a new skill

1. Create `skills/<name>/SKILL.md`
2. Follow patterns in existing skills (`plan-deep` for planning-style skills, `gh-scout` for multi-phase skills with knowledge-base interaction)
3. Add a one-line descriptor to the README's skills catalog
4. If the skill composes subagents or other skills, note that dependency in the SKILL.md header

### Adding a new rule

1. Create `rules/<name>.md`
2. Add YAML frontmatter with `paths:` if the rule should only load for specific file patterns (most global rules have no path constraint)
3. Lead the rule with *the stance*, not the mechanism — rules carry the *why* alongside the *what* so edge cases are easier to judge
4. Add a one-line descriptor to the README's rules catalog
5. If the rule is hard to comply with (proactive action, invisible non-compliance), add a hook script — see `rules/rule-enforcement.md` for the four-level escalation pattern

### Adding a new script

1. Create `scripts/<name>.sh`
2. Make it executable (`chmod +x`)
3. Source `scripts/hook-log.sh` for observability; call `hook_log` at key points
4. Wire it up in the example `settings.json` under the appropriate hook event
5. Document it in README's hooks table

### Modifying existing files

- Edit before creating. Look for the hook before adding another file.
- Rules and skills reference `~/.claude/` paths in their instructions — this is correct, it resolves through symlinks after setup
- If a rule's stance changes, update the `Why this matters` / `How to apply` sections to match
- Keep the README synchronized — if you add/remove/rename, the catalog must reflect it

## Relationship to the live private system

This repo is the public face of a live private system that evolves faster than this snapshot. The live system lives at `~/claude-system/` on the operator's machine; this public repo pulls from it via a sanitization pass that:

1. Strips personal memory references, project names, and people names
2. Replaces chronicle/voice/hallucination contents with structure-only templates
3. Removes project-specific skills and rules
4. Replaces concrete paths (`~/Playful Sincerity/...`) with generic examples

When the live system evolves, this repo gets updated as part of larger releases — not every change. Expect the methodology paper's description of a given rule to be slightly ahead of this repo's version. The stance is the same; specific language may drift.

## Key constraints

- **NEVER commit secrets, API keys, credentials, personal data.**
- **NEVER port operator-specific skills or chronicle entries.** Sanitize or skip.
- Skills and agents reference `~/.claude/` paths in their instructions — this is correct (resolves through symlinks after setup)
- The global `~/.claude/CLAUDE.md` is a SEPARATE file from this one (see `examples/global-CLAUDE.md.example` for the starter template)
- `~/.claude/settings.json` is NOT symlinked — Claude Code writes to it directly

## Related

- **Live ecosystem:** [Playful Sincerity](https://playfulsincerity.com)
- **Methodology paper:** [Digital Core Methodology](https://github.com/Playful-Sincerity/DCM-Digital-Core-Methodology)
- **Claude Code docs:** https://docs.anthropic.com/en/docs/claude-code
