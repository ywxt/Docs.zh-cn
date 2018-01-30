---
title: "数据保护密钥管理和 ASP.NET Core 的生存时间"
author: rick-anderson
description: "了解有关数据保护密钥管理和 ASP.NET Core 的生存时间。"
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/configuration/default-settings
ms.openlocfilehash: b43c14af015d5e03f46200c51a1218a581b1de0c
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="data-protection-key-management-and-lifetime-in-aspnet-core"></a><span data-ttu-id="d3de4-103">数据保护密钥管理和 ASP.NET Core 的生存时间</span><span class="sxs-lookup"><span data-stu-id="d3de4-103">Data Protection key management and lifetime in ASP.NET Core</span></span>

<span data-ttu-id="d3de4-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d3de4-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="key-management"></a><span data-ttu-id="d3de4-105">密钥管理</span><span class="sxs-lookup"><span data-stu-id="d3de4-105">Key management</span></span>

<span data-ttu-id="d3de4-106">应用程序将尝试检测其操作环境并处理其自己的密钥配置。</span><span class="sxs-lookup"><span data-stu-id="d3de4-106">The app attempts to detect its operational environment and handle key configuration on its own.</span></span>

1. <span data-ttu-id="d3de4-107">如果应用程序承载于[Azure Apps](https://azure.microsoft.com/services/app-service/)，密钥保存到*%HOME%\ASP.NET\DataProtection-Keys*文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3de4-107">If the app is hosted in [Azure Apps](https://azure.microsoft.com/services/app-service/), keys are persisted to the *%HOME%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="d3de4-108">此文件夹由网络存储提供支持，并且在托管应用的所有计算机同步。</span><span class="sxs-lookup"><span data-stu-id="d3de4-108">This folder is backed by network storage and is synchronized across all machines hosting the app.</span></span>
   * <span data-ttu-id="d3de4-109">密钥未保护静止。</span><span class="sxs-lookup"><span data-stu-id="d3de4-109">Keys aren't protected at rest.</span></span>
   * <span data-ttu-id="d3de4-110">*数据保护密钥*文件夹提供密钥环在单个部署槽中的应用程序的所有实例。</span><span class="sxs-lookup"><span data-stu-id="d3de4-110">The *DataProtection-Keys* folder supplies the key ring to all instances of an app in a single deployment slot.</span></span>
   * <span data-ttu-id="d3de4-111">单独的部署槽，如过渡和生产环境，请不要共享密钥链。</span><span class="sxs-lookup"><span data-stu-id="d3de4-111">Separate deployment slots, such as Staging and Production, don't share a key ring.</span></span> <span data-ttu-id="d3de4-112">更换之间部署槽，如交换过渡到生产环境或使用 A / B 测试，使用数据保护任何应用将无法解密使用密钥链内前一槽的存储的数据。</span><span class="sxs-lookup"><span data-stu-id="d3de4-112">When you swap between deployment slots, for example swapping Staging to Production or using A/B testing, any app using Data Protection won't be able to decrypt stored data using the key ring inside the previous slot.</span></span> <span data-ttu-id="d3de4-113">这会导致对正在注销的应用程序使用标准的 ASP.NET Core cookie 身份验证，因为它使用数据保护来保护其 cookie 的用户。</span><span class="sxs-lookup"><span data-stu-id="d3de4-113">This leads to users being logged out of an app that uses the standard ASP.NET Core cookie authentication, as it uses Data Protection to protect its cookies.</span></span> <span data-ttu-id="d3de4-114">如果你需要独立于槽的密钥环，使用 Azure Blob 存储，Azure 密钥保管库，SQL 存储区中，之类的外部密钥环提供程序，或 Redis 缓存。</span><span class="sxs-lookup"><span data-stu-id="d3de4-114">If you desire slot-independent key rings, use an external key ring provider, such as Azure Blob Storage, Azure Key Vault, a SQL store, or Redis cache.</span></span>

1. <span data-ttu-id="d3de4-115">如果可用的用户配置文件，将密钥保存到*%LOCALAPPDATA%\ASP.NET\DataProtection-Keys*文件夹。</span><span class="sxs-lookup"><span data-stu-id="d3de4-115">If the user profile is available, keys are persisted to the *%LOCALAPPDATA%\ASP.NET\DataProtection-Keys* folder.</span></span> <span data-ttu-id="d3de4-116">如果操作系统是 Windows，密钥被加密使用 DPAPI 对静止。</span><span class="sxs-lookup"><span data-stu-id="d3de4-116">If the operating system is Windows, the keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="d3de4-117">如果应用程序托管在 IIS 中，密钥会保留到 HKLM 注册表仅对辅助进程帐户是 ACLed 某个特殊的注册表项中。</span><span class="sxs-lookup"><span data-stu-id="d3de4-117">If the app is hosted in IIS, keys are persisted to the HKLM registry in a special registry key that's ACLed only to the worker process account.</span></span> <span data-ttu-id="d3de4-118">使用 DPAPI 对密钥静态加密。</span><span class="sxs-lookup"><span data-stu-id="d3de4-118">Keys are encrypted at rest using DPAPI.</span></span>

1. <span data-ttu-id="d3de4-119">如果没有这些条件匹配，密钥不保留在当前进程之外。</span><span class="sxs-lookup"><span data-stu-id="d3de4-119">If none of these conditions match, keys aren't persisted outside of the current process.</span></span> <span data-ttu-id="d3de4-120">进程关闭时，生成所有密钥都都将丢失。</span><span class="sxs-lookup"><span data-stu-id="d3de4-120">When the process shuts down, all generated keys are lost.</span></span>

<span data-ttu-id="d3de4-121">开发人员可始终完全控制，并且可重写如何和密钥的存储位置。</span><span class="sxs-lookup"><span data-stu-id="d3de4-121">The developer is always in full control and can override how and where keys are stored.</span></span> <span data-ttu-id="d3de4-122">上面的前三个选项应提供很好的默认值对于大多数应用程序类似于如何 ASP.NET  **\<machineKey >**过去可以正常运行自动生成例程。</span><span class="sxs-lookup"><span data-stu-id="d3de4-122">The first three options above should provide good defaults for most apps similar to how the ASP.NET **\<machineKey>** auto-generation routines worked in the past.</span></span> <span data-ttu-id="d3de4-123">最终的回退选项是要求开发人员指定的唯一情形[配置](xref:security/data-protection/configuration/overview)前部如果他们想要密钥持久性，但此回退仅发生在极少数情况下。</span><span class="sxs-lookup"><span data-stu-id="d3de4-123">The final, fallback option is the only scenario that requires the developer to specify [configuration](xref:security/data-protection/configuration/overview) upfront if they want key persistence, but this fallback only occurs in rare situations.</span></span>

<span data-ttu-id="d3de4-124">当承载 Docker 容器中时，应是 （共享的卷或容器的生存期结束后仍然存在的主机装入的卷） 的 Docker 卷的文件夹中保留密钥或在外部提供程序，如[Azure 密钥保管库](https://azure.microsoft.com/services/key-vault/)或[Redis](https://redis.io/)。</span><span class="sxs-lookup"><span data-stu-id="d3de4-124">When hosting in a Docker container, keys should be persisted in a folder that's a Docker volume (a shared volume or a host-mounted volume that persists beyond the container's lifetime) or in an external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span> <span data-ttu-id="d3de4-125">如果应用程序不能访问共享的网络卷，可能也是在 web 场方案中有用外部提供程序 (请参阅[PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem)有关详细信息)。</span><span class="sxs-lookup"><span data-stu-id="d3de4-125">An external provider is also useful in web farm scenarios if apps can't access a shared network volume (see [PersistKeysToFileSystem](xref:security/data-protection/configuration/overview#persistkeystofilesystem) for more information).</span></span>

> [!WARNING]
> <span data-ttu-id="d3de4-126">如果开发人员重写上面所述的规则和点的特定的密钥存储库的数据保护系统，则会禁用自动加密对静止的密钥。</span><span class="sxs-lookup"><span data-stu-id="d3de4-126">If the developer overrides the rules outlined above and points the Data Protection system at a specific key repository, automatic encryption of keys at rest is disabled.</span></span> <span data-ttu-id="d3de4-127">在 rest 保护可能会通过重新启用[配置](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="d3de4-127">At-rest protection can be re-enabled via [configuration](xref:security/data-protection/configuration/overview).</span></span>

## <a name="key-lifetime"></a><span data-ttu-id="d3de4-128">密钥的生存期</span><span class="sxs-lookup"><span data-stu-id="d3de4-128">Key lifetime</span></span>

<span data-ttu-id="d3de4-129">默认情况下，密钥具有 90 天的生存期。</span><span class="sxs-lookup"><span data-stu-id="d3de4-129">Keys have a 90-day lifetime by default.</span></span> <span data-ttu-id="d3de4-130">密钥过期时，该应用将自动生成新密钥，并将新的密钥设置为活动密钥。</span><span class="sxs-lookup"><span data-stu-id="d3de4-130">When a key expires, the app automatically generates a new key and sets the new key as the active key.</span></span> <span data-ttu-id="d3de4-131">只要已停用的密钥保留在系统上，你的应用程序可以解密受保护的与之任何数据。</span><span class="sxs-lookup"><span data-stu-id="d3de4-131">As long as retired keys remain on the system, your app can decrypt any data protected with them.</span></span> <span data-ttu-id="d3de4-132">请参阅[密钥管理](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="d3de4-132">See [key management](xref:security/data-protection/implementation/key-management#key-expiration-and-rolling) for more information.</span></span>

## <a name="default-algorithms"></a><span data-ttu-id="d3de4-133">默认的算法</span><span class="sxs-lookup"><span data-stu-id="d3de4-133">Default algorithms</span></span>

<span data-ttu-id="d3de4-134">使用的默认负载保护算法是 AES 256 CBC 机密性和 HMACSHA256 真实性。</span><span class="sxs-lookup"><span data-stu-id="d3de4-134">The default payload protection algorithm used is AES-256-CBC for confidentiality and HMACSHA256 for authenticity.</span></span> <span data-ttu-id="d3de4-135">512 位主密钥，每隔 90 天更改一次用于派生用于每个负载基于这些算法的两个子键。</span><span class="sxs-lookup"><span data-stu-id="d3de4-135">A 512-bit master key, changed every 90 days, is used to derive the two sub-keys used for these algorithms on a per-payload basis.</span></span> <span data-ttu-id="d3de4-136">请参阅[子项派生](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="d3de4-136">See [subkey derivation](xref:security/data-protection/implementation/subkeyderivation#additional-authenticated-data-and-subkey-derivation) for more information.</span></span>

## <a name="see-also"></a><span data-ttu-id="d3de4-137">请参阅</span><span class="sxs-lookup"><span data-stu-id="d3de4-137">See also</span></span>

* [<span data-ttu-id="d3de4-138">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="d3de4-138">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)
