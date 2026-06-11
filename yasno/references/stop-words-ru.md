# Russian: stop words and bureaucratese (канцелярит)

Reference for pass 1 when the text is in Russian. The principle: a word gets deleted if the meaning doesn't change without it, or replaced with something concrete.

## Канцелярит → plain language

| Bureaucratese | Replacement |
|---|---|
| данный, указанный | этот / тот / drop |
| является (чем-то) | это / a dash: «X — инструмент» |
| осуществляет проверку / запуск / обработку | проверяет / запускает / обрабатывает |
| производит установку / настройку | устанавливает / настраивает |
| выполняет функцию | делает / отвечает за |
| в рамках проекта / процесса | в проекте / при... / drop |
| с целью | чтобы |
| посредством, путём | через / с помощью / instrumental case |
| в случае, если | если |
| на сегодняшний день, в настоящее время | сейчас / drop |
| имеет возможность | может |
| необходимо отметить | drop, state the point |
| вышеуказанный, нижеследующий | этот / ниже / link to the section |
| функционал | возможности / what exactly it can do |
| при помощи использования | через |
| обеспечивает возможность | позволяет / даёт |
| в процессе работы | при работе / когда работает |
| по причине того, что | потому что |
| во избежание | чтобы не |

## Verbal nouns → verbs

Pattern: «производить / осуществлять / выполнять» + noun ending in -ние/-ка → verb.

- «выполнить перезагрузку» → «перезагрузить»
- «произвести валидацию» → «провалидировать» / «проверить»
- «осуществить миграцию» → «мигрировать» / «перенести»
- «при возникновении ошибки» → «если возникла ошибка» / «при ошибке»

## Parasitic fillers (delete entirely)

стоит отметить, важно отметить, следует подчеркнуть, как известно, как уже говорилось, на самом деле, по сути, в принципе, собственно, безусловно, конечно же, разумеется, кстати говоря, между тем, при этом (when there is no actual connection), таким образом (opening every other paragraph), итак.

Exception: a filler stays if it genuinely changes meaning. «Кстати, в v2 этот флаг убрали» is fine if it really is a side note.

## Intensifiers (replace with a fact or cut)

очень, крайне, чрезвычайно, максимально, значительно, существенно, невероятно, по-настоящему, действительно (as an intensifier).

- «очень быстро» → «за 200 мс» / «быстрее v1 в 3 раза» / just «быстро» if there is no number
- «существенно упрощает» → say what exactly it simplifies: «вместо пяти манифестов — один»

## Judgments without facts (replace with the concrete thing)

качественный, надёжный, удобный, эффективный, оптимальный, гибкий, мощный, простой, интуитивный.

Rule: a judgment is allowed only when the proving fact stands right after it. «Надёжный: переживает рестарт ноды без потери состояния» — fine. «Надёжное решение» on its own — junk.

## Marketing clichés (delete always)

уникальный, инновационный, передовой, лидирующий, решение под ключ, лучший в своём классе, широкий спектр возможностей, индивидуальный подход, динамично развивающийся, незаменимый.

## Hedges

как правило, в большинстве случаев, обычно, чаще всего, в целом, в общем случае.

Keep one only when exceptions really exist — and then name them: «Под Linux работает из коробки; на macOS нужен ещё один шаг (ниже)».

## ты / вы

Pick one form of address and keep it through the whole text. The documentation default is «вы» lowercase — capitalized «Вы» is business-letter bureaucratese.
