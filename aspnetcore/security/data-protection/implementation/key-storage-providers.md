---
title: 在 ASP.NET Core 中的密钥存储提供程序
author: rick-anderson
description: 了解有关 ASP.NET Core 以及如何配置密钥的存储位置中的密钥存储提供程序。
ms.author: riande
ms.date: 07/16/2018
uid: security/data-protection/implementation/key-storage-providers
ms.openlocfilehash: 74d62e88b40cfcefb81d699a5aba2665c56ac51a
ms.sourcegitcommit: 8f8924ce4eb9effeaf489f177fb01b66867da16f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2018
ms.locfileid: "39219259"
---
# <a name="key-storage-providers-in-aspnet-core"></a><span data-ttu-id="a22ea-103">在 ASP.NET Core 中的密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="a22ea-103">Key storage providers in ASP.NET Core</span></span>

<span data-ttu-id="a22ea-104">数据保护系统[默认情况下使用的发现机制](xref:security/data-protection/configuration/default-settings)来确定应该保留加密密钥的位置。</span><span class="sxs-lookup"><span data-stu-id="a22ea-104">The data protection system [employs a discovery mechanism by default](xref:security/data-protection/configuration/default-settings) to determine where cryptographic keys should be persisted.</span></span> <span data-ttu-id="a22ea-105">开发人员可以重写默认的发现机制，并手动指定的位置。</span><span class="sxs-lookup"><span data-stu-id="a22ea-105">The developer can override the default discovery mechanism and manually specify the location.</span></span>

> [!WARNING]
> <span data-ttu-id="a22ea-106">如果指定了显式密钥持久性位置，数据保护系统注销 rest 机制，在默认密钥加密，因此不再静态加密密钥。</span><span class="sxs-lookup"><span data-stu-id="a22ea-106">If you specify an explicit key persistence location, the data protection system deregisters the default key encryption at rest mechanism, so keys are no longer encrypted at rest.</span></span> <span data-ttu-id="a22ea-107">我们建议你此外[指定一个显式的密钥加密机制](xref:security/data-protection/implementation/key-encryption-at-rest)对于生产部署。</span><span class="sxs-lookup"><span data-stu-id="a22ea-107">It's recommended that you additionally [specify an explicit key encryption mechanism](xref:security/data-protection/implementation/key-encryption-at-rest) for production deployments.</span></span>

## <a name="file-system"></a><span data-ttu-id="a22ea-108">文件系统</span><span class="sxs-lookup"><span data-stu-id="a22ea-108">File system</span></span>

<span data-ttu-id="a22ea-109">若要配置的文件基于系统的密钥存储库，请调用[PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem)配置例程，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a22ea-109">To configure a file system-based key repository, call the [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem) configuration routine as shown below.</span></span> <span data-ttu-id="a22ea-110">提供[DirectoryInfo](/dotnet/api/system.io.directoryinfo)指向存储密钥的存储库：</span><span class="sxs-lookup"><span data-stu-id="a22ea-110">Provide a [DirectoryInfo](/dotnet/api/system.io.directoryinfo) pointing to the repository where keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"c:\temp-keys\"));
}
```

<span data-ttu-id="a22ea-111">`DirectoryInfo`可以指向本地计算机上的某个目录，也可以指向网络共享上的文件夹。</span><span class="sxs-lookup"><span data-stu-id="a22ea-111">The `DirectoryInfo` can point to a directory on the local machine, or it can point to a folder on a network share.</span></span> <span data-ttu-id="a22ea-112">如果指向本地计算机上的目录 （和的方案是只在本地计算机上的应用需要使用此存储库的访问权限），请考虑使用[Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (在 Windows) 来加密静态密钥。</span><span class="sxs-lookup"><span data-stu-id="a22ea-112">If pointing to a directory on the local machine (and the scenario is that only apps on the local machine require access to use this repository), consider using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) (on Windows) to encrypt the keys at rest.</span></span> <span data-ttu-id="a22ea-113">否则，请考虑使用[X.509 证书](xref:security/data-protection/implementation/key-encryption-at-rest)来加密静态密钥。</span><span class="sxs-lookup"><span data-stu-id="a22ea-113">Otherwise, consider using an [X.509 certificate](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt keys at rest.</span></span>

## <a name="azure-and-redis"></a><span data-ttu-id="a22ea-114">Azure 和 Redis</span><span class="sxs-lookup"><span data-stu-id="a22ea-114">Azure and Redis</span></span>

<span data-ttu-id="a22ea-115">[Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/)并[Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/)包允许将数据保护密钥存储在 Azure 存储或 Redis 缓存。</span><span class="sxs-lookup"><span data-stu-id="a22ea-115">The [Microsoft.AspNetCore.DataProtection.AzureStorage](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.AzureStorage/) and [Microsoft.AspNetCore.DataProtection.Redis](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection.Redis/) packages allow storing data protection keys in Azure Storage or a Redis cache.</span></span> <span data-ttu-id="a22ea-116">可以在 web 应用的多个实例之间共享密钥。</span><span class="sxs-lookup"><span data-stu-id="a22ea-116">Keys can be shared across several instances of a web app.</span></span> <span data-ttu-id="a22ea-117">应用可以跨多个服务器共享身份验证 cookie 或 CSRF 保护。</span><span class="sxs-lookup"><span data-stu-id="a22ea-117">Apps can share authentication cookies or CSRF protection across multiple servers.</span></span> <span data-ttu-id="a22ea-118">若要配置 Azure Blob 存储提供程序，请调用之一[PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage)重载：</span><span class="sxs-lookup"><span data-stu-id="a22ea-118">To configure the Azure Blob Storage provider, call one of the [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blob URI including SAS token>"));
}
```

