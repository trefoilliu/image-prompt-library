# Image Prompt Library Skill

A Codex skill for maintaining image prompt libraries with numbered image entries, reusable visual style profiles, source metadata, and a static HTML gallery dashboard.

## What It Does

This skill helps Codex maintain an image prompt library by adding referenced images into numbered `library/000001/` folders, creating `prompt.md` metadata files for each image, recording image source metadata, assigning reusable `article_style_profile` values, managing reusable visual style prompts in `style_profiles/*.md`, updating `viewer/catalog.js`, creating or maintaining a static HTML gallery viewer, and keeping library order, grouped display, and gallery behavior consistent.

## Expected Library Structure

The expected project structure is:

library/
  000001/
    image.png
    prompt.md
  000002/
    image.png
    prompt.md

style_profiles/
  flat-technical-manual.md
  hand-drawn-safety-card.md

viewer/
  index.html
  styles.css
  app.js
  catalog.js

## Image Entry Format

Each image entry should live in a numbered folder such as `library/000001/`. Each entry should contain `image.png` and `prompt.md`.

A typical `prompt.md` file can include front matter with title, tags, source, and article style profile, followed by prompt text and notes.

Example:

---
title: Example Technical Diagram
tags:
  - technical-illustration
  - safety
source:
  type: document
  name: example-source.pdf
article_style_profile: flat-technical-manual
---

## Prompt

Create a technical safety illustration showing...

## Notes

Use this image for explaining...

## Visual Style Profiles

The skill uses `article_style_profile` to group images that can appear together in the same article, manual, guide, or slide deck without feeling visually inconsistent. This is a visual-language profile, not a content category.

Good profile names describe the look and presentation style, such as `flat-technical-manual`, `hand-drawn-safety-card`, or `blueprint-training-slide`.

Each reusable style profile should be stored under `style_profiles/`.

A style profile can describe overall visual language, layout density, line style, color palette, typography feel, diagram perspective, annotation style, and things to avoid.

Example style profile:

# flat-technical-manual

Use a restrained technical manual style. Prefer flat 2D diagrams, white backgrounds, thin black or gray outlines, simple geometric machinery, blue measurement arrows, dashed construction lines, compact labels, and minimal color accents. Avoid photorealism, dramatic perspective, decorative lighting, marketing-style composition, and polished 3D rendering.

## Static HTML Gallery

This skill can help create or maintain a static gallery viewer. The viewer can support an `All` view that shows every image in library order, a `Grouped` view that shows every image grouped by `article_style_profile`, search by id, title, tags, prompt, notes, source, and style profile, card size switching, fixed-size dashed image frames, proportional image scaling with `object-fit: contain`, lightbox preview, copy prompt button, and optional source metadata display.

The gallery is designed to work as a simple static HTML viewer without requiring a backend.

## Source Metadata

Images can come from different places, such as documents, web pages, screenshots, generated images, internal diagrams, or manually created assets.

Source metadata should record where the image came from without embedding private files or sensitive local paths in public repositories.

Example:

source:
  type: document
  name: example-source.pdf

For private projects, source metadata can be more detailed locally. For public skill repositories, avoid including private documents, personal paths, credentials, or proprietary image data.

## Installation

Copy the `image-prompt-library` skill folder into your Codex skills directory:

~/.codex/skills/image-prompt-library/

The skill folder should contain:

SKILL.md
agents/openai.yaml
references/library-rules.md

If publishing this skill as a GitHub repository, the repository root can contain:

README.md
SKILL.md
agents/
references/

## Usage

Ask Codex to use the skill when maintaining an image prompt library.

Examples:

Use $image-prompt-library to add these images to my image prompt library.

Use $image-prompt-library to classify these images by visual style profile.

Use $image-prompt-library to create a static HTML gallery viewer for this library.

Use $image-prompt-library to update the viewer so images are grouped by visual style.

Use $image-prompt-library to add source metadata to these image entries.

## Design Principles

This skill treats an image prompt library as more than a folder of images. Each image should have a stable numeric id, the actual image asset, a reusable generation prompt, source metadata, tags for searching, notes for future use, and a visual style profile for grouping.

The key idea is that prompts should be reusable in parts: content prompt describes what the image shows, style profile describes how the image should look, source metadata records where the reference came from, and notes explain how the image should be used.

This makes it easier to generate new images that fit an existing article, guide, manual, or slide deck.

## Privacy

This repository should contain only the Codex skill itself.

Do not include private image libraries, source documents, generated image assets, personal filesystem paths, credentials, API keys, or proprietary project data.

Keep real image collections in a separate local workspace or private repository.
