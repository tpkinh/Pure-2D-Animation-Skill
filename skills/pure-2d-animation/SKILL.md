---
name: pure-2d-animation
description: Redraw supplied images in the project's locked South Asian historical storybook-comic style: clean tapered ink, believable adult anatomy, controlled expressive caricature, jewel-tone costumes, ornate period detail, luminous 2D coloring, and atmospheric backgrounds. Use for narrative scenes, portraits, character sheets, and illustrated or bilingual book spreads. Do not use for photorealism, 3D renders, minimalist flat icons, generic anime, or vector-only asset editing.
---

# Historical Storybook 2D

Convert the complete input image—not only its characters—into one coherent historical storybook illustration while preserving the source narrative.

## Required workflow

1. Inspect every supplied image before editing. Treat each image as a separate edit target unless the user explicitly requests a composite or page spread.
2. Identify the output mode before prompting: narrative scene, character portrait, character sheet, or illustrated/bilingual book spread. Then identify every character, identity cue, action, relationship, emotion, costume, prop, architectural element, weather effect, foreground/background layer, composition, camera angle, negative-space region, text block, and aspect ratio.
3. For every face, record age, adult facial proportions, gaze, eyelid openness, eyebrow angle, mouth shape, emotional intensity, hair/facial-hair silhouette, and role in the scene. Preserve deliberate dramatic expressions rather than neutralizing them.
4. Preserve, in order of priority: narrative meaning → character identity and role → action/relationships → expression → period clothing/props → composition → text and page layout → aspect ratio.
5. Read [references/style-lock.md](references/style-lock.md) before preparing the edit prompt or generating an image.
6. Use an image-editing/generation tool with the supplied image as the visual reference. Re-illustrate the entire visual system; do not apply a superficial filter.
7. Review the result against every item in the reference checklist. If it fails, retry with one focused correction while repeating the preservation constraints. Allow at most two correction passes after the first generation.
8. Deliver only a result that passes. If the third attempt still fails, report the remaining defect instead of presenting it as approved.

## Locked output modes

- **Narrative scene:** stage readable relationships, gestures, tears, rain, crowds, architecture, and dramatic story beats; keep focal figures crisp and distant layers atmospheric.
- **Character portrait:** use believable adult proportions, a clear silhouette, controlled facial modeling, detailed culturally specific clothing and jewelry, and an environment that supports rather than competes with the subject.
- **Character sheet:** keep one identity consistent across turnaround views, expressions, poses, clothing, palette, and accessories; use a calm light background and preserve every label exactly.
- **Illustrated/bilingual spread:** preserve page split, text-safe zones, margins, columns, reading order, and wording; place richly rendered scene art around or below the text with lower background contrast behind copy.

## Output handling

- Never overwrite the source image.
- Use the user's requested output folder and filename when provided.
- Otherwise, save the approved image in an `outputs` folder beside the active project artifacts as `<source-name>-storybook-2d.png`.
- If the filename exists, append `-v2`, `-v3`, and so on.
- State where the approved file was saved and confirm that the full-scene checklist passed.

## Scope rule

The style applies to characters, faces, hair, skin, clothing, jewelry, weapons, architecture, crowds, weather, lighting, props, and backgrounds. Foreground characters receive the most line and material detail; distant layers may be softer, hazier, and less detailed to support text and narrative focus.
