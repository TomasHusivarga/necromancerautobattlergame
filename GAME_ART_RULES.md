# Game Art Rules

These rules exist because the game must stay readable in motion, at gameplay scale, and across many AI-generated assets. Pretty concept art is not enough.

## Core Rule

Every asset must support gameplay readability first.

Good game art must:

- Communicate what the object is.
- Communicate what it does.
- Stay readable at final in-game size.
- Match the camera angle.
- Match the lighting and palette.
- Fit the technical pipeline.
- Be easy enough to reproduce consistently.

Reject assets that look impressive as a standalone illustration but become muddy, confusing, or inconsistent in Unity.

## Big Shape Rule

The target is not detailed concept art. The target is graphic, hand-drawn game art built from large readable shapes.

Every asset should be designed as:

```text
big silhouette -> large shadow blocks -> 2-3 material accents -> small details only where needed
```

Do not start with texture. Do not cover the whole asset with scratches, stitches, cracks, pores, straps, and noise. Details should support the big shape, not replace it.

For characters:

- Use large connected body masses.
- Use a few bold shadow shapes.
- Use detail clusters only at focal points: face, weapon/attack limb, mutation.
- Keep empty/resting areas on the body so the eye can read the form.
- Avoid evenly distributed micro-detail across the entire sprite.

For environments:

- Use large value groups.
- Keep the lane center clean.
- Put detail at edges and focal landmarks.
- Background should read as shapes, not wallpaper texture.

For UI:

- Use clear frame shapes.
- Keep interiors plain for real Unity text.
- Avoid overly ornate borders that create visual noise.

## Readability Hierarchy

Judge assets in this order:

1. Silhouette.
2. Large internal shadow shapes.
3. Value contrast.
4. Gameplay role.
5. Color identity.
6. Material detail.
7. Small decorative detail.

If the silhouette fails, details do not matter.

## Silhouette Rules

Characters need strong outer shapes.

For zombies:

- Head shape must read separately from torso.
- Torso mass must show the zombie role: brute, plague, runner, etc.
- Front arm must clearly show attack function.
- Back arm must not visually merge with torso.
- Front and back legs must not fuse into one blob.
- Feet must make ground contact readable.

At the asset's intended gameplay size, the player should understand:

- Is this unit fast or slow?
- Is it tanky or fragile?
- What is its main attack?
- Is it infected/mutated/special?

Silhouette test:

```text
Convert to black silhouette.
Scale to expected lab preview, UI, or battle size.
If the role is not readable, reject or redesign.
```

## Value And Contrast Rules

Use value contrast more than tiny detail.

Characters:

- Highest contrast.
- Clear rim/edge separation from background.
- Important gameplay parts should have stronger contrast.

Backgrounds:

- Lower contrast than characters.
- Fewer sharp details near the lane center.
- Dark enough that health bars, effects, and units remain readable.

UI:

- Highest text readability.
- Decorative frame contrast must not compete with labels/numbers.

Do not let everything use the same contrast level. If everything is detailed, nothing is readable.

## Color Rules

Use color for gameplay meaning.

Suggested color language:

- Necromancer/player: sickly green, bone, black iron.
- Human enemies: torch orange, dull red cloth, steel, leather.
- Plague: green glow, yellow-green fluid, rotten grey flesh.
- Brute: darker flesh, heavy iron, bigger shadow blocks.
- Runner: sharper shapes, leaner silhouette, less armor.
- UI neutral: parchment, brass, dark metal, bone.
- Warnings/damage: muted red.

Avoid:

- Pure monochrome green.
- Random saturated colors.
- Background colors that compete with unit identity.
- Tiny color details that disappear at intended gameplay size.

## Detail Density Rules

Detail must be controlled.

Use more detail on:

- Lab preview character.
- UI icons.
- Large structures.
- Master reference art.

Use less detail on:

- Battle units.
- Background terrain.
- Repeated props.
- Far background.

AI often adds too much micro-detail. Remove or reject noisy texture if it damages readability.

Hard limits for the master style:

