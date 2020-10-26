# Windows
Long term users will notice that the `win32` folder, the `.sln` file, and `.vcproj` files are all gone. In their place: `CMakeLists.txt` files in every folder that has something to be built. Don't worry, `Visual Studio 2017` and `Visual Studio 2019` have `CMake` built-in.

To open the project, follow these steps and open the `CMakeLists.txt` file in the root of the repo.

`File > Open > Folder` in the repo root will also work. 

![vs_build_1](https://user-images.githubusercontent.com/1389729/96963902-2b00cf00-1512-11eb-804c-47ea881888b9.png)
![image](https://user-images.githubusercontent.com/1389729/97025486-cd47a380-1560-11eb-8d02-0d19b539bd2c.png)

CMake will think for a moment and start configuring your build.
```
...
1> Working directory: C:\topaz\topaz\out\build\x86-Debug
1> [CMake] -- The CXX compiler identification is MSVC 19.27.29112.0
1> [CMake] -- Check for working CXX compiler: C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Tools/MSVC/14.27.29110/bin/Hostx86/x86/cl.exe
1> [CMake] -- Check for working CXX compiler: C:/Program Files (x86)/Microsoft Visual Studio/2019/Community/VC/Tools/MSVC/14.27.29110/bin/Hostx86/x86/cl.exe - works
1> [CMake] -- Detecting CXX compiler ABI info
...
```

After a little time, the output log should present you with:
```
...
1> [CMake] -- Configuring done
1> [CMake] -- Generating done
1> [CMake] -- Build files have been written to: C:/topaz/topaz/out/build/x86-Debug
1> Extracted CMake variables.
1> Extracted source files and headers.
1> Extracted code model.
1> Extracted includes paths.
1> CMake generation finished.
```

Configuration is now done!

You can select your build type here:

![image](https://user-images.githubusercontent.com/1389729/97194560-f2cbeb80-17b2-11eb-9353-f91831308ff7.png)

If you want to build everything, you can go here:

![image](https://user-images.githubusercontent.com/1389729/97194671-198a2200-17b3-11eb-94d0-20927d88d7ef.png)

If you want to build and debug a specific executable, you can go here:

![image](https://user-images.githubusercontent.com/1389729/97194922-6241db00-17b3-11eb-806c-0f2f3cb047cd.png)

Debug paths, executable output paths etc. are all handled automatically, unlike the old `.sln` files which didn't work for debugging 'out-of-the-box'.

## Windows Commandline
_Make sure you have `CMake` available to use in your `PATH` through some means._
```
mkdir build
cd build
cmake .. && cmake --build .
```

The default is x64, you can force 32-bit with: `cmake .. -A Win32 && cmake --build .`

## Generate a .sln file
_Make sure you have `CMake` available to use in your `PATH` through some means._

If for some reason you want a `.sln` file, you can generate one with:
`cmake -G "Visual Studio 16 2019" ..` or `cmake -G "Visual Studio 15 2017" ..`

# Linux
The same CMake steps as before (make sure you have CMake installed with `sudo apt install cmake` or similar):
```
mkdir build
cd build
cmake ..
make -j $(nproc)
```

## Troubleshooting
#### Paths containing spaces
Currently, the build will fail on paths that contain spaces: https://github.com/project-topaz/topaz/issues/1436

#### Drive Letters
It appears as though the build will fail if you try to launch it from a raw drive letter (eg. `D:/`). Instead, use a subfolder: `D:/topaz`.

#### External Libraries
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
```
cmake .. -DMYSQL_INCLUDE_DIR=C:\dev\topaz\ext\lib\mysql -DMYSQL_LIBRARY=C:\dev\topaz\ext\lib\libmariadb.lib
```

## Why the change?
Historically, we've had 3 build systems: VS Solution, Linux makefile and CMake. On all platforms, when you wanted to add a file you had to add them to the VS `.sln` file, often by hand. This made cross-platform development annoying, and merge conflicts on the XML-based `.sln` files were a pain. `CMake` files are simple and allow us to more easily split the project into logical chunks to build and apply different build settings to.

This first version is recreating the original build as closely as possible. Now that it's complete, it will allow us to:
- Make sure build flags and warning/error settings are the same on platforms.
- Add/remove/upgrade external dependencies more easily.
- Apply tools like `UBSan` and `Valgrind` to the build more easily.
- Easily apply performance benchmarking tools like `Orbit` or `Tracy`.
- Add/split-out new executables more easily, reusing existing code.

## Adding Files
Add the `.h` and the `.cpp` file to the `SOURCES` list in the `CMakeLists.txt` file in the folder where the new files live.

![image](https://user-images.githubusercontent.com/1389729/96964877-e7a76000-1513-11eb-9757-710e53b2858a.png)

If you use `Visual Studio` or `CLion`, they will automatically pick up this change and regenerate your CMake cache. On Linux you will need to update your cache by running `cmake ..` in your `build` folder before you run `make`.
