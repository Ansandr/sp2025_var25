# Visual Studio Configuration Guide for DFA Generator 2025

## Opening the Project

### Method 1: Open as CMake Project (Recommended for VS 2019+)

1. **Launch Visual Studio 2019 or 2022**

2. **Open the Folder**:
   - Click `File` ? `Open` ? `Folder...`
   - Navigate to the repository root directory (where the main `CMakeLists.txt` is located)
   - Click `Select Folder`

3. **Wait for CMake Configuration**:
   - Visual Studio will automatically detect CMake
   - Watch the **Output** window (View ? Output)
   - Look for "CMake generation finished" message
   - This may take 30-60 seconds on first run

4. **Verify Configuration**:
   - Toolbar should show configuration dropdown: `x64-Debug`, `x64-Release`, etc.
   - Solution Explorer shows project structure
   - All projects are listed under `CMake Targets View`

### Method 2: Generate and Open .sln File

If you prefer working with traditional Visual Studio solutions:

```powershell
# Open Developer Command Prompt for VS 2019 or 2022
# Navigate to repository root

# For Visual Studio 2022:
cmake --preset vs2022

# For Visual Studio 2019:
cmake --preset vs2019

# Open the generated solution
start build\vs2022\cw_sp2__2024_2025.sln
```

## Project Configuration

### Setting the Startup Project

When you open the folder, `dfa_generator__2025` is not automatically set as the startup project.

**To set it**:
1. In Solution Explorer, find `dfa_generator__2025` under CMake Targets
2. Right-click on `dfa_generator__2025.exe`
3. Select `Set as Startup Project`
4. The project name will appear bold

### Build Configurations

Visual Studio supports these configurations:

| Configuration | Description | Optimization | Debug Info |
|---------------|-------------|--------------|------------|
| **x64-Debug** | Debug build | None | Full |
| **x64-Release** | Release build | Maximum | None |
| **x64-RelWithDebInfo** | Optimized with debug info | Yes | Yes |
| **x64-MinSizeRel** | Size optimized | For size | Minimal |

**To switch**:
- Use the dropdown in the toolbar next to the run button
- Or: Build ? Configuration Manager

### Project Properties

**To view/edit** (for CMake projects):
1. Right-click `dfa_generator__2025` in Solution Explorer
2. Select `CMake Settings for dfa_generator__2025`
3. This opens `CMakeSettings.json` for editing

**Key settings** (already configured):
- **Working Directory**: `${projectDir}` (the dfa_generator__2025 folder)
- **Output Directory**: `${workspaceRoot}/out/build/${name}/bin`
- **Compiler Definitions**: `_CRT_SECURE_NO_WARNINGS`, `WIN32_LEAN_AND_MEAN`, `USE_DFA_MINIMIZATION`

## Building

### Build Single Project

**Option 1**: Using menu
1. In Solution Explorer, right-click `dfa_generator__2025`
2. Select `Build`

**Option 2**: Using keyboard
1. Select `dfa_generator__2025` in Solution Explorer
2. Press `Ctrl+B`

### Build Entire Solution

- Menu: `Build` ? `Build All` 
- Keyboard: `Ctrl+Shift+B`
- Toolbar: Click the build icon (hammer)

### Rebuild

To force a complete rebuild:
1. `Build` ? `Rebuild dfa_generator__2025`
2. Or right-click project ? `Rebuild`

### Clean

To remove build artifacts:
1. `Build` ? `Clean dfa_generator__2025`
2. Or right-click project ? `Clean`

**Note**: For CMake projects, cleaning removes the `out/build/` directory contents.

## Running and Debugging

### Run Without Debugging

**Method 1**: Menu
- `Debug` ? `Start Without Debugging`
- Keyboard: `Ctrl+F5`

**Method 2**: Toolbar
- Click the green arrow with "Local Debugger" label

**Method 3**: Solution Explorer
- Right-click `dfa_generator__2025.exe`
- Select `Debug` ? `Start Without Debugging`

### Run With Debugging

**Start Debugging**:
1. Set `dfa_generator__2025` as Startup Project (if not already)
2. Press `F5` or click `Debug` ? `Start Debugging`
3. Or click green arrow in toolbar

**Setting Breakpoints**:
1. Open `dfa_generator___part_impl.cpp`
2. Click in the left margin (gray area) next to a line number
3. A red dot appears indicating a breakpoint
4. When debugging, execution will pause at breakpoints

