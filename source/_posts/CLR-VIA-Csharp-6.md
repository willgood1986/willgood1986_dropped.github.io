---
title: CLR-VIA-Csharp-6
date: 2017-06-13 08:29:48
tags: CLR
categories: C#
---
> Type and member basics. The common members are Constants, Fields, Constructors(instance/type),methods, operator overload,Conversion operators,property, events.
<!--more-->

1. Basically, when you add a key/value pair to a collection, a hash code for the key object is obtained first. This hash code indicates which “bucket” the key/value pair should be stored in. When the collection needs to look up a key, it gets the hash code for the specified key object. This code identifies the “bucket” that is now searched sequentially, looking for a stored key object that is equal to the specified key object. Using this algorithm of storing and looking up keys means that if you change a key object that is in a collection, the collection will no longer be able to find the object. If you intend to change a key object in a hash table, you should remove the original key/value pair, modify the key object, and then add the new key/value pair back into the hash table.
2. A static event is a mechanism that allows a type to send a notification to one or more static or instance methods. An instance (nonstatic) event is a mechanism that allows an object to send a notification to one or more static or instance methods. Events are usually raised in response to a state change occurring in the type or object offering the event. An event consists of two methods that allow static or instance methods to register and unregister interest in the event. In addition to the two methods, events typically use a delegate field to maintain the set of registered methods
3. If you do not explicitly specify either of these when you define a type, the C# compiler sets the type’s visibility to internal.
4. The CLR and C# support this via friend assemblies. This friend assembly feature is also useful when you want to have one assembly containing code that performs unit tests against the internal types within another assembly. When an assembly is built, it can indicate other assemblies it considers “friends” by using the InternalsVisibleTo attribute defined in the System.Runtime.CompilerServices namespace.
5. For any member to be accessible, it must be defined in a type that is visible. C# requires that a member in the base type and inherited type must have the same accessibility.
6. Static class must inherit from System.Object; Cannot implement any interface, only define static members, cannot be used as a method parameter, field, or local variable. In a word, static type T can not perform T x usage.
7. The key word sealed, when applied to Type, it means that type can not be a base type. when applied to method, it only can be applied to the method overriding a virtual method.
8. C# use CallVirt IL instruction which checks object variable null-being to call instance method(virtual and non-virtual).Even though some methods won't access member fields. However, to some degree, it's more safe and gets slower than it could be.
9. Calling a virtual method doesn't perform as well as calling a non-virtual method. Because CLR must look up the the type of the object at runtime in order to determine which type defines the method.
10. In C#, use the key word new to hide the same method in the base class.
