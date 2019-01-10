---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现对调试 ASP.NET Core 应用的支持（在 Windows Server 上的 IIS 后方运行时）。
ms.author: riande
ms.custom: mvc
ms.date: 12/18/2018
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 44570bb28451ce4c5fde12ec77e3856fb5bd3062
ms.sourcegitcommit: 816f39e852a8f453e8682081871a31bc66db153a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2018
ms.locfileid: "53637658"
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="393f4-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="393f4-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="393f4-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)、[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="393f4-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="393f4-105">本文介绍了对调试（在 Windows Server 上的 IIS 后方运行的）ASP.NET Core 应用的 [Visual Studio](https://www.visualstudio.com/vs/) 支持。</span><span class="sxs-lookup"><span data-stu-id="393f4-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="393f4-106">本主题逐步介绍如何启用此功能并设置项目。</span><span class="sxs-lookup"><span data-stu-id="393f4-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="393f4-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="393f4-107">Prerequisites</span></span>

* [<span data-ttu-id="393f4-108">Visual Studio（适用于 Windows）</span><span class="sxs-lookup"><span data-stu-id="393f4-108">Visual Studio for Windows</span></span>](https://www.microsoft.com/net/download/windows)
* <span data-ttu-id="393f4-109">ASP.NET 和 Web 开发工作负荷</span><span class="sxs-lookup"><span data-stu-id="393f4-109">**ASP.NET and web development** workload</span></span>
* <span data-ttu-id="393f4-110">.NET Core 跨平台开发工作负荷</span><span class="sxs-lookup"><span data-stu-id="393f4-110">**.NET Core cross-platform development** workload</span></span>
* <span data-ttu-id="393f4-111">X.509 安全证书</span><span class="sxs-lookup"><span data-stu-id="393f4-111">X.509 security certificate</span></span>

## <a name="enable-iis"></a><span data-ttu-id="393f4-112">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="393f4-112">Enable IIS</span></span>

1. <span data-ttu-id="393f4-113">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="393f4-113">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="393f4-114">选中“Internet Information Services”复选框。</span><span class="sxs-lookup"><span data-stu-id="393f4-114">Select the **Internet Information Services** check box.</span></span>

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="393f4-116">IIS 安装可能需要重启系统。</span><span class="sxs-lookup"><span data-stu-id="393f4-116">The IIS installation may require a system restart.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="393f4-117">配置 IIS</span><span class="sxs-lookup"><span data-stu-id="393f4-117">Configure IIS</span></span>

<span data-ttu-id="393f4-118">IIS 必须具有具备以下配置的网站：</span><span class="sxs-lookup"><span data-stu-id="393f4-118">IIS must have a website configured with the following:</span></span>

* <span data-ttu-id="393f4-119">与应用启动配置文件 URL 主机名匹配的主机名。</span><span class="sxs-lookup"><span data-stu-id="393f4-119">A host name that matches the app's launch profile URL host name.</span></span>
* <span data-ttu-id="393f4-120">使用分配的证书绑定端口 443。</span><span class="sxs-lookup"><span data-stu-id="393f4-120">Binding for port 443 with an assigned certificate.</span></span>

<span data-ttu-id="393f4-121">例如，所添加网站的主机名设置为“localhost”（在本主题之后部分启动配置文件也将使用“localhost”）。</span><span class="sxs-lookup"><span data-stu-id="393f4-121">For example, the **Host name** for an added website is set to "localhost" (the launch profile will also use "localhost" later in this topic).</span></span> <span data-ttu-id="393f4-122">端口设置为“443”(HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="393f4-122">The port is set to "443" (HTTPS).</span></span> <span data-ttu-id="393f4-123">“IIS Express 开发证书”已分配给该网站，但可使用任何有效的证书：</span><span class="sxs-lookup"><span data-stu-id="393f4-123">The **IIS Express Development Certificate** is assigned to the website, but any valid certificate works:</span></span>

![在 IIS 中添加网站窗口，显示已分配证书的端口 443 上 localhost 的绑定集。](development-time-iis-support/_static/add-website-window.png)

<span data-ttu-id="393f4-125">如果 IIS 安装已经有一个默认网站，且其主机名与应用的启动配置文件 URL 主机名相匹配：</span><span class="sxs-lookup"><span data-stu-id="393f4-125">If the IIS installation already has a **Default Web Site** with a host name that matches the app's launch profile URL host name:</span></span>

* <span data-ttu-id="393f4-126">为端口 443 (HTTPS) 添加端口绑定。</span><span class="sxs-lookup"><span data-stu-id="393f4-126">Add a port binding for port 443 (HTTPS).</span></span>
* <span data-ttu-id="393f4-127">向网站分配一个有效证书。</span><span class="sxs-lookup"><span data-stu-id="393f4-127">Assign a valid certificate to the website.</span></span>

## <a name="enable-development-time-iis-support-in-visual-studio"></a><span data-ttu-id="393f4-128">在 Visual Studio 中启用开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="393f4-128">Enable development-time IIS support in Visual Studio</span></span>

1. <span data-ttu-id="393f4-129">启动 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="393f4-129">Launch the Visual Studio installer.</span></span>
1. <span data-ttu-id="393f4-130">选择“开发时 IIS 支持”组件。</span><span class="sxs-lookup"><span data-stu-id="393f4-130">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="393f4-131">该组件在“ASP.NET 和 Web 开发”工作负荷的“摘要”面板中列为可选。</span><span class="sxs-lookup"><span data-stu-id="393f4-131">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="393f4-132">该组件将安装 [ASP.NET Core 模块](xref:host-and-deploy/aspnet-core-module)，该模块是运行具有 IIS 的 ASP.NET Core 应用所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="393f4-132">The component installs the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps with IIS.</span></span>

![修改 Visual Studio 功能：“工作负荷”选项卡处于选中状态。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="393f4-136">配置项目</span><span class="sxs-lookup"><span data-stu-id="393f4-136">Configure the project</span></span>

### <a name="https-redirection"></a><span data-ttu-id="393f4-137">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="393f4-137">HTTPS redirection</span></span>

<span data-ttu-id="393f4-138">对于新项目，请选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框：</span><span class="sxs-lookup"><span data-stu-id="393f4-138">For a new project, select the check box to **Configure for HTTPS** in the **New ASP.NET Core Web Application** window:</span></span>

![选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框。](development-time-iis-support/_static/new-app.png)

<span data-ttu-id="393f4-140">在现有项目中，通过调用 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 扩展方法在 `Startup.Configure` 中使用 HTTPS 重定向中间件：</span><span class="sxs-lookup"><span data-stu-id="393f4-140">In an existing project, use HTTPS Redirection Middleware in `Startup.Configure` by calling the [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) extension method:</span></span>

```csharp
public void Configure(IApplicationBuilder app, IHostingEnvironment env)
{
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Error");
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseCookiePolicy();

    app.UseMvc();
}
```

### <a name="iis-launch-profile"></a><span data-ttu-id="393f4-141">IIS 启动配置文件</span><span class="sxs-lookup"><span data-stu-id="393f4-141">IIS launch profile</span></span>

<span data-ttu-id="393f4-142">创建新的启动配置文件以添加开发时 IIS 支持：</span><span class="sxs-lookup"><span data-stu-id="393f4-142">Create a new launch profile to add development-time IIS support:</span></span>

1. <span data-ttu-id="393f4-143">对于配置文件，请选择“新建”按钮。</span><span class="sxs-lookup"><span data-stu-id="393f4-143">For **Profile**, select the **New** button.</span></span> <span data-ttu-id="393f4-144">在弹出窗口中将该配置文件命名为“IIS”。</span><span class="sxs-lookup"><span data-stu-id="393f4-144">Name the profile "IIS" in the popup window.</span></span> <span data-ttu-id="393f4-145">选择“确定”创建配置文件。</span><span class="sxs-lookup"><span data-stu-id="393f4-145">Select **OK** to create the profile.</span></span>
1. <span data-ttu-id="393f4-146">对于“启动”设置，请从列表中选择“IIS”。</span><span class="sxs-lookup"><span data-stu-id="393f4-146">For the **Launch** setting, select **IIS** from the list.</span></span>
1. <span data-ttu-id="393f4-147">选中“启动浏览器”复选框并提供终结点 URL。</span><span class="sxs-lookup"><span data-stu-id="393f4-147">Select the check box for **Launch browser** and provide the endpoint URL.</span></span> <span data-ttu-id="393f4-148">使用 HTTPS 协议。</span><span class="sxs-lookup"><span data-stu-id="393f4-148">Use the HTTPS protocol.</span></span> <span data-ttu-id="393f4-149">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="393f4-149">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="393f4-150">在“环境变量”部分中，选择“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="393f4-150">In the **Environment variables** section, select the **Add** button.</span></span> <span data-ttu-id="393f4-151">提供一个密钥为 `ASPNETCORE_ENVIRONMENT` 和值为 `Development` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="393f4-151">Provide an environment variable with a key of `ASPNETCORE_ENVIRONMENT` and a value of `Development`.</span></span>
1. <span data-ttu-id="393f4-152">在“Web 服务器设置”区域中，设置“应用 URL”。</span><span class="sxs-lookup"><span data-stu-id="393f4-152">In the **Web Server Settings** area, set the **App URL**.</span></span> <span data-ttu-id="393f4-153">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="393f4-153">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="393f4-154">保存配置文件。</span><span class="sxs-lookup"><span data-stu-id="393f4-154">Save the profile.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="393f4-159">或者，可以将启动配置文件手动添加到应用中的 [launchSettings.json](http://json.schemastore.org/launchsettings) 文件：</span><span class="sxs-lookup"><span data-stu-id="393f4-159">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iis": {
      "applicationUrl": "https://localhost/WebApplication1",
      "sslPort": 0
    }
  },
  "profiles": {
    "IIS": {
      "commandName": "IIS",
      "launchBrowser": true,
      "launchUrl": "https://localhost/WebApplication1",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

## <a name="run-the-project"></a><span data-ttu-id="393f4-160">运行该项目</span><span class="sxs-lookup"><span data-stu-id="393f4-160">Run the project</span></span>

<span data-ttu-id="393f4-161">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="393f4-161">In Visual Studio:</span></span>

* <span data-ttu-id="393f4-162">确认已将生成配置下拉列表设置为“调试”。</span><span class="sxs-lookup"><span data-stu-id="393f4-162">Confirm that the build configuration drop-down list is set to **Debug**.</span></span>
* <span data-ttu-id="393f4-163">将“运行”按钮设置为 IIS 配置文件，然后选择此按钮以启动该应用。</span><span class="sxs-lookup"><span data-stu-id="393f4-163">Set the Run button to the **IIS** profile and select the button to start the app.</span></span>

![将 VS 工具栏中的“运行”按钮设置为 IIS 配置文件，并将生成配置下拉列表设置为“发布”。](development-time-iis-support/_static/toolbar.png)

<span data-ttu-id="393f4-165">如果不以管理员身份运行，Visual Studio 可能会提示重启。</span><span class="sxs-lookup"><span data-stu-id="393f4-165">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="393f4-166">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="393f4-166">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="393f4-167">如果使用不受信任的开发证书，则浏览器可能会要求你为不受信任的证书创建异常。</span><span class="sxs-lookup"><span data-stu-id="393f4-167">If an untrusted development certificate is used, the browser may require you to create an exception for the untrusted certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="393f4-168">通过[仅我的代码](/visualstudio/debugger/just-my-code)调试“发布”生成配置，从而导致降低编译器优化体验。</span><span class="sxs-lookup"><span data-stu-id="393f4-168">Debugging a Release build configuration with [Just My Code](/visualstudio/debugger/just-my-code) and compiler optimizations results in a degraded experience.</span></span> <span data-ttu-id="393f4-169">例如，不会遇到断点。</span><span class="sxs-lookup"><span data-stu-id="393f4-169">For example, break points aren't hit.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="393f4-170">其他资源</span><span class="sxs-lookup"><span data-stu-id="393f4-170">Additional resources</span></span>

* [<span data-ttu-id="393f4-171">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="393f4-171">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="393f4-172">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="393f4-172">Introduction to ASP.NET Core Module</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="393f4-173">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="393f4-173">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="393f4-174">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="393f4-174">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
