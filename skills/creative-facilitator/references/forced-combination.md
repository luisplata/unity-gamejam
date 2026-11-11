# Forced Combination

The collision method: take two unrelated sources, extract their rules, and translate a pairing into something a person does differently.

## Definition and purpose

Forced Combination makes a possibility that neither source contains by colliding them. The unit of work is an attribute — a part, a rule, or a behaviour — never a whole noun. A pairing becomes a combination only when it survives translation into a concrete action that did not exist before. "Library plus gym" is a setting; "you return the book by completing a lap" is a combination. The difference is the verb, not the vocabulary.

## When to use, when not to use

Use it when:

- one mechanism has to become a different mechanism, not a different theme;
- the pool has one shape and more volume will only repeat it;
- a candidate was dropped and the clock still has room for one more attempt.

Do not use it when:

- the pool already has clusters with declared relations — shape them, do not collide more;
- the caller has nothing yet and needs volume — Brainstorming fills faster;
- the caller has already decided and wants the choice confirmed.

## Inputs and preparation

Reads `challenge` (one sentence, required), one or two source rules, and optionally `knowns`, `max_minutes`, `prior_attempts[]`. It runs from `challenge` alone: with no second source, take one from the caller's own material — the dropped direction, a must-have, the setting.

- Budget ten minutes and say it out loud: four for extraction, four for pairing and translation, two for the check.
- Name source one; when `prior_attempts[]` is present, its last direction is a legitimate source — a mechanism that failed is still a mechanism. Then name source two from outside the problem's own field (a sport, a kitchen, a queue, a timetable, a game of chance) and say in one clause why it is distant.
- Write down the challenge's verb. That verb is what has to change.

## Procedure

Five steps, each with a stop condition.

1. **One rule per source.** For each source, write the single rule that governs it, one sentence, present tense ("an input lands on the beat or it does not land"). Stop when both sentences state a rule rather than describe a thing.
2. **Extract into three columns** — parts, rules, behaviours — three to five items per source. "A kitchen" is a part; "food is served when it is ready, not when it is ordered" is a rule. Stop when each source has at least three items and at least one is a rule or a behaviour.
3. **Pair across columns.** A pair is eligible only when its two attributes come from different columns: a rule with a part, a behaviour with a rule. Same-column pairs produce a list, not a collision. Stop at three eligible pairs.
4. **Translate the pair into an action.** For each pair write one sentence answering "what does the person do differently now?". If the sentence only renames a source — "a platformer, but with jazz" — it is not a translation: drop it and say so in one clause. Stop when the sentence contains a new verb.
5. **Check and return.** For each survivor, name its constraint source and its mechanism change in the `why`. Return two or three. Stop at the clock with whatever survived: one survivor, or none, is a valid return.

When a candidate is dropped and time remains, this is the recovery pass: the dropped mechanism becomes source one, and a survivor must change the verb rather than the label.

## Example prompts

- "Force a combination: a bus timetable and a lending library. Ten minutes."
- "Combiná el mecanismo que descartamos con una regla de otro deporte. Dame dos."
- "Two sources: a night market and a school timetable. What changes for the person?"

## Worked example

```text
challenge: 2D platformer, theme "growth", the gravity-flip direction was dropped
           because the flip read badly at that scale. 25 minutes left.

sources:   S1 gravity-flip platformer · rule: up and down are inverted for the whole screen
           S2 one-button rhythm game (distant: no spatial skill at all) ·
              rule: an input lands on the beat or it does not land

extract:   S1 parts: floor, ceiling, player · behaviour: a jump commits you until you land
           S2 parts: the track, the beat bar · behaviour: a press is early, on time, or missed

pair A  S1 behaviour × S2 rules — the flip is available only on the beat; mistime it
        and nothing moves. Verb: "flip when you want" becomes "wait, then flip".
        why: S2's rule that a press lands on the beat or not at all. (ai, derived_from S1)
pair B  S1 parts × S2 behaviour — floor and ceiling pulse; landing early costs the next
        beat. Verb: timing the landing replaces aiming it.
        why: the same beat rule, read as a clock. (ai, derived_from S1)
pair C  S1 rules × S2 parts — the screen inverts every time the track changes. No new
        verb: a timer replaced the trigger, the action is the same. Dropped.
```

Two survivors, and every `why` names the source it borrowed from; pair C is not a combination — the flip kept its action and gained a timer.

## Common mistakes

- **Adjective swaps.** "The same mechanic with a horror theme" is one source, not two. If the verb did not move, nothing was combined.
- **Word association dressed as a connection.** "A library is a kind of archive and so is a game" names a shared category. Correct it by naming the attribute each side contributes, then translate it into an action.
- **Combining three sources.** A third source turns the sentence into a setting. Two is the load; take the third back out.
- **Skipping the translation step.** A pair is not a possibility until someone does something different. Write the action sentence before you write the `why`.
- **Extracting nouns instead of rules.** "A night market" tells you nothing; "you can only buy what the stall has made today" is extractable. Re-extract.

## Outputs

- `pool[]` — two or three entries, each `provenance`, `cluster`, and `derived_from` naming the source it came from.
- `connections[]` — one entry per survivor; `why` is one sentence and names both the constraint source and the mechanism change.
- `clusters[]` — three to five, each with a declared `relation`: one survivor plus its two sources is already three anchors, so the count comes from the material, not from padding.
- `open_questions[]` — the assumptions, the untested pairings, the dropped pair and its reason.
- `suggested_next` — one sentence, advisory.
- `verdict` — not emitted. Nothing returned here orders the survivors by quality.

## Quality checklist

- [ ] Two sources, each with its rule in one sentence.
- [ ] Each source contributed an item from a different column.
- [ ] Every survivor's `why` names the constraint source.
- [ ] Every survivor changes the verb, not the label.
- [ ] Dropped pairs were dropped for sameness, and the reason is stated in one clause.
- [ ] Two or three survivors; fewer is a valid return.
- [ ] No pairing relies on a shared category as its argument.
- [ ] The ten-minute budget was stated, and the return fits inside it.
