# Maze Game (OpenGL/GLUT)

A simple, fast-paced maze game built with C++ and OpenGL/GLUT. Reach the goal before the timer runs out, avoid enemies, and watch out for trap dots!

## Overview

- Grid-based maze rendered with OpenGL (orthographic view)
- Win by reaching the green goal square before time ends
- Collect gold dots along the way (optional)
- Enemies patrol corridors — touching one ends the game
- Trap dots instantly end the game with a special message

Core gameplay and rendering live in [Maze Game/main.cpp](Maze%20Game/main.cpp).

## Controls

- Arrow keys: Move
- `R`: Restart
- `Q` or `Esc`: Quit

## Requirements

- Windows (tested with Visual Studio 2012 project structure)
- Visual Studio (2012 or newer recommended)
- OpenGL libraries: `opengl32.lib`, `glu32.lib`
- GLUT implementation: either classic `glut32.lib` or `freeglut.lib`

This project includes headers `gl/gl.h` and `gl/glut.h`. If your environment does not have GLUT installed, use FreeGLUT.

### Installing GLUT/FreeGLUT (Windows)

- Option A (classic GLUT): Install GLUT and add `glut32.lib` to your Linker → Input, and place `glut32.dll` next to your executable (e.g., in the `Debug/` output folder).
- Option B (FreeGLUT): Install FreeGLUT, add `freeglut.lib` to Linker → Input, ensure headers are in your Include path, and place `freeglut.dll` next to your executable.
- Always link `opengl32.lib` and `glu32.lib` in addition to GLUT/FreeGLUT.

## Build & Run

1. Open the solution: [Maze Game.sln](Maze%20Game.sln) in Visual Studio.
2. Set Configuration to `Debug` and Platform to `Win32`/`x86`.
3. Verify Linker → Input contains:
   - `opengl32.lib`, `glu32.lib`, plus one of: `glut32.lib` or `freeglut.lib`.
4. Build the project (Build → Build Solution).
5. Ensure the corresponding `glut32.dll` or `freeglut.dll` is in the same folder as the executable (e.g., [Maze Game/Debug](Maze%20Game/Debug)).
6. Run with `F5` or start without debugging.

## Gameplay Details

- Maze size: 11 rows × 15 columns
- Cell size: 40 units
- Time limit: 14 seconds (display turns red under 6 seconds)
- Tile types:
  - `1`: Wall (dark gray)
  - `2`: Dot (gold)
  - `3`: Goal (green)
  - `4`: Enemy spawn (red enemies patrol horizontally)
  - `5`: Trap dot (looks like a dot; hitting it ends the game)
- Player: Yellow Pac-Man-style shape
- Enemies: Red circles; collision radius tuned for fast gameplay

Messages shown when the game ends:

- Win: "YOU WIN!"
- Trap: "You LOSE!"
- Timeout/lose: "TIME OVER - YOU LOSE!"

## Project Structure

```
Maze Game.sln
Maze Game.sdf
Debug/
  Maze Game.ilk
Maze Game/
  main.cpp
  Maze Game.vcxproj
  Maze Game.vcxproj.filters
  Debug/
    Maze Game.lastbuildstate
```

## Troubleshooting

- Compiler error: `gl/glut.h` not found
  - Install GLUT/FreeGLUT and add its Include path.
- Linker errors: unresolved GLUT/OpenGL symbols
  - Add `opengl32.lib`, `glu32.lib`, and `glut32.lib` or `freeglut.lib` to Linker → Input.
- Runtime error: `glut32.dll`/`freeglut.dll` missing
  - Place the DLL next to the built executable (e.g., `Debug/`).
- Black or empty window
  - Verify your GPU/driver supports OpenGL; ensure the DLLs match architecture (x86 for Win32 builds).

## Notes

- The timer runs via GLUT timers; enemies update at ~60 FPS.
- Maze layout and tile codes are defined directly in `main.cpp` and can be edited to customize levels.

Enjoy the challenge — reach the goal before the clock runs out!
