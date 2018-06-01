---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现对调试 ASP.NET Core 应用的支持（在 Windows Server 上的 IIS 后方运行时）。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/14/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/iis/development-time-iis-support
ms.openlocfilehash: 0bf4585d44e61c5e7e5b89ce9d8dfdfa10d5460e
ms.sourcegitcommit: a66f38071e13685bbe59d48d22aa141ac702b432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
ms.locfileid: "34233074"
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="6ce1d-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="6ce1d-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="6ce1d-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)、[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="6ce1d-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="6ce1d-105">本文介绍了对调试（在 Windows Server 上的 IIS 后方运行的）ASP.NET Core 应用的 [Visual Studio](https://www.visualstudio.com/vs/) 支持。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="6ce1d-106">本主题逐步介绍如何启用此功能并设置项目。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ce1d-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="6ce1d-107">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a><span data-ttu-id="6ce1d-108">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="6ce1d-108">Enable IIS</span></span>

1. <span data-ttu-id="6ce1d-109">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-109">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="6ce1d-110">选中“Internet Information Services”复选框。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-110">Select the **Internet Information Services** check box.</span></span>

![Windows 功能将选中的“Internet Information Services”复选框显示为实心方形（而不是复选标记），指示已启用某些 IIS 功能](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="6ce1d-112">IIS 安装可能需要重启系统。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-112">The IIS installation may require a system restart.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="6ce1d-113">配置 IIS</span><span class="sxs-lookup"><span data-stu-id="6ce1d-113">Configure IIS</span></span>

<span data-ttu-id="6ce1d-114">IIS 必须具有具备以下配置的网站：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-114">IIS must have a website configured with the following:</span></span>

* <span data-ttu-id="6ce1d-115">与应用启动配置文件 URL 主机名匹配的主机名。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-115">A host name that matches the app's launch profile URL host name.</span></span>
* <span data-ttu-id="6ce1d-116">使用分配的证书绑定端口 443。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-116">Binding for port 443 with an assigned certificate.</span></span>

<span data-ttu-id="6ce1d-117">例如，所添加网站的主机名设置为“localhost”（在本主题之后部分启动配置文件也将使用“localhost”）。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-117">For example, the **Host name** for an added website is set to "localhost" (the launch profile will also use "localhost" later in this topic).</span></span> <span data-ttu-id="6ce1d-118">端口设置为“443”(HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-118">The port is set to "443" (HTTPS).</span></span> <span data-ttu-id="6ce1d-119">“IIS Express 开发证书”已分配给该网站，但可使用任何有效的证书：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-119">The **IIS Express Development Certificate** is assigned to the website, but any valid certificate works:</span></span>

![在 IIS 中添加网站窗口，显示已分配证书的端口 443 上 localhost 的绑定集。](development-time-iis-support/_static/add-website-window.png)

<span data-ttu-id="6ce1d-121">如果 IIS 安装已经有一个默认网站，且其主机名与应用的启动配置文件 URL 主机名相匹配：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-121">If the IIS installation already has a **Default Web Site** with a host name that matches the app's launch profile URL host name:</span></span>

* <span data-ttu-id="6ce1d-122">为端口 443 (HTTPS) 添加端口绑定。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-122">Add a port binding for port 443 (HTTPS).</span></span>
* <span data-ttu-id="6ce1d-123">向网站分配一个有效证书。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-123">Assign a valid certificate to the website.</span></span>

## <a name="enable-development-time-iis-support-in-visual-studio"></a><span data-ttu-id="6ce1d-124">在 Visual Studio 中启用开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="6ce1d-124">Enable development-time IIS support in Visual Studio</span></span>

1. <span data-ttu-id="6ce1d-125">启动 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-125">Launch the Visual Studio installer.</span></span>
1. <span data-ttu-id="6ce1d-126">选择“开发时 IIS 支持”组件。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-126">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="6ce1d-127">该组件在“ASP.NET 和 Web 开发”工作负荷的“摘要”面板中列为可选。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-127">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="6ce1d-128">此组件将安装 [ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)，该模块是在反向代理配置中的 IIS 的后方运行 ASP.NET Core 应用所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-128">The component installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps behind IIS in a reverse proxy configuration.</span></span>

![修改 Visual Studio 功能：选择“工作负荷”选项卡。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="6ce1d-132">配置项目</span><span class="sxs-lookup"><span data-stu-id="6ce1d-132">Configure the project</span></span>

### <a name="https-redirection"></a><span data-ttu-id="6ce1d-133">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="6ce1d-133">HTTPS redirection</span></span>

<span data-ttu-id="6ce1d-134">对于新项目，请选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-134">For a new project, select the check box to **Configure for HTTPS** in the **New ASP.NET Core Web Application** window:</span></span>

![选中“新建 ASP.NET Core Web 应用程序”窗口中的“配置 HTTPS”复选框。](development-time-iis-support/_static/new-app.png)

<span data-ttu-id="6ce1d-136">在现有项目中，通过调用 [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) 扩展方法在 `Startup.Configure` 中使用 HTTPS 重定向中间件：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-136">In an existing project, use HTTPS Redirection Middleware in `Startup.Configure` by calling the [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) extension method:</span></span>

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

### <a name="iis-launch-profile"></a><span data-ttu-id="6ce1d-137">IIS 启动配置文件</span><span class="sxs-lookup"><span data-stu-id="6ce1d-137">IIS launch profile</span></span>

<span data-ttu-id="6ce1d-138">创建新的启动配置文件以添加开发时 IIS 支持：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-138">Create a new launch profile to add development-time IIS support:</span></span>

1. <span data-ttu-id="6ce1d-139">对于配置文件，请选择“新建”按钮。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-139">For **Profile**, select the **New** button.</span></span> <span data-ttu-id="6ce1d-140">在弹出窗口中将该配置文件命名为“IIS”。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-140">Name the profile "IIS" in the popup window.</span></span> <span data-ttu-id="6ce1d-141">选择“确定”创建配置文件。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-141">Select **OK** to create the profile.</span></span>
1. <span data-ttu-id="6ce1d-142">对于“启动”设置，请从列表中选择“IIS”。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-142">For the **Launch** setting, select **IIS** from the list.</span></span>
1. <span data-ttu-id="6ce1d-143">选中“启动浏览器”复选框并提供终结点 URL。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-143">Select the check box for **Launch browser** and provide the endpoint URL.</span></span> <span data-ttu-id="6ce1d-144">使用 HTTPS 协议。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-144">Use the HTTPS protocol.</span></span> <span data-ttu-id="6ce1d-145">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-145">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="6ce1d-146">在“环境变量”部分中，选择“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-146">In the **Environment variables** section, select the **Add** button.</span></span> <span data-ttu-id="6ce1d-147">提供一个密钥为 `ASPNETCORE_ENVIRONMENT` 和值为 `Development` 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-147">Provide an environment variable with a key of `ASPNETCORE_ENVIRONMENT` and a value of `Development`.</span></span>
1. <span data-ttu-id="6ce1d-148">在“Web 服务器设置”区域中，设置“应用 URL”。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-148">In the **Web Server Settings** area, set the **App URL**.</span></span> <span data-ttu-id="6ce1d-149">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-149">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="6ce1d-150">保存配置文件。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-150">Save the profile.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="6ce1d-155">或者，可以将启动配置文件手动添加到应用中的 [launchSettings.json](http://json.schemastore.org/launchsettings) 文件：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-155">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

## <a name="run-the-project"></a><span data-ttu-id="6ce1d-156">运行该项目</span><span class="sxs-lookup"><span data-stu-id="6ce1d-156">Run the project</span></span>

<span data-ttu-id="6ce1d-157">在 VS 用户界面中，将“运行”按钮设置为 IIS 配置文件，然后选择此按钮以启动该应用：</span><span class="sxs-lookup"><span data-stu-id="6ce1d-157">In the VS UI, set the Run button to the **IIS** profile and select the button to start the app:</span></span>

![运行 VS 工具栏中设置为“IIS”配置文件的按钮。](development-time-iis-support/_static/toolbar.png)

<span data-ttu-id="6ce1d-159">如果不以管理员身份运行，Visual Studio 可能会提示重启。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-159">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="6ce1d-160">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-160">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="6ce1d-161">如果使用不受信任的开发证书，则浏览器可能会要求你为不受信任的证书创建异常。</span><span class="sxs-lookup"><span data-stu-id="6ce1d-161">If an untrusted development certificate is used, the browser may require you to create an exception for the untrusted certificate.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6ce1d-162">其他资源</span><span class="sxs-lookup"><span data-stu-id="6ce1d-162">Additional resources</span></span>

* [<span data-ttu-id="6ce1d-163">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="6ce1d-163">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="6ce1d-164">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="6ce1d-164">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="6ce1d-165">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="6ce1d-165">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="6ce1d-166">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="6ce1d-166">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
