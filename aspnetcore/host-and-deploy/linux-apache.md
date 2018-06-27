---
title: 使用 Apache 在 Linux 上托管 ASP.NET Core
description: 了解如何在 CentOS 上将 Apache 设置为反向代理服务器，以将 HTTP 流量重定向到在 Kestrel 上运行的 ASP.NET Core Web 应用。
author: spboyer
ms.author: spboyer
ms.custom: mvc
ms.date: 03/13/2018
uid: host-and-deploy/linux-apache
ms.openlocfilehash: 69e92af08eabede023608e612f1fbd48a8f2608e
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275446"
---
# <a name="host-aspnet-core-on-linux-with-apache"></a><span data-ttu-id="ffb23-103">使用 Apache 在 Linux 上托管 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ffb23-103">Host ASP.NET Core on Linux with Apache</span></span>

<span data-ttu-id="ffb23-104">作者：[Shayne Boyer](https://github.com/spboyer)</span><span class="sxs-lookup"><span data-stu-id="ffb23-104">By [Shayne Boyer](https://github.com/spboyer)</span></span>

<span data-ttu-id="ffb23-105">使用本指南，了解如何在 [CentOS 7](https://www.centos.org/) 上将 [Apache](https://httpd.apache.org/) 设置为反向代理服务器，以将 HTTP 流量重定向到在 [Kestrel](xref:fundamentals/servers/kestrel) 上运行的 ASP.NET Core Web 应用。</span><span class="sxs-lookup"><span data-stu-id="ffb23-105">Using this guide, learn how to set up [Apache](https://httpd.apache.org/) as a reverse proxy server on [CentOS 7](https://www.centos.org/) to redirect HTTP traffic to an ASP.NET Core web app running on [Kestrel](xref:fundamentals/servers/kestrel).</span></span> <span data-ttu-id="ffb23-106">[mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) 和相关模块可创建服务器的反向代理。</span><span class="sxs-lookup"><span data-stu-id="ffb23-106">The [mod_proxy extension](http://httpd.apache.org/docs/2.4/mod/mod_proxy.html) and related modules create the server's reverse proxy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffb23-107">系统必备</span><span class="sxs-lookup"><span data-stu-id="ffb23-107">Prerequisites</span></span>

1. <span data-ttu-id="ffb23-108">运行 CentOS 7 的服务器，使用具有 sudo 特权的标准用户帐户。</span><span class="sxs-lookup"><span data-stu-id="ffb23-108">Server running CentOS 7 with a standard user account with sudo privilege.</span></span>
1. <span data-ttu-id="ffb23-109">在服务器上安装 .NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="ffb23-109">Install the .NET Core runtime on the server.</span></span>
   1. <span data-ttu-id="ffb23-110">访问 [.NET Core“所有下载”页](https://www.microsoft.com/net/download/all)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-110">Visit the [.NET Core All Downloads page](https://www.microsoft.com/net/download/all).</span></span>
   1. <span data-ttu-id="ffb23-111">从“运行时”下的列表中选择最新的非预览运行时。</span><span class="sxs-lookup"><span data-stu-id="ffb23-111">Select the latest non-preview runtime from the list under **Runtime**.</span></span>
   1. <span data-ttu-id="ffb23-112">选择并执行适用于 CentOS/Oracle 的说明。</span><span class="sxs-lookup"><span data-stu-id="ffb23-112">Select and follow the instructions for CentOS/Oracle.</span></span>
1. <span data-ttu-id="ffb23-113">一个现有 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="ffb23-113">An existing ASP.NET Core app.</span></span>

## <a name="publish-and-copy-over-the-app"></a><span data-ttu-id="ffb23-114">通过应用发布和复制</span><span class="sxs-lookup"><span data-stu-id="ffb23-114">Publish and copy over the app</span></span>

<span data-ttu-id="ffb23-115">配置应用以进行[依赖框架的部署](/dotnet/core/deploying/#framework-dependent-deployments-fdd)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-115">Configure the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd).</span></span>

<span data-ttu-id="ffb23-116">在开发环境中运行 [dotnet publish](/dotnet/core/tools/dotnet-publish)，将应用打包到可在服务器上运行的目录中（例如 bin/Release/&lt;target_framework_moniker&gt;/publish）：</span><span class="sxs-lookup"><span data-stu-id="ffb23-116">Run [dotnet publish](/dotnet/core/tools/dotnet-publish) from the development environment to package an app into a directory (for example, *bin/Release/&lt;target_framework_moniker&gt;/publish*) that can run on the server:</span></span>

```console
dotnet publish --configuration Release
```

<span data-ttu-id="ffb23-117">如果不希望维护服务器上的 .NET Core 运行时，还可将应用发布为[独立部署](/dotnet/core/deploying/#self-contained-deployments-scd)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-117">The app can also be published as a [self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) if you prefer not to maintain the .NET Core runtime on the server.</span></span>

<span data-ttu-id="ffb23-118">使用集成到组织工作流的工具（例如 SCP、SFTP）将 ASP.NET Core 应用复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="ffb23-118">Copy the ASP.NET Core app to the server using a tool that integrates into the organization's workflow (for example, SCP, SFTP).</span></span> <span data-ttu-id="ffb23-119">通常可在 var 目录（例如 var/aspnetcore/hellomvc）下找到 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="ffb23-119">It's common to locate web apps under the *var* directory (for example, *var/aspnetcore/hellomvc*).</span></span>

> [!NOTE]
> <span data-ttu-id="ffb23-120">在生产部署方案中，持续集成工作流会执行发布应用并将资产复制到服务器的工作。</span><span class="sxs-lookup"><span data-stu-id="ffb23-120">Under a production deployment scenario, a continuous integration workflow does the work of publishing the app and copying the assets to the server.</span></span>

## <a name="configure-a-proxy-server"></a><span data-ttu-id="ffb23-121">配置代理服务器</span><span class="sxs-lookup"><span data-stu-id="ffb23-121">Configure a proxy server</span></span>

<span data-ttu-id="ffb23-122">反向代理是为动态 Web 应用提供服务的常见设置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-122">A reverse proxy is a common setup for serving dynamic web apps.</span></span> <span data-ttu-id="ffb23-123">反向代理终止 HTTP 请求，并将其转发到 ASP.NET 应用。</span><span class="sxs-lookup"><span data-stu-id="ffb23-123">The reverse proxy terminates the HTTP request and forwards it to the ASP.NET app.</span></span>

<span data-ttu-id="ffb23-124">代理服务器将客户端请求转发到另一个服务器，而不是自身实现这些请求。</span><span class="sxs-lookup"><span data-stu-id="ffb23-124">A proxy server is one which forwards client requests to another server instead of fulfilling requests itself.</span></span> <span data-ttu-id="ffb23-125">反向代理转发到固定的目标，通常代表任意客户端。</span><span class="sxs-lookup"><span data-stu-id="ffb23-125">A reverse proxy forwards to a fixed destination, typically on behalf of arbitrary clients.</span></span> <span data-ttu-id="ffb23-126">在本指南中，Apache 被配置为反向代理，在 Kestrel 为 ASP.NET Core 应用提供服务的同一服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="ffb23-126">In this guide, Apache is configured as the reverse proxy running on the same server that Kestrel is serving the ASP.NET Core app.</span></span>

<span data-ttu-id="ffb23-127">由于请求是通过反向代理转接的，因此使用 [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) 包中的[转接头中间件](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-127">Because requests are forwarded by reverse proxy, use the [Forwarded Headers Middleware](xref:host-and-deploy/proxy-load-balancer) from the [Microsoft.AspNetCore.HttpOverrides](https://www.nuget.org/packages/Microsoft.AspNetCore.HttpOverrides/) package.</span></span> <span data-ttu-id="ffb23-128">此中间件使用 `X-Forwarded-Proto` 标头来更新 `Request.Scheme`，使重定向 URI 和其他安全策略能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="ffb23-128">The middleware updates the `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="ffb23-129">调用转接头中间件后，必须放置依赖于该架构的组件，例如身份验证、链接生成、重定向和地理位置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-129">Any component that depends on the scheme, such as authentication, link generation, redirects, and geolocation, must be placed after invoking the Forwarded Headers Middleware.</span></span> <span data-ttu-id="ffb23-130">作为一般规则，转接头中间件应在诊断和错误处理中间件以外的其他中间件之前运行。</span><span class="sxs-lookup"><span data-stu-id="ffb23-130">As a general rule, Forwarded Headers Middleware should run before other middleware except diagnostics and error handling middleware.</span></span> <span data-ttu-id="ffb23-131">此顺序可确保依赖于转接头信息的中间件可以使用标头值进行处理。</span><span class="sxs-lookup"><span data-stu-id="ffb23-131">This ordering ensures that the middleware relying on forwarded headers information can consume the header values for processing.</span></span>

::: moniker range=">= aspnetcore-2.0"
> [!NOTE]
> <span data-ttu-id="ffb23-132">使用或不使用反向代理服务器进行配置对 ASP.NET Core 2.0 或更高版本的应用来说都是有效且受支持的托管配置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-132">Either configuration&mdash;with or without a reverse proxy server&mdash;is a valid and supported hosting configuration for ASP.NET Core 2.0 or later apps.</span></span> <span data-ttu-id="ffb23-133">有关详细信息，请参阅[何时结合使用 Kestrel 和反向代理](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-133">For more information, see [When to use Kestrel with a reverse proxy](xref:fundamentals/servers/kestrel#when-to-use-kestrel-with-a-reverse-proxy).</span></span>
::: moniker-end

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="ffb23-134">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="ffb23-134">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="ffb23-135">在调用 [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。</span><span class="sxs-lookup"><span data-stu-id="ffb23-135">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseAuthentication](/dotnet/api/microsoft.aspnetcore.builder.authappbuilderextensions.useauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="ffb23-136">配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：</span><span class="sxs-lookup"><span data-stu-id="ffb23-136">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="ffb23-137">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="ffb23-137">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="ffb23-138">在调用 [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) 和 [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) 或类似的身份验证方案中间件之前，调用 `Startup.Configure` 中的 [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) 方法。</span><span class="sxs-lookup"><span data-stu-id="ffb23-138">Invoke the [UseForwardedHeaders](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersextensions.useforwardedheaders) method in `Startup.Configure` before calling [UseIdentity](/dotnet/api/microsoft.aspnetcore.builder.builderextensions.useidentity) and [UseFacebookAuthentication](/dotnet/api/microsoft.aspnetcore.builder.facebookappbuilderextensions.usefacebookauthentication) or similar authentication scheme middleware.</span></span> <span data-ttu-id="ffb23-139">配置中间件以转接 `X-Forwarded-For` 和 `X-Forwarded-Proto` 标头：</span><span class="sxs-lookup"><span data-stu-id="ffb23-139">Configure the middleware to forward the `X-Forwarded-For` and `X-Forwarded-Proto` headers:</span></span>

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

<span data-ttu-id="ffb23-140">如果没有为中间件指定 [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions)，则要转接的默认标头为 `None`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-140">If no [ForwardedHeadersOptions](/dotnet/api/microsoft.aspnetcore.builder.forwardedheadersoptions) are specified to the middleware, the default headers to forward are `None`.</span></span>

<span data-ttu-id="ffb23-141">对于托管在代理服务器和负载均衡器后方的应用，可能需要附加配置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-141">Additional configuration might be required for apps hosted behind proxy servers and load balancers.</span></span> <span data-ttu-id="ffb23-142">有关详细信息，请参阅[配置 ASP.NET Core 以使用代理服务器和负载均衡器](xref:host-and-deploy/proxy-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-142">For more information, see [Configure ASP.NET Core to work with proxy servers and load balancers](xref:host-and-deploy/proxy-load-balancer).</span></span>

### <a name="install-apache"></a><span data-ttu-id="ffb23-143">安装 Apache</span><span class="sxs-lookup"><span data-stu-id="ffb23-143">Install Apache</span></span>

<span data-ttu-id="ffb23-144">将 CentOS 包更新为其最新稳定版本：</span><span class="sxs-lookup"><span data-stu-id="ffb23-144">Update CentOS packages to their latest stable versions:</span></span>

```bash
sudo yum update -y
```

<span data-ttu-id="ffb23-145">使用单个 `yum` 命令在 CentOS 上安装 Apache Web 服务器：</span><span class="sxs-lookup"><span data-stu-id="ffb23-145">Install the Apache web server on CentOS with a single `yum` command:</span></span>

```bash
sudo yum -y install httpd mod_ssl
```

<span data-ttu-id="ffb23-146">运行该命令后的示例输出：</span><span class="sxs-lookup"><span data-stu-id="ffb23-146">Sample output after running the command:</span></span>

```bash
Downloading packages:
httpd-2.4.6-40.el7.centos.4.x86_64.rpm               | 2.7 MB  00:00:01
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Installing : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 
Verifying  : httpd-2.4.6-40.el7.centos.4.x86_64      1/1 

Installed:
httpd.x86_64 0:2.4.6-40.el7.centos.4

Complete!
```

> [!NOTE]
> <span data-ttu-id="ffb23-147">在此示例中，输出反映了 httpd.86_64，因为 CentOS 7 版本是 64 位的。</span><span class="sxs-lookup"><span data-stu-id="ffb23-147">In this example, the output reflects httpd.86_64 since the CentOS 7 version is 64 bit.</span></span> <span data-ttu-id="ffb23-148">若要验证 Apache 的安装位置，请从命令提示符运行 `whereis httpd`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-148">To verify where Apache is installed, run `whereis httpd` from a command prompt.</span></span>

### <a name="configure-apache"></a><span data-ttu-id="ffb23-149">配置 Apache</span><span class="sxs-lookup"><span data-stu-id="ffb23-149">Configure Apache</span></span>

<span data-ttu-id="ffb23-150">Apache 的配置文件位于 `/etc/httpd/conf.d/` 目录内。</span><span class="sxs-lookup"><span data-stu-id="ffb23-150">Configuration files for Apache are located within the `/etc/httpd/conf.d/` directory.</span></span> <span data-ttu-id="ffb23-151">除了 `/etc/httpd/conf.modules.d/` 中的模块配置文件外（其中包含加载模块所需的任何配置文件），将对任何带 .conf 扩展名的文件按字母顺序进行处理。</span><span class="sxs-lookup"><span data-stu-id="ffb23-151">Any file with the *.conf* extension is processed in alphabetical order in addition to the module configuration files in `/etc/httpd/conf.modules.d/`, which contains any configuration files necessary to load modules.</span></span>

<span data-ttu-id="ffb23-152">为应用创建名为 hellomvc.conf 的配置文件：</span><span class="sxs-lookup"><span data-stu-id="ffb23-152">Create a configuration file, named *hellomvc.conf*, for the app:</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ServerName www.example.com
    ServerAlias *.example.com
    ErrorLog ${APACHE_LOG_DIR}hellomvc-error.log
    CustomLog ${APACHE_LOG_DIR}hellomvc-access.log common
</VirtualHost>
```

<span data-ttu-id="ffb23-153">`VirtualHost` 块可以在服务器上的一个或多个文件中多次出现。</span><span class="sxs-lookup"><span data-stu-id="ffb23-153">The `VirtualHost` block can appear multiple times, in one or more files on a server.</span></span> <span data-ttu-id="ffb23-154">在前面的配置文件中，Apache 接受端口 80 上的公共流量。</span><span class="sxs-lookup"><span data-stu-id="ffb23-154">In the preceding configuration file, Apache accepts public traffic on port 80.</span></span> <span data-ttu-id="ffb23-155">正在向域 `www.example.com` 提供服务，`*.example.com` 别名解析为同一网站。</span><span class="sxs-lookup"><span data-stu-id="ffb23-155">The domain `www.example.com` is being served, and the `*.example.com` alias resolves to the same website.</span></span> <span data-ttu-id="ffb23-156">有关详细信息，请参阅[基于名称的虚拟主机支持](https://httpd.apache.org/docs/current/vhosts/name-based.html)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-156">See [Name-based virtual host support](https://httpd.apache.org/docs/current/vhosts/name-based.html) for more information.</span></span> <span data-ttu-id="ffb23-157">请求会通过代理从根位置转到 127.0.0.1 处的服务器的端口 5000。</span><span class="sxs-lookup"><span data-stu-id="ffb23-157">Requests are proxied at the root to port 5000 of the server at 127.0.0.1.</span></span> <span data-ttu-id="ffb23-158">对于双向通信，需要 `ProxyPass` 和 `ProxyPassReverse`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-158">For bi-directional communication, `ProxyPass` and `ProxyPassReverse` are required.</span></span>

> [!WARNING]
> <span data-ttu-id="ffb23-159">未能指定 VirtualHost 块中的正确 [ServerName 指令](https://httpd.apache.org/docs/current/mod/core.html#servername)会公开应用的安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="ffb23-159">Failure to specify a proper [ServerName directive](https://httpd.apache.org/docs/current/mod/core.html#servername) in the **VirtualHost** block exposes your app to security vulnerabilities.</span></span> <span data-ttu-id="ffb23-160">如果可控制整个父域（区别于易受攻击的 `*.com`），则子域通配符绑定（例如，`*.example.com`）不具有此安全风险。</span><span class="sxs-lookup"><span data-stu-id="ffb23-160">Subdomain wildcard binding (for example, `*.example.com`) doesn't pose this security risk if you control the entire parent domain (as opposed to `*.com`, which is vulnerable).</span></span> <span data-ttu-id="ffb23-161">有关详细信息，请参阅 [rfc7230 第 5.4 条](https://tools.ietf.org/html/rfc7230#section-5.4)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-161">See [rfc7230 section-5.4](https://tools.ietf.org/html/rfc7230#section-5.4) for more information.</span></span>

<span data-ttu-id="ffb23-162">可以使用 `ErrorLog` 和 `CustomLog` 指令配置每个 `VirtualHost` 的日志记录。</span><span class="sxs-lookup"><span data-stu-id="ffb23-162">Logging can be configured per `VirtualHost` using `ErrorLog` and `CustomLog` directives.</span></span> <span data-ttu-id="ffb23-163">`ErrorLog` 是服务器记录错误的位置，`CustomLog` 则设置文件名和日志文件的格式。</span><span class="sxs-lookup"><span data-stu-id="ffb23-163">`ErrorLog` is the location where the server logs errors, and `CustomLog` sets the filename and format of log file.</span></span> <span data-ttu-id="ffb23-164">在这种情况下，这是记录请求信息的位置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-164">In this case, this is where request information is logged.</span></span> <span data-ttu-id="ffb23-165">每个请求将各占一行。</span><span class="sxs-lookup"><span data-stu-id="ffb23-165">There's one line for each request.</span></span>

<span data-ttu-id="ffb23-166">保存文件，并测试配置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-166">Save the file and test the configuration.</span></span> <span data-ttu-id="ffb23-167">如果一切正常，响应应为 `Syntax [OK]`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-167">If everything passes, the response should be `Syntax [OK]`.</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="ffb23-168">重新启动 Apache：</span><span class="sxs-lookup"><span data-stu-id="ffb23-168">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

## <a name="monitoring-the-app"></a><span data-ttu-id="ffb23-169">监视应用</span><span class="sxs-lookup"><span data-stu-id="ffb23-169">Monitoring the app</span></span>

<span data-ttu-id="ffb23-170">Apache 现在已设置为将对 `http://localhost:80` 发起的请求转发到运行在 `http://127.0.0.1:5000` 处的 Kestrel 上的 ASP.NET Core 应用。</span><span class="sxs-lookup"><span data-stu-id="ffb23-170">Apache is now setup to forward requests made to `http://localhost:80` to the ASP.NET Core app running on Kestrel at `http://127.0.0.1:5000`.</span></span>  <span data-ttu-id="ffb23-171">但是，未将 Apache 设置为管理 Kestrel 进程。</span><span class="sxs-lookup"><span data-stu-id="ffb23-171">However, Apache isn't set up to manage the Kestrel process.</span></span> <span data-ttu-id="ffb23-172">使用 systemd，并创建服务文件以启动和监视基础 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="ffb23-172">Use *systemd* and create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="ffb23-173">systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。</span><span class="sxs-lookup"><span data-stu-id="ffb23-173">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="ffb23-174">创建服务文件</span><span class="sxs-lookup"><span data-stu-id="ffb23-174">Create the service file</span></span>

<span data-ttu-id="ffb23-175">创建服务定义文件：</span><span class="sxs-lookup"><span data-stu-id="ffb23-175">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="ffb23-176">应用的一个示例服务文件：</span><span class="sxs-lookup"><span data-stu-id="ffb23-176">An example service file for the app:</span></span>

```
[Unit]
Description=Example .NET Web API App running on CentOS 7

[Service]
WorkingDirectory=/var/aspnetcore/hellomvc
ExecStart=/usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
Restart=always
# Restart service after 10 seconds if dotnet service crashes
RestartSec=10
SyslogIdentifier=dotnet-example
User=apache
Environment=ASPNETCORE_ENVIRONMENT=Production 

[Install]
WantedBy=multi-user.target
```

> [!NOTE]
> <span data-ttu-id="ffb23-177">**用户** &mdash; 如果配置未使用用户 apache，则必须先创建用户，并为该用户提供适当的文件所有权。</span><span class="sxs-lookup"><span data-stu-id="ffb23-177">**User** &mdash; If the user *apache* isn't used by the configuration, the user must be created first and given proper ownership for files.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb23-178">必须转义某些值（例如，SQL 连接字符串）以供配置提供程序读取环境变量。</span><span class="sxs-lookup"><span data-stu-id="ffb23-178">Some values (for example, SQL connection strings) must be escaped for the configuration providers to read the environment variables.</span></span> <span data-ttu-id="ffb23-179">使用以下命令生成适当的转义值以供在配置文件中使用：</span><span class="sxs-lookup"><span data-stu-id="ffb23-179">Use the following command to generate a properly escaped value for use in the configuration file:</span></span>
>
> ```console
> systemd-escape "<value-to-escape>"
> ```

<span data-ttu-id="ffb23-180">保存该文件并启用该服务：</span><span class="sxs-lookup"><span data-stu-id="ffb23-180">Save the file and enable the service:</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="ffb23-181">启动该服务，并确认它正在运行：</span><span class="sxs-lookup"><span data-stu-id="ffb23-181">Start the service and verify that it's running:</span></span>

```bash
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API App running on CentOS 7
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

<span data-ttu-id="ffb23-182">在配置了反向代理并通过 systemd 管理 Kestrel 后，Web 应用现已完全配置，并能在本地计算机上的浏览器中从 `http://localhost` 进行访问。</span><span class="sxs-lookup"><span data-stu-id="ffb23-182">With the reverse proxy configured and Kestrel managed through *systemd*, the web app is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="ffb23-183">检查响应标头，服务器标头表示 ASP.NET Core 应用由 Kestrel 提供服务：</span><span class="sxs-lookup"><span data-stu-id="ffb23-183">Inspecting the response headers, the **Server** header indicates that the ASP.NET Core app is served by Kestrel:</span></span>

```
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="ffb23-184">查看日志</span><span class="sxs-lookup"><span data-stu-id="ffb23-184">Viewing logs</span></span>

<span data-ttu-id="ffb23-185">由于使用 Kestrel 的 Web 应用是通过 systemd 进行管理的，因此事件和进程将记录到集中日志。</span><span class="sxs-lookup"><span data-stu-id="ffb23-185">Since the web app using Kestrel is managed using *systemd*, events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="ffb23-186">但是，此日志包含由 systemd 管理的所有服务和进程的条目。</span><span class="sxs-lookup"><span data-stu-id="ffb23-186">However, this journal includes entries for all of the services and processes managed by *systemd*.</span></span> <span data-ttu-id="ffb23-187">若要查看特定于 `kestrel-hellomvc.service` 的项，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="ffb23-187">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="ffb23-188">若要进行时间筛选，请使用命令指定时间选项。</span><span class="sxs-lookup"><span data-stu-id="ffb23-188">For time filtering, specify time options with the command.</span></span> <span data-ttu-id="ffb23-189">例如，使用 `--since today` 筛选出当天或 `--until 1 hour ago` 来查看前一小时的条目。</span><span class="sxs-lookup"><span data-stu-id="ffb23-189">For example, use `--since today` to filter for the current day or `--until 1 hour ago` to see the previous hour's entries.</span></span> <span data-ttu-id="ffb23-190">有关详细信息，请参阅 [journalctl 手册页](https://www.unix.com/man-page/centos/1/journalctl/)。</span><span class="sxs-lookup"><span data-stu-id="ffb23-190">For more information, see the [man page for journalctl](https://www.unix.com/man-page/centos/1/journalctl/).</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-the-app"></a><span data-ttu-id="ffb23-191">保护应用</span><span class="sxs-lookup"><span data-stu-id="ffb23-191">Securing the app</span></span>

### <a name="configure-firewall"></a><span data-ttu-id="ffb23-192">配置防火墙</span><span class="sxs-lookup"><span data-stu-id="ffb23-192">Configure firewall</span></span>

<span data-ttu-id="ffb23-193">*Firewalld* 是管理防火墙的动态守护程序，支持网络区域。</span><span class="sxs-lookup"><span data-stu-id="ffb23-193">*Firewalld* is a dynamic daemon to manage the firewall with support for network zones.</span></span> <span data-ttu-id="ffb23-194">仍可以使用 iptable 管理端口和数据包筛选。</span><span class="sxs-lookup"><span data-stu-id="ffb23-194">Ports and packet filtering can still be managed by iptables.</span></span> <span data-ttu-id="ffb23-195">默认情况下应安装 *Firewalld*。</span><span class="sxs-lookup"><span data-stu-id="ffb23-195">*Firewalld* should be installed by default.</span></span> <span data-ttu-id="ffb23-196">`yum` 可用于安装包或验证是否已安装。</span><span class="sxs-lookup"><span data-stu-id="ffb23-196">`yum` can be used to install the package or verify it's installed.</span></span>

```bash
sudo yum install firewalld -y
```

<span data-ttu-id="ffb23-197">使用 `firewalld` 仅打开应用所需的端口。</span><span class="sxs-lookup"><span data-stu-id="ffb23-197">Use `firewalld` to open only the ports needed for the app.</span></span> <span data-ttu-id="ffb23-198">在此示例中，使用的是端口 80 和 443。</span><span class="sxs-lookup"><span data-stu-id="ffb23-198">In this case, port 80 and 443 are used.</span></span> <span data-ttu-id="ffb23-199">以下命令将端口 80 和 443 永久设置为打开：</span><span class="sxs-lookup"><span data-stu-id="ffb23-199">The following commands permanently set ports 80 and 443 to open:</span></span>

```bash
sudo firewall-cmd --add-port=80/tcp --permanent
sudo firewall-cmd --add-port=443/tcp --permanent
```

<span data-ttu-id="ffb23-200">重新加载防火墙设置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-200">Reload the firewall settings.</span></span> <span data-ttu-id="ffb23-201">检查默认区域中可用的服务和端口。</span><span class="sxs-lookup"><span data-stu-id="ffb23-201">Check the available services and ports in the default zone.</span></span> <span data-ttu-id="ffb23-202">通过检查 `firewall-cmd -h` 获取可用选项。</span><span class="sxs-lookup"><span data-stu-id="ffb23-202">Options are available by inspecting `firewall-cmd -h`.</span></span>

```bash
sudo firewall-cmd --reload
sudo firewall-cmd --list-all
```

```bash
public (default, active)
interfaces: eth0
sources: 
services: dhcpv6-client
ports: 443/tcp 80/tcp
masquerade: no
forward-ports: 
icmp-blocks: 
rich rules: 
```

### <a name="ssl-configuration"></a><span data-ttu-id="ffb23-203">SSL 配置</span><span class="sxs-lookup"><span data-stu-id="ffb23-203">SSL configuration</span></span>

<span data-ttu-id="ffb23-204">若要配置 Apache 用于 SSL，需使用 mod_ssl 模块。</span><span class="sxs-lookup"><span data-stu-id="ffb23-204">To configure Apache for SSL, the *mod_ssl* module is used.</span></span> <span data-ttu-id="ffb23-205">安装了 httpd 模块时，也会安装了 mod_ssl 模块。</span><span class="sxs-lookup"><span data-stu-id="ffb23-205">When the *httpd* module was installed, the *mod_ssl* module was also installed.</span></span> <span data-ttu-id="ffb23-206">如果未安装，请使用 `yum` 将其添加到配置。</span><span class="sxs-lookup"><span data-stu-id="ffb23-206">If it wasn't installed, use `yum` to add it to the configuration.</span></span>

```bash
sudo yum install mod_ssl
```

<span data-ttu-id="ffb23-207">若要强制使用 SSL，请安装 `mod_rewrite` 模块以启用 URL 重写：</span><span class="sxs-lookup"><span data-stu-id="ffb23-207">To enforce SSL, install the `mod_rewrite` module to enable URL rewriting:</span></span>

```bash
sudo yum install mod_rewrite
```

<span data-ttu-id="ffb23-208">修改 hellomvc.conf 文件以启用 URL 重写和端口 443 上的安全通信：</span><span class="sxs-lookup"><span data-stu-id="ffb23-208">Modify the *hellomvc.conf* file to enable URL rewriting and secure communication on port 443:</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5000/
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

> [!NOTE]
> <span data-ttu-id="ffb23-209">此示例中使用了本地生成的证书。</span><span class="sxs-lookup"><span data-stu-id="ffb23-209">This example is using a locally-generated certificate.</span></span> <span data-ttu-id="ffb23-210">SSLCertificateFile 应为域名的主证书文件。</span><span class="sxs-lookup"><span data-stu-id="ffb23-210">**SSLCertificateFile** should be the primary certificate file for the domain name.</span></span> <span data-ttu-id="ffb23-211">SSLCertificateKeyFile 应为创建 CSR 时生成的密钥文件。</span><span class="sxs-lookup"><span data-stu-id="ffb23-211">**SSLCertificateKeyFile** should be the key file generated when CSR is created.</span></span> <span data-ttu-id="ffb23-212">SSLCertificateChainFile 应为证书颁发机构提供的中间证书文件（如有）。</span><span class="sxs-lookup"><span data-stu-id="ffb23-212">**SSLCertificateChainFile** should be the intermediate certificate file (if any) that was supplied by the certificate authority.</span></span>

<span data-ttu-id="ffb23-213">保存文件，并测试配置：</span><span class="sxs-lookup"><span data-stu-id="ffb23-213">Save the file and test the configuration:</span></span>

```bash
sudo service httpd configtest
```

<span data-ttu-id="ffb23-214">重新启动 Apache：</span><span class="sxs-lookup"><span data-stu-id="ffb23-214">Restart Apache:</span></span>

```bash
sudo systemctl restart httpd
```

## <a name="additional-apache-suggestions"></a><span data-ttu-id="ffb23-215">其他 Apache 建议</span><span class="sxs-lookup"><span data-stu-id="ffb23-215">Additional Apache suggestions</span></span>

### <a name="additional-headers"></a><span data-ttu-id="ffb23-216">其他标头</span><span class="sxs-lookup"><span data-stu-id="ffb23-216">Additional headers</span></span>

<span data-ttu-id="ffb23-217">为了防止恶意攻击，应对一些标头进行修改或添加一些标头。</span><span class="sxs-lookup"><span data-stu-id="ffb23-217">In order to secure against malicious attacks, there are a few headers that should either be modified or added.</span></span> <span data-ttu-id="ffb23-218">确保已安装 `mod_headers` 模块：</span><span class="sxs-lookup"><span data-stu-id="ffb23-218">Ensure that the `mod_headers` module is installed:</span></span>

```bash
sudo yum install mod_headers
```

#### <a name="secure-apache-from-clickjacking-attacks"></a><span data-ttu-id="ffb23-219">保护 Apache 免受点击劫持攻击</span><span class="sxs-lookup"><span data-stu-id="ffb23-219">Secure Apache from clickjacking attacks</span></span>

<span data-ttu-id="ffb23-220">[点击劫持](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger)（也称为 *UI 伪装攻击*）是一种恶意攻击，其中网站访问者会上当受骗，从而导致在与当前要访问的页面不同的页面上单击链接或按钮。</span><span class="sxs-lookup"><span data-stu-id="ffb23-220">[Clickjacking](https://blog.qualys.com/securitylabs/2015/10/20/clickjacking-a-common-implementation-mistake-that-can-put-your-websites-in-danger), also known as a *UI redress attack*, is a malicious attack where a website visitor is tricked into clicking a link or button on a different page than they're currently visiting.</span></span> <span data-ttu-id="ffb23-221">使用 `X-FRAME-OPTIONS` 可保护网站。</span><span class="sxs-lookup"><span data-stu-id="ffb23-221">Use `X-FRAME-OPTIONS` to secure the site.</span></span>

<span data-ttu-id="ffb23-222">编辑 *httpd.conf* 文件：</span><span class="sxs-lookup"><span data-stu-id="ffb23-222">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="ffb23-223">添加行 `Header append X-FRAME-OPTIONS "SAMEORIGIN"`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-223">Add the line `Header append X-FRAME-OPTIONS "SAMEORIGIN"`.</span></span> <span data-ttu-id="ffb23-224">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="ffb23-224">Save the file.</span></span> <span data-ttu-id="ffb23-225">重启 Apache。</span><span class="sxs-lookup"><span data-stu-id="ffb23-225">Restart Apache.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="ffb23-226">MIME 类型探查</span><span class="sxs-lookup"><span data-stu-id="ffb23-226">MIME-type sniffing</span></span>

<span data-ttu-id="ffb23-227">`X-Content-Type-Options` 标头阻止 Internet Explorer 进行 *MIME 探查*（从文件内容中确定文件的 `Content-Type`）。</span><span class="sxs-lookup"><span data-stu-id="ffb23-227">The `X-Content-Type-Options` header prevents Internet Explorer from *MIME-sniffing* (determining a file's `Content-Type` from the file's content).</span></span> <span data-ttu-id="ffb23-228">如果服务器通过设置 `nosniff` 选项将 `Content-Type` 标头设置为 `text/html`，则不管文件内容为何，Internet Explorer 都会将内容呈现为 `text/html`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-228">If the server sets the `Content-Type` header to `text/html` with the `nosniff` option set, Internet Explorer renders the content as `text/html` regardless of the file's content.</span></span>

<span data-ttu-id="ffb23-229">编辑 *httpd.conf* 文件：</span><span class="sxs-lookup"><span data-stu-id="ffb23-229">Edit the *httpd.conf* file:</span></span>

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

<span data-ttu-id="ffb23-230">添加行 `Header set X-Content-Type-Options "nosniff"`。</span><span class="sxs-lookup"><span data-stu-id="ffb23-230">Add the line `Header set X-Content-Type-Options "nosniff"`.</span></span> <span data-ttu-id="ffb23-231">保存该文件。</span><span class="sxs-lookup"><span data-stu-id="ffb23-231">Save the file.</span></span> <span data-ttu-id="ffb23-232">重启 Apache。</span><span class="sxs-lookup"><span data-stu-id="ffb23-232">Restart Apache.</span></span>

### <a name="load-balancing"></a><span data-ttu-id="ffb23-233">负载平衡</span><span class="sxs-lookup"><span data-stu-id="ffb23-233">Load Balancing</span></span>

<span data-ttu-id="ffb23-234">此示例演示如何在同一实例计算机上的 CentOS 7 和 Kestrel 上设置和配置 Apache。</span><span class="sxs-lookup"><span data-stu-id="ffb23-234">This example shows how to setup and configure Apache on CentOS 7 and Kestrel on the same instance machine.</span></span> <span data-ttu-id="ffb23-235">为了不出现单一故障点；使用 mod_proxy_balancer 并修改 VirtualHost 可实现在 Apache 代理服务器后方管理 Web 应用的多个实例。</span><span class="sxs-lookup"><span data-stu-id="ffb23-235">In order to not have a single point of failure; using *mod_proxy_balancer* and modifying the **VirtualHost** would allow for managing multiple instances of the web apps behind the Apache proxy server.</span></span>

```bash
sudo yum install mod_proxy_balancer
```

<span data-ttu-id="ffb23-236">在下面所示的配置文件中，`hellomvc` 应用的其他实例设置为在端口 5001 上运行。</span><span class="sxs-lookup"><span data-stu-id="ffb23-236">In the configuration file shown below, an additional instance of the `hellomvc` app is setup to run on port 5001.</span></span> <span data-ttu-id="ffb23-237">“代理”部分设置了具有两个成员的均衡器配置，以便对 byrequests 进行负载均衡。</span><span class="sxs-lookup"><span data-stu-id="ffb23-237">The *Proxy* section is set with a balancer configuration with two members to load balance *byrequests*.</span></span>

```
<VirtualHost *:*>
    RequestHeader set "X-Forwarded-Proto" expr=%{REQUEST_SCHEME}
</VirtualHost>

<VirtualHost *:80>
    RewriteEngine On
    RewriteCond %{HTTPS} !=on
    RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R,L]
</VirtualHost>

<VirtualHost *:443>
    ProxyPass / balancer://mycluster/ 

    ProxyPassReverse / http://127.0.0.1:5000/
    ProxyPassReverse / http://127.0.0.1:5001/

    <Proxy balancer://mycluster>
        BalancerMember http://127.0.0.1:5000
        BalancerMember http://127.0.0.1:5001 
        ProxySet lbmethod=byrequests
    </Proxy>

    <Location />
        SetHandler balancer
    </Location>
    ErrorLog /var/log/httpd/hellomvc-error.log
    CustomLog /var/log/httpd/hellomvc-access.log common
    SSLEngine on
    SSLProtocol all -SSLv2
    SSLCipherSuite ALL:!ADH:!EXPORT:!SSLv2:!RC4+RSA:+HIGH:+MEDIUM:!LOW:!RC4
    SSLCertificateFile /etc/pki/tls/certs/localhost.crt
    SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
</VirtualHost>
```

### <a name="rate-limits"></a><span data-ttu-id="ffb23-238">速率限制</span><span class="sxs-lookup"><span data-stu-id="ffb23-238">Rate Limits</span></span>

<span data-ttu-id="ffb23-239">使用 httpd 模块中包含的 mod_ratelimit，客户端的带宽可以限制为：</span><span class="sxs-lookup"><span data-stu-id="ffb23-239">Using *mod_ratelimit*, which is included in the *httpd* module, the bandwidth of clients can be limited:</span></span>

```bash
sudo nano /etc/httpd/conf.d/ratelimit.conf
```
<span data-ttu-id="ffb23-240">示例文件将根位置下的带宽限制为 600 KB/秒：</span><span class="sxs-lookup"><span data-stu-id="ffb23-240">The example file limits bandwidth as 600 KB/sec under the root location:</span></span>

```
<IfModule mod_ratelimit.c>
    <Location />
        SetOutputFilter RATE_LIMIT
        SetEnv rate-limit 600
    </Location>
</IfModule>
```

## <a name="additional-resources"></a><span data-ttu-id="ffb23-241">其他资源</span><span class="sxs-lookup"><span data-stu-id="ffb23-241">Additional resources</span></span>

* [<span data-ttu-id="ffb23-242">配置 ASP.NET Core 以使用代理服务器和负载均衡器</span><span class="sxs-lookup"><span data-stu-id="ffb23-242">Configure ASP.NET Core to work with proxy servers and load balancers</span></span>](xref:host-and-deploy/proxy-load-balancer)
