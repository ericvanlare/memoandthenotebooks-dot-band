---
name: adding-band-photos
description: "Compresses and adds new band photos to the website (photos.html and index.html). Use when adding new photos, uploading pictures, or updating the photo gallery."
---

# Adding Band Photos

Compresses band photos for web use and adds them to `photos.html` and `index.html`, keeping newest photos first.

## Step 1: Compress the photos

The user will copy original photo files into `assets/` (or tell you where they are on disk). Compress each one using `sips`:

```bash
sips -Z 1200 "<input>" --out "assets/MATN_<N>_web.jpg" -s format jpeg
```

- `-Z 1200`: Constrains the longest dimension to 1200px, preserving aspect ratio.
- Output format: JPEG (no explicit quality flag — use sips defaults).
- Naming: `MATN_<N>_web.jpg` where `<N>` continues from the highest existing number in `assets/`.

Verify each output:
```bash
sips -g pixelWidth -g pixelHeight "assets/MATN_<N>_web.jpg"
ls -lh "assets/MATN_<N>_web.jpg"
```

Expected: longest side 1200px, file size ~100–350KB.

## Step 2: Update photos.html

This page shows **all** photos in descending order (newest first).

- Add new `<img>` entries at the **top** of the grid, following this pattern:
  ```html
  <img src="assets/MATN_<N>_web.jpg" alt="Band Photo <N>" class="aspect-square object-cover cursor-pointer hover:opacity-80 transition-opacity shadow-lg" onclick="openLightbox(<INDEX>)" />
  ```
- Re-index **all** `onclick="openLightbox(N)"` values sequentially from 0.
- Add the new photos to the **top** of the `const images = [...]` JS array:
  ```js
  { src: 'assets/MATN_<N>_web.jpg', alt: 'Band Photo <N>' },
  ```

## Step 3: Update index.html

The homepage shows only the **4 most recent** photos in the "PHOTOS & ARTWORK" section.

- Update the 4 `<img>` tags in the grid to show the 4 newest photos (newest first).
- Update the `onclick="openLightbox(N)"` indices to 0–3.
- Update the `const images = [...]` JS array to match those same 4 photos.
- Update the "VIEW ALL (N) →" link count to reflect the total number of photos.

## Step 4: Git — only commit `_web` files

**Only `_web.jpg` files should be committed and pushed.** The original uncompressed photos the user copied in must NOT be included in commits.

When staging files:
- Stage each `_web.jpg` explicitly: `git add assets/MATN_<N>_web.jpg`
- Stage the HTML files: `git add index.html photos.html`
- **Never** use `git add .` or `git add -A`
- **Never** stage the original source files (e.g., `.JPEG`, `.PNG`, `.HEIC`, etc.)

## Checklist

- [ ] Photos compressed to `MATN_<N>_web.jpg` in `assets/` (longest side 1200px)
- [ ] photos.html: New photos added to grid at top
- [ ] photos.html: All `openLightbox()` indices sequential from 0
- [ ] photos.html: JS `images` array updated
- [ ] index.html: 4 most recent photos in grid
- [ ] index.html: JS `images` array updated
- [ ] index.html: "VIEW ALL (N)" count updated
- [ ] Only `_web.jpg` files and HTML files staged in git (no originals)
