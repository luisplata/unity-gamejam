# Brainstorming

The volume-first method: generate raw options under a clock, then shape them.

## Definition and purpose

Brainstorming fills an empty pool before anything in it is examined. Three rules hold at once: judgement is deferred until the clock ends, an idea grows out of another rather than replacing it, and a question that arrives mid-burst is recorded, not asked. Its purpose is material for the caller — a pool, its clusters, and the connections between them. It produces no decision.

## When to use, when not to use

Use it when:

- the problem is open and the pool is empty or thin;
- the caller wants more directions than one person would have written alone;
- nobody has committed to a direction yet.

Do not use it when:

- the pool already has clusters with declared relations — that needs shaping, not volume;
- the caller has one mechanism to bend — that is Forced Combination;
- the caller wants one candidate defended, compared, or chosen — that is convergence.

## Inputs and preparation

Reads `challenge` (one sentence, required) and, when present, `knowns`, `max_minutes`, `prior_attempts[]`. It runs from `challenge` alone.

- Write the challenge back as a question and pair it with a number: "twelve ideas in fifteen minutes", the stop time read from `max_minutes` (with no field, say "twenty minutes" once and start).
- Treat `prior_attempts[]` as "already tried, do not re-emit the same wording" — the causes are seeds, not forbidden ground.
- Note the two facts you are missing. They go to `open_questions[]`, not into a question.

## Procedure

Five passes. Each has a stop condition; the clock can end any of them, and the pool as it stands is the return.

1. **Frame** — restate the challenge as one question, state the target count and the stop time, empty the pool. Stop when the frame is a question and the target is a number.
2. **First burst** — write ideas at speed, one line each, attaching `provenance` at creation and editing nothing. Stop at five entries, or when a full minute yields no new line.
3. **Build** — take the most recent three entries and change exactly one thing in each: the actor, the medium, the constraint. The new entry is `user` with `derived_from`; the seed keeps its own label and wording. Stop when a change returns the same idea with different nouns.
4. **Shift the frame, then burst again** — change one boundary on purpose: another person, another place, another season, smaller budget. Two minutes of generation from the new frame. Stop at the clock, then move to shaping with whatever is left.
5. **Shape, then clarify** — name three to five clusters, declare each `relation` in a sentence, and write one-sentence connections between entries from different clusters. Then ask what the frame still needs — one question at a time, no more than two, and only where the answer would change the frame. Stop when both are spent or the clock ends, then close.

## Example prompts

- "Brainstorm with me for 15 minutes: how might a small museum reach people who never walk in?"
- "Dame veinte ideas para que la gente del barrio use la plaza en invierno. Sin filtrar ninguna."
- "Five more minutes, and build on the last three instead of starting new ones."

## Worked example

```text
challenge: a neighbourhood library wants to reach teenagers who never come in.
frame: how might the library reach them where they already are? · 12 ideas, 15 min.

B01 a shelf inside the laundromat                       (ai, C1)
B02 lend seeds and tools, not only books                (ai, C2)
B03 a stall outside the school gate at 3pm              (user, C1)
B04 let one teenager curate a shelf each month          (ai, C3)
B05 a table at the Saturday football pitch              (user, C1)
B06 lend a backpack: a book, a snack, a bus card        (ai, C2)

user: "B06 but the borrower picks the snack"
B07 backpack, snack chosen by the borrower              (user, C2, derived_from B06)

B08 library cards handed out in the school lunch queue  (user, C1)

clusters: C1 "go where they already are" (B01 B03 B05 B08)
          C2 "lend something that is not a book" (B02 B06 B07)
          C3 "hand the curation over" (B04)
connections: B04+B08 -- "the person who curates is the one who can hand the card over"
open_questions: does the laundromat have wall space
suggested_next: The caller's criteria decide next; C1 and C2 can run as one programme.
```

B06 stays `ai` and B07 arrives as `user`; the seed is never relabelled, and the pair is never merged into one entry.

## Common mistakes

- **Polishing during the burst.** Fixing wording mid-pass costs entries. Keep the line raw and edit in the shaping pass.
- **Word association dressed as a connection.** "Lending seeds and lending books are both lending" names a shared word, not a mechanism. Correct it by stating what changes for the person doing it, or drop the connection.
- **Judging before the clock ends.** "That one won't work" is an answer for later, not a filter now. Record the doubt, keep the entry.
- **Asking instead of assuming.** A missing fact is not a question unless it changes the frame. State the assumption into `open_questions[]` and continue.
- **Clustering at the third entry.** Early grouping flattens the pool into what you already believed. Cluster only after the target is met or the clock forces it.

## Outputs

- `pool[]` — every entry, each with `provenance`, `cluster`, and `derived_from` where it was built from another.
- `clusters[]` — three to five, each with members and a one-sentence `relation`.
- `connections[]` — `why` is one sentence and names a mechanism.
- `open_questions[]` — the assumptions and deferred questions; `suggested_next` — one sentence, advisory.
- `verdict` — not emitted. Nothing returned here orders the pool by quality.

## Quality checklist

- [ ] The frame is a question, and the target is a number.
- [ ] Every entry has a `provenance` and a `cluster`.
- [ ] Three to five clusters, each with a declared `relation`.
- [ ] Every connection is one sentence and survives the "shared word" test.
- [ ] Questions: none during a burst, two at the most, all after generation.
- [ ] Every deferred question sits in `open_questions[]`.
- [ ] No entry, sentence, or ordering states which idea is better.
- [ ] The return works with `challenge` alone — no assumption about the domain.
