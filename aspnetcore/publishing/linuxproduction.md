---
title: "使用 Nginx 在 Linux 上托管 ASP.NET Core"
description: "介绍如何在 Ubuntu 16.04 上将 Nginx 设置为反向代理，从而将 HTTP 流量转发到在 Kestrel 上运行的 ASP.NET Core Web 应用程序。"
keywords: "ASP.NET Core, Linux, nginx, Ubuntu, 反向代理"
author: rick-anderson
ms.author: riande
manager: wpickett
ms.date: 08/21/2017
ms.topic: article
ms.assetid: 1c33e576-33de-481a-8ad3-896b94fde0e3
ms.technology: aspnet
ms.prod: asp.net-core
uid: publishing/linuxproduction
ms.openlocfilehash: 7c7b949fc922c605aa4554c158200a4123c4eb1c
ms.sourcegitcommit: fc98e93464ccf37d9904e89a71cdddbd4bbdb86a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="set-up-a-hosting-environment-for-aspnet-core-on-linux-with-nginx-and-deploy-to-it"></a><span data-ttu-id="bb0c0-104">使用 Nginx 在 Linux 上为 ASP.NET Core 设置托管环境，并对其进行部署</span><span class="sxs-lookup"><span data-stu-id="bb0c0-104">Set up a hosting environment for ASP.NET Core on Linux with Nginx, and deploy to it</span></span>

