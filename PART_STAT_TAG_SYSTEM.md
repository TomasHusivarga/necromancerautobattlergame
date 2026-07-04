# Part Stat Tag System

This spec defines how modular zombie parts create battle behavior, role identity, and visual signals. The player does not choose fixed classes. A zombie becomes a tank, healer, mage, archer, support, runner, brute, or hybrid because of the parts equipped.

## Design Goal

The system must support weird hybrid builds without requiring unique rules for every combination.

Core rules:

- Parts provide stats, tags, active abilities, passive effects, and visual signals.
- Roles emerge from the total build.
- The lab preview shows the exact modular zombie.
- The battle sprite simplifies the design into readable squad-scale visual signals.
- Formulas should stay simple enough that the player understands why a design works or fails.

Example:

```text
shield arm + healing staff arm + heavy torso = tank healer
intelligence torso + healing staff arm + relic arm = pure healer
bow arm + relic arm + runner legs = ranged support
```

## Core Stats

Use these as the main part stats.

| Stat | Meaning | Usually Comes From |
|---|---|---|
| `strength` | Physical power, melee damage, knockback | Arms, brute torsos |
| `vitality` | Health, regeneration, survival | Torsos, legs, mutations |
| `armor` | Flat damage reduction and front-line durability | Torsos, shield arms, bone parts |
| `dexterity` | Attack speed, ranged accuracy, dodge-like behavior | Legs, bows, light arms |
| `intelligence` | Spell damage, healing strength, status scaling | Heads, caster torsos, staff arms |
| `focus` | Cooldown recovery, aura strength, support consistency | Heads, relics, support parts |
| `speed` | Movement and engage speed | Legs, runner parts |
| `stability` | Knockback resistance, line holding, shield reliability | Legs, heavy torsos, shields |

Keep these stats visible in the lab through icons/bars, not a spreadsheet wall.

## Derived Battle Stats

Derived stats are calculated from core stats and abilities.

| Derived Stat | Use |
|---|---|
| `health` | Total hit points |
| `damage` | Basic attack or ability damage |
| `attackSpeed` | Attacks per second or attack cooldown |
| `range` | Attack or cast range |
| `cooldownReduction` | Reduces active ability cooldowns |
| `healingPower` | Increases healing and regeneration effects |
| `spellPower` | Increases spell, AoE, and status effect strength |
| `controlCost` | Spawn/control budget cost |

MVP formula rules:

```text
base stats = sum(all equipped part stats)
final_speed = average(front_leg.speed, back_leg.speed) + other speed bonuses
health = 20 + vitality * 10
damage = active ability base damage + scaling stat
healingPower = intelligence + focus
spellPower = intelligence + focus * 0.5
cooldownReduction = focus * small tuning value
controlCost = sum(part controlCost values)
```

These formulas are starting rules, not final balance. Avoid hidden multipliers until the game needs them.

## Slots

Each slot has a mechanical job and a visual job.

| Slot | Mechanical Responsibility | Visual Signal |
|---|---|---|
| `head` | Targeting, intelligence, focus, behavior modifiers | Face, eyes, caster/scout/brute identity |
| `torso` | Vitality, armor, archetype mass, core scaling | Body size, toughness, caster body, plague body |
| `front_arm` | Main active ability by default | Primary weapon/tool silhouette |
| `back_arm` | Offhand, shield, relic, secondary utility, passive support | Secondary tool, shield, relic, banner |
| `front_leg` | Speed, stability, stride silhouette | Movement type, front readable leg |
| `back_leg` | Speed, stability, movement support | Secondary movement type |
| `mutation` | One rule-changing effect or overlay | Color tint, aura, growth, VFX marker |

## Tags

Tags are used for role detection, tooltips, battle visual mapping, and future content filters.

Initial tags:

```text
tank
melee
ranged
healing
support
caster
plague
bone
shield
relic
bow
staff
runner
brute
```

Tag rules:

- A part can have multiple tags.
- Tags should describe what the part does and what it should visually communicate.
- Tags should not hide important effects. If a tag changes gameplay, the UI needs an icon or tooltip.
- Do not create many near-duplicate tags early.

## Ability Rules

Active abilities usually come from tools and arms.

Default priority:

1. `front_arm` grants the main active ability.
2. `back_arm` grants offhand defense, utility, relic boost, or a secondary attack.
3. `head` modifies targeting or scaling.
4. `torso` modifies durability, archetype scaling, or aura capacity.
5. `legs` modify movement, stability, and engage behavior.
6. `mutation` adds one visible rule-changing effect.

