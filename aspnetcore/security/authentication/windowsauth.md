---
title: 在 ASP.NET Core 中配置 Windows 身份验证
author: scottaddie
description: 了解如何在使用 IIS Express、 IIS、 HTTP.sys 和 WebListener 的 ASP.NET Core 中配置 Windows 身份验证。
ms.author: riande
ms.custom: mvc
ms.date: 11/01/2018
uid: security/authentication/windowsauth
ms.openlocfilehash: 87fcab75555c1dae0b2815c30d79fd4615df9660
ms.sourcegitcommit: 85f2939af7a167b9694e1d2093277ffc9a741b23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "50968288"
---
# <a name="configure-windows-authentication-in-aspnet-core"></a><span data-ttu-id="aaf5d-103">在 ASP.NET Core 中配置 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="aaf5d-103">Configure Windows Authentication in ASP.NET Core</span></span>

<span data-ttu-id="aaf5d-104">作者：[Steve Smith](https://ardalis.com) 和 [Scott Addie](https://twitter.com/Scott_Addie)</span><span class="sxs-lookup"><span data-stu-id="aaf5d-104">By [Steve Smith](https://ardalis.com) and [Scott Addie](https://twitter.com/Scott_Addie)</span></span>

<span data-ttu-id="aaf5d-105">承载有 IIS、 ASP.NET Core 应用可以配置 Windows 身份验证[HTTP.sys](xref:fundamentals/servers/httpsys)，或[WebListener](xref:fundamentals/servers/weblistener)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-105">Windows Authentication can be configured for ASP.NET Core apps hosted with IIS, [HTTP.sys](xref:fundamentals/servers/httpsys), or [WebListener](xref:fundamentals/servers/weblistener).</span></span>

## <a name="windows-authentication"></a><span data-ttu-id="aaf5d-106">Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="aaf5d-106">Windows Authentication</span></span>

<span data-ttu-id="aaf5d-107">Windows 身份验证依赖于操作系统的 ASP.NET Core 应用的用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-107">Windows Authentication relies on the operating system to authenticate users of ASP.NET Core apps.</span></span> <span data-ttu-id="aaf5d-108">使用 Active Directory 域标识或其他 Windows 帐户标识的用户在公司网络上运行你的服务器时，可以使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-108">You can use Windows Authentication when your server runs on a corporate network using Active Directory domain identities or other Windows accounts to identify users.</span></span> <span data-ttu-id="aaf5d-109">Windows 身份验证是最适合于 intranet 环境中的用户、 客户端应用程序和 web 服务器属于同一个 Windows 域。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-109">Windows Authentication is best suited to intranet environments in which users, client applications, and web servers belong to the same Windows domain.</span></span>

<span data-ttu-id="aaf5d-110">[了解有关 Windows 身份验证的详细信息，并为 IIS 安装](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-110">[Learn more about Windows Authentication and installing it for IIS](/iis/configuration/system.webServer/security/authentication/windowsAuthentication/).</span></span>

## <a name="enable-windows-authentication-in-an-aspnet-core-app"></a><span data-ttu-id="aaf5d-111">启用 Windows 身份验证在 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="aaf5d-111">Enable Windows Authentication in an ASP.NET Core app</span></span>

<span data-ttu-id="aaf5d-112">Visual Studio Web 应用程序模板可配置为支持 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-112">The Visual Studio Web Application template can be configured to support Windows Authentication.</span></span>

### <a name="use-the-windows-authentication-app-template"></a><span data-ttu-id="aaf5d-113">使用 Windows 身份验证应用程序模板</span><span class="sxs-lookup"><span data-stu-id="aaf5d-113">Use the Windows Authentication app template</span></span>

<span data-ttu-id="aaf5d-114">在 Visual Studio 中：</span><span class="sxs-lookup"><span data-stu-id="aaf5d-114">In Visual Studio:</span></span>

1. <span data-ttu-id="aaf5d-115">创建新的 ASP.NET Core Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-115">Create a new ASP.NET Core Web Application.</span></span>
1. <span data-ttu-id="aaf5d-116">从模板列表中选择 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-116">Select Web Application from the list of templates.</span></span>
1. <span data-ttu-id="aaf5d-117">选择**更改身份验证**按钮，然后选择**Windows 身份验证**。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-117">Select the **Change Authentication** button and select **Windows Authentication**.</span></span>

<span data-ttu-id="aaf5d-118">运行应用。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-118">Run the app.</span></span> <span data-ttu-id="aaf5d-119">用户名将显示在顶部的应用程序。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-119">The username appears in the top right of the app.</span></span>

![Windows 身份验证浏览器屏幕截图](windowsauth/_static/browser-screenshot.png)

<span data-ttu-id="aaf5d-121">对于使用 IIS Express 的开发工作，该模板提供使用 Windows 身份验证所需的所有配置。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-121">For development work using IIS Express, the template provides all the configuration necessary to use Windows Authentication.</span></span> <span data-ttu-id="aaf5d-122">以下部分介绍如何手动配置 Windows 身份验证的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-122">The following section shows how to manually configure an ASP.NET Core app for Windows Authentication.</span></span>

### <a name="visual-studio-settings-for-windows-and-anonymous-authentication"></a><span data-ttu-id="aaf5d-123">Windows 和匿名身份验证的 visual Studio 设置</span><span class="sxs-lookup"><span data-stu-id="aaf5d-123">Visual Studio settings for Windows and anonymous authentication</span></span>

<span data-ttu-id="aaf5d-124">Visual Studio 项目**属性**页的**调试**选项卡提供有关 Windows 身份验证和匿名身份验证的复选框。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-124">The Visual Studio project **Properties** page's **Debug** tab provides check boxes for Windows Authentication and anonymous authentication.</span></span>

![Windows 身份验证浏览器屏幕截图](windowsauth/_static/vs-auth-property-menu.png)

<span data-ttu-id="aaf5d-126">或者，可以在配置这两个属性*launchSettings.json*文件：</span><span class="sxs-lookup"><span data-stu-id="aaf5d-126">Alternatively, these two properties can be configured in the *launchSettings.json* file:</span></span>

[!code-json[](windowsauth/sample/launchSettings.json?highlight=3-4)]

## <a name="enable-windows-authentication-with-iis"></a><span data-ttu-id="aaf5d-127">启用与 IIS Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="aaf5d-127">Enable Windows Authentication with IIS</span></span>

<span data-ttu-id="aaf5d-128">IIS 使用[ASP.NET Core 模块](xref:fundamentals/servers/aspnet-core-module)到承载 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-128">IIS uses the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) to host ASP.NET Core apps.</span></span> <span data-ttu-id="aaf5d-129">在 IIS 中，不应用配置 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-129">Windows Authentication is configured in IIS, not the app.</span></span> <span data-ttu-id="aaf5d-130">以下部分说明如何使用 IIS 管理器配置为使用 Windows 身份验证的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-130">The following sections show how to use IIS Manager to configure an ASP.NET Core app to use Windows Authentication.</span></span>

### <a name="iis-configuration"></a><span data-ttu-id="aaf5d-131">IIS 配置</span><span class="sxs-lookup"><span data-stu-id="aaf5d-131">IIS configuration</span></span>

<span data-ttu-id="aaf5d-132">启用 Windows 身份验证的 IIS 角色服务。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-132">Enable the IIS Role Service for Windows Authentication.</span></span> <span data-ttu-id="aaf5d-133">有关详细信息，请参阅[IIS 角色服务 （请参阅步骤 2） 中启用 Windows 身份验证](xref:host-and-deploy/iis/index#iis-configuration)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-133">For more information, see [Enable Windows Authentication in IIS Role Services (see Step 2)](xref:host-and-deploy/iis/index#iis-configuration).</span></span>

<span data-ttu-id="aaf5d-134">默认情况下，IIS 集成中间件配置为自动进行身份验证请求。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-134">IIS Integration Middleware is configured to automatically authenticate requests by default.</span></span> <span data-ttu-id="aaf5d-135">有关详细信息，请参阅[使用 IIS 的 Windows 上托管 ASP.NET Core: IIS 选项 (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-135">For more information, see [Host ASP.NET Core on Windows with IIS: IIS options (AutomaticAuthentication)](xref:host-and-deploy/iis/index#iis-options).</span></span>

<span data-ttu-id="aaf5d-136">默认情况下，ASP.NET Core 模块配置为转发到应用的 Windows 身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-136">The ASP.NET Core Module is configured to forward the Windows Authentication token to the app by default.</span></span> <span data-ttu-id="aaf5d-137">有关详细信息，请参阅[ASP.NET Core 模块配置参考： aspNetCore 元素的特性](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-137">For more information, see [ASP.NET Core Module configuration reference: Attributes of the aspNetCore element](xref:host-and-deploy/aspnet-core-module#attributes-of-the-aspnetcore-element).</span></span>

### <a name="create-a-new-iis-site"></a><span data-ttu-id="aaf5d-138">创建新的 IIS 站点</span><span class="sxs-lookup"><span data-stu-id="aaf5d-138">Create a new IIS site</span></span>

<span data-ttu-id="aaf5d-139">指定的名称和文件夹，并允许它创建新的应用程序池。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-139">Specify a name and folder and allow it to create a new application pool.</span></span>

### <a name="customize-authentication"></a><span data-ttu-id="aaf5d-140">自定义身份验证</span><span class="sxs-lookup"><span data-stu-id="aaf5d-140">Customize authentication</span></span>

<span data-ttu-id="aaf5d-141">打开该站点的身份验证功能。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-141">Open the Authentication features for the site.</span></span>

![IIS 身份验证菜单](windowsauth/_static/iis-authentication-menu.png)

<span data-ttu-id="aaf5d-143">禁用匿名身份验证并启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-143">Disable Anonymous Authentication and enable Windows Authentication.</span></span>

![IIS 身份验证设置](windowsauth/_static/iis-auth-settings.png)

### <a name="publish-your-project-to-the-iis-site-folder"></a><span data-ttu-id="aaf5d-145">将你的项目发布到 IIS 的站点文件夹</span><span class="sxs-lookup"><span data-stu-id="aaf5d-145">Publish your project to the IIS site folder</span></span>

<span data-ttu-id="aaf5d-146">使用 Visual Studio 或.NET Core CLI，将应用发布到目标文件夹。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-146">Using Visual Studio or the .NET Core CLI, publish the app to the destination folder.</span></span>

![Visual Studio 发布对话框](windowsauth/_static/vs-publish-app.png)

<span data-ttu-id="aaf5d-148">详细了解如何[发布到 IIS](xref:host-and-deploy/iis/index)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-148">Learn more about [publishing to IIS](xref:host-and-deploy/iis/index).</span></span>

<span data-ttu-id="aaf5d-149">启动应用程序以验证 Windows 身份验证正常工作。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-149">Launch the app to verify Windows Authentication is working.</span></span>

::: moniker range=">= aspnetcore-2.0"

## <a name="enable-windows-authentication-with-httpsys"></a><span data-ttu-id="aaf5d-150">启用 Windows 身份验证使用 HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="aaf5d-150">Enable Windows Authentication with HTTP.sys</span></span>

<span data-ttu-id="aaf5d-151">虽然 Kestrel 不支持 Windows 身份验证，您可以使用[HTTP.sys](xref:fundamentals/servers/httpsys)以在 Windows 上支持自承载的方案。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-151">Although Kestrel doesn't support Windows Authentication, you can use [HTTP.sys](xref:fundamentals/servers/httpsys) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="aaf5d-152">下面的示例配置以使用 Windows 身份验证使用 HTTP.sys 的应用程序的 web 主机：</span><span class="sxs-lookup"><span data-stu-id="aaf5d-152">The following example configures the app's web host to use HTTP.sys with Windows Authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program2x.cs?highlight=9-14)]

> [!NOTE]
> <span data-ttu-id="aaf5d-153">HTTP.sys 通过 Kerberos 身份验证协议委托给内核模式身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-153">HTTP.sys delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="aaf5d-154">Kerberos 和 HTTP.sys 不支持用户模式身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-154">User mode authentication isn't supported with Kerberos and HTTP.sys.</span></span> <span data-ttu-id="aaf5d-155">必须使用计算机帐户来解密从 Active Directory 获取的并由客户端转发到服务器的 Kerberos 令牌/票证，以便对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-155">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="aaf5d-156">注册主机的服务主体名称 (SPN)，而不是应用的用户。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-156">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

> [!NOTE]
> <span data-ttu-id="aaf5d-157">HTTP.sys 不支持 Nano Server 版本 1709年或更高版本上。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-157">HTTP.sys isn't supported on Nano Server version 1709 or later.</span></span> <span data-ttu-id="aaf5d-158">若要使用 Windows 身份验证和 HTTP.sys 与 Nano Server，使用[Server Core (microsoft/windowsservercore) 容器](https://hub.docker.com/r/microsoft/windowsservercore/)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-158">To use Windows Authentication and HTTP.sys with Nano Server, use a [Server Core (microsoft/windowsservercore) container](https://hub.docker.com/r/microsoft/windowsservercore/).</span></span> <span data-ttu-id="aaf5d-159">在 Server Core 上的详细信息，请参阅[什么是 Windows Server 中的服务器核心安装选项？](/windows-server/administration/server-core/what-is-server-core)。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-159">For more information on Server Core, see [What is the Server Core installation option in Windows Server?](/windows-server/administration/server-core/what-is-server-core).</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

## <a name="enable-windows-authentication-with-weblistener"></a><span data-ttu-id="aaf5d-160">启用与 WebListener 的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="aaf5d-160">Enable Windows Authentication with WebListener</span></span>

<span data-ttu-id="aaf5d-161">虽然 Kestrel 不支持 Windows 身份验证，您可以使用[WebListener](xref:fundamentals/servers/weblistener)以在 Windows 上支持自承载的方案。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-161">Although Kestrel doesn't support Windows Authentication, you can use [WebListener](xref:fundamentals/servers/weblistener) to support self-hosted scenarios on Windows.</span></span> <span data-ttu-id="aaf5d-162">下面的示例配置应用程序的 web 主机，若要将 WebListener 与 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="aaf5d-162">The following example configures the app's web host to use WebListener with Windows Authentication:</span></span>

[!code-csharp[](windowsauth/sample/Program1x.cs?highlight=6-11)]

> [!NOTE]
> <span data-ttu-id="aaf5d-163">WebListener 通过 Kerberos 身份验证协议委托给内核模式身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-163">WebListener delegates to kernel mode authentication with the Kerberos authentication protocol.</span></span> <span data-ttu-id="aaf5d-164">Kerberos 和 WebListener 不支持用户模式身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-164">User mode authentication isn't supported with Kerberos and WebListener.</span></span> <span data-ttu-id="aaf5d-165">必须使用计算机帐户来解密从 Active Directory 获取的并由客户端转发到服务器的 Kerberos 令牌/票证，以便对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-165">The machine account must be used to decrypt the Kerberos token/ticket that's obtained from Active Directory and forwarded by the client to the server to authenticate the user.</span></span> <span data-ttu-id="aaf5d-166">注册主机的服务主体名称 (SPN)，而不是应用的用户。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-166">Register the Service Principal Name (SPN) for the host, not the user of the app.</span></span>

::: moniker-end

## <a name="work-with-windows-authentication"></a><span data-ttu-id="aaf5d-167">使用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="aaf5d-167">Work with Windows Authentication</span></span>

<span data-ttu-id="aaf5d-168">匿名访问的配置状态确定的方式`[Authorize]`和`[AllowAnonymous]`应用中使用属性。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-168">The configuration state of anonymous access determines the way in which the `[Authorize]` and `[AllowAnonymous]` attributes are used in the app.</span></span> <span data-ttu-id="aaf5d-169">以下两个部分介绍如何处理的匿名访问权限的禁止和允许配置状态。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-169">The following two sections explain how to handle the disallowed and allowed configuration states of anonymous access.</span></span>

### <a name="disallow-anonymous-access"></a><span data-ttu-id="aaf5d-170">不允许匿名访问</span><span class="sxs-lookup"><span data-stu-id="aaf5d-170">Disallow anonymous access</span></span>

<span data-ttu-id="aaf5d-171">启用 Windows 身份验证，并且禁用了匿名访问，则`[Authorize]`和`[AllowAnonymous]`特性不起作用。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-171">When Windows Authentication is enabled and anonymous access is disabled, the `[Authorize]` and `[AllowAnonymous]` attributes have no effect.</span></span> <span data-ttu-id="aaf5d-172">如果 IIS 站点 （或 HTTP.sys 或 WebListener 服务器） 配置为不允许匿名访问，请求将永远不会到达您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-172">If the IIS site (or HTTP.sys or WebListener server) is configured to disallow anonymous access, the request never reaches your app.</span></span> <span data-ttu-id="aaf5d-173">出于此原因，`[AllowAnonymous]`属性不适用。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-173">For this reason, the `[AllowAnonymous]` attribute isn't applicable.</span></span>

### <a name="allow-anonymous-access"></a><span data-ttu-id="aaf5d-174">允许匿名访问</span><span class="sxs-lookup"><span data-stu-id="aaf5d-174">Allow anonymous access</span></span>

<span data-ttu-id="aaf5d-175">启用 Windows 身份验证和匿名访问，使用`[Authorize]`和`[AllowAnonymous]`属性。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-175">When both Windows Authentication and anonymous access are enabled, use the `[Authorize]` and `[AllowAnonymous]` attributes.</span></span> <span data-ttu-id="aaf5d-176">`[Authorize]`属性允许你保护部分，该应用程序的真正需要 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-176">The `[Authorize]` attribute allows you to secure pieces of the app which truly do require Windows Authentication.</span></span> <span data-ttu-id="aaf5d-177">`[AllowAnonymous]`特性重写`[Authorize]`特性允许匿名访问的应用中的使用情况。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-177">The `[AllowAnonymous]` attribute overrides `[Authorize]` attribute usage within apps which allow anonymous access.</span></span> <span data-ttu-id="aaf5d-178">请参阅[简单授权](xref:security/authorization/simple)属性使用情况详细信息。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-178">See [Simple Authorization](xref:security/authorization/simple) for attribute usage details.</span></span>

<span data-ttu-id="aaf5d-179">在 ASP.NET Core 2.x，请`[Authorize]`属性需要进行额外配置中的*Startup.cs*以进行 Windows 身份验证质询匿名请求。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-179">In ASP.NET Core 2.x, the `[Authorize]` attribute requires additional configuration in *Startup.cs* to challenge anonymous requests for Windows Authentication.</span></span> <span data-ttu-id="aaf5d-180">建议的配置略有根据正在使用的 web 服务器而异。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-180">The recommended configuration varies slightly based on the web server being used.</span></span>

> [!NOTE]
> <span data-ttu-id="aaf5d-181">默认情况下，缺少授权可访问的页面的用户会显示 HTTP 403 响应为空。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-181">By default, users who lack authorization to access a page are presented with an empty HTTP 403 response.</span></span> <span data-ttu-id="aaf5d-182">[StatusCodePages 中间件](xref:fundamentals/error-handling#configure-status-code-pages)可以配置为向用户提供更好的"拒绝访问"体验。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-182">The [StatusCodePages middleware](xref:fundamentals/error-handling#configure-status-code-pages) can be configured to provide users with a better "Access Denied" experience.</span></span>

#### <a name="iis"></a><span data-ttu-id="aaf5d-183">IIS</span><span class="sxs-lookup"><span data-stu-id="aaf5d-183">IIS</span></span>

<span data-ttu-id="aaf5d-184">如果使用 IIS，添加以下代码到`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="aaf5d-184">If using IIS, add the following to the `ConfigureServices` method:</span></span>

```csharp
// IISDefaults requires the following import:
// using Microsoft.AspNetCore.Server.IISIntegration;
services.AddAuthentication(IISDefaults.AuthenticationScheme);
```

#### <a name="httpsys"></a><span data-ttu-id="aaf5d-185">HTTP.sys</span><span class="sxs-lookup"><span data-stu-id="aaf5d-185">HTTP.sys</span></span>

<span data-ttu-id="aaf5d-186">如果使用 HTTP.sys，添加以下代码到`ConfigureServices`方法：</span><span class="sxs-lookup"><span data-stu-id="aaf5d-186">If using HTTP.sys, add the following to the `ConfigureServices` method:</span></span>

```csharp
// HttpSysDefaults requires the following import:
// using Microsoft.AspNetCore.Server.HttpSys;
services.AddAuthentication(HttpSysDefaults.AuthenticationScheme);
```

### <a name="impersonation"></a><span data-ttu-id="aaf5d-187">Impersonation</span><span class="sxs-lookup"><span data-stu-id="aaf5d-187">Impersonation</span></span>

<span data-ttu-id="aaf5d-188">ASP.NET Core 未实现模拟。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-188">ASP.NET Core doesn't implement impersonation.</span></span> <span data-ttu-id="aaf5d-189">应用程序运行具有使用应用程序池或进程标识的所有请求的应用程序标识。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-189">Apps run with the application identity for all requests, using app pool or process identity.</span></span> <span data-ttu-id="aaf5d-190">如果您需要显式执行代表用户操作，使用`WindowsIdentity.RunImpersonated`。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-190">If you need to explicitly perform an action on behalf of a user, use `WindowsIdentity.RunImpersonated`.</span></span> <span data-ttu-id="aaf5d-191">在此上下文中运行的单个操作，然后关闭上下文。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-191">Run a single action in this context and then close the context.</span></span>

[!code-csharp[](windowsauth/sample/Startup.cs?name=snippet_Impersonate&highlight=10-18)]

<span data-ttu-id="aaf5d-192">请注意，`RunImpersonated`不支持异步操作，不应该用于复杂的方案。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-192">Note that `RunImpersonated` doesn't support asynchronous operations and shouldn't be used for complex scenarios.</span></span> <span data-ttu-id="aaf5d-193">例如，包装整个请求或中间件链不受支持或推荐的。</span><span class="sxs-lookup"><span data-stu-id="aaf5d-193">For example, wrapping entire requests or middleware chains isn't supported or recommended.</span></span>
