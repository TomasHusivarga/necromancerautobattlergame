# Zombie Test Set Prompts

## plague_zombie_modular_test_sheet_01.png

Status: concept/reference only, not production-ready.

Use:

- Style exploration.
- Limb separation test.
- Visual target for future plague zombie parts.

Known issues:

- Not transparent full-canvas production parts.
- Generated as a reference sheet, not six individual `1024 x 1024` slot exports.
- Needs stricter follow-up prompts or manual separation before Unity use.
- Must be checked against `zombie_side_v1_template.svg` before becoming production art.

Prompt:

```text
Use case: game-assets
Asset type: concept reference sheet for modular zombie parts
Primary request: Create one coherent modular zombie art test sheet showing exactly six separate body parts for one plague zombie: head, torso, front_arm, back_arm, front_leg, back_leg.
Scene/backdrop: simple dark neutral preview background, no environment, no labels, no text.
Subject: six separated modular zombie body parts arranged cleanly in a grid, all from the same plague zombie design, designed to fit a 1024x1024 side-view paper-doll rig.
Style/medium: dark fantasy 2D game art, painterly hand-painted, readable side-scrolling 2.5D style, not photorealistic.
Composition/framing: landscape reference sheet, each part isolated with generous spacing; parts face right and match the same body proportions.
Camera/angle: right-facing side view with slight three-quarter depth, clear horizontal lane readability, visible top surfaces only subtly, not isometric, not top-down.
Rig constraints: canonical full art canvas is 1024x1024, body center x=512, ground y=860. The generated sheet is a concept sheet, but the parts must visually follow these anchors: head neck near center, torso shoulders and hips consistent, front_arm and front_leg are near-side limbs closest to camera, back_arm and back_leg are far-side limbs partly behind body.
Limb convention: front means near-side limb closest to the camera; back means far-side limb partly behind the body. Do not mirror front and back limbs exactly. Do not draw isometric, top-down, or left-facing parts.
Visual design: plague zombie, stitched pale green-grey flesh, exposed seams, bone/iron straps, sickly green necromantic glow in small accents, strong silhouette, moderate detail suitable for Unity 2D gameplay.
Constraints: no readable text, no labels, no watermark, no background scene, no floor shadow, no full assembled zombie, no extra body parts, no fused legs, no full lower body inside one leg slot, no excessive gore.
```
