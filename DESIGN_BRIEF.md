# Necromancer Autobattler Design Brief

## Core Pitch

A 2D necromancer strategy/autobattler where the player runs a corpse-engineering lab, builds custom zombies from modular body parts, then sends those designs into automatic lane battles.

The player does not micro-control units during combat. Zombies march forward, meet enemy waves, attack automatically, die, and generate results. The main player skill is in designing bodies before battle: choosing heads, torsos, arms, individual legs, mutations, and passive effects that combine into useful combat roles.

## Target Scope

This should be designed as a 3-month solo-dev project. The first playable version must prove the main hook before expanding content.

The game should feel like:

- Build strange zombies in the lab.
- Watch them fight automatically.
- Learn what failed.
- Unlock or recover better corpse parts.
- Improve the design and try again.

It should not start as:

- A full RPG.
- A large campaign.
- A physics-heavy creature simulator.
- A complex RTS with real-time player control.
- A game requiring unique full-body art for every zombie combination.

## Player Loop

1. Choose available corpse parts in the lab.
2. Assemble one or more zombie designs.
3. Assign zombies to a lane or wave order.
4. Start the battle.
5. Units march and fight automatically.
6. Player receives rewards: parts, reagents, gold, research, or corpse scraps.
7. Player upgrades parts, unlocks mutations, and edits zombie designs.

## Main Game Pillars

Every feature should support at least one of these pillars:

- Corpse engineering: the fun comes from building weird bodies with clear mechanical tradeoffs.
- Automatic proof: battles should quickly prove whether a design works.
- Readable failure: when zombies lose, the player should understand why.
- Cheap iteration: editing a zombie should be fast, visual, and low-friction.
- Controlled scope: content should come from recombining parts, not hand-building hundreds of unique units.

If a feature does not support these pillars, it should wait.

## Core Screens And Modules

The game can be built as a small set of focused modules.

Required modules for the first complete version:

- `lab`: main hub for building, upgrading, and choosing battles.
- `assembler`: UI for selecting zombie parts and previewing the final body.
- `part_inventory`: owned corpse parts, locked parts, duplicates, quality, and stats.
- `battle`: lane combat simulation and rendering.
- `battle_results`: win/loss summary, rewards, casualties, and useful feedback.
- `progression`: unlocks, research, upgrades, and campaign state.
- `save_system`: owned parts, zombie designs, resources, completed battles, settings.
- `content_data`: definitions for parts, enemies, battles, rewards, effects, and research.

Nice-to-have later modules:

- `graveyard`: corpse harvesting, part recycling, and random salvage.
- `experiments`: mutation crafting and risky upgrades.
- `black_market`: buying rare parts or selling surplus material.
- `codex`: enemy/part encyclopedia.
- `events`: small text choices between battles.
- `achievements`: optional long-term goals.

## Lab Structure

The lab should be a practical hub, not a large base-building game.

First version lab actions:

- Build or edit zombie design.
- View owned parts.
- View stats and effects for assembled zombie.
- Choose next battle.
- Spend resources on simple research or upgrades.
- Save named zombie designs.

Possible lab stations:

- Assembly Table: combine body parts into zombie templates.
- Corpse Storage: view available body parts and duplicates.
- Research Desk: unlock new slots, part families, or stat bonuses.
- Mutation Vat: add one mutation/effect to a zombie.
- Battle Map: choose the next enemy encounter.

For MVP, these can be buttons or tabs on one lab screen. They do not need to be separate rooms.

## Zombie Design System

The zombie design is a template. The player assembles a design from parts, then the battle spawns zombies from that design.

Each design should store:

- Selected `head`
- Selected `torso`
- Selected `front_arm`
- Selected `back_arm`
- Selected `front_leg`
- Selected `back_leg`
- Optional `mutation`
- Name
- Color tint or small cosmetic marker if easy
- Calculated stats
- Calculated effects
- Spawn cost or control cost

