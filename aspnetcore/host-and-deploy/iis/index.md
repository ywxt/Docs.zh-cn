---
title: "使用 IIS 在 Windows 上托管 ASP.NET Core"
author: guardrex
description: "了解如何在 Windows Server Internet Information Services (IIS) 上托管 ASP.NET Core 应用。"
ms.author: riande
manager: wpickett
ms.custom: mvc
ms.date: 03/13/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: host-and-deploy/iis/index
ms.openlocfilehash: 18c7448ad79891d04eca1e939a0aeeabe417bde8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="host-aspnet-core-on-windows-with-iis"></a>使用 IIS 在 Windows 上托管 ASP.NET Core

作者：[Luke Latham](https://github.com/guardrex) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)

## <a name="supported-operating-systems"></a>支持的操作系统

支持下列操作系统：

* Windows 7 和更新版本
* Windows Server 2008 R2 和 更新版本&#8224;

&#8224;在概念上，本文档描述的 IIS 配置也适用于在 Nano Server IIS 上托管 ASP.NET Core 应用，但有关具体说明，请参阅 [ASP.NET Core 与 Nano Server 上运行的 IIS](xref:tutorials/nano-server)。

[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）在使用 IIS 的反向代理配置中不起作用。 请使用 [Kestrel 服务器](xref:fundamentals/servers/kestrel)。

## <a name="iis-configuration"></a>IIS 配置

启用 Web 服务器 (IIS) 角色并建立角色服务。

### <a name="windows-desktop-operating-systems"></a>Windows 桌面操作系统

导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。 打开“Internet Information Services”组和“Web 管理工具”。 选中“IIS 管理控制台”框。 选中“万维网服务”框。 接受“万维网服务”的默认功能，或自定义 IIS 功能。

![在“Windows 功能”中选择了“IIS 管理控制台”和“万维网服务”。](index/_static/windows-features-win10.png)

### <a name="windows-server-operating-systems"></a>Windows Server 操作系统

对于服务器操作系统，通过“管理”菜单或“服务器管理器”中的链接使用“添加角色和功能”向导。 在“服务器角色”步骤中，选中“Web 服务器(IIS)”框。

![在选择服务器角色步骤中选择了“Web 服务器 IIS”角色。](index/_static/server-roles-ws2016.png)

在“角色服务”步骤中，选择所需 IIS 角色服务，或接受提供的默认角色服务。

![在选择角色服务步骤中选择了默认角色服务。](index/_static/role-services-ws2016.png)

继续执行“确认”步骤，安装 Web 服务器角色和服务。 安装 Web 服务器 (IIS) 角色后无需重启服务器/IIS。

## <a name="install-the-net-core-windows-server-hosting-bundle"></a>安装 .NET Core Windows Server 托管捆绑包

1. 在托管系统上安装 [.NET Core Windows Server 托管捆绑包](https://aka.ms/dotnetcore-2-windowshosting)。 捆绑包可安装 .NET Core 运行时、.NET Core 库和 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。 该模块创建 IIS 与 Kestrel 服务器之间的反向代理。 如果系统没有 Internet 连接，请先获取并安装 [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840)，再安装 .NET Core Windows Server 托管捆绑包。

2. 重启系统，或在命令提示符处依次执行 net stop was /y 和 net start w3svc，了解系统路径的更改。

> [!NOTE]
> 有关 IIS 共享配置的信息，请参阅[使用 IIS 共享配置的 ASP.NET Core 模块](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)。

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a>使用 Visual Studio 进行发布时安装 Web 部署

使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)将应用部署到服务器时，请在服务器上安装最新版本的 Web 部署。 要安装 Web 部署，请使用 [Web 平台安装程序 (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) 或直接从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=43717)获取安装程序。 建议使用 WebPI。 WebPI 为托管提供程序提供独立的安装程序和配置。

## <a name="application-configuration"></a>应用程序配置

### <a name="enabling-the-iisintegration-components"></a>启用 IISIntegration 组件

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x)

典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机。 `CreateDefaultBuilder` 将 [Kestrel](xref:fundamentals/servers/kestrel) 配置为 Web 服务器，并通过配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)的基路径和端口来实现 IIS 集成：

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x)

