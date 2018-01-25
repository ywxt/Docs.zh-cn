---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: "选择 Web 部署到适当的方法 |Microsoft 文档"
author: jrjlee
description: "当使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b77aa37160f3822f58908866e44497aea3d3bdc8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="choosing-the-right-approach-to-web-deployment"></a><span data-ttu-id="447f9-103">选择 Web 部署到适当的方法</span><span class="sxs-lookup"><span data-stu-id="447f9-103">Choosing the Right Approach to Web Deployment</span></span>
====================
<span data-ttu-id="447f9-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="447f9-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="447f9-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="447f9-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="447f9-106">当使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取打包的 web 应用程序到 web 服务器上。</span><span class="sxs-lookup"><span data-stu-id="447f9-106">When you work with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your packaged web applications onto a web server.</span></span> <span data-ttu-id="447f9-107">你可以：</span><span class="sxs-lookup"><span data-stu-id="447f9-107">You can either:</span></span>
> 
> - <span data-ttu-id="447f9-108">通过以目标部署应用程序从远程位置*Web 部署代理服务*（也称为"远程代理"） 目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="447f9-108">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the "remote agent") on the destination server.</span></span>
> - <span data-ttu-id="447f9-109">部署应用程序从远程位置使用 Web 部署按需 （也称为"临时代理"）。</span><span class="sxs-lookup"><span data-stu-id="447f9-109">Deploy the application from a remote location using Web Deploy On Demand (also known as the "temp agent").</span></span>
> - <span data-ttu-id="447f9-110">通过以目标部署应用程序从远程位置*IIS Web 部署处理程序*目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="447f9-110">Deploy the application from a remote location by targeting the *IIS Web Deploy Handler* on the destination server.</span></span>
> - <span data-ttu-id="447f9-111">手动复制到目标服务器的 web 包并导入通过 IIS 管理器中部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="447f9-111">Deploy the application by manually copying the web package to the destination server and importing it through IIS Manager.</span></span>
> 
> <span data-ttu-id="447f9-112">如何配置你的目标 web 服务器将取决于你想要使用哪种部署的方法。</span><span class="sxs-lookup"><span data-stu-id="447f9-112">How you configure your destination web servers will depend on which approach to deployment you want to use.</span></span> <span data-ttu-id="447f9-113">本主题将帮助您决定哪种部署的方法最适合你。</span><span class="sxs-lookup"><span data-stu-id="447f9-113">This topic will help you decide which approach to deployment is right for you.</span></span>


<span data-ttu-id="447f9-114">下表显示的主要优点和缺点的每个部署方法，以及通常最适合每种方法的方案。</span><span class="sxs-lookup"><span data-stu-id="447f9-114">This table shows the main advantages and disadvantages of each deployment approach, together with the scenarios that most typically suit each approach.</span></span>

