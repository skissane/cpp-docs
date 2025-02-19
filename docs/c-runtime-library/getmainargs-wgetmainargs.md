---
description: "Learn more about: __getmainargs, __wgetmainargs"
title: "__getmainargs, __wgetmainargs"
ms.date: "11/04/2016"
api_name: ["__wgetmainargs", "__getmainargs"]
api_location: ["msvcr100.dll", "msvcrt.dll", "msvcr110_clr0400.dll", "msvcr80.dll", "msvcr110.dll", "msvcr90.dll", "msvcr120.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["__wgetmainargs", "__getmainargs"]
helpviewer_keywords: ["__wgetmainargs", "__getmainargs"]
ms.assetid: f72f54eb-9509-4bdf-8752-40fc49055439
---
# __getmainargs, __wgetmainargs

Invokes command-line parsing and copies the arguments to `main()` back through the passed pointers.

## Syntax

```cpp
int __getmainargs(
    int * argc,
   char *** argv,
   char *** env,
   int doWildCard,
_startupinfo * startInfo);

int __wgetmainargs (
   int *argc,
   wchar_t ***argv,
   wchar_t ***env,
   int doWildCard,
   _startupinfo * startInfo)
```

#### Parameters

*`argc`*\
An integer that contains the number of arguments that follow in `argv`. The `argc` parameter is always greater than or equal to 1.

*`argv`*\
An array of null-terminated strings representing command-line arguments entered by the user of the program. By convention, `argv[0]` is the command with which the program is invoked, argv[1] is the first command-line argument, and so on, until argv[argc], which is always **NULL**. The first command-line argument is always `argv[1]` and the last one is `argv[argc - 1]`.

*`env`*\
An array of strings that represent the variables set in the user's environment. This array is terminated by a **NULL** entry.

*`doWildCard`*\
An integer that if set to 1 expands the wildcards in the command line arguments, or if set to 0 does nothing.

*`startInfo`*\
Other information to be passed to the CRT DLL.

## Return value

0 if successful; a negative value if unsuccessful.

## Remarks

Use `__getmainargs` on non-wide character platforms, and `__wgetmainargs` on wide-character (Unicode) platforms.

## Requirements

|Routine|Required header|
|-------------|---------------------|
|__getmainargs|internal.h|
|__wgetmainargs|internal.h|
