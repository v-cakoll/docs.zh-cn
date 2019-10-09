---
title: 版本 2.2 到 3.0 的加密中断性变更 - .NET Core
description: 列出 .NET Core、ASP.NET Core 和 EF Core 的版本 2.2 到 3.0 的中断性变更。
ms.date: 09/10/2019
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 44caf042404d44ec4c5cb7b7e25883d8460efeb5
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216941"
---
# <a name="breaking-changes-for-migration-from-version-22-to-30"></a><span data-ttu-id="c5968-103">从版本 2.2 迁移到 3.0 的中断性变更</span><span class="sxs-lookup"><span data-stu-id="c5968-103">Breaking changes for migration from Version 2.2 to 3.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5968-104">本文正在构建中。</span><span class="sxs-lookup"><span data-stu-id="c5968-104">This article is under construction.</span></span> <span data-ttu-id="c5968-105">这并不是 .NET Core 中断性变更的完整列表。</span><span class="sxs-lookup"><span data-stu-id="c5968-105">This is not a complete list of .NET Core breaking changes.</span></span> <span data-ttu-id="c5968-106">如需详细了解 .NET Core 重大变更，请参阅 GitHub 上 dotnet/docs 存储库中的各个[重大变更问题](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Abreaking-change)。</span><span class="sxs-lookup"><span data-stu-id="c5968-106">For more information on .NET Core breaking changes, you can examine individual [breaking changes issues](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Abreaking-change) in the dotnet/docs repository on GitHub.</span></span> 

<span data-ttu-id="c5968-107">若要从 .NET Core、ASP.NET Core 或 EF Core 的版本 2.2 迁移至 3.0，请参阅以下主题，了解可能影响应用的中断性变更：</span><span class="sxs-lookup"><span data-stu-id="c5968-107">If you are migrating from version 2.2 to version 3.0 of .NET Core, ASP.NET Core, or EF Core, review the following topics for breaking changes that may affect your app:</span></span>

## <a name="corefx"></a><span data-ttu-id="c5968-108">CoreFx</span><span class="sxs-lookup"><span data-stu-id="c5968-108">CoreFx</span></span>

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/floating-point-changes.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/ziparchiveentry-and-inconsistent-entry-sizes.md)]

## <a name="cryptography"></a><span data-ttu-id="c5968-109">密码</span><span class="sxs-lookup"><span data-stu-id="c5968-109">Cryptography</span></span>

[!INCLUDE[EnvelopedCms defaults to AES-256 encryption](~/includes/core-changes/cryptography/envelopedcms-defaults-to-aes256.md)]

***

[!INCLUDE[Minimum size for RSAOpenSsl key generation has increased](~/includes/core-changes/cryptography/minimum-rsaopenssl-key-size-change.md)]

***

[!INCLUDE[.NET Core 3.0 prefers OpenSSL 1.1.x to OpenSSL 1.0.x](~/includes/core-changes/cryptography/net-core-3-0-prefers-openssl-1-1-x.md)]

## <a name="globalization"></a><span data-ttu-id="c5968-110">全球化</span><span class="sxs-lookup"><span data-stu-id="c5968-110">Globalization</span></span>

[!INCLUDE["C" locale maps to the invariant locale](~/includes/core-changes/globalization/c-locale-maps-to-invariant-locale.md)]

## <a name="visual-basic"></a><span data-ttu-id="c5968-111">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="c5968-111">Visual Basic</span></span>

[!INCLUDE[vbNewLine is obsolete](~/includes/core-changes/visualbasic/vbnewline-is-obsolete.md)]

## <a name="entity-framework-core"></a><span data-ttu-id="c5968-112">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="c5968-112">Entity Framework Core</span></span>

[<span data-ttu-id="c5968-113">Entity Framework Core 重大变更</span><span class="sxs-lookup"><span data-stu-id="c5968-113">Entity Framework Core breaking changes</span></span>](/ef/core/what-is-new/ef-core-3.0/breaking-changes)