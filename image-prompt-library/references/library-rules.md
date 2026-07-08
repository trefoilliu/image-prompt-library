# Image Library Rules

## Folder Layout

```text
library/
  000001/
    image.png
    prompt.md
style_profiles/
  flat-technical-manual.md
viewer/
  catalog.js
```

## prompt.md Sections

Use the existing simple structure unless the user requests a schema migration:

```md
## Prompt

Content prompt describing what the image shows.

## Notes

Short Chinese note explaining what visual pattern this reference is useful for.
```

Future structured prompts may split this into `Content Prompt`, `Local Style Notes`, and `Full Prompt`, but do not migrate old files unless asked.

## catalog.js Entry Shape

```js
{
  id: "000001",
  title: "",
  image: "../library/000001/image.png",
  promptFile: "../library/000001/prompt.md",
  tags: [],
  created: "YYYY-MM-DD",
  source: { type: "document", title: "" },
  articleStyleProfile: "flat-technical-manual",
  prompt: "",
  notes: ""
}
```

Keep `prompt` concise enough for card preview. Keep full details in `prompt.md`.

## Style Profile Naming

Use style-first names, not content/source-first names.

Good:

- `flat-technical-manual`
- `blueprint-training-slide`
- `hand-drawn-safety-card`
- `black-line-installation-manual`

Avoid:

- `machinery-safety-guide`
- `safety-light-curtain`

## Style Profile File Shape

```md
---
id: profile-id
name: 中文显示名
type: article_style_profile
created: YYYY-MM-DD
---

# 中文显示名

## Prompt

Reusable style prompt.

## Compatibility

What kind of article/deck/manual this can coexist in.

## Works Well For

- Typical image roles.
```

## Validation

After edits:

1. Check each new directory contains `image.png` and `prompt.md`.
2. Parse `viewer/catalog.js` with Node `vm.runInContext`.
3. Confirm the last id and style profile counts.
4. Confirm `viewer/app.js` has a display label for any new profile.

## Public Release Hygiene

When preparing this skill for publication, include only the skill files:

```text
SKILL.md
agents/openai.yaml
references/library-rules.md
```

Do not include a user's `library/`, generated images, private source PDFs, local filesystem paths, or project-specific data.