在应用依赖项中加入对 [Microsoft.AspNetCore.Server.IISIntegration ](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/)包的依赖项。 通过向 WebHostBuilder 添加 UseIISIntegration 扩展方法，将 IIS 集成中间件合并到应用中：

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

`UseKestrel` 和 `UseIISIntegration` 均为必需。 调用 `UseIISIntegration` 的代码不会影响代码可移植性。 如果应用不以 IIS 为背景运行（例如，应用直接在 Kestrel 上运行），则 `UseIISIntegration` 无操作。

---

有关托管的详细信息，请参阅 [ASP.NET Core 中的托管](xref:fundamentals/hosting)。

### <a name="iis-options"></a>IIS 选项

要配置 IIS 选项，请在 `ConfigureServices` 中包括 `IISOptions` 的服务配置：

```csharp
services.Configure<IISOptions>(options => 
{
    ...
});
```

| 选项                         | 默认 | 设置 |
| ------------------------------ | ------- | ------- |
| `AutomaticAuthentication`      | `true`  | 若为 `true`，身份验证中间件将设置 `HttpContext.User` 并响应一般质询。 若为 `false`，身份验证中间件仅提供标识 (`HttpContext.User`) 并在 `AuthenticationScheme` 显式请求时响应质询。 必须在 IIS 中启用 Windows 身份验证使 `AutomaticAuthentication` 得以运行。 |
| `AuthenticationDisplayName`    | `null`  | 设置在登录页上向用户显示的显示名。 |
| `ForwardClientCertificate`     | `true`  | 若为 `true`，且存在 `MS-ASPNETCORE-CLIENTCERT` 请求头，则填充 `HttpContext.Connection.ClientCertificate`。 |

### <a name="webconfig"></a>web.config

web.config 文件的主要用途是配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。 它可以提供其他 IIS 配置设置。 web.config 的创建、转换和发布 由 .NET Core Web SDK (`Microsoft.NET.Sdk.Web`) 处理。 SDK 设置在项目文件 `<Project Sdk="Microsoft.NET.Sdk.Web">` 的顶部。 要防止 SDK 转换 *web.config* 文件，请将 **\<IsTransformWebConfigDisabled>** 属性添加到项目文件，并将其设置为 `true`：

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

如果项目中有 web.config 文件，则会使用正确 processPath 和参数转换该文件，以便配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，并将该文件移动到[已发布的输出](xref:host-and-deploy/directory-structure)。 转换不会修改文件中的 IIS 配置设置。

### <a name="webconfig-location"></a>web.config 位置

.NET Core 应用通过 IIS 与 Kestrel 服务器之间的反向代理托管。 为了创建反向代理，web.config 文件必须存在于已部署应用的内容根路径（通常为应用基路径）中，该路径是向 IIS 提供的网站物理路径。 若要使用 Web 部署发布多个应用，应用的根路径中需要包含 web.config 文件。

敏感文件存在于应用的物理路径中，包括子文件夹，如 \<assembly_name>.runtimeconfig.json、\<assembly_name>.xml（XML 文档注释）和 \<assembly_name>.deps.json。 存在 web.config 文件并使用该文件配置站点时，IIS 会阻止提供这些敏感文件。 因此，切勿意外重命名 web.config 文件或将其从部署中删除，这一点非常重要。

## <a name="create-the-iis-website"></a>创建 IIS 网站

1. 在目标 IIS 系统上，创建一个文件夹，将应用的已发布文件夹和文件包含在其中，如 [目录结构](xref:host-and-deploy/directory-structure)中所述。

2. 在文件夹中创建一个“日志”文件夹，用于在启用 stdout 日志记录时保存 stdout 日志。 如果部署应用时有效负载中包含了“日志”文件夹，请跳过此步骤。 有关如何让 MSBuild 创建“日志”文件夹的说明，请参阅[目录结构](xref:host-and-deploy/directory-structure)主题。

