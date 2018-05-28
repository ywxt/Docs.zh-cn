---
title: 配置 ASP.NET 核心数据保护
author: rick-anderson
description: 了解如何在 ASP.NET 核心中配置数据保护。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 07/17/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/configuration/overview
ms.openlocfilehash: 803b81f5f69496900791ca1d1976f70f8c266f29
ms.sourcegitcommit: 466300d32f8c33e64ee1b419a2cbffe702863cdf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2018
---
# <a name="configure-aspnet-core-data-protection"></a><span data-ttu-id="5ac01-103">配置 ASP.NET 核心数据保护</span><span class="sxs-lookup"><span data-stu-id="5ac01-103">Configure ASP.NET Core Data Protection</span></span>

<span data-ttu-id="5ac01-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="5ac01-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="5ac01-105">初始化数据保护系统时，它将应用[默认设置](xref:security/data-protection/configuration/default-settings)基于的操作环境。</span><span class="sxs-lookup"><span data-stu-id="5ac01-105">When the Data Protection system is initialized, it applies [default settings](xref:security/data-protection/configuration/default-settings) based on the operational environment.</span></span> <span data-ttu-id="5ac01-106">这些设置并在一台计算机上运行的应用程序通常适用。</span><span class="sxs-lookup"><span data-stu-id="5ac01-106">These settings are generally appropriate for apps running on a single machine.</span></span> <span data-ttu-id="5ac01-107">有情况下，开发人员可能需要更改默认设置：</span><span class="sxs-lookup"><span data-stu-id="5ac01-107">There are cases where a developer may want to change the default settings:</span></span>

* <span data-ttu-id="5ac01-108">应用程序分布在多台计算机。</span><span class="sxs-lookup"><span data-stu-id="5ac01-108">The app is spread across multiple machines.</span></span>
* <span data-ttu-id="5ac01-109">出于合规性原因。</span><span class="sxs-lookup"><span data-stu-id="5ac01-109">For compliance reasons.</span></span>

<span data-ttu-id="5ac01-110">对于这些情况下，数据保护系统提供丰富的配置 API。</span><span class="sxs-lookup"><span data-stu-id="5ac01-110">For these scenarios, the Data Protection system offers a rich configuration API.</span></span>

