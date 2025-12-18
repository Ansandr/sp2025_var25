# DFA Generator 2025 - Setup Checklist

Use this checklist to verify your development environment is properly configured.

## ? Prerequisites Check

### Required Software

- [ ] **CMake 3.15+** installed and in PATH

  ```bash
  cmake --version  # Should show 3.15 or higher
  ```

- [ ] **C++ Compiler** with C++17 support:
  - **Windows**:
    - [ ] Visual Studio 2019 or 2022 with C++ workload
    - [ ] OR MinGW-w64 (GCC 7+)
  - **Linux**:
    - [ ] GCC 7+ or Clang 5+

    ```bash
    g++ --version  # or clang++ --version
    ```

  - **macOS**:

    - [ ] Xcode Command Line Tools

    ```bash
    xcode-select --version
    ```

### Optional Software

- Download from link in `Graphviz-14.0.5-win32--link.txt`
- Extract to `dfa_generator__2025/Graphviz-14.0.5-win32/`

### IDE Setup

#### For Visual Studio Users

- [ ] Visual Studio 2019 or 2022 installed
- [ ] C++ CMake tools component installed
  - Open Visual Studio Installer ? Modify ? Individual Components
  - Check "C++ CMake tools for Windows"

#### For VSCode Users

- [+] VSCode installed
- [+] "C/C++" by Microsoft
- [+] "CMake Tools" by Microsoft

## ? Project Structure Check

Verify these directories and files exist:

```text
Repository Root/
├── CMakeLists.txt                    [+] Main CMake file
├── CMakePresets.json                 [+] Build presets
├── BUILD_INSTRUCTIONS.md             [+] Build guide
├── QUICK_START.md                    [+] Quick start
├── README.md                         [+] Project overview
│
├── .vscode/
│   ├── launch.json                   [+] Debug configs
│   ├── settings.json                 [+] VSCode settings
│   └── tasks.json                    [+] Build tasks
│
├── dfa_generator__2025/
│   ├── CMakeLists.txt                [+] Project CMake
│   ├── README.md                     [+] Project docs
│   ├── CMAKE_MIGRATION.md            [+] Migration guide
│   ├── dfa_generator___part_impl.cpp [+] Source code
│   └── Graphviz-14.0.5-win32--link.txt [+] Graphviz link
│
├── built_src/                        [ ] Will be created by build
└── built_doc/                        [ ] Will be created by build
```

## ? Build Configuration

### Visual Studio

#### Method 1: CMake Project (Recommended)

1. [ ] Open Visual Studio
2. [ ] File ? Open ? Folder...
3. [ ] Select repository root directory
4. [ ] Wait for "CMake generation finished" in Output window
5. [ ] Verify configurations appear in toolbar: `x64-Debug`, `x64-Release`

#### Method 2: Generate Solution

1. [ ] Open Developer Command Prompt for VS
2. [ ] Navigate to repository root
3. [ ] Run: `cmake --preset vs2022` (or `vs2019`)
4. [ ] Check: `build/vs2022/cw_sp2__2024_2025.sln` created
5. [ ] Open the solution in Visual Studio

### VSCode

1. [+] Open repository root in VSCode
2. [+] CMake Tools should detect project automatically
3. [ ] Status bar shows: [CMake: dfa_generator__2025] or similar
4. [ ] Ctrl+Shift+P ? "CMake: Select a Kit"
5. [ ] Choose your compiler (Visual Studio, GCC, or Clang)
6. [ ] Ctrl+Shift+P ? "CMake: Configure"
7. [ ] Check Output panel for "Build files have been written to..."

### Command Line

1. [ ] Open terminal in repository root
2. [ ] Run: `cmake -B build`
3. [ ] Verify no errors in output
4. [ ] Check: `build/` directory created with build files

## Build Test

### Build the Project

**Visual Studio:**

1. [ ] Select `dfa_generator__2025` in Solution Explorer
2. [ ] Build ? Build dfa_generator__2025 (or Ctrl+B)
3. [ ] Check Output window for "Build succeeded"
4. [ ] Verify: `out/build/x64-Debug/bin/dfa_generator__2025.exe` exists

**VSCode:**