The first version should allow 1 active zombie design. A later version can allow 3-5 saved designs and let the player choose a spawn order.

Example roles:

- Tank: high health torso, shield back arm, slow leg pair.
- Charger: runner legs, claw front arm, fragile torso.
- Plague carrier: plague head, plague torso, mutation that spreads infection.
- Hook disruptor: hook front arm, stable legs, control-focused head.
- Exploder: bloated torso, unstable mutation, cheap parts.

Important rule: the player should be able to read the assembled zombie and understand its role before battle.

## Battle Model

Battles use automatic lane combat:

- Units spawn from the player's side.
- Enemies spawn from the opposite side or from wave triggers.
- Units walk toward enemies.
- When in range, units stop and attack.
- Melee units block each other.
- Ranged or special parts can attack from behind the front line.
- Battle ends when the enemy base/wave is cleared or the player's force collapses.

The goal is readable combat, not tactical micro. The battle should quickly show whether a body design works.

## Battle Flow

Recommended first battle flow:

1. Load selected zombie design.
2. Spawn player zombies at fixed intervals or from a simple spawn budget.
3. Spawn enemies in scripted waves.
4. Units move toward the nearest valid target.
5. Units stop when inside attack range.
6. Units attack automatically based on cooldown.
7. Effects apply through simple status rules.
8. Battle ends on victory, defeat, or timeout.
9. Show result summary and rewards.

The player can watch, pause, speed up, and restart. Direct combat commands should not be part of the first version.

## Unit Behavior

Keep AI simple and deterministic.

Base unit states:

- `spawning`
- `moving`
- `attacking`
- `stunned`
- `dying`
- `dead`

Targeting priority:

1. Enemy blocking movement in front.
2. Closest enemy in attack range.
3. Enemy base/objective if no unit blocks the path.

Optional targeting modifiers from heads:

- Attack weakest enemy.
- Attack nearest infected enemy.
- Prefer ranged enemies.
- Prefer armored enemies.

Do not build complex pathfinding for the first version. A single lane can be represented as one horizontal axis.

## Combat Stats

Minimum combat stats:

- `health`
- `armor`
- `moveSpeed`
- `attackDamage`
- `attackSpeed`
- `attackRange`
- `controlCost`
- `bodyMass`
- `plaguePower`

Possible later stats:

- `critChance`
- `blockChance`
- `lifesteal`
- `knockback`
- `tenacity`
- `fireResist`
- `plagueResist`
- `stunResist`

MVP damage formula:

```text
damage_taken = max(1, incoming_damage - armor)
```

This is simple and readable. Replace it later only if balance needs it.

## Status Effects

Use only a few status effects at first.

MVP effects:

- Plague: takes damage over time.
- Slow: reduced movement speed.
- Stun: cannot move or attack briefly.
- Armor Break: temporary armor reduction.
- Regeneration: heals over time.

Later effects:

- Burn.
- Bleed.
- Fear.
- Taunt.
- Shield.
- Corpse Mark.
- Infection burst.

Each status effect needs:

- Name.
- Icon.
- Duration.
- Stack rule.
- Visual indicator.
- Gameplay effect.

Avoid invisible effects. If the player cannot see or understand an effect, it will feel random.

## Enemy Design

Enemies exist to test zombie designs.

MVP enemy faction: villagers, guards, or graveyard hunters.

First enemy types:

- Militia: basic melee blocker.
- Crossbowman: low health ranged enemy.
- Guard: armored slow enemy.

Later enemy types:

- Priest: heals or cleanses plague.
- Torchbearer: burning damage, strong against regeneration.
- Trapper: slows or roots fast zombies.
- Knight: high armor boss-style unit.
- Alchemist: area damage and anti-plague tools.
- Gravehound: fast unit that punishes slow builds.

Enemy encounters should teach counters:

