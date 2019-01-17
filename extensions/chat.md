# Chat extension

## Client-to-server commands
- **CHAT &lt;chatMessage&gt;**  
Send a new chat message.

## Server-to-client commands
- **CHAT_MESSAGE &lt;playerName&gt; &lt;chatMessage&gt;**  
A new chat message has arrived. playerName indicates the player who sent the message.

## Command arguments
- **chatMessage**  
  The chat message. This is a base64-encoded string that contains the chat message.

- **playerName**  
  The player name, as described in the base protocol

## Base64 in Java
Base64 in Java can be used in the following manner:

````Java
System.out.println(Base64.getEncoder().encodeToString("Hello, world!😋".getBytes()));
System.out.println(new String(Base64.getDecoder().decode("SGVsbG8sIHdvcmxkIfCfmIs=")));
````