Examples:

| Part Type | Common Ability Pattern |
|---|---|
| Claw arm | Melee attack, bleed/plague on hit, cleave |
| Shield arm | Block, taunt, armor aura, damage reduction |
| Healing staff arm | Heal bolt, heal pulse, regeneration |
| Bow arm | Ranged attack, armor-piercing shot |
| Mage staff arm | AoE blast, plague cloud, bone spike |
| Relic arm | Passive spell/heal boost, aura, cooldown support |
| Brute torso | Health/armor scaling, knockback resistance |
| Scholar torso | Intelligence/focus scaling, lower vitality |

## Role Detection

Roles are labels inferred from stats and tags. They help the UI explain the build and help battle art choose simplified visual signals.

| Role Label | Detection Pattern |
|---|---|
| Tank | High `vitality`, `armor`, `stability`, or `shield` tag |
| Healer | `healing` tag plus high `intelligence` or `focus` |
| Mage / AoE | `caster` or `staff` tag plus high `intelligence` and AoE ability |
| Archer | `ranged` and `bow` tags, often high `dexterity` |
| Runner / Assassin | High `speed` and `dexterity`, low `vitality` |
| Support | `support` or `relic` tag, focus/aura/passive utility |
| Brute | `brute` tag, high `strength`, high `vitality`, low speed |
| Plague Carrier | `plague` tag, plaguePower/status ability |

Hybrids should be expected. A build can show two role labels:

```text
primary role = strongest role score
secondary role = second strongest role score if close enough
```

Examples:

- `Tank Healer`
- `Archer Support`
- `Plague Runner`
- `Brute Caster`

## Battle Visual Mapping

The lab view shows exact parts. The battle view should simplify the build so squads stay readable.

Battle visual recipe:

```text
body mass = torso family + vitality/armor
main silhouette = front_arm ability/tool
offhand silhouette = back_arm tag/tool
movement silhouette = leg speed/stability
overlay = mutation/family/status color
role icon or aura = strongest role tags
```

Do not require every lab part detail to appear in the battle sprite. Preserve the readable identity:

- Shield equipped: show shield or block silhouette.
- Healing staff equipped: show staff glow or healer aura.
- Bow equipped: show ranged bow silhouette.
- Relic equipped: show relic/offhand icon, banner, or aura.
- Runner legs: show leaner faster movement silhouette.
- Brute torso: show heavier body mass.
- Plague tags: show green plague accent.

## Example Part Definitions

These are design examples, not final balance numbers.

```json
{
  "id": "grave_shield_arm_01",
  "slot": "back_arm",
  "family": "bone",
  "tags": ["tank", "shield", "support"],
  "stats": {
    "armor": 3,
    "stability": 4,
    "vitality": 1,
    "speed": -1,
    "controlCost": 2
  },
  "activeAbility": null,
  "passives": ["block_chance_small", "frontline_guard"],
  "visualSignals": ["shield", "heavy_offhand", "tank"]
}
```

```json
{
  "id": "healing_staff_arm_01",
  "slot": "front_arm",
  "family": "plague",
  "tags": ["healing", "staff", "caster", "support"],
  "stats": {
    "intelligence": 3,
    "focus": 2,
    "strength": -1,
    "controlCost": 2
  },
  "activeAbility": "heal_bolt",
  "scalesWith": ["intelligence", "focus"],
  "visualSignals": ["staff", "green_heal_glow", "caster"]
}
```

```json
{
  "id": "relic_carrier_arm_01",
  "slot": "back_arm",
  "family": "bone",
  "tags": ["relic", "support", "caster"],
  "stats": {
    "focus": 4,
    "intelligence": 1,
    "stability": -1,
    "controlCost": 2
  },
  "activeAbility": null,
  "passives": ["spell_power_small", "healing_power_small"],
  "visualSignals": ["relic", "aura", "support"]
}
```

```json
{
  "id": "scholar_ribcage_torso_01",
  "slot": "torso",
  "family": "plague",
  "tags": ["caster", "support"],
  "stats": {
    "intelligence": 5,
    "focus": 3,
    "vitality": -1,
    "armor": 0,
    "controlCost": 2
  },
  "passives": ["ability_scaling_small"],
  "visualSignals": ["thin_caster_body", "glowing_ribs"]
}
```

