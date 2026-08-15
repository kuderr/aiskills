---
name: yasno-review
description: Review existing documentation against the yasno and naglyadno rules and fix it. Use when the user asks to review or clean up a doc, README, RFC, ADR for style, length, or structure — "отревьюй доку", "проверь по yasno", "поправь доку", "слишком длинно", "review this doc", "this doc is too long", or invokes /yasno-review. Reviews prose quality only; checking facts against sources is yasno-factcheck's job. For writing new docs from scratch, use the yasno skill directly.
---

# Yasno review: find style problems in docs, then fix them

Review documentation against the yasno rulebook, report findings as a list, apply fixes when asked.

## Scope

What to review, in order:

1. Paths the user gave (file or directory).
2. Otherwise docs changed on the current branch: `git diff $(git merge-base master HEAD) --name-only` plus working-tree changes, filtered to markdown.
3. Otherwise ask.

Review prose only. Never change content inside code blocks, commands, API routes, config samples, or quotes — formatting around them is fair game, their content is not. Whether the doc's facts are true is out of scope — when a doc is dense with numbers, defaults, and described behavior, suggest running yasno-factcheck after the style pass.

## Rulebook

The rules live in the yasno skill, installed next to this one — read `../yasno/SKILL.md` relative to this file. For a docs set or an RFC/ADR also read `../yasno/references/project-docs.md`; for text that smells machine-generated, `../yasno/references/ai-patterns.md`; when unsure about a specific word, the stop-word list for the text's language. If the sibling path doesn't resolve, invoke the yasno skill instead.

Length and structure rules come from naglyadno — read `../naglyadno/SKILL.md` if it's installed. Its hard 100-line prose cap supersedes yasno's soft ~200-line budget; when naglyadno is absent, review against ~200 and say which budget you used.

## What to check

Work file by file. Cheap signals first — count before judging:

- **Length**: count prose lines per page — fenced blocks, tables, and images don't count:

  ```bash
  awk '/^```/{f=!f; next} !f && !/^\|/ && !/^!\[/ && NF' doc.md | wc -l
  ```

  Over 100 → say by how much, then propose the fix in naglyadno's order: convert prose to a visual, split by question, move reference bulk to an appendix. Never propose cutting facts to fit.
- **Bullet density**: lists whose items are full sentences with reasons and cross-references are prose in a costume — rejoin them. Lists of flags, prerequisites, numbered steps stay.
- **Backtick noise**: sentences with 3+ inline-code spans; terms used as ordinary words wrapped in backticks (verdicts, statuses, component names after first mention).
- **Bold spam**: bold for emphasis inside sentences; more than a handful of bolds per page.
- **Prose that should be a visual**: run the whole content-to-form table from naglyadno, not just diagrams. A flow with 3+ participants or a lifecycle past three states → mermaid sequence or state diagram; parameters, defaults, and limits narrated in sentences → table; a paragraph per alternative → one row per option; a field list describing a payload → a real example in a code block; a narrated procedure → numbered copyable commands. The reverse case too: a diagram followed by a re-telling of every arrow → keep the diagram, cut the re-telling, leave one pointing paragraph.
- **Splitting and appendices**: a file answering more than one question → propose the seams by naming each question and its filename. Flag splits done wrong — `part-1`/`part-2` cuts by size, or files repeating the same context instead of linking. Flag appendices holding a step of the argument rather than reference bulk, and bare "see appendix" links that don't name what's behind them.
- **Stop words, bureaucratese, AI tells**: per the yasno passes 1–2 and ai-patterns list.
- **Structure**: echo intros under headings, uninformative headings, "Conclusion" sections, main point buried below the fold.
- **Edit-history residue**: ghost contrasts ("uses X, not Y" where Y is just the previous draft), "now"/"new" without an anchor, UPD markers, sedimentary appends.
- **RFC/ADR extras**: missing status line, open questions that aren't open (no owner, no blocker, or already answered in the body), template residue — commented-out blocks, `<!-- ... -->` prompts, "(?)".
- **Docs set extras** (when reviewing more than one file): facts stated in two places, drifting term forms, mixed placeholder conventions, hub page that's an essay instead of a router.

## Output

One line per finding: `file:line — rule — fix`. Group by file, worst problems first. Concrete fixes, not advice: show the replacement phrase, not "consider rephrasing". A dense repeated pattern (say, backticks on every verdict) is one finding with a count, not forty lines.

If the user asked to fix (--fix, «поправь», "clean it up") — apply the fixes after reporting, then reread each touched section whole: the edit is done when a new reader can't tell where the seam is. Otherwise stop at the report and offer to apply.

Two fixes are structural, not editorial: splitting a file and moving bulk into an appendix both change what links to what. Report the plan — file names, the question each answers, what moves where — and apply it only on a yes. Converting prose to a diagram or a table is an ordinary fix, but the facts in it must survive the conversion: every number, name, and edge case from the paragraphs appears in the visual or in the paragraph that follows it.