- No full-surface scratch/noise treatment.
- No equally detailed every-inch rendering.
- No tiny repeated stitches everywhere.
- No metal straps covering the whole body.
- No busy background directly behind active units.
- No small props competing with character silhouettes.

Acceptable detail pattern:

- 70% large clean shape/shadow.
- 20% secondary material shapes.
- 10% small detail accents.

For screen mockups and master references, use an even stricter readability target:

- 80% large readable layout blocks.
- 15% secondary shapes.
- 5% accent detail.

Do not generate finished-looking dense illustration screens as production references. If a concept requires zooming in to understand the UI or units, it is too detailed.

Screen mockup hard limits:

- Lab builder mockup: one main zombie preview, one inventory panel, one stat/part panel, one bottom action/resource strip.
- Battle mockup: 3-5 squad groups per side, 2-3 spell effects maximum, one bottom spell bar.
- Avoid tiny repeated unit clusters, highly textured ground everywhere, ornate borders around every panel, and dozens of small icons.
- Prefer flat readable UI blocks and strong spacing over decorative complexity.

## Shape Language Rules

The game should have a recognizable shape language.

Recommended direction:

- Hand-drawn gothic dark fantasy.
- Bold ink outlines.
- Sharp angular shadow shapes.
- Slightly exaggerated silhouettes.
- Corpse-engineering details: clamps, stitches, bone pins, green reagent glass, metal brackets.

Avoid making every asset rounded, smooth, realistic, or generic fantasy.

## Camera And Angle Rules

Use the correct project camera standard for the screen:

- Lab/zombie builder: side-view modular paper-doll art.
- Battle: old-RTS high-angle orthographic battlefield art.
- UI: front or three-quarter icon art as needed for clarity.

Do not mix the lab and battle cameras in one asset. Side-view zombies are for construction and inspection. Battle units are smaller high-angle sprites designed for many squads on screen.

## Modular Zombie Rules

Lab modular zombie art must follow:

- `ART_RIG_GUIDE.md`
- `CAMERA_AND_PERSPECTIVE.md`
- `assets/rigs/zombie_side_v1.json`

Required slots:

- `head`
- `torso`
- `front_arm`
- `back_arm`
- `front_leg`
- `back_leg`

Important:

- `front` means camera-near, not travel direction.
- `back` means camera-far, partly behind the body.
- Do not generate fused legs.
- Do not generate torso with arm attached.
- Do not generate visible arm sockets, shoulder holes, or mechanical limb slots on the torso.
- Shoulder joints should be plain overlap/stump areas because separate arm sprites cover them in Unity.
- Do not generate a full body when only one part is requested.
- Do not accept parts that only work with the matching set.

Battle zombie sprites are a separate asset category. They may be simplified full-body RTS-scale sprites derived from a zombie design/family, and they do not need to expose every modular body part in MVP.

## Separate Part Generation Rule

For modular zombies, test parts as separate generations before trusting a full-body sheet.

Required test process:

1. Generate one full assembled style preview only to establish the family identity.
2. Generate each slot as its own separate image: `head`, `torso`, `front_arm`, `back_arm`, `front_leg`, `back_leg`.
3. Save each part as its own file and record the prompt.
4. Assemble the parts in Unity or a local preview to check whether they work together.

Reason:

- Full-body sheets often look better, but hide whether the rig actually works.
- Separate generations reveal style drift, anchor drift, wrong limb direction, accidental extra body parts, and weak overlap areas.

Separate part tests are not production-approved until they pass the rig assembly check.

When generating a single slot:

- The image must contain only that slot.
- The part must be drawn on the full `1024 x 1024 px` canvas.
- The part must face right.
- The anchor area must stay near the canonical coordinate.
- Use the current master-shape style: bold silhouette, large shadow blocks, restrained detail.
- Avoid fake labels, guides, text, floor shadows, frames, and other body slots.

## Animation Readiness Rules

A body part must support animation.

Before accepting a part, ask:

