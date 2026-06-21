# Yin Yang Generator

A free, browser-based tool for constructing a yin–yang symbol from precise
golden-ratio (φ / Φ) relationships, with a live-adjustable eye size, color
presets, two measurement overlays, and PNG/SVG export. No install, no
build step — it's a single HTML file you can open directly or host as a
static page.

**Live tool:** https://sacred-geometry.github.io/YinYangGenerator/

---

## Basic terms: Ear, Lobe, Eye

The symbol is built from three concentric measurements, all defined
relative to the same center point. Using consistent names for each one
makes every ratio in the tool (and in this README) unambiguous.

| Term | What it is | Radius |
|---|---|---|
| **Ear** | The outermost circle — the full boundary of the symbol | `R` (= 1) |
| **Lobe** | The radius of the two large S-curve swirls (the black/white "comma" shapes) | `R / 2` |
| **Eye** | The small circle of the *opposite* color nested inside each Lobe | variable, adjustable |

A quick way to keep them straight: the **Ear** is the whole symbol's
outer edge, the **Lobe** is the swirl, and the **Eye** is the dot inside
the swirl. ("Lobe" is used here in the literal sense of a rounded
projecting part, the way an earlobe is the rounded part of an ear — the
Lobe sits inside the Ear, and the Eye sits inside the Lobe.)

### Fixed vs. variable

This distinction matters because it's the whole logic of the tool:

- **Fixed (never changes, regardless of any setting):**
  - The Ear radius (`R = 1`, everything else scales from this)
  - The Lobe radius (always exactly `R / 2`)
  - The S-curve that divides the two halves
  - Every point and ratio derived only from Ear + Lobe — for example, the
    segment construction in the "Other Segments" view (points A, B, G, H,
    O) is **100% independent of eye size**. AB = φ·R and AG = Φ·R no
    matter how large or small you make the eyes.

- **Variable (you control this with the slider, presets, or equation
  input):**
  - The **Eye** radius, expressed as a ratio of the Lobe radius
    (`Eye ∶ Lobe`). This is the one true free parameter in the whole
    symbol. Everything else in the diagram is computed from it.
  - Colors (Ear A/B, Eye A/B, Background)

Because only one number (the eye ratio) is free, the tool frames eye
size as "Eye : Lobe Radius" rather than an absolute size — it's always a
fraction of the Lobe, so the symbol stays proportionally correct no
matter what radius you're rendering it at.

### Why φ and Φ are frequently expressed

φ (phi, ≈ 0.618) and Φ (Phi, ≈ 1.618) are reciprocals of each other
(Φ = 1/φ = φ + 1). Because the Ear radius is exactly twice the Lobe
radius, several distances in the symbol resolve to clean multiples of φ
or Φ automatically — not because they were forced to, but because of
the 2:1 Ear-to-Lobe ratio itself (a 1, ½, √5⁄2 right triangle drops out
of the construction). The **Eye Ratio Presets** panel offers several
φ-power values (e.g. the default, φ³ ≈ 0.236) as well as plain fractions
(⅓, ¼, 5⁄21, etc.) and a free-form equation box if you want to explore
your own ratio (supports `phi`, `Phi`, `Pi`, `sqrt()`, and arithmetic).

### The two measurement overlays

- **Vertical Line Ratios** — reads the symbol from apex to base along
  the vertical axis, showing every segment length and its cumulative
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
