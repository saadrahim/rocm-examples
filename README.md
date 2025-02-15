# ROCm Examples

## Repository Contents
- [Common](/Common/) contains common utility functionality shared between the examples.
- [HIP-Basic](/HIP-Basic/) hosts self-contained recipes showcasing HIP runtime functionality.
    - [device_query](/HIP-Basic/device_query): Program that showcases how properties from the device may be queried.
    - [dynamic_shared](/HIP-Basic/dynamic_shared): Program that showcases how to use dynamic shared memory with the help of a simple matrix transpose kernel.
    - [hello_world](/HIP-Basic/hello_world): Simple program that showcases launching kernels and printing from the device.
    - [hipify](/HIP-Basic/hipify): Simple program and build definitions that showcase automatically converting a CUDA `.cu` source into portable HIP `.hip` source.
    - [matrix_multiplication](/HIP-Basic/matrix_multiplication/): Multiply two dynamically sized matrices utilizing shared memory.
    - [occupancy](/HIP-Basic/occupancy/): Shows how to find optimal configuation parameters for a kernel launch with maximum occupancy.
    - [saxpy](/HIP-Basic/saxpy/): Implements the $Y_i=aX_i+Y_i$ kernel and explains basic HIP functionality.
- [Dockerfiles](/Dockerfiles/) hosts Dockerfiles with ready-to-use environments for the various samples. See [Dockerfiles/README.md](Dockerfiles/README.md) for details.
- [docs](/docs/)
    - [CONTRIBUTING.md](docs/CONTRIBUTING.md) contains information on how to contribute to the examples.
- [Libraries](/Libraries/)
    - [hipCUB](/Libraries/hipCUB/)
        - [device_radix_sort](/Libraries/hipCUB/device_radix_sort/): Simple program that showcases `hipcub::DeviceRadixSort::SortPairs`.
        - [device_sum](/Libraries/hipCUB/device_sum/): Simple program that showcases `hipcub::DeviceReduce::Sum`.
    - [rocPRIM](/Libraries/rocPRIM/)
        - [block_sum](/Libraries/rocPRIM/block_sum/): Simple program that showcases `rocprim::block_reduce` with an addition operator.
        - [device_sum](/Libraries/rocPRIM/device_sum/): Simple program that showcases `rocprim::reduce` with an addition operator.
    - [rocRAND](/Libraries/rocRAND/)
        - [simple_distributions_cpp](/Libraries/rocRAND/simple_distributions_cpp/): A command-line app to compare random number generation on the CPU and on the GPU with rocRAND.
    - [rocThrust](/Libraries/rocThrust/)
        - [device_ptr](/Libraries/rocThrust/device_ptr/): Simple program that showcases the usage of the `thrust::device_ptr` template.
        - [norm](/Libraries/rocThrust/norm/): An example that computes the Euclidean norm of a `thrust::device_vector`.
        - [reduce_sum](/Libraries/rocThrust/reduce_sum/): An example that computes the sum of a `thrust::device_vector` integer vector using the `thrust::reduce()` generalized summation and the `thrust::plus` operator.
        - [remove_points](/Libraries/rocThrust/remove_points/): Simple program that demonstrates the usage of the `thrust` random number generation, host vector, generation, tuple, zip iterator, and conditional removal templates. It generates a number of random points in a unit square and then removes all of them outside the unit circle.
        - [saxpy](/Libraries/rocThrust/saxpy/): Simple program that implements the SAXPY operation (`Y[i] = a * X[i] + Y[i]`) using rocThrust and showcases the usage of the vector and functor templates and of `thrust::fill` and `thrust::transform` operations.
        - [vectors](/Libraries/rocThrust/vectors/): Simple program that showcases the `host_vector` and the `device_vector` of rocThrust.

## Prerequisites
### Linux
- [CMake](https://cmake.org/download/) (at least version 3.21)
- A number of examples also support building via  GNU Make - available through the distribution's package manager
- [ROCm](https://docs.amd.com/bundle/ROCm-Installation-Guide-v5.1.3/page/Overview_of_ROCm_Installation_Methods.html) (at least version 5.x.x)
- For example-specific prerequisites, see the example subdirectories.

### Windows
- [Visual Studio](https://visualstudio.microsoft.com/) 2019 or 2022 with the "Desktop Development with C++" workload
- [CMake](https://cmake.org/download/) (at least version 3.21)
- ROCm toolchain for Windows (No public release yet)
  - The Visual Studio ROCm extension needs to be installed to build with the solution files.

## Building the example suite
### Linux
These instructions assume that the prerequisites for every example are installed on the system.

#### CMake
- `$ git clone https://github.com/amd/rocm-examples.git`
- `$ cd rocm-examples`
- `$ cmake -S . -B build` (on ROCm) or `$ cmake -S . -B build -D GPU_RUNTIME=CUDA` (on CUDA)
- `$ cmake --build build`

#### Make
Beware that only a subset of the examples support building via Make.
- `$ git clone https://github.com/amd/rocm-examples.git`
- `$ cd rocm-examples`
- `$ make` (on ROCm) or `$ make GPU_RUNTIME=CUDA` (on CUDA)

### Linux with Docker
Alternatively, instead of installing the prerequisites on the system, the [Dockerfiles](/Dockerfiles/) in this repository can be used to build images that provide all required prerequisites. Note, that the ROCm kernel GPU driver still needs to be installed on the host system.

The following instructions showcase building the Docker image and full example suite inside the container using CMake:
- `$ git clone https://github.com/amd/rocm-examples.git`
- `$ cd rocm-examples/Dockerfiles`
- `$ docker build . -t rocm-examples -f hip-libraries-rocm-ubuntu.Dockerfile` (on ROCm) or `$ docker build . -t rocm-examples -f hip-libraries-cuda-ubuntu.Dockerfile` (on CUDA)
- `$ docker run -it --device /dev/kfd --device /dev/dri rocm-examples bash` (on ROCm) or `$ docker run -it --gpus=all rocm-examples bash` (on CUDA)
- `# git clone https://github.com/amd/rocm-examples.git`
- `# cd rocm-examples`
- `# cmake -S . -B build` (on ROCm) or `$ cmake -S . -B build -D GPU_RUNTIME=CUDA` (on CUDA)
- `# cmake --build build`

The built executables can be found and run in the `build` directory:
- `# ./build/Libraries/rocRAND/simple_distributions_cpp/simple_distributions_cpp`

### Windows
#### Visual Studio
The repository has Visual Studio project files for all examples and individually for each example.
- Project files for Visual Studio are named as the example with `_vs<Visual Studio Version>` suffix added e.g. `device_sum_vs2019.sln` for the device sum example.
- The project files can be built from Visual Studio or from the command line using MSBuild.
  - Use the build solution command in Visual Studio to build.
  - To build from the command line execute `C:\Program Files (x86)\Microsoft Visual Studio\<Visual Studio Version>\<Edition>\MSBuild\Current\Bin\MSBuild.exe <path to project folder>`.
    - To build in Release mode pass the `/p:Configuration=Release` option to MSBuild.
    - The exutables will be created in a subfolder named "Debug" or "Release" inside the project folder.
- The HIP specific project settings like the GPU architectures targeted can be set on the `General [AMD HIP C++]` tab of project properties.
