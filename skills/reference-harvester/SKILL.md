---
name: reference-harvester
description: Use when gathering and curating reference images or a moodboard from visual ideas, examples, or source material.
---

# Reference Harvester

Build a visually coherent reference library. Success means delivering the requested number of **reviewed, useful images**, not merely downloading that many files.

Use public, user-authorized, or otherwise permitted sources. Do not bypass access controls or remove watermarks. Mention likely reuse restrictions when relevant.

## Workflow

### 1. Establish the target

Inspect supplied images, links, playlists, titles, and existing folders. Infer a short internal visual brief containing:

- core subject
- desired mood and any productive contradiction, such as “horror and comedy”
- recurring visual motifs
- era, texture, palette, and production quality
- composition, framing, and readability requirements
- minimum useful resolution
- target count and output directory

Ask the user only when a missing decision would materially change the result. Infer reversible details.

### 2. Build a search vocabulary

Search beyond the user's literal phrase. Combine:

- proper names, episodes, segments, characters, and creators
- visual motifs and actions
- adjacent terminology used by fans or archives
- alternate languages, spellings, and historical names
- source-specific queries for video, archives, press images, and image search

Use multiple discovery queries rather than repeatedly paraphrasing one query.

### 3. Gather an oversized candidate pool

Aim for at least 1.5–3 times the requested final count.

For video sources:

1. Prefer the highest practical source resolution.
2. Sample multiple timestamps across each promising video.
3. Avoid intros, outros, transitions, black frames, and motion blur.
4. Use upload thumbnails only when they genuinely match the brief; label them as thumbnails rather than frames.
5. Keep source URL, title, timestamp, and resolution.

Do not place unreviewed candidates in the final library unless the user explicitly requests raw results.

### 4. Review visually

Visually inspect every retained image, including sampled video frames. Use contact sheets for large candidate pools, but inspect individual files whenever the sheet is ambiguous. Judge candidates on:

- **theme match** — does it express the requested visual idea?
- **readability** — can the subject and action be understood?
- **composition** — does it feel intentional rather than accidental?
- **distinctiveness** — does it contribute something memorable?
- **technical quality** — resolution, focus, exposure, compression
- **redundancy** — is a stronger near-duplicate already retained?
- **random-frame risk** — would this look meaningless without explanation?

Reject images that are empty, generic, illegible, badly blurred, weakly framed, redundant, or merely related by title.

### 5. Iterate from the strongest results

Describe what makes the best candidates work, then search and sample again using those discovered qualities. Re-extract frames from promising videos before abandoning them. Continue until the requested number of accepted images exists or sources are genuinely exhausted.

If quality and count conflict, favor quality and clearly report the shortfall rather than padding the set.

### 6. Deliver cleanly

Use clear, stable filenames and avoid claiming a resolution that was not verified. Unless the user requests another structure, produce:

```text
<output>/
├── images or numbered image files
├── CONTACT-SHEET.jpg      # useful for larger sets
├── SOURCES.md
└── manifest.json          # when metadata volume justifies it
```

`SOURCES.md` should identify every retained image with its source URL and, for video frames, timestamp. A useful manifest entry is:

```json
{
  "filename": "014-example.jpg",
  "source_url": "https://example.com/video",
  "source_type": "video-frame",
  "timestamp_seconds": 183,
  "resolution": "1280x720",
  "selection_reason": "Uncanny costume, readable action, and strong horror-comedy tension"
}
```

Keep temporary videos, rejected candidates, and intermediate contact sheets outside the final directory unless the user asks to retain them.

## Verify and report

Verify the accepted image count, measured dimensions, and correspondence between source records and retained files.

Report the output path, accepted count, source types, verified resolution range, and any limitations or shortfall.
