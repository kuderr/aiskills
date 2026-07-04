# aiskills

A collection of skills for Claude and other agents that support the [Agent Skills](https://agentskills.io) format. A skill is a folder with a `SKILL.md` file: instructions the agent loads when the task matches, plus optional reference files it reads on demand.

## Skills

### yasno

Writes and edits human-sounding prose — documentation first, but also articles, emails, and posts. Works for English and Russian.

What it does in practice: leads with what the reader needs, kills bureaucratese and filler words ("utilize" → "use", «осуществляет проверку» → «проверяет»), keeps formatting minimal (no bold spam, no bullet mush, no "Conclusion" sections), and strips AI patterns like the rule of three, negative parallelism, and "It's important to note". It also guards against overcorrection: technical details, versions, flags, and warnings stay; the text doesn't turn telegraphic.

Reference files load on demand: stop-word lists for English and Russian, an extended catalog of AI tells, a tone cheat sheet for nine document types (README, runbook, design doc, release notes, and so on), and a guide to multi-file documentation sets — hub pages, one source of truth, page budget, diagram and terminology discipline, RFC anatomy.

### yasno-review

Reviews existing docs against the yasno rules and fixes them on request. Point it at a file or folder, or let it pick up the docs changed on the current branch. Findings come one line each — location, rule, concrete fix: bullet mush, backtick noise, bold spam, pages over the ~200-line budget, prose that should be a diagram, stale open questions in RFCs. With `--fix` it applies the edits. Install it next to yasno — it reads the rules from there.

### yasno-factcheck

Checks whether a document tells the truth, where yasno-review checks how it reads. Extracts every checkable claim — numbers, defaults, field names, described behavior — and verifies each against the code or spec, factored: the claim becomes a question that doesn't contain the doc's answer, the question is answered from the source alone, the answers are compared. Verdicts come as one line per problem: confirmed, contradicted (with the source's file:line), stale, or unsupported. On fix, contradicted facts get corrected to the source's value; unsupported ones become questions to the author, not guesses.

## Installation

Claude Code — copy the skill folder into your skills directory:

```bash
git clone https://github.com/kuderr/aiskills
cp -r aiskills/yasno ~/.claude/skills/
```

Claude.ai — pack the folder into a zip, rename the extension to `.skill`, and upload it in Settings → Capabilities.

Other agents (Cursor, Codex, and the rest) — point your agent at the skill folder or install it with the [skills CLI](https://skills.sh):

```bash
npx skills add kuderr/aiskills/yasno
```