- Crossbowmen punish slow zombies.
- Guards punish low armor-piercing damage.
- Priests punish plague-only builds.
- Swarms punish single-target brutes.

## Encounter Design

Each battle should have a clear purpose.

MVP encounter examples:

- Battle 1: basic militia wave, teaches movement and melee.
- Battle 2: militia plus crossbowmen, tests speed or durability.
- Battle 3: armored guard plus support, tests damage type and sustain.

Encounter fields:

```json
{
  "id": "battle_01_militia",
  "displayName": "Village Patrol",
  "waves": [
    { "time": 1.0, "enemy": "militia", "count": 2 },
    { "time": 8.0, "enemy": "militia", "count": 3 }
  ],
  "rewards": {
    "boneScraps": 20,
    "reagents": 1,
    "partChoices": ["plague_head_01", "brute_torso_01"]
  }
}
```

## Rewards

Rewards should push the player back into the lab.

Reward types:

- New body part.
- Choice between 2-3 parts.
- Upgrade material.
- Mutation reagent.
- Research point.
- Cosmetic tint or lab decoration later.

MVP reward rule:

- Give one fixed reward plus one choice reward.
- Keep rewards deterministic until the core game is balanced.

Random rewards can come later after the game has enough content.

## Failure And Retry

Losing should be useful, not just punitive.

After defeat, show:

- How long the battle lasted.
- Which enemy dealt most damage.
- Which zombie part contributed most damage or tanking.
- Whether zombies died before reaching enemies.
- Whether armor, range, speed, or plague resistance was the main problem.

MVP can show simple hints:

- "Your zombies died before reaching ranged enemies. Try faster legs or more health."
- "Armored enemies blocked most of your damage. Try armor break or higher damage arms."
- "Plague damage was cleansed. Try brute force or attack speed."

The player should keep progress after losing, unless a later roguelite mode is intentionally added.

## Later Multiplayer Direction

If early access proves the solo game has strong retention, a later expansion can add 1v1 automatic lane battles.

The multiplayer pitch:

- Two players bring their own zombie designs.
- Each side spawns units from opposite ends of the lane.
- Units march forward and fight automatically.
- Players win by breaking through enemy waves, destroying an objective, or outlasting the opponent.
- The skill is in pre-battle design, build order, counters, and adaptation between rounds.

This should be treated as a later product direction, not an MVP feature.

Recommended multiplayer shape:

- Asynchronous or round-based first, real-time later only if demand justifies it.
- 1 lane first, multiple lanes later.
- Fixed match rules with a build budget to avoid pay-to-win progression problems.
- Matchmaking only after private/friend matches work.
- Deterministic battle simulation so both clients can reproduce the same result.
- Clear replay/results screen so players can understand why they lost.

Possible 1v1 modes:

- Mirror Budget Duel: both players build from the same point budget.
- Collection Duel: players use their unlocked parts, with power normalization.
- Draft Duel: players draft parts from shared choices before fighting.
- Best-of-3 Lab Duel: players can adjust designs between short rounds.

Multiplayer design risks:

- Networking, matchmaking, cheating, and balance can easily exceed solo-dev scope.
- Player progression can make PvP feel unfair if stronger accounts simply have better parts.
- Real-time sync is expensive if the battle simulation is not deterministic.
- PvP balance can damage the solo game if every part has to be balanced for both modes.

Design implication for the solo game:

- Keep battle simulation deterministic where practical.
- Keep part definitions data-driven.
- Avoid hidden random rolls inside combat.
- Separate account progression from match rules.
- Do not build multiplayer UI, servers, accounts, ranking, or matchmaking during the first version.

## Main Hook: Corpse Engineering

Zombies are built from modular body slots. Each slot changes stats, behavior, or effects.

Required slots for the first rig:

- `head`
- `torso`
- `front_arm`
- `back_arm`
- `front_leg`
- `back_leg`

Optional later slots:

- `mutation`
- `parasite`
- `spine`
- `aura`
- `held_item`
- `skin_overlay`

