---
title: 限制在 ASP.NET Core 的受保护负载的生存期
author: rick-anderson
description: 了解如何限制使用 ASP.NET Core 数据保护 Api 的受保护负载的生存期。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/consumer-apis/limited-lifetime-payloads
ms.openlocfilehash: 8dc3b856ec67477ec8ae777749c9bf3107eb4eda
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36278052"
---
# <a name="limit-the-lifetime-of-protected-payloads-in-aspnet-core"></a><span data-ttu-id="c5e84-103">限制在 ASP.NET Core 的受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="c5e84-103">Limit the lifetime of protected payloads in ASP.NET Core</span></span>

<span data-ttu-id="c5e84-104">有一些应用程序开发人员希望创建将在一段时间后过期的受保护的负载的情形。</span><span class="sxs-lookup"><span data-stu-id="c5e84-104">There are scenarios where the application developer wants to create a protected payload that expires after a set period of time.</span></span> <span data-ttu-id="c5e84-105">例如，受保护的负载可能表示只应为有效一小时的密码重置令牌。</span><span class="sxs-lookup"><span data-stu-id="c5e84-105">For instance, the protected payload might represent a password reset token that should only be valid for one hour.</span></span> <span data-ttu-id="c5e84-106">当然也可以为开发人员创建他们自己包含的嵌入的到期日期的负载格式和高级开发人员可能想要执行此操作，但对于开发人员的大多数管理这些过期时间可能变得需要很长时间。</span><span class="sxs-lookup"><span data-stu-id="c5e84-106">It's certainly possible for the developer to create their own payload format that contains an embedded expiration date, and advanced developers may wish to do this anyway, but for the majority of developers managing these expirations can grow tedious.</span></span>

<span data-ttu-id="c5e84-107">若要简化此过程对于我们的开发人员受众，包[Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/)用于创建在一段时间后自动过期的负载包含实用工具 Api。</span><span class="sxs-lookup"><span data-stu-id="c5e84-107">To make this easier for our developer audience, the package [Microsoft.AspNetCore.DataProtection.Extensions](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Extensions/) contains utility APIs for creating payloads that automatically expire after a set period of time.</span></span> <span data-ttu-id="c5e84-108">这些 Api 的挂起注销`ITimeLimitedDataProtector`类型。</span><span class="sxs-lookup"><span data-stu-id="c5e84-108">These APIs hang off of the `ITimeLimitedDataProtector` type.</span></span>

## <a name="api-usage"></a><span data-ttu-id="c5e84-109">API 使用情况</span><span class="sxs-lookup"><span data-stu-id="c5e84-109">API usage</span></span>

<span data-ttu-id="c5e84-110">`ITimeLimitedDataProtector`接口是用于保护和取消保护的限时 / 自即将到期的负载的核心接口。</span><span class="sxs-lookup"><span data-stu-id="c5e84-110">The `ITimeLimitedDataProtector` interface is the core interface for protecting and unprotecting time-limited / self-expiring payloads.</span></span> <span data-ttu-id="c5e84-111">若要创建的实例`ITimeLimitedDataProtector`，你需要先正则表达式的实例[IDataProtector](xref:security/data-protection/consumer-apis/overview)构造具有特定的用途。</span><span class="sxs-lookup"><span data-stu-id="c5e84-111">To create an instance of an `ITimeLimitedDataProtector`, you'll first need an instance of a regular [IDataProtector](xref:security/data-protection/consumer-apis/overview) constructed with a specific purpose.</span></span> <span data-ttu-id="c5e84-112">一次`IDataProtector`实例可用时，调用`IDataProtector.ToTimeLimitedDataProtector`扩展方法，能获得重新保护程序内置到期功能。</span><span class="sxs-lookup"><span data-stu-id="c5e84-112">Once the `IDataProtector` instance is available, call the `IDataProtector.ToTimeLimitedDataProtector` extension method to get back a protector with built-in expiration capabilities.</span></span>

<span data-ttu-id="c5e84-113">`ITimeLimitedDataProtector` 公开以下 API 图面和扩展方法：</span><span class="sxs-lookup"><span data-stu-id="c5e84-113">`ITimeLimitedDataProtector` exposes the following API surface and extension methods:</span></span>

* <span data-ttu-id="c5e84-114">CreateProtector （字符串目的）： ITimeLimitedDataProtector-此 API 已类似于现有`IDataProtectionProvider.CreateProtector`在于它可以用于创建[目的链](xref:security/data-protection/consumer-apis/purpose-strings)从根的限时保护程序。</span><span class="sxs-lookup"><span data-stu-id="c5e84-114">CreateProtector(string purpose) : ITimeLimitedDataProtector - This API is similar to the existing `IDataProtectionProvider.CreateProtector` in that it can be used to create [purpose chains](xref:security/data-protection/consumer-apis/purpose-strings) from a root time-limited protector.</span></span>

* <span data-ttu-id="c5e84-115">保护 （字节 [] 纯文本，DateTimeOffset 到期）： byte]</span><span class="sxs-lookup"><span data-stu-id="c5e84-115">Protect(byte[] plaintext, DateTimeOffset expiration) : byte[]</span></span>

* <span data-ttu-id="c5e84-116">保护 （字节 [] 纯文本、 TimeSpan 生存期）： byte]</span><span class="sxs-lookup"><span data-stu-id="c5e84-116">Protect(byte[] plaintext, TimeSpan lifetime) : byte[]</span></span>

