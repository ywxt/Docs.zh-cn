---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: 选择 Web 部署的适当方法 |Microsoft Docs
author: jrjlee
description: 使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eb1b7d50e5d7461d760ad7a963cc70369b7a4513
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807046"
---
<a name="choosing-the-right-approach-to-web-deployment"></a><span data-ttu-id="94f29-103">选择 Web 部署的适当方法</span><span class="sxs-lookup"><span data-stu-id="94f29-103">Choosing the Right Approach to Web Deployment</span></span>
====================
<span data-ttu-id="94f29-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="94f29-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="94f29-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="94f29-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="94f29-106">使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 2.0 或更高版本时，有三种主要方法可用于获取已打包的 web 应用程序到 web 服务器上。</span><span class="sxs-lookup"><span data-stu-id="94f29-106">When you work with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your packaged web applications onto a web server.</span></span> <span data-ttu-id="94f29-107">您可以：</span><span class="sxs-lookup"><span data-stu-id="94f29-107">You can either:</span></span>
> 
> - <span data-ttu-id="94f29-108">将从远程位置应用程序部署通过面向*Web 部署代理服务*（也称为"远程代理"） 在目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="94f29-108">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the "remote agent") on the destination server.</span></span>
> - <span data-ttu-id="94f29-109">部署中使用 Web 部署按需 （也称为"临时代理"） 的远程位置的应用程序。</span><span class="sxs-lookup"><span data-stu-id="94f29-109">Deploy the application from a remote location using Web Deploy On Demand (also known as the "temp agent").</span></span>
> - <span data-ttu-id="94f29-110">将从远程位置应用程序部署通过面向*IIS Web 部署处理程序*目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="94f29-110">Deploy the application from a remote location by targeting the *IIS Web Deploy Handler* on the destination server.</span></span>
> - <span data-ttu-id="94f29-111">将应用程序部署手动将 web 包复制到目标服务器并将其导通过 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="94f29-111">Deploy the application by manually copying the web package to the destination server and importing it through IIS Manager.</span></span>
> 
> <span data-ttu-id="94f29-112">配置目标 web 服务器的方式取决于你想要使用哪种部署的方法。</span><span class="sxs-lookup"><span data-stu-id="94f29-112">How you configure your destination web servers will depend on which approach to deployment you want to use.</span></span> <span data-ttu-id="94f29-113">本主题将帮助您决定哪种部署的方法是最适合你。</span><span class="sxs-lookup"><span data-stu-id="94f29-113">This topic will help you decide which approach to deployment is right for you.</span></span>


<span data-ttu-id="94f29-114">此表显示的主要优点和缺点的每个部署方法，以及通常最适合每种方法的方案。</span><span class="sxs-lookup"><span data-stu-id="94f29-114">This table shows the main advantages and disadvantages of each deployment approach, together with the scenarios that most typically suit each approach.</span></span>