The first vertical slice should use only the required slots plus one optional mutation/effect slot if implementation stays simple.

## Part Gameplay Roles

Each body part should have a clear gameplay purpose.

Heads:

- Targeting behavior.
- Intelligence or control.
- Special trigger effects.
- Examples: plague head, brute head, scout head, screaming head.

Torsos:

- Health, armor, resistance, carried organs.
- Main zombie archetype identity.
- Examples: bloated torso, stitched guard torso, infected ribcage.

Front arms:

- Primary attack.
- Melee reach, damage, attack speed, cleave.
- Examples: claw arm, butcher hook, bone blade.

Back arms:

- Secondary attack or utility.
- Shield, ranged spit, grab, buff, corpse harvest.
- Examples: shield arm, spitter arm, extra claw.

Legs:

- Movement speed.
- Stability, charge, knockback resistance.
- Split into `front_leg` and `back_leg` so walk cycles can animate each leg separately.
- Examples: shambling front leg, runner back leg, armored front leg.

Mutations:

- One clear extra rule.
- Examples: explodes on death, spreads plague, regenerates, splits into crawlers.

## Body Part Data Model

Every part should be data-driven. Avoid hard-coding individual part behavior inside battle logic unless a mechanic truly needs custom code.

Suggested part fields:

```json
{
  "id": "plague_head_01",
  "slot": "head",
  "family": "plague",
  "displayName": "Plague Head",
  "description": "Adds plague buildup to basic attacks.",
  "rarity": "common",
  "image": "assets/zombies/parts/head/plague_head_01.png",
  "rig": "zombie_side_v1",
  "tags": ["plague", "control"],
  "stats": {
    "health": 5,
    "plaguePower": 2,
    "controlCost": 1
  },
  "effects": ["plague_on_hit"]
}
```

Suggested fields:

- `id`
- `slot`
- `family`
- `displayName`
- `description`
- `rarity`
- `image`
- `rig`
- `tags`
- `stats`
- `effects`
- `unlockRequirement`
- `sellValue`
- `upgradeLevel`

## Part Families

Part families make content easier to understand and easier to produce.

Recommended initial families:

- Plague: poison, damage over time, infection spread, medium stats.
- Brute: health, armor, knockback resistance, slow attacks.
- Runner: speed, attack rate, low health, flanking pressure.

Later families:

- Bone: armor piercing, spikes, brittle but sharp.
- Blood: lifesteal, sacrifice, regeneration.
- Frost: slow, brittle armor, crowd control.
- Fire: burning, self-damage risk, explosive deaths.
- Royal: command aura, expensive, rare elite body parts.
- Insect: swarm effects, extra limbs, fragile but numerous.
- Mechanical: armor, overheating, saws, unstable engines.

Do not add all later families early. The first goal is to prove that three families can mix into interesting builds.

## Resources And Economy

Keep the economy readable. The player should not need six currencies in the first version.

Recommended first resources:

- Corpse Parts: actual owned parts used for building.
- Bone Scraps: common upgrade/crafting material.
- Reagents: uncommon material for mutations and research.
- Gold: optional general shop currency if a shop exists.

MVP can start with only:

- Parts
- Bone Scraps
- Reagents

Resource sources:

- Battle rewards.
- Salvaging duplicate parts.
- Bonus rewards for optional objectives.
- Later: graveyard harvesting or shop purchases.

Resource sinks:

- Unlocking new part families.
- Upgrading part level.
- Rerolling a reward choice.
- Creating a mutation.
- Buying a missing part.

Avoid a heavy economy until the battle loop is fun.

## Progression

Progression should unlock more design choices, not just bigger numbers.

MVP progression:

- Win battle 1 to unlock the second part family.
- Win battle 2 to unlock mutation slot.
- Win battle 3 to unlock stronger enemy encounter or second saved zombie design.

Possible progression tracks:

