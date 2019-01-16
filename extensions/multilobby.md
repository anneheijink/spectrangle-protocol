# Multi-lobby extension



## Client-to-server commands
- **JOIN &lt;playerName&gt; \[lobbyName\]**  
Same behaviour as described in the base protocol.
When _lobbyName_ is specified and the player is not able to join the lobby (eg. full lobby), the server should respond with an ERROR command.
When _lobbyName_ is specified and the lobby does not exist, the server should create a lobby with that name and respond with a LOBBY command.

- **LOBBIES**  
Requests the server to send a list of active lobbies. The server sends an ACTIVE_LOBBIES command in response.

## Server-to-client commands
- **ACTIVE_LOBBIES &lt;lobbyName&gt;,&lt;playerName&gt;,\[playerName\] ...**  
Lists all active lobbies on the server. Different lobbies are separated by whitespaces. The players in each lobby are displayed as a comma-separated list.

## Command arguments
- **lobbyName**  
  The lobby name.  
  Allowed Characters: [A-Za-z0-9\_.-], so:
  - letters and capital letters
  - digits
  - underscore
  - period
  - hyphen

- **playerName**  
  The player name, as described in the base protocol.
