# Yin Yang Generator

A free, browser-based tool for constructing a yin–yang symbol from precise
golden-ratio (φ / Φ) relationships, featuring adjustable eye sizing, color pickers with
presets, two measurement overlays, and PNG/JPG export. No install, no
build step — it's a single HTML file you can open directly or host as a
static page.

**Live tool:** https://sacred-geometry.github.io/YinYangGenerator/

---

## Basic terms: Ear, Lobe, Eye

The symbol is built from three circular measurements, all defined
relative to the same center point. The Ear radii originates at (0,0), the Lobes are positioned at fixed offsets along the vertical axis ($\pm 0.5$), and the Eyes are then placed at those exact same points.

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
    segment construction in the "Other Segments" view (points A, B, C, G, H,
    O) is **100% independent of eye size**. AB = φ·R (~.618) and AG = Φ·R (~1.618) no
    matter how large or small you make the eyes.

- **Variable :**
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
of the construction). The **Eye Ratio Presets** panel offers several
φ-power values (e.g. the default, φ³ ≈ 0.236) as well as plain fractions
(⅓, ¼, 5⁄21,) and a free-form equation box if you want to explore
your own ratio (supports `phi`, `Phi`, `Pi`,  e , tau ,`sqrt()`, and arithmetic).

### The two measurement overlays

- **Vertical Line Ratios** — reads the symbol from apex to base along
  the vertical axis, showing segment length and its cumulative
  distance from the apex, each as a decimal multiple of `R`.
- **Other Segments** — shows the fixed construction described above:
  a line from point **A** (where the right midline meets the Ear) through
  each Lobe's center, out to the far edge of the Ear. This reveals the
  exact φ/Φ relationships that exist independent of eye size, plus the
  two live points (E, F) where that same line crosses the Eye's own
  boundary.

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
Everything (rendering, color presets, PNG/SVG export) runs entirely in
the page.

---

## Acknowledgements

This tool was generated with the assistance of **Claude**, an AI assistant
made by [Anthropic](https://www.anthropic.com). The interactive Yin Yang
Generator — including the golden-ratio construction logic, measurement
overlays, color presets, equation input, and PNG/SVG export — was built
through a collaborative conversation with Claude, which handled the geometry,
the code, and the documentation.

### Special thanks to the Geometers

The mathematical foundations this tool rests upon were discovered and shared
by geometers whose work makes projects like this possible.

A particular note of gratitude goes to **John Arioni**,
whose elegant exposition of the golden-ratio relationships of
the yin–yang symbol provided inspiration for the development of this Generator Tool. Image displayed at *Cut The Knot*:

> [The Golden Ratio in Yin Yang — Cut The Knot](https://www.cut-the-knot.org/do_you_know/GoldenRatioInYinYang.shtml)

The tradition of geometers who discover, prove, and freely share this kind
of foundational knowledge is what allows tools like this to exist. Golden-Section Calipers were also utilized in the co-creation of this work. Thank you.