- Part family unlocks.
- Mutation unlocks.
- More saved zombie designs.
- Higher part levels.
- More battle rewards.
- More enemy factions.
- Lab station upgrades.

Example research nodes:

- Basic Stitching: unlock zombie assembly.
- Reinforced Sutures: +10% torso health.
- Fresh Legs: unlock runner legs.
- Contained Infection: unlock plague mutation slot.
- Crude Command: allow 2 active zombie designs.
- Harvest Discipline: improve duplicate salvage rewards.

Progression should avoid permanent traps. A player should not be able to spend resources in a way that ruins their run.

## Part Upgrades And Crafting

Part upgrades should be simple at first.

MVP upgrade model:

- Each part can be level 1-3.
- Upgrade cost uses Bone Scraps and sometimes Reagents.
- Upgrades increase existing stats.
- Upgrades do not change the visual asset.

Later upgrade model:

- Add a small modifier to a part.
- Fuse duplicates.
- Add quality tiers.
- Add unstable experiment outcomes.

Avoid early crafting systems that require recipes, timers, many ingredients, or large inventories.

## Mutation System

Mutations are optional rule-changing effects. They should be few but meaningful.

MVP mutations:

- Explosive: zombie explodes on death.
- Regenerative: zombie slowly heals out of combat or below half health.
- Infectious: plague can spread to nearby enemies.

Mutation rules:

- One mutation per zombie design in the first version.
- Mutations should be visible in the preview through a tint, overlay, particles, or icon.
- Mutations should have clear tradeoffs when possible.

Example tradeoffs:

- Explosive: high death damage, but lower max health.
- Regenerative: sustain, but higher control cost.
- Infectious: strong against groups, weak against armored single targets.

## First Vertical Slice

The first playable slice should include enough content to test the full loop without pretending to be a finished game.

Recommended scope:

- 1 lab screen.
- 1 battle screen.
- 1 lane.
- 1 zombie assembly UI.
- 1 enemy faction.
- 3 enemy types.
- 6 body slots.
- 3 choices per slot.
- 1 optional mutation slot.
- 3 short battles.
- Basic rewards after each battle.
- Save/load for unlocked parts and current zombie designs.

This gives up to 729 base body combinations with only 18 required part assets, before mutations. That is enough to test whether modular assembly is fun.

## UI And UX Requirements

The UI should make body-building clear.

Lab UI:

- Large zombie preview.
- Slot list with selected parts.
- Part inventory grid.
- Stats panel with before/after comparison.
- Effect icons with short tooltips.
- Start battle button.

Assembler UI:

- Click a body slot.
- Show compatible parts for that slot.
- Preview updates immediately.
- Show stat changes before confirming.
- Support locked parts visibly but do not clutter the first build.

Battle UI:

- Health bars.
- Small status icons.
- Wave progress.
- Pause and speed controls.
- Restart.
- Return to lab after battle.

Results UI:

- Victory/defeat.
- Rewards.
- Damage dealt.
- Damage taken.
- Zombie deaths.
- One or two useful feedback lines.

Avoid spreadsheet UI. The player needs enough numbers to make choices, but the zombie body should remain the main visual focus.

## Audio Needs

Audio can be simple but should support feedback.

MVP audio:

- Button click.
- Part attach/stitch sound.
- Battle start.
- Basic hit.
- Heavy hit.
- Zombie death.
- Enemy death.
- Plague/status tick.
- Victory.
- Defeat.

Later audio:

- Family-specific attack sounds.
- Lab ambience.
- Mutation vat bubbling.
- Boss music.

## Visual Effects Needs

MVP effects:

- Hit flash.
- Damage number or simple damage pop.
- Death fade or collapse.
- Plague particle/tint.
- Explosion for explosive mutation.
- Selection outline in assembler.

Avoid complex animation requirements early. Simple layered sprites, small movement, squash/flash, and particles are enough for a prototype.

