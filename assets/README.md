# Asset Folder Rules

This folder is for art, graphics, visual references, generated image assets, UI mockups, rigs, VFX references, environment art, and export-ready asset files.

Do not place gameplay scripts, Unity scenes, prefabs, code modules, logic assets, or partner-owned implementation files here unless the team explicitly changes this rule.

## Current Structure

- `production/` is for approved or near-approved assets that are safe to use as the current project direction.
- `work_in_progress/` is for generated candidates, prompt iterations, raw generations, Photoshop edits, contact sheets, rejected tests, and archived experiments.
- Existing historical folders such as `art-style/`, `characters/`, `images/`, and `rigs/` remain valid references. Do not move those files casually because docs and the whiteboard may link to them.

## Production Use

Use `production/` when an asset has passed a basic readability and direction check:

- It matches the approved graphic gothic big-shape style.
- It uses the correct camera for its purpose.
- It is readable at expected gameplay scale.
- It has no fake readable text, watermark, or unwanted background.
- For modular zombie parts, it follows the lab rig slot rules and anchor expectations.

Use `production/exports_for_unity/` only for files prepared for import into Unity. Keep source candidates and messy working files out of that folder.

## Work In Progress Use

Use `work_in_progress/` for anything that is still being tested:

- `generated_candidates/` for first-pass image generations by category.
- `prompt_iterations/` for experiments that test wording, camera, rig alignment, or style.
- `raw_generations/` for untouched AI outputs.
- `photoshop_edits/` for manual cleanup attempts.
- `contact_sheets/` for comparison sheets.
- `rejected/` for useful failures that should not be treated as current direction.
- `archive/` for old exploratory material that should remain discoverable.

## Naming

- Use lowercase snake_case names.
- Include category and version where useful, for example `plague_head_01.png` or `battle_screen_v05_simplified.png`.
- Record accepted prompts in the nearest relevant `PROMPTS.md` when practical.
