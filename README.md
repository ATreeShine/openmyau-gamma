# MyauFix

A Minecraft 1.8.9 Forge client forked from **OpenMyau** (20250910), with the original
issues fixed, new bypasses, and every **OpenSkid** module merged in as `openskid-<Name>`.

> If you think this is a piece of shit, then you're right.
> If you think it's very useful, then you're also right.

---

## Features

- **135 original client modules** — `AimAssist`, `KillAura`, the 53 `Yuri*` modules,
  `CSCAFFOLD`, etc. — all preserved with their original names, properties and behaviour.
- **205 imported OpenSkid modules** — combat, movement, BedWars utilities, player/world
  detectors, render modules, and more. They appear in the ClickGui, take keybinds and are
  saved/loaded by your config exactly like your own modules.
- **`test-scaffold`** — the flagship scaffold with Watchdog/Watchdog2/Watchdog3 fast modes,
  tower modes (Vanilla / Extra / Telly / Watchdog / Watchdog Low), keep-Y modes, SNAP
  rotations, and a full set of in-game tunables (see below).
- **`YuriKillAura`** — ported from Yuri, with the line-of-sight check and raycast gate
  fixed (see below).
- **Custom account tooling** (`me.ksyz.accountmanager`) for Microsoft / session login.

### Module namespaces

`openskid-` prefixed modules are the ones imported from OpenSkid, so they can be told
apart from your own modules (e.g. `openskid-KillAura` vs `KillAura`, `openskid-Scaffold`
vs `Scaffold`). When no exact unprefixed match exists, chat commands also resolve the
`openskid-` modules by their bare name — so `.t killaura` and `.t openskid-killaura`
both work.

---

## Requirements

- Minecraft **1.8.9** with Forge **11.15.1.2318-1.8.9**
- Java 8 runtime (build toolchain)

## Installation

1. Drop `MyauFix-1.6.jar` into your Forge `mods/` folder.
2. Launch the game with Forge 1.8.9.
3. Open the module GUI and start toggling.

## Building from source

```bash
export JAVA_HOME=/path/to/jdk17
./gradlew clean remapJar shadowJar --offline
# output: build/libs/MyauFix-1.6.jar
```

## Commands & usage

Chat commands (with the default prefix `.`):

| Command | What it does |
| --- | --- |
| `.t <module> [on/off]` | Toggle a module (alias: `.toggle`) |
| `.module <module>` | Show/inspect a module's settings |
| `.list` | List modules |
| `.config <name>` | Save/load a config |
| `.friend ...` | Manage friends |
| `.hide / .show` | Hide/show modules in the arraylist |
| `.vclip <dist>` | Vertical clip |
| `.ign <name>` | Spoof/set your ign |

Use the in-game ClickGui to adjust sliders and toggles — most module properties
(floats/ints/percentages) are sliders, modes are clickable mode selectors, and booleans
are checkboxes.

### `test-scaffold` highlights

Rotations come in `NONE / DEFAULT / BACKWARDS / SIDEWAYS / SNAP`, sprint/auto-jump in
Watchdog modes, and a rich set of live-tunable sliders:

- **Watchdog fast modes** — `wd-max-yaw`, `wd-yaw-random`, `wd-ground-only`,
  `wd-clamp-delay`, `wd-auto-jump`
- **Watchdog2** — `wd2-flag-yaw`, `wd2-base-yaw`, `wd2-yaw-random`
- **Watchdog3** — `wd3-yaw-offset`, `wd3-yaw-threshold`, `wd3-place-delay`
- **Tower / keep-Y** — tower mode, keep-Y mode, `timer-boost`, `timer-slowdown`
- **Movement** — `ground-motion`, `air-motion`, `speed-motion`, `multi-place-extra`,
  `safe-walk`, `swing`, `item-spoof`, `block-counter`
- **Tower motion tweaks** — `tower-nudge-motion`, `tower-jump-speed`,
  `tower-phase2-scale`, `tower-phase3-scale`, `tower-drift-min/max`, `edge-padding-min/max`,
  `drop-accel`, `drop-damp`, `extra-cycle-limit`, `edge-approach-base` / jitter
- **Rotation clamps** — `yaw-clamp-min/max`, `initial-pitch-min/max`,
  `telly-yaw-factor-min/max`, `telly-pitch-min/max`, `telly-placement-delay`,
  `telly-yaw-clamp-min/max`

### `YuriKillAura` fixes

- The line-of-sight check (`canSeeEntity`) was tracing the **wrong direction**
  (testing the block *behind* the player). It now traces from the player's eyes to the
  entity's mid-body.
- `rayHitsTarget` previously compared the wanted rotation against the rotation it
  *itself computed* (always ≈ 0, so the raycast gate never actually blocked anything).
  It now compares against the rotation actually sent that tick.
- Target selection now respects FOV and through-walls visibility, and the rotation
  speed is clamped to ≥ 1.
- New `FOV` slider (30–360, default 360 = off) and a wider `Seek Range` floor (1).

---

## Configuration

Configs live in the client's config folder and are JSON. The default `default.json` is
loaded on startup if present. Every property (mode, slider, checkbox, color, text) of
every module is saved/loaded, so your in-game tweaks survive restarts.

---

## GUI fix

If you notice rendering glitches with the GUI / HUD after upgrading (chat, scoreboard,
hotbar or top bar not looking right), run these commands in chat:

```
.t renderfixes
.t hotbar
.t dynamicisland
```

These toggle the matching OpenSkid render modules (`openskid-RenderFixes`,
`openskid-Hotbar`, `openskid-DynamicIsland`) to re-apply the fixed rounded-corner
rendering, the custom hotbar/XP bar, and the ping/server/FPS top bar.

---

## Contributions

Code reference: [OpenMyau](https://github.com/60124808866/OpenMyau) ·
[Leader Client](https://github.com/Mornly/LeaderClient) ·
[OpenMyau-Plus](https://github.com/IamNespola/OpenMyau-Plus) ·
[MyauReborn](https://github.com/Infinity114514/MyauReborn)

Developer: [Mornly](https://github.com/Mornly)

## Disclaimer

This is a utility client for Minecraft 1.8.9. Use it at your own risk; using clients like
this can get you banned on public servers.
