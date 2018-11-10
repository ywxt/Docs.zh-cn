---
title: 在 Windows 服务中托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 10/30/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 11913019bfe5d06c259b806fce9cc580a8280ad5
ms.sourcegitcommit: fc2486ddbeb15ab4969168d99b3fe0fbe91e8661
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50758188"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>在 Windows 服务中托管 ASP.NET Core

作者：[Luke Latham](https://github.com/guardrex)、[Tom Dykstra](https://github.com/tdykstra)

不将 IIS 用作 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)时，可在 Windows 上托管 ASP.NET Core 应用。 作为 Windows 服务进行托管时，应用将在重新启动后自动启动。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="convert-a-project-into-a-windows-service"></a>将项目转换为 Windows 服务

要将现有 ASP.NET Core 项目设置为作为服务运行，至少需要执行以下更改：

1. 在项目文件中：

   * 确认是否存在 Windows [运行时标识符 (RID)](/dotnet/core/rid-catalog)，或将其添加到包含目标框架的 `<PropertyGroup>` 中：

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.2</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      要发布多个 RID：

      * 通过以分号分隔的列表提供 RID。
      * 使用属性名称 `<RuntimeIdentifiers>`（复数）。

      有关详细信息，请参阅 [.NET Core RID 目录](/dotnet/core/rid-catalog)。

   * 为 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices) 添加包引用。

1. 在 `Program.Main` 中，进行下列更改：

   * 调用 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)，而不是 `host.Run`。

   * 调用 [UseContentRoot](xref:fundamentals/host/web-host#content-root) 并使用应用的发布位置路径，而不是 `Directory.GetCurrentDirectory()`。

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,16)]

1. 使用 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish)、[Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles) 或 Visual Studio Code 发布应用。 使用 Visual Studio 时，先选择“FolderProfile”并配置“目标位置”，再选择“发布”按钮。

   要使用命令行接口 (CLI) 工具发布示例应用，请在项目文件夹的命令提示符处运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令。 必须在项目文件的 `<RuntimeIdenfifier>`（或 `<RuntimeIdentifiers>`）属性中指定 RID。 在下面的示例中，应用是通过 `win7-x64` 运行时的“发布”配置发布到在 c:\\svc 中创建的文件夹：

   ```console
   dotnet publish --configuration Release --runtime win7-x64 --output c:\svc
   ```

1. 运行 `net user` 命令，创建服务用户帐户：

   ```console
   net user {USER ACCOUNT} {PASSWORD} /add
   ```

   对于示例应用，使用用户名 `ServiceUser` 和密码创建用户帐户。 在下面的命令中，将 `{PASSWORD}` 替换为[强密码](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements)。

   ```console
   net user ServiceUser {PASSWORD} /add
   ```

   如果需要将用户添加到组中，请运行 `net localgroup` 命令（其中 `{GROUP}` 是组名称）：

   ```console
   net localgroup {GROUP} {USER ACCOUNT} /add
   ```

   有关详细信息，请参阅[服务用户帐户](/windows/desktop/services/service-user-accounts)。

1. 运行 [icacls](/windows-server/administration/windows-commands/icacls) 命令，授予对应用文件夹的写入/读取/执行权限：

   ```console
   icacls "{PATH}" /grant {USER ACCOUNT}:(OI)(CI){PERMISSION FLAGS} /t
   ```

   * `{PATH}` &ndash; 应用文件夹路径。
   * `{USER ACCOUNT}` &ndash; 用户帐户 (SID)。
   * `(OI)` &ndash; 对象继承标志将权限传播给从属文件。
   * `(CI)` &ndash; 容器继承标志将权限传播给从属文件夹。
   * `{PERMISSION FLAGS}` &ndash; 设置应用的访问权限。
     * 写入 (`W`)
     * 读取 (`R`)
     * 执行 (`X`)
     * 完全 (`F`)
     * 修改 (`M`)
   * `/t` &ndash; 以递归方式应用于现有从属文件夹和文件。

   对于发布到 c:\\sv 文件夹的示例应用，以及拥有写入/读取/执行权限的 `ServiceUser` 帐户，请运行以下命令：

   ```console
   icacls "c:\svc" /grant ServiceUser:(OI)(CI)WRX /t
   ```

   有关详细信息，请参阅 [icacls](/windows-server/administration/windows-commands/icacls)。

1. 使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具创建服务。 `binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。 每个参数和值的等于号和引号字符之间必须有空格。

   ```console
   sc create {SERVICE NAME} binPath= "{PATH}" obj= "{DOMAIN}\{USER ACCOUNT}" password= "{PASSWORD}"
   ```

   * `{SERVICE NAME}` &ndash; 要在[服务控制管理器](/windows/desktop/services/service-control-manager)中分配给服务的名称。
   * `{PATH}` &ndash; 可执行服务的路径。
   * `{DOMAIN}`（或为本地计算机名称，如果计算机不是域加入的话）；以及 `{USER ACCOUNT}` &ndash; 域（或为本地计算机名称）和运行服务所用的用户帐户。 请勿省略 `obj` 参数。 `obj` 的默认值为 [LocalSystem 帐户](/windows/desktop/services/localsystem-account)。 使用 `LocalSystem` 帐户运行服务会带来重大安全风险。 请始终使用在服务器上拥有有限权限的用户帐户运行服务。
   * `{PASSWORD}` &ndash; 用户帐户密码。

   如下示例中：

   * 服务名为 MyService。
   * 已发布的服务驻留在 c:\\svc 文件夹中。 应用可执行文件名为 AspNetCoreService.exe。 `binPath` 值是放在半角双引号 (") 中。
   * 服务是使用 `ServiceUser` 帐户运行。 将 `{DOMAIN}` 替换为用户帐户的域或本地计算机名称。 将 `obj` 值放在半角双引号 (") 中。 例如，如果托管系统是名为 `MairaPC` 的本地计算机，请将 `obj` 设置为 `"MairaPC\ServiceUser"`。
   * 将 `{PASSWORD}` 替换为用户帐户密码。 `password` 值是放在半角双引号 (") 中。

   ```console
   sc create MyService binPath= "c:\svc\aspnetcoreservice.exe" obj= "{DOMAIN}\ServiceUser" password= "{PASSWORD}"
   ```

   > [!IMPORTANT]
   > 请确保参数的等于号和参数值之间有空格。

1. 使用 `sc start {SERVICE NAME}` 命令启动服务。

   要启动示例应用服务，请使用以下命令：

   ```console
   sc start MyService
   ```

   此命令需要几秒钟才能启动服务。

1. 要检查服务的状态，请使用 `sc query {SERVICE NAME}` 命令。 状态报告为以下值之一：

   * `START_PENDING`
   * `RUNNING`
   * `STOP_PENDING`
   * `STOPPED`

   使用以下命令检查示例应用服务的状态：

   ```console
   sc query MyService
   ```

1. 当服务处于 `RUNNING` 状态并且服务是 Web 应用时，在应用所在路径中浏览应用（默认路径为 `http://localhost:5000`；在使用 [HTTPS 重定向中间件](xref:security/enforcing-ssl)时，它将重定向到 `https://localhost:5001`）。

   对于示例应用服务，请在 `http://localhost:5000` 浏览应用。

1. 使用 `sc stop {SERVICE NAME}` 命令停止服务。

   以下命令可停止示例应用服务：

   ```console
   sc stop MyService
   ```

1. 停止服务并经过短暂延迟后，使用 `sc delete {SERVICE NAME}` 命令卸载服务。

   检查示例应用服务的状态：

   ```console
   sc query MyService
   ```

   当示例应用服务处于 `STOPPED` 状态时，使用以下命令卸载示例应用服务：

   ```console
   sc delete MyService
   ```

## <a name="run-the-app-outside-of-a-service"></a>在服务之外运行应用

在服务之外运行时更便于进行测试和调试，因此通常仅在特定情况下添加调用 `RunAsService` 的代码。 例如，应用可以使用 `--console` 命令行参数或在已附加调试器时作为控制台应用运行：

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

由于 ASP.NET Core 配置需要命令行参数的名称/值对，因此将先删除 `--console` 开关，然后再将参数传递到 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)。

> [!NOTE]
> 不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。

## <a name="handle-stopping-and-starting-events"></a>处理停止和启动事件

要处理 [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting)、[OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 和 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 事件，请执行以下额外更改：

1. 创建从 [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice) 派生的类：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. 创建可将自定义 `WebHostService` 传递给 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run) 的 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 的扩展方法：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. 在 `Program.Main` 中，调用新扩展方法 `RunAsCustomService`，而不是 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=17)]

   > [!NOTE]
   > 不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。

如果自定义 `WebHostService` 代码需要来自依赖项注入（如记录器）的服务，请从 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 属性中获取：

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a>代理服务器和负载均衡器方案

与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。 有关更多信息，请参见<xref:host-and-deploy/proxy-load-balancer>。

## <a name="configure-https"></a>配置 HTTPS

若要为服务配置安全终结点，请执行以下操作：

1. 使用平台的证书获取和部署机制，为托管系统创建 X.509 证书。
1. 将 [Kestrel 服务器 HTTPS 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)指定为使用此证书。

不支持使用 ASP.NET Core HTTPS 开发证书保护服务终结点。

## <a name="current-directory-and-content-root"></a>当前目录和内容根

通过为 Windows 服务调用 `Directory.GetCurrentDirectory()` 返回的当前工作目录是 C:\\WINDOWS\\system32 文件夹。 system32 文件夹不是存储服务文件（如设置文件）的合适位置。 使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 时，通过以下某种方法使用 [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath) 维护和访问服务的资产和设置文件：

* 使用内容根路径。 `IHostingEnvironment.ContentRootPath` 是创建服务时提供给 `binPath` 参数的同一路径。 不要使用 `Directory.GetCurrentDirectory()` 创建设置文件的路径，而是使用内容根路径并在应用的内容根中维护文件。
* 将文件存储在磁盘中的合适位置。 使用 `SetBasePath` 指定到包含文件的文件夹的绝对路径。

## <a name="additional-resources"></a>其他资源

* [Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)（包括 HTTPS 配置和 SNI 支持）
* <xref:fundamentals/host/web-host>
