cmake_minimum_required(VERSION 3.31)
project (SimpleClangCppWin32)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(SetFromEnv)
include(ProjectSettings)

add_subdirectory(src/Common)
add_subdirectory(src/App)
