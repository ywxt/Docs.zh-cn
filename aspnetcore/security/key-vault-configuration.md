---
title: 在 ASP.NET Core 的 azure 密钥保管库配置提供程序
author: guardrex
description: 了解如何使用 Azure 密钥保管库配置提供程序来配置应用程序使用在运行时加载的名称 / 值对。
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: security/key-vault-configuration
ms.openlocfilehash: 06445eb2ecec4cf101b23a4bfe131b2c56a18f62
ms.sourcegitcommit: 4d74644f11e0dac52b4510048490ae731c691496
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50090301"
---
# <a name="azure-key-vault-configuration-provider-in-aspnet-core"></a><span data-ttu-id="11267-103">在 ASP.NET Core 的 azure 密钥保管库配置提供程序</span><span class="sxs-lookup"><span data-stu-id="11267-103">Azure Key Vault configuration provider in ASP.NET Core</span></span>

<span data-ttu-id="11267-104">通过[Luke Latham](https://github.com/guardrex)和[Andrew Stanton-nurse](https://github.com/anurse)</span><span class="sxs-lookup"><span data-stu-id="11267-104">By [Luke Latham](https://github.com/guardrex) and [Andrew Stanton-Nurse](https://github.com/anurse)</span></span>

<span data-ttu-id="11267-105">本文档介绍如何使用[Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/)配置提供程序将从 Azure Key Vault 机密中加载应用配置值。</span><span class="sxs-lookup"><span data-stu-id="11267-105">This document explains how to use the [Microsoft Azure Key Vault](https://azure.microsoft.com/services/key-vault/) configuration provider to load app configuration values from Azure Key Vault secrets.</span></span> <span data-ttu-id="11267-106">Azure Key Vault 是基于云的服务，可帮助你保护加密密钥和机密使用的应用和服务。</span><span class="sxs-lookup"><span data-stu-id="11267-106">Azure Key Vault is a cloud-based service that helps you safeguard cryptographic keys and secrets used by apps and services.</span></span> <span data-ttu-id="11267-107">常见的方案包括控制对敏感的配置数据的访问并符合 fips 140-2 的要求级别 2 硬件安全模块 (HSM) 时验证存储配置数据。</span><span class="sxs-lookup"><span data-stu-id="11267-107">Common scenarios include controlling access to sensitive configuration data and meeting the requirement for FIPS 140-2 Level 2 validated Hardware Security Modules (HSM's) when storing configuration data.</span></span> <span data-ttu-id="11267-108">此功能仅适用于面向 ASP.NET Core 1.1 的应用或更高版本。</span><span class="sxs-lookup"><span data-stu-id="11267-108">This feature is available for apps that target ASP.NET Core 1.1 or higher.</span></span>

<span data-ttu-id="11267-109">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="11267-109">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="package"></a><span data-ttu-id="11267-110">Package</span><span class="sxs-lookup"><span data-stu-id="11267-110">Package</span></span>

<span data-ttu-id="11267-111">若要使用的提供程序，添加到引用[Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/)包。</span><span class="sxs-lookup"><span data-stu-id="11267-111">To use the provider, add a reference to the [Microsoft.Extensions.Configuration.AzureKeyVault](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureKeyVault/) package.</span></span>

## <a name="app-configuration"></a><span data-ttu-id="11267-112">应用配置</span><span class="sxs-lookup"><span data-stu-id="11267-112">App configuration</span></span>

<span data-ttu-id="11267-113">你可以浏览的提供程序[示例应用](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples)。</span><span class="sxs-lookup"><span data-stu-id="11267-113">You can explore the provider with the [sample apps](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples).</span></span> <span data-ttu-id="11267-114">建立密钥保管库并在保管库中创建机密后，示例应用安全地将机密值加载到其配置并在网页中显示它们。</span><span class="sxs-lookup"><span data-stu-id="11267-114">Once you establish a key vault and create secrets in the vault, the sample apps securely load the secret values into their configurations and display them in webpages.</span></span>

<span data-ttu-id="11267-115">提供程序添加到应用程序的配置中使用`AddAzureKeyVault`扩展。</span><span class="sxs-lookup"><span data-stu-id="11267-115">The provider is added to the app's configuration with the `AddAzureKeyVault` extension.</span></span> <span data-ttu-id="11267-116">在示例应用中，则该扩展将从加载的三个配置值*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="11267-116">In the sample apps, the extension uses three configuration values loaded from the *appsettings.json* file.</span></span>

| <span data-ttu-id="11267-117">应用设置</span><span class="sxs-lookup"><span data-stu-id="11267-117">App Setting</span></span>    | <span data-ttu-id="11267-118">描述</span><span class="sxs-lookup"><span data-stu-id="11267-118">Description</span></span>                    | <span data-ttu-id="11267-119">示例</span><span class="sxs-lookup"><span data-stu-id="11267-119">Example</span></span>                                      |
| -------------- | ------------------------------ | -------------------------------------------- |
| `Vault`        | <span data-ttu-id="11267-120">Azure 密钥保管库名称</span><span class="sxs-lookup"><span data-stu-id="11267-120">Azure Key Vault name</span></span>           | <span data-ttu-id="11267-121">contosovault</span><span class="sxs-lookup"><span data-stu-id="11267-121">contosovault</span></span>                                 |
| `ClientId`     | <span data-ttu-id="11267-122">Azure Active Directory 应用 Id</span><span class="sxs-lookup"><span data-stu-id="11267-122">Azure Active Directory App Id</span></span>  | <span data-ttu-id="11267-123">627e911e-43cc-61d4-992e-12db9c81b413</span><span class="sxs-lookup"><span data-stu-id="11267-123">627e911e-43cc-61d4-992e-12db9c81b413</span></span>         |
| `ClientSecret` | <span data-ttu-id="11267-124">Azure Active Directory 应用密钥</span><span class="sxs-lookup"><span data-stu-id="11267-124">Azure Active Directory App Key</span></span> | <span data-ttu-id="11267-125">g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=</span><span class="sxs-lookup"><span data-stu-id="11267-125">g58K3dtg59o1Pa+e59v2Tx829w6VxTB2yv9sv/101di=</span></span> |

[!code-csharp[Program](key-vault-configuration/samples/basic-sample/2.x/Program.cs?name=snippet1)]

## <a name="create-key-vault-secrets-and-load-configuration-values-basic-sample"></a><span data-ttu-id="11267-126">创建密钥保管库机密并加载配置值 （basic 示例）</span><span class="sxs-lookup"><span data-stu-id="11267-126">Create key vault secrets and load configuration values (basic-sample)</span></span>

1. <span data-ttu-id="11267-127">创建密钥保管库并将设置 Azure Active Directory (Azure AD) 应用程序中的指南[开始使用 Azure 密钥保管库](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="11267-127">Create a key vault and set up Azure Active Directory (Azure AD) for the app following the guidance in [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).</span></span>
   * <span data-ttu-id="11267-128">将机密添加到密钥保管库使用[AzureRM 密钥保管库 PowerShell 模块](/powershell/module/azurerm.keyvault)从可用[PowerShell 库](https://www.powershellgallery.com/packages/AzureRM.KeyVault)，则[Azure 密钥保管库 REST API](/rest/api/keyvault/)，或者[Azure 门户](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="11267-128">Add secrets to the key vault using the [AzureRM Key Vault PowerShell Module](/powershell/module/azurerm.keyvault) available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.KeyVault), the [Azure Key Vault REST API](/rest/api/keyvault/), or the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="11267-129">为创建的机密*手动*或*证书*机密。</span><span class="sxs-lookup"><span data-stu-id="11267-129">Secrets are created as either *Manual* or *Certificate* secrets.</span></span> <span data-ttu-id="11267-130">*证书*机密使用的应用和服务证书，但不是支持配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="11267-130">*Certificate* secrets are certificates for use by apps and services but are not supported by the configuration provider.</span></span> <span data-ttu-id="11267-131">应使用*手动*选项可创建带有配置提供程序使用的名称-值对机密。</span><span class="sxs-lookup"><span data-stu-id="11267-131">You should use the *Manual* option to create name-value pair secrets for use with the configuration provider.</span></span>
     * <span data-ttu-id="11267-132">以名称-值对的形式创建简单的机密。</span><span class="sxs-lookup"><span data-stu-id="11267-132">Simple secrets are created as name-value pairs.</span></span> <span data-ttu-id="11267-133">Azure 密钥保管库机密名称被限制为字母数字字符和短划线。</span><span class="sxs-lookup"><span data-stu-id="11267-133">Azure Key Vault secret names are limited to alphanumeric characters and dashes.</span></span>
     * <span data-ttu-id="11267-134">层次结构的值 （配置节） 使用`--`（两个短划线） 作为分隔符，在该示例。</span><span class="sxs-lookup"><span data-stu-id="11267-134">Hierarchical values (configuration sections) use `--` (two dashes) as a separator in the sample.</span></span> <span data-ttu-id="11267-135">通常用于分隔的子项中的一部分的冒号[ASP.NET Core 配置](xref:fundamentals/configuration/index)，机密名称中不允许出现。</span><span class="sxs-lookup"><span data-stu-id="11267-135">Colons, which are normally used to delimit a section from a subkey in [ASP.NET Core configuration](xref:fundamentals/configuration/index), aren't allowed in secret names.</span></span> <span data-ttu-id="11267-136">因此，两个短划线的使用和机密加载到应用的配置时交换的冒号。</span><span class="sxs-lookup"><span data-stu-id="11267-136">Therefore, two dashes are used and swapped for a colon when the secrets are loaded into the app's configuration.</span></span>
     * <span data-ttu-id="11267-137">创建两个*手动*具有以下名称 / 值对的机密。</span><span class="sxs-lookup"><span data-stu-id="11267-137">Create two *Manual* secrets with the following name-value pairs.</span></span> <span data-ttu-id="11267-138">第一个机密是一个简单的名称和值，并第二个密钥使用部分和子项中的机密名称创建机密值：</span><span class="sxs-lookup"><span data-stu-id="11267-138">The first secret is a simple name and value, and the second secret creates a secret value with a section and subkey in the secret name:</span></span>
       * <span data-ttu-id="11267-139">`SecretName`: `secret_value_1`</span><span class="sxs-lookup"><span data-stu-id="11267-139">`SecretName`: `secret_value_1`</span></span>
       * <span data-ttu-id="11267-140">`Section--SecretName`: `secret_value_2`</span><span class="sxs-lookup"><span data-stu-id="11267-140">`Section--SecretName`: `secret_value_2`</span></span>
   * <span data-ttu-id="11267-141">与 Azure Active Directory 中注册示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="11267-141">Register the sample app with Azure Active Directory.</span></span>
   * <span data-ttu-id="11267-142">授权应用访问密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="11267-142">Authorize the app to access the key vault.</span></span> <span data-ttu-id="11267-143">当你使用`Set-AzureRmKeyVaultAccessPolicy`PowerShell cmdlet 来授权应用程序访问密钥保管库，提供`List`并`Get`对使用机密的访问`-PermissionsToSecrets list,get`。</span><span class="sxs-lookup"><span data-stu-id="11267-143">When you use the `Set-AzureRmKeyVaultAccessPolicy` PowerShell cmdlet to authorize the app to access the key vault, provide `List` and `Get` access to secrets with `-PermissionsToSecrets list,get`.</span></span>

2. <span data-ttu-id="11267-144">更新应用程序的*appsettings.json*包含的值的文件`Vault`， `ClientId`，和`ClientSecret`。</span><span class="sxs-lookup"><span data-stu-id="11267-144">Update the app's *appsettings.json* file with the values of `Vault`, `ClientId`, and `ClientSecret`.</span></span>
3. <span data-ttu-id="11267-145">运行示例应用，获取从其配置值`IConfigurationRoot`具有作为机密名称相同的名称。</span><span class="sxs-lookup"><span data-stu-id="11267-145">Run the sample app, which obtains its configuration values from `IConfigurationRoot` with the same name as the secret name.</span></span>
   * <span data-ttu-id="11267-146">非层次结构值： 的值`SecretName`一起被获取`config["SecretName"]`。</span><span class="sxs-lookup"><span data-stu-id="11267-146">Non-hierarchical values: The value for `SecretName` is obtained with `config["SecretName"]`.</span></span>
   * <span data-ttu-id="11267-147">层次结构的值 （部分）： 使用`:`（冒号） 表示法或`GetSection`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="11267-147">Hierarchical values (sections): Use `:` (colon) notation or the `GetSection` extension method.</span></span> <span data-ttu-id="11267-148">使用任一方法获取的配置值：</span><span class="sxs-lookup"><span data-stu-id="11267-148">Use either of these approaches to obtain the configuration value:</span></span>
     * `config["Section:SecretName"]`
     * `config.GetSection("Section")["SecretName"]`

<span data-ttu-id="11267-149">运行应用时，网页显示加载的机密值：</span><span class="sxs-lookup"><span data-stu-id="11267-149">When you run the app, a webpage shows the loaded secret values:</span></span>

![通过使用 Azure 密钥保管库配置提供程序加载浏览器窗口，其中显示密钥值](key-vault-configuration/_static/sample1.png)

## <a name="bind-an-array-to-a-class"></a><span data-ttu-id="11267-151">将数组绑定至类</span><span class="sxs-lookup"><span data-stu-id="11267-151">Bind an array to a class</span></span>

<span data-ttu-id="11267-152">提供程序支持的配置值读入数组绑定到 POCO 数组。</span><span class="sxs-lookup"><span data-stu-id="11267-152">The provider is capable of reading configuration values into an array for binding to a POCO array.</span></span>

<span data-ttu-id="11267-153">从允许包含冒号的键的配置源读取数据时 (`:`) 使用分隔符，数字键段来区分对数组组成的密钥 (`:0:`， `:1:`，...</span><span class="sxs-lookup"><span data-stu-id="11267-153">When reading from a configuration source that allows keys to contain colon (`:`) separators, a numeric key segment is used to distinguish the keys that make up an array (`:0:`, `:1:`, …</span></span> <span data-ttu-id="11267-154">`:{n}:`）格式模式中出现的位置生成。</span><span class="sxs-lookup"><span data-stu-id="11267-154">`:{n}:`).</span></span> <span data-ttu-id="11267-155">有关详细信息，请参阅[配置： 将数组绑定到一个类](xref:fundamentals/configuration/index#bind-an-array-to-a-class)。</span><span class="sxs-lookup"><span data-stu-id="11267-155">For more information, see [Configuration: Bind an array to a class](xref:fundamentals/configuration/index#bind-an-array-to-a-class).</span></span>

<span data-ttu-id="11267-156">Azure 密钥保管库密钥不能使用冒号作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="11267-156">Azure Key Vault keys can't use a colon as a separator.</span></span> <span data-ttu-id="11267-157">本主题中介绍的方法使用双短划线 (`--`) 作为 （部分） 的层次结构值的分隔符。</span><span class="sxs-lookup"><span data-stu-id="11267-157">The approach described in this topic uses double dashes (`--`) as a separator for hierarchical values (sections).</span></span> <span data-ttu-id="11267-158">使用双短划线和数值的关键段数组密钥存储在 Azure 密钥保管库 (`--0--`， `--1--`，...</span><span class="sxs-lookup"><span data-stu-id="11267-158">Array keys are stored in Azure Key Vault with double dashes and numeric key segments (`--0--`, `--1--`, …</span></span> <span data-ttu-id="11267-159">`--{n}--`）格式模式中出现的位置生成。</span><span class="sxs-lookup"><span data-stu-id="11267-159">`--{n}--`).</span></span>

<span data-ttu-id="11267-160">请参阅以下[Serilog](https://serilog.net/)日志记录提供程序配置提供的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="11267-160">Examine the following [Serilog](https://serilog.net/) logging provider configuration provided by a JSON file.</span></span> <span data-ttu-id="11267-161">有两个对象中定义的文本`WriteTo`数组，它反映两个 Serilog*接收器*，其中介绍了日志记录输出的目标：</span><span class="sxs-lookup"><span data-stu-id="11267-161">There are two object literals defined in the `WriteTo` array that reflect two Serilog *sinks*, which describe destinations for logging output:</span></span>

```json
"Serilog": {
  "WriteTo": [
    {
      "Name": "AzureTableStorage",
      "Args": {
        "storageTableName": "logs",
        "connectionString": "DefaultEnd...ountKey=Eby8...GMGw=="
      }
    },
    {
      "Name": "AzureDocumentDB",
      "Args": {
        "endpointUrl": "https://contoso.documents.azure.com:443",
        "authorizationKey": "Eby8...GMGw=="
      }
    }
  ]
}
```

<span data-ttu-id="11267-162">在上面的 JSON 文件中所示的配置存储在 Azure 密钥保管库中使用双短划线 (`--`) 表示法和数字段：</span><span class="sxs-lookup"><span data-stu-id="11267-162">The configuration shown in the preceding JSON file is stored in Azure Key Vault using double dash (`--`) notation and numeric segments:</span></span>

| <span data-ttu-id="11267-163">键</span><span class="sxs-lookup"><span data-stu-id="11267-163">Key</span></span> | <span data-ttu-id="11267-164">“值”</span><span class="sxs-lookup"><span data-stu-id="11267-164">Value</span></span> |
| --- | ----- |
| `Serilog--WriteTo--0--Name` | `AzureTableStorage` |
| `Serilog--WriteTo--0--Args--storageTableName` | `logs` |
| `Serilog--WriteTo--0--Args--connectionString` | `DefaultEnd...ountKey=Eby8...GMGw==` |
| `Serilog--WriteTo--1--Name` | `AzureDocumentDB` |
| `Serilog--WriteTo--1--Args--endpointUrl` | `https://contoso.documents.azure.com:443` |
| `Serilog--WriteTo--1--Args--authorizationKey` | `Eby8...GMGw==` |

## <a name="create-prefixed-key-vault-secrets-and-load-configuration-values-key-name-prefix-sample"></a><span data-ttu-id="11267-165">创建带前缀的密钥保管库机密并加载配置值 （密钥的名称的前缀的示例）</span><span class="sxs-lookup"><span data-stu-id="11267-165">Create prefixed key vault secrets and load configuration values (key-name-prefix-sample)</span></span>

<span data-ttu-id="11267-166">`AddAzureKeyVault` 此外提供了接受的实现的重载`IKeyVaultSecretManager`，可用于控制如何密钥保管库机密将转换为配置项。</span><span class="sxs-lookup"><span data-stu-id="11267-166">`AddAzureKeyVault` also provides an overload that accepts an implementation of `IKeyVaultSecretManager`, which allows you to control how key vault secrets are converted into configuration keys.</span></span> <span data-ttu-id="11267-167">例如，可以实现的接口来加载基于你在应用启动时提供的前缀值的机密值。</span><span class="sxs-lookup"><span data-stu-id="11267-167">For example, you can implement the interface to load secret values based on a prefix value you provide at app startup.</span></span> <span data-ttu-id="11267-168">这可以使您例如，若要加载基于应用的版本的密钥。</span><span class="sxs-lookup"><span data-stu-id="11267-168">This allows you, for example, to load secrets based on the version of the app.</span></span>

> [!WARNING]
> <span data-ttu-id="11267-169">若要将多个应用的机密放入同一个密钥保管库或将环境机密不使用在密钥保管库机密的前缀 (例如，*开发*而不是*生产*机密) 到相同保管库。</span><span class="sxs-lookup"><span data-stu-id="11267-169">Don't use prefixes on key vault secrets to place secrets for multiple apps into the same key vault or to place environmental secrets (for example, *development* versus *production* secrets) into the same vault.</span></span> <span data-ttu-id="11267-170">我们建议，不同的应用程序和开发/生产环境使用单独的密钥保管库来隔离应用环境的最高级别的安全性。</span><span class="sxs-lookup"><span data-stu-id="11267-170">We recommend that different apps and development/production environments use separate key vaults to isolate app environments for the highest level of security.</span></span>

<span data-ttu-id="11267-171">使用第二个示例应用程序，在 key vault 中创建机密`5000-AppSecret`（密钥保管库机密名称中不允许句点） 表示您的应用程序的版本为 5.0.0.0 应用程序密码。</span><span class="sxs-lookup"><span data-stu-id="11267-171">Using the second sample app, you create a secret in the key vault for `5000-AppSecret` (periods aren't allowed in key vault secret names) representing an app secret for version 5.0.0.0 of your app.</span></span> <span data-ttu-id="11267-172">有关另一个版本，5.1.0.0，创建的机密`5100-AppSecret`。</span><span class="sxs-lookup"><span data-stu-id="11267-172">For another version, 5.1.0.0, you create a secret for `5100-AppSecret`.</span></span> <span data-ttu-id="11267-173">每个应用程序版本将其自己的机密值加载到作为其配置`AppSecret`、 在加载机密的版本剥离。</span><span class="sxs-lookup"><span data-stu-id="11267-173">Each app version loads its own secret value into its configuration as `AppSecret`, stripping off the version as it loads the secret.</span></span> <span data-ttu-id="11267-174">该示例的实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="11267-174">The sample's implementation is shown below:</span></span>

[!code-csharp[Configuration builder](key-vault-configuration/samples/key-name-prefix-sample/2.x/Program.cs?name=snippet1&highlight=18)]

[!code-csharp[PrefixKeyVaultSecretManager](key-vault-configuration/samples/key-name-prefix-sample/2.x/Startup.cs?name=snippet1)]

<span data-ttu-id="11267-175">`Load`方法调用循环访问保管库机密以找出具有版本前缀的提供程序算法。</span><span class="sxs-lookup"><span data-stu-id="11267-175">The `Load` method is called by a provider algorithm that iterates through the vault secrets to find the ones that have the version prefix.</span></span> <span data-ttu-id="11267-176">当版本前缀找到`Load`，该算法使用`GetKey`方法返回的机密名称的配置名称。</span><span class="sxs-lookup"><span data-stu-id="11267-176">When a version prefix is found with `Load`, the algorithm uses the `GetKey` method to return the configuration name of the secret name.</span></span> <span data-ttu-id="11267-177">它剥离机密的名称从版本前缀，并返回到应用程序的配置名称-值对的加载的机密名称的其余部分。</span><span class="sxs-lookup"><span data-stu-id="11267-177">It strips off the version prefix from the secret's name and returns the rest of the secret name for loading into the app's configuration name-value pairs.</span></span>

<span data-ttu-id="11267-178">当您实现这种方法：</span><span class="sxs-lookup"><span data-stu-id="11267-178">When you implement this approach:</span></span>

1. <span data-ttu-id="11267-179">密钥保管库机密进行加载。</span><span class="sxs-lookup"><span data-stu-id="11267-179">The key vault secrets are loaded.</span></span>
2. <span data-ttu-id="11267-180">字符串密码`5000-AppSecret`匹配。</span><span class="sxs-lookup"><span data-stu-id="11267-180">The string secret for `5000-AppSecret` is matched.</span></span>
3. <span data-ttu-id="11267-181">版本`5000`去除 （替换为短划线），从离开的键名`AppSecret`机密值加载到应用的配置。</span><span class="sxs-lookup"><span data-stu-id="11267-181">The version, `5000` (with the dash), is stripped off of the key name leaving `AppSecret` to load with the secret value into the app's configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="11267-182">您还可以提供您自己`KeyVaultClient`实现`AddAzureKeyVault`。</span><span class="sxs-lookup"><span data-stu-id="11267-182">You can also provide your own `KeyVaultClient` implementation to `AddAzureKeyVault`.</span></span> <span data-ttu-id="11267-183">提供自定义客户端可以共享单个实例的配置提供程序和您的应用程序的其他部件之间的客户端。</span><span class="sxs-lookup"><span data-stu-id="11267-183">Supplying a custom client allows you to share a single instance of the client between the configuration provider and other parts of your app.</span></span>

1. <span data-ttu-id="11267-184">创建密钥保管库并将设置 Azure Active Directory (Azure AD) 应用程序中的指南[开始使用 Azure 密钥保管库](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="11267-184">Create a key vault and set up Azure Active Directory (Azure AD) for the app following the guidance in [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).</span></span>
   * <span data-ttu-id="11267-185">将机密添加到密钥保管库使用[AzureRM 密钥保管库 PowerShell 模块](/powershell/module/azurerm.keyvault)从可用[PowerShell 库](https://www.powershellgallery.com/packages/AzureRM.KeyVault)，则[Azure 密钥保管库 REST API](/rest/api/keyvault/)，或者[Azure 门户](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="11267-185">Add secrets to the key vault using the [AzureRM Key Vault PowerShell Module](/powershell/module/azurerm.keyvault) available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.KeyVault), the [Azure Key Vault REST API](/rest/api/keyvault/), or the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="11267-186">为创建的机密*手动*或*证书*机密。</span><span class="sxs-lookup"><span data-stu-id="11267-186">Secrets are created as either *Manual* or *Certificate* secrets.</span></span> <span data-ttu-id="11267-187">*证书*机密使用的应用和服务证书，但不是支持配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="11267-187">*Certificate* secrets are certificates for use by apps and services but are not supported by the configuration provider.</span></span> <span data-ttu-id="11267-188">应使用*手动*选项可创建带有配置提供程序使用的名称-值对机密。</span><span class="sxs-lookup"><span data-stu-id="11267-188">You should use the *Manual* option to create name-value pair secrets for use with the configuration provider.</span></span>
     * <span data-ttu-id="11267-189">层次结构的值 （配置节） 使用`--`（两个短划线） 作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="11267-189">Hierarchical values (configuration sections) use `--` (two dashes) as a separator.</span></span>
     * <span data-ttu-id="11267-190">创建两个*手动*具有以下名称 / 值对的机密：</span><span class="sxs-lookup"><span data-stu-id="11267-190">Create two *Manual* secrets with the following name-value pairs:</span></span>
       * <span data-ttu-id="11267-191">`5000-AppSecret`: `5.0.0.0_secret_value`</span><span class="sxs-lookup"><span data-stu-id="11267-191">`5000-AppSecret`: `5.0.0.0_secret_value`</span></span>
       * <span data-ttu-id="11267-192">`5100-AppSecret`: `5.1.0.0_secret_value`</span><span class="sxs-lookup"><span data-stu-id="11267-192">`5100-AppSecret`: `5.1.0.0_secret_value`</span></span>
   * <span data-ttu-id="11267-193">与 Azure Active Directory 中注册示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="11267-193">Register the sample app with Azure Active Directory.</span></span>
   * <span data-ttu-id="11267-194">授权应用访问密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="11267-194">Authorize the app to access the key vault.</span></span> <span data-ttu-id="11267-195">当你使用`Set-AzureRmKeyVaultAccessPolicy`PowerShell cmdlet 来授权应用程序访问密钥保管库，提供`List`并`Get`对使用机密的访问`-PermissionsToSecrets list,get`。</span><span class="sxs-lookup"><span data-stu-id="11267-195">When you use the `Set-AzureRmKeyVaultAccessPolicy` PowerShell cmdlet to authorize the app to access the key vault, provide `List` and `Get` access to secrets with `-PermissionsToSecrets list,get`.</span></span>

2. <span data-ttu-id="11267-196">更新应用程序的*appsettings.json*包含的值的文件`Vault`， `ClientId`，和`ClientSecret`。</span><span class="sxs-lookup"><span data-stu-id="11267-196">Update the app's *appsettings.json* file with the values of `Vault`, `ClientId`, and `ClientSecret`.</span></span>
3. <span data-ttu-id="11267-197">运行示例应用，获取从其配置值`IConfigurationRoot`具有作为带前缀的机密名称相同的名称。</span><span class="sxs-lookup"><span data-stu-id="11267-197">Run the sample app, which obtains its configuration values from `IConfigurationRoot` with the same name as the prefixed secret name.</span></span> <span data-ttu-id="11267-198">在此示例中，前缀是应用的版本，提供给`PrefixKeyVaultSecretManager`添加 Azure Key Vault 配置提供程序时。</span><span class="sxs-lookup"><span data-stu-id="11267-198">In this sample, the prefix is the app's version, which you provided to the `PrefixKeyVaultSecretManager` when you added the Azure Key Vault configuration provider.</span></span> <span data-ttu-id="11267-199">值`AppSecret`一起被获取`config["AppSecret"]`。</span><span class="sxs-lookup"><span data-stu-id="11267-199">The value for `AppSecret` is obtained with `config["AppSecret"]`.</span></span> <span data-ttu-id="11267-200">由应用生成的网页显示加载的值：</span><span class="sxs-lookup"><span data-stu-id="11267-200">The webpage generated by the app shows the loaded value:</span></span>

   ![浏览器窗口中显示为 5.0.0.0 应用的版本时，通过使用 Azure 密钥保管库配置提供程序加载的机密值](key-vault-configuration/_static/sample2-1.png)

4. <span data-ttu-id="11267-202">更改中的项目文件中的应用程序集版本`5.0.0.0`到`5.1.0.0`并再次运行应用。</span><span class="sxs-lookup"><span data-stu-id="11267-202">Change the version of the app assembly in the project file from `5.0.0.0` to `5.1.0.0` and run the app again.</span></span> <span data-ttu-id="11267-203">这一次，返回的机密值是`5.1.0.0_secret_value`。</span><span class="sxs-lookup"><span data-stu-id="11267-203">This time, the secret value returned is `5.1.0.0_secret_value`.</span></span> <span data-ttu-id="11267-204">由应用生成的网页显示加载的值：</span><span class="sxs-lookup"><span data-stu-id="11267-204">The webpage generated by the app shows the loaded value:</span></span>

   ![浏览器窗口，其中显示 5.1.0.0 应用的版本时，通过使用 Azure 密钥保管库配置提供程序加载的机密值](key-vault-configuration/_static/sample2-2.png)

## <a name="control-access-to-the-clientsecret"></a><span data-ttu-id="11267-206">控制对客户端密码的访问</span><span class="sxs-lookup"><span data-stu-id="11267-206">Control access to the ClientSecret</span></span>

<span data-ttu-id="11267-207">使用[机密管理器工具](xref:security/app-secrets)维护`ClientSecret`外部项目源树。</span><span class="sxs-lookup"><span data-stu-id="11267-207">Use the [Secret Manager tool](xref:security/app-secrets) to maintain the `ClientSecret` outside of your project source tree.</span></span> <span data-ttu-id="11267-208">使用机密管理器中，你将应用程序机密与特定项目相关联并跨多个项目共享它们。</span><span class="sxs-lookup"><span data-stu-id="11267-208">With Secret Manager, you associate app secrets with a specific project and share them across multiple projects.</span></span>

<span data-ttu-id="11267-209">在开发环境支持证书中的.NET Framework 应用时，可以使用 X.509 证书验证到 Azure 密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="11267-209">When developing a .NET Framework app in an environment that supports certificates, you can authenticate to Azure Key Vault with an X.509 certificate.</span></span> <span data-ttu-id="11267-210">X.509 证书的私钥由操作系统管理。</span><span class="sxs-lookup"><span data-stu-id="11267-210">The X.509 certificate's private key is managed by the OS.</span></span> <span data-ttu-id="11267-211">有关详细信息，请参阅[使用证书而不是客户端密码进行身份验证](/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret)。</span><span class="sxs-lookup"><span data-stu-id="11267-211">For more information, see [Authenticate with a Certificate instead of a Client Secret](/azure/key-vault/key-vault-use-from-web-application#authenticate-with-a-certificate-instead-of-a-client-secret).</span></span> <span data-ttu-id="11267-212">使用`AddAzureKeyVault`接受重载`X509Certificate2`(`_env`在下面的示例：</span><span class="sxs-lookup"><span data-stu-id="11267-212">Use the `AddAzureKeyVault` overload that accepts an `X509Certificate2` (`_env` in the following example :</span></span>

```csharp
var builtConfig = config.Build();

var store = new X509Store(StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
var cert = store.Certificates
    .Find(X509FindType.FindByThumbprint, 
        config["CertificateThumbprint"], false);

config.AddAzureKeyVault(
    builtConfig["Vault"],
    builtConfig["ClientId"],
    cert.OfType<X509Certificate2>().Single(),
    new EnvironmentSecretManager(context.HostingEnvironment.ApplicationName));

store.Close();
```

## <a name="reload-secrets"></a><span data-ttu-id="11267-213">重新加载机密</span><span class="sxs-lookup"><span data-stu-id="11267-213">Reload secrets</span></span>

<span data-ttu-id="11267-214">机密缓存，直至`IConfigurationRoot.Reload()`调用。</span><span class="sxs-lookup"><span data-stu-id="11267-214">Secrets are cached until `IConfigurationRoot.Reload()` is called.</span></span> <span data-ttu-id="11267-215">已过期，已禁用，并且已更新密钥保管库中的机密不遵循之前应用此`Reload`执行。</span><span class="sxs-lookup"><span data-stu-id="11267-215">Expired, disabled, and updated secrets in the key vault are not respected by the app until `Reload` is executed.</span></span>

```csharp
Configuration.Reload();
```

## <a name="disabled-and-expired-secrets"></a><span data-ttu-id="11267-216">已禁用和过期的机密</span><span class="sxs-lookup"><span data-stu-id="11267-216">Disabled and expired secrets</span></span>

<span data-ttu-id="11267-217">已禁用并已过期机密引发`KeyVaultClientException`。</span><span class="sxs-lookup"><span data-stu-id="11267-217">Disabled and expired secrets throw a `KeyVaultClientException`.</span></span> <span data-ttu-id="11267-218">若要防止应用引发，将为您的应用程序或更新已禁用或已过期机密。</span><span class="sxs-lookup"><span data-stu-id="11267-218">To prevent your app from throwing, replace your app or update the disabled/expired secret.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="11267-219">疑难解答</span><span class="sxs-lookup"><span data-stu-id="11267-219">Troubleshoot</span></span>

<span data-ttu-id="11267-220">如果应用程序无法加载使用提供程序的配置，一条错误消息写入到[ASP.NET Core 日志记录基础结构](xref:fundamentals/logging/index)。</span><span class="sxs-lookup"><span data-stu-id="11267-220">When the app fails to load configuration using the provider, an error message is written to the [ASP.NET Core Logging infrastructure](xref:fundamentals/logging/index).</span></span> <span data-ttu-id="11267-221">以下条件下将不加载配置：</span><span class="sxs-lookup"><span data-stu-id="11267-221">The following conditions will prevent configuration from loading:</span></span>

* <span data-ttu-id="11267-222">应用未正确配置 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="11267-222">The app isn't configured correctly in Azure Active Directory.</span></span>
* <span data-ttu-id="11267-223">密钥保管库不存在于 Azure 密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="11267-223">The key vault doesn't exist in Azure Key Vault.</span></span>
* <span data-ttu-id="11267-224">应用程序无权访问密钥保管库。</span><span class="sxs-lookup"><span data-stu-id="11267-224">The app isn't authorized to access the key vault.</span></span>
* <span data-ttu-id="11267-225">访问策略不包括`Get`和`List`权限。</span><span class="sxs-lookup"><span data-stu-id="11267-225">The access policy doesn't include `Get` and `List` permissions.</span></span>
* <span data-ttu-id="11267-226">在密钥保管库，配置数据 （名称 / 值对） 是错误命名为，缺少，禁用，或已过期。</span><span class="sxs-lookup"><span data-stu-id="11267-226">In the key vault, the configuration data (name-value pair) is incorrectly named, missing, disabled, or expired.</span></span>
* <span data-ttu-id="11267-227">应用了错误的密钥保管库名称 (`Vault`)，Azure AD 应用程序 Id (`ClientId`)，或 Azure AD 密钥 (`ClientSecret`)。</span><span class="sxs-lookup"><span data-stu-id="11267-227">The app has the wrong key vault name (`Vault`), Azure AD App Id (`ClientId`), or Azure AD Key (`ClientSecret`).</span></span>
* <span data-ttu-id="11267-228">Azure AD 密钥 (`ClientSecret`) 已过期。</span><span class="sxs-lookup"><span data-stu-id="11267-228">The Azure AD Key (`ClientSecret`) is expired.</span></span>
* <span data-ttu-id="11267-229">配置密钥 （名称） 不正确的应用中的想要加载的值。</span><span class="sxs-lookup"><span data-stu-id="11267-229">The configuration key (name) is incorrect in the app for the value you're trying to load.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11267-230">其他资源</span><span class="sxs-lookup"><span data-stu-id="11267-230">Additional resources</span></span>

* <xref:fundamentals/configuration/index>
* [<span data-ttu-id="11267-231">Microsoft Azure： 密钥保管库</span><span class="sxs-lookup"><span data-stu-id="11267-231">Microsoft Azure: Key Vault</span></span>](https://azure.microsoft.com/services/key-vault/)
* [<span data-ttu-id="11267-232">Microsoft Azure： 密钥保管库文档</span><span class="sxs-lookup"><span data-stu-id="11267-232">Microsoft Azure: Key Vault Documentation</span></span>](/azure/key-vault/)
* [<span data-ttu-id="11267-233">如何生成和传输受 HSM 保护密钥的 Azure 密钥保管库</span><span class="sxs-lookup"><span data-stu-id="11267-233">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>](/azure/key-vault/key-vault-hsm-protected-keys)
* [<span data-ttu-id="11267-234">KeyVaultClient 类</span><span class="sxs-lookup"><span data-stu-id="11267-234">KeyVaultClient Class</span></span>](/dotnet/api/microsoft.azure.keyvault.keyvaultclient)
