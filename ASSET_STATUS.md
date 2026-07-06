# Asset Status

This file tracks current assets and specs. It should answer: what exists, what is current, and what happens next?

Current folder rule: approved or near-approved visual assets should be saved or copied into `assets/production/`. Experiments, raw generations, Photoshop edits, prompt iterations, and rejected tests should stay in `assets/work_in_progress/` or in the existing historical folders when already linked by docs or the whiteboard.

| Asset / Spec | Status | Current Best | Next Action |
|---|---|---|---|
| Approved graphic style | Approved style target | `assets/art-style/references/approved_graphic_big_shape_style_reference.png` | Use in all future visual prompts |
| Lab screen concept | Current reference candidate | `assets/art-style/screen_concepts/lab_builder_inventory_concept_04_pc_style_ref.png` | Convert into `LAB_UI_LAYOUT_SPEC.md` |
| Battle runtime prototype | Playable prototype | `E:\UnityProject\TD Game\Assets\Scenes\BattlePhaseTest1.unity` | Add health bars, hit feedback, and data-driven stats |
| Battle screen concept | Reference only | `assets/art-style/screen_concepts/battle_screen_rts_spells_concept_04_pc_style_ref.png` | Use only as visual reference; runtime prototype is now primary |
| Lab zombie rig | Drafted | `assets/rigs/zombie_side_v1.json`, `ART_RIG_GUIDE.md` | Test one full modular lab set |
| Battle zombie rig | Not defined | none | Write `BATTLE_RIG_V1.md` |
| Modular zombie prompt spec | Drafted for lab | `assets/characters/zombies/MODULAR_ZOMBIE_PROMPT_SPEC.md` | Use only for lab/builder parts |
| Battle zombie prompt spec | Drafted for battle | `assets/characters/zombies/BATTLE_ZOMBIE_PROMPT_SPEC.md` | Revise after battle rig spec and runtime scale tests |
| Part stat/tag system | Drafted | `PART_STAT_TAG_SYSTEM.md` | Use it to write first part definitions and battle visual mapping |
| UI kit | Not started | V4 screen concepts | Extract panel, button, card, icon style after layout specs |
| Terrain | Prototype imported in Unity | `E:\UnityProject\TD Game\Assets\_Project\Art\Environment\Battle\` | Improve readability/resolution after gameplay behavior is stable |
| Spells/VFX | Not started | Battle V4 spell bar/effects | Define 5 first spells and icon/VFX requirements |
| Code ownership rule | Active | `E:\UnityProject\TD Game\Assets\_Scripts\Tom_Code\README.md` | Keep Codex/Tom code under `Tom_Code` |

## Status Labels

- `Approved style target`: use as the visual standard.
- `Current reference candidate`: best current guide, not final production.
- `Needs simplification`: useful direction but must be reduced before locking.
- `Playable prototype`: implemented in Unity and usable for runtime testing.
- `Reference only`: useful visual history, not the current implementation target.
- `Drafted`: written enough to guide tests.
- `Not defined`: needs a spec before production assets.
- `Not started`: no real production asset work yet.
