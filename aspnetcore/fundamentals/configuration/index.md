---
title: ASP.NET Core 中的配置
author: guardrex
description: 理解如何使用配置 API 配置 ASP.NET Core 应用。
ms.author: riande
ms.custom: mvc
ms.date: 10/09/2018
uid: fundamentals/configuration/index
ms.openlocfilehash: 35f283becd156da22a4d9d2034055ee79b75ffda
ms.sourcegitcommit: 4bdf7703aed86ebd56b9b4bae9ad5700002af32d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2018
ms.locfileid: "49326168"
---
# <a name="configuration-in-aspnet-core"></a><span data-ttu-id="e757a-103">ASP.NET Core 中的配置</span><span class="sxs-lookup"><span data-stu-id="e757a-103">Configuration in ASP.NET Core</span></span>

<span data-ttu-id="e757a-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="e757a-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="e757a-105">ASP.NET Core 中的应用配置基于配置提供程序建立的键值对。</span><span class="sxs-lookup"><span data-stu-id="e757a-105">App configuration in ASP.NET Core is based on key-value pairs established by *configuration providers*.</span></span> <span data-ttu-id="e757a-106">配置提供程序将配置数据从各种配置源读取到键值对：</span><span class="sxs-lookup"><span data-stu-id="e757a-106">Configuration providers read configuration data into key-value pairs from a variety of configuration sources:</span></span>

::: moniker range=">= aspnetcore-2.1"

* <span data-ttu-id="e757a-107">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e757a-107">Azure Key Vault</span></span>
* <span data-ttu-id="e757a-108">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-108">Command-line arguments</span></span>
* <span data-ttu-id="e757a-109">（已安装或已创建的）自定义提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-109">Custom providers (installed or created)</span></span>
* <span data-ttu-id="e757a-110">目录文件</span><span class="sxs-lookup"><span data-stu-id="e757a-110">Directory files</span></span>
* <span data-ttu-id="e757a-111">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-111">Environment variables</span></span>
* <span data-ttu-id="e757a-112">内存中的 .NET 对象</span><span class="sxs-lookup"><span data-stu-id="e757a-112">In-memory .NET objects</span></span>
* <span data-ttu-id="e757a-113">设置文件</span><span class="sxs-lookup"><span data-stu-id="e757a-113">Settings files</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0 || aspnetcore-1.1"

* <span data-ttu-id="e757a-114">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e757a-114">Azure Key Vault</span></span>
* <span data-ttu-id="e757a-115">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-115">Command-line arguments</span></span>
* <span data-ttu-id="e757a-116">（已安装或已创建的）自定义提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-116">Custom providers (installed or created)</span></span>
* <span data-ttu-id="e757a-117">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-117">Environment variables</span></span>
* <span data-ttu-id="e757a-118">内存中的 .NET 对象</span><span class="sxs-lookup"><span data-stu-id="e757a-118">In-memory .NET objects</span></span>
* <span data-ttu-id="e757a-119">设置文件</span><span class="sxs-lookup"><span data-stu-id="e757a-119">Settings files</span></span>

::: moniker-end

::: moniker range="= aspnetcore-1.0"

* <span data-ttu-id="e757a-120">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-120">Command-line arguments</span></span>
* <span data-ttu-id="e757a-121">（已安装或已创建的）自定义提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-121">Custom providers (installed or created)</span></span>
* <span data-ttu-id="e757a-122">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-122">Environment variables</span></span>
* <span data-ttu-id="e757a-123">内存中的 .NET 对象</span><span class="sxs-lookup"><span data-stu-id="e757a-123">In-memory .NET objects</span></span>
* <span data-ttu-id="e757a-124">设置文件</span><span class="sxs-lookup"><span data-stu-id="e757a-124">Settings files</span></span>

::: moniker-end

<span data-ttu-id="e757a-125">选项模式是本主题中描述的配置概念的扩展。</span><span class="sxs-lookup"><span data-stu-id="e757a-125">The *options pattern* is an extension of the configuration concepts described in this topic.</span></span> <span data-ttu-id="e757a-126">选项使用类来表示相关设置的组。</span><span class="sxs-lookup"><span data-stu-id="e757a-126">Options uses classes to represent groups of related settings.</span></span> <span data-ttu-id="e757a-127">有关使用选项模式的详细信息，请参阅 <xref:fundamentals/configuration/options>。</span><span class="sxs-lookup"><span data-stu-id="e757a-127">For more information on using the options pattern, see <xref:fundamentals/configuration/options>.</span></span>

<span data-ttu-id="e757a-128">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/index/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="e757a-128">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/configuration/index/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="e757a-129">本主题中提供的示例依赖于以下内容：</span><span class="sxs-lookup"><span data-stu-id="e757a-129">The examples provided in this topic rely upon:</span></span>

