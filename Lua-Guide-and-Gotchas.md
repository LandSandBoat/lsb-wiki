**This guide is only relevant after the Sol refactoring is complete**

# Gotchas

### General
We use Sol, which has a Lua 5.3 compatibility layer, on top of luajit 2.0, which acts like Lua 5.1. Given this mismatch there are a few idiosyncracies to be aware of, listed below.

### ipairs, pairs, collections
https://sol2.readthedocs.io/en/latest/containers.html
```
Containers from C++ are stored as userdata with special usertype metatables with special operations
...
calling pairs( c ) in Lua 5.1 / LuaJIT will crash with assertion failure (Lua expects c to be a table);
can be used as regular function c:pairs() to get around limitation
```

If returning a container from C++ into Lua, it will be treated as userdata, not a container. You cannot call `pair(container)`. Instead you must call the convenience function: `container:pairs()`. Same for `ipairs`.