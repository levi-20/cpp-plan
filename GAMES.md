# C++ Game Development Roadmap
> Path: From C++ basics to building your first game without a big engine  
> Track your progress by checking off each item as you complete it.

---

## Phase 1 — Strengthen Your C++ Foundation
> **Goal:** Be confident with OOP, memory, and the STL before touching any game code.  
> **Estimated time:** 4–6 weeks  
> **Milestone:** Write a `Player`, `Enemy`, and `Bullet` class that can be stored in a `std::vector`.

### OOP — Classes and Objects
- [ ] Write a class with member variables, methods, constructor, destructor
- [ ] Understand `public`, `private`, `protected`
- [ ] Understand `this` pointer
- [ ] Know the difference between a class and a struct

### Pointers and Memory
- [ ] Declare and dereference pointers
- [ ] Understand stack vs heap memory
- [ ] Use `new` and `delete`
- [ ] Learn `unique_ptr` and `shared_ptr` to avoid memory leaks

### Inheritance and Polymorphism
- [ ] Create a base class (e.g. `GameObject`) and derive from it
- [ ] Use `virtual` functions and `override`
- [ ] Understand pure virtual functions and abstract classes
- [ ] Know when to use inheritance vs composition

### STL Containers
- [ ] Use `std::vector` — add, remove, iterate
- [ ] Use `std::map` and `std::unordered_map`
- [ ] Use `std::deque` and `std::queue`
- [ ] Understand range-based for loops and iterators

