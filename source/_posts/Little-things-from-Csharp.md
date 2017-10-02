---
title: Little things from Csharp
date: 2017-09-25 06:56:17
tags: C#
categories: C#
---
> Some little tips from small code practice. Codes are checked in the [Github](https://github.com/willgood1986/funnycodes).

<!--more-->


1. Array.BinarySearch(array, target). It works on a ordered list.

2. ^(\d{3}).{0,}.mp3$ -> $1.mp3 替换第一个组 得到的结果（123adsgadg.mp3）123.mp3

3. Console Redirector -> Console.SetOut(StreamWriter); default standard output - Console.Out

4. Dictionary operation, add a key-value pair, Dict[Key] = Value

5. Format Date Time  

   Current format:'d' - short date 9/25/2017 
   Current format:'D' - long date Monday, September 25, 2017
   Current format:'G' - general date 9/25/2017 1:24 AM
   Current format:'M' - general date September 25 
   Current format:'s' - sortable date 2017-09-25T01:24:03
   Current format:'T' - long time 1:24:03 AM
   Current format:'u' - universal time time in ISO 8601 2017-09-25 01:24:03Z
   Current format:'U' - universal time in full date format Monday, September 25, 2017 8:24:03 AM
   Current format:'Y' - year/month September 2017

6. Format Enumerate Type

    Current format:'g' - general Sadness

    Current format:'F' - Flags Sadness

    Current format:'D' - Decimal 4 Current format:'X' - Hexadecimal 00000004

7. Format Number

   Current format:'D' - Decimail Origin:200 -> 200

   Current format:'C' - Currency Origin:200 -> $200.00

   Current format:'E' - exponential notation Origin:200 -> 2.000000E+002

   Current format:'F' - fixed-point Origin:200 -> 200.00

   Current format:'N' - number Origin:200 -> 200.00

   Current format:Origin:{0} -> 'P' - Percent 20,000.00 %

   Current format:Origin:{0} -> 'R' - Percent Origin:2.01 -> 2.01

   Current format:Origin:{0} -> 'X' - hexadecimal Origin:200 -> C8
8. Format(format-Pattern, content). If format-Pattern is null, it works and ignores the format-pattern  

9. String - Encoded Bytes. Encoding.UTF8.GetBytes/GetString  

10. Print a byte array we can call BitConverter.ToString(ByteArray) Convert.ToByte(Char, 16)  

11. Encoding.UTF8.GetBytes(String); Convert.ToBase64String();Convert.FromBase64String; Encoding.UTF8.GetString.

