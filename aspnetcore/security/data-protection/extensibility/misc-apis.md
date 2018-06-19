---
title: 杂项 ASP.NET 核心数据保护 Api
author: rick-anderson
description: 了解有关 ASP.NET 核心数据保护 ISecret 接口。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 484c6a0979a10e7cf2b801873655caa99a42532c
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
ms.locfileid: "30072759"
---
# <a name="miscellaneous-aspnet-core-data-protection-apis"></a><span data-ttu-id="c2446-103">杂项 ASP.NET 核心数据保护 Api</span><span class="sxs-lookup"><span data-stu-id="c2446-103">Miscellaneous ASP.NET Core Data Protection APIs</span></span>

<a name="data-protection-extensibility-mics-apis"></a>

>[!WARNING]
> <span data-ttu-id="c2446-104">实现的任意以下接口的类型应该是线程安全的多个调用方。</span><span class="sxs-lookup"><span data-stu-id="c2446-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="isecret"></a><span data-ttu-id="c2446-105">ISecret</span><span class="sxs-lookup"><span data-stu-id="c2446-105">ISecret</span></span>

<span data-ttu-id="c2446-106">`ISecret`接口表示一个机密的值，如加密的密钥材料。</span><span class="sxs-lookup"><span data-stu-id="c2446-106">The `ISecret` interface represents a secret value, such as cryptographic key material.</span></span> <span data-ttu-id="c2446-107">它包含以下 API 图面：</span><span class="sxs-lookup"><span data-stu-id="c2446-107">It contains the following API surface:</span></span>

* <span data-ttu-id="c2446-108">`Length`: `int`</span><span class="sxs-lookup"><span data-stu-id="c2446-108">`Length`: `int`</span></span>

* <span data-ttu-id="c2446-109">`Dispose()`: `void`</span><span class="sxs-lookup"><span data-stu-id="c2446-109">`Dispose()`: `void`</span></span>

* <span data-ttu-id="c2446-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span><span class="sxs-lookup"><span data-stu-id="c2446-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span></span>

<span data-ttu-id="c2446-111">`WriteSecretIntoBuffer`方法填充原始机密值与提供的缓冲区。</span><span class="sxs-lookup"><span data-stu-id="c2446-111">The `WriteSecretIntoBuffer` method populates the supplied buffer with the raw secret value.</span></span> <span data-ttu-id="c2446-112">此 API 将作为参数的缓冲区的原因而不返回`byte[]`直接是，这使调用方机会固定限制对托管的垃圾回收器的机密暴露该缓冲区对象。</span><span class="sxs-lookup"><span data-stu-id="c2446-112">The reason this API takes the buffer as a parameter rather than returning a `byte[]` directly is that this gives the caller the opportunity to pin the buffer object, limiting secret exposure to the managed garbage collector.</span></span>

<span data-ttu-id="c2446-113">`Secret`类型是的具体实现`ISecret`机密的值在进程中内存中的存储位置。</span><span class="sxs-lookup"><span data-stu-id="c2446-113">The `Secret` type is a concrete implementation of `ISecret` where the secret value is stored in in-process memory.</span></span> <span data-ttu-id="c2446-114">在 Windows 平台上的机密的值加密通过[CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c2446-114">On Windows platforms, the secret value is encrypted via [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span></span>
