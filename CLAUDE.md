# minorGems

General-purpose C++ utility and platform-abstraction library. Used by both the One Life client and server.

## Directory Structure

| Folder | Purpose |
|--------|---------|
| `network/` | Socket abstractions: `Socket`, `SocketServer`, `SocketClient`, `SocketPoll`, `SocketStream`, `HostAddress` |
| `game/` | Platform-independent game loop abstraction; `game.h` declares the interface |
| `game/platforms/SDL/` | SDL-backed platform implementation including socket I/O wrappers (`gameSDL.cpp`) |
| `crypto/` | SHA-1, HMAC-SHA1 (used for login authentication in One Life) |
| `util/` | `SimpleVector`, `SettingsManager`, `stringUtils`, logging (`AppLog`/`FileLog`), random sources |
| `graphics/` | Graphics utilities |
| `sound/` | Audio utilities |
| `ui/` | UI utilities |
| `system/` | System-level utilities |
| `math/` | Math utilities |
| `io/` | I/O utilities |
| `formats/` | File format utilities |

## Key Networking API

Declared in `game/game.h`, implemented in `game/platforms/SDL/gameSDL.cpp`:

| Function | Purpose |
|----------|---------|
| `openSocketConnection(addr, port)` | Opens a non-blocking TCP socket, returns integer handle |
| `sendToSocket(handle, data, len)` | Non-blocking send |
| `readFromSocket(handle, buffer, len)` | Non-blocking read (0 = no data, -1 = error) |
| `closeSocket(handle)` | Close and clean up |

Server-side uses `SocketServer` and `SocketPoll` directly from `network/`.

## Key Crypto API

`crypto/hashes/sha1.h` — HMAC-SHA1 used in the One Life login handshake to hash passwords and account keys against the server challenge string.
