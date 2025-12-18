# DFA Generator 2025

This project generates Deterministic Finite Automaton (DFA) transition tables from regular expressions represented in a custom notation.

## Overview

The DFA generator takes regular expressions and converts them into transition tables that can be used for pattern matching and lexical analysis. It supports:

- Custom regular expression notation with special operators
- Epsilon transitions
- DFA minimization (optional)
- Multiple output formats (header files, text files, visual diagrams)
- Generation of both full DFA and partial DFA (without dead states)

## Building with CMake

### Prerequisites

- CMake 3.15 or higher
- C++17 compatible compiler
- Optional: Graphviz for generating visual diagrams (should be in `Graphviz-14.0.5-win32/bin/` directory)

### Build Instructions

#### Using Visual Studio 2019+

1. Open the parent directory in Visual Studio
2. Visual Studio will automatically detect and configure CMake
3. Select the `dfa_generator__2025` target
4. Build using `Ctrl+Shift+B`

#### Using VSCode

1. Open the parent directory in VSCode
2. Install the CMake Tools extension
3. Press `Ctrl+Shift+P` and select "CMake: Configure"
4. Press `F7` to build
5. Use the debug configuration "(Windows) Launch dfa_generator" to run

#### Command Line

```bash
# From the parent directory
mkdir build && cd build
cmake ..
cmake --build . --target dfa_generator__2025

# The executable will be in build/bin/dfa_generator__2025.exe (or .out on Linux/macOS)
```

### Using CMake Presets

The project supports CMake presets for easier configuration:

```bash
# Configure with Visual Studio 2022
cmake --preset vs2022

# Build
cmake --build --preset vs2022

# Or configure with Ninja and Debug mode
cmake --preset debug
cmake --build --preset debug
```

## Project Structure

```
dfa_generator__2025/
├── CMakeLists.txt                    # CMake build configuration
├── README.md                         # This file
├── dfa_generator___part_impl.cpp    # Main implementation
├── Graphviz-14.0.5-win32--link.txt  # Link to Graphviz download
└── (generated files)                 # Created after first run
    ├── ../built_src/                # Generated header files
    │   ├── file1.hpp                # Transition table 1
    │   ├── file2.hpp                # Transition table 2
    │   ├── file3.hpp                # Transition table 3
    │   └── file4.hpp                # Transition table 4
    └── ../built_doc/                # Generated documentation
        ├── fsm1.dot, .svg, .pdf     # FSM visualizations
        ├── fsm2.dot, .svg, .pdf
        ├── fsm3.dot, .svg, .pdf
        ├── fsm4.dot, .svg, .pdf
        └── full_dfa/                # Full DFA diagrams
            └── fsm*.dot, .svg, .pdf
```

## Regular Expression Notation

The generator uses a custom notation for regular expressions:

- `|` - Alternation (OR)
- `~` - Kleene star (zero or more)
- `^` - Optional (zero or one)
- `(` `)` - Grouping
- `\\` - Escape character for special symbols
- Double characters (`((`, `))`, `||`, `~~`, `^^`) - Literal representation

### Examples

```cpp
// Token recognition
TOKENS_RN: ";|:(^|=)|=(:|=)|+|-|*|,|!=|[|]|(((|)))|{|}|<=|>=|..."

// Keyword recognition
KEYWORDS_RN: ";|:(^|=)|=(:|=)|+|-|*|...|N(AME|OT)|D(ATA|O(^|WNTO)|IV)|..."

// Identifier recognition (7 uppercase letters after underscore)
IDENTIFIERS_RN: "_[A-Z][A-Z][A-Z][A-Z][A-Z][A-Z][A-Z]"

// Unsigned integer recognition
UNSIGNEDVALUES_RN: "0|[1-9][0-9]*"
```

## Generated Output

The generator creates:

1. **Header Files** (`../built_src/file*.hpp`):
   - Transition table arrays
   - State definitions
   - Final state arrays

2. **Text Files** (`../built_src/file*.txt`):
   - Human-readable transition tables

3. **Visualization Files** (if Graphviz is available):
   - `.dot` - GraphViz source files
   - `.svg` - Scalable vector graphics
   - `.pdf` - PDF diagrams

## Configuration

### Working Directory

The CMake configuration ensures the working directory is set correctly:

- **Visual Studio**: Set via `VS_DEBUGGER_WORKING_DIRECTORY`
- **VSCode**: Set in `.vscode/launch.json` via the `cwd` property

### Output Directories

The program expects to write to:

- `../built_src/` - For generated source files
- `../built_doc/` - For documentation and diagrams
- `../built_doc/full_dfa/` - For full DFA diagrams

These directories are automatically created by the CMake build process.

## DFA Minimization

