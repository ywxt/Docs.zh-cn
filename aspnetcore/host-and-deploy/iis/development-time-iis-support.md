---
title: Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持
author: shirhatti
description: 发现的用于调试 ASP.NET Core 应用时在 Windows Server 上运行之后 IIS 的支持。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="development-time-iis-support-in-visual-studio-for-aspnet-core"></a><span data-ttu-id="dff38-103">Visual Studio 中针对 ASP.NET Core 的开发时 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="dff38-103">Development-time IIS support in Visual Studio for ASP.NET Core</span></span>

<span data-ttu-id="dff38-104">通过[Sourabh Shirhatti](https://twitter.com/sshirhatti)和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="dff38-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="dff38-105">本指南介绍了[Visual Studio](https://www.visualstudio.com/vs/)支持的用于调试在 IIS 后面运行 Windows Server 上的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="dff38-105">This article describes [Visual Studio](https://www.visualstudio.com/vs/) support for debugging ASP.NET Core apps running behind IIS on Windows Server.</span></span> <span data-ttu-id="dff38-106">本主题将指导完成启用此功能，并设置项目。</span><span class="sxs-lookup"><span data-stu-id="dff38-106">This topic walks through enabling this feature and setting up a project.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dff38-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="dff38-107">Prerequisites</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="enable-iis"></a><span data-ttu-id="dff38-108">启用 IIS</span><span class="sxs-lookup"><span data-stu-id="dff38-108">Enable IIS</span></span>

1. <span data-ttu-id="dff38-109">导航到“控制面板” > “程序” > “程序和功能” > “打开或关闭 Windows 功能”（位于屏幕左侧）。</span><span class="sxs-lookup"><span data-stu-id="dff38-109">Navigate to **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off** (left side of the screen).</span></span>
1. <span data-ttu-id="dff38-110">选择**Internet Information Services**复选框。</span><span class="sxs-lookup"><span data-stu-id="dff38-110">Select the **Internet Information Services** check box.</span></span>

![检查为黑色方块 （不复选标记） 后，该值指示启用了 IIS 功能的某些 Windows 功能显示 Internet Information Services 复选框](development-time-iis-support/_static/enable_iis.png)

<span data-ttu-id="dff38-112">IIS 安装可能需要重新启动系统。</span><span class="sxs-lookup"><span data-stu-id="dff38-112">The IIS installation may require a system restart.</span></span>

## <a name="configure-iis"></a><span data-ttu-id="dff38-113">配置 IIS</span><span class="sxs-lookup"><span data-stu-id="dff38-113">Configure IIS</span></span>

<span data-ttu-id="dff38-114">IIS 必须拥有的网站进行以下配置：</span><span class="sxs-lookup"><span data-stu-id="dff38-114">IIS must have a website configured with the following:</span></span>

* <span data-ttu-id="dff38-115">应用程序的发布配置文件 URL 主机名称相匹配的主机名称。</span><span class="sxs-lookup"><span data-stu-id="dff38-115">A host name that matches the app's launch profile URL host name.</span></span>
* <span data-ttu-id="dff38-116">端口 443 与分配的证书的绑定。</span><span class="sxs-lookup"><span data-stu-id="dff38-116">Binding for port 443 with an assigned certificate.</span></span>

<span data-ttu-id="dff38-117">例如，**主机名**添加的网站设置为"localhost"（启动配置文件将还使用"localhost"本主题中的更高版本）。</span><span class="sxs-lookup"><span data-stu-id="dff38-117">For example, the **Host name** for an added website is set to "localhost" (the launch profile will also use "localhost" later in this topic).</span></span> <span data-ttu-id="dff38-118">端口设置为"443"(HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="dff38-118">The port is set to "443" (HTTPS).</span></span> <span data-ttu-id="dff38-119">**IIS Express 开发证书**分配给网站，但任何有效的证书工作原理：</span><span class="sxs-lookup"><span data-stu-id="dff38-119">The **IIS Express Development Certificate** is assigned to the website, but any valid certificate works:</span></span>

![显示分配的证书为 localhost 设置的绑定在端口 443 上的 IIS 中添加网站窗口。](development-time-iis-support/_static/add-website-window.png)

<span data-ttu-id="dff38-121">如果 IIS 安装已具有**Default Web Site**使用与应用程序的发布配置文件 URL 主机名匹配的主机名：</span><span class="sxs-lookup"><span data-stu-id="dff38-121">If the IIS installation already has a **Default Web Site** with a host name that matches the app's launch profile URL host name:</span></span>

* <span data-ttu-id="dff38-122">添加为端口 443 (HTTPS) 的端口绑定。</span><span class="sxs-lookup"><span data-stu-id="dff38-122">Add a port binding for port 443 (HTTPS).</span></span>
* <span data-ttu-id="dff38-123">向网站分配一个有效的证书。</span><span class="sxs-lookup"><span data-stu-id="dff38-123">Assign a valid certificate to the website.</span></span>

## <a name="enable-development-time-iis-support-in-visual-studio"></a><span data-ttu-id="dff38-124">启用 Visual Studio 中的开发时间 IIS 支持</span><span class="sxs-lookup"><span data-stu-id="dff38-124">Enable development-time IIS support in Visual Studio</span></span>

1. <span data-ttu-id="dff38-125">启动 Visual Studio 安装程序。</span><span class="sxs-lookup"><span data-stu-id="dff38-125">Launch the Visual Studio installer.</span></span>
1. <span data-ttu-id="dff38-126">选择**IIS 支持的开发时间**组件。</span><span class="sxs-lookup"><span data-stu-id="dff38-126">Select the **Development time IIS support** component.</span></span> <span data-ttu-id="dff38-127">列出为可选中了该组件**摘要**面板**ASP.NET 和 web 开发**工作负荷。</span><span class="sxs-lookup"><span data-stu-id="dff38-127">The component is listed as optional in the **Summary** panel for the **ASP.NET and web development** workload.</span></span> <span data-ttu-id="dff38-128">组件安装[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)，即反向代理配置中运行 ASP.NET Core 后面 IIS 的应用所需的本机 IIS 模块。</span><span class="sxs-lookup"><span data-stu-id="dff38-128">The component installs the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module), which is a native IIS module required to run ASP.NET Core apps behind IIS in a reverse proxy configuration.</span></span>

![修改 Visual Studio 功能：选择“工作负荷”选项卡。](development-time-iis-support/_static/development_time_support.png)

## <a name="configure-the-project"></a><span data-ttu-id="dff38-132">配置项目</span><span class="sxs-lookup"><span data-stu-id="dff38-132">Configure the project</span></span>

### <a name="https-redirection"></a><span data-ttu-id="dff38-133">HTTPS 重定向</span><span class="sxs-lookup"><span data-stu-id="dff38-133">HTTPS redirection</span></span>

<span data-ttu-id="dff38-134">对于新项目中，选中复选框以**针对 HTTPS 配置**中**新 ASP.NET 核心 Web 应用程序**窗口：</span><span class="sxs-lookup"><span data-stu-id="dff38-134">For a new project, select the check box to **Configure for HTTPS** in the **New ASP.NET Core Web Application** window:</span></span>

![新的 ASP.NET 核心 Web 应用程序窗口，并针对 HTTPS 复选框处于选中状态配置。](development-time-iis-support/_static/new-app.png)

<span data-ttu-id="dff38-136">在现有项目中，使用 HTTPS 重定向中的中间件`Startup.Configure`通过调用[UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)扩展方法：</span><span class="sxs-lookup"><span data-stu-id="dff38-136">In an existing project, use HTTPS Redirection Middleware in `Startup.Configure` by calling the [UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection) extension method:</span></span>

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

### <a name="iis-launch-profile"></a><span data-ttu-id="dff38-137">IIS 启动配置文件</span><span class="sxs-lookup"><span data-stu-id="dff38-137">IIS launch profile</span></span>

<span data-ttu-id="dff38-138">创建新的发布配置文件添加开发时间 IIS 支持：</span><span class="sxs-lookup"><span data-stu-id="dff38-138">Create a new launch profile to add development-time IIS support:</span></span>

1. <span data-ttu-id="dff38-139">有关**配置文件**，选择**新建**按钮。</span><span class="sxs-lookup"><span data-stu-id="dff38-139">For **Profile**, select the **New** button.</span></span> <span data-ttu-id="dff38-140">在弹出窗口中将该配置文件"IIS"。</span><span class="sxs-lookup"><span data-stu-id="dff38-140">Name the profile "IIS" in the popup window.</span></span> <span data-ttu-id="dff38-141">选择**确定**创建配置文件。</span><span class="sxs-lookup"><span data-stu-id="dff38-141">Select **OK** to create the profile.</span></span>
1. <span data-ttu-id="dff38-142">有关**启动**设置中选择**IIS**从列表中。</span><span class="sxs-lookup"><span data-stu-id="dff38-142">For the **Launch** setting, select **IIS** from the list.</span></span>
1. <span data-ttu-id="dff38-143">选中的复选框**启动浏览器**和提供的终结点 URL。</span><span class="sxs-lookup"><span data-stu-id="dff38-143">Select the check box for **Launch browser** and provide the endpoint URL.</span></span> <span data-ttu-id="dff38-144">使用 HTTPS 协议。</span><span class="sxs-lookup"><span data-stu-id="dff38-144">Use the HTTPS protocol.</span></span> <span data-ttu-id="dff38-145">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="dff38-145">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="dff38-146">在**环境变量**部分中，选择**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="dff38-146">In the **Environment variables** section, select the **Add** button.</span></span> <span data-ttu-id="dff38-147">环境变量提供的密钥`ASPNETCORE_ENVIRONMENT`和的值`Development`。</span><span class="sxs-lookup"><span data-stu-id="dff38-147">Provide an environment variable with a key of `ASPNETCORE_ENVIRONMENT` and a value of `Development`.</span></span>
1. <span data-ttu-id="dff38-148">在**Web 服务器设置**区域中，设置**应用程序 URL**。</span><span class="sxs-lookup"><span data-stu-id="dff38-148">In the **Web Server Settings** area, set the **App URL**.</span></span> <span data-ttu-id="dff38-149">本示例使用 `https://localhost/WebApplication1`。</span><span class="sxs-lookup"><span data-stu-id="dff38-149">This example uses `https://localhost/WebApplication1`.</span></span>
1. <span data-ttu-id="dff38-150">保存配置文件。</span><span class="sxs-lookup"><span data-stu-id="dff38-150">Save the profile.</span></span>

![选择了“调试”选项卡的“项目属性”窗口。](development-time-iis-support/_static/project_properties.png)

<span data-ttu-id="dff38-155">或者，手动添加到的启动配置文件[launchSettings.json](http://json.schemastore.org/launchsettings)应用程序中的文件：</span><span class="sxs-lookup"><span data-stu-id="dff38-155">Alternatively, manually add a launch profile to the [launchSettings.json](http://json.schemastore.org/launchsettings) file in the app:</span></span>

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

## <a name="run-the-project"></a><span data-ttu-id="dff38-156">运行项目</span><span class="sxs-lookup"><span data-stu-id="dff38-156">Run the project</span></span>

<span data-ttu-id="dff38-157">在 VS UI 中，设置为运行按钮**IIS**分析，并选择按钮以启动应用程序：</span><span class="sxs-lookup"><span data-stu-id="dff38-157">In the VS UI, set the Run button to the **IIS** profile and select the button to start the app:</span></span>

![在 VS 工具栏中设置为"IIS"配置文件运行按钮。](development-time-iis-support/_static/toolbar.png)

<span data-ttu-id="dff38-159">如果未以管理员身份运行 visual Studio 可能会提示重新启动。</span><span class="sxs-lookup"><span data-stu-id="dff38-159">Visual Studio may prompt a restart if not running as an administrator.</span></span> <span data-ttu-id="dff38-160">如果出现提示，请重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="dff38-160">If prompted, restart Visual Studio.</span></span>

<span data-ttu-id="dff38-161">如果将使用的不受信任的开发证书，浏览器可能需要你针对不受信任的证书创建例外。</span><span class="sxs-lookup"><span data-stu-id="dff38-161">If an untrusted development certificate is used, the browser may require you to create an exception for the untrusted certificate.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dff38-162">其他资源</span><span class="sxs-lookup"><span data-stu-id="dff38-162">Additional resources</span></span>

* [<span data-ttu-id="dff38-163">使用 IIS 在 Windows 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="dff38-163">Host ASP.NET Core on Windows with IIS</span></span>](xref:host-and-deploy/iis/index)
* [<span data-ttu-id="dff38-164">ASP.NET Core 模块简介</span><span class="sxs-lookup"><span data-stu-id="dff38-164">Introduction to ASP.NET Core Module</span></span>](xref:fundamentals/servers/aspnet-core-module)
* [<span data-ttu-id="dff38-165">ASP.NET Core 模块配置参考</span><span class="sxs-lookup"><span data-stu-id="dff38-165">ASP.NET Core Module configuration reference</span></span>](xref:host-and-deploy/aspnet-core-module)
* [<span data-ttu-id="dff38-166">Enforce HTTPS</span><span class="sxs-lookup"><span data-stu-id="dff38-166">Enforce HTTPS</span></span>](xref:security/enforcing-ssl)
