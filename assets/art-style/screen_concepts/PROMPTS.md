# Screen Concept Prompts

## V2 Cleaner Mockups

Files:

```text
lab_builder_inventory_concept_02_clean.png
battle_screen_rts_spells_concept_02_clean.png
```

Status: `reference_candidate`

Goal:

- Replace the previous dense illustrated screen concepts with cleaner production-readability mockups.
- Show actual screen composition that could be copied into Unity.
- Keep lab and battle cameras visibly different.

Assessment:

- Lab V2 is much closer to a usable builder layout: clear inventory, central zombie construction board, selected-part panel, and bottom action strip.
- Battle V2 is much closer to a playable RTS/autobattle view: fewer squad groups, clearer battlefield spacing, and a readable spell bar.
- Both still contain more decorative detail than final production should use, especially UI borders and battlefield texture.
- Treat these as direction references, not production UI or final style lock.

Next prompt changes:

```text
Even flatter UI panels, fewer decorative border details, larger negative space, lower terrain texture density, more placeholder-like production mockup, less finished illustration.
```

## Lab V2 Prompt Summary

```text
Clean production readability mockup for a necromancer autobattler lab builder screen. Simple usable game UI, not splash art. One large side-view modular zombie preview in the center, one inventory panel on the left with 12-16 large corpse-part cards, one selected-part stats panel on the right, one bottom action/resource bar. Dark gothic UI, restrained detail, large readable shapes, plain panel interiors, no fake text, no dense ornament, no tiny icons, no busy background.
```

## Battle V2 Prompt Summary

```text
Clean production readability mockup for a necromancer autobattler RTS battle screen. Old-RTS high-angle orthographic battlefield, broad readable terrain patches, 3-5 zombie squad groups versus 3-5 human enemy squad groups, two spell effects maximum, one bottom spell bar with five large icon cards. Simple dark gothic UI, readable unit silhouettes, low terrain texture density, no fake text, no dense illustration detail, no huge unit crowd, no ornate border on every element.
```

## V3 Graphic Mockups

Files:

```text
lab_builder_inventory_concept_03_graphic.png
battle_screen_rts_spells_concept_03_graphic.png
```

Status: `superseded_reference_candidate`

Assessment:

- Kept the readable V2 structure.
- Moved somewhat closer to the big-shape gothic direction.
- Still looked too much like rendered game UI/RTS screenshot styling rather than the approved flat graphic reference.
- Superseded by V4, which uses the explicit approved style reference.

## Approved Style Reference

File:

```text
../references/approved_graphic_big_shape_style_reference.png
```

Use this as the current visual style target for screen concepts and future asset prompts.

Key style traits:

- Thick black ink outlines.
- Hard angular silhouettes.
- Large flat shadow blocks.
- Limited palette.
- Low rendering and low texture.
- Quiet empty areas.
- Simple gothic UI frames with plain interiors.
- Strong PC-screen readability.

## V4 PC Style Reference Mockups

Files:

```text
lab_builder_inventory_concept_04_pc_style_ref.png
battle_screen_rts_spells_concept_04_pc_style_ref.png
```

Status: `current_best_screen_reference_candidate`

Goal:

- Preserve V2/V3 screen layout readability.
- Match the approved graphic big-shape style reference more directly.
- Keep PC 16:9 readability in mind.

Assessment:

- Lab V4 is the strongest current lab screen direction: clear PC layout, large builder preview, restrained panels, and closer zombie/UI style match.
- Battle V4 is closer to the approved style than V2/V3: stronger black outlines, flatter terrain, and more graphic unit treatment.
- Battle V4 still has more individual units and terrain marks than final production should use.
- Both are reference candidates, not final UI or production art.

Next prompt changes:

```text
Use even fewer individual figures per squad, make each squad read as one grouped formation shape, reduce inventory item rendering, simplify terrain marks further, and keep all UI frames closer to the approved reference sheet.
```