```json
{
  "id": "runner_legs_01",
  "slot": "front_leg_or_back_leg",
  "family": "runner",
  "tags": ["runner"],
  "stats": {
    "speed": 5,
    "dexterity": 2,
    "stability": -2,
    "vitality": -1,
    "controlCost": 1
  },
  "passives": ["fast_engage"],
  "visualSignals": ["lean_legs", "fast_stance"]
}
```

```json
{
  "id": "bone_bow_arm_01",
  "slot": "front_arm",
  "family": "bone",
  "tags": ["ranged", "bow"],
  "stats": {
    "dexterity": 4,
    "strength": 1,
    "stability": -1,
    "controlCost": 2
  },
  "activeAbility": "bone_arrow",
  "scalesWith": ["dexterity"],
  "visualSignals": ["bow", "ranged_stance"]
}
```

## Example Builds

### Tank Healer

```text
torso: brute_torso_01
front_arm: healing_staff_arm_01
back_arm: grave_shield_arm_01
front_leg: armored_front_leg_01
back_leg: armored_back_leg_01
head: focus_head_01
```

Result:

- Key stats: high vitality, armor, stability, medium intelligence/focus.
- Tags: `tank`, `shield`, `healing`, `staff`, `support`.
- Behavior: holds the line and casts small heals.
- Battle visual: heavy body, shield silhouette, staff glow, green support aura.

### Pure Healer

```text
torso: scholar_ribcage_torso_01
front_arm: healing_staff_arm_01
back_arm: relic_carrier_arm_01
legs: slow_safe_legs
head: focus_head_01
```

Result:

- Key stats: high intelligence, high focus, low armor.
- Tags: `healing`, `staff`, `relic`, `support`, `caster`.
- Behavior: heals from backline, weak if reached.
- Battle visual: thin caster body, staff, relic glow, larger healing aura.

### AoE Mage

```text
torso: scholar_ribcage_torso_01
front_arm: plague_staff_arm_01
back_arm: relic_carrier_arm_01
legs: basic_shambler_legs
head: mage_skull_head_01
```

Result:

- Key stats: high intelligence/focus, medium speed, low armor.
- Tags: `caster`, `staff`, `plague`, `relic`.
- Behavior: casts plague cloud or bone spike AoE.
- Battle visual: staff silhouette, purple/green cast effect, caster squad marker.

### Archer Support

```text
torso: light_ribcage_torso_01
front_arm: bone_bow_arm_01
back_arm: relic_carrier_arm_01
legs: runner_legs_01
head: scout_head_01
```

Result:

- Key stats: high dexterity, high focus, high speed, low durability.
- Tags: `ranged`, `bow`, `support`, `relic`, `runner`.
- Behavior: fires from behind front line and supports cooldowns or buffs.
- Battle visual: bow silhouette, lean formation, small relic/aura accent.

### Fast Plague Runner

```text
torso: plague_torso_01
front_arm: claw_arm_01
back_arm: spitter_arm_01
legs: runner_legs_01
head: plague_head_01
mutation: infectious_01
```

Result:

- Key stats: high speed, plague power, low armor.
- Tags: `runner`, `plague`, `melee`.
- Behavior: reaches enemies quickly and spreads plague.
- Battle visual: lean fast body, green claws/spit, plague trail accent.

## MVP Rules

- One main active ability per zombie is enough for the first prototype.
- More passive effects are allowed, but each must be visible or explainable.
- Avoid hidden synergies until the basic system is fun.
- Avoid hard counters that make a build useless.
- Prefer clear tradeoffs: slow but durable, fast but fragile, strong healing but weak damage.

## Unity Data Direction

Future Unity data can use one `PartDefinition` shape:

```json
{
  "id": "part_id",
  "slot": "front_arm",
  "family": "bone",
  "tags": ["ranged", "bow"],
  "stats": {
    "strength": 0,
    "vitality": 0,
    "armor": 0,
    "dexterity": 4,
    "intelligence": 0,
    "focus": 0,
    "speed": 0,
    "stability": -1,
    "controlCost": 2
  },
  "activeAbility": "bone_arrow",
  "passives": [],
  "visualSignals": ["bow", "ranged_stance"]
}
```

The same data should drive:

- Lab stat panel.
- Zombie role labels.
- Battle behavior.
- Battle visual recipe.
- Result screen explanations.

