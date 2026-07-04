# Master Style Reference Prompts

## master_style_candidate_01.png

Status: superseded iteration test, not current target.

Iteration note:

- Useful for first hand-drawn gothic direction.
- Too illustration-heavy and too busy for the current readability target.
- Do not use as the main reference for production assets.

Use:

- Evaluate the hand-drawn gothic direction.
- Judge whether the project should move away from smoother painterly rendering.
- Reference for future zombie, environment, UI, prop, structure, and VFX tests if approved.

Prompt:

```text
Use case: game-assets
Asset type: master style reference image for a Unity 2D game art pipeline
Primary request: Create a master visual style template for a necromancer autobattler game, inspired by hand-drawn gothic dark fantasy with bold ink outlines and sharp shadow shapes, but not copying any existing game style.
Scene/backdrop: a side-scrolling 2.5D horizontal lane scene that shows the whole game identity in one image: necromancer lab side on the left, automatic battlefield lane in the middle, guarded village/graveyard enemy side on the right.
Subject: one modular stitched plague zombie in right-facing side view near the center-left, a necromancer workbench/lab silhouette behind it, enemy militia silhouettes on the right, dark terrain strip, dead trees, rocks, grave markers, wooden barricade, small UI frame samples along the bottom edge.
Style/medium: hand-drawn gothic 2D game art, bold black ink outlines, angular silhouettes, sharp blocky shadows, limited painterly texture, readable game asset shapes, not photorealistic.
Composition/framing: wide landscape concept board, clear horizontal lane readability, characters mostly side-view with slight three-quarter depth, visible top surfaces only subtly, not isometric, not top-down.
Lighting/mood: high contrast, moody candle and moon lighting, controlled necromantic green glow from zombie/lab, warm torch orange on enemy village side.
Color palette: black ink shadows, desaturated bone, rotted green-grey flesh, dark iron, old wood, grave soil, muted blood red, brass UI accents, small bright necromantic green highlights.
Materials/textures: stitched flesh, surgical clamps, bone pins, green glass reagent bottles, worn metal straps, cracked stone, dead wood, parchment UI panels.
Constraints: no readable text, no logos, no watermark, no exact Darkest Dungeon copy, no photorealism, no isometric view, no top-down view, no excessive gore, no clutter that hides silhouettes.
Purpose: this is the master art direction reference that future AI-generated zombies, UI, rocks, trees, props, structures, terrain, and VFX should match.
```

## master_style_candidate_02_readability.png

Status: superseded iteration test, not current target.

Iteration note:

- Improved lane readability compared with candidate 01.
- Still too much scene/detail density for the desired big-shape direction.
- Do not use as the main reference for production assets.

Use:

- Compare against `master_style_candidate_01.png`.
- Evaluate readability-first hand-drawn gothic direction.
- Check whether larger silhouettes, lower-detail backgrounds, and cleaner UI samples work better for the game.

Prompt:

```text
Use case: game-assets
Asset type: master style reference candidate for a Unity 2D side-scrolling autobattler
Primary request: Create a new readable master visual style template for a necromancer autobattler game. Prioritize gameplay readability over illustration detail.
Scene/backdrop: side-scrolling 2.5D horizontal lane scene with three clear zones: necromancer lab/base on the far left, clean open combat lane in the center, guarded village gate on the far right. Background should be dark and low-detail behind units.
Subject: one large stitched plague zombie on the left-center facing right, three readable human enemy silhouettes on the right facing left, a few simple props only: dead tree silhouette, rocks, grave marker, wooden barricade, green reagent vat. Include a small bottom strip showing clean UI frame samples and 5 simple icons, with no readable text.
Style/medium: hand-drawn gothic 2D game art, bold black ink outlines, strong readable silhouettes, angular shadow shapes, limited texture, controlled highlights, slightly stylized proportions, not photorealistic.
Composition/framing: wide landscape concept board. Characters must be larger and clearer than background. Keep the center lane open and uncluttered. Use strong value grouping: characters high contrast, background low contrast, UI clean and separated.
Camera/angle: side-scrolling 2.5D game art, right-facing side view with slight three-quarter depth, clear horizontal lane readability, visible top surfaces only subtly, not isometric, not top-down.
Gameplay readability rules: silhouette first, value contrast second, gameplay role third. Zombie head, torso, arms, and legs must read separately. Enemy units must have clear weapon roles. Background must not compete with units. No tiny decorative noise behind characters.
Color palette: black ink shadows, desaturated bone, rotted green-grey flesh, dark iron, old wood, grave soil, muted blood red, small bright necromantic green highlights, enemy torch orange accents. Avoid pure monochrome green.
Materials/textures: stitched flesh, surgical clamps, bone pins, green reagent glass, worn metal straps, cracked stone, dead wood, parchment and brass UI panels.
UI samples: clean gothic UI frames with plain empty interiors for real Unity text, simple readable icons, not ornate clutter.
Constraints: no readable text, no logos, no watermark, no exact Darkest Dungeon copy, no photorealism, no isometric view, no top-down view, no excessive gore, no clutter, no dense texture behind units, no fake labels.
Purpose: candidate master art direction reference for future AI-generated zombies, UI, rocks, trees, props, structures, terrain, and VFX.
```

