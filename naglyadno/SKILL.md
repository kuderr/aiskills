---
name: naglyadno
description: Keep technical documents short and visual — a hard 100-line cap on prose per document, with diagrams, tables, and code examples carrying what text would otherwise narrate, and big topics split across several linked documents instead of one long file. Use whenever writing or restructuring a doc, README, RFC, ADR, design doc, runbook, architecture section, документацию, дизайн-док — and whenever a document runs long, feels like a wall of text, or describes flows, states, topologies, or components in prose. Complements yasno (how the prose reads); this skill governs how much prose there is and what replaces it.
---

# Naglyadno: show it, don't narrate it

A reader scans a document before deciding to read it. What they can grab in that scan — a diagram, a table, a command they can copy — is what makes them stay and lets them act. Paragraphs are the slowest way to deliver structure, and structure is most of what a technical document contains.

Two rules do the work: **a hard cap of 100 prose lines per document**, and **anything expressible as a picture, a table, or an example is not written as prose**. The cap is what forces the second rule to actually happen.

This tightens yasno's soft ~200-line page budget to a hard 100 and supersedes it. Prose style stays yasno's job; diagram commentary, one-source-of-truth, hub pages, and RFC anatomy live in `yasno/references/project-docs.md` — read it for a docs set.

## The 100-line cap

Counted: prose, headings, list items — everything the reader parses as sentences.

Not counted: fenced blocks (code, `mermaid`, config, logs, terminal output), tables, images, frontmatter, link-only lines.

```bash
awk '/^```/{f=!f; next} !f && !/^\|/ && !/^!\[/ && NF' doc.md | wc -l
```

Run it before delivering. Over 100 means one of three things, in this order of preference: content that should be a visual is still prose → convert it; the document answers more than one question → split it; bulk reference material sits in the body → move it to an appendix. Cutting facts is never the answer — brevity is about words, not facts.

The cap is not a target to fill. A 30-line document that answers its question is finished, not thin.

## What replaces prose

| Content | Form | Prose smell that signals it |
|---|---|---|
| Who calls whom, in what order | sequence diagram | three or more participants narrated in order |
| Components, topology, data paths | flowchart / block diagram | "X talks to Y, which forwards to Z through W" |
| Statuses, verdicts, lifecycles | state diagram | more than three states described in sentences |
| Parameters, defaults, limits, fields | table | "the default is X; for Y it's Z; the maximum is..." |
| Options and their trade-offs | table, one row per option | a paragraph per alternative |
| A new model against a known one | bridge table ("analog in BGP") | "this is similar to, except that..." |
| Request / response / config shape | code block with a real example | fields described in a list |
| A procedure | numbered copyable commands | narrated steps |
| Quantities, durations, sizes | a number in the sentence | "fast", "large", "may take some time" |

Default diagram format is `mermaid` — it renders in GitHub, GitLab, and most doc sites, and it diffs as text. ASCII art only where mermaid can't render.

What stays prose, and belongs to nobody else: why the design is this way, what it costs, what breaks if you get it wrong, what the system deliberately does **not** do, and the one paragraph after each visual pointing at what to notice in it. That paragraph points — it does not re-tell the diagram. If the text after a state machine walks every state again, the same content lives twice and one copy goes stale.

## Split by question, not by size

One document answers one question. When the topic has several, each gets its own file — every file under its own 100-line cap, not one 400-line file wearing a table of contents.

Find the seams by listing the questions the material answers ("what is this and why", "how a request flows through it", "how we deploy it", "what we rejected and why"). Each question that a different reader arrives with, at a different moment, is a document. A hub page routes between them: two or three sentences plus a table mapping file → question it answers. Order with numbered filenames (`01-`, `02-`).

Splitting is not a loophole. Two smells that the split went wrong: each file repeats the same context to stand alone (one source of truth is broken — link instead), or the files are `part-1` / `part-2` cut at a line count (nobody knows which one holds their answer).

## Appendices

Bulk that a reader needs *sometimes* and never reads top to bottom — a full config, an API dump, a long migration table, benchmark output, raw logs — goes into an appendix file next to the document: `appendix-a-full-config.md`. Appendices are exempt from the cap; they are reference material, not narrative.

Two conditions. The main document must be complete without them — an appendix holds detail, never a step in the argument. And the link lives in the exact sentence that needs it, naming what's behind it: "Full policy set — appendix A", not a bare "see appendix".

An appendix that turns out to have its own argument and its own reader isn't an appendix — it's a document. Give it a number and put it in the hub.

## Working order

1. List the questions the material answers. More than one → more than one file.
2. Per file: pick the form for each piece of content from the table above, before writing prose.
3. Draw the visuals first. What's left to write is the connective tissue and the "what to notice" paragraphs.
4. Run the counter. Over 100 → convert, split, or move to an appendix.
5. Check the hub page and every cross-link resolves to the right file and section.

## Checklist

1. Prose lines ≤ 100 by the counter?
2. Any flow, state machine, topology, or parameter set still living in paragraphs?
3. Does every diagram have one pointing paragraph — and only one, not a re-telling?
4. Does each file answer exactly one question, and does its name say which?
5. Do appendices hold only reference bulk, with the main doc readable without opening them?
6. Did anything get shorter by losing a fact, a flag, a version, or a warning? Put it back.
