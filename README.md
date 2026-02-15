# C Compiler Front-End

A comprehensive C compiler front-end implementation built using **Flex** (lexical analyzer) and **Bison/Yacc** (parser generator). This project implements the first three phases of a compiler: **Lexical Analysis**, **Syntax Analysis**, and **Semantic Analysis** with symbol table management and error detection.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Language Features](#language-features)
- [Error Detection](#error-detection)
- [Output Files](#output-files)
- [Project Architecture](#project-architecture)
- [Examples](#examples)
- [Contributing](#contributing)

## 🎯 Overview

This compiler front-end processes C-like source code through multiple phases:

1. **Lexical Analysis**: Tokenizes the input source code into meaningful tokens (keywords, identifiers, operators, constants, etc.)
2. **Syntax Analysis**: Parses tokens according to a context-free grammar and builds a parse tree
3. **Semantic Analysis**: Performs type checking, scope management, and validates semantic rules

The compiler generates detailed logs of the compilation process and reports all detected errors in separate files.

## ✨ Features

### Lexical Analysis
- Token recognition for keywords, identifiers, operators, and constants
- Support for integer, float, and character literals
- String literal handling with escape sequence support
- Single-line (`//`) and multi-line (`/* */`) comment processing
- Comprehensive lexical error detection

### Syntax Analysis
- Context-free grammar implementation using Bison/Yacc
- Parse tree generation with grammar rule logging
- Support for complex expressions and statements

### Semantic Analysis
- **Symbol Table Management**: Hierarchical scope management using hash tables
- **Type Checking**: Validates type compatibility in expressions and assignments
- **Function Declaration/Definition Matching**: Ensures consistency between declarations and definitions
- **Parameter Validation**: Checks argument count and type matching
- **Array Handling**: Validates array declarations and indexing
- **Scope Resolution**: Proper variable and function lookup across scopes

### Error Detection
- Lexical errors (unrecognized characters, malformed numbers, etc.)
- Syntax errors (parse errors)
- Semantic errors (type mismatches, undeclared variables, etc.)

## 📁 Project Structure

```
C-compiler-Full/
├── My Codes/
│   ├── 1805051.l              # Flex lexical analyzer specification
│   ├── 1805051.y              # Bison/Yacc parser specification
│   ├── 1805051_SymbolInfo.h   # Symbol information class definition
│   ├── 1805051_ScopeTable.h   # Scope table (hash table) implementation
│   ├── 1805051_SymbolTable.h  # Symbol table (scope manager) implementation
│   ├── SymbolTable.cpp         # Symbol table includes
│   ├── input.c                # Sample input file
│   └── run1.sh                # Build and execution script
└── README.md                  # This file
```

## 🛠 Technologies Used

- **Flex**: Fast lexical analyzer generator
- **Bison/Yacc**: Parser generator
- **C++**: Implementation language
- **GNU Compiler Collection (GCC)**: Compilation toolchain

## 📦 Prerequisites

Before building and running the compiler, ensure you have the following installed:

- **Flex** (Fast Lexical Analyzer)
  ```bash
  # Ubuntu/Debian
  sudo apt-get install flex
  
  # macOS
  brew install flex
  
  # Windows (using MinGW or WSL)
  # Install through package manager
  ```

- **Bison** (Parser Generator)
  ```bash
  # Ubuntu/Debian
  sudo apt-get install bison
  
  # macOS
  brew install bison
  
  # Windows (using MinGW or WSL)
  # Install through package manager
  ```

- **GCC/G++** (C++ Compiler)
  ```bash
  # Ubuntu/Debian
  sudo apt-get install g++

  # macOS
  # Usually pre-installed, or install via Xcode Command Line Tools
  ```

## 🚀 Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd C-compiler-Full
   ```

2. **Navigate to the source directory**:
   ```bash
   cd "My Codes"
   ```

3. **Make the build script executable** (Linux/macOS):
   ```bash
   chmod +x run1.sh
   ```

## 💻 Usage

### Building the Compiler

**Option 1: Using the provided script** (Linux/macOS):
```bash
./run1.sh
```

**Option 2: Manual build**:
```bash
# Compile C++ source files
g++ -w -c *.cpp

# Generate parser from Yacc file
yacc -d -y 1805051.y
g++ -w -c -o y.o y.tab.c

# Generate scanner from Flex file
flex 1805051.l
g++ -w -c -o l.o lex.yy.c

# Link all object files
g++ -w y.o l.o -lfl -o 1805051
```

**Note for Windows users**: You may need to use `g++ -fpermissive -w -c -o l.o lex.yy.c` instead of the standard command if you encounter compilation errors.

### Running the Compiler

```bash
./1805051 <input_file>
```

Example:
```bash
./1805051 input.c
```

### Input File Format

The compiler accepts C-like source code files. See `input.c` for an example.

## 🔤 Language Features

### Supported Keywords
- Data types: `int`, `char`, `float`, `double`, `void`
- Control flow: `if`, `else`, `for`, `while`, `do`, `switch`, `case`, `default`
- Functions: `return`
- Other: `break`, `continue`

### Operators
- **Arithmetic**: `+`, `-`, `*`, `/`, `%`
- **Relational**: `<`, `>`, `<=`, `>=`, `==`, `!=`
- **Logical**: `&&`, `||`, `!`
- **Increment/Decrement**: `++`, `--`
- **Assignment**: `=`

### Data Types
- **Integers**: `int` (e.g., `42`, `-10`)
- **Floating Point**: `float` (e.g., `3.14`, `2.5E10`)
- **Characters**: `char` (e.g., `'a'`, `'\n'`)
- **Arrays**: One-dimensional arrays (e.g., `int arr[10]`)
- **Functions**: Function declarations and definitions

### Statements
- Variable declarations
- Function declarations and definitions
- Expression statements
- Control flow statements (`if-else`, `for`, `while`)
- Return statements
- Print statements (`printf`)

### Expressions
- Arithmetic expressions with proper operator precedence
- Relational and logical expressions
- Function calls
- Array indexing
- Unary operations

## ⚠️ Error Detection

The compiler detects and reports various types of errors:

### Lexical Errors
- **Unrecognized characters**: Invalid characters in source code
- **Too many decimal points**: Malformed floating-point numbers (e.g., `3.14.5`)
- **Ill-formed numbers**: Invalid number formats
- **Unterminated strings**: Strings not properly closed
- **Unterminated comments**: Multi-line comments not closed
- **Multi-character constants**: Invalid character literals
- **Empty character constants**: Empty `''` literals
- **Unterminated characters**: Invalid character literal formats

### Semantic Errors
- **Undeclared variables/functions**: Using identifiers before declaration
- **Multiple declarations**: Declaring the same identifier multiple times in the same scope
- **Type mismatches**: Incompatible types in assignments or expressions
- **Function declaration/definition mismatch**: Inconsistencies between function declarations and definitions
- **Parameter count mismatch**: Wrong number of arguments in function calls
- **Parameter type mismatch**: Incompatible argument types
- **Return type errors**: Returning incompatible types or returning values from void functions
- **Array type errors**: Using arrays as variables or vice versa
- **Void type errors**: Using void functions in expressions
- **Division/Modulus by zero**: Runtime error detection
- **Non-integer modulus operands**: Using non-integer types with `%` operator

## 📄 Output Files

After compilation, the compiler generates two output files:

1. **`1805051_log.txt`**: Comprehensive log file containing:
   - All recognized tokens
   - Grammar rule applications
   - Parse tree information
   - Symbol table dumps for each scope
   - Total line count
   - Total error count

2. **`1805051_error.txt`**: Error report file containing:
   - All detected errors with line numbers
   - Error descriptions
   - Only semantic and lexical errors (syntax errors are handled by the parser)

## 🏗 Project Architecture

### Lexical Analyzer (`1805051.l`)
- Defines token patterns using regular expressions
- Handles different states for strings and comments
- Creates `SymbolInfo` objects for tokens
- Reports lexical errors

### Parser (`1805051.y`)
- Defines context-free grammar rules
- Performs syntax analysis
- Implements semantic actions for:
  - Symbol table management
  - Type checking
  - Error detection
  - Scope management

### Symbol Table System

#### `SymbolInfo` Class
- Stores information about identifiers (variables, functions, arrays)
- Maintains name, type, data type, key type (variable/function/array)
- Stores function parameters and array sizes

#### `ScopeTable` Class
- Implements a hash table for symbol storage within a scope
- Uses SDBM hash function for indexing
- Supports chaining for collision resolution
- Maintains parent scope reference for hierarchical lookup

#### `SymbolTable` Class
- Manages multiple scope tables
- Implements scope entering/exiting
- Provides lookup functionality across all scopes
- Maintains scope hierarchy

## 📝 Examples

### Example 1: Simple Variable Declaration
```c
int x, y, z;
float a;
```

### Example 2: Function Declaration and Definition
```c
void foo();

int var(int a, int b) {
    return a + b;
}

void foo() {
    x = 2;
    y = x - 5;
}
```

### Example 3: Arrays and Expressions
```c
int main() {
    int a[2], c, i, j;
    float d;
    a[0] = 5;
    i = a[0] + a[1];
    j = 2 * 3 + (5 % 3 < 4 && 8) || 2;
    d = var(1, 2 * 3) + 3.5 * 2;
    return 0;
}
```

### Example 4: Control Flow
```c
int main() {
    int x = 5;
    if (x > 0) {
        x = x + 1;
    } else {
        x = x - 1;
    }
    
    while (x > 0) {
        x = x - 1;
    }
    
    for (int i = 0; i < 10; i++) {
        x = x + i;
    }
    
    return 0;
}
```

## 🔍 Understanding the Output

### Log File Structure
```
Line <line_number>: <grammar_rule>
<token_information>

ScopeTable # <scope_id>
<bucket_number> --> <symbol_name> : <symbol_type> ...

Total Lines: <count>
Total Errors: <count>
```

### Error File Structure
```
Error at line <line_number>: <error_description>
```

## 🐛 Troubleshooting

### Common Issues

1. **Flex/Bison not found**
   - Ensure Flex and Bison are installed and in your PATH
   - Verify installation: `flex --version` and `bison --version`

2. **Compilation errors with lex.yy.c**
   - Try: `g++ -fpermissive -w -c -o l.o lex.yy.c`

3. **Linker errors with `-lfl`**
   - On some systems, use `-ll` instead: `g++ -w y.o l.o -ll -o 1805051`

4. **Permission denied on script**
   - Make executable: `chmod +x run1.sh`

## 📚 Further Reading

- [Flex Manual](https://www.gnu.org/software/flex/manual/)
- [Bison Manual](https://www.gnu.org/software/bison/manual/)
- [Compiler Design Principles](https://en.wikipedia.org/wiki/Compiler)

## 👥 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 📄 License

This project is open source and available for educational purposes.

## 🙏 Acknowledgments

- Built as part of a compiler design course project
- Uses standard compiler construction techniques and tools

---

**Note**: This is a front-end compiler implementation focusing on lexical, syntax, and semantic analysis. It does not generate executable code but provides comprehensive analysis and error reporting for C-like source code.