<span data-ttu-id="bb0c0-105">作者：[Sourabh Shirhatti](https://twitter.com/sshirhatti)</span><span class="sxs-lookup"><span data-stu-id="bb0c0-105">By [Sourabh Shirhatti](https://twitter.com/sshirhatti)</span></span>

<span data-ttu-id="bb0c0-106">本指南介绍如何在 Ubuntu 16.04 服务器上设置生产就绪 ASP.NET Core 环境。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-106">This guide explains setting up a production-ready ASP.NET Core environment on an Ubuntu 16.04 Server.</span></span>

<span data-ttu-id="bb0c0-107">注意：对于 Ubuntu 14.04，建议进行监控，以此作为监视 Kestrel 进程的解决方案。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-107">**Note:** For Ubuntu 14.04, supervisord is recommended as a solution for monitoring the Kestrel process.</span></span> <span data-ttu-id="bb0c0-108">在 Ubuntu 14.04 上不提供 systemd。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-108">systemd is not available on Ubuntu 14.04.</span></span> [<span data-ttu-id="bb0c0-109">请参阅本文档的早期版本</span><span class="sxs-lookup"><span data-stu-id="bb0c0-109">See previous version of this document</span></span>](https://github.com/aspnet/Docs/blob/e9c1419175c4dd7e152df3746ba1df5935aaafd5/aspnetcore/publishing/linuxproduction.md)

<span data-ttu-id="bb0c0-110">本指南：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-110">This guide:</span></span>

* <span data-ttu-id="bb0c0-111">将现有 ASP.NET Core 应用程序置于反向代理服务器后面</span><span class="sxs-lookup"><span data-stu-id="bb0c0-111">Places an existing ASP.NET Core application behind a reverse proxy server</span></span>
* <span data-ttu-id="bb0c0-112">设置反向代理服务器，以便将请求转发到 Kestrel Web 服务器</span><span class="sxs-lookup"><span data-stu-id="bb0c0-112">Sets up the reverse proxy server to forward requests to the Kestrel web server</span></span>
* <span data-ttu-id="bb0c0-113">确保 Web 应用程序在启动时作为守护程序运行</span><span class="sxs-lookup"><span data-stu-id="bb0c0-113">Ensures the web application runs on startup as a daemon</span></span>
* <span data-ttu-id="bb0c0-114">配置进程管理工具以帮助重新启动 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="bb0c0-114">Configures a process management tool to help restart the web application</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb0c0-115">系统必备</span><span class="sxs-lookup"><span data-stu-id="bb0c0-115">Prerequisites</span></span>

1. <span data-ttu-id="bb0c0-116">使用具有 sudo 特权的标准用户帐户访问 Ubuntu 16.04 服务器</span><span class="sxs-lookup"><span data-stu-id="bb0c0-116">Access to an Ubuntu 16.04 Server with a standard user account with sudo privilege</span></span>
2. <span data-ttu-id="bb0c0-117">现有 ASP.NET Core 应用程序</span><span class="sxs-lookup"><span data-stu-id="bb0c0-117">An existing ASP.NET Core application</span></span>

## <a name="copy-over-your-app"></a><span data-ttu-id="bb0c0-118">复制应用</span><span class="sxs-lookup"><span data-stu-id="bb0c0-118">Copy over your app</span></span>

<span data-ttu-id="bb0c0-119">从开发环境中运行`dotnet publish` 以将应用打包到可在服务器上运行的独立目录。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-119">Run `dotnet publish` from the dev environment to package an app into a self-contained directory that can run on the server.</span></span>

<span data-ttu-id="bb0c0-120">使用集成到你的工作流的任何工具（SCP 和 FTP 等）将 ASP.NET Core 应用复制到服务器。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-120">Copy the ASP.NET Core app to the server using whatever tool (SCP, FTP, etc.) integrates into your workflow.</span></span> <span data-ttu-id="bb0c0-121">测试应用，例如：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-121">Test the app, for example:</span></span>
 - <span data-ttu-id="bb0c0-122">从命令行中，运行 `dotnet yourapp.dll`</span><span class="sxs-lookup"><span data-stu-id="bb0c0-122">From the command line, run `dotnet yourapp.dll`</span></span>
 - <span data-ttu-id="bb0c0-123">在浏览器中，导航到 `http://<serveraddress>:<port>` 以确认应用在 Linux 上正常运行。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-123">In a browser, navigate to `http://<serveraddress>:<port>` to verify the app works on Linux.</span></span> 
 
## <a name="configure-a-reverse-proxy-server"></a><span data-ttu-id="bb0c0-124">配置反向代理服务器</span><span class="sxs-lookup"><span data-stu-id="bb0c0-124">Configure a reverse proxy server</span></span>

<span data-ttu-id="bb0c0-125">反向代理是为动态 Web 应用程序提供服务的常见设置。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-125">A reverse proxy is a common setup for serving dynamic web applications.</span></span> <span data-ttu-id="bb0c0-126">反向代理终止 HTTP 请求，并将其转发到 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-126">A reverse proxy terminates the HTTP request and forwards it to the ASP.NET Core application.</span></span>

### <a name="why-use-a-reverse-proxy-server"></a><span data-ttu-id="bb0c0-127">为何使用反向代理服务器？</span><span class="sxs-lookup"><span data-stu-id="bb0c0-127">Why use a reverse proxy server?</span></span>

<span data-ttu-id="bb0c0-128">Kestrel 非常适合从 ASP.NET Core 提供动态内容，但是，Web 服务部件的功能不像 IIS、Apache 或 Nginx 等服务器那样强大。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-128">Kestrel is great for serving dynamic content from ASP.NET Core; however, the web serving parts aren’t as feature rich as servers like IIS, Apache, or Nginx.</span></span> <span data-ttu-id="bb0c0-129">反向代理服务器可以从 HTTP 服务器卸载服务静态内容、缓存请求、压缩请求和 SSL 终端等工作。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-129">A reverse proxy server can offload work like serving static content, caching requests, compressing requests, and SSL termination from the HTTP server.</span></span> <span data-ttu-id="bb0c0-130">反向代理服务器可能驻留在专用计算机上，也可能与 HTTP 服务器一起部署。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-130">A reverse proxy server may reside on a dedicated machine or may be deployed alongside an HTTP server.</span></span>

<span data-ttu-id="bb0c0-131">鉴于此指南的目的，使用 Nginx 的单个实例。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-131">For the purposes of this guide, a single instance of Nginx is used.</span></span> <span data-ttu-id="bb0c0-132">它与 HTTP 服务器一起运行在同一服务器上。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-132">It runs on the same server, alongside the HTTP server.</span></span> <span data-ttu-id="bb0c0-133">根据你的要求，可以选择不同的设置。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-133">Based on your requirements, you may choose a different setup.</span></span>

<span data-ttu-id="bb0c0-134">由于请求通过反向代理转发，因此使用 `Microsoft.AspNetCore.HttpOverrides` 包中的 `ForwardedHeaders` 中间件。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-134">Because requests are forwarded by reverse proxy, use the `ForwardedHeaders` middleware from the `Microsoft.AspNetCore.HttpOverrides` package.</span></span> <span data-ttu-id="bb0c0-135">此中间件使用 `X-Forwarded-Proto` 标头来更新 `Request.Scheme`，使重定向 URI 和其他安全策略能够正常工作。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-135">This middleware updates `Request.Scheme`, using the `X-Forwarded-Proto` header, so that redirect URIs and other security policies work correctly.</span></span>

<span data-ttu-id="bb0c0-136">设置反向代理服务器时，身份验证中间件需要首先运行 `UseForwardedHeaders`。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-136">When setting up a reverse proxy server, the authentication middleware needs `UseForwardedHeaders` to run first.</span></span> <span data-ttu-id="bb0c0-137">此顺序可确保身份验证中间件可以使用受影响的值，并生成正确的重定向 URI。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-137">This ordering ensures that the authentication middleware can consume the affected values and generate correct redirect URIs.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="bb0c0-138">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="bb0c0-138">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="bb0c0-139">在调用 `UseAuthentication` 或类似的身份验证方案中间件之前，调用 `UseForwardedHeaders` 方法（在 *Startup.cs* 的 `Configure` 方法中）：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-139">Invoke the `UseForwardedHeaders` method (in the `Configure` method of *Startup.cs*) before calling `UseAuthentication` or similar authentication scheme middleware:</span></span>

```csharp
app.UseForwardedHeaders(new ForwardedHeadersOptions
{
    ForwardedHeaders = ForwardedHeaders.XForwardedFor | ForwardedHeaders.XForwardedProto
});

app.UseAuthentication();
```

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="bb0c0-140">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="bb0c0-140">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="bb0c0-141">在调用 `UseIdentity`、`UseFacebookAuthentication` 或类似的身份验证方案中间件之前，调用 `UseForwardedHeaders` 方法（在 *Startup.cs* 的 `Configure` 方法中）：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-141">Invoke the `UseForwardedHeaders` method (in the `Configure` method of *Startup.cs*) before calling `UseIdentity` and `UseFacebookAuthentication` or similar authentication scheme middleware:</span></span>

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

### <a name="install-nginx"></a><span data-ttu-id="bb0c0-142">安装 Nginx</span><span class="sxs-lookup"><span data-stu-id="bb0c0-142">Install Nginx</span></span>

```bash
sudo apt-get install nginx
```

> [!NOTE]
> <span data-ttu-id="bb0c0-143">如果计划安装可选 Nginx 模块，可能需要从源生成 Nginx。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-143">If you plan to install optional Nginx modules, you may be required to build Nginx from source.</span></span>

<span data-ttu-id="bb0c0-144">使用 `apt-get` 安装 Nginx。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-144">Use `apt-get` to install Nginx.</span></span> <span data-ttu-id="bb0c0-145">安装程序创建一个 System V init 脚本，该脚本运行 Nginx 作为系统启动时的守护程序。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-145">The installer creates a System V init script that runs Nginx as daemon on system startup.</span></span> <span data-ttu-id="bb0c0-146">因为是首次安装 Nginx，通过运行以下命令显式启动：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-146">Since Nginx was installed for the first time, explicitly start it by running:</span></span>

```bash
sudo service nginx start
```

<span data-ttu-id="bb0c0-147">确认浏览器显示 Nginx 的默认登陆页。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-147">Verify a browser displays the default landing page for Nginx.</span></span>

### <a name="configure-nginx"></a><span data-ttu-id="bb0c0-148">配置 Nginx</span><span class="sxs-lookup"><span data-stu-id="bb0c0-148">Configure Nginx</span></span>

<span data-ttu-id="bb0c0-149">若要将 Nginx 配置为反向代理以将请求转发到 ASP.NET Core 应用程序，请修改 `/etc/nginx/sites-available/default`。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-149">To configure Nginx as a reverse proxy to forward requests to our ASP.NET Core application, modify `/etc/nginx/sites-available/default`.</span></span> <span data-ttu-id="bb0c0-150">在文本编辑器中打开它，并将内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-150">Open it in a text editor, and replace the contents with the following:</span></span>

```nginx
server {
    listen 80;
    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection keep-alive;
        proxy_set_header Host $http_host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

<span data-ttu-id="bb0c0-151">此 Nginx 配置文件将传入的公共流量从端口 `80` 转发到端口 `5000`。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-151">This Nginx configuration file forwards incoming public traffic from port `80` to port `5000`.</span></span>

<span data-ttu-id="bb0c0-152">完成对 Nginx 配置的修改后，可运行 `sudo nginx -t` 以验证配置文件的语法。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-152">Once you have completed making changes to your Nginx configuration, you can run `sudo nginx -t` to verify the syntax of your configuration files.</span></span> <span data-ttu-id="bb0c0-153">如果配置文件测试成功，可以通过运行 `sudo nginx -s reload` 让 Nginx 选取更改。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-153">If the configuration file test is successful, you can ask Nginx to pick up the changes by running `sudo nginx -s reload`.</span></span>

## <a name="monitoring-our-application"></a><span data-ttu-id="bb0c0-154">监视应用程序</span><span class="sxs-lookup"><span data-stu-id="bb0c0-154">Monitoring our application</span></span>

<span data-ttu-id="bb0c0-155">Nginx 现在已设置为将对 `http://yourhost:80` 发起的请求转发到运行在 `http://127.0.0.1:5000` 中的 Kestrel 上的 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-155">Nginx is now setup to forward requests made to `http://yourhost:80` on to the ASP.NET Core application running on Kestrel at `http://127.0.0.1:5000`.</span></span> <span data-ttu-id="bb0c0-156">但是，未将 Nginx 设置为管理 Kestrel 进程。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-156">However, Nginx is not set up to manage the Kestrel process.</span></span> <span data-ttu-id="bb0c0-157">可以使用 systemd 并创建服务文件以启动和监视基础 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-157">You can use *systemd* and create a service file to start and monitor the underlying web app.</span></span> <span data-ttu-id="bb0c0-158">systemd 是一个 init 系统，可以提供用于启动、停止和管理进程的许多强大的功能。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-158">*systemd* is an init system that provides many powerful features for starting, stopping, and managing processes.</span></span> 

### <a name="create-the-service-file"></a><span data-ttu-id="bb0c0-159">创建服务文件</span><span class="sxs-lookup"><span data-stu-id="bb0c0-159">Create the service file</span></span>

<span data-ttu-id="bb0c0-160">创建服务定义文件：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-160">Create the service definition file:</span></span>

```bash
sudo nano /etc/systemd/system/kestrel-hellomvc.service
```

<span data-ttu-id="bb0c0-161">以下是我们的应用程序的一个示例服务文件：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-161">The following is an example service file for our application:</span></span>

```ini
[Unit]
Description=Example .NET Web API Application running on Ubuntu

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

<span data-ttu-id="bb0c0-162">请注意：如果配置未使用用户 www-data，则必须先创建此处定义的用户，并为该用户提供适当的文件所有权。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-162">**Note:** If the user *www-data* is not used by your configuration, the user defined here must be created first and given proper ownership for files.</span></span>

<span data-ttu-id="bb0c0-163">保存该文件，并启用该服务。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-163">Save the file, and enable the service.</span></span>

```bash
systemctl enable kestrel-hellomvc.service
```

<span data-ttu-id="bb0c0-164">启用该服务，并确认它正在运行。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-164">Start the service and verify that it is running.</span></span>

```
systemctl start kestrel-hellomvc.service
systemctl status kestrel-hellomvc.service

● kestrel-hellomvc.service - Example .NET Web API Application running on Ubuntu
    Loaded: loaded (/etc/systemd/system/kestrel-hellomvc.service; enabled)
    Active: active (running) since Thu 2016-10-18 04:09:35 NZDT; 35s ago
Main PID: 9021 (dotnet)
    CGroup: /system.slice/kestrel-hellomvc.service
            └─9021 /usr/local/bin/dotnet /var/aspnetcore/hellomvc/hellomvc.dll
```

<span data-ttu-id="bb0c0-165">配置反向代理并通过 systemd 管理 Kestrel 后，Web 应用程序即已完全配置并能从 `http://localhost` 中的本地计算机上的浏览器访问。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-165">With the reverse proxy configured and Kestrel managed through systemd, the web application is fully configured and can be accessed from a browser on the local machine at `http://localhost`.</span></span> <span data-ttu-id="bb0c0-166">也可以从远程计算机进行访问，同时限制可能进行阻止的任何防火墙。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-166">It is also accessible from a remote machine, barring any firewall that might be blocking.</span></span> <span data-ttu-id="bb0c0-167">检查响应标头，`Server` 标头显示由 Kestrel 所提供的 ASP.NET Core 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-167">Inspecting the response headers, the `Server` header shows the ASP.NET Core application being served by Kestrel.</span></span>

```text
HTTP/1.1 200 OK
Date: Tue, 11 Oct 2016 16:22:23 GMT
Server: Kestrel
Keep-Alive: timeout=5, max=98
Connection: Keep-Alive
Transfer-Encoding: chunked
```

### <a name="viewing-logs"></a><span data-ttu-id="bb0c0-168">查看日志</span><span class="sxs-lookup"><span data-stu-id="bb0c0-168">Viewing logs</span></span>

<span data-ttu-id="bb0c0-169">使用 Kestrel 的 Web 应用程序是通过 `systemd` 进行管理的，因此所有事件和进程都被记录到集中日志。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-169">Since the web application using Kestrel is managed using `systemd`, all events and processes are logged to a centralized journal.</span></span> <span data-ttu-id="bb0c0-170">但是，此日志包含由 `systemd` 管理的所有服务和进程的全部条目。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-170">However, this journal includes all entries for all services and processes managed by `systemd`.</span></span> <span data-ttu-id="bb0c0-171">若要查看特定于 `kestrel-hellomvc.service` 的项，请使用以下命令：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-171">To view the `kestrel-hellomvc.service`-specific items, use the following command:</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service
```

<span data-ttu-id="bb0c0-172">有关进一步筛选，时间选项（如 `--since today`、`--until 1 hour ago` 或这些选项的组合）可以减少返回的条目数。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-172">For further filtering, time options such as `--since today`, `--until 1 hour ago` or a combination of these can reduce the amount of entries returned.</span></span>

```bash
sudo journalctl -fu kestrel-hellomvc.service --since "2016-10-18" --until "2016-10-18 04:00"
```

## <a name="securing-our-application"></a><span data-ttu-id="bb0c0-173">保护应用程序</span><span class="sxs-lookup"><span data-stu-id="bb0c0-173">Securing our application</span></span>

### <a name="enable-apparmor"></a><span data-ttu-id="bb0c0-174">启用 AppArmor</span><span class="sxs-lookup"><span data-stu-id="bb0c0-174">Enable AppArmor</span></span>

<span data-ttu-id="bb0c0-175">Linux 安全模块 (LSM) 是一个框架，它是自 Linux 2.6 后的 Linux kernel 的一部分。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-175">Linux Security Modules (LSM) is a framework that is part of the Linux kernel since Linux 2.6.</span></span> <span data-ttu-id="bb0c0-176">LSM 支持安全模块的不同实现。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-176">LSM supports different implementations of security modules.</span></span> <span data-ttu-id="bb0c0-177">[AppArmor](https://wiki.ubuntu.com/AppArmor) 是实现强制访问控制系统的 LSM，它允许将程序限制在一组有限的资源内。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-177">[AppArmor](https://wiki.ubuntu.com/AppArmor) is a LSM that implements a Mandatory Access Control system which allows confining the program to a limited set of resources.</span></span> <span data-ttu-id="bb0c0-178">确保已启用并成功配置 AppArmor。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-178">Ensure AppArmor is enabled and properly configured.</span></span>

### <a name="configuring-our-firewall"></a><span data-ttu-id="bb0c0-179">配置防火墙</span><span class="sxs-lookup"><span data-stu-id="bb0c0-179">Configuring our firewall</span></span>

<span data-ttu-id="bb0c0-180">关闭所有未使用的外部端口。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-180">Close off all external ports that are not in use.</span></span> <span data-ttu-id="bb0c0-181">通过为配置防火墙提供命令行接口，不复杂的防火墙 (ufw) 为 `iptables` 提供了前端。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-181">Uncomplicated firewall (ufw) provides a front end for `iptables` by providing a command line interface for configuring the firewall.</span></span> <span data-ttu-id="bb0c0-182">确认已配置 `ufw` 以允许所需的任何端口上的流量。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-182">Verify that `ufw` is configured to allow traffic on any ports you need.</span></span>

```bash
sudo apt-get install ufw
sudo ufw enable

sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

### <a name="securing-nginx"></a><span data-ttu-id="bb0c0-183">保护 Nginx</span><span class="sxs-lookup"><span data-stu-id="bb0c0-183">Securing Nginx</span></span>

<span data-ttu-id="bb0c0-184">Nginx 的默认分配不启用 SSL。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-184">The default distribution of Nginx doesn't enable SSL.</span></span> <span data-ttu-id="bb0c0-185">若要启用其他安全功能，请从源生成。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-185">To enable additional security features, build from source.</span></span>

#### <a name="download-the-source-and-install-the-build-dependencies"></a><span data-ttu-id="bb0c0-186">下载源并安装生成依赖项</span><span class="sxs-lookup"><span data-stu-id="bb0c0-186">Download the source and install the build dependencies</span></span>

```bash
# Install the build dependencies
sudo apt-get update
sudo apt-get install build-essential zlib1g-dev libpcre3-dev libssl-dev libxslt1-dev libxml2-dev libgd2-xpm-dev libgeoip-dev libgoogle-perftools-dev libperl-dev

# Download nginx 1.10.0 or latest
wget http://www.nginx.org/download/nginx-1.10.0.tar.gz
tar zxf nginx-1.10.0.tar.gz
```

#### <a name="change-the-nginx-response-name"></a><span data-ttu-id="bb0c0-187">更改 Nginx 响应名称</span><span class="sxs-lookup"><span data-stu-id="bb0c0-187">Change the Nginx response name</span></span>

<span data-ttu-id="bb0c0-188">编辑 src/http/ngx_http_header_filter_module.c：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-188">Edit *src/http/ngx_http_header_filter_module.c*:</span></span>

```c
static char ngx_http_server_string[] = "Server: Your Web Server" CRLF;
static char ngx_http_server_full_string[] = "Server: Your Web Server" CRLF;
```

#### <a name="configure-the-options-and-build"></a><span data-ttu-id="bb0c0-189">配置选项和生成</span><span class="sxs-lookup"><span data-stu-id="bb0c0-189">Configure the options and build</span></span>

<span data-ttu-id="bb0c0-190">正则表达式需要 PCRE 库。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-190">The PCRE library is required for regular expressions.</span></span> <span data-ttu-id="bb0c0-191">正则表达式用于 ngx_http_rewrite_module 的位置指令。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-191">Regular expressions are used in the location directive for the ngx_http_rewrite_module.</span></span> <span data-ttu-id="bb0c0-192">http_ssl_module adds HTTPS 协议支持。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-192">The http_ssl_module adds HTTPS protocol support.</span></span>

<span data-ttu-id="bb0c0-193">请考虑使用诸如“ModSecurity”的 Web 应用程序防火墙来加强对应用程序的保护。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-193">Consider using a web application firewall like *ModSecurity* to harden your application.</span></span>

```bash
./configure
--with-pcre=../pcre-8.38
--with-zlib=../zlib-1.2.8
--with-http_ssl_module
--with-stream
--with-mail=dynamic
```

#### <a name="configure-ssl"></a><span data-ttu-id="bb0c0-194">配置 SSL</span><span class="sxs-lookup"><span data-stu-id="bb0c0-194">Configure SSL</span></span>

* <span data-ttu-id="bb0c0-195">通过指定由受信任的证书颁发机构 (CA) 颁发的有效证书来配置服务器，以侦听端口 `443` 上的 HTTPS 流量。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-195">Configure your server to listen to HTTPS traffic on port `443` by specifying a valid certificate issued by a trusted Certificate Authority (CA).</span></span>

* <span data-ttu-id="bb0c0-196">通过采用以下“/etc/nginx/nginx.conf”文件中所示的某些做法来增强安全保护。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-196">Harden your security by employing some of the practices depicted in the following */etc/nginx/nginx.conf* file.</span></span> <span data-ttu-id="bb0c0-197">示例包括选择更强的密码并将通过 HTTP 的所有流量重定向到 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-197">Examples include choosing a stronger cipher and redirecting all traffic over HTTP to HTTPS.</span></span>

* <span data-ttu-id="bb0c0-198">添加 `HTTP Strict-Transport-Security` (HSTS) 标头可确保由客户端发起的所有后续请求都仅通过 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-198">Adding an `HTTP Strict-Transport-Security` (HSTS) header ensures all subsequent requests made by the client are over HTTPS only.</span></span>

* <span data-ttu-id="bb0c0-199">如果计划以后禁用 SSL，则不要添加 Strict-Transport-Security 标头或选择相应的 `max-age`。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-199">Do not add the Strict-Transport-Security header or chose an appropriate `max-age` if you plan to disable SSL in the future.</span></span>

<span data-ttu-id="bb0c0-200">添加 /etc/nginx/proxy.conf 配置文件：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-200">Add the */etc/nginx/proxy.conf* configuration file:</span></span>

[!code-nginx[Main](linuxproduction/proxy.conf)]

<span data-ttu-id="bb0c0-201">编辑 /etc/nginx/nginx.conf 配置文件。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-201">Edit the */etc/nginx/nginx.conf* configuration file.</span></span> <span data-ttu-id="bb0c0-202">示例包含一个配置文件中的 `http` 和 `server` 部分。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-202">The example contains both `http` and `server` sections in one configuration file.</span></span>

[!code-nginx[Main](../publishing/linuxproduction/nginx.conf?highlight=2)]

#### <a name="secure-nginx-from-clickjacking"></a><span data-ttu-id="bb0c0-203">保护 Nginx 免受点击劫持的侵害</span><span class="sxs-lookup"><span data-stu-id="bb0c0-203">Secure Nginx from clickjacking</span></span>
<span data-ttu-id="bb0c0-204">点击劫持是收集受感染用户的点击数的恶意技术。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-204">Clickjacking is a malicious technique to collect an infected user's clicks.</span></span> <span data-ttu-id="bb0c0-205">点击劫持诱使受害者（访问者）点击受感染的网站。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-205">Clickjacking tricks the victim (visitor) into clicking on an infected site.</span></span> <span data-ttu-id="bb0c0-206">使用 X-FRAME-OPTIONS 保护你的网站。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-206">Use X-FRAME-OPTIONS to secure your site.</span></span>

<span data-ttu-id="bb0c0-207">编辑 nginx.conf 文件：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-207">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="bb0c0-208">添加行 `add_header X-Frame-Options "SAMEORIGIN";` 并保存文件，然后重新启动 Nginx。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-208">Add the line `add_header X-Frame-Options "SAMEORIGIN";` and save the file, then restart Nginx.</span></span>

#### <a name="mime-type-sniffing"></a><span data-ttu-id="bb0c0-209">MIME 类型探查</span><span class="sxs-lookup"><span data-stu-id="bb0c0-209">MIME-type sniffing</span></span>

<span data-ttu-id="bb0c0-210">此标头可阻止大部分浏览器通过 MIME 方式探查来自已声明内容类型的响应，因为标头会指示浏览器不要替代响应内容类型。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-210">This header prevents most browsers from MIME-sniffing a response away from the declared content type, as the header instructs the browser not to override the response content type.</span></span> <span data-ttu-id="bb0c0-211">使用 `nosniff` 选项后，如果服务器认为内容是“文本/html”，则浏览器将其显示为“文本/html”。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-211">With the `nosniff` option, if the server says the content is "text/html", the browser renders it as "text/html".</span></span>

<span data-ttu-id="bb0c0-212">编辑 nginx.conf 文件：</span><span class="sxs-lookup"><span data-stu-id="bb0c0-212">Edit the *nginx.conf* file:</span></span>

```bash
sudo nano /etc/nginx/nginx.conf
```

<span data-ttu-id="bb0c0-213">添加行 `add_header X-Content-Type-Options "nosniff";` 并保存文件，然后重新启动 Nginx。</span><span class="sxs-lookup"><span data-stu-id="bb0c0-213">Add the line `add_header X-Content-Type-Options "nosniff";` and save the file, then restart Nginx.</span></span>
