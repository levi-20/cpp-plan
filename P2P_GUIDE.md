# Steam P2P Chat App — Self-Guided Learning Plan

Build a minimal Steam chat app in C++ step by step. Each phase builds on the previous one — get each working before moving on.

**What you need before starting:**
- Two machines (or a friend with their own machine), each with Steam installed on separate accounts.
- A C++17 compiler (MSVC on Windows, GCC/Clang on Linux/macOS).
- CMake 3.16+.
- A free [Steamworks partner account](https://partner.steamgames.com) (the $100 fee is only for publishing — registration is free).
- The [Steamworks SDK](https://partner.steamgames.com/downloads/steamworks_sdk.zip) downloaded and extracted.

---

## Phase 1 — Hello Steam

**Goal:** Call `SteamAPI_Init()` successfully and print your Steam persona name.

This forces you to solve all the boring-but-essential setup: downloading the SDK, setting up CMake (or your preferred build system), linking the library, getting `steam_appid.txt` right, and having Steam running in the background.

**Read these:**
- [Getting Started / Installing the SDK](https://partner.steamgames.com/doc/sdk/installingsdk) — SDK download and folder structure
- [Initialization and Shutdown](https://partner.steamgames.com/doc/sdk/api#initialization_and_shutdown) — `SteamAPI_Init`, `SteamAPI_Shutdown`
- [ISteamFriends](https://partner.steamgames.com/doc/api/ISteamFriends) — `GetPersonaName()`

**Key things to figure out:**
- Where to put the SDK headers and libs so your build system finds them.
- What `steam_appid.txt` is, what goes in it (hint: `480`), and where it needs to live.
- What happens if Steam isn't running when you call `SteamAPI_Init()`.

**Done when:** You run your exe, it prints "Logged in as: YourSteamName", and exits cleanly.

---

## Phase 2 — Understand the Callback System

**Goal:** Understand how Steamworks async callbacks work before writing any real logic.

This is the most important concept in Steamworks. Almost everything is async — you call a function, and Steam fires a callback later with the result. If you skip this phase, everything after will be confusing.

**Read these:**
- [Callbacks](https://partner.steamgames.com/doc/sdk/api#callbacks) — how the callback system works
- The Spacewar sample in `sdk/examples/` — see how it registers and handles callbacks

**Key things to figure out:**
- What `SteamAPI_RunCallbacks()` does and why it must be called in a loop.
- What happens if you don't call it (hint: nothing else works).
- How the `STEAM_CALLBACK` macro works — what it generates under the hood.
- The difference between `STEAM_CALLBACK` (auto-registered) and `CCallResult` (for call-specific results).

**Done when:** You can explain to yourself why `SteamAPI_RunCallbacks()` must be called in a loop, and what happens if you don't.

---

## Phase 3 — Create and Join a Lobby

**Goal:** Use `ISteamMatchmaking` to create a lobby on one machine and join it from another. No messages yet — just the lobby lifecycle.

**Read these:**
- [ISteamMatchmaking](https://partner.steamgames.com/doc/api/ISteamMatchmaking) — `CreateLobby`, `JoinLobby`, `RequestLobbyList`, `GetNumLobbyMembers`, `GetLobbyMemberByIndex`
- [LobbyCreated_t](https://partner.steamgames.com/doc/api/ISteamMatchmaking#LobbyCreated_t) — callback after `CreateLobby`
- [LobbyEnter_t](https://partner.steamgames.com/doc/api/ISteamMatchmaking#LobbyEnter_t) — callback after `JoinLobby`
- [LobbyChatUpdate_t](https://partner.steamgames.com/doc/api/ISteamMatchmaking#LobbyChatUpdate_t) — fired when someone joins/leaves

**Key things to figure out:**
- The lobby type enum (`k_ELobbyTypePublic`, `k_ELobbyTypeFriendsOnly`, etc.) and which one lets strangers find your lobby via `RequestLobbyList`.
- How `RequestLobbyList` → `LobbyMatchList_t` → `GetLobbyByIndex` → `JoinLobby` chains together.
- How to build a main loop with non-blocking stdin so you can type commands without blocking `SteamAPI_RunCallbacks()`.

**Build it as:** A console app with a main loop. Type `host` to create a lobby, `join` to find and join one. Print when people enter or leave.

**Done when:** Machine A hosts, Machine B joins, both sides print that the other person entered the lobby.

---

## Phase 4 — Send and Receive Messages

**Goal:** With two people in a lobby, send a string from one side and print it on the other.

You already know *who* to talk to from the lobby member list. Now use the networking API to actually move bytes between them.

**Read these:**
- [ISteamNetworkingMessages](https://partner.steamgames.com/doc/api/ISteamNetworkingMessages) — `SendMessageToUser`, `ReceiveMessagesOnChannel`, `AcceptSessionWithUser`
- [SteamNetworkingMessagesSessionRequest_t](https://partner.steamgames.com/doc/api/ISteamNetworkingMessages#SteamNetworkingMessagesSessionRequest_t) — you **must** handle this callback or messages silently fail
- [SteamNetworkingMessage_t](https://partner.steamgames.com/doc/api/SteamNetworkingMessage_t) — the message struct you receive

**Key things to figure out:**
- How to build a `SteamNetworkingIdentity` from a `CSteamID` (look at `SetSteamID()`).
- Why `AcceptSessionWithUser` matters — what happens if you don't call it.
- The difference between `k_nSteamNetworkingSend_Reliable` and `k_nSteamNetworkingSend_UnreliableNoDelay` — try both and see.
- How `ReceiveMessagesOnChannel` works — it's a polling model, not a callback. You call it every tick.
- Don't forget to call `Release()` on every received message.

**Done when:** Two people can type messages back and forth in their console windows, seeing each other's Steam name and text.

---

## Phase 5 — Polish and Experiment

**Goal:** Now that chat works, play with the APIs and build intuition.

**Things to try:**
- **Lobby metadata:** Use `SetLobbyData()` / `GetLobbyData()` to attach info like a room name or game mode. Read it before joining.
- **Lobby filters:** Call `AddRequestLobbyListStringFilter()` before `RequestLobbyList()` to only find lobbies matching certain criteria.
- **Send structs instead of strings:** Define a simple struct (position, health, etc.), memcpy it into the send buffer, and deserialize on the other side. This is how you'll sync game state later.
- **Unreliable sends:** Switch to `k_nSteamNetworkingSend_UnreliableNoDelay` and send rapid messages. See how it behaves differently — dropped messages, ordering, etc.
- **Multiple channels:** Use channel 0 for one type of data and channel 1 for another. Poll both.
- **Lobby chat vs P2P messaging:** Steamworks also has `SendLobbyChatMsg` / `LobbyChatMsg_t` — compare it to `ISteamNetworkingMessages` and understand when you'd use which.

---

## Reference: Useful Doc Pages

| Topic | URL |
|-------|-----|
| SDK download | https://partner.steamgames.com/downloads/steamworks_sdk.zip |
| API overview | https://partner.steamgames.com/doc/sdk/api |
| Callbacks | https://partner.steamgames.com/doc/sdk/api#callbacks |
| ISteamMatchmaking | https://partner.steamgames.com/doc/api/ISteamMatchmaking |
| ISteamNetworkingMessages | https://partner.steamgames.com/doc/api/ISteamNetworkingMessages |
| ISteamFriends | https://partner.steamgames.com/doc/api/ISteamFriends |
| Spacewar sample | Included in SDK at `sdk/examples/` |

---

## Troubleshooting Tips

These are things you'll likely run into. Try to solve them yourself first, but if you're stuck:

- **`SteamAPI_Init` fails** — Is Steam running? Is `steam_appid.txt` next to your exe with just `480` in it?
- **Lobby created but the other person can't find it** — Are both on App ID 480? Is the lobby type Public?
- **Messages not arriving** — Are you handling `SteamNetworkingMessagesSessionRequest_t` and calling `AcceptSessionWithUser`? This is the #1 gotcha.
- **Main loop freezes when waiting for input** — You're using blocking I/O. You need non-blocking stdin so `SteamAPI_RunCallbacks()` keeps pumping. On Windows look at `_kbhit()`, on Linux look at `select()` on stdin.
- **Linker errors** — Check that you're building x64 (the SDK ships 64-bit libs). Make sure the lib path in your build config actually points to the right platform folder.
