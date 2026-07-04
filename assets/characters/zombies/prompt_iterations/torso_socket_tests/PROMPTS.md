# Torso Socket Prompt Iterations

## plague_torso_03_socket_test

Status: cleanup candidate, not production-ready.

Files:

```text
raw_chroma/plague_torso_03_socket_test_raw.png
transparent/plague_torso_03_socket_test.png
```

What improved:

- The prompt produced torso only.
- No head, arms, hands, legs, or full zombie body were included.
- Shoulder areas read more like sockets than the previous test.
- The big-shape style is still close to the preferred direction.

What failed or needs improvement:

- Still too much side hardware for a universal torso slot.
- Green reagent tube may interfere visually with back-arm swaps.
- Torso has more small surface cuts than ideal.
- Anchor placement still needs manual or Unity validation.
- Output came from chroma-key removal, not true transparent generation.

Prompt lesson:

- The phrase `simple shoulder sockets/overlap zones, not bulky armor caps` helped.
- Next version should say `no side-mounted equipment near shoulder sockets` and move green accents to the chest center only.
- Next version should ask for `plain socket silhouettes` and `large unbroken flesh planes`.

Prompt:

```text
Use case: game-assets
Asset type: Unity 2D modular zombie paper-doll part, torso only, strict rig prompt test
Primary request: Generate plague_torso_03_socket_test as ONE TORSO SLOT ONLY for a Unity modular zombie rig.
Output contract: one body slot only, centered on a 1024x1024 Unity full-canvas sprite coordinate system, right-facing side view with slight three-quarter depth, no other body slots.
Canvas/background: create the torso on a perfectly flat solid #ff00ff chroma-key background for background removal. The background must be one uniform color with no shadows, gradients, texture, floor plane, or lighting variation. Do not use #ff00ff anywhere in the subject. Keep generous empty padding around the torso so no edges are cropped.
Slot: torso only.
Subject: ONLY torso from neck socket to hip socket. No head, no arms, no hands, no legs, no pelvis below hip overlap. Shoulder areas must be simple sockets/overlap zones, not bulky armor caps. Do not draw shoulder pads that belong to arms.
Anchors: neck socket near x=512 y=356, front shoulder socket near x=584 y=460, back shoulder socket near x=448 y=464, hip overlap near x=512 y=650 on the 1024 canvas.
Shape goal: one large readable ribcage/chest mass with simple arm sockets and a hip socket. The torso should support swapped arms and legs.
Overlap rule: shoulders should be plain connection sockets that can hide the top of separate arm sprites. Hips should be a simple lower overlap area for separate leg sprites.
Style reference: match master_style_candidate_03_big_shapes. Graphic hand-drawn gothic 2D game art, bold black ink outline, large readable silhouette, large flat shadow blocks, angular comic-ink shadows, restrained detail, dark bone/rotted flesh/iron palette, controlled necromantic green accent, not painterly, not fully rendered.
Design: plague zombie torso, torn ribcage, rotten grey-green flesh, one small green reagent tube or glow accent on torso only. Large quiet body areas. No full-surface texture.
Detail rule: 70 percent large clean silhouette and shadow, 20 percent secondary material shapes, 10 percent small accents. Keep quiet empty areas. No evenly distributed scratches, no texture noise, no stitches everywhere, no straps everywhere.
Camera: side-scrolling 2.5D game art, right-facing side view with slight three-quarter depth, visible top surfaces only subtly, not isometric, not top-down, not photorealistic.
Reject conditions: no readable text, no watermark, no labels, no frame, no full zombie, no head, no arms, no hands, no legs, no pelvis, no shoulder armor caps, no floor shadow, no cast shadow, no isometric view, no top-down view, no left-facing part, no excessive gore.
```

## plague_torso_04_hidden_back_socket

Status: rejected as production direction.

Files:

```text
raw_chroma/plague_torso_04_hidden_back_socket_raw.png
transparent/plague_torso_04_hidden_back_socket.png
```

What improved:

- Removed the obvious right-edge socket issue from `plague_torso_03_socket_test`.
- Reduced side-mounted equipment.

What failed:

- Created a large visible socket on the opposite side.
- Still communicates "empty arm hole" instead of "arm overlap area."

Lesson:

- Asking for one hidden socket is not enough. The prompt should avoid visible sockets entirely and ask for plain shoulder overlap stumps.

## plague_torso_05_plain_overlap_shoulders

Status: closer, but still not preferred.

Files:

```text
raw_chroma/plague_torso_05_plain_overlap_shoulders_raw.png
transparent/plague_torso_05_plain_overlap_shoulders.png
```

What improved:

- Removed the bad right-side visible socket.
- Shoulders started to read more like overlap masses.
- Reduced mechanical side hardware.

What failed:

- Still shows a dark socket-like shoulder opening.
- Still has more internal wound holes than needed.

Lesson:

- The phrase `no visible arm sockets` helps, but the prompt must also ban `shoulder holes`, `black shoulder tunnels`, and ask for `plain torn-flesh shoulder stumps`.

## plague_torso_06_plain_shoulder_stumps

Status: current best torso prompt result, cleanup candidate.

Files:

```text
raw_chroma/plague_torso_06_plain_shoulder_stumps_raw.png
transparent/plague_torso_06_plain_shoulder_stumps.png
torso_socket_iteration_contact_sheet.png
```

What improved:

- No obvious visible arm socket on the right side.
- Shoulders read as coverable overlap stumps rather than holes.
- Better for modular arm swapping.
- Keeps the preferred big-shape gothic style.

Remaining issues:

- Still has more internal cuts/wounds than ideal.
- Shoulder stump texture may need small Photoshop cleanup.
- Needs real rig assembly with arms before being called production-ready.

Prompt lesson:

- Best wording so far: `plain torn-flesh shoulder stumps/overlap tabs only`, `the separate arm sprites will cover these shoulder stumps in Unity`, `no visible arm sockets`, `no shoulder holes`, `no black shoulder tunnels`.
- For torso generation, visible sockets are a trap. Use overlap stumps instead.
