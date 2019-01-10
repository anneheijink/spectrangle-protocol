# spectrangle-protocol
This is a protocol definition of the spectrangle game. Possible extensions are defined in the extensions directory. Examples on how to use the protocol can be found in the examples directory.

Values between angle brackets (&lt; and &gt;) indicate a _required_ argument.  
Values between square brackets ([ and ]) indicate an _optional_ argument.


## Client-to-server commands
**JOIN &lt;playerName&gt; \[lobbyName\]**  
The player indicates he wants to join a lobby.

**READY**  
The player indicates he is ready to start the game.

**MOVE PLAY &lt;tile&gt; &lt;location&gt;**  
The player places a tile on the board.

**MOVE SWAP &lt;tile&gt;**  
The player swaps a tile from his inventory with a tile in the bag.
This command is only valid when it's the players turn and the player is not able to make a valid move.

**MOVE SKIP &lt;tile&gt;**  
This command is only valid when it's the players turn and the player is not able to make a valid move.

**EXIT**  
The player indicates he leaves the lobby/game.

## Server-to-client commands
**ERROR &lt;errorCode&gt; &lt;errorMessage&gt;**  
This is sent to the client when the client has sent an invalid command to the server.

**LOBBY &lt;playerName&gt;**  
The server confirms the client has succesfully entered the lobby, and lists the other players that are in the lobby.
Note this command can be sent every time a client enters or leaves the lobby.

**START &lt;playerName&gt;**  
The game has started with the players listed. Players take turns in the order listed. Note a game should only be started when all players in the lobby have sent the READY command.

**TILE &lt;playerName&gt;,&lt;tile\>,[oldTile]**  
A tile has been given to a player. This also indicates it's the next players turn.
When there are no tiles left or a player skipped his turn, this command will not have any arguments.
When a player has swapped tiles, oldTile indicates the tile that has been removed from the players inventory.

**SCORE &lt;playerName&gt;,&lt;points&gt;**  
This indicates that the game has finished.

## Command arguments
**playerName**  
The display name of the player. Allowed characters: [A-Za-z0-9_-], so:
- letters and capital letters
- digits
- underscore
- dash

**tile**  
The definition of a tile, consisting of 3 letters and one digit. See also Tile definition.

**errorCode**  
An integer value describing the error type. This must be a value described in the _error codes_ section. A value of 0 must be used when this function is not implemented.

**errorMessage**  
A textual representation of the error, intended to be displayed to the user.

## Tile definition
A tile is always represented by 3 letters and one digit (eg. PPY1). When rotated 0 degrees, tiles are numbered counterclockwise, starting at the 'horizontal' face. The rotation is also defined counterclockwise. The digit is either 0, 1 or 2, depending on the rotation.

### examples
- ![0 degrees](https://raw.githubusercontent.com/anneheijink/spectrangle-protocol/master/images/0deg.png) RGB0

- ![120 degrees](https://raw.githubusercontent.com/anneheijink/spectrangle-protocol/master/images/120deg.png) RGB1

- ![240 degrees](https://raw.githubusercontent.com/anneheijink/spectrangle-protocol/master/images/240deg.png) RGB2

### used colors
The following letters are user for the colors:
- R: red
- G: green
- B: blue
- Y: yellow
- P: purple
- W: white

### tiles in the game
In total, there are 36 tiles in the game. Each tile is listed below with their corresponding value.
- RRR0 (6 points)
- BBB0 (6 points)
- GGG0 (6 points)
- YYY0 (6 points)
- PPP0 (6 points)
- RRY0 (5 points)
- RRP0 (5 points)
- BBR0 (5 points)
- BBP0 (5 points)
- GGR0 (5 points)
- GGB0 (5 points)
- YYG0 (5 points)
- YYB0 (5 points)
- PPY0 (5 points)
- PPG0 (5 points)
- RRB0 (4 points)
- RRG0 (4 points)
- BBG0 (4 points)
- BBY0 (4 points)
- GGY0 (4 points)
- GGP0 (4 points)
- YYR0 (4 points)
- YYP0 (4 points)
- PPR0 (4 points)
- PPB0 (4 points)
- YBP0 (3 points)
- RGY0 (3 points)
- BGP0 (3 points)
- GRB0 (3 points)
- BRP0 (2 points)
- YPR0 (2 points)
- YPG0 (2 points)
- GRP0 (1 point)
- BYG0 (1 point)
- RYB0 (1 point)
- WWW0 (1 point)

## Error codes
- **0**: Generic / unknown error.
- **1**: Unrecognized command.
- **2**: Invalid arguments.
- **3**: Invalid player name.
- **4**: Player name already taken.
- **5**: Not your turn.
- **6**: Invalid move.
- **7**: Not in a lobby.
- **8**: Not in a game.
