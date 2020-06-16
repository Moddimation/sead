# sead

Decompilation of Nintendo's standard library (modern version)

Unlike the original [sead decomp project](https://github.com/aboood40091/sead), which this repo derives from, this project targets more recent versions of sead.

The objective is to recreate the standard library as accurately as possible, so that eventually interoperability can be achieved by adding support for other platforms and by making it easier to create projects that interact with sead games.

Because sead is statically linked into games, it is required to legally own at least one recent first-party Nintendo game. Picking a game that ships with debugging symbols is probably a good idea:

* Super Mario Odyssey (version 1.0.0) ([buy it here](https://www.nintendo.com/games/detail/super-mario-odyssey-switch/))
* Splatoon 2 (version <= 3.1.0) ([buy it here](https://www.nintendo.com/games/detail/splatoon-2-switch/))
* [Nintendo Labo](https://labo.nintendo.com/) (the pilot build has symbols and assertions)
* Any other title that has symbols and uses sead

File names, function names and the file organization come from debugging symbols, assertions and information in all of the aforementioned titles.
Nobody except Nintendo has the source code of sead, not even third-party developers.

Note that many names (especially for inlined, templated functions) are just plain guesses.

## Modules

For progress, refer to [the GitHub project page](https://github.com/zeldamods/sead/projects/1). Several modules currently fail to build for Switch.

* **audio** - Audio
* **basis** - Types, asserts, allocation operators
* **codec** - Base64, CRC16, CRC32
* **container** - Templated container classes
* **controller** - Controller
* **devenv** - Development environment (debug utilities)
* **filedevice** - File IO
* **framework** - Framework (game framework, tasks, etc.)
* **geom** - Geometry
* **gfx** - Graphics
* **heap** - Heap (arenas, disposers, different types of heaps)
* **hostio** - Host IO (communication with PCs)
* **math** - Maths utilities (vector, matrix, etc.)
* **message** - libms wrapper
* **mc** - Multi-core support
* **prim** - Primitives (strings, enums, RTTI, etc.)
* **random** - Random number generator
* **resource** - Resource (loading, decompressing, etc.)
* **stream** - Stream IO
* **thread** - Thread utilities (threads, critical sections, message queues, etc.)
* **time** - Time utilities

### Platform specific source

Platform-specific files are usually placed into a subdirectory that is called:

* **cafe** for Wii U
* **ctr** for 3DS
* **nin** for Switch (or any other platform that uses nn?)

## Building and contributing

Building this project requires:

- A C++17 capable compiler (or >= Clang 4.0). While older parts of sead are written in C++03, the newer modules in sead target C++11 (or newer) and recent C++ language or library features make writing C++ more convenient.
- CMake 3.10+

When implementing .cpp functions, please compare the assembly output against the original function and make it match the original code. At this scale, that is pretty muchc the only way to ensure accuracy and functional equivalency.
