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

### Evaluation Strategy
- Set of rules for evaluating expressions
    - General Types:
        - [Lazy Evaluation (call-by-need)](https://en.wikipedia.org/wiki/Lazy_evaluation)
        - [Partial Evaluation](https://en.wikipedia.org/wiki/Partial_evaluation)
        - [Remote Evaluation](https://en.wikipedia.org/wiki/Remote_evaluation)
            - Transmitting executable software code from client system to server system, and results sent back to client system from server.
        - [Short-circuit evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation)
            - Aka Minimal Evaluation
            - Semantic of some boolean operators
                - Second argument is executed only if the first argument does not suffice to determine the value of the expressionn
                    - When `False AND True`, overall value must be `False`.
                    - When `True OR False`, overall value must be `True`.
    


## Misc Basics

### Dangling Pointer
- Address of local var and return
    - Dangerous!
    - In stack frame - so in memory - but correct/normal access is lost
    - Caused by deallocation
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
    - Avoid reading/writing to a pointer after de-referencing
    - To prevent this issue as well as security, some systems zero out data after freeing
        - This manifests bugs faster if you have a dangling pointer (Oh no, I lost my data!)

### Undefined vs Unspecified Behavior
- [Undefined Behavior](https://en.wikipedia.org/wiki/Undefined_behavior)
    - When a program contains or is executing code for which it's programming language specs do not mandate specific requirements.
    - Nickname: Nasal Demons
    - Allowed in some languages
    - Used to be used by developers for optimization - code written to take advantage of compiler and platforms supported (Optimized for compiler/platform.)
    - In more modern situations, Undefined behavior usually represents unambiguous bugs in code.
        - Ex. Indexing an array outside of it's bounds
    - Runtime assumes undefined behavior never happens. It does not check against the conditions
    - Example:
        - At the start of your program:
            - `n=0`
        - You then make 2 threads.
            1. `n = 1`
            2. `while(n==0) { ... }`
        - Compiles into the following:
        ```
        if(n==0){
            while(<InsertLoopHere>)
        }
        ```
        - Your code will first be n = 0, and then on thread 1 be n = 0 and on the other undeclared
        - You will have a caveat bug - optimized into existence by compiler.
        - The above code should loop forever.
- [Unspecified Behavior](https://en.wikipedia.org/wiki/Unspecified_behavior)
    - When the final executable produced has different behavior when compiled on a different compiler.



# Interesting Side-notes

- F# = Microsoft version of Java