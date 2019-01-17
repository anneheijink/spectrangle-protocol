# spectrangle-protocol
This is a protocol definition of the spectrangle game. Possible extensions are defined in the extensions directory. Examples on how to use the protocol can be found in the examples directory.

Values between angle brackets ( &lt; &gt; ) indicate a _required_ argument. (occurs exactly 1 time)  
Values between square brackets ( [ ] ) indicate an _optional_ argument. (occurs 0 or 1 times)  
An ellipsis (...) indicates the possible repetition of the (group of) arguments since the last whitespace.


## Client-to-server commands
**JOIN &lt;playerName&gt; \[lobbyName\]**  
The player indicates he wants to join a lobby. Servers that do not support the multilobby extension should ignore the _lobbyName_ argument.

**READY**  
The player indicates he is ready to start the game.

**MOVE_PLAY &lt;tile&gt; &lt;location&gt;**  
The player places a tile on the board.

**MOVE_SWAP &lt;tile&gt;**  
The player swaps a tile from his inventory with a tile in the bag.
This command is only valid when it's the players turn and the player is not able to make a valid move.

**MOVE_SKIP**  
The player skips his turn. This command is only valid when it's the players turn and the player is not able to make a valid move.

**EXIT**  
The player indicates he leaves the lobby/game.

## Server-to-client commands
**ERROR &lt;errorCode&gt; &lt;errorMessage&gt;**  
This is sent to the client when the client has sent an invalid command to the server.

**LOBBY \[playerName\] ...**  
The server confirms the client has succesfully entered the lobby, and lists the other players that are in the lobby.
Note this command can be sent every time a client enters or leaves the lobby.

**START &lt;playerName&gt; ...**  
The game has started with the players listed. Players take turns in the order listed. Note a game should only be started when all players in the lobby have sent the READY command.

**UPDATE &lt;playerName&gt; \[tile\] [location]**   
This indicates the player has finished his turn. When the player made a moved, this will be specified by the _tile_ and _location_ arguments. When the player skipped his turn, _tile_ and _location_ will not be present. When the player swapped a tile, only the _playerName_ and _tile_ arguments will be present. The _tile_ argument always indicates a tile that is to be removed from the player's inventory.

**TILE &lt;playerName&gt; &lt;tile\>**  
A tile has been given to a player.
In case the player skipped his turn, this command will not be sent.
In case the player swapped a tile, this command will be sent in combination with an UPDATE command.

**SCORE &lt;playerName&gt;,&lt;points&gt; &lt;playerName&gt;,&lt;points&gt; ...**  
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

**location**  
An integer between 0 and 35. It can be calculated using the formula `index=row^2+rowIndex`, where row is the row number starting at 0, and rowIndex starting at 0 for the leftmost field.

**errorCode**  
An integer value describing the error type. This must be a value described in the _error codes_ section. A value of 0 must be used when this function is not implemented.

**errorMessage**  
A textual representation of the error, intended to be displayed to the user.

**points**  
An integer value greater than or equal to 0.

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
- **9**: Unsupported extension