| <span data-ttu-id="94f29-115">方法</span><span class="sxs-lookup"><span data-stu-id="94f29-115">Approach</span></span> | <span data-ttu-id="94f29-116">优点</span><span class="sxs-lookup"><span data-stu-id="94f29-116">Advantages</span></span> | <span data-ttu-id="94f29-117">缺点</span><span class="sxs-lookup"><span data-stu-id="94f29-117">Disadvantages</span></span> | <span data-ttu-id="94f29-118">典型的方案</span><span class="sxs-lookup"><span data-stu-id="94f29-118">Typical Scenarios</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="94f29-119">远程代理</span><span class="sxs-lookup"><span data-stu-id="94f29-119">Remote Agent</span></span> | <span data-ttu-id="94f29-120">它很容易设置。</span><span class="sxs-lookup"><span data-stu-id="94f29-120">It is easy to set up.</span></span> <span data-ttu-id="94f29-121">它是适用于 web 应用程序和内容的常规更新。</span><span class="sxs-lookup"><span data-stu-id="94f29-121">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="94f29-122">用户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="94f29-122">The user must be an administrator on the target server.</span></span> <span data-ttu-id="94f29-123">用户不能提供备用凭据。</span><span class="sxs-lookup"><span data-stu-id="94f29-123">the user can't supply alternative credentials.</span></span> | <span data-ttu-id="94f29-124">开发环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-124">Development environments.</span></span> <span data-ttu-id="94f29-125">测试环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-125">Test environments.</span></span> |
| <span data-ttu-id="94f29-126">临时代理</span><span class="sxs-lookup"><span data-stu-id="94f29-126">Temp Agent</span></span> | <span data-ttu-id="94f29-127">没有必要在目标计算机上安装 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="94f29-127">There is no need to install Web Deploy on the target computer.</span></span> <span data-ttu-id="94f29-128">自动使用最新版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="94f29-128">The latest version of Web Deploy is automatically used.</span></span> | <span data-ttu-id="94f29-129">用户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="94f29-129">The user must be an administrator on the target server.</span></span> <span data-ttu-id="94f29-130">用户不能提供备用凭据。</span><span class="sxs-lookup"><span data-stu-id="94f29-130">The user can't supply alternative credentials.</span></span> | <span data-ttu-id="94f29-131">开发环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-131">Development environments.</span></span> <span data-ttu-id="94f29-132">测试环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-132">Test environments.</span></span> |
| <span data-ttu-id="94f29-133">Web 部署处理程序</span><span class="sxs-lookup"><span data-stu-id="94f29-133">Web Deploy Handler</span></span> | <span data-ttu-id="94f29-134">非管理员用户可以将内容部署。</span><span class="sxs-lookup"><span data-stu-id="94f29-134">Non-administrator users can deploy content.</span></span> <span data-ttu-id="94f29-135">它是适用于 web 应用程序和内容的常规更新。</span><span class="sxs-lookup"><span data-stu-id="94f29-135">It is suitable for regular updates to web applications and content.</span></span> | <span data-ttu-id="94f29-136">它是更复杂，无法设置。</span><span class="sxs-lookup"><span data-stu-id="94f29-136">It is a lot more complex to set up.</span></span> | <span data-ttu-id="94f29-137">过渡环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-137">Staging environments.</span></span> <span data-ttu-id="94f29-138">Intranet 生产环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-138">Intranet production environments.</span></span> <span data-ttu-id="94f29-139">托管的环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-139">Hosted environments.</span></span> |
| <span data-ttu-id="94f29-140">离线部署</span><span class="sxs-lookup"><span data-stu-id="94f29-140">Offline Deployment</span></span> | <span data-ttu-id="94f29-141">它是非常容易设置。</span><span class="sxs-lookup"><span data-stu-id="94f29-141">It is very easy to set up.</span></span> <span data-ttu-id="94f29-142">它是适用于隔离环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-142">It is suitable for isolated environments.</span></span> | <span data-ttu-id="94f29-143">服务器管理员必须手动复制并导入 web 包每次。</span><span class="sxs-lookup"><span data-stu-id="94f29-143">The server administrator must manually copy and import the web package every time.</span></span> | <span data-ttu-id="94f29-144">面向 Internet 的生产环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-144">Internet-facing production environments.</span></span> <span data-ttu-id="94f29-145">隔离的网络环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-145">Isolated network environments.</span></span> |
  

## <a name="using-the-remote-agent"></a><span data-ttu-id="94f29-146">使用远程代理</span><span class="sxs-lookup"><span data-stu-id="94f29-146">Using the Remote Agent</span></span>

<span data-ttu-id="94f29-147">在安装 Web 部署使用默认设置在目标服务器上时，Web 部署代理服务 （"远程代理"） 自动安装并启动。</span><span class="sxs-lookup"><span data-stu-id="94f29-147">When you install Web Deploy using the default settings on a destination server, the Web Deployment Agent Service (the "remote agent") is automatically installed and started.</span></span> <span data-ttu-id="94f29-148">默认情况下，远程代理公开 HTTP 终结点在此地址：</span><span class="sxs-lookup"><span data-stu-id="94f29-148">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]


