# Image Prompt Library

A Codex skill for maintaining image prompt libraries with numbered image entries, reusable visual style profiles, source metadata, and a static HTML gallery dashboard.

## What It Does

This skill helps Codex maintain an image prompt library by:

- Adding referenced images into numbered `library/000001/` folders
- Creating `prompt.md` metadata files
- Recording source metadata for images
- Assigning reusable `article_style_profile` values
- Managing reusable `style_profiles/*.md` prompts
- Updating `viewer/catalog.js`
- Generating or maintaining a static HTML gallery viewer
- Keeping `All` and grouped gallery views consistent

## Expected Library Structure

```text
library/
  000001/
    image.png
    prompt.md

style_profiles/
  flat-technical-manual.md

viewer/
  index.html
  styles.css
  app.js
  catalog.js
