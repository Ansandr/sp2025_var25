# Quick Start Guide

## For Visual Studio Users

### Method 1: Open as CMake Project (Recommended - VS 2019+)
1. Launch Visual Studio 2019 or later
2. Click `File` ? `Open` ? `Folder...`
3. Select the root project folder (containing `CMakeLists.txt`)
4. Wait for CMake to configure automatically (see Output window)
5. Select build configuration from toolbar: `x64-Debug` or `x64-Release`
6. Press `F7` or `Ctrl+Shift+B` to build
7. Run executables from `out/build/x64-Debug/bin/` or `out/build/x64-Release/bin/`

### Method 2: Generate .sln File
```powershell
# Open Developer Command Prompt for VS 2019
# Navigate to project root, then:

mkdir build-vs
cd build-vs
cmake .. -G "Visual Studio 16 2019" -A x64
# This creates cw_sp2__2024_2025.sln

# Open the solution
start cw_sp2__2024_2025.sln
```

**Setting Startup Project:**
- Right-click on desired project (e.g., `cw_sp2__2025_2026`)
- Select `Set as Startup Project`
- Press `F5` to debug or `Ctrl+F5` to run without debugging

---

## For VSCode Users

### Initial Setup
1. **Install Required Extensions:**
   - Open VSCode
   - Press `Ctrl+Shift+X` to open Extensions
   - Install:
     - `C/C++` by Microsoft
     - `CMake Tools` by Microsoft
     - `CMake` by twxs (optional, for syntax highlighting)

2. **Open Project:**
   - Launch VSCode
   - Click `File` ? `Open Folder...`
   - Select the root project folder
   - VSCode will detect CMake automatically

### Building

**First Time Setup:**
1. Press `Ctrl+Shift+P` to open Command Palette
2. Type and select: `CMake: Select a Kit`
3. Choose your compiler:
   - **Windows**: Visual Studio Build Tools or GCC/MinGW
   - **Linux**: GCC or Clang
   - **macOS**: Clang

**Configure and Build:**
```
Ctrl+Shift+P ? "CMake: Configure"  (First time only)
F7           ? Build all
Shift+F7     ? Clean and rebuild
```

**Or use the status bar:**
- Click on `[Build]` button in the bottom status bar

### Running and Debugging

**Run without debugging:**
1. After building, executables are in `build/bin/`
2. Open integrated terminal: `` Ctrl+` ``
3. Run: `./build/bin/cw_sp2__2025_2026` (Linux/Mac) or `.\build\bin\cw_sp2__2025_2026.exe` (Windows)

**Debug:**
1. Open a source file from the project you want to debug
2. Set breakpoints by clicking left of line numbers
3. Press `F5` or click `Run` ? `Start Debugging`
4. Select the appropriate launch configuration (Windows or Linux/macOS)

### Useful VSCode Shortcuts
- `Ctrl+Shift+P` - Command Palette
- `F7` - Build
- `F5` - Start Debugging
- `Ctrl+F5` - Run Without Debugging
- `` Ctrl+` `` - Toggle Terminal
- `Ctrl+Shift+B` - Run Build Task

### Changing Build Configuration
1. Click on build variant in status bar (bottom)
2. Select: `Debug`, `Release`, `RelWithDebInfo`, or `MinSizeRel`

---

## Common Operations

### Build Single Project
**Visual Studio:**
- Right-click project in Solution Explorer ? `Build`

**VSCode:**
```bash
# In terminal
cmake --build build --target dfa_generator__2025
```

### Clean Build
**Visual Studio:**
- `Build` ? `Clean Solution`

**VSCode:**
```bash
# In terminal
cmake --build build --target clean
# Or delete build directory
rm -rf build  # Linux/Mac
rmdir /s build  # Windows CMD
```

### Rebuild Everything
**Visual Studio:**
- `Build` ? `Rebuild Solution`

**VSCode:**
```bash
# Clean and build
cmake --build build --clean-first
```

---

## Project Executables

After building, you'll find these executables in `build/bin/` (VSCode) or `out/build/x64-Debug/bin/` (Visual Studio):

- `cw_sp2__2025_2026` - Main compiler
- `dfa_generator__2025` - DFA generator
- `verify_syntax_by_EBNF__2025` - Syntax verifier
- `verify_syntax_by_EBNF_nonpacked__2025` - Alternative syntax verifier
- `wrapWithInOutPipe` - I/O wrapper
- `image_pattern_generator` - Pattern generator
- `assembly_pattern` - Assembly pattern (Windows only)
- `dpda1_for_ll2_generator__2025` - LL(2) parser generator

---

## Troubleshooting

### VSCode: "CMake Tools is not configured"
- Press `Ctrl+Shift+P` ? `CMake: Select a Kit`
- Choose your compiler

### VSCode: Build fails with "Generator not found"
- Install Ninja: `choco install ninja` (Windows) or `apt install ninja-build` (Linux)
- Or use different generator in `.vscode/settings.json`: change `"cmake.generator": "Ninja"` to `"cmake.generator": "Unix Makefiles"` (Linux) or remove the line (auto-detect)

### Visual Studio: CMake configuration fails
- Make sure you have "C++ CMake tools for Windows" installed
- Go to Visual Studio Installer ? Modify ? Individual Components
- Check "C++ CMake tools for Windows"

### Permission denied when running executable
**Linux/macOS:**
```bash
chmod +x build/bin/*
```

---

## Additional Resources

- Full build instructions: See [BUILD_INSTRUCTIONS.md](BUILD_INSTRUCTIONS.md)
- CMake documentation: https://cmake.org/documentation/
- Visual Studio CMake: https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio
- VSCode CMake Tools: https://github.com/microsoft/vscode-cmake-tools
