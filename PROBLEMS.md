# C++ Practice Roadmap
 
A structured progression of problems and mini-projects to learn C++ — from fundamentals through systems programming. Designed for developers with backend experience (Node.js, Go) who want to build real things, not solve toy problems.
 
---
 
## Phase 1: Getting Comfortable (Week 1–2)
 
> **Goal:** Get fluent with C++ syntax, compilation, I/O, strings, and basic memory model. You already know programming — this is about mapping your existing knowledge to C++ idioms.
 
### Problem 1.1 — CLI Quiz Game
**Type:** Mini-project (~80 lines)
**What you'll learn:** File I/O, `std::string`, `std::getline`, `std::ifstream`, basic control flow, `struct`
 
**Task:** Build a quiz app that reads questions from a CSV file (`question,answer` format), presents them one at a time in the terminal, scores the user, and supports a `--time` flag for a countdown timer.
 
**Stretch:** Add a `--shuffle` flag using `<random>` and `std::shuffle`.
 
**Key concepts to explore:**
- `argc` / `argv` for command-line arguments
- `std::ifstream` and parsing CSV lines with `std::getline` + `std::stringstream`
- `struct Question { string text; string answer; };`
 
**Reference:** This is the C++ version of Gophercises #1.
 
---
 
### Problem 1.2 — Word Frequency Counter
**Type:** Short problem (~50 lines)
**What you'll learn:** `std::map`, `std::vector`, iterators, sorting with custom comparators
 
**Task:** Read a text file, count word frequencies (case-insensitive), and print the top N words sorted by frequency.
 
**Stretch:** Handle punctuation stripping. Use `std::unordered_map` and compare performance with `std::map`.
 
---
 
### Problem 1.3 — Number Guessing Game (with smart hints)
**Type:** Short problem (~40 lines)
**What you'll learn:** `<random>`, `std::cin`, loops, basic error handling on bad input
 
**Task:** Generate a random number 1–100. Give binary search-style hints (higher/lower). Track attempts. Handle non-integer input gracefully without crashing.
 
---
 
### Problem 1.4 — Simple Calculator (Expression Parser)
**Type:** Mini-project (~120 lines)
**What you'll learn:** `std::stack`, string parsing, operator precedence, the Shunting-yard algorithm
 
**Task:** Build a command-line calculator that handles `+`, `-`, `*`, `/`, parentheses, and respects operator precedence. Input like `3 + 4 * (2 - 1)` should output `7`.
 
**Key concepts:**
- Using `std::stack<double>` and `std::stack<char>`
- Character-by-character parsing
- This is your first taste of a real parsing problem
 
---
 
## Phase 2: OOP & Memory (Week 3–4)
 
> **Goal:** Understand classes, inheritance, RAII, smart pointers, and the Rule of Five. This is where C++ diverges most from Node.js/Go.
 
### Problem 2.1 — Task Manager (CRUD with Classes)
**Type:** Mini-project (~200 lines)
**What you'll learn:** Classes, constructors, destructors, `std::vector<Task>`, operator overloading, file persistence
 
**Task:** Build a CLI task manager. Commands: `add`, `list`, `done <id>`, `delete <id>`, `save`, `load`. Tasks are stored in a `std::vector<Task>` and serialized to a JSON-like text file.
 
**Key concepts:**
- Class design: `Task` with `id`, `title`, `completed`, `created_at`
- `TaskManager` class encapsulating the vector and file I/O
- Overload `operator<<` for pretty printing
- Destructor that auto-saves
 
---
 
### Problem 2.2 — Shape Hierarchy (Polymorphism)
**Type:** Short problem (~100 lines)
**What you'll learn:** Inheritance, virtual functions, `override`, pure virtual (abstract classes), `std::unique_ptr` with polymorphism
 
**Task:** Create a `Shape` base class with `area()` and `perimeter()` as pure virtual methods. Implement `Circle`, `Rectangle`, `Triangle`. Store mixed shapes in a `std::vector<std::unique_ptr<Shape>>` and compute total area.
 
**Why this matters:** This teaches vtable dispatch — the C++ equivalent of Go's interfaces, but with different tradeoffs.
 
---
 
### Problem 2.3 — String Class from Scratch
**Type:** Mini-project (~200 lines)
**What you'll learn:** Rule of Five, deep copy, move semantics, `operator[]`, `operator+`, `operator<<`, raw `new`/`delete`
 
**Task:** Implement `MyString` with:
- Constructor from `const char*`
- Copy constructor & copy assignment (deep copy the buffer)
- Move constructor & move assignment (steal the buffer)
- Destructor (free the buffer)
- `length()`, `c_str()`, `operator[]`, `operator+`, `operator==`
 
**This is the single most important exercise for understanding C++ memory.** Do it with raw `new[]`/`delete[]` first, then refactor to `std::unique_ptr<char[]>`.
 
---
 
### Problem 2.4 — Smart Pointer Implementation
**Type:** Short problem (~80 lines)
**What you'll learn:** Templates, reference counting, RAII
 
