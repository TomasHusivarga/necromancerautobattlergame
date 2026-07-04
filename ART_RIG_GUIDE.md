# Zombie Side Rig V1 Art Guide

This is the drawing standard for modular zombie parts used in the lab, corpse-builder screen, large unit preview, and inspection UI. Do not treat this as the battle sprite standard. Actual battles use a separate old-RTS high-angle camera.

## Fixed Canvas

- Canvas: `1024 x 1024 px`
- Background: transparent
- Facing: right
- Camera: side view with slight three-quarter depth
- Body center: `x = 512`
- Ground line: `y = 860`
- Lighting: soft top-left
- Export each body part on the full `1024 x 1024 px` canvas first

Full-canvas exports are less efficient, but they remove offset problems while the rig is still being proven.

This side-view rig is valuable because the player needs to inspect body construction clearly. The battlefield can use simplified high-angle sprites derived from the zombie's role/family instead of showing every modular part.

## Slots

Required slots:

- `head`
- `torso`
- `front_arm`
- `back_arm`
- `front_leg`
- `back_leg`

## Front And Back Limb Convention

The zombie faces right. The viewer sees the zombie from a side view with slight three-quarter depth.

Use this convention for every character part:

- `front_arm`: the near-side arm, closest to the camera/viewer. It appears on top of the torso and usually has the clearest silhouette.
- `back_arm`: the far-side arm, farther from the camera/viewer. It sits behind the torso and should be slightly darker, less detailed, or partially hidden.
- `front_leg`: the near-side leg, closest to the camera/viewer. It appears in front of the torso/hip mass and should be the most readable leg.
- `back_leg`: the far-side leg, farther from the camera/viewer. It sits behind the front leg and torso/hip mass and should be slightly darker, less detailed, or partially hidden.

Do not interpret `front` as "toward the direction of travel." In this rig, `front` means camera-near. Since the zombie faces right, both arms and both legs still belong to the same right-facing body.

Depth treatment:

- Near-side limbs: full contrast, clearer edges, more visible details.
- Far-side limbs: 10-20% darker or lower contrast, partly occluded by torso/near limb where appropriate.
- Do not mirror front and back limbs exactly. They need different silhouettes so the walk cycle reads.
- Do not draw left-facing limbs for right-facing zombies.
- Do not draw both legs fused together.
- Do not draw a whole lower body inside one leg slot.

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

Use these coordinates on the `1024 x 1024 px` canvas:

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

The exact visual outline can vary, but the attachment points must stay stable.

These coordinates are pivot/overlap targets, not visible socket designs. Do not draw circular shoulder holes, black tunnels, or mechanical slots into the torso. Arm sprites cover the shoulder joint areas in Unity, so torso art should use plain shoulder stumps or quiet overlap shapes.

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

## Angle Rules

The lab rig is not the battle camera.

Use this angle:

```text
Right-facing side-view 2D modular zombie paper-doll art for a corpse-building screen, slight three-quarter depth, full-canvas sprite, no visible sockets, limbs overlap and cover joints.
```

For modular zombie parts:

- Head and torso can show slight chest/face depth.
- Arms and legs must still attach as side-view paper-doll parts.
- Feet must sit naturally on the ground line.
- Top surfaces should be subtle. If a part looks like a small old-RTS battle unit instead of a builder-preview body part, reject it for this rig.

## Limb-Specific Drawing Notes

`front_arm`:

- Pivot at `front_arm_shoulder`.
- Draw as the near-side attacking arm.
- It can cross in front of the torso.
- It should support attack animations clearly.

`back_arm`:

- Pivot at `back_arm_shoulder`.
- Draw as the far-side support arm.
- It should sit behind the torso in layer order.
- Keep it readable, but do not let it compete with the front arm.

`front_leg`:

- Pivot at `front_leg_hip`.
- Foot should land near `front_foot_ground`.
- Draw as the near-side stride leg.
- It can overlap the back leg.

`back_leg`:

- Pivot at `back_leg_hip`.
- Foot should land near `back_foot_ground`.
- Draw as the far-side support leg.
- It should be slightly darker/lower contrast than the front leg.

If an AI generation mixes these up, regenerate or manually correct before accepting the asset.

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

- It uses the `1024 x 1024 px` template.
- It faces right.
- It has no background.
- It has no baked shadow.
- It does not include another body slot by accident.
- It touches or overlaps its anchor area cleanly.
- Shoulder joints are covered by limb overlap, not exposed as visible sockets.
- It still works when combined with parts from another family.
- Feet reach the ground line when relevant.
- Shoulder, hip, and neck areas have enough overlap to hide seams.
- The silhouette reads in the lab preview and when scaled down for UI inspection.

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

Before treating a family as production-ready, test one family with separate generations per slot:

```text
head
torso
front_arm
back_arm
front_leg
back_leg
```

Do not rely only on a full-body sheet. Separate generations expose whether the style, anchors, overlap areas, and front/back limb logic survive the real modular workflow.

## Important Rule

A part is not finished just because it looks good alone. It is finished only when it works on the rig with unrelated parts from another family.
