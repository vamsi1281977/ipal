IPAL: Imperative Procedural Abstraction Language

IPAL is a subset of Visual Basic .NET. We believe this subset provides a good foundation for learning the most important aspect of computing, that is: procedural abstraction. A functional procedural abstraction language could be Scheme, it is from Structure and Interpretation of Computer Programs that we get the phrase: perfection of part and adequacy of collection (the part is a function/procedure, the collection is a set of procedures/functions). The vehicle for learning is code to solve Project Euler problems 001 through 025 (for now). We will specify the guidelines for IPAL and illustrate with code that solves Project Euler problems.

Guideline 0: All programs must be written in a single file. The motivation for this is the original Standard Pascal an academic language which supported only single files.
Guideline 1: Always use 'Option Strict On' and 'Option Infer Off'. The motivation for this is that explicitly specified types make the code more readable and Visual Basic is a verbose programming language anyway.
