------------------------
AUTHOR
------------------------

David Austin
CS-33101: Programming Languages
Final Project

FOR LOOP EXTENSION - CS-33101 Final Project
===========================================

This project extends a basic interpreter to support the `for` loop construct. 
It includes changes to the grammar, parser, and test system, and leverages 
existing `while` support in the evaluator.

------------------------
USAGE
------------------------

To run the interpreter:

  $ python runner.py [filename]

- If a filename is provided, it will execute that file.
- Otherwise, it will launch an interactive REPL.

------------------------
KEY COMPONENTS
------------------------

1. tokenizer.py
   - Lexical analysis of source code
   - Converts input into a list of tokens

2. parser.py
   - Converts token streams into an abstract syntax tree (AST)
   - Implements full recursive-descent parsing for:
     - expressions, statements, control flow
     - `for` statements (via `parse_for_statement`)

3. evaluator.py
   - Evaluates the AST and performs actions
   - Supports variable assignment, loops, function calls, etc.
   - `for` loops are desugared into `while` + update logic

4. runner.py
   - Command-line entry point
   - Supports both file-based execution and interactive REPL

------------------------
FOR LOOP IMPLEMENTATION
------------------------

Grammar Rule:
  for_statement = "for" "(" expression ";" expression ";" expression ")" statement_list

Desugaring:
  A `for` loop is transformed into the following AST:

    {
      "tag": "statement_list",
      "statements": [
        init,
        {
          "tag": "while",
          "condition": condition,
          "do": {
            "tag": "statement_list",
            "statements": [body, update]
          }
        }
      ]
    }

Parser Changes:
- Added `parse_for_statement(tokens)`
- Integrated into `parse_statement()`
- Added test: `test_parse_for_statement()`

------------------------
DIRECTORY STRUCTURE
------------------------

CS-33101-FP-main/
- tokenizer.py         # Tokenizes input source code
- parser.py            # Converts tokens to AST, includes for-loop support
- evaluator.py         # Traverses the AST and executes logic
- runner.py            # Runs interpreter or REPL
- README.txt           # This file
(tests inside parser/evaluator files)
