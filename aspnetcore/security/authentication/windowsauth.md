---
title: "在 ASP.NET 核心中配置 Windows 身份验证"
author: ardalis
description: "本文介绍如何在 ASP.NET Core 上使用 IIS Express、 IIS、 HTTP.sys，和 WebListener 中配置 Windows 身份验证。"
manager: wpickett
ms.author: riande
ms.date: 10/24/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/authentication/windowsauth
ms.openlocfilehash: c229537e7f533eea2173dbc51b8d0d0e097d434a
ms.sourcegitcommit: 49fb3b7669b504d35edad34db8285e56b958a9fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2018
---
# <a name="configure-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="5a38b-103">在 ASP.NET Core 应用程序配置 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="5a38b-103">Configure Windows authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="5a38b-104">作者：[Steve Smith](https://ardalis.com) 和 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="5a38b-104">By [Steve Smith](https://ardalis.com) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="5a38b-105">Windows 身份验证可以配置用于与 IIS 托管的 ASP.NET Core 应用[HTTP.sys](xref:fundamentals/servers/httpsys)，或[WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="5a38b-105">Windows authentication can be configured for ASP.NET Core apps hosted with IIS, [HTTP.sys](xref:fundamentals/servers/httpsys), or [WebListener](xref:fundamentals/servers/weblistener).</span></span>

## <a name="what-is-windows-authentication"></a><span data-ttu-id="5a38b-106">什么是 Windows 身份验证？</span><span class="sxs-lookup"><span data-stu-id="5a38b-106">What is Windows authentication?</span></span>

<span data-ttu-id="5a38b-107">Windows 身份验证依赖于操作系统的 ASP.NET Core 应用的用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-107">Windows authentication relies on the operating system to authenticate users of ASP.NET Core apps.</span></span> <span data-ttu-id="5a38b-108">在使用 Active Directory 域标识或其他 Windows 帐户来标识用户的企业网络上运行你的服务器时，你可以使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-108">You can use Windows authentication when your server runs on a corporate network using Active Directory domain identities or other Windows accounts to identify users.</span></span> <span data-ttu-id="5a38b-109">Windows 身份验证是最适合 intranet 环境中的用户、 客户端应用程序和 web 服务器属于同一 Windows 域。</span><span class="sxs-lookup"><span data-stu-id="5a38b-109">Windows authentication is best suited to intranet environments in which users, client applications, and web servers belong to the same Windows domain.</span></span>

