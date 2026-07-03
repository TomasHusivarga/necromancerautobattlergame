# Camera And Perspective Standard

The game should use a side-scrolling 2.5D presentation, not isometric.

## Decision

Use a fixed side-view lane camera with slight vertical visibility for ground and props.

Recommended game camera:

```text
Camera type: Orthographic
Gameplay view: side-scrolling 2.5D lane
Camera yaw: 0 degrees
Camera pitch: 0 degrees for pure 2D camera, with artwork faking slight top visibility
Art perspective: side view with slight three-quarter depth
Visible ground/top surfaces: about 10-20%
Unit facing: right for player zombies, mirrored left for enemies
Lane direction: left to right
Near-side limbs: called front_arm/front_leg
Far-side limbs: called back_arm/back_leg
```

This means the Unity camera can stay simple and orthographic. The 2.5D look comes from layered background, ground strips, prop placement, parallax, shadows, and artwork showing a small amount of top surface.

## Why Not Isometric

Isometric is good for tactical maps and free movement, but this game is about automatic horizontal lane fights. Isometric would make modular zombie parts harder because every limb would need more perspective consistency, and combat readability would become harder at small size.

For this project, side-view 2.5D gives:

- Clear left-to-right combat.
- Easier modular body rigging.
- Easier walk and attack animation.
- Stronger unit silhouettes.
- Easier UI/battle readability.
- Less asset production risk.

## Art Angle

Use this art rule:

```text
Characters: mostly side view, slight three-quarter depth
Ground: visible top plane, shallow angle
Props: side-view readable, slight visible top when useful
Structures: side-facing facade with small visible roof/top plane
UI icons: front/three-quarter view as needed for clarity
```

Do not draw zombies as full isometric units. They should read like side-view combat units.

## Character Limb Depth

For characters, `front` and `back` describe camera depth, not travel direction.

```text
front_arm/front_leg = near-side limb, closer to camera/viewer
back_arm/back_leg = far-side limb, farther from camera/viewer
```

The near-side limb should usually have stronger contrast and clearer shape. The far-side limb should sit behind the body and can be slightly darker, less detailed, or partially occluded.

This matters for AI prompts. Do not ask for generic "left arm" or "right leg" unless the body-side meaning is explicitly needed. Prefer `near-side/front_arm`, `far-side/back_arm`, `near-side/front_leg`, and `far-side/back_leg`.

## Practical Visual Ratio

For gameplay art:

```text
Front/side silhouette importance: 80-90%
Top-surface visibility: 10-20%
```

This gives enough depth for a 2.5D look without making modular alignment painful.

## Unity Setup

Recommended first Unity setup:

```text
Camera Projection: Orthographic
Camera Rotation: 0, 0, 0
Sorting: SpriteRenderer sorting layers / order in layer
Depth: created through sorting layers, parallax backgrounds, shadows, and scale
```

Possible sorting layers:

```text
BackgroundFar
BackgroundNear
Ground
UnitsBack
Units
UnitsFront
VFX
UI
```

Keep the camera fixed during combat for MVP. Add small smooth camera movement only after battles are readable.

## Asset Prompt Wording

Use this wording in AI prompts:

```text
Side-scrolling 2.5D game art, right-facing side view with slight three-quarter depth, clear horizontal lane readability, visible top surfaces only subtly, not isometric, not top-down, not photorealistic.
```

For characters:

```text
Right-facing side-view 2D game sprite with slight three-quarter depth, strong silhouette, feet aligned to the ground line, modular paper-doll proportions, not isometric.
```

For modular zombie limbs:

```text
Right-facing side-view 2D modular zombie part. Front means the near-side limb closest to the camera, back means the far-side limb partly behind the body. Do not mirror front and back limbs exactly. Do not draw isometric, top-down, or left-facing parts.
```

For structures:

```text
Side-view 2.5D structure for a horizontal lane battle, facade facing camera with a small visible roof/top plane, readable silhouette, not isometric.
```

For terrain:

```text
Horizontal side-scrolling lane ground strip with slight visible top plane, dark fantasy painterly style, low contrast behind units, not top-down and not isometric.
```

## What To Test First

Before generating many assets, test three perspective samples:

1. One zombie on the rig template.
2. One enemy militia sprite.
3. One lane background strip with rocks/tree/structure.

Put them together in Unity at gameplay zoom. If they feel like the same world and the zombie reads clearly, lock the angle.

## Rejection Rules

Reject generated assets if:

- They look isometric.
- They look top-down.
- They face the wrong direction.
- The feet do not sit on the ground line.
- The top surface is too visible.
- The sprite loses silhouette clarity.
- The asset would require repainting to match the lane camera.
