---
title: 使用 Nginx 在 Linux 上托管 ASP.NET Core
author: rick-anderson
description: 介绍如何在 Ubuntu 16.04 上将 Nginx 设置为反向代理，从而将 HTTP 流量转发到在 Kestrel 上运行的 ASP.NET Core Web 应用。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 03/13/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/linux-nginx
ms.openlocfilehash: d37aa25c712d715aa4134587a84e5923f9cb5b79
ms.sourcegitcommit: 50d40c83fa641d283c097f986dde5341ebe1b44c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2018
ms.locfileid: "34452550"
---
# <a name="host-aspnet-core-on-linux-with-nginx"></a><span data-ttu-id="c072b-103">使用 Nginx 在 Linux 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="c072b-103">Host ASP.NET Core on Linux with Nginx</span></span>

<span data-ttu-id="c072b-104">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="c072b-104">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="c072b-105">本指南介绍如何在 Ubuntu 16.04 服务器上设置生产就绪 ASP.NET Core 环境。</span><span class="sxs-lookup"><span data-stu-id="c072b-105">This guide explains setting up a production-ready ASP.NET Core environment on an Ubuntu 16.04 Server.</span></span>

> [!NOTE]
> <span data-ttu-id="c072b-106">对于 Ubuntu 14.04，建议进行监控，以此作为监视 Kestrel 进程的解决方案。</span><span class="sxs-lookup"><span data-stu-id="c072b-106">For Ubuntu 14.04, *supervisord* is recommended as a solution for monitoring the Kestrel process.</span></span> <span data-ttu-id="c072b-107">在 Ubuntu 14.04 上不提供 systemd。</span><span class="sxs-lookup"><span data-stu-id="c072b-107">*systemd* isn't available on Ubuntu 14.04.</span></span> <span data-ttu-id="c072b-108">[请参阅本文档的早期版本](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c072b-108">[See previous version of this document](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md).</span></span>

<span data-ttu-id="c072b-109">本指南：</span><span class="sxs-lookup"><span data-stu-id="c072b-109">This guide:</span></span>

* <span data-ttu-id="c072b-110">将现有 ASP.NET Core 应用置于反向代理服务器后方。</span><span class="sxs-lookup"><span data-stu-id="c072b-110">Places an existing ASP.NET Core app behind a reverse proxy server.</span></span>
* <span data-ttu-id="c072b-111">设置反向代理服务器，以便将请求转发到 Kestrel Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="c072b-111">Sets up the reverse proxy server to forward requests to the Kestrel web server.</span></span>
* <span data-ttu-id="c072b-112">确保 Web 应用在启动时作为守护程序运行。</span><span class="sxs-lookup"><span data-stu-id="c072b-112">Ensures the web app runs on startup as a daemon.</span></span>
* <span data-ttu-id="c072b-113">配置进程管理工具以帮助重新启动 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c072b-113">Configures a process management tool to help restart the web app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c072b-114">系统必备</span><span class="sxs-lookup"><span data-stu-id="c072b-114">Prerequisites</span></span>

1. <span data-ttu-id="c072b-115">使用具有 sudo 特权的标准用户帐户访问 Ubuntu 16.04 服务器</span><span class="sxs-lookup"><span data-stu-id="c072b-115">Access to an Ubuntu 16.04 Server with a standard user account with sudo privilege</span></span>
1. <span data-ttu-id="c072b-116">现有 ASP.NET Core 应用</span><span class="sxs-lookup"><span data-stu-id="c072b-116">An existing ASP.NET Core app</span></span>

## <a name="copy-over-the-app"></a><span data-ttu-id="c072b-117">复制应用</span><span class="sxs-lookup"><span data-stu-id="c072b-117">Copy over the app</span></span>

<span data-ttu-id="c072b-118">从开发环境中运行 [dotnet publish](/dotnet/core/tools/dotnet-publish) 以将应用打包到可在服务器上运行的独立目录。</span><span class="sxs-lookup"><span data-stu-id="c072b-118">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the dev environment to package an app into a self-contained directory that can run on the server.</span></span>

