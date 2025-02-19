---
description: "Learn more about: gcvt"
title: "gcvt"
ms.date: "12/16/2019"
api_name: ["gcvt"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["gcvt"]
helpviewer_keywords: ["gcvt function"]
ms.assetid: 913478fd-ef22-4dee-b558-ff2bd6d72f3d
---
# gcvt

The Microsoft-specific function name `gcvt` is a deprecated alias for the [`_gcvt`](gcvt.md) function. By default, it generates [Compiler warning (level 3) C4996](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md). The name is deprecated because it doesn't follow the Standard C rules for implementation-specific names. However, the function is still supported.

We recommend you use [`_gcvt`](gcvt.md) or the security-enhanced [`_gcvt_s`](gcvt-s.md) function instead. Or, you can continue to use this function name, and disable the warning. For more information, see [Turn off the warning](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md#turn-off-the-warning) and [POSIX function names](../../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md#posix-function-names).
