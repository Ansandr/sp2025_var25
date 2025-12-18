cmake_minimum_required(VERSION 3.15)

project(cw_sp2__2024_2025 LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Set default build type if not specified
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Build type" FORCE)
endif()

# Add compiler flags for MSVC
if(MSVC)
    add_compile_definitions(_CRT_SECURE_NO_WARNINGS)
    add_compile_definitions(WIN32_LEAN_AND_MEAN)
    add_compile_options(/W3)
    # Set runtime library
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()

# Add compiler flags for GCC/Clang
if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    add_compile_options(-Wall -Wextra)
endif()

# Define output directories
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

# Make output directories for Debug and Release the same
foreach(OUTPUTCONFIG ${CMAKE_CONFIGURATION_TYPES})
    string(TOUPPER ${OUTPUTCONFIG} OUTPUTCONFIG_UPPER)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${OUTPUTCONFIG_UPPER} ${CMAKE_BINARY_DIR}/bin)
    set(CMAKE_LIBRARY_OUTPUT_DIRECTORY_${OUTPUTCONFIG_UPPER} ${CMAKE_BINARY_DIR}/lib)
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_${OUTPUTCONFIG_UPPER} ${CMAKE_BINARY_DIR}/lib)
endforeach()

# Add subdirectories for each project
add_subdirectory(dfa_generator__2025)
add_subdirectory(cw_sp2__2025_2026)
add_subdirectory(verify_syntax_by_EBNF__2025)
add_subdirectory(verify_syntax_by_EBNF_nonpacked__2025)
add_subdirectory(wrapWithInOutPipe)
add_subdirectory(assembly_pattern)
add_subdirectory(image_pattern_generator)

# Check if dpda1_for_ll2_generator__2025 exists
if(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/dpda1_for_ll2_generator__2025)
    add_subdirectory(dpda1_for_ll2_generator__2025)
endif()

# Print configuration information
message(STATUS "=== Build Configuration ===")
message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")
message(STATUS "C++ compiler: ${CMAKE_CXX_COMPILER_ID} ${CMAKE_CXX_COMPILER_VERSION}")
message(STATUS "C++ standard: ${CMAKE_CXX_STANDARD}")
message(STATUS "Output directory: ${CMAKE_BINARY_DIR}/bin")
