---
title: CLR-VIA-Csharp-12 Generic
date: 2017-07-08 07:43:16
tags: CLR
categories: C#
---
> OOP provides a mechanism of **Code Reuse**, generic provides a mechanism of **Algorithm Reuse**

<!--more-->

1. FCL allows creation of generic reference type and value type as well as value type generic, it does not allow creation of **generic enumerated types**. In addition, FCL allows creation of generic interface and delegate.
2. Benefits by Generic include:
- Source code protection, no need to access source code.
- Type-Safty. Only compatible types work.
- Better peformance. No type cast need.
3. Prepare environment:
```bash
   GC.Collect();
   GC.WaitingForFinalizers();
   GC.Collect();
   # P269
   # StartWatch.StartNew();
```
4. The commonly used interfaces in FCL are contained in the System.Collection.Generic namespace.
5. Array.BinarySearch?
6. Open type VS. Closed type
 - **Open type** is a type with a generic type parameter.
 - System doesn't allow instance of open type.(It also applies to interface, abstruct class, etc.)
7. Activator.CreateInstance(type)
8. A generic type sample. All elements in the list must be the same type.
```bash
   class Node<T>
  { 
    T m_data;
    Node<T> m_next;

    Node(T i_data): this(i_data, null)
    {
    }
    
    Node(T i_data, Node<T> i_next)
    {
       m_data = i_data;
       m_next = i_next
    }

    public override String ToString()
    {
       return m_data.ToString() + (m_next != null) ? m_next.ToString() : String.Empty
    }
  }
```
10. A varied type version, we can define a generic base type.
```bash
  insternal class Node 
   {
      protected m_next Node

      public Node(Node i_next)
      {
         m_next = i_next
      }
   }

  internal class TypedNode<T> : Node
  {
     T m_data;

     public TypedNode(T i_data, Node i_next) : base(i_next)
     {
       m_data = i_data
     }

     public TypedNode(T i_data) : this (i_data, null)
     {
     }
     
     public override String ToString()
     { 
         return m_data.ToString() + (m_next != null) ? m_next.ToString() : String.Empty;
     }
  }

  
```
11. A generic type parameter can be marked as(Only applies to reference type):
 - Invariant, defualt
 - Contravariant, change a type to its child type, marked with **in**, method parameter
 - Covariant, change a type to its base type, marked with **out**, the return type.
```bash
   public delegate TResult Func<in T, out TResult>(T i_input)
   Func<Object, ArgumentException> func1 = null;
   Func<String, Exception> func2 = func1; // no explicit case needed.
```
12. Generic constraits:
 - class MyList<T> where T : class / struct / new
13. All value types have a default parameterless consructor.
14. Methods held in a generic class can directly use the generic type. Mehods themselves can declare new type. 
15. Generic type inference use the type of the variable, not the actual type of the value.
```bash
   String s1 = "abc";
   Object s2 = "abc";
   Action(s1, s2) => inference result => Action<String, Object>
```