<span data-ttu-id="c072b-119">使用集成到组织工作流的任何工具（例如 SCP、FTP）将 ASP.NET Core 应用复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="c072b-119">Copy the ASP.NET Core app to the server using whatever tool integrates into the organization's workflow (for example, SCP, FTP).</span></span> <span data-ttu-id="c072b-120">测试应用，例如：</span><span class="sxs-lookup"><span data-stu-id="c072b-120">Test the app, for example:</span></span>

* <span data-ttu-id="c072b-121">从命令行中，运行 `dotnet <app_assembly>.dll`。</span><span class="sxs-lookup"><span data-stu-id="c072b-121">From the command line, run `dotnet <app_assembly>.dll`.</span></span>
* <span data-ttu-id="c072b-122">在浏览器中，导航到 `http://<serveraddress>:<port>` 以确认应用在 Linux 上正常运行。</span><span class="sxs-lookup"><span data-stu-id="c072b-122">In a browser, navigate to `http://<serveraddress>:<port>` to verify the app works on Linux.</span></span> 
 
## <a name="configure-a-reverse-proxy-server"></a><span data-ttu-id="c072b-123">配置反向代理服务器</span><span class="sxs-lookup"><span data-stu-id="c072b-123">Configure a reverse proxy server</span></span>

<span data-ttu-id="c072b-124">反向代理是为动态 Web 应用提供服务的常见设置。</span><span class="sxs-lookup"><span data-stu-id="c072b-124">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="c072b-125">反向代理终止 HTTP 请求，并将其转发到 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="c072b-125">A reverse proxy terminates the HTTP request and forwards it to the ASP.NET Core app.</span></span>

### <a name="why-use-a-reverse-proxy-server"></a><span data-ttu-id="c072b-126">为何使用反向代理服务器？</span><span class="sxs-lookup"><span data-stu-id="c072b-126">Why use a reverse proxy server?</span></span>

<span data-ttu-id="c072b-127">Kestrel 非常适合从 ASP.NET Core 提供动态内容。</span><span class="sxs-lookup"><span data-stu-id="c072b-127">Kestrel is great for serving dynamic content from ASP.NET Core.</span></span> <span data-ttu-id="c072b-128">但是，Web 服务功能不像服务器（如 IIS、Apache 或 Nginx）那样功能丰富。</span><span class="sxs-lookup"><span data-stu-id="c072b-128">However, the web serving capabilities aren't as feature rich as servers such as IIS, Apache, or Nginx.</span></span> <span data-ttu-id="c072b-129">反向代理服务器可以从 HTTP 服务器卸载服务静态内容、缓存请求、压缩请求和 SSL 终端等工作。</span><span class="sxs-lookup"><span data-stu-id="c072b-129">A reverse proxy server can offload work such as serving static content, caching requests, compressing requests, and SSL termination from the HTTP server.</span></span> <span data-ttu-id="c072b-130">反向代理服务器可能驻留在专用计算机上，也可能与 HTTP 服务器一起部署。</span><span class="sxs-lookup"><span data-stu-id="c072b-130">A reverse proxy server may reside on a dedicated machine or may be deployed alongside an HTTP server.</span></span>

<span data-ttu-id="c072b-131">鉴于此指南的目的，使用 Nginx 的单个实例。</span><span class="sxs-lookup"><span data-stu-id="c072b-131">For the purposes of this guide, a single instance of Nginx is used.</span></span> <span data-ttu-id="c072b-132">它与 HTTP 服务器一起运行在同一服务器上。</span><span class="sxs-lookup"><span data-stu-id="c072b-132">It runs on the same server, alongside the HTTP server.</span></span> <span data-ttu-id="c072b-133">根据要求，可以选择不同的设置。</span><span class="sxs-lookup"><span data-stu-id="c072b-133">Based on requirements, a different setup may be chosen.</span></span>

