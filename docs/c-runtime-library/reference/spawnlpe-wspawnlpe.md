---
description: "Learn more about: _spawnlpe, _wspawnlpe"
title: "_spawnlpe, _wspawnlpe"
ms.date: "11/04/2016"
api_name: ["_spawnlpe", "_wspawnlpe"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll", "api-ms-win-crt-process-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["_wspawnlpe", "_spawnlpe", "wspawnlpe"]
helpviewer_keywords: ["_wspawnlpe function", "wspawnlpe function", "processes, creating", "spawnlpe function", "_spawnlpe function", "processes, executing new", "process creation"]
ms.assetid: e171ebfa-70e7-4c44-8331-2a291fc17bd6
---
# _spawnlpe, _wspawnlpe

Creates and executes a new process.

> [!IMPORTANT]
> This API cannot be used in applications that execute in the Windows Runtime. For more information, see [CRT functions not supported in Universal Windows Platform apps](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md).

## Syntax

```C
intptr_t _spawnlpe(
   int mode,
   const char *cmdname,
   const char *arg0,
   const char *arg1,
   ... const char *argn,
   NULL,
   const char *const *envp
);
intptr_t _wspawnlpe(
   int mode,
   const wchar_t *cmdname,
   const wchar_t *arg0,
   const wchar_t *arg1,
   ... const wchar_t *argn,
   NULL,
   const wchar_t *const *envp
);
```

### Parameters

*`mode`*\
Execution mode for the calling process.

*`cmdname`*\
Path of the file to be executed.

*`arg0`*, *`arg1`*, ... *`argN`*\
List of pointers to arguments. The *`arg0`* argument is typically a pointer to *`cmdname`*. The arguments *`arg1`* through *`argN`* are pointers to the character strings that form the new argument list. Following *`argN`*, there must be a **NULL** pointer to mark the end of the argument list.

*`envp`*\
Array of pointers to environment settings.

## Return value

The return value from a synchronous **_spawnlpe** or **_wspawnlpe** (**_P_WAIT** specified for *`mode`*) is the exit status of the new process. The return value from an asynchronous **_spawnlpe** or **_wspawnlpe** (**_P_NOWAIT** or **_P_NOWAITO** specified for *`mode`*) is the process handle. The exit status is 0 if the process terminated normally. You can set the exit status to a nonzero value if the spawned process specifically uses a nonzero argument to call the **exit** routine. If the new process did not explicitly set a positive exit status, a positive exit status indicates an abnormal exit caused by an abort or an interrupt. A return value of -1 indicates an error (the new process is not started). In this case, **errno** is set to one of the following values.

| Value | Description |
|-|-|
| **E2BIG** | Argument list exceeds 1024 bytes. |
| **EINVAL** | *`mode`* argument is invalid. |
| **ENOENT** | File or path is not found. |
| **ENOEXEC** | Specified file is not executable or has invalid executable-file format. |
| **ENOMEM** | Not enough memory is available to execute the new process. |

For more information about these and other return codes, see [`errno`, `_doserrno`, `_sys_errlist`, and `_sys_nerr`](../errno-doserrno-sys-errlist-and-sys-nerr.md).

## Remarks

Each of these functions creates and executes a new process, passes each command-line argument as a separate parameter, and passes an array of pointers to environment settings. These functions use the **PATH** environment variable to find the file to execute.

These functions validate their parameters. If either *`cmdname`* or *`arg0`* is an empty string or a null pointer, the invalid parameter handler is invoked, as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, these functions set **errno** to **EINVAL**, and return -1. No new process is spawned.

## Requirements

|Routine|Required header|
|-------------|---------------------|
|**_spawnlpe**|\<process.h>|
|**_wspawnlpe**|\<stdio.h> or \<wchar.h>|

For more compatibility information, see [Compatibility](../compatibility.md).

## Example

See the example in [`_spawn`, `_wspawn` functions](../spawn-wspawn-functions.md).

## See also

[Process and environment control](../process-and-environment-control.md)\
[`_spawn`, `_wspawn` functions](../spawn-wspawn-functions.md)\
[`abort`](abort.md)\
[`atexit`](atexit.md)\
[`_exec`, `_wexec` functions](../exec-wexec-functions.md)\
[`exit`, `_Exit`, `_exit`](exit-exit-exit.md)\
[`_flushall`](flushall.md)\
[`_getmbcp`](getmbcp.md)\
[`_onexit`, `_onexit_m`](onexit-onexit-m.md)\
[`_setmbcp`](setmbcp.md)\
[`system`, `_wsystem`](system-wsystem.md)