## Save Data

Save only what must persist.

Suggested save fields:

```json
{
  "version": 1,
  "resources": {
    "boneScraps": 0,
    "reagents": 0
  },
  "ownedParts": ["plague_head_01"],
  "partLevels": {
    "plague_head_01": 1
  },
  "unlockedResearch": ["basic_stitching"],
  "completedBattles": [],
  "zombieDesigns": [
    {
      "name": "First Horror",
      "head": "plague_head_01",
      "torso": "plague_torso_01",
      "frontArm": "plague_front_arm_01",
      "backArm": "plague_back_arm_01",
      "frontLeg": "plague_front_leg_01",
      "backLeg": "plague_back_leg_01",
      "mutation": null
    }
  ]
}
```

Use versioned save data from the start. It prevents pain when fields change.

## Content Data Files

Recommended content files:

```text
data/
  parts.json
  effects.json
  enemies.json
  encounters.json
  rewards.json
  research.json
  balance.json
```

Keep content editable without touching core battle code.

## Technical Modules

If built in a typical 2D engine, the code can be separated into these systems:

- `PartDefinition`
- `ZombieDesign`
- `ZombieStatsCalculator`
- `ZombiePreviewRenderer`
- `InventoryService`
- `ResearchService`
- `EncounterDefinition`
- `BattleController`
- `LaneController`
- `UnitController`
- `TargetingSystem`
- `DamageSystem`
- `StatusEffectSystem`
- `RewardService`
- `SaveService`
- `ContentDatabase`
- `BattleReplayData` later, if deterministic replays or multiplayer become important

Keep battle logic independent from UI where possible. The same zombie design data should drive preview, stats, save files, and spawned combat units.

## Unity Rig Direction

The first Unity rig should be one reusable animated prefab. Code swaps sprites into fixed slots; animation clips move the slot transforms.

Recommended hierarchy:

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

Each slot has a `SpriteRenderer`. The Animator should animate the slot objects, not unique finished zombie sprites.

Important pivot rules:

- Head pivots at neck.
- Torso pivots around hips or body center.
- Arms pivot at shoulders.
- Front leg pivots at front hip.
- Back leg pivots at back hip.
- Root stays on the ground center.

Separate front/back legs are worth it because walking can show actual alternating leg motion. A single combined leg sprite would limit walk readability and make every zombie feel like it slides.

## Balancing Rules

Balance for clear tradeoffs first, exact numbers second.

Good tradeoffs:

- Fast but fragile.
- Durable but slow.
- High damage but expensive.
- Strong plague but weak direct damage.
- Explosive but disposable.
- Armored but vulnerable to armor break.

Bad tradeoffs:

- Same part but slightly better in every way.
- Hidden penalties.
- Effects that cannot be seen.
- Numbers so small the player cannot feel the difference.

Use a small number scale at first:

- Health: 20-200.
- Damage: 3-30.
- Armor: 0-10.
- Attack speed: 0.5-2.0 attacks per second.
- Movement speed: 30-120 pixels per second.

## Production Risks

Likely risks:

- Modular art does not align cleanly across generated parts.
- Feature creep turns the game into an RPG/base-builder instead of a focused autobattler.
- Battle results are hard to read, so player choices feel random.
- Too many resources or effects make the game hard to balance.
- Animation workload grows beyond solo-dev scope.

Mitigations:

- Lock one rig template before creating many parts.
- Build battle with placeholders before final art.
- Keep effects visible and limited.
- Use deterministic encounters during early balancing.
- Delay multi-lane battles, advanced crafting, and procedural rewards.

## Do Not Build Yet

These are good later ideas, but risky for the first slice:

- Multiple simultaneous lanes.
- Large army management.
- Procedural campaigns.
- Equipment inventories.
- Dozens of status effects.
- Online features.
- Multiplayer, matchmaking, accounts, rankings, or servers.
- Advanced animation blending.
- Physics-based body deformation.
- Unique death animations for every part.
- Full-body generated sprites for every combination.

