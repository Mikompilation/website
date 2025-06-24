# Summary
Fatal Frame 1 uses an Atypical enum switch case design for modes of ingame functionality. 
As far as we are currently aware the modes are the same across versions. (`PAL, NTSC`)
Ingame uses several structs to define and interact with the various logic throught the engine though most prolific is `ingame_wrk`

# Modes

### Ingame Work Modes
<details>
<summary>List Of INGAME MODE</summary>
```c
enum {
	INGAME_MODE_FIRST_LOAD = 0,
	INGAME_MODE_INIT = 1,
	INGAME_MODE_WAIT = 2,
	INGAME_MODE_NEW_GAME = 3,
	INGAME_MODE_LOAD_START = 4,
	INGAME_MODE_MSN_TITLE = 5,
	INGAME_MODE_NOMAL = 6,
	INGAME_MODE_EVENT = 7,
	INGAME_MODE_SPECIAL_EVENT = 8,
	INGAME_MODE_AREA_MOVE = 9,
	INGAME_MODE_MENU = 10,
	INGAME_MODE_PAUSE = 11,
	INGAME_MODE_SPD_MAP = 12,
	INGAME_MODE_SPD_OPT = 13,
	INGAME_MODE_GET_ITEM = 14,
	INGAME_MODE_WANDER_SOUL = 15,
	INGAME_MODE_SAVE_POINT = 16,
	INGAME_MODE_PHOTO_AFTER = 17,
	INGAME_MODE_GHOST_DEAD = 18,
	INGAME_MODE_SGST_DISP = 19,
	INGAME_MODE_GAME_OVER = 20,
	INGAME_MODE_GAME_OVER_ALBUM = 21,
	INGAME_MODE_INTER_MSN = 22,
	INGAME_MODE_ENDING = 23,
	INGAME_MODE_WAIT_MSN0 = 24
};
```
</details>

## Process of Initalization
The process of Initalization starts wtih mode `INGAME_MODE_INIT`
Calls [InGameInit](https://decomp.me/scratch/8dB6u)
Where all ingame engine initalization's occur prior to the title screen.
Most notably loads Player data, preloads Model data, initalizes the event system 
And most other systems as well.

Then we continue to `INGAME_MODE_MSN_TITLE`
[InGameInit2](https://decomp.me/scratch/IJ5HJ) is called
Stage data, Camera data, all rendering systes are loaded here.
Memory Card data will have already been read prior to this being called and the player set into the scene.

## Missions

### Zero Hour
Mafuyu, Miku's older brother is playable in this mode, and this mode only.
Features it's own Battle System found mainly in `ap_zgost.c`, `ZeroHourAppearMain` being the main spawn logic for it.
Appears to feature it's own physics logic that does not apply to Miku.
Mission uses black and white filter effect over screen that is used throught many scenes of the game.
Force activating the debug menu allows this filter to be turned on and off at a whim.

### Miku Missions, Nights 1, 2, 3, 4
The main logic of the game. All Standard modes, battle functions, events, room transitions, etc apply here.

- `INGAME_MODE_NORMAL`:
The main game loop. Player control and gameplay stuff occurs in here.
This will also check for the BattleModeGame if the player has previously completed this game and selected it.

- `INGAME_MODE_EVENT`:
Calls [EventMain](https://decomp.me/scratch/AvnAm)
Event system is run here. Will be talked about in more detail in other documentation.
Needless to say, this wrenches control from main game loop and subsuqently player.

- `INGAME_MODE_SPECIAL_EVENT`:
Special events consist of several different types and functions.
Though most notable are the ingame puzzles

  - Star Puzzle (The Sliding Stone game)
  - Dial Key Door (The Number lock combination doors)
  - Doll Puzzle (Kaaggommee, Kaaggommee) - Used only a single time in Night 2

At least some of these have their own list of files on disc for hard coded puzzles.
Each of these each have their own seperate game loop that takes inputs.