**Debug Windows** (available while debugging):
- **Autos** (Debug ? Windows ? Autos): Shows variables in current scope
- **Locals** (Debug ? Windows ? Locals): Shows all local variables
- **Watch** (Debug ? Windows ? Watch): Add expressions to watch
- **Call Stack** (Debug ? Windows ? Call Stack): Shows function call hierarchy
- **Breakpoints** (Debug ? Windows ? Breakpoints): Manage all breakpoints
- **Output** (View ? Output): Shows program output and debug messages

**Debug Controls**:
| Action | Keyboard | Description |
|--------|----------|-------------|
| **Start** | `F5` | Start debugging |
| **Stop** | `Shift+F5` | Stop debugging |
| **Restart** | `Ctrl+Shift+F5` | Restart debugging |
| **Continue** | `F5` | Continue execution |
| **Step Over** | `F10` | Execute next line |
| **Step Into** | `F11` | Step into function |
| **Step Out** | `Shift+F11` | Step out of function |
| **Run to Cursor** | `Ctrl+F10` | Run to cursor position |

## Working Directory Configuration

**Important**: The program must run from the `dfa_generator__2025` directory to access relative paths.

### Verify Working Directory

1. Right-click `dfa_generator__2025` in Solution Explorer
2. Select `Debug and Launch Settings`
3. This opens `launch.vs.json`
4. Verify or add:
   ```json
   {
     "type": "default",
     "project": "CMakeLists.txt",
     "projectTarget": "dfa_generator__2025.exe",
     "name": "dfa_generator__2025.exe",
     "currentDir": "${projectDir}"
   }
   ```

**Note**: `${projectDir}` resolves to `dfa_generator__2025/` directory.

### Custom Launch Configuration

If you need custom settings:

1. Create/edit `launch.vs.json` in the project directory
2. Add configuration:
   ```json
   {
     "version": "0.2.1",
     "defaults": {},
     "configurations": [
       {
         "type": "default",
         "project": "CMakeLists.txt",
         "projectTarget": "dfa_generator__2025.exe (dfa_generator__2025\\dfa_generator__2025.exe)",
         "name": "dfa_generator__2025.exe",
         "currentDir": "${projectDir}",
         "env": {
           "PATH": "${env.PATH};${projectDir}\\Graphviz-14.0.5-win32\\bin"
         }
       }
     ]
   }
   ```

## Output and Generated Files

### Build Output Location

After building, executables are placed in:

```
out/
??? build/
    ??? x64-Debug/          (or x64-Release, etc.)
        ??? bin/
            ??? dfa_generator__2025.exe
```

### Generated Files Location

When you run the program, files are generated in:

```
built_src/                  (parent directory of project)
??? file1.hpp
??? file1.txt
??? file2.hpp
??? file2.txt
??? file3.hpp
??? file3.txt
??? file4.hpp
??? file4.txt

built_doc/                  (parent directory of project)
??? fsm1.dot
??? fsm1.svg               (if Graphviz available)
??? fsm1.pdf               (if Graphviz available)
??? fsm2.dot, .svg, .pdf
??? fsm3.dot, .svg, .pdf
??? fsm4.dot, .svg, .pdf
??? full_dfa/
    ??? fsm*__full_dfa.*
```

## Output Window

The **Output** window shows various information:

**To open**: `View` ? `Output` or `Ctrl+Alt+O`

**Important channels**:
1. **Build**: Shows compilation progress and errors
2. **CMake**: Shows CMake configuration output
3. **Debug**: Shows debug messages and program output

**Tip**: Use the dropdown in Output window to switch between channels.

## IntelliSense and Code Navigation

### IntelliSense Configuration

Visual Studio automatically configures IntelliSense for CMake projects.

**Verify IntelliSense is working**:
- Hover over a variable ? Tooltip shows type
- Ctrl+Click on a function ? Jumps to definition
- Type a few characters ? Auto-complete suggestions appear

**If IntelliSense is not working**:
1. Wait for CMake configuration to complete
2. `Project` ? `Rescan Solution`
3. Close and reopen the solution

### Code Navigation Shortcuts

| Action | Keyboard | Description |
|--------|----------|-------------|
| **Go to Definition** | `F12` | Jump to definition |
| **Go to Declaration** | `Ctrl+F12` | Jump to declaration |
| **Find All References** | `Shift+F12` | Find all uses |
| **Go to Implementation** | `Ctrl+F12` | Go to implementation |
| **Navigate Backward** | `Ctrl+-` | Go back |
| **Navigate Forward** | `Ctrl+Shift+-` | Go forward |
| **Find in Files** | `Ctrl+Shift+F` | Search all files |
| **Go to Line** | `Ctrl+G` | Go to line number |

