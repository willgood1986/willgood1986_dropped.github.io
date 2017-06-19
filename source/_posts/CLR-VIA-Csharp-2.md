---
title: CLR-VIA-Csharp-2
date: 2017-06-02 18:39:39
tags:
  - CLR
Categories:
  - C#
    
---
> Introduce Assembly and configuration

<!--more-->


1. A managed PE file has four main parts: the PE32(+) header, the CLR header, the metadata, and the IL.
 - The PE32(+) header is the standard information what Windows expects.
 - The CLR header is a smalll block of information that is specific to modules that require the CLR (managed modules). The header includes the major and minor version number of the CLR that the module was built for: some flags, a MethodDef token indicating the module's entry point method if this module is a CUI, GUI or Windows Store executable, and an optional strong-name digital signature. Finally, the header contains the size and offsets of certain metadata tables contained within the module.** CLR header detailed format saw in IMAGE_COR20_HEADER in CorHdr.h header file **.
 - The metadata is a block of binary data that consists of several tables, including definition tables, reference tables, and manifest tables.
2. An assembly is a collection of one or more files containing type definitions and resource files. The CLR operates on assemblies; that is, the CLR always loads the file that contains the manifest metadata tables first and then uses the manifest to get the names of the other files that are in the assembly.
3. We can use ILDasm.exe to view internal detailed information.
4. You configure an application to download assembly files by specifying a ** CodeBase ** element identifies a URL pointing to where all of an assembly's files can be found. When attempting to load an assembly's file, the CLR obtains the ** CodeBase ** element's URL and checks the machine's download cache to see if the file is present. If it is, the file is loaded. If the file isn't in the cache, the CLR downloads the file into the cache from the location the URL points to. If the file can't be found, the CLR throws a FileNotFoundException exception at runtime.
5. The assembly file that contains the manifest also has an AssemblyRef table in it. This table contains an entry for all of the assemblies referenced by all of the assembly's files.
6. An application can control its directory and its subdirectories but has no control over other directories.We can put some files in subdirecotr, and configure them properly. And we can add a block in the application configuration file(The value of privatePath can be multiple semicolon-delimited paths):
```
<runtime>
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
<probing privatePath="AuxFiles" />
</assemblyBinding>
</runtime>
</configuration> 
```
7. CLR would atuomatically scan for a subdirectory whose name matches the name of the assembly being searched for.

