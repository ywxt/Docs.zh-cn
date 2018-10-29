---
title: 在 Windows 服务中托管 ASP.NET Core
author: guardrex
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
ms.author: tdykstra
ms.custom: mvc
ms.date: 09/25/2018
uid: host-and-deploy/windows-service
ms.openlocfilehash: f9b1c3fbfafa839c116688e0ac63804afcd5dbe0
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2018
ms.locfileid: "50206668"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>在 Windows 服务中托管 ASP.NET Core

作者：[Luke Latham](https://github.com/guardrex)、[Tom Dykstra](https://github.com/tdykstra)

不将 IIS 用作 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)时，可在 Windows 上托管 ASP.NET Core 应用。 作为 Windows 服务进行托管时，应用将在重新启动后自动启动。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/samples)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="convert-a-project-into-a-windows-service"></a>将项目转换为 Windows 服务

要将现有 ASP.NET Core 项目设置为作为服务运行，至少需要执行以下更改：

1. 在项目文件中：

   * 确认是否存在 Windows [运行时标识符 (RID)](/dotnet/core/rid-catalog)，或将其添加到包含目标框架的 `<PropertyGroup>` 中：

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

      要发布多个 RID：

      * 通过以分号分隔的列表提供 RID。
      * 使用属性名称 `<RuntimeIdentifiers>`（复数）。

      有关详细信息，请参阅 [.NET Core RID 目录](/dotnet/core/rid-catalog)。

   * 为 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices) 添加包引用。

1. 在 `Program.Main` 中，进行下列更改：

   * 调用 [host.RunAsService](/dotnet/api/microsoft.aspnetcore.hosting.windowsservices.webhostwindowsserviceextensions.runasservice)，而不是 `host.Run`。

   * 调用 [UseContentRoot](xref:fundamentals/host/web-host#content-root) 并使用应用的发布位置路径，而不是 `Directory.GetCurrentDirectory()`。

     ::: moniker range=">= aspnetcore-2.0"

     [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=8-9,16)]

     ::: moniker-end

     ::: moniker range="< aspnetcore-2.0"

     [!code-csharp[](windows-service/samples_snapshot/1.x/AspNetCoreService/Program.cs?name=ServiceOnly&highlight=3-4,8,13)]

     ::: moniker-end

1. 发布应用。 使用 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 或 [Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)。 使用 Visual Studio 时，请选择 FolderProfile。

   要使用命令行接口 (CLI) 工具发布示例应用，请在项目文件夹的命令提示符处运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 命令。 必须在项目文件的 `<RuntimeIdenfifier>`（或 `<RuntimeIdentifiers>`）属性中指定 RID。 在以下示例中，应用在 `win7-x64` 运行时的发布配置中发布：

   ```console
   dotnet publish --configuration Release --runtime win7-x64
   ```

1. 使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具创建服务。 `binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。 等于号和路径开头的引号字符之间需要添加空格。

   ```console
   sc create <SERVICE_NAME> binPath= "<PATH_TO_SERVICE_EXECUTABLE>"
   ```

   对于项目文件夹中发布的服务，请使用 publish 文件夹的路径创建服务。 如下示例中：

   * 该项目位于 c:\\my_services\\AspNetCoreService 文件夹中。
   * 项目在 `Release` 配置中发布。
   * 目标框架名字对象 (TFM) 为 `netcoreapp2.1`。
   * 运行时标识符 (RID) 为 `win7-x64`。
   * 应用可执行文件名为 AspNetCoreService.exe。
   * 服务名为 MyService。

   示例:

   ```console
   sc create MyService binPath= "c:\my_services\AspNetCoreService\bin\Release\netcoreapp2.1\win7-x64\publish\AspNetCoreService.exe"
   ```

   > [!IMPORTANT]
   > 确保 `binPath=` 参数与其值之间存在空格。

   从其他文件夹发布和启动服务：

      * 使用 `dotnet publish` 命令上的 [--output &lt;OUTPUT_DIRECTORY&gt;](/dotnet/core/tools/dotnet-publish#options) 选项。 如果使用 Visual Studio，请在“FolderProfile”发布属性页面中配置“目标位置”，然后再选择“发布”按钮。
      * 通过使用输出文件夹路径的 `sc.exe` 命令创建服务。 在向 `binPath` 提供的路径中包含服务可执行文件的名称。

1. 使用 `sc start <SERVICE_NAME>` 命令启动服务。

   要启动示例应用服务，请使用以下命令：

   ```console
   sc start MyService
   ```

   此命令需要几秒钟才能启动服务。

1. 要检查服务的状态，请使用 `sc query <SERVICE_NAME>` 命令。 状态报告为以下值之一：

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

## <a name="run-the-app-outside-of-a-service"></a>在服务之外运行应用

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

   [!code-csharp[](windows-service/samples/2.x/AspNetCoreService/Program.cs?name=HandleStopStart&highlight=17)]

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

## <a name="configure-https"></a>配置 HTTPS

指定 [Kestrel 服务器 HTTPS 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)。

## <a name="current-directory-and-content-root"></a>当前目录和内容根

通过为 Windows 服务调用 `Directory.GetCurrentDirectory()` 返回的当前工作目录是 C:\\WINDOWS\\system32 文件夹。 system32 文件夹不是存储服务文件（如设置文件）的合适位置。 使用 [IConfigurationBuilder](/dotnet/api/microsoft.extensions.configuration.iconfigurationbuilder) 时，通过以下某种方法使用 [FileConfigurationExtensions.SetBasePath](/dotnet/api/microsoft.extensions.configuration.fileconfigurationextensions.setbasepath) 维护和访问服务的资产和设置文件：

* 使用内容根路径。 `IHostingEnvironment.ContentRootPath` 是创建服务时提供给 `binPath` 参数的同一路径。 不要使用 `Directory.GetCurrentDirectory()` 创建设置文件的路径，而是使用内容根路径并在应用的内容根中维护文件。
* 将文件存储在磁盘中的合适位置。 使用 `SetBasePath` 指定到包含文件的文件夹的绝对路径。

## <a name="additional-resources"></a>其他资源

* [Kestrel 终结点配置](xref:fundamentals/servers/kestrel#endpoint-configuration)（包括 HTTPS 配置和 SNI 支持）
* <xref:fundamentals/host/web-host>
