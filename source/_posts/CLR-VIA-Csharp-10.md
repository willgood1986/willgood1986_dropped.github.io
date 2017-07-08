---
title: CLR-VIA-Csharp-10 Property
date: 2017-07-04 06:10:16
tags: CLR
categories: C#
---
> Properites allow source code to call a method by using a simpilifid syntax. There are parameterful and parameterless properties.
<!--more-->

1. When you define a property and did not provide an implementation for the get/set methods, then the CLR compiler will automatically define a private field. And the CLR compiler will automatically implement the get/set methods. This kind of property is called Automatically Implemented Property(AIP). AIP is different from a field. AIP actually has a default implementation of set/get methods. Meanwhile, field is not property, not having a set/get method.
2. A property cannot be passed as a ref/out parameter to method.
3. It takes longer to access a property than field. As access to a property acutally jumps to access methods.A property mehtod may need extra memory.
4. A parameterful property usually acts as an indexer.
```bash
   public Int32 this[Int32 i_index] 
   {get; set;}
```
5. A property is based on set_xxx and set_xxx method. 