* <span data-ttu-id="e757a-130">使用 <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*> 设置应用的基本路径。</span><span class="sxs-lookup"><span data-stu-id="e757a-130">Setting the base path of the app with <xref:Microsoft.Extensions.Configuration.FileConfigurationExtensions.SetBasePath*>.</span></span> <span data-ttu-id="e757a-131">通过引用 [Microsoft.Extensions.Configuration.FileExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.FileExtensions/) 包，可以向应用提供 `SetBasePath`。</span><span class="sxs-lookup"><span data-stu-id="e757a-131">`SetBasePath` is made available to an app by referencing the [Microsoft.Extensions.Configuration.FileExtensions](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.FileExtensions/) package.</span></span>
* <span data-ttu-id="e757a-132">使用 <xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*> 解析配置文件的各个部分。</span><span class="sxs-lookup"><span data-stu-id="e757a-132">Resolving sections of configuration files with <xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*>.</span></span> <span data-ttu-id="e757a-133">通过引用 [Microsoft.Extensions.Configuration](https://www.nuget.org/packages/Microsoft.Extensions.Configuration/) 包向应用提供 `GetSection`。</span><span class="sxs-lookup"><span data-stu-id="e757a-133">`GetSection` is made available to an app by referencing the [Microsoft.Extensions.Configuration](https://www.nuget.org/packages/Microsoft.Extensions.Configuration/) package.</span></span>
* <span data-ttu-id="e757a-134">使用 <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> 和 [Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) 将配置绑定到 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="e757a-134">Binding configuration to .NET classes with <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> and [Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*).</span></span> <span data-ttu-id="e757a-135">通过引用 [Microsoft.Extensions.Configuration.Binder](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Binder/) 包向应用提供 `Bind` 和 `Get<T>`。</span><span class="sxs-lookup"><span data-stu-id="e757a-135">`Bind` and `Get<T>` are made available to an app by referencing the [Microsoft.Extensions.Configuration.Binder](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.Binder/) package.</span></span> <span data-ttu-id="e757a-136">ASP.NET Core 1.1 或更高版本中提供了 `Get<T>`。</span><span class="sxs-lookup"><span data-stu-id="e757a-136">`Get<T>` is available in ASP.NET Core 1.1 or later.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-137">这三个包均包括在 [Microsoft.AspNetCore.App 元包](xref:fundamentals/metapackage-app)中。</span><span class="sxs-lookup"><span data-stu-id="e757a-137">These three packages are included in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-138">这三个包均包括在 [Microsoft.AspNetCore.All 元包](xref:fundamentals/metapackage)中。</span><span class="sxs-lookup"><span data-stu-id="e757a-138">These three packages are included in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span>

::: moniker-end

## <a name="host-vs-app-configuration"></a><span data-ttu-id="e757a-139">主机与应用配置</span><span class="sxs-lookup"><span data-stu-id="e757a-139">Host vs. app configuration</span></span>

<span data-ttu-id="e757a-140">在配置并启动应用之前，配置并启动主机。</span><span class="sxs-lookup"><span data-stu-id="e757a-140">Before the app is configured and started, a *host* is configured and launched.</span></span> <span data-ttu-id="e757a-141">主机负责应用程序启动和生存期管理。</span><span class="sxs-lookup"><span data-stu-id="e757a-141">The host is responsible for app startup and lifetime management.</span></span> <span data-ttu-id="e757a-142">应用和主机均使用本主题中所述的配置提供程序进行配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-142">Both the app and the host are configured using the configuration providers described in this topic.</span></span> <span data-ttu-id="e757a-143">主机配置键值对成为应用的全局配置的一部分。</span><span class="sxs-lookup"><span data-stu-id="e757a-143">Host configuration key-value pairs become part of the app's global configuration.</span></span> <span data-ttu-id="e757a-144">有关在构建主机时如何使用配置提供程序以及配置源如何影响主机配置的详细信息，请参阅 <xref:fundamentals/host/index>。</span><span class="sxs-lookup"><span data-stu-id="e757a-144">For more information on how the configuration providers are used when the host is built and how configuration sources affect host configuration, see <xref:fundamentals/host/index>.</span></span>

## <a name="security"></a><span data-ttu-id="e757a-145">安全性</span><span class="sxs-lookup"><span data-stu-id="e757a-145">Security</span></span>

<span data-ttu-id="e757a-146">采用以下最佳实践：</span><span class="sxs-lookup"><span data-stu-id="e757a-146">Adopt the following best practices:</span></span>

* <span data-ttu-id="e757a-147">请勿在配置提供程序代码或纯文本配置文件中存储密码或其他敏感数据。</span><span class="sxs-lookup"><span data-stu-id="e757a-147">Never store passwords or other sensitive data in configuration provider code or in plain text configuration files.</span></span>
* <span data-ttu-id="e757a-148">不要在开发或测试环境中使用生产机密。</span><span class="sxs-lookup"><span data-stu-id="e757a-148">Don't use production secrets in development or test environments.</span></span>
* <span data-ttu-id="e757a-149">请在项目外部指定机密，避免将其意外提交到源代码存储库。</span><span class="sxs-lookup"><span data-stu-id="e757a-149">Specify secrets outside of the project so that they can't be accidentally committed to a source code repository.</span></span>

<span data-ttu-id="e757a-150">详细了解[如何使用多个环境](xref:fundamentals/environments)和管理[使用 Secret Manager 的开发中的应用机密的安全存储](xref:security/app-secrets)（包括使用环境变量存储敏感数据的建议）。</span><span class="sxs-lookup"><span data-stu-id="e757a-150">Learn more about [how to use multiple environments](xref:fundamentals/environments) and managing the [safe storage of app secrets in development with the Secret Manager](xref:security/app-secrets) (includes advice on using environment variables to store sensitive data).</span></span> <span data-ttu-id="e757a-151">Secret Manager 使用文件配置提供程序将用户机密存储在本地系统上的 JSON 文件中。</span><span class="sxs-lookup"><span data-stu-id="e757a-151">The Secret Manager uses the File Configuration Provider to store user secrets in a JSON file on the local system.</span></span> <span data-ttu-id="e757a-152">本主题后面将介绍文件配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-152">The File Configuration Provider is described later in this topic.</span></span>

<span data-ttu-id="e757a-153">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 是安全存储应用机密的一种选择。</span><span class="sxs-lookup"><span data-stu-id="e757a-153">[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) is one option for the safe storage of app secrets.</span></span> <span data-ttu-id="e757a-154">有关更多信息，请参见<xref:security/key-vault-configuration>。</span><span class="sxs-lookup"><span data-stu-id="e757a-154">For more information, see <xref:security/key-vault-configuration>.</span></span>

## <a name="hierarchical-configuration-data"></a><span data-ttu-id="e757a-155">分层配置数据</span><span class="sxs-lookup"><span data-stu-id="e757a-155">Hierarchical configuration data</span></span>

<span data-ttu-id="e757a-156">配置 API 能够通过在配置键中使用分隔符来展平分层数据以保持分层配置数据。</span><span class="sxs-lookup"><span data-stu-id="e757a-156">The Configuration API is capable of maintaining hierarchical configuration data by flattening the hierarchical data with the use of a delimiter in the configuration keys.</span></span>

<span data-ttu-id="e757a-157">在以下 JSON 文件中，两个节的结构化层次结构中存在四个键：</span><span class="sxs-lookup"><span data-stu-id="e757a-157">In the following JSON file, four keys exist in a structured hierarchy of two sections:</span></span>

```json
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  }
}
```

<span data-ttu-id="e757a-158">将文件读入配置时，将创建唯一键以保持配置源的原始分层数据结构。</span><span class="sxs-lookup"><span data-stu-id="e757a-158">When the file is read into configuration, unique keys are created to maintain the original hierarchical data structure of the configuration source.</span></span> <span data-ttu-id="e757a-159">使用冒号 (`:`) 展平节和键以保持原始结构：</span><span class="sxs-lookup"><span data-stu-id="e757a-159">The sections and keys are flattened with the use of a colon (`:`) to maintain the original structure:</span></span>

* <span data-ttu-id="e757a-160">section0:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-160">section0:key0</span></span>
* <span data-ttu-id="e757a-161">section0:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-161">section0:key1</span></span>
* <span data-ttu-id="e757a-162">section1:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-162">section1:key0</span></span>
* <span data-ttu-id="e757a-163">section1:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-163">section1:key1</span></span>

<span data-ttu-id="e757a-164"><xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*> 和 <xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*> 方法可用于隔离各个节和配置数据中某节的子节。</span><span class="sxs-lookup"><span data-stu-id="e757a-164"><xref:Microsoft.Extensions.Configuration.ConfigurationSection.GetSection*> and <xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*> methods are available to isolate sections and children of a section in the configuration data.</span></span> <span data-ttu-id="e757a-165">稍后将在 [GetSection、GetChildren 和 Exists](#getsection-getchildren-and-exists) 中介绍这些方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-165">These methods are described later in [GetSection, GetChildren, and Exists](#getsection-getchildren-and-exists).</span></span>

## <a name="conventions"></a><span data-ttu-id="e757a-166">约定</span><span class="sxs-lookup"><span data-stu-id="e757a-166">Conventions</span></span>

<span data-ttu-id="e757a-167">在应用启动时，将按照指定的配置提供程序的顺序读取配置源。</span><span class="sxs-lookup"><span data-stu-id="e757a-167">At app startup, configuration sources are read in the order that their configuration providers are specified.</span></span>

<span data-ttu-id="e757a-168">应用启动后，在更改基础设置文件时，文件配置提供程序可以重载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-168">File Configuration Providers have the ability to reload configuration when an underlying settings file is changed after app startup.</span></span> <span data-ttu-id="e757a-169">本主题后面将介绍文件配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-169">The File Configuration Provider is described later in this topic.</span></span>

<span data-ttu-id="e757a-170">应用的[依赖关系注入 (DI)](xref:fundamentals/dependency-injection) 容器中提供了 <xref:Microsoft.Extensions.Configuration.IConfiguration>。</span><span class="sxs-lookup"><span data-stu-id="e757a-170"><xref:Microsoft.Extensions.Configuration.IConfiguration> is available in the app's [Dependency Injection (DI)](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="e757a-171">配置提供程序不能使用 DI，因为主机在设置这些提供程序时 DI 不可用。</span><span class="sxs-lookup"><span data-stu-id="e757a-171">Configuration providers can't utilize DI, as it's not available when they're set up by the host.</span></span>

<span data-ttu-id="e757a-172">配置键采用以下约定：</span><span class="sxs-lookup"><span data-stu-id="e757a-172">Configuration keys adopt the following conventions:</span></span>

* <span data-ttu-id="e757a-173">键不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="e757a-173">Keys are case-insensitive.</span></span> <span data-ttu-id="e757a-174">例如，`ConnectionString` 和 `connectionstring` 被视为等效键。</span><span class="sxs-lookup"><span data-stu-id="e757a-174">For example, `ConnectionString` and `connectionstring` are treated as equivalent keys.</span></span>
* <span data-ttu-id="e757a-175">如果由相同或不同的配置提供程序设置相同键的值，则键上设置的最后一个值就是所使用的值。</span><span class="sxs-lookup"><span data-stu-id="e757a-175">If a value for the same key is set by the same or different configuration providers, the last value set on the key is the value used.</span></span>
* <span data-ttu-id="e757a-176">分层键</span><span class="sxs-lookup"><span data-stu-id="e757a-176">Hierarchical keys</span></span>
  * <span data-ttu-id="e757a-177">在配置 API 中，冒号分隔符 (`:`) 适用于所有平台。</span><span class="sxs-lookup"><span data-stu-id="e757a-177">Within the Configuration API, a colon separator (`:`) works on all platforms.</span></span>
  * <span data-ttu-id="e757a-178">在环境变量中，冒号分隔符可能无法适用于所有平台。</span><span class="sxs-lookup"><span data-stu-id="e757a-178">In environment variables, a colon separator may not work on all platforms.</span></span> <span data-ttu-id="e757a-179">而所有平台均支持采用双下划线 (`__`)，并可以将其转换为冒号。</span><span class="sxs-lookup"><span data-stu-id="e757a-179">A double underscore (`__`) is supported by all platforms and is converted to a colon.</span></span>
  * <span data-ttu-id="e757a-180">在 Azure Key Vault 中，分层键使用 `--`（两个破折号）作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="e757a-180">In Azure Key Vault, hierarchical keys use `--` (two dashes) as a separator.</span></span> <span data-ttu-id="e757a-181">将机密加载到应用的配置中时，必须提供代码以用冒号替换破折号。</span><span class="sxs-lookup"><span data-stu-id="e757a-181">You must provide code to replace the dashes with a colon when the secrets are loaded into the app's configuration.</span></span>
* <span data-ttu-id="e757a-182"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder> 支持使用配置键中的数组索引将数组绑定到对象。</span><span class="sxs-lookup"><span data-stu-id="e757a-182">The <xref:Microsoft.Extensions.Configuration.ConfigurationBinder> supports binding arrays to objects using array indices in configuration keys.</span></span> <span data-ttu-id="e757a-183">数组绑定将在[将数组绑定到类](#bind-an-array-to-a-class)部分中进行介绍。</span><span class="sxs-lookup"><span data-stu-id="e757a-183">Array binding is described in the [Bind an array to a class](#bind-an-array-to-a-class) section.</span></span>

<span data-ttu-id="e757a-184">配置值采用以下约定：</span><span class="sxs-lookup"><span data-stu-id="e757a-184">Configuration values adopt the following conventions:</span></span>

* <span data-ttu-id="e757a-185">值是字符串。</span><span class="sxs-lookup"><span data-stu-id="e757a-185">Values are strings.</span></span>
* <span data-ttu-id="e757a-186">NULL 值不能存储在配置中或绑定到对象。</span><span class="sxs-lookup"><span data-stu-id="e757a-186">Null values can't be stored in configuration or bound to objects.</span></span>

## <a name="providers"></a><span data-ttu-id="e757a-187">提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-187">Providers</span></span>

<span data-ttu-id="e757a-188">下表显示了 ASP.NET Core 应用可用的配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-188">The following table shows the configuration providers available to ASP.NET Core apps.</span></span>

::: moniker range=">= aspnetcore-2.1"

| <span data-ttu-id="e757a-189">提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-189">Provider</span></span> | <span data-ttu-id="e757a-190">通过以下对象提供配置&hellip;</span><span class="sxs-lookup"><span data-stu-id="e757a-190">Provides configuration from&hellip;</span></span> |
| -------- | ----------------------------------- |
| <span data-ttu-id="e757a-191">[Azure Key Vault 配置提供程序](xref:security/key-vault-configuration)（安全主题）</span><span class="sxs-lookup"><span data-stu-id="e757a-191">[Azure Key Vault Configuration Provider](xref:security/key-vault-configuration) (*Security* topics)</span></span> | <span data-ttu-id="e757a-192">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e757a-192">Azure Key Vault</span></span> |
| [<span data-ttu-id="e757a-193">命令行配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-193">Command-line Configuration Provider</span></span>](#command-line-configuration-provider) | <span data-ttu-id="e757a-194">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-194">Command-line parameters</span></span> |
| [<span data-ttu-id="e757a-195">自定义配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-195">Custom configuration provider</span></span>](#custom-configuration-provider) | <span data-ttu-id="e757a-196">自定义源</span><span class="sxs-lookup"><span data-stu-id="e757a-196">Custom source</span></span> |
| [<span data-ttu-id="e757a-197">环境变量配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-197">Environment variables Configuration Provider</span></span>](#environment-variables-configuration-provider) | <span data-ttu-id="e757a-198">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-198">Environment variables</span></span> |
| [<span data-ttu-id="e757a-199">文件配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-199">File Configuration Provider</span></span>](#file-configuration-provider) | <span data-ttu-id="e757a-200">文件（INI、JSON、XML）</span><span class="sxs-lookup"><span data-stu-id="e757a-200">Files (INI, JSON, XML)</span></span> |
| [<span data-ttu-id="e757a-201">Key-per-file 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-201">Key-per-file Configuration Provider</span></span>](#key-per-file-configuration-provider) | <span data-ttu-id="e757a-202">目录文件</span><span class="sxs-lookup"><span data-stu-id="e757a-202">Directory files</span></span> |
| [<span data-ttu-id="e757a-203">内存配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-203">Memory Configuration Provider</span></span>](#memory-configuration-provider) | <span data-ttu-id="e757a-204">内存中集合</span><span class="sxs-lookup"><span data-stu-id="e757a-204">In-memory collections</span></span> |
| <span data-ttu-id="e757a-205">[用户机密 (Secret Manager)](xref:security/app-secrets)（安全主题）</span><span class="sxs-lookup"><span data-stu-id="e757a-205">[User secrets (Secret Manager)](xref:security/app-secrets) (*Security* topics)</span></span> | <span data-ttu-id="e757a-206">用户配置文件目录中的文件</span><span class="sxs-lookup"><span data-stu-id="e757a-206">File in the user profile directory</span></span> |

::: moniker-end

::: moniker range="= aspnetcore-2.0 || aspnetcore-1.1"

| <span data-ttu-id="e757a-207">提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-207">Provider</span></span> | <span data-ttu-id="e757a-208">通过以下对象提供配置&hellip;</span><span class="sxs-lookup"><span data-stu-id="e757a-208">Provides configuration from&hellip;</span></span> |
| -------- | ----------------------------------- |
| <span data-ttu-id="e757a-209">[Azure Key Vault 配置提供程序](xref:security/key-vault-configuration)（安全主题）</span><span class="sxs-lookup"><span data-stu-id="e757a-209">[Azure Key Vault Configuration Provider](xref:security/key-vault-configuration) (*Security* topics)</span></span> | <span data-ttu-id="e757a-210">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e757a-210">Azure Key Vault</span></span> |
| [<span data-ttu-id="e757a-211">命令行配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-211">Command-line Configuration Provider</span></span>](#command-line-configuration-provider) | <span data-ttu-id="e757a-212">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-212">Command-line parameters</span></span> |
| [<span data-ttu-id="e757a-213">自定义配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-213">Custom configuration provider</span></span>](#custom-configuration-provider) | <span data-ttu-id="e757a-214">自定义源</span><span class="sxs-lookup"><span data-stu-id="e757a-214">Custom source</span></span> |
| [<span data-ttu-id="e757a-215">环境变量配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-215">Environment variables Configuration Provider</span></span>](#environment-variables-configuration-provider) | <span data-ttu-id="e757a-216">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-216">Environment variables</span></span> |
| [<span data-ttu-id="e757a-217">文件配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-217">File Configuration Provider</span></span>](#file-configuration-provider) | <span data-ttu-id="e757a-218">文件（INI、JSON、XML）</span><span class="sxs-lookup"><span data-stu-id="e757a-218">Files (INI, JSON, XML)</span></span> |
| [<span data-ttu-id="e757a-219">内存配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-219">Memory Configuration Provider</span></span>](#memory-configuration-provider) | <span data-ttu-id="e757a-220">内存中集合</span><span class="sxs-lookup"><span data-stu-id="e757a-220">In-memory collections</span></span> |
| <span data-ttu-id="e757a-221">[用户机密 (Secret Manager)](xref:security/app-secrets)（安全主题）</span><span class="sxs-lookup"><span data-stu-id="e757a-221">[User secrets (Secret Manager)](xref:security/app-secrets) (*Security* topics)</span></span> | <span data-ttu-id="e757a-222">用户配置文件目录中的文件</span><span class="sxs-lookup"><span data-stu-id="e757a-222">File in the user profile directory</span></span> |

::: moniker-end

::: moniker range="= aspnetcore-1.0"

| <span data-ttu-id="e757a-223">提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-223">Provider</span></span> | <span data-ttu-id="e757a-224">通过以下对象提供配置&hellip;</span><span class="sxs-lookup"><span data-stu-id="e757a-224">Provides configuration from&hellip;</span></span> |
| -------- | ----------------------------------- |
| [<span data-ttu-id="e757a-225">命令行配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-225">Command-line Configuration Provider</span></span>](#command-line-configuration-provider) | <span data-ttu-id="e757a-226">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-226">Command-line parameters</span></span> |
| [<span data-ttu-id="e757a-227">自定义配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-227">Custom configuration provider</span></span>](#custom-configuration-provider) | <span data-ttu-id="e757a-228">自定义源</span><span class="sxs-lookup"><span data-stu-id="e757a-228">Custom source</span></span> |
| [<span data-ttu-id="e757a-229">环境变量配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-229">Environment variables Configuration Provider</span></span>](#environment-variables-configuration-provider) | <span data-ttu-id="e757a-230">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-230">Environment variables</span></span> |
| [<span data-ttu-id="e757a-231">文件配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-231">File Configuration Provider</span></span>](#file-configuration-provider) | <span data-ttu-id="e757a-232">文件（INI、JSON、XML）</span><span class="sxs-lookup"><span data-stu-id="e757a-232">Files (INI, JSON, XML)</span></span> |
| [<span data-ttu-id="e757a-233">内存配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-233">Memory Configuration Provider</span></span>](#memory-configuration-provider) | <span data-ttu-id="e757a-234">内存中集合</span><span class="sxs-lookup"><span data-stu-id="e757a-234">In-memory collections</span></span> |
| <span data-ttu-id="e757a-235">[用户机密 (Secret Manager)](xref:security/app-secrets)（安全主题）</span><span class="sxs-lookup"><span data-stu-id="e757a-235">[User secrets (Secret Manager)](xref:security/app-secrets) (*Security* topics)</span></span> | <span data-ttu-id="e757a-236">用户配置文件目录中的文件</span><span class="sxs-lookup"><span data-stu-id="e757a-236">File in the user profile directory</span></span> |

::: moniker-end

<span data-ttu-id="e757a-237">按照启动时指定的配置提供程序的顺序读取配置源。</span><span class="sxs-lookup"><span data-stu-id="e757a-237">Configuration sources are read in the order that their configuration providers are specified at startup.</span></span> <span data-ttu-id="e757a-238">本主题中所述的配置提供程序按字母顺序进行介绍，而不是按代码排列顺序进行介绍。</span><span class="sxs-lookup"><span data-stu-id="e757a-238">The configuration providers described in this topic are described in alphabetical order, not in the order that your code may arrange them.</span></span> <span data-ttu-id="e757a-239">代码中的配置提供程序应以特定顺序排列以符合基础配置源的优先级。</span><span class="sxs-lookup"><span data-stu-id="e757a-239">Order configuration providers in your code to suit your priorities for the underlying configuration sources.</span></span>

<span data-ttu-id="e757a-240">配置提供程序的典型顺序为：</span><span class="sxs-lookup"><span data-stu-id="e757a-240">A typical sequence of configuration providers is:</span></span>

1. <span data-ttu-id="e757a-241">文件（appsettings.json、appsettings.{Environment}.json，其中 `{Environment}` 是应用的当前托管环境）</span><span class="sxs-lookup"><span data-stu-id="e757a-241">Files (*appsettings.json*, *appsettings.{Environment}.json*, where `{Environment}` is the app's current hosting environment)</span></span>
1. [<span data-ttu-id="e757a-242">Azure 密钥保管库</span><span class="sxs-lookup"><span data-stu-id="e757a-242">Azure Key Vault</span></span>](xref:security/key-vault-configuration)
1. <span data-ttu-id="e757a-243">[用户机密 (Secret Manager)](xref:security/app-secrets)（仅限开发环境中）</span><span class="sxs-lookup"><span data-stu-id="e757a-243">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment only)</span></span>
1. <span data-ttu-id="e757a-244">环境变量</span><span class="sxs-lookup"><span data-stu-id="e757a-244">Environment variables</span></span>
1. <span data-ttu-id="e757a-245">命令行参数</span><span class="sxs-lookup"><span data-stu-id="e757a-245">Command-line arguments</span></span>

<span data-ttu-id="e757a-246">通常的做法是将命令行配置提供程序置于一系列提供程序的末尾，以允许命令行参数替代由其他提供程序设置的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-246">It's a common practice to position the Command-line Configuration Provider last in a series of providers to allow command-line arguments to override configuration set by the other providers.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-247">在使用 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 初始化新的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，将使用此提供程序序列。</span><span class="sxs-lookup"><span data-stu-id="e757a-247">This sequence of providers is put into place when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="e757a-248">有关详细信息，请参阅 [Web 主机：设置主机](xref:fundamentals/host/web-host#set-up-a-host)。</span><span class="sxs-lookup"><span data-stu-id="e757a-248">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-249">可以使用 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 和在 `Startup` 中调用其 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder.Build*> 方法来为应用（而不是主机）创建此提供程序序列：</span><span class="sxs-lookup"><span data-stu-id="e757a-249">This sequence of providers can be created for the app (not the host) with a <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> and a call to its <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder.Build*> method in `Startup`:</span></span>

```csharp
public Startup(IHostingEnvironment env)
{
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true)
        .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true, 
            reloadOnChange: true);

    var appAssembly = Assembly.Load(new AssemblyName(env.ApplicationName));

    if (appAssembly != null)
    {
        builder.AddUserSecrets(appAssembly, optional: true);
    }

    builder.AddEnvironmentVariables();

    Configuration = builder.Build();
}

public IConfiguration Configuration { get; }

public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IConfiguration>(Configuration);
}
```

<span data-ttu-id="e757a-250">在前面的示例中，<xref:Microsoft.Extensions.Hosting.IHostingEnvironment> 提供了环境名称 (`env.EnvironmentName`) 和应用程序集名称 (`env.ApplicationName`)。</span><span class="sxs-lookup"><span data-stu-id="e757a-250">In the preceding example, the environment name (`env.EnvironmentName`) and app assembly name (`env.ApplicationName`) are provided by the <xref:Microsoft.Extensions.Hosting.IHostingEnvironment>.</span></span> <span data-ttu-id="e757a-251">有关更多信息，请参见<xref:fundamentals/environments>。</span><span class="sxs-lookup"><span data-stu-id="e757a-251">For more information, see <xref:fundamentals/environments>.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="configureappconfiguration"></a><span data-ttu-id="e757a-252">ConfigureAppConfiguration</span><span class="sxs-lookup"><span data-stu-id="e757a-252">ConfigureAppConfiguration</span></span>

<span data-ttu-id="e757a-253">构建 Web 主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置提供程序以及 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 自动添加的配置提供程序：</span><span class="sxs-lookup"><span data-stu-id="e757a-253">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the Web Host to specify the app's configuration providers in addition to those added automatically by <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>:</span></span>

[!code-csharp[](index/samples/2.x/ConfigurationSample/Program.cs?name=snippet_Program&highlight=19)]

::: moniker-end

## <a name="command-line-configuration-provider"></a><span data-ttu-id="e757a-254">命令行配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-254">Command-line Configuration Provider</span></span>

<span data-ttu-id="e757a-255"><xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> 在运行时从命令行参数键值对加载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-255">The <xref:Microsoft.Extensions.Configuration.CommandLine.CommandLineConfigurationProvider> loads configuration from command-line argument key-value pairs at runtime.</span></span>

<span data-ttu-id="e757a-256">要激活命令行配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-256">To activate command-line configuration, the <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> extension method is called on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-257">使用 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 初始化新的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时会自动调用 `AddCommandLine`。</span><span class="sxs-lookup"><span data-stu-id="e757a-257">`AddCommandLine` is automatically called when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="e757a-258">有关详细信息，请参阅 [Web 主机：设置主机](xref:fundamentals/host/web-host#set-up-a-host)。</span><span class="sxs-lookup"><span data-stu-id="e757a-258">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

<span data-ttu-id="e757a-259">此外，`CreateDefaultBuilder` 也会加载：</span><span class="sxs-lookup"><span data-stu-id="e757a-259">`CreateDefaultBuilder` also loads:</span></span>

* <span data-ttu-id="e757a-260">appsettings.json 和 appsettings.{Environment}.json 的可选配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-260">Optional configuration from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>
* <span data-ttu-id="e757a-261">[用户机密 (Secret Manager)](xref:security/app-secrets)（在开发环境中）。</span><span class="sxs-lookup"><span data-stu-id="e757a-261">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment).</span></span>
* <span data-ttu-id="e757a-262">环境变量。</span><span class="sxs-lookup"><span data-stu-id="e757a-262">Environment variables.</span></span>

<span data-ttu-id="e757a-263">`CreateDefaultBuilder` 最后添加命令行配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-263">`CreateDefaultBuilder` adds the Command-line Configuration Provider last.</span></span> <span data-ttu-id="e757a-264">在运行时传递的命令行参数会替代由其他提供程序设置的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-264">Command-line arguments passed at runtime override configuration set by the other providers.</span></span>

<span data-ttu-id="e757a-265">`CreateDefaultBuilder` 在构造主机时起作用。</span><span class="sxs-lookup"><span data-stu-id="e757a-265">`CreateDefaultBuilder` acts when the host is constructed.</span></span> <span data-ttu-id="e757a-266">因此，`CreateDefaultBuilder` 激活的命令行配置可能会影响主机的配置方式。</span><span class="sxs-lookup"><span data-stu-id="e757a-266">Therefore, command-line configuration activated by `CreateDefaultBuilder` can affect how the host is configured.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-267">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-267">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration.</span></span>

<span data-ttu-id="e757a-268">`CreateDefaultBuilder` 已经调用了 `AddCommandLine`。</span><span class="sxs-lookup"><span data-stu-id="e757a-268">`AddCommandLine` has already been called by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="e757a-269">如果需要提供应用配置并仍然能够使用命令行参数覆盖该配置，请在 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 中调用应用的其他提供程序并最后调用 `AddCommandLine`。</span><span class="sxs-lookup"><span data-stu-id="e757a-269">If you need to provide app configuration and still be able to override that configuration with command-line arguments, call the app's additional providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> and call `AddCommandLine` last.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                // Call other providers here and call AddCommandLine last.
                config.AddCommandLine(args)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-270">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-270">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-271">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>。</span><span class="sxs-lookup"><span data-stu-id="e757a-271">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method.</span></span>

<span data-ttu-id="e757a-272">调用 `UseConfiguration` 时，`CreateDefaultBuilder` 已调用 `AddCommandLine`。</span><span class="sxs-lookup"><span data-stu-id="e757a-272">`AddCommandLine` has already been called by `CreateDefaultBuilder` when `UseConfiguration` is called.</span></span> <span data-ttu-id="e757a-273">如果需要提供应用配置并仍然能够使用命令行参数覆盖该配置，请在 `ConfigurationBuilder` 中调用应用的其他提供程序并最后调用 `AddCommandLine`。</span><span class="sxs-lookup"><span data-stu-id="e757a-273">If you need to provide app configuration and still be able to override that configuration with command-line arguments, call the app's additional providers on a `ConfigurationBuilder` and call `AddCommandLine` last.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            // Call other providers here and call AddCommandLine last.
            .AddCommandLine(args)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-274">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-274">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-275">要激活命令行配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-275">To activate command-line configuration, call the <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-276">最后调用提供程序，以允许在运行时传递的命令行参数替代由其他配置提供程序设置的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-276">Call the provider last to allow the command-line arguments passed at runtime to override configuration set by other configuration providers.</span></span>

<span data-ttu-id="e757a-277">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>：</span><span class="sxs-lookup"><span data-stu-id="e757a-277">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    // Call additional providers here as needed.
    // Call AddCommandLine last to allow arguments to override other configuration.
    .AddCommandLine(args)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="e757a-278">**示例**</span><span class="sxs-lookup"><span data-stu-id="e757a-278">**Example**</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-279">2.x 示例应用利用静态便捷方法 `CreateDefaultBuilder` 来构建主机，其中包括对 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 的调用。</span><span class="sxs-lookup"><span data-stu-id="e757a-279">The 2.x sample app takes advantage of the static convenience method `CreateDefaultBuilder` to build the host, which includes a call to <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-280">1.x 示例应用在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 上调用 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*>。</span><span class="sxs-lookup"><span data-stu-id="e757a-280">The 1.x sample app calls <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> on a <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

::: moniker-end

1. <span data-ttu-id="e757a-281">在项目的目录中打开命令提示符。</span><span class="sxs-lookup"><span data-stu-id="e757a-281">Open a command prompt in the project's directory.</span></span>
1. <span data-ttu-id="e757a-282">为 `dotnet run` 命令提供命令行参数 `dotnet run CommandLineKey=CommandLineValue`。</span><span class="sxs-lookup"><span data-stu-id="e757a-282">Supply a command-line argument to the `dotnet run` command, `dotnet run CommandLineKey=CommandLineValue`.</span></span>
1. <span data-ttu-id="e757a-283">应用运行后，在 `http://localhost:5000` 打开应用的浏览器。</span><span class="sxs-lookup"><span data-stu-id="e757a-283">After the app is running, open a browser to the app at `http://localhost:5000`.</span></span>
1. <span data-ttu-id="e757a-284">观察输出是否包含提供给 `dotnet run` 的配置命令行参数的键值对。</span><span class="sxs-lookup"><span data-stu-id="e757a-284">Observe that the output contains the key-value pair for the configuration command-line argument provided to `dotnet run`.</span></span>

### <a name="arguments"></a><span data-ttu-id="e757a-285">自变量</span><span class="sxs-lookup"><span data-stu-id="e757a-285">Arguments</span></span>

<span data-ttu-id="e757a-286">该值必须后跟一个等号 (`=`)，否则当值后跟一个空格时，键必须具有前缀（`--` 或 `/`）。</span><span class="sxs-lookup"><span data-stu-id="e757a-286">The value must follow an equals sign (`=`), or the key must have a prefix (`--` or `/`) when the value follows a space.</span></span> <span data-ttu-id="e757a-287">如果使用等号（例如，`CommandLineKey=`），则该值可以为 null。</span><span class="sxs-lookup"><span data-stu-id="e757a-287">The value can be null if an equals sign is used (for example, `CommandLineKey=`).</span></span>

| <span data-ttu-id="e757a-288">键前缀</span><span class="sxs-lookup"><span data-stu-id="e757a-288">Key prefix</span></span>               | <span data-ttu-id="e757a-289">示例</span><span class="sxs-lookup"><span data-stu-id="e757a-289">Example</span></span>                                                |
| ------------------------ | ------------------------------------------------------ |
| <span data-ttu-id="e757a-290">无前缀</span><span class="sxs-lookup"><span data-stu-id="e757a-290">No prefix</span></span>                | `CommandLineKey1=value1`                               |
| <span data-ttu-id="e757a-291">双划线 (`--`)</span><span class="sxs-lookup"><span data-stu-id="e757a-291">Two dashes (`--`)</span></span>        | <span data-ttu-id="e757a-292">`--CommandLineKey2=value2`， `--CommandLineKey2 value2`</span><span class="sxs-lookup"><span data-stu-id="e757a-292">`--CommandLineKey2=value2`, `--CommandLineKey2 value2`</span></span> |
| <span data-ttu-id="e757a-293">正斜杠 (`/`)</span><span class="sxs-lookup"><span data-stu-id="e757a-293">Forward slash (`/`)</span></span>      | <span data-ttu-id="e757a-294">`/CommandLineKey3=value3`， `/CommandLineKey3 value3`</span><span class="sxs-lookup"><span data-stu-id="e757a-294">`/CommandLineKey3=value3`, `/CommandLineKey3 value3`</span></span>   |

<span data-ttu-id="e757a-295">在同一命令中，不要将使用等号的命令行参数键值对与使用空格的键值对混合使用。</span><span class="sxs-lookup"><span data-stu-id="e757a-295">Within the same command, don't mix command-line argument key-value pairs that use an equals sign with key-value pairs that use a space.</span></span>

<span data-ttu-id="e757a-296">示例命令：</span><span class="sxs-lookup"><span data-stu-id="e757a-296">Example commands:</span></span>

```console
dotnet run CommandLineKey1=value --CommandLineKey2=value /CommandLineKey2=value
dotnet run --CommandLineKey1 value /CommandLineKey2 value
dotnet run CommandLineKey1= CommandLineKey2=value
```

### <a name="switch-mappings"></a><span data-ttu-id="e757a-297">交换映射</span><span class="sxs-lookup"><span data-stu-id="e757a-297">Switch mappings</span></span>

<span data-ttu-id="e757a-298">交换映射支持键名替换逻辑。</span><span class="sxs-lookup"><span data-stu-id="e757a-298">Switch mappings allow key name replacement logic.</span></span> <span data-ttu-id="e757a-299">使用 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 手动构建配置时，可以为 <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> 方法提供交换替换字典。</span><span class="sxs-lookup"><span data-stu-id="e757a-299">When you manually build configuration with a <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>, you can provide a dictionary of switch replacements to the <xref:Microsoft.Extensions.Configuration.CommandLineConfigurationExtensions.AddCommandLine*> method.</span></span>

<span data-ttu-id="e757a-300">当使用交换映射字典时，会检查字典中是否有与命令行参数提供的键匹配的键。</span><span class="sxs-lookup"><span data-stu-id="e757a-300">When the switch mappings dictionary is used, the dictionary is checked for a key that matches the key provided by a command-line argument.</span></span> <span data-ttu-id="e757a-301">如果在字典中找到命令行键，则传回字典值（键替换）以将键值对设置为应用的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-301">If the command-line key is found in the dictionary, the dictionary value (the key replacement) is passed back to set the key-value pair into the app's configuration.</span></span> <span data-ttu-id="e757a-302">对任何具有单划线 (`-`) 前缀的命令行键而言，交换映射都是必需的。</span><span class="sxs-lookup"><span data-stu-id="e757a-302">A switch mapping is required for any command-line key prefixed with a single dash (`-`).</span></span>

<span data-ttu-id="e757a-303">交换映射字典键规则：</span><span class="sxs-lookup"><span data-stu-id="e757a-303">Switch mappings dictionary key rules:</span></span>

* <span data-ttu-id="e757a-304">交换必须以单划线 (`-`) 或双划线 (`--`) 开头。</span><span class="sxs-lookup"><span data-stu-id="e757a-304">Switches must start with a dash (`-`) or double-dash (`--`).</span></span>
* <span data-ttu-id="e757a-305">交换映射字典不得包含重复键。</span><span class="sxs-lookup"><span data-stu-id="e757a-305">The switch mappings dictionary must not contain duplicate keys.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-306">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-306">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static readonly Dictionary<string, string> _switchMappings = 
        new Dictionary<string, string>
        {
            { "-CLKey1", "CommandLineKey1" },
            { "-CLKey2", "CommandLineKey2" }
        };

    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    // Do not pass the args to CreateDefaultBuilder
    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder()
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddCommandLine(args, _switchMappings)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-307">如前面的示例所示，当使用交换映射时，对 `CreateDefaultBuilder` 的调用不应传递参数。</span><span class="sxs-lookup"><span data-stu-id="e757a-307">As shown in the preceding example, the call to `CreateDefaultBuilder` shouldn't pass arguments when switch mappings are used.</span></span> <span data-ttu-id="e757a-308">`CreateDefaultBuilder` 方法的 `AddCommandLine` 调用不包括映射的交换，并且无法将交换映射字典传递给 `CreateDefaultBuilder`。</span><span class="sxs-lookup"><span data-stu-id="e757a-308">`CreateDefaultBuilder` method's `AddCommandLine` call doesn't include mapped switches, and there's no way to pass the switch mapping dictionary to `CreateDefaultBuilder`.</span></span> <span data-ttu-id="e757a-309">如果参数包含映射的交换并传递给 `CreateDefaultBuilder`，则其 `AddCommandLine` 提供程序无法使用 <xref:System.FormatException> 进行初始化。</span><span class="sxs-lookup"><span data-stu-id="e757a-309">If the arguments include a mapped switch and are passed to `CreateDefaultBuilder`, its `AddCommandLine` provider fails to initialize with a <xref:System.FormatException>.</span></span> <span data-ttu-id="e757a-310">解决方案不是将参数传递给 `CreateDefaultBuilder`，而是允许 `ConfigurationBuilder` 方法的 `AddCommandLine` 方法处理参数和交换映射字典。</span><span class="sxs-lookup"><span data-stu-id="e757a-310">The solution isn't to pass the arguments to `CreateDefaultBuilder` but instead to allow the `ConfigurationBuilder` method's `AddCommandLine` method to process both the arguments and the switch mapping dictionary.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var switchMappings = new Dictionary<string, string>
            {
                { "-CLKey1", "CommandLineKey1" },
                { "-CLKey2", "CommandLineKey2" }
            };

        var config = new ConfigurationBuilder()
            .AddCommandLine(args, switchMappings)
            .Build();

        // Do not pass the args to CreateDefaultBuilder
        return WebHost.CreateDefaultBuilder()
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-311">如前面的示例所示，当使用交换映射时，对 `CreateDefaultBuilder` 的调用不应传递参数。</span><span class="sxs-lookup"><span data-stu-id="e757a-311">As shown in the preceding example, the call to `CreateDefaultBuilder` shouldn't pass arguments when switch mappings are used.</span></span> <span data-ttu-id="e757a-312">`CreateDefaultBuilder` 方法的 `AddCommandLine` 调用不包括映射的交换，并且无法将交换映射字典传递给 `CreateDefaultBuilder`。</span><span class="sxs-lookup"><span data-stu-id="e757a-312">`CreateDefaultBuilder` method's `AddCommandLine` call doesn't include mapped switches, and there's no way to pass the switch mapping dictionary to `CreateDefaultBuilder`.</span></span> <span data-ttu-id="e757a-313">如果参数包含映射的交换并传递给 `CreateDefaultBuilder`，则其 `AddCommandLine` 提供程序无法使用 <xref:System.FormatException> 进行初始化。</span><span class="sxs-lookup"><span data-stu-id="e757a-313">If the arguments include a mapped switch and are passed to `CreateDefaultBuilder`, its `AddCommandLine` provider fails to initialize with a <xref:System.FormatException>.</span></span> <span data-ttu-id="e757a-314">解决方案不是将参数传递给 `CreateDefaultBuilder`，而是允许 `ConfigurationBuilder` 方法的 `AddCommandLine` 方法处理参数和交换映射字典。</span><span class="sxs-lookup"><span data-stu-id="e757a-314">The solution isn't to pass the arguments to `CreateDefaultBuilder` but instead to allow the `ConfigurationBuilder` method's `AddCommandLine` method to process both the arguments and the switch mapping dictionary.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
public static void Main(string[] args)
{
    var switchMappings = new Dictionary<string, string>
        {
            { "-CLKey1", "CommandLineKey1" },
            { "-CLKey2", "CommandLineKey2" }
        };

    var config = new ConfigurationBuilder()
        .AddCommandLine(args, switchMappings)
        .Build();

    var host = new WebHostBuilder()
        .UseConfiguration(config)
        .UseKestrel()
        .UseStartup<Startup>()
        .Start();

    using (host)
    {
        Console.ReadLine();
    }
}
```

::: moniker-end

<span data-ttu-id="e757a-315">创建交换映射字典后，它将包含下表所示的数据。</span><span class="sxs-lookup"><span data-stu-id="e757a-315">After the switch mappings dictionary is created, it contains the data shown in the following table.</span></span>

| <span data-ttu-id="e757a-316">键</span><span class="sxs-lookup"><span data-stu-id="e757a-316">Key</span></span>       | <span data-ttu-id="e757a-317">“值”</span><span class="sxs-lookup"><span data-stu-id="e757a-317">Value</span></span>             |
| --------- | ----------------- |
| `-CLKey1` | `CommandLineKey1` |
| `-CLKey2` | `CommandLineKey2` |

<span data-ttu-id="e757a-318">如果在启动应用时使用了交换映射的键，则配置将接收字典提供的密钥上的配置值：</span><span class="sxs-lookup"><span data-stu-id="e757a-318">If the switch-mapped keys are used when starting the app, configuration receives the configuration value on the key supplied by the dictionary:</span></span>

```console
dotnet run -CLKey1=value1 -CLKey2=value2
```

<span data-ttu-id="e757a-319">运行上述命令后，配置包含下表中显示的值。</span><span class="sxs-lookup"><span data-stu-id="e757a-319">After running the preceding command, configuration contains the values shown in the following table.</span></span>

| <span data-ttu-id="e757a-320">键</span><span class="sxs-lookup"><span data-stu-id="e757a-320">Key</span></span>               | <span data-ttu-id="e757a-321">“值”</span><span class="sxs-lookup"><span data-stu-id="e757a-321">Value</span></span>    |
| ----------------- | -------- |
| `CommandLineKey1` | `value1` |
| `CommandLineKey2` | `value2` |

## <a name="environment-variables-configuration-provider"></a><span data-ttu-id="e757a-322">环境变量配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-322">Environment Variables Configuration Provider</span></span>

<span data-ttu-id="e757a-323"><xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> 在运行时从环境变量键值对加载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-323">The <xref:Microsoft.Extensions.Configuration.EnvironmentVariables.EnvironmentVariablesConfigurationProvider> loads configuration from environment variable key-value pairs at runtime.</span></span>

<span data-ttu-id="e757a-324">要激活环境变量配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-324">To activate environment variables configuration, call the <xref:Microsoft.Extensions.Configuration.EnvironmentVariablesExtensions.AddEnvironmentVariables*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-325">在环境变量中使用分层键时，冒号分隔符 (`:`) 可能无法适用于所有平台。</span><span class="sxs-lookup"><span data-stu-id="e757a-325">When working with hierarchical keys in environment variables, a colon separator (`:`) may not work on all platforms.</span></span> <span data-ttu-id="e757a-326">所有平台均支持采用双下划线 (`__`)，并可以用冒号替换。</span><span class="sxs-lookup"><span data-stu-id="e757a-326">A double underscore (`__`) is supported by all platforms and is replaced by a colon.</span></span>

<span data-ttu-id="e757a-327">借助 [Azure 应用服务](https://azure.microsoft.com/services/app-service/)，用户可以在 Azure 门户中设置使用环境变量配置提供程序替代应用配置的环境变量。</span><span class="sxs-lookup"><span data-stu-id="e757a-327">[Azure App Service](https://azure.microsoft.com/services/app-service/) permits you to set environment variables in the Azure Portal that can override app configuration using the Environment Variables Configuration Provider.</span></span> <span data-ttu-id="e757a-328">有关详细信息，请参阅 [Azure 应用：使用 Azure 门户替代应用配置](xref:host-and-deploy/azure-apps/index#override-app-configuration-using-the-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="e757a-328">For more information, see [Azure Apps: Override app configuration using the Azure Portal](xref:host-and-deploy/azure-apps/index#override-app-configuration-using-the-azure-portal).</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-329">使用 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 初始化新的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时会自动调用 `AddEnvironmentVariables`。</span><span class="sxs-lookup"><span data-stu-id="e757a-329">`AddEnvironmentVariables` is automatically called when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="e757a-330">有关详细信息，请参阅 [Web 主机：设置主机](xref:fundamentals/host/web-host#set-up-a-host)。</span><span class="sxs-lookup"><span data-stu-id="e757a-330">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

<span data-ttu-id="e757a-331">此外，`CreateDefaultBuilder` 也会加载：</span><span class="sxs-lookup"><span data-stu-id="e757a-331">`CreateDefaultBuilder` also loads:</span></span>

* <span data-ttu-id="e757a-332">appsettings.json 和 appsettings.{Environment}.json 的可选配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-332">Optional configuration from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>
* <span data-ttu-id="e757a-333">[用户机密 (Secret Manager)](xref:security/app-secrets)（在开发环境中）。</span><span class="sxs-lookup"><span data-stu-id="e757a-333">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment).</span></span>
* <span data-ttu-id="e757a-334">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="e757a-334">Command-line arguments.</span></span>

<span data-ttu-id="e757a-335">在根据用户机密和 appsettings 文件建立配置后，调用环境变量配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-335">The Environment Variable Configuration Provider is called after configuration is established from user secrets and *appsettings* files.</span></span> <span data-ttu-id="e757a-336">在此位置调用提供程序允许在运行时读取的环境变量替代由用户机密和 appsettings 文件设置的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-336">Calling the provider in this position allows the environment variables read at runtime to override configuration set by user secrets and *appsettings* files.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-337">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-337">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration.</span></span>

<span data-ttu-id="e757a-338">前缀为 `ASPNETCORE_` 的环境变量的 `AddEnvironmentVariables` 已被 `CreateDefaultBuilder` 调用。</span><span class="sxs-lookup"><span data-stu-id="e757a-338">`AddEnvironmentVariables` for environment variables prefixed with `ASPNETCORE_` has already been called by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="e757a-339">如果需要从其他环境变量提供应用配置，请在 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 中调用应用的其他提供程序，并使用前缀调用 `AddEnvironmentVariables`。</span><span class="sxs-lookup"><span data-stu-id="e757a-339">If you need to provide app configuration from additional environment variables, call the app's additional providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> and call `AddEnvironmentVariables` with the prefix.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                // Call additional providers here as needed.
                // Call AddEnvironmentVariables last if you need to allow environment
                // variables to override values from other providers.
                config.AddEnvironmentVariables(prefix: "PREFIX_")
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-340">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-340">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-341">在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 `AddEnvironmentVariables` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-341">Call the `AddEnvironmentVariables` extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span> <span data-ttu-id="e757a-342">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>。</span><span class="sxs-lookup"><span data-stu-id="e757a-342">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method.</span></span>

<span data-ttu-id="e757a-343">前缀为 `ASPNETCORE_` 的环境变量的 `AddEnvironmentVariables` 已被 `CreateDefaultBuilder` 调用。</span><span class="sxs-lookup"><span data-stu-id="e757a-343">`AddEnvironmentVariables` for environment variables prefixed with `ASPNETCORE_` has already been called by `CreateDefaultBuilder`.</span></span> <span data-ttu-id="e757a-344">如果需要从其他环境变量提供应用配置，请在 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 中调用应用的其他提供程序，并使用前缀调用 `AddEnvironmentVariables`。</span><span class="sxs-lookup"><span data-stu-id="e757a-344">If you need to provide app configuration from additional environment variables, call the app's additional providers in <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> and call `AddEnvironmentVariables` with the prefix.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            // Call additional providers here as needed.
            // Call AddEnvironmentVariables last if you need to allow environment
            // variables to override values from other providers.
            .AddEnvironmentVariables(prefix: "PREFIX_")
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-345">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-345">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-346">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>：</span><span class="sxs-lookup"><span data-stu-id="e757a-346">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .AddEnvironmentVariables()
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="e757a-347">**示例**</span><span class="sxs-lookup"><span data-stu-id="e757a-347">**Example**</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-348">2.x 示例应用利用静态便捷方法 `CreateDefaultBuilder` 来构建主机，其中包括对 `AddEnvironmentVariables` 的调用。</span><span class="sxs-lookup"><span data-stu-id="e757a-348">The 2.x sample app takes advantage of the static convenience method `CreateDefaultBuilder` to build the host, which includes a call to `AddEnvironmentVariables`.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-349">1.x 示例应用在 `ConfigurationBuilder` 上调用 `AddEnvironmentVariables`。</span><span class="sxs-lookup"><span data-stu-id="e757a-349">The 1.x sample app calls `AddEnvironmentVariables` on a `ConfigurationBuilder`.</span></span>

::: moniker-end

1. <span data-ttu-id="e757a-350">运行示例应用。</span><span class="sxs-lookup"><span data-stu-id="e757a-350">Run the sample app.</span></span> <span data-ttu-id="e757a-351">在 `http://localhost:5000` 打开应用的浏览器。</span><span class="sxs-lookup"><span data-stu-id="e757a-351">Open a browser to the app at `http://localhost:5000`.</span></span>
1. <span data-ttu-id="e757a-352">观察输出是否包含环境变量 `ENVIRONMENT` 的键值对。</span><span class="sxs-lookup"><span data-stu-id="e757a-352">Observe that the output contains the key-value pair for the environment variable `ENVIRONMENT`.</span></span> <span data-ttu-id="e757a-353">该值反映了应用运行的环境，在本地运行时通常为 `Development`。</span><span class="sxs-lookup"><span data-stu-id="e757a-353">The value reflects the environment in which the app is running, typically `Development` when running locally.</span></span>

<span data-ttu-id="e757a-354">为了使应用呈现的环境变量列表简短，应用将环境变量筛选为以下列内容开头的变量：</span><span class="sxs-lookup"><span data-stu-id="e757a-354">To keep the list of environment variables rendered by the app short, the app filters environment variables to those that start with the following:</span></span>

* <span data-ttu-id="e757a-355">ASPNETCORE_</span><span class="sxs-lookup"><span data-stu-id="e757a-355">ASPNETCORE_</span></span>
* <span data-ttu-id="e757a-356">urls</span><span class="sxs-lookup"><span data-stu-id="e757a-356">urls</span></span>
* <span data-ttu-id="e757a-357">日志记录</span><span class="sxs-lookup"><span data-stu-id="e757a-357">Logging</span></span>
* <span data-ttu-id="e757a-358">ENVIRONMENT</span><span class="sxs-lookup"><span data-stu-id="e757a-358">ENVIRONMENT</span></span>
* <span data-ttu-id="e757a-359">contentRoot</span><span class="sxs-lookup"><span data-stu-id="e757a-359">contentRoot</span></span>
* <span data-ttu-id="e757a-360">AllowedHosts</span><span class="sxs-lookup"><span data-stu-id="e757a-360">AllowedHosts</span></span>
* <span data-ttu-id="e757a-361">applicationName</span><span class="sxs-lookup"><span data-stu-id="e757a-361">applicationName</span></span>
* <span data-ttu-id="e757a-362">CommandLine</span><span class="sxs-lookup"><span data-stu-id="e757a-362">CommandLine</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-363">如果希望公开应用可用的所有环境变量，请将 Pages/Index.cshtml.cs 中的 `FilteredConfiguration` 更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="e757a-363">If you wish to expose all of the environment variables available to the app, change the `FilteredConfiguration` in *Pages/Index.cshtml.cs* to the following:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-364">如果希望公开应用可用的所有环境变量，请将 Controllers/HomeController.cs 中的 `FilteredConfiguration` 更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="e757a-364">If you wish to expose all of the environment variables available to the app, change the `FilteredConfiguration` in *Controllers/HomeController.cs* to the following:</span></span>

::: moniker-end

```csharp
FilteredConfiguration = _config.AsEnumerable();
```

### <a name="prefixes"></a><span data-ttu-id="e757a-365">前缀</span><span class="sxs-lookup"><span data-stu-id="e757a-365">Prefixes</span></span>

<span data-ttu-id="e757a-366">为 `AddEnvironmentVariables` 方法提供前缀时，将筛选加载到应用的配置中的环境变量。</span><span class="sxs-lookup"><span data-stu-id="e757a-366">Environment variables loaded into the app's configuration are filtered when you supply a prefix to the `AddEnvironmentVariables` method.</span></span> <span data-ttu-id="e757a-367">例如，要筛选前缀 `CUSTOM_` 上的环境变量，请将前缀提供给配置提供程序：</span><span class="sxs-lookup"><span data-stu-id="e757a-367">For example, to filter environment variables on the prefix `CUSTOM_`, supply the prefix to the configuration provider:</span></span>

```csharp
var config = new ConfigurationBuilder()
    .AddEnvironmentVariables("CUSTOM_")
    .Build();
```

<span data-ttu-id="e757a-368">创建配置键值对时，将去除前缀。</span><span class="sxs-lookup"><span data-stu-id="e757a-368">The prefix is stripped off when the configuration key-value pairs are created.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-369">静态便捷方法 `CreateDefaultBuilder` 创建一个 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 以建立应用的主机。</span><span class="sxs-lookup"><span data-stu-id="e757a-369">The static convenience method `CreateDefaultBuilder` creates a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> to establish the app's host.</span></span> <span data-ttu-id="e757a-370">创建 `WebHostBuilder` 时，它会在前缀为 `ASPNETCORE_` 的环境变量中找到其主机配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-370">When `WebHostBuilder` is created, it finds its host configuration in environment variables prefixed with `ASPNETCORE_`.</span></span>

::: moniker-end

<span data-ttu-id="e757a-371">**连接字符串前缀**</span><span class="sxs-lookup"><span data-stu-id="e757a-371">**Connection string prefixes**</span></span>

<span data-ttu-id="e757a-372">针对为应用环境配置 Azure 连接字符串所涉及的四个连接字符串环境变量，配置 API 具有特殊的处理规则。</span><span class="sxs-lookup"><span data-stu-id="e757a-372">The Configuration API has special processing rules for four connection string environment variables involved in configuring Azure connection strings for the app environment.</span></span> <span data-ttu-id="e757a-373">如果没有向 `AddEnvironmentVariables` 提供前缀，则具有表中所示前缀的环境变量将加载到应用中。</span><span class="sxs-lookup"><span data-stu-id="e757a-373">Environment variables with the prefixes shown in the table are loaded into the app if no prefix is supplied to `AddEnvironmentVariables`.</span></span>

| <span data-ttu-id="e757a-374">连接字符串前缀</span><span class="sxs-lookup"><span data-stu-id="e757a-374">Connection string prefix</span></span> | <span data-ttu-id="e757a-375">提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-375">Provider</span></span> |
| ------------------------ | -------- |
| `CUSTOMCONNSTR_` | <span data-ttu-id="e757a-376">自定义提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-376">Custom provider</span></span> |
| `MYSQLCONNSTR_` | [<span data-ttu-id="e757a-377">MySQL</span><span class="sxs-lookup"><span data-stu-id="e757a-377">MySQL</span></span>](https://www.mysql.com/) |
| `SQLAZURECONNSTR_` | [<span data-ttu-id="e757a-378">Azure SQL 数据库</span><span class="sxs-lookup"><span data-stu-id="e757a-378">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/) |
| `SQLCONNSTR_` | [<span data-ttu-id="e757a-379">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e757a-379">SQL Server</span></span>](https://www.microsoft.com/sql-server/) |

<span data-ttu-id="e757a-380">当发现环境变量并使用表中所示的四个前缀中的任何一个加载到配置中时：</span><span class="sxs-lookup"><span data-stu-id="e757a-380">When an environment variable is discovered and loaded into configuration with any of the four prefixes shown in the table:</span></span>

* <span data-ttu-id="e757a-381">通过删除环境变量前缀并添加配置键节 (`ConnectionStrings`) 来创建配置键。</span><span class="sxs-lookup"><span data-stu-id="e757a-381">The configuration key is created by removing the environment variable prefix and adding a configuration key section (`ConnectionStrings`).</span></span>
* <span data-ttu-id="e757a-382">创建一个新的配置键值对，表示数据库连接提供程序（`CUSTOMCONNSTR_` 除外，它没有声明的提供程序）。</span><span class="sxs-lookup"><span data-stu-id="e757a-382">A new configuration key-value pair is created that represents the database connection provider (except for `CUSTOMCONNSTR_`, which has no stated provider).</span></span>

| <span data-ttu-id="e757a-383">环境变量键</span><span class="sxs-lookup"><span data-stu-id="e757a-383">Environment variable key</span></span> | <span data-ttu-id="e757a-384">转换的配置键</span><span class="sxs-lookup"><span data-stu-id="e757a-384">Converted configuration key</span></span> | <span data-ttu-id="e757a-385">提供程序配置条目</span><span class="sxs-lookup"><span data-stu-id="e757a-385">Provider configuration entry</span></span>                                                    |
| ------------------------ | --------------------------- | ------------------------------------------------------------------------------- |
| `CUSTOMCONNSTR_<KEY>`    | `ConnectionStrings:<KEY>`   | <span data-ttu-id="e757a-386">配置条目未创建。</span><span class="sxs-lookup"><span data-stu-id="e757a-386">Configuration entry not created.</span></span>                                                |
| `MYSQLCONNSTR_<KEY>`     | `ConnectionStrings:<KEY>`   | <span data-ttu-id="e757a-387">键：`ConnectionStrings:<KEY>_ProviderName`：</span><span class="sxs-lookup"><span data-stu-id="e757a-387">Key: `ConnectionStrings:<KEY>_ProviderName`:</span></span><br><span data-ttu-id="e757a-388">值：`MySql.Data.MySqlClient`</span><span class="sxs-lookup"><span data-stu-id="e757a-388">Value: `MySql.Data.MySqlClient`</span></span> |
| `SQLAZURECONNSTR_<KEY>`  | `ConnectionStrings:<KEY>`   | <span data-ttu-id="e757a-389">键：`ConnectionStrings:<KEY>_ProviderName`：</span><span class="sxs-lookup"><span data-stu-id="e757a-389">Key: `ConnectionStrings:<KEY>_ProviderName`:</span></span><br><span data-ttu-id="e757a-390">值：`System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="e757a-390">Value: `System.Data.SqlClient`</span></span>  |
| `SQLCONNSTR_<KEY>`       | `ConnectionStrings:<KEY>`   | <span data-ttu-id="e757a-391">键：`ConnectionStrings:<KEY>_ProviderName`：</span><span class="sxs-lookup"><span data-stu-id="e757a-391">Key: `ConnectionStrings:<KEY>_ProviderName`:</span></span><br><span data-ttu-id="e757a-392">值：`System.Data.SqlClient`</span><span class="sxs-lookup"><span data-stu-id="e757a-392">Value: `System.Data.SqlClient`</span></span>  |

## <a name="file-configuration-provider"></a><span data-ttu-id="e757a-393">文件配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-393">File Configuration Provider</span></span>

<span data-ttu-id="e757a-394"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> 是从文件系统加载配置的基类。</span><span class="sxs-lookup"><span data-stu-id="e757a-394"><xref:Microsoft.Extensions.Configuration.FileConfigurationProvider> is the base class for loading configuration from the file system.</span></span> <span data-ttu-id="e757a-395">以下配置提供程序专用于特定文件类型：</span><span class="sxs-lookup"><span data-stu-id="e757a-395">The following configuration providers are dedicated to specific file types:</span></span>

* [<span data-ttu-id="e757a-396">INI 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-396">INI Configuration Provider</span></span>](#ini-configuration-provider)
* [<span data-ttu-id="e757a-397">JSON 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-397">JSON Configuration Provider</span></span>](#json-configuration-provider)
* [<span data-ttu-id="e757a-398">XML 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-398">XML Configuration Provider</span></span>](#xml-configuration-provider)

### <a name="ini-configuration-provider"></a><span data-ttu-id="e757a-399">INI 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-399">INI Configuration Provider</span></span>

<span data-ttu-id="e757a-400"><xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider> 在运行时从 INI 文件键值对加载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-400">The <xref:Microsoft.Extensions.Configuration.Ini.IniConfigurationProvider> loads configuration from INI file key-value pairs at runtime.</span></span>

<span data-ttu-id="e757a-401">若要激活 INI 文件配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.IniConfigurationExtensions.AddIniFile*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-401">To activate INI file configuration, call the <xref:Microsoft.Extensions.Configuration.IniConfigurationExtensions.AddIniFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-402">冒号可用作 INI 文件配置中的节分隔符。</span><span class="sxs-lookup"><span data-stu-id="e757a-402">The colon can be used to as a section delimiter in INI file configuration.</span></span>

<span data-ttu-id="e757a-403">重载允许指定：</span><span class="sxs-lookup"><span data-stu-id="e757a-403">Overloads permit specifying:</span></span>

* <span data-ttu-id="e757a-404">文件是否可选。</span><span class="sxs-lookup"><span data-stu-id="e757a-404">Whether the file is optional.</span></span>
* <span data-ttu-id="e757a-405">如果文件更改，是否重载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-405">Whether the configuration is reloaded if the file changes.</span></span>
* <span data-ttu-id="e757a-406"><xref:Microsoft.Extensions.FileProviders.IFileProvider> 用于访问该文件。</span><span class="sxs-lookup"><span data-stu-id="e757a-406">The <xref:Microsoft.Extensions.FileProviders.IFileProvider> used to access the file.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-407">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-407">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddIniFile("config.ini", optional: true, reloadOnChange: true)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-408">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-408">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-409">调用 `CreateDefaultBuilder` 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-409">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddIniFile("config.ini", optional: true, reloadOnChange: true)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-410">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-410">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-411">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>：</span><span class="sxs-lookup"><span data-stu-id="e757a-411">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddIniFile("config.ini", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="e757a-412">INI 配置文件的通用示例：</span><span class="sxs-lookup"><span data-stu-id="e757a-412">A generic example of an INI configuration file:</span></span>

```ini
[section0]
key0=value
key1=value

[section1]
subsection:key=value

[section2:subsection0]
key=value

[section2:subsection1]
key=value
```

<span data-ttu-id="e757a-413">以前的配置文件使用 `value` 加载以下键：</span><span class="sxs-lookup"><span data-stu-id="e757a-413">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="e757a-414">section0:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-414">section0:key0</span></span>
* <span data-ttu-id="e757a-415">section0:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-415">section0:key1</span></span>
* <span data-ttu-id="e757a-416">section1:subsection:key</span><span class="sxs-lookup"><span data-stu-id="e757a-416">section1:subsection:key</span></span>
* <span data-ttu-id="e757a-417">section2:subsection0:key</span><span class="sxs-lookup"><span data-stu-id="e757a-417">section2:subsection0:key</span></span>
* <span data-ttu-id="e757a-418">section2:subsection1:key</span><span class="sxs-lookup"><span data-stu-id="e757a-418">section2:subsection1:key</span></span>

### <a name="json-configuration-provider"></a><span data-ttu-id="e757a-419">JSON 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-419">JSON Configuration Provider</span></span>

<span data-ttu-id="e757a-420"><xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider> 在运行时期间从 JSON 文件键值对加载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-420">The <xref:Microsoft.Extensions.Configuration.Json.JsonConfigurationProvider> loads configuration from JSON file key-value pairs during runtime.</span></span>

<span data-ttu-id="e757a-421">若要激活 JSON 文件配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-421">To activate JSON file configuration, call the <xref:Microsoft.Extensions.Configuration.JsonConfigurationExtensions.AddJsonFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-422">重载允许指定：</span><span class="sxs-lookup"><span data-stu-id="e757a-422">Overloads permit specifying:</span></span>

* <span data-ttu-id="e757a-423">文件是否可选。</span><span class="sxs-lookup"><span data-stu-id="e757a-423">Whether the file is optional.</span></span>
* <span data-ttu-id="e757a-424">如果文件更改，是否重载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-424">Whether the configuration is reloaded if the file changes.</span></span>
* <span data-ttu-id="e757a-425"><xref:Microsoft.Extensions.FileProviders.IFileProvider> 用于访问该文件。</span><span class="sxs-lookup"><span data-stu-id="e757a-425">The <xref:Microsoft.Extensions.FileProviders.IFileProvider> used to access the file.</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-426">使用 <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*> 初始化新的 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，会自动调用 `AddJsonFile` 两次。</span><span class="sxs-lookup"><span data-stu-id="e757a-426">`AddJsonFile` is automatically called twice when you initialize a new <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with <xref:Microsoft.AspNetCore.WebHost.CreateDefaultBuilder*>.</span></span> <span data-ttu-id="e757a-427">调用该方法来从以下文件加载配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-427">The method is called to load configuration from:</span></span>

* <span data-ttu-id="e757a-428">appsettings.json &ndash; 首先读取此文件。</span><span class="sxs-lookup"><span data-stu-id="e757a-428">*appsettings.json* &ndash; This file is read first.</span></span> <span data-ttu-id="e757a-429">该文件的环境版本可以替代 appsettings.json 文件提供的值。</span><span class="sxs-lookup"><span data-stu-id="e757a-429">The environment version of the file can override the values provided by the *appsettings.json* file.</span></span>
* <span data-ttu-id="e757a-430">*appsettings.{Environment}.json*&ndash; 根据 [IHostingEnvironment.EnvironmentName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.EnvironmentName*) 加载文件的环境版本。</span><span class="sxs-lookup"><span data-stu-id="e757a-430">*appsettings.{Environment}.json* &ndash; The environment version of the file is loaded based on the [IHostingEnvironment.EnvironmentName](xref:Microsoft.Extensions.Hosting.IHostingEnvironment.EnvironmentName*).</span></span>

<span data-ttu-id="e757a-431">有关详细信息，请参阅 [Web 主机：设置主机](xref:fundamentals/host/web-host#set-up-a-host)。</span><span class="sxs-lookup"><span data-stu-id="e757a-431">For more information, see [Web Host: Set up a host](xref:fundamentals/host/web-host#set-up-a-host).</span></span>

<span data-ttu-id="e757a-432">此外，`CreateDefaultBuilder` 也会加载：</span><span class="sxs-lookup"><span data-stu-id="e757a-432">`CreateDefaultBuilder` also loads:</span></span>

* <span data-ttu-id="e757a-433">环境变量。</span><span class="sxs-lookup"><span data-stu-id="e757a-433">Environment variables.</span></span>
* <span data-ttu-id="e757a-434">[用户机密 (Secret Manager)](xref:security/app-secrets)（在开发环境中）。</span><span class="sxs-lookup"><span data-stu-id="e757a-434">[User secrets (Secret Manager)](xref:security/app-secrets) (in the Development environment).</span></span>
* <span data-ttu-id="e757a-435">命令行参数。</span><span class="sxs-lookup"><span data-stu-id="e757a-435">Command-line arguments.</span></span>

<span data-ttu-id="e757a-436">首先建立 JSON 配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-436">The JSON Configuration Provider is established first.</span></span> <span data-ttu-id="e757a-437">因此，用户机密、环境变量和命令行参数会替代由 appsettings 文件设置的配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-437">Therefore, user secrets, environment variables, and command-line arguments override configuration set by the *appsettings* files.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-438">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定除 appsettings.json 和 appsettings.{Environment}.json 以外的文件的应用配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-438">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration for files other than *appsettings.json* and *appsettings.{Environment}.json*:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddJsonFile("config.json", optional: true, reloadOnChange: true)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-439">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-439">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-440">还可以在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上直接调用 `AddJsonFile` 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-440">You can also directly call the `AddJsonFile` extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-441">调用 `CreateDefaultBuilder` 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-441">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddJsonFile("config.json", optional: true, reloadOnChange: true)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-442">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-442">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-443">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>：</span><span class="sxs-lookup"><span data-stu-id="e757a-443">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("config.json", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="e757a-444">**示例**</span><span class="sxs-lookup"><span data-stu-id="e757a-444">**Example**</span></span>

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-445">2.x 示例应用利用静态便捷方法 `CreateDefaultBuilder` 来构建主机，其中包括对 `AddJsonFile` 的两次调用。</span><span class="sxs-lookup"><span data-stu-id="e757a-445">The 2.x sample app takes advantage of the static convenience method `CreateDefaultBuilder` to build the host, which includes two calls to `AddJsonFile`.</span></span> <span data-ttu-id="e757a-446">配置从 appsettings.json 和 appsettings.{Environment}.json 进行加载。</span><span class="sxs-lookup"><span data-stu-id="e757a-446">Configuration is loaded from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-447">1.x 示例应用在 `ConfigurationBuilder` 上调用 `AddJsonFile` 两次。</span><span class="sxs-lookup"><span data-stu-id="e757a-447">The 1.x sample app calls `AddJsonFile` twice on a `ConfigurationBuilder`.</span></span> <span data-ttu-id="e757a-448">配置从 appsettings.json 和 appsettings.{Environment}.json 进行加载。</span><span class="sxs-lookup"><span data-stu-id="e757a-448">Configuration is loaded from *appsettings.json* and *appsettings.{Environment}.json*.</span></span>

::: moniker-end

1. <span data-ttu-id="e757a-449">运行示例应用。</span><span class="sxs-lookup"><span data-stu-id="e757a-449">Run the sample app.</span></span> <span data-ttu-id="e757a-450">在 `http://localhost:5000` 打开应用的浏览器。</span><span class="sxs-lookup"><span data-stu-id="e757a-450">Open a browser to the app at `http://localhost:5000`.</span></span>
1. <span data-ttu-id="e757a-451">观察输出是否包含表中所示的配置的键值对，具体取决于环境。</span><span class="sxs-lookup"><span data-stu-id="e757a-451">Observe that the output contains key-value pairs for the configuration shown in the table depending on the environment.</span></span> <span data-ttu-id="e757a-452">记录配置键使用冒号 (`:`) 作为分层分隔符。</span><span class="sxs-lookup"><span data-stu-id="e757a-452">Logging configuration keys use the colon (`:`) as a hierarchical separator.</span></span>

| <span data-ttu-id="e757a-453">键</span><span class="sxs-lookup"><span data-stu-id="e757a-453">Key</span></span>                        | <span data-ttu-id="e757a-454">开发值</span><span class="sxs-lookup"><span data-stu-id="e757a-454">Development Value</span></span> | <span data-ttu-id="e757a-455">生产值</span><span class="sxs-lookup"><span data-stu-id="e757a-455">Production Value</span></span> |
| -------------------------- | :---------------: | :--------------: |
| <span data-ttu-id="e757a-456">Logging:LogLevel:System</span><span class="sxs-lookup"><span data-stu-id="e757a-456">Logging:LogLevel:System</span></span>    | <span data-ttu-id="e757a-457">信息</span><span class="sxs-lookup"><span data-stu-id="e757a-457">Information</span></span>       | <span data-ttu-id="e757a-458">信息</span><span class="sxs-lookup"><span data-stu-id="e757a-458">Information</span></span>      |
| <span data-ttu-id="e757a-459">Logging:LogLevel:Microsoft</span><span class="sxs-lookup"><span data-stu-id="e757a-459">Logging:LogLevel:Microsoft</span></span> | <span data-ttu-id="e757a-460">信息</span><span class="sxs-lookup"><span data-stu-id="e757a-460">Information</span></span>       | <span data-ttu-id="e757a-461">信息</span><span class="sxs-lookup"><span data-stu-id="e757a-461">Information</span></span>      |
| <span data-ttu-id="e757a-462">Logging:LogLevel:Default</span><span class="sxs-lookup"><span data-stu-id="e757a-462">Logging:LogLevel:Default</span></span>   | <span data-ttu-id="e757a-463">调试</span><span class="sxs-lookup"><span data-stu-id="e757a-463">Debug</span></span>             | <span data-ttu-id="e757a-464">Error</span><span class="sxs-lookup"><span data-stu-id="e757a-464">Error</span></span>            |
| <span data-ttu-id="e757a-465">AllowedHosts</span><span class="sxs-lookup"><span data-stu-id="e757a-465">AllowedHosts</span></span>               | *                 | *                |

### <a name="xml-configuration-provider"></a><span data-ttu-id="e757a-466">XML 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-466">XML Configuration Provider</span></span>

<span data-ttu-id="e757a-467"><xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider> 在运行时从 XML 文件键值对加载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-467">The <xref:Microsoft.Extensions.Configuration.Xml.XmlConfigurationProvider> loads configuration from XML file key-value pairs at runtime.</span></span>

<span data-ttu-id="e757a-468">若要激活 XML 文件配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.XmlConfigurationExtensions.AddXmlFile*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-468">To activate XML file configuration, call the <xref:Microsoft.Extensions.Configuration.XmlConfigurationExtensions.AddXmlFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-469">重载允许指定：</span><span class="sxs-lookup"><span data-stu-id="e757a-469">Overloads permit specifying:</span></span>

* <span data-ttu-id="e757a-470">文件是否可选。</span><span class="sxs-lookup"><span data-stu-id="e757a-470">Whether the file is optional.</span></span>
* <span data-ttu-id="e757a-471">如果文件更改，是否重载配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-471">Whether the configuration is reloaded if the file changes.</span></span>
* <span data-ttu-id="e757a-472"><xref:Microsoft.Extensions.FileProviders.IFileProvider> 用于访问该文件。</span><span class="sxs-lookup"><span data-stu-id="e757a-472">The <xref:Microsoft.Extensions.FileProviders.IFileProvider> used to access the file.</span></span>

<span data-ttu-id="e757a-473">创建配置键值对时，将忽略配置文件的根节点。</span><span class="sxs-lookup"><span data-stu-id="e757a-473">The root node of the configuration file is ignored when the configuration key-value pairs are created.</span></span> <span data-ttu-id="e757a-474">不要在文件中指定文档类型定义 (DTD) 或命名空间。</span><span class="sxs-lookup"><span data-stu-id="e757a-474">Don't specify a Document Type Definition (DTD) or namespace in the file.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-475">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-475">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddXmlFile("config.xml", optional: true, reloadOnChange: true)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-476">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-476">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-477">调用 `CreateDefaultBuilder` 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-477">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var config = new ConfigurationBuilder()
            .SetBasePath(Directory.GetCurrentDirectory())
            .AddXmlFile("config.xml", optional: true, reloadOnChange: true)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-478">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-478">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-479">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>：</span><span class="sxs-lookup"><span data-stu-id="e757a-479">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var config = new ConfigurationBuilder()
    .SetBasePath(Directory.GetCurrentDirectory())
    .AddXmlFile("config.xml", optional: true, reloadOnChange: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

<span data-ttu-id="e757a-480">XML 配置文件可以为重复节使用不同的元素名称：</span><span class="sxs-lookup"><span data-stu-id="e757a-480">XML configuration files can use distinct element names for repeating sections:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <section0>
    <key0>value</key0>
    <key1>value</key1>
  </section0>
  <section1>
    <key0>value</key0>
    <key1>value</key1>
  </section1>
</configuration>
```

<span data-ttu-id="e757a-481">以前的配置文件使用 `value` 加载以下键：</span><span class="sxs-lookup"><span data-stu-id="e757a-481">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="e757a-482">section0:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-482">section0:key0</span></span>
* <span data-ttu-id="e757a-483">section0:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-483">section0:key1</span></span>
* <span data-ttu-id="e757a-484">section1:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-484">section1:key0</span></span>
* <span data-ttu-id="e757a-485">section1:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-485">section1:key1</span></span>

<span data-ttu-id="e757a-486">如果使用 `name` 属性来区分元素，则使用相同元素名称的重复元素可以正常工作：</span><span class="sxs-lookup"><span data-stu-id="e757a-486">Repeating elements that use the same element name work if the `name` attribute is used to distinguish the elements:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <section name="section0">
    <key name="key0">value</key>
    <key name="key1">value</key>
  </section>
  <section name="section1">
    <key name="key0">value</key>
    <key name="key1">value</key>
  </section>
</configuration>
```

<span data-ttu-id="e757a-487">以前的配置文件使用 `value` 加载以下键：</span><span class="sxs-lookup"><span data-stu-id="e757a-487">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="e757a-488">section:section0:key:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-488">section:section0:key:key0</span></span>
* <span data-ttu-id="e757a-489">section:section0:key:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-489">section:section0:key:key1</span></span>
* <span data-ttu-id="e757a-490">section:section1:key:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-490">section:section1:key:key0</span></span>
* <span data-ttu-id="e757a-491">section:section1:key:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-491">section:section1:key:key1</span></span>

<span data-ttu-id="e757a-492">属性可用于提供值：</span><span class="sxs-lookup"><span data-stu-id="e757a-492">Attributes can be used to supply values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <key attribute="value" />
  <section>
    <key attribute="value" />
  </section>
</configuration>
```

<span data-ttu-id="e757a-493">以前的配置文件使用 `value` 加载以下键：</span><span class="sxs-lookup"><span data-stu-id="e757a-493">The previous configuration file loads the following keys with `value`:</span></span>

* <span data-ttu-id="e757a-494">key:attribute</span><span class="sxs-lookup"><span data-stu-id="e757a-494">key:attribute</span></span>
* <span data-ttu-id="e757a-495">section:key:attribute</span><span class="sxs-lookup"><span data-stu-id="e757a-495">section:key:attribute</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="key-per-file-configuration-provider"></a><span data-ttu-id="e757a-496">Key-per-file 配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-496">Key-per-file Configuration Provider</span></span>

<span data-ttu-id="e757a-497"><xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider> 使用目录的文件作为配置键值对。</span><span class="sxs-lookup"><span data-stu-id="e757a-497">The <xref:Microsoft.Extensions.Configuration.KeyPerFile.KeyPerFileConfigurationProvider> uses a directory's files as configuration key-value pairs.</span></span> <span data-ttu-id="e757a-498">该键是文件名。</span><span class="sxs-lookup"><span data-stu-id="e757a-498">The key is the file name.</span></span> <span data-ttu-id="e757a-499">该值包含文件的内容。</span><span class="sxs-lookup"><span data-stu-id="e757a-499">The value contains the file's contents.</span></span> <span data-ttu-id="e757a-500">Key-per-file 配置提供程序用于 Docker 托管方案。</span><span class="sxs-lookup"><span data-stu-id="e757a-500">The Key-per-file Configuration Provider is used in Docker hosting scenarios.</span></span>

<span data-ttu-id="e757a-501">若要激活 Key-per-file 配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-501">To activate key-per-file configuration, call the <xref:Microsoft.Extensions.Configuration.KeyPerFileConfigurationBuilderExtensions.AddKeyPerFile*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span> <span data-ttu-id="e757a-502">文件的 `directoryPath` 必须是绝对路径。</span><span class="sxs-lookup"><span data-stu-id="e757a-502">The `directoryPath` to the files must be an absolute path.</span></span>

<span data-ttu-id="e757a-503">重载允许指定：</span><span class="sxs-lookup"><span data-stu-id="e757a-503">Overloads permit specifying:</span></span>

* <span data-ttu-id="e757a-504">配置源的 `Action<KeyPerFileConfigurationSource>` 委托。</span><span class="sxs-lookup"><span data-stu-id="e757a-504">An `Action<KeyPerFileConfigurationSource>` delegate that configures the source.</span></span>
* <span data-ttu-id="e757a-505">目录是否可选以及目录的路径。</span><span class="sxs-lookup"><span data-stu-id="e757a-505">Whether the directory is optional and the path to the directory.</span></span>

<span data-ttu-id="e757a-506">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-506">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.SetBasePath(Directory.GetCurrentDirectory());
                config.AddKeyPerFile(directoryPath: path, optional: true)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-507">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-507">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
var path = Path.Combine(Directory.GetCurrentDirectory(), "path/to/files");
var config = new ConfigurationBuilder()
    .AddKeyPerFile(directoryPath: path, optional: true)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

::: moniker-end

## <a name="memory-configuration-provider"></a><span data-ttu-id="e757a-508">内存配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-508">Memory Configuration Provider</span></span>

<span data-ttu-id="e757a-509"><xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider> 使用内存中集合作为配置键值对。</span><span class="sxs-lookup"><span data-stu-id="e757a-509">The <xref:Microsoft.Extensions.Configuration.Memory.MemoryConfigurationProvider> uses an in-memory collection as configuration key-value pairs.</span></span>

<span data-ttu-id="e757a-510">若要激活内存中集合配置，请在 <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder> 的实例上调用 <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection*> 扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-510">To activate in-memory collection configuration, call the <xref:Microsoft.Extensions.Configuration.MemoryConfigurationBuilderExtensions.AddInMemoryCollection*> extension method on an instance of <xref:Microsoft.Extensions.Configuration.ConfigurationBuilder>.</span></span>

<span data-ttu-id="e757a-511">可以使用 `IEnumerable<KeyValuePair<String,String>>` 初始化配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-511">The configuration provider can be initialized with an `IEnumerable<KeyValuePair<String,String>>`.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="e757a-512">构建主机时调用 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> 以指定应用的配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-512">Call <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*> when building the host to specify the app's configuration:</span></span>

```csharp
public class Program
{
    public static readonly Dictionary<string, string> _dict = 
        new Dictionary<string, string>
        {
            {"MemoryCollectionKey1", "value1"},
            {"MemoryCollectionKey2", "value2"}
        };

    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((hostingContext, config) =>
            {
                config.AddInMemoryCollection(_dict)
            })
            .UseStartup<Startup>();
}
```

<span data-ttu-id="e757a-513">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-513">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="e757a-514">调用 `CreateDefaultBuilder` 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-514">When calling `CreateDefaultBuilder`, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateWebHostBuilder(args).Build().Run();
    }

    public static IWebHostBuilder CreateWebHostBuilder(string[] args)
    {
        var dict = new Dictionary<string, string>
            {
                {"MemoryCollectionKey1", "value1"},
                {"MemoryCollectionKey2", "value2"}
            };

        var config = new ConfigurationBuilder()
            .AddInMemoryCollection(dict)
            .Build();

        return WebHost.CreateDefaultBuilder(args)
            .UseConfiguration(config)
            .UseStartup<Startup>();
    }
}
```

<span data-ttu-id="e757a-515">直接创建 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> 时，请使用以下配置调用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*>：</span><span class="sxs-lookup"><span data-stu-id="e757a-515">When creating a <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> directly, call <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> with the configuration:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-516">使用 <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> 方法将配置应用到 <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder>：</span><span class="sxs-lookup"><span data-stu-id="e757a-516">Apply the configuration to <xref:Microsoft.AspNetCore.Hosting.WebHostBuilder> with the <xref:Microsoft.AspNetCore.Hosting.HostingAbstractionsWebHostBuilderExtensions.UseConfiguration*> method:</span></span>

::: moniker-end

```csharp
var dict = new Dictionary<string, string>
    {
        {"MemoryCollectionKey1", "value1"},
        {"MemoryCollectionKey2", "value2"}
    };

var config = new ConfigurationBuilder()
    .AddInMemoryCollection(dict)
    .Build();

var host = new WebHostBuilder()
    .UseConfiguration(config)
    .UseKestrel()
    .UseStartup<Startup>();
```

## <a name="getvalue"></a><span data-ttu-id="e757a-517">GetValue</span><span class="sxs-lookup"><span data-stu-id="e757a-517">GetValue</span></span>

<span data-ttu-id="e757a-518">[ConfigurationBinder.GetValue&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.GetValue*) 从具有指定键的配置中提取一个值，并将其转换为指定类型。</span><span class="sxs-lookup"><span data-stu-id="e757a-518">[ConfigurationBinder.GetValue&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.GetValue*) extracts a value from configuration with a specified key and converts it to the specified type.</span></span> <span data-ttu-id="e757a-519">如果未找到该键，则过载允许你提供默认值。</span><span class="sxs-lookup"><span data-stu-id="e757a-519">An overload permits you to provide a default value if the key isn't found.</span></span>

<span data-ttu-id="e757a-520">以下示例使用键 `NumberKey` 从配置中提取字符串值，键入该值作为 `int`，并将值存储在变量 `intValue` 中。</span><span class="sxs-lookup"><span data-stu-id="e757a-520">The following example extracts the string value from configuration with the key `NumberKey`, types the value as an `int`, and stores the value in the variable `intValue`.</span></span> <span data-ttu-id="e757a-521">如果在配置键中找不到 `NumberKey`，则 `intValue` 会接收 `99` 的默认值：</span><span class="sxs-lookup"><span data-stu-id="e757a-521">If `NumberKey` isn't found in the configuration keys, `intValue` receives the default value of `99`:</span></span>

```csharp
var intValue = config.GetValue<int>("NumberKey", 99);
```

## <a name="getsection-getchildren-and-exists"></a><span data-ttu-id="e757a-522">GetSection、GetChildren 和 Exists</span><span class="sxs-lookup"><span data-stu-id="e757a-522">GetSection, GetChildren, and Exists</span></span>

<span data-ttu-id="e757a-523">对于下面的示例，请考虑以下 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="e757a-523">For the examples that follow, consider the following JSON file.</span></span> <span data-ttu-id="e757a-524">在两个节中找到四个键，其中一个包含一对子节：</span><span class="sxs-lookup"><span data-stu-id="e757a-524">Four keys are found across two sections, one of which includes a pair of subsections:</span></span>

```json
{
  "section0": {
    "key0": "value",
    "key1": "value"
  },
  "section1": {
    "key0": "value",
    "key1": "value"
  },
  "section2": {
    "subsection0" : {
      "key0": "value",
      "key1": "value"
    },
    "subsection1" : {
      "key0": "value",
      "key1": "value"
    }
  }
}
```

<span data-ttu-id="e757a-525">将文件读入配置时，会创建以下唯一的分层键来保存配置值：</span><span class="sxs-lookup"><span data-stu-id="e757a-525">When the file is read into configuration, the following unique hierarchical keys are created to hold the configuration values:</span></span>

* <span data-ttu-id="e757a-526">section0:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-526">section0:key0</span></span>
* <span data-ttu-id="e757a-527">section0:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-527">section0:key1</span></span>
* <span data-ttu-id="e757a-528">section1:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-528">section1:key0</span></span>
* <span data-ttu-id="e757a-529">section1:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-529">section1:key1</span></span>
* <span data-ttu-id="e757a-530">section2:subsection0:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-530">section2:subsection0:key0</span></span>
* <span data-ttu-id="e757a-531">section2:subsection0:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-531">section2:subsection0:key1</span></span>
* <span data-ttu-id="e757a-532">section2:subsection1:key0</span><span class="sxs-lookup"><span data-stu-id="e757a-532">section2:subsection1:key0</span></span>
* <span data-ttu-id="e757a-533">section2:subsection1:key1</span><span class="sxs-lookup"><span data-stu-id="e757a-533">section2:subsection1:key1</span></span>

### <a name="getsection"></a><span data-ttu-id="e757a-534">GetSection</span><span class="sxs-lookup"><span data-stu-id="e757a-534">GetSection</span></span>

<span data-ttu-id="e757a-535">[IConfiguration.GetSection](xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection*) 使用指定的子节键提取配置子节。</span><span class="sxs-lookup"><span data-stu-id="e757a-535">[IConfiguration.GetSection](xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection*) extracts a configuration subsection with the specified subsection key.</span></span>

<span data-ttu-id="e757a-536">若要返回仅包含 `section1` 中键值对的 <xref:Microsoft.Extensions.Configuration.IConfigurationSection>，请调用 `GetSection` 并提供节名称：</span><span class="sxs-lookup"><span data-stu-id="e757a-536">To return an <xref:Microsoft.Extensions.Configuration.IConfigurationSection> containing only the key-value pairs in `section1`, call `GetSection` and supply the section name:</span></span>

```csharp
var configSection = _config.GetSection("section1");
```

<span data-ttu-id="e757a-537">同样，若要获取 `section2:subsection0` 中键的值，请调用 `GetSection` 并提供节路径：</span><span class="sxs-lookup"><span data-stu-id="e757a-537">Similarly, to obtain the values for keys in `section2:subsection0`, call `GetSection` and supply the section path:</span></span>

```csharp
var configSection = _config.GetSection("section2:subsection0");
```

<span data-ttu-id="e757a-538">`GetSection` 永远不会返回 `null`。</span><span class="sxs-lookup"><span data-stu-id="e757a-538">`GetSection` never returns `null`.</span></span> <span data-ttu-id="e757a-539">如果找不到匹配的节，则返回空 `IConfigurationSection`。</span><span class="sxs-lookup"><span data-stu-id="e757a-539">If a matching section isn't found, an empty `IConfigurationSection` is returned.</span></span>

### <a name="getchildren"></a><span data-ttu-id="e757a-540">GetChildren</span><span class="sxs-lookup"><span data-stu-id="e757a-540">GetChildren</span></span>

<span data-ttu-id="e757a-541">在 `section2` 上调用 [IConfiguration.GetChildren](xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*) 会获得 `IEnumerable<IConfigurationSection>`，其中包括：</span><span class="sxs-lookup"><span data-stu-id="e757a-541">A call to [IConfiguration.GetChildren](xref:Microsoft.Extensions.Configuration.IConfiguration.GetChildren*) on `section2` obtains an `IEnumerable<IConfigurationSection>` that includes:</span></span>

* `subsection0`
* `subsection1`

```csharp
var configSection = _config.GetSection("section2");

var children = configSection.GetChildren();
```

::: moniker range=">= aspnetcore-2.0"

### <a name="exists"></a><span data-ttu-id="e757a-542">存在</span><span class="sxs-lookup"><span data-stu-id="e757a-542">Exists</span></span>

<span data-ttu-id="e757a-543">使用 [ConfigurationExtensions.Exists](xref:Microsoft.Extensions.Configuration.ConfigurationExtensions.Exists*) 确定配置节是否存在：</span><span class="sxs-lookup"><span data-stu-id="e757a-543">Use [ConfigurationExtensions.Exists](xref:Microsoft.Extensions.Configuration.ConfigurationExtensions.Exists*) to determine if a configuration section exists:</span></span>

```csharp
var sectionExists = _config.GetSection("section2:subsection2").Exists();
```

<span data-ttu-id="e757a-544">给定示例数据，`sectionExists` 为 `false`，因为配置数据中没有 `section2:subsection2` 节。</span><span class="sxs-lookup"><span data-stu-id="e757a-544">Given the example data, `sectionExists` is `false` because there isn't a `section2:subsection2` section in the configuration data.</span></span>

::: moniker-end

## <a name="bind-to-a-class"></a><span data-ttu-id="e757a-545">绑定至类</span><span class="sxs-lookup"><span data-stu-id="e757a-545">Bind to a class</span></span>

<span data-ttu-id="e757a-546">可以使用选项模式将配置绑定到表示相关设置组的类。</span><span class="sxs-lookup"><span data-stu-id="e757a-546">Configuration can be bound to classes that represent groups of related settings using the *options pattern*.</span></span> <span data-ttu-id="e757a-547">有关更多信息，请参见<xref:fundamentals/configuration/options>。</span><span class="sxs-lookup"><span data-stu-id="e757a-547">For more information, see <xref:fundamentals/configuration/options>.</span></span>

<span data-ttu-id="e757a-548">配置值作为字符串返回，但调用 <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> 可以构造 [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) 对象。</span><span class="sxs-lookup"><span data-stu-id="e757a-548">Configuration values are returned as strings, but calling <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> enables the construction of [POCO](https://wikipedia.org/wiki/Plain_Old_CLR_Object) objects.</span></span>

<span data-ttu-id="e757a-549">示例应用包含 `Starship` 模型 (Models/Starship.cs)：</span><span class="sxs-lookup"><span data-stu-id="e757a-549">The sample app contains a `Starship` model (*Models/Starship.cs*):</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/Starship.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/Starship.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-550">当示例应用使用 JSON 配置提供程序加载配置时，starship.json 文件的 `starship` 节会创建配置：</span><span class="sxs-lookup"><span data-stu-id="e757a-550">The `starship` section of the *starship.json* file creates the configuration when the sample app uses the JSON Configuration Provider to load the configuration:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-json[](index/samples/2.x/ConfigurationSample/starship.json)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-json[](index/samples/1.x/ConfigurationSample/starship.json)]

::: moniker-end

<span data-ttu-id="e757a-551">创建以下配置键值对：</span><span class="sxs-lookup"><span data-stu-id="e757a-551">The following configuration key-value pairs are created:</span></span>

| <span data-ttu-id="e757a-552">键</span><span class="sxs-lookup"><span data-stu-id="e757a-552">Key</span></span>                   | <span data-ttu-id="e757a-553">“值”</span><span class="sxs-lookup"><span data-stu-id="e757a-553">Value</span></span>                                             |
| --------------------- | ------------------------------------------------- |
| <span data-ttu-id="e757a-554">starship:name</span><span class="sxs-lookup"><span data-stu-id="e757a-554">starship:name</span></span>         | <span data-ttu-id="e757a-555">USS Enterprise</span><span class="sxs-lookup"><span data-stu-id="e757a-555">USS Enterprise</span></span>                                    |
| <span data-ttu-id="e757a-556">starship:registry</span><span class="sxs-lookup"><span data-stu-id="e757a-556">starship:registry</span></span>     | <span data-ttu-id="e757a-557">NCC-1701</span><span class="sxs-lookup"><span data-stu-id="e757a-557">NCC-1701</span></span>                                          |
| <span data-ttu-id="e757a-558">starship:class</span><span class="sxs-lookup"><span data-stu-id="e757a-558">starship:class</span></span>        | <span data-ttu-id="e757a-559">Constitution</span><span class="sxs-lookup"><span data-stu-id="e757a-559">Constitution</span></span>                                      |
| <span data-ttu-id="e757a-560">starship:length</span><span class="sxs-lookup"><span data-stu-id="e757a-560">starship:length</span></span>       | <span data-ttu-id="e757a-561">304.8</span><span class="sxs-lookup"><span data-stu-id="e757a-561">304.8</span></span>                                             |
| <span data-ttu-id="e757a-562">starship:commissioned</span><span class="sxs-lookup"><span data-stu-id="e757a-562">starship:commissioned</span></span> | <span data-ttu-id="e757a-563">False</span><span class="sxs-lookup"><span data-stu-id="e757a-563">False</span></span>                                             |
| <span data-ttu-id="e757a-564">trademark</span><span class="sxs-lookup"><span data-stu-id="e757a-564">trademark</span></span>             | <span data-ttu-id="e757a-565">Paramount Pictures Corp. http://www.paramount.com</span><span class="sxs-lookup"><span data-stu-id="e757a-565">Paramount Pictures Corp. http://www.paramount.com</span></span> |

<span data-ttu-id="e757a-566">示例应用使用 `starship` 键调用 `GetSection`。</span><span class="sxs-lookup"><span data-stu-id="e757a-566">The sample app calls `GetSection` with the `starship` key.</span></span> <span data-ttu-id="e757a-567">`starship` 键值对是独立的。</span><span class="sxs-lookup"><span data-stu-id="e757a-567">The `starship` key-value pairs are isolated.</span></span> <span data-ttu-id="e757a-568">在子节传入 `Starship` 类的实例时调用 `Bind` 方法。</span><span class="sxs-lookup"><span data-stu-id="e757a-568">The `Bind` method is called on the subsection passing in an instance of the `Starship` class.</span></span> <span data-ttu-id="e757a-569">绑定实例值后，将实例分配给用于呈现的属性：</span><span class="sxs-lookup"><span data-stu-id="e757a-569">After binding the instance values, the instance is assigned to a property for rendering:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Pages/Index.cshtml.cs?name=snippet_starship)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Controllers/HomeController.cs?name=snippet_starship)]

::: moniker-end

## <a name="bind-to-an-object-graph"></a><span data-ttu-id="e757a-570">绑定至对象图</span><span class="sxs-lookup"><span data-stu-id="e757a-570">Bind to an object graph</span></span>

<span data-ttu-id="e757a-571"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> 能够绑定整个 POCO 对象图。</span><span class="sxs-lookup"><span data-stu-id="e757a-571"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> is capable of binding an entire POCO object graph.</span></span>

<span data-ttu-id="e757a-572">该示例包含 `TvShow` 模型，其对象图包含 `Metadata` 和 `Actors` 类 (Models/TvShow.cs)：</span><span class="sxs-lookup"><span data-stu-id="e757a-572">The sample contains a `TvShow` model whose object graph includes `Metadata` and `Actors` classes (*Models/TvShow.cs*):</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/TvShow.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/TvShow.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-573">示例应用有一个包含配置数据的 tvshow.xml 文件：</span><span class="sxs-lookup"><span data-stu-id="e757a-573">The sample app has a *tvshow.xml* file containing the configuration data:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-xml[](index/samples/2.x/ConfigurationSample/tvshow.xml)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-xml[](index/samples/1.x/ConfigurationSample/tvshow.xml)]

::: moniker-end

<span data-ttu-id="e757a-574">使用 `Bind` 方法将配置绑定到整个 `TvShow` 对象图。</span><span class="sxs-lookup"><span data-stu-id="e757a-574">Configuration is bound to the entire `TvShow` object graph with the `Bind` method.</span></span> <span data-ttu-id="e757a-575">将绑定实例分配给用于呈现的属性：</span><span class="sxs-lookup"><span data-stu-id="e757a-575">The bound instance is assigned to a property for rendering:</span></span>

::: moniker range=">= aspnetcore-2.0"

```csharp
var tvShow = new TvShow();
_config.GetSection("tvshow").Bind(tvShow);
TvShow = tvShow;
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

```csharp
var tvShow = new TvShow();
_config.GetSection("tvshow").Bind(tvShow);
viewModel.TvShow = tvShow;
```

::: moniker-end

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="e757a-576">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) 绑定并返回指定类型。</span><span class="sxs-lookup"><span data-stu-id="e757a-576">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) binds and returns the specified type.</span></span> <span data-ttu-id="e757a-577">`Get<T>` 比使用 `Bind` 更方便。</span><span class="sxs-lookup"><span data-stu-id="e757a-577">`Get<T>` is more convenient than using `Bind`.</span></span> <span data-ttu-id="e757a-578">以下代码显示如何将 `Get<T>` 与前面的示例一起使用，该示例允许将绑定实例直接分配给用于呈现的属性：</span><span class="sxs-lookup"><span data-stu-id="e757a-578">The following code shows how to use `Get<T>` with the preceding example, which allows the bound instance to be directly assigned to the property used for rendering:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Pages/Index.cshtml.cs?name=snippet_tvshow)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Controllers/HomeController.cs?name=snippet_tvshow)]

::: moniker-end

## <a name="bind-an-array-to-a-class"></a><span data-ttu-id="e757a-579">将数组绑定至类</span><span class="sxs-lookup"><span data-stu-id="e757a-579">Bind an array to a class</span></span>

<span data-ttu-id="e757a-580">示例应用演示了本部分中介绍的概念。</span><span class="sxs-lookup"><span data-stu-id="e757a-580">*The sample app demonstrates the concepts explained in this section.*</span></span>

<span data-ttu-id="e757a-581"><xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> 支持使用配置键中的数组索引将数组绑定到对象。</span><span class="sxs-lookup"><span data-stu-id="e757a-581">The <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind*> supports binding arrays to objects using array indices in configuration keys.</span></span> <span data-ttu-id="e757a-582">公开数字键段（`:0:`、`:1:`、&hellip; `:{n}:`）的任何数组格式都能够与 POCO 类数组进行数组绑定。</span><span class="sxs-lookup"><span data-stu-id="e757a-582">Any array format that exposes a numeric key segment (`:0:`, `:1:`, &hellip; `:{n}:`) is capable of array binding to a POCO class array.</span></span>

> [!NOTE]
> <span data-ttu-id="e757a-583">绑定是按约定提供的。</span><span class="sxs-lookup"><span data-stu-id="e757a-583">Binding is provided by convention.</span></span> <span data-ttu-id="e757a-584">不需要自定义配置提供程序实现数组绑定。</span><span class="sxs-lookup"><span data-stu-id="e757a-584">Custom configuration providers aren't required to implement array binding.</span></span>

<span data-ttu-id="e757a-585">**内存中数组处理**</span><span class="sxs-lookup"><span data-stu-id="e757a-585">**In-memory array processing**</span></span>

<span data-ttu-id="e757a-586">请考虑下表中所示的配置键和值。</span><span class="sxs-lookup"><span data-stu-id="e757a-586">Consider the configuration keys and values shown in the following table.</span></span>

| <span data-ttu-id="e757a-587">键</span><span class="sxs-lookup"><span data-stu-id="e757a-587">Key</span></span>     | <span data-ttu-id="e757a-588">“值”</span><span class="sxs-lookup"><span data-stu-id="e757a-588">Value</span></span>  |
| :-----: | :----: |
| <span data-ttu-id="e757a-589">array:0</span><span class="sxs-lookup"><span data-stu-id="e757a-589">array:0</span></span> | <span data-ttu-id="e757a-590">value0</span><span class="sxs-lookup"><span data-stu-id="e757a-590">value0</span></span> |
| <span data-ttu-id="e757a-591">array:1</span><span class="sxs-lookup"><span data-stu-id="e757a-591">array:1</span></span> | <span data-ttu-id="e757a-592">value1</span><span class="sxs-lookup"><span data-stu-id="e757a-592">value1</span></span> |
| <span data-ttu-id="e757a-593">array:2</span><span class="sxs-lookup"><span data-stu-id="e757a-593">array:2</span></span> | <span data-ttu-id="e757a-594">value2</span><span class="sxs-lookup"><span data-stu-id="e757a-594">value2</span></span> |
| <span data-ttu-id="e757a-595">array:4</span><span class="sxs-lookup"><span data-stu-id="e757a-595">array:4</span></span> | <span data-ttu-id="e757a-596">value4</span><span class="sxs-lookup"><span data-stu-id="e757a-596">value4</span></span> |
| <span data-ttu-id="e757a-597">array:5</span><span class="sxs-lookup"><span data-stu-id="e757a-597">array:5</span></span> | <span data-ttu-id="e757a-598">value5</span><span class="sxs-lookup"><span data-stu-id="e757a-598">value5</span></span> |

<span data-ttu-id="e757a-599">使用内存配置提供程序在示例应用中加载这些键和值：</span><span class="sxs-lookup"><span data-stu-id="e757a-599">These keys and values are loaded in the sample app using the Memory Configuration Provider:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Program.cs?name=snippet_Program&highlight=3-10,22)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Startup.cs?name=snippet_Startup&highlight=5-12,16)]

::: moniker-end

<span data-ttu-id="e757a-600">该数组跳过索引 &num;3 的值。</span><span class="sxs-lookup"><span data-stu-id="e757a-600">The array skips a value for index &num;3.</span></span> <span data-ttu-id="e757a-601">配置绑定程序无法绑定 null 值，也无法在绑定对象中创建 null 条目，这在演示将此数组绑定到对象的结果时变得清晰。</span><span class="sxs-lookup"><span data-stu-id="e757a-601">The configuration binder isn't capable of binding null values or creating null entries in bound objects, which becomes clear in a moment when the result of binding this array to an object is demonstrated.</span></span>

<span data-ttu-id="e757a-602">在示例应用中，POCO 类可用于保存绑定的配置数据：</span><span class="sxs-lookup"><span data-stu-id="e757a-602">In the sample app, a POCO class is available to hold the bound configuration data:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/ArrayExample.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/ArrayExample.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-603">将配置数据绑定至对象：</span><span class="sxs-lookup"><span data-stu-id="e757a-603">The configuration data is bound to the object:</span></span>

```csharp
var arrayExample = new ArrayExample();
_config.GetSection("array").Bind(arrayExample);
```

::: moniker range=">= aspnetcore-1.1"

<span data-ttu-id="e757a-604">还可以使用 [ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) 语法，从而产生更精简的代码：</span><span class="sxs-lookup"><span data-stu-id="e757a-604">[ConfigurationBinder.Get&lt;T&gt;](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get*) syntax can also be used, which results in more compact code:</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Pages/Index.cshtml.cs?name=snippet_array)]

::: moniker-end

::: moniker range="= aspnetcore-1.1"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Controllers/HomeController.cs?name=snippet_array)]

::: moniker-end

<span data-ttu-id="e757a-605">绑定对象（`ArrayExample` 的实例）从配置接收数组数据。</span><span class="sxs-lookup"><span data-stu-id="e757a-605">The bound object, an instance of `ArrayExample`, receives the array data from configuration.</span></span>

| <span data-ttu-id="e757a-606">`ArrayExamples.Entries` 索引</span><span class="sxs-lookup"><span data-stu-id="e757a-606">`ArrayExamples.Entries` Index</span></span> | <span data-ttu-id="e757a-607">`ArrayExamples.Entries` 值</span><span class="sxs-lookup"><span data-stu-id="e757a-607">`ArrayExamples.Entries` Value</span></span> |
| :---------------------------: | :---------------------------: |
| <span data-ttu-id="e757a-608">0</span><span class="sxs-lookup"><span data-stu-id="e757a-608">0</span></span>                             | <span data-ttu-id="e757a-609">value0</span><span class="sxs-lookup"><span data-stu-id="e757a-609">value0</span></span>                        |
| <span data-ttu-id="e757a-610">1</span><span class="sxs-lookup"><span data-stu-id="e757a-610">1</span></span>                             | <span data-ttu-id="e757a-611">value1</span><span class="sxs-lookup"><span data-stu-id="e757a-611">value1</span></span>                        |
| <span data-ttu-id="e757a-612">2</span><span class="sxs-lookup"><span data-stu-id="e757a-612">2</span></span>                             | <span data-ttu-id="e757a-613">value2</span><span class="sxs-lookup"><span data-stu-id="e757a-613">value2</span></span>                        |
| <span data-ttu-id="e757a-614">3</span><span class="sxs-lookup"><span data-stu-id="e757a-614">3</span></span>                             | <span data-ttu-id="e757a-615">value4</span><span class="sxs-lookup"><span data-stu-id="e757a-615">value4</span></span>                        |
| <span data-ttu-id="e757a-616">4</span><span class="sxs-lookup"><span data-stu-id="e757a-616">4</span></span>                             | <span data-ttu-id="e757a-617">value5</span><span class="sxs-lookup"><span data-stu-id="e757a-617">value5</span></span>                        |

<span data-ttu-id="e757a-618">绑定对象中的索引 &num;3 保留 `array:4` 配置键的配置数据及其值 `value4`。</span><span class="sxs-lookup"><span data-stu-id="e757a-618">Index &num;3 in the bound object holds the configuration data for the `array:4` configuration key and its value of `value4`.</span></span> <span data-ttu-id="e757a-619">当绑定包含数组的配置数据时，配置键中的数组索引仅用于在创建对象时迭代配置数据。</span><span class="sxs-lookup"><span data-stu-id="e757a-619">When configuration data containing an array is bound, the array indices in the configuration keys are merely used to iterate the configuration data when creating the object.</span></span> <span data-ttu-id="e757a-620">无法在配置数据中保留 null 值，并且当配置键中的数组跳过一个或多个索引时，不会在绑定对象中创建 null 值条目。</span><span class="sxs-lookup"><span data-stu-id="e757a-620">A null value can't be retained in configuration data, and a null-valued entry isn't created in a bound object when an array in configuration keys skip one or more indices.</span></span>

<span data-ttu-id="e757a-621">可以在由任何在配置中生成正确键值对的配置提供程序绑定到 `ArrayExamples` 实例之前提供索引 &num;3 的缺失配置项。</span><span class="sxs-lookup"><span data-stu-id="e757a-621">The missing configuration item for index &num;3 can be supplied before binding to the `ArrayExamples` instance by any configuration provider that produces the correct key-value pair in configuration.</span></span> <span data-ttu-id="e757a-622">如果示例包含具有缺失键值对的其他 JSON 配置提供程序，则 `ArrayExamples.Entries` 与完整配置数组相匹配：</span><span class="sxs-lookup"><span data-stu-id="e757a-622">If the sample included an additional JSON Configuration Provider with the missing key-value pair, the `ArrayExamples.Entries` matches the complete configuration array:</span></span>

<span data-ttu-id="e757a-623">*missing_value.json*:</span><span class="sxs-lookup"><span data-stu-id="e757a-623">*missing_value.json*:</span></span>

```json
{
  "array:entries:3": "value3"
}
```

::: moniker range=">= aspnetcore-2.0"

<span data-ttu-id="e757a-624">在 <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>中：</span><span class="sxs-lookup"><span data-stu-id="e757a-624">In <xref:Microsoft.Extensions.Hosting.HostBuilder.ConfigureAppConfiguration*>:</span></span>

```csharp
config.AddJsonFile("missing_value.json", optional: false, reloadOnChange: false);
```

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="e757a-625">在 `Startup` 构造函数中：</span><span class="sxs-lookup"><span data-stu-id="e757a-625">In the `Startup` constructor:</span></span>

```csharp
.AddJsonFile("missing_value.json", optional: false, reloadOnChange: false);
```

::: moniker-end

<span data-ttu-id="e757a-626">将表中所示的键值对加载到配置中。</span><span class="sxs-lookup"><span data-stu-id="e757a-626">The key-value pair shown in the table is loaded into configuration.</span></span>

| <span data-ttu-id="e757a-627">键</span><span class="sxs-lookup"><span data-stu-id="e757a-627">Key</span></span>             | <span data-ttu-id="e757a-628">“值”</span><span class="sxs-lookup"><span data-stu-id="e757a-628">Value</span></span>  |
| :-------------: | :----: |
| <span data-ttu-id="e757a-629">array:entries:3</span><span class="sxs-lookup"><span data-stu-id="e757a-629">array:entries:3</span></span> | <span data-ttu-id="e757a-630">value3</span><span class="sxs-lookup"><span data-stu-id="e757a-630">value3</span></span> |

<span data-ttu-id="e757a-631">如果在 JSON 配置提供程序包含索引 &num;3 的条目之后绑定 `ArrayExamples` 类实例，则 `ArrayExamples.Entries` 数组包含该值。</span><span class="sxs-lookup"><span data-stu-id="e757a-631">If the `ArrayExamples` class instance is bound after the JSON Configuration Provider includes the entry for index &num;3, the `ArrayExamples.Entries` array includes the value.</span></span>

| <span data-ttu-id="e757a-632">`ArrayExamples.Entries` 索引</span><span class="sxs-lookup"><span data-stu-id="e757a-632">`ArrayExamples.Entries` Index</span></span> | <span data-ttu-id="e757a-633">`ArrayExamples.Entries` 值</span><span class="sxs-lookup"><span data-stu-id="e757a-633">`ArrayExamples.Entries` Value</span></span> |
| :---------------------------: | :---------------------------: |
| <span data-ttu-id="e757a-634">0</span><span class="sxs-lookup"><span data-stu-id="e757a-634">0</span></span>                             | <span data-ttu-id="e757a-635">value0</span><span class="sxs-lookup"><span data-stu-id="e757a-635">value0</span></span>                        |
| <span data-ttu-id="e757a-636">1</span><span class="sxs-lookup"><span data-stu-id="e757a-636">1</span></span>                             | <span data-ttu-id="e757a-637">value1</span><span class="sxs-lookup"><span data-stu-id="e757a-637">value1</span></span>                        |
| <span data-ttu-id="e757a-638">2</span><span class="sxs-lookup"><span data-stu-id="e757a-638">2</span></span>                             | <span data-ttu-id="e757a-639">value2</span><span class="sxs-lookup"><span data-stu-id="e757a-639">value2</span></span>                        |
| <span data-ttu-id="e757a-640">3</span><span class="sxs-lookup"><span data-stu-id="e757a-640">3</span></span>                             | <span data-ttu-id="e757a-641">value3</span><span class="sxs-lookup"><span data-stu-id="e757a-641">value3</span></span>                        |
| <span data-ttu-id="e757a-642">4</span><span class="sxs-lookup"><span data-stu-id="e757a-642">4</span></span>                             | <span data-ttu-id="e757a-643">value4</span><span class="sxs-lookup"><span data-stu-id="e757a-643">value4</span></span>                        |
| <span data-ttu-id="e757a-644">5</span><span class="sxs-lookup"><span data-stu-id="e757a-644">5</span></span>                             | <span data-ttu-id="e757a-645">value5</span><span class="sxs-lookup"><span data-stu-id="e757a-645">value5</span></span>                        |

<span data-ttu-id="e757a-646">**JSON 数组处理**</span><span class="sxs-lookup"><span data-stu-id="e757a-646">**JSON array processing**</span></span>

<span data-ttu-id="e757a-647">如果 JSON 文件包含数组，则会为具有从零开始的节索引的数组元素创建配置键。</span><span class="sxs-lookup"><span data-stu-id="e757a-647">If a JSON file contains an array, configuration keys are created for the array elements with a zero-based section index.</span></span> <span data-ttu-id="e757a-648">在以下配置文件中，`subsection` 是一个数组：</span><span class="sxs-lookup"><span data-stu-id="e757a-648">In the following configuration file, `subsection` is an array:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-json[](index/samples/2.x/ConfigurationSample/json_array.json)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-json[](index/samples/1.x/ConfigurationSample/json_array.json)]

::: moniker-end

<span data-ttu-id="e757a-649">JSON 配置提供程序将配置数据读入以下键值对：</span><span class="sxs-lookup"><span data-stu-id="e757a-649">The JSON Configuration Provider reads the configuration data into the following key-value pairs:</span></span>

| <span data-ttu-id="e757a-650">键</span><span class="sxs-lookup"><span data-stu-id="e757a-650">Key</span></span>                     | <span data-ttu-id="e757a-651">“值”</span><span class="sxs-lookup"><span data-stu-id="e757a-651">Value</span></span>  |
| ----------------------- | :----: |
| <span data-ttu-id="e757a-652">json_array:key</span><span class="sxs-lookup"><span data-stu-id="e757a-652">json_array:key</span></span>          | <span data-ttu-id="e757a-653">valueA</span><span class="sxs-lookup"><span data-stu-id="e757a-653">valueA</span></span> |
| <span data-ttu-id="e757a-654">json_array:subsection:0</span><span class="sxs-lookup"><span data-stu-id="e757a-654">json_array:subsection:0</span></span> | <span data-ttu-id="e757a-655">valueB</span><span class="sxs-lookup"><span data-stu-id="e757a-655">valueB</span></span> |
| <span data-ttu-id="e757a-656">json_array:subsection:1</span><span class="sxs-lookup"><span data-stu-id="e757a-656">json_array:subsection:1</span></span> | <span data-ttu-id="e757a-657">valueC</span><span class="sxs-lookup"><span data-stu-id="e757a-657">valueC</span></span> |
| <span data-ttu-id="e757a-658">json_array:subsection:2</span><span class="sxs-lookup"><span data-stu-id="e757a-658">json_array:subsection:2</span></span> | <span data-ttu-id="e757a-659">valueD</span><span class="sxs-lookup"><span data-stu-id="e757a-659">valueD</span></span> |

<span data-ttu-id="e757a-660">在示例应用中，以下 POCO 类可用于绑定配置键值对：</span><span class="sxs-lookup"><span data-stu-id="e757a-660">In the sample app, the following POCO class is available to bind the configuration key-value pairs:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/JsonArrayExample.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/JsonArrayExample.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-661">绑定后，`JsonArrayExample.Key` 保存值 `valueA`。</span><span class="sxs-lookup"><span data-stu-id="e757a-661">After binding, `JsonArrayExample.Key` holds the value `valueA`.</span></span> <span data-ttu-id="e757a-662">子节值存储在 POCO 数组属性 `Subsection` 中。</span><span class="sxs-lookup"><span data-stu-id="e757a-662">The subsection values are stored in the POCO array property, `Subsection`.</span></span>

| <span data-ttu-id="e757a-663">`JsonArrayExample.Subsection` 索引</span><span class="sxs-lookup"><span data-stu-id="e757a-663">`JsonArrayExample.Subsection` Index</span></span> | <span data-ttu-id="e757a-664">`JsonArrayExample.Subsection` 值</span><span class="sxs-lookup"><span data-stu-id="e757a-664">`JsonArrayExample.Subsection` Value</span></span> |
| :---------------------------------: | :---------------------------------: |
| <span data-ttu-id="e757a-665">0</span><span class="sxs-lookup"><span data-stu-id="e757a-665">0</span></span>                                   | <span data-ttu-id="e757a-666">valueB</span><span class="sxs-lookup"><span data-stu-id="e757a-666">valueB</span></span>                              |
| <span data-ttu-id="e757a-667">1</span><span class="sxs-lookup"><span data-stu-id="e757a-667">1</span></span>                                   | <span data-ttu-id="e757a-668">valueC</span><span class="sxs-lookup"><span data-stu-id="e757a-668">valueC</span></span>                              |
| <span data-ttu-id="e757a-669">2</span><span class="sxs-lookup"><span data-stu-id="e757a-669">2</span></span>                                   | <span data-ttu-id="e757a-670">valueD</span><span class="sxs-lookup"><span data-stu-id="e757a-670">valueD</span></span>                              |

## <a name="custom-configuration-provider"></a><span data-ttu-id="e757a-671">自定义配置提供程序</span><span class="sxs-lookup"><span data-stu-id="e757a-671">Custom configuration provider</span></span>

<span data-ttu-id="e757a-672">该示例应用演示了如何使用[实体框架 (EF)](/ef/core/) 创建从数据库读取配置键值对的基本配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-672">The sample app demonstrates how to create a basic configuration provider that reads configuration key-value pairs from a database using [Entity Framework (EF)](/ef/core/).</span></span>

<span data-ttu-id="e757a-673">提供程序具有以下特征：</span><span class="sxs-lookup"><span data-stu-id="e757a-673">The provider has the following characteristics:</span></span>

* <span data-ttu-id="e757a-674">EF 内存中数据库用于演示目的。</span><span class="sxs-lookup"><span data-stu-id="e757a-674">The EF in-memory database is used for demonstration purposes.</span></span> <span data-ttu-id="e757a-675">若要使用需要连接字符串的数据库，请实现辅助 `ConfigurationBuilder` 以从另一个配置提供程序提供连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e757a-675">To use a database that requires a connection string, implement a secondary `ConfigurationBuilder` to supply the connection string from another configuration provider.</span></span>
* <span data-ttu-id="e757a-676">提供程序在启动时将数据库表读入配置。</span><span class="sxs-lookup"><span data-stu-id="e757a-676">The provider reads a database table into configuration at startup.</span></span> <span data-ttu-id="e757a-677">提供程序不会基于每个键查询数据库。</span><span class="sxs-lookup"><span data-stu-id="e757a-677">The provider doesn't query the database on a per-key basis.</span></span>
* <span data-ttu-id="e757a-678">未实现更改时重载，因此在应用启动后更新数据库对应用的配置没有任何影响。</span><span class="sxs-lookup"><span data-stu-id="e757a-678">Reload-on-change isn't implemented, so updating the database after the app starts has no effect on the app's configuration.</span></span>

<span data-ttu-id="e757a-679">定义用于在数据库中存储配置值的 `EFConfigurationValue` 实体。</span><span class="sxs-lookup"><span data-stu-id="e757a-679">Define an `EFConfigurationValue` entity for storing configuration values in the database.</span></span>

<span data-ttu-id="e757a-680">*Models/EFConfigurationValue.cs*：</span><span class="sxs-lookup"><span data-stu-id="e757a-680">*Models/EFConfigurationValue.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Models/EFConfigurationValue.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Models/EFConfigurationValue.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-681">添加 `EFConfigurationContext` 以存储和访问配置的值。</span><span class="sxs-lookup"><span data-stu-id="e757a-681">Add an `EFConfigurationContext` to store and access the configured values.</span></span>

<span data-ttu-id="e757a-682">*EFConfigurationProvider/EFConfigurationContext.cs*：</span><span class="sxs-lookup"><span data-stu-id="e757a-682">*EFConfigurationProvider/EFConfigurationContext.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationContext.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationContext.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-683">创建用于实现 <xref:Microsoft.Extensions.Configuration.IConfigurationSource> 的类。</span><span class="sxs-lookup"><span data-stu-id="e757a-683">Create a class that implements <xref:Microsoft.Extensions.Configuration.IConfigurationSource>.</span></span>

<span data-ttu-id="e757a-684">*EFConfigurationProvider/EFConfigurationSource.cs*：</span><span class="sxs-lookup"><span data-stu-id="e757a-684">*EFConfigurationProvider/EFConfigurationSource.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationSource.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationSource.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-685">通过从 <xref:Microsoft.Extensions.Configuration.ConfigurationProvider> 继承来创建自定义配置提供程序。</span><span class="sxs-lookup"><span data-stu-id="e757a-685">Create the custom configuration provider by inheriting from <xref:Microsoft.Extensions.Configuration.ConfigurationProvider>.</span></span> <span data-ttu-id="e757a-686">当数据库为空时，配置提供程序将对其进行初始化。</span><span class="sxs-lookup"><span data-stu-id="e757a-686">The configuration provider initializes the database when it's empty.</span></span>

<span data-ttu-id="e757a-687">*EFConfigurationProvider/EFConfigurationProvider.cs*：</span><span class="sxs-lookup"><span data-stu-id="e757a-687">*EFConfigurationProvider/EFConfigurationProvider.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationProvider.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/EFConfigurationProvider/EFConfigurationProvider.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-688">可以使用 `AddEFConfiguration` 扩展方法将配置源添加到 `ConfigurationBuilder`。</span><span class="sxs-lookup"><span data-stu-id="e757a-688">An `AddEFConfiguration` extension method permits adding the configuration source to a `ConfigurationBuilder`.</span></span>

<span data-ttu-id="e757a-689">Extensions/EntityFrameworkExtensions.cs：</span><span class="sxs-lookup"><span data-stu-id="e757a-689">*Extensions/EntityFrameworkExtensions.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Extensions/EntityFrameworkExtensions.cs?name=snippet1)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Extensions/EntityFrameworkExtensions.cs?name=snippet1)]

::: moniker-end

<span data-ttu-id="e757a-690">下面的代码演示如何在 Program.cs 中使用自定义的 `EFConfigurationProvider`：</span><span class="sxs-lookup"><span data-stu-id="e757a-690">The following code shows how to use the custom `EFConfigurationProvider` in *Program.cs*:</span></span>

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](index/samples/2.x/ConfigurationSample/Program.cs?name=snippet_Program&highlight=26)]

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](index/samples/1.x/ConfigurationSample/Startup.cs?name=snippet_Startup&highlight=24)]

::: moniker-end

## <a name="access-configuration-during-startup"></a><span data-ttu-id="e757a-691">在启动期间访问配置</span><span class="sxs-lookup"><span data-stu-id="e757a-691">Access configuration during startup</span></span>

<span data-ttu-id="e757a-692">将 `IConfiguration` 注入 `Startup` 构造函数以访问 `Startup.ConfigureServices` 中的配置值。</span><span class="sxs-lookup"><span data-stu-id="e757a-692">Inject `IConfiguration` into the `Startup` constructor to access configuration values in `Startup.ConfigureServices`.</span></span> <span data-ttu-id="e757a-693">若要访问 `Startup.Configure` 中的配置，请将 `IConfiguration` 直接注入方法或使用构造函数中的实例：</span><span class="sxs-lookup"><span data-stu-id="e757a-693">To access configuration in `Startup.Configure`, either inject `IConfiguration` directly into the method or use the instance from the constructor:</span></span>

```csharp
public class Startup
{
    private readonly IConfiguration _config;

    public Startup(IConfiguration config)
    {
        _config = config;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        var value = _config["key"];
    }

    public void Configure(IApplicationBuilder app, IConfiguration config)
    {
        var value = config["key"];
    }
}
```

<span data-ttu-id="e757a-694">有关使用启动便捷方法访问配置的示例，请参阅[应用启动：便捷方法](xref:fundamentals/startup#convenience-methods)。</span><span class="sxs-lookup"><span data-stu-id="e757a-694">For an example of accessing configuration using startup convenience methods, see [App startup: Convenience methods](xref:fundamentals/startup#convenience-methods).</span></span>

## <a name="access-configuration-in-a-razor-pages-page-or-mvc-view"></a><span data-ttu-id="e757a-695">在 Razor Pages 页或 MVC 视图中访问配置</span><span class="sxs-lookup"><span data-stu-id="e757a-695">Access configuration in a Razor Pages page or MVC view</span></span>

<span data-ttu-id="e757a-696">若要访问 Razor Pages 页或 MVC 视图中的配置设置，请为 [Microsoft.Extensions.Configuration 命名空间](xref:Microsoft.Extensions.Configuration)添加 [using 指令](xref:mvc/views/razor#using)（[C# 参考：using 指令](/dotnet/csharp/language-reference/keywords/using-directive)）并将 <xref:Microsoft.Extensions.Configuration.IConfiguration> 注入页面或视图。</span><span class="sxs-lookup"><span data-stu-id="e757a-696">To access configuration settings in a Razor Pages page or an MVC view, add a [using directive](xref:mvc/views/razor#using) ([C# reference: using directive](/dotnet/csharp/language-reference/keywords/using-directive)) for the [Microsoft.Extensions.Configuration namespace](xref:Microsoft.Extensions.Configuration) and inject <xref:Microsoft.Extensions.Configuration.IConfiguration> into the page or view.</span></span>

<span data-ttu-id="e757a-697">在 Razor 页面页中：</span><span class="sxs-lookup"><span data-stu-id="e757a-697">In a Razor Pages page:</span></span>

```cshtml
@page
@model IndexModel
@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Index Page</title>
</head>
<body>
    <h1>Access configuration in a Razor Pages page</h1>
    <p>Configuration value for 'key': @Configuration["key"]</p>
</body>
</html>
```

<span data-ttu-id="e757a-698">在 MVC 视图中：</span><span class="sxs-lookup"><span data-stu-id="e757a-698">In an MVC view:</span></span>

```cshtml
@using Microsoft.Extensions.Configuration
@inject IConfiguration Configuration

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Index View</title>
</head>
<body>
    <h1>Access configuration in an MVC view</h1>
    <p>Configuration value for 'key': @Configuration["key"]</p>
</body>
</html>
```

## <a name="add-configuration-from-an-external-assembly"></a><span data-ttu-id="e757a-699">从外部程序集添加配置</span><span class="sxs-lookup"><span data-stu-id="e757a-699">Add configuration from an external assembly</span></span>

<span data-ttu-id="e757a-700">通过 <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> 实现，可在启动时从应用 `Startup` 类之外的外部程序集向应用添加增强功能。</span><span class="sxs-lookup"><span data-stu-id="e757a-700">An <xref:Microsoft.AspNetCore.Hosting.IHostingStartup> implementation allows adding enhancements to an app at startup from an external assembly outside of the app's `Startup` class.</span></span> <span data-ttu-id="e757a-701">有关更多信息，请参见<xref:fundamentals/configuration/platform-specific-configuration>。</span><span class="sxs-lookup"><span data-stu-id="e757a-701">For more information, see <xref:fundamentals/configuration/platform-specific-configuration>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e757a-702">其他资源</span><span class="sxs-lookup"><span data-stu-id="e757a-702">Additional resources</span></span>

* <xref:fundamentals/configuration/options>
* [<span data-ttu-id="e757a-703">深入了解 Microsoft 配置</span><span class="sxs-lookup"><span data-stu-id="e757a-703">Deep Dive into Microsoft Configuration</span></span>](https://www.paraesthesia.com/archive/2018/06/20/microsoft-extensions-configuration-deep-dive/)
