---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 配置的团队生成权限部署 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何配置权限以使您生成服务器可以自动 b 的一部分将内容部署到 web 服务器和数据库服务器...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 4698349d664816ec49475bbfe71fb32af79ea96d
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "30890276"
---
<a name="configuring-permissions-for-team-build-deployment"></a><span data-ttu-id="77cfe-103">配置权限的团队的生成部署</span><span class="sxs-lookup"><span data-stu-id="77cfe-103">Configuring Permissions for Team Build Deployment</span></span>
====================
<span data-ttu-id="77cfe-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="77cfe-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="77cfe-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="77cfe-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="77cfe-106">本主题介绍如何配置权限以使您生成服务器可以将内容部署到 web 服务器和数据库服务器，作为自动的生成过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="77cfe-106">This topic describes how to configure permissions to enable your build server to deploy content to web servers and database servers as part of an automated build process.</span></span>


<span data-ttu-id="77cfe-107">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案&#x2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="77cfe-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="77cfe-108">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中的生成过程控制通过&#x2014;另一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="77cfe-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="77cfe-109">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="77cfe-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="77cfe-110">任务概述</span><span class="sxs-lookup"><span data-stu-id="77cfe-110">Task Overview</span></span>

<span data-ttu-id="77cfe-111">当你安装 Team Foundation Server (TFS) 2010年生成服务时，你指定想要运行的服务的标识。</span><span class="sxs-lookup"><span data-stu-id="77cfe-111">When you install the Team Foundation Server (TFS) 2010 build service, you specify the identity with which you want the service to run.</span></span> <span data-ttu-id="77cfe-112">默认情况下，这是网络服务帐户。</span><span class="sxs-lookup"><span data-stu-id="77cfe-112">By default, this is the Network Service account.</span></span> <span data-ttu-id="77cfe-113">或者，你可以配置生成服务使用域帐户运行。</span><span class="sxs-lookup"><span data-stu-id="77cfe-113">Alternatively, you can configure the build service to run using a domain account.</span></span>

<span data-ttu-id="77cfe-114">需要 Windows 身份验证，以及你打算自动执行使用 Team Build，任何部署任务将使用的生成服务标识运行。</span><span class="sxs-lookup"><span data-stu-id="77cfe-114">Any deployment tasks that require Windows authentication, and that you plan to automate using Team Build, will run using the build service identity.</span></span> <span data-ttu-id="77cfe-115">在这种情况下，你将需要授予你的 web 服务器和数据库服务器上任何所需的权限的生成服务标识。</span><span class="sxs-lookup"><span data-stu-id="77cfe-115">As such, you'll need to grant the build service identity any required permissions on your web servers and your database servers.</span></span>

> [!NOTE]
> <span data-ttu-id="77cfe-116">网络服务帐户使用的计算机帐户向其他计算机进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="77cfe-116">The Network Service account uses the machine account to authenticate to other computers.</span></span> <span data-ttu-id="77cfe-117">计算机帐户采用格式 * [域名]\[计算机名称] ***$**&#x2014;例如**FABRIKAM\TFSBUILD$**。</span><span class="sxs-lookup"><span data-stu-id="77cfe-117">Machine accounts take the form *[domain name]\[machine name]***$**&#x2014;for example, **FABRIKAM\TFSBUILD$**.</span></span> <span data-ttu-id="77cfe-118">在这种情况下，如果你的生成服务运行时使用的网络服务标识，则应为你的生成服务器授予对计算机帐户标识任何所需的权限。</span><span class="sxs-lookup"><span data-stu-id="77cfe-118">As such, if your build service runs using the Network Service identity, you should grant any required permissions to the machine account identity for your build server.</span></span>


## <a name="configuring-web-server-permissions"></a><span data-ttu-id="77cfe-119">配置 Web 服务器权限</span><span class="sxs-lookup"><span data-stu-id="77cfe-119">Configuring Web Server Permissions</span></span>

<span data-ttu-id="77cfe-120">中所述[选择用于 Web 部署的右方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)，如果你想要将 web 包部署到远程 web 服务器可以使用两种主要方法：</span><span class="sxs-lookup"><span data-stu-id="77cfe-120">As described in [Choosing the Right Approach to Web Deployment](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), there are two main approaches you can use if you want to deploy web packages to a remote web server:</span></span>

- <span data-ttu-id="77cfe-121">通过以目标部署应用程序从远程位置*Web 部署代理服务*（也称为远程代理） 目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="77cfe-121">Deploy the application from a remote location by targeting the *Web Deployment Agent Service* (also known as the remote agent) on the destination server.</span></span>
- <span data-ttu-id="77cfe-122">通过以目标部署应用程序从远程位置*Internet Information Services* (*IIS) Web 部署处理程序*目标服务器上。</span><span class="sxs-lookup"><span data-stu-id="77cfe-122">Deploy the application from a remote location by targeting the *Internet Information Services* (*IIS) Web Deploy Handler* on the destination server.</span></span>

