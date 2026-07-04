# Battle Zombie Prompt Spec

Use this file when generating zombie sprites for the actual automatic battle screen.

Battle zombies are not the same asset type as lab modular zombie parts. The player builds detailed side-view zombies in the lab, but the battlefield needs small old-RTS high-angle sprites that stay readable when many squads are on screen.

## Current Battle Camera Target

```text
Old-RTS high-angle orthographic 2D/2.5D battlefield art, camera looking down at units from above, visible head/shoulders/back and ground contact, small squad-scale readability, not side-scrolling, not fighting-game profile, not front-facing portrait.
```

References for feel:

- Warlords Battlecry
- Stronghold Crusader
- Age of Empires

Do not copy those games. Use them only for camera, scale, and readability expectations.

## Production Image Contract

Every battle zombie sprite must obey this contract:

- Full body unit sprite or short animation frame.
- Transparent background for final assets.
- Old-RTS high-angle orthographic camera.
- Designed for small squad-scale readability.
- Strong silhouette before interior detail.
- Visible head/shoulders/back/top planes where useful.
- Clear ground contact.
- No side-view paper-doll profile.
- No modular body-part slots.
- No visible rig anchors, guide lines, labels, text, watermark, frame, or background scene.

For AI generation tests, use a flat chroma-key background and remove it locally.

## Design Mapping

The battle sprite should communicate the zombie design at a simplified level.

Required visible signals:

- Family: plague, brute, runner, etc.
- Role: tank, fast attacker, ranged/spitter, support, swarm.
- Major mutation if present.
- Team identity: necromantic green/bone/dark iron.

Not required for MVP:

- Every exact modular arm/leg/head part.
- Exact socket/anchor geometry from the lab rig.
- Full visual fidelity to the large lab preview.

## Prompt Block

Use this block for battle zombie generation:

```text
Use case: game-assets
Asset type: old-RTS high-angle battle unit sprite for a Unity 2D necromancer autobattler
Output contract: one full-body zombie unit only, transparent-ready sprite on a flat chroma-key background, designed for small squad-scale readability, no background scene.
Canvas/background: create the unit on a perfectly flat solid #ff00ff chroma-key background for background removal. The background must be one uniform color with no shadows, gradients, texture, floor plane, or lighting variation. Do not use #ff00ff anywhere in the subject.
Camera: old-RTS high-angle orthographic 2D/2.5D battlefield art, camera looking down at the unit from above, visible head/shoulders/back and ground contact, not side-scrolling, not fighting-game profile, not front-facing portrait, not pure top-down token.
Style reference: graphic hand-drawn gothic 2D game art, bold readable outline, large shadow blocks, restrained detail, dark bone/rotted flesh/iron palette, controlled necromantic green accents, not photorealistic, not noisy.
Detail rule: must read when many units are on screen. Large silhouette first, simple material blocks second, small accents last.
Reject conditions: no readable text, no watermark, no labels, no frame, no lab paper-doll body part, no side-view profile, no huge portrait pose, no floor shadow baked into the sprite, no excessive gore, no busy micro-detail.
```

## First Battle Zombie Tests

Generate these before production:

1. `plague_battle_unit_01`
2. `brute_battle_unit_01`
3. `runner_battle_unit_01`

Acceptance test:

- Place 8-20 copies on a mock battlefield.
- Scale to expected RTS unit size.
- Confirm each role reads immediately.
- Confirm the units do not visually fight with terrain.
- Confirm they match the same camera as enemy units and structures.

## Acceptance Levels

Use these labels:

```text
accepted_battle_style_reference
cleanup_candidate
battle_scale_test_candidate
production_candidate
rejected
```

Do not label a battle unit `production_candidate` until it has been tested in a battlefield mockup with multiple units.
