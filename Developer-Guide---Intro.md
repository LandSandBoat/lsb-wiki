**WORK IN PROGRESS**

**So you want to develop for Topaz Next huh? (or forks and related projects)**

In this series of articles we're going to go over common concerns, tips and tricks, and examples you'll find useful on your journey. The topics are organized (roughly) from general and beginner-friendly, to specific and advanced.

**Topics**
- The Tech Stack (C++, Lua, SQL, (Python))
  - C++
  - Lua
  - SQL
  - Python
- Scripting (Lua)
  - Your first change
- SQL & Database Access
  - Locking & Tables
- High-level Architecture (C++)
  - Entities
  - Battlefields
  - Instances
  - Ticks & time_server
  - Performance profiling with Tracey
- Low-level Architecture (C++)
  - The 'Kernel'
  - IPC & Messaging
  - Networking & Packets

```
--------------------------------------------------------------------
Benchmark                          Time             CPU   Iterations
--------------------------------------------------------------------
BM_Core_Function                2.13 ns         2.13 ns    448000000
BM_New_Sol_Cache_Function       56.4 ns         55.8 ns      8960000
BM_Old_Lua_Read_From_Disk      61804 ns        61384 ns        11200
```