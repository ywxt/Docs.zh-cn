---
title: "各种 API"
author: rick-anderson
description: "本文档概述了 ASP.NET 核心数据保护 ISecret 接口。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/extensibility/misc-apis
ms.openlocfilehash: 88a08a25abf4c4e1ba0746087b05b1cc8fa13024
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="miscellaneous-apis"></a><span data-ttu-id="f8ecf-103">各种 API</span><span class="sxs-lookup"><span data-stu-id="f8ecf-103">Miscellaneous APIs</span></span>

<a name="data-protection-extensibility-mics-apis"></a>

>[!WARNING]
> <span data-ttu-id="f8ecf-104">实现的任意以下接口的类型应该是线程安全的多个调用方。</span><span class="sxs-lookup"><span data-stu-id="f8ecf-104">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="isecret"></a><span data-ttu-id="f8ecf-105">ISecret</span><span class="sxs-lookup"><span data-stu-id="f8ecf-105">ISecret</span></span>

<span data-ttu-id="f8ecf-106">`ISecret`接口表示一个机密的值，如加密的密钥材料。</span><span class="sxs-lookup"><span data-stu-id="f8ecf-106">The `ISecret` interface represents a secret value, such as cryptographic key material.</span></span> <span data-ttu-id="f8ecf-107">它包含以下 API 图面：</span><span class="sxs-lookup"><span data-stu-id="f8ecf-107">It contains the following API surface:</span></span>

* <span data-ttu-id="f8ecf-108">`Length`: `int`</span><span class="sxs-lookup"><span data-stu-id="f8ecf-108">`Length`: `int`</span></span>

* <span data-ttu-id="f8ecf-109">`Dispose()`: `void`</span><span class="sxs-lookup"><span data-stu-id="f8ecf-109">`Dispose()`: `void`</span></span>

* <span data-ttu-id="f8ecf-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span><span class="sxs-lookup"><span data-stu-id="f8ecf-110">`WriteSecretIntoBuffer(ArraySegment<byte> buffer)`: `void`</span></span>

<span data-ttu-id="f8ecf-111">`WriteSecretIntoBuffer`方法填充原始机密值与提供的缓冲区。</span><span class="sxs-lookup"><span data-stu-id="f8ecf-111">The `WriteSecretIntoBuffer` method populates the supplied buffer with the raw secret value.</span></span> <span data-ttu-id="f8ecf-112">此 API 将作为参数的缓冲区的原因而不返回`byte[]`直接是，这使调用方机会固定限制对托管的垃圾回收器的机密暴露该缓冲区对象。</span><span class="sxs-lookup"><span data-stu-id="f8ecf-112">The reason this API takes the buffer as a parameter rather than returning a `byte[]` directly is that this gives the caller the opportunity to pin the buffer object, limiting secret exposure to the managed garbage collector.</span></span>

<span data-ttu-id="f8ecf-113">`Secret`类型是的具体实现`ISecret`机密的值在进程中内存中的存储位置。</span><span class="sxs-lookup"><span data-stu-id="f8ecf-113">The `Secret` type is a concrete implementation of `ISecret` where the secret value is stored in in-process memory.</span></span> <span data-ttu-id="f8ecf-114">在 Windows 平台上的机密的值加密通过[CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8ecf-114">On Windows platforms, the secret value is encrypted via [CryptProtectMemory](https://msdn.microsoft.com/library/windows/desktop/aa380262(v=vs.85).aspx).</span></span>
