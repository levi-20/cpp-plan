# C++ Game Development Learning Plan
> Focus: Multiplayer game with Steam Networking  
> Track your progress by checking off each item as you complete it.

---

## Phase 1 — C++ Essentials
> **Goal:** Be comfortable reading and writing C++ classes, using pointers, and working with the STL.  
> **Estimated time:** 4–6 weeks  
> **Milestone:** Build a console-based game (e.g. number guessing game) with a `Player` class, a score, and a game loop.

### Classes and Objects
- [ ] Understand what a class is and how it differs from a struct
- [ ] Write a class with member variables and methods
- [ ] Understand constructors and destructors
- [ ] Learn about `public`, `private`, and `protected` access specifiers
- [ ] Understand `this` pointer

**Resources**
- [LearnCpp — Classes (Chapter 13)](https://www.learncpp.com/cpp-tutorial/introduction-to-object-oriented-programming/)
- [cppreference — Classes](https://en.cppreference.com/w/cpp/language/classes)

---

### Pointers and References
- [ ] Understand what a pointer is and how to declare one
- [ ] Learn to dereference a pointer (`*`) and get an address (`&`)
- [ ] Understand the difference between a pointer and a reference
- [ ] Know when to pass by value, pointer, or reference
- [ ] Understand null pointers and how to check for them

**Resources**
- [LearnCpp — Pointers (Chapter 9)](https://www.learncpp.com/cpp-tutorial/introduction-to-pointers/)
- [LearnCpp — References](https://www.learncpp.com/cpp-tutorial/lvalue-references/)

---

### Memory Management
- [ ] Understand stack vs heap memory
- [ ] Use `new` and `delete` to allocate and free heap memory
- [ ] Understand memory leaks and how to avoid them
- [ ] Learn about smart pointers — `unique_ptr` and `shared_ptr`
- [ ] Know why smart pointers are preferred over raw `new`/`delete`

**Resources**
- [LearnCpp — Dynamic Memory Allocation](https://www.learncpp.com/cpp-tutorial/dynamic-memory-allocation-with-new-and-delete/)
- [LearnCpp — Smart Pointers (Chapter 22)](https://www.learncpp.com/cpp-tutorial/introduction-to-smart-pointers-move-semantics/)

---

### Inheritance and Polymorphism
- [ ] Create a base class and a derived class
- [ ] Understand `virtual` functions and why they matter
- [ ] Learn about pure virtual functions and abstract classes
- [ ] Understand `override` keyword
- [ ] Know when to use inheritance vs composition

**Resources**
- [LearnCpp — Inheritance (Chapter 17)](https://www.learncpp.com/cpp-tutorial/introduction-to-inheritance/)
- [LearnCpp — Virtual Functions (Chapter 18)](https://www.learncpp.com/cpp-tutorial/pointers-and-references-to-the-base-class-of-derived-objects/)

---

### STL Containers
- [ ] Use `std::vector` — add, remove, iterate elements
- [ ] Use `std::map` and `std::unordered_map` for key-value storage
- [ ] Use `std::queue` and `std::deque`
- [ ] Understand iterators and range-based for loops
- [ ] Know which container to pick for which situation

**Resources**
- [LearnCpp — STL Containers (Chapter 23)](https://www.learncpp.com/cpp-tutorial/the-standard-library/)
- [cppreference — Containers](https://en.cppreference.com/w/cpp/container)
- [Hackingcpp — Container cheat sheet](https://hackingcpp.com/cpp/std/containers.html)

---

## Phase 2 — Patterns You'll See in Game Code
> **Goal:** Understand how games are structured in code — loops, states, events, and data passing.  
> **Estimated time:** 3–4 weeks  
> **Milestone:** Write a simple game loop with at least two states (menu and playing) that passes data between them.

### Game Loop and Delta Time
- [ ] Understand what a game loop is and why it's needed
- [ ] Implement a basic game loop in C++
- [ ] Understand fixed timestep vs variable timestep
- [ ] Calculate and apply delta time so game speed is framerate-independent
- [ ] Know the difference between update and render steps

**Resources**
- [Game Programming Patterns — Game Loop](https://gameprogrammingpatterns.com/game-loop.html)
- [Fix Your Timestep (classic article)](https://gafferongames.com/post/fix_your_timestep/)

---

### Callbacks and Function Pointers
- [ ] Understand what a callback is
- [ ] Use raw function pointers in C++
- [ ] Use `std::function` and lambdas as callbacks
- [ ] Understand how Steam uses callbacks (polling vs dispatch)
- [ ] Write a simple observer pattern using callbacks

**Resources**
- [LearnCpp — Function Pointers](https://www.learncpp.com/cpp-tutorial/function-pointers/)
- [LearnCpp — std::function](https://www.learncpp.com/cpp-tutorial/introduction-to-lambdas-anonymous-functions/)

---

### State Machines
- [ ] Understand what a finite state machine (FSM) is
- [ ] Implement a simple enum-based state machine
- [ ] Handle transitions between states (menu → playing → game over)
- [ ] Use a class-based state machine with a base `GameState` class
- [ ] Know how to pass data between states

**Resources**
- [Game Programming Patterns — State](https://gameprogrammingpatterns.com/state.html)
- [LearnCpp — Enumerations](https://www.learncpp.com/cpp-tutorial/unscoped-enumerations/)

---

### Simple Event / Message System
- [ ] Understand why decoupled events are useful in games
- [ ] Implement a simple event dispatcher in C++
- [ ] Understand the observer pattern
- [ ] Know the difference between immediate and queued events
- [ ] Connect events to callbacks

**Resources**
- [Game Programming Patterns — Observer](https://gameprogrammingpatterns.com/observer.html)
- [Game Programming Patterns — Event Queue](https://gameprogrammingpatterns.com/event-queue.html)

---

### Structs and Basic Serialization
- [ ] Use structs to represent game messages (e.g. `PlayerStateMsg`)
- [ ] Understand memory layout of a struct
- [ ] Cast a struct to a `char*` / `void*` to send as raw bytes
- [ ] Read raw bytes back into a struct on the receiving end
- [ ] Understand endianness and why it matters for networking

**Resources**
- [LearnCpp — Structs](https://www.learncpp.com/cpp-tutorial/introduction-to-structs-members-and-member-selection/)
- [Beej's Guide — Data serialization](https://beej.us/guide/bgnet/html/#serialization)

---

## Phase 3 — Networking Fundamentals
> **Goal:** Understand how multiplayer games handle data over a network before touching any SDK.  
> **Estimated time:** 3–4 weeks  
> **Milestone:** Explain out loud (or write down) how a position update travels from one player's machine to another and arrives correctly.

### TCP vs UDP
- [ ] Understand what TCP guarantees (ordered, reliable delivery)
- [ ] Understand what UDP gives you (fast, no guarantee)
- [ ] Know why most games use UDP for real-time data
- [ ] Understand when to use reliable vs unreliable sends
- [ ] Know how Steam's send flags map to these concepts

**Resources**
- [Beej's Guide — TCP vs UDP](https://beej.us/guide/bgnet/html/#what-is-a-socket)
- [Gaffer on Games — UDP vs TCP](https://gafferongames.com/post/udp_vs_tcp/)

---

### Client-Server vs Peer-to-Peer
- [ ] Understand the client-server model and its advantages
- [ ] Understand peer-to-peer and its tradeoffs
- [ ] Know what a "listen server" is (a player who is also the host)
- [ ] Understand how Steam P2P works under the hood (relay network)
- [ ] Decide which model fits your game

**Resources**
- [Gaffer on Games — What every programmer needs to know about game networking](https://gafferongames.com/post/what_every_programmer_needs_to_know_about_game_networking/)
- [Valve — Steam Networking overview](https://partner.steamgames.com/doc/features/multiplayer/networking)

---

### Latency and Packet Loss
- [ ] Understand what latency (ping) is and how it affects gameplay
- [ ] Understand packet loss and jitter
- [ ] Learn about client-side prediction
- [ ] Learn about lag compensation basics
- [ ] Understand rollback netcode at a high level

**Resources**
- [Gaffer on Games — Snapshot Interpolation](https://gafferongames.com/post/snapshot_interpolation/)
- [Gaffer on Games — Client-Side Prediction](https://gafferongames.com/post/prediction_and_rolling_back/)
- [Rollback netcode explained (Fightin' Words)](https://words.infil.net/w02-netcode.html)

---

### What to Send Over the Network
- [ ] Understand the difference between sending full state vs sending inputs
- [ ] Know what data changes every frame vs what changes rarely
- [ ] Understand bandwidth budgeting — how much data per second is acceptable
- [ ] Learn basic techniques to reduce data size (quantization, delta compression)
- [ ] Decide on a message format for your game

**Resources**
- [Gaffer on Games — State Synchronization](https://gafferongames.com/post/state_synchronization/)
- [Valve — Source Multiplayer Networking](https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking)

---

## Phase 4 — Steam SDK
> **Goal:** Use ISteamNetworkingSockets and ISteamMatchmaking to connect two players and exchange game data.  
> **Estimated time:** Ongoing alongside game development  
> **Milestone:** Two players connect via a Steam lobby and exchange position updates in real time.

### SDK Setup
- [ ] Create a Steamworks partner account at `partner.steamgames.com`
- [ ] Download the Steamworks SDK
- [ ] Add SDK headers and link `steam_api64.lib` in your project
- [ ] Create `steam_appid.txt` with `480` for testing
- [ ] Call `SteamAPI_Init()` and `SteamAPI_Shutdown()` correctly

**Resources**
- [Steamworks SDK Docs — Getting Started](https://partner.steamgames.com/doc/sdk)
- [Steamworks — ISteamNetworkingSockets](https://partner.steamgames.com/doc/api/ISteamNetworkingSockets)

---

### Lobbies with ISteamMatchmaking
- [ ] Understand what a Steam lobby is
- [ ] Create a lobby with `CreateLobby()`
- [ ] Join a lobby with `JoinLobby()`
- [ ] List available lobbies with `RequestLobbyList()`
- [ ] Set and read lobby metadata (game mode, player count)
- [ ] Handle lobby callbacks (member joined, left, owner changed)

**Resources**
- [Steamworks — Matchmaking](https://partner.steamgames.com/doc/features/multiplayer/matchmaking)
- [Steamworks — ISteamMatchmaking API](https://partner.steamgames.com/doc/api/ISteamMatchmaking)

---

### ISteamNetworkingSockets — Send and Receive
- [ ] Create a listen socket with `CreateListenSocketP2P()`
- [ ] Connect to a host with `ConnectP2P()`
- [ ] Accept incoming connections in a callback
- [ ] Create a poll group and assign connections to it
- [ ] Receive messages with `ReceiveMessagesOnPollGroup()`
- [ ] Send reliable and unreliable messages
- [ ] Always call `Release()` on received messages

**Resources**
- [Steamworks — ISteamNetworkingSockets](https://partner.steamgames.com/doc/api/ISteamNetworkingSockets)
- [Valve GameNetworkingSockets on GitHub](https://github.com/ValveSoftware/GameNetworkingSockets)

---

### Handling Disconnects
- [ ] Detect when a remote player disconnects via callback
- [ ] Clean up connection handles on disconnect
- [ ] Implement a reconnect flow
- [ ] Handle host migration (if using listen server)
- [ ] Notify other players when someone leaves

**Resources**
- [Steamworks — Connection State Changes](https://partner.steamgames.com/doc/api/ISteamNetworkingSockets#SteamNetConnectionStatusChangedCallback_t)

---

## Useful References to Bookmark

| Resource | What it covers |
|---|---|
| [LearnCpp.com](https://www.learncpp.com/) | Best free C++ tutorial site, beginner to advanced |
| [cppreference.com](https://en.cppreference.com/) | Complete C++ standard library reference |
| [Game Programming Patterns](https://gameprogrammingpatterns.com/) | Free book — patterns used in real game codebases |
| [Gaffer on Games](https://gafferongames.com/) | Deep networking articles written for game devs |
| [Beej's Guide to Network Programming](https://beej.us/guide/bgnet/) | Classic, readable intro to sockets and networking |
| [Steamworks Documentation](https://partner.steamgames.com/doc/home) | Official Steam SDK reference |
| [Valve GameNetworkingSockets (GitHub)](https://github.com/ValveSoftware/GameNetworkingSockets) | Open source version of Steam networking — great examples |
| [Hackingcpp.com](https://hackingcpp.com/) | Visual C++ cheat sheets and container guides |
