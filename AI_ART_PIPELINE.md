# AI Art Production Pipeline

This project assumes AI-generated art is the primary asset source. Manual Photoshop work should be light cleanup, alignment, cutout correction, color matching, and small paintovers, not full asset production.

## Main Rule

Do not generate random isolated assets directly into production.

Use this order:

1. Create a master style reference.
2. Create category reference sheets.
3. Generate production assets from those references.
4. Validate assets in Unity.
5. Lightly correct in Photoshop only when needed.

The goal is consistency. A beautiful asset that does not match the game is not production-ready.

## Master Style Reference

The project needs one master artwork that defines the whole visual language.

It should show:

- Necromancer lab atmosphere.
- One modular zombie.
- Lane battlefield direction.
- Village/guard enemy side.
- Terrain treatment.
- Rocks, trees, props, and structures.
- UI material language.
- Lighting and color palette.

This image is not directly a game asset. It is a reference anchor for all later prompts.

Master style target:

- Dark fantasy.
- Readable 2D game art.
- Hand-painted/painterly, not photorealistic.
- Slightly stylized proportions.
- High silhouette clarity.
- Green necromantic magic.
- Bone, old iron, dark wood, candlelight, grave soil, muted blood accents.
- Clean enough for small gameplay readability.

Avoid:

- Photorealism.
- Overly detailed noise.
- Random horror gore.
- Comic/cartoon exaggeration.
- Pure monochrome green palette.
- Inconsistent camera angle.
- Assets that only look good as illustrations but fail as game sprites.

## Asset Categories

Use separate generation standards per category.

Perspective standard:

- Use `CAMERA_AND_PERSPECTIVE.md`.
- The game uses side-scrolling 2.5D, not isometric.
- Characters should be mostly side view with slight three-quarter depth.
- Environment assets can show subtle top surfaces, but must still support horizontal lane readability.

### Modular Zombie Parts

Purpose: runtime-swappable character parts.

Canonical rig:

- `assets/rigs/zombie_side_v1.json`
- `assets/rigs/zombie_side_v1_template.svg`
- `ART_RIG_GUIDE.md`

Production rules:

- Use `1024 x 1024 px` full-canvas exports.
- Transparent background.
- Right-facing side view.
- Same anchors and ground line.
- Separate slots: `head`, `torso`, `front_arm`, `back_arm`, `front_leg`, `back_leg`.
- `front_arm` and `front_leg` mean near-side limbs closest to camera.
- `back_arm` and `back_leg` mean far-side limbs partly behind the body.
- No baked shadows.
- No background.
- No accidental extra body slots.

Photoshop cleanup:

- Remove background.
- Fix seam overlap.
- Align anchor points.
- Match color/contrast.
- Clean edge artifacts.

### Enemies

Purpose: opposing readable units in lane battles.

Recommended first enemy asset types:

- Militia.
- Crossbowman.
- Guard.
- Priest later.

Rules:

- Same side-view gameplay camera as zombies.
- Enemy silhouettes must differ clearly from zombies.
- Human enemies can be full sprites at first; modular enemies are not required for MVP.
- Use warmer torch/iron/cloth colors to contrast necromancer green.
- Keep weapons readable at battle scale.

### Environment Tiles And Terrain

Purpose: battlefield lanes, lab floors, village ground, graveyard ground.

Asset types:

- Ground strips.
- Dirt/stone tiles.
- Graveyard terrain.
- Village road.
- Lab floor.
- Background layers.

Rules:

- Avoid high-detail noise that fights with units.
- Terrain should be darker and lower contrast than characters.
- Create repeatable/tileable variants where needed.
- Keep lane readability first.

### Props

Purpose: visual worldbuilding and UI/lab dressing.

Examples:

- Bones.
- Candles.
- Reagent bottles.
- Coffins.
- Workbench tools.
- Corpse trays.
- Chains.
- Grave markers.
- Barrels.
- Crates.

Rules:

