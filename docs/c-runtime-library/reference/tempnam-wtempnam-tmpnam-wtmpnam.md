---
description: "Learn more about: _tempnam, _wtempnam, tmpnam, _wtmpnam"
title: "_tempnam, _wtempnam, tmpnam, _wtmpnam"
ms.date: "11/04/2016"
api_name: ["_wtempnam", "_wtmpnam", "tmpnam", "_tempnam"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll", "api-ms-win-crt-stdio-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["wtempnam", "_wtmpnam", "wtmpnam", "tmpnam", "_wtempnam", "_tempnam"]
helpviewer_keywords: ["wtempnam function", "file names [C++], creating temporary", "_tempnam function", "ttmpnam function", "tmpnam function", "tempnam function", "wtmpnam function", "temporary files, creating", "file names [C++], temporary", "_ttmpnam function", "_wtmpnam function", "_wtempnam function"]
ms.assetid: 3ce75f0f-5e30-42a6-9791-8d7cbfe70fca
---
# _tempnam, _wtempnam, tmpnam, _wtmpnam

Generate names you can use to create temporary files. More secure versions of some of these functions are available; see [`tmpnam_s`, `_wtmpnam_s`](tmpnam-s-wtmpnam-s.md).

## Syntax

```C
char *_tempnam(
   const char *dir,
   const char *prefix
);
wchar_t *_wtempnam(
   const wchar_t *dir,
   const wchar_t *prefix
);
char *tmpnam(
   char *str
);
wchar_t *_wtmpnam(
   wchar_t *str
);
```

### Parameters

*`prefix`*\
The string that will be pre-pended to names returned by **_tempnam**.

*`dir`*\
The path used in the file name if there is no TMP environment variable, or if TMP is not a valid directory.

*`str`*\
Pointer that will hold the generated name and will be identical to the name returned by the function. This is a convenient way to save the generated name.

## Return value

Each of these functions returns a pointer to the name generated or **NULL** if there is a failure. Failure can occur if you attempt more than **TMP_MAX** (see STDIO.H) calls with **tmpnam** or if you use **_tempnam** and there is an invalid directory name specified in the TMP environment variable and in the *`dir`* parameter.

> [!NOTE]
> The pointers returned by **tmpnam** and **_wtmpnam** point to internal static buffers. [`free`](free.md) should not be called to deallocate those pointers. **free** needs to be called for pointers allocated by **_tempnam** and **_wtempnam**.

## Remarks

Each of these functions returns the name of a file that does not currently exist. **tmpnam** returns a name that's unique in the designated Windows temporary directory returned by [GetTempPathW](/windows/win32/api/fileapi/nf-fileapi-gettemppathw). **\_tempnam** generates a unique name in a directory other than the designated one. Note than when a file name is pre-pended with a backslash and no path information, such as \fname21, this indicates that the name is valid for the current working directory.

For **tmpnam**, you can store this generated file name in *`str`*. If *`str`* is **NULL**, then **tmpnam** leaves the result in an internal static buffer. Thus any subsequent calls destroy this value. The name generated by **tmpnam** consists of a program-generated file name and, after the first call to **tmpnam**, a file extension of sequential numbers in base 32 (.1-.vvu, when **TMP_MAX** in STDIO.H is 32,767).

**_tempnam** will generate a unique file name for a directory chosen by the following rules:

- If the TMP environment variable is defined and set to a valid directory name, unique file names will be generated for the directory specified by TMP.

- If the TMP environment variable is not defined or if it is set to the name of a directory that does not exist, **_tempnam** will use the *`dir`* parameter as the path for which it will generate unique names.

- If the TMP environment variable is not defined or if it is set to the name of a directory that does not exist, and if *`dir`* is either **NULL** or set to the name of a directory that does not exist, **_tempnam** will use the current working directory to generate unique names. Currently, if both TMP and *`dir`* specify names of directories that do not exist, the **_tempnam** function call will fail.

The name returned by **_tempnam** will be a concatenation of *`prefix`* and a sequential number, which will combine to create a unique file name for the specified directory. **_tempnam** generates file names that have no extension. **_tempnam** uses [`malloc`](malloc.md) to allocate space for the filename; the program is responsible for freeing this space when it is no longer needed.

**_tempnam** and **tmpnam** automatically handle multibyte-character string arguments as appropriate, recognizing multibyte-character sequences according to the OEM code page obtained from the operating system. **_wtempnam** is a wide-character version of **_tempnam**; the arguments and return value of **_wtempnam** are wide-character strings. **_wtempnam** and **_tempnam** behave identically except that **_wtempnam** does not handle multibyte-character strings. **_wtmpnam** is a wide-character version of **tmpnam**; the argument and return value of **_wtmpnam** are wide-character strings. **_wtmpnam** and **tmpnam** behave identically except that **_wtmpnam** does not handle multibyte-character strings.

If **_DEBUG** and **_CRTDBG_MAP_ALLOC** are defined, **_tempnam** and **_wtempnam** are replaced by calls to [`_tempnam_dbg` and `_wtempnam_dbg`](tempnam-dbg-wtempnam-dbg.md).

### Generic-text routine mappings

|TCHAR.H routine|_UNICODE & _MBCS not defined|_MBCS defined|_UNICODE defined|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_ttmpnam**|**tmpnam**|**tmpnam**|**_wtmpnam**|
|**_ttempnam**|**_tempnam**|**_tempnam**|**_wtempnam**|

## Requirements

|Routine|Required header|
|-------------|---------------------|
|**_tempnam**|\<stdio.h>|
|**_wtempnam**, **_wtmpnam**|\<stdio.h> or \<wchar.h>|
|**tmpnam**|\<stdio.h>|

For more compatibility information, see [Compatibility](../compatibility.md).

## Example

```C
// crt_tempnam.c
// compile with: /W3
// This program uses tmpnam to create a unique filename in the
// temporary directory, and _tempname to create a unique filename
// in C:\\tmp.

#include <stdio.h>
#include <stdlib.h>

int main(void)
{
   char * name1 = NULL;
   char * name2 = NULL;
   char * name3 = NULL;

   // Create a temporary filename for the current working directory:
   if ((name1 = tmpnam(NULL)) != NULL) { // C4996
   // Note: tmpnam is deprecated; consider using tmpnam_s instead
      printf("%s is safe to use as a temporary file.\n", name1);
   } else {
      printf("Cannot create a unique filename\n");
   }

   // Create a temporary filename in temporary directory with the
   // prefix "stq". The actual destination directory may vary
   // depending on the state of the TMP environment variable and
   // the global variable P_tmpdir.

   if ((name2 = _tempnam("c:\\tmp", "stq")) != NULL) {
      printf("%s is safe to use as a temporary file.\n", name2);
   } else {
      printf("Cannot create a unique filename\n");
   }

   // When name2 is no longer needed:
   if (name2) {
      free(name2);
   }

   // Unset TMP environment variable, then create a temporary filename in C:\tmp.
   if (_putenv("TMP=") != 0) {
      printf("Could not remove TMP environment variable.\n");
   }

   // With TMP unset, we will use C:\tmp as the temporary directory.
   // Create a temporary filename in C:\tmp with prefix "stq".
   if ((name3 = _tempnam("c:\\tmp", "stq")) != NULL) {
      printf("%s is safe to use as a temporary file.\n", name3);
   }
   else {
      printf("Cannot create a unique filename\n");
   }

   // When name3 is no longer needed:
   if (name3) {
      free(name3);
   }

   return 0;
}
```

```Output
C:\Users\LocalUser\AppData\Local\Temp\sriw.0 is safe to use as a temporary file.
C:\Users\LocalUser\AppData\Local\Temp\stq2 is safe to use as a temporary file.
c:\tmp\stq3 is safe to use as a temporary file.
```

## See also

[Stream I/O](../stream-i-o.md)\
[`_getmbcp`](getmbcp.md)\
[`malloc`](malloc.md)\
[`_setmbcp`](setmbcp.md)\
[`tmpfile`](tmpfile.md)\
[`tmpfile_s`](tmpfile-s.md)
