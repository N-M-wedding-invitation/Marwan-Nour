# N ~ M — Wedding Invitation

A single-page cinematic wedding invitation: a full-screen 3D envelope opens on tap into a
minimal luxury invitation for 22 September 2026, Princess Garden Hall, Damanhour, Egypt.

## Files
```
index.html          ← the entire site (HTML + CSS + JS, uses Three.js from a CDN)
models/envelope.glb ← put YOUR envelope model here (placeholder folder included)
music/wedding-music.mp3 ← put YOUR instrumental track here (placeholder folder included)
```

## To run it
Open `index.html` through a local server (not `file://`, browsers block module imports
and GLTF loading from the file system). Easiest options:

- VS Code "Live Server" extension, or
- `npx serve .` in this folder, or
- `python3 -m http.server` in this folder

Then visit the printed localhost URL on desktop or your phone (same Wi‑Fi).

## Adding your own assets
1. Drop your file at `models/envelope.glb` (must be named exactly that, or edit the
   path in `index.html` where it says `loader.load('/models/envelope.glb', ...)`).
2. Drop an instrumental wedding track at `music/wedding-music.mp3` (or edit the
   `<audio src="...">` path in `index.html`).

## Making the GLB "opening" animation work well
The site tries three strategies, in order, so it will look right no matter how your
model is built:
1. **Embedded animation clip** — if your GLB has a baked animation whose name contains
   "open" (e.g. `Open`, `EnvelopeOpen`), it will be played automatically on tap.
2. **Named flap mesh** — if no clip exists, the script looks for a mesh/node whose name
   contains "flap", "lid", "top", or "seal" and rotates it open procedurally.
3. **Fallback** — if neither is found, the envelope still zooms and the invitation
   still transitions in smoothly; it just won't visibly "unfold."

For the best result, name your flap object something like `Flap` or bake a camera-free
animation clip called `Open` in Blender before exporting.

## Notes
- The model is auto-scaled and centered, so it should frame nicely regardless of the
  original unit scale — just make sure the envelope is built roughly "flat," facing +Z.
- Music never autoplays before the tap (browser policy + design intent); it fades in
  gently right after the tap, and can be muted with the floating button bottom-right.
- Scrolling is locked on the envelope screen and unlocked only after opening.
- Countdown targets 22 Sept 2026, 18:00 Egypt time (UTC+2) — adjust the `WEDDING_DATE`
  line in `index.html` if the ceremony time changes.
