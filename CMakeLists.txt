cmake_minimum_required(VERSION 3.31)
if(CMAKE_C_COMPILER MATCHES "clang-cl-msvcenv\\.cmd$")
  set(CMAKE_C_COMPILER_ID "Clang" CACHE STRING "" FORCE)
  set(CMAKE_CXX_COMPILER_ID "Clang" CACHE STRING "" FORCE)
endif()
project (SimpleClangCppWin32)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(SetFromEnv)
include(ProjectSettings)
include(ClangTidy)

add_subdirectory(src/Common)
add_subdirectory(src/App)
