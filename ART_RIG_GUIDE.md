# Zombie Side Rig V1 Art Guide

This is the drawing standard for all modular zombie parts. Do not start producing many parts until this template works in Unity with at least one walk and attack animation.

## Fixed Canvas

- Canvas: `512 x 512 px`
- Background: transparent
- Facing: right
- Camera: side view with slight three-quarter depth
- Body center: `x = 256`
- Ground line: `y = 430`
- Lighting: soft top-left
- Export each body part on the full `512 x 512 px` canvas first

Full-canvas exports are less efficient, but they remove offset problems while the rig is still being proven.

## Slots

Required slots:

- `head`
- `torso`
- `front_arm`
- `back_arm`
- `front_leg`
- `back_leg`

Optional later slots:

- `mutation_overlay`
- `effects`

## Layer Order

Draw and preview parts in this order:

```text
1. back_arm
2. back_leg
3. front_leg
4. torso
5. head
6. front_arm
7. mutation_overlay
8. effects
```

## Anchor Points

Use these coordinates on the `512 x 512 px` canvas:

```json
{
  "head_neck": { "x": 256, "y": 170 },
  "torso_neck": { "x": 256, "y": 178 },
  "torso_front_shoulder": { "x": 292, "y": 230 },
  "torso_back_shoulder": { "x": 224, "y": 232 },
  "front_arm_shoulder": { "x": 292, "y": 230 },
  "back_arm_shoulder": { "x": 224, "y": 232 },
  "torso_hips": { "x": 256, "y": 325 },
  "front_leg_hip": { "x": 276, "y": 326 },
  "back_leg_hip": { "x": 236, "y": 326 },
  "front_foot_ground": { "x": 282, "y": 430 },
  "back_foot_ground": { "x": 230, "y": 430 }
}
```

The exact visual outline can vary, but the attachment points must stay stable.

## Unity Slot Mapping

Recommended Unity hierarchy:

```text
ZombieRig
  VisualRoot
    BackArmSlot
    BackLegSlot
    FrontLegSlot
    TorsoSlot
    HeadSlot
    FrontArmSlot
    MutationOverlaySlot
  Effects
  UI
```

Unity animation should move these slot transforms. The art should be drawn so every replacement sprite still fits the same slot.

## Pivot Rules

If using full-canvas PNGs first, all sprites can sit in matching slot transforms.

If trimming sprites later:

- Head pivot: `head_neck`
- Torso pivot: `torso_hips` or body center, depending on the Unity animation test
- Front arm pivot: `front_arm_shoulder`
- Back arm pivot: `back_arm_shoulder`
- Front leg pivot: `front_leg_hip`
- Back leg pivot: `back_leg_hip`

Do not trim production sprites until the full-canvas version works.

## Drawing Checklist

Before accepting a part:

- It uses the `512 x 512 px` template.
- It faces right.
- It has no background.
- It has no baked shadow.
- It does not include another body slot by accident.
- It touches or overlaps its anchor area cleanly.
- It still works when combined with parts from another family.
- Feet reach the ground line when relevant.
- Shoulder, hip, and neck areas have enough overlap to hide seams.
- The silhouette reads at small battle size.

## First Production Set

Create three families with six required parts each:

```text
plague_head_01
plague_torso_01
plague_front_arm_01
plague_back_arm_01
plague_front_leg_01
plague_back_leg_01

brute_head_01
brute_torso_01
brute_front_arm_01
brute_back_arm_01
brute_front_leg_01
brute_back_leg_01

runner_head_01
runner_torso_01
runner_front_arm_01
runner_back_arm_01
runner_front_leg_01
runner_back_leg_01
```

Total: `18` production parts.

## Important Rule

A part is not finished just because it looks good alone. It is finished only when it works on the rig with unrelated parts from another family.
