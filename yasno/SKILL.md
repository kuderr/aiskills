---
name: yasno
description: Write and edit human-sounding documentation and prose in English or Russian following plain-language / infostyle principles (Ilyakhov's "Пиши, сокращай" / "Ясно, понятно"). Use this skill EVERY time the user asks to write or rewrite a README, documentation, guide, instruction, article, post, email, design doc, runbook, release notes, документацию, инструкцию, статью — or asks for text "без воды", "по-человечески", "not like AI", "make it human", "remove the slop", "clean this text up". Also use it when producing any prose deliverable longer than a couple of paragraphs, even if the user didn't mention style — clean writing should be the default.
---

# Yasno: human writing without fluff or slop

A skill for writing and editing prose — documentation first, but also guides, articles, and emails. The goal: text that reads easily, gets to the point, and doesn't look like an AI wall of text. The foundation is Russian infostyle ("Пиши, сокращай" / "Ясно, понятно" by Maxim Ilyakhov) plus rules against the formal tells of machine-generated text. Works for English and Russian.

The core principle: text is written in the reader's world. Not "what I want to say" but "what the reader needs to understand or do."

## How to work

1. **Identify the reader, the useful action, and the register.** One sentence: who reads this and what they can do after reading. Example: "A DevOps engineer installing the operator for the first time — after the README they deploy it in their cluster and create the first policy." The document type sets the register: a README is not written like a runbook, and a runbook is not written like a blog post. A cheat sheet covering nine document types lives in `references/registers.md`; read it when the document type is unusual or the tone is in doubt. If the reader isn't clear from the task — ask the user, or make an explicit assumption and state it.
2. **Build the skeleton.** The main thing goes first. Then in descending order of importance to the reader: what they can't act without, then details, then reference material at the end.
3. **Write the draft.** Don't think about beauty, think about meaning.
4. **Run four editing passes**: stop words → syntax → paragraphs → formatting. Each pass is described below.
5. **Check against the final checklist** at the end of this file.

If the user gives you an existing text and asks to clean it up — skip steps 1–3 and work through the editing passes. Preserve meaning and facts: invent nothing, lose nothing important.

## Pass 1: stop words and bureaucratese

Remove words that carry no meaning. If a word can be deleted and the sentence doesn't change — delete it.

- **Filler and judgments**: "it should be noted", "as we all know", "needless to say", "great", "high-quality", "convenient" (without saying what makes it convenient).
- **Intensifiers**: "very", "extremely", "significantly", "highly". Replace the intensifier with a fact or a number.
- **Bureaucratese**: "utilize" → "use", "in order to" → "to", "prior to" → "before", "performs validation" → "validates", "at this point in time" → "now".
- **Nominalizations** → verbs: "perform an installation of dependencies" → "install dependencies".
- **Passive** → active: "the policy is programmed by the operator" → "the operator programs the policy".
- **Marketing clichés**: "unique", "innovative", "powerful", "flexible solution". Instead of praise — what it concretely does.

Full replacement lists: `references/stop-words-en.md` for English, `references/stop-words-ru.md` for Russian (канцелярит, вводные-паразиты, отглагольные существительные). Open the relevant file when cleaning someone else's text or when unsure about a specific word.

Important: removing junk doesn't mean removing meaning. "Very fast" is bad not because shorter is the goal, but because it's empty. "Responds in 5 ms at p99" is longer — and is the correct replacement.

## Pass 2: syntax

- One sentence — one thought. A three-line sentence almost always splits into two.
- Vary sentence length. Three same-length sentences in a row is a machine-text tell. But don't turn the text into a telegram: choppy three-word sentences back to back read as badly as mile-long ones.
- Concrete over abstract. "Supports various formats" → "Supports JSON and YAML". "May take some time" → "Takes 2–3 minutes".
- A new concept gets an example immediately. A term without an example gets skimmed past, not understood.
- Explain through what the reader already knows. A DevOps engineer doesn't need EndpointSlice explained; a junior gets one sentence on what it is.
- Don't hedge with "usually", "in most cases", "typically" when you can say it precisely. If you can't — say honestly in which cases it differs.

## Pass 3: paragraphs and structure

- A paragraph is a mini-text: the first sentence is the main point, the rest unpacks it. A reader skimming only the first sentence of each paragraph should understand the whole text.
- The main thing goes at the top of the document. The first paragraph answers "what is this and why should I care" — it doesn't warm up with "in today's world...".
- Headings are informative: not "Introduction", "Features", "Conclusion" — but "Installation", "How SIDs are allocated", "What to do when policies conflict".
- No "Conclusion" / "Summary" / "Wrapping up" sections. The text ends on the last useful thought.
- Exactly as much detail as the reader's action requires. Versions, flags, limitations, footgun warnings are necessary detail — don't touch them. Musings about "why this matters in general" are fluff — cut them.

## Pass 4: formatting

The default is plain paragraphs of prose. Formatting is added only when its absence makes things worse.

- **Lists** — only for genuinely enumerable things: installation steps, a set of flags, requirements. Don't shred a connected argument into bullets. If list items look like "**Word:** explanation", it should probably be a prose paragraph.
- **Bold** — almost never. Acceptable: a term at first definition, a UI element ("click **Apply**"). Bold for "emphasis" sprinkled inside sentences is slop.
- **Headings** — no more than one per 3–5 paragraphs. A heading above every paragraph is slop.
- **Tables** — only for genuinely tabular data (parameter: name / type / default). Not for a two-row "comparison of approaches".
- No emoji in headings or documentation body. Never touch or "decorate" anything inside code blocks.
- Nested lists — one level of nesting maximum.

## AI tells: always remove

These constructions instantly mark a text as machine-generated. In English:

- "It's important to note", "It's worth mentioning", "Let's dive into", "Let's explore"
- "plays a crucial role", "a wide range of", "an essential tool", "in today's fast-paced world"
- The rule of three: "fast, simple, and secure" — three parallel adjectives/nouns as a rhythmic tic.
- Negative parallelism: "It's not just an operator — it's a whole platform."
- Question-as-opener: "So what exactly is SRv6? Let's find out."
- Every paragraph exactly three sentences long, each ending on a punchy closing line.
- Trailing -ing clauses: "..., highlighting the importance of observability."
- delve, leverage, seamless, robust, comprehensive, crucial, foster, harness, em-dash overuse.

The same patterns exist in Russian («важно отметить», «играет ключевую роль», «это не просто X — это Y», «давайте разберёмся»). The extended list with fixes for both languages is in `references/ai-patterns.md`. Read it when cleaning a text that smells of AI, or as a final sweep on anything longer than a page.

## What NOT to do (overcorrection)

Anti-slop easily becomes a new kind of slop. Don't:

- Cut technical detail for the sake of brevity. Brevity is about words, not facts. A flag, a version, an edge case, a data-loss warning — they stay.
- Make the text telegraphic. Infostyle is natural speech, not SMS.
- Inject "personality", jokes, or opinions into reference documentation. For a README, an API reference, or a runbook, a neutral calm tone IS the human voice.
- Change code, commands, API names, configs, quotes, or legal wording.
- Simplify into distortion. "The operator stores state in etcd" cannot become "the operator remembers everything".

## Examples

**Bureaucratese → plain**

Before: "This service performs the processing of incoming requests with the purpose of ensuring an even distribution of load across application instances."

After: "The service receives requests and spreads them evenly across pods."

**Bullet mush → prose**

Before:
> **Key benefits:**
> - **Reliability:** the operator is fault-tolerant
> - **Transparency:** state is always visible
> - **Flexibility:** easy to configure

After: "The operator survives restarts without losing allocations: state lives in the CRD status and is visible through kubectl. Configuration is a single manifest — no per-node config files."

**AI intro → real intro**

Before: "In today's cloud-native landscape, managing network policies plays a crucial role. SRv6 is not just a protocol — it's a powerful tool for building flexible networks."

After: "srv6-operator allocates SIDs and programs SRv6 policies on cluster nodes through a CRD. Below: installation and your first policy."

## Final checklist

Before delivering the text, verify:

1. Does the first paragraph answer "what is this and why should the reader care"?
2. Read it aloud (mentally): if you stumble — rewrite.
3. Can a word be removed without losing meaning? Remove it. Can a fact be removed? No — put it back.
4. Does every new concept come with an example?
5. Bold usages countable on one hand, at most one list per screen, informative headings, no "Conclusion"?
6. No stop words or AI tells? When in doubt — check `references/`.
7. Three same-length sentences in a row? Split one or merge two.
