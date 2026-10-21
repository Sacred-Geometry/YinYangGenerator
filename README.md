# Yin Yang Generator

A free, browser-based tool for constructing a yin–yang symbol from precise
golden-ratio (φ / Φ) relationships, featuring adjustable eye sizing, color pickers with
presets, three measurement overlays, a Design Constants panel with live
layout checks, and PNG/JPG export. No install, no
build step — it's a single HTML file you can open directly or host as a
static page.

**Live tool:** https://sacred-geometry.github.io/YinYangGenerator/

---

## Basic terms: Ear, Lobe, Eye

The symbol is built from three circular measurements, all defined
relative to the same center point. The Ear radius originates at (0,0), the Lobes are positioned at fixed offsets along the vertical axis (±0.5), and the Eyes are then placed at those exact same points.

| Term | What it is | Radius |
|---|---|---|
| **Ears** | The outermost boundary of the symbol, the two semi-circle halves. | `R` (= 1) |
| **Lobes** | The radii of the two S-curve swirls (the black/white "comma" shapes) | `R / 2` |
| **Eyes** | The small circle nested at the center of each Lobe | variable, adjustable |

### Fixed vs. variable

This distinction matters because it's the whole logic of the tool:

- **Fixed (never changes, regardless of any setting):**
  - The Ear radius (`R = 1`, everything else scales from this)
  - The Lobe radius (always exactly `R / 2`)
  - The S-curve that divides the two halves
  - Every point and ratio derived only from Ear + Lobe — for example, the
    segment construction in the "Other Segments" displays points A, B, C, G, H,
    and O that are **independent of eye size**. AB = φ·R (≈ 0.618) and AG = Φ·R (≈ 1.618), no matter how large or small the eyes.

- **Variable:**
  - The **Eye** radius, is adjusted with the slider, presets, or equation
  input, expressed as a ratio of the Lobe radius (`Eye ∶ Lobe`).
  - Colors are adjusted with presets and color pickers, as well as style options. (Ear A/B, Eye A/B, Background)

Because only one number (the eye ratio) is variable, the tool frames eye
size as "Eye : Lobe Radius" rather than an absolute size — as it remains a
fraction of the Lobe so the other portions of the symbol stay proportionally correct no
matter what radius is rendered.

### Why φ and Φ are frequently expressed

φ (phi, ≈ 0.618) and Φ (Phi, ≈ 1.618) are reciprocals of each other
(Φ = 1/φ = φ + 1). Because the Ear radius is exactly twice the Lobe
radius, several distances in the symbol resolve to clean multiples of φ
or Φ automatically — not because they were forced to, but because of
the 2:1 Ear-to-Lobe ratio itself (a 1, ½, √5⁄2 right triangle is inherent
in the construction). The **Eye Ratio Presets** panel offers several
φ/Φ derived values (e.g. the default, φ³ ≈ 0.236) as well as plain fractions
(⅓, ¼, 5⁄21) and a free-form equation box to explore
other ratios (supports `phi`, `Phi`, `Pi`, `e`, `tau`, `sqrt()`, and arithmetic).

### The three measurement overlays

- **Vertical Line Ratios** — reads the symbol from apex to base along
  the vertical axis, showing segment length and its cumulative
  distance from the apex, each as a decimal multiple of `R`.
- **Other Segments** — shows the fixed construction described above:
  a line from point **A** (where the right midline meets the Ear) through
  each Lobe's center, out to the far edge of the Ear. This reveals the
  exact φ/Φ relationships that exist independent of eye size, plus the
  two live points (E, F) where that same line crosses the Eye's own
  boundary.
- **Measure** — an interactive click-to-measure mode. Clicking points
  directly on the symbol accumulates measurements in a floating panel:
  one click identifies the nearest named construction point, two clicks
  report the distance between them (expressed as a multiple of `R`), and
  three clicks compute the angle at the middle point along with the ratio
  of the two flanking segments. The panel can be dragged anywhere on
  screen and cleared between measurements.

---

## The Design Constants panel

The **Design Constants** button opens a panel with the construction's fixed
numbers and a live check of what is on your screen right now. Symbol radius
= 1; the symbol's edge to the box corner is φ; so the center to the corner is
1 + φ = Φ.

### Terms

| Term | Meaning |
|---|---|
| **Geometry box** | The square the construction is defined in. The panel's "1000-unit box" figures are in these abstract units, not screen pixels. |
| **Rendered canvas** | The geometry box as actually drawn, in a whole number of screen pixels. |
| **Layout frame** | The invisible page element around the canvas. It is sized to the canvas. |

### Live checks

The checks are kept apart so a failure says which layer is at fault:

- **Centre alignment** — is the rendered canvas centred where the page layout
  puts the center? This is the only check that tests the canvas *on the page*.
- **Phi geometry** — is the symbol's radius exactly `SYM_K` (≈ 0.874) times the
  box's half-side, so that center → corner ÷ radius = Φ, and does the drawn
  bitmap agree with that to within a fraction of a pixel?
