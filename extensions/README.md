# Spectrangle protocol extensions
In this directory possible extensions for the spectangle protocol are defined. Since a server doesn't have to implement extensions,

Described extensions:
- Chat
- Multiple lobbies
- Mirrored tiles

## Client-to-server commands
- **EXTENSIONS &lt;extensionName&gt; ...**  
Requests the server to send a list of supported extensions. When the server doesn't support any extensions, the server may respond with an ERROR command (same behaviour as any other unknown command). When the server supports one or more extensions, it must respond with an AVAILABLE_EXTENSIONS command. This command can be sent at any time, also before the JOIN command.


- **ENABLE_EXTENSION &lt;extensionName&gt; ...**  
Inform the server that the client can handle the extension(s). In case the server doesn't support the requested extension(s), the server should respond with an unsupported extension error. Note: this doesn't neccesarily mean the server is going to use the specified extensions. 

## Server-to-client commands
- **AVAILABLE_EXTENSIONS &lt;extensionName&gt; ...**  
A list of available extensions

## Command arguments

- **extensionName**  
Must be one of the following:
  - chat
  - multilobby
  - mirrored
