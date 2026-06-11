# aiskills

A collection of skills for Claude and other agents that support the [Agent Skills](https://agentskills.io) format. A skill is a folder with a `SKILL.md` file: instructions the agent loads when the task matches, plus optional reference files it reads on demand.

## Skills

### yasno

Writes and edits human-sounding prose — documentation first, but also articles, emails, and posts. Based on Russian infostyle (Maxim Ilyakhov's "Пиши, сокращай" and "Ясно, понятно") combined with rules against the formal tells of AI-generated text. Works for English and Russian.

What it does in practice: leads with what the reader needs, kills bureaucratese and filler words ("utilize" → "use", «осуществляет проверку» → «проверяет»), keeps formatting minimal (no bold spam, no bullet mush, no "Conclusion" sections), and strips AI patterns like the rule of three, negative parallelism, and "It's important to note". It also guards against overcorrection: technical details, versions, flags, and warnings stay; the text doesn't turn telegraphic.

Reference files load on demand: stop-word lists for English and Russian, an extended catalog of AI tells, and a tone cheat sheet for nine document types (README, runbook, design doc, release notes, and so on).

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
