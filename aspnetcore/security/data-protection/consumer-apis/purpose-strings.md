---
title: 在 ASP.NET 核心目的字符串
author: rick-anderson
description: 了解如何在 ASP.NET 核心数据保护 Api 中使用目的字符串。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/consumer-apis/purpose-strings
ms.openlocfilehash: 8fe0020256d3a105b1968db693b0c667244957ec
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
ms.locfileid: "30077648"
---
# <a name="purpose-strings-in-aspnet-core"></a><span data-ttu-id="8901a-103">在 ASP.NET 核心目的字符串</span><span class="sxs-lookup"><span data-stu-id="8901a-103">Purpose strings in ASP.NET Core</span></span>

<a name="data-protection-consumer-apis-purposes"></a>

<span data-ttu-id="8901a-104">使用组件`IDataProtectionProvider`必须传递一个唯一*目的*参数`CreateProtector`方法。</span><span class="sxs-lookup"><span data-stu-id="8901a-104">Components which consume `IDataProtectionProvider` must pass a unique *purposes* parameter to the `CreateProtector` method.</span></span> <span data-ttu-id="8901a-105">目的*参数*是固有的数据保护系统中，安全的因为它提供了加密的使用者之间的隔离，即使根加密密钥是相同的。</span><span class="sxs-lookup"><span data-stu-id="8901a-105">The purposes *parameter* is inherent to the security of the data protection system, as it provides isolation between cryptographic consumers, even if the root cryptographic keys are the same.</span></span>

<span data-ttu-id="8901a-106">当使用者指定目的时，目的字符串用于以及根加密密钥派生加密子项唯一到该使用者。</span><span class="sxs-lookup"><span data-stu-id="8901a-106">When a consumer specifies a purpose, the purpose string is used along with the root cryptographic keys to derive cryptographic subkeys unique to that consumer.</span></span> <span data-ttu-id="8901a-107">这将隔离应用程序中其他加密使用者的使用者： 其他组件不能读取其有效负载，并且它无法读取任何其他组件的负载。</span><span class="sxs-lookup"><span data-stu-id="8901a-107">This isolates the consumer from all other cryptographic consumers in the application: no other component can read its payloads, and it cannot read any other component's payloads.</span></span> <span data-ttu-id="8901a-108">这种隔离还会呈现不可行的整个类别的针对组件的攻击。</span><span class="sxs-lookup"><span data-stu-id="8901a-108">This isolation also renders infeasible entire categories of attack against the component.</span></span>

![目的图示例](purpose-strings/_static/purposes.png)

<span data-ttu-id="8901a-110">在上图中，`IDataProtector`实例 A 和 B**无法**读取对方的负载，仅自己。</span><span class="sxs-lookup"><span data-stu-id="8901a-110">In the diagram above, `IDataProtector` instances A and B **cannot** read each other's payloads, only their own.</span></span>

<span data-ttu-id="8901a-111">目的字符串不一定是机密。</span><span class="sxs-lookup"><span data-stu-id="8901a-111">The purpose string doesn't have to be secret.</span></span> <span data-ttu-id="8901a-112">它只应是唯一其他任何功能良好组件不断将提供相同的目的字符串。</span><span class="sxs-lookup"><span data-stu-id="8901a-112">It should simply be unique in the sense that no other well-behaved component will ever provide the same purpose string.</span></span>

>[!TIP]
> <span data-ttu-id="8901a-113">使用该组件使用的数据保护 Api 的命名空间和类型名称是一个很好的经验法则，如下所示此信息将不会发生冲突的做法。</span><span class="sxs-lookup"><span data-stu-id="8901a-113">Using the namespace and type name of the component consuming the data protection APIs is a good rule of thumb, as in practice this information will never conflict.</span></span>
>
><span data-ttu-id="8901a-114">Contoso 编写的组件，它负责 minting 持有者令牌可能 Contoso.Security.BearerToken 用作其用途字符串。</span><span class="sxs-lookup"><span data-stu-id="8901a-114">A Contoso-authored component which is responsible for minting bearer tokens might use Contoso.Security.BearerToken as its purpose string.</span></span> <span data-ttu-id="8901a-115">或者-甚至更好地-它可能使用 Contoso.Security.BearerToken.v1 作为其用途字符串。</span><span class="sxs-lookup"><span data-stu-id="8901a-115">Or - even better - it might use Contoso.Security.BearerToken.v1 as its purpose string.</span></span> <span data-ttu-id="8901a-116">追加版本号，为将来的版本，以 Contoso.Security.BearerToken.v2 用作其用途，并且负载到位会完全独立于另一个不同的版本。</span><span class="sxs-lookup"><span data-stu-id="8901a-116">Appending the version number allows a future version to use Contoso.Security.BearerToken.v2 as its purpose, and the different versions would be completely isolated from one another as far as payloads go.</span></span>

<span data-ttu-id="8901a-117">由于目的参数`CreateProtector`是一个字符串数组，上述无法已改为指定为`[ "Contoso.Security.BearerToken", "v1" ]`。</span><span class="sxs-lookup"><span data-stu-id="8901a-117">Since the purposes parameter to `CreateProtector` is a string array, the above could've been instead specified as `[ "Contoso.Security.BearerToken", "v1" ]`.</span></span> <span data-ttu-id="8901a-118">这允许建立目的的层次结构，并打开与数据保护系统的多租户方案的可能性。</span><span class="sxs-lookup"><span data-stu-id="8901a-118">This allows establishing a hierarchy of purposes and opens up the possibility of multi-tenancy scenarios with the data protection system.</span></span>

