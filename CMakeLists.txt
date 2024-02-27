cmake_minimum_required(VERSION 3.27)
project(CheckClang)

set(CMAKE_CXX_STANDARD 17)

# Set the path to your LLVM and Clang installation
set(INCLUDE_DIRS D:\\Software\\Installed\\llvmclang\\include)
set(LIBRARY_DIRS D:\\Software\\Installed\\llvmclang\\lib)

# Find LLVM package
#find_package(LLVM REQUIRED CONFIG)

# Set include directories
include_directories(${INCLUDE_DIRS})

# Add LLVM definitions
#add_definitions(${LLVM_DEFINITIONS})

# Link against LLVM libraries
link_directories(${LIBRARY_DIRS})
#llvm_map_components_to_libnames(llvm_libs core support)

# Your executable target
add_executable(CheckClang main.cpp)

# Link against LLVM libraries
target_link_libraries(CheckClang ${llvm_libs})