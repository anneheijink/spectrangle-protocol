# Chat extension

## Client-to-server commands
- **CHAT &lt;chatMessage&gt;**  
Send a new chat message.

## Server-to-client commands
- **CHAT_MESSAGE &lt;playerName&gt; &lt;chatMessage&gt;**  
A new chat message has arrived. playerName indicates the player who sent the message.

## Command arguments
- **chatMessage**  
  The chat message. This is always the last argument in a command.
  Allowed Characters: [A-Za-z0-9 \_.,-~], so:
  - letters and capital letters
  - digits
  - whitespace
  - underscore
  - period
  - comma
  - hyphen

- **playerName**  
  The player name, as described in the base protocol