- **Pixel-grid alignment** — does the canvas start on a whole screen pixel and
  map 1 : 1 onto screen pixels?

Two audits give the details. The **Edge audit** draws the symbol on its own at
the canvas's exact pixel size and measures the gap from the symbol to each side
and each corner. It tests the symbol *inside* its canvas, not the canvas on the
page. The **Layout audit** compares the canvas with the layout center, the
layout frame, and the pixel grid.

### What can and cannot be exact

- A box made of whole screen pixels can be centred to within ±0.5 px at best.
  An even side centres on a whole pixel and an odd side on a half pixel. The
  page chooses the side so the error stays as close to 0 as the display scale
  (browser zoom × screen density) allows.
- CSS sizes are stored in 1⁄64 CSS px, so at some zoom levels (for example 110%
  or 150%) not every screen pixel can be addressed exactly. The page prefers
  pixels that can be, when that costs less than half a pixel of centring.
- On-screen drawing is anti-aliased, so a measured edge can differ from the
  ideal by a fraction of a pixel (the panel shows these as, for example,
  "+0.100"). Calipers laid on a screenshot cannot resolve that.
- The box aims for **610 CSS px** (a Fibonacci number) when the window has room,
  and shrinks to fit otherwise. The panel's "Rendered canvas" line shows the
  actual size.
- The symbol-to-box area ratio is π⁄(2Φ²) ≈ 0.599991. It is close to ⅗ but not
  equal to it; π is about 0.0015% below 6Φ²⁄5.

---

## Acknowledgements

This tool was generated with the assistance of **Claude**, an AI assistant
made by [Anthropic](https://www.anthropic.com). The interactive Yin Yang
Generator — including the golden-ratio construction logic, measurement
overlays, color presets, equation input, and PNG/JPG export — was built
through a series of collaborative conversations between [Giacomo Aureo](https://BronzeSquare.wixsite.com/labyrinth) and Claude. Claude was tasked with the geometry, HTML code development, and documentation, however Grok/XaI, ChatGPT, and Gemini also made contributions in math and code audits.

### Special thanks to the Geometers

The mathematical foundations this tool rests upon were discovered and shared
by geometers whose work makes projects like this possible.

A particular note of gratitude goes to **John Arioni**,
whose elegant exposition of the golden-ratio relationships of
the yin–yang symbol provided inspiration for the development of this Generator Tool. Image displayed at *Cut The Knot*:

> [The Golden Ratio in Yin Yang — Cut The Knot](https://www.cut-the-knot.org/do_you_know/GoldenRatioInYinYang.shtml)

The tradition of geometers who discover, prove, and freely share this kind
of foundational knowledge is what allows tools like this to exist. Golden-Section Calipers were also utilized in the co-creation of this work. Thank you.

---

## Hosting this on GitHub

This repo (`Sacred-Geometry/YinYangGenerator`) is the right place for the
tool. Here's how to get the HTML file in and live.

### 1. Add the file to the repo

**Easiest — directly in the GitHub web UI:**

1. Go to https://github.com/Sacred-Geometry/YinYangGenerator
2. Click **Add file → Upload files**
3. Drag in `index.html` (rename the file to exactly `index.html` if it
   isn't already — this matters for step 3 below)
4. Scroll down, add a commit message like `Add Yin Yang Generator app`,
   and click **Commit changes** (committing straight to `main` is fine
   for a small repo like this)

**Or from the command line, if you have git installed:**

```bash
git clone https://github.com/Sacred-Geometry/YinYangGenerator.git
cd YinYangGenerator
# copy the HTML file into this folder, named index.html
git add index.html
git commit -m "Add Yin Yang Generator app"
git push origin main
```

### 2. Add this README

If you're reading this file locally, upload it the same way (**Add
file → Upload files**, or `git add README.md`) so it replaces the
placeholder README already in the repo.

### 3. Turn on GitHub Pages

GitHub Pages serves static files straight out of the repo — no build
step needed for a single HTML file like this one.

1. In the repo, go to **Settings → Pages** (left sidebar, under "Code
   and automation")
2. Under **Build and deployment → Source**, choose **Deploy from a
   branch**
3. Under **Branch**, select `main` and folder `/ (root)`, then **Save**
4. Wait a minute or two, then refresh the page — GitHub will show
   **"Your site is live at..."** with the URL

Because the org name is `Sacred-Geometry` and Pages URLs are always
lowercased, the live URL is:

```
https://sacred-geometry.github.io/YinYangGenerator/
```

GitHub automatically serves `index.html` as the default page for that
URL — which is why the file needs to be named exactly `index.html` (not
`YinYang_Generator.html` or similar) for the clean URL above to work
without extra configuration.

### 4. Updating the tool later

Any time you upload a new version of `index.html` (web UI upload, or
`git push`), GitHub Pages rebuilds automatically within a few minutes —
no other steps needed.

---

## Local use

You can also just double-click `index.html` to open it in any modern
browser — no server, no internet connection, and no install required.
Everything (rendering, color presets, PNG/JPG export) runs entirely in
the page.
