1. &gt;  JOIN alice
2. &lt;  LOBBY alice
3. &lt;  LOBBY alice,bob
4. &gt;  READY
5. &lt;  START bob,alice
6. &lt;  TILE alice RRP0,BRP0,WWW0,RYB0
7. &lt;  TILE bob RRR0,RRY0,RRY0,YBP0
8. &lt;  UPDATE bob RRY1 6
9. &lt;  TILE bob PPR0
10. &gt; MOVE RRP2 6
11. &lt; ERROR 6 This field is already taken.
12. &gt; MOVE RRP2 35
13. &lt; TILE alice PPP0
14 ...
15. &lt; SCORE alice,50 bob,60
16. &gt; EXIT

# Explanation
At first, Alice tries to join the lobby (1). Since she is the first player entering the lobby, the server answers with a LOBBY command, containing only Alice's name (2). After a while, Bob also joins the lobby. The server sends a new LOBBY command to both Alice and bob (3).