**Resources**
- [LearnCpp.com — full C++ tutorial](https://www.learncpp.com/)
- [cppreference — STL Containers](https://en.cppreference.com/w/cpp/container)
- [Hackingcpp — Container cheat sheet](https://hackingcpp.com/cpp/std/containers.html)

---

## Phase 2 — Core Game Development Concepts
> **Goal:** Think like a game developer — understand how a game runs frame by frame.  
> **Estimated time:** 3–4 weeks  
> **Milestone:** Write a game loop that updates and renders at a consistent speed regardless of framerate.

### Game Loop
- [ ] Understand what a game loop is and why it's needed
- [ ] Implement a basic loop: process input → update → render
- [ ] Understand fixed vs variable timestep
- [ ] Calculate and apply delta time correctly

### Delta Time
- [ ] Use `std::chrono` to measure frame time
- [ ] Multiply movement by delta time so speed is framerate-independent
- [ ] Understand why skipping delta time causes fast/slow gameplay on different machines

### Entity Management
- [ ] Store game objects in a `std::vector`
- [ ] Add and remove entities safely during the game loop
- [ ] Understand the basic idea behind an Entity-Component-System (ECS)

### Input Handling
- [ ] Poll keyboard and mouse input each frame
- [ ] Map raw input to game actions (e.g. move, jump, shoot)
- [ ] Understand the difference between key held vs key just pressed

**Resources**
- [Game Programming Patterns — Game Loop](https://gameprogrammingpatterns.com/game-loop.html)
- [Fix Your Timestep (classic article)](https://gafferongames.com/post/fix_your_timestep/)

---

## Phase 3 — Pick a Lightweight Framework
> **Goal:** Get a window open, render shapes, play sound, and read input using SFML or SDL2.  
> **Estimated time:** 2–3 weeks  
> **Milestone:** Open a window, draw a moving rectangle, and respond to keyboard input.

### SFML (recommended for beginners)
- [ ] Install SFML and link it to your project
- [ ] Open a `RenderWindow` and run the game loop inside it
- [ ] Draw shapes (`RectangleShape`, `CircleShape`, `Sprite`)
- [ ] Handle keyboard and mouse events with `sf::Event`
- [ ] Play a sound with `sf::Sound` and `sf::SoundBuffer`
- [ ] Display text with `sf::Font` and `sf::Text`

### SDL2 (more industry-used)
- [ ] Install SDL2 and initialize it
- [ ] Create a window and renderer
- [ ] Draw rectangles and textures
- [ ] Poll events and handle keyboard input
- [ ] Play audio with SDL_mixer

**Resources**
- [SFML Official Tutorials](https://www.sfml-dev.org/tutorials/2.6/)
- [SDL2 Lazy Foo Tutorials](https://lazyfoo.net/tutorials/SDL/)
- [SFML vs SDL2 comparison](https://www.reddit.com/r/gamedev/comments/sdl_vs_sfml/)

---

## Phase 4 — Game Math Essentials
> **Goal:** Understand the math that powers movement, collisions, and positioning.  
> **Estimated time:** 2–3 weeks  
> **Milestone:** Make a ball bounce off walls with correct angle reflection.

### 2D Vectors
- [ ] Understand a 2D vector as a position or direction (x, y)
- [ ] Add, subtract, and scale vectors
- [ ] Calculate vector length (magnitude)
- [ ] Normalize a vector (make it length 1)
- [ ] Use dot product to check directions

### Coordinate Systems
- [ ] Understand screen coordinates (origin top-left, y goes down)
- [ ] Convert between world space and screen space
- [ ] Understand what a camera/viewport is

### Collision Detection
- [ ] Implement AABB (axis-aligned bounding box) collision
- [ ] Implement circle vs circle collision
- [ ] Detect and respond to wall collisions
- [ ] Remove or destroy objects on collision

### Basic Physics
- [ ] Apply velocity to position each frame
- [ ] Apply gravity as a constant downward acceleration
- [ ] Implement simple friction / drag
- [ ] Clamp speed to a maximum value

**Resources**
- [Math for Game Developers (YouTube)](https://www.youtube.com/playlist?list=PLW3Zl3wyJwWOpdhYedlD-yCB7WQoHf-My)
- [2D Game Collision Detection (free book)](https://www.jeffreythompson.org/collision-detection/)

---

## Phase 5 — Game Architecture Patterns
> **Goal:** Structure your game code so it's readable, extensible, and doesn't become a mess.  
> **Estimated time:** 2–3 weeks  
> **Milestone:** Implement a working menu → playing → game over state flow.

### Game States
- [ ] Implement a simple enum-based state machine
- [ ] Handle transitions: menu → playing → paused → game over
- [ ] Use a class-based state machine with a `GameState` base class
- [ ] Know how to pass data between states (e.g. final score to game over screen)

### Entity-Component-System (ECS)
- [ ] Understand the problem ECS solves (vs deep inheritance trees)
- [ ] Separate data (components) from logic (systems)
- [ ] Implement a simple ECS manually
- [ ] Understand when ECS is overkill (small games) vs necessary (large games)

### Scene Management
- [ ] Understand what a scene is (a self-contained game state)
- [ ] Load and unload scenes without leaking memory
- [ ] Keep scenes decoupled from each other

### Event Systems
- [ ] Implement a simple event dispatcher
- [ ] Use events to decouple systems (e.g. "enemy died" fires a score event)
- [ ] Understand immediate vs queued events

**Resources**
- [Game Programming Patterns — full free book](https://gameprogrammingpatterns.com/)
- [Game Programming Patterns — State](https://gameprogrammingpatterns.com/state.html)
- [Game Programming Patterns — Observer](https://gameprogrammingpatterns.com/observer.html)

---

## Phase 6 — Build Your First Game
> **Goal:** Ship a small, complete, playable game. Every bug you fix teaches you something a tutorial cannot.  
> **Estimated time:** 2–6 weeks depending on scope  
> **Milestone:** A game with a start screen, gameplay loop, score, and game over screen.

### Recommended order
- [ ] **Pong** — game loop, collision, basic AI, score
- [ ] **Snake** — `std::deque`, grid movement, self-collision
- [ ] **Breakout** — `std::vector` of objects, destroy on hit, levels
- [ ] **Space Invaders** — class hierarchy, bullet pooling, wave system
- [ ] **Simple platformer** — gravity, tile collision, camera scrolling

### Things to do for every project
- [ ] Use Git from day one — commit after every working feature
- [ ] Write a `README.md` describing what the game is and how to build it
- [ ] Separate game logic from rendering as much as possible
- [ ] Play your game and ask: what feels broken? Fix it.

**Resources**
- [SFML Game Development (book)](https://www.packtpub.com/product/sfml-game-development/9781849696845)
- [Lazy Foo SDL2 Game tutorials](https://lazyfoo.net/tutorials/SDL/)
- [OneLoneCoder — C++ game dev YouTube](https://www.youtube.com/@javidx9)

---

## Useful References to Bookmark

| Resource | What it covers |
|---|---|
| [LearnCpp.com](https://www.learncpp.com/) | Best free C++ tutorial, beginner to advanced |
| [cppreference.com](https://en.cppreference.com/) | Complete C++ standard library reference |
| [Game Programming Patterns](https://gameprogrammingpatterns.com/) | Free book — patterns used in real game codebases |
| [SFML Official Tutorials](https://www.sfml-dev.org/tutorials/2.6/) | Getting started with SFML step by step |
| [Lazy Foo SDL2 Tutorials](https://lazyfoo.net/tutorials/SDL/) | Getting started with SDL2 step by step |
| [Gaffer on Games](https://gafferongames.com/) | Networking and game loop deep dives |
| [OneLoneCoder YouTube](https://www.youtube.com/@javidx9) | C++ game dev projects built from scratch |
| [Hackingcpp.com](https://hackingcpp.com/) | Visual C++ cheat sheets |
| [Math for Game Devs (YouTube)](https://www.youtube.com/playlist?list=PLW3Zl3wyJwWOpdhYedlD-yCB7WQoHf-My) | Game math explained visually |
