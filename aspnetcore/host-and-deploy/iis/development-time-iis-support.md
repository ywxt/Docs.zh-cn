---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现对调试 ASP.NET Core 应用的支持（在 Windows Server 上的 IIS 后方运行时）。
ms.author: riande
ms.custom: mvc
ms.date: 05/14/2018
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: eb8b4369d6d5434adbac187f59b18d7a2b80055c
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277649"
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="f9e40-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="f9e40-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="f9e40-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)、[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="f9e40-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="f9e40-105">本文介绍了对调试（在 Windows Server 上的 IIS 后方运行的）ASP.NET Core 应用的 [Visual Studio](https://www.visualstudio.com/vs/) 支持。</span><span class="sxs-lookup"><span data-stu-id="f9e40-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="f9e40-106">本主题逐步介绍如何启用此功能并设置项目。</span><span class="sxs-lookup"><span data-stu-id="f9e40-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9e40-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="f9e40-107">Prerequisites</span></span>

* [<span data-ttu-id="f9e40-108">Visual Studio（适用于 Windows）</span><span class="sxs-lookup"><span data-stu-id="f9e40-108">Visual Studio for Windows</span></span>](https://www.microsoft.com/net/download/windows)
* <span data-ttu-id="f9e40-109">ASP.NET 和 Web 开发工作负荷</span><span class="sxs-lookup"><span data-stu-id="f9e40-109">**ASP.NET and web development** workload</span></span>
* <span data-ttu-id="f9e40-110">.NET Core 跨平台开发工作负荷</span><span class="sxs-lookup"><span data-stu-id="f9e40-110">**.NET Core cross-platform development** workload</span></span>
* <span data-ttu-id="f9e40-111">X.509 安全证书</span><span class="sxs-lookup"><span data-stu-id="f9e40-111">X.509 security certificate</span></span>

## <a name="enable-iis"></a><span data-ttu-id="f9e40-112">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="f9e40-112">Enable IIS</span></span>

1. <span data-ttu-id="f9e40-113">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="f9e40-113">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="f9e40-114">选中“Internet Information Services”复选框。</span><span class="sxs-lookup"><span data-stu-id="f9e40-114">Select the **Internet Information Services** check box.</span></span>

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="f9e40-116">IIS 安装可能需要重启系统。</span><span class="sxs-lookup"><span data-stu-id="f9e40-116">The IIS installation may require a system restart.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="f9e40-117">配置 IIS</span><span class="sxs-lookup"><span data-stu-id="f9e40-117">Configure IIS</span></span>

<span data-ttu-id="f9e40-118">IIS 必须具有具备以下配置的网站：</span><span class="sxs-lookup"><span data-stu-id="f9e40-118">IIS must have a website configured with the following:</span></span>

* <span data-ttu-id="f9e40-119">与应用启动配置文件 URL 主机名匹配的主机名。</span><span class="sxs-lookup"><span data-stu-id="f9e40-119">A host name that matches the app's launch profile URL host name.</span></span>
* <span data-ttu-id="f9e40-120">使用分配的证书绑定端口 443。</span><span class="sxs-lookup"><span data-stu-id="f9e40-120">Binding for port 443 with an assigned certificate.</span></span>

<span data-ttu-id="f9e40-121">例如，所添加网站的主机名设置为“localhost”（在本主题之后部分启动配置文件也将使用“localhost”）。</span><span class="sxs-lookup"><span data-stu-id="f9e40-121">For example, the **Host name** for an added website is set to "localhost" (the launch profile will also use "localhost" later in this topic).</span></span> <span data-ttu-id="f9e40-122">端口设置为“443”(HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="f9e40-122">The port is set to "443" (HTTPS).</span></span> <span data-ttu-id="f9e40-123">“IIS Express 开发证书”已分配给该网站，但可使用任何有效的证书：</span><span class="sxs-lookup"><span data-stu-id="f9e40-123">The **IIS Express Development Certificate** is assigned to the website, but any valid certificate works:</span></span>

![在 IIS 中添加网站窗口，显示已分配证书的端口 443 上 localhost 的绑定集。](development-time-iis-support/_static/add-website-window.png)

<span data-ttu-id="f9e40-125">如果 IIS 安装已经有一个默认网站，且其主机名与应用的启动配置文件 URL 主机名相匹配：</span><span class="sxs-lookup"><span data-stu-id="f9e40-125">If the IIS installation already has a **Default Web Site** with a host name that matches the app's launch profile URL host name:</span></span>

* <span data-ttu-id="f9e40-126">为端口 443 (HTTPS) 添加端口绑定。</span><span class="sxs-lookup"><span data-stu-id="f9e40-126">Add a port binding for port 443 (HTTPS).</span></span>
* <span data-ttu-id="f9e40-127">向网站分配一个有效证书。</span><span class="sxs-lookup"><span data-stu-id="f9e40-127">Assign a valid certificate to the website.</span></span>

## <a name="enable-development-time-iis-support-in-visual-studio"></a><span data-ttu-id="f9e40-128">在 Visual Studio 中启用开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="f9e40-128">Enable development-time IIS support in Visual Studio</span></span>

1. <span data-ttu-id="f9e40-129">启动 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="f9e40-129">Launch the Visual Studio installer.</span></span>
1. <span data-ttu-id="f9e40-130">选择“开发时 IIS 支持”组件。</span><span class="sxs-lookup"><span data-stu-id="f9e40-130">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="f9e40-131">该组件在“ASP.NET 和 Web 开发”工作负荷的“摘要”面板中列为可选。</span><span class="sxs-lookup"><span data-stu-id="f9e40-131">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="f9e40-132">此组件将安装 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，该模块是在反向代理配置中的 IIS 的后方运行 ASP.NET Core 应用所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="f9e40-132">The component installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps behind IIS in a reverse proxy configuration.</span></span>

![修改 Visual Studio 功能：选择“工作负荷”选项卡。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="f9e40-136">配置项目</span><span class="sxs-lookup"><span data-stu-id="f9e40-136">Configure the project</span></span>

### <a name="https-redirection"></a><span data-ttu-id="f9e40-137">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="f9e40-137">HTTPS redirection</span></span>

<span data-ttu-id="f9e40-138">对于新项目，请选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框：</span><span class="sxs-lookup"><span data-stu-id="f9e40-138">For a new project, select the check box to **Configure for HTTPS** in the **New ASP.NET Core Web Application** window:</span></span>

![选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框。](development-time-iis-support/_static/new-app.png)

<span data-ttu-id="f9e40-140">在现有项目中，通过调用 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 扩展方法在 `Startup.Configure` 中使用 HTTPS 重定向中间件：</span><span class="sxs-lookup"><span data-stu-id="f9e40-140">In an existing project, use HTTPS Redirection Middleware in `Startup.Configure` by calling the [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) extension method:</span></span>

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

### <a name="iis-launch-profile"></a><span data-ttu-id="f9e40-141">IIS 启动配置文件</span><span class="sxs-lookup"><span data-stu-id="f9e40-141">IIS launch profile</span></span>

<span data-ttu-id="f9e40-142">创建新的启动配置文件以添加开发时 IIS 支持：</span><span class="sxs-lookup"><span data-stu-id="f9e40-142">Create a new launch profile to add development-time IIS support:</span></span>

1. <span data-ttu-id="f9e40-143">对于配置文件，请选择“新建”按钮。</span><span class="sxs-lookup"><span data-stu-id="f9e40-143">For **Profile**, select the **New** button.</span></span> <span data-ttu-id="f9e40-144">在弹出窗口中将该配置文件命名为“IIS”。</span><span class="sxs-lookup"><span data-stu-id="f9e40-144">Name the profile "IIS" in the popup window.</span></span> <span data-ttu-id="f9e40-145">选择“确定”创建配置文件。</span><span class="sxs-lookup"><span data-stu-id="f9e40-145">Select **OK** to create the profile.</span></span>
1. <span data-ttu-id="f9e40-146">对于“启动”设置，请从列表中选择“IIS”。</span><span class="sxs-lookup"><span data-stu-id="f9e40-146">For the **Launch** setting, select **IIS** from the list.</span></span>
1. <span data-ttu-id="f9e40-147">选中“启动浏览器”复选框并提供终结点 URL。</span><span class="sxs-lookup"><span data-stu-id="f9e40-147">Select the check box for **Launch browser** and provide the endpoint URL.</span></span> <span data-ttu-id="f9e40-148">使用 HTTPS 协议。</span><span class="sxs-lookup"><span data-stu-id="f9e40-148">Use the HTTPS protocol.</span></span> <span data-ttu-id="f9e40-149">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="f9e40-149">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="f9e40-150">在“环境变量”部分中，选择“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="f9e40-150">In the **Environment variables** section, select the **Add** button.</span></span> <span data-ttu-id="f9e40-151">提供一个密钥为 `ASPNETCORE_ENVIRONMENT` 和值为 `Development` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="f9e40-151">Provide an environment variable with a key of `ASPNETCORE_ENVIRONMENT` and a value of `Development`.</span></span>
1. <span data-ttu-id="f9e40-152">在“Web 服务器设置”区域中，设置“应用 URL”。</span><span class="sxs-lookup"><span data-stu-id="f9e40-152">In the **Web Server Settings** area, set the **App URL**.</span></span> <span data-ttu-id="f9e40-153">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="f9e40-153">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="f9e40-154">保存配置文件。</span><span class="sxs-lookup"><span data-stu-id="f9e40-154">Save the profile.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="f9e40-159">或者，可以将启动配置文件手动添加到应用中的 [launchSettings.json](http://json.schemastore.org/launchsettings) 文件：</span><span class="sxs-lookup"><span data-stu-id="f9e40-159">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

## <a name="run-the-project"></a><span data-ttu-id="f9e40-160">运行该项目</span><span class="sxs-lookup"><span data-stu-id="f9e40-160">Run the project</span></span>

<span data-ttu-id="f9e40-161">在 VS 用户界面中，将“运行”按钮设置为 IIS 配置文件，然后选择此按钮以启动该应用：</span><span class="sxs-lookup"><span data-stu-id="f9e40-161">In the VS UI, set the Run button to the **IIS** profile and select the button to start the app:</span></span>

![运行 VS 工具栏中设置为“IIS”配置文件的按钮。](development-time-iis-support/_static/toolbar.png)

<span data-ttu-id="f9e40-163">如果不以管理员身份运行，Visual Studio 可能会提示重启。</span><span class="sxs-lookup"><span data-stu-id="f9e40-163">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="f9e40-164">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f9e40-164">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="f9e40-165">如果使用不受信任的开发证书，则浏览器可能会要求你为不受信任的证书创建异常。</span><span class="sxs-lookup"><span data-stu-id="f9e40-165">If an untrusted development certificate is used, the browser may require you to create an exception for the untrusted certificate.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9e40-166">其他资源</span><span class="sxs-lookup"><span data-stu-id="f9e40-166">Additional resources</span></span>

* [<span data-ttu-id="f9e40-167">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="f9e40-167">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="f9e40-168">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="f9e40-168">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="f9e40-169">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="f9e40-169">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="f9e40-170">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="f9e40-170">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
