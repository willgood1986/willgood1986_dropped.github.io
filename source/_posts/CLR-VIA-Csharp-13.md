---
title: CLR-VIA-Csharp-13 Interface
date: 2017-07-09 08:13:19
tags: CLR
categories: C#
---

> CLR doesn't support multiple inheritance. While it supports implement multipleinterfaces at the same time.

<!--more-->

1. Value type can implement interfaces. If you cast an instance of an interface, a box will happen.Becaulse an interface variable that points to an object on the heap.
2. There are two types of implementation of interface.
 - **Explicit** Prefix the name of the method with the name of the interface. No access identifier can be applied( **Private** in the meta data). User can only  call the method in the interface from interface variable. Cannot be marked with **virtual**, Can not be overrided either.
3. Generic interface supplies three benefits:
 - Compile type safety - Specific type
 - Much less boxing
 - Can be implemented multiple times (class CompareUtility : ICompare<String>, ICompare<Int32>)
4. A bad code example: Boxing, Compile-Type-Safety Loss(IIEI: Implicit Implementation Mehod of Interface)
```bash
   struct UseIIMI : IComparable
   {
       private Int32 m_value;
       
       public UseIIMI(
       Int32 i_value
       )
       {
          m_value = i_value;
       }
       
       public Int32 CompareTo(
          Object i_object
       )
      {
          var value = ((UseIIMI)i_object)
          var result = m_value - value;
      }
   }

  // Call 
  var useIIMI = new UseIIMI(0);
  useIIMI.CompareTo(10);
  
  var object = new Object();

  // Undesired boxing
  v.CompareTo(v);

  //Invalid Cast Exception
  v.CompareTo(o) 
```
5. Use EIMI to work around the issue above.
```bash
   struct UseEIMI : IComparable
   {
      private Int32 m_value;

      public UseEIMI(
      Int32 i_value
      )
      {
         m_value = i_value;
      }

      public Int32 CompareTo(
      UseEIMI i_useEIMI
      )
      {
         var value = i_useEIMI.m_value;
         return m_value = m_value - value;
      }

      public Int32 ICOmparable.CompareTo(
       Object i_object
      )
      {
         var value = ((UseEIMI)i_object).m_value;
         
         return m_value - value;  
      }
   }

6. There are some side effects when using EIMI
  - EIMI must be called from Interface
  - EIMI cannot be called by derived type
  - Undesired boxing when come to Value type