- Props should use the same material language as the master reference.
- Generate in small themed sheets where possible.
- Use transparent background for foreground props.
- Avoid random scale; props need approximate size categories.

Size categories:

- Small prop: `256 x 256`
- Medium prop: `512 x 512`
- Large prop: `1024 x 1024`

### Rocks, Trees, And Natural Objects

Purpose: battlefield decoration and biome identity.

Rules:

- Use muted colors and strong silhouettes.
- Avoid photoreal texture.
- Generate as isometric/side-view compatible depending on scene use.
- Use transparent cutouts for foreground objects.
- Keep variations within one shape language.

Initial set:

- 3 rocks.
- 3 dead trees.
- 3 graveyard bushes/roots.
- 3 broken fence pieces.

### Structures

Purpose: battlefield background and objectives.

Examples:

- Necromancer base.
- Village gate.
- Watchtower.
- Graveyard crypt.
- Lab exterior.
- Barricade.

Rules:

- Larger assets can be `2048 x 1024` or `2048 x 2048`.
- Must match side-view lane perspective.
- Do not overdetail backgrounds.
- Important structures need readable silhouette at gameplay zoom.

### UI Art

Purpose: menus, panels, icons, buttons, cards, frames.

Rules:

- UI should be dark fantasy but clean and readable.
- Use parchment, bone, dark metal, old wood, green glow, and brass accents.
- Avoid decorative frames that waste too much screen space.
- Text areas must stay plain enough for real UI text.
- Generate UI frames without fake text.

Initial UI assets:

- Panel frame.
- Button states.
- Part card frame.
- Reward card frame.
- Resource icons.
- Status icons.
- Slot icons.

### VFX

Purpose: hit feedback and readable status effects.

First effects:

- Plague puff.
- Hit slash.
- Armor break spark.
- Death soul wisp.
- Explosion.
- Heal/regeneration glow.

Rules:

- Effects need transparent background.
- Must read at small size.
- Do not hide unit silhouettes.
- Prefer simple sprite sheets or small frame sequences.

## Prompt Strategy

Every production prompt should include:

- Reference to the master style.
- Asset category.
- Exact game use.
- Camera angle.
- Canvas size.
- Background requirement.
- Avoid list.

Example structure:

```text
Create a [category] asset for a 2D dark fantasy necromancer autobattler.
Match the master style reference: hand-painted, readable, dark olive/bone/iron palette, green necromantic accents, side-view gameplay readability.
Asset: [specific asset]
Use: [battle unit / lab prop / UI card / structure]
Canvas: [size]
Background: transparent / simple dark preview background
Camera: [right-facing side view / front UI icon / side-view structure]
Constraints: no text, no logo, no photorealism, no random extra objects, no excessive gore.
```

## Quality Gates

An AI asset is accepted only if:

- It matches the master style.
- It matches the correct camera/perspective.
- It works at gameplay size.
- It has clean edges or can be cleaned quickly.
- It does not introduce a new art direction.
- It can be used in Unity without major repainting.

Reject or regenerate when:

- Perspective is wrong.
- Lighting does not match.
- Detail level is too noisy.
- Shape language does not match.
- It contains fake text.
- It has important cropped edges.
- It needs heavy manual repainting.

## Folder Plan

Recommended production structure:

```text
assets/
  art-style/
    master/
    references/
  characters/
    zombies/
    enemies/
  environment/
    terrain/
    props/
    rocks_trees/
    structures/
  ui/
    frames/
    icons/
    cards/
  vfx/
  rigs/
```

## Practical Workflow

1. Generate master style reference.
2. Approve or regenerate until the whole game direction feels right.
3. Generate zombie family reference sheet.
4. Generate environment reference sheet.
5. Generate UI reference sheet.
6. Create first actual production assets.
7. Import into Unity.
8. Test at gameplay scale.
9. Photoshop cleanup only if the asset is close.
10. Save accepted asset and prompt notes.

## Important Production Warning

AI art can make the game look impressive fast, but inconsistency is the main risk. The master style reference and category sheets are more important than any single asset.
