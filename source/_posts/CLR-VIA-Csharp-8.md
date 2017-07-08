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

15. By default, types don't have type constructor. And there is only one type constructor. Type constructor is executed at the first time when the type is accessed. C# doesn't allow defining a parameterless instance constructor for value type, allow defining a parameterless type constructor. Type constructor would always be private. And this is guaranteed by the C#, user should just keep it.
16. Value type doesn't allow inline fields, but allow static fields.
```bash
struct SomeValueType
{
    # This is not allowed. Code will not be inlined
    private Int32 m_internalCount = 3;

   # This is permitted
   private static Int32 m_number = 10
}

```
17. Methods of operator overload must be marked **Static** and **public** . In addition, one of the parameter type must be the same as the type that the operater overload method is defined within.
```bash
class SomeType
{
   public static SomeType operator+(SomeType i_op1, SomeType i_op2)
}
```
18.Convention methods must be marked static and pulic. And either the input parameter type or the return type must be same as the type that convention type is defined within. From other type to this type, use the key word implicit; otherwise use explicit key word
```bash
class sealed SomeType
{

   public SomeType(Int32 i_num) {...}
   public static Int32 ToInt32(SomeType i_someType) {...}
   
   public static implicit operator SomeType(Int32 i_num)
   {
     return new SomeType(i_num);
   }

   public static explicit operator Int32(SomeType i_someType)
   {
      return i_someType.ToInt32();
   } 
}
```
19. Convention methods are not invoked when use **as** or **is** operand.
20. Extension method
```bash
public static class SomeTypeExtension
{
  public static DoSomething(this SomeType i_someType, ...)
  {
  }
}
```
21. We also can define extension methods for interface types as following
```bash
public static ShowItems<T>(this IEnumerable<T> items)
{ 
   foreach (var item in items)
   {
       Console.Write(item)
   }
}
```
22. Extension methods are corestone of Microsofts langueage integrated query. 
23. Define extension methods for Delegate methods
```bash
public static InvokeAndCatch<TException>(this Action<Object> func, Object i_object) where TException : Exception
{
   try
   {
      func(i_object)
   }
   catch (TException)
  {
}
}
```
```bash
  Action<Object> action = obj => Console.Write(obj.GetType())
  action.InvokeAndCatch<NullReferenceException>(null)
```