<span data-ttu-id="c072b-134">由于请求是通过反向代理转接的，因此使用 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 程序包中的转接头中间件。</span><span class="sxs-lookup"><span data-stu-id="c072b-134">Because requests are forwarded by reverse proxy, use the Forwarded Headers Middleware from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="c072b-135">此中间件使用 `X-Forwarded-Proto` 标头来更新 `Request.Scheme`，使重定向 URI 和其他安全策略能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="c072b-135">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="c072b-136">当使用任何类型的身份验证中间件时，必须先运行转接头中间件。</span><span class="sxs-lookup"><span data-stu-id="c072b-136">When using any type of authentication middleware, the Forwarded Headers Middleware must run first.</span></span> <span data-ttu-id="c072b-137">此顺序可确保身份验证中间件可以使用标头值，并生成正确的重定向 URI。</span><span class="sxs-lookup"><span data-stu-id="c072b-137">This ordering ensures that the authentication middleware can consume the header values and generate correct redirect URIs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="c072b-138">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="c072b-138">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="c072b-139">在调用 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。</span><span class="sxs-lookup"><span data-stu-id="c072b-139">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="c072b-140">配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：</span><span class="sxs-lookup"><span data-stu-id="c072b-140">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="c072b-141">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="c072b-141">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="c072b-142">在调用 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 和 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。</span><span class="sxs-lookup"><span data-stu-id="c072b-142">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) and [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="c072b-143">配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：</span><span class="sxs-lookup"><span data-stu-id="c072b-143">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseIdentity();
app.UseFacebookAuthentication(new FacebookOptions()
{
    AppId = Configuration["Authentication:Facebook:AppId"],
    AppSecret = Configuration["Authentication:Facebook:AppSecret"]
});
```

---

<span data-ttu-id="c072b-144">如果没有为中间件指定 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)，则要转接的默认标头为 `None`。</span><span class="sxs-lookup"><span data-stu-id="c072b-144">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default headers to forward are `None`.</span></span>

<span data-ttu-id="c072b-145">对于托管在代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="c072b-145">Additional configuration might be required for apps hosted behind proxy servers and load balancers.</span></span> <span data-ttu-id="c072b-146">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="c072b-146">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="install-nginx"></a><span data-ttu-id="c072b-147">安装 Nginx</span><span class="sxs-lookup"><span data-stu-id="c072b-147">Install Nginx</span></span>

```bash
sudo apt-get install nginx
```

> [!NOTE]
> <span data-ttu-id="c072b-148">如果将安装可选 Nginx 模块，则可能需要从源代码生成 Nginx。</span><span class="sxs-lookup"><span data-stu-id="c072b-148">If optional Nginx modules will be installed, building Nginx from source might be required.</span></span>

<span data-ttu-id="c072b-149">使用 `apt-get` 安装 Nginx。</span><span class="sxs-lookup"><span data-stu-id="c072b-149">Use `apt-get` to install Nginx.</span></span> <span data-ttu-id="c072b-150">安装程序创建一个 System V init 脚本，该脚本运行 Nginx 作为系统启动时的守护程序。</span><span class="sxs-lookup"><span data-stu-id="c072b-150">The installer creates a System V init script that runs Nginx as daemon on system startup.</span></span> <span data-ttu-id="c072b-151">因为是首次安装 Nginx，通过运行以下命令显式启动：</span><span class="sxs-lookup"><span data-stu-id="c072b-151">Since Nginx was installed for the first time, explicitly start it by running:</span></span>

```bash
sudo service nginx start
```

<span data-ttu-id="c072b-152">确认浏览器显示 Nginx 的默认登陆页。</span><span class="sxs-lookup"><span data-stu-id="c072b-152">Verify a browser displays the default landing page for Nginx.</span></span>

### <a name="configure-nginx"></a><span data-ttu-id="c072b-153">配置 Nginx</span><span class="sxs-lookup"><span data-stu-id="c072b-153">Configure Nginx</span></span>

<span data-ttu-id="c072b-154">若要将 Nginx 配置为反向代理以将请求转接到 ASP.NET Core 应用，请修改 /etc/nginx/sites-available/default。</span><span class="sxs-lookup"><span data-stu-id="c072b-154">To configure Nginx as a reverse proxy to forward requests to your ASP.NET Core app, modify */etc/nginx/sites-available/default*.</span></span> <span data-ttu-id="c072b-155">在文本编辑器中打开它，并将内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="c072b-155">Open it in a text editor, and replace the contents with the following:</span></span>

```nginx
server {
    listen        80;
    server_name   example.com *.example.com;
    location / {
        proxy_pass         http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $http_host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

<span data-ttu-id="c072b-156">当没有匹配的 `server_name` 时，Nginx 使用默认服务器。</span><span class="sxs-lookup"><span data-stu-id="c072b-156">When no `server_name` matches, Nginx uses the default server.</span></span> <span data-ttu-id="c072b-157">如果没有定义默认服务器，则配置文件中的第一台服务器是默认服务器。</span><span class="sxs-lookup"><span data-stu-id="c072b-157">If no default server is defined, the first server in the configuration file is the default server.</span></span> <span data-ttu-id="c072b-158">作为最佳做法，添加指定默认服务器，它会在配置文件中返回状态代码 444。</span><span class="sxs-lookup"><span data-stu-id="c072b-158">As a best practice, add a specific default server which returns a status code of 444 in your configuration file.</span></span> <span data-ttu-id="c072b-159">默认的服务器配置示例是：</span><span class="sxs-lookup"><span data-stu-id="c072b-159">A default server configuration example is:</span></span>

```nginx
server {
    listen   80 default_server;
    # listen [::]:80 default_server deferred;
    return   444;
}
```

<span data-ttu-id="c072b-160">使用上述配置文件和默认服务器，Nginx 接受主机标头 `example.com` 或 `*.example.com` 端口 80 上的公共流量。</span><span class="sxs-lookup"><span data-stu-id="c072b-160">With the preceding configuration file and default server, Nginx accepts public traffic on port 80 with host header `example.com` or `*.example.com`.</span></span> <span data-ttu-id="c072b-161">与这些主机不匹配的请求不会转接到 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="c072b-161">Requests not matching these hosts won't get forwarded to Kestrel.</span></span> <span data-ttu-id="c072b-162">Nginx 将匹配的请求转接到 `http://localhost:5000` 中的 Kestrel。</span><span class="sxs-lookup"><span data-stu-id="c072b-162">Nginx forwards the matching requests to Kestrel at `http://localhost:5000`.</span></span> <span data-ttu-id="c072b-163">有关详细信息，请参阅 [nginx 如何处理请求](https://nginx.org/docs/http/request_processing.html)。</span><span class="sxs-lookup"><span data-stu-id="c072b-163">See [How nginx processes a request](https://nginx.org/docs/http/request_processing.html) for more information.</span></span>

> [!WARNING]
> <span data-ttu-id="c072b-164">未能指定正确的 [server_name 指令](https://nginx.org/docs/http/server_names.html)会公开应用的安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="c072b-164">Failure to specify a proper [server_name directive](https://nginx.org/docs/http/server_names.html) exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="c072b-165">如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.example.com`）不具有此安全风险。</span><span class="sxs-lookup"><span data-stu-id="c072b-165">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="c072b-166">有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。</span><span class="sxs-lookup"><span data-stu-id="c072b-166">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="c072b-167">完成配置 Nginx 后，运行 `sudo nginx -t` 来验证配置文件的语法。</span><span class="sxs-lookup"><span data-stu-id="c072b-167">Once the Nginx configuration is established, run `sudo nginx -t` to verify the syntax of the configuration files.</span></span> <span data-ttu-id="c072b-168">如果配置文件测试成功，可以通过运行 `sudo nginx -s reload` 强制 Nginx 选取更改。</span><span class="sxs-lookup"><span data-stu-id="c072b-168">If the configuration file test is successful, force Nginx to pick up the changes by running `sudo nginx -s reload`.</span></span>

## <a name="monitoring-the-app"></a><span data-ttu-id="c072b-169">监视应用</span><span class="sxs-lookup"><span data-stu-id="c072b-169">Monitoring the app</span></span>

<span data-ttu-id="c072b-170">服务器设置为将对 `http://<serveraddress>:80` 发起的请求转接到在 `http://127.0.0.1:5000` 中的 Kestrel 上运行的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="c072b-170">The server is setup to forward requests made to `http://<serveraddress>:80` on to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span> <span data-ttu-id="c072b-171">但是，未将 Nginx 设置为管理 Kestrel 进程。</span><span class="sxs-lookup"><span data-stu-id="c072b-171">However, Nginx isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="c072b-172">systemd 可用于创建服务文件以启动和监视基础 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c072b-172">*systemd* can be used to create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="c072b-173">systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。</span><span class="sxs-lookup"><span data-stu-id="c072b-173">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="c072b-174">创建服务文件</span><span class="sxs-lookup"><span data-stu-id="c072b-174">Create the service file</span></span>

<span data-ttu-id="c072b-175">创建服务定义文件：</span><span class="sxs-lookup"><span data-stu-id="c072b-175">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="c072b-176">以下是应用的一个示例服务文件：</span><span class="sxs-lookup"><span data-stu-id="c072b-176">The following is an example service file for the app:</span></span>

```ini
[Unit]
Description=Example .NET Web API App running on Ubuntu

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
RestartSec=10  # Restart service after 10 seconds if dotnet service crashes
SyslogIdentifier=dotnet-example
User=www-data
Environment=ASPNETCORE_ENVIRONMENT=Production
Environment=DOTNET_PRINT_TELEMETRY_MESSAGE=false

[Install]
WantedBy=multi-user.target
```

<span data-ttu-id="c072b-177">如果配置未使用用户 www-data，则必须先创建此处定义的用户，并为该用户提供适当的文件所有权。</span><span class="sxs-lookup"><span data-stu-id="c072b-177">If the user *www-data* isn't used by the configuration, the user defined here must be created first and given proper ownership for files.</span></span>

<span data-ttu-id="c072b-178">Linux 具有区分大小写的文件系统。</span><span class="sxs-lookup"><span data-stu-id="c072b-178">Linux has a case-sensitive file system.</span></span> <span data-ttu-id="c072b-179">将 ASPNETCORE_ENVIRONMENT 设置为“生产”会导致搜索配置文件 appsettings.Production.json，而不是 appsettings.production.json。</span><span class="sxs-lookup"><span data-stu-id="c072b-179">Setting ASPNETCORE_ENVIRONMENT to "Production" results in searching for the configuration file *appsettings.Production.json*, not *appsettings.production.json*.</span></span>

> [!NOTE]
> <span data-ttu-id="c072b-180">必须转义某些值（例如，SQL 连接字符串）以供配置提供程序读取环境变量。</span><span class="sxs-lookup"><span data-stu-id="c072b-180">Some values (for example, SQL connection strings) must be escaped for the configuration providers to read the environment variables.</span></span> <span data-ttu-id="c072b-181">使用以下命令生成适当的转义值以供在配置文件中使用：</span><span class="sxs-lookup"><span data-stu-id="c072b-181">Use the following command to generate a properly escaped value for use in the configuration file:</span></span>
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

<span data-ttu-id="c072b-182">保存该文件并启用该服务。</span><span class="sxs-lookup"><span data-stu-id="c072b-182">Save the file and enable the service.</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="c072b-183">启用该服务，并确认它正在运行。</span><span class="sxs-lookup"><span data-stu-id="c072b-183">Start the service and verify that it's running.</span></span>

```
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on Ubuntu
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

<span data-ttu-id="c072b-184">在配置了反向代理并通过 systemd 管理 Kestrel 后，Web 应用现已完全配置，并能在本地计算机上的浏览器中从 `http://localhost` 进行访问。</span><span class="sxs-lookup"><span data-stu-id="c072b-184">With the reverse proxy configured and Kestrel managed through systemd, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="c072b-185">也可以从远程计算机进行访问，同时限制可能进行阻止的任何防火墙。</span><span class="sxs-lookup"><span data-stu-id="c072b-185">It's also accessible from a remote machine, barring any firewall that might be blocking.</span></span> <span data-ttu-id="c072b-186">检查响应标头，`Server` 标头显示由 Kestrel 所提供的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="c072b-186">Inspecting the response headers, the `Server` header shows the ASP.NET Core app being served by Kestrel.</span></span>

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="c072b-187">查看日志</span><span class="sxs-lookup"><span data-stu-id="c072b-187">Viewing logs</span></span>

<span data-ttu-id="c072b-188">使用 Kestrel 的 Web 应用是通过 `systemd` 进行管理的，因此所有事件和进程都被记录到集中日志。</span><span class="sxs-lookup"><span data-stu-id="c072b-188">Since the web app using Kestrel is managed using `systemd`, all events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="c072b-189">但是，此日志包含由 `systemd` 管理的所有服务和进程的全部条目。</span><span class="sxs-lookup"><span data-stu-id="c072b-189">However, this journal includes all entries for all services and processes managed by `systemd`.</span></span> <span data-ttu-id="c072b-190">若要查看特定于 `kestrel-hellomvc.service` 的项，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="c072b-190">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="c072b-191">有关进一步筛选，使用时间选项（如 `--since today`、`--until 1 hour ago`）或这些选项的组合可以减少返回的条目数。</span><span class="sxs-lookup"><span data-stu-id="c072b-191">For further filtering, time options such as `--since today`, `--until 1 hour ago` or a combination of these can reduce the amount of entries returned.</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a><span data-ttu-id="c072b-192">保护应用</span><span class="sxs-lookup"><span data-stu-id="c072b-192">Securing the app</span></span>

### <a name="enable-apparmor"></a><span data-ttu-id="c072b-193">启用 AppArmor</span><span class="sxs-lookup"><span data-stu-id="c072b-193">Enable AppArmor</span></span>

<span data-ttu-id="c072b-194">Linux 安全模块 (LSM) 是一个框架，它是自 Linux 2.6 后的 Linux kernel 的一部分。</span><span class="sxs-lookup"><span data-stu-id="c072b-194">Linux Security Modules (LSM) is a framework that's part of the Linux kernel since Linux 2.6.</span></span> <span data-ttu-id="c072b-195">LSM 支持安全模块的不同实现。</span><span class="sxs-lookup"><span data-stu-id="c072b-195">LSM supports different implementations of security modules.</span></span> <span data-ttu-id="c072b-196">[AppArmor](https://wiki.ubuntu.com/AppArmor) 是实现强制访问控制系统的 LSM，它允许将程序限制在一组有限的资源内。</span><span class="sxs-lookup"><span data-stu-id="c072b-196">[AppArmor](https://wiki.ubuntu.com/AppArmor) is a LSM that implements a Mandatory Access Control system which allows confining the program to a limited set of resources.</span></span> <span data-ttu-id="c072b-197">确保已启用并成功配置 AppArmor。</span><span class="sxs-lookup"><span data-stu-id="c072b-197">Ensure AppArmor is enabled and properly configured.</span></span>

### <a name="configuring-the-firewall"></a><span data-ttu-id="c072b-198">配置防火墙</span><span class="sxs-lookup"><span data-stu-id="c072b-198">Configuring the firewall</span></span>

<span data-ttu-id="c072b-199">关闭所有未使用的外部端口。</span><span class="sxs-lookup"><span data-stu-id="c072b-199">Close off all external ports that are not in use.</span></span> <span data-ttu-id="c072b-200">通过为配置防火墙提供命令行接口，不复杂的防火墙 (ufw) 为 `iptables` 提供了前端。</span><span class="sxs-lookup"><span data-stu-id="c072b-200">Uncomplicated firewall (ufw) provides a front end for `iptables` by providing a command line interface for configuring the firewall.</span></span> <span data-ttu-id="c072b-201">确认已配置 `ufw` 以允许所需的任何端口上的流量。</span><span class="sxs-lookup"><span data-stu-id="c072b-201">Verify that `ufw` is configured to allow traffic on any ports needed.</span></span>

```bash
sudo apt-get install ufw
sudo ufw enable

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### <a name="securing-nginx"></a><span data-ttu-id="c072b-202">保护 Nginx</span><span class="sxs-lookup"><span data-stu-id="c072b-202">Securing Nginx</span></span>

<span data-ttu-id="c072b-203">Nginx 的默认分配不启用 SSL。</span><span class="sxs-lookup"><span data-stu-id="c072b-203">The default distribution of Nginx doesn't enable SSL.</span></span> <span data-ttu-id="c072b-204">若要启用其他安全功能，请从源生成。</span><span class="sxs-lookup"><span data-stu-id="c072b-204">To enable additional security features, build from source.</span></span>

#### <a name="download-the-source-and-install-the-build-dependencies"></a><span data-ttu-id="c072b-205">下载源并安装生成依赖项</span><span class="sxs-lookup"><span data-stu-id="c072b-205">Download the source and install the build dependencies</span></span>

```bash
# Install the build dependencies
sudo apt-get update
sudo apt-get install build-essential zlib1g-dev libpcre3-dev libssl-dev libxslt1-dev libxml2-dev libgd2-xpm-dev libgeoip-dev libgoogle-perftools-dev libperl-dev

# Download Nginx 1.10.0 or latest
wget http://www.nginx.org/download/nginx-1.10.0.tar.gz
tar zxf nginx-1.10.0.tar.gz
```

#### <a name="change-the-nginx-response-name"></a><span data-ttu-id="c072b-206">更改 Nginx 响应名称</span><span class="sxs-lookup"><span data-stu-id="c072b-206">Change the Nginx response name</span></span>

<span data-ttu-id="c072b-207">编辑 src/http/ngx_http_header_filter_module.c：</span><span class="sxs-lookup"><span data-stu-id="c072b-207">Edit *src/http/ngx_http_header_filter_module.c*:</span></span>

```c
static char ngx_http_server_string[] = "Server: Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Web Server" CRLF;
```

#### <a name="configure-the-options-and-build"></a><span data-ttu-id="c072b-208">配置选项和生成</span><span class="sxs-lookup"><span data-stu-id="c072b-208">Configure the options and build</span></span>

<span data-ttu-id="c072b-209">正则表达式需要 PCRE 库。</span><span class="sxs-lookup"><span data-stu-id="c072b-209">The PCRE library is required for regular expressions.</span></span> <span data-ttu-id="c072b-210">正则表达式用于 ngx_http_rewrite_module 的位置指令。</span><span class="sxs-lookup"><span data-stu-id="c072b-210">Regular expressions are used in the location directive for the ngx_http_rewrite_module.</span></span> <span data-ttu-id="c072b-211">http_ssl_module adds HTTPS 协议支持。</span><span class="sxs-lookup"><span data-stu-id="c072b-211">The http_ssl_module adds HTTPS protocol support.</span></span>

<span data-ttu-id="c072b-212">请考虑使用诸如“ModSecurity”的 Web 应用防火墙来加强对应用的保护。</span><span class="sxs-lookup"><span data-stu-id="c072b-212">Consider using a web app firewall like *ModSecurity* to harden the app.</span></span>

```bash
./configure
--with-pcre=../pcre-8.38
--with-zlib=../zlib-1.2.8
--with-http_ssl_module
--with-stream
--with-mail=dynamic
```

#### <a name="configure-ssl"></a><span data-ttu-id="c072b-213">配置 SSL</span><span class="sxs-lookup"><span data-stu-id="c072b-213">Configure SSL</span></span>

* <span data-ttu-id="c072b-214">通过指定由受信任的证书颁发机构 (CA) 颁发的有效证书来配置服务器，以侦听端口 `443` 上的 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="c072b-214">Configure the server to listen to HTTPS traffic on port `443` by specifying a valid certificate issued by a trusted Certificate Authority (CA).</span></span>

* <span data-ttu-id="c072b-215">通过采用以下“/etc/nginx/nginx.conf”文件中所示的某些做法来增强安全保护。</span><span class="sxs-lookup"><span data-stu-id="c072b-215">Harden the security by employing some of the practices depicted in the following */etc/nginx/nginx.conf* file.</span></span> <span data-ttu-id="c072b-216">示例包括选择更强的密码并将通过 HTTP 的所有流量重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="c072b-216">Examples include choosing a stronger cipher and redirecting all traffic over HTTP to HTTPS.</span></span>

* <span data-ttu-id="c072b-217">添加 `HTTP Strict-Transport-Security` (HSTS) 标头可确保由客户端发起的所有后续请求都仅通过 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="c072b-217">Adding an `HTTP Strict-Transport-Security` (HSTS) header ensures all subsequent requests made by the client are over HTTPS only.</span></span>

* <span data-ttu-id="c072b-218">如果以后会禁用 SSL，则不要添加 Strict-Transport-Security 标头或选择相应的 `max-age`。</span><span class="sxs-lookup"><span data-stu-id="c072b-218">Don't add the Strict-Transport-Security header or chose an appropriate `max-age` if SSL will be disabled in the future.</span></span>

<span data-ttu-id="c072b-219">添加 /etc/nginx/proxy.conf 配置文件：</span><span class="sxs-lookup"><span data-stu-id="c072b-219">Add the */etc/nginx/proxy.conf* configuration file:</span></span>

[!code-nginx[](linux-nginx/proxy.conf)]

<span data-ttu-id="c072b-220">编辑 /etc/nginx/nginx.conf 配置文件。</span><span class="sxs-lookup"><span data-stu-id="c072b-220">Edit the */etc/nginx/nginx.conf* configuration file.</span></span> <span data-ttu-id="c072b-221">示例包含一个配置文件中的 `http` 和 `server` 部分。</span><span class="sxs-lookup"><span data-stu-id="c072b-221">The example contains both `http` and `server` sections in one configuration file.</span></span>

[!code-nginx[](linux-nginx/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a><span data-ttu-id="c072b-222">保护 Nginx 免受点击劫持的侵害</span><span class="sxs-lookup"><span data-stu-id="c072b-222">Secure Nginx from clickjacking</span></span>
<span data-ttu-id="c072b-223">点击劫持是收集受感染用户的点击数的恶意技术。</span><span class="sxs-lookup"><span data-stu-id="c072b-223">Clickjacking is a malicious technique to collect an infected user's clicks.</span></span> <span data-ttu-id="c072b-224">点击劫持诱使受害者（访问者）点击受感染的网站。</span><span class="sxs-lookup"><span data-stu-id="c072b-224">Clickjacking tricks the victim (visitor) into clicking on an infected site.</span></span> <span data-ttu-id="c072b-225">使用 X-FRAME-OPTIONS 保护站点。</span><span class="sxs-lookup"><span data-stu-id="c072b-225">Use X-FRAME-OPTIONS to secure the site.</span></span>

<span data-ttu-id="c072b-226">编辑 nginx.conf 文件：</span><span class="sxs-lookup"><span data-stu-id="c072b-226">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="c072b-227">添加行 `add_header X-Frame-Options "SAMEORIGIN";` 并保存文件，然后重新启动 Nginx。</span><span class="sxs-lookup"><span data-stu-id="c072b-227">Add the line `add_header X-Frame-Options "SAMEORIGIN";` and save the file, then restart Nginx.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="c072b-228">MIME 类型探查</span><span class="sxs-lookup"><span data-stu-id="c072b-228">MIME-type sniffing</span></span>

<span data-ttu-id="c072b-229">此标头可阻止大部分浏览器通过 MIME 方式探查来自已声明内容类型的响应，因为标头会指示浏览器不要替代响应内容类型。</span><span class="sxs-lookup"><span data-stu-id="c072b-229">This header prevents most browsers from MIME-sniffing a response away from the declared content type, as the header instructs the browser not to override the response content type.</span></span> <span data-ttu-id="c072b-230">使用 `nosniff` 选项后，如果服务器认为内容是“文本/html”，则浏览器将其显示为“文本/html”。</span><span class="sxs-lookup"><span data-stu-id="c072b-230">With the `nosniff` option, if the server says the content is "text/html", the browser renders it as "text/html".</span></span>

<span data-ttu-id="c072b-231">编辑 nginx.conf 文件：</span><span class="sxs-lookup"><span data-stu-id="c072b-231">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="c072b-232">添加行 `add_header X-Content-Type-Options "nosniff";` 并保存文件，然后重新启动 Nginx。</span><span class="sxs-lookup"><span data-stu-id="c072b-232">Add the line `add_header X-Content-Type-Options "nosniff";` and save the file, then restart Nginx.</span></span>