<a name="data-protection-contoso-purpose"></a>

>[!WARNING]
> <span data-ttu-id="8901a-119">组件不应允许不受信任的用户输入要用于目的链的输入的唯一来源。</span><span class="sxs-lookup"><span data-stu-id="8901a-119">Components shouldn't allow untrusted user input to be the sole source of input for the purposes chain.</span></span>
>
><span data-ttu-id="8901a-120">例如，考虑 Contoso.Messaging.SecureMessage 负责存储安全消息的组件。</span><span class="sxs-lookup"><span data-stu-id="8901a-120">For example, consider a component Contoso.Messaging.SecureMessage which is responsible for storing secure messages.</span></span> <span data-ttu-id="8901a-121">如果安全消息的组件是为了调用`CreateProtector([ username ])`，则恶意用户可能创建的帐户用户名"Contoso.Security.BearerToken"在尝试获取要调用的组件`CreateProtector([ "Contoso.Security.BearerToken" ])`，从而无意中造成安全消息传送可以预见到身份验证令牌的 mint 负载的系统。</span><span class="sxs-lookup"><span data-stu-id="8901a-121">If the secure messaging component were to call `CreateProtector([ username ])`, then a malicious user might create an account with username "Contoso.Security.BearerToken" in an attempt to get the component to call `CreateProtector([ "Contoso.Security.BearerToken" ])`, thus inadvertently causing the secure messaging system to mint payloads that could be perceived as authentication tokens.</span></span>
>
><span data-ttu-id="8901a-122">将消息传递组件的更好目的链`CreateProtector([ "Contoso.Messaging.SecureMessage", "User: username" ])`，它提供适当的隔离。</span><span class="sxs-lookup"><span data-stu-id="8901a-122">A better purposes chain for the messaging component would be `CreateProtector([ "Contoso.Messaging.SecureMessage", "User: username" ])`, which provides proper isolation.</span></span>

<span data-ttu-id="8901a-123">通过提供隔离和行为`IDataProtectionProvider`， `IDataProtector`，和目的如下所示：</span><span class="sxs-lookup"><span data-stu-id="8901a-123">The isolation provided by and behaviors of `IDataProtectionProvider`, `IDataProtector`, and purposes are as follows:</span></span>

* <span data-ttu-id="8901a-124">为给定`IDataProtectionProvider`对象，`CreateProtector`方法将创建`IDataProtector`对象唯一绑定到同时`IDataProtectionProvider`对象创建它，并已传递到方法的目的参数。</span><span class="sxs-lookup"><span data-stu-id="8901a-124">For a given `IDataProtectionProvider` object, the `CreateProtector` method will create an `IDataProtector` object uniquely tied to both the `IDataProtectionProvider` object which created it and the purposes parameter which was passed into the method.</span></span>

* <span data-ttu-id="8901a-125">目的参数不得为空。</span><span class="sxs-lookup"><span data-stu-id="8901a-125">The purpose parameter must not be null.</span></span> <span data-ttu-id="8901a-126">（如果目的指定为一个数组，这意味着数组不能为零长度和数组的所有元素必须都为非 null。）非空字符串目的从技术上讲允许但不建议这样做。</span><span class="sxs-lookup"><span data-stu-id="8901a-126">(If purposes is specified as an array, this means that the array must not be of zero length and all elements of the array must be non-null.) An empty string purpose is technically allowed but is discouraged.</span></span>

* <span data-ttu-id="8901a-127">两个用途自变量是等效的当且仅当它们包含相同的字符串 （使用序号比较器） 中的顺序相同。</span><span class="sxs-lookup"><span data-stu-id="8901a-127">Two purposes arguments are equivalent if and only if they contain the same strings (using an ordinal comparer) in the same order.</span></span> <span data-ttu-id="8901a-128">单一用途参数等效于相应的单个元素目的数组。</span><span class="sxs-lookup"><span data-stu-id="8901a-128">A single purpose argument is equivalent to the corresponding single-element purposes array.</span></span>

* <span data-ttu-id="8901a-129">两个`IDataProtector`对象相等，当且仅当它们在创建等效项从`IDataProtectionProvider`对象，并且等效目的形参。</span><span class="sxs-lookup"><span data-stu-id="8901a-129">Two `IDataProtector` objects are equivalent if and only if they're created from equivalent `IDataProtectionProvider` objects with equivalent purposes parameters.</span></span>

* <span data-ttu-id="8901a-130">为给定`IDataProtector`对象、 调用`Unprotect(protectedData)`将返回原始`unprotectedData`当且仅当`protectedData := Protect(unprotectedData)`有关等效`IDataProtector`对象。</span><span class="sxs-lookup"><span data-stu-id="8901a-130">For a given `IDataProtector` object, a call to `Unprotect(protectedData)` will return the original `unprotectedData` if and only if `protectedData := Protect(unprotectedData)` for an equivalent `IDataProtector` object.</span></span>

> [!NOTE]
> <span data-ttu-id="8901a-131">我们不会考虑的如果某些组件有意选择已知与另一个组件发生冲突的目的字符串。</span><span class="sxs-lookup"><span data-stu-id="8901a-131">We're not considering the case where some component intentionally chooses a purpose string which is known to conflict with another component.</span></span> <span data-ttu-id="8901a-132">此类组件将考虑恶意内容，实质上是和此系统并不旨在中，恶意代码已在运行的工作进程内提供的安全保证。</span><span class="sxs-lookup"><span data-stu-id="8901a-132">Such a component would essentially be considered malicious, and this system isn't intended to provide security guarantees in the event that malicious code is already running inside of the worker process.</span></span>
