# Yin Yang Generator

A free, browser-based tool for constructing a yin–yang symbol from precise
golden-ratio (φ / Φ) relationships, featuring adjustable eye sizing, color pickers with
presets, three measurement overlays, an Inspect panel (design constants) with live
screen checks, and PNG/JPG/SVG export. No install, no
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

The same menu also offers **Construction guides (calipers)**, which draws the
golden-section caliper check on the live symbol at all four corners: center →
edge `1`, edge → corner `φ`, the whole `Φ`.

---

## The Inspect panel

The **Inspect** button opens a panel with the construction's fixed
numbers and a live check of what is on your screen right now. Symbol radius
= 1; the symbol's edge to the box corner is φ; so the center to the corner is
1 + φ = Φ.

### Terms

| Term | Meaning |
|---|---|
| **Geometry box** | The square the construction is defined in. The panel's "1000-unit box" figures are in these abstract units, not screen pixels. |
| **Box on screen** | The geometry box as actually drawn: a whole, even number of screen pixels, so the center falls on a pixel corner. |
| **Layout frame** | The page element around the box, centered in the stage by the page layout. |

### How the box is placed

The page layout centers the frame. The canvas inside it is then nudged by less
than half a screen pixel so its corner lands exactly on a whole screen pixel.
Without that nudge, at fractional display scales (for example 1.125× or 1.2×,
common on Chromebooks) the browser can round one edge of the box differently
from the other and drop a row or column of pixels, which puts the corners on
that side slightly off. With it, the box is shown at exactly its intended size.

The live picture is always drawn on that canvas, at the screen's own
resolution. The SVG vector form is used for export.

### The exact rim

The rim is where the Φ check is read, so its edge pixels are not left to the
graphics chip's edge smoothing (which, on some machines, draws the circle a few
hundredths of a pixel small, and by different amounts in different directions).
Whenever the picture is still, and in every export and audit, the page works out
how much of each rim pixel lies inside the circle and uses exactly that as the
pixel's coverage; the colour stays what was drawn there. The circle is then the
same at every box size and on every machine. While the symbol is animating, the
graphics chip draws it as before.

### Live checks

Each section of the panel tests one layer, so a problem says where it is:

- **Your screen** — **Check my screen** asks Chrome to share this tab, shows a
  plain test card for a moment (a white disc on a grey box, black around it),
  measures a frame of the real screen pixels, and stops sharing. Each captured
  frame is checked before it is used, because Chrome can hand back a picture of
  the tab from before the test card appeared. It reports the symbol's center
  and, for each of the four corners, where the Φ mark lands relative to the rim.
  **Copy these figures** copies the result as text.
- **The picture the page draws** — the same scene drawn offscreen and measured
  from its own pixels: box, rim, center, the **Four-corner Φ test** (center →
  corner ÷ rim radius at ↖ ↗ ↙ ↘ separately), **Corner spread** and
  **Caliper miss**. No design constant enters the measurement; Φ appears only as
  the answer it is compared with.

Both checks find the rim from pixel areas: the covered area gives the radius,
the center of that area gives the symbol's center, and the covered area inside a
narrow wedge (±7.5°) toward each side and corner gives the rim's distance in that
direction. Sampling the picture along a line to the corner instead reads the rim
up to 0.05 px off, by an amount that changes with the box size (it depends on
where the rim crosses the pixel grid on the diagonal), so even a perfect circle
reads better at some sizes than others that way. Areas don't have that problem,
and resizing or blurring a capture doesn't shift them.
- **What calipers can see at each corner** — the contrast between the rim and
  the box at each corner. A rim that is close to the box color (for example
  white on cream, or a light metallic highlight on a near-white box) is hard to
  set a caliper point against, even when it is exactly in place. The panel also
  rates the box corners against the stage, and recommends the Light theme for
  caliper work.
- **Placement on the page** — pixel-grid alignment (and the nudge applied),
  page centering, and which drawing path the canvas uses.
- **Other display scales** — the offscreen test repeated at 1× to 2×.

### Controlled Φ rim diagnostic

Three views of the same geometry, for physical measurement:

- **Normal** — the symbol as styled.
- **Caliper target** — a pale-blue (#DEE9FF) disc on white with white cross hairs and an
  off-white center circle of radius φ⁷ (exactly 1⁄Φ⁷ of the outer radius), so a
  caliper point can be set on the center against a light patch; a light-yellow
  cross inside that circle marks the exact center.
- **Outer edge only** — a pale-blue (#DEE9FF) disc on an off-white field with
  white cross hairs and a tiny yellow dot on the exact center.

Both discs are light on purpose: a metal caliper point is easy to see in front of
a light color and lost in front of a dark one. For the same reason, use the
**Light** theme when measuring with calipers.

In both test views the four corners are identical and turning the symbol
changes nothing, so they separate the geometry from the colors at each corner.
Closing Inspect while a test view is on folds the panel down to a small
switcher with the three views; its ✕ appears once **Normal** is chosen, and ⤢
opens the full panel again.

### Graphics-chip comparison

Adding `?raster=cpu` to the address (for example
`…/YinYangGenerator/?raster=cpu`) makes every canvas draw in software instead
of on the graphics chip. The panel's **Canvas drawing** row shows which is in
use. Remove it to go back. The rim's exact areas are worked out by the page
itself, so they are the same either way.

### What can and cannot be exact

- A screen pixel can only be partly covered, so the rim is drawn as exact
  partial coverage rather than as a hard line; measured from those areas it
  lands within about a thousandth of a pixel of the ideal. A captured frame that
  Chrome has resized is good to about a tenth of a pixel. A quarter pixel is
  below what calipers on a screen can resolve.
- No box size is more exact than another: every size measures Φ to six
  decimals. A bigger box still helps physical measurement, because a given
  caliper error is then a smaller share of the radius.
- CSS sizes are stored in 1⁄64 CSS px, so at some display scales not every
  screen pixel can be addressed exactly; the remaining grid error is shown, and
  is a few hundredths of a pixel at most.
- The box aims for **610 CSS px** (a Fibonacci number) when the window has room,
  and shrinks to fit otherwise. The panel's "Box on screen" line shows the
  actual size.
- For a reference that needs no screen at all, export a PNG at 2584 px and
  print it at 100%.
- The SVG export states the geometry exactly (radius 437.016024 in a 1000-unit
  box, each half drawn as its own path), but how it looks depends on the program
  that displays it: browsers smooth vector edges their own way, typically a
  tenth of a pixel or so. A PNG export carries the page's exact rim in its
  pixels, so it is the better file to measure.
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
