IPAL: Imperative Procedural Abstraction Language (authors: Vamsikrishna Kalapala, Microsoft Copilot)

IPAL is a subset of Visual Basic .NET. We believe this subset provides a good foundation for learning the most important aspect of computing, that is: procedural abstraction. A functional procedural abstraction language could be Scheme, it is from Structure and Interpretation of Computer Programs that we get the phrase: perfection of part and adequacy of collection (the part is a function/procedure, the collection is a set of procedures/functions). The vehicle for learning is code to solve Project Euler problems 001 through 025 (for now). We will specify the guidelines for IPAL and illustrate with code that solves Project Euler problems.

Guideline 0: All programs must be written in a single file. The motivation for this is the original Standard Pascal an academic language which supported only single files.

Guideline 1: Always use 'Option Strict On' and 'Option Infer Off'. The motivation for this is that explicitly specified types make the code more readable and Visual Basic is a verbose programming language anyway.

Guideline 2: All namespaces used must be explicitly imported and aliased. Do not directly alias a type, all types must be accessed through a namespace alias. The namespace aliasing convention is: for namespaces starting with the letter S - S0, S1, ..., S9, SA, SB, ..., SZ. If you ever need to import more than 36 namespaces beginning with the same letter please let us know!

Example 0 - Solution to Project Euler Problem 001:
```
Option Strict On
Option Infer  Off

Imports S0 = System

Module ProjectEuler
  Function Solve(ByVal a as S0.Int64,
                 ByVal b as S0.Int64,
                 ByVal c as S0.Int64) as S0.Int64
    Dim d as S0.Int64 = 0L
    Dim e as S0.Int64
    For e = 0 To c Step a
      d = d + e
    Next e
    Dim f as S0.Int64
    For f = 0 To c Step b
      If (f Mod a) <> 0L Then
        d = d + f
      End If
    Next f
    Return d
  End Function

  Sub Main(ByVal args as String())
    Dim a as S0.Int64 = Solve(3L, 5L, 999L)
    S0.Console.WriteLine(a)
  End Sub
End Module
```
