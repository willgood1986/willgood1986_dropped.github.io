---
title: CLR-VIA-Csharp-8 Methods
date: 2017-06-16 21:05:50
tags: CLR
Categories: C#
---
> Methods are to change state of the object.They may be inform of constructor(instance/type), operator overload, type conversion, extension methods, and partial methods.
<!--more-->

### Constructor ###

1. Constructors are methods to initialize the object of the type to be good state.
2. All fields that the constructor doesn't explicitly overwrite are guaranteed to 0 or null.
3. Unlike other methods, constructors are never inherited. That is, a class has only the instance constructor that class defines itself. You can never apply modifiers, like new, virtual, abstruct, sealed, override, etc to instance constructor. If a class doesn't include any constructor, the compiler will define a parameterless constructor by default.
4. A class's instance constructor must access the base type's constructor before accessing the inherited fields on base type.
5. In some cases, creating an instance of type can go without calling instance constructor. For example, Object.MemberWiseClone; Deserializing the object at runtime with serializer.
6. Never call a virtual method in the instance constructor. As fields are not fully initialized yet.
7. We can use the keyword this to make a constructor chain to guarantee the right initialization.
8. Value type constructors work quite diefferently from reference type constructors.
9. The CLR always allows the creation of value type instances, and there is no way to prevent a value type to be initialized.For this reason, value types don't even need to have a construtor defined.And CLR doesn't emit default parameterless constructor.
10. Value type constructor only be invoked when calling the value type constructor explicitly using the new keyword.
11. To improve performance of the application at runtime, the value types are initialized by default.The value of each field is set zero or null(for reference type). However, if the value tye has a constructor defined, and called explicitly, the constructor will be executed.
12. Most important, for value type, the C# compiler doesn't allow defining a parameterless constructor for a value type.In this way, the C# compiler will initialize all fields to zero or null.And instance fields initializers is not permitted. The following is an example. 
```
internal struct SomeType
{
   internal Int32 Int32Value = 32;
}
```
13. You should overrite the value type explicitly.The reason is that value type is stack-based. Stack-based value type fields are not guaranteed to be zero/null.There would be a compiling error.  
```
internal void SomeMethod()
{
   Int32 totalNumber;
   Console.WriteLine("Total number is :{0}", totalNumber).
}
```
14. If you define a constructor for a value type. Every field in the value type must be initialized explicitly too. The following is a wrong demo.
```
internal struct Triangle
{
   internal Double LengthOfA;
   internal Double LenghtOfB;
   internal Double LengthOfC;

   internal Triangle()
   {
       LengthOfA = 3d;
       LengthOfB = 4d;
   }
}