| <span data-ttu-id="447f9-115">方法</span><span class="sxs-lookup"><span data-stu-id="447f9-115">Approach</span></span> | <span data-ttu-id="447f9-116">优点</span><span class="sxs-lookup"><span data-stu-id="447f9-116">Advantages</span></span> | <span data-ttu-id="447f9-117">缺点</span><span class="sxs-lookup"><span data-stu-id="447f9-117">Disadvantages</span></span> | <span data-ttu-id="447f9-118">典型的方案</span><span class="sxs-lookup"><span data-stu-id="447f9-118">Typical Scenarios</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="447f9-119">远程代理</span><span class="sxs-lookup"><span data-stu-id="447f9-119">Remote Agent</span></span> | <span data-ttu-id="447f9-120">很容易设置。</span><span class="sxs-lookup"><span data-stu-id="447f9-120">It is easy to set up.</span></span> <span data-ttu-id="447f9-121">它是适用于 web 应用程序和内容的定期更新。</span><span class="sxs-lookup"><span data-stu-id="447f9-121">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="447f9-122">用户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="447f9-122">The user must be an administrator on the target server.</span></span> <span data-ttu-id="447f9-123">用户不能提供备用凭据。</span><span class="sxs-lookup"><span data-stu-id="447f9-123">the user can't supply alternative credentials.</span></span> | <span data-ttu-id="447f9-124">开发环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-124">Development environments.</span></span> <span data-ttu-id="447f9-125">测试环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-125">Test environments.</span></span> |
| <span data-ttu-id="447f9-126">临时代理</span><span class="sxs-lookup"><span data-stu-id="447f9-126">Temp Agent</span></span> | <span data-ttu-id="447f9-127">没有无需在目标计算机上安装 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="447f9-127">There is no need to install Web Deploy on the target computer.</span></span> <span data-ttu-id="447f9-128">Web 部署的最新版本会自动使用。</span><span class="sxs-lookup"><span data-stu-id="447f9-128">The latest version of Web Deploy is automatically used.</span></span> | <span data-ttu-id="447f9-129">用户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="447f9-129">The user must be an administrator on the target server.</span></span> <span data-ttu-id="447f9-130">用户不能提供备用凭据。</span><span class="sxs-lookup"><span data-stu-id="447f9-130">The user can't supply alternative credentials.</span></span> | <span data-ttu-id="447f9-131">开发环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-131">Development environments.</span></span> <span data-ttu-id="447f9-132">测试环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-132">Test environments.</span></span> |
| <span data-ttu-id="447f9-133">Web 部署处理程序</span><span class="sxs-lookup"><span data-stu-id="447f9-133">Web Deploy Handler</span></span> | <span data-ttu-id="447f9-134">非管理员用户可以将内容部署。</span><span class="sxs-lookup"><span data-stu-id="447f9-134">Non-administrator users can deploy content.</span></span> <span data-ttu-id="447f9-135">它是适用于 web 应用程序和内容的定期更新。</span><span class="sxs-lookup"><span data-stu-id="447f9-135">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="447f9-136">它是更加复杂，无法设置。</span><span class="sxs-lookup"><span data-stu-id="447f9-136">It is a lot more complex to set up.</span></span> | <span data-ttu-id="447f9-137">过渡环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-137">Staging environments.</span></span> <span data-ttu-id="447f9-138">Intranet 生产环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-138">Intranet production environments.</span></span> <span data-ttu-id="447f9-139">托管的环境中。</span><span class="sxs-lookup"><span data-stu-id="447f9-139">Hosted environments.</span></span> |
| <span data-ttu-id="447f9-140">脱机部署</span><span class="sxs-lookup"><span data-stu-id="447f9-140">Offline Deployment</span></span> | <span data-ttu-id="447f9-141">它是很容易设置。</span><span class="sxs-lookup"><span data-stu-id="447f9-141">It is very easy to set up.</span></span> <span data-ttu-id="447f9-142">它是适用于独立的环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-142">It is suitable for isolated environments.</span></span> | <span data-ttu-id="447f9-143">服务器管理员必须手动复制并导入的 web 包每次。</span><span class="sxs-lookup"><span data-stu-id="447f9-143">The server administrator must manually copy and import the web package every time.</span></span> | <span data-ttu-id="447f9-144">面向 Internet 的生产环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-144">Internet-facing production environments.</span></span> <span data-ttu-id="447f9-145">隔离的网络环境中。</span><span class="sxs-lookup"><span data-stu-id="447f9-145">Isolated network environments.</span></span> |
  

## <a name="using-the-remote-agent"></a><span data-ttu-id="447f9-146">使用远程代理</span><span class="sxs-lookup"><span data-stu-id="447f9-146">Using the Remote Agent</span></span>

