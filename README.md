# Shift-Reduce Parser Using Stack

## 1. Project overview

This project implements a **bottom-up Shift-Reduce Parser** using **FLEX and C**. It accepts a context-free grammar (CFG) from the user, reads an input expression, converts the input into tokens using FLEX, and checks whether the token sequence can be reduced to the grammar's start symbol.

During parsing, the program displays a step-by-step table containing:

- **STEP** – the current parsing step.
- **STACK** – the current parser stack.
- **INPUT** – the remaining input followed by `$`.
- **ACTION** – the operation performed (`SHIFT`, `REDUCE`, `ACCEPT`, or `ERROR`).

At the end, the program reports whether the input string is accepted or rejected and displays the total number of SHIFT and REDUCE operations.

## 2. Technologies used

- C programming language
- FLEX (lexical analyzer generator)
- Stack-based Shift-Reduce Parsing
- Command-line interface

## 3. Project files

Keep the FLEX source file (for example, `shift_reduce.l`) in your project directory.

The source file contains:
- Grammar input and production storage
- FLEX lexical rules
- Token collection
- Stack operations
- Shift and reduce operations
- Parsing trace and final result

## 4. Requirements

Install:
- A C compiler such as GCC
- FLEX

The commands below are for Linux or a compatible terminal with FLEX and GCC installed.

## 5. How to build

Save the source code as `shift_reduce.l`, then open a terminal in the same directory.

Run:

```bash
flex shift_reduce.l
gcc lex.yy.c -o shift_reduce_parser -lfl
```

If your system does not require the FLEX library explicitly, the following may also work:

```bash
gcc lex.yy.c -o shift_reduce_parser
```

## 6. How to run

Run the compiled program:

```bash
./shift_reduce_parser
```

On Windows, run the generated executable from Command Prompt:

```bat
shift_reduce_parser.exe
```

The exact build commands on Windows depend on the installed FLEX/GCC distribution.

## 7. How to enter a grammar

Enter one production per line. Use spaces between grammar symbols and write the arrow as `->`. Press ENTER on an empty line after entering all productions.

Example grammar:

```text
E -> T
T -> T * F
T -> F
F -> id
```

The first production's left-hand side (`E` in this example) becomes the start symbol.

For this grammar:
- `E`, `T`, and `F` are non-terminals.
- `id` and `*` are terminals.
- An identifier or number in the input is converted to the token `id`.

**Important input rules:**
- Separate grammar symbols with spaces.
- Do not write an empty production; the program does not support epsilon productions.
- The grammar must be entered before the expression.
- The parser uses the productions in the order entered. For this implementation, use an unambiguous grammar and test the production order carefully.

## 8. Example execution

Use the grammar:

```text
E -> T
T -> T * F
T -> F
F -> id
```

When prompted for the expression, enter:

```text
a*b
```

The lexer converts the expression into:

```text
id * id
```

The parser performs SHIFT and REDUCE operations. The exact step numbers and stack trace are printed by the program. The final result should be:

```text
RESULT: STRING ACCEPTED!
```

The program also prints the total SHIFT and REDUCE operations.

## 9. Test cases

See **Test Programs.txt** for five accepted inputs and three error-focused test cases, together with the expected parser results and notes about features not implemented in this version.

## 10. Current implementation scope and limitations

This README describes the uploaded source code as it is currently written.

1. **Lexical analysis:** FLEX recognizes identifiers and numbers. Both are returned to the parser as the token `id`. Whitespace is ignored. Other single characters are returned as their character tokens.
2. **Syntax analysis:** The parser uses a stack and the entered CFG to perform SHIFT and REDUCE operations.
3. **Semantic analysis:** Symbol-table-based type checking and other semantic checks are not implemented. Therefore, the program cannot identify semantic errors.
4. **Lexical errors:** There is no dedicated lexical-error reporting rule. An unrecognized character is returned as a token and may later cause the parser to reject the input. The program does not report it specifically as a lexical error.
5. **Grammar restrictions:** Empty productions are not supported. Grammar symbols must be separated by spaces.
6. **Parsing strategy:** The implementation selects the first matching reduction in the production list. It is a simple shift-reduce demonstration, not a complete LR parser generator; it does not construct ACTION/GOTO tables or resolve shift/reduce conflicts.

## 11. Conclusion

The project demonstrates the basic working process of a Shift-Reduce Parser using a stack. It combines FLEX-based tokenization with bottom-up parsing and displays each SHIFT and REDUCE operation. The program can be used to experiment with simple context-free grammars and observe how an input string is reduced to the start symbol.
