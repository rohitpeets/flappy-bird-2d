# Flappy Bird 2D

A Flappy Bird clone built from scratch in Java using Swing/AWT — no game engine, just JFrame, JPanel, and a manual game loop.

## Features

- Classic side-scrolling pipe-dodging gameplay with custom collision detection
- **Local split-screen multiplayer** — two players race side-by-side in the same window
- **Score-to-currency economy** — every pipe you pass is worth 1 point, and your score is added straight to your coin balance when you die. No separate grind: your skill at the base game is what funds the shop.
- **Shop with 3 unlockable bird skins** at increasing price tiers (500 / 2,000 / 10,000 coins), plus an equip system to switch which unlocked skin you play as
- Persistent save data — points, owned skins, and equipped skin all survive between sessions, stored in flat text files under `resources/data/`
- Sound effects for jumps and collisions

## Shop & Progression

| Skin | Cost | File |
|---|---|---|
| Bird 1 | 500 coins | `resources/images/bird1.png` |
| Bird 2 | 2,000 coins | `resources/images/bird2.png` |
| Bird 3 | 10,000 coins | `resources/images/bird3.png` |

- `Points.java` tracks your running coin balance, persisted to `resources/data/points.txt`.
- `Skins.java` handles purchases: checks your balance against a skin's cost, deducts on purchase, and writes ownership state to `resources/data/skins.txt` as a bitmask (`0,1,0` = only Bird 2 owned).
- `Equipped.java` tracks which owned skin is currently active, persisted to `resources/data/equipped.txt`, independent of ownership so you can freely switch between anything you've unlocked.
- On death, `Window.java` adds that run's score directly to your stored point balance (`initialPoints + score`) before returning to the end screen — so a good run funds your next shop purchase immediately, no separate currency conversion step.

## Architecture

- `Code/AppExecute.java` — entry point, builds the base `JFrame`
- `helper/GameManager.java` — swaps the active `JPanel` (menu, game, shop, end screen) without recreating the window
- `Code/MainWindow.java` — main menu UI
- `Code/Window.java` — core gameplay: pipe spawning, physics, collision, scoring, and the score-to-balance payout on death
- `Code/MultiplayerWindow.java` — runs two `Window` instances side-by-side with independent key listeners
- `Code/ShopWindow.java` — shop UI, wired to `Skins.java` for purchases
- `Code/Skins.java` — purchase logic and skin ownership persistence
- `Code/Equipped.java` — tracks and persists which skin is currently equipped
- `Code/Points.java` — persistent coin balance, backed by a flat text file
- `Code/Sound.java` — audio playback
- `Code/GameEnd.java` — end-of-run screen, shows points earned and win/loss state in multiplayer

## Running it

Open in Eclipse (project includes `.classpath` / `.project`) or compile directly:

```bash
javac -d bin src/Code/*.java src/helper/*.java
java -cp bin Code.AppExecute
```

## Controls

Space / click to flap. Avoid the pipes. In multiplayer, both players share the window with independent controls.
