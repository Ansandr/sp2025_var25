# Verify Syntax by EBNF Nonpacked 2025 Project

add_executable(verify_syntax_by_EBNF_nonpacked__2025
    main.c
)

set_target_properties(verify_syntax_by_EBNF_nonpacked__2025 PROPERTIES
    LINKER_LANGUAGE C
)

target_compile_definitions(verify_syntax_by_EBNF_nonpacked__2025 PRIVATE
    _CRT_SECURE_NO_WARNINGS
)

# Check if Boost is available
find_package(Boost QUIET)
if(Boost_FOUND)
    target_include_directories(verify_syntax_by_EBNF_nonpacked__2025 PRIVATE ${Boost_INCLUDE_DIRS})
elseif(EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/../boost)
    target_include_directories(verify_syntax_by_EBNF_nonpacked__2025 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../boost)
endif()

# Set working directory for debugging (Visual Studio)
set_target_properties(verify_syntax_by_EBNF_nonpacked__2025 PROPERTIES
    VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Install target
install(TARGETS verify_syntax_by_EBNF_nonpacked__2025
    RUNTIME DESTINATION bin
)
