---
name: compressing-posters
description: Compresses show poster images for web use. Use when adding a new poster, resizing a poster, or asked to compress a poster image.
---

# Compressing Posters

Resizes poster images so the longest dimension is 1200px (maintaining aspect ratio) and saves them as `_web.jpg` in `assets/posters/`.

## Workflow

1. Identify the uncompressed poster file in `assets/posters/` (typically a `.JPEG` or `.png` without `_web` in the name).
2. Check its dimensions with `sips -g pixelWidth -g pixelHeight <file>`.
3. Determine the longest dimension (width or height).
4. Resize using `sips`:
   - If height is the longest: `sips --resampleHeight 1200 "<input>" --out "<output>_web.jpg"`
   - If width is the longest: `sips --resampleWidth 1200 "<input>" --out "<output>_web.jpg"`
5. Verify the output dimensions and file size with `sips` and `ls -lh`.

## Output naming convention

- Input: `poster-YYYY-MM-DD.JPEG` (or any extension)
- Output: `poster-YYYY-MM-DD_web.jpg`

## Exception

If the poster is square (or nearly square, e.g. 1080×1079), do NOT stretch it to 1200px. Keep original dimensions and just save as `_web.jpg`. Square posters look bad when stretched.

## Expected results

- Longest dimension: 1200px
- File size: typically 250–560KB
- Format: JPEG
