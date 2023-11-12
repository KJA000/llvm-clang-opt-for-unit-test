# compiler optimization analyzing

llvm clang
toolchain for aarm64
tflite
cmake -DCMAKE_TOOLCHAIN_FILE=../arm_compiler.cmake ../tensorflow/lite/examples/minimal
make benchmark_model

# arm_compiler.cmake
set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_PROCESSOR aarch64)

set(triple aarch64-linux-gnu)
set(toolchain /home/jiae/toolchains/gcc-arm-8.3-2019.03-x86_64-aarch64-linux-gnu)

set(CMAKE_SYSROOT ${toolchain}/aarch64-linux-gnu/libc)

set(CMAKE_C_COMPILER   clang-10)
set(CMAKE_CXX_COMPILER clang-10)
set(CMAKE_AR llvm-ar)

set(CMAKE_C_FLAGS "-O3 --gcc-toolchain=${toolchain}")
set(CMAKE_CXX_FLAGS "-O3 --gcc-toolchain=${toolchain}")
set(CMAKE_ASM_FLAGS "-target aarch64-linux-gnu --gcc-toolchain=${toolchain}")

//overwrite O3 default flag
set(CMAKE_C_FLAGS_RELEASE "-DNDEBUG")
set(CMAKE_CXX_FLAGS_RELEASE "-DNDEBUG")
set(CMAKE_ASM_FLAGS_RELEASE "-DNDEBUG")

set(CMAKE_EXE_LINKER_FLAGS "-fuse-ld=lld -L${toolchain}/aarch64-linux-gnu/libc/lib64 -L${toolchain}/lib/gcc/aarch64-linux-gnu/8.3.0 -lm -lstdc++")

set(CMAKE_C_COMPILER_FORCED TRUE)
set(CMAKE_CXX_COMPILER_FORCED TRUE)

set(CMAKE_C_COMPILER_TARGET ${triple})
set(CMAKE_CXX_COMPILER_TARGET ${triple})

list(APPEND CMAKE_CXX_COMPILE_FEATURES
    cxx_std_11
    cxx_std_17
)

set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_PACKAGE ONLY)


실행시간측정