**Task:** Implement a simplified `SharedPtr<T>` with:
- Reference count (heap-allocated `int*`)
- Constructor, copy constructor, copy assignment, destructor
- `operator*`, `operator->`, `use_count()`
 
**Stretch:** Add a `WeakPtr<T>` that doesn't affect the count.
 
---
 
## Phase 3: Data Structures & Algorithms (Week 5–7)
 
> **Goal:** Implement classic data structures from scratch. This builds deep fluency with pointers, templates, and iterator patterns.
 
### Problem 3.1 — Linked List with Iterators
**Type:** Mini-project (~250 lines)
**What you'll learn:** Node-based structures, raw pointers, `begin()`/`end()`, range-based for loop compatibility
 
**Task:** Implement a templated `LinkedList<T>` with:
- `push_front`, `push_back`, `pop_front`, `size`, `empty`
- An inner `Iterator` class so you can do `for (auto& val : list)`
- `operator<<` for printing
 
**Stretch:** Make it doubly-linked with `reverse()`.
 
---
 
### Problem 3.2 — Hash Map
**Type:** Mini-project (~300 lines)
**What you'll learn:** Hashing, collision resolution (chaining), dynamic resizing, load factor
 
**Task:** Implement `HashMap<K, V>` using separate chaining:
- `put(key, val)`, `get(key)`, `remove(key)`, `contains(key)`
- Resize when load factor > 0.75
- Use `std::hash<K>` for hashing
 
**Comparison:** After building it, benchmark against `std::unordered_map`.
 
---
 
### Problem 3.3 — Binary Search Tree
**Type:** Mini-project (~200 lines)
**What you'll learn:** Recursive tree algorithms, `std::unique_ptr` for tree nodes, in-order traversal
 
**Task:** Implement a BST with `insert`, `search`, `remove`, `in_order_traversal`, `min`, `max`, `height`.
 
**Stretch:** Add a `to_sorted_vector()` method. Visualize the tree with an ASCII printer.
 
---
 
### Problem 3.4 — Priority Queue (Min-Heap)
**Type:** Short problem (~100 lines)
**What you'll learn:** Heap property, array-based tree representation, `sift_up`/`sift_down`
 
**Task:** Implement a min-heap backed by `std::vector<T>`. Support `push`, `pop`, `top`, `size`. Use it to solve: "Find the K largest elements in a stream."
 
---
 
### Problem 3.5 — Graph with BFS/DFS
**Type:** Mini-project (~200 lines)
**What you'll learn:** Adjacency list representation, `std::unordered_map<int, std::vector<int>>`, queue/stack-based traversal
 
**Task:** Build a `Graph` class. Implement:
- `add_edge(u, v)` (undirected)
- `bfs(start)` — returns visit order
- `dfs(start)` — returns visit order
- `shortest_path(start, end)` — unweighted
 
**Stretch:** Add `has_cycle()` and `connected_components()`.
 
---
 
## Phase 4: Real-World Mini-Projects (Week 8–10)
 
> **Goal:** Build things that resemble real software. File formats, networking, concurrency.
 
### Problem 4.1 — JSON Parser
**Type:** Mini-project (~400 lines)
**What you'll learn:** Recursive descent parsing, `std::variant`, `std::map`, `std::vector`, `std::string_view`
 
**Task:** Parse a JSON string into a tree of `JsonValue` objects:
```cpp
using JsonValue = std::variant<
    std::nullptr_t,
    bool,
    double,
    std::string,
    std::vector<JsonValue>,
    std::map<std::string, JsonValue>
>;
```
Support: strings, numbers, booleans, null, arrays, objects. Handle escape sequences.
 
**This is one of the best intermediate C++ projects.** It exercises parsing, variant types, recursion, and error handling all at once.
 
---
 
### Problem 4.2 — HTTP/1.1 Client
**Type:** Mini-project (~250 lines)
**What you'll learn:** POSIX sockets (`socket`, `connect`, `send`, `recv`), HTTP protocol, string parsing
 
**Task:** Build a CLI tool that can `GET` a URL and print the response body:
```
./httpclient https://httpbin.org/get
```
Parse the URL, open a TCP connection, send a raw HTTP/1.1 request, parse the response headers, and print the body.
 
**Key concepts:**
- `struct sockaddr_in`, `getaddrinfo`
- Building HTTP request strings manually
- Chunked transfer encoding (stretch)
 
---
 
### Problem 4.3 — File Compressor (Huffman Coding)
**Type:** Mini-project (~350 lines)
**What you'll learn:** Trees, priority queues, bitwise operations, file I/O with binary data
 
**Task:** Implement Huffman compression and decompression:
1. Count character frequencies
2. Build the Huffman tree using a min-heap
3. Generate prefix codes
4. Encode the file as a bitstream
5. Write a header so the decoder can reconstruct the tree
 
**This teaches you to think in bits** — something you rarely do in Node.js or Go.
 
---
 
### Problem 4.4 — Concurrent Task Queue
**Type:** Mini-project (~200 lines)
**What you'll learn:** `std::thread`, `std::mutex`, `std::condition_variable`, producer-consumer pattern
 
