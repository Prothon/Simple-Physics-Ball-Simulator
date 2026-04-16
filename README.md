# Physics Sandbox — Grade 12 Remake

A physics simulator originally written in Visual Basic 6 as a Grade 12 exam project (~2006), rebuilt in JavaScript/Canvas as a single HTML file.

## How to Run

Just open `index.html` in any browser. No server, no dependencies, no build step.

## Features

- **Click & drag** to place and launch a ball (slingshot mechanic)
- **Gravity, friction, bounciness, wind, air drag** — all adjustable with sliders
- **Gravity wells** — right-click to place. Uses Newton's inverse-square law (`F = GM/r²`)
- **9 planet/scenario presets** — Earth, Moon, Mars, Jupiter, Zero-G, Super Ball, Windstorm, Ice, Mud
- **Time scale** — slow-mo to fast-forward
- **Live formula overlay** — shows the actual physics equations with real values plugged in
- **Force arrows** — visualize gravity (red), velocity (yellow), wind (blue), and well pull (purple)
- **X/Y coordinate axes** with labeled tick marks
- **Trail visualization** and bounce flash effects
- **Hover tooltips** on every slider explaining the physics in kid-friendly language with real formulas
- **Console logging** — full replayable state dumps for debugging

## Experiments to Try

1. Set gravity to 0, place a gravity well, throw the ball sideways — **orbit!**
2. Set bounciness to 1.0 — does the ball ever stop?
3. Max wind + throw against it — can you make it hover?
4. Gravity 1.62 = the Moon, 24.79 = Jupiter
5. Place multiple wells and watch chaotic trajectories (three-body problem!)

## Origin Story

The original VB6 version simulated gravity, bouncing, friction, and wind using `Timer` controls as a game loop. This remake preserves the same physics concepts with proper implementations:

- `requestAnimationFrame` game loop instead of VB Timer hacks
- Coefficient of restitution instead of manual energy return
- Air drag (velocity-dependent) instead of hard speed caps
- Newton's gravitational law for gravity wells
- Resting contact detection to prevent infinite micro-bouncing

## License

Do whatever you want with it. It's a learning tool.
