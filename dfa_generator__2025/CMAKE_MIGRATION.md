# DFA Generator 2025 - CMake Migration Summary

## Migration Complete ?

The `dfa_generator__2025` project has been successfully migrated to CMake with full support for both Visual Studio and VSCode.

## What Was Done

### 1. Updated CMakeLists.txt Configuration
**File**: `dfa_generator__2025/CMakeLists.txt`

**Key Changes**:
- Set C++ standard to C++17 (required for the project)
- Added compiler definitions: `_CRT_SECURE_NO_WARNINGS`, `WIN32_LEAN_AND_MEAN`, `USE_DFA_MINIMIZATION`
- Configured include directories to find `../built_src/` headers
- Set working directory to project source directory for both Visual Studio and VSCode debugging
- Added custom command to create output directories (`../built_doc/`, `../built_doc/full_dfa/`)
- Configured runtime output directory for consistent executable placement

### 2. Created Project Documentation
**File**: `dfa_generator__2025/README.md`

Comprehensive project-specific documentation including:
- Project overview and features
- Build instructions for Visual Studio, VSCode, and command line
- Regular expression notation reference
- Generated file structure
- Configuration options
- Debugging instructions
- Troubleshooting guide

### 3. Project Integration
**Verified**: `CMakeLists.txt` (root)

The project is properly integrated into the solution:
- Included via `add_subdirectory(dfa_generator__2025)`
- Inherits global C++ standard and compiler settings
- Uses shared output directories

## How to Use

### Visual Studio 2019/2022

**Method 1: Open as CMake Project** (Recommended)
1. File ? Open ? Folder...
2. Select the repository root directory
3. Visual Studio auto-configures CMake
4. Select configuration (Debug/Release)
5. Build ? Build All (Ctrl+Shift+B)
6. Set `dfa_generator__2025` as startup project
7. Debug ? Start Debugging (F5)

**Method 2: Generate Solution File**
```powershell
cmake --preset vs2022
cmake --build --preset vs2022
```
Then open `build/vs2022/cw_sp2__2024_2025.sln`

### VSCode

**First Time Setup**:
1. Install extensions: "C/C++" and "CMake Tools" by Microsoft
2. Open folder in VSCode
3. Ctrl+Shift+P ? "CMake: Configure"
4. Select your compiler kit

**Building**:
- Press F7 to build
- Or click [Build] in status bar

**Debugging**:
1. Set breakpoints in source files
2. Press F5
3. Select "(Windows) Launch dfa_generator" configuration
4. The working directory is automatically set to `dfa_generator__2025/`

### Command Line

```bash
# Configure
cmake -B build

# Build
cmake --build build --target dfa_generator__2025

# Run (from correct working directory)
cd dfa_generator__2025
../build/bin/dfa_generator__2025
```

## Project Structure

```
dfa_generator__2025/
??? CMakeLists.txt                    # CMake configuration
??? README.md                         # Project documentation
??? dfa_generator___part_impl.cpp    # Main implementation
??? Graphviz-14.0.5-win32--link.txt  # Graphviz download link
?
../built_src/                         # Generated files (parent dir)
??? file1.hpp                         # Transition table 1 (Tokens)
??? file1.txt
??? file2.hpp                         # Transition table 2 (Keywords)
??? file2.txt
??? file3.hpp                         # Transition table 3 (Identifiers)
??? file3.txt
??? file4.hpp                         # Transition table 4 (Unsigned Values)
??? file4.txt
?
../built_doc/                         # Generated documentation
??? fsm1.dot, .svg, .pdf             # Partial FSM visualizations
??? fsm2.dot, .svg, .pdf
??? fsm3.dot, .svg, .pdf
??? fsm4.dot, .svg, .pdf
??? full_dfa/
    ??? fsm*.dot, .svg, .pdf         # Full DFA visualizations
```

## Key Features of the CMake Configuration

1. **Automatic Directory Creation**: Output directories are created automatically during build

2. **Correct Working Directory**: The executable runs from the project source directory where it can access relative paths (`../built_src/`, `../built_doc/`)

3. **Include Path Configuration**: The build system knows to look in `../built_src/` for generated headers

4. **Cross-Platform Support**: Works on Windows (MSVC/MinGW), Linux (GCC/Clang), and macOS (Clang)