<span data-ttu-id="77cfe-123">远程代理在这种情况下具有两个主要限制：</span><span class="sxs-lookup"><span data-stu-id="77cfe-123">The remote agent has two key limitations in this case:</span></span>

- <span data-ttu-id="77cfe-124">远程代理支持仅 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="77cfe-124">The remote agent supports only NTLM authentication.</span></span> <span data-ttu-id="77cfe-125">换而言之，部署必须使用生成服务标识&#x2014;不能模拟另一个帐户。</span><span class="sxs-lookup"><span data-stu-id="77cfe-125">In other words, the deployment must use the build service identity&#x2014;you can't impersonate another account.</span></span>
- <span data-ttu-id="77cfe-126">若要使用远程代理，请执行部署的帐户必须是目标服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="77cfe-126">To use the remote agent, the account that performs the deployment must be an administrator on the target server.</span></span>

<span data-ttu-id="77cfe-127">总之，这些两个限制使远程代理方法不希望出现自动 Team Build 部署。</span><span class="sxs-lookup"><span data-stu-id="77cfe-127">Together, these two limitations make the remote agent approach undesirable for an automated Team Build deployment.</span></span> <span data-ttu-id="77cfe-128">若要使用此方法，你需要使生成服务帐户在任何目标 web 服务器上的管理员。</span><span class="sxs-lookup"><span data-stu-id="77cfe-128">To use this approach, you'd need to make the build service account an administrator on any target web servers.</span></span>

<span data-ttu-id="77cfe-129">与此相反，Web 部署处理程序方法提供了各种优势：</span><span class="sxs-lookup"><span data-stu-id="77cfe-129">In contrast, the Web Deploy Handler approach offers various advantages:</span></span>

- <span data-ttu-id="77cfe-130">Web 部署处理程序通过 HTTPS，允许你将备用帐户的凭据传递给 IIS Web 部署工具 （Web 部署） 支持基本身份验证。</span><span class="sxs-lookup"><span data-stu-id="77cfe-130">The Web Deploy Handler supports basic authentication over HTTPS, which allows you to pass the credentials of an alternative account to the IIS Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="77cfe-131">你可以配置目标 web 服务器，以允许非管理员用户将内容部署到特定使用 Web 部署处理程序的 IIS 网站。</span><span class="sxs-lookup"><span data-stu-id="77cfe-131">You can configure target web servers to allow non-administrator users to deploy content to specific IIS websites using the Web Deploy Handler.</span></span>

<span data-ttu-id="77cfe-132">因此，很显然更可取的方法时自动执行 Team Build 中的 web 包部署的目标 Web 部署处理程序。</span><span class="sxs-lookup"><span data-stu-id="77cfe-132">As a result, it's clearly preferable to target the Web Deploy Handler when you automate web package deployment from Team Build.</span></span> <span data-ttu-id="77cfe-133">这是建议的过程：</span><span class="sxs-lookup"><span data-stu-id="77cfe-133">This is the recommended process:</span></span>

1. <span data-ttu-id="77cfe-134">创建用于部署的低特权域帐户。</span><span class="sxs-lookup"><span data-stu-id="77cfe-134">Create a low-privileged domain account to use for the deployment.</span></span>
2. <span data-ttu-id="77cfe-135">配置 Web 部署处理程序和中所述向帐户授予所需的权限，将内容部署到特定的 IIS 网站，[配置用于 Web 部署发布 （Web 部署处理程序） 的 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="77cfe-135">Configure the Web Deploy Handler and grant the account the required permissions to deploy content to a specific IIS website, as described in [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span>
3. <span data-ttu-id="77cfe-136">调用 Web 部署和面向 Web 部署处理程序，使用基本身份验证并提供域帐户的凭据创建，以执行部署。</span><span class="sxs-lookup"><span data-stu-id="77cfe-136">Invoke Web Deploy and target the Web Deploy Handler, using basic authentication and supplying the credentials of the domain account you created, to perform the deployment.</span></span>

<span data-ttu-id="77cfe-137">在[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案，你指定的身份验证类型 (基本或 NTLM)，Web 部署凭据和特定于环境的项目文件中的终结点地址 （远程代理或 Web 部署处理程序）。</span><span class="sxs-lookup"><span data-stu-id="77cfe-137">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, you specify the authentication type (basic or NTLM), the Web Deploy credentials, and the endpoint address (remote agent or Web Deploy Handler) in the environment-specific project file.</span></span> <span data-ttu-id="77cfe-138">这些值用于制定和项目文件执行时运行 Web 部署命令。</span><span class="sxs-lookup"><span data-stu-id="77cfe-138">These values are used to formulate and run a Web Deploy command when the project file is executed.</span></span> <span data-ttu-id="77cfe-139">有关详细信息，请参阅[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="77cfe-139">For more information, see [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="77cfe-140">有关详细信息配置 Web 部署处理程序，包括如何配置权限，请参阅[配置用于 Web 部署发布 （Web 部署处理程序） 的 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="77cfe-140">For more information on configuring the Web Deploy Handler, including how to configure permissions, see [Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="77cfe-141">有关配置远程代理的详细信息，请参阅[配置用于 Web 部署发布 （远程代理） 的 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。</span><span class="sxs-lookup"><span data-stu-id="77cfe-141">For more information on configuring the remote agent, see [Configuring a Web Server for Web Deploy Publishing (Remote Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).</span></span>

## <a name="configuring-database-server-permissions"></a><span data-ttu-id="77cfe-142">配置数据库服务器权限</span><span class="sxs-lookup"><span data-stu-id="77cfe-142">Configuring Database Server Permissions</span></span>

<span data-ttu-id="77cfe-143">若要将数据库部署到 SQL Server，你必须：</span><span class="sxs-lookup"><span data-stu-id="77cfe-143">To deploy a database to SQL Server, you must:</span></span>

- <span data-ttu-id="77cfe-144">SQL Server 实例上创建部署的帐户的登录名。</span><span class="sxs-lookup"><span data-stu-id="77cfe-144">Create a login for the deploying account on the SQL Server instance.</span></span>
- <span data-ttu-id="77cfe-145">登录名授予**DBCreator** SQL Server 实例上的权限。</span><span class="sxs-lookup"><span data-stu-id="77cfe-145">Grant the login **DBCreator** permissions on the SQL Server instance.</span></span>
- <span data-ttu-id="77cfe-146">初始部署之后，将登录添加到**db\_所有者**目标数据库上的角色。</span><span class="sxs-lookup"><span data-stu-id="77cfe-146">After the initial deployment, add the login to the **db\_owner** role on the target database.</span></span> <span data-ttu-id="77cfe-147">这是必需的因为在后续部署上您要修改现有数据库，而不创建新的数据库。</span><span class="sxs-lookup"><span data-stu-id="77cfe-147">This is required because on subsequent deployments, you're modifying an existing database rather than creating a new database.</span></span>

<span data-ttu-id="77cfe-148">你可以进行身份验证到使用 NTLM 身份验证或 SQL Server 身份验证的 SQL Server 实例：</span><span class="sxs-lookup"><span data-stu-id="77cfe-148">You can authenticate to a SQL Server instance using either NTLM authentication or SQL Server authentication:</span></span>

- <span data-ttu-id="77cfe-149">如果使用 NTLM 身份验证，你需要授予上面所述与生成服务帐户的权限。</span><span class="sxs-lookup"><span data-stu-id="77cfe-149">If you use NTLM authentication, you need to grant the permissions described above to the build service account.</span></span>
- <span data-ttu-id="77cfe-150">如果你使用 SQL Server 身份验证，你需要授予上述到 SQL Server 帐户的权限。</span><span class="sxs-lookup"><span data-stu-id="77cfe-150">If you use SQL Server authentication, you need to grant the permissions described above to the SQL Server account.</span></span> <span data-ttu-id="77cfe-151">你还需要在你用于部署数据库的连接字符串中包含的 SQL Server 用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="77cfe-151">You also need to include the SQL Server user name and password in the connection string you use to deploy the database.</span></span>

<span data-ttu-id="77cfe-152">有关如何配置数据库部署的权限的分步详细信息，请参阅[数据库服务器配置用于 Web 部署发布](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="77cfe-152">For step-by-step details on how to configure permissions for database deployment, see [Configuring a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

## <a name="conclusion"></a><span data-ttu-id="77cfe-153">结束语</span><span class="sxs-lookup"><span data-stu-id="77cfe-153">Conclusion</span></span>

<span data-ttu-id="77cfe-154">此时，你应该了解所需的权限，以及打开你的身份验证选项时自动进行 Team Build 中的 web 应用程序和数据库部署。</span><span class="sxs-lookup"><span data-stu-id="77cfe-154">At this point, you should understand the permissions required, together with the authentication options open to you, when you automate web application and database deployments from Team Build.</span></span> <span data-ttu-id="77cfe-155">你还应是能够实现对 IIS web 服务器和 SQL Server 数据库服务器的所需的权限。</span><span class="sxs-lookup"><span data-stu-id="77cfe-155">You should also be able to implement the necessary permissions on IIS web servers and SQL Server database servers.</span></span>

## <a name="further-reading"></a><span data-ttu-id="77cfe-156">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="77cfe-156">Further Reading</span></span>

<span data-ttu-id="77cfe-157">有关配置 Windows server 环境以支持远程部署的详细信息，请参阅[用于 Web 部署配置服务器环境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="77cfe-157">For more information on configuring Windows server environments to support remote deployment, see [Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="77cfe-158">上一篇</span><span class="sxs-lookup"><span data-stu-id="77cfe-158">Previous</span></span>](deploying-a-specific-build.md)
