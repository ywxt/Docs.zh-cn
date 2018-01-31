---
title: "使用 IIS 在 Windows 上托管 ASP.NET Core"
author: guardrex
description: "了解如何在 Windows Server Internet Information Services (IIS) 上托管 ASP.NET Core 应用。"
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/index
ms.openlocfilehash: 1df438af2394f41b686413cd1ce5ad73a9416ec5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="host-aspnet-core-on-windows-with-iis"></a><span data-ttu-id="b4b79-103">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b4b79-103">Host ASP.NET Core on Windows with IIS</span></span>

<span data-ttu-id="b4b79-104">作者：[Luke Latham](https://github.com/guardrex) 和 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b4b79-104">By [Luke Latham](https://github.com/guardrex) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="b4b79-105">支持的操作系统</span><span class="sxs-lookup"><span data-stu-id="b4b79-105">Supported operating systems</span></span>

<span data-ttu-id="b4b79-106">支持下列操作系统：</span><span class="sxs-lookup"><span data-stu-id="b4b79-106">The following operating systems are supported:</span></span>

* <span data-ttu-id="b4b79-107">Windows 7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="b4b79-107">Windows 7 and newer</span></span>
* <span data-ttu-id="b4b79-108">Windows Server 2008 R2 和 更新版本&#8224;</span><span class="sxs-lookup"><span data-stu-id="b4b79-108">Windows Server 2008 R2 and newer&#8224;</span></span>

<span data-ttu-id="b4b79-109">&#8224;在概念上，本文档描述的 IIS 配置也适用于在 Nano Server IIS 上托管 ASP.NET Core 应用，但有关具体说明，请参阅 [ASP.NET Core 与 Nano Server 上运行的 IIS](xref:tutorials/nano-server)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-109">&#8224;Conceptually, the IIS configuration described in this document also applies to hosting ASP.NET Core apps on Nano Server IIS, but refer to [ASP.NET Core with IIS on Nano Server](xref:tutorials/nano-server) for specific instructions.</span></span>

<span data-ttu-id="b4b79-110">[HTTP.sys 服务器](xref:fundamentals/servers/httpsys)（以前称为 [WebListener](xref:fundamentals/servers/weblistener)）在使用 IIS 的反向代理配置中不起作用。</span><span class="sxs-lookup"><span data-stu-id="b4b79-110">[HTTP.sys server](xref:fundamentals/servers/httpsys) (formerly called [WebListener](xref:fundamentals/servers/weblistener)) won't work in a reverse proxy configuration with IIS.</span></span> <span data-ttu-id="b4b79-111">请使用 [Kestrel 服务器](xref:fundamentals/servers/kestrel)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-111">Use the [Kestrel server](xref:fundamentals/servers/kestrel).</span></span>

## <a name="iis-configuration"></a><span data-ttu-id="b4b79-112">IIS 配置</span><span class="sxs-lookup"><span data-stu-id="b4b79-112">IIS configuration</span></span>

<span data-ttu-id="b4b79-113">启用 Web 服务器 (IIS) 角色并建立角色服务。</span><span class="sxs-lookup"><span data-stu-id="b4b79-113">Enable the **Web Server (IIS)** role and establish role services.</span></span>

### <a name="windows-desktop-operating-systems"></a><span data-ttu-id="b4b79-114">Windows 桌面操作系统</span><span class="sxs-lookup"><span data-stu-id="b4b79-114">Windows desktop operating systems</span></span>

<span data-ttu-id="b4b79-115">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="b4b79-115">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span> <span data-ttu-id="b4b79-116">打开“Internet Information Services”组和“Web 管理工具”。</span><span class="sxs-lookup"><span data-stu-id="b4b79-116">Open the group for **Internet Information Services** and **Web Management Tools**.</span></span> <span data-ttu-id="b4b79-117">选中“IIS 管理控制台”框。</span><span class="sxs-lookup"><span data-stu-id="b4b79-117">Check the box for **IIS Management Console**.</span></span> <span data-ttu-id="b4b79-118">选中“万维网服务”框。</span><span class="sxs-lookup"><span data-stu-id="b4b79-118">Check the box for **World Wide Web Services**.</span></span> <span data-ttu-id="b4b79-119">接受“万维网服务”的默认功能，或自定义 IIS 功能。</span><span class="sxs-lookup"><span data-stu-id="b4b79-119">Accept the default features for **World Wide Web Services** or customize the IIS features.</span></span>

![在“Windows 功能”中选择了“IIS 管理控制台”和“万维网服务”。](index/_static/windows-features-win10.png)

### <a name="windows-server-operating-systems"></a><span data-ttu-id="b4b79-121">Windows Server 操作系统</span><span class="sxs-lookup"><span data-stu-id="b4b79-121">Windows Server operating systems</span></span>

<span data-ttu-id="b4b79-122">对于服务器操作系统，通过“管理”菜单或“服务器管理器”中的链接使用“添加角色和功能”向导。</span><span class="sxs-lookup"><span data-stu-id="b4b79-122">For server operating systems, use the **Add Roles and Features** wizard via the **Manage** menu or the link in **Server Manager**.</span></span> <span data-ttu-id="b4b79-123">在“服务器角色”步骤中，选中“Web 服务器(IIS)”框。</span><span class="sxs-lookup"><span data-stu-id="b4b79-123">On the **Server Roles** step, check the box for **Web Server (IIS)**.</span></span>

![在选择服务器角色步骤中选择了“Web 服务器 IIS”角色。](index/_static/server-roles-ws2016.png)

<span data-ttu-id="b4b79-125">在“角色服务”步骤中，选择所需 IIS 角色服务，或接受提供的默认角色服务。</span><span class="sxs-lookup"><span data-stu-id="b4b79-125">On the **Role services** step, select the IIS role services desired or accept the default role services provided.</span></span>

![在选择角色服务步骤中选择了默认角色服务。](index/_static/role-services-ws2016.png)

<span data-ttu-id="b4b79-127">继续执行“确认”步骤，安装 Web 服务器角色和服务。</span><span class="sxs-lookup"><span data-stu-id="b4b79-127">Proceed through the **Confirmation** step to install the web server role and services.</span></span> <span data-ttu-id="b4b79-128">安装 Web 服务器 (IIS) 角色后无需重启服务器/IIS。</span><span class="sxs-lookup"><span data-stu-id="b4b79-128">A server/IIS restart isn't required after installing the Web Server (IIS) role.</span></span>

## <a name="install-the-net-core-windows-server-hosting-bundle"></a><span data-ttu-id="b4b79-129">安装 .NET Core Windows Server 托管捆绑包</span><span class="sxs-lookup"><span data-stu-id="b4b79-129">Install the .NET Core Windows Server Hosting bundle</span></span>

1. <span data-ttu-id="b4b79-130">在托管系统上安装 [.NET Core Windows Server 托管捆绑包](https://aka.ms/dotnetcore-2-windowshosting)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-130">Install the [.NET Core Windows Server Hosting bundle](https://aka.ms/dotnetcore-2-windowshosting) on the hosting system.</span></span> <span data-ttu-id="b4b79-131">捆绑包可安装 .NET Core 运行时、.NET Core 库和 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-131">The bundle installs the .NET Core Runtime, .NET Core Library, and the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="b4b79-132">该模块创建 IIS 与 Kestrel 服务器之间的反向代理。</span><span class="sxs-lookup"><span data-stu-id="b4b79-132">The module creates the reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="b4b79-133">如果系统没有 Internet 连接，请先获取并安装 [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840)，再安装 .NET Core Windows Server 托管捆绑包。</span><span class="sxs-lookup"><span data-stu-id="b4b79-133">If the system doesn't have an Internet connection, obtain and install the [Microsoft Visual C++ 2015 Redistributable](https://www.microsoft.com/download/details.aspx?id=53840) before installing the .NET Core Windows Server Hosting bundle.</span></span>

2. <span data-ttu-id="b4b79-134">重启系统，或在命令提示符处依次执行 net stop was /y 和 net start w3svc，了解系统路径的更改。</span><span class="sxs-lookup"><span data-stu-id="b4b79-134">Restart the system or execute **net stop was /y** followed by **net start w3svc** from a command prompt to pick up a change to the system PATH.</span></span>

> [!NOTE]
> <span data-ttu-id="b4b79-135">有关 IIS 共享配置的信息，请参阅[使用 IIS 共享配置的 ASP.NET Core 模块](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-135">For information on IIS Shared Configuration, see [ASP.NET Core Module with IIS Shared Configuration](xref:host-and-deploy/aspnet-core-module#aspnet-core-module-with-an-iis-shared-configuration).</span></span>

## <a name="install-web-deploy-when-publishing-with-visual-studio"></a><span data-ttu-id="b4b79-136">使用 Visual Studio 进行发布时安装 Web 部署</span><span class="sxs-lookup"><span data-stu-id="b4b79-136">Install Web Deploy when publishing with Visual Studio</span></span>

<span data-ttu-id="b4b79-137">使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)将应用部署到服务器时，请在服务器上安装最新版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="b4b79-137">When deploying apps to servers with [Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy), install the latest version of Web Deploy on the server.</span></span> <span data-ttu-id="b4b79-138">要安装 Web 部署，请使用 [Web 平台安装程序 (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) 或直接从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=43717)获取安装程序。</span><span class="sxs-lookup"><span data-stu-id="b4b79-138">To install Web Deploy, use the [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) or obtain an installer directly from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=43717).</span></span> <span data-ttu-id="b4b79-139">建议使用 WebPI。</span><span class="sxs-lookup"><span data-stu-id="b4b79-139">The preferred method is to use WebPI.</span></span> <span data-ttu-id="b4b79-140">WebPI 为托管提供程序提供独立的安装程序和配置。</span><span class="sxs-lookup"><span data-stu-id="b4b79-140">WebPI offers a standalone setup and a configuration for hosting providers.</span></span>

## <a name="application-configuration"></a><span data-ttu-id="b4b79-141">应用程序配置</span><span class="sxs-lookup"><span data-stu-id="b4b79-141">Application configuration</span></span>

### <a name="enabling-the-iisintegration-components"></a><span data-ttu-id="b4b79-142">启用 IISIntegration 组件</span><span class="sxs-lookup"><span data-stu-id="b4b79-142">Enabling the IISIntegration components</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="b4b79-143">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="b4b79-143">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="b4b79-144">典型的 Program.cs 调用 [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) 以开始设置主机。</span><span class="sxs-lookup"><span data-stu-id="b4b79-144">A typical *Program.cs* calls [CreateDefaultBuilder](/dotnet/api/microsoft.aspnetcore.webhost.createdefaultbuilder) to begin setting up a host.</span></span> <span data-ttu-id="b4b79-145">`CreateDefaultBuilder` 将 [Kestrel](xref:fundamentals/servers/kestrel) 配置为 Web 服务器，并通过配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)的基路径和端口来实现 IIS 集成：</span><span class="sxs-lookup"><span data-stu-id="b4b79-145">`CreateDefaultBuilder` configures [Kestrel](xref:fundamentals/servers/kestrel) as the web server and enables IIS integration by configuring the base path and port for the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module):</span></span>

```csharp
public static IWebHost BuildWebHost(string[] args) =>
    WebHost.CreateDefaultBuilder(args)
        ...
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="b4b79-146">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="b4b79-146">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="b4b79-147">在应用依赖项中加入对 [Microsoft.AspNetCore.Server.IISIntegration ](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/)包的依赖项。</span><span class="sxs-lookup"><span data-stu-id="b4b79-147">Include a dependency on the [Microsoft.AspNetCore.Server.IISIntegration](https://www.nuget.org/packages/Microsoft.AspNetCore.Server.IISIntegration/) package in the app's dependencies.</span></span> <span data-ttu-id="b4b79-148">通过向 WebHostBuilder 添加 UseIISIntegration 扩展方法，将 IIS 集成中间件合并到应用中：</span><span class="sxs-lookup"><span data-stu-id="b4b79-148">Incorporate IIS Integration middleware into the app by adding the *UseIISIntegration* extension method to *WebHostBuilder*:</span></span>

```csharp
var host = new WebHostBuilder()
    .UseKestrel()
    .UseIISIntegration()
    ...
```

<span data-ttu-id="b4b79-149">`UseKestrel` 和 `UseIISIntegration` 均为必需。</span><span class="sxs-lookup"><span data-stu-id="b4b79-149">Both `UseKestrel` and `UseIISIntegration` are required.</span></span> <span data-ttu-id="b4b79-150">调用 `UseIISIntegration` 的代码不会影响代码可移植性。</span><span class="sxs-lookup"><span data-stu-id="b4b79-150">Code calling `UseIISIntegration` doesn't affect code portability.</span></span> <span data-ttu-id="b4b79-151">如果应用不以 IIS 为背景运行（例如，应用直接在 Kestrel 上运行），则 `UseIISIntegration` 无操作。</span><span class="sxs-lookup"><span data-stu-id="b4b79-151">If the app isn't run behind IIS (for example, the app is run directly on Kestrel), `UseIISIntegration` no-ops.</span></span>

---

<span data-ttu-id="b4b79-152">有关托管的详细信息，请参阅 [ASP.NET Core 中的托管](xref:fundamentals/hosting)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-152">For more information on hosting, see [Hosting in ASP.NET Core](xref:fundamentals/hosting).</span></span>

### <a name="iis-options"></a><span data-ttu-id="b4b79-153">IIS 选项</span><span class="sxs-lookup"><span data-stu-id="b4b79-153">IIS options</span></span>

<span data-ttu-id="b4b79-154">要配置 IIS 选项，请在 `ConfigureServices` 中包括 `IISOptions` 的服务配置：</span><span class="sxs-lookup"><span data-stu-id="b4b79-154">To configure IIS options, include a service configuration for `IISOptions` in `ConfigureServices`:</span></span>

```csharp
services.Configure<IISOptions>(options => 
{
    ...
});
```

| <span data-ttu-id="b4b79-155">选项</span><span class="sxs-lookup"><span data-stu-id="b4b79-155">Option</span></span>                         | <span data-ttu-id="b4b79-156">默认</span><span class="sxs-lookup"><span data-stu-id="b4b79-156">Default</span></span> | <span data-ttu-id="b4b79-157">设置</span><span class="sxs-lookup"><span data-stu-id="b4b79-157">Setting</span></span> |
| ------------------------------ | ------- | ------- |
| `AutomaticAuthentication`      | `true`  | <span data-ttu-id="b4b79-158">若为 `true`，身份验证中间件将设置 `HttpContext.User` 并响应一般质询。</span><span class="sxs-lookup"><span data-stu-id="b4b79-158">If `true`, the authentication middleware sets the `HttpContext.User` and responds to generic challenges.</span></span> <span data-ttu-id="b4b79-159">若为 `false`，身份验证中间件仅提供标识 (`HttpContext.User`) 并在 `AuthenticationScheme` 显式请求时响应质询。</span><span class="sxs-lookup"><span data-stu-id="b4b79-159">If `false`, the authentication middleware only provides an identity (`HttpContext.User`) and responds to challenges when explicitly requested by the `AuthenticationScheme`.</span></span> <span data-ttu-id="b4b79-160">必须在 IIS 中启用 Windows 身份验证使 `AutomaticAuthentication` 得以运行。</span><span class="sxs-lookup"><span data-stu-id="b4b79-160">Windows Authentication must be enabled in IIS for `AutomaticAuthentication` to function.</span></span> |
| `AuthenticationDisplayName`    | `null`  | <span data-ttu-id="b4b79-161">设置在登录页上向用户显示的显示名。</span><span class="sxs-lookup"><span data-stu-id="b4b79-161">Sets the display name shown to users on login pages.</span></span> |
| `ForwardClientCertificate`     | `true`  | <span data-ttu-id="b4b79-162">若为 `true`，且存在 `MS-ASPNETCORE-CLIENTCERT` 请求头，则填充 `HttpContext.Connection.ClientCertificate`。</span><span class="sxs-lookup"><span data-stu-id="b4b79-162">If `true` and the `MS-ASPNETCORE-CLIENTCERT` request header is present, the `HttpContext.Connection.ClientCertificate` is populated.</span></span> |

### <a name="webconfig"></a><span data-ttu-id="b4b79-163">web.config</span><span class="sxs-lookup"><span data-stu-id="b4b79-163">web.config</span></span>

<span data-ttu-id="b4b79-164">web.config 文件的主要用途是配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-164">The *web.config* file's primary purpose is to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module).</span></span> <span data-ttu-id="b4b79-165">它可以提供其他 IIS 配置设置。</span><span class="sxs-lookup"><span data-stu-id="b4b79-165">It may optionally provide additional IIS configuration settings.</span></span> <span data-ttu-id="b4b79-166">web.config 的创建、转换和发布 由 .NET Core Web SDK (`Microsoft.NET.Sdk.Web`) 处理。</span><span class="sxs-lookup"><span data-stu-id="b4b79-166">Creating, transforming, and publishing *web.config* is handled by the .NET Core Web SDK (`Microsoft.NET.Sdk.Web`).</span></span> <span data-ttu-id="b4b79-167">SDK 设置在项目文件 `<Project Sdk="Microsoft.NET.Sdk.Web">` 的顶部。</span><span class="sxs-lookup"><span data-stu-id="b4b79-167">The SDK is set  at the top of the project file, `<Project Sdk="Microsoft.NET.Sdk.Web">`.</span></span> <span data-ttu-id="b4b79-168">要防止 SDK 转换 *web.config* 文件，请将 **\<IsTransformWebConfigDisabled>** 属性添加到项目文件，并将其设置为 `true`：</span><span class="sxs-lookup"><span data-stu-id="b4b79-168">To prevent the SDK from transforming the *web.config* file, add the **\<IsTransformWebConfigDisabled>** property to the project file with a setting of `true`:</span></span>

```xml
<PropertyGroup>
  <IsTransformWebConfigDisabled>true</IsTransformWebConfigDisabled>
</PropertyGroup>
```

<span data-ttu-id="b4b79-169">如果项目中有 web.config 文件，则会使用正确 processPath 和参数转换该文件，以便配置 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，并将该文件移动到[已发布的输出](xref:host-and-deploy/directory-structure)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-169">If a *web.config* file is in the project, it's transformed with the correct *processPath* and *arguments* to configure the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) and moved to [published output](xref:host-and-deploy/directory-structure).</span></span> <span data-ttu-id="b4b79-170">转换不会修改文件中的 IIS 配置设置。</span><span class="sxs-lookup"><span data-stu-id="b4b79-170">The transformation doesn't modify IIS configuration settings in the file.</span></span>

### <a name="webconfig-location"></a><span data-ttu-id="b4b79-171">web.config 位置</span><span class="sxs-lookup"><span data-stu-id="b4b79-171">web.config location</span></span>

<span data-ttu-id="b4b79-172">.NET Core 应用通过 IIS 与 Kestrel 服务器之间的反向代理托管。</span><span class="sxs-lookup"><span data-stu-id="b4b79-172">.NET Core apps are hosted via a reverse proxy between IIS and the Kestrel server.</span></span> <span data-ttu-id="b4b79-173">为了创建反向代理，web.config 文件必须存在于已部署应用的内容根路径（通常为应用基路径）中，该路径是向 IIS 提供的网站物理路径。</span><span class="sxs-lookup"><span data-stu-id="b4b79-173">In order to create the reverse proxy, the *web.config* file must be present at the content root path (typically the app base path) of the deployed app, which is the website physical path provided to IIS.</span></span> <span data-ttu-id="b4b79-174">若要使用 Web 部署发布多个应用，应用的根路径中需要包含 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-174">The *web.config* file is required at the root of the app to enable the publishing of multiple apps using Web Deploy.</span></span>

<span data-ttu-id="b4b79-175">敏感文件存在于应用的物理路径中，包括子文件夹，如 \<assembly_name>.runtimeconfig.json、\<assembly_name>.xml（XML 文档注释）和 \<assembly_name>.deps.json。</span><span class="sxs-lookup"><span data-stu-id="b4b79-175">Sensitive files exist on the app's physical path, including subfolders, such as *\<assembly_name>.runtimeconfig.json*, *\<assembly_name>.xml* (XML Documentation comments), and *\<assembly_name>.deps.json*.</span></span> <span data-ttu-id="b4b79-176">存在 web.config 文件并使用该文件配置站点时，IIS 会阻止提供这些敏感文件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-176">When the *web.config* file is present and configures the site, IIS prevents these sensitive files from being served.</span></span> <span data-ttu-id="b4b79-177">因此，切勿意外重命名 web.config 文件或将其从部署中删除，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="b4b79-177">**Therefore, it's important that the *web.config* file isn't accidently renamed or removed from the deployment.**</span></span>

## <a name="create-the-iis-website"></a><span data-ttu-id="b4b79-178">创建 IIS 网站</span><span class="sxs-lookup"><span data-stu-id="b4b79-178">Create the IIS Website</span></span>

1. <span data-ttu-id="b4b79-179">在目标 IIS 系统上，创建一个文件夹，将应用的已发布文件夹和文件包含在其中，如 [目录结构](xref:host-and-deploy/directory-structure)中所述。</span><span class="sxs-lookup"><span data-stu-id="b4b79-179">On the target IIS system, create a folder to contain the app's published folders and files, which are described in [Directory Structure](xref:host-and-deploy/directory-structure).</span></span>

2. <span data-ttu-id="b4b79-180">在文件夹中创建一个“日志”文件夹，用于在启用 stdout 日志记录时保存 stdout 日志。</span><span class="sxs-lookup"><span data-stu-id="b4b79-180">Within the folder, create a *logs* folder to hold stdout logs when stdout logging is enabled.</span></span> <span data-ttu-id="b4b79-181">如果部署应用时有效负载中包含了“日志”文件夹，请跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="b4b79-181">If the app is deployed with a *logs* folder in the payload, skip this step.</span></span> <span data-ttu-id="b4b79-182">有关如何让 MSBuild 创建“日志”文件夹的说明，请参阅[目录结构](xref:host-and-deploy/directory-structure)主题。</span><span class="sxs-lookup"><span data-stu-id="b4b79-182">For instructions on how to make MSBuild create the *logs* folder, see the [Directory structure](xref:host-and-deploy/directory-structure) topic.</span></span>

3. <span data-ttu-id="b4b79-183">在 IIS 管理器中创建新网站。</span><span class="sxs-lookup"><span data-stu-id="b4b79-183">In **IIS Manager**, create a new website.</span></span> <span data-ttu-id="b4b79-184">提供网站名称，并将物理路径设置为应用的部署文件夹。</span><span class="sxs-lookup"><span data-stu-id="b4b79-184">Provide a **Site name** and set the **Physical path** to the app's deployment folder.</span></span> <span data-ttu-id="b4b79-185">提供“绑定”配置并创建网站。</span><span class="sxs-lookup"><span data-stu-id="b4b79-185">Provide the **Binding** configuration and create the website.</span></span>

4. <span data-ttu-id="b4b79-186">将“应用程序池”设置为“无托管代码”。</span><span class="sxs-lookup"><span data-stu-id="b4b79-186">Set the application pool to **No Managed Code**.</span></span> <span data-ttu-id="b4b79-187">ASP.NET Core 在单独的进程中运行，并管理运行时。</span><span class="sxs-lookup"><span data-stu-id="b4b79-187">ASP.NET Core runs in a separate process and manages the runtime.</span></span>

5. <span data-ttu-id="b4b79-188">打开“添加网站”窗口。</span><span class="sxs-lookup"><span data-stu-id="b4b79-188">Open the **Add Website** window.</span></span>

   ![选择“站点”上下文菜单中的“添加网站”。](index/_static/add-website-context-menu-ws2016.png)

6. <span data-ttu-id="b4b79-190">配置网站。</span><span class="sxs-lookup"><span data-stu-id="b4b79-190">Configure the website.</span></span>

   ![在“添加网站”步骤中提供网站名称、物理路径和主机名。](index/_static/add-website-ws2016.png)

7. <span data-ttu-id="b4b79-192">在“应用程序池”面板中，右键单击网站的应用池，并从弹出菜单中选择“基本设置...”，打开“编辑应用程序池”窗口。</span><span class="sxs-lookup"><span data-stu-id="b4b79-192">In the **Application Pools** panel, open the **Edit Application Pool** window by right-clicking on the website's app pool and selecting **Basic Settings...** from the popup menu.</span></span>

   ![从应用程序池的上下文菜单中选择“基本设置”。](index/_static/apppools-basic-settings-ws2016.png)

8. <span data-ttu-id="b4b79-194">将“.NET CLR 版本”设置为“无托管代码”。</span><span class="sxs-lookup"><span data-stu-id="b4b79-194">Set the **.NET CLR version** to **No Managed Code**.</span></span>

   ![将“.NET CLR 版本”设置为“无托管代码”。](index/_static/edit-apppool-ws2016.png)
     
    <span data-ttu-id="b4b79-196">请注意：将“.NET CLR 版本”设置为“无托管代码”是可选步骤。</span><span class="sxs-lookup"><span data-stu-id="b4b79-196">Note: Setting the **.NET CLR version** to **No Managed Code** is optional.</span></span> <span data-ttu-id="b4b79-197">ASP.NET Core 不依赖加载桌面 CLR。</span><span class="sxs-lookup"><span data-stu-id="b4b79-197">ASP.NET Core doesn't rely on loading the desktop CLR.</span></span>

9. <span data-ttu-id="b4b79-198">确认进程模型标识拥有适当的权限。</span><span class="sxs-lookup"><span data-stu-id="b4b79-198">Confirm the process model identity has the proper permissions.</span></span>

   <span data-ttu-id="b4b79-199">如果将应用池的默认标识（“进程模型” > “标识”）从 ApplicationPoolIdentity 更改为另一标识，请验证新标识拥有所需的权限，可访问应用的文件夹、数据库和其他所需资源。</span><span class="sxs-lookup"><span data-stu-id="b4b79-199">If the default identity of the app pool (**Process Model** > **Identity**) is changed from **ApplicationPoolIdentity** to another identity, verify that the new identity has the required permissions to access the app's folder, database, and other required resources.</span></span>
   
## <a name="deploy-the-app"></a><span data-ttu-id="b4b79-200">部署应用</span><span class="sxs-lookup"><span data-stu-id="b4b79-200">Deploy the app</span></span>

<span data-ttu-id="b4b79-201">将应用部署到在目标 IIS 系统上创建的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b4b79-201">Deploy the app to the folder created on the target IIS system.</span></span> <span data-ttu-id="b4b79-202">建议使用的部署机制是 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-202">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) is the recommended mechanism for deployment.</span></span>

<span data-ttu-id="b4b79-203">确认要部署的已发布应用未运行。</span><span class="sxs-lookup"><span data-stu-id="b4b79-203">Confirm that the published app for deployment isn't running.</span></span> <span data-ttu-id="b4b79-204">如果应用正在运行，publish 文件夹中的文件会被锁定。</span><span class="sxs-lookup"><span data-stu-id="b4b79-204">Files in the *publish* folder are locked when the app is running.</span></span> <span data-ttu-id="b4b79-205">无法覆盖已锁定的文件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-205">Locked files can't be overwritten.</span></span> <span data-ttu-id="b4b79-206">若要在部署中解除已锁定的文件，请停止应用池：</span><span class="sxs-lookup"><span data-stu-id="b4b79-206">To release locked files in a deployment, stop the app pool:</span></span>

* <span data-ttu-id="b4b79-207">在服务器上的 IIS 管理器中进行手动操作。</span><span class="sxs-lookup"><span data-stu-id="b4b79-207">Manually in the IIS Manager on the server.</span></span>
* <span data-ttu-id="b4b79-208">使用 Web 部署并在项目文件中引用 `Microsoft.NET.Sdk.Web`。</span><span class="sxs-lookup"><span data-stu-id="b4b79-208">Using Web Deploy and referencing `Microsoft.NET.Sdk.Web` in the project file.</span></span> <span data-ttu-id="b4b79-209">系统会在 Web 应用目录的根目录中放置一个 app_offline.htm 文件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-209">An *app_offline.htm* file is placed at the root of the web app directory.</span></span> <span data-ttu-id="b4b79-210">该文件存在时，ASP.NET Core 模块会在部署过程中正常关闭该应用并提供 app_offline.htm 文件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-210">When the file is present, the ASP.NET Core Module gracefully shuts down the app and serves the *app_offline.htm* file during the deployment.</span></span> <span data-ttu-id="b4b79-211">有关详细信息，请参阅 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module#appofflinehtm)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-211">For more information, see the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module#appofflinehtm).</span></span>
* <span data-ttu-id="b4b79-212">使用 PowerShell 来停止和重新启动应用池（需要使用 PowerShell 5 或更高版本）：</span><span class="sxs-lookup"><span data-stu-id="b4b79-212">Use PowerShell to stop and restart the app pool (requires PowerShell 5 or later):</span></span>
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

### <a name="web-deploy-with-visual-studio"></a><span data-ttu-id="b4b79-213">在 Visual Studio 内使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="b4b79-213">Web Deploy with Visual Studio</span></span>

<span data-ttu-id="b4b79-214">要了解如何创建用于 Web 部署的发布配置文件，请参阅[用于 ASP.NET Core 应用部署的 Visual Studio 发布配置文件](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-214">See the [Visual Studio publish profiles for ASP.NET Core app deployment](xref:host-and-deploy/visual-studio-publish-profiles#publish-profiles) topic to learn how to create a publish profile for use with Web Deploy.</span></span> <span data-ttu-id="b4b79-215">如果托管提供程序提供了发布配置文件或支持创建发布配置文件，请下载配置文件并使用 Visual Studio 的“发布”对话框进行导入。</span><span class="sxs-lookup"><span data-stu-id="b4b79-215">If the hosting provider supplies a Publish Profile or support for creating one, download their profile and import it using the Visual Studio **Publish** dialog.</span></span>

![“发布”对话框页](index/_static/pub-dialog.png)

### <a name="web-deploy-outside-of-visual-studio"></a><span data-ttu-id="b4b79-217">在 Visual Studio 之外使用 Web 部署</span><span class="sxs-lookup"><span data-stu-id="b4b79-217">Web Deploy outside of Visual Studio</span></span>

<span data-ttu-id="b4b79-218">也可以在 Visual Studio 之外从命令行使用 [Web 部署](/iis/publish/using-web-deploy/introduction-to-web-deploy)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-218">[Web Deploy](/iis/publish/using-web-deploy/introduction-to-web-deploy) can also be used outside of Visual Studio from the command line.</span></span> <span data-ttu-id="b4b79-219">有关详细信息，请参阅 [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool)（Web 部署工具）。</span><span class="sxs-lookup"><span data-stu-id="b4b79-219">For more information, see [Web Deployment Tool](/iis/publish/using-web-deploy/use-the-web-deployment-tool).</span></span>

### <a name="alternatives-to-web-deploy"></a><span data-ttu-id="b4b79-220">Web 部署的替代方法</span><span class="sxs-lookup"><span data-stu-id="b4b79-220">Alternatives to Web Deploy</span></span>

<span data-ttu-id="b4b79-221">有多种方法可以将应用移动到托管系统，例如 Xcopy、Robocopy 或 PowerShell，使用其中任何一种方法皆可。</span><span class="sxs-lookup"><span data-stu-id="b4b79-221">Use any of several methods to move the app to the hosting system, such as Xcopy, Robocopy, or PowerShell.</span></span> <span data-ttu-id="b4b79-222">Visual Studio 用户可以使用[发布示例](https://github.com/aspnet/vsweb-publish/blob/master/samples/samples.md)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-222">Visual Studio users may use the [Publish Samples](https://github.com/aspnet/vsweb-publish/blob/master/samples/samples.md).</span></span>

## <a name="browse-the-website"></a><span data-ttu-id="b4b79-223">浏览网站</span><span class="sxs-lookup"><span data-stu-id="b4b79-223">Browse the website</span></span>

![Microsoft Edge 浏览器已加载 IIS 启动页。](index/_static/browsewebsite.png)

## <a name="data-protection"></a><span data-ttu-id="b4b79-225">数据保护</span><span class="sxs-lookup"><span data-stu-id="b4b79-225">Data protection</span></span>

<span data-ttu-id="b4b79-226">数据保护由多个 ASP.NET 中间件使用，包括用于身份验证的中间件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-226">Data Protection is used by several ASP.NET middlewares, including those used in authentication.</span></span> <span data-ttu-id="b4b79-227">即使不从用户代码中调用数据保护 API，也应该使用部署脚本或在用户代码中配置数据保护，以创建持久的密钥存储。</span><span class="sxs-lookup"><span data-stu-id="b4b79-227">Even if Data Protection APIs aren't called from user's code, Data Protection should be configured with a deployment script or in user code to create a persistent key store.</span></span> <span data-ttu-id="b4b79-228">如果不配置数据保护，则密钥存储在内存中。重启应用时，密钥会被丢弃。</span><span class="sxs-lookup"><span data-stu-id="b4b79-228">If data protection isn't configured, the keys are held in memory and discarded when the app restarts.</span></span>

<span data-ttu-id="b4b79-229">如果 keyring 存储于内存中，则当应用重启时：</span><span class="sxs-lookup"><span data-stu-id="b4b79-229">If the keyring is stored in memory when the app restarts:</span></span>

* <span data-ttu-id="b4b79-230">所有 Forms 身份验证令牌都无效。</span><span class="sxs-lookup"><span data-stu-id="b4b79-230">All forms authentication tokens are invalidated.</span></span> 
* <span data-ttu-id="b4b79-231">用户需要在下一次请求时再次登录。</span><span class="sxs-lookup"><span data-stu-id="b4b79-231">Users are required to sign in again on their next request.</span></span> 
* <span data-ttu-id="b4b79-232">无法再解密使用 keyring 保护的任何数据。</span><span class="sxs-lookup"><span data-stu-id="b4b79-232">Any data protected with the keyring can no longer be decrypted.</span></span>

<span data-ttu-id="b4b79-233">要在 IIS 下配置数据保护，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="b4b79-233">To configure Data Protection under IIS, use **one** of the following approaches:</span></span>

### <a name="create-a-data-protection-registry-hive"></a><span data-ttu-id="b4b79-234">创建数据保护注册表配置单元</span><span class="sxs-lookup"><span data-stu-id="b4b79-234">Create a Data Protection Registry Hive</span></span>

<span data-ttu-id="b4b79-235">ASP.NET 应用使用的数据保护密钥存储在应用外部的注册表配置单元中。</span><span class="sxs-lookup"><span data-stu-id="b4b79-235">Data Protection keys used by ASP.NET apps are stored in registry hives external to the apps.</span></span> <span data-ttu-id="b4b79-236">要持久保存给定应用的密钥，需为应用池创建注册表配置单元。</span><span class="sxs-lookup"><span data-stu-id="b4b79-236">To persist the keys for a given app, create a registry hive for the app pool.</span></span>

<span data-ttu-id="b4b79-237">对于独立的非 Web 场 IIS 安装，可以对用于 ASP.NET Core 应用的每个应用池使用[数据保护 Provision-AutoGenKeys.ps1 PowerShell 脚本](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-237">For standalone, non-webfarm IIS installations, the [Data Protection Provision-AutoGenKeys.ps1 PowerShell script](https://github.com/aspnet/DataProtection/blob/dev/Provision-AutoGenKeys.ps1) can be used for each app pool used with an ASP.NET Core app.</span></span> <span data-ttu-id="b4b79-238">此脚本在仅对工作进程帐户实现 ACL 的 HKLM 注册表中创建特殊的注册表项。</span><span class="sxs-lookup"><span data-stu-id="b4b79-238">This script creates a special registry key in the HKLM registry that's ACLed only to the worker process account.</span></span> <span data-ttu-id="b4b79-239">通过计算机范围的密钥使用 DPAPI 对密钥静态加密。</span><span class="sxs-lookup"><span data-stu-id="b4b79-239">Keys are encrypted at rest using DPAPI with a machine-wide key.</span></span>

<span data-ttu-id="b4b79-240">在 Web 场方案中，可以将应用配置为使用 UNC 路径存储其数据保护密钥环。</span><span class="sxs-lookup"><span data-stu-id="b4b79-240">In web farm scenarios, an app can be configured to use a UNC path to store its data protection keyring.</span></span> <span data-ttu-id="b4b79-241">默认情况下，数据保护密钥未加密。</span><span class="sxs-lookup"><span data-stu-id="b4b79-241">By default, the data protection keys are not encrypted.</span></span> <span data-ttu-id="b4b79-242">确保这种共享的文件权限仅限于运行应用所用的 Windows 帐户。</span><span class="sxs-lookup"><span data-stu-id="b4b79-242">Ensure that the file permissions for such a share are limited to the Windows account the app runs as.</span></span> <span data-ttu-id="b4b79-243">此外，可使用 X509 证书保护静态密钥。</span><span class="sxs-lookup"><span data-stu-id="b4b79-243">In addition, an X509 certificate can be used to protect keys at rest.</span></span> <span data-ttu-id="b4b79-244">建议使用允许用户上传证书的机制：将证书放置在用户信任的证书存储中，并确保在运行用户应用的所有计算机上都可使用这些证书。</span><span class="sxs-lookup"><span data-stu-id="b4b79-244">Consider a mechanism to allow users to upload certificates: Place certificates into the user's trusted certificate store and ensure they're available on all machines where the user's app runs.</span></span> <span data-ttu-id="b4b79-245">有关详细信息，请参阅[配置数据保护](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-245">See [Configuring Data Protection](xref:security/data-protection/configuration/overview) for details.</span></span>

### <a name="configure-the-iis-application-pool-to-load-the-user-profile"></a><span data-ttu-id="b4b79-246">配置 IIS 应用程序池以加载用户配置文件</span><span class="sxs-lookup"><span data-stu-id="b4b79-246">Configure the IIS Application Pool to load the user profile</span></span>

<span data-ttu-id="b4b79-247">此设置位于应用池“高级设置”下的“进程模型”部分。</span><span class="sxs-lookup"><span data-stu-id="b4b79-247">This setting is in the **Process Model** section under the **Advanced Settings** for the app pool.</span></span> <span data-ttu-id="b4b79-248">将“加载用户配置文件”设置为 `True`。</span><span class="sxs-lookup"><span data-stu-id="b4b79-248">Set Load User Profile to `True`.</span></span> <span data-ttu-id="b4b79-249">这会将密钥存储在用户配置文件目录下，并使用 DPAPI 和特定于用户帐户（用于应用池）的密钥的进行保护。</span><span class="sxs-lookup"><span data-stu-id="b4b79-249">This stores keys under the user profile directory and protects them using DPAPI with a key specific to the user account used for the app pool.</span></span>

### <a name="use-the-file-system-as-a-key-ring-store"></a><span data-ttu-id="b4b79-250">将文件系统用作密钥环存储</span><span class="sxs-lookup"><span data-stu-id="b4b79-250">Use the file system as a key ring store</span></span>

<span data-ttu-id="b4b79-251">调整应用代码，[将文件系统用作密钥环存储](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-251">Adjust the app code to [use the file system as a key ring store](xref:security/data-protection/configuration/overview).</span></span> <span data-ttu-id="b4b79-252">使用 X509 证书保护 keyring，并确保该证书是受信任的证书。</span><span class="sxs-lookup"><span data-stu-id="b4b79-252">Use an X509 certificate to protect the keyring and ensure the certificate is a trusted certificate.</span></span> <span data-ttu-id="b4b79-253">如果它是自签名证书，则将该证书放置于受信任的根存储中。</span><span class="sxs-lookup"><span data-stu-id="b4b79-253">If it's a self signed certificate, place the certificate in the Trusted Root store.</span></span>

<span data-ttu-id="b4b79-254">当在 Web 场中使用 IIS 时：</span><span class="sxs-lookup"><span data-stu-id="b4b79-254">When using IIS in a web farm:</span></span>

* <span data-ttu-id="b4b79-255">使用所有计算机都可以访问的文件共享。</span><span class="sxs-lookup"><span data-stu-id="b4b79-255">Use a file share that all machines can access.</span></span>
* <span data-ttu-id="b4b79-256">将 X509 证书部署到每台计算机。</span><span class="sxs-lookup"><span data-stu-id="b4b79-256">Deploy an X509 certificate to each machine.</span></span> <span data-ttu-id="b4b79-257">[通过代码配置数据保护](xref:security/data-protection/configuration/overview)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-257">Configure [data protection in code](xref:security/data-protection/configuration/overview).</span></span>

### <a name="set-a-machine-wide-policy-for-data-protection"></a><span data-ttu-id="b4b79-258">设置用于数据保护的计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="b4b79-258">Set a machine-wide policy for data protection</span></span>

<span data-ttu-id="b4b79-259">数据保护系统对以下操作提供有限支持：为使用数据保护 API 的所有应用设置默认[计算机范围的策略](xref:security/data-protection/configuration/machine-wide-policy)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-259">The data protection system has limited support for setting a default [machine-wide policy](xref:security/data-protection/configuration/machine-wide-policy) for all apps that consume the Data Protection APIs.</span></span> <span data-ttu-id="b4b79-260">有关详细信息，请参阅[数据保护](xref:security/data-protection/index)文档。</span><span class="sxs-lookup"><span data-stu-id="b4b79-260">See the [data protection](xref:security/data-protection/index) documentation for more details.</span></span>

## <a name="configuration-of-sub-applications"></a><span data-ttu-id="b4b79-261">配置子应用程序</span><span class="sxs-lookup"><span data-stu-id="b4b79-261">Configuration of sub-applications</span></span>

<span data-ttu-id="b4b79-262">在根应用下添加的子应用不应将 ASP.NET Core 模块作为处理程序包含在其中。</span><span class="sxs-lookup"><span data-stu-id="b4b79-262">Sub-apps added under the root app shouldn't include the ASP.NET Core Module as a handler.</span></span> <span data-ttu-id="b4b79-263">如果在子应用的 web.config 文件中将该模块添加为处理程序，则尝试浏览子应用时会收到 500.19（内部服务器错误），即引用错误的配置文件。</span><span class="sxs-lookup"><span data-stu-id="b4b79-263">If the module is added as a handler in a sub-app's *web.config* file, a 500.19 (Internal Server Error) referencing the faulty config file is received when attempting to browse the sub-app.</span></span> <span data-ttu-id="b4b79-264">以下示例显示 ASP.NET Core 子应用的已发布 web.config 文件的内容：</span><span class="sxs-lookup"><span data-stu-id="b4b79-264">The following example shows the contents of a published *web.config* file for an ASP.NET Core sub-app:</span></span>

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

<span data-ttu-id="b4b79-265">在 ASP.NET Core 应用下托管非 ASP.NET Core 子应用时，需在子应用的 web.config 文件中显式删除继承的处理程序：</span><span class="sxs-lookup"><span data-stu-id="b4b79-265">When hosting a non-ASP.NET Core sub-app underneath an ASP.NET Core app, explicitly remove the inherited handler in the sub-app *web.config* file:</span></span>

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

<span data-ttu-id="b4b79-266">有关配置 ASP.NET Core 模块的详细信息，请参阅 [ASP.NET Core 模块简介](xref:fundamentals/servers/aspnet-core-module)和 [ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-266">For more information on configuring the ASP.NET Core Module, see the [Introduction to ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) topic and the [ASP.NET Core Module configuration reference](xref:host-and-deploy/aspnet-core-module).</span></span>

## <a name="configuration-of-iis-with-webconfig"></a><span data-ttu-id="b4b79-267">使用 web.config 配置 IIS</span><span class="sxs-lookup"><span data-stu-id="b4b79-267">Configuration of IIS with web.config</span></span>

<span data-ttu-id="b4b79-268">对于那些应用于反向代理配置的 IIS 功能，IIS 配置受 web.config 的 \<system.webServer> 部分影响。</span><span class="sxs-lookup"><span data-stu-id="b4b79-268">IIS configuration is influenced by the **\<system.webServer>** section of *web.config* for those IIS features that apply to a reverse proxy configuration.</span></span> <span data-ttu-id="b4b79-269">如果用户在系统级别将 IIS 配置为使用动态压缩，可通过应用的 web.config 文件中的 \<urlCompression> 元素为应用禁用该设置。</span><span class="sxs-lookup"><span data-stu-id="b4b79-269">If IIS is configured at the system level to use dynamic compression, that setting can be disabled for an app with the **\<urlCompression>** element in the app's *web.config* file.</span></span> <span data-ttu-id="b4b79-270">有关详细信息，请参阅 [\<system.webServer> 的配置参考](https://docs.microsoft.com/iis/configuration/system.webServer/)、[ASP.NET Core 模块配置参考](xref:host-and-deploy/aspnet-core-module)和 [配合使用 IIS 模块与 ASP.NET Core](xref:host-and-deploy/iis/modules)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-270">For more information, see the [configuration reference for \<system.webServer>](https://docs.microsoft.com/iis/configuration/system.webServer/), [ASP.NET Core Module Configuration Reference](xref:host-and-deploy/aspnet-core-module) and [Using IIS Modules with ASP.NET Core](xref:host-and-deploy/iis/modules).</span></span> <span data-ttu-id="b4b79-271">如果需要为在独立应用池中运行的单个应用设置环境变量（IIS 10.0+ 中支持此操作），请参阅 IIS 参考文档的[环境变量 \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) 主题中的“AppCmd.exe 命令”部分。</span><span class="sxs-lookup"><span data-stu-id="b4b79-271">If there's a need to set environment variables for individual apps running in isolated app pools (supported on IIS 10.0+), see the *AppCmd.exe command* section of the [Environment Variables \<environmentVariables>](/iis/configuration/system.applicationHost/applicationPools/add/environmentVariables/#appcmdexe) topic in the IIS reference documentation.</span></span>

## <a name="configuration-sections-of-webconfig"></a><span data-ttu-id="b4b79-272">web.config 的配置节</span><span class="sxs-lookup"><span data-stu-id="b4b79-272">Configuration sections of web.config</span></span>

<span data-ttu-id="b4b79-273">ASP.NET Core 应用不会使用 web.config 中的 ASP.NET Framework 应用的配置部分进行配置：</span><span class="sxs-lookup"><span data-stu-id="b4b79-273">Configruation sections of ASP.NET Framework apps in *web.config* aren't used by ASP.NET Core apps for configuration:</span></span>

* <span data-ttu-id="b4b79-274">**\<system.web>**</span><span class="sxs-lookup"><span data-stu-id="b4b79-274">**\<system.web>**</span></span>
* <span data-ttu-id="b4b79-275">\<appSettings></span><span class="sxs-lookup"><span data-stu-id="b4b79-275">**\<appSettings>**</span></span>
* <span data-ttu-id="b4b79-276">\<connectionStrings></span><span class="sxs-lookup"><span data-stu-id="b4b79-276">**\<connectionStrings>**</span></span>
* <span data-ttu-id="b4b79-277">\<location></span><span class="sxs-lookup"><span data-stu-id="b4b79-277">**\<location>**</span></span>

<span data-ttu-id="b4b79-278">会使用其他的配置提供程序配置 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="b4b79-278">ASP.NET Core apps are configured using other configuration providers.</span></span> <span data-ttu-id="b4b79-279">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="b4b79-279">For more information, see [Configuration](xref:fundamentals/configuration/index).</span></span>

## <a name="application-pools"></a><span data-ttu-id="b4b79-280">应用程序池</span><span class="sxs-lookup"><span data-stu-id="b4b79-280">Application Pools</span></span>

<span data-ttu-id="b4b79-281">在单个系统上托管多个网站时，需在每个应用自己的应用池中运行各应用，以隔离各应用。</span><span class="sxs-lookup"><span data-stu-id="b4b79-281">When hosting multiple websites on a single system, isolate the apps from each other by running each app in its own app pool.</span></span> <span data-ttu-id="b4b79-282">IIS“添加网站”对话框默认执行此配置。</span><span class="sxs-lookup"><span data-stu-id="b4b79-282">The IIS **Add Website** dialog defaults to this configuration.</span></span> <span data-ttu-id="b4b79-283">提供了站点名称时，该文本会自动传输到“应用程序池”文本框。</span><span class="sxs-lookup"><span data-stu-id="b4b79-283">When **Site name** is provided, the text is automatically transferred to the **Application pool** textbox.</span></span> <span data-ttu-id="b4b79-284">添加网站时，会使用该站点名称创建新的应用池。</span><span class="sxs-lookup"><span data-stu-id="b4b79-284">A new app pool is created using the site name when the website is added.</span></span>

## <a name="application-pool-identity"></a><span data-ttu-id="b4b79-285">应用程序池标识</span><span class="sxs-lookup"><span data-stu-id="b4b79-285">Application Pool Identity</span></span>

<span data-ttu-id="b4b79-286">通过应用池标识帐户，可以在唯一帐户下运行应用，而无需创建和管理域或本地帐户。</span><span class="sxs-lookup"><span data-stu-id="b4b79-286">An app pool identity account allows an app to run under a unique account without having to create and manage domains or local accounts.</span></span> <span data-ttu-id="b4b79-287">在 IIS 8.0+ 上，IIS 管理员工作进程 (WAS) 使用新应用池的名称创建一个虚拟帐户，并默认在此帐户下运行应用池的工作进程。</span><span class="sxs-lookup"><span data-stu-id="b4b79-287">On IIS 8.0+, the IIS Admin Worker Process (WAS) creates a virtual account with the name of the new app pool and runs the app pool's worker processes under this account by default.</span></span> <span data-ttu-id="b4b79-288">在 IIS 管理控制台中，确保应用池“高级设置”下的“标识”设置为使用 ApplicationPoolIdentity：</span><span class="sxs-lookup"><span data-stu-id="b4b79-288">In the IIS Management Console under **Advanced Settings** for the app pool, ensure that the **Identity** is set to use **ApplicationPoolIdentity**:</span></span>

![应用程序池“高级设置”对话框](index/_static/apppool-identity.png)

<span data-ttu-id="b4b79-290">IIS 管理进程使用 Windows 安全系统中应用池的名称创建安全标识符。</span><span class="sxs-lookup"><span data-stu-id="b4b79-290">The IIS management process creates a secure identifier with the name of the app pool in the Windows Security System.</span></span> <span data-ttu-id="b4b79-291">可使用此标识保护资源；但此标识不是真实的用户帐户，不会在 Windows 用户管理控制台中显示。</span><span class="sxs-lookup"><span data-stu-id="b4b79-291">Resources can be secured by using this identity; however, this identity isn't a real user account and won't show up in the Windows User Management Console.</span></span>

<span data-ttu-id="b4b79-292">如果 IIS 工作进程需要对应用的高级访问权限，请为包含该应用的目录修改访问控制列表 (ACL)：</span><span class="sxs-lookup"><span data-stu-id="b4b79-292">If the IIS worker process requires elevated access to the app, modify the Access Control List (ACL) for the directory containing the app:</span></span>

1. <span data-ttu-id="b4b79-293">打开 Windows 资源管理器并导航到目录。</span><span class="sxs-lookup"><span data-stu-id="b4b79-293">Open Windows Explorer and navigate to the directory.</span></span>

2. <span data-ttu-id="b4b79-294">右键单击该目录，然后选择“属性”。</span><span class="sxs-lookup"><span data-stu-id="b4b79-294">Right-click on the directory and select **Properties**.</span></span>

3. <span data-ttu-id="b4b79-295">在“安全”选项卡下，选择“编辑”按钮，然后单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="b4b79-295">Under the **Security** tab, select the **Edit** button and then the **Add** button.</span></span>

4. <span data-ttu-id="b4b79-296">选择“位置”按钮，并确保该系统处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="b4b79-296">Select the **Locations** button and make sure the system is selected.</span></span>

5. <span data-ttu-id="b4b79-297">在“输入要选择的对象名称”文本框中输入“IIS AppPool\DefaultAppPool”。</span><span class="sxs-lookup"><span data-stu-id="b4b79-297">Enter **IIS AppPool\DefaultAppPool** in **Enter the object names to select** textbox.</span></span>

   ![选择应用文件夹的用户或组对话框](index/_static/select-users-or-groups-1.png)

6. <span data-ttu-id="b4b79-299">选择“检查名称”按钮。</span><span class="sxs-lookup"><span data-stu-id="b4b79-299">Select the **Check Names** button.</span></span> <span data-ttu-id="b4b79-300">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="b4b79-300">Select **OK**.</span></span>

   ![选择应用文件夹的用户或组对话框](index/_static/select-users-or-groups-2.png)

<span data-ttu-id="b4b79-302">也可使用 ICACLS 工具通过命令提示符完成此操作：</span><span class="sxs-lookup"><span data-stu-id="b4b79-302">This can also be accomplished via a command prompt using the **ICACLS** tool:</span></span>

```console
ICACLS C:\sites\MyWebApp /grant "IIS AppPool\DefaultAppPool":F
```

## <a name="additional-resources"></a><span data-ttu-id="b4b79-303">其他资源</span><span class="sxs-lookup"><span data-stu-id="b4b79-303">Additional resources</span></span>

* [<span data-ttu-id="b4b79-304">对 IIS 上的 ASP.NET Core 进行故障排除</span><span class="sxs-lookup"><span data-stu-id="b4b79-304">Troubleshoot ASP.NET Core on IIS</span></span>](xref:host-and-deploy/iis/troubleshoot)
* [<span data-ttu-id="b4b79-305">Azure 应用服务和 IIS 上 ASP.NET Core 的常见错误参考</span><span class="sxs-lookup"><span data-stu-id="b4b79-305">Common errors reference for Azure App Service and IIS with ASP.NET Core</span></span>](xref:host-and-deploy/azure-iis-errors-reference)
* [<span data-ttu-id="b4b79-306">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="b4b79-306">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="b4b79-307">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="b4b79-307">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="b4b79-308">配合使用 IIS 模块与 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b4b79-308">Using IIS Modules with ASP.NET Core</span></span>](xref:host-and-deploy/iis/modules)
* [<span data-ttu-id="b4b79-309">ASP.NET Core 简介</span><span class="sxs-lookup"><span data-stu-id="b4b79-309">Introduction to ASP.NET Core</span></span>](../index.md)
* [<span data-ttu-id="b4b79-310">Microsoft IIS 官方网站</span><span class="sxs-lookup"><span data-stu-id="b4b79-310">The Official Microsoft IIS Site</span></span>](https://www.iis.net/)
* [<span data-ttu-id="b4b79-311">Microsoft TechNet 库：Windows Server</span><span class="sxs-lookup"><span data-stu-id="b4b79-311">Microsoft TechNet Library: Windows Server</span></span>](https://docs.microsoft.com/windows-server/windows-server-versions)
