cmake_minimum_required(VERSION 3.0)


project(Horror)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Set the include directories
include_directories(include)

# Find SFML
find_package(SFML 2.5 COMPONENTS graphics window system REQUIRED)

# Collect all source files in the src directory
file(GLOB_RECURSE SOURCES "src/*.cpp")

# Add the executable
add_executable(Horror ${SOURCES})

# Link SFML libraries
target_link_libraries(Horror sfml-graphics sfml-window sfml-system)

# Copy the assets directory to the build directory
add_custom_command(TARGET Horror POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/assets $<TARGET_FILE_DIR:Horror>/assets)

# Set the working directory to the directory containing the assets
set_target_properties(Horror PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY $<TARGET_FILE_DIR:MyProject>)