3. 在 IIS 管理器中创建新网站。 提供网站名称，并将物理路径设置为应用的部署文件夹。 提供“绑定”配置并创建网站。

4. 将“应用程序池”设置为“无托管代码”。 ASP.NET Core 在单独的进程中运行，并管理运行时。

5. 打开“添加网站”窗口。

   ![选择“站点”上下文菜单中的“添加网站”。](index/_static/add-website-context-menu-ws2016.png)

6. 配置网站。

   ![在“添加网站”步骤中提供网站名称、物理路径和主机名。](index/_static/add-website-ws2016.png)

7. 在“应用程序池”面板中，右键单击网站的应用池，并从弹出菜单中选择“基本设置...”，打开“编辑应用程序池”窗口。

   ![从应用程序池的上下文菜单中选择“基本设置”。](index/_static/apppools-basic-settings-ws2016.png)

8. 将“.NET CLR 版本”设置为“无托管代码”。

   ![将“.NET CLR 版本”设置为“无托管代码”。](index/_static/edit-apppool-ws2016.png)
     
    请注意：将“.NET CLR 版本”设置为“无托管代码”是可选步骤。 ASP.NET Core 不依赖加载桌面 CLR。

9. 确认进程模型标识拥有适当的权限。

   如果将应用池的默认标识（“进程模型” > “标识”）从 ApplicationPoolIdentity 更改为另一标识，请验证新标识拥有所需的权限，可访问应用的文件夹、数据库和其他所需资源。
   
## <a name="deploy-the-app"></a>部署应用

将应用部署到在目标 IIS 系统上创建的文件夹。 建议使用的部署机制是 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)。

确认要部署的已发布应用未运行。 如果应用正在运行，publish 文件夹中的文件会被锁定。 无法覆盖已锁定的文件。 若要在部署中解除已锁定的文件，请停止应用池：