> [!NOTE]
> <span data-ttu-id="94f29-149">您可以替换 [*server*] 与你的 web 服务器的计算机名称，你的 web 服务器或主机名的 IP 地址解析为你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="94f29-149">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="94f29-150">服务器管理员可以通过指定此终结点地址部署 web 包从开发人员的计算机或生成服务器等远程位置。</span><span class="sxs-lookup"><span data-stu-id="94f29-150">Server administrators can deploy web packages from a remote location, like a developer machine or a build server, by specifying this endpoint address.</span></span> <span data-ttu-id="94f29-151">例如，假设在 Fabrikam，Inc.Matt 婷已在自己的开发人员计算机上生成 ContactManager.Mvc web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="94f29-151">For example, suppose Matt Hink at Fabrikam, Inc. has built the ContactManager.Mvc web application project on his developer machine.</span></span> <span data-ttu-id="94f29-152">生成过程生成 web 包，连同 *。 deploy.cmd*安装包所需的文件，其中包含 Web 部署命令。</span><span class="sxs-lookup"><span data-stu-id="94f29-152">The build process generates a web package, together with a *.deploy.cmd* file that contains the Web Deploy commands required to install the package.</span></span> <span data-ttu-id="94f29-153">如果 Matt TESTWEB1 服务器上的服务器管理员，他可以通过他的开发人员计算机上运行以下命令部署到测试 web 服务器的 web 应用程序：</span><span class="sxs-lookup"><span data-stu-id="94f29-153">If Matt is a server administrator on the TESTWEB1 server, he can deploy the web application to the test web server by running this command on his developer machine:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]


<span data-ttu-id="94f29-154">在实际的这一事实，如果您提供计算机名称，因此 Matt 只需键入以下 Web 部署的可执行文件可以推断出远程代理的终结点地址：</span><span class="sxs-lookup"><span data-stu-id="94f29-154">In actual fact, the Web Deploy executable can infer the endpoint address of the remote agent if you provide the machine name, so Matt only needs to type this:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]


> [!NOTE]
> <span data-ttu-id="94f29-155">有关 Web 部署命令行语法的详细信息和 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-155">For more information on Web Deploy command-line syntax and *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="94f29-156">远程代理提供了简单方法以从远程位置，将内容部署，这种方法可以十分适用于一次单击或自动部署。</span><span class="sxs-lookup"><span data-stu-id="94f29-156">The remote agent offers a straightforward way to deploy content from a remote location, and this approach can work well with one-click or automated deployment.</span></span> <span data-ttu-id="94f29-157">但是，运行部署命令的用户还必须是域管理员或目标服务器上的本地管理员组的成员。</span><span class="sxs-lookup"><span data-stu-id="94f29-157">However, the user who runs the deployment command must also be either a domain administrator or a member of the local administrators group on the destination server.</span></span> <span data-ttu-id="94f29-158">此外，远程代理不支持基本身份验证，因此不能在命令行上传递其他凭据。</span><span class="sxs-lookup"><span data-stu-id="94f29-158">In addition, the remote agent doesn't support basic authentication, so you can't pass alternative credentials on the command line.</span></span>

<span data-ttu-id="94f29-159">远程代理提供了在开发或测试方案，其中这并不常见的开发人员可以完全权限管理员控制测试服务器环境中，并且通常重新生成并重新部署非常的应用程序中部署的有用方法频繁。</span><span class="sxs-lookup"><span data-stu-id="94f29-159">The remote agent provides a useful approach to deployment in development or test scenarios, where it's not uncommon for developers to have full administrator control over a test server environment, and applications are typically rebuilt and redeployed very frequently.</span></span> <span data-ttu-id="94f29-160">但是，这种方法是通常不到可接受过渡或生产环境。</span><span class="sxs-lookup"><span data-stu-id="94f29-160">However, this approach is usually less acceptable for staging or production environments.</span></span>

