# Camera And Perspective Standard

The project now uses two different camera standards because the lab and the battlefield have different jobs.

## Decision

Use side-view art for the zombie builder, and old-RTS high-angle art for battles.

```text
Lab / zombie builder: side-view 2D paper-doll preview
Battlefield: high-angle orthographic RTS camera
Unity camera: orthographic
Battle inspiration: Warlords Battlecry, Stronghold Crusader, Age of Empires style readability
Battle purpose: many small squads visible at once
```

This means earlier side-view zombie rig work is still useful for the lab and unit inspection screen. It should not define the actual battle camera.

## Lab Camera

Use this for:

- corpse-building screen
- modular zombie preview
- body-part inventory
- part cards when showing large character art
- close-up unit inspection

Lab art standard:

```text
Right-facing side-view 2D modular zombie art, slight three-quarter depth, strong silhouette, full-canvas paper-doll parts, no visible sockets, limbs overlap and cover joints.
```

The lab can show large, attractive modular zombies because the player needs to understand the body design.

## Battle Camera

Use this for:

- actual automatic battles
- units and squads on the battlefield
- battle terrain
- battle props
- battle structures
- projectiles and VFX

Battle art standard:

```text
Old-RTS high-angle orthographic 2D/2.5D battlefield art, camera looking down at units and terrain from above, readable squad-scale sprites, visible ground plane, visible tops of buildings and shoulders/heads, not side-scrolling, not fighting-game profile.
```

Recommended battle camera language:

```text
Camera type: Orthographic
Gameplay view: old-RTS high-angle battlefield
Camera yaw: fixed diagonal or near-diagonal map view
Camera pitch/art angle: high angled view, roughly 45-60 degrees from the ground plane
Unit scale: small squad-scale sprites, readable in groups
Battle readability: many units, projectiles, terrain, structures, and UI visible at once
```

Do not use side-scrolling character prompts for battlefield units.

## Why Two Cameras

The main hook is corpse-engineering, so the lab needs readable body parts and satisfying character construction. The battle needs to show many units and squads, so old-RTS perspective is a better fit than large side-view sprites.

This split reduces production risk:

- Lab art can be detailed and modular.
- Battle art can be simpler, smaller, and more readable.
- The same zombie design data can drive both the large lab preview and the simplified battle representation.
- The battle can support multiple squads without oversized sprites filling the screen.

## Unit Representation

The player builds zombies from modular parts in the lab. In battle, each built zombie design should be represented by a simplified RTS-scale unit sprite or small sprite set.

Recommended first implementation:

```text
Lab: modular side-view paper-doll zombie
Battle: small high-angle RTS unit sprite derived from the design's role/family
```

Do not require every modular body part to be individually visible in the battlefield sprite for MVP. The battle sprite only needs to communicate the unit role, family, and major mutation.

## Prompt Wording

For lab modular zombie parts:

```text
Right-facing side-view 2D modular zombie paper-doll part for a corpse-building screen, slight three-quarter depth, full-canvas sprite, no visible sockets, limbs overlap and cover joints, not RTS battle scale.
```

For battle units:

```text
Old-RTS high-angle orthographic unit sprite for a dark fantasy autobattler, viewed from above at a fixed battlefield angle, small squad-scale readability, visible head/shoulders/back and ground contact, clear silhouette at tiny size, not side-scrolling, not front-facing portrait, not fighting-game profile.
```

For battle terrain:

```text
Old-RTS high-angle orthographic terrain tile or ground patch, visible top plane, muted contrast behind units, readable dirt/stone/graveyard material, tileable or blendable, not side-scrolling background.
```

For battle structures:

```text
Old-RTS high-angle orthographic structure, visible roof/top surfaces and front/side faces, readable silhouette at gameplay zoom, dark fantasy material language, not side-view facade.
```

For lab props/UI:

```text
Dark fantasy gothic 2D game art, readable shapes, usable in a lab interface, enough plain space for real UI text where needed.
```

## Rejection Rules

Reject lab modular parts if:

- They look like tiny RTS units instead of builder-preview parts.
- They do not fit the side-view paper-doll rig.
- They expose shoulder sockets or mechanical limb slots.
- They include extra body slots.

Reject battle assets if:

- They look like side-scrolling lane sprites.
- They are too large or detailed for many units on screen.
- They use front-facing portrait perspective.
- They do not match the old-RTS high-angle camera.
- Buildings do not show believable top surfaces.
- Unit silhouettes collapse at squad scale.

## First Perspective Tests

Before production, create and compare:

1. One side-view lab zombie preview using the modular rig.
2. One high-angle RTS plague zombie battle sprite.
3. One high-angle RTS militia/enemy battle sprite.
4. One high-angle terrain patch with a small structure/prop.

Only lock production prompts after these four samples feel like the same game.
