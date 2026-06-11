# English: stop words, fluff, and corporate jargon

Reference for pass 1 when the text is in English. The principle: a word gets deleted if the meaning doesn't change without it, or replaced with something concrete.

## Bureaucratic → plain

| Fluff | Plain |
|---|---|
| utilize, leverage, harness | use |
| facilitate | help / let / make possible |
| in order to | to |
| prior to | before |
| subsequent to | after |
| in the event that | if |
| due to the fact that | because |
| at this point in time | now |
| with regard to, in terms of | about / for / drop |
| a number of | several / the exact number |
| the majority of | most |
| in close proximity to | near |
| has the ability to, is able to | can |
| it is recommended that you | we recommend / straight imperative: "Set..." |
| please note that | drop it, say the thing |
| as per | per / following / drop |
| via the use of | with |
| in conjunction with | with |
| is dependent on | depends on |
| make use of | use |

## Nominalizations → verbs

Pattern: perform / conduct / carry out / make / provide + noun → verb.

- perform an installation → install
- conduct an analysis → analyze
- make a determination → determine
- provide assistance → help
- carry out a migration → migrate
- take into consideration → consider
- reach a conclusion → conclude

## Throat-clearing openers (delete entirely)

It should be noted that; It is worth mentioning that; Needless to say; It goes without saying; As you may already know; First and foremost; At the end of the day; The fact of the matter is; When it comes to (as an opener); Generally speaking.

## Intensifiers (replace with a fact or cut)

very, really, extremely, incredibly, highly, significantly, substantially, dramatically, vastly.

- "significantly faster" → "3× faster on our benchmark" or just "faster"
- "highly scalable" → up to how many nodes/RPS was it tested

## Hedges and weasels

somewhat, fairly, quite, rather, arguably, essentially, basically, typically, usually, in most cases, more or less.

Keep one only when exceptions really exist — and then name them: "Works out of the box on Linux; macOS needs one extra step (below)."

## Vague praise (keep only with proof right next to it)

powerful, robust, flexible, seamless, intuitive, user-friendly, efficient, scalable, lightweight, blazing fast.

"Lightweight: a single 8 MB static binary" — fine. "A lightweight solution" on its own — junk.

## Marketing clichés (delete always)

world-class, best-in-class, cutting-edge, state-of-the-art, next-generation, industry-leading, game-changing, turnkey, end-to-end solution, unlock the power of, take X to the next level, supercharge, effortlessly, revolutionize.

## Redundant pairs (cut the dead half)

advance planning → planning; end result → result; final outcome → outcome; completely eliminate → eliminate; absolutely essential → essential; basic fundamentals → fundamentals; future plans → plans; past history → history; join together → join; revert back → revert; repeat again → repeat; brief summary → summary; new innovation → innovation; close collaboration → collaboration; mutual agreement → agreement.

## Filler transitions

Additionally, Furthermore, Moreover, In addition — once per text is fine. At the start of every paragraph it's a machine-text tell. Most paragraphs need no connector at all: if the order of thoughts is right, the reader sees the connection.

## Politeness

"Please" once per instruction is fine; in every sentence it's noise. "Kindly" — never. Steps of a procedure need no politeness at all: "Run the installer", not "Please kindly run the installer".