<span data-ttu-id="94f29-161">使用远程代理方法的方案的端到端示例，请参阅[方案： 配置用于 Web 部署测试环境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="94f29-161">For an end-to-end example of a scenario that uses the remote agent approach, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span>

## <a name="using-the-temp-agent"></a><span data-ttu-id="94f29-162">使用临时代理</span><span class="sxs-lookup"><span data-stu-id="94f29-162">Using the Temp Agent</span></span>

<span data-ttu-id="94f29-163">部署的临时代理方法是与远程代理方法类似。</span><span class="sxs-lookup"><span data-stu-id="94f29-163">The temp agent approach to deployment is similar to the remote agent approach.</span></span> <span data-ttu-id="94f29-164">但是，与远程代理方法中，不需要在目标 web 服务器上安装 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="94f29-164">However, in contrast to the remote agent approach, you don't need to install Web Deploy on the destination web server.</span></span> <span data-ttu-id="94f29-165">相反，当您执行部署时，Web 部署将在目标服务器上安装 web 部署代理服务的临时版本并将使用此若要将内容部署到 IIS。</span><span class="sxs-lookup"><span data-stu-id="94f29-165">Instead, when you perform the deployment, Web Deploy will install a temporary version of the web deployment agent service on the destination server and will use this to deploy your content to IIS.</span></span> <span data-ttu-id="94f29-166">部署完成后，删除所有临时文件。</span><span class="sxs-lookup"><span data-stu-id="94f29-166">When the deployment is complete, all temporary files are removed.</span></span>

<span data-ttu-id="94f29-167">如果你想要使用临时代理提供程序设置中，添加 **/g**你部署的命令的标志：</span><span class="sxs-lookup"><span data-stu-id="94f29-167">If you want to use the temp agent provider setting, add the **/g** flag to your deployment command:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]


> [!NOTE]
> <span data-ttu-id="94f29-168">不能使用临时代理如果目标计算机上安装 web 部署代理服务，则即使该服务未运行。</span><span class="sxs-lookup"><span data-stu-id="94f29-168">You can't use the temp agent if the web deployment agent service is installed on the destination computer, even if the service is not running.</span></span>


<span data-ttu-id="94f29-169">此方法的优点是，无需维护的 Web 部署在目标服务器上进行安装。</span><span class="sxs-lookup"><span data-stu-id="94f29-169">The advantage of this approach is that you don't need to maintain installations of Web Deploy on your destination servers.</span></span> <span data-ttu-id="94f29-170">此外，不需要确保源和目标计算机正在运行相同版本的 Web 部署。</span><span class="sxs-lookup"><span data-stu-id="94f29-170">Furthermore, you don't need to ensure that the source and destination computers are running the same version of Web Deploy.</span></span> <span data-ttu-id="94f29-171">但是，此方法面临相同的主体限制远程代理方法，即，你必须在目标服务器上的本地管理员才能部署内容，并且支持仅 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="94f29-171">However, this approach suffers from the same principal limitations as the remote agent approach, namely that you must be a local administrator on the destination server in order to deploy content, and only NTLM authentication is supported.</span></span> <span data-ttu-id="94f29-172">临时代理方法还要求在目标环境的更多初始配置。</span><span class="sxs-lookup"><span data-stu-id="94f29-172">The temp agent approach also requires a lot more initial configuration of the destination environment.</span></span>

<span data-ttu-id="94f29-173">使用临时代理的详细信息，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)并[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-173">For more information on using the temp agent, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx) and [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

## <a name="using-the-web-deploy-handler"></a><span data-ttu-id="94f29-174">使用 Web 部署处理程序</span><span class="sxs-lookup"><span data-stu-id="94f29-174">Using the Web Deploy Handler</span></span>

<span data-ttu-id="94f29-175">适用于 IIS 7 及更高版本，Web 部署提供了通过 IIS Web 部署处理程序采用其他部署方法。</span><span class="sxs-lookup"><span data-stu-id="94f29-175">For IIS 7 onwards, Web Deploy offers an alternative deployment approach through the IIS Web Deploy Handler.</span></span> <span data-ttu-id="94f29-176">与 IIS Web 管理服务 (WMSvc)，它旨在允许用户从远程位置管理 IIS 网站紧密地集成 Web 部署处理程序。</span><span class="sxs-lookup"><span data-stu-id="94f29-176">The Web Deploy Handler is closely integrated with the IIS Web Management Service (WMSvc), which is designed to allow users to manage IIS websites from remote locations.</span></span>

<span data-ttu-id="94f29-177">默认情况下，远程代理公开 HTTP 终结点在此地址：</span><span class="sxs-lookup"><span data-stu-id="94f29-177">By default, the remote agent exposes an HTTP endpoint at this address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]


