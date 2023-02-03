## Build Troubleshooting

## Windows Commandline

_Make sure you have `CMake` available to use in your `PATH` through some means._

```sh
mkdir build
cd build
cmake .. && cmake --build .
```

The default is x64, you can force 32-bit with: `cmake .. -A Win32 && cmake --build .`

# Linux

The same CMake steps as before (make sure you have CMake installed with `sudo apt install cmake` or similar):
```
mkdir build
cd build
cmake ..
make -j $(nproc)
```

## Troubleshooting

### Paths containing spaces

Previously, the build could fail on paths that contain spaces. While it works _now_, it isn't recommended.

### Drive Letters

It appears as though the build will fail if you try to launch it from a raw drive letter (eg. `D:/`). Instead, use a subfolder: `D:/topaz`.

### External Libraries

On Windows, if you have versions of our external libraries installed on your machine, CMake might try to use them. You'll be able to catch this during configuration when CMake reports:

```
-- MYSQL_LIBRARY: C:\mysql-ver-1.0\lib
-- MYSQL_INCLUDE_DIR: C:\mysql-ver-1.0\include
```

This should be reporting the bundled versions we keep, something like this:

```
-- MYSQL_LIBRARY: C:\dev\topaz\ext\lib\mysql
-- MYSQL_INCLUDE_DIR: C:\dev\topaz\ext\include\mysql
```

If this happens, you can override these paths when you configure CMake:

```sh
cmake .. -DMYSQL_INCLUDE_DIR=C:\dev\topaz\ext\lib\mysql -DMYSQL_LIBRARY=C:\dev\topaz\ext\lib\libmariadb.lib
```
