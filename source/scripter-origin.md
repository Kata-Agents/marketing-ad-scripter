# Where this member came from

`marketing-ad-scripter` was not converted from a skill file, the way the other
six members of this department were. It was reconstructed from the contract the
surrounding stages specify, because the source folder does not contain one.

## What was missing

The pipeline the source files describe has seven stages:

    Scoper -> Researcher -> Angler -> Hooksmith -> Scripter -> Producer -> Tester

Six skill files exist. **There is no scripter file.** Stage five, the one that
turns words into something producible, is absent from the folder.

## How its contract was recovered

The other six define it precisely enough to rebuild, because each one either
hands it something or reads what it produced:

- **Hooksmith** states its own boundary as "you do not write shot lists, camera
  directions, timing, or storyboards. That is Scripter." So those four are the
  scripter's output.
- **Producer** reads `scripts.json` and works from `continuity_kit` (visual
  rule, wardrobe and set lock, light direction, production register), from
  modules carrying `capture_method: real` or `generated`, from `variant_seeds`,
  and from `qa_protocol.runs_per_prompt`, default three. Each of those is a
  field the scripter must therefore produce.
- **Tester's** qa mode compares a delivered clip against the scripter's
  `seedance_prompt` and `beats`, against the angle's `continuity_kit`, and
  against Decision A (text native or post) and Decision B (voice native or
  post). So the scripter owns those decisions.
- The **assembly map** that Tester's setup mode reads comes from the script
  pack as well.

Everything this member does is one of those. Nothing was invented to fill the
gap beyond the wording.

## What is NOT reconstructed

The source files refer to a specific video generator by name and to a shared
run-folder contract at `~/.claude/marketing/PIPELINE.md`. **That file does not
exist on the machine this was built from**, so the run-folder layout, the id
chain format and the connector notes could not be read. This member is
therefore written tool-neutral: it specifies structure, framing limits,
constraint blocks and variant seeds, and says explicitly that parameter names
and limits must be confirmed against whatever generator is actually used.

If the real scripter file turns up, it should be diffed against this member
rather than assumed to agree with it.