> [!NOTE]
> <span data-ttu-id="94f29-178">您可以替换 [*server*] 与你的 web 服务器的计算机名称，你的 web 服务器或主机名的 IP 地址解析为你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="94f29-178">You can replace [*server*] with the machine name of your web server, an IP address for your web server, or a hostname that resolves to your web server.</span></span>


<span data-ttu-id="94f29-179">Web 部署处理程序通过远程代理和临时代理，其最大优点是，您可以配置 IIS 以允许非管理员用户将应用程序和内容部署到特定的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="94f29-179">The big advantage of the Web Deploy Handler over the remote agent, and the temp agent, is that you can configure IIS to allow non-administrator users to deploy applications and content to specific IIS websites.</span></span> <span data-ttu-id="94f29-180">Web 部署处理程序还支持基本身份验证，因此可在 Web 部署命令中作为参数提供备用凭据。</span><span class="sxs-lookup"><span data-stu-id="94f29-180">The Web Deploy Handler also supports basic authentication, so you can provide alternative credentials as parameters in your Web Deploy commands.</span></span> <span data-ttu-id="94f29-181">主要缺点是，Web 部署处理程序是最初要设置和配置更复杂。</span><span class="sxs-lookup"><span data-stu-id="94f29-181">The major drawback is that the Web Deploy Handler is initially a lot more complicated to set up and configure.</span></span>

<span data-ttu-id="94f29-182">对于非管理员用户，Web 管理服务 (WMSvc) 将仅允许用户连接到 IIS 使用站点级别的连接，而不是服务器级连接。</span><span class="sxs-lookup"><span data-stu-id="94f29-182">In the case of non-administrator users, the Web Management Service (WMSvc) will only allow the user to connect to IIS using a site-level connection, rather than a server-level connection.</span></span> <span data-ttu-id="94f29-183">若要访问特定站点，可以将特定于站点的查询字符串包含在终结点地址：</span><span class="sxs-lookup"><span data-stu-id="94f29-183">To access a particular site, you can include a site-specific query string in the endpoint address:</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]


<span data-ttu-id="94f29-184">例如，假设生成过程配置为自动部署到过渡环境的 web 应用程序每次成功生成之后。</span><span class="sxs-lookup"><span data-stu-id="94f29-184">For example, suppose a build process is configured to automatically deploy a web application to a staging environment after every successful build.</span></span> <span data-ttu-id="94f29-185">如果使用远程代理方法，您需要在目标服务器上进行的生成进程标识管理员。</span><span class="sxs-lookup"><span data-stu-id="94f29-185">If you used the remote agent approach, you'd need to make the build process identity an administrator on your destination servers.</span></span> <span data-ttu-id="94f29-186">与此相反，使用 Web 部署处理程序方法您可以授予非管理员用户&#x2014;**FABRIKAM\stagingdeployer**在这种情况下&#x2014;，特定的 IIS 网站和生成过程的权限可以提供这些若要将 web 包部署的凭据。</span><span class="sxs-lookup"><span data-stu-id="94f29-186">In contrast, using the Web Deploy Handler approach you can give a non-administrator user&#x2014;**FABRIKAM\stagingdeployer** in this case&#x2014;permission to a specific IIS website only, and the build process can provide these credentials to deploy the web package.</span></span>


[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]


> [!NOTE]
> <span data-ttu-id="94f29-187">Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-187">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="94f29-188">有关使用的详细信息 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-188">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>


<span data-ttu-id="94f29-189">Web 部署处理程序提供了部署在过渡环境、 宿主的环境和基于 intranet 的生产环境中，远程访问服务器可用但不是管理员凭据的有用方法。</span><span class="sxs-lookup"><span data-stu-id="94f29-189">The Web Deploy Handler provides a useful approach to deployment in staging environments, hosted environments, and intranet-based production environments, where remote access to the server is available but administrator credentials are not.</span></span>