<span data-ttu-id="447f9-147">在安装 Web 部署使用默认设置在目标服务器上时，Web 部署代理服务 （"远程代理"） 将自动安装和启动。</span><span class="sxs-lookup"><span data-stu-id="447f9-147">When you install Web Deploy using the default settings on a destination server, the Web Deployment Agent Service (the "remote agent") is automatically installed and started.</span></span> <span data-ttu-id="447f9-148">默认情况下，远程代理公开在此地址的 HTTP 终结点：</span><span class="sxs-lookup"><span data-stu-id="447f9-148">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> <span data-ttu-id="447f9-149">你可以替换 [*服务器*] 与 web 服务器的计算机名称，你的 web 服务器或主机名的 IP 地址解析为你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="447f9-149">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="447f9-150">服务器管理员可以通过指定此终结点地址来部署 web 包从远程位置，如开发人员计算机或生成服务器。</span><span class="sxs-lookup"><span data-stu-id="447f9-150">Server administrators can deploy web packages from a remote location, like a developer machine or a build server, by specifying this endpoint address.</span></span> <span data-ttu-id="447f9-151">例如，假设在 Fabrikam，Inc.的 Matt 婷已在其开发人员计算机上生成 ContactManager.Mvc web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="447f9-151">For example, suppose Matt Hink at Fabrikam, Inc. has built the ContactManager.Mvc web application project on his developer machine.</span></span> <span data-ttu-id="447f9-152">生成过程生成了 web 包，连同*。 deploy.cmd*安装包所需的文件，其中包含 Web 部署命令。</span><span class="sxs-lookup"><span data-stu-id="447f9-152">The build process generates a web package, together with a *.deploy.cmd* file that contains the Web Deploy commands required to install the package.</span></span> <span data-ttu-id="447f9-153">如果 Matt TESTWEB1 服务器上的服务器管理员，他可以通过在其开发人员计算机上运行此命令来部署 web 应用程序与测试 web 服务器：</span><span class="sxs-lookup"><span data-stu-id="447f9-153">If Matt is a server administrator on the TESTWEB1 server, he can deploy the web application to the test web server by running this command on his developer machine:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


