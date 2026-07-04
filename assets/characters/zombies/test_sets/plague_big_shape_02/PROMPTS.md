# Plague Big Shape 02 Modular Test

Status: separate-generation rig/style test, not production-approved.

Style reference:

- Uses `assets/art-style/master/master_style_candidate_03_big_shapes.png` as the current preferred visual direction.
- Goal is graphic hand-drawn gothic art with bold silhouettes, large black shadow shapes, limited interior detail, and restrained green plague accents.

Generated files:

```text
raw_chroma/plague_head_02_big_shape_raw.png
raw_chroma/plague_torso_02_big_shape_raw.png
raw_chroma/plague_front_arm_02_big_shape_raw.png
raw_chroma/plague_back_arm_02_big_shape_raw.png
raw_chroma/plague_front_leg_02_big_shape_raw.png
raw_chroma/plague_back_leg_02_big_shape_raw.png

transparent/plague_head_02_big_shape.png
transparent/plague_torso_02_big_shape.png
transparent/plague_front_arm_02_big_shape.png
transparent/plague_back_arm_02_big_shape.png
transparent/plague_front_leg_02_big_shape.png
transparent/plague_back_leg_02_big_shape.png

plague_big_shape_02_contact_sheet.png
plague_big_shape_02_rough_assembly_preview.png
```

Assessment:

- The art style is much closer to the intended direction than earlier zombie tests.
- The six parts mostly stay in the same visual family despite being generated separately.
- The assembled rough preview gives a readable zombie silhouette.
- These files are not production-ready because the image generator did not keep exact `1024 x 1024 px` source canvases.
- Anchor positions are approximate, not validated.
- The torso includes large shoulder hardware, which may limit arm swapping.
- The head and torso are stronger than the legs for the big-shape target.
- This test supports the rule that each modular limb should be generated separately before trusting the workflow.

Base prompt pattern:

```text
Use case: game-assets
Asset type: modular zombie part, <slot> only, rig test concept
Primary request: Generate plague_<slot>_02_big_shape as one separate modular zombie <slot> asset for a Unity paper-doll rig.
Canvas and background: square 1024x1024 composition on a perfectly flat solid #ff00ff chroma-key background for background removal. The background must be one uniform color with no shadows, gradients, texture, floor plane, or lighting variation. Do not use #ff00ff anywhere in the subject.
Subject: ONLY the requested slot. No other body parts, no frame, no labels. Right-facing side view with slight three-quarter depth. Place the attachment overlap near the canonical rig coordinate.
Style/medium: match master_style_candidate_03_big_shapes: graphic hand-drawn gothic 2D game art, bold black ink outline, poster-like large shapes, large flat shadow blocks, angular comic-ink shadows, limited interior detail, clear game-sprite readability, not painterly, not fully rendered.
Detail rules: 70 percent large clean silhouette and shadow, 20 percent secondary material shapes, 10 percent small accents. No evenly distributed scratches, no stitches everywhere, no texture noise.
Constraints: no readable text, no watermark, no extra body parts, no full zombie, no floor shadow, no isometric view, no top-down view, no left-facing part, no excessive gore.
```

Next iteration:

- Try a stricter production-template prompt that says the output must be centered on a `1024 x 1024` full-canvas Unity sprite sheet coordinate system.
- Consider generating on a visible rig template or mannequin guide first, then using Photoshop/manual cleanup.
- Reduce torso shoulder hardware or separate shoulder caps into arm overlap instead.
- Make front/back legs simpler and more clearly compatible with a walk cycle.
