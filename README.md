# 🎱 Physics Sandbox

**A physics simulator originally written in Visual Basic 6 as a Grade 12 exam project (~2006), rebuilt in JavaScript/Canvas as a single HTML file.**

Built as a teaching tool for my son Daniel (9 years old) to explore physics concepts hands-on before diving into Unity. Every slider has a hover tooltip explaining the physics in plain English with the real formula underneath.

![No dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen) ![Single file](https://img.shields.io/badge/files-1%20HTML-blue) ![License](https://img.shields.io/badge/license-do%20whatever-orange)

## 🚀 How to Run

Just open `index.html` in any browser. No server, no dependencies, no build step, no install.

```
double-click index.html
```

That's it.

## 🎮 Controls

| Action | What it does |
|--------|-------------|
| **Left click** | Place the ball |
| **Drag + release** | Aim and throw (slingshot style — pull back to shoot forward) |
| **Right click** | Place a gravity well |
| **🔄 Reset** | Clear everything, back to Zero-G defaults |

## ⚙️ Physics Parameters

### 🌍 World Forces
| Slider | What it does | Formula | Real-world reference |
|--------|-------------|---------|---------------------|
| **Gravity** | Downward acceleration | `Vy += g × Δt` | Earth = 9.81, Moon = 1.62, Jupiter = 24.79 |
| **Wind** | Horizontal acceleration | `Vx += wind × Δt` | Negative = left, positive = right |
| **Air Drag** | Speed-dependent resistance | `V *= (1 − drag × speed)` | 0% = vacuum, ~0.2% = Earth air, 1% = soup |

### 🧱 Surface Properties
| Slider | What it does | Formula | Real-world reference |
|--------|-------------|---------|---------------------|
| **Bounciness** | Energy kept after bounce (coefficient of restitution) | `Vy = −Vy × e` | Basketball ≈ 0.75, Baseball ≈ 0.55, Brick = 0 |
| **Friction** | Ground slowing (kinetic friction) | `Vx *= (1 − μ)` | Ice ≈ 0.01, Gym floor ≈ 0.25, Sand ≈ 0.60 |

### 🎮 Controls
| Slider | What it does |
|--------|-------------|
| **Throw Power** | Launch velocity multiplier (10% = gentle, 100% = cannon) |
| **Time Scale** | Slow-mo (0.1x) to fast-forward (2x). Default 0.25x for easy observation |

### 🪐 Gravity Wells
| Slider | What it does | Formula |
|--------|-------------|---------|
| **Well Mass** | Strength of placed gravity wells | `F = G × mass / distance²` (Newton's law) |

Right-click to place wells anywhere. Each well pulls the ball toward it using the inverse-square law — the closer the ball gets, the dramatically stronger the pull. Place multiple wells for chaotic multi-body trajectories.

## 🌍 Scenario Presets

| Preset | Gravity | Bounce | Friction | Drag | Notes |
|--------|---------|--------|----------|------|-------|
| 🌍 Earth | 9.81 | 0.40 | 0.25 | 0.20% | Standard physics |
| 🌙 Moon | 1.62 | 0.50 | 0.10 | 0% | No atmosphere, low gravity |
| 🔴 Mars | 3.72 | 0.45 | 0.20 | 0.05% | Thin atmosphere |
| 🟠 Jupiter | 24.79 | 0.30 | 0.30 | 0.50% | Crushing gravity, thick atmosphere |
| 🛸 Zero-G | 0 | 0.95 | 0 | 0% | **Default.** Pure space — add wells for orbits! |
| 🟡 Super Ball | 9.81 | 0.95 | 0.05 | 0.10% | Almost no energy loss |
| 🌪️ Windstorm | 9.81 | 0.40 | 0.25 | 0.30% | Strong sideways wind |
| 🧊 Ice Rink | 9.81 | 0.40 | 0.01 | 0.05% | Ball slides forever |
| 🟤 Mud Pit | 9.81 | 0.05 | 0.90 | 0.80% | Ball goes splat |

## 🧪 Experiments to Try

1. **Orbit** — Zero-G, place one well (mass ~1000), throw the ball sideways past it. If the speed is right, it orbits. Too fast = escape. Too slow = captured.
2. **Three-body problem** — Place 3 wells in a triangle, throw the ball through the middle. Watch chaos.
3. **Terminal velocity** — Set gravity to 30, drag to 0.5%. Drop the ball. Watch it accelerate then plateau — that's terminal velocity.
4. **Hover** — Set wind to max, throw the ball into the wind. Can you balance it?
5. **Perfect bounce** — Bounciness 1.0. Does the ball ever stop? (Spoiler: air drag still slows it)
6. **Moon jump** — Gravity 1.62, throw upward. Compare to Earth (9.81). Same throw, 6× higher.
7. **Slingshot maneuver** — Zero-G, place a well, throw the ball so it curves around the well and exits faster than it entered. This is how NASA sends probes to Jupiter.

## 📊 Visual Features

- **Force arrows** — Red (gravity), Yellow (velocity), Blue (wind), Purple (gravity well pull)
- **Purple pull lines** — Always visible, length and thickness show relative force strength. With multiple wells you can instantly see which one is dominant.
- **Trail** — Fading path showing the ball's trajectory (parabolas under gravity, ellipses around wells)
- **Bounce flash** — Yellow burst on collision
- **Coordinate axes** — X/Y axes with meter tick marks. Dashed crosshair from ball to axes shows position.
- **Live formula overlay** — Shows every physics equation with real values plugged in, updating in real-time
- **Hover tooltips** — Every slider label has a detailed explanation with the formula and real-world examples

## 🔧 Console Debugging

Open browser DevTools (F12 → Console) to see:

- **🚀 LAUNCH** — Full initial state (position, velocity, all parameters, all wells) — enough to reproduce any scenario
- **━━━ FRAME N ━━━** — Every 60 frames (1/sec): complete state dump with ball position, velocity, all params, sim bounds, and per-well force breakdown
- **BOUNCE** — Every collision with impact velocity and result
- **🪐 WELL PLACED** — Position and mass of each placed well
- **🪐 CAPTURED** — When the ball is absorbed by a well
- **⏸ PAUSED** — When the ball comes to rest (simulation stops to save CPU)

## 📖 Origin Story

The original VB6 version (~2006) was a Grade 12 exam project — a circle bouncing around a VB form using `Timer` controls as a game loop, with gravity, friction, wind, and bouncing. You clicked twice to set position and velocity. Global variables everywhere. `HealthPotminor()`, `HealthPotminor2()`, `HealthPotminor3()` — the same function copy-pasted for each party member.

This remake preserves the same core physics with proper implementations:

| Concept | VB6 Original | JS Remake |
|---------|-------------|-----------|
| Game loop | `Timer.Interval = 1` | `requestAnimationFrame` (60fps) |
| Bounce | `EReturn = 0.4` | Coefficient of restitution (e) |
| Speed limit | None (ball could teleport) | Air drag (velocity-dependent) |
| Gravity | `Gravity * Gravity * Time` (wrong but close) | `g × Δt` (correct) |
| Resting | Ball jittered forever | Resting contact detection |
| Friction | `Acc(5) - (Acc(5) * (UFK / 100))` | `Vx *= (1 − μ)` (same idea, turns out) |

The resting contact bug — where gravity fights the floor collision in an infinite loop — was a real bug we had to debug with console logging. It's the same problem real physics engines solve with "sleeping" systems.

## 🗂️ Code Structure

Everything is in one file (`index.html`) organized into 13 labeled sections:

1. **SETUP** — Canvas, element references
2. **CONSTANTS** — PPM, DT, RADIUS
3. **SLIDERS** — Declarative slider system (add new ones in 3 steps)
4. **GAME STATE** — Ball, trail, wells, interaction state machine
5. **SCENARIOS** — Planet presets (add new ones in 2 steps)
6. **TUTORIAL** — Step-by-step onboarding
7. **INPUT HANDLING** — Mouse events, reset, well placement
8. **PHYSICS** — The `step()` function — heart of the simulation
9. **DRAWING HELPERS** — `drawArrow()`, `drawCircle()`, `drawRing()`
10. **DRAW** — Main render function
11. **DRAW SUB-FUNCTIONS** — Axes, wells, aiming UI, ball, formula overlay
12. **READOUT** — Side panel numbers
13. **GAME LOOP** — `requestAnimationFrame` loop

Want to modify something? Search for `SECTION` and jump to the right one.

## License

Do whatever you want with it. It's a learning tool.