<span data-ttu-id="a22ea-119">若要配置 Redis，调用之一[PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis)重载：</span><span class="sxs-lookup"><span data-stu-id="a22ea-119">To configure on Redis, call one of the [PersistKeysToRedis](/dotnet/api/microsoft.aspnetcore.dataprotection.redisdataprotectionbuilderextensions.persistkeystoredis) overloads:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    var redis = ConnectionMultiplexer.Connect("<URI>");
    services.AddDataProtection()
        .PersistKeysToRedis(redis, "DataProtection-Keys");
}
```

<span data-ttu-id="a22ea-120">有关详细信息，请参阅下列主题：</span><span class="sxs-lookup"><span data-stu-id="a22ea-120">For more information, see the following topics:</span></span>

* [<span data-ttu-id="a22ea-121">StackExchange.Redis ConnectionMultiplexer</span><span class="sxs-lookup"><span data-stu-id="a22ea-121">StackExchange.Redis ConnectionMultiplexer</span></span>](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Basics.md)
* [<span data-ttu-id="a22ea-122">Azure Redis 缓存</span><span class="sxs-lookup"><span data-stu-id="a22ea-122">Azure Redis Cache</span></span>](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache#connect-to-the-cache)
* [<span data-ttu-id="a22ea-123">aspnet/DataProtection 示例</span><span class="sxs-lookup"><span data-stu-id="a22ea-123">aspnet/DataProtection samples</span></span>](https://github.com/aspnet/DataProtection/samples)

## <a name="registry"></a><span data-ttu-id="a22ea-124">注册表</span><span class="sxs-lookup"><span data-stu-id="a22ea-124">Registry</span></span>

<span data-ttu-id="a22ea-125">**仅适用于 Windows 的部署。**</span><span class="sxs-lookup"><span data-stu-id="a22ea-125">**Only applies to Windows deployments.**</span></span>

<span data-ttu-id="a22ea-126">有时应用程序可能没有到文件系统的写访问权限。</span><span class="sxs-lookup"><span data-stu-id="a22ea-126">Sometimes the app might not have write access to the file system.</span></span> <span data-ttu-id="a22ea-127">请考虑应用正在作为虚拟服务帐户的方案 (如*w3wp.exe*的应用程序池标识)。</span><span class="sxs-lookup"><span data-stu-id="a22ea-127">Consider a scenario where an app is running as a virtual service account (such as *w3wp.exe*'s app pool identity).</span></span> <span data-ttu-id="a22ea-128">在这些情况下，管理员可以预配的服务帐户标识都可访问的注册表项。</span><span class="sxs-lookup"><span data-stu-id="a22ea-128">In these cases, the administrator can provision a registry key that's accessible by the service account identity.</span></span> <span data-ttu-id="a22ea-129">调用[PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry)扩展方法，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a22ea-129">Call the [PersistKeysToRegistry](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystoregistry) extension method as shown below.</span></span> <span data-ttu-id="a22ea-130">提供[RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey)指向存储加密密钥的位置：</span><span class="sxs-lookup"><span data-stu-id="a22ea-130">Provide a [RegistryKey](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.registryxmlrepository.registrykey) pointing to the location where cryptographic keys should be stored:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToRegistry(Registry.CurrentUser.OpenSubKey(@"SOFTWARE\Sample\keys"));
}
```

> [!IMPORTANT]
> <span data-ttu-id="a22ea-131">我们建议使用[Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest)来加密静态密钥。</span><span class="sxs-lookup"><span data-stu-id="a22ea-131">We recommend using [Windows DPAPI](xref:security/data-protection/implementation/key-encryption-at-rest) to encrypt the keys at rest.</span></span>

## <a name="custom-key-repository"></a><span data-ttu-id="a22ea-132">自定义密钥存储库</span><span class="sxs-lookup"><span data-stu-id="a22ea-132">Custom key repository</span></span>

<span data-ttu-id="a22ea-133">如果不适当的内置机制，开发人员可以通过提供自定义指定自己的密钥持久性机制[IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository)。</span><span class="sxs-lookup"><span data-stu-id="a22ea-133">If the in-box mechanisms aren't appropriate, the developer can specify their own key persistence mechanism by providing a custom [IXmlRepository](/dotnet/api/microsoft.aspnetcore.dataprotection.repositories.ixmlrepository).</span></span>
