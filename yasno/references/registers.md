# Registers: tone per document type

The same material is written differently in a README, a runbook, and a blog post. Before writing, identify the document type — it sets the register: temperature, pronouns, whether opinions and humor are allowed. Word rules (stop words, concreteness, formatting) apply equally in every register.

## README

Reader: a stranger deciding in 30 seconds whether to use the tool. Register: neutral, compact. The first paragraph says what this is and what problem it solves. Imperative in instructions ("Run", "Install"). No humor, no first person, no project history at the top. Badges and screenshots only if they genuinely help understanding.

## Runbook, how-to, troubleshooting

Reader: someone mid-incident or following steps, often under stress. Register: command. Imperative, numbered steps are appropriate and welcome. Zero lyricism. A warning goes BEFORE the dangerous command, not after. Every step states the expected result so the reader knows nothing broke: "The pod reaches Running within a minute."

## Design doc, RFC, ADR

Reader: colleagues deciding whether to approve. Register: reasoning. First person plural is fine ("we propose"). Honest trade-offs are mandatory: what we lose, which alternatives were considered and why they were rejected. Naming the weak spots of your own proposal builds trust, it doesn't undermine it.

## Release notes, changelog

Reader: users, skimming. Register: factual. Breaking changes first, with migration instructions. Phrase from the user's benefit: "You can now filter policies by label", not "Added the FilterByLabel method". No self-congratulation ("we are excited to announce").

## Commit message, PR description

Reader: the reviewer now and the archaeologist a year later. Register: telegraphic — the only text type where telegraphic style is appropriate. Subject line in the imperative, up to 70 characters. Body explains what and why, not how (the how is visible in the diff). Link the issue if there is one.

## Error message, UI text

Reader: an annoyed user at the moment of failure. Register: dry and useful. Formula: what happened + what to do. "Could not connect to the cluster: token expired. Run kubectl login." No "Oops!", no "Something went wrong", no emoji.

## Email, support reply, chat message

Reader: a specific person. Register: warmth is allowed, first person is fine. But the answer to the question goes in the first paragraph, not after three paragraphs of context. If the answer is "no" — say "no" in the first sentence, then explain.

## Blog post, article

Reader: came voluntarily, will leave at any moment. Register: authorial. Voice, opinions, first person, personal stories, and humor are allowed — this is the only register where "personality" belongs. But word rules still apply: fluff and bureaucratese kill an authorial text too.

## Tutorial

Reader: a beginner doing it step by step for the first time. Register: hand-holding. Second person ("you"). After each step — what the reader should see. Explain only what's needed right now; theory "for later" goes into a link or gets cut. Anticipate the typical failure: "If you see connection refused, check that port 8080 is free."

## Two cross-cutting rules

In Russian documentation, pick «ты» or «вы» and keep it through the whole text. The documentation default is «вы» lowercase — capitalized «Вы» is business-letter bureaucratese.

Switching registers inside one document is a mistake. If a README suddenly turns jokey in the Troubleshooting section, the reader stumbles. One document — one register.
