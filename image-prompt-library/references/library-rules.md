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
  index.html
  styles.css
  app.js
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

## Static HTML Viewer

The skill may generate or maintain a static dashboard under `viewer/`.

Recommended files:

```text
viewer/
  index.html   # page structure
  styles.css   # layout, cards, fixed frames, lightbox
  app.js       # search, size switcher, all/grouped views, copy button
  catalog.js   # image metadata
```

Recommended behavior:

- `All`: show all images in catalog order.
- `分组` or `Grouped`: show all images grouped by `articleStyleProfile`.
- Search filters by id, title, tags, prompt, notes, source, and style profile label.
- Size switcher changes card width while keeping all image frames identical within that mode.
- Card image frames use a fixed aspect ratio, usually 4:3.
- Images use proportional `contain` scaling; never crop library images just to fit the viewer.
- Long titles, source strings, and prompts must wrap instead of widening cards.
- Lightbox/details view should show the full image and metadata.
- Source metadata can be retained in `catalog.js` but hidden in the UI for screenshots.

Recommended CSS ideas:

```css
.gallery-medium {
  grid-template-columns: repeat(auto-fill, 260px);
}

.image-frame {
  width: 100%;
  aspect-ratio: 4 / 3;
  display: grid;
  place-items: center;
}

.image-frame img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
```

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
5. If viewer files changed, run a lightweight syntax check such as `node -c viewer/app.js`.

## Public Release Hygiene

When preparing this skill for publication, include only the skill files:

```text
SKILL.md
agents/openai.yaml
references/library-rules.md
```

Do not include a user's `library/`, generated images, private source PDFs, local filesystem paths, or project-specific data.
