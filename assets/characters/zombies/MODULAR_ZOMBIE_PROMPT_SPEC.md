# Modular Zombie Prompt Spec

Use this file when generating modular zombie art for the lab, corpse-builder screen, large unit preview, and inspection UI. The goal is not only good-looking art. The goal is art that can be swapped on the Unity paper-doll rig without repainting.

Actual battles use a separate old-RTS high-angle camera. Do not use this side-view modular prompt spec for small battlefield sprites.

## Current Style Target

Use `assets/art-style/master/master_style_candidate_03_big_shapes.png` as the current preferred style reference.

Style summary:

```text
Graphic hand-drawn gothic 2D game art, bold black ink outline, large readable silhouettes, large flat shadow blocks, restrained interior detail, dark bone/rotted flesh/iron palette, controlled necromantic green accents, not painterly, not photorealistic, not noisy.
```

## Production Image Contract

Every modular zombie part must obey this contract:

- One file contains one body slot only.
- Canvas target: `1024 x 1024 px`.
- Full-canvas export first, not trimmed.
- Facing: right.
- Camera: side view with slight three-quarter depth for the lab/builder preview.
- Background: transparent for final assets.
- For AI generation tests, use a flat chroma-key background and remove it locally.
- No floor shadow, contact shadow, labels, frame, guide text, watermark, or background props.
- No extra body slots.
- No baked lower body in torso.
- No torso piece attached to arm.
- No pelvis attached to leg, except a small overlap tab needed to hide the hip seam.
- No mirrored-identical front/back limbs.

If any of these fail, the image is a reject or cleanup candidate, not production art.

## Anchor Contract

Use these anchor targets on the `1024 x 1024 px` canvas:

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

The image model may not place pixels exactly. The prompt must still state exact anchor intent so manual cleanup has a clear target.

## Universal Prompt Block

Use this block in every modular zombie part prompt:

```text
Use case: game-assets
Asset type: Unity 2D modular zombie paper-doll part
Output contract: one body slot only, centered on a 1024x1024 Unity full-canvas sprite coordinate system, right-facing side view with slight three-quarter depth for the lab builder, no other body slots.
Canvas/background: create the part on a perfectly flat solid #ff00ff chroma-key background for background removal. The background must be one uniform color with no shadows, gradients, texture, floor plane, or lighting variation. Do not use #ff00ff anywhere in the subject.
Style reference: match master_style_candidate_03_big_shapes. Graphic hand-drawn gothic 2D game art, bold black ink outline, large readable silhouette, large flat shadow blocks, angular comic-ink shadows, restrained detail, dark bone/rotted flesh/iron palette, controlled necromantic green accents, not painterly, not fully rendered.
Detail rule: 70 percent large clean silhouette and shadow, 20 percent secondary material shapes, 10 percent small accents. Keep quiet empty areas. No evenly distributed scratches, no texture noise, no stitches everywhere, no straps everywhere.
Camera: right-facing side-view 2D modular zombie paper-doll art for a corpse-building screen, slight three-quarter depth, visible top surfaces only subtly, not old-RTS battle scale, not top-down, not photorealistic.
Reject conditions: no readable text, no watermark, no labels, no frame, no full zombie, no extra body parts, no floor shadow, no cast shadow, no old-RTS high-angle battle sprite, no top-down view, no left-facing part, no excessive gore.
```

## Slot Prompts

### Head

```text
Slot: head only.
Subject: ONLY the zombie head and a short neck overlap stump. No torso, no shoulders, no arms, no legs.
Anchor: neck overlap centered near x=512 y=340 on the 1024 canvas.
Shape goal: large readable skull/face silhouette, clear jaw, clear dark eye hollow, one controlled green plague glow accent.
Overlap rule: leave enough neck stump below the head to hide the torso seam.
```

### Torso

```text
Slot: torso only.
Subject: ONLY torso from neck overlap to hip overlap. No head, no arms, no hands, no legs, no pelvis below hip overlap.
Anchors: neck overlap near x=512 y=356, front shoulder covered-joint area near x=584 y=460, back shoulder covered-joint area near x=448 y=464, hip overlap near x=512 y=650.
Shape goal: one large readable ribcage/chest mass with plain shoulder stumps/overlap tabs and a simple lower hip overlap.
Overlap rule: shoulders are not visible sockets. Separate arm sprites cover the shoulder joint areas in Unity, so the torso only needs plain torn-flesh overlap stumps that can hide under limbs.
Perspective rule: the torso must read as a right-facing side-view mass with slight three-quarter depth. Do not show both shoulder attachment areas equally. The far-side/back shoulder should be mostly hidden by torso silhouette and shadow.
Avoid: visible arm sockets, circular holes, shoulder tunnels, black openings, mechanical slots, attached arms, attached shoulder pads, symmetrical shoulder details, huge side hardware that makes every arm need matching geometry.
```

