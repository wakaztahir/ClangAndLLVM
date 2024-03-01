cmake_minimum_required(VERSION 3.27)
project(CheckClang)

set(CMAKE_CXX_STANDARD 17)

# Set the path to your LLVM and Clang installation
set(LLVM_DIR "D:/Software/Installed/llvmclang/lib/cmake/llvm")
set(Clang_DIR "D:/Software/Installed/llvmclang/lib/cmake/clang")

find_package(LLVM REQUIRED CONFIG)
find_package(Clang REQUIRED CONFIG)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

# Set your project compile flags.
if (MSVC)
    # Set iterator debugging level
    add_compile_options(/D_ITERATOR_DEBUG_LEVEL=0)  # Change to 0, 1, or 2 as needed
endif ()

# E.g. if using the C++ header files
# you will need to enable C++11 support
# for your compiler.

include_directories(${LLVM_INCLUDE_DIRS})
separate_arguments(LLVM_DEFINITIONS_LIST NATIVE_COMMAND ${LLVM_DEFINITIONS})
add_definitions(${LLVM_DEFINITIONS_LIST})

# Your executable target
add_executable(CheckClang main.cpp)

# Find the libraries that correspond to the LLVM components
# that we wish to use
llvm_map_components_to_libnames(llvm_libs support core irreader)

# Other clang libs clangTooling clangAST clangASTMatchers clangBasic
# Link against LLVM libraries
#LLVMX86AsmParser # MC, MCParser, Support, X86Desc, X86Info
#LLVMX86Desc # MC, Support, X86AsmPrinter, X86Info
#LLVMX86AsmPrinter # MC, Support, X86Utils
#LLVMX86Info # MC, Support, Target
#LLVMX86Utils # Core, Support
#LLVMipo
#LLVMScalarOpts
#LLVMInstCombine
#LLVMTransformUtils
#LLVMipa
#LLVMAnalysis
#LLVMTarget
#LLVMOption # Support
#LLVMMCParser # MC, Support
#LLVMMC # Object, Support
#LLVMObject # BitReader, Core, Support
#LLVMBitReader # Core, Support
#LLVMCore # Support
#LLVMSupport
target_link_libraries(CheckClang ${llvm_libs})

#clangFrontend
#clangSerialization
#clangDriver
#clangParse
#clangSema
#clangAnalysis
#clangAST
#clangBasic
#clangEdit
#clangLex
#clangTooling
target_link_libraries(CheckClang clangTooling)

# These compile options are available /MD /MDd /MT /MTd
# Set the runtime library option for the target
target_compile_options(CheckClang PRIVATE /MD)