# ABG Elec Consultants — Portfolio Website

Single-page portfolio site for **ABG Elec Consultants** (Est. 2004), an EHV
substation and transmission EPC contractor working at 33kV–230kV across
South India.

## Contents

| File | Description |
| --- | --- |
| `index.html` | The complete site — markup, styles, scripts and image assets in one file |

## Running locally

The site is a single static file with no build step. Open it directly:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
```

Some browsers restrict `file://` requests, so prefer a local server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Structure of `index.html`

| Lines | Contents |
| --- | --- |
| 1–21 | `<head>` — metadata and external CDN dependencies |
| 23–1504 | `<style>` — the "wheatish & greenish" design system |
| 1506–2578 | `<body>` — page sections |
| 2579–3655 | `<script>` — embedded image data and page behaviour |

### Sections

`hero` · `heritage` · `dossiers` · `projects` · `corridors` · `digital-twin`
· `gallery` · `clients` · `dispatch-section`

### Project catalog

The `projectsCatalog` array in `index.html` drives the project grid, its filter
pills and the dossier modal. It lists the 10 commissioned projects that have
their own field photographs; the card count and filter results are derived from
it at runtime, so adding an entry needs no other change. An entry's
`photosList` supplies its dossier gallery, so a new project needs its images
added to `siteImages` (or dropped into `images/`) under the same filenames.

### External dependencies

Loaded from CDNs at runtime, so the page needs network access to render fully:

- [Google Fonts](https://fonts.google.com) — Syne, JetBrains Mono, Plus Jakarta Sans
- [Font Awesome](https://fontawesome.com) 6.4.0 — icons
- [Three.js](https://threejs.org) r128 + `OrbitControls` — the 3D digital-twin visualiser

## A note on the images

All 37 photographs are base64-encoded into `index.html`: 34 in the `siteImages`
object and 3 more inline on `<img>` tags in the markup. That is why the file is
~10 MB with a single 9.6 MB line. The lookup helper already falls back to real
files:

```js
function getImageSrc(filename) {
  return siteImages[filename] || ('images/' + filename);
}
```

So the blobs can be extracted into an `images/` directory without touching any
other code — worth doing if the file becomes awkward to edit or diff.
