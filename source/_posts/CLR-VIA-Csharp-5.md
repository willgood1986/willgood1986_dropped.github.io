---
title: CLR-VIA-Csharp-5
date: 2017-06-12 06:46:40
tags: CLR
categories: C#
---
> Primitive, Reference, Value type
<!--more-->

1. By default, overflow checking is turned off. It makes the code runs faster. One way to get the C# compiler to control overflows is to use the /checked+ compiler switch. Programmers can control overflow checking in checking in specific regions of their code.
2. The variable representing the instance doesn't contain a pointer to an instance; the variable contains the fields of the instance itself. Value type instances don't come under the control of the garbage collector, Integer, Boolean, Decimal, Timespan, Enumeration
3. Even though you can't choose a base type when defining your own value type, a value type can implement one or more interfaces if you choose. In addition, all value types are sealed, which prevents a value type from being used as a base type for any other reference type or value type.

SomeVal v1 = new SomeVal(). It would zero all of the fields in the value type instance.

4. When a type offers no members that alter its fields, we say that the type is immutable. In fact, it is recommended that many value types mark all their fields as readonly.

5. The size of instances of your type is also a condition to take into account because by default, arguments are passed by value, which causes the fields in the value type instances to be copied, hurting performance.

6. It is obvious that the C# compiler team believes that structures are commonly used when inter-operating with unmanaged code, and for this to work, the fields must stay in the order defined by the programmer. However, if you are creating a value type that has nothing to do with interoperability with unmanaged code, you could override the C# compiler's default. Explicit layout is typically used to simulate what would be a union in unmanaged C/C++ because you can have multiple fields starting at the same offset in memory.

7. It's possible to convert a value type to a reference type by using a mechanism called boxing. Allocate memory on managed heap, copy fields of value type instance, return the reference to the heap.

8. One of the biggest improvements is that the generic collection classes allow you to work with collections of value types without requiring that items in the collection be boxed/unboxed.

9. This in itself greatly improves performance because fewer objects will be created on the managed heap thereby reducing the number of garbage collections required by your application.

10. Furthermore, you will get compile-time type safety, and your source code will be cleaner due to fewer casts.

11. A value type is to be boxed when call GetType method. Because it needs to a pointer to point at managed heap.

12. There are four rules on Equals:
 - Reflexive X.Equals(x) returns true
 - Symmetric. x.Equals(y) == y.Equals(x)
 - Transive. if (x.Equals(y) && y.Eqauls(z)) then x.Equals(z) returns true
 - Consistent. No changes during comparison.
13. Recommanded practice when implementing Equals:
 - GetHashCode
 - IEquatable<T>.Equals() to provide a type-safe Equals method for internal use.
 - Override ==, !=
 - If sorting required, consider of ICompare.CompareTo and ICompare<T>.CompareTo for type-safe, overriding operator <=,<,>,>=
14. Never persists hash code. Cause type may be changed some time.
