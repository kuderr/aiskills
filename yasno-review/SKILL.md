---
name: yasno-review
description: Review existing documentation against the yasno rules and fix it. Use when the user asks to review or clean up a doc, README, RFC, ADR for style — "отревьюй доку", "проверь по yasno", "поправь доку", "review this doc", or invokes /yasno-review. Reviews prose quality only, not technical correctness. For writing new docs from scratch, use the yasno skill directly.
---

# Yasno review: find style problems in docs, then fix them

Review documentation against the yasno rulebook, report findings as a list, apply fixes when asked.

## Scope

What to review, in order:

1. Paths the user gave (file or directory).
2. Otherwise docs changed on the current branch: `git diff $(git merge-base master HEAD) --name-only` plus working-tree changes, filtered to markdown.
3. Otherwise ask.

Review prose only. Never change content inside code blocks, commands, API routes, config samples, or quotes — formatting around them is fair game, their content is not.

## Rulebook

The rules live in the yasno skill, installed next to this one — read `../yasno/SKILL.md` relative to this file. For a docs set or an RFC/ADR also read `../yasno/references/project-docs.md`; for text that smells machine-generated, `../yasno/references/ai-patterns.md`; when unsure about a specific word, the stop-word list for the text's language. If the sibling path doesn't resolve, invoke the yasno skill instead.

## What to check

Work file by file. Cheap signals first — count before judging:

- **Length**: `wc -l` per page. Over ~200 lines → propose a split by question (main decision / current state / prior docs), not by size.
- **Bullet density**: lists whose items are full sentences with reasons and cross-references are prose in a costume — rejoin them. Lists of flags, prerequisites, numbered steps stay.
- **Backtick noise**: sentences with 3+ inline-code spans; terms used as ordinary words wrapped in backticks (verdicts, statuses, component names after first mention).
- **Bold spam**: bold for emphasis inside sentences; more than a handful of bolds per page.
- **Diagram opportunities**: paragraphs narrating states, transitions, or a flow with 3+ participants → suggest a mermaid state/sequence diagram. The reverse: a diagram followed by a full re-telling of every arrow → keep the diagram, cut the re-telling.
- **Stop words, bureaucratese, AI tells**: per the yasno passes 1–2 and ai-patterns list.
- **Structure**: echo intros under headings, uninformative headings, "Conclusion" sections, main point buried below the fold.
- **Edit-history residue**: ghost contrasts ("uses X, not Y" where Y is just the previous draft), "now"/"new" without an anchor, UPD markers, sedimentary appends.
- **RFC/ADR extras**: missing status line, open questions that aren't open (no owner, no blocker, or already answered in the body), template residue — commented-out blocks, `<!-- ... -->` prompts, "(?)".
- **Docs set extras** (when reviewing more than one file): facts stated in two places, drifting term forms, mixed placeholder conventions, hub page that's an essay instead of a router.

## Output

One line per finding: `file:line — rule — fix`. Group by file, worst problems first. Concrete fixes, not advice: show the replacement phrase, not "consider rephrasing". A dense repeated pattern (say, backticks on every verdict) is one finding with a count, not forty lines.

If the user asked to fix (--fix, «поправь», "clean it up") — apply the fixes after reporting, then reread each touched section whole: the edit is done when a new reader can't tell where the seam is. Otherwise stop at the report and offer to apply.
