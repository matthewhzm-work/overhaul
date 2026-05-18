# Matthew Ho — Portfolio Overhaul (Sandbox)

## What This Is
This is a **sandbox/overhaul branch** of the live portfolio at matthewho.work.
- Live site repo: github.com/matthewhzm-work/matthewho.github.io (DO NOT touch from this session)
- This repo: github.com/matthewhzm-work/overhaul — deployed at matthewhzm-work.github.io/overhaul
- Local folder: /Users/matthewho/Documents/GitHub/portfolio-overhaul

This is a safe environment to experiment freely. Nothing here affects the live site.

## Starting Point
Copied from the live site at commit cab9a47 (May 2026). All files, images and content are identical to the live site at that point.

## File Structure
- `index.html` — Homepage: 3-column independent flex grid, About section, Recognition section
- `work.html` — All project pages (single file, block-based renderer + legacy template fallback)
- `admin.html` — Password-protected CMS
- `data.js` — Single source of truth for all content. Exposes `PORTFOLIO_DATA` global.
- `images/` — All processed images as WebP (80% quality, 2400px max) or optimised GIF

## Design System (current — may be overhauled)
- Fonts: Lexend (display/titles), Inter (body), IBM Plex Mono (labels/UI/mono)
- Colours: --paper:#F5F4EF  --ink:#0A0A0A  --red:#E8200C  --mid:#888  --light:#E2E1DC
- Nav: fixed, transparent, 2-row on mobile. Name left · tagline+awardstrip centre · links right
- Cards: 3 independent flex columns (true Pinterest masonry), 8px gap, translateY(-8px) lift on hover, red overlay, NO shadow, NO image zoom
- Video embeds: max-width 1075px, centred
- Images: always full height (height:auto), never cropped

## Block-Based Page Builder
Every active project has a `blocks` array in data.js. When `P.blocks && P.blocks.length > 0`, work.html renders from blocks and ignores projectTemplate entirely.

### Block Types
- `video`     — {id, type, url, videoType, caption, width}
- `callout`   — {id, type, text, size, align}
- `text`      — {id, type, html, columns, width}
- `image`     — {id, type, url, caption, width, lightbox}
- `image-row` — {id, type, images:[{url,caption}], layout, columns, gap, lightbox}
                layout: 'grid' | 'scroll'
- `image-viewer` — {id, type, images:[{url,caption}], width, lightbox}
- `split`     — {id, type, leftType, leftUrl, leftVideoType, leftHtml, leftLabel,
                              rightType, rightUrl, rightVideoType, rightHtml, rightLabel}

### Block IDs
Short unique id per block (e.g. 'b101'). Must be unique across ALL projects in data.js.

## Key Rules (inherited from live site — relax freely in overhaul)
1. Never use oninput closures for save logic — always read from DOM by ID on save
2. Never put variable references in inline onclick strings — use LB_POOLS string keys
3. Always filter D.projects by active !== false before rendering grid or rail
4. Images must use height:auto — never object-fit:cover on displayed images
5. No credentials/meta sidebar on any project page template
6. Never document passwords or credentials in any tracked file

## GitHub Deployment
Push via GitHub Desktop. Pages auto-deploys from main branch.
Preview URL: matthewhzm-work.github.io/overhaul
Note: no custom domain on this repo — CNAME was intentionally removed.
