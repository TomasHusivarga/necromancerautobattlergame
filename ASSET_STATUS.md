# Asset Status

This file tracks current assets and specs. It should answer: what exists, what is current, and what happens next?

| Asset / Spec | Status | Current Best | Next Action |
|---|---|---|---|
| Approved graphic style | Approved style target | `assets/art-style/references/approved_graphic_big_shape_style_reference.png` | Use in all future visual prompts |
| Lab screen concept | Current reference candidate | `assets/art-style/screen_concepts/lab_builder_inventory_concept_04_pc_style_ref.png` | Convert into `LAB_UI_LAYOUT_SPEC.md` |
| Battle screen concept | Needs simplification | `assets/art-style/screen_concepts/battle_screen_rts_spells_concept_04_pc_style_ref.png` | Generate Battle V5 with fewer figures and simpler terrain |
| Lab zombie rig | Drafted | `assets/rigs/zombie_side_v1.json`, `ART_RIG_GUIDE.md` | Test one full modular lab set |
| Battle zombie rig | Not defined | none | Write `BATTLE_RIG_V1.md` |
| Modular zombie prompt spec | Drafted for lab | `assets/characters/zombies/MODULAR_ZOMBIE_PROMPT_SPEC.md` | Use only for lab/builder parts |
| Battle zombie prompt spec | Drafted for battle | `assets/characters/zombies/BATTLE_ZOMBIE_PROMPT_SPEC.md` | Revise after Battle V5 and battle rig spec |
| Part stat/tag system | Drafted | `PART_STAT_TAG_SYSTEM.md` | Use it to write first part definitions and battle visual mapping |
| UI kit | Not started | V4 screen concepts | Extract panel, button, card, icon style after layout specs |
| Terrain | Not started | Battle V4 as rough direction | Generate simplified high-angle terrain patch after Battle V5 |
| Spells/VFX | Not started | Battle V4 spell bar/effects | Define 5 first spells and icon/VFX requirements |

## Status Labels

- `Approved style target`: use as the visual standard.
- `Current reference candidate`: best current guide, not final production.
- `Needs simplification`: useful direction but must be reduced before locking.
- `Drafted`: written enough to guide tests.
- `Not defined`: needs a spec before production assets.
- `Not started`: no real production asset work yet.