5. **IDE Integration**: 
   - Visual Studio: Uses `VS_DEBUGGER_WORKING_DIRECTORY` property
   - VSCode: Launch configurations in `.vscode/launch.json` set `cwd`

6. **Build Presets**: Supports CMakePresets.json for easy configuration switching

## Generated Files

When you run `dfa_generator__2025`, it generates:

1. **Header Files** (`../built_src/file*.hpp`):
   - `transitionTable1` through `transitionTable4`
   - State constants (Q000, Q001, ...)
   - Final state arrays

2. **Text Files** (`../built_src/file*.txt`):
   - Human-readable transition tables with state names

3. **Visualization Files** (if Graphviz available):
   - **Partial DFA** (without dead states): `../built_doc/fsm*.{dot,svg,pdf}`
   - **Full DFA** (with dead states): `../built_doc/full_dfa/fsm*.{dot,svg,pdf}`

## Configuration Options

### Enable/Disable DFA Minimization

**Enabled by default** via `target_compile_definitions` in CMakeLists.txt.

To disable:
```cmake
# Comment out or remove this line in CMakeLists.txt:
# target_compile_definitions(dfa_generator__2025 PRIVATE USE_DFA_MINIMIZATION)
```

### Graphviz Integration

- Place Graphviz in `Graphviz-14.0.5-win32/bin/` directory
- Or install system-wide and update path in source code
- Download link available in `Graphviz-14.0.5-win32--link.txt`

## Integration with Other Projects

The generated files in `../built_src/` are used by:
- `cw_sp2__2025_2026` - Main compiler (lexical analysis)
- Other verification tools in the solution

## Testing the Setup

1. **Build the project**:
   ```bash
   cmake --build build --target dfa_generator__2025
   ```

2. **Run the executable**:
   ```bash
   cd dfa_generator__2025
   ../build/bin/dfa_generator__2025
   ```

3. **Verify output**:
   - Check that `../built_src/file*.hpp` files are created
   - Check that `../built_doc/` contains `.dot` files
   - If Graphviz is available, check for `.svg` and `.pdf` files

## Troubleshooting

### Build Errors

**Problem**: Cannot find `../built_src/file1.hpp` etc.

**Solution**: The files don't exist yet! You need to run `dfa_generator__2025` first to generate them. The build process for other projects expects these files to exist.

**Recommended order**:
1. Build and run `dfa_generator__2025` first
2. Then build other projects that depend on the generated files

### Runtime Errors

**Problem**: Program cannot create output files

**Solution**: Ensure you're running from the correct directory:
```bash
# Correct
cd dfa_generator__2025
../build/bin/dfa_generator__2025

# Incorrect
./build/bin/dfa_generator__2025  # Wrong working directory!
```

### Graphviz Not Found

**Problem**: Diagram files (.svg, .pdf) are not generated

**Solution**: 
1. Download Graphviz from the link in `Graphviz-14.0.5-win32--link.txt`
2. Extract to `dfa_generator__2025/Graphviz-14.0.5-win32/`
3. Re-run the program

## Migration Benefits

? **Visual Studio Support**: Full integration with VS 2019/2022  
? **VSCode Support**: Complete debugging and build support  
? **Cross-Platform**: Works on Windows, Linux, and macOS  
? **Modern Build System**: Uses industry-standard CMake  
? **Consistent Configuration**: Centralized build settings  
? **Better IDE Integration**: Proper IntelliSense and debugging  
? **Automated Setup**: Directories created automatically  
? **Build Presets**: Easy switching between configurations  

## Next Steps

1. **Try it out**: Build and run the project following the instructions above
2. **Explore**: Check the generated files in `../built_src/` and `../built_doc/`
3. **Customize**: Modify the regular expressions in the source code if needed
4. **Integrate**: Use the generated transition tables in your other projects

## Additional Resources

- **Project README**: `dfa_generator__2025/README.md`
- **General Build Instructions**: `BUILD_INSTRUCTIONS.md`
- **Quick Start Guide**: `QUICK_START.md`
- **CMake Documentation**: https://cmake.org/documentation/
- **Visual Studio CMake**: https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio
- **VSCode CMake Tools**: https://github.com/microsoft/vscode-cmake-tools

---

**Migration completed by**: GitHub Copilot  
**Date**: 2025  
**Status**: ? Ready for use in Visual Studio and VSCode
