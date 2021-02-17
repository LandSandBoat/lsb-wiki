<img src="https://user-images.githubusercontent.com/1389729/97106613-832f0100-16cb-11eb-8452-267e406bceb9.png" width="640" height="480"/>

```
A real time, nanosecond resolution, remote telemetry, hybrid frame and sampling profiler for games and other applications.
```
**Tracy GitHub:** https://github.com/wolfpld/tracy

**Tracy Release v0.7.3:** https://github.com/wolfpld/tracy/releases/download/v0.7.3/Tracy-0.7.3.7z

**Tracy User Guide:** https://github.com/wolfpld/tracy/releases/download/v0.7.3/tracy.pdf

## Intro

We can't know how good/bad our performance is until we measure it.

`Tracy` is made up of two parts:
- The client - which you build into your program and will broadcast your performance information.
- The server - an external program (available in the Tracy Release) which will receive the information and allow you to analyze it. 

## Setup

Add `-DTRACY_ENABLE=ON` to your `CMake` configuration arguments. It will download and build the `Tracy` client into `topaz_game` for you.

1) Build `topaz_game` with `-DTRACY_ENABLE=ON` (or use one of the `-Tracy` targets in VS)
2) Launch `Tracy.exe` from the Tracy Release
3) In Tracy, press "Connect". It will wait for data to be sent to it.
4) Launch `topaz_game` and watch the data stream in.

## Gotchas
Remember that there are a lot of things that can affect performance.
- Platform (Windows, Linux, OSX)
- Architecture (x86, x86_64)
- Type of build (Debug, RelWithDebugInfo, Release, MinSizeRel)
- Compiler (MSVC, Clang, GCC)
- Your system specs (CPU Speed, Available Memory, Memory Latency, HDD R/W speed etc.)
- Other programs using your system's resources
- Virtualization/Containerization (VMWare, WSL, Docker)

If you're performing before/after testing, try as hard as you can to make sure the conditions are the same for both runs and change as little as possible for each change. It is also helpful to take multiple readings and many samples per reading to try and get an accurate view of performance.

#### Common Hiccups
- `ShowWarning`, `std::cout / std::endl`, `printf`, and syscalls of any kind can be slow and blocking. `ShowInfo` was measured to take **7 milliseconds**. When you're trying to track down performance hits of **50 microseconds**, you will freak out if you forget this fact after you've peppered your target code with prints.

## Finding Problems
Searchable statistics are in the `Statistics` header, log messages are in `Messages`. You can click and drag and zoom around the main timeline window for information about whats going on. You can "re-attach" to the most active frames by clicking on the `Pause/Resume` header and using the options there.

**Known bottlenecks**
- Expensive pathing and navmesh access... all the time... every tick... every mob... everywhere...
- `parse` routine is slow

**Issues identified by Tracy (and fixed)**
- Excessive use of Lua's `prepFile` (runtime file reads, not gone)