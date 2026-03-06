---
name: adding-show-posters
description: Adds new show posters to the website (index.html and shows.html). Use when uploading posters to the site, adding new shows, or updating the shows pages.
---

# Adding Show Posters

Adds compressed `_web.jpg` poster images to `index.html` and `shows.html`, keeping everything in reverse chronological order (newest first).

## Prerequisites

Posters must already be compressed as `_web.jpg` files in `assets/posters/`. If not, use the `compressing-posters` skill first.

## Workflow

### 1. index.html — Featured posters grid

The homepage shows only the **4 most recent** posters in the "UPCOMING & RECENT SHOWS" section.

- Update the 4 `<img>` tags in the grid to show the 4 newest posters (newest first).
- Update the `onclick="openPosterLightbox(N)"` indices to be 0–3.
- Update the `const posters = [...]` JS array to match those same 4 posters.
- Update the "VIEW ALL (N) →" link count to reflect the total number of shows.

### 2. shows.html — Full poster gallery

This page lists **all** posters in reverse chronological order.

- Add new poster entries at the top of the grid, following this pattern:
  ```html
  <div class="flex flex-col">
    <img src="assets/posters/poster-YYYY-MM-DD_web.jpg" alt="Show Month DD, YYYY" class="cursor-pointer hover:opacity-80 transition-opacity shadow-lg mb-2" style="aspect-ratio: 0.77;" onclick="openLightbox(N)" />
    <p class="text-sm font-semibold">Month DD, YYYY</p>
  </div>
  ```
- Re-index **all** `onclick="openLightbox(N)"` values sequentially from 0.
- Add the new posters to the top of the `const posters = [...]` JS array.

### Special case: square posters

If a poster has a non-standard aspect ratio (e.g., the December 11, 2025 poster), wrap it in a black background div:
```html
<div class="bg-black cursor-pointer hover:opacity-80 transition-opacity shadow-lg mb-2" style="aspect-ratio: 0.77;" onclick="openLightbox(N)">
  <img src="assets/posters/poster-YYYY-MM-DD_web.jpg" alt="..." class="w-full h-full object-contain" />
</div>
```

## Checklist

- [ ] Poster `_web.jpg` file exists in `assets/posters/`
- [ ] index.html: 4 most recent posters in grid
- [ ] index.html: JS `posters` array updated
- [ ] index.html: "VIEW ALL (N)" count updated
- [ ] shows.html: New poster added to grid at correct position
- [ ] shows.html: All `openLightbox()` indices are sequential
- [ ] shows.html: JS `posters` array updated
