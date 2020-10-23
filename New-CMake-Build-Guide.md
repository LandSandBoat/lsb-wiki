## Windows
Long term users will notice that the `win32` folder, the `.sln` file, and `.vcproj` files are all gone. In their place: `CMakeLists.txt` files in every folder that has something to be built. Don't worry, `Visual Studio 2017` and `Visual Studio 2019` have `CMake` built-in.

To open the project, follow these steps and open the `CMakeLists.txt` file in the root of the repo. 

![vs_build_1](https://user-images.githubusercontent.com/1389729/96963902-2b00cf00-1512-11eb-804c-47ea881888b9.png)

Visual Studio will handle everything from there, and you'll be able to select your target to build and debug like you did before. Debug paths, executable output paths etc. are all handled automatically.

## Linux
The same CMake steps as before (make sure you have CMake installed with `sudo apt install cmake` or similar):
```
mkdir build
cd build
cmake ..
make -j`nproc`
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
