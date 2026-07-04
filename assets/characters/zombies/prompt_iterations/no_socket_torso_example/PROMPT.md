# No-Socket Torso Example 01

## Files

```text
raw_chroma/plague_torso_no_socket_example_01_raw.png
transparent/plague_torso_no_socket_example_01.png
```

## Prompt Goal

Test whether torso generation improves when shoulder sockets are removed entirely and replaced with covered overlap/stump language.

## Assessment

Status: `rig_test_candidate`

Works:

- No clean circular arm socket.
- Shoulder area reads more like a covered stump/overlap mass.
- Strong readable torso silhouette.
- Large shadow blocks and low detail density are closer to the preferred direction.

Problems:

- Torso is still too front/three-quarter; it should be more side-view for the lane battle rig.
- Neck opening shows too much top surface.
- Chest/rib opening is visually strong and may compete with the head and front arm.
- Needs assembly test with arms before it can be treated as production candidate.

Next prompt change:

```text
Make the torso flatter in side profile, less front-facing, with less visible top surface on the neck cut. Keep shoulder joints as hidden overlap stumps covered by arms. Reduce the central rib opening so the silhouette reads before interior detail.
```

