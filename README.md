# Flappy Bird 2D

A Flappy Bird clone built from scratch in Java using Swing/AWT — no game engine, just JFrame, JPanel, and a manual game loop.

## Features

- Classic side-scrolling pipe-dodging gameplay with custom collision detection
- **Local split-screen multiplayer** — two players race side-by-side in the same window
- **Shop system** — earn coins per run, unlock and equip 3 bird skins at increasing price tiers
- Persistent save data for points, skins, and equipped state (`resources/data/`)
- Sound effects for jumps and collisions

## Architecture

- `Code/AppExecute.java` — entry point, builds the base `JFrame`
- `helper/GameManager.java` — swaps the active `JPanel` (menu, game, shop, end screen) without recreating the window
- `Code/MainWindow.java` — main menu UI
- `Code/Window.java` — core gameplay: pipe spawning, physics, collision, scoring
- `Code/MultiplayerWindow.java` — runs two `Window` instances side-by-side with independent key listeners
- `Code/ShopWindow.java` / `Skins.java` / `Points.java` / `Equipped.java` — currency, unlocks, and persistence
- `Code/Sound.java` — audio playback
- `Code/GameEnd.java` — end-of-run screen with score and replay

## Running it

Open in Eclipse (project includes `.classpath` / `.project`) or compile directly:

```bash
javac -d bin src/Code/*.java src/helper/*.java
java -cp bin Code.AppExecute
```

## Controls

Space / click to flap. Avoid the pipes. In multiplayer, both players share the window with independent controls.