* 在服务器上的 IIS 管理器中进行手动操作。
* 使用 Web 部署并在项目文件中引用 `Microsoft.NET.Sdk.Web`。 系统会在 Web 应用目录的根目录中放置一个 app_offline.htm 文件。 该文件存在时，ASP.NET Core 模块会在部署过程中正常关闭该应用并提供 app_offline.htm 文件。 有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#appofflinehtm)。
* 使用 PowerShell 来停止和重新启动应用池（需要使用 PowerShell 5 或更高版本）：
  ```PowerShell
  $webAppPoolName = 'APP_POOL_NAME'

  # Stop the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
      Stop-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Stopped') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Stopped
  }

  # Provide script commands here to deploy the app

  # Restart the AppPool
  if((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
      Start-WebAppPool -Name $webAppPoolName
      while((Get-WebAppPoolState $webAppPoolName).Value -ne 'Started') {
          Start-Sleep -s 1
      }
      Write-Host `-AppPool Started
  }
  ```

### <a name="web-deploy-with-visual-studio"></a>在 Visual Studio 内使用 Web 部署

要了解如何创建用于 Web 部署的发布配置文件，请参阅[用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles)。 如果托管提供程序提供了发布配置文件或支持创建发布配置文件，请下载配置文件并使用 Visual Studio 的“发布”对话框进行导入。

![“发布”对话框页](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a>在 Visual Studio 之外使用 Web 部署

也可以在 Visual Studio 之外从命令行使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)。 有关详细信息，请参阅 [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool)（Web 部署工具）。

### <a name="alternatives-to-web-deploy"></a>Web 部署的替代方法

有多种方法可以将应用移动到托管系统，例如 Xcopy、Robocopy 或 PowerShell，使用其中任何一种方法皆可。 Visual Studio 用户可以使用[发布示例](https://github.com/aspnet/vsweb-publish/blob/master/samples/samples.md)。

## <a name="browse-the-website"></a>浏览网站

![Microsoft Edge 浏览器已加载 IIS 启动页。](index/_static/browsewebsite.png)

## <a name="data-protection"></a>数据保护

数据保护由多个 ASP.NET 中间件使用，包括用于身份验证的中间件。 即使不从用户代码中调用数据保护 API，也应该使用部署脚本或在用户代码中配置数据保护，以创建持久的密钥存储。 如果不配置数据保护，则密钥存储在内存中。重启应用时，密钥会被丢弃。

如果 keyring 存储于内存中，则当应用重启时：

* 所有 Forms 身份验证令牌都无效。 
* 用户需要在下一次请求时再次登录。 
* 无法再解密使用 keyring 保护的任何数据。

要在 IIS 下配置数据保护，请使用以下方法之一：

### <a name="create-a-data-protection-registry-hive"></a>创建数据保护注册表配置单元

ASP.NET 应用使用的数据保护密钥存储在应用外部的注册表配置单元中。 要持久保存给定应用的密钥，需为应用池创建注册表配置单元。

对于独立的非 Web 场 IIS 安装，可以对用于 ASP.NET Core 应用的每个应用池使用[数据保护 Provision-AutoGenKeys.ps1 PowerShell 脚本](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1)。 此脚本在仅对工作进程帐户实现 ACL 的 HKLM 注册表中创建特殊的注册表项。 通过计算机范围的密钥使用 DPAPI 对密钥静态加密。

在 Web 场方案中，可以将应用配置为使用 UNC 路径存储其数据保护密钥环。 默认情况下，数据保护密钥未加密。 确保这种共享的文件权限仅限于运行应用所用的 Windows 帐户。 此外，可使用 X509 证书保护静态密钥。 建议使用允许用户上传证书的机制：将证书放置在用户信任的证书存储中，并确保在运行用户应用的所有计算机上都可使用这些证书。 有关详细信息，请参阅[配置数据保护](xref:security/data-protection/configuration/overview)。

### <a name="configure-the-iis-application-pool-to-load-the-user-profile"></a>配置 IIS 应用程序池以加载用户配置文件

此设置位于应用池“高级设置”下的“进程模型”部分。 将“加载用户配置文件”设置为 `True`。 这会将密钥存储在用户配置文件目录下，并使用 DPAPI 和特定于用户帐户（用于应用池）的密钥的进行保护。

### <a name="use-the-file-system-as-a-key-ring-store"></a>将文件系统用作密钥环存储

调整应用代码，[将文件系统用作密钥环存储](xref:security/data-protection/configuration/overview)。 使用 X509 证书保护 keyring，并确保该证书是受信任的证书。 如果它是自签名证书，则将该证书放置于受信任的根存储中。

当在 Web 场中使用 IIS 时：

* 使用所有计算机都可以访问的文件共享。
* 将 X509 证书部署到每台计算机。 [通过代码配置数据保护](xref:security/data-protection/configuration/overview)。

### <a name="set-a-machine-wide-policy-for-data-protection"></a>设置用于数据保护的计算机范围的策略

数据保护系统对以下操作提供有限支持：为使用数据保护 API 的所有应用设置默认[计算机范围的策略](xref:security/data-protection/configuration/machine-wide-policy)。 有关详细信息，请参阅[数据保护](xref:security/data-protection/index)文档。

## <a name="configuration-of-sub-applications"></a>配置子应用程序

在根应用下添加的子应用不应将 ASP.NET Core 模块作为处理程序包含在其中。 如果在子应用的 web.config 文件中将该模块添加为处理程序，则尝试浏览子应用时会收到 500.19（内部服务器错误），即引用错误的配置文件。 以下示例显示 ASP.NET Core 子应用的已发布 web.config 文件的内容：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

在 ASP.NET Core 应用下托管非 ASP.NET Core 子应用时，需在子应用的 web.config 文件中显式删除继承的处理程序：

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <remove name="aspNetCore"/>
    </handlers>
    <aspNetCore processPath="dotnet" 
      arguments=".\<assembly_name>.dll" 
      stdoutLogEnabled="false" 
      stdoutLogFile=".\logs\stdout" />
  </system.webServer>
</configuration>
```

