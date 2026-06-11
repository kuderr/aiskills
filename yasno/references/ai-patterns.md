# AI tells: the extended list

Reference for the final sweep. These are the patterns readers and detectors use to spot machine-generated text. Each comes with a replacement or a way to fix it.

## English

### Vocabulary red flags (replace with plain words)

delve → look at / dig into; leverage → use; utilize → use; seamless → smooth / drop; robust → reliable / a concrete fact; comprehensive → full / drop; crucial → important / drop; foster → build / encourage; harness → use; streamline → simplify; elevate → improve; empower → let / enable; cutting-edge, state-of-the-art → drop; game-changer → drop; landscape ("the testing landscape") → drop; journey ("your Kubernetes journey") → drop; dive deep → look at.

### Phrase patterns

- "It's important to note that..." → say the thing
- "In today's fast-paced world..." → delete the whole opener
- "Whether you're a beginner or an expert..." → delete
- "Let's explore / dive into..." → just explore it
- "In conclusion / To sum up" + a recap paragraph → delete
- Negative parallelism: "It's not just a tool, it's a platform" → state what it is
- The rule of three: "fast, simple, and secure" → keep two, or one with a concrete fact, or an honest list of however many items there really are
- Trailing -ing clauses: "..., highlighting the importance of observability" / "..., ensuring reliability" → split into a sentence with a real subject, or delete if empty
- Vague attribution: "Industry experts agree...", "Many developers find..." → name the source or drop the claim
- Em-dash overuse — more than one or two per paragraph reads as AI; replace with commas, periods, or restructure

### Punctuation and formatting tells

- Bold mid-sentence for "emphasis", sprinkled everywhere
- Bullet lists where every item is "**Word:** explanation"
- A heading every two paragraphs
- Emoji in headings (🚀 Features)
- Every section ending with a one-line takeaway
- Curly and straight quotes mixed inconsistently (pick one, keep it)

## Russian

### Marker phrases (delete or rewrite)

- «Важно отметить, что...» → state the point directly
- «Стоит подчеркнуть...» → delete
- «Давайте разберёмся / погрузимся / рассмотрим подробнее» → delete, just do it
- «Не секрет, что...», «Ни для кого не секрет...» → delete
- «В современном мире...», «В эпоху цифровизации...» → delete the whole opener, start with the substance
- «Играет ключевую/важную роль» → say what it concretely does
- «Представляет собой» → «это» or a dash
- «Широкий спектр», «целый ряд» → list what exactly
- «Подводя итог», «В заключение хочется сказать» → delete along with the recap paragraph
- «Это позволит вам...» in every other paragraph → vary or delete

### Structural patterns

- **The rule of three**: «быстро, удобно и безопасно», «разработчики, тестировщики и аналитики». Three parallel items as a rhythmic tic. Fix: keep two, or one with a concrete fact, or an honest list of however many there really are.
- **Negative parallelism**: «Это не просто X — это Y», «Дело не в X, а в Y». Fix: say directly what Y is.
- **Question-as-opener**: «Что же такое оператор? Давайте разберёмся». Fix: lead with the answer.
- **Punchy closer** on every paragraph: a final aphorism-like line. Once or twice per text is fine; on every paragraph it's a tell.
- **Identical paragraphs**: each one three sentences of roughly equal length. Fix: merge, split, change the rhythm.
- **Echo structure**: every section built the same way (definition → three bullets → takeaway).

## Fixing rhythm (both languages)

1. Read the paragraph aloud. If the intonation is identical on every sentence, the rhythm is machine-like.
2. Find two adjacent short sentences about the same thing — merge them.
3. Find a sentence with three commas and a subordinate clause — split it.
4. Make sure at least one sentence in the paragraph doesn't start with the subject.