The generator includes an optional DFA minimization step controlled by the `USE_DFA_MINIMIZATION` preprocessor definition. This is enabled by default in the CMake configuration.

To disable minimization:

```cmake
# In CMakeLists.txt, remove or comment out:
# target_compile_definitions(dfa_generator__2025 PRIVATE USE_DFA_MINIMIZATION)
```

## Running the Program

After building, run the executable from the project directory:

```bash
# Windows
cd dfa_generator__2025
..\build\bin\dfa_generator__2025.exe

# Linux/macOS
cd dfa_generator__2025
../build/bin/dfa_generator__2025
```

The program will:

1. Generate transition tables for all four FSMs
2. Create header files in `../built_src/`
3. Create visualization files in `../built_doc/`
4. Print progress to the console

## Debugging in Visual Studio

1. Set `dfa_generator__2025` as the startup project
2. The working directory is automatically set to the project source directory
3. Press `F5` to start debugging

## Debugging in VSCode

1. Select the "(Windows) Launch dfa_generator" or "(Linux/macOS) Launch dfa_generator" configuration
2. Press `F5` to start debugging
3. The `cwd` is automatically set to the project source directory

## Notes

- The program is designed to run from its source directory
- Generated files are placed in parent directory locations
- The transition tables use a row-major format: `table[symbol][state]`
- State numbering starts from Q000
- The dead state is typically the last state in the full DFA

## Specifying Custom Languages

To define your own language patterns, modify the regex definitions in `dfa_generator___part_impl.cpp`:

### Step 1: Define Your Regular Expression

Add your pattern using the custom notation. For example:

```cpp
// Define a pattern for programming language tokens
#define CUSTOM_TOKENS_RN    "("\
    "=|+|-|*|/|%|"\
    "(((|)))|{|}|;|,|"\
    "[|]|:=|==|!=|<|>|<=|>=|"\
    "~"        /* Kleene star: zero or more */ \
    "^|"       /* Optional: zero or one */ \
    "and|or|not|"\
    "[_A-Za-z][_A-Za-z0-9]*"  /* Identifiers */ \
")"

#define CUSTOM_KEYWORDS_RN  "("\
    "if|then|else|endif|"\
    "while|do|endwhile|"\
    "for|to|endfor|"\
    "function|return|"\
    "var|const|type"\
")"
```

### Step 2: Create Include Files

Create header files to hold your generated tables:

```bash
# Create placeholder headers that will be filled by the generator
touch ../built_src/custom_tokens.hpp
touch ../built_src/custom_keywords.hpp
```

### Step 3: Reference in dfa_generator__part_impl.cpp

Add includes and macros for your new tables:

```cpp
#include "../built_src/custom_tokens.hpp"
#define CUSTOM_TOKENS_PATH "../built_doc/custom_tokens"
#define CUSTOM_TOKENS_FILE_A "../built_src/custom_tokens.hpp"
#define CUSTOM_TOKENS_FILE_B "../built_src/custom_tokens.txt"
#define CUSTOM_TOKENS_TABLE "customTokensTable"
#define RN_CUSTOM CUSTOM_TOKENS_RN

// ... (repeat for keywords, identifiers, values as needed)
```

### Step 4: Add Processing in main()

```cpp
int main() {
#ifndef PRINT_ALTERNATION_SYMBOL
    // Existing code...
    
    // Add your custom language
    transition_count = 0;
    finit_states_count = 0;
    generatorB((char*)RN_CUSTOM, 
               (char*)CUSTOM_TOKENS_FILE_A, 
               (char*)CUSTOM_TOKENS_FILE_B, 
               (char*)CUSTOM_TOKENS_TABLE);
    
    // ... repeat for other custom patterns
    
    return buildAllFSMs();
#endif
}
```

### Step 5: Rebuild

```bash
# From repository root
cmake --build build --target dfa_generator__2025
cd dfa_generator__2025
..\build\bin\dfa_generator__2025.exe
```

### Custom Regex Notation Guide

| Operator | Meaning | Example | Matches |
|----------|---------|---------|---------|
| `\|` | Alternation (OR) | `a\|b` | "a" or "b" |
| `~` | Kleene star (0 or more) | `a~` | "", "a", "aa", "aaa", ... |
| `^` | Optional (0 or 1) | `a^` | "" or "a" |
| `()` | Grouping | `(a\|b)c` | "ac" or "bc" |
| `\\` | Escape character | `\\(` | Literal "(" |
| `((`, `))`, `\|\|`, `~~`, `^^` | Literal operators | `((\|))` | Literal "(\|)" |
| `[]` | Character class | `[a-z]` | Any lowercase letter |
| `-` | Range in class | `[0-9A-F]` | Hex digit |

### Practical Examples

#### Simple Calculator Language

