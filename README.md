# image-prompt-library

A Codex skill for maintaining image prompt libraries with numbered image entries, source metadata, reusable visual style profiles, and grouped gallery support.

## What It Does

This skill helps Codex maintain an image prompt library by:

- Adding referenced images into numbered `library/000001/` folders
- Creating `prompt.md` metadata files
- Recording image sources
- Assigning reusable `article_style_profile` values
- Managing `style_profiles/*.md`
- Updating `viewer/catalog.js`
- Keeping gallery grouping behavior consistent

## Installation

Copy the `image-prompt-library/` folder into your Codex skills directory:

```text
~/.codex/skills/image-prompt-library/
