---
title: CLR-VIA-Csharp-7 Constants and Fields
date: 2017-06-15 06:49:13
tags: CLR
Categories: C#
---
> Data members - Constants and Fields
<!--more-->

1. A **Constant** is a symbol that has a never-changing value. When defining a constant symbol, its value must be determinable at compile time.Then the compiler save the value into the assembly's metadata.In that way, primitive type, non-primitive type only assigned with null. Constants are considered part of Type. That is saide, constants are always considered to static fields. Define constants causes creation of metadata.
2. When code refers to a constant. CLR looks up the value in the metadata of the assembly in which defines the constant, extract the value, embeds the value into the IL codes.As the value of a constant is directly embeded into the IL code. It doesn't require additional memory to be allocated at runtime. It cannot get the address of the constant and never be passed by reference.
3. For readonly fields, then can only be edited in the constructor. The way intialized when defining the varialbe. The code block acutally is put into constructor which is call **inline**
