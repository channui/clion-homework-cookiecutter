# Base CLion Project setup for simple homework

## Installation

### MacOS
As of right now the default compiler on macOS DOES NOT support
-fsanitize=address to check for leaks.  Right now the llvm clang/clang++
compiler from homebrew will support it (g++ does not on Apple Silicon).

This requires brew to be installed

Start a terminal and execute the following to install brew from the https://brew.sh website:

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

Follow the instructions to activate brew.

Install catch2, boost and llvm:

    brew install catch2 boost llvm

Boost is optional but is a wonderful set of libraries, llvm is required to give
you -fsanitize leak checking, and catch2 is a unit testing framework (boost also contains one).

#### Configure CLion

1. Navigate to CLion -> Preferences -> Build, Execution, Deployment -> Toolchains
2. Click the + button to create a new Toolchain
3. Set the C Compiler to /opt/homebrew/opt/llvm/bin/clang
4. Set the C++ Compiler to /opt/homebrew/opt/llvm/bin/clang++
5. Navigate to CLion -> Preferences -> Build, Execution, Deployment -> CMake
6. Click the + button to create a new Profile
7. Select the Toolchain you you previously created

1. Navigate to CLion -> Preferences -> Build, Execution, Deployment -> Dynamic Analysis Tools -> Sanitizers
2. Uncheck Use visual represntation for Sanitizer's output
3. Prepend `detect_leaks=1` to the Address Sanitizer line

