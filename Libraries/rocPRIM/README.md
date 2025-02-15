# rocPRIM Examples

## Summary
The examples in this subdirectory showcase the functionality of the [rocPRIM](https://github.com/ROCmSoftwarePlatform/rocPRIM) library. The examples build on both Linux and Windows for the ROCm (AMD GPU) backend.

## Prerequisites
### Linux
- [CMake](https://cmake.org/download/) (at least version 3.21)
- OR GNU Make - available via the distribution's package manager
- [ROCm](https://docs.amd.com/bundle/ROCm-Installation-Guide-v5.1.3/page/Overview_of_ROCm_Installation_Methods.html) (at least version 5.x.x)
- [rocPRIM](https://github.com/ROCmSoftwarePlatform/rocPRIM)
    - `rocPRIM-dev` package available from [repo.radeon.com](https://repo.radeon.com/rocm/). The repository is added during the standard ROCm [install procedure](https://docs.amd.com/bundle/ROCm-Installation-Guide-v5.1.3/page/How_to_Install_ROCm.html).

### Windows
- [Visual Studio](https://visualstudio.microsoft.com/) 2019 or 2022 with the "Desktop Development with C++" workload
- [CMake](https://cmake.org/download/) (at least version 3.21)
- ROCm toolchain for Windows (No public release yet)
    - The Visual Studio ROCm extension needs to be installed to build with the solution files.
- [rocPRIM](https://github.com/ROCmSoftwarePlatform/rocPRIM)
    - Installed as part of the ROCm SDK on Windows for ROCm platform.


## Building
### Linux
Make sure that the dependencies are installed, or use one of the [provided Dockerfiles](../../Dockerfiles/) to build and run the examples in a containerized environment.

#### Using CMake
All examples in the `rocPRIM` subdirectory can be built by a single CMake project.

- `$ cd Libraries/rocPRIM`
- `$ cmake -S . -B build`
- `$ cmake --build build`

#### Using Make
All examples can be built by a single invocation to Make.
- `$ cd Libraries/rocPRIM`
- `$ make`

### Windows
#### Visual Studio
Visual Studio solution files are available for the individual examples. To build all examples for rocPRIM open the top level solution file [ROCm-Examples-VS2019.sln](../../ROCm-Examples-VS2019.sln) and filter for rocPRIM.

For more detailed build instructions refer to the top level [README.md](../../README.md#visual-studio).
