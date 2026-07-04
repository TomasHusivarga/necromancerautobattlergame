# Agent Instructions

These instructions apply to all work in this repository. Speak English.

## Before Generating Any Image Or Asset

Read these files first:

1. `AI_ART_PIPELINE.md`
2. `CAMERA_AND_PERSPECTIVE.md`
3. `ART_RIG_GUIDE.md`
4. `GAME_ART_RULES.md`
5. `assets/characters/zombies/MODULAR_ZOMBIE_PROMPT_SPEC.md` when generating zombie parts
6. `assets/characters/zombies/BATTLE_ZOMBIE_PROMPT_SPEC.md` when generating battle zombie sprites
7. `assets/rigs/zombie_side_v1.json` when generating lab zombie parts

Do not generate production assets from a standalone prompt without checking these files.

Game art must be readable in Unity at gameplay scale. Treat silhouette, value contrast, camera angle, and gameplay role as more important than surface detail.

Big shape rule: generate graphic game art, not busy concept art. Assets should read as big silhouette, large shadow blocks, a few material accents, and only limited detail clusters. Avoid evenly distributed scratches, cracks, straps, pores, and texture noise.

Screen concepts must be clean production readability mockups, not dense finished illustrations. For lab screens, show one main zombie preview, one inventory panel, one stats/details panel, and one bottom action/resource strip. For battle screens, show 3-5 squad groups per side, 2-3 spell effects, broad terrain patches, and one bottom spell bar. Avoid dozens of tiny icons, repeated unit clusters, ornate borders on every panel, and texture everywhere.

## Core Art Direction

The game uses:

- Dark fantasy 2D game art.
- Two camera standards: side-view art for the lab/zombie builder, and old-RTS high-angle orthographic art for actual battles.
- Lab characters are mostly side-view with slight three-quarter depth.
- Battle units are small high-angle RTS sprites designed for many squads on screen.
- Orthographic Unity camera.
- Clear battlefield readability at squad scale.
- Graphic hand-drawn gothic style with bold ink outlines and large shadow blocks, not photorealism.
- Green necromantic accents, bone, dark iron, dark wood, grave soil, muted blood, candlelight.

Avoid:

- Using side-scrolling/lane camera prompts for battle assets.
- Using RTS high-angle prompts for modular lab body parts.
- Pure top-down camera with no readable vertical form.
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

Use the correct camera for the asset's actual screen.

For lab modular zombie parts:

```text
Right-facing side-view 2D modular zombie paper-doll part for a corpse-building screen, slight three-quarter depth, full-canvas sprite, no visible sockets, limbs overlap and cover joints, not RTS battle scale.
```

For battle units:

```text
Old-RTS high-angle orthographic unit sprite for a dark fantasy autobattler, viewed from above at a fixed battlefield angle, small squad-scale readability, visible head/shoulders/back and ground contact, clear silhouette at tiny size, not side-scrolling, not front-facing portrait, not fighting-game profile.
```

For battle structures:

```text
Old-RTS high-angle orthographic structure, visible roof/top surfaces and front/side faces, readable silhouette at gameplay zoom, dark fantasy material language, not side-view facade.
```

For battle terrain:

```text
Old-RTS high-angle orthographic terrain tile or ground patch, visible top plane, muted contrast behind units, readable dirt/stone/graveyard material, tileable or blendable, not side-scrolling background.
```

## Zombie Part Rig Rules

All modular zombie parts for the lab/builder preview must follow `zombie_side_v1`. This rig is for corpse construction and inspection, not necessarily the final battlefield unit sprite.

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

For modular zombie tests, generate each slot as its own separate image before trusting a full-body sheet. Separate generation is required to expose style drift, anchor drift, wrong limb direction, accidental extra body parts, and poor overlap areas. Treat these as rig tests until assembled successfully.

Required limb prompt wording:

```text
Right-facing side-view 2D modular zombie part for the lab builder. Front means the near-side limb closest to the camera, back means the far-side limb partly behind the body. Do not mirror front and back limbs exactly. Do not draw RTS high-angle, top-down, or left-facing parts for this rig.
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
- Check silhouette readability.
- Check value contrast.
- Check gameplay role readability.
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

Do not commit, push, upload, or publish changes unless the user explicitly asks for that specific Git action.
