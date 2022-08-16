# Tracy

[https://github.com/wolfpld/tracy](https://github.com/wolfpld/tracy)

> A real time, nanosecond resolution, remote telemetry, hybrid frame and sampling profiler for games and other applications.

<img src="https://user-images.githubusercontent.com/1389729/97106613-832f0100-16cb-11eb-8452-267e406bceb9.png" width="640" height="480"/>

## Intro

We can't know how good/bad our performance is until we measure it.

`Tracy` is made up of two parts:

- The client - which you build into your program and will broadcast your performance information.
- The server - an external program (available in the Tracy Release) which will receive the information and allow you to analyze it.

## Setup

If building on the command line, add `-DTRACY_ENABLE=ON` to your configuration arguments. It will download the Tracy client and server, and build the `Tracy` client into `xi_map` for you.

If building from Visual Studio, select one of the `-Tracy` build configurations and build as normal.

![image](https://user-images.githubusercontent.com/1389729/184948461-879157e5-b367-462c-8d21-6e56036216a8.png)

```sh
1> Working directory: C:\ffxi\server\build\x64-Release-Tracy
1> [CMake] -- C:/ProgramData/chocolatey/bin/ccache.exe found and enabled
1> [CMake] -- CMAKE_SOURCE_DIR: C:/ffxi/server
1> [CMake] -- CMAKE_SIZEOF_VOID_P == 8: 64-bit build
1> [CMake] -- ENABLE_FAST_MATH: ON
1> [CMake] -- TRACY_ENABLE: ON
1> [CMake] -- Downloading Tracy development library
1> [CMake] x tracy-0.8.2/
1> [CMake] x tracy-0.8.2/.github/
1> [CMake] x tracy-0.8.2/.github/FUNDING.yml
1> [CMake] x tracy-0.8.2/.github/sponsor.png
1> [CMake] x tracy-0.8.2/.github/workflows/
... 
1> [CMake] -- Downloading Tracy client
1> [CMake] x capture.exe
1> [CMake] x csvexport.exe
1> [CMake] x import-chrome.exe
1> [CMake] x Tracy.exe
1> [CMake] x update.exe
1> [CMake] -- Modifying C:/ffxi/server/ext/tracy/tracy-0.8.2/client/TracyProfiler.hpp
...
1> [CMake] -- Configuring done
1> [CMake] -- Generating done
1> [CMake] -- Build files have been written to: C:/ffxi/server/build/x64-Release-Tracy
```

`Tracy.exe` will be placed in your repo root.

## Usage

Run your Tracy-enabled `xi_map.exe` and then launch `Tracy.exe`. You will see it connect and start profiling. You can launch `Tracy.exe` before or after `xi_map.exe`, it isn't important.

It is usually better to wait until startup has completed before you attach Tracy, as the startup routine isn't a good indicator of the server's runtime performance.

Once connected, you should see something like this:

![image](https://user-images.githubusercontent.com/1389729/184949465-373513d3-5af2-4737-8734-3bf12e14a24f.png)

If you want to record a trace for later use you can click on the `Wifi symbol` and you'll be given the option to save the current trace.

![image](https://user-images.githubusercontent.com/1389729/184949741-25c5c6a9-fa5e-4beb-80b2-3d0202058aa2.png)

**WARNING** Traces can be very large! Plan accordingly!

## Finding Problems

Searchable statistics are in the `Statistics` header, log messages are in `Messages`. You can click and drag and zoom around the main timeline window for information about whats going on. You can "re-attach" to the most active frames by clicking on the `Pause/Resume` header and using the options there.

![image](https://user-images.githubusercontent.com/1389729/184949889-ac577f3b-8124-42e2-8954-493289a86683.png)

![image](https://user-images.githubusercontent.com/1389729/184949998-5cade8da-af6c-49a5-8115-e37f2014655d.png)

If you click on the entries in the `Statistics` menu, you can drill down into that function and look at it in more detail.

![image](https://user-images.githubusercontent.com/1389729/184950126-3e32ad0c-3f30-48ac-945d-6a6efd120633.png)

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

## Known bottlenecks

- Expensive pathing and navmesh access... all the time... every tick... every mob... everywhere...
- `parse` routine is slow
