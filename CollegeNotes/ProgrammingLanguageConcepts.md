# Programming Language Concepts

*Notes for Readers:* 
- Some of the content is material from my college notes - others were pulled/updated via research.
- Links will be provided.

# Class 1 - The Basics

## General History of languages from '70s to 2010s
- 40s: Assembly
- 50s: Fortran, LISP
- 60s: COBOL, BASIC, B
- 70s: C, SQL, Meta Language, SAS, Pascal
- 80s: SmallTalk, CBASIC, C++, Perl, Objective-C, Erlang
- 90s: Python, Visual Basic, R, Lua, ANSI Common Lisp, Java, PHP, Javascript, Ruby
- 00s: C#, Visual Basic .NET, Scala, F#, Clojure, Go
- 10s: Rust, Swift, TypeScript

[Languages by Year - Wikipedia](https://en.wikipedia.org/wiki/Timeline_of_programming_languages)

## Basic Fundamentals

### Statement vs Expressions
- Side Effect vs value
- **[Statement:](https://en.wikipedia.org/wiki/Statement_(computer_science))**
    - A group of expressions and/or statements that carry out a task/action.
    - Two-sided - either do tasks, or don't.
    - When returning a value, can be used as an expression.
        - This is why a class/function is a statement *and* an expression in certain languages (ex. JavaScript)
    - Java example:
        - `X = 5 * 2`
    - C++ example:
        - `x = (Y = 0);`
            - Nested Statement
            - Inner declaration is a side-effect (statement) of the outer statement.
            - Excudes from the inside-out.
            - Assigns 0 to y, then y to x. The value passed from Y to X is a pointer to Y.
- **[Expression:](https://en.wikipedia.org/wiki/Expression_(computer_science))**
    - Word/group of symbols that is a value.
    - Anything that executes and ends up being a value
    - A value is unique - in meaning or character
    - Can also be a statement
        - C++ example:
            - [Comma operator](https://en.wikipedia.org/wiki/Comma_operator)
            - `(e1,e2,e3)`
                - One expression

### Literal vs Variables/Constants
- Text representation of a value vs Symbolic name with a storage location
- **[Literal](https://en.wikipedia.org/wiki/Literal_(computer_programming))**
    - Text representation of a value
    - Written in language
- **Variables/Constants**
    - ***[Variables](https://en.wikipedia.org/wiki/Variable_(computer_science))***
        - A name representing a Abstract storage location containing a value
    - ***[Constant](https://en.wikipedia.org/wiki/Constant_(computer_programming))***
        - Value not altered by program during *normal* execution
        - Can be declared similar to a variable - "Named Constant"

### [Operators:](https://en.wikipedia.org/wiki/Operator_(computer_programming))
- Provides functionality that may not be possible to define as a user defined function (sizeof in C) OR has syntax different than a function ( + )
- Often Arithmetic or memory manipulation
- C++ Example:
    - `x++` or `++x`
        - [Postfix / Prefix Increment operators](https://learn.microsoft.com/en-us/cpp/cpp/postfix-increment-and-decrement-operators-increment-and-decrement?view=msvc-170)
        - Also an expression on top of an Operator
- [Ternary Operator:](https://en.wikipedia.org/wiki/Ternary_operation)
    - Operator that takes 3 arguments (aka operands)
    - If-then-else

### [Conditional Statement vs Conditional Expression vs Conditional Construct](https://en.wikipedia.org/wiki/Conditional_(computer_programming))
- Conditional Statement:
    - Executed for side-effects
    - `return (expression)`
- Conditional Expression:
    - Return values
    - `return N;`

### Dangling Pointer
- Address of local var and return
    - Dangerous!
    - In stack frame, but lost
    - data was lost/deallocated
    - When calling a dangling pointer, no longer allocated to reference
        ``` C++
        *P = (int x ) malloc(SizeOf(int)); // Goes onto heap
        // *P = location in memory - is pointer
        pLocation = 0x11223344
        free(p);
        // Oh no! It's unallocated!
        // Data is still at the location but not (easily) accessible
        int x = *pLocation
        // This will ONLY recover the data on the system code was compiled on.
        // Always avoid!
        ```
        - This can further be complicated by [Endianness](https://en.wikipedia.org/wiki/Endianness) (Little vs Big)
            - Intel = Little Endian

# Interesting Side-notes

- F# = Microsoft version of Java