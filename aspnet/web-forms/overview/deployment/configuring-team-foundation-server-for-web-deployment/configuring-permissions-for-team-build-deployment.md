---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 配置权限的团队生成部署 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何配置权限，以使您的生成服务器将自动 b 的一部分内容部署到 web 服务器和数据库服务器...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: f84e72bd5991b0407008ccdaff5243979cbb986e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37384657"
---
<a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="c31e0-103">配置权限的团队生成部署</span><span class="sxs-lookup"><span data-stu-id="c31e0-103">Configuring Permissions for Team Build Deployment</span></span>
====================
<span data-ttu-id="c31e0-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c31e0-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c31e0-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="c31e0-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c31e0-106">本主题介绍如何配置权限，以使您的生成服务器将自动的生成过程的一部分内容部署到 web 服务器和数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="c31e0-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>


<span data-ttu-id="c31e0-107">本主题窗体的一系列教程基于虚构公司 Fabrikam，Inc.的企业部署要求的一部分本系列教程将使用的示例解决方案&#x2014; [Contact Manager 解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示真实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="c31e0-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="c31e0-108">这些教程的核心部署方法取决于拆分项目文件方法中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，在生成过程由控制这两个项目文件&#x2014;一个包含构建适用于每个目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="c31e0-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="c31e0-109">在生成时，特定于环境的项目文件合并到不限环境的项目文件，以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="c31e0-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c31e0-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="c31e0-110">Task Overview</span></span>

<span data-ttu-id="c31e0-111">在安装 Team Foundation Server (TFS) 2010年生成服务时，你指定想要运行的服务的标识。</span><span class="sxs-lookup"><span data-stu-id="c31e0-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="c31e0-112">默认情况下，这是网络服务帐户。</span><span class="sxs-lookup"><span data-stu-id="c31e0-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="c31e0-113">或者，可以配置生成服务使用域帐户运行。</span><span class="sxs-lookup"><span data-stu-id="c31e0-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="c31e0-114">需要 Windows 身份验证，并且打算使用 Team Build，自动执行的任何部署任务将使用生成服务标识运行。</span><span class="sxs-lookup"><span data-stu-id="c31e0-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="c31e0-115">在这种情况下，你将需要授予你的 web 服务器和数据库服务器上任何所需的权限的生成服务标识。</span><span class="sxs-lookup"><span data-stu-id="c31e0-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="c31e0-116">网络服务帐户使用计算机帐户对其他计算机进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="c31e0-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="c31e0-117">计算机帐户需要在窗体 * [域名]\[计算机名称] ***$**&#x2014;等**FABRIKAM\TFSBUILD$**。</span><span class="sxs-lookup"><span data-stu-id="c31e0-117">Machine accounts take the form *[domain name]\[machine name]***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="c31e0-118">在这种情况下，如果生成服务运行时使用网络服务标识，则应授予计算机帐户标识为任何所需的权限为您的生成服务器。</span><span class="sxs-lookup"><span data-stu-id="c31e0-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>


## <a name="configuring-web-server-permissions"></a><span data-ttu-id="c31e0-119">配置 Web 服务器权限</span><span class="sxs-lookup"><span data-stu-id="c31e0-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="c31e0-120">如中所述[选择右方法对 Web 部署](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)，如果你想要将 web 包部署到远程 web 服务器可以使用两种主要方法：</span><span class="sxs-lookup"><span data-stu-id="c31e0-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="c31e0-121">将从远程位置应用程序部署通过面向*Web 部署代理服务*（也称为远程代理） 目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="c31e0-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="c31e0-122">将从远程位置应用程序部署通过面向*Internet 信息服务*(*IIS) Web 部署处理程序*目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="c31e0-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="c31e0-123">远程代理在这种情况下具有两个关键限制：</span><span class="sxs-lookup"><span data-stu-id="c31e0-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="c31e0-124">远程代理仅支持 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="c31e0-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="c31e0-125">换而言之，部署必须使用生成服务标识&#x2014;不能模拟另一个帐户。</span><span class="sxs-lookup"><span data-stu-id="c31e0-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="c31e0-126">若要使用远程代理，执行部署的帐户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="c31e0-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="c31e0-127">总之，这些两个限制使远程代理方法不可取的 Team Build 的自动化部署。</span><span class="sxs-lookup"><span data-stu-id="c31e0-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="c31e0-128">若要使用此方法，您需要使生成服务帐户在任何目标 web 服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="c31e0-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="c31e0-129">与此相反，Web 部署处理程序方法提供了各种优势：</span><span class="sxs-lookup"><span data-stu-id="c31e0-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="c31e0-130">Web 部署处理程序通过 HTTPS，以便您可以将备用帐户的凭据传递给 IIS Web 部署工具 （Web 部署） 支持基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="c31e0-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="c31e0-131">可以配置目标 web 服务器以允许非管理员用户将内容部署到使用 Web 部署处理程序的特定 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="c31e0-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="c31e0-132">因此，很显然更可取的方法时自动执行从 Team Build web 包部署的目标 Web 部署处理程序。</span><span class="sxs-lookup"><span data-stu-id="c31e0-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="c31e0-133">这是建议采用的过程：</span><span class="sxs-lookup"><span data-stu-id="c31e0-133">This is the recommended process:</span></span>

1. <span data-ttu-id="c31e0-134">创建要用于部署的低特权域帐户。</span><span class="sxs-lookup"><span data-stu-id="c31e0-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="c31e0-135">配置 Web 部署处理程序并为帐户授予所需的权限将内容部署到特定的 IIS 网站，如中所述[用于 Web 部署发布 （Web 部署处理程序） 配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="c31e0-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="c31e0-136">调用 Web 部署和目标 Web 部署处理程序，使用基本身份验证并提供域帐户的凭据创建，来执行部署。</span><span class="sxs-lookup"><span data-stu-id="c31e0-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="c31e0-137">在中[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案，你指定的身份验证类型 (基本或 NTLM)，Web 部署凭据和特定于环境的项目文件中的终结点地址 （远程代理或 Web 部署处理程序）。</span><span class="sxs-lookup"><span data-stu-id="c31e0-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="c31e0-138">这些值用于构建和执行项目文件时运行 Web 部署命令。</span><span class="sxs-lookup"><span data-stu-id="c31e0-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="c31e0-139">有关详细信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="c31e0-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="c31e0-140">有关详细信息配置 Web 部署处理程序，包括如何配置权限，请参阅[用于 Web 部署发布 （Web 部署处理程序） 配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="c31e0-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="c31e0-141">有关配置远程代理的详细信息，请参阅[配置 Web 服务器的 Web 部署发布 （远程代理）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="c31e0-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="c31e0-142">配置数据库服务器权限</span><span class="sxs-lookup"><span data-stu-id="c31e0-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="c31e0-143">若要将数据库部署到 SQL Server，必须：</span><span class="sxs-lookup"><span data-stu-id="c31e0-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="c31e0-144">SQL Server 实例上创建部署帐户的登录名。</span><span class="sxs-lookup"><span data-stu-id="c31e0-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="c31e0-145">授予该登录名**DBCreator** SQL Server 实例上的权限。</span><span class="sxs-lookup"><span data-stu-id="c31e0-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="c31e0-146">在初始部署后添加到的登录名**db\_所有者**对目标数据库的角色。</span><span class="sxs-lookup"><span data-stu-id="c31e0-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="c31e0-147">这是必需的因为在后续部署，您要修改现有数据库而不是创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="c31e0-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="c31e0-148">您可以进行身份验证到使用 NTLM 身份验证或 SQL Server 身份验证的 SQL Server 实例：</span><span class="sxs-lookup"><span data-stu-id="c31e0-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="c31e0-149">如果使用 NTLM 身份验证，需要授予上述生成服务帐户的权限。</span><span class="sxs-lookup"><span data-stu-id="c31e0-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="c31e0-150">如果使用 SQL Server 身份验证，需要授予上述 SQL Server 帐户的权限。</span><span class="sxs-lookup"><span data-stu-id="c31e0-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="c31e0-151">此外需要用于部署的数据库连接字符串中包含的 SQL Server 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="c31e0-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="c31e0-152">有关如何配置权限的数据库部署的分步详细信息，请参阅[配置数据库服务器的 Web 部署发布](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="c31e0-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="c31e0-153">结束语</span><span class="sxs-lookup"><span data-stu-id="c31e0-153">Conclusion</span></span>

<span data-ttu-id="c31e0-154">此时，应了解所需的权限，以及打开您的身份验证选项时自动从 Team Build 的 web 应用程序和数据库部署。</span><span class="sxs-lookup"><span data-stu-id="c31e0-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="c31e0-155">此外应能够在 IIS web 服务器和 SQL Server 数据库服务器上实现所需的权限。</span><span class="sxs-lookup"><span data-stu-id="c31e0-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c31e0-156">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="c31e0-156">Further Reading</span></span>

<span data-ttu-id="c31e0-157">有关配置 Windows server 环境，以支持远程部署的详细信息，请参阅[用于 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="c31e0-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c31e0-158">上一篇</span><span class="sxs-lookup"><span data-stu-id="c31e0-158">Previous</span></span>](deploying-a-specific-build.md)
