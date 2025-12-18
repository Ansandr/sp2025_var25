# Assembly Pattern Project

# This project contains assembly code that needs special handling
# For now, we'll create a custom target to handle the assembly file

# Check if MASM is available (only on Windows with Visual Studio)
if(MSVC)
    enable_language(ASM_MASM)
    
    add_executable(assembly_pattern
        patter.asm
    )
    
    set_source_files_properties(patter.asm PROPERTIES LANGUAGE ASM_MASM)
    
    # Set working directory for debugging (Visual Studio)
    set_target_properties(assembly_pattern PROPERTIES
        VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"
        LINK_FLAGS "/SUBSYSTEM:CONSOLE /ENTRY:mainCRTStartup"
    )
    
    # Install target
    install(TARGETS assembly_pattern
        RUNTIME DESTINATION bin
    )
else()
    message(WARNING "Assembly Pattern project requires MASM (Microsoft Macro Assembler) and is only supported on Windows with MSVC")
endif()
