# Nintendo DS Platformer

A 2D platformer for the Nintendo DS, written in C with [devkitPro](https://devkitpro.org/) (devkitARM + libnds). Developed as a group project for the Computer Structure course (*Estructura de Computadores*) at the University of the Basque Country (UPV/EHU), 2024–2025.

<!-- Add a screenshot or GIF here, e.g. ![Gameplay](docs/gameplay.gif) -->

## Features

- Three levels, with a level-select screen that unlocks levels as you clear them
- Five lives and a 60-second countdown per attempt
- Touch-screen menus (start, level select, tutorial) and a pause screen
- Sprites and backgrounds converted from PNG with grit

## Low-level details

The project works directly with the DS hardware rather than relying only on library helpers:

- **Memory-mapped registers:** the keypad, timer and interrupt-control registers (`IME`, `IE`, `IF`, `TIMER0_CNT`, `TIMER0_DAT`, `TECLAS_CNT`…) are defined and configured by hand in `include/definiciones.h` and `source/perifericos.c`.
- **Interrupt-driven input and timing:** Start/Select are handled through keypad interrupts and the countdown through a timer interrupt, each with its own service routine (`source/rutinasAtencion.c`).
- **State machine:** the game loop in `source/juego.c` switches between menu, tutorial, level select, gameplay, pause, game over and victory states.

## How to Build

1. Install [devkitPro](https://devkitpro.org/wiki/Getting_Started) with the `nds-dev` package group, and make sure `DEVKITARM` is set in your environment.
2. From the project root, run:

   ```bash
   make
   ```

   This produces `platformer-nds.nds` (the file name follows the folder name).
3. Open the `.nds` file in a Nintendo DS emulator such as [melonDS](https://melonds.kuribo64.net/) or DeSmuME.

## Controls

| Input            | Action |
|------------------|--------|
| D-pad left/right | Move   |
| B                | Jump   |
| Start            | Start game (menu) / pause (in game) |
| Select           | Level select (in game) |
| Touch screen     | Menu buttons |

## Project Structure

- `source/`: game code (game loop, player, levels, sprites, backgrounds, peripherals, interrupt routines)
- `include/`: headers and hardware register definitions
- `gfx/`: PNG graphics and their grit conversion settings
- `Makefile`: devkitPro build script

## Authors

Developed as a group project with fellow students.
