# Require CMake 3.15+ (matching scikit-build-core) Use new versions of all
# policies up to CMake 4.0
cmake_minimum_required(VERSION 3.15...4.0)

project(
  ${SKBUILD_PROJECT_NAME}
  VERSION ${SKBUILD_PROJECT_VERSION}
  LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Find pybind11 and Python
find_package(pybind11 CONFIG REQUIRED)

# Create the _core module
python_add_library(_core MODULE cpp/src/interface.cpp WITH_SOABI)
target_link_libraries(_core PRIVATE pybind11::headers)

# Define macros
target_compile_definitions(_core PRIVATE VERSION_INFO=${PROJECT_VERSION})

# The install directory is the output (wheel) directory
install(TARGETS _core DESTINATION optimo)

if(CMAKE_EXPORT_COMPILE_COMMANDS)
    add_custom_target(copy_compile_commands ALL
        COMMAND ${CMAKE_COMMAND} -E copy_if_different
                ${CMAKE_BINARY_DIR}/compile_commands.json
                ${PROJECT_SOURCE_DIR}/compile_commands.json
        COMMENT "Copying compile_commands.json to target directory"
    )
endif()