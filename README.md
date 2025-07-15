IPAL: Imperative Procedural Abstraction Language (authors: Vamsikrishna Kalapala, Microsoft Copilot)

IPAL is a subset of Visual Basic .NET. We believe this subset provides a good foundation for learning the most important aspect of computing, that is: procedural abstraction. A functional procedural abstraction language could be Scheme, it is from Structure and Interpretation of Computer Programs that we get the phrase: perfection of part and adequacy of collection (the part is a function/procedure, the collection is a set of procedures/functions). The vehicle for learning is code to solve Project Euler problems 001 through 010 (for now). We will specify the guidelines for IPAL and illustrate with code that solves Project Euler problems.

Guideline 0: All programs must be written in a single file. The motivation for this is the original Standard Pascal an academic language which supported only single files.

Guideline 1: Always use 'Option Explicit On', 'Option Strict On' and 'Option Infer Off'. The motivation for this is that explicitly specified variables with types make the code more readable and Visual Basic is a verbose programming language anyway.

Guideline 2: All namespaces used must be explicitly imported and aliased. Do not directly alias a type, all types must be accessed through a namespace alias. The namespace aliasing convention is: for namespaces starting with the letter S - S0, S1, ..., S9, SA, SB, ..., SZ. If you ever need to import more than 36 namespaces beginning with the same letter please let us know!

Example 1 - Solution to Project Euler Problem 001:
```
Option Explicit On
Option Infer    Off
Option Strict   On

Imports S0 = System
Imports S1 = System.Diagnostics

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
    Dim a as S1.Stopwatch = S1.Stopwatch.StartNew()
    Dim b as S0.Int64 = Solve(3L, 5L, 999L)
    a.Stop()
    S0.Console.WriteLine(b)
    S0.Console.WriteLine(">>>>>> Time taken: " & a.ElapsedMilliseconds & " ms. <<<<<<")
  End Sub
End Module
```

Example 2 - Solution to Project Euler Problem 002:
```
Option Explicit On
Option Infer    Off
Option Strict   On

Imports S0 = System
Imports S1 = System.Diagnostics

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
    Dim a as S1.Stopwatch = S1.Stopwatch.StartNew()
    Dim b as S0.Int64 = Solve(4000000L)
    a.Stop()
    S0.Console.WriteLine(b)
    S0.Console.WriteLine(">>>>>> Time taken: " & a.ElapsedMilliseconds & " ms. <<<<<<") 
  End Sub
End Module

```

Example 3 - Solution to Problem 003
```
Option Explicit On
Option Infer    Off
Option Strict   On

Imports S0 = System
Imports S1 = System.Diagnostics

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
    Dim a as S1.Stopwatch = S1.Stopwatch.StartNew()
    Dim b as S0.Int64 = LargestPrimeFactor(600851475143L)
    a.Stop()
    S0.Console.WriteLine(b)
    S0.Console.WriteLine(">>>>>> Time taken: " & a.ElapsedMilliseconds & " ms. <<<<<<")
  End Sub
End Module
```

Guideline 3: Perfection of Part. Each function/procedure should do conceptually one thing and one thing only. This is illustrated in the following example (see ReverseDigits).

Example 004: Solution to Project Euler Problem 004
```
Option Strict On
Option Infer Off

Imports S0 = System

Module ProjectEuler
  Function ReverseDigits(ByVal a As S0.Int64) As S0.Int64
    Const kBase As S0.Int64 = 10L
    Dim b As S0.Int64 = 0L
    While a > 0L
      Dim c As S0.Int64
      c = a Mod kBase
      a = a \ kBase
      b = (b * kBase) + c
    End While
    Return b
  End Function

  Function Solve(ByVal a As S0.Int64, ByVal b As S0.Int64) As S0.Int64
    Dim c As S0.Int64 = 0L
    Dim d As S0.Int64
    For d = a To b
      Dim e As S0.Int64
      For e = d To b
        Dim f As S0.Int64 = d * e
        Dim g As S0.Int64 = ReverseDigits(f)
        If f = g Then
          c = S0.Math.Max(c, f)
        End If
      Next e
    Next d
    Return c
  End Function

  Sub Main(ByVal args As String())
    Dim a As S0.Int64 = Solve(100L, 999L)
    S0.Console.WriteLine(a)
  End Sub
End Module
```

Guideline 4: Adequacy of collection. Not only should each function/procedure should conceptually do one thing only, but also the collection of functions/procedures should solve the problem at hand (See GreatestCommonDivisor and LeastCommonMultiple in the example below).

```
Option Strict On
Option Infer Off

Imports S0 = System

Module ProjectEuler
  Function GreatestCommonDivisor(ByVal a as S0.Int64,
                                 ByVal b as S0.Int64) as S0.Int64
    If a < 0L Then
      Return GreatestCommonDivisor((- a), b)
    ElseIf b < 0L Then
      Return GreatestCommonDivisor(a, (- b))
    ElseIf a = 0L Then
      If b = 0L Then
        Throw New Exception("check failed")
      Else
        Return b
      End If
    Else
      While b > 0L
        Dim c as S0.Int64 = a Mod b
        a = b
        b = c
      End While
      Return a
    End If
  End Function

  Function LeastCommonMultiple(ByVal a As S0.Int64,
                               ByVal b as S0.Int64) As S0.Int64
    Dim c as S0.Int64 = GreatestCommonDivisor(a, b)
    Dim d as S0.Int64 = a \ c
    Dim e as S0.Int64 = b * d
    Return e
  End Function

  Function Solve(ByVal a As S0.Int64) As S0.Int64
    Dim b as S0.Int64 = 1L
    Dim c as S0.Int64
    For c = 1 to a
      b = LeastCommonMultiple(b, c)
    Next c
    Return b
  End Function

  Sub Main(ByVal args As String())
    Dim a As S0.Int64 = Solve(20L)
    S0.Console.WriteLine(a)
  End Sub
End Module
```

Guideline 5: There may be exceptions to guidelines 3 and 4.  Sometimes it may be both easier and cleaner to implement one function/procedure that solves the problem at hand. See Examples 1,2 and 6.

Example 6 - Solution to Project Euler Problem 006:

```
Option Strict On
Option Infer  Off

Imports S0 = System

Module ProjectEuler
  Function Solve(ByVal a as S0.Int64) as S0.Int64
    Dim b as S0.Int64 = 0L
    Dim c as S0.Int64 = 0L
    Dim d as S0.Int64
    For d = 1 To a
      b = b + d
      c = c + (d * d)
    Next d
    Dim e as S0.Int64 = b * b
    Dim f as S0.Int64 = e - c
    Return f
  End Function

  Sub Main(ByVal args as String())
    Dim a as S0.Int64 = Solve(100L)
    S0.Console.WriteLine(a)
  End Sub
End Module
```