有关配置 ASP.NET Core 模块的详细信息，请参阅 [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)和 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。

## <a name="configuration-of-iis-with-webconfig"></a>使用 web.config 配置 IIS

对于那些应用于反向代理配置的 IIS 功能，IIS 配置受 web.config 的 \<system.webServer> 部分影响。 如果用户在系统级别将 IIS 配置为使用动态压缩，可通过应用的 web.config 文件中的 \<urlCompression> 元素为应用禁用该设置。 有关详细信息，请参阅 [\<system.webServer> 的配置参考](https://docs.microsoft.com/iis/configuration/system.webServer/)、[ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)和 [配合使用 IIS 模块与 ASP.NET Core](xref:host-and-deploy/iis/modules)。 如果需要为在独立应用池中运行的单个应用设置环境变量（IIS 10.0+ 中支持此操作），请参阅 IIS 参考文档的[环境变量 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主题中的“AppCmd.exe 命令”部分。

## <a name="configuration-sections-of-webconfig"></a>web.config 的配置节

ASP.NET Core 应用不会使用 web.config 中的 ASP.NET Framework 应用的配置部分进行配置：

* **\<system.web>**
* \<appSettings>
* \<connectionStrings>
* \<location>

会使用其他的配置提供程序配置 ASP.NET Core 应用。 有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。

## <a name="application-pools"></a>应用程序池

在单个系统上托管多个网站时，需在每个应用自己的应用池中运行各应用，以隔离各应用。 IIS“添加网站”对话框默认执行此配置。 提供了站点名称时，该文本会自动传输到“应用程序池”文本框。 添加网站时，会使用该站点名称创建新的应用池。

## <a name="application-pool-identity"></a>应用程序池标识

通过应用池标识帐户，可以在唯一帐户下运行应用，而无需创建和管理域或本地帐户。 在 IIS 8.0+ 上，IIS 管理员工作进程 (WAS) 使用新应用池的名称创建一个虚拟帐户，并默认在此帐户下运行应用池的工作进程。 在 IIS 管理控制台中，确保应用池“高级设置”下的“标识”设置为使用 ApplicationPoolIdentity：

![应用程序池“高级设置”对话框](index/_static/apppool-identity.png)

IIS 管理进程使用 Windows 安全系统中应用池的名称创建安全标识符。 可使用此标识保护资源；但此标识不是真实的用户帐户，不会在 Windows 用户管理控制台中显示。

如果 IIS 工作进程需要对应用的高级访问权限，请为包含该应用的目录修改访问控制列表 (ACL)：

1. 打开 Windows 资源管理器并导航到目录。

2. 右键单击该目录，然后选择“属性”。

3. 在“安全”选项卡下，选择“编辑”按钮，然后单击“添加”按钮。

4. 选择“位置”按钮，并确保该系统处于选中状态。

5. 在“输入要选择的对象名称”文本框中输入“IIS AppPool\DefaultAppPool”。

   ![选择应用文件夹的用户或组对话框](index/_static/select-users-or-groups-1.png)

6. 选择“检查名称”按钮。 选择“确定”。

   ![选择应用文件夹的用户或组对话框](index/_static/select-users-or-groups-2.png)

也可使用 ICACLS 工具通过命令提示符完成此操作：

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

## <a name="additional-resources"></a>其他资源

* [对 IIS 上的 ASP.NET Core 进行故障排除](xref:host-and-deploy/iis/troubleshoot)
* [Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考](xref:host-and-deploy/azure-iis-errors-reference)
* [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)
* [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)
* [配合使用 IIS 模块与 ASP.NET Core](xref:host-and-deploy/iis/modules)
* [ASP.NET Core 简介](../index.md)
* [Microsoft IIS 官方网站](https://www.iis.net/)
* [Microsoft TechNet 库：Windows Server](https://docs.microsoft.com/windows-server/windows-server-versions)
