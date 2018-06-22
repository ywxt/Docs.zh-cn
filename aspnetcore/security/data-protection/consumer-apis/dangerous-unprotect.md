---
title: 取消保护已吊销在 ASP.NET 核心中键的有效负载
author: rick-anderson
description: 了解如何取消保护数据，使用密钥，因为已吊销，在 ASP.NET Core 应用程序保护。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/dangerous-unprotect
ms.openlocfilehash: ed0c2a309e899f018b09b3edc86b65b299647914
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272381"
---
# <a name="unprotect-payloads-whose-keys-have-been-revoked-in-aspnet-core"></a><span data-ttu-id="81e0f-103">取消保护已吊销在 ASP.NET 核心中键的有效负载</span><span class="sxs-lookup"><span data-stu-id="81e0f-103">Unprotect payloads whose keys have been revoked in ASP.NET Core</span></span>


<a name="data-protection-consumer-apis-dangerous-unprotect"></a>

<span data-ttu-id="81e0f-104">ASP.NET 核心数据保护 Api 主要不用于机密负载的无限期持久性。</span><span class="sxs-lookup"><span data-stu-id="81e0f-104">The ASP.NET Core data protection APIs are not primarily intended for indefinite persistence of confidential payloads.</span></span> <span data-ttu-id="81e0f-105">其他技术喜欢[Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx)和[Azure Rights Management](https://docs.microsoft.com/rights-management/)更适合于以下场景： 无限期存储，并且它们的相应强密钥管理功能。</span><span class="sxs-lookup"><span data-stu-id="81e0f-105">Other technologies like [Windows CNG DPAPI](https://msdn.microsoft.com/library/windows/desktop/hh706794%28v=vs.85%29.aspx) and [Azure Rights Management](https://docs.microsoft.com/rights-management/) are more suited to the scenario of indefinite storage, and they have correspondingly strong key management capabilities.</span></span> <span data-ttu-id="81e0f-106">也就是说，无需进行任何开发人员禁止使用 ASP.NET Core 数据保护 Api 进行长期保护的机密数据。</span><span class="sxs-lookup"><span data-stu-id="81e0f-106">That said, there's nothing prohibiting a developer from using the ASP.NET Core data protection APIs for long-term protection of confidential data.</span></span> <span data-ttu-id="81e0f-107">密钥绝不会移除从密钥链中，因此`IDataProtector.Unprotect`，只要键为可用，有效始终可以恢复现有的负载。</span><span class="sxs-lookup"><span data-stu-id="81e0f-107">Keys are never removed from the key ring, so `IDataProtector.Unprotect` can always recover existing payloads as long as the keys are available and valid.</span></span>

<span data-ttu-id="81e0f-108">但是，则会产生问题在开发人员尝试取消保护数据作为保护与吊销键，`IDataProtector.Unprotect`在这种情况下将引发异常。</span><span class="sxs-lookup"><span data-stu-id="81e0f-108">However, an issue arises when the developer tries to unprotect data that has been protected with a revoked key, as `IDataProtector.Unprotect` will throw an exception in this case.</span></span> <span data-ttu-id="81e0f-109">这些类型的负载可以轻松地重新创建这些系统，以及在坏的情况下站点访问者可能需要重新登录，这可能是特别适用于短期或临时负载 （如身份验证令牌） 的。</span><span class="sxs-lookup"><span data-stu-id="81e0f-109">This might be fine for short-lived or transient payloads (like authentication tokens), as these kinds of payloads can easily be recreated by the system, and at worst the site visitor might be required to log in again.</span></span> <span data-ttu-id="81e0f-110">但持久化负载，具有`Unprotect`抛出可能导致不可接受数据丢失。</span><span class="sxs-lookup"><span data-stu-id="81e0f-110">But for persisted payloads, having `Unprotect` throw could lead to unacceptable data loss.</span></span>

## <a name="ipersisteddataprotector"></a><span data-ttu-id="81e0f-111">IPersistedDataProtector</span><span class="sxs-lookup"><span data-stu-id="81e0f-111">IPersistedDataProtector</span></span>

<span data-ttu-id="81e0f-112">若要支持允许负载为即使在遇到吊销密钥时未受保护的方案，数据保护系统包含`IPersistedDataProtector`类型。</span><span class="sxs-lookup"><span data-stu-id="81e0f-112">To support the scenario of allowing payloads to be unprotected even in the face of revoked keys, the data protection system contains an `IPersistedDataProtector` type.</span></span> <span data-ttu-id="81e0f-113">若要获取其实例`IPersistedDataProtector`，只需获取其实例`IDataProtector`在正常情况和重试强制转换`IDataProtector`到`IPersistedDataProtector`。</span><span class="sxs-lookup"><span data-stu-id="81e0f-113">To get an instance of `IPersistedDataProtector`, simply get an instance of `IDataProtector` in the normal fashion and try casting the `IDataProtector` to `IPersistedDataProtector`.</span></span>

> [!NOTE]
> <span data-ttu-id="81e0f-114">并非所有`IDataProtector`实例可以强制转换为`IPersistedDataProtector`。</span><span class="sxs-lookup"><span data-stu-id="81e0f-114">Not all `IDataProtector` instances can be cast to `IPersistedDataProtector`.</span></span> <span data-ttu-id="81e0f-115">开发人员应使用 C# 作为运算符或类似以避免运行时异常导致通过无效强制转换，并且应在准备好正确地处理失败案例。</span><span class="sxs-lookup"><span data-stu-id="81e0f-115">Developers should use the C# as operator or similar to avoid runtime exceptions caused by invalid casts, and they should be prepared to handle the failure case appropriately.</span></span>

<span data-ttu-id="81e0f-116">`IPersistedDataProtector` 公开以下 API 图面：</span><span class="sxs-lookup"><span data-stu-id="81e0f-116">`IPersistedDataProtector` exposes the following API surface:</span></span>

```csharp
DangerousUnprotect(byte[] protectedData, bool ignoreRevocationErrors,
     out bool requiresMigration, out bool wasRevoked) : byte[]
```

<span data-ttu-id="81e0f-117">此 API 采用 （作为字节数组） 的受保护的负载，并返回未受保护的负载。</span><span class="sxs-lookup"><span data-stu-id="81e0f-117">This API takes the protected payload (as a byte array) and returns the unprotected payload.</span></span> <span data-ttu-id="81e0f-118">没有任何基于字符串的重载。</span><span class="sxs-lookup"><span data-stu-id="81e0f-118">There's no string-based overload.</span></span> <span data-ttu-id="81e0f-119">Out 参数的两个如下所示。</span><span class="sxs-lookup"><span data-stu-id="81e0f-119">The two out parameters are as follows.</span></span>

* <span data-ttu-id="81e0f-120">`requiresMigration`： 将设置为 true 时用于保护此负载密钥不再是活动默认密钥，例如，用于保护此负载的关键是旧，密钥滚动操作包含以来执行的位置。</span><span class="sxs-lookup"><span data-stu-id="81e0f-120">`requiresMigration`: will be set to true if the key used to protect this payload is no longer the active default key, e.g., the key used to protect this payload is old and a key rolling operation has since taken place.</span></span> <span data-ttu-id="81e0f-121">调用方可能想要考虑重新保护具体取决于其业务需求的负载。</span><span class="sxs-lookup"><span data-stu-id="81e0f-121">The caller may wish to consider reprotecting the payload depending on their business needs.</span></span>

* <span data-ttu-id="81e0f-122">`wasRevoked`： 将设置为 true 时用来保护此负载的密钥已被吊销。</span><span class="sxs-lookup"><span data-stu-id="81e0f-122">`wasRevoked`: will be set to true if the key used to protect this payload was revoked.</span></span>

>[!WARNING]
> <span data-ttu-id="81e0f-123">传递时应格外谨慎`ignoreRevocationErrors: true`到`DangerousUnprotect`方法。</span><span class="sxs-lookup"><span data-stu-id="81e0f-123">Exercise extreme caution when passing `ignoreRevocationErrors: true` to the `DangerousUnprotect` method.</span></span> <span data-ttu-id="81e0f-124">如果调用此方法后的`wasRevoked`值是为 true，则用来保护此负载的密钥已被吊销，并且负载的真实性应被视为可疑。</span><span class="sxs-lookup"><span data-stu-id="81e0f-124">If after calling this method the `wasRevoked` value is true, then the key used to protect this payload was revoked, and the payload's authenticity should be treated as suspect.</span></span> <span data-ttu-id="81e0f-125">在这种情况下，才继续操作操作系统上不受保护的负载，如果你具有一些单独的保障，它是可信的例如所来自的安全数据库，而不是由不受信任的 web 客户端发送。</span><span class="sxs-lookup"><span data-stu-id="81e0f-125">In this case, only continue operating on the unprotected payload if you have some separate assurance that it's authentic, e.g. that it's coming from a secure database rather than being sent by an untrusted web client.</span></span>

[!code-csharp[](dangerous-unprotect/samples/dangerous-unprotect.cs)]