## CMake Integration

### CMake Menu

Visual Studio provides a CMake menu:
- **Build**: `Project` ? `CMake`
- **Cache**: View and edit CMake cache
- **Configure Cache**: Reconfigure CMake

### Viewing CMake Cache

1. `Project` ? `CMake` ? `Cache` ? `View Cache`
2. Shows `CMakeCache.txt` in editor

**Important cache entries**:
- `CMAKE_CXX_COMPILER`: C++ compiler path
- `CMAKE_BUILD_TYPE`: Current build type
- `CMAKE_CXX_STANDARD`: C++ standard (should be 17)

### Reconfiguring CMake

If you modify CMakeLists.txt:
1. `Project` ? `CMake` ? `Configure Cache`
2. Or save the CMakeLists.txt file (auto-reconfigure)

## Performance Tips

### Speed Up Build Times

1. **Use Ninja generator** (faster than MSBuild):
   - `Tools` ? `Options` ? `CMake`
   - Set `Generator` to `Ninja`

2. **Enable parallel builds**:
   - For MSBuild: Already enabled by default
   - For Ninja: Set in CMake settings

3. **Use precompiled headers** (already configured in CMakeLists.txt):
   - Automatically used for frequently included headers

### Reduce Solution Load Time

1. **Close unnecessary files**: Close files you're not editing
2. **Disable unnecessary features**: 
   - `Tools` ? `Options` ? `Text Editor` ? `C/C++`
   - Disable features you don't use

## Troubleshooting

### "Cannot find CMakeLists.txt"

**Problem**: Visual Studio doesn't detect CMake project

**Solution**:
1. Make sure you opened the **folder**, not a .sln file
2. CMakeLists.txt should be in the root folder
3. Try: `File` ? `Close Folder` ? `File` ? `Open` ? `Folder...`

### "CMake executable not found"

**Problem**: CMake is not installed or not in PATH

**Solution**:
1. Install CMake from https://cmake.org/download/
2. Or install via Visual Studio Installer:
   - Run Visual Studio Installer
   - Modify ? Individual Components
   - Check "C++ CMake tools for Windows"
3. Restart Visual Studio

### Build Errors "Cannot find file1.hpp"

**Problem**: Other projects depend on generated files

**Solution**:
1. Build and run `dfa_generator__2025` first
2. This generates the required header files
3. Then build other projects

### "Working directory is incorrect"

**Problem**: Program cannot find `../built_src/` or `../built_doc/`

**Solution**:
1. Verify debugging configuration uses `${projectDir}`
2. Check `launch.vs.json` for `"currentDir": "${projectDir}"`
3. If running from command line, `cd` to `dfa_generator__2025` first

### IntelliSense Shows Errors but Build Succeeds

**Problem**: IntelliSense is out of sync

**Solution**:
1. `Project` ? `Rescan Solution`
2. Or close and reopen Visual Studio
3. Delete `out/` directory and reconfigure

## Best Practices

### Recommended Workflow

1. **Start Visual Studio**
2. **Open the folder** (repository root)
3. **Wait for CMake** to finish configuring
4. **Set startup project** to `dfa_generator__2025`
5. **Build** the project (`Ctrl+Shift+B`)
6. **Debug** or run (`F5` or `Ctrl+F5`)

### Debugging Workflow

1. **Set breakpoints** in areas you want to inspect
2. **Start debugging** (`F5`)
3. **Use debug windows**:
   - Autos for current scope
   - Locals for all variables
   - Watch for specific expressions
4. **Step through code** (`F10`/`F11`)
5. **Inspect variables** by hovering or in watch windows

### Code Editing Tips

1. **Use IntelliSense**: Let auto-complete help you
2. **Navigate with F12**: Jump to definitions
3. **Use Find All References**: See where code is used (`Shift+F12`)
4. **Format code**: Select code ? `Edit` ? `Advanced` ? `Format Selection` (`Ctrl+K, Ctrl+F`)

## Additional Resources

### Visual Studio Documentation
- [CMake Projects in Visual Studio](https://docs.microsoft.com/en-us/cpp/build/cmake-projects-in-visual-studio)
- [Debugging in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/debugger/)

### Project Documentation
- `README.md` - Project overview and usage
- `CMAKE_MIGRATION.md` - CMake migration details
- `SETUP_CHECKLIST.md` - Setup verification checklist
- `BUILD_INSTRUCTIONS.md` - General build instructions

---

**Visual Studio Version**: 2019, 2022  
**Last Updated**: 2025  
**Status**: ? Complete CMake Integration
