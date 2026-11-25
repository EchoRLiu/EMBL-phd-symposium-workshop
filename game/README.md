# Robot in the Sandbox

A tiny, single-file browser game. Steer a little robot around a sandy
test track and collect as many **GPUs** as you can before the
**60-second** timer runs out.

No libraries, no build step, no network. One file.

## Play

Open `index.html` in any modern browser:

```bash
# from the repo root, either:
xdg-open game/index.html   # Linux
open game/index.html       # macOS
# ...or just double-click the file
```

No server needed — it runs from `file://`.

## Objective

- One GPU is on the field at a time.
- Touch it to collect it: **+1 GPU**, then a new one materializes
  somewhere else (never right on top of you).
- When the 60-second timer hits zero, the run ends.
- Your best score is saved in your browser (`localStorage`) and shown
  on the start screen.

## Controls

| Key | Action |
| --- | --- |
| `↑` (or `W`) | Throttle |
| `↓` (or `S`) | Brake / reverse |
| `←` / `→` (or `A` / `D`) | Turn |
| `P` | Pause / resume |
| `M` | Mute / unmute sound |
| `Enter` | Start / play again (also resumes when paused) |

The robot drives like a little off-road car: it coasts, so it takes a
moment to stop after releasing the throttle, steering gets tighter as
you pick up speed, and slams into the sandbox wall bounce you back.

## Notes

- `index.html` is the entire game (HTML + CSS + JS in one file).
- Sound effects are synthesized with the Web Audio API — nothing is
  downloaded; press `M` if you want silence.
- Best score is per browser profile; clearing site data resets it.
