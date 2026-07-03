# Agent Instructions

These instructions apply to all work in this repository. Speak English.

## Before Generating Any Image Or Asset

Read these files first:

1. `AI_ART_PIPELINE.md`
2. `CAMERA_AND_PERSPECTIVE.md`
3. `ART_RIG_GUIDE.md`
4. `assets/rigs/zombie_side_v1.json` when generating zombie parts

Do not generate production assets from a standalone prompt without checking these files.

## Core Art Direction

The game uses:

- Dark fantasy 2D game art.
- Side-scrolling 2.5D, not isometric.
- Mostly side-view characters with slight three-quarter depth.
- Orthographic Unity camera.
- Clear horizontal lane readability.
- Painterly/hand-painted style, not photorealism.
- Green necromantic accents, bone, dark iron, dark wood, grave soil, muted blood, candlelight.

Avoid:

- Isometric camera.
- Top-down camera.
- Photorealism.
- Overly noisy detail.
- Fake readable text inside images.
- Random extra objects.
- Excessive gore.
- Assets that look good alone but do not match the game.

## Master Style Rule

Use the approved master style reference once it exists. Until then, generated images are concept/reference candidates only.

Do not mass-generate production assets before the master style reference and category sheets are approved.

Preferred order:

1. Master style reference.
2. Zombie reference sheet.
3. Environment reference sheet.
4. UI reference sheet.
5. Production assets.
6. Unity validation.
7. Light Photoshop cleanup if needed.

## Camera And Perspective Prompt Rule

Include this wording, or a close equivalent, in asset prompts:

```text
Side-scrolling 2.5D game art, right-facing side view with slight three-quarter depth, clear horizontal lane readability, visible top surfaces only subtly, not isometric, not top-down, not photorealistic.
```

For structures:

```text
Side-view 2.5D structure for a horizontal lane battle, facade facing camera with a small visible roof/top plane, readable silhouette, not isometric.
```

For terrain:

```text
Horizontal side-scrolling lane ground strip with slight visible top plane, dark fantasy painterly style, low contrast behind units, not top-down and not isometric.
```

## Zombie Part Rig Rules

All modular zombie parts must follow `zombie_side_v1`.

Canonical rig:

- Canvas: `1024 x 1024 px`
- Body center: `x = 512`
- Ground line: `y = 860`
- Facing: right
- Background: transparent for production parts
- Slots: `head`, `torso`, `front_arm`, `back_arm`, `front_leg`, `back_leg`

Front/back limb meaning:

- `front_arm` and `front_leg` are the near-side limbs closest to the camera/viewer.
- `back_arm` and `back_leg` are the far-side limbs farther from the camera/viewer.
- `front` does not mean forward/travel direction.
- For right-facing zombies, all parts still face right.
- Far-side limbs should usually be slightly darker, lower contrast, or partially hidden.
- Do not generate mirrored-identical front/back limbs.
- Do not generate a full lower body inside one leg slot.

Layer order:

```text
1. back_arm
2. back_leg
3. front_leg
4. torso
5. head
6. front_arm
7. mutation_overlay
8. effects
```

Anchor points:

```json
{
  "head_neck": { "x": 512, "y": 340 },
  "torso_neck": { "x": 512, "y": 356 },
  "torso_front_shoulder": { "x": 584, "y": 460 },
  "torso_back_shoulder": { "x": 448, "y": 464 },
  "front_arm_shoulder": { "x": 584, "y": 460 },
  "back_arm_shoulder": { "x": 448, "y": 464 },
  "torso_hips": { "x": 512, "y": 650 },
  "front_leg_hip": { "x": 552, "y": 652 },
  "back_leg_hip": { "x": 472, "y": 652 },
  "front_foot_ground": { "x": 564, "y": 860 },
  "back_foot_ground": { "x": 460, "y": 860 }
}
```

Production zombie parts must not include other body slots, baked shadows, floor, background, labels, frames, or text.

Required limb prompt wording:

```text
Right-facing side-view 2D modular zombie part. Front means the near-side limb closest to the camera, back means the far-side limb partly behind the body. Do not mirror front and back limbs exactly. Do not draw isometric, top-down, or left-facing parts.
```

## Asset Save Paths

Save generated project assets inside this repository, not only in temporary or Codex-generated folders.

Use this structure:

```text
assets/
  art-style/
    master/
    references/
  characters/
    zombies/
    enemies/
  environment/
    terrain/
    props/
    rocks_trees/
    structures/
  ui/
    frames/
    icons/
    cards/
  vfx/
  rigs/
```

Use lowercase snake_case file names.

Examples:

```text
assets/art-style/master/master_style_v01.png
assets/characters/zombies/parts/plague_head_01.png
assets/environment/rocks_trees/dead_tree_01.png
assets/ui/icons/bone_scraps_icon_01.png
```

## Prompt Notes

When generating an accepted asset, record the final prompt or short prompt summary near the asset if practical.

Preferred prompt note file:

```text
assets/<category>/PROMPTS.md
```

At minimum, final responses should mention:

- What was generated.
- Where it was saved.
- Whether it is concept, reference, or production.
- Any known cleanup needed.

## Quality Gate

Before marking an asset as accepted:

- Check it matches the art direction.
- Check perspective/camera angle.
- Check it works at gameplay scale.
- Check there is no fake text or watermark.
- Check transparent assets have usable edges.
- For zombie parts, check the rig anchors and slot boundaries.
- For UI, check there is enough plain space for real text.
- For terrain/background, check it does not overpower units.

Reject or regenerate assets that would require heavy repainting.

## Git And Documentation

When asset standards change, update:

- `AGENTS.md`
- `AI_ART_PIPELINE.md`
- `ART_RIG_GUIDE.md` if rig-related
- `CAMERA_AND_PERSPECTIVE.md` if angle-related
- `README.md` if adding a major new reference file

After meaningful accepted changes, commit and push them unless the user says not to.
