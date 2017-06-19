---
title: CLR-VIA-Csharp-3
date: 2017-06-02 19:06:03
tags:
  - CLR
categories:
  - C#
---
> Introduce Strong Name Assembly
<!--more-->

1. A full qualified assembly name consists of four parts: name, version, culture, key.
2. Use the following commands to generate public/private key :
```
 # Create a public/private key pair
 SN -k MyCompany.snk
 # view public key
 SN -p MyCompany.snk MyCompany.PublicKey sha256
 SN -tp MyCompany.PublicKey 
```
The SN utility doesn't offer any way for you to display the private key.
```
 csc /keyfile:MyCompany.snk program.cs
```
 
3. By the way, the AssemblyDef entry always stores the full public key, not the public key token. The full public key is necessary to ensure that the file hasn’t been tampered with.
4. A strongly named assembly consists of four attributes that uniquely identify the assembly: a file name(without an extension), a version number, a culture identity, and a public key. Since public keys are very large numbers, we frequently use a small hash value derived from a public key.
5. If an assembly is to be accessed by multiple applications, the assembly must be placed into a well-known directory, and the CLR must know to look in this directory automatically when a reference to the assembly is detected. This well-known location is called the global assembly cache (GAC). We can find the directory by:
```
%SystemRoot%Microsoft.NET\Assembly

```
6. The GAC directory is structured, containing many subdirectories, and an algorithm is used to generate the names of these sub-directories. We should only install strongly named assembly using the tool GACUtil.exe.
7. Signing an assembly with a private key and embedding the signature and public key within an assembly allows the CLR to verify that the assembly has not been modified or corrupted.
8. Only check if assembly is tampered with in GAC when intalling, check every time the assembly is loaded when the assembly is not in GAC.
9. Use the following steps to delay sign and sign at final:
```
CSC /keyfile: MyCompany.PublicKey /delaysign MyAssembly.cs
Disable file integrity check by: 
SN.exe -Vr MyAssembly.dll
SN.exe -Ra MyAssembly.dll MyCompany.PrivateKey
SN.exe -Vu MyAssembly.dll
```