<span data-ttu-id="94f29-190">使用 Web 部署处理程序方法的方案的端到端示例，请参阅[方案： 配置用于 Web 部署的过渡环境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="94f29-190">For an end-to-end example of a scenario that uses the Web Deploy Handler approach, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

## <a name="using-offline-deployment"></a><span data-ttu-id="94f29-191">使用离线部署</span><span class="sxs-lookup"><span data-stu-id="94f29-191">Using Offline Deployment</span></span>

<span data-ttu-id="94f29-192">在某些情况下，不可能或可行，若要从远程位置将应用程序和内容部署到 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="94f29-192">In some cases, it's not possible or practical to deploy applications and content to an IIS website from a remote location.</span></span> <span data-ttu-id="94f29-193">例如，在源和目标计算机可能在隔离的网络或网络段或防火墙策略可能不允许远程访问。</span><span class="sxs-lookup"><span data-stu-id="94f29-193">For example, the source and destination computers may be in isolated networks or network segments, or firewall policy may not permit remote access.</span></span>

<span data-ttu-id="94f29-194">在类似这样的情况下，您仍然可以使用打包和发布功能的 Web 部署;您只是不能使用它们从远程位置。</span><span class="sxs-lookup"><span data-stu-id="94f29-194">In scenarios like these, you can still use the packaging and publishing capabilities of Web Deploy; you just can't use them from a remote location.</span></span> <span data-ttu-id="94f29-195">相反，目标服务器上的管理员必须复制到服务器上的 web 包并将其导入通过 IIS 管理器。</span><span class="sxs-lookup"><span data-stu-id="94f29-195">Instead, an administrator on the destination server must copy the web package onto the server and import it through IIS Manager.</span></span>

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

<span data-ttu-id="94f29-196">离线部署方法是在面向 Internet 的生产环境中，其中外围网络中的服务器可能会受到限制与内部网络中的计算机的连接通常很有用。</span><span class="sxs-lookup"><span data-stu-id="94f29-196">The offline deployment approach is typically useful in Internet-facing production environments, where servers in a perimeter network may have restricted connectivity with computers in the internal network.</span></span>

<span data-ttu-id="94f29-197">使用离线部署方法的方案的端到端示例，请参阅[方案： 配置用于 Web 部署的生产环境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="94f29-197">For an end-to-end example of a scenario that uses the offline deployment approach, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

## <a name="further-reading"></a><span data-ttu-id="94f29-198">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="94f29-198">Further Reading</span></span>

<span data-ttu-id="94f29-199">Web 部署命令行操作和语法的详细信息，请参阅[Web 部署命令行参考](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-199">For more information on Web Deploy command-line operations and syntax, see [Web Deploy Command Line Reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx).</span></span> <span data-ttu-id="94f29-200">有关使用的详细信息 *。 deploy.cmd*文件，请参阅[如何： 部署包使用 deploy.cmd 文件安装](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-200">For more information on using the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span>

<span data-ttu-id="94f29-201">可以在其中部署 web 包从远程计算机的不同方式的更多常规指南，请参阅[使用 Web 部署远程](https://technet.microsoft.com/library/ee461175(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-201">For more general guidance on the different ways in which you can deploy web packages from a remote computer, see [Using Web Deploy Remotely](https://technet.microsoft.com/library/ee461175(WS.10).aspx).</span></span> <span data-ttu-id="94f29-202">使用 Web 按需部署的详细信息，请参阅[按需部署的 Web](https://technet.microsoft.com/library/ee517345(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="94f29-202">For more information on using Web Deploy On Demand, see [Web Deploy On Demand](https://technet.microsoft.com/library/ee517345(WS.10).aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="94f29-203">[上一页](configuring-server-environments-for-web-deployment.md)
> [下一页](scenario-configuring-a-test-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="94f29-203">[Previous](configuring-server-environments-for-web-deployment.md)
[Next](scenario-configuring-a-test-environment-for-web-deployment.md)</span></span>