**Task:** Build a thread-safe task queue:
- `enqueue(task)` — add a callable
- Worker threads pull and execute tasks
- `shutdown()` — stop accepting, drain remaining tasks
- Configurable thread count
 
```cpp
TaskQueue pool(4); // 4 worker threads
pool.enqueue([]{ /* work */ });
pool.shutdown();
```
 
**This is the C++ equivalent of a Go worker pool with channels.**
 
---
 
### Problem 4.5 — Markdown to HTML Converter
**Type:** Mini-project (~300 lines)
**What you'll learn:** State machine parsing, `std::regex` (and why it's slow), string building
 
**Task:** Convert a subset of Markdown to HTML:
- `# headings` (h1–h6)
- `**bold**`, `*italic*`, `` `code` ``
- `- unordered lists`
- `[links](url)`
- Blank line = new paragraph
 
**Stretch:** Add fenced code blocks with `<pre><code>`.
 
---
 
## Phase 5: Systems Programming (Week 11–13)
 
> **Goal:** Interact with the OS directly. Memory, processes, sockets. This is what C++ was built for.
 
### Problem 5.1 — Memory Allocator
**Type:** Mini-project (~300 lines)
**What you'll learn:** `sbrk`/`mmap`, free-list management, memory alignment, fragmentation
 
**Task:** Implement a simple `malloc`/`free` replacement:
- Use `mmap` to request memory from the OS
- Maintain a free list of blocks
- Support `my_malloc(size)` and `my_free(ptr)`
- Handle block splitting and coalescing
 
**This is the ultimate "understand how memory works" exercise.**
 
---
 
### Problem 5.2 — Simple Shell
**Type:** Mini-project (~250 lines)
**What you'll learn:** `fork`, `exec`, `waitpid`, `pipe`, `dup2`, signal handling
 
**Task:** Build a Unix shell that supports:
- Running commands: `ls -la`
- Piping: `cat file.txt | grep error | wc -l`
- Built-in commands: `cd`, `exit`, `pwd`
- Ctrl+C handling (don't kill the shell)
 
**Note:** This requires Linux/macOS. On Windows, use WSL.
 
---
 
### Problem 5.3 — TCP Chat Server
**Type:** Mini-project (~350 lines)
**What you'll learn:** Socket programming, `select`/`poll`/`epoll`, non-blocking I/O, broadcasting
 
**Task:** Build a multi-client chat server:
- Clients connect via `telnet` or `nc`
- Messages from one client are broadcast to all others
- Handle disconnections gracefully
- Print `[username] joined/left` messages
 
**Stretch:** Add private messaging with `/msg username text`.
 
---
 
### Problem 5.4 — Key-Value Store with Persistence
**Type:** Mini-project (~400 lines)
**What you'll learn:** File-based storage, write-ahead log, `std::unordered_map`, TCP server, serialization
 
**Task:** Build a Redis-like key-value store:
- Commands: `SET key value`, `GET key`, `DEL key`, `KEYS`
- TCP interface (talk to it with `nc`)
- Write-ahead log for crash recovery
- Periodic snapshotting to disk
 
**This combines networking, data structures, file I/O, and concurrency** — a capstone project.
 
---
 
## Recommended Resources
 
### Online Judges & Practice Sites
- **Exercism C++ Track** — exercism.org/tracks/cpp (structured exercises with mentoring)
- **LeetCode** — Use C++ as your language to practice algorithms
- **Advent of Code** — adventofcode.com (annual puzzles, great for learning any language)
- **Project Euler** — projecteuler.net (math + programming)
- **Codewars** — C++ katas at various difficulty levels
 
### Books (pick one to start)
- **"A Tour of C++"** by Bjarne Stroustrup — concise intro for experienced programmers
- **"C++ Primer"** by Lippman — thorough reference
- **"Effective Modern C++"** by Scott Meyers — best practices for C++11/14
 
### References
- **cppreference.com** — the definitive C++ standard library reference
- **Compiler Explorer** (godbolt.org) — see what your C++ compiles to
- **C++ Insights** (cppinsights.io) — see what the compiler does with your templates, lambdas, etc.
 
### YouTube Channels
- **The Cherno** — C++ series from basics to game engine
- **CppCon** — conference talks (watch Jason Turner, Herb Sutter, Kate Gregory)
- **javidx9 (OneLoneCoder)** — systems programming projects in C++
 
---
 
## Compilation Cheat Sheet
 
```bash
# Basic compilation (use g++ or clang++)
g++ -std=c++20 -Wall -Wextra -o program main.cpp
 
# Debug build (with sanitizers — catches memory bugs)
g++ -std=c++20 -g -fsanitize=address,undefined -o program main.cpp
 
# Optimized build
g++ -std=c++20 -O2 -o program main.cpp
 
# Multi-file project
g++ -std=c++20 -Wall -o program main.cpp utils.cpp parser.cpp
 
# Using CMake (recommended for anything > 1 file)
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug
make
```
 
**Always compile with `-Wall -Wextra`** — the compiler catches bugs you'd spend hours debugging.
 
**Always use `-fsanitize=address,undefined` during development** — it catches memory leaks, buffer overflows, and undefined behavior at runtime.
