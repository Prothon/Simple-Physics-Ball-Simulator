# 🎱 Physics Sandbox

**A physics simulator originally written in Visual Basic 6 as a Grade 12 exam project (~2006), rebuilt in JavaScript/Canvas as a single HTML file.**

Built as a teaching tool for my son Daniel (9 years old) to explore physics concepts hands-on before diving into Unity. Every slider has a hover tooltip explaining the physics in plain English with the real formula underneath.

![No dependencies](https://img.shields.io/badge/dependencies-zero-brightgreen) ![Single file](https://img.shields.io/badge/files-1%20HTML-blue) ![License](https://img.shields.io/badge/license-do%20whatever-orange)

---

## 🚀 How to Run

**Online:** [Play it on GitHub Pages](https://Prothon.github.io/Grade12-Physics-Program-Remake/) *(replace with your actual URL after enabling Pages)*

**Locally:**
```
double-click index.html
```

No server. No dependencies. No build step. No install. Works in any modern browser.

---

## 🎮 Controls

| Action | What it does |
|--------|-------------|
| **Left click + drag** | Place the ball, aim, and throw (slingshot style — pull back to shoot forward) |
| **Right click** | Place a gravity well at cursor position |
| **🔄 Reset** | Clear everything — ball, wells, trail — back to Zero-G defaults |
| **🗑️ Clear All Wells** | Remove gravity wells without resetting the ball |
| **Scenario buttons** | Instantly switch all physics parameters (active button shows pressed-in) |

---

## ⚙️ Physics Parameters

Sliders are organized into logical groups. Hover over any label for a detailed tooltip with the real formula and kid-friendly explanation.

### 🌍 World Forces
Forces that act on the ball from the environment.

| Slider | Range | Default | Formula | What it does |
|--------|-------|---------|---------|-------------|
| **Gravity** | 0 – 30 m/s² | 0 (Zero-G) | `Vy += g × Δt` | Downward acceleration. Earth = 9.81, Moon = 1.62, Jupiter = 24.79 |
| **Wind** | -5 – 5 m/s² | 0 | `Vx += wind × Δt` | Horizontal acceleration. Negative = left, positive = right |
| **Air Drag** | 0% – 1% | 0.10% | `V *= (1 − drag × speed)` | Speed-dependent resistance. Creates terminal velocity. 0% = vacuum, ~0.2% = Earth air |

### 🧱 Surface Properties
What happens when the ball touches walls or the floor.

| Slider | Range | Default | Formula | What it does |
|--------|-------|---------|---------|-------------|
| **Bounciness** | 0 – 1.00 | 0.60 | `Vy = −Vy × e` | Coefficient of restitution. 0 = splat, 1 = perfect bounce. Basketball ≈ 0.75 |
| **Friction** | 0 – 1.00 | 0 | `Vx *= (1 − μ)` | Kinetic friction on ground contact. Ice ≈ 0.01, Gym floor ≈ 0.25, Sand ≈ 0.60 |

### 🎮 Controls
How you interact with the simulation.

| Slider | Range | Default | What it does |
|--------|-------|---------|-------------|
| **Throw Power** | 5% – 100% | 30% | Launch velocity multiplier. 10% = gentle toss, 100% = cannon |
| **Time Scale** | 0.1x – 2x | 0.25x | Slow-mo to fast-forward. All forces multiplied by this value |

### 🪐 Gravity Wells
Right-click to place. Each well pulls the ball using Newton's inverse-square law.

| Slider | Range | Default | Formula | What it does |
|--------|-------|---------|---------|-------------|
| **Well Mass** | 50 – 10,000 | 200 | `F = G × mass / dist²` | Strength of placed wells. Higher mass = stronger pull. Force increases dramatically at close range |

**Gravity well behaviors:**
- Wells are strong enough to overpower Earth gravity at high mass (~5000+)
- Wells can pull a resting ball off the floor
- Ball is "captured" if it reaches within 3px of a well center
- Purple pull arrows always visible — length and thickness show relative force
- Concentric rings scale with mass to show influence area
- Multiple wells create chaotic multi-body trajectories

---

## 🌍 Scenario Presets

Click a preset to instantly set all parameters. Active preset shows as a pressed-in button.

| Preset | Gravity | Bounce | Friction | Drag | Wind | Notes |
|--------|---------|--------|----------|------|------|-------|
| 🌍 **Earth** | 9.81 | 0.40 | 0.25 | 0.20% | 0 | Standard physics |
| 🌙 **Moon** | 1.62 | 0.50 | 0.10 | 0% | 0 | No atmosphere, low gravity |
| 🔴 **Mars** | 3.72 | 0.45 | 0.20 | 0.05% | 0 | Thin atmosphere |
| 🟠 **Jupiter** | 24.79 | 0.30 | 0.30 | 0.50% | 0 | Crushing gravity, thick atmosphere |
| 🛸 **Zero-G** | 0 | 0.60 | 0 | 0.10% | 0 | **Default.** Space — add wells for orbits! |
| 🟡 **Super Ball** | 9.81 | 0.95 | 0.05 | 0.10% | 0 | Almost no energy loss on bounce |
| 🌪️ **Windstorm** | 9.81 | 0.40 | 0.25 | 0.30% | 4.5 | Strong sideways wind |
| 🧊 **Ice Rink** | 9.81 | 0.40 | 0.01 | 0.05% | 0 | Ball slides forever |
| 🟤 **Mud Pit** | 9.81 | 0.05 | 0.90 | 0.80% | 0 | Ball goes splat |

All presets use 0.25x time scale for easy observation.

---

## 📊 Visual Features

### Force Arrows (toggle with "Show forces on ball")
| Color | Force | When visible |
|-------|-------|-------------|
| 🔴 Red | Gravity | When gravity > 0 |
| 🟡 Yellow | Velocity | When speed > 1.0 px/f |
| 🔵 Blue | Wind | When wind ≠ 0 |
| 🟣 Purple | Gravity well pull | Always (per well). Length 20–150px, thickness scales with force |

### Other Visuals
- **Trail** — Fading path showing trajectory. Parabolas under gravity, ellipses around wells
- **Bounce flash** — Yellow burst on collision (toggleable)
- **Coordinate axes** — X (red) and Y (green) axes ARE the floor and left wall. Tick marks every 5 meters with labels in the margin
- **Crosshair** — Dashed lines from ball to both axes showing exact position
- **Coordinate label** — `(x, y)` in meters floating next to the ball
- **Pulsing ring** — Shows on placed ball before launch (drag to aim)
- **Launch arrow** — Red arrow showing throw direction and power
- **Live formula overlay** — Semi-transparent box at top showing every physics equation with live values:
  ```
  Position:   x = 45.2 m    y = 12.8 m
  Velocity:   Vx = 3.2 m/s    Vy = -8.1 m/s

  Gravity:    Vy += g × Δt  →  Vy += 9.81 × 0.0167
  Wind:       Vx += wind × Δt  →  Vx += 0.0 × 0.0167
  Drag:       V = V × (1 − 0.0020 × speed)
  Movement:   x += Vx × Δt     y += Vy × Δt

  On bounce:  Vy = −Vy × e  (e = 0.40)
  Friction:   Vx = Vx × (1 − μ)  (μ = 0.25)
  Wells:      F = mass / dist²  (2 active)
  ```

---

## 🧪 Experiments to Try

1. **🛸 Orbit** — Zero-G (default), place one well (mass ~2000), throw the ball sideways past it. If the speed is right, it orbits. Too fast = escape. Too slow = captured.

2. **🌀 Three-body problem** — Place 3 wells in a triangle, throw the ball through the middle. Watch chaos unfold. This is an unsolved problem in physics!

3. **⬇️ Terminal velocity** — Earth preset, set gravity to 30, drag to 0.5%. Drop the ball from the top. Watch it accelerate then plateau — that's terminal velocity.

4. **🌬️ Hover** — Windstorm preset, throw the ball into the wind (left). Can you balance it?

5. **♾️ Perfect bounce** — Super Ball preset, set bounciness to 1.0. Does the ball ever stop? (Spoiler: air drag still slows it)

6. **🌙 Moon jump** — Moon preset, throw upward. Switch to Earth. Same throw, 6× less height.

7. **🚀 Slingshot maneuver** — Zero-G, place a well, throw the ball so it curves around the well and exits faster than it entered. This is how NASA sends probes to Jupiter.

8. **⚔️ Gravity vs gravity** — Earth preset, place a max-mass well (10000) above the ball. Watch it lift off the floor against Earth's gravity.

9. **🎱 Billiards** — Zero-G, no drag, bounciness 0.95. Throw the ball and watch it ricochet off walls forever.

10. **🕳️ Black hole** — Zero-G, place one well at mass 10000. Throw the ball nearby. Watch the capture.

---

## 🔧 Console Debugging

Open browser DevTools (`F12` → Console) for full replayable state logging:

| Log | When | What it shows |
|-----|------|--------------|
| `🚀 LAUNCH` | On throw | Ball position, velocity, all slider params, all wells — full replay state |
| `🌍 SCENARIO` | On preset click | Scenario name and all parameter values |
| `🪐 WELL PLACED` | On right-click | Well position and mass |
| `━━━ FRAME N ━━━` | Every 60 frames (1/sec) | Complete state: ball, speed, onFloor, all params, bounds, per-well force breakdown |
| `BOUNCE` | On collision | Which surface, impact velocity, resulting velocity |
| `DRAG` | Every second | Drag coefficient, speed, drag factor applied |
| `🪐 CAPTURED` | On well capture | Which well absorbed the ball |
| `⏸ PAUSED` | On idle (250ms at rest) | Final state. Simulation stops until next input |

Every log contains enough data to reproduce the exact scenario.

---

## 🧠 Physics Concepts Covered

This simulator demonstrates these real physics concepts:

| Concept | Where to see it |
|---------|----------------|
| **Newton's Second Law** (F = ma) | Gravity and wind accelerate the ball |
| **Projectile motion** | Throw on Earth — the trail shows a parabola |
| **Coefficient of restitution** | Bounciness slider — energy loss on collision |
| **Kinetic friction** | Friction slider — ground slows horizontal movement |
| **Air resistance / drag** | Drag slider — speed-dependent force, creates terminal velocity |
| **Newton's Law of Gravitation** | Gravity wells — F = GM/r², inverse-square law |
| **Orbital mechanics** | Zero-G + well — circular/elliptical orbits |
| **Escape velocity** | Throw too fast past a well — ball escapes |
| **Gravitational capture** | Throw too slow — ball spirals in |
| **Slingshot effect** | Ball curves around well and exits faster |
| **Three-body problem** | Multiple wells — chaotic, unpredictable trajectories |
| **Terminal velocity** | High gravity + drag — speed plateaus |
| **Resting contact** | Ball on floor — gravity balanced by normal force |
| **Conservation of energy** | Bounciness 1.0 + no drag = ball bounces forever |

---

## 📖 Origin Story

### The VB6 Original (~2006)

The original was a Grade 12 exam project — a circle bouncing around a VB6 form using `Timer` controls as a game loop. You clicked twice to set position and velocity. It had gravity, friction, wind, and bouncing. Global variables everywhere. The physics were wrong but close enough to look right.

The same developer also built "Dragon Wars" — a full RPG with a 3-party system (Warrior/Mage/Assassin/Healer), exponential XP scaling, a 10×10 tile map, armor system, potions, save/load with custom `.DW` files, sound effects, and a final boss. In VB6. In high school. With `HealthPotminor()`, `HealthPotminor2()`, `HealthPotminor3()` — the same function copy-pasted for each party member. Going from 1 team member to 3 caused an 8-hour merge disaster that led to learning about version control.

### What Changed

| Concept | VB6 Original | JS Remake |
|---------|-------------|-----------|
| Game loop | `Timer.Interval = 1` | `requestAnimationFrame` (60fps) |
| Bounce | `EReturn = 0.4` | Coefficient of restitution (e) |
| Speed limit | None (ball could teleport) | Air drag (velocity-dependent) |
| Gravity | `Gravity * Gravity * Time` (wrong but close) | `g × Δt` (correct) |
| Resting | Ball jittered forever | Resting contact detection with idle pause |
| Friction | `Acc(5) - (Acc(5) * (UFK / 100))` | `Vx *= (1 − μ)` (same idea, turns out) |
| Walls | Bounced at any speed | Impact threshold — rests against wall if pushed gently |
| Gravity wells | Didn't exist | Newton's inverse-square law with capture radius |
| Debugging | `frmDis` with live labels | Full console logging with replayable state dumps |

### Bugs We Fixed Along the Way

1. **Resting contact jitter** — Gravity pushed ball into floor, bounce pushed it back, repeat at 60fps forever. Fixed with resting state detection.
2. **Gravity well death spiral** — Ball orbited at 10px radius with force hitting the clamp ceiling every frame. Fixed with distance clamping and air drag.
3. **Wall bounce spam** — Wind pushed ball into wall, wall bounced it back, wind pushed it again. Fixed with impact velocity threshold.
4. **Corner trap** — Ball on floor against wall with wind, velocity oscillating near zero. Fixed with corner detection that zeroes velocity.

These are all real problems that real physics engines solve. The resting contact problem is why engines like Box2D have "sleeping" systems.

---

## 🗂️ Code Structure

Everything is in one file (`index.html`, ~1000 lines) organized into 13 labeled sections. Search for `SECTION` to navigate.

| Section | What it does |
|---------|-------------|
| 1. SETUP | Canvas, element references |
| 2. CONSTANTS | PPM (15), DT (1/60), RADIUS (14), MARGIN |
| 3. SLIDERS | Declarative slider system — add new ones in 3 steps |
| 4. GAME STATE | Ball, trail, wells, interaction state machine (idle → placed → launched) |
| 5. SCENARIOS | Planet presets — add new ones in 2 steps |
| 6. TUTORIAL | Step-by-step onboarding overlay |
| 7. INPUT | Mouse events, reset, well placement, scenario buttons |
| 8. PHYSICS | `step()` — forces, wells, drag, movement, collisions, resting contact |
| 9. DRAW HELPERS | `drawArrow()`, `drawCircle()`, `drawRing()`, unit conversions |
| 10. DRAW | Main render — grid, axes, wells, trail, ball, formula overlay |
| 11. DRAW SUBS | `drawAxes()`, `drawGravityWells()`, `drawAimingUI()`, `drawBall()`, `drawFormulaOverlay()` |
| 12. READOUT | Side panel numbers (speed, height, direction, bounces, wells) |
| 13. GAME LOOP | `requestAnimationFrame` — step, draw, readout, repeat |

### How to Add Things

**New slider:**
1. Add `<label>` + `<input type="range">` in the HTML
2. Add entry to `SLIDERS` object with element IDs and format function
3. Use `param('yourName')` anywhere in the code

**New scenario:**
1. Add entry to `SCENARIOS` object with values for each slider
2. Add `<button class="scene-btn" data-scene="yourName">` in the HTML

**New force:**
1. Calculate it in `step()` after the `// --- APPLY FORCES ---` comment
2. Add to `ball.vx` or `ball.vy`
3. Optionally draw an arrow in `drawBall()`

---

## License

Do whatever you want with it. It's a learning tool.
