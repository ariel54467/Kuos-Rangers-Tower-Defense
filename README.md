# Kuo's Rangers

Kuo's Rangers is a C++ tower-defense game built with CMake and Allegro 5. Choose a troop roster, defend the route with several turret types, use special abilities, and compete for a place on the local scoreboard.

## Features

- Start, settings, troop selection, gameplay, win, lose, and scoreboard scenes
- Five selectable troop types
- Multiple enemies and defensive turrets
- Reverse-BFS enemy pathfinding
- Freeze and missile abilities
- Economy and ability upgrades
- Adjustable BGM and sound-effect volume
- Persistent local scoreboard with player name, score, and date
- Two map and enemy-wave resource sets

## How To Play

1. Select **Play** from the main menu.
2. Choose at least one troop for your roster. You can select up to four.
3. Select **Start** to begin the stage.
4. Use the buttons along the bottom of the game screen to buy defenses and abilities.
5. Use the mouse to interact with buttons and place supported defenses.
6. Stop enemies from reaching the end of the route. Losing all lives ends the game.
7. After winning, enter a player name before returning so the score can be saved.

### Keyboard Shortcuts

| Key | Action |
| --- | --- |
| `Q` | Select/buy the machine-gun turret |
| `W` | Select/buy the laser turret |
| `E` | Select/buy the missile turret |
| `R` | Select/buy the fourth turret |
| `0`-`9` | Set the game-speed multiplier |
| `Tab` | Toggle pathfinding debug values |

## Project Structure

```text
.
+-- Bullet/             Projectile classes
+-- Enemy/              Enemy classes and movement behavior
+-- Engine/             Game engine, resource, audio, and scene systems
+-- Resource/           Maps, waves, images, fonts, audio, and scoreboard
+-- Scene/              Menus, gameplay, settings, and result scenes
+-- Turret/             Turret and defensive-unit classes
+-- UI/                 Reusable controls and animation components
+-- CMakeLists.txt      CMake build definition
+-- main.cpp            Program entry point
+-- windows.cmd         Windows build-and-run helper
```

## Windows Requirements

- 64-bit Windows
- CMake 3.27 or newer
- LLVM-MinGW or another compatible 64-bit MinGW toolchain
- Allegro 5 MinGW development SDK with monolith library support

The compiler's `bin` folder must be on `PATH`. It must provide a C++ compiler such as `clang++.exe` or `g++.exe`, plus `mingw32-make.exe`.

The Allegro SDK folder must contain:

```text
include/allegro5/allegro.h
lib/liballegro_monolith.dll.a
```

By default, the build looks for Allegro under `C:\allegro`. To use another location, set `ALLEGRO_ROOT` to the SDK folder.

Example PowerShell setup:

```powershell
$env:Path = "C:\llvm-mingw\bin;$env:Path"
$env:ALLEGRO_ROOT = "C:\allegro"
```

## Build And Run On Windows

Open a terminal in the project root and run:

```powershell
.\windows.cmd
```

The script checks the required tools, configures CMake, builds the game, copies the resources and Allegro DLL to `build`, and starts the game.

To compile without starting the game, run `windows.cmd --build-only`.

To build manually:

```powershell
cmake -S . -B build -G "MinGW Makefiles" -DCMAKE_BUILD_TYPE=Debug -DALLEGRO_ROOT="$env:ALLEGRO_ROOT"
cmake --build build --parallel 8
.\build\2024_I2P2_TowerDefense_with_answer.exe
```

Run the executable from inside the `build` folder. The game loads `Resource` files relative to its working directory.

## Linux And macOS

Install CMake, a C++14 compiler, `pkg-config`, Allegro 5, and the Allegro image, font, TTF, primitives, audio, and codec add-ons. Then run:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build --parallel
./build/2024_I2P2_TowerDefense_with_answer
```

## Moving To Another Laptop

Copy or clone the entire project. Keep `Resource`, all source folders, `CMakeLists.txt`, and `allegro_monolith-5.2.dll` together. The `build` folder is generated and does not need to be copied or uploaded.

On the new laptop:

1. Install CMake and LLVM-MinGW.
2. Install or copy the Allegro 5 MinGW SDK.
3. Add the compiler `bin` directory to `PATH`.
4. Set `ALLEGRO_ROOT` if Allegro is not located at `C:\allegro`.
5. Run `windows.cmd` from the project root.

## Troubleshooting

### Allegro headers or library not found

Check that `ALLEGRO_ROOT` points to the SDK folder, not its `include` subfolder.

### CMake reports a generator mismatch

Delete only the generated `build` folder, then run `windows.cmd` again.

### The game starts but resources are missing

Build with CMake and run the executable from the `build` folder. CMake copies the complete `Resource` directory there.

### Missing Allegro DLL

Confirm that `allegro_monolith-5.2.dll` is present in the project root, then rebuild.