## Modular 2D Asset Direction

Use a paper-doll pipeline: separate transparent PNG layers are assembled into a complete zombie at runtime or during import.

This is the right direction because full-body sprite generation does not scale. If every possible zombie needs a unique complete sprite, asset work becomes impossible. Modular parts make the art workload manageable, but only if every part follows the same rig rules.

Current proof-of-concept assets:

- `C:\Users\husiv\Documents\New project\generated-assets\plague-zombie-transparent.png`
- `C:\Users\husiv\Documents\New project\generated-assets\modular-zombie-test\modular-plague-zombie-sheet-transparent.png`
- `C:\Users\husiv\Documents\New project\generated-assets\modular-zombie-test\plague-zombie-head.png`
- `C:\Users\husiv\Documents\New project\generated-assets\modular-zombie-test\plague-zombie-torso.png`
- `C:\Users\husiv\Documents\New project\generated-assets\modular-zombie-test\plague-zombie-front-arm.png`
- `C:\Users\husiv\Documents\New project\generated-assets\modular-zombie-test\plague-zombie-back-arm.png`
- `C:\Users\husiv\Documents\New project\generated-assets\modular-zombie-test\plague-zombie-legs.png` as old combined-leg proof only
- `C:\Users\husiv\Documents\New project\generated-assets\pitch\necromancer-lab-lane-battle-pitch.png`

These are useful as visual direction, not final production standards.

## Modular Zombie Rig Spec

### Canvas

Use one fixed canvas size for every assembled zombie and every individual part export.

Recommended first rig:

- Canvas: `512x512`
- Facing: right-facing side/profile or three-quarter side view
- Ground line: `y=430`
- Body center line: `x=256`
- Transparent background
- No shadow baked into body parts
- No weapon or effect extending outside the canvas

Every body part PNG should be exported on the full `512x512` canvas, positioned exactly where it belongs on the assembled zombie. This is less storage-efficient, but much safer for a solo project because parts can be layered without per-file manual offsets.

### Layer Order

Render body parts in this order:

1. `back_arm`
2. `back_leg`
3. `front_leg`
4. `torso`
5. `head`
6. `front_arm`
7. `mutation_overlay`
8. `effects`

This keeps the rear arm behind the body and the front arm visibly readable.

### Anchor Points

Each part should use consistent anchor points even if exported on a full canvas. Store anchors as metadata so the rig can later move to trimmed sprites if needed.

Base anchors:

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

These numbers are starting values. Once the first production template is drawn, they should be locked and reused.

### Required Metadata

Each part should have a small metadata file or data entry.

Example:

```json
{
  "id": "plague_head_01",
  "slot": "head",
  "displayName": "Plague Head",
  "image": "zombie_parts/head/plague_head_01.png",
  "rig": "zombie_side_v1",
  "anchors": {
    "head_neck": { "x": 256, "y": 170 }
  },
  "stats": {
    "control": 1,
    "plaguePower": 2
  },
  "effects": ["plague_bite"]
}
```

## Asset Generation Rules

AI generation can be used for concepting and first-pass parts, but production assets need strict checking.

Every generated part must follow this guide:

- Same `512x512` transparent canvas.
- Same camera angle.
- Same scale.
- Same lighting direction.
- Same ground line.
- Same neck, shoulder, hip, and foot positions.
- No full-body parts hidden inside individual slot images.
- No mismatched perspective.
- No cropped limbs.
- No extra heads, weapons, floating gore, text, labels, frames, or background.
- Silhouette must remain readable at small size.
- Attachment areas must be clean enough to overlap without obvious gaps.

Recommended production workflow:

1. Generate full zombie concept for style.
2. Generate or manually cut modular parts using the locked template.
3. Place parts on the fixed canvas.
4. Export transparent PNGs.
5. Test each part against at least two different parts from other sets.
6. Reject or fix parts that only work with their original matching set.

