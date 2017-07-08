---
title: CLR-VIA-Csharp-9 Parameters
date: 2017-07-04 05:29:45
tags: CLR
categories: C#
---
> Introduce parameters in methods
<!--more-->

1. Parameters with default values are marked with **OptionalAttribute** and **DefaultParameterValueAttribute** held the default value in the constructor. Both attributes are in System.Runtime.InteropServices.
2. Default value must be primitive types or null if reference types.
3. It is not permitted to declare a parameter by implicit type local variable(var). Because there is no callsite passing arguments, the compiler cannot infer the type.
4. By default, CLR assumes all arguments are passed by value.
5. From the perspective of CLR, ref and out are identical.So they cannot be used for method overload.
6. use params keyword to accept a bunch of arguments.However, it would incur an additional performance hit.
7. When define a parameter type in method, it is better to use the weakest type. For it would be used in a much wider range of scenarios.
```bash
  # preferred
  void ProcessBytes(Stream i_someStream)
  # Not recommanded
  void ProcessBytes(FileStream i_fileStream)
```
8. On the flip side, it is best to define the return type of a method by using the strongest type.
9. Const-ness of parameters is unsupported in CLR. 
