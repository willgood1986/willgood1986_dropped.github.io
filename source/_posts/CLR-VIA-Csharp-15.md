---
title: CLR-VIA-Csharp-15 Enumerated types and bit flags
date: 2017-07-18 07:14:10
tags: CLR
categories: C#
---
> Enumerated types are easy to use. They perform like constants. Be aware of version issue.

<!--more-->

1. Enumerated type is primitive type and value type.
2. They can explicity inherit from integer type, such as byte, int32, long, etc.We can determine the actual type by calling Enum.GetUnderlyingType.
```bash
  enum MailboxType : byte
    {
        Unknown = 0,
        UserMailbox = 1,
        RoomMailbox = 2,
        EquipmentMailbox = 4
    }

    var type = Enum.GetUnderlyingType(typeof(MailboxType));

            Console.WriteLine("Underlying type: {0}", type); // System.Byte
``` 
2. Enum is a reference type.
3. Enmu's format method
```bash
    internal static void TestEnumFormat()
        {
            Byte value = 4;

            var result = Enum.Format(typeof(MailboxType), value, "G");

            Console.WriteLine("value:{0}, format:'G', result:{1}", value, result);
        }
    // Output: value:4, format:'G', result:EquipmentMailbox
```
4. GetAllValues
```bash
  internal static void PrintAllMembers()
        {
            MailboxType[] values = (MailboxType[])Enum.GetValues(typeof(MailboxType));

            Console.WriteLine("value\tSymbol");
            Console.WriteLine("-----\t----");

            foreach (var value in values)
            {
                Console.WriteLine("{0,5:D}\t{0:G}", value);
            }
        }

   // out put:
   value	Symbol
-----	----
    0	Unknown
    1	UserMailbox
    2	RoomMailbox
    4	EquipmentMailbox
```
6. Enum.IsDefined is implemented by **Reflection**, it has a bad performance.
7. We can apply FLagsAttribute to enumerated type. And when calling ToString(), it can infer by combination of members. Members in enumerated type should be bitwised.