```cpp
#define CALC_TOKENS_RN  "("\
    "+|-|~|\\*|/|%|"\                  /* Operators */\
    "(((|)))|"\                        /* Parentheses */\
    "[0-9]~"                           /* Numbers (0 or more digits) */\
")"
```

#### JSON-like Format

```cpp
#define JSON_TOKENS_RN  "("\
    "{|}|\\[|\\]|:|,|"\                /* Structural chars */\
    "true|false|null|"\                /* Keywords */\
    "\"[^\"]*\"~"                      /* Strings */\
")"
```

#### Custom Identifier Rules

```cpp
// Identifiers: uppercase letter, followed by 0-6 uppercase letters, underscore, or digits
#define CUSTOM_ID_RN    "("\
    "[A-Z]|"\                          /* Uppercase letter */\
    "[A-Z0-9_]~"                       /* Optional: upper, digit, or underscore */\
")"
```

### Debugging Your Regular Expression

To debug your regex pattern, uncomment `#define PRINT_ALTERNATION_SYMBOL` in `main()` and modify the test string. This will print all symbols NOT in your exclusion set, helping verify your pattern matches the intended alphabet.

```cpp
#define PRINT_ALTERNATION_SYMBOL
int main() {
    // This will print available symbols for your language
    printAlternationSymbol((char*)"your_excluded_symbols");
}
```

### Limitations and Considerations

- **Maximum states**: Limited to 1024 states (configurable via `MAX_STATES`)
- **Symbol range**: Only supports symbols 0-255 (single-byte ASCII and extended ASCII)
- **Regex complexity**: Very complex nested patterns may generate large NFAs
- **Performance**: Use DFA minimization to keep generated tables manageable
- **Binary compatibility**: Generated header files are C++ but can be used from C with minor modifications

### Verifying Generated Output

After generating custom tables, verify correctness:

1. **Check header files** (`built_src/*.hpp`):
   - Look for well-formed transition tables
   - Verify final states array contains expected states

2. **Review text files** (`built_src/*.txt`):
   - Human-readable transition tables for manual inspection

3. **Inspect diagrams** (`built_doc/*.dot`):
   - Open GraphViz files to visualize the automaton
   - Check that the state graph makes sense

4. **Test integration**:
   - Use generated tables in your lexical analyzer
   - Verify correct token recognition

## How dfa_generator__part_impl.cpp Works

The DFA generator processes custom regular expression notation to build transition tables. Here's the workflow:

### Architecture

1. **Language Specification**
   - Four language patterns are defined using the custom regex notation (lines 400-560):
     - `TOKENS_RN` - Token patterns (operators, delimiters)
     - `KEYWORDS_RN` - Reserved keywords
     - `IDENTIFIERS_RN` - Identifier patterns
     - `UNSIGNEDVALUES_RN` - Numeric value patterns

2. **NFA Construction** (`process_term()`, `process_alternation()`)
   - The regex parser builds an NFA by recursively processing the pattern string
   - Handles operators: `|` (alternation), `~` (Kleene star), `^` (optional)
   - Escaped operators use double characters: `((`, `))`, `||`, `~~`, `^^`
   - Transitions array stores state-to-state relationships with symbols

3. **DFA Conversion** (`generate_transition_table()`)
   - Applies epsilon closure to convert NFA to DFA
   - Builds transition table indexed by `[symbol][state]`
   - All 256 possible symbols are supported

4. **DFA Minimization** (optional, `removing_unreachable_DFA_states()`)
   - Removes unreachable states not connected from start state
   - Renames states sequentially
   - Enabled by `USE_DFA_MINIMIZATION` define

5. **Output Generation**
   - Generates C++ header files with transition table arrays
   - Creates human-readable text representations
   - Builds GraphViz `.dot` files for visualization
   - Optionally converts to SVG and PDF diagrams

### Key Structures

```cpp
// NFA transition: "from state --[symbol]--> to state"
struct Transition {
    int from;           // From state
    int to;             // To state
    int symbolCode;     // ASCII value of symbol (-1 = epsilon)
};

// Global arrays holding the NFA
Transition transitions[1024];        // All NFA transitions
int finit_states[1024];              // Final/accepting states
int transition_table[MAX_STATES][SYMBOL_NUMBER];  // Final DFA table
```

### Main Processing Flow

```cpp
main() {
    for (each of 4 languages) {
        transition_count = 0;           // Reset NFA
        finit_states_count = 0;
        generatorB(regex, outputFile1, outputFile2, tableName);
        // generatorB():
        //   1. process_alternation() -> parses regex -> builds NFA
        //   2. removing_unreachable_DFA_states() -> minimizes NFA
        //   3. generate_transition_table() -> converts to DFA table
        //   4. print_transition_table_to_file() -> writes output
    }
    buildAllFSMs();                     // Generate visualizations
}
```
