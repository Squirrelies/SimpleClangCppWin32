project(SimpleClangCppWin32_App)

set(LOCAL_EXPORT_NAME App)
set(RC_INTERNALNAME "SimpleClangCppWin32")
set(RC_FILEDESCRIPTION "The SimpleClangCppWin32 application.")
set(RC_ORIGINALFILENAME "${RC_INTERNALNAME}.exe")
configure_file(${CMAKE_SOURCE_DIR}/src/VersionInfo.rc.in ${PROJECT_BINARY_DIR}/VersionInfoApp.rc @ONLY)

### For Console Applications
#add_executable(${PROJECT_NAME})
### For Win32 Applications
add_executable(${PROJECT_NAME} WIN32)
add_executable(SimpleClangCppWin32::App ALIAS ${PROJECT_NAME})

# set_project_compile_options(${PROJECT_NAME} "-Wno-cast-function-type-mismatch")
# set_project_compile_definitions(${PROJECT_NAME})
# set_project_link_options(${PROJECT_NAME})

target_sources(${PROJECT_NAME}
    PRIVATE
        ${PROJECT_BINARY_DIR}/VersionInfoApp.rc
        Main.cpp
)

target_include_directories(${PROJECT_NAME}
    PUBLIC
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

target_link_libraries(${PROJECT_NAME}
PRIVATE SimpleClangCppWin32::Common
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