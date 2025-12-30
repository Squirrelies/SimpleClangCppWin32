project(SimpleClangCppWin32_Common)

set(LOCAL_EXPORT_NAME Common)
set(RC_INTERNALNAME "SimpleClangCppWin32.Common")
set(RC_FILEDESCRIPTION "A shared library for SimpleClangCppWin32 containing common functions.")
set(RC_ORIGINALFILENAME "${RC_INTERNALNAME}.dll")
configure_file(${CMAKE_SOURCE_DIR}/src/VersionInfo.rc.in ${PROJECT_BINARY_DIR}/VersionInfoCommon.rc @ONLY)

add_library(${PROJECT_NAME} SHARED)
add_library(SimpleClangCppWin32::Common ALIAS ${PROJECT_NAME})

# set_project_compile_options(${PROJECT_NAME})
# set_project_compile_definitions(${PROJECT_NAME})
# set_project_link_options(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
    PRIVATE
        ${PROJECT_BINARY_DIR}/VersionInfoCommon.rc
        Common.cpp
)

target_include_directories(${PROJECT_NAME}
    PUBLIC
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

set_target_properties(${PROJECT_NAME} PROPERTIES
    OUTPUT_NAME ${RC_INTERNALNAME}
    EXPORT_NAME ${LOCAL_EXPORT_NAME}
)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD COMMAND $<$<OR:$<CONFIG:RELEASE>,$<CONFIG:MINSIZEREL>>:${CMAKE_STRIP}> ARGS --strip-all $<TARGET_FILE:${PROJECT_NAME}>)

install(TARGETS ${PROJECT_NAME}
    EXPORT SimpleClangCppWin32Targets
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
)

install(DIRECTORY include/
    DESTINATION include
)