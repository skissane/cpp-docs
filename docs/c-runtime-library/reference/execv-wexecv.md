---
description: "Learn more about: _execv, _wexecv"
title: "_execv, _wexecv"
ms.date: "4/2/2020"
api_name: ["_wexecv", "_execv", "_o__execv", "_o__wexecv"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll", "api-ms-win-crt-process-l1-1-0.dll", "api-ms-win-crt-private-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["_execv", "_wexecv", "wexecv"]
helpviewer_keywords: ["_wexecv function", "_execv function", "wexecv function", "execv function"]
ms.assetid: 8dbaf7bc-9040-4316-a0c1-db7e866b52af
---
# _execv, _wexecv

Loads and executes new child processes.

> [!IMPORTANT]
> This API cannot be used in applications that execute in the Windows Runtime. For more information, see [CRT functions not supported in Universal Windows Platform apps](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## Syntax

```C
intptr_t _execv(
   const char *cmdname,
   const char *const *argv
);
intptr_t _wexecv(
   const wchar_t *cmdname,
   const wchar_t *const *argv
);
```

### Parameters

*`cmdname`*\
Path of the file to execute.

*`argv`*\
Array of pointers to parameters.

## Return value

If successful, these functions don't return to the calling process. A return value of -1 indicates an error, in which case the **errno** global variable is set.

|**errno** value|Description|
|-------------------|-----------------|
|**E2BIG**|The space required for the arguments and environment settings exceeds 32 KB.|
|**EACCES**|The specified file has a locking or sharing violation.|
|**EINVAL**|Invalid parameter.|
|**EMFILE**|Too many files open (the specified file must be opened to determine whether it's executable).|
|**ENOENT**|The file or path not found.|
|**ENOEXEC**|The specified file isn't executable or has an invalid executable-file format.|
|**ENOMEM**|Not enough memory is available to execute the new process; the available memory has been corrupted; or an invalid block exists, indicating that the calling process wasn't allocated properly.|

For more information about these and other return codes, see [`errno`, `_doserrno`, `_sys_errlist`, and `_sys_nerr`](../errno-doserrno-sys-errlist-and-sys-nerr.md).

## Remarks

Each of these functions loads and executes a new process, passing an array of pointers to command-line arguments.

The **_execv** functions validate their parameters. If *`cmdname`* is a null pointer, or if *`argv`* is a null pointer, pointer to an empty array, or if the array contains an empty string as the first argument, the **_execv** functions invoke the invalid parameter handler as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, these functions set **errno** to **EINVAL** and return -1. No process is launched.

By default, this function's global state is scoped to the application. To change this behavior, see [Global state in the CRT](../global-state.md).

## Requirements

|Function|Required header|Optional header|
|--------------|---------------------|---------------------|
|**_execv**|\<process.h>|\<errno.h>|
|**_wexecv**|\<process.h> or \<wchar.h>|\<errno.h>|

For more compatibility information, see [Compatibility](../compatibility.md).

## Example

See the example in [`_exec`, `_wexec` functions](../exec-wexec-functions.md).

## See also

[Process and environment control](../process-and-environment-control.md)\
[`_exec`, `_wexec` functions](../exec-wexec-functions.md)\
[`abort`](abort.md)\
[`atexit`](atexit.md)\
[`exit`, `_Exit`, `_exit`](exit-exit-exit.md)\
[`_onexit`, `_onexit_m`](onexit-onexit-m.md)\
[`_spawn`, `_wspawn` functions](../spawn-wspawn-functions.md)\
[`system`, `_wsystem`](system-wsystem.md)
