---
uid: config-builder
title: ASP.NET 的配置生成器
author: rick-anderson
description: 了解如何将配置数据从外部源中的 web.config 值以外的源。
ms.author: riande
ms.date: 10/29/2018
ms.technology: aspnet
msc.type: content
ms.openlocfilehash: 4dcc62573fad13ec8b37b2c59e884eec7ca80b92
ms.sourcegitcommit: 54655f1e1abf0b64d19506334d94cfdb0caf55f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50148832"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="a9efb-103">ASP.NET 的配置生成器</span><span class="sxs-lookup"><span data-stu-id="a9efb-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="a9efb-104">通过[Stephen Molloy](https://github.com/StephenMolloy)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a9efb-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="a9efb-105">配置生成器提供用于 ASP.NET 应用，以配置值从外部源的现代和敏捷机制。</span><span class="sxs-lookup"><span data-stu-id="a9efb-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="a9efb-106">配置生成器：</span><span class="sxs-lookup"><span data-stu-id="a9efb-106">Configuration builders:</span></span>

* <span data-ttu-id="a9efb-107">是可在.NET Framework 4.7.1 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="a9efb-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="a9efb-108">提供用于读取配置值的灵活机制。</span><span class="sxs-lookup"><span data-stu-id="a9efb-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="a9efb-109">解决它们移动到容器并云环境已设定焦点的情况下，一些应用程序的基本需求。</span><span class="sxs-lookup"><span data-stu-id="a9efb-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="a9efb-110">可用来提高通过来自以前不可用的源的配置数据 （例如，Azure 密钥保管库和环境变量） 的保护.NET 配置系统中。</span><span class="sxs-lookup"><span data-stu-id="a9efb-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="a9efb-111">键/值配置生成器</span><span class="sxs-lookup"><span data-stu-id="a9efb-111">Key/value configuration builders</span></span>

<span data-ttu-id="a9efb-112">配置生成器可以处理的常见方案是提供用于配置各节的键/值模式的基本的键/值替代机制。</span><span class="sxs-lookup"><span data-stu-id="a9efb-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="a9efb-113">ConfigurationBuilders 的.NET Framework 概念不局限于特定的配置节或模式。</span><span class="sxs-lookup"><span data-stu-id="a9efb-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="a9efb-114">但是，在配置生成器的许多`Microsoft.Configuration.ConfigurationBuilders`([github](https://github.com/aspnet/MicrosoftConfigurationBuilders)， [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) 中的键/值模式工作。</span><span class="sxs-lookup"><span data-stu-id="a9efb-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="a9efb-115">键/值配置生成器设置</span><span class="sxs-lookup"><span data-stu-id="a9efb-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="a9efb-116">以下设置适用于所有键/值配置生成器中`Microsoft.Configuration.ConfigurationBuilders`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="a9efb-117">模式</span><span class="sxs-lookup"><span data-stu-id="a9efb-117">Mode</span></span>

<span data-ttu-id="a9efb-118">配置生成器使用外部源的键/值信息来填充所选的键/值元素的配置系统。</span><span class="sxs-lookup"><span data-stu-id="a9efb-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="a9efb-119">具体而言，`<appSettings/>`和`<connectionStrings/>`部分配置生成器从得到特殊处理。</span><span class="sxs-lookup"><span data-stu-id="a9efb-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="a9efb-120">构建者在三种模式下工作：</span><span class="sxs-lookup"><span data-stu-id="a9efb-120">The builders work in three modes:</span></span>

* <span data-ttu-id="a9efb-121">`Strict` 默认模式。</span><span class="sxs-lookup"><span data-stu-id="a9efb-121">`Strict` - The default mode.</span></span> <span data-ttu-id="a9efb-122">在此模式下，配置生成器只对进行操作的已知键/值为中心的配置节。</span><span class="sxs-lookup"><span data-stu-id="a9efb-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="a9efb-123">`Strict` 模式枚举的部分中的每个密钥。</span><span class="sxs-lookup"><span data-stu-id="a9efb-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="a9efb-124">如果在外部源中找到匹配项：</span><span class="sxs-lookup"><span data-stu-id="a9efb-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="a9efb-125">配置生成器将从外部源的值替换为生成的配置节中的值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="a9efb-126">`Greedy` -与密切相关此模式下`Strict`模式。</span><span class="sxs-lookup"><span data-stu-id="a9efb-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="a9efb-127">而不是被限制为原始配置中已存在的密钥：</span><span class="sxs-lookup"><span data-stu-id="a9efb-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="a9efb-128">配置生成器将所有键/值对从外部源都添加到生成的配置节。</span><span class="sxs-lookup"><span data-stu-id="a9efb-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="a9efb-129">`Expand` -对进行操作的原始 XML 之前被分析为的配置节对象。</span><span class="sxs-lookup"><span data-stu-id="a9efb-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="a9efb-130">它可以认为的令牌字符串中的扩展。</span><span class="sxs-lookup"><span data-stu-id="a9efb-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="a9efb-131">与模式匹配的原始 XML 字符串的任何部分`${token}`是标记扩展的候选项。</span><span class="sxs-lookup"><span data-stu-id="a9efb-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="a9efb-132">如果没有相应的值在外部源中找到，则不会更改该令牌。</span><span class="sxs-lookup"><span data-stu-id="a9efb-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="a9efb-133">在此模式下构建者并不局限于`<appSettings/>`和`<connectionStrings/>`部分。</span><span class="sxs-lookup"><span data-stu-id="a9efb-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="a9efb-134">中的以下标记*web.config*使[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)中`Strict`模式：</span><span class="sxs-lookup"><span data-stu-id="a9efb-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="a9efb-135">下面的代码读取`<appSettings/>`并`<connectionStrings/>`前面所示*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="a9efb-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="a9efb-136">前面的代码将设置属性值为：</span><span class="sxs-lookup"><span data-stu-id="a9efb-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="a9efb-137">中的值*web.config*文件如果密钥未设置环境变量中。</span><span class="sxs-lookup"><span data-stu-id="a9efb-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="a9efb-138">值的环境变量，如果设置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="a9efb-139">例如，`ServiceID`将包含：</span><span class="sxs-lookup"><span data-stu-id="a9efb-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="a9efb-140">"从 web.config 的 ServiceID value"，如果环境变量`ServiceID`未设置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="a9efb-141">值`ServiceID`环境变量，如果设置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="a9efb-142">下图显示`<appSettings/>`键/值从上述*web.config*文件设置环境编辑器中的文件：</span><span class="sxs-lookup"><span data-stu-id="a9efb-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![环境编辑器](config-builder/static/env.png)

<span data-ttu-id="a9efb-144">注意： 你可能需要退出并重新启动 Visual Studio 以查看环境变量中的更改。</span><span class="sxs-lookup"><span data-stu-id="a9efb-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="a9efb-145">前缀处理</span><span class="sxs-lookup"><span data-stu-id="a9efb-145">Prefix handling</span></span>

<span data-ttu-id="a9efb-146">键前缀可以简化设置密钥，因为：</span><span class="sxs-lookup"><span data-stu-id="a9efb-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="a9efb-147">.NET Framework 配置非常复杂且嵌套。</span><span class="sxs-lookup"><span data-stu-id="a9efb-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="a9efb-148">外部键/值源通常是基本和平面的性质。</span><span class="sxs-lookup"><span data-stu-id="a9efb-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="a9efb-149">例如，不嵌套环境变量。</span><span class="sxs-lookup"><span data-stu-id="a9efb-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="a9efb-150">使用任何以下方法来同时注入`<appSettings/>`和`<connectionStrings/>`到通过环境变量配置：</span><span class="sxs-lookup"><span data-stu-id="a9efb-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="a9efb-151">与`EnvironmentConfigBuilder`在默认`Strict`模式和配置文件中相应的密钥名称。</span><span class="sxs-lookup"><span data-stu-id="a9efb-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="a9efb-152">前面的代码和标记，采用此方法。</span><span class="sxs-lookup"><span data-stu-id="a9efb-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="a9efb-153">使用这种方法，你可以**不**具有相同命名的密钥在这种`<appSettings/>`和`<connectionStrings/>`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="a9efb-154">使用两个`EnvironmentConfigBuilder`中的 s`Greedy`具有不同前缀的模式和`stripPrefix`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="a9efb-155">使用此方法，该应用可以读取`<appSettings/>`和`<connectionStrings/>`而无需更新配置文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="a9efb-156">下一节[stripPrefix](#stripprefix)，演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a9efb-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="a9efb-157">使用两个`EnvironmentConfigBuilder`中的 s`Greedy`模式具有不同的前缀。</span><span class="sxs-lookup"><span data-stu-id="a9efb-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="a9efb-158">使用此方法不能将重复的键名称，作为密钥名称必须不同的前缀。</span><span class="sxs-lookup"><span data-stu-id="a9efb-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="a9efb-159">例如：</span><span class="sxs-lookup"><span data-stu-id="a9efb-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="a9efb-160">与前面的标记，可以使用同一平面的键/值源来填充两个不同部分的配置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="a9efb-161">下图显示`<appSettings/>`并`<connectionStrings/>`键/值从上述*web.config*文件设置环境编辑器中的文件：</span><span class="sxs-lookup"><span data-stu-id="a9efb-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![环境编辑器](config-builder/static/prefix.png)

<span data-ttu-id="a9efb-163">下面的代码读取`<appSettings/>`并`<connectionStrings/>`键/值包含在前面*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="a9efb-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="a9efb-164">前面的代码将设置属性值为：</span><span class="sxs-lookup"><span data-stu-id="a9efb-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="a9efb-165">中的值*web.config*文件如果密钥未设置环境变量中。</span><span class="sxs-lookup"><span data-stu-id="a9efb-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="a9efb-166">值的环境变量，如果设置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="a9efb-167">例如，使用以前*web.config*文件中，设置键/值在上一环境编辑器映像，和前面的代码中，以下值：</span><span class="sxs-lookup"><span data-stu-id="a9efb-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="a9efb-168">键</span><span class="sxs-lookup"><span data-stu-id="a9efb-168">Key</span></span>              | <span data-ttu-id="a9efb-169">“值”</span><span class="sxs-lookup"><span data-stu-id="a9efb-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="a9efb-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="a9efb-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="a9efb-171">从 env 变量 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="a9efb-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="a9efb-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="a9efb-172">AppSetting_default</span></span>            | <span data-ttu-id="a9efb-173">从 env AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="a9efb-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="a9efb-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="a9efb-174">ConnStr_default</span></span>         | <span data-ttu-id="a9efb-175">从 env ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="a9efb-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="a9efb-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="a9efb-176">stripPrefix</span></span>

<span data-ttu-id="a9efb-177">`stripPrefix`： 一个布尔值，默认为`false`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="a9efb-178">前面的 XML 标记分隔应用程序设置从连接字符串，但要求中的所有键*web.config*文件以使用指定的前缀。</span><span class="sxs-lookup"><span data-stu-id="a9efb-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="a9efb-179">例如，前缀`AppSetting`必须添加到`ServiceID`密钥 ("AppSetting_ServiceID")。</span><span class="sxs-lookup"><span data-stu-id="a9efb-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="a9efb-180">与`stripPrefix`，在不使用的前缀*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="a9efb-181">前缀必须有配置生成器源 （例如，在环境中。）我们预计大多数开发人员将使用`stripPrefix`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="a9efb-182">应用程序通常剥离前缀。</span><span class="sxs-lookup"><span data-stu-id="a9efb-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="a9efb-183">以下*web.config*去除前缀：</span><span class="sxs-lookup"><span data-stu-id="a9efb-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="a9efb-184">在前面*web.config*文件中，`default`密钥是在这种`<appSettings/>`和`<connectionStrings/>`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="a9efb-185">下图显示`<appSettings/>`并`<connectionStrings/>`键/值从上述*web.config*文件设置环境编辑器中的文件：</span><span class="sxs-lookup"><span data-stu-id="a9efb-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![环境编辑器](config-builder/static/prefix.png)

<span data-ttu-id="a9efb-187">下面的代码读取`<appSettings/>`并`<connectionStrings/>`键/值包含在前面*web.config*文件：</span><span class="sxs-lookup"><span data-stu-id="a9efb-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="a9efb-188">前面的代码将设置属性值为：</span><span class="sxs-lookup"><span data-stu-id="a9efb-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="a9efb-189">中的值*web.config*文件如果密钥未设置环境变量中。</span><span class="sxs-lookup"><span data-stu-id="a9efb-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="a9efb-190">值的环境变量，如果设置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="a9efb-191">例如，使用以前*web.config*文件中，设置键/值在上一环境编辑器映像，和前面的代码中，以下值：</span><span class="sxs-lookup"><span data-stu-id="a9efb-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="a9efb-192">键</span><span class="sxs-lookup"><span data-stu-id="a9efb-192">Key</span></span>              | <span data-ttu-id="a9efb-193">“值”</span><span class="sxs-lookup"><span data-stu-id="a9efb-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="a9efb-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="a9efb-194">ServiceID</span></span>           | <span data-ttu-id="a9efb-195">从 env 变量 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="a9efb-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="a9efb-196">default</span><span class="sxs-lookup"><span data-stu-id="a9efb-196">default</span></span>            | <span data-ttu-id="a9efb-197">从 env AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="a9efb-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="a9efb-198">default</span><span class="sxs-lookup"><span data-stu-id="a9efb-198">default</span></span>         | <span data-ttu-id="a9efb-199">从 env ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="a9efb-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="a9efb-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="a9efb-200">tokenPattern</span></span>

<span data-ttu-id="a9efb-201">`tokenPattern`: String，默认值为 `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="a9efb-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="a9efb-202">`Expand`行为的生成器搜索令牌如下所示的原始 XML `${token}`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="a9efb-203">搜索通过默认正则表达式`@"\$\{(\w+)\}"`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="a9efb-204">匹配字符的字符集`\w`比 XML 和许多配置源允许更为严格。</span><span class="sxs-lookup"><span data-stu-id="a9efb-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="a9efb-205">使用`tokenPattern`的详细信息时比字符`@"\$\{(\w+)\}"`所需的标记名称中。</span><span class="sxs-lookup"><span data-stu-id="a9efb-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="a9efb-206">`tokenPattern`： 字符串：</span><span class="sxs-lookup"><span data-stu-id="a9efb-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="a9efb-207">允许开发人员可以更改用于令牌匹配正则表达式。</span><span class="sxs-lookup"><span data-stu-id="a9efb-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="a9efb-208">会不执行任何验证，以确保它是格式良好、 非危险的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="a9efb-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="a9efb-209">它必须包含一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="a9efb-209">It must contain a capture group.</span></span> <span data-ttu-id="a9efb-210">整个正则表达式必须匹配整个标记。</span><span class="sxs-lookup"><span data-stu-id="a9efb-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="a9efb-211">第一次捕获必须是要在配置源中查找的令牌名称。</span><span class="sxs-lookup"><span data-stu-id="a9efb-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="a9efb-212">配置生成器中 Microsoft.Configuration.ConfigurationBuilders</span><span class="sxs-lookup"><span data-stu-id="a9efb-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="a9efb-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="a9efb-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="a9efb-214">[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span><span class="sxs-lookup"><span data-stu-id="a9efb-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="a9efb-215">是最简单的配置生成器。</span><span class="sxs-lookup"><span data-stu-id="a9efb-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="a9efb-216">从环境中读取值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-216">Reads values from the environment.</span></span>
* <span data-ttu-id="a9efb-217">不具有任何其他配置选项。</span><span class="sxs-lookup"><span data-stu-id="a9efb-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="a9efb-218">`name`是任意的属性值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="a9efb-219">**注意：** 在 Windows 容器环境中，在运行时设置的变量仅注入到入口点进程环境。</span><span class="sxs-lookup"><span data-stu-id="a9efb-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="a9efb-220">作为服务运行的应用或这些变量除非否则注入通过容器中的一种机制，否则不能识别非入口点过程。</span><span class="sxs-lookup"><span data-stu-id="a9efb-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="a9efb-221">有关[IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-基于容器的当前版本[ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41)会处理此中*DefaultAppPool*仅。</span><span class="sxs-lookup"><span data-stu-id="a9efb-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="a9efb-222">其他基于 Windows 的容器变体可能需要开发自己的非入口点进程的注入机制。</span><span class="sxs-lookup"><span data-stu-id="a9efb-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="a9efb-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="a9efb-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="a9efb-224">永远不会存储密码、 敏感的连接字符串或在源代码中的其他敏感数据。</span><span class="sxs-lookup"><span data-stu-id="a9efb-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="a9efb-225">不应使用生产机密进行开发或测试。</span><span class="sxs-lookup"><span data-stu-id="a9efb-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="a9efb-226">此配置生成器提供了一个功能类似于[ASP.NET Core 机密管理器](/aspnet/core/security/app-secrets)。</span><span class="sxs-lookup"><span data-stu-id="a9efb-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="a9efb-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可在.NET Framework 项目中，但必须指定机密文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="a9efb-228">或者，可以定义`UserSecretsId`属性在项目文件，并创建正确的位置进行读取的原始机密文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="a9efb-229">若要保留从你的项目的外部依赖关系，密钥文件是 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="a9efb-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="a9efb-230">XML 格式设置是实现详细信息，和格式不应依赖。</span><span class="sxs-lookup"><span data-stu-id="a9efb-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="a9efb-231">如果您需要共享*secrets.json*使用.NET Core 项目文件，请考虑使用[SimpleJsonConfigBuilder](#simplejsonconfig)。</span><span class="sxs-lookup"><span data-stu-id="a9efb-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfig).</span></span> <span data-ttu-id="a9efb-232">`SimpleJsonConfigBuilder`设置格式的.NET Core 还应考虑可能发生变更的实现细节。</span><span class="sxs-lookup"><span data-stu-id="a9efb-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="a9efb-233">配置属性`UserSecretsConfigBuilder`:</span><span class="sxs-lookup"><span data-stu-id="a9efb-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="a9efb-234">`userSecretsId` -这是用于确定 XML 机密文件的首选的方法。</span><span class="sxs-lookup"><span data-stu-id="a9efb-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="a9efb-235">其工作原理类似于.NET Core，使用`UserSecretsId`项目属性来存储此标识符。</span><span class="sxs-lookup"><span data-stu-id="a9efb-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="a9efb-236">字符串必须是唯一的它不需要是一个 GUID。</span><span class="sxs-lookup"><span data-stu-id="a9efb-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="a9efb-237">使用此属性，`UserSecretsConfigBuilder`查找已知的本地位置 (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) 属于此标识符的机密文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="a9efb-238">`userSecretsFile` -指定包含机密的文件一个可选属性。</span><span class="sxs-lookup"><span data-stu-id="a9efb-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="a9efb-239">`~`可以在开始使用字符引用应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="a9efb-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="a9efb-240">此特性或`userSecretsId`特性是必需的。</span><span class="sxs-lookup"><span data-stu-id="a9efb-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="a9efb-241">如果同时指定两者，`userSecretsFile`优先。</span><span class="sxs-lookup"><span data-stu-id="a9efb-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="a9efb-242">`optional`： 布尔值，默认值`true`-可防止引发异常，如果找不到机密文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="a9efb-243">`name`是任意的属性值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="a9efb-244">机密文件的格式如下：</span><span class="sxs-lookup"><span data-stu-id="a9efb-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="a9efb-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="a9efb-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="a9efb-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)读取存储中的值[Azure 密钥保管库](/azure/key-vault/key-vault-whatis)。</span><span class="sxs-lookup"><span data-stu-id="a9efb-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="a9efb-247">`vaultName` 是所需 （保管库的名称），或者在保管库的 URI。</span><span class="sxs-lookup"><span data-stu-id="a9efb-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="a9efb-248">其他属性允许控制有关要连接到的保管库，但如果未在使用的环境中运行应用程序，则只需要有`Microsoft.Azure.Services.AppAuthentication`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="a9efb-249">Azure 服务身份验证库用于执行环境中的连接信息在可能的情况自动提取。</span><span class="sxs-lookup"><span data-stu-id="a9efb-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="a9efb-250">您可以自动覆盖连接字符串，从而选取的连接信息。</span><span class="sxs-lookup"><span data-stu-id="a9efb-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="a9efb-251">`vaultName` -需要`uri`中未提供。</span><span class="sxs-lookup"><span data-stu-id="a9efb-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="a9efb-252">要从其中读取键/值对在 Azure 订阅中指定的保管库的名称。</span><span class="sxs-lookup"><span data-stu-id="a9efb-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="a9efb-253">`connectionString` -的连接字符串可供[AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)</span><span class="sxs-lookup"><span data-stu-id="a9efb-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="a9efb-254">`uri` -连接到具有指定其他 Key Vault 提供程序`uri`值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="a9efb-255">如果未指定，Azure (`vaultName`) 是保管库提供程序。</span><span class="sxs-lookup"><span data-stu-id="a9efb-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="a9efb-256">`version` -Azure 密钥保管库的机密提供版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="a9efb-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="a9efb-257">如果`version`生成器仅检索匹配此版本的机密的指定。</span><span class="sxs-lookup"><span data-stu-id="a9efb-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="a9efb-258">`preloadSecretNames` -默认情况下，此生成器 querys**所有**密钥在密钥保管库的名称，初始化时。</span><span class="sxs-lookup"><span data-stu-id="a9efb-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="a9efb-259">若要防止读取所有密钥值，请将此属性设置为`false`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="a9efb-260">此值设置为`false`一次读取一个机密。</span><span class="sxs-lookup"><span data-stu-id="a9efb-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="a9efb-261">正在读取一次一个地很有用的如果保管库允许"Get"访问权限但不是"List"访问的机密。</span><span class="sxs-lookup"><span data-stu-id="a9efb-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="a9efb-262">**注意：** 使用时`Greedy`模式下，`preloadSecretNames`必须是`true`（默认值。）</span><span class="sxs-lookup"><span data-stu-id="a9efb-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="a9efb-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="a9efb-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="a9efb-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)是使用作为值的源目录的文件的基本配置生成器。</span><span class="sxs-lookup"><span data-stu-id="a9efb-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="a9efb-265">文件的名称是键，并且其内容是值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="a9efb-266">已安排的容器环境中运行时，此配置生成器可以很有用。</span><span class="sxs-lookup"><span data-stu-id="a9efb-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="a9efb-267">系统，例如 Docker Swarm 和 Kubernetes 提供`secrets`到此密钥每个文件的方式在其已安排的 windows 容器。</span><span class="sxs-lookup"><span data-stu-id="a9efb-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="a9efb-268">属性的详细信息：</span><span class="sxs-lookup"><span data-stu-id="a9efb-268">Attribute details:</span></span>

* <span data-ttu-id="a9efb-269">`directoryPath` - 必需。</span><span class="sxs-lookup"><span data-stu-id="a9efb-269">`directoryPath` - Required.</span></span> <span data-ttu-id="a9efb-270">指定的路径查找的值。</span><span class="sxs-lookup"><span data-stu-id="a9efb-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="a9efb-271">适用于 Windows 机密存储中的 docker *C:\ProgramData\Docker\secrets*目录默认情况下。</span><span class="sxs-lookup"><span data-stu-id="a9efb-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="a9efb-272">`ignorePrefix` 的排除文件，以此前缀开头。</span><span class="sxs-lookup"><span data-stu-id="a9efb-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="a9efb-273">默认值为"ignore。"。</span><span class="sxs-lookup"><span data-stu-id="a9efb-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="a9efb-274">`keyDelimiter` 默认值是`null`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="a9efb-275">如果指定，配置生成器将遍历多个级别的目录中，建立使用该分隔符的键名。</span><span class="sxs-lookup"><span data-stu-id="a9efb-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="a9efb-276">如果此值为`null`，配置生成器仅查找目录的最高级别。</span><span class="sxs-lookup"><span data-stu-id="a9efb-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="a9efb-277">`optional` 默认值是`false`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="a9efb-278">指定是否源目录不存在配置生成器是否应导致错误。</span><span class="sxs-lookup"><span data-stu-id="a9efb-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="a9efb-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="a9efb-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="a9efb-280">永远不会存储密码、 敏感的连接字符串或在源代码中的其他敏感数据。</span><span class="sxs-lookup"><span data-stu-id="a9efb-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="a9efb-281">不应使用生产机密进行开发或测试。</span><span class="sxs-lookup"><span data-stu-id="a9efb-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="a9efb-282">.NET core 项目经常使用 JSON 文件进行配置。</span><span class="sxs-lookup"><span data-stu-id="a9efb-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="a9efb-283">[SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/)生成器，允许.NET Framework 中使用的.NET Core JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="a9efb-284">此配置生成器是提供源的数据平面的键/值映射到特定的键/值区域的.NET Framework 配置基本。</span><span class="sxs-lookup"><span data-stu-id="a9efb-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="a9efb-285">此配置 builder**不**层次结构配置为提供。</span><span class="sxs-lookup"><span data-stu-id="a9efb-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="a9efb-286">JSON 后备文件是类似于字典的路由值不是复杂的层次结构对象。</span><span class="sxs-lookup"><span data-stu-id="a9efb-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="a9efb-287">可以使用多级别的分层文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="a9efb-288">此提供程序`flatten`s 通过追加在每个级别使用的属性名称的深度`:`作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="a9efb-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="a9efb-289">属性的详细信息：</span><span class="sxs-lookup"><span data-stu-id="a9efb-289">Attribute details:</span></span>

* <span data-ttu-id="a9efb-290">`jsonFile` - 必需。</span><span class="sxs-lookup"><span data-stu-id="a9efb-290">`jsonFile` - Required.</span></span> <span data-ttu-id="a9efb-291">指定要读取从 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="a9efb-292">`~`可以在开始使用字符引用应用程序根。</span><span class="sxs-lookup"><span data-stu-id="a9efb-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="a9efb-293">`optional` -布尔值，默认值是`true`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="a9efb-294">可防止引发异常，如果找不到 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="a9efb-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="a9efb-295">`jsonMode` - `[Flat|Sectional]`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="a9efb-296">默认为 `Flat`。</span><span class="sxs-lookup"><span data-stu-id="a9efb-296">`Flat` is the default.</span></span> <span data-ttu-id="a9efb-297">当`jsonMode`是`Flat`，JSON 文件是一个平面键/值源。</span><span class="sxs-lookup"><span data-stu-id="a9efb-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="a9efb-298">`EnvironmentConfigBuilder`和`AzureKeyVaultConfigBuilder`也是一个平面键/值源。</span><span class="sxs-lookup"><span data-stu-id="a9efb-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="a9efb-299">当`SimpleJsonConfigBuilder`中配置`Sectional`模式：</span><span class="sxs-lookup"><span data-stu-id="a9efb-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="a9efb-300">从概念上讲，为多个字典只是在最高级别对 JSON 文件被划分。</span><span class="sxs-lookup"><span data-stu-id="a9efb-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="a9efb-301">每个字典仅应用于附加到它们的顶级属性名称匹配的配置节。</span><span class="sxs-lookup"><span data-stu-id="a9efb-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="a9efb-302">例如：</span><span class="sxs-lookup"><span data-stu-id="a9efb-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="a9efb-303">实现自定义的键/值配置生成器</span><span class="sxs-lookup"><span data-stu-id="a9efb-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="a9efb-304">如果配置生成器不能满足您的需要，可以编写一个自定义。</span><span class="sxs-lookup"><span data-stu-id="a9efb-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="a9efb-305">`KeyValueConfigBuilder`基类处理替换模式和大多数前缀关注点。</span><span class="sxs-lookup"><span data-stu-id="a9efb-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="a9efb-306">只需实现项目：</span><span class="sxs-lookup"><span data-stu-id="a9efb-306">An implementing project need only:</span></span>

* <span data-ttu-id="a9efb-307">从基类继承并实现通过的键/值对的基本源`GetValue`和`GetAllValues`:</span><span class="sxs-lookup"><span data-stu-id="a9efb-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="a9efb-308">添加[Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)到项目。</span><span class="sxs-lookup"><span data-stu-id="a9efb-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="a9efb-309">`KeyValueConfigBuilder`基类提供了很多的工作和一致的行为在键/值之间配置生成器。</span><span class="sxs-lookup"><span data-stu-id="a9efb-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9efb-310">其他资源</span><span class="sxs-lookup"><span data-stu-id="a9efb-310">Additional resources</span></span>

* [<span data-ttu-id="a9efb-311">配置生成器 GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="a9efb-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="a9efb-312">对 Azure 密钥保管库中使用.NET 进行服务到服务身份验证</span><span class="sxs-lookup"><span data-stu-id="a9efb-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
