# Necromancer Autobattler Game

Planning repository for a solo-dev 2D necromancer strategy/autobattler concept.

Open `index.html` or `whiteboard.html` to view the visual project whiteboard.

The GitHub Pages site is the partner-facing project overview. Keep `index.html` and `whiteboard.html` identical when updating the whiteboard.

See `DESIGN_BRIEF.md` for the deeper design notes, mechanics, systems, scope boundaries, asset pipeline, and later multiplayer direction.

Project control files:

- `PROJECT_DECISIONS.md` - locked/current decisions
- `ROADMAP.md` - current work order
- `ASSET_STATUS.md` - asset and spec status tracker
- `PROMPT_LIBRARY.md` - reusable prompt blocks
- `PART_STAT_TAG_SYSTEM.md` - modular part stats, tags, roles, and battle visual mapping

Art/rig sync files:

- `AGENTS.md`
- `GAME_ART_RULES.md`
- `ART_RIG_GUIDE.md`
- `AI_ART_PIPELINE.md`
- `CAMERA_AND_PERSPECTIVE.md`
- `assets/characters/zombies/BATTLE_ZOMBIE_PROMPT_SPEC.md`
- `assets/characters/zombies/MODULAR_ZOMBIE_PROMPT_SPEC.md`
- `assets/rigs/zombie_side_v1.json`
- `assets/rigs/zombie_side_v1_template.svg`

Asset folder rules:

- `assets/README.md` - strict art-only folder rules
- `assets/production/` - approved or near-approved current visual assets
- `assets/work_in_progress/` - generated candidates, raw outputs, edits, prompt iterations, rejected tests, and archive material

Unity coordination notes:

- Current playable battle prototype: `E:\UnityProject\TD Game\Assets\Scenes\BattlePhaseTest1.unity`
- Tom/Codex-created Unity scripts: `E:\UnityProject\TD Game\Assets\_Scripts\Tom_Code`
- Partner/root scripts outside `Tom_Code` should not be edited unless explicitly requested or required for compilation.
- Fix Unity `.meta` tracking before pushing Unity project files.
