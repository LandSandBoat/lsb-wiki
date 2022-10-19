# Development Guide (General)

## Performance

LSB and its predecessors are mostly single-threaded. This means we have to be conscious of how much work we're doing at any given time. If we commit to doing too much work, or the work takes too long, the performance of the server will degrade; leading to lag and/or instability.

Below are some benchmarks comparing similar workloads in C++, in Lua using function caching, and Lua without using funciton caching.

```txt
--------------------------------------------------------------------
Benchmark                          Time             CPU   Iterations
--------------------------------------------------------------------
BM_Core_Function                2.13 ns         2.13 ns    448000000
BM_New_Sol_Cache_Function       56.4 ns         55.8 ns      8960000
BM_Old_Lua_Read_From_Disk      61804 ns        61384 ns        11200
```

As you can see, C++ is the clear winner, with function-cached Lua being an order of magnitude slower, and with uncached Lua being a further order of magnitude slower than that.

This means that if a piece of work is particularly large or performance critical it should be moved into C++. Otherwise, it's probably fine to exist in Lua.

**NOTE:** This comparison doesn't include SQL queries. They tend to be as slow, or slower than disk reads. Read and write from SQL as little as possible (or cache everything you can!).

Performance critical systems that should always stay in C++:

- Networking (packet sending/recieving)
- Entity iteration
- Navmesh access
- Database reads & writes
- File reads & writes
