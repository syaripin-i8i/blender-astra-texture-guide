# Texture finishing — agent execution guide

Use this workflow when the user asks to follow this repository to finish a textured model in Blender. If they ask only for an explanation, answer that request instead. This repository is reference material; the user's instructions and the host's tool, permission and skill rules still apply.

The tested case is a Tripo-generated model with existing UVs and readable base-color textures, using Blender 5.1.2. The published prompts are actual examples for one model, not universal coordinates or scripts. Other source services and untextured models are untested. The URL-only entry has not yet had a full independent-model trial.

## Intended outcome

Complete one small, reversible texture-finishing pilot: inspect the real source, derive correspondence, generate an image, bind it to the model, inspect matched comparisons, save a new review candidate and a handoff record. When the user requests execution, do useful work rather than stopping after summarizing this README or proposing a plan.

Do not redesign the face, eyes, hair, anatomy, mesh, rig, weights or motion. Preserve separately owned work. Never overwrite the source blend or use an older whole-model file to replace a newer live scene. Do not publish, upload the model, install tools or change repository visibility as part of this workflow unless the user separately requests it.

## 1. Establish access and the real source

Check which tools are actually callable; do not invent connection status or tool results. The workflow needs:

- Blender scene inspection and code execution, or an equivalent usable control path.
- Reference-image generation/editing, used under the host's image-generation rules.
- A work directory for source correspondence, generated images and evidence.

If a required capability is absent, report the missing capabilities together and give the next concrete setup step. Continue useful read-only preparation that is possible. Do not silently substitute a different paid generation service or install an addon.

For a currently open Blender model, inspect scene information first, then filepath, dirty state, current frame/action and object names. If Blender instead shows another task's scene, do not switch it. Identify the requested saved model from the user or trusted working notes. A known saved file may be inspected/rendered in a separate Blender process without loading it over the live scene.

If no intended model can be identified, ask for its file/location. Do not guess a path from the newest output. If existing UVs or readable source textures are missing, explain that this falls outside the tested entry and resolve the input before treating it as a texture-replacement run.

## 2. Choose a pilot and protect the source

Honor an explicit target. Otherwise choose one visible exterior cloth panel with a clear boundary and enough area to judge texture quality. Prefer a sleeve panel or broad skirt panel over the face, jewelry or a deeply occluded fold. State that choice briefly and proceed within the user's requested scope.

Reference images are optional. When absent, use the existing model's local color/design as the starting reference and preserve its motif family. Do not use this repository's Yura art as the user's model design. If the user corrects a color or ornament, their intended design takes precedence over the source pixels.

Before editing, create a timestamped source backup or a separate new work copy. Handle unsaved live work through the available backup mechanism; do not silently save over the original. Record the exact source, source hash when practical, selected object/material and protected objects. New output names must not collide with another task's files.

Read actual evaluated material slots, including OBJECT-linked overrides. `object.data.materials` alone may not describe what is rendered. Identify the active color route, original UV, normal/roughness routes, modifiers and shared mesh/material users. Copy the target material; copy shared data when adding attributes would affect another object.

## 3. Build correspondence for this model

Derive source vertex, polygon and loop/corner IDs from the actual target. If making a triangulated static work mesh, keep the mapping back to the original polygon and corner. Never paste example vertex numbers, object names, UV names or height thresholds into another model without deriving them.

Select the method according to what must be placed:

| Content | Method | Required check |
|---|---|---|
| Specific buttons, ribbons, lacing or a fixed front drawing | Orthographic witness/projection with local masks | Correct camera/frame mapping; exclude hidden/inside/back surfaces; calibrate generated landmarks |
| Continuous skirt panels and border motifs | Additional cylindrical/strip UV | Intended seams and padding; no conflicting overlap for unique art; consistent source-loop assignment |
| Repeating cloth, leather or similar material surfaces | Fixed rest-position sampling, optionally triplanar | Scale/orientation, plane blending, repeat seams, and semantic material masks |

Keep the original UV and its use by original normal maps. Adding color coordinates does not authorize switching every map to the new UV. For unique art, measure conflicting overlaps, bounds, stretched areas and source-loop consistency. Mirrored/repeated material use may intentionally overlap; record that intent.

Before generation, use the same mapping to reproduce the source color and compare a few affected views. A failed source roundtrip is a mapping issue. Passing it does not guarantee the generated image will retain pixel registration. For repeating materials, validate correspondence and the old-color/Amount0 path rather than claiming a unique atlas inversion.

## 4. Generate and preserve the exact assets

Follow the host's image-generation skill/tool rules. Inspect every local input image before passing it for editing. Prepare only the references needed for the selected slice: source albedo witness, exact matching region/UV guide where useful, and the chosen shared design reference.