### Front Arm

```text
Slot: front_arm only.
Meaning: near-side arm closest to the camera, drawn above torso in the final layer order.
Subject: ONLY one arm from shoulder overlap to hand/claw. No torso, no shoulder pad from torso, no second arm.
Anchor: shoulder overlap near x=584 y=460.
Shape goal: readable attack silhouette, extended forward/right claw pose, strongest contrast of the two arms.
Overlap rule: upper arm must have enough shoulder mass to cover the torso joint area while rotating.
Avoid: full chest fragments, loose floating shoulder armor, mirrored back-arm pose.
```

### Back Arm

```text
Slot: back_arm only.
Meaning: far-side arm farther from camera, drawn behind torso in the final layer order.
Subject: ONLY one darker support arm from shoulder overlap to hand/claw. No torso, no second arm.
Anchor: shoulder overlap near x=448 y=464.
Shape goal: simpler lower-contrast support silhouette, not identical to front arm.
Overlap rule: upper arm must tuck behind torso and still be visible at lab preview and part-card size.
Avoid: strong green glow, same pose as front arm, arm shape that disappears behind torso completely.
```

### Front Leg

```text
Slot: front_leg only.
Meaning: near-side leg closest to camera, drawn in front of the back leg.
Subject: ONLY one leg from hip overlap to foot. No pelvis, no second leg, no torso.
Anchors: hip overlap near x=552 y=652, foot contact near x=564 y=860.
Shape goal: readable stride leg with clear knee and broad foot shape for walk animation.
Overlap rule: small upper-thigh/hip overlap tab is allowed to hide the seam.
Avoid: attached skirt/pelvis, fused second leg, thin unreadable foot, too much cloth covering the knee.
```

### Back Leg

```text
Slot: back_leg only.
Meaning: far-side leg farther from camera, drawn behind front leg and torso.
Subject: ONLY one darker support leg from hip overlap to foot. No pelvis, no second leg, no torso.
Anchors: hip overlap near x=472 y=652, foot contact near x=460 y=860.
Shape goal: simpler lower-contrast support leg, different silhouette from front leg, clear planted foot.
Overlap rule: small upper-thigh/hip overlap tab is allowed to hide the seam.
Avoid: same pose as front leg, attached pelvis, fused second leg, foot that cannot plant on the ground line.
```

## Test Order

Generate in this order:

1. Torso.
2. Head.
3. Front leg.
4. Back leg.
5. Front arm.
6. Back arm.

Reason: torso defines the body mass and covered joint areas. Legs prove ground/hip placement. Arms are easiest to adjust after the torso overlap shape is known.

## Prompt Iteration Rules

Change one constraint at a time.

Track each attempt with:

- Slot.
- Prompt version.
- What improved.
- What failed.
- Whether it is accepted, cleanup candidate, or rejected.

Common failures and fixes:

```text
Failure: image includes multiple body parts.
Fix: move "ONLY this slot" to the first subject sentence and repeat "no other body slots" in reject conditions.

Failure: torso includes arm/shoulder armor.
Fix: ask for "plain shoulder stumps/overlap tabs only, no shoulder caps, no arm fragments."

Failure: torso shows visible arm sockets or shoulder holes.
Fix: ask for "no visible arm sockets, no shoulder holes, no black shoulder tunnels, arms will cover the plain shoulder stumps in Unity."

Failure: limb has no useful pivot overlap.
Fix: ask for "large plain overlap tab at the shoulder/hip, designed to cover the joint area during animation."

Failure: part is too detailed/noisy.
Fix: ask for "poster-like shape design, quiet empty areas, no surface texture."

Failure: canvas is not exact or part is cropped.
Fix: treat as concept only; use local padding/canvas correction or regenerate with stronger "full-canvas Unity sprite coordinate system" wording.
```

## Acceptance Levels

Use these labels:

```text
accepted_style_reference
cleanup_candidate
rig_test_candidate
production_candidate
rejected
```

Do not label a part `production_candidate` until it has been assembled on the rig.

Production for this file means production-ready for the lab/builder rig. Battle production candidates need their own high-angle RTS prompt spec.