* <span data-ttu-id="c5e84-117">保护 （字节 [] 纯文本）： byte]</span><span class="sxs-lookup"><span data-stu-id="c5e84-117">Protect(byte[] plaintext) : byte[]</span></span>

* <span data-ttu-id="c5e84-118">保护 （字符串纯文本，DateTimeOffset 到期）： 字符串</span><span class="sxs-lookup"><span data-stu-id="c5e84-118">Protect(string plaintext, DateTimeOffset expiration) : string</span></span>

* <span data-ttu-id="c5e84-119">保护 (TimeSpan 生存期中的字符串纯文本）： 字符串</span><span class="sxs-lookup"><span data-stu-id="c5e84-119">Protect(string plaintext, TimeSpan lifetime) : string</span></span>

* <span data-ttu-id="c5e84-120">保护 （字符串纯文本）： 字符串</span><span class="sxs-lookup"><span data-stu-id="c5e84-120">Protect(string plaintext) : string</span></span>

<span data-ttu-id="c5e84-121">除了核心`Protect`方法需要仅是纯文本形式，存在一些新重载允许指定的负载的到期日期。</span><span class="sxs-lookup"><span data-stu-id="c5e84-121">In addition to the core `Protect` methods which take only the plaintext, there are new overloads which allow specifying the payload's expiration date.</span></span> <span data-ttu-id="c5e84-122">到期日期可以指定为绝对日期 (通过`DateTimeOffset`) 或相对的时间 (从当前系统时间，通过`TimeSpan`)。</span><span class="sxs-lookup"><span data-stu-id="c5e84-122">The expiration date can be specified as an absolute date (via a `DateTimeOffset`) or as a relative time (from the current system time, via a `TimeSpan`).</span></span> <span data-ttu-id="c5e84-123">如果调用不带过期的重载，则负载假定为永远不会过期。</span><span class="sxs-lookup"><span data-stu-id="c5e84-123">If an overload which doesn't take an expiration is called, the payload is assumed never to expire.</span></span>

* <span data-ttu-id="c5e84-124">取消保护 (字节 [] protectedData，出 DateTimeOffset 到期): byte]</span><span class="sxs-lookup"><span data-stu-id="c5e84-124">Unprotect(byte[] protectedData, out DateTimeOffset expiration) : byte[]</span></span>

* <span data-ttu-id="c5e84-125">取消保护 (字节 [] protectedData): byte]</span><span class="sxs-lookup"><span data-stu-id="c5e84-125">Unprotect(byte[] protectedData) : byte[]</span></span>

* <span data-ttu-id="c5e84-126">取消保护 (出 DateTimeOffset 过期字符串 protectedData): 字符串</span><span class="sxs-lookup"><span data-stu-id="c5e84-126">Unprotect(string protectedData, out DateTimeOffset expiration) : string</span></span>

* <span data-ttu-id="c5e84-127">取消保护 (字符串 protectedData): 字符串</span><span class="sxs-lookup"><span data-stu-id="c5e84-127">Unprotect(string protectedData) : string</span></span>

<span data-ttu-id="c5e84-128">`Unprotect`方法返回原始的未受保护的数据。</span><span class="sxs-lookup"><span data-stu-id="c5e84-128">The `Unprotect` methods return the original unprotected data.</span></span> <span data-ttu-id="c5e84-129">如果尚未超过负载，绝对过期则返回为可选输出参数以及原始的未受保护数据。</span><span class="sxs-lookup"><span data-stu-id="c5e84-129">If the payload hasn't yet expired, the absolute expiration is returned as an optional out parameter along with the original unprotected data.</span></span> <span data-ttu-id="c5e84-130">如果负载已过期，则取消保护方法的所有重载将都引发 CryptographicException。</span><span class="sxs-lookup"><span data-stu-id="c5e84-130">If the payload is expired, all overloads of the Unprotect method will throw CryptographicException.</span></span>

>[!WARNING]
> <span data-ttu-id="c5e84-131">它具有不建议使用这些 Api 来保护需要长期或无限期暂留的负载。</span><span class="sxs-lookup"><span data-stu-id="c5e84-131">It's not advised to use these APIs to protect payloads which require long-term or indefinite persistence.</span></span> <span data-ttu-id="c5e84-132">"，我可以承受为要在一个月后永久性不可恢复的受保护负载？"</span><span class="sxs-lookup"><span data-stu-id="c5e84-132">"Can I afford for the protected payloads to be permanently unrecoverable after a month?"</span></span> <span data-ttu-id="c5e84-133">可用作一个很好的经验法则;如果问题的回答是没有然后开发人员应考虑备用 Api。</span><span class="sxs-lookup"><span data-stu-id="c5e84-133">can serve as a good rule of thumb; if the answer is no then developers should consider alternative APIs.</span></span>

<span data-ttu-id="c5e84-134">使用下面的示例[非 DI 代码路径](xref:security/data-protection/configuration/non-di-scenarios)用于实例化数据保护系统的。</span><span class="sxs-lookup"><span data-stu-id="c5e84-134">The sample below uses the [non-DI code paths](xref:security/data-protection/configuration/non-di-scenarios) for instantiating the data protection system.</span></span> <span data-ttu-id="c5e84-135">若要运行此示例，请确保先添加对 Microsoft.AspNetCore.DataProtection.Extensions 包的引用。</span><span class="sxs-lookup"><span data-stu-id="c5e84-135">To run this sample, ensure that you have first added a reference to the Microsoft.AspNetCore.DataProtection.Extensions package.</span></span>

[!code-csharp[](limited-lifetime-payloads/samples/limitedlifetimepayloads.cs)]
