---
title: CLR-VIA-Csharp-14
date: 2017-07-11 05:39:21
tags: CLR
categories: C#
---
> String plays a great role in most every programming language. We should have good look at How String works in C#

<!--more-->

1. String is **Immutable**. Any modifications would cause new string creation.If the size is big, a bad performance issue is hit.
2. We could use **SecurityString** to handle some private data.
3. In .Net framework, characters are always represented in 16-bit unicode code values. Instances of Char can call GetUnicodeCatory to check unicode type.
4. Char.GetNumericValue('u\0033')
5. Convert.ToXXX works under Range-Check.It would raise an Overflow exception ifcheck got failed.
6. String is a reference type. That is, it always lives in heap, not in the stack of a thread.
7. It is prohibited when trying to use the new operator to construct a string object from literal string.
8. String is well integrated with CLR.The C# provides an easy-to-use syntax to start with String as followed:
```bash
   var Student = "Student"; // A string object.
```
9. A literal string is stored in the metadata of the Assembly. It does not consume additional space.
10. Comparing Strings
 - ToUpperInvariant performs better than ToLowerInvariant.
 - StringComparing.Ordianl/OridinalIgnoreCase options are fastest.
 - By default, CompareTo(IComparable) performs a case-sensitive comparison, Equal performs an ordinal comparison
11. InvariantCulture is associated with English, but not with any country or region.
12. String.ToUpperInvariant performs better than String.ToLowerInvariant.
13. StringComparison.Ordinal works Check length and value of each char.
14. String will be extended when comparing is not by StringComparison.Ordinal.For example:
```bash
using System;
using System.Globalization;
public static class Program {
public static void Main() {
String s1 = "Strasse";
String s2 = "Straße";
Boolean eq;
// CompareOrdinal returns nonzero.
eq = String.Compare(s1, s2, StringComparison.Ordinal) == 0;
Console.WriteLine("Ordinal comparison: '{0}' {2} '{1}'", s1, s2,
eq ? "==" : "!=");
// Compare Strings appropriately for people
// who speak German (de) in Germany (DE)
// as the string will be extended, ß will be extended to ss,
// it will be equal no matter what culture is passed by.
CultureInfo ci = new CultureInfo("de-DE");
// Compare returns zero.
eq = String.Compare(s1, s2, true, ci) == 0;
Console.WriteLine("Cultural comparison: '{0}' {2} '{1}'", s1, s2,
eq ? "==" : "!=");
}
}
Building and running this code produces the following output:
Ordinal comparison: 'Strasse' != 'Straße'
Cultural comparison: 'Strasse' == 'Straße'
```
15. Use String.Intern
```bash
  s1 = "Hello";
  s2 = "Hello";

  s1 = String.Intern(s1);
  s2 = String.Intern(s2)
  if (Object.ReferenceEqual(s1, s2))
  {
     Console.Writeline(s1, s2);
  }
```
16. String TextElement
```
   void PrintTextElement(String s)
   {
       var stringInfo = new StringInfo(s);
       for (var i = 0; i < stringInfo.LengthInTextElements; i++)
       {
           Console.WriteLine(stringInfo.SubStringByTextElement(i, 1))
       }
   }
```
17. String.Clone returns a reference to the specific string.
18. StringBuilder manages sting by an internal array of char.
19. ToString in IFormattable. CultureInfo implement IFormatProvider.
```bash
   String ToString(String format, IFormatProvider formatProvider)
   Object GetFormat() in IFormatProvider
```
20. Common format style - number 200
```bash
Current format:'D' - Decimail Origin:200 -> 200
Current format:'C' - Currency Origin:200 -> $200.00
Current format:'E' - exponential notation Origin:200 -> 2.000000E+002
Current format:'F' - fixed-point Origin:200 -> 200.00
Current format:'N' - number Origin:200 -> 200.00
Current format:Origin:{0} -> 'P' - Percent 20,000.00 %
Current format:Origin:{0} -> 'R' - Percent Origin:2.01 -> 2.01

Current format:Origin:{0} -> 'X' - hexadecimal Origin:200 -> C8
```
21. Common format style - Date
```bash
Current format:'d' - short date 7/17/2017
Current format:'D' - long date Monday, July 17, 2017
Current format:'G' - general date 7/17/2017 6:23 AM
Current format:'M' - general date July 17
Current format:'s' - sortable date 2017-07-17T06:23:07
Current format:'T' - long time 6:23:07 AM
Current format:'u' - universal time time in ISO 8601 2017-07-17 06:23:07Z
Current format:'U' - universal time in full date format Monday, July 17, 2017 1:23:07 PM

Current format:'Y' - year/month July 2017
```
22. Common format style - enum
```bash
Current format:'g' - general Sadness
Current format:'F' - Flags Sadness
Current format:'D' - Decimal 4

Current format:'X' - Hexadecimal 00000004
```
23. Encoding - UTF-8/UTF-16
 - UTF-8, encoding dynamically, one byte, two bytes, three bytes
 - UTF-16, always two bytes
24. Encoding and Decoding
```bash
private static void TestEncoding()
		{
			var greeting = "Hello world.";

			var encodingUTF8 = Encoding.UTF8;

			Byte[] encodedBytes = encodingUTF8.GetBytes(greeting);

			var str = encodingUTF8.GetString(encodedBytes);

			Console.WriteLine("Encoding.GetString result is:" + str);

			var encodedString = BitConverter.ToString(encodedBytes);

			var results = encodedString.Split(new Char[] { '-' }, StringSplitOptions.RemoveEmptyEntries).Select(b => Convert.ToByte(b, 16)).ToArray<Byte>();

			Console.WriteLine("Encoded bytes:" + BitConverter.ToString(encodedBytes));

			Console.WriteLine("Decoded result: {0}", encodingUTF8.GetString(results));
		}
```
25. Encoding and decoding based base64
```bash
private static void EncodeAndDecodeWithBase64()
		{
			var greeting = "Hello, World";

			var bytes = Encoding.UTF8.GetBytes(greeting);

			var base64String = Convert.ToBase64String(bytes);

			Console.WriteLine("Base64String is: {0}", base64String);

			bytes = Convert.FromBase64String(base64String);

			var decodedString = Encoding.UTF8.GetString(bytes);

			Console.WriteLine("decoded string: {0}", decodedString);
		}
```