## Naming Convention

Use lowercase snake case for files and IDs.

Folders:

```text
assets/
  zombies/
    rigs/
      zombie_side_v1.json
    parts/
      head/
      torso/
      front_arm/
      back_arm/
      front_leg/
      back_leg/
      mutation/
```

File names:

```text
<theme>_<slot>_<variant>.png
```

Examples:

```text
plague_head_01.png
plague_torso_01.png
plague_front_arm_01.png
plague_back_arm_01.png
plague_front_leg_01.png
plague_back_leg_01.png
brute_front_arm_01.png
runner_front_leg_01.png
```

IDs should match file names without extension.

## First Part Set

For the first slice, create three coherent part families:

Plague:

- Applies poison/plague effects.
- Medium health.
- Good over time.

Brute:

- High health and melee damage.
- Slow.
- Good front-line unit.

Runner:

- Fast and fragile.
- Good for reaching ranged enemies or rushing objectives.

Initial parts:

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

## Minimum Stat Model

Keep the first stat model small.

Zombie stats:

- `health`
- `armor`
- `moveSpeed`
- `attackDamage`
- `attackSpeed`
- `attackRange`
- `plaguePower`
- `controlCost`

Part effects should be additive unless there is a strong reason otherwise.

Example body calculation:

```text
final_health = torso.health + head.health + arms.health + front_leg.health + back_leg.health
final_move_speed = average(front_leg.moveSpeed, back_leg.moveSpeed) + mutation.moveSpeedBonus
final_attack_damage = front_arm.attackDamage + back_arm.attackDamage
```

Avoid complex hidden formulas in the first slice. The player should understand why a zombie works or fails.

## AI Asset Prompt Template

Use a strict prompt like this for production attempts:

```text
Create one modular 2D game sprite body part for a right-facing side-view zombie paper-doll rig.

Slot: [head / torso / front_arm / back_arm / front_leg / back_leg]
Theme: [plague / brute / runner]

Canvas: 512x512 transparent PNG.
Camera: consistent right-facing side view, slight three-quarter depth only.
Style: dark fantasy hand-painted 2D game sprite, readable silhouette, detailed but clean.
Lighting: top-left soft light.
Scale: must match a humanoid zombie whose feet stand on y=430 and body center is x=256.
Attachment points must match the zombie_side_v1 rig.

Do not include background, floor, shadow, labels, text, frame, full body, extra limbs, extra heads, weapons unless they are part of this slot, or cropped edges.

The part must fit with other modular zombie parts and must not depend on matching parts from the same set.
```

For better consistency, generate against a visible template sheet or manually align after generation.

## Quality Gate For Parts

Before accepting a part:

- Composite it with all three torsos or all three heads relevant to its slot.
- Check for neck gaps.
- Check shoulder overlap.
- Check hip alignment.
- Check feet on ground line.
- Check silhouette at battle size.
- Check that the part still reads when tinted, damaged, or partially covered by effects.

A part is not production-ready if it only looks good in the original full matched zombie.

## Recommended Implementation Order

1. Build a static zombie assembler that layers six PNG parts.
2. Add metadata-driven part selection.
3. Add simple stat aggregation.
4. Build one lane battle with placeholder rectangles or rough sprites.
5. Connect assembled zombie stats to battle behavior.
6. Add rewards and unlocks.
7. Replace placeholder parts with first production-quality modular set.
8. Add polish only after the loop is playable.

## Success Criteria

The concept is working if:

- A player can build visibly different zombies from parts.
- Different bodies perform differently in automatic fights.
- Combat results make the player want to adjust the design.
- The asset pipeline can produce new parts without redrawing full zombies.
- The first 18 parts can be mixed without obvious attachment failures.

If the modular rig is unreliable, reduce visual ambition before increasing content. The whole project depends on reusable body parts.