<span data-ttu-id="447f9-154">在实际事实中，Web 部署的可执行文件可以推导出的终结点地址的远程代理，如果你提供计算机名称，因此 Matt 只需键入：</span><span class="sxs-lookup"><span data-stu-id="447f9-154">In actual fact, the Web Deploy executable can infer the endpoint address of the remote agent if you provide the machine name, so Matt only needs to type this:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="447f9-155">有关 Web 部署命令行语法的详细信息和*。 deploy.cmd*文件，请参阅[如何： 安装部署包 Using deploy.cmd 文件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-155">For more information on Web Deploy command-line syntax and *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="447f9-156">远程代理提供了一个简单的方法，将从远程位置的内容部署，这种方法可以很好地配合一键式或自动部署。</span><span class="sxs-lookup"><span data-stu-id="447f9-156">The remote agent offers a straightforward way to deploy content from a remote location, and this approach can work well with one-click or automated deployment.</span></span> <span data-ttu-id="447f9-157">但是，运行的部署命令的用户还必须是域管理员或目标服务器上的本地管理员组的成员。</span><span class="sxs-lookup"><span data-stu-id="447f9-157">However, the user who runs the deployment command must also be either a domain administrator or a member of the local administrators group on the destination server.</span></span> <span data-ttu-id="447f9-158">此外，远程代理不支持基本身份验证，所以不能传递命令行上的备用凭据。</span><span class="sxs-lookup"><span data-stu-id="447f9-158">In addition, the remote agent doesn't support basic authentication, so you can't pass alternative credentials on the command line.</span></span>

<span data-ttu-id="447f9-159">远程代理会提供到开发或测试方案，其中它并不常见的开发人员能够完全权限管理员控制测试服务器环境中，并且通常重新生成并重新非常部署的应用程序的部署很有用的方法频繁。</span><span class="sxs-lookup"><span data-stu-id="447f9-159">The remote agent provides a useful approach to deployment in development or test scenarios, where it's not uncommon for developers to have full administrator control over a test server environment, and applications are typically rebuilt and redeployed very frequently.</span></span> <span data-ttu-id="447f9-160">但是，这种方法是通常不太适用于过渡环境或生产环境。</span><span class="sxs-lookup"><span data-stu-id="447f9-160">However, this approach is usually less acceptable for staging or production environments.</span></span>

<span data-ttu-id="447f9-161">有关使用远程代理方法的方案的端到端示例，请参阅[方案： 配置 Web 部署的测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="447f9-161">For an end-to-end example of a scenario that uses the remote agent approach, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span>

## <a name="using-the-temp-agent"></a><span data-ttu-id="447f9-162">使用临时代理</span><span class="sxs-lookup"><span data-stu-id="447f9-162">Using the Temp Agent</span></span>

<span data-ttu-id="447f9-163">部署的临时代理方法是类似于远程代理方法。</span><span class="sxs-lookup"><span data-stu-id="447f9-163">The temp agent approach to deployment is similar to the remote agent approach.</span></span> <span data-ttu-id="447f9-164">但是，与远程代理方法中，你不需要在目标 web 服务器上安装 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="447f9-164">However, in contrast to the remote agent approach, you don't need to install Web Deploy on the destination web server.</span></span> <span data-ttu-id="447f9-165">相反，当执行部署时，Web 部署将在目标服务器上安装 web 部署代理服务的临时版本和将使用它来将你的内容部署到 IIS。</span><span class="sxs-lookup"><span data-stu-id="447f9-165">Instead, when you perform the deployment, Web Deploy will install a temporary version of the web deployment agent service on the destination server and will use this to deploy your content to IIS.</span></span> <span data-ttu-id="447f9-166">部署完成后，删除所有临时文件。</span><span class="sxs-lookup"><span data-stu-id="447f9-166">When the deployment is complete, all temporary files are removed.</span></span>

<span data-ttu-id="447f9-167">如果你想要使用临时代理提供程序设置中，添加**/g**标志设为你部署的命令：</span><span class="sxs-lookup"><span data-stu-id="447f9-167">If you want to use the temp agent provider setting, add the **/g** flag to your deployment command:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="447f9-168">即使服务未运行，不能如果在目标计算机上安装 web 部署代理服务使用临时代理。</span><span class="sxs-lookup"><span data-stu-id="447f9-168">You can't use the temp agent if the web deployment agent service is installed on the destination computer, even if the service is not running.</span></span>


<span data-ttu-id="447f9-169">此方法的优点是，你不需要维护的 Web 部署目标服务器上的安装。</span><span class="sxs-lookup"><span data-stu-id="447f9-169">The advantage of this approach is that you don't need to maintain installations of Web Deploy on your destination servers.</span></span> <span data-ttu-id="447f9-170">此外，你不需要确保源和目标计算机都运行相同版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="447f9-170">Furthermore, you don't need to ensure that the source and destination computers are running the same version of Web Deploy.</span></span> <span data-ttu-id="447f9-171">但是，此方法会受到与远程代理方法时，相同的主体限制即，你必须在目标服务器上的本地管理员才能部署内容，并且支持仅 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="447f9-171">However, this approach suffers from the same principal limitations as the remote agent approach, namely that you must be a local administrator on the destination server in order to deploy content, and only NTLM authentication is supported.</span></span> <span data-ttu-id="447f9-172">临时代理方法还要求目标环境的大量的初始的配置。</span><span class="sxs-lookup"><span data-stu-id="447f9-172">The temp agent approach also requires a lot more initial configuration of the destination environment.</span></span>

<span data-ttu-id="447f9-173">使用临时代理的详细信息，请参阅[如何： 安装部署包 Using deploy.cmd 文件](https://msdn.microsoft.com/library/ff356104.aspx)和[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-173">For more information on using the temp agent, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx) and [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

## <a name="using-the-web-deploy-handler"></a><span data-ttu-id="447f9-174">使用 Web 部署处理程序</span><span class="sxs-lookup"><span data-stu-id="447f9-174">Using the Web Deploy Handler</span></span>

<span data-ttu-id="447f9-175">对于 IIS 7 及以上版本，Web 部署提供通过 IIS Web 部署处理程序的另一种部署方法。</span><span class="sxs-lookup"><span data-stu-id="447f9-175">For IIS 7 onwards, Web Deploy offers an alternative deployment approach through the IIS Web Deploy Handler.</span></span> <span data-ttu-id="447f9-176">与 IIS Web 管理服务 (WMSvc)，它旨在允许用户从远程位置管理 IIS 网站紧密地集成 Web 部署处理程序。</span><span class="sxs-lookup"><span data-stu-id="447f9-176">The Web Deploy Handler is closely integrated with the IIS Web Management Service (WMSvc), which is designed to allow users to manage IIS websites from remote locations.</span></span>

<span data-ttu-id="447f9-177">默认情况下，远程代理公开在此地址的 HTTP 终结点：</span><span class="sxs-lookup"><span data-stu-id="447f9-177">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> <span data-ttu-id="447f9-178">你可以替换 [*服务器*] 与 web 服务器的计算机名称，你的 web 服务器或主机名的 IP 地址解析为你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="447f9-178">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="447f9-179">Web 部署处理程序通过远程代理、 和临时代理，其最大优点是，你可以配置 IIS 以允许非管理员用户部署到特定的 IIS 网站的应用程序和内容。</span><span class="sxs-lookup"><span data-stu-id="447f9-179">The big advantage of the Web Deploy Handler over the remote agent, and the temp agent, is that you can configure IIS to allow non-administrator users to deploy applications and content to specific IIS websites.</span></span> <span data-ttu-id="447f9-180">Web 部署处理程序还支持基本身份验证，因此你也可以在 Web 部署命令作为参数提供备用凭据。</span><span class="sxs-lookup"><span data-stu-id="447f9-180">The Web Deploy Handler also supports basic authentication, so you can provide alternative credentials as parameters in your Web Deploy commands.</span></span> <span data-ttu-id="447f9-181">主要缺点是，Web 部署处理程序并最初设置和配置大量更复杂。</span><span class="sxs-lookup"><span data-stu-id="447f9-181">The major drawback is that the Web Deploy Handler is initially a lot more complicated to set up and configure.</span></span>

<span data-ttu-id="447f9-182">对于非管理员用户，Web 管理服务 (WMSvc) 将仅允许用户连接到 IIS 使用的站点级连接，而不是服务器级连接。</span><span class="sxs-lookup"><span data-stu-id="447f9-182">In the case of non-administrator users, the Web Management Service (WMSvc) will only allow the user to connect to IIS using a site-level connection, rather than a server-level connection.</span></span> <span data-ttu-id="447f9-183">若要访问特定站点，您可以在终结点地址包括特定于站点的查询字符串：</span><span class="sxs-lookup"><span data-stu-id="447f9-183">To access a particular site, you can include a site-specific query string in the endpoint address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


<span data-ttu-id="447f9-184">例如，假设生成过程配置为自动部署到过渡环境的 web 应用程序每次成功生成之后。</span><span class="sxs-lookup"><span data-stu-id="447f9-184">For example, suppose a build process is configured to automatically deploy a web application to a staging environment after every successful build.</span></span> <span data-ttu-id="447f9-185">如果使用远程代理方法时，你将需要在目标服务器上进行生成进程标识管理员。</span><span class="sxs-lookup"><span data-stu-id="447f9-185">If you used the remote agent approach, you'd need to make the build process identity an administrator on your destination servers.</span></span> <span data-ttu-id="447f9-186">与此相反，使用 Web 部署处理程序方法你可以为提供的非管理员用户 （&） #x 2014;**FABRIKAM\stagingdeployer**在此用例和 #x 2014; 对仅，一个特定的 IIS 网站和生成过程的权限可以提供这些凭据以部署 web 包。</span><span class="sxs-lookup"><span data-stu-id="447f9-186">In contrast, using the Web Deploy Handler approach you can give a non-administrator user&#x2014;**FABRIKAM\stagingdeployer** in this case&#x2014;permission to a specific IIS website only, and the build process can provide these credentials to deploy the web package.</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> <span data-ttu-id="447f9-187">有关 Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-187">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="447f9-188">有关详细信息使用*。 deploy.cmd*文件，请参阅[如何： 安装部署包 Using deploy.cmd 文件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-188">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="447f9-189">Web 部署处理程序提供到过渡环境、 托管的环境中，和基于 intranet 的生产环境中，远程访问服务器可用但不是管理员凭据的部署很有用的方法。</span><span class="sxs-lookup"><span data-stu-id="447f9-189">The Web Deploy Handler provides a useful approach to deployment in staging environments, hosted environments, and intranet-based production environments, where remote access to the server is available but administrator credentials are not.</span></span>

<span data-ttu-id="447f9-190">有关使用 Web 部署处理程序方法的方案的端到端示例，请参阅[方案： 配置 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="447f9-190">For an end-to-end example of a scenario that uses the Web Deploy Handler approach, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

## <a name="using-offline-deployment"></a><span data-ttu-id="447f9-191">使用脱机部署</span><span class="sxs-lookup"><span data-stu-id="447f9-191">Using Offline Deployment</span></span>

<span data-ttu-id="447f9-192">在某些情况下，不可能或可行从远程位置将应用程序和内容部署到 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="447f9-192">In some cases, it's not possible or practical to deploy applications and content to an IIS website from a remote location.</span></span> <span data-ttu-id="447f9-193">例如，在源和目标计算机可能在隔离的网络或网络段，或者防火墙策略可能不允许远程访问。</span><span class="sxs-lookup"><span data-stu-id="447f9-193">For example, the source and destination computers may be in isolated networks or network segments, or firewall policy may not permit remote access.</span></span>

<span data-ttu-id="447f9-194">在类似这样的情况下，你可以仍使用打包和发布功能的 Web 部署;你只需不能使用它们从远程位置。</span><span class="sxs-lookup"><span data-stu-id="447f9-194">In scenarios like these, you can still use the packaging and publishing capabilities of Web Deploy; you just can't use them from a remote location.</span></span> <span data-ttu-id="447f9-195">相反，目标服务器上的管理员必须复制到服务器上的 web 包，并将其导入通过 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="447f9-195">Instead, an administrator on the destination server must copy the web package onto the server and import it through IIS Manager.</span></span>

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

<span data-ttu-id="447f9-196">脱机的部署方法通常是很有用在面向 Internet 的生产环境中，其中外围网络中的服务器可能与内部网络中的计算机的连接受到限制。</span><span class="sxs-lookup"><span data-stu-id="447f9-196">The offline deployment approach is typically useful in Internet-facing production environments, where servers in a perimeter network may have restricted connectivity with computers in the internal network.</span></span>

<span data-ttu-id="447f9-197">有关使用脱机的部署方法的方案的端到端示例，请参阅[方案： 配置 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="447f9-197">For an end-to-end example of a scenario that uses the offline deployment approach, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

## <a name="further-reading"></a><span data-ttu-id="447f9-198">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="447f9-198">Further Reading</span></span>

<span data-ttu-id="447f9-199">有关 Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-199">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="447f9-200">有关详细信息使用*。 deploy.cmd*文件，请参阅[如何： 安装部署包 Using deploy.cmd 文件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-200">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>

<span data-ttu-id="447f9-201">你可以在其中部署 web 包从远程计算机的不同方法的更多常规指南，请参阅[使用 Web 部署远程](https://technet.microsoft.com/library/ee461175(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-201">For more general guidance on the different ways in which you can deploy web packages from a remote computer, see [Using Web Deploy Remotely](https://technet.microsoft.com/library/ee461175(WS.10).aspx).</span></span> <span data-ttu-id="447f9-202">有关使用 Web 按需部署的详细信息，请参阅[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="447f9-202">For more information on using Web Deploy On Demand, see [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="447f9-203">[上一页](configuring-server-environments-for-web-deployment.md)
[下一页](scenario-configuring-a-test-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="447f9-203">[Previous](configuring-server-environments-for-web-deployment.md)
[Next](scenario-configuring-a-test-environment-for-web-deployment.md)</span></span>