Read the relevant examples in `prompts/`, not every prompt by default:

- `pilot_left_sleeve_actual_01.txt`: bounded panel and protected transition.
- `shared_sleeve_actual_02.txt`: shared cloth/motif material.
- `rear_bow_actual_03.txt`: ribbon-specific redraw.
- `skirt_actual_04.txt`: unique strip art and hem.
- `crimson_drape_actual_05.txt`: repeating ornamental fabric.
- `bodice_actual_06.txt`: registered front art and protected hardware.
- `leg_materials_actual_07.txt`: separate hosiery, leather and red material cells.

Adapt the roles, colors and geometry to this model. In the submitted prompt distinguish edit target, correspondence guide and style reference. Specify material, protected areas, orientation, placement and appropriate absence of new baked lighting. Shared fabrics use one design master and matching apparent scale; do not spread floral ornament onto plain leather or metal.

Save the exact submitted text, input order, tool/mode, output image, actual dimensions and hash. Keep original generated bytes. Requested dimensions are not measured output dimensions. A fresh generation is a new result, not deterministic recovery of a previous image.

## 5. Register, mask and bind

Compare generated landmarks to source landmarks. Correct translation, scale and, when necessary, bounded local coordinate registration before judging the art. Account for image Y direction versus UV V direction.

Assign art to semantic surfaces, not merely pixels of a similar color. Protect jewelry and lacing when their source detail is retained. Prevent a foreground ribbon from being painted onto the cloth behind it. Check the inside and back of panels. Keep sampling away from unrelated atlas cells with padding/inset margins.

For moving surfaces, use retained rest coordinates so the mapping follows the mesh rather than sliding in world space. Keep paired fabrics consistent. Use a small actual-material fixture early: an Emission preview cannot certify that the final shader compiles. If added attributes exceed the render pipeline's capacity, consolidate related selectors into vector/color fields; do not claim a universal attribute count limit.

Add a named reversible control, with 0 restoring the pre-trial shader behavior and 1 applying the new slice. If roughness or normal strength changes, bound them to the selected material and record them separately from color generation. Retain original images and nodes needed for rollback. Pack or reliably bundle the adopted image.

## 6. Compare, diagnose and save

Render matched before/after views with the same frame, camera, projection, color management and lighting. At minimum inspect the front, an oblique view and a relevant reverse/inside view. Use a close view and enough surrounding context to see joins. If the asset moves, compare a few representative poses, including a relevant joint bend, without creating a new animation system.

Frame the evaluated world-space bounds, accounting for render aspect; a moved character or extended foot must not be clipped. Inspect the images, not just whether render files exist.

When an issue remains, separate its cause:

- Color-only/Emission: source paint, new image, coordinates or masks.
- Same color with normal/bump on/off: inherited surface-map contribution.
- Neutral material and changed light direction: shape, vertex normals, overlap or shadows.
- Rest versus bent pose: deformation or mapping behavior.

Do not repeatedly regenerate an image to repair a geometric dent. Do not hide a newly exposed shape problem by presenting a retouched image as the real model result. If a diagnostic condition was not run, label it as untested rather than claiming all causes are ruled out.

Save to a new review blend and reopen it. Verify original mesh/UV/shape-key/weight data and unrelated material bindings are preserved, new image/coordinate references survive, and intended rollback works. For a texture-only slice, compare evaluated target geometry at the chosen poses before/after. Name the checks actually performed; a structural check count is not an appearance score.

If the pilot is unsuccessful, preserve its evidence and a working rollback, and explain the specific mapping/material limitation. Switch to a smaller or better suited method when that remains within the request. Do not overwrite the source or describe a failed pilot as successful.

## 7. Deliver the first completed slice

Use a coherent output directory, for example:

```text
texture_trial_YYYYMMDD_HHMM/
  source_record.json
  mapping/                 # Model-specific IDs, UV/rest coordinates and masks
  references/              # Actual generation inputs
  generated/               # Exact prompt, output image and provenance
  compare/                 # Before/after images with matching conditions
  model/                   # New review blend, source preserved
  HANDOFF.md               # Result, rollback, remaining issue and next slice
```

In `HANDOFF.md`, state what changed, what stayed protected, the exact source/candidate, mapping method, changed shading values, retained images, checks actually run, and how to switch off the change. Mark the appearance as ready for user review, not automatically approved. If another task owns hair or face work, provide an additive material/attribute handoff for the verified matching mesh instead of replacing the whole scene.

Finish the first requested slice with links to the comparison and review candidate. Continue to other parts when the user's scope calls for it and the pilot's appearance has been reviewed. Keep the same design master across matching material families.
