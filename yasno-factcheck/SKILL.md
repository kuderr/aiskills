---
name: yasno-factcheck
description: Verify the factual claims of a document against their sources — code, configs, API specs, tickets. Use when the user asks to fact-check a doc, check a doc against the code, "проверь факты", "сверь доку с кодом", "фактчек", "fact-check this", or invokes /yasno-factcheck; also before an important doc ships. Complements yasno-review — review checks how the doc reads, factcheck checks whether it's true.
---

# Yasno factcheck: every claim against its source

A reviewer catches awkward prose in seconds and a wrong default never — the sentence reads fine. Wrong facts are the expensive kind of wrong: a number or a field name gets copied from the doc into configs and decisions long after anyone could tell where it came from. This skill checks a document's claims against the ground truth they describe.

## Scope

Same resolution as yasno-review: paths the user gave, otherwise docs changed on the current branch, otherwise ask. Then identify the ground truth — the repos, configs, and specs the document describes. If part of it is unreachable (another team's repo, a closed wiki), say so up front: claims grounded there get a question with an owner, not a guess.

## Step 1: extract claims

Read the document and pull out every atomic, checkable claim:

- numbers: ports, timeouts, TTLs, limits, versions, sizes
- names: fields, flags, API routes, components, CRDs, config keys
- defaults and behaviors: "by default X", "when Y happens, the system does Z"
- states and transitions: verdicts, statuses, what moves between them
- environment: "runs in namespace X", "deployed through Y", "owned by team Z"

Claims live in the visuals as much as in the prose, and in a doc written under naglyadno most of them do. Extract from every form: arrows and participants in a sequence diagram (who actually calls whom, in what order), states and transitions in a state diagram (including the ones the code has and the picture doesn't), every cell of a parameter or defaults table, field names and values in an example payload or config, flags in a copyable command. A diagram is the easiest place for a stale fact to hide — nobody rereads a picture the way they reread a sentence.

Opinions and decisions are the author's — not checkable. But a decision often carries a checkable half: "we chose X because Y is slower" contains "Y is slower", and that one gets checked.

## Step 2: verify factored

The trap in checking a finished text is anchoring: reread the sentence, nod, move on — it's fluent, so it feels true. Fluency isn't evidence. Verify factored: turn the claim into a question that doesn't contain the doc's answer ("what is the default TTL of the access cache?", not "is the TTL 24h like the doc says?"), answer it from the source alone, then compare the two answers.

When subagents are available, this is exactly what they're for: give the verifier the question and the source paths — not the document. An answer produced blind to the draft can't inherit its mistake.

Source hierarchy as in yasno: code beats config, config beats the wiki, everything beats memory. And a citation is not a verification — a doc that links to the spec can still misquote it. Open the link and read what it actually says.

## Step 3: verdicts

- **confirmed** — the source agrees; keep its file:line for the report
- **contradicted** — the doc says X, the source says Y; the worst kind, report first
- **stale** — was true once, the source has changed since; git log tells
- **unsupported** — no source found: invented, or grounded somewhere unreachable — a question for the user, never a silent pass

A contradiction is not automatically the doc's fault: sometimes the code is the bug. When the doc looks intentional and the code looks accidental, show both and ask — don't "fix" the doc to match a bug.

## Output

One line per problem claim: `file:line — claim — verdict — source`. Contradicted first, then stale, then unsupported. Confirmed claims are one summary line with a count, not a list.

A claim found in a visual is reported at the visual's line with what it is: `arch.md:41 — sequence diagram, agent → apiserver — contradicted — the agent writes to the queue, agent/sync.go:120`. Fixes go into the diagram, table, or example itself; a corrected sentence next to a wrong picture leaves the contradiction in place.

If the user asked to fix: contradicted and stale facts get corrected to the source's value; unsupported facts become batched questions with your best guess attached — never silently deleted, never silently kept.

The author pushing back — "it's right, I remember" — is a data point, not a source. Recheck against the code and show what you found. If the author owns the fact (a deadline, a decision, a name they're choosing), their word is the source: record it and move on.
