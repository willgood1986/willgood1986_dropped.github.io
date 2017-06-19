---
title: CLR-VIA-Csharp-4
date: 2017-06-12 06:38:20
tags: CLR
categories: C#
---
> Have a quick look at Type in C sharp
<!--more-->

1. All types except for System.Object is inherited from System.Object by default.
2. There are four public method in System.Object.
 - ToString()
 - GetHashCode
 - Equals
 - GetType()

3. There are two overhead memebers, one is Type Object Pointer, the other is Sync Block Index on heap.
4. Stacks build from High adress to Low address. They are used for passing arguments and storing local variables for methods. When calling another method, first pushing arguments one by one to stack, then put the return address then. This can make sure that when method is executed, the pointer can return to source method.
5. After referred Assemblies are loaded, create types used on the heap.