> [!WARNING]
> <span data-ttu-id="5ac01-111">类似于配置文件，数据保护密钥环应保护使用适当的权限。</span><span class="sxs-lookup"><span data-stu-id="5ac01-111">Similar to configuration files, the data protection key ring should be protected using appropriate permissions.</span></span> <span data-ttu-id="5ac01-112">你可以选择加密静止的密钥，但这不能防止攻击者创建新密钥。</span><span class="sxs-lookup"><span data-stu-id="5ac01-112">You can choose to encrypt keys at rest, but this doesn't prevent attackers from creating new keys.</span></span> <span data-ttu-id="5ac01-113">因此，应用的安全会受到影响。</span><span class="sxs-lookup"><span data-stu-id="5ac01-113">Consequently, your app's security is impacted.</span></span> <span data-ttu-id="5ac01-114">使用数据保护配置的存储位置应具有其访问仅限于应用程序本身，你将保护配置文件工作方式相似。</span><span class="sxs-lookup"><span data-stu-id="5ac01-114">The storage location configured with Data Protection should have its access limited to the app itself, similar to the way you would protect configuration files.</span></span> <span data-ttu-id="5ac01-115">例如，如果你选择存储在磁盘上的密钥令牌环，使用文件系统权限。</span><span class="sxs-lookup"><span data-stu-id="5ac01-115">For example, if you choose to store your key ring on disk, use file system permissions.</span></span> <span data-ttu-id="5ac01-116">确保仅在标识你的 web 应用运行具有读取、 写入和创建该目录的访问。</span><span class="sxs-lookup"><span data-stu-id="5ac01-116">Ensure only the identity under which your web app runs has read, write, and create access to that directory.</span></span> <span data-ttu-id="5ac01-117">如果你使用 Azure 表存储，仅该 web 应用应能够读取、 写入或在表存储等中创建新条目。</span><span class="sxs-lookup"><span data-stu-id="5ac01-117">If you use Azure Table Storage, only the web app should have the ability to read, write, or create new entries in the table store, etc.</span></span>
>
> <span data-ttu-id="5ac01-118">扩展方法[AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection)返回[IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-118">The extension method [AddDataProtection](/dotnet/api/microsoft.extensions.dependencyinjection.dataprotectionservicecollectionextensions.adddataprotection) returns an [IDataProtectionBuilder](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotectionbuilder).</span></span> <span data-ttu-id="5ac01-119">`IDataProtectionBuilder` 显示扩展方法，你可以链接在一起以配置数据保护选项。</span><span class="sxs-lookup"><span data-stu-id="5ac01-119">`IDataProtectionBuilder` exposes extension methods that you can chain together to configure Data Protection options.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="protectkeyswithazurekeyvault"></a><span data-ttu-id="5ac01-120">ProtectKeysWithAzureKeyVault</span><span class="sxs-lookup"><span data-stu-id="5ac01-120">ProtectKeysWithAzureKeyVault</span></span>

<span data-ttu-id="5ac01-121">将中的密钥存储[Azure 密钥保管库](https://azure.microsoft.com/services/key-vault/)，配置与系统[ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault)中`Startup`类：</span><span class="sxs-lookup"><span data-stu-id="5ac01-121">To store keys in [Azure Key Vault](https://azure.microsoft.com/services/key-vault/), configure the system with [ProtectKeysWithAzureKeyVault](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault) in the `Startup` class:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToAzureBlobStorage(new Uri("<blobUriWithSasToken>"))
        .ProtectKeysWithAzureKeyVault("<keyIdentifier>", "<clientId>", "<clientSecret>");
}
```

<span data-ttu-id="5ac01-122">设置密钥链存储位置 (例如， [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage))。</span><span class="sxs-lookup"><span data-stu-id="5ac01-122">Set the key ring storage location (for example, [PersistKeysToAzureBlobStorage](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.persistkeystoazureblobstorage)).</span></span> <span data-ttu-id="5ac01-123">必须设置位置，因为调用`ProtectKeysWithAzureKeyVault`实现[IXmlEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmlencryptor)禁用自动数据保护设置，包括密钥链存储位置。</span><span class="sxs-lookup"><span data-stu-id="5ac01-123">The location must be set because calling `ProtectKeysWithAzureKeyVault` implements an [IXmlEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.xmlencryption.ixmlencryptor) that disables automatic data protection settings, including the key ring storage location.</span></span> <span data-ttu-id="5ac01-124">前面的示例使用 Azure Blob 存储来持久保存密钥链。</span><span class="sxs-lookup"><span data-stu-id="5ac01-124">The preceding example uses Azure Blob Storage to persist the key ring.</span></span> <span data-ttu-id="5ac01-125">有关详细信息，请参阅[密钥存储提供程序： Azure 和 Redis](xref:security/data-protection/implementation/key-storage-providers#azure-and-redis)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-125">For more information, see [Key storage providers: Azure and Redis](xref:security/data-protection/implementation/key-storage-providers#azure-and-redis).</span></span> <span data-ttu-id="5ac01-126">您还可以保留使用在本地密钥环[PersistKeysToFileSystem](xref:security/data-protection/implementation/key-storage-providers#file-system)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-126">You can also persist the key ring locally with [PersistKeysToFileSystem](xref:security/data-protection/implementation/key-storage-providers#file-system).</span></span>

<span data-ttu-id="5ac01-127">`keyIdentifier`是用于密钥加密的密钥保管库密钥标识符 (例如， `https://contosokeyvault.vault.azure.net/keys/dataprotection/`)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-127">The `keyIdentifier` is the key vault key identifier used for key encryption (for example, `https://contosokeyvault.vault.azure.net/keys/dataprotection/`).</span></span>

<span data-ttu-id="5ac01-128">`ProtectKeysWithAzureKeyVault` 重载：</span><span class="sxs-lookup"><span data-stu-id="5ac01-128">`ProtectKeysWithAzureKeyVault` overloads:</span></span>

* <span data-ttu-id="5ac01-129">[ProtectKeysWithAzureKeyVault (IDataProtectionBuilder，KeyVaultClient，String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_Microsoft_Azure_KeyVault_KeyVaultClient_System_String_)允许使用[KeyVaultClient](/dotnet/api/microsoft.azure.keyvault.keyvaultclient)以启用数据保护系统使用密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="5ac01-129">[ProtectKeysWithAzureKeyVault(IDataProtectionBuilder, KeyVaultClient, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_Microsoft_Azure_KeyVault_KeyVaultClient_System_String_) permits the use of a [KeyVaultClient](/dotnet/api/microsoft.azure.keyvault.keyvaultclient) to enable the data protection system to use the key vault.</span></span>
* <span data-ttu-id="5ac01-130">[ProtectKeysWithAzureKeyVault （IDataProtectionBuilder、 字符串、 字符串、 X509Certificate2）](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_Security_Cryptography_X509Certificates_X509Certificate2_)允许使用`ClientId`和[X509Certificate](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2)以启用数据保护系统使用密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="5ac01-130">[ProtectKeysWithAzureKeyVault(IDataProtectionBuilder, String, String, X509Certificate2)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_Security_Cryptography_X509Certificates_X509Certificate2_) permits the use of a `ClientId` and [X509Certificate](/dotnet/api/system.security.cryptography.x509certificates.x509certificate2) to enable the data protection system to use the key vault.</span></span>
* <span data-ttu-id="5ac01-131">[ProtectKeysWithAzureKeyVault （IDataProtectionBuilder、 字符串、 字符串、 字符串）](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_String_)允许使用`ClientId`和`ClientSecret`以启用数据保护系统使用密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="5ac01-131">[ProtectKeysWithAzureKeyVault(IDataProtectionBuilder, String, String, String)](/dotnet/api/microsoft.aspnetcore.dataprotection.azuredataprotectionbuilderextensions.protectkeyswithazurekeyvault#Microsoft_AspNetCore_DataProtection_AzureDataProtectionBuilderExtensions_ProtectKeysWithAzureKeyVault_Microsoft_AspNetCore_DataProtection_IDataProtectionBuilder_System_String_System_String_System_String_) permits the use of a `ClientId` and `ClientSecret` to enable the data protection system to use the key vault.</span></span>

::: moniker-end

## <a name="persistkeystofilesystem"></a><span data-ttu-id="5ac01-132">PersistKeysToFileSystem</span><span class="sxs-lookup"><span data-stu-id="5ac01-132">PersistKeysToFileSystem</span></span>

<span data-ttu-id="5ac01-133">将密钥存储在 UNC 共享而不是在 *%LOCALAPPDATA%* 默认位置，配置与系统[PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span><span class="sxs-lookup"><span data-stu-id="5ac01-133">To store keys on a UNC share instead of at the *%LOCALAPPDATA%* default location, configure the system with [PersistKeysToFileSystem](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.persistkeystofilesystem):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"));
}
```

> [!WARNING]
> <span data-ttu-id="5ac01-134">如果更改密钥持久性位置，系统将不再自动加密组合键，其余部分，因为它不知道 DPAPI 是否合适的加密机制。</span><span class="sxs-lookup"><span data-stu-id="5ac01-134">If you change the key persistence location, the system no longer automatically encrypts keys at rest, since it doesn't know whether DPAPI is an appropriate encryption mechanism.</span></span>

## <a name="protectkeyswith"></a><span data-ttu-id="5ac01-135">ProtectKeysWith\*</span><span class="sxs-lookup"><span data-stu-id="5ac01-135">ProtectKeysWith\*</span></span>

<span data-ttu-id="5ac01-136">你可以将系统配置为通过调用的任何保护静止的密钥[ProtectKeysWith\* ](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions)配置 Api。</span><span class="sxs-lookup"><span data-stu-id="5ac01-136">You can configure the system to protect keys at rest by calling any of the [ProtectKeysWith\*](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions) configuration APIs.</span></span> <span data-ttu-id="5ac01-137">请考虑以下示例中，它将密钥存储的 UNC 共享上并对这些密钥在使用特定的 X.509 证书的其余部分进行加密：</span><span class="sxs-lookup"><span data-stu-id="5ac01-137">Consider the example below, which stores keys on a UNC share and encrypts those keys at rest with a specific X.509 certificate:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .PersistKeysToFileSystem(new DirectoryInfo(@"\\server\share\directory\"))
        .ProtectKeysWithCertificate("thumbprint");
}
```

<span data-ttu-id="5ac01-138">请参阅[将加密密钥在 Rest](xref:security/data-protection/implementation/key-encryption-at-rest)有关更多示例和讨论的内置密钥加密机制。</span><span class="sxs-lookup"><span data-stu-id="5ac01-138">See [Key Encryption At Rest](xref:security/data-protection/implementation/key-encryption-at-rest) for more examples and discussion on the built-in key encryption mechanisms.</span></span>

## <a name="setdefaultkeylifetime"></a><span data-ttu-id="5ac01-139">SetDefaultKeyLifetime</span><span class="sxs-lookup"><span data-stu-id="5ac01-139">SetDefaultKeyLifetime</span></span>

<span data-ttu-id="5ac01-140">若要配置系统而不是默认值 90 天使用的密钥生存期为 14 天，使用[SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span><span class="sxs-lookup"><span data-stu-id="5ac01-140">To configure the system to use a key lifetime of 14 days instead of the default 90 days, use [SetDefaultKeyLifetime](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setdefaultkeylifetime):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetDefaultKeyLifetime(TimeSpan.FromDays(14));
}
```

## <a name="setapplicationname"></a><span data-ttu-id="5ac01-141">SetApplicationName</span><span class="sxs-lookup"><span data-stu-id="5ac01-141">SetApplicationName</span></span>

<span data-ttu-id="5ac01-142">默认情况下，数据保护系统隔离应用程序从另一个，即使它们共享相同的物理密钥存储库。</span><span class="sxs-lookup"><span data-stu-id="5ac01-142">By default, the Data Protection system isolates apps from one another, even if they're sharing the same physical key repository.</span></span> <span data-ttu-id="5ac01-143">这可以阻止应用了解对方的受保护的负载。</span><span class="sxs-lookup"><span data-stu-id="5ac01-143">This prevents the apps from understanding each other's protected payloads.</span></span> <span data-ttu-id="5ac01-144">若要共享两个应用程序之间的受保护的负载，使用[SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname)与每个应用程序相同的值：</span><span class="sxs-lookup"><span data-stu-id="5ac01-144">To share protected payloads between two apps, use [SetApplicationName](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.setapplicationname) with the same value for each app:</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .SetApplicationName("shared app name");
}
```

## <a name="disableautomatickeygeneration"></a><span data-ttu-id="5ac01-145">DisableAutomaticKeyGeneration</span><span class="sxs-lookup"><span data-stu-id="5ac01-145">DisableAutomaticKeyGeneration</span></span>

<span data-ttu-id="5ac01-146">您可能有不希望自动轮转 （创建新的密钥） 的密钥，因为它们接近过期的应用的方案。</span><span class="sxs-lookup"><span data-stu-id="5ac01-146">You may have a scenario where you don't want an app to automatically roll keys (create new keys) as they approach expiration.</span></span> <span data-ttu-id="5ac01-147">这一个示例可能是应用程序设置在主要/辅助关系中，其中仅主应用程序负责密钥管理问题，而辅助应用只需密钥环的只读视图。</span><span class="sxs-lookup"><span data-stu-id="5ac01-147">One example of this might be apps set up in a primary/secondary relationship, where only the primary app is responsible for key management concerns and secondary apps simply have a read-only view of the key ring.</span></span> <span data-ttu-id="5ac01-148">可以配置辅助应用程序通过配置与系统以只读方式处理密钥环[DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span><span class="sxs-lookup"><span data-stu-id="5ac01-148">The secondary apps can be configured to treat the key ring as read-only by configuring the system with [DisableAutomaticKeyGeneration](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.disableautomatickeygeneration):</span></span>

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDataProtection()
        .DisableAutomaticKeyGeneration();
}
```

## <a name="per-application-isolation"></a><span data-ttu-id="5ac01-149">每个应用程序隔离</span><span class="sxs-lookup"><span data-stu-id="5ac01-149">Per-application isolation</span></span>

<span data-ttu-id="5ac01-150">数据保护系统提供了 ASP.NET 核心主机，但它自动隔离了从另一个，应用程序，即使这些应用在相同的工作进程帐户下运行，并且使用相同的主密钥材料。</span><span class="sxs-lookup"><span data-stu-id="5ac01-150">When the Data Protection system is provided by an ASP.NET Core host, it automatically isolates apps from one another, even if those apps are running under the same worker process account and are using the same master keying material.</span></span> <span data-ttu-id="5ac01-151">这是某种程度上类似于 IsolateApps 修饰符从 System.Web 的 **\<machineKey >** 元素。</span><span class="sxs-lookup"><span data-stu-id="5ac01-151">This is somewhat similar to the IsolateApps modifier from System.Web's **\<machineKey>** element.</span></span>

<span data-ttu-id="5ac01-152">隔离机制的工作原理是作为唯一的租户，因此考虑本地计算机上的每个应用[IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector)取得 root 权限的任何给定的应用会自动包括为鉴别器的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="5ac01-152">The isolation mechanism works by considering each app on the local machine as a unique tenant, thus the [IDataProtector](/dotnet/api/microsoft.aspnetcore.dataprotection.idataprotector) rooted for any given app automatically includes the app ID as a discriminator.</span></span> <span data-ttu-id="5ac01-153">应用程序的唯一 ID 来自两个位置之一：</span><span class="sxs-lookup"><span data-stu-id="5ac01-153">The app's unique ID comes from one of two places:</span></span>

1. <span data-ttu-id="5ac01-154">如果在 IIS 中托管应用的唯一标识符是应用程序的配置路径。</span><span class="sxs-lookup"><span data-stu-id="5ac01-154">If the app is hosted in IIS, the unique identifier is the app's configuration path.</span></span> <span data-ttu-id="5ac01-155">如果在 web 场环境中部署应用后，此值应为稳定，前提是在 web 场中的所有计算机同样配置 IIS 环境。</span><span class="sxs-lookup"><span data-stu-id="5ac01-155">If an app is deployed in a web farm environment, this value should be stable assuming that the IIS environments are configured similarly across all machines in the web farm.</span></span>

2. <span data-ttu-id="5ac01-156">如果应用程序不在 IIS 中承载的的唯一标识符是应用程序的物理路径。</span><span class="sxs-lookup"><span data-stu-id="5ac01-156">If the app isn't hosted in IIS, the unique identifier is the physical path of the app.</span></span>

<span data-ttu-id="5ac01-157">唯一标识符旨在得以重置&mdash;同时的各个应用程序和计算机本身。</span><span class="sxs-lookup"><span data-stu-id="5ac01-157">The unique identifier is designed to survive resets &mdash; both of the individual app and of the machine itself.</span></span>

<span data-ttu-id="5ac01-158">此隔离机制假设应用不可恶意。</span><span class="sxs-lookup"><span data-stu-id="5ac01-158">This isolation mechanism assumes that the apps are not malicious.</span></span> <span data-ttu-id="5ac01-159">恶意应用程序始终可以影响在相同的工作进程帐户下运行的任何其他应用程序。</span><span class="sxs-lookup"><span data-stu-id="5ac01-159">A malicious app can always impact any other app running under the same worker process account.</span></span> <span data-ttu-id="5ac01-160">在共享宿主环境中应用是相互不受信任，托管提供商应采取措施来确保应用，包括分离应用的基础密钥的存储库之间的操作系统级别隔离。</span><span class="sxs-lookup"><span data-stu-id="5ac01-160">In a shared hosting environment where apps are mutually untrusted, the hosting provider should take steps to ensure OS-level isolation between apps, including separating the apps' underlying key repositories.</span></span>

<span data-ttu-id="5ac01-161">如果由 ASP.NET 核心主机未提供数据保护系统 (例如，如果通过其实例化`DataProtectionProvider`具体类型) 应用程序隔离在默认情况下处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="5ac01-161">If the Data Protection system isn't provided by an ASP.NET Core host (for example, if you instantiate it via the `DataProtectionProvider` concrete type) app isolation is disabled by default.</span></span> <span data-ttu-id="5ac01-162">当禁用应用程序隔离时，相同的密钥材料作为后盾的所有应用可以都共享的负载，只要它们提供相应[目的](xref:security/data-protection/consumer-apis/purpose-strings)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-162">When app isolation is disabled, all apps backed by the same keying material can share payloads as long as they provide the appropriate [purposes](xref:security/data-protection/consumer-apis/purpose-strings).</span></span> <span data-ttu-id="5ac01-163">若要提供在此环境中的应用程序隔离，调用[SetApplicationName](#setapplicationname)方法的配置对象，并提供每个应用程序的唯一名称。</span><span class="sxs-lookup"><span data-stu-id="5ac01-163">To provide app isolation in this environment, call the [SetApplicationName](#setapplicationname) method on the configuration object and provide a unique name for each app.</span></span>

## <a name="changing-algorithms-with-usecryptographicalgorithms"></a><span data-ttu-id="5ac01-164">更改与 UseCryptographicAlgorithms 算法</span><span class="sxs-lookup"><span data-stu-id="5ac01-164">Changing algorithms with UseCryptographicAlgorithms</span></span>

<span data-ttu-id="5ac01-165">数据保护堆栈可以更改默认的算法使用的新生成的键。</span><span class="sxs-lookup"><span data-stu-id="5ac01-165">The Data Protection stack allows you to change the default algorithm used by newly-generated keys.</span></span> <span data-ttu-id="5ac01-166">执行此操作的最简单方法是调用[UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms)从配置回调：</span><span class="sxs-lookup"><span data-stu-id="5ac01-166">The simplest way to do this is to call [UseCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecryptographicalgorithms) from the configuration callback:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ac01-167">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-167">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptorConfiguration()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ac01-168">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-168">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

```csharp
services.AddDataProtection()
    .UseCryptographicAlgorithms(
        new AuthenticatedEncryptionSettings()
    {
        EncryptionAlgorithm = EncryptionAlgorithm.AES_256_CBC,
        ValidationAlgorithm = ValidationAlgorithm.HMACSHA256
    });
```

---

<span data-ttu-id="5ac01-169">默认值 EncryptionAlgorithm AES 256 CBC，且默认 ValidationAlgorithm HMACSHA256。</span><span class="sxs-lookup"><span data-stu-id="5ac01-169">The default EncryptionAlgorithm is AES-256-CBC, and the default ValidationAlgorithm is HMACSHA256.</span></span> <span data-ttu-id="5ac01-170">默认策略可以设置由系统管理员通过[计算机范围策略](xref:security/data-protection/configuration/machine-wide-policy)，但显式调用`UseCryptographicAlgorithms`将替代默认策略。</span><span class="sxs-lookup"><span data-stu-id="5ac01-170">The default policy can be set by a system administrator via a [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy), but an explicit call to `UseCryptographicAlgorithms` overrides the default policy.</span></span>

<span data-ttu-id="5ac01-171">调用`UseCryptographicAlgorithms`允许你指定从预定义的内置列表所需的算法。</span><span class="sxs-lookup"><span data-stu-id="5ac01-171">Calling `UseCryptographicAlgorithms` allows you to specify the desired algorithm from a predefined built-in list.</span></span> <span data-ttu-id="5ac01-172">你不必担心算法的实现。</span><span class="sxs-lookup"><span data-stu-id="5ac01-172">You don't need to worry about the implementation of the algorithm.</span></span> <span data-ttu-id="5ac01-173">在上述方案中，数据保护系统会尝试在 Windows 上运行使用 AES 的 CNG 实现。</span><span class="sxs-lookup"><span data-stu-id="5ac01-173">In the scenario above, the Data Protection system attempts to use the CNG implementation of AES if running on Windows.</span></span> <span data-ttu-id="5ac01-174">否则，则会返回到托管[System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes)类。</span><span class="sxs-lookup"><span data-stu-id="5ac01-174">Otherwise, it falls back to the managed [System.Security.Cryptography.Aes](/dotnet/api/system.security.cryptography.aes) class.</span></span>

<span data-ttu-id="5ac01-175">你可以手动指定通过调用实现[UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-175">You can manually specify an implementation via a call to [UseCustomCryptographicAlgorithms](/dotnet/api/microsoft.aspnetcore.dataprotection.dataprotectionbuilderextensions.usecustomcryptographicalgorithms).</span></span>

> [!TIP]
> <span data-ttu-id="5ac01-176">更改算法不会影响现有的密钥在密钥环。</span><span class="sxs-lookup"><span data-stu-id="5ac01-176">Changing algorithms doesn't affect existing keys in the key ring.</span></span> <span data-ttu-id="5ac01-177">它只影响新生成的键。</span><span class="sxs-lookup"><span data-stu-id="5ac01-177">It only affects newly-generated keys.</span></span>

### <a name="specifying-custom-managed-algorithms"></a><span data-ttu-id="5ac01-178">指定自定义托管的算法</span><span class="sxs-lookup"><span data-stu-id="5ac01-178">Specifying custom managed algorithms</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ac01-179">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-179">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5ac01-180">若要指定自定义托管的算法，创建[ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration)指向的实现类型的实例：</span><span class="sxs-lookup"><span data-stu-id="5ac01-180">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.managedauthenticatedencryptorconfiguration) instance that points to the implementation types:</span></span>

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptorConfiguration()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ac01-181">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-181">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5ac01-182">若要指定自定义托管的算法，创建[ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings)指向的实现类型的实例：</span><span class="sxs-lookup"><span data-stu-id="5ac01-182">To specify custom managed algorithms, create a [ManagedAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.managedauthenticatedencryptionsettings) instance that points to the implementation types:</span></span>

```csharp
serviceCollection.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new ManagedAuthenticatedEncryptionSettings()
    {
        // A type that subclasses SymmetricAlgorithm
        EncryptionAlgorithmType = typeof(Aes),

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // A type that subclasses KeyedHashAlgorithm
        ValidationAlgorithmType = typeof(HMACSHA256)
    });
```

---

<span data-ttu-id="5ac01-183">通常\*类型属性必须指向具体，可实例化 （通过公共的无参数 ctor) 实现的[SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm)和[KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm)，不过系统特殊的情况下等某些值`typeof(Aes)`为方便起见。</span><span class="sxs-lookup"><span data-stu-id="5ac01-183">Generally the \*Type properties must point to concrete, instantiable (via a public parameterless ctor) implementations of [SymmetricAlgorithm](/dotnet/api/system.security.cryptography.symmetricalgorithm) and [KeyedHashAlgorithm](/dotnet/api/system.security.cryptography.keyedhashalgorithm), though the system special-cases some values like `typeof(Aes)` for convenience.</span></span>

> [!NOTE]
> <span data-ttu-id="5ac01-184">SymmetricAlgorithm 必须 ≥ 128 位的密钥长度和块大小的 ≥ 64 位，并且它必须支持使用 PKCS #7 填充 CBC 模式下的加密。</span><span class="sxs-lookup"><span data-stu-id="5ac01-184">The SymmetricAlgorithm must have a key length of ≥ 128 bits and a block size of ≥ 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="5ac01-185">KeyedHashAlgorithm 的摘要大小必须 > = 128 位，并且它必须支持密钥长度等于 length 哈希算法的摘要。</span><span class="sxs-lookup"><span data-stu-id="5ac01-185">The KeyedHashAlgorithm must have a digest size of >= 128 bits, and it must support keys of length equal to the hash algorithm's digest length.</span></span> <span data-ttu-id="5ac01-186">KeyedHashAlgorithm 并非是严格要求，要 HMAC。</span><span class="sxs-lookup"><span data-stu-id="5ac01-186">The KeyedHashAlgorithm isn't strictly required to be HMAC.</span></span>

### <a name="specifying-custom-windows-cng-algorithms"></a><span data-ttu-id="5ac01-187">指定自定义 Windows CNG 算法</span><span class="sxs-lookup"><span data-stu-id="5ac01-187">Specifying custom Windows CNG algorithms</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ac01-188">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-188">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5ac01-189">若要指定自定义 Windows CNG 算法通过 HMAC 验证使用 CBC 模式下加密，创建[CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration)实例，其中包含的算法的信息：</span><span class="sxs-lookup"><span data-stu-id="5ac01-189">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ac01-190">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-190">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5ac01-191">若要指定自定义 Windows CNG 算法通过 HMAC 验证使用 CBC 模式下加密，创建[CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings)实例，其中包含的算法的信息：</span><span class="sxs-lookup"><span data-stu-id="5ac01-191">To specify a custom Windows CNG algorithm using CBC-mode encryption with HMAC validation, create a [CngCbcAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cngcbcauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngCbcAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256,

        // Passed to BCryptOpenAlgorithmProvider
        HashAlgorithm = "SHA256",
        HashAlgorithmProvider = null
    });
```

---

> [!NOTE]
> <span data-ttu-id="5ac01-192">对称块加密算法的密钥长度必须 > = 128 位的块大小 > = 64 位，并且它必须支持使用 PKCS #7 填充 CBC 模式下的加密。</span><span class="sxs-lookup"><span data-stu-id="5ac01-192">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of >= 64 bits, and it must support CBC-mode encryption with PKCS #7 padding.</span></span> <span data-ttu-id="5ac01-193">哈希算法的摘要大小必须 > = 128 位并且必须支持与 BCRYPT 打开\_ALG\_处理\_HMAC\_标志标志。</span><span class="sxs-lookup"><span data-stu-id="5ac01-193">The hash algorithm must have a digest size of >= 128 bits and must support being opened with the BCRYPT\_ALG\_HANDLE\_HMAC\_FLAG flag.</span></span> <span data-ttu-id="5ac01-194">\*提供程序属性可以设置为空，默认的提供程序用于为指定的算法。</span><span class="sxs-lookup"><span data-stu-id="5ac01-194">The \*Provider properties can be set to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="5ac01-195">请参阅[BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx)文档以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="5ac01-195">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5ac01-196">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-196">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5ac01-197">若要指定自定义 Windows CNG 算法通过验证使用 Galois/计数器模式加密，创建[CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration)实例，其中包含的算法的信息：</span><span class="sxs-lookup"><span data-stu-id="5ac01-197">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptorConfiguration](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cnggcmauthenticatedencryptorconfiguration) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptorConfiguration()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5ac01-198">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5ac01-198">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5ac01-199">若要指定自定义 Windows CNG 算法通过验证使用 Galois/计数器模式加密，创建[CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings)实例，其中包含的算法的信息：</span><span class="sxs-lookup"><span data-stu-id="5ac01-199">To specify a custom Windows CNG algorithm using Galois/Counter Mode encryption with validation, create a [CngGcmAuthenticatedEncryptionSettings](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.cnggcmauthenticatedencryptionsettings) instance that contains the algorithmic information:</span></span>

```csharp
services.AddDataProtection()
    .UseCustomCryptographicAlgorithms(
        new CngGcmAuthenticatedEncryptionSettings()
    {
        // Passed to BCryptOpenAlgorithmProvider
        EncryptionAlgorithm = "AES",
        EncryptionAlgorithmProvider = null,

        // Specified in bits
        EncryptionAlgorithmKeySize = 256
    });
```

---

> [!NOTE]
> <span data-ttu-id="5ac01-200">对称块加密算法的密钥长度必须 > = 128 位的块大小为完全 128 位，并且它必须支持 GCM 加密。</span><span class="sxs-lookup"><span data-stu-id="5ac01-200">The symmetric block cipher algorithm must have a key length of >= 128 bits, a block size of exactly 128 bits, and it must support GCM encryption.</span></span> <span data-ttu-id="5ac01-201">你可以设置[EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider)属性为 null，以便使用默认提供程序指定的算法。</span><span class="sxs-lookup"><span data-stu-id="5ac01-201">You can set the [EncryptionAlgorithmProvider](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.configurationmodel.cngcbcauthenticatedencryptorconfiguration.encryptionalgorithmprovider) property to null to use the default provider for the specified algorithm.</span></span> <span data-ttu-id="5ac01-202">请参阅[BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx)文档以了解更多信息。</span><span class="sxs-lookup"><span data-stu-id="5ac01-202">See the [BCryptOpenAlgorithmProvider](https://msdn.microsoft.com/library/windows/desktop/aa375479(v=vs.85).aspx) documentation for more information.</span></span>

### <a name="specifying-other-custom-algorithms"></a><span data-ttu-id="5ac01-203">指定其他自定义算法</span><span class="sxs-lookup"><span data-stu-id="5ac01-203">Specifying other custom algorithms</span></span>

<span data-ttu-id="5ac01-204">尽管不作为第一类 API 公开，则数据保护系统是算法的可扩展，足以允许指定几乎任何类型。</span><span class="sxs-lookup"><span data-stu-id="5ac01-204">Though not exposed as a first-class API, the Data Protection system is extensible enough to allow specifying almost any kind of algorithm.</span></span> <span data-ttu-id="5ac01-205">例如，很可能需要包含在硬件安全模块 (HSM) 的所有键，并为核心的自定义实现加密和解密的例程。</span><span class="sxs-lookup"><span data-stu-id="5ac01-205">For example, it's possible to keep all keys contained within a Hardware Security Module (HSM) and to provide a custom implementation of the core encryption and decryption routines.</span></span> <span data-ttu-id="5ac01-206">请参阅[IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor)中[核心加密可扩展性](xref:security/data-protection/extensibility/core-crypto)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="5ac01-206">See [IAuthenticatedEncryptor](/dotnet/api/microsoft.aspnetcore.dataprotection.authenticatedencryption.iauthenticatedencryptor) in [Core cryptography extensibility](xref:security/data-protection/extensibility/core-crypto) for more information.</span></span>

## <a name="persisting-keys-when-hosting-in-a-docker-container"></a><span data-ttu-id="5ac01-207">保留密钥： 当在 Docker 容器中承载</span><span class="sxs-lookup"><span data-stu-id="5ac01-207">Persisting keys when hosting in a Docker container</span></span>

<span data-ttu-id="5ac01-208">在中承载时[Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/)容器，应在维护密钥：</span><span class="sxs-lookup"><span data-stu-id="5ac01-208">When hosting in a [Docker](/dotnet/standard/microservices-architecture/container-docker-introduction/) container, keys should be maintained in either:</span></span>

* <span data-ttu-id="5ac01-209">是一个 Docker 卷容器的生存期结束，例如共享的卷或者主机已装入卷后仍然存在，一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="5ac01-209">A folder that's a Docker volume that persists beyond the container's lifetime, such as a shared volume or a host-mounted volume.</span></span>
* <span data-ttu-id="5ac01-210">外部提供程序，如[Azure 密钥保管库](https://azure.microsoft.com/services/key-vault/)或[Redis](https://redis.io/)。</span><span class="sxs-lookup"><span data-stu-id="5ac01-210">An external provider, such as [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) or [Redis](https://redis.io/).</span></span>

## <a name="see-also"></a><span data-ttu-id="5ac01-211">请参阅</span><span class="sxs-lookup"><span data-stu-id="5ac01-211">See also</span></span>

* [<span data-ttu-id="5ac01-212">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="5ac01-212">Non DI Aware Scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)
* [<span data-ttu-id="5ac01-213">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="5ac01-213">Machine Wide Policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)
