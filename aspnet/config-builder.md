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
# <a name="configuration-builders-for-aspnet"></a>ASP.NET 的配置生成器

通过[Stephen Molloy](https://github.com/StephenMolloy)和[Rick Anderson](https://twitter.com/RickAndMSFT)

配置生成器提供用于 ASP.NET 应用，以配置值从外部源的现代和敏捷机制。

配置生成器：

* 是可在.NET Framework 4.7.1 和更高版本。
* 提供用于读取配置值的灵活机制。
* 解决它们移动到容器并云环境已设定焦点的情况下，一些应用程序的基本需求。
* 可用来提高通过来自以前不可用的源的配置数据 （例如，Azure 密钥保管库和环境变量） 的保护.NET 配置系统中。

## <a name="keyvalue-configuration-builders"></a>键/值配置生成器

配置生成器可以处理的常见方案是提供用于配置各节的键/值模式的基本的键/值替代机制。 ConfigurationBuilders 的.NET Framework 概念不局限于特定的配置节或模式。 但是，在配置生成器的许多`Microsoft.Configuration.ConfigurationBuilders`([github](https://github.com/aspnet/MicrosoftConfigurationBuilders)， [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) 中的键/值模式工作。

## <a name="keyvalue-configuration-builders-settings"></a>键/值配置生成器设置

以下设置适用于所有键/值配置生成器中`Microsoft.Configuration.ConfigurationBuilders`。

### <a name="mode"></a>模式

配置生成器使用外部源的键/值信息来填充所选的键/值元素的配置系统。 具体而言，`<appSettings/>`和`<connectionStrings/>`部分配置生成器从得到特殊处理。 构建者在三种模式下工作：

* `Strict` 默认模式。 在此模式下，配置生成器只对进行操作的已知键/值为中心的配置节。 `Strict` 模式枚举的部分中的每个密钥。 如果在外部源中找到匹配项：

   * 配置生成器将从外部源的值替换为生成的配置节中的值。
* `Greedy` -与密切相关此模式下`Strict`模式。 而不是被限制为原始配置中已存在的密钥：

  * 配置生成器将所有键/值对从外部源都添加到生成的配置节。

* `Expand` -对进行操作的原始 XML 之前被分析为的配置节对象。 它可以认为的令牌字符串中的扩展。 与模式匹配的原始 XML 字符串的任何部分`${token}`是标记扩展的候选项。 如果没有相应的值在外部源中找到，则不会更改该令牌。 在此模式下构建者并不局限于`<appSettings/>`和`<connectionStrings/>`部分。

中的以下标记*web.config*使[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)中`Strict`模式：

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

下面的代码读取`<appSettings/>`并`<connectionStrings/>`前面所示*web.config*文件：

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

前面的代码将设置属性值为：

* 中的值*web.config*文件如果密钥未设置环境变量中。
* 值的环境变量，如果设置。

例如，`ServiceID`将包含：

* "从 web.config 的 ServiceID value"，如果环境变量`ServiceID`未设置。
* 值`ServiceID`环境变量，如果设置。

下图显示`<appSettings/>`键/值从上述*web.config*文件设置环境编辑器中的文件：

![环境编辑器](config-builder/static/env.png)

注意： 你可能需要退出并重新启动 Visual Studio 以查看环境变量中的更改。

### <a name="prefix-handling"></a>前缀处理

键前缀可以简化设置密钥，因为：

* .NET Framework 配置非常复杂且嵌套。
* 外部键/值源通常是基本和平面的性质。 例如，不嵌套环境变量。

使用任何以下方法来同时注入`<appSettings/>`和`<connectionStrings/>`到通过环境变量配置：

* 与`EnvironmentConfigBuilder`在默认`Strict`模式和配置文件中相应的密钥名称。 前面的代码和标记，采用此方法。 使用这种方法，你可以**不**具有相同命名的密钥在这种`<appSettings/>`和`<connectionStrings/>`。
* 使用两个`EnvironmentConfigBuilder`中的 s`Greedy`具有不同前缀的模式和`stripPrefix`。 使用此方法，该应用可以读取`<appSettings/>`和`<connectionStrings/>`而无需更新配置文件。 下一节[stripPrefix](#stripprefix)，演示如何执行此操作。
* 使用两个`EnvironmentConfigBuilder`中的 s`Greedy`模式具有不同的前缀。 使用此方法不能将重复的键名称，作为密钥名称必须不同的前缀。  例如：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

与前面的标记，可以使用同一平面的键/值源来填充两个不同部分的配置。

下图显示`<appSettings/>`并`<connectionStrings/>`键/值从上述*web.config*文件设置环境编辑器中的文件：

![环境编辑器](config-builder/static/prefix.png)

下面的代码读取`<appSettings/>`并`<connectionStrings/>`键/值包含在前面*web.config*文件：

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

前面的代码将设置属性值为：

* 中的值*web.config*文件如果密钥未设置环境变量中。
* 值的环境变量，如果设置。

例如，使用以前*web.config*文件中，设置键/值在上一环境编辑器映像，和前面的代码中，以下值：

|  键              | “值” |
| ----------------- | ------------ |
|     AppSetting_ServiceID           | 从 env 变量 AppSetting_ServiceID|
|    AppSetting_default            | 从 env AppSetting_default 值 |
|       ConnStr_default         | 从 env ConnStr_default val|

### <a name="stripprefix"></a>stripPrefix

`stripPrefix`： 一个布尔值，默认为`false`。 

前面的 XML 标记分隔应用程序设置从连接字符串，但要求中的所有键*web.config*文件以使用指定的前缀。 例如，前缀`AppSetting`必须添加到`ServiceID`密钥 ("AppSetting_ServiceID")。 与`stripPrefix`，在不使用的前缀*web.config*文件。 前缀必须有配置生成器源 （例如，在环境中。）我们预计大多数开发人员将使用`stripPrefix`。

应用程序通常剥离前缀。 以下*web.config*去除前缀：

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

在前面*web.config*文件中，`default`密钥是在这种`<appSettings/>`和`<connectionStrings/>`。

下图显示`<appSettings/>`并`<connectionStrings/>`键/值从上述*web.config*文件设置环境编辑器中的文件：

![环境编辑器](config-builder/static/prefix.png)

下面的代码读取`<appSettings/>`并`<connectionStrings/>`键/值包含在前面*web.config*文件：

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

前面的代码将设置属性值为：

* 中的值*web.config*文件如果密钥未设置环境变量中。
* 值的环境变量，如果设置。

例如，使用以前*web.config*文件中，设置键/值在上一环境编辑器映像，和前面的代码中，以下值：

|  键              | “值” |
| ----------------- | ------------ |
|     ServiceID           | 从 env 变量 AppSetting_ServiceID|
|    default            | 从 env AppSetting_default 值 |
|    default         | 从 env ConnStr_default val|

### <a name="tokenpattern"></a>tokenPattern

`tokenPattern`: String，默认值为 `@"\$\{(\w+)\}"`

`Expand`行为的生成器搜索令牌如下所示的原始 XML `${token}`。 搜索通过默认正则表达式`@"\$\{(\w+)\}"`。 匹配字符的字符集`\w`比 XML 和许多配置源允许更为严格。 使用`tokenPattern`的详细信息时比字符`@"\$\{(\w+)\}"`所需的标记名称中。

`tokenPattern`： 字符串：

* 允许开发人员可以更改用于令牌匹配正则表达式。
* 会不执行任何验证，以确保它是格式良好、 非危险的正则表达式。
* 它必须包含一个捕获组。 整个正则表达式必须匹配整个标记。 第一次捕获必须是要在配置源中查找的令牌名称。

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a>配置生成器中 Microsoft.Configuration.ConfigurationBuilders

### <a name="environmentconfigbuilder"></a>EnvironmentConfigBuilder

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):

* 是最简单的配置生成器。
* 从环境中读取值。
* 不具有任何其他配置选项。
* `name`是任意的属性值。

**注意：** 在 Windows 容器环境中，在运行时设置的变量仅注入到入口点进程环境。 作为服务运行的应用或这些变量除非否则注入通过容器中的一种机制，否则不能识别非入口点过程。 有关[IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-基于容器的当前版本[ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41)会处理此中*DefaultAppPool*仅。 其他基于 Windows 的容器变体可能需要开发自己的非入口点进程的注入机制。

### <a name="usersecretsconfigbuilder"></a>UserSecretsConfigBuilder

> [!WARNING]
> 永远不会存储密码、 敏感的连接字符串或在源代码中的其他敏感数据。 不应使用生产机密进行开发或测试。

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

此配置生成器提供了一个功能类似于[ASP.NET Core 机密管理器](/aspnet/core/security/app-secrets)。

[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可在.NET Framework 项目中，但必须指定机密文件。 或者，可以定义`UserSecretsId`属性在项目文件，并创建正确的位置进行读取的原始机密文件。 若要保留从你的项目的外部依赖关系，密钥文件是 XML 格式。 XML 格式设置是实现详细信息，和格式不应依赖。 如果您需要共享*secrets.json*使用.NET Core 项目文件，请考虑使用[SimpleJsonConfigBuilder](#simplejsonconfig)。 `SimpleJsonConfigBuilder`设置格式的.NET Core 还应考虑可能发生变更的实现细节。

配置属性`UserSecretsConfigBuilder`:

* `userSecretsId` -这是用于确定 XML 机密文件的首选的方法。 其工作原理类似于.NET Core，使用`UserSecretsId`项目属性来存储此标识符。 字符串必须是唯一的它不需要是一个 GUID。 使用此属性，`UserSecretsConfigBuilder`查找已知的本地位置 (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) 属于此标识符的机密文件。
* `userSecretsFile` -指定包含机密的文件一个可选属性。 `~`可以在开始使用字符引用应用程序根目录。 此特性或`userSecretsId`特性是必需的。 如果同时指定两者，`userSecretsFile`优先。
* `optional`： 布尔值，默认值`true`-可防止引发异常，如果找不到机密文件。 
* `name`是任意的属性值。

机密文件的格式如下：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a>AzureKeyVaultConfigBuilder

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

[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)读取存储中的值[Azure 密钥保管库](/azure/key-vault/key-vault-whatis)。

`vaultName` 是所需 （保管库的名称），或者在保管库的 URI。 其他属性允许控制有关要连接到的保管库，但如果未在使用的环境中运行应用程序，则只需要有`Microsoft.Azure.Services.AppAuthentication`。 Azure 服务身份验证库用于执行环境中的连接信息在可能的情况自动提取。 您可以自动覆盖连接字符串，从而选取的连接信息。

* `vaultName` -需要`uri`中未提供。 要从其中读取键/值对在 Azure 订阅中指定的保管库的名称。
* `connectionString` -的连接字符串可供[AzureServiceTokenProvider](https://docs.microsoft.com/en-us/azure/key-vault/service-to-service-authentication#connection-string-support)
* `uri` -连接到具有指定其他 Key Vault 提供程序`uri`值。 如果未指定，Azure (`vaultName`) 是保管库提供程序。
* `version` -Azure 密钥保管库的机密提供版本控制功能。 如果`version`生成器仅检索匹配此版本的机密的指定。
* `preloadSecretNames` -默认情况下，此生成器 querys**所有**密钥在密钥保管库的名称，初始化时。 若要防止读取所有密钥值，请将此属性设置为`false`。 此值设置为`false`一次读取一个机密。 正在读取一次一个地很有用的如果保管库允许"Get"访问权限但不是"List"访问的机密。 **注意：** 使用时`Greedy`模式下，`preloadSecretNames`必须是`true`（默认值。）

### <a name="keyperfileconfigbuilder"></a>KeyPerFileConfigBuilder

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

[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)是使用作为值的源目录的文件的基本配置生成器。 文件的名称是键，并且其内容是值。 已安排的容器环境中运行时，此配置生成器可以很有用。 系统，例如 Docker Swarm 和 Kubernetes 提供`secrets`到此密钥每个文件的方式在其已安排的 windows 容器。

属性的详细信息：

* `directoryPath` - 必需。 指定的路径查找的值。 适用于 Windows 机密存储中的 docker *C:\ProgramData\Docker\secrets*目录默认情况下。
* `ignorePrefix` 的排除文件，以此前缀开头。 默认值为"ignore。"。
* `keyDelimiter` 默认值是`null`。 如果指定，配置生成器将遍历多个级别的目录中，建立使用该分隔符的键名。 如果此值为`null`，配置生成器仅查找目录的最高级别。
* `optional` 默认值是`false`。 指定是否源目录不存在配置生成器是否应导致错误。

### <a name="simplejsonconfigbuilder"></a>SimpleJsonConfigBuilder

> [!WARNING]
> 永远不会存储密码、 敏感的连接字符串或在源代码中的其他敏感数据。 不应使用生产机密进行开发或测试。

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

.NET core 项目经常使用 JSON 文件进行配置。 [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/)生成器，允许.NET Framework 中使用的.NET Core JSON 文件。 此配置生成器是提供源的数据平面的键/值映射到特定的键/值区域的.NET Framework 配置基本。 此配置 builder**不**层次结构配置为提供。 JSON 后备文件是类似于字典的路由值不是复杂的层次结构对象。 可以使用多级别的分层文件。 此提供程序`flatten`s 通过追加在每个级别使用的属性名称的深度`:`作为分隔符。

属性的详细信息：

* `jsonFile` - 必需。 指定要读取从 JSON 文件。 `~`可以在开始使用字符引用应用程序根。
* `optional` -布尔值，默认值是`true`。 可防止引发异常，如果找不到 JSON 文件。
* `jsonMode` - `[Flat|Sectional]`。 默认为 `Flat`。 当`jsonMode`是`Flat`，JSON 文件是一个平面键/值源。 `EnvironmentConfigBuilder`和`AzureKeyVaultConfigBuilder`也是一个平面键/值源。 当`SimpleJsonConfigBuilder`中配置`Sectional`模式：

  * 从概念上讲，为多个字典只是在最高级别对 JSON 文件被划分。
  * 每个字典仅应用于附加到它们的顶级属性名称匹配的配置节。 例如：

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

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a>实现自定义的键/值配置生成器

如果配置生成器不能满足您的需要，可以编写一个自定义。 `KeyValueConfigBuilder`基类处理替换模式和大多数前缀关注点。 只需实现项目：

* 从基类继承并实现通过的键/值对的基本源`GetValue`和`GetAllValues`:
* 添加[Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)到项目。

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

`KeyValueConfigBuilder`基类提供了很多的工作和一致的行为在键/值之间配置生成器。

## <a name="additional-resources"></a>其他资源

* [配置生成器 GitHub 存储库](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [对 Azure 密钥保管库中使用.NET 进行服务到服务身份验证](/azure/key-vault/service-to-service-authentication#connection-string-support)
