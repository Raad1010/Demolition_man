Gameplay

The game contains a number of entities that will need to be implemented within your application.

Map

The map designates where Bomb Guy and enemies are allowed to move. Laid out as a grid, enemies can
move along rows and columns where there is no wall. Maps are 13 rows tall, and 15 columns wide, with a 64
pixel offset between the top of the screen and the start of the first row. Each grid space is 32x32 pixels.
There are 4 different tile types within the map: solid, broken, empty and goal. Solid tiles cannot be broken
and form physical barriers for Bomb Guy and the enemies. Broken tiles also form physical barriers for Bomb
Guy and the enemies, however can be broken with the use of bombs. Empty tiles can be traversed through.
The goal tile is the target tile for Bomb Guy. Upon reaching the Goal tile, the player has completed the level.
Enemies can traverse through the Goal tile.
Map layouts are stored in text files, and the name of the map file can be found in config.json under the “path”
attribute. Sample Map and config.json files can be found under resources on Ed. Map files store the maps as
multidimensional character arrays, where each character represents what is in that cell. Note that a map is
valid if it has a bounding border, a starting location for Bomb Guy, and a Goal Tile (all maps used for marking
will be valid, but you should write your own tests for invalid maps and handle them as you see fit). There is
no minimum requirement for the number of enemies, or the layout of the remainder of the map. Note that
if another character is represented in the Map file (for example, ‘P’ to represent the starting location for
Bomb Guy), the tile should be empty.

Bomb Guy

Bomb Guy is the player-controlled character in the game. Bomb Guy can move vertically and horizontally on
the map and cannot pass through walls. Bomb Guy is controlled with the arrow keys (up, down, left and
right). Bomb Guy changes their grid space on the map when the key is pressed (not held). For example, if the
player presses down the left key, Bomb Guy should move one grid space to the left (assuming that they are
able to). Bomb Guy should not move left again until the player releases the left key and presses it again.
Also present in the configuration file is the number of lives Bomb Guy has. The field is stored under the “lives”
attribute. Bomb Guy can lose a life whenever they collide with an enemy or an explosion.
Bomb Guy has four sprites that can be rendered for each cardinal direction that form a walking animation
cycle. Each sprite should be rendered for 0.2 seconds before moving onto the next sprite in the cycle. Bomb
Guy should face same direction as they have just moved. For example, if Bomb Guy has just moved left, then
the left-facing animation cycle should be rendered. Similarly, if Bomb Guy has just moved down, then the
down-facing animation cycle should be rendered. On start-up, Bomb Guy should begin with the down-facing
animation cycle.
When Bomb Guy reaches the goal tile, the next level should be loaded. Each level is stored in order in the
configuration file in the field “levels”. If Bomb Guy reaches the goal tile for the final level, the win screen is
shown.
Bomb Guy’s starting location is marked in the map file with the ‘P’ character.

Enemies

Enemies are the antagonists of Bomb Guy. Like Bomb Guy, enemies can move horizontally and vertically on
the map. They cannot pass through solid and broken walls, however can pass through each other. All enemies
move once every second, according to the AI for the specific enemy type. The Red Enemy moves in a straight
line and turns to a random decision every time its path is blocked by a solid/broken wall. The Yellow Enemy
moves in a straight line, but on collision with a wall will attempt to move clockwise (if it was moving left, it
will try to move up, and if unable to, then try right and then left; similarly if it was moving down, it will try to
move left, otherwise up or right).
When an enemy occupies the same grid space as Bomb Guy, Bomb Guy loses a life and the current level is
reset. When Bomb Guy loses all of his lives, the game ends.
All enemies have the same animation patterns as Bomb Guy, with a 4 frame walking cycle animation for each
cardinal direction, with each frame lasting 0.2 seconds.

Bomb

Bomb Guy has an infinite supply of bombs which they can use to help clear a path to the goal and remove
enemies. When the player presses the SPACE key, Bomb Guy places a bomb on the grid space that they are
standing on. The bomb remains stationary there for 2 seconds, at which point it detonates, causing an
explosion.
The explosion’s shockwave and fire extend in the four cardinal directions to a maximum of 2 grid spaces
away from the location the bomb was placed. The explosion can be stopped earlier than 2 spaces if it
comes in contact with a wall (either solid or broken), however broken tiles are then turned into empty tiles
if they are caught in an explosion. An example of this can be seen below with before, during and after
screenshots of an explosion.
If Bomb Guy is caught in the explosion, they lose a life and the level resets (assuming they have more than
1 life). If an enemy is caught in the explosion, they are removed from the level.
The bomb has 8 sprites used for its animation. Each sprite should last for 0.25 seconds, such that when the
final sprite ends, the explosion begins.
There are 3 sprites for the explosion. The centre sprite is used where the bomb was placed. The horizontal
explosion sprite is used for explosions in the same row as the original placement. The vertical explosion
sprite is used for explosions in the same column as the original placement. The explosion should remain on
the screen for 0.5 seconds.

UI

There are two main UI elements present on the screen: the number of lives remaining, and the time
remaining for the level. Both should be shown at the top of the screen, using the provided icon sprites and
PressStart2P-Regular.ttf font.
Note that the time remaining in seconds for each level is stored in the configuration file under the field
“time”. If the timer reaches 0, the player loses the game.

Game Over Screen

There are two loss conditions for the game: Bomb Guy loses all of their lives, and the level timer reaches 0
seconds remaining. When a loss condition is reached.

Win Screen

If Bomb Guy reaches the goal tile for the final level before any loss condition is reached, the player wins the
game.
