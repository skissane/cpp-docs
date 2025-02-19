---
description: "Learn more about: unlink"
title: "unlink"
ms.date: "12/16/2019"
api_name: ["unlink"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["unlink"]
helpviewer_keywords: ["unlink function"]
ms.assetid: 2cd82055-5770-48be-88ee-4b2c70541c46
---
# unlink

The Microsoft-implemented POSIX function name `unlink` is a deprecated alias for the [`_unlink`](unlink-wunlink.md) function. By default, it generates [Compiler warning (level 3) C4996](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md). The name is deprecated because it doesn't follow the Standard C rules for implementation-specific names. However, the function is still supported.

We recommend you use [`_unlink`](unlink-wunlink.md) instead. Or, you can continue to use this function name, and disable the warning. For more information, see [Turn off the warning](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md#turn-off-the-warning) and [POSIX function names](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md#posix-function-names).
