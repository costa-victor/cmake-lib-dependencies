
# CMake library dependencies

This educational repository contains a collection of examples showing how to use CMake for creating, building, installing, managing dependencies, and using libraries with CMake and C++.
Additionally, the dependency chain between the libraries is represented by the following topics:
- `headerOnlyLib` is a header-only library
- `headerOnlyLib/example` demonstrate how to use the `headerOnlyLib`
- `someLibA` is a static library
- `someLibA/example` demonstrate how to use the `someLibA`
- `someLibB` is a static library, but it also depends on `someLibA` and therefore it's propagated when `someLibB` is consumed.
- `someLibB/example` demonstrate how to use the `someLibB` and its dependency `someLibA`.
- `someLibC` is a static library, but it depends on `someLibB`, which already has a dependecy on the `someLibA`.
- `someLibC/example` demonstrate how to use the `someLibC` and its dependency `someLibB` and `headerOnlyLib`.
- `App` depends on the `someLibA`, `someLibB` and `someLibC`


_**NOTE:** Tested on macOS/Ubuntu, this may not work on Windows_

## Project Structure

```bash
├── App                    # Application example
│   ├── CMakeLists.txt
│   └── src
├── README.md
├── LICENSE
├── headerOnlyLib          # Header only library
│   ├── CMakeLists.txt
│   ├── cmake
│   ├── example
│   └── include
├── someLibA               # Static library A
│   ├── CMakeLists.txt
│   ├── cmake
│   ├── example
│   ├── include
│   └── src
├── someLibB               # Static library B which depends on A
│   ├── CMakeLists.txt
│   ├── cmake
│   ├── example
│   ├── include
│   └── src
└── someLibC               # Static library C which depends on B and headerOnlyLib
    ├── CMakeLists.txt
    ├── cmake
    ├── example
    ├── include
    └── src
```

## Requirements

- CMake 3.20 or higher
- C++11 compatible compiler

## Building the Project

### Building and installing someLib's A,B,C and headerOnlyLib individually

1. Navigate to the library directory:

   ```bash
   cd someLibA
   ```

2. Create and navigate to the build directory:

   ```bash
   mkdir -p build
   cd build
   ```

3. Configure, build and install the library:

   ```bash
   cmake ..
   cmake --build . --target install
   ```

### Building and installing all the libraries

1. Execute all the commands above with one command

   ```bash
   make
   ```

### Building and running the Application

1. Navigate to the `App` directory:

   ```bash
   cd App
   ```

2. Create and navigate to the build directory:

   ```bash
   mkdir -p build
   cd build
   ```

3. Configure and build the application (make sure `someLibA` and `someLibB` are installed and found by CMake):

   ```bash
   cmake ..
   cmake --build .
   ./app
   ```


## Extra

### Example for someLib's A,B,C and headerOnlyLib

You can find example usage of the library in the `example` folder.