<span data-ttu-id="5a38b-110">[了解有关 Windows 身份验证和为 IIS 安装](https://docs.microsoft.com/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)。</span><span class="sxs-lookup"><span data-stu-id="5a38b-110">[Learn more about Windows authentication and installing it for IIS](https://docs.microsoft.com/iis/configuration/system.webServer/security/authentication/windowsAuthentication/).</span></span>

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="5a38b-111">启用 ASP.NET Core 应用程序中的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="5a38b-111">Enable Windows authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="5a38b-112">Visual Studio Web 应用程序模板可以配置为支持 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-112">The Visual Studio Web Application template can be configured to support Windows authentication.</span></span>

### <a name="use-the-windows-authentication-app-template"></a><span data-ttu-id="5a38b-113">使用 Windows 身份验证应用程序模板</span><span class="sxs-lookup"><span data-stu-id="5a38b-113">Use the Windows authentication app template</span></span>

<span data-ttu-id="5a38b-114">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="5a38b-114">In Visual Studio:</span></span>
1. <span data-ttu-id="5a38b-115">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a38b-115">Create a new ASP.NET Core Web Application.</span></span> 
1. <span data-ttu-id="5a38b-116">从模板列表中选择 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a38b-116">Select Web Application from the list of templates.</span></span>
1. <span data-ttu-id="5a38b-117">选择**更改身份验证**按钮，然后选择**Windows 身份验证**。</span><span class="sxs-lookup"><span data-stu-id="5a38b-117">Select the **Change Authentication** button and select **Windows Authentication**.</span></span> 

<span data-ttu-id="5a38b-118">运行应用。</span><span class="sxs-lookup"><span data-stu-id="5a38b-118">Run the app.</span></span> <span data-ttu-id="5a38b-119">用户名已显示在顶部的应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="5a38b-119">The username appears in the top right of the app.</span></span>

![Windows 身份验证浏览器屏幕快照](windowsauth/_static/browser-screenshot.png)

<span data-ttu-id="5a38b-121">对于使用 IIS Express 的开发工作，该模板提供所有使用 Windows 身份验证所需的配置。</span><span class="sxs-lookup"><span data-stu-id="5a38b-121">For development work using IIS Express, the template provides all the configuration necessary to use Windows authentication.</span></span> <span data-ttu-id="5a38b-122">以下部分说明如何手动配置 Windows 身份验证的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="5a38b-122">The following section shows how to manually configure an ASP.NET Core app for Windows authentication.</span></span>

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a><span data-ttu-id="5a38b-123">为 Windows 以及匿名身份验证的 visual Studio 设置</span><span class="sxs-lookup"><span data-stu-id="5a38b-123">Visual Studio settings for Windows and anonymous authentication</span></span>

<span data-ttu-id="5a38b-124">Visual Studio 项目**属性**页面的**调试**选项卡为 Windows 身份验证和匿名身份验证提供的复选框。</span><span class="sxs-lookup"><span data-stu-id="5a38b-124">The Visual Studio project **Properties** page's **Debug** tab provides check boxes for Windows authentication and anonymous authentication.</span></span>

![Windows 身份验证浏览器屏幕快照](windowsauth/_static/vs-auth-property-menu.png)

<span data-ttu-id="5a38b-126">或者，在中配置这两个属性*launchSettings.json*文件：</span><span class="sxs-lookup"><span data-stu-id="5a38b-126">Alternatively, these two properties can be configured in the *launchSettings.json* file:</span></span>

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a><span data-ttu-id="5a38b-127">启用与 IIS 的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="5a38b-127">Enable Windows authentication with IIS</span></span>

<span data-ttu-id="5a38b-128">IIS 使用[ASP.NET 核心模块](xref:fundamentals/servers/aspnet-core-module)(ANCM) 来承载 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="5a38b-128">IIS uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) (ANCM) to host ASP.NET Core apps.</span></span> <span data-ttu-id="5a38b-129">ANCM 流 Windows 身份验证到 IIS 默认情况下。</span><span class="sxs-lookup"><span data-stu-id="5a38b-129">The ANCM flows Windows authentication to IIS by default.</span></span> <span data-ttu-id="5a38b-130">IIS，不是应用程序项目中进行配置的 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-130">Configuration of Windows authentication is done within IIS, not the application project.</span></span> <span data-ttu-id="5a38b-131">以下部分说明如何使用 IIS 管理器来配置 ASP.NET Core 应用以使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-131">The following sections show how to use IIS Manager to configure an ASP.NET Core app to use Windows authentication.</span></span>

### <a name="create-a-new-iis-site"></a><span data-ttu-id="5a38b-132">创建一个新的 IIS 站点</span><span class="sxs-lookup"><span data-stu-id="5a38b-132">Create a new IIS site</span></span>

<span data-ttu-id="5a38b-133">指定名称和文件夹，并允许它创建新的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="5a38b-133">Specify a name and folder and allow it to create a new application pool.</span></span>

### <a name="customize-authentication"></a><span data-ttu-id="5a38b-134">自定义身份验证</span><span class="sxs-lookup"><span data-stu-id="5a38b-134">Customize authentication</span></span>

<span data-ttu-id="5a38b-135">打开身份验证菜单上的站点。</span><span class="sxs-lookup"><span data-stu-id="5a38b-135">Open the Authentication menu for the site.</span></span>

![IIS 身份验证菜单](windowsauth/_static/iis-authentication-menu.png)

<span data-ttu-id="5a38b-137">禁用匿名身份验证并启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-137">Disable Anonymous Authentication and enable Windows Authentication.</span></span>

