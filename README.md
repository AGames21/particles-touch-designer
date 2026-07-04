# particles-touch-designer

**v1.0** — Hand-tracked GPU particles + live camera distortion, in a single `index.html`.

Move your hands in front of the front camera: particles trail off your fingertips
(MediaPipe Hands + Three.js), and your body ripples/glitches through a custom GLSL
displacement shader driven by hand movement speed. Five presets (Fire, Glitch,
Galaxy, Chrome, Neon) swap live via config objects — no reload.

## How to host

iOS Safari only allows camera access on **HTTPS** origins, so:

- **GitHub Pages (recommended):** repo **Settings ▸ Pages ▸ Deploy from a branch**,
  pick the branch and `/ (root)`. Open `https://<user>.github.io/particles-touch-designer/`
  on your iPhone. HTTPS is automatic.
- **Local desktop testing:** `npx serve` or `python3 -m http.server` — `http://localhost`
  counts as a secure context on your own machine.
- **Testing on a phone from a dev machine:** tunnel it, e.g. `npx ngrok http 8000`
  or `cloudflared tunnel --url http://localhost:8000`.
- **Plain `file://` open won't work** — no camera access, and the CDN-hosted
  libraries (Three.js, MediaPipe) need network anyway.

## Notes

- Front camera, portrait, targets 30fps+ on iPhone (lite hand model, capped pixel
  ratio, single-draw-call particle pool, 30 Hz detection).
- Tap-to-start overlay is required: iOS won't open the camera without a user gesture.
- Fullscreen button uses the Fullscreen API where available; iPhone Safari has none,
  so it falls back to hiding the UI chrome.
- No hands detected? Touch/mouse drag works as a fallback emitter.
