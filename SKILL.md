---
name: photo-retouch-pro
description: Retouch existing photos with identity and detail preservation. Use for natural cleanup, object removal, background or clothing replacement, enhancement, outpainting, relighting, closed-eye correction, garment smoothing, and removing elements from the user's designs. Supports 精修、换背景、换装、扩图、修闭眼 and prompt-only requests.
---

# Photo Retouch Pro

Turn a photo-edit request into a tightly scoped edit, using one or more of the ten modes in [references/modes.md](references/modes.md). The default is natural photographic realism. A request to write or improve a prompt ends with a prompt; a request to edit an image proceeds to editing when an image-editing tool is available.

## Establish the edit

- Inspect the supplied image before editing. For a local file, use the environment's image viewer. If the image is missing, ask for the image or an accessible path; do not invent its appearance.
- Identify the edit target and distinguish the base image from identity, clothing, or background references. Ask only when ambiguity would change the result, such as two people matching an unspecified target.
- Infer the applicable modes from natural language; users do not need to select a number. Read the matching sections of `references/modes.md`.
- Define what may change and what must stay. An explicit requested change overrides the corresponding default lock: replacing clothes unlocks clothes, relighting unlocks illumination, and so on. Preserve the rest.
- Preserve the source aspect ratio and framing unless the user asks for expansion, cropping, or a specific output ratio. Do not silently crop to satisfy a tool's default canvas.

## Default preservation rules

Preserve identity, facial geometry, age cues, skin tone, body proportions, hair, pose, expression, clothing, accessories, background, composition, and legible text except the properties explicitly targeted. Do not add beauty reshaping, a younger face, body slimming, skin whitening, makeup, or new styling to a generic request for professional retouching.

Keep pores, fine skin lines, fabric grain, seams, and physically plausible shadows. Remove temporary minor blemishes only where consistent with the request. Keep distinctive moles, scars, tattoos, and other identifying features unless their removal is requested.

For existing illustrations or designs, preserve their original medium and style; do not force them into photography.

## Build and perform the edit

Combine the selected mode with a concise editing brief:

```text
Base image: [which input]
Requested changes: [specific regions and properties]
Preserve: [all important unedited properties]
Reference roles: [only if references exist]
Integration: [lighting, shadow, reflection, perspective, texture, edge conditions]
Output: [aspect ratio, size and format when specified]
Avoid: [failure modes specific to this edit]
```

Use the host's image-editing tool and attach the actual base image. In Codex, prefer the built-in image-generation/editing capability (such as `image_gen.imagegen`) and local reference paths when supported. Follow the host's tool contract; do not assume parameters, maximum resolution, masks, or transparent output are supported. Do not silently switch to a paid external API or require an API key for prompt creation.

If only prompt output is possible, provide the completed prompt and explain that no edited image was generated. Do not present a prompt as a finished image.

For multiple changes, combine compatible edits in one request to reduce identity drift. For dependent edits, perform scene or geometry changes before finishing and upscaling. Keep the original image as the identity anchor across passes. Do not apply all ten modes automatically.

## Precision and resolution

- Local generative edits do not guarantee unchanged pixels outside the target. If exact preservation is required, use a supported mask or composite the edited region over the original with suitable tooling. If unavailable, state the limitation before promising exact preservation.
- Enhancement is not recovery of unknowable detail. Do not invent readable text, faces, logos, jewelry engravings, or other details hidden by severe blur.
- For "8K", agree on or infer explicit dimensions: normally a 7680-pixel long edge with the original ratio preserved; UHD 8K specifically means 7680 x 4320. Honor explicitly provided dimensions instead.
- Verify exported pixel dimensions. When the editing tool cannot output the requested size, distinguish native generation from a separately supported upscale. Offer a feasible output and report its actual dimensions; never label a smaller output "8K".
- For closed eyes, prefer a clearly identified open-eye reference of the same person. Without one, make a conservative plausible correction and disclose that unseen eye details are inferred; do not assert their real eye color or exact shape.

## Check and deliver

Inspect the result against the original and the selected mode. Check identity, hands, contours, hair edges, nearby text, pattern repetition, perspective, contact shadows, and reflections where relevant. Look especially for seams, halos, duplicate objects, flat fabric, waxy skin, and overly sharp invented details.

When a visible defect remains, make a focused correction, preserving the base identity reference. Avoid unbounded regeneration: after two unsuccessful corrective attempts, report the unresolved defect with the best available result rather than claiming success.

Save a new file, for example `portrait-retouch-v1.png`, in the requested folder or project output folder. Do not overwrite the original unless explicitly requested. Preserve transparency when present unless the task changes it.

Return the edited image or its usable file link, actual dimensions when verified, a short description of changes, and any material limitation. Do not claim checks that were not performed. Do not publish photos or upload them to GitHub merely because this skill itself is hosted there.
