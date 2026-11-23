# MITHUN // ASCII Abyss

An endless ASCII deep sea. The name **MITHUN** glows in the middle of it, shedding sparks,
while jellyfish pulse past, fish school by, bubbles rise and currents sweep through everything.

Pure HTML + CSS + JavaScript on a `<canvas>`. **No dependencies, no build step.**

## Features
- Huge glowing MITHUN lettering that assembles from loose particles, with light waves sweeping through it
- Jellyfish that pulse, propel themselves and have independently waving tentacles
- Fish schools swimming in both directions, scattering when you approach
- Hundreds of bubbles and drifting plankton, light rays, swaying seaweed, rocks
- Global current system with occasional big current waves
- Mouse / touch interaction (things drift away from your cursor) and mouse parallax
- Terminal-style boot loader, FPS monitor, pause and regenerate buttons
- Adaptive quality: sheds particles automatically if the frame rate drops

## Controls
| Action | Button | Key |
|---|---|---|
| Pause / resume | `pause` | `Space` |
| Regenerate scene | `regenerate` | `R` |
| Toggle FPS monitor | `fps` | `F` |

Click / tap / press any key during the boot screen to skip it.

## Run locally
Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000      # then visit http://localhost:8000
```

## Deploy to GitHub Pages
1. Create a repository on GitHub and push this folder to the `main` branch:
   ```bash
   git init && git add . && git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. In the repo go to **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. The included workflow (`.github/workflows/pages.yml`) deploys on every push to `main`.
   Your site appears at `https://<you>.github.io/<repo>/`.

(Alternative: Source = "Deploy from a branch", branch `main`, folder `/ (root)`. `.nojekyll` is included.)

## Project layout
```
index.html          page shell + loader markup
css/style.css       theme, HUD, loader
js/util.js          helpers, pointer state, ocean current model
js/renderer.js      ASCII cell grid, colour-batched canvas drawing, glow layer
js/world.js         rays, plankton, bubbles, seabed
js/creatures.js     jellyfish and fish schools
js/title.js         MITHUN pixel-font particle lettering
js/ui.js            boot loader, buttons, FPS meter
js/main.js          engine loop, input, regenerate, adaptive quality
```

## Customising
- Change the name: edit `TEXT` in `js/title.js` (letters available: M I T H U N — add more glyphs to `FONT`).
- Amount of life: jelly count in `Engine.generate()` (`js/main.js`); bubble/plankton density in `js/world.js`.
- Colours: `COLORS` in `js/renderer.js` and the CSS variables in `css/style.css`.

## Performance notes
All visuals are written into one character grid and drawn in a few colour batches per frame; the glow is a
second canvas blurred by the GPU. A frame governor lowers particle density below ~45 FPS.

MIT licensed.
