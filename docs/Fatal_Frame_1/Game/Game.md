# Summary
Game is the inializer of Fatal Frame that has different types each with different functions.
Game is used to select the current "Game Mode" that lead each to their own state machines and modes.

[Main Function of Game](https://decomp.me/scratch/I3p0e)

## Types of Game
<details>
<summary>List Of Game</summary>
```c
enum GAME_MODE {
	GAME_MODE_INIT = 0,
	GAME_MODE_MCCHECK = 1,
	GAME_MODE_OUTGAME = 2,
	GAME_MODE_INGAME = 3
};
```
</details>

## Modes

### INIT
Initalizer on first startup, Calls [GameInit](https://decomp.me/scratch/1bB4V) -> [GameInitLoad](https://decomp.me/scratch/Q5V7S) as well as [gra3dInit](https://decomp.me/scratch/NOvdS) to initalize some renderer params

<details>
<summary> List of Game Init</summary>
```c
enum {
	GAME_INIT_LOAD_START = 0,
	GAME_INIT_LOAD_MSG_DAT = 1,
	GAME_INIT_WAIT_MSG_DAT = 2,
	GAME_INIT_LOAD_FONT_TEX = 3,
	GAME_INIT_WAIT_FONT_TEX = 4,
	GAME_INIT_LOAD_SE_STAT = 5,
	GAME_INIT_WAIT_SE_STAT = 6,
	GAME_INIT_LOAD_END = 7
};
```
</details>

Initalization is done in a simplistic Switch case design, step by step.
Load required files, sets next step, processes files and continue.

### MCCHECK 
[mcStartCheckMain](https://decomp.me/scratch/jA7bV)
Checks for valid inserted card and checks for space.
Works in steps to do so.


### OUTGAME
[OutGameCtrl](https://decomp.me/scratch/fSeg3)
Outgame encompases several key functions including Title Screen, save menus and other non InGame functions including starting Battle Mode.
Outgame's main purpose is anything before or after gameplay.
Displays the main logo's before actual gameplay starts
Sets and loads all title screen functions
Handles Battle Mode menus and mode changing
Handles all other menus, Options, Debug's, etc.

### INGAME
[InGameCtrl](https://decomp.me/scratch/wcowl)
[InGameMain](https://decomp.me/scratch/1ERKo) - Note original match by Karas. This is adjusted, adding a missing jtbl and enums

The Main Functionality of this engine where the main game loop and all other main game stuff occurs.
Ingame has several modes and functions that occur in those modes.