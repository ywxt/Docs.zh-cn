---
title: 在 Windows 服务中托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
ms.author: tdykstra
ms.custom: mvc
ms.date: 06/04/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: 4fd0cc881eff3b1bbdfdf51e223d0fd42051c31d
ms.sourcegitcommit: 516d0645c35ea784a3ae807be087ae70446a46ee
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2018
ms.locfileid: "39320734"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>在 Windows 服务中托管 ASP.NET Core

作者：[Luke Latham](https://github.com/guardrex)、[Tom Dykstra](https://github.com/tdykstra)

不将 IIS 用作 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)时，可在 Windows 上托管 ASP.NET Core 应用。 作为 Windows 服务托管时，无需人工干预应用即可在重新启动和崩溃后自动启动。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="get-started"></a>入门

要将现有 ASP.NET Core 项目设置为在服务中运行，需要执行以下最小更改：

1. 在项目文件中：

   1. 确认是否存在运行时标识符，或将其添加到包含目标框架的 \<PropertyGroup> 中：

      ::: moniker range=">= aspnetcore-2.1"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

      ::: moniker range="= aspnetcore-2.0"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

      ::: moniker range="< aspnetcore-2.0"

      ```xml
      <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        <RuntimeIdentifier>win7-x64</RuntimeIdentifier>
      </PropertyGroup>
      ```

      ::: moniker-end

   1. 为 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/) 添加包引用。

1. 在 `Program.Main` 中，进行下列更改：

   * 调用 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)，而不是 `host.Run`。

   * 调用 [UseContentRoot](xref:fundamentals/host/web-host#content-root) 并使用应用的发布位置路径，而不是 `Directory.GetCurrentDirectory()`。

     ::: moniker range=">= aspnetcore-2.0"

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,12)]

     ::: moniker-end

     ::: moniker range="< aspnetcore-2.0"

     [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]

     ::: moniker-end

1. 发布应用。 使用 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 或 [Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)。

   要从命令行发布示例应用，请从项目文件夹中的控制台窗口中运行以下命令：

   ```console
   dotnet publish --configuration Release
   ```

1. 使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具创建服务。 `binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。 等于号和路径开头的引号字符之间需要添加空格。

   ```console
   sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"
   ```

   对于项目文件夹中发布的服务，请使用 publish 文件夹的路径创建服务。 下例中的服务已实现以下操作：

   * 命名为“MyService”。
   * 发布到 c:\\my_services\\AspNetCoreService\\bin\\Release\\&lt;TARGET_FRAMEWORK&gt;\\publish 文件夹。
   * 由名为 AspNetCoreService.exe 的应用可执行文件表示。

   利用管理员特权打开一个命令行界面，运行以下命令：

   ```console
   sc create MyService binPath= "c:\my_services\AspNetCoreService\bin\Release\<TARGET_FRAMEWORK>\publish\AspNetCoreService.exe"
   ```
   
   > [!IMPORTANT]
   > 确保 `binPath=` 参数与其值之间存在空格。
   
   从其他文件夹发布和启动服务：
   
   1. 使用 `dotnet publish` 命令上的 [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) 选项。
   1. 通过使用输出文件夹路径的 `sc.exe` 命令创建服务。 在向 `binPath` 提供的路径中包含服务可执行文件的名称。

1. 使用 `sc start <SERVICE_NAME>` 命令启动服务。

   要启动示例应用服务，请使用以下命令：

   ```console
   sc start MyService
   ```

   此命令需要几秒钟才能启动服务。

1. `sc query <SERVICE_NAME>` 命令可用于检查并确定服务状态：

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

1. 使用 `sc stop <SERVICE_NAME>` 命令停止服务。

   以下命令可停止示例应用服务：

   ```console
   sc stop MyService
   ```

1. 停止服务并经过短暂延迟后，使用 `sc delete <SERVICE_NAME>` 命令卸载服务。

   检查示例应用服务的状态：

   ```console
   sc query MyService
   ```

   当示例应用服务处于 `STOPPED` 状态时，使用以下命令卸载示例应用服务：

   ```console
   sc delete MyService
   ```

## <a name="provide-a-way-to-run-outside-of-a-service"></a>提供在服务之外运行的方法

在服务之外运行时更便于进行测试和调试，因此通常仅在特定情况下添加调用 `RunAsService` 的代码。 例如，应用可以使用 `--console` 命令行参数或在已附加调试器时作为控制台应用运行：

::: moniker range=">= aspnetcore-2.0"

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

由于 ASP.NET Core 配置需要命令行参数的名称/值对，因此将先删除 `--console` 开关，然后再将参数传递到 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder)。

> [!NOTE]
> 不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。

::: moniker-end

::: moniker range="< aspnetcore-2.0"

[!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOrConsole)]

::: moniker-end

## <a name="handle-stopping-and-starting-events"></a>处理停止和启动事件

要处理 [OnStarting](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarting)、[OnStarted](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstarted) 和 [OnStopping](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice.onstopping) 事件，请执行以下额外更改：

1. 创建从 [WebHostService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostservice) 派生的类：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=NoLogging)]

2. 创建可将自定义 `WebHostService` 传递给 [ServiceBase.Run](/dotnet/api/system.serviceprocess.servicebase.run) 的 [IWebHost](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost) 的扩展方法：

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. 在 `Program.Main` 中，调用新扩展方法 `RunAsCustomService`，而不是 [RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)：

   ::: moniker range=">= aspnetcore-2.0"

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=14)]

   > [!NOTE]
   > 不将 `Main` 中的 `isService` 传递到 `CreateWebHostBuilder`，因为 `CreateWebHostBuilder` 的签名必须是 `CreateWebHostBuilder(string[])`才能使[集成测试](xref:test/integration-tests)正常运行。

   ::: moniker-end

   ::: moniker range="< aspnetcore-2.0"

   [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=27)]

   ::: moniker-end

如果自定义 `WebHostService` 代码需要来自依赖项注入（如记录器）的服务，请从 [IWebHost.Services](/dotnet/api/microsoft.aspnetcore.hosting.iwebhost.services) 属性中获取：

[!code-csharp[](windows-service/samples/2.x/AspNetCoreService/CustomWebHostService.cs?name=Logging&highlight=7-8)]

## <a name="proxy-server-and-load-balancer-scenarios"></a>代理服务器和负载均衡器方案

与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。 有关更多信息，请参见<xref:host-and-deploy/proxy-load-balancer>。

## <a name="additional-resources"></a>其他资源

* [Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)（包括 HTTPS 配置和 SNI 支持）
* <xref:fundamentals/host/web-host>