![IIS 身份验证设置](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a><span data-ttu-id="5a38b-139">将你的项目发布到 IIS 站点文件夹</span><span class="sxs-lookup"><span data-stu-id="5a38b-139">Publish your project to the IIS site folder</span></span>

<span data-ttu-id="5a38b-140">使用 Visual Studio 或.NET 核心 CLI，将应用发布到目标文件夹。</span><span class="sxs-lookup"><span data-stu-id="5a38b-140">Using Visual Studio or the .NET Core CLI, publish the app to the destination folder.</span></span>

![Visual Studio 发布对话框](windowsauth/_static/vs-publish-app.png)

<span data-ttu-id="5a38b-142">详细了解[发布到 IIS](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="5a38b-142">Learn more about [publishing to IIS](xref:host-and-deploy/iis/index).</span></span>

<span data-ttu-id="5a38b-143">启动应用程序来验证使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-143">Launch the app to verify Windows authentication is working.</span></span>

## <a name="enable-windows-authentication-with-httpsys-or-weblistener"></a><span data-ttu-id="5a38b-144">启用 Windows 身份验证与 HTTP.sys 或 WebListener</span><span class="sxs-lookup"><span data-stu-id="5a38b-144">Enable Windows authentication with HTTP.sys or WebListener</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="5a38b-145">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="5a38b-145">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="5a38b-146">尽管 Kestrel 不支持 Windows 身份验证，你可以使用[HTTP.sys](xref:fundamentals/servers/httpsys)以在 Windows 上支持自承载的方案。</span><span class="sxs-lookup"><span data-stu-id="5a38b-146">Although Kestrel doesn't support Windows authentication, you can use [HTTP.sys](xref:fundamentals/servers/httpsys) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="5a38b-147">下面的示例将配置应用程序的 web 主机 HTTP.sys 用于 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="5a38b-147">The following example configures the app's web host to use HTTP.sys with Windows authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="5a38b-148">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="5a38b-148">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="5a38b-149">尽管 Kestrel 不支持 Windows 身份验证，你可以使用[WebListener](xref:fundamentals/servers/weblistener)以在 Windows 上支持自承载的方案。</span><span class="sxs-lookup"><span data-stu-id="5a38b-149">Although Kestrel doesn't support Windows authentication, you can use [WebListener](xref:fundamentals/servers/weblistener) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="5a38b-150">下面的示例将配置应用程序的 web 主机 WebListener 用于 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="5a38b-150">The following example configures the app's web host to use WebListener with Windows authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program1x.cs?highlight=6-11)]

---

## <a name="work-with-windows-authentication"></a><span data-ttu-id="5a38b-151">使用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="5a38b-151">Work with Windows authentication</span></span>

<span data-ttu-id="5a38b-152">匿名访问的配置状态确定的方式`[Authorize]`和`[AllowAnonymous]`特性用于应用程序中。</span><span class="sxs-lookup"><span data-stu-id="5a38b-152">The configuration state of anonymous access determines the way in which the `[Authorize]` and `[AllowAnonymous]` attributes are used in the app.</span></span> <span data-ttu-id="5a38b-153">以下两节介绍如何处理的匿名访问权限不允许的和允许配置状态。</span><span class="sxs-lookup"><span data-stu-id="5a38b-153">The following two sections explain how to handle the disallowed and allowed configuration states of anonymous access.</span></span>

### <a name="disallow-anonymous-access"></a><span data-ttu-id="5a38b-154">不允许匿名访问</span><span class="sxs-lookup"><span data-stu-id="5a38b-154">Disallow anonymous access</span></span>

<span data-ttu-id="5a38b-155">当启用了 Windows 身份验证并且禁用了匿名访问，`[Authorize]`和`[AllowAnonymous]`属性产生任何影响。</span><span class="sxs-lookup"><span data-stu-id="5a38b-155">When Windows authentication is enabled and anonymous access is disabled, the `[Authorize]` and `[AllowAnonymous]` attributes have no effect.</span></span> <span data-ttu-id="5a38b-156">如果 IIS 站点 （或 HTTP.sys 或 WebListener 服务器） 配置为不允许匿名访问，请求将永远不会到达你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5a38b-156">If the IIS site (or HTTP.sys or WebListener server) is configured to disallow anonymous access, the request never reaches your app.</span></span> <span data-ttu-id="5a38b-157">为此，`[AllowAnonymous]`属性不适用。</span><span class="sxs-lookup"><span data-stu-id="5a38b-157">For this reason, the `[AllowAnonymous]` attribute isn't applicable.</span></span>

### <a name="allow-anonymous-access"></a><span data-ttu-id="5a38b-158">允许匿名访问</span><span class="sxs-lookup"><span data-stu-id="5a38b-158">Allow anonymous access</span></span>

<span data-ttu-id="5a38b-159">当启用了 Windows 身份验证和匿名访问时，使用`[Authorize]`和`[AllowAnonymous]`属性。</span><span class="sxs-lookup"><span data-stu-id="5a38b-159">When both Windows authentication and anonymous access are enabled, use the `[Authorize]` and `[AllowAnonymous]` attributes.</span></span> <span data-ttu-id="5a38b-160">`[Authorize]`属性允许你保护的应用程序的部分，真正需要 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="5a38b-160">The `[Authorize]` attribute allows you to secure pieces of the app which truly do require Windows authentication.</span></span> <span data-ttu-id="5a38b-161">`[AllowAnonymous]`特性重写`[Authorize]`属性中允许匿名访问的应用程序的使用情况。</span><span class="sxs-lookup"><span data-stu-id="5a38b-161">The `[AllowAnonymous]` attribute overrides `[Authorize]` attribute usage within apps which allow anonymous access.</span></span> <span data-ttu-id="5a38b-162">请参阅[简单授权](xref:security/authorization/simple)对于特性用法的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5a38b-162">See [Simple Authorization](xref:security/authorization/simple) for attribute usage details.</span></span>

<span data-ttu-id="5a38b-163">在 ASP.NET Core 2.x，`[Authorize]`属性要求中的其他配置*Startup.cs*质询对于 Windows 身份验证的匿名请求。</span><span class="sxs-lookup"><span data-stu-id="5a38b-163">In ASP.NET Core 2.x, the `[Authorize]` attribute requires additional configuration in *Startup.cs* to challenge anonymous requests for Windows authentication.</span></span> <span data-ttu-id="5a38b-164">建议的配置略有根据正在使用的 web 服务器而有所不同。</span><span class="sxs-lookup"><span data-stu-id="5a38b-164">The recommended configuration varies slightly based on the web server being used.</span></span>

> [!NOTE]
> <span data-ttu-id="5a38b-165">默认情况下，缺少授权可访问的页面的用户将出现一个空白文档。</span><span class="sxs-lookup"><span data-stu-id="5a38b-165">By default, users who lack authorization to access a page are presented with a blank document.</span></span> <span data-ttu-id="5a38b-166">[StatusCodePages 中间件](xref:fundamentals/error-handling#configuring-status-code-pages)可以配置为用户提供更好的"拒绝访问"体验。</span><span class="sxs-lookup"><span data-stu-id="5a38b-166">The [StatusCodePages middleware](xref:fundamentals/error-handling#configuring-status-code-pages) can be configured to provide users with a better "Access Denied" experience.</span></span>

#### <a name="iis"></a><span data-ttu-id="5a38b-167">IIS</span><span class="sxs-lookup"><span data-stu-id="5a38b-167">IIS</span></span>

<span data-ttu-id="5a38b-168">如果使用 IIS，添加到以下`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="5a38b-168">If using IIS, add the following to the `ConfigureServices` method:</span></span> 

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a><span data-ttu-id="5a38b-169">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="5a38b-169">HTTP.sys</span></span>

<span data-ttu-id="5a38b-170">如果使用 HTTP.sys，添加到以下`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="5a38b-170">If using HTTP.sys, add the following to the `ConfigureServices` method:</span></span>

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a><span data-ttu-id="5a38b-171">Impersonation</span><span class="sxs-lookup"><span data-stu-id="5a38b-171">Impersonation</span></span>

<span data-ttu-id="5a38b-172">ASP.NET 核心未实现模拟。</span><span class="sxs-lookup"><span data-stu-id="5a38b-172">ASP.NET Core doesn't implement impersonation.</span></span> <span data-ttu-id="5a38b-173">使用应用程序池或进程标识的所有请求的应用程序标识使用运行应用。</span><span class="sxs-lookup"><span data-stu-id="5a38b-173">Apps run with the application identity for all requests, using app pool or process identity.</span></span> <span data-ttu-id="5a38b-174">如果你需要显式执行代表用户操作，使用`WindowsIdentity.RunImpersonated`。</span><span class="sxs-lookup"><span data-stu-id="5a38b-174">If you need to explicitly perform an action on behalf of a user, use `WindowsIdentity.RunImpersonated`.</span></span> <span data-ttu-id="5a38b-175">在此上下文中运行的单个操作，然后关闭上下文。</span><span class="sxs-lookup"><span data-stu-id="5a38b-175">Run a single action in this context and then close the context.</span></span>

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

<span data-ttu-id="5a38b-176">请注意，`RunImpersonated`不支持异步操作，并且不应可用于复杂的方案。</span><span class="sxs-lookup"><span data-stu-id="5a38b-176">Note that `RunImpersonated` doesn't support asynchronous operations and shouldn't be used for complex scenarios.</span></span> <span data-ttu-id="5a38b-177">例如，包装整个请求或中间件链不受支持或建议。</span><span class="sxs-lookup"><span data-stu-id="5a38b-177">For example, wrapping entire requests or middleware chains isn't supported or recommended.</span></span>

---
