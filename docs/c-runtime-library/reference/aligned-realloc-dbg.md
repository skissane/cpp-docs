---
description: "Learn more about: _aligned_realloc_dbg"
title: "_aligned_realloc_dbg"
ms.date: "11/04/2016"
api_name: ["_aligned_realloc_dbg"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["aligned_realloc_dbg", "_aligned_realloc_dbg"]
helpviewer_keywords: ["_aligned_realloc_dbg function", "aligned_realloc_dbg function"]
ms.assetid: 8aede920-991e-44cd-867f-83dc2165db47
---
# _aligned_realloc_dbg

Changes the size of a memory block that was allocated with [`_aligned_malloc`](aligned-malloc.md) or [`_aligned_offset_malloc`](aligned-offset-malloc.md) (debug version only).

## Syntax

```C
void * _aligned_realloc_dbg(
   void *memblock,
   size_t size,
   size_t alignment,
   const char *filename,
   int linenumber
);
```

### Parameters

*`memblock`*\
The current memory block pointer.

*`size`*\
The size of the requested memory allocation.

*`alignment`*\
The alignment value, which must be an integer power of 2.

*`filename`*\
Pointer to the name of the source file that requested the **realloc** operation or **NULL**.

*`linenumber`*\
Line number in the source file where the **realloc** operation was requested or **NULL**.

## Return value

**_aligned_realloc_dbg** returns a void pointer to the reallocated (and possibly moved) memory block. The return value is **NULL** if the size is zero and the buffer argument isn't **NULL**, or if there isn't enough available memory to expand the block to the given size. In the first case, the original block is freed. In the second, the original block is unchanged. The return value points to a storage space that is suitably aligned for storage of any type of object. To get a pointer to a type other than void, use a type cast on the return value.

It's an error to reallocate memory and change the alignment of a block.

## Remarks

**_aligned_realloc_dbg** is a debug version of the [`_aligned_realloc`](aligned-realloc.md) function. When [`_DEBUG`](../debug.md) isn't defined, each call to **_aligned_realloc_dbg** is reduced to a call to **_aligned_realloc**. Both **_aligned_realloc** and **_aligned_realloc_dbg** reallocate a memory block in the base heap, but **_aligned_realloc_dbg** accommodates several debugging features: buffers on either side of the user portion of the block to test for leaks, and *`filename`*/*`linenumber`* information to determine the origin of allocation requests. Tracking specific allocation types with a block type parameter isn't a supported debug feature for aligned allocations. Aligned allocations will appear as a `_NORMAL_BLOCK` block type.

**_aligned_realloc_dbg** reallocates the specified memory block with slightly more space than the requested *`newSize`*. *`newSize`* might be greater or less than the size of the originally allocated memory block. The extra space is used by the debug heap manager to link the debug memory blocks and to provide the application with debug header information and overwrite buffers. The reallocation might both move the original memory block to a different location in the heap, and change the size of the memory block. If the memory block is moved, the contents of the original block are overwritten.

**_aligned_realloc_dbg** sets **errno** to **ENOMEM** if a memory allocation fails or if the amount of memory needed (including the overhead mentioned previously) exceeds **_HEAP_MAXREQ**. For information about this and other error codes, see [`errno`, `_doserrno`, `_sys_errlist`, and `_sys_nerr`](../errno-doserrno-sys-errlist-and-sys-nerr.md).

Also, **_aligned_realloc_dbg** validates its parameters. If *`alignment`* isn't a power of 2, this function invokes the invalid parameter handler, as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, this function returns **NULL** and sets **errno** to **EINVAL**.

For information about how memory blocks are allocated, initialized, and managed in the debug version of the base heap, see [CRT debug heap details](/visualstudio/debugger/crt-debug-heap-details). For information about the allocation block types and how they're used, see [Types of blocks on the debug heap](/visualstudio/debugger/crt-debug-heap-details). For information about the differences between standard heap functions and their debug versions, see [Debug versions of heap allocation functions](/visualstudio/debugger/debug-versions-of-heap-allocation-functions).

## Requirements

|Routine|Required header|
|-------------|---------------------|
|**_aligned_realloc_dbg**|\<crtdbg.h>|

For more compatibility information, see [Compatibility](../compatibility.md).

## Libraries

Debug versions of [C run-time libraries](../crt-library-features.md) only.

## See also

[Debug routines](../debug-routines.md)
