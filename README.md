# Marketing Ad Scripter

Turns a creative bank into a shootable script pack: modules with beats and timings, a continuity kit per angle, generation prompts, and the assembly map that says how the pieces cut back together.

It decides, per module, whether the thing is GENERATED or must be REALLY CAPTURED — and it treats that line as load-bearing. A genuine interface, a real result, a real person's testimonial: those are captured, because a model asked to render them produces something that is convincing and false, and the ad then claims something the product did not do.

Continuity is specified rather than hoped for. Modules generated separately only cut together if the wardrobe, the set, the light direction and the production register were locked in writing beforehand; continuity discovered at the edit is continuity that was never there.

Every prompt ships with a variant set and a stated number of runs, because one run is not evidence that a prompt works — it is one sample, and the difference between the runs is what tells a good prompt from a lucky frame. It writes the spec and the QA protocol; it does not generate, render or measure anything.

## What this is, precisely

A FindAgent **`mcp-tool`** agent. Each of its 6 tools is a
`prompt-template` action: the tool renders an instruction and hands it back to the
model that called it.

Two consequences worth being blunt about, because they decide whether this is useful to you:

- **It calls no model and reaches no network.** A tool call costs nothing and returns
  the same text for the same input, every time. There is no API key, no credential
  slot and no egress.
- **It observes nothing.** It has no access to your repository, your logs, your
  analytics or your devices. Every template is written so that supplying nothing
  produces an honest statement of what is missing rather than a confident-looking
  answer about data nobody provided. If you ask for a report and give it no findings,
  it will tell you the work has not been done — not invent it.

## Tools

| Tool | What it returns | Required input |
|---|---|---|
| `plan_module_breakdown` | Break an angle's creative into producible modules and decide, per module, whether it is generated or must be really captured — treating anything that claims what the product did as capture. | `creative_bank_angle` |
| `build_continuity_kit` | Lock the continuity rules for an angle — wardrobe, set, light direction, production register and the reference assets — so separately produced modules cut together. | `angle_modules` |
| `write_shot_beats` | Write a module as timed beats — what is on screen, what is said, what is written — with the sound-off reading checked beat by beat. | `module`, `continuity_kit` |
| `write_generation_prompt` | Write the generation prompt for a module with its framing limits, constraint block and variant seeds, plus the wording lint that silently changes what a generator does. | `module_beats`, `continuity_kit` |
| `define_qa_protocol` | Define what QA receives and what it must check for these modules, including how many runs per prompt and which dimensions cannot be judged from frames alone. | `module_specs` |
| `draft_script_pack` | Assemble the script pack for production — modules, continuity kits, prompts, the assembly map and the QA protocol — refusing to produce one when no modules were specified. | `campaign_context` |

Optional inputs render as empty when omitted. Every template names that case and says
what it could not determine, so an empty slot degrades into a stated gap rather than a
dangling clause.

## Part of a department

This agent is one member of the **marketing video ad** department, a
hub-orchestrator team of 7. The hub is `marketing-brief-scoper`, which locks the brief every later
stage reads; the other members are
reached through it or called directly as `<alias>__<tool>`.

| Agent | Stage in the pipeline |
|---|---|
| `marketing-brief-scoper` | 1 — interviews for the brief and freezes it (department hub) |
| `marketing-ad-researcher` | 2 — competitor harvest plan, longevity ranking, customer voice, coverage |
| `marketing-angle-strategist` | 3 — scored angle map with auditable arithmetic |
| `marketing-hook-writer` | 4 — the modular creative bank, built on verbatim customer language |
| `marketing-ad-scripter` | 5 — modules, continuity kits, prompts, assembly map, QA protocol |
| `marketing-production-planner` | 6 — blockers, tracks, cost estimate, shoot briefs, release gates |
| `marketing-ad-tester` | 7 — clip QA, test design, readout, and the feedback loop back to 3, 4 and 5 |

Each member is published independently and works on its own.

## Provenance

`source/scripter-origin.md` is the note recording how this member's contract was reconstructed. The tool templates carry its
instructions, parameterised: anything the original hard-coded to one team's repositories,
file paths or people became an input you supply, and where a template would otherwise
depend on reading something it cannot reach, it asks for that material as an argument
instead.

## Licence and use

Published by Kata Team on FindAgent. Free to connect.
