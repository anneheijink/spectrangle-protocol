1. &gt;  JOIN alice
2. &lt;  LOBBY alice
3. &lt;  LOBBY alice,bob
4. &gt;  READY
5. &lt;  START bob,alice
6. &lt;  TILE alice RRP0
7. &lt;  TILE alice BRP0
8. &lt;  TILE alice WWW0
9. &lt;  TILE alice RYB0
10. &lt; TILE bob RRR0
11. &lt; TILE bob RRY0
12. &lt; TILE bob YBP0
13. &lt; TILE bob YBP0
14. &lt; UPDATE bob RRY1 6
15. &lt; TILE bob PPR0
16. &gt; MOVE RRP2 6
17. &lt; ERROR 6 This field is already taken.
18. &gt; MOVE RRP2 35
19. &lt; UPDATE alice RRP2 35
20. &lt; TILE alice PPP0
21. ...
22. &lt; SCORE alice,50 bob,60
23. &gt; EXIT

# Explanation
The communication between Alice and the server is shown above.

At first, Alice tries to join the lobby (1). Since she is the first player entering the lobby, the server answers with a LOBBY command, containing only Alice's name (2). After a while, Bob also joins the lobby. The server sends a new LOBBY command to both Alice and bob (3).

Alice and Bob have decided they want to play a 2-player game, so they both send a READY command (4). After the server has received a READY command from all players in the lobby, it will send a START command, with the players that are playing as arguments (5). The players will also take turns in this order.

At the start of the game the server will hand each player four tiles (6-13). At this moment Alice has to wait for Bob to make his turn. When Bob has made a move, the server tells this to the other players by sending an UPDATE command (14). At this moment Alice knows it's her turn. Immediately after the UPDATE command, the server sends a TILE command to hand Bob a new tile (15). Note this command wouldn't have been sent if Bob had skipped his turn.

Next Alice tries to make a move (16). In this example, Alice forgets to do proper checking before she sends her MOVE command to the server. Because she tries to place the tile on a field that is already taken, the server responds with an ERROR command (17). Now Alice knows her attempted move was invalid and she has to try again.

She tries again by using a different location (18). This time, her attempted move is valid. The server confirms this by sending an UPDATE command to all players (19). Immediately after this, Alice is handed a new tile (20).

After this, Bob and Alice continue playing their game (21). When the game is finished (ie. no players can make a valid move) the server indicates the game is finished by sending a SCORE command (22). Alice decides she doesn't want to play anymore, so she sends an EXIT command to exit the game (23). In case she would want to play a new game with these players, she would have sent a READY command.
