---
name: ai-video-asset-manager
description: Manage AI video production assets for consistent long-form generation. Handles character sheets, multi-state variants, locations, voice locks, shot rules, period constraints and iteration logs. Use for AI feature films, series, or any multi-shot project requiring locked identity, states, scenes and voice. Triggers on character sheet, asset library, character states, location kit, voice lock, CINEDANCE, Higgsfield workflow, consistent AI film assets, or when building production-ready reference systems for text-to-video.
---

# AI Video Asset Manager

Production system for locking visual and audio identity across long AI video projects. Derived from the open-sourced Higgsfield "Cully Hill Boys" pipeline (text-to-video only, $2M feature).

Core principle: **Assets first. Nothing generates until every face, place, prop and voice condition is locked.**

## Core Production Rules

1. Assets first — no generation until character sheets, states, locations and voice blocks are locked.
2. Describe everything every time — the model has no memory.
3. Change one thing at a time.
4. Give the model less freedom — a corner, not a room; a map, not guesswork.
5. Shot won't land after 10-15 iterations? Simplify the shot, not the words.
6. Log every version: what changed + verdict.

## Branch 1 — Character Base Sheet

Generate a technical three-panel character reference sheet.

**Required structure:**
- Panel 1: Full-body front view (head omitted)
- Panel 2: Full-body rear view (head omitted)
- Panel 3: Large close portrait in subtle 3/4 view (with and without smile variants)

**Critical rules:**
- Remove heads from both full-body panels. Soft small faces on wide shots are the exact faces the model will copy badly. Force it to pull face only from the close portrait.
- Prepare two close-ups: neutral + smile. Without the smile reference the model invents teeth and mouth shape every time the character smiles.
- Neutral mid-grey seamless background (#808080). Soft even lighting, no harsh shadows or rim light.
- Identical scale, camera height, lighting and ground line between front and back panels.
- Never redesign clothing, proportions or identity from the source photos.

**Prompt template location:** `references/character-sheet-prompt.md`

## Branch 2 — Character State Variants

One character = multiple locked assets, one per narrative state.

Examples:
- Clean / starting state
- Wet / post-water
- Injured / bloody / split brow
- Different costume acts

**Rules:**
- Never mix states inside one text prompt. Create separate full asset packages.
- Each state asset must pass a stress test: 10 generations in different poses and lighting. Must remain recognisable in 10/10.
- If the test fails, fix the description, not the model.
- Splitting assets is cheaper than arguing with inconsistency later.

Store each state as an independent sheet + prompt block.

## Branch 3 — Location / Scene Kits

Generate locations for future camera angles, not frontal wallpaper.

**Rules:**
- Never use pure frontal room plates. The model cannot read volume and invents new surroundings past the frame edges.
- Always leave an anchor: “hero at the lamp, facing the door”.
- Best practice: generate a slow walking video of the empty location. The model is forced to draw the other sides consistently. One plate → full volumetric kit.
- Period lock: write hard constraints (e.g. “nothing in frame newer than 2011”). Models default to contemporary objects.

**Old money vs new money example:**
- Old: patina, dried oxblood, tarnished gold, one aged lamp
- New: saturated crimson, mirror-bright brass, identical lamps in symmetry
Never mix the two visual languages.

## Branch 4 — Voice Lock

Voice is not an asset image. It is a fixed block of conditions.

**Structure the voice block once and paste it unchanged every time the character speaks:**
- Register (e.g. low gravelly)
- Tempo
- Accent written phonetically inside the lines (th → f/v, dropped h, glottal t, -ing → -in')
- Manner / delivery

Never rephrase or use synonyms. Changing wording widens the sampling space and the voice drifts.

For music performance: pre-record the track, cut into breath-length blocks, feed the audio file itself as “the live performance”. Assign mouth ownership explicitly or every character mouths the lyrics.

## Branch 5 — Shot Construction Devices

Proven locking techniques:

- **Speech count lock**: “The take contains exactly three words: ‘Pull it, Oli.’” Prevents model-added mumbles or foreign language.
- **Height ruler**: Never use “tall/short”. Always bind to a fixed environment point or body part.
  Example: “大爷的肩膀高度与门把手齐平”
  Extreme scales must be written very explicitly and repeated, otherwise the model defaults to normal proportions.
- **Multi-character positioning**: 
  1. Lock one spatial anchor first (e.g. reception desk on the right)
  2. Position every character relative to that anchor
  3. Use concrete body-part comparisons between characters (“大妈的肚脐高度与大爷眼睛齐平”)
  4. Keep the description order consistent: Anchor → Character A → Character B
- **Off-screen event list**: Write what must NOT appear (no limb, no shadow, no reflection) when an action happens outside frame.
- **Asynchronous reactions**: Two characters reacting to the same event must never move in sync. Synchronised reaction reads as animation.
- **Geometry from text**: Assets carry the picture; wording carries geometry and camera.

## Branch 6 — Iteration & Logging

- Work scene by scene.
- Surgical changes only: one line changes, everything else word-for-word identical.
- Maintain a version log (version number, exact change, pass/fail).
- After 10–15 failed iterations the problem is almost never more wording. Simplify: split the shot, remove an action, change the angle.

## Branch 7 — Exception Handling

When a complex physical interaction (fight, continuous contact, weapon exchange) refuses to generate cleanly:
- Film real stunt performers on phone.
- Use the footage as pure motion reference.
- Overlay locked character assets, interior and lighting on top.
This is the only permitted departure from pure text-to-video.

## Workflow Order

1. Lock all base character sheets (with smile variants).
2. Create every required state variant and stress-test them.
3. Build location kits with anchors + optional walk-through videos.
4. Write and freeze voice blocks.
5. Only then generate shots, always referencing the locked assets by exact description.
6. Log everything.

## References

- Detailed character sheet generation prompt → `references/character-sheet-prompt.md`
- Voice block examples → `references/voice-blocks.md`
- Shot device examples → `references/shot-devices.md`
- Full production rules checklist → `references/production-rules.md`
