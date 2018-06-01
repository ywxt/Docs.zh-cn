---
title: 在 Windows 服务中托管 ASP.NET Core
author: rick-anderson
description: 了解如何在 Windows 服务中托管 ASP.NET Core 应用。
manager: wpickett
ms.author: tdykstra
ms.custom: mvc
ms.date: 01/30/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/windows-service
ms.openlocfilehash: 29f83ee585c73aeb57a09f70ea8e28650c05ce69
ms.sourcegitcommit: a19261eb82b948af6e4a1664fcfb8dabb16150e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
ms.locfileid: "34153524"
---
# <a name="host-aspnet-core-in-a-windows-service"></a>在 Windows 服务中托管 ASP.NET Core

作者：[Tom Dykstra](https://github.com/tdykstra)

不使用 IIS 在 Windows 上托管 ASP.NET Core 应用的推荐方式是在 [Windows 服务](/dotnet/framework/windows-services/introduction-to-windows-service-applications)中运行应用。 作为 Windows 服务托管时，无需人工干预应用即可在重新启动和崩溃后自动启动。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/host-and-deploy/windows-service/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）。 有关如何运行示例应用的说明，请参阅示例的 README.md 文件。

## <a name="prerequisites"></a>系统必备

* 应用必须在 .NET Framework 运行时运行。 在 .csproj 文件中，指定 [TargetFramework](/nuget/schema/target-frameworks) 和 [RuntimeIdentifier](/dotnet/articles/core/rid-catalog) 的相应值。 以下是一个示例：

  [!code-xml[](windows-service/sample/AspNetCoreService.csproj?range=3-6)]

  在 Visual Studio 中创建项目时，请使用“ASP.NET Core 应用程序(.NET Framework)”模板。

* 如果应用接收来自 Internet（而不仅仅来自内部网络）的请求，则必须使用 [HTTP.sys](xref:fundamentals/servers/httpsys) Web 服务器（对于 ASP.NET Core 1.x 应用，以前称为 [WebListener](xref:fundamentals/servers/weblistener)）而不是 [Kestrel](xref:fundamentals/servers/kestrel)。 建议将 IIS 用作反向代理服务器与 Kestrel 进行 Edge 部署。 有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。

## <a name="get-started"></a>入门

本部分介绍了将现有的 ASP.NET Core 项目设置为在服务中运行所需的最小更改。

1. 安装 NuGet 包 [Microsoft.AspNetCore.Hosting.WindowsServices](https://www.nuget.org/packages/Microsoft.AspNetCore.Hosting.WindowsServices/)。

2. 在 `Program.Main` 中，进行下列更改：

   * 调用 `host.RunAsService` 而非 `host.Run`。

   * 如果代码调用 `UseContentRoot`，请使用发布位置的路径，而不是 `Directory.GetCurrentDirectory()`。

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=ServiceOnly&highlight=3-4,7,12)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOnly&highlight=3-4,8,14)]

   ---

3. 将应用发布到文件夹。 使用可发布到文件夹的 [dotnet publish](/dotnet/articles/core/tools/dotnet-publish) 或 [Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles)。

4. 通过创建和启动服务进行测试。

   使用管理权限打开命令行界面，以便使用 [sc.exe](https://technet.microsoft.com/library/bb490995) 命令行工具来创建和启动服务。 如果将该服务命名为 MyService、发布到 `c:\svc`，以及命名为 AspNetCoreService，则相应的命令为：

   ```console
   sc create MyService binPath="c:\svc\aspnetcoreservice.exe"
   sc start MyService
   ```

   `binPath` 值是应用的可执行文件的路径，其中包括可执行文件的文件名。

   ![控制台窗口创建和启动示例](windows-service/_static/create-start.png)

   完成这些命令后，浏览到作为控制台应用运行时的同一路径（默认情况下为 `http://localhost:5000`）：

   ![在服务中运行](windows-service/_static/running-in-service.png)

## <a name="provide-a-way-to-run-outside-of-a-service"></a>提供在服务之外运行的方法

在服务之外运行时更便于进行测试和调试，因此通常仅在特定情况下添加调用 `RunAsService` 的代码。 例如，应用可以使用 `--console` 命令行参数或在已附加调试器时作为控制台应用运行：

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

[!code-csharp[](windows-service/sample/Program.cs?name=ServiceOrConsole)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

[!code-csharp[](windows-service/sample_snapshot/Program.cs?name=ServiceOrConsole)]

---

## <a name="handle-stopping-and-starting-events"></a>处理停止和启动事件

若要处理 `OnStarting`、`OnStarted` 和 `OnStopping` 事件，请进行以下其他更改：

1. 创建一个从 `WebHostService` 派生的类：

   [!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=NoLogging)]

2. 创建可将自定义 `WebHostService` 传递给 `ServiceBase.Run` 的 `IWebHost` 的扩展方法：

   [!code-csharp[](windows-service/sample/WebHostServiceExtensions.cs?name=ExtensionsClass)]

3. 在 `Program.Main` 中，调用新的扩展方法 `RunAsCustomService`，而不是 `RunAsService`：

   # <a name="aspnet-core-2xtabaspnetcore2x"></a>[ASP.NET Core 2.x](#tab/aspnetcore2x/)

   [!code-csharp[](windows-service/sample/Program.cs?name=HandleStopStart&highlight=24)]

   # <a name="aspnet-core-1xtabaspnetcore1x"></a>[ASP.NET Core 1.x](#tab/aspnetcore1x/)

   [!code-csharp[](windows-service/sample_snapshot/Program.cs?name=HandleStopStart&highlight=26)]

   ---

如果自定义 `WebHostService` 代码需要来自依赖关系注入（如记录器）的服务，请从 `IWebHost` 的 `Services` 属性中获取该服务：

[!code-csharp[](windows-service/sample/CustomWebHostService.cs?name=Logging&highlight=7)]

## <a name="proxy-server-and-load-balancer-scenarios"></a>代理服务器和负载均衡器方案

与来自 Internet 或公司网络的请求进行交互且在代理或负载均衡器后方的服务可能需要其他配置。 有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。

## <a name="acknowledgments"></a>鸣谢

本文是在以下出版物来源的帮助下编写的：

* [作为 Windows 服务托管 ASP.NET Core](https://stackoverflow.com/questions/37346383/hosting-asp-net-core-as-windows-service/37464074)
* [如何在 Windows 服务中托管 ASP.NET Core](https://dotnetthoughts.net/how-to-host-your-aspnet-core-in-a-windows-service/)