## master_style_candidate_03_big_shapes.png

Status: current strongest master-shape candidate, still not locked.

Use:

- Evaluate the stricter big-shape direction.
- Use as a better reference for bold silhouettes, large shadow blocks, restrained detail, gothic UI framing, and readable structures.
- Do not treat the zombie as production-ready modular rig art; it is a style/shape reference only.

Assessment:

- Better than candidates 01 and 02 for large readable forms.
- Good direction for UI frames and structure silhouette.
- Zombie is readable, but still a single full-body illustration rather than a properly separated rig template.
- For future zombie parts, keep this shape language but enforce the 1024 canvas, anchors, separated limbs, and transparent per-slot exports.

Prompt:

```text
Use case: game-assets
Asset type: master style reference candidate for a Unity 2D side-scrolling necromancer autobattler
Primary request: Create master_style_candidate_03_big_shapes, a stricter big-shape art direction template. This is NOT polished concept art; it is a readable game-art shape guide.
Scene/backdrop: A simple side-scrolling 2.5D horizontal lane presentation with minimal background. Show only four large readable examples: one stitched zombie unit facing right, one human militia enemy facing left, one necromancer lab structure block, and one gothic UI frame/icon sample strip. Keep empty space between examples.
Subject: Large bold silhouettes and major shape groups only. Zombie has separate readable head, torso, near-side arm, far-side arm, near-side leg, far-side leg. Enemy has one clear weapon silhouette. Lab structure is a large readable facade shape with subtle top plane. UI samples have plain empty interiors for real Unity text.
Style/medium: graphic hand-drawn gothic 2D game art, bold black ink outline, poster-like screenprint shape design, large flat shadow blocks, angular comic-ink shadows, limited interior detail, clear game-sprite readability, not painterly, not fully rendered.
Composition/framing: Wide landscape style sheet, not a cinematic illustration. Big objects, lots of negative space, clean lane readability. Side-scrolling 2.5D game art, right-facing side view with slight three-quarter depth, visible top surfaces only subtly, not isometric, not top-down, not photorealistic.
Lighting/mood: high-contrast dark fantasy with hard shadow shapes. Use light only to separate silhouettes, not to render texture.
Color palette: black ink shadows, desaturated bone, rotted grey-green flesh, dark iron, dead wood, grave soil, muted blood red, one controlled necromantic green accent, small warm torch orange accent on enemy side.
Detail rules: 70 percent large clean silhouette and shadow, 20 percent secondary material shapes, 10 percent small accents. Small accents only at the zombie face, attack hand, enemy weapon, lab reagent glow, and UI icon. Leave large quiet areas with no scratches or texture.
Constraints: no readable text, no logos, no watermark, no exact Darkest Dungeon copy, no photorealism, no isometric view, no top-down view, no excessive gore, no busy background, no tiny repeated scratches, no surface noise, no stitches everywhere, no straps everywhere, no fully rendered concept-art detail, no clutter, no fake labels.
Purpose: candidate master art direction reference for future AI-generated zombies, UI, rocks, trees, props, structures, terrain, and VFX. The goal is stronger readability and bigger graphic shapes than previous candidates.
```