1. [ ] Press F7 or click [Build] in status bar
2. [ ] Check Output ? Build for success message
3. [ ] Verify: `build/bin/dfa_generator__2025.exe` (or `.out` on Linux/Mac) exists

**Command Line:**

```bash
cmake --build build --target dfa_generator__2025
```

1. [ ] No errors in output
2. [ ] Verify: `build/bin/dfa_generator__2025[.exe]` exists

## ? Run Test

### Execute the Program

**Important**: Must run from the project directory!

**Windows:**

```powershell
cd dfa_generator__2025
..\build\bin\dfa_generator__2025.exe
```

**Linux/macOS:**

```bash
cd dfa_generator__2025
../build/bin/dfa_generator__2025
```

### Verify Output

After running, check these were created:

**Generated Source Files:**

- [ ] `../built_src/file1.hpp` - Tokens transition table
- [ ] `../built_src/file1.txt` - Tokens readable format
- [ ] `../built_src/file2.hpp` - Keywords transition table
- [ ] `../built_src/file2.txt` - Keywords readable format
- [ ] `../built_src/file3.hpp` - Identifiers transition table
- [ ] `../built_src/file3.txt` - Identifiers readable format
- [ ] `../built_src/file4.hpp` - Unsigned values transition table
- [ ] `../built_src/file4.txt` - Unsigned values readable format

**Generated Documentation (Partial DFA):**

- [ ] `../built_doc/fsm1.dot` - GraphViz source
- [ ] `../built_doc/fsm1.svg` - SVG diagram (if Graphviz available)
- [ ] `../built_doc/fsm1.pdf` - PDF diagram (if Graphviz available)
- [ ] Same for fsm2, fsm3, fsm4

**Generated Documentation (Full DFA):**

- [ ] `../built_doc/full_dfa/fsm1__full_dfa.dot`
- [ ] `../built_doc/full_dfa/fsm1__full_dfa.svg` (if Graphviz available)
- [ ] `../built_doc/full_dfa/fsm1__full_dfa.pdf` (if Graphviz available)
- [ ] Same for fsm2, fsm3, fsm4

**Console Output:**

- [ ] "Transitions (transitionTableX):" printed
- [ ] "Finit states (transitionTableX):" printed
- [ ] "Dead state (transitionTableX):" printed
- [ ] "NEW:" section showing minimized states
- [ ] Final progress messages showing completion

## ? Debug Test

### Visual Studio Debugging

1. [ ] Right-click `dfa_generator__2025` ? Set as Startup Project
2. [ ] Set breakpoint in `main()` function (line ~675)
3. [ ] Press F5 or Debug ? Start Debugging
4. [ ] Verify breakpoint is hit
5. [ ] Check Watch window: Variables are accessible
6. [ ] Check Autos window: Current scope variables shown
7. [ ] Continue execution (F5) and verify program completes

### VSCode Debugging

1. [ ] Open `dfa_generator___part_impl.cpp`
2. [ ] Set breakpoint on line `int main()` (line ~675)
3. [ ] Press F5 or Run ? Start Debugging
4. [ ] Select "(Windows) Launch dfa_generator" config
5. [ ] Verify breakpoint is hit
6. [ ] Check Variables panel: Local variables shown
7. [ ] Check Debug Console: GDB/LLDB messages appear
8. [ ] Continue (F5) and verify program completes

### Working Directory

**Visual Studio:**

- [ ] Right-click `dfa_generator__2025` ? Properties
- [ ] Configuration Properties ? Debugging
- [ ] Check "Working Directory" ends with `\dfa_generator__2025`

**VSCode:**

- [ ] Open `.vscode/launch.json`
- [ ] Find "(Windows) Launch dfa_generator" configuration
- [ ] Verify: `"cwd": "${workspaceFolder}/dfa_generator__2025"`

## Need Help?

Consult these resources:

1. `README.md` - Project-specific documentation
2. `CMAKE_MIGRATION.md` - Migration details and usage
3. `BUILD_INSTRUCTIONS.md` - Comprehensive build guide
4. `QUICK_START.md` - Quick reference for common tasks

**Setup Status**: [ ] Complete ?

*Once all checkboxes are marked, you're ready to develop and use the DFA Generator!*
