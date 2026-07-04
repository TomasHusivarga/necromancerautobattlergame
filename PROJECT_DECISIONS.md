# Project Decisions

This file records locked or current project decisions. Keep it short. Detailed reasoning belongs in the design docs and prompt history.

## Current Direction

- Game concept: solo-dev 2D necromancer strategy/autobattler.
- Core loop: build zombies in the lab, send the designs into automatic RTS-style squad battles, learn from results, improve designs.
- Lab view: side-view modular zombie builder for corpse engineering and inspection.
- Battle view: old-RTS high-angle orthographic squad battlefield for actual combat.
- Target platform: PC screen first.

## Art Direction

- Approved style target: `assets/art-style/references/approved_graphic_big_shape_style_reference.png`.
- Style traits: thick black ink outlines, hard angular silhouettes, large flat shadow blocks, limited palette, low rendering, low texture, quiet empty areas.
- Avoid: painterly rendering, realistic texture, dense gothic decoration, tiny repeated detail, fake readable text.

## Current Best References

| Area | Current Best | Status |
|---|---|---|
| Lab screen | `assets/art-style/screen_concepts/lab_builder_inventory_concept_04_pc_style_ref.png` | Current reference candidate |
| Battle screen | `assets/art-style/screen_concepts/battle_screen_rts_spells_concept_04_pc_style_ref.png` | Needs V5 simplification |
| Style reference | `assets/art-style/references/approved_graphic_big_shape_style_reference.png` | Approved style target |

## Production Rules

- The lab zombie rig and the battle unit sprites are separate visual systems.
- Lab art can show detailed modular body parts.
- Battle art should simplify the built design into readable squad-scale silhouettes.
- Battle V4 is not final. The next battle concept should reduce individual figures, terrain marks, and small detail.
- Do not commit, push, upload, or publish to GitHub unless explicitly asked.

