You can find a template for the examples in the [exampleLibraryTemplate](../Libraries/exampleLibraryTemplate) directory.
It includes templates for the `Makefile/CMakeLists.txt`s, `main.hip` and the `README.md`s.

To keep the style of the examples consistent, please follow the following guidelines when implementing your example.

# Guidelines

## Make/CMake
Use the `Makefile/CMakeLists.txt`s files as templates and style-guide.<br/>
Each example has to at least support `CMake` as build system. The simpler examples should also support `Make`.<br/>
Every example has to be able to be built separately from the others, but also has to be added to the top-level build scripts (compare the `Makefile/CMakelists.txt`s in the exampleLibraryTemplate).

## Code Format
The formatting rules of the examples are enforced by `clang-format` using the `.clang-format` file in the top-level directory.

## Naming Conventions
- Use `lower_snake_case` style to name variables and functions (e.g. block_size, multiply_kernel and multiply_host).
- Use `PascalCase` for `class`, `struct`, `enum` and template argument definitions.

## Binary Naming Conventions
Use the prefix of the library for the name of the binary, so that there are no conflicts between libraries (e.g. hipcub_device_sum and rocprim_device_sum).

## Utilities
Utility-functions (printing vectors, etc) and common error-handling code, that is used by all examples, should be moved to the common utility-header [example_utils.hpp](../Common/example_utils.hpp).

## Error Handling
Error checking and handling should be applied where appropriate, e.g. when handling user input. `HIP_CHECK` should be used whenever possible. Exceptions should only be used if the complexity of the program requires it.<br/>
In most cases printing an explanation to stderr and terminating the program with an error code, as specified in the common header, is sufficient.

## Printing Intermediate Results
Results should be printed when they are helpful for the understanding and showcasing the example. However the output shouldn't be overwhelming, printing a vector with hundreds of entries is usually not useful.

## .gitignore
The .gitignore in the `example_template`-subdirectory is needed to exclude the binary generated when using Make.