- Can this rotate from the pivot without looking broken?
- Is there enough overlap at the shoulder/hip/neck?
- Are shoulder joints covered by limb overlap instead of drawn as visible sockets?
- Will the front arm attack arc read?
- Can the legs alternate in a walk cycle?
- Does the foot look like it can plant on the ground line?

If a part only works as a static illustration, it is not ready.

## UI Rules

UI should be gothic but practical.

Rules:

- Real text must be added in Unity, not baked into generated images.
- UI frames need plain inner space.
- Icons must read at small size.
- Buttons need normal/hover/pressed/disabled states later.
- Do not let decorative borders consume too much space.
- Use clear icon shapes before decorative detail.
- Keep the number of visible panels low. If every edge has decoration, the interface becomes unreadable.
- Inventory grids should show fewer larger examples in concept art, not dozens of tiny final icons.

UI style:

- Bone.
- Brass.
- Dark iron.
- Parchment.
- Green glass.
- Inked gothic edges.

## Environment Rules

Environment should support units, not compete with them.

Battle terrain/backgrounds:

- Old-RTS high-angle orthographic ground plane.
- Darker and lower contrast than characters where units overlap.
- Strong readable terrain material groups.
- Minimal busy detail behind unit silhouettes.
- Ground contact must be clear.
- Use broad terrain patches first. Do not fill the whole battlefield with cracks, pebbles, grass blades, bones, and rubble.

Props:

- Strong silhouette.
- Limited detail.
- Consistent material language.
- Scale category must be clear.

Structures:

- Big readable shape first.
- Details second.
- Battle structures must match the old-RTS high-angle camera, with visible tops/roofs and believable front/side faces.
- Lab structures and props can use side-view presentation if they only appear in the builder.
- Avoid mixing side-view facades into the RTS battlefield.

## VFX Rules

Effects must communicate gameplay quickly.

Rules:

- Do not hide unit silhouettes.
- Use short, readable shapes.
- Use color consistently.
- Keep plague/heal/death/armor-break visually distinct.
- Transparent background for production VFX.

First VFX language:

- Plague: green smoke, bubbles, skull wisps.
- Hit: pale slash/impact flash.
- Armor break: orange sparks, cracked shield shape.
- Death: green soul wisp.
- Heal: soft green upward glow.

## AI Generation Rules

Every production prompt must include:

- Asset category.
- Exact use in game.
- Camera angle.
- Canvas size.
- Background requirement.
- Style rules.
- Avoid list.
- Whether it is concept, reference, or production.

Do not generate large batches until one asset from that category passes Unity readability.

## Scale Test

Every accepted asset must be tested at approximate final scale:

```text
Lab zombie preview: 300-700 px tall on screen
Battle unit: small RTS squad-scale sprite, exact size to be validated in Unity
Elite/boss unit: larger than normal battle unit but still compatible with RTS camera
UI icon: 32-96 px
Small prop: 64-128 px
Medium prop: 128-256 px
Large structure: scene-dependent
```

If the asset only looks good at full size, it is not good enough.

## Acceptance Checklist

Before accepting an asset:

- Silhouette reads.
- Value contrast works.
- Gameplay role is clear.
- Camera angle matches.
- Style matches the master direction.
- It works at expected in-game scale.
- No fake readable text.
- No watermark.
- No accidental extra objects.
- No heavy manual repainting required.
- For modular parts, anchors and slot boundaries are plausible.

## Master Style Candidate Checklist

A master style reference must show:

- Character readability.
- Enemy readability.
- Lane readability.
- Environment treatment.
- UI treatment.
- Prop language.
- VFX language.
- Palette.
- Lighting.

Reject a master candidate if it is too busy to read at a glance.

## Iteration Notes

Older style candidates are part of the decision trail, not automatic production references. When a newer candidate fixes a problem, mark the older one as superseded in its prompt notes instead of deleting it.

Current direction:

- Prefer candidate images that look like shape/design sheets, not finished illustration spreads.
- Strongest references should use large silhouettes, large shadow blocks, quiet empty areas, and restrained accents.
- A full-body zombie in a master reference is only a style target. Production zombie art still needs separate rig-compatible parts on the project canvas with the approved anchors.
