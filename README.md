IPAL: Imperative Procedural Abstraction Language (authors: Vamsikrishna Kalapala, Microsoft Copilot)

IPAL is a subset of Visual Basic .NET. We believe this subset provides a good foundation for learning the most important aspect of computing, that is: procedural abstraction. A functional procedural abstraction language could be Scheme, it is from Structure and Interpretation of Computer Programs that we get the phrase: perfection of part and adequacy of collection (the part is a function/procedure, the collection is a set of procedures/functions). The vehicle for learning is code to solve Project Euler problems 001 through 025 (for now). We will specify the guidelines for IPAL and illustrate with code that solves Project Euler problems.

Guideline 0: All programs must be written in a single file. The motivation for this is the original Standard Pascal an academic language which supported only single files.

Guideline 1: Always use 'Option Strict On' and 'Option Infer Off'. The motivation for this is that explicitly specified types make the code more readable and Visual Basic is a verbose programming language anyway.

Guideline 2: All namespaces used must be explicitly imported and aliased. Do not directly alias a type, all types must be accessed through a namespace alias. The namespace aliasing convention is: for namespaces starting with the letter S - S0, S1, ..., S9, SA, SB, ..., SZ. If you ever need to import more than 36 namespaces beginning with the same letter please let us know!

Example 1 - Solution to Project Euler Problem 001:
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

Example 2 - Solution to Project Euler Problem 002:
```
Option Strict On
Option Infer  Off

Imports S0 = System

Module ProjectEuler
  Function Solve(ByVal a as S0.Int64) as S0.Int64
    Dim b as S0.Int64 = 0L
    Dim c as S0.Int64 = 1L
    Dim d as S0.Int64 = 0L
    While b <= a
      If (b Mod 2L) = 0L Then
        d = b + d
      End If
      Dim e as S0.Int64 = b + c
      b = c
      c = e
    End While
    Return d
  End Function

  Sub Main(ByVal args as String())
    Dim a as S0.Int64 = Solve(4000000L)
    S0.Console.WriteLine(a)
  End Sub
End Module
```

Example 3 - Solution to Problem 003
```
Option Strict On
Option Infer  Off

Imports S0 = System

Module ProjectEuler
  Function LargestPrimeFactor(ByVal a as S0.Int64) as S0.Int64
    If a < 2L Then
      Throw New Exception("check failed")
    ElseIf a < 4L Then
      Return a
    Else
      Dim b as S0.Int64 = 2L
      Dim c as S0.Int64 = b * b
      Dim d as S0.Int64 = 0L
      While b <= a
        If (a Mod b) = 0L Then
          a = a \ b
          d = b
        Else
          b = b + If(b = 2L, 1L, 2L)
          c = b * b
        End If
      End While
      Return S0.Math.Max(a, d)
    End If
  End Function

  Sub Main(ByVal args as String())
    Dim a as S0.Int64 = LargestPrimeFactor(600851475143L)
    S0.Console.WriteLine(a)
  End Sub
End Module
```

Guideline 3: Perfection of Part. Each function/procedure should do conceptually one thing and one thing only. This is illustrated in the following example.

Example 004: Solution to Project Euler Problem 004
```
```
