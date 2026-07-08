---
name: image-prompt-library
description: Maintain an image prompt library and its static HTML gallery dashboard: add referenced images into numbered library folders, create prompt.md metadata, update viewer/catalog.js, generate or update viewer/index.html, viewer/styles.css, and viewer/app.js, manage source records, assign or create article_style_profile entries, keep style_profiles/*.md reusable prompts, and preserve grouped gallery behavior. Use when the user asks to add images, continue maintaining an image prompt library, classify visual style, organize same-article visual styles, generate an image library dashboard, or update a gallery/viewer for this library structure.
---

# Image Prompt Library

Use this skill for a local image prompt library with `library/`, `style_profiles/`, and optional static `viewer/` folders.

## Core Workflow

1. Inspect the current `library/` directories and choose the next six-digit id.
2. Copy each provided image into `library/<id>/image.png`.
3. Create `library/<id>/prompt.md` with frontmatter and sections matching the existing library.
4. Record provenance in `source`.
5. Assign `article_style_profile` by visual compatibility, not content topic.
6. If no existing style profile fits, create `style_profiles/<profile-id>.md`.
7. Update `viewer/catalog.js` with the same metadata.
8. Create or update static viewer files when requested or when the library already has a viewer.
9. Validate that `viewer/catalog.js` parses and that all new files exist.

## Required Metadata

Each `prompt.md` must include:

```yaml
---
title: ""
tags: []
created: YYYY-MM-DD
source:
  type: document | web | image | slide | generated | other
  title: ""
  url: ""
  path: ""
article_style_profile: profile-id
---
```

Omit empty optional source fields when appropriate.
Do not include private local paths, personal information, credentials, or unpublished source details unless the user explicitly wants them recorded in their private library.

## Article Style Profiles

`article_style_profile` is a reusable visual-language prompt, not a content category. It answers:

> Can this image appear in the same article or deck as other images using this profile without feeling visually inconsistent?

Store profile prompts under `style_profiles/<profile-id>.md`. Read existing profiles before creating a new one.

Use existing profiles when present and compatible:

- `flat-technical-manual`: flat 2D technical manual / safety guide style.
- `blueprint-training-slide`: blueprint-inspired technical slide style.
- `hand-drawn-safety-card`: hand-drawn educational safety card style.
- `black-line-installation-manual`: monochrome installation manual line art.

Create a new profile only when the image would feel visually out of place in all existing profiles.

## Viewer Rules

The static viewer may include `viewer/index.html`, `viewer/styles.css`, `viewer/app.js`, and `viewer/catalog.js`.

Default viewer behavior:

- `All`: show all images in library order.
- `分组`: show all images grouped by `articleStyleProfile`.
- Cards use fixed-size dashed image frames.
- Images fit proportionally inside frames using contain behavior.
- Lightbox/details view may show image, title, tags, visual style, prompt, notes, and optional source metadata.
- Source metadata may be hidden in the UI while retained in data if the user wants a cleaner screenshot.

When adding a new profile, add its label to `styleProfileLabels` in `viewer/app.js`.

## References

For fuller conventions and examples, read `references/library-rules.md` only when needed.
