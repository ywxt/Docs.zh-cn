---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: 为 Web 程序包部署配置参数 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何设置参数值，如 Internet 信息服务 (IIS) web 应用程序名称、 连接字符串和服务终结点...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: e6db7a8351e01bbbc14eb2b993248ee7d5a84f7e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386544"
---
<a name="configuring-parameters-for-web-package-deployment"></a><span data-ttu-id="d2fa2-103">为 Web 程序包部署配置参数</span><span class="sxs-lookup"><span data-stu-id="d2fa2-103">Configuring Parameters for Web Package Deployment</span></span>
====================
<span data-ttu-id="d2fa2-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="d2fa2-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="d2fa2-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="d2fa2-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="d2fa2-106">本主题介绍如何将 web 包部署到远程 IIS web 服务器时设置参数值，如 Internet 信息服务 (IIS) web 应用程序名称、 连接字符串和服务终结点。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-106">This topic describes how to set parameter values, like Internet Information Services (IIS) web application names, connection strings, and service endpoints, when you deploy a web package to a remote IIS web server.</span></span>


<span data-ttu-id="d2fa2-107">生成 web 应用程序项目、 生成和打包过程时生成三个密钥文件：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-107">When you build a web application project, the build and packaging process generates three key files:</span></span>

- <span data-ttu-id="d2fa2-108">一个 *[项目名称].zip*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-108">A *[project name].zip* file.</span></span> <span data-ttu-id="d2fa2-109">这是你的 web 应用程序项目的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-109">This is the web deployment package for your web application project.</span></span> <span data-ttu-id="d2fa2-110">此包包含所有程序集、 文件、 数据库脚本和重新创建远程 IIS web 服务器上的 web 应用程序所需的资源。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-110">This package contains all the assemblies, files, database scripts, and resources required to recreate your web application on a remote IIS web server.</span></span>
- <span data-ttu-id="d2fa2-111">一个 *[项目名称].deploy.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-111">A *[project name].deploy.cmd* file.</span></span> <span data-ttu-id="d2fa2-112">这包含一系列 web 部署包发布到远程 IIS web 服务器的 Web Deploy (MSDeploy.exe) 的参数化命令。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-112">This contains a set of parameterized Web Deploy (MSDeploy.exe) commands that publish your web deployment package to a remote IIS web server.</span></span>
- <span data-ttu-id="d2fa2-113">一个 *[项目名称]。SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-113">A *[project name].SetParameters.xml* file.</span></span> <span data-ttu-id="d2fa2-114">这提供了一组到 MSDeploy.exe 命令的参数值。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-114">This provides a set of parameter values to the MSDeploy.exe command.</span></span> <span data-ttu-id="d2fa2-115">可以更新此文件中的值并将其传递给 Web 部署作为命令行参数部署 web 包时。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-115">You can update the values in this file and pass it to Web Deploy as a command-line parameter when you deploy your web package.</span></span>

> [!NOTE]
> <span data-ttu-id="d2fa2-116">有关生成和打包过程的详细信息，请参阅[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-116">For more information on the build and packaging process, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>


<span data-ttu-id="d2fa2-117">*SetParameters.xml*文件动态生成 web 应用程序项目文件和你的项目中的任何配置文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-117">The *SetParameters.xml* file is dynamically generated from your web application project file and any configuration files within your project.</span></span> <span data-ttu-id="d2fa2-118">当生成并打包项目中，Web 发布管道 (WPP) 会自动检测大量可能的部署环境，如目标 IIS web 应用程序和任何数据库连接字符串之间发生更改的变量。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-118">When you build and package your project, the Web Publishing Pipeline (WPP) will automatically detect lots of the variables that are likely to change between deployment environments, like the destination IIS web application and any database connection strings.</span></span> <span data-ttu-id="d2fa2-119">这些值是自动参数化 web 部署包中，添加到*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-119">These values are automatically parameterized in the web deployment package and added to the *SetParameters.xml* file.</span></span> <span data-ttu-id="d2fa2-120">例如，如果您添加的连接字符串*web.config*文件在 web 应用程序项目中，生成过程将检测此更改，并将添加到一个条目*SetParameters.xml*文件相应地。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-120">For example, if you add a connection string to the *web.config* file in your web application project, the build process will detect this change and will add an entry to the *SetParameters.xml* file accordingly.</span></span>

<span data-ttu-id="d2fa2-121">在许多情况下，这种自动参数化将足以胜任。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-121">In a lot of cases, this automatic parameterization will be sufficient.</span></span> <span data-ttu-id="d2fa2-122">但是，如果你的用户需要改变的部署环境，如应用程序设置或服务终结点 Url 之间的其他设置您需要告诉 WPP 参数化部署包中的这些值并将相应的条目添加到*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-122">However, if your users need to vary other settings between deployment environments, like application settings or service endpoint URLs, you need to tell the WPP to parameterize these values in the deployment package and add corresponding entries to the *SetParameters.xml* file.</span></span> <span data-ttu-id="d2fa2-123">以下各节说明如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-123">The sections that follow explain how to do this.</span></span>

### <a name="automatic-parameterization"></a><span data-ttu-id="d2fa2-124">自动参数化</span><span class="sxs-lookup"><span data-stu-id="d2fa2-124">Automatic Parameterization</span></span>

<span data-ttu-id="d2fa2-125">当生成和打包 web 应用程序时，WPP 将自动参数化这些内容：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-125">When you build and package a web application, the WPP will automatically parameterize these things:</span></span>

- <span data-ttu-id="d2fa2-126">目标 IIS web 应用程序路径和名称。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-126">The destination IIS web application path and name.</span></span>
- <span data-ttu-id="d2fa2-127">中的任何连接字符串您*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-127">Any connection strings in your *web.config* file.</span></span>
- <span data-ttu-id="d2fa2-128">将添加到任何数据库的连接字符串**打包/发布 SQL**项目属性页中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-128">Connection strings for any databases you add to the **Package/Publish SQL** tab in the project property pages.</span></span>

<span data-ttu-id="d2fa2-129">例如，如果要生成并打包[联系人管理器](the-contact-manager-solution.md)而无需涉及以任何方式 WPP 参数化过程的示例解决方案将生成此*ContactManager.Mvc.SetParameters.xml*文件：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-129">For example, if you were to build and package the [Contact Manager](the-contact-manager-solution.md) sample solution without touching the parameterization process in any way, the WPP would generate this *ContactManager.Mvc.SetParameters.xml* file:</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]


<span data-ttu-id="d2fa2-130">这种情况下：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-130">In this case:</span></span>

- <span data-ttu-id="d2fa2-131">**IIS Web 应用程序名称**参数是你想要部署 web 应用程序的 IIS 路径。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-131">The **IIS Web Application Name** parameter is the IIS path where you want to deploy the web application.</span></span> <span data-ttu-id="d2fa2-132">默认值取自**打包/发布 Web**项目属性页中的页。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-132">The default value is taken from the **Package/Publish Web** page in the project property pages.</span></span>
- <span data-ttu-id="d2fa2-133">**ApplicationServices Web.config 连接字符串**参数从生成**connectionStrings/添加**中的元素*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-133">The **ApplicationServices-Web.config Connection String** parameter was generated from a **connectionStrings/add** element in the *web.config* file.</span></span> <span data-ttu-id="d2fa2-134">它表示应用程序应使用联系成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-134">It represents the connection string that the application should use to contact the membership database.</span></span> <span data-ttu-id="d2fa2-135">此处将提供的值代入已部署*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-135">The value you provide here will be substituted into the deployed *web.config* file.</span></span> <span data-ttu-id="d2fa2-136">默认值取自部署前*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-136">The default value is taken from the pre-deployment *web.config* file.</span></span>

<span data-ttu-id="d2fa2-137">WPP 还对其生成部署包中的这些属性进行参数化。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-137">The WPP also parameterizes these properties in the deployment package it generates.</span></span> <span data-ttu-id="d2fa2-138">在安装部署包时，可以为这些属性提供值。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-138">You can provide values for these properties when you install the deployment package.</span></span> <span data-ttu-id="d2fa2-139">如果您安装包手动通过 IIS 管理器中，如中所述[手动安装 Web 程序包](manually-installing-web-packages.md)，安装向导会提示您提供任何参数的值。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-139">If you install the package manually through IIS Manager, as described in [Manually Installing Web Packages](manually-installing-web-packages.md), the installation wizard prompts you to provide values for any parameters.</span></span> <span data-ttu-id="d2fa2-140">如果安装包使用远程 *。 deploy.cmd*文件，如中所述[部署 Web 包](deploying-web-packages.md)，Web 部署将查找与此*SetParameters.xml*文件为提供的参数值。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-140">If you install the package remotely using the *.deploy.cmd* file, as described in [Deploying Web Packages](deploying-web-packages.md), Web Deploy will look to this *SetParameters.xml* file to provide the parameter values.</span></span> <span data-ttu-id="d2fa2-141">您可以编辑中的值*SetParameters.xml*手动，文件或可自定义自动化生成和部署过程的一部分的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-141">You can edit the values in the *SetParameters.xml* file manually, or you can customize the file as part of an automated build and deployment process.</span></span> <span data-ttu-id="d2fa2-142">本主题后面的更详细地介绍此过程。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-142">This process is described in more detail later in this topic.</span></span>

### <a name="custom-parameterization"></a><span data-ttu-id="d2fa2-143">自定义参数化</span><span class="sxs-lookup"><span data-stu-id="d2fa2-143">Custom Parameterization</span></span>

<span data-ttu-id="d2fa2-144">在更复杂的部署方案中，通常需要在部署你的项目之前，参数化的其他属性。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-144">In more complex deployment scenarios, you'll often want to parameterize additional properties before you deploy your project.</span></span> <span data-ttu-id="d2fa2-145">通常情况下，您应参数化的任何属性和设置目标环境之间而变化的。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-145">Generally speaking, you should parameterize any properties and settings that will vary between destination environments.</span></span> <span data-ttu-id="d2fa2-146">这些条件包括：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-146">These can include:</span></span>

- <span data-ttu-id="d2fa2-147">服务中的终结点*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-147">Service endpoints in the *web.config* file.</span></span>
- <span data-ttu-id="d2fa2-148">中的应用程序设置*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-148">Application settings in the *web.config* file.</span></span>
- <span data-ttu-id="d2fa2-149">为所需的任何其他声明性属性提示用户指定。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-149">Any other declarative properties that you want to prompt users to specify.</span></span>

<span data-ttu-id="d2fa2-150">参数化这些属性的最简单方法是添加*parameters.xml*到你的 web 应用程序项目的根文件夹的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-150">The easiest way to parameterize these properties is to add a *parameters.xml* file to the root folder of your web application project.</span></span> <span data-ttu-id="d2fa2-151">例如，在 Contact Manager 解决方案中，ContactManager.Mvc 项目包括*parameters.xml*根文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-151">For example, in the Contact Manager solution, the ContactManager.Mvc project includes a *parameters.xml* file in the root folder.</span></span>

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

<span data-ttu-id="d2fa2-152">如果您打开此文件，将看到它包含单个**参数**条目。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-152">If you open this file, you'll see that it contains a single **parameter** entry.</span></span> <span data-ttu-id="d2fa2-153">该条目使用的 XML 路径语言 (XPath) 查询来查找并参数化中的 ContactService Windows Communication Foundation (WCF) 服务的终结点 URL *web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-153">The entry uses an XML Path Language (XPath) query to locate and parameterize the endpoint URL of the ContactService Windows Communication Foundation (WCF) service in the *web.config* file.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]


<span data-ttu-id="d2fa2-154">除了参数化的部署包中的终结点 URL，WPP 还将添加到对应的条目*SetParameters.xml*获取与部署包一起生成的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-154">In addition to parameterizing the endpoint URL in the deployment package, the WPP also adds a corresponding entry to the *SetParameters.xml* file that gets generated alongside the deployment package.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]


<span data-ttu-id="d2fa2-155">如果手动安装部署包，IIS 管理器将提示您一起自动参数化的属性的服务终结点地址。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-155">If you install the deployment package manually, IIS Manager will prompt you for the service endpoint address alongside the properties that were parameterized automatically.</span></span> <span data-ttu-id="d2fa2-156">如果运行安装部署包 *。 deploy.cmd*文件中，您可以编辑*SetParameters.xml*文件服务终结点地址的值一起提供的值自动参数化的属性。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-156">If you install the deployment package by running the *.deploy.cmd* file, you can edit the *SetParameters.xml* file to provide a value for the service endpoint address together with values for the properties that were parameterized automatically.</span></span>

<span data-ttu-id="d2fa2-157">有关如何创建完整的详细信息*parameters.xml*文件，请参阅[如何： 安装到配置部署设置包时使用参数](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-157">For full details on how to create a *parameters.xml* file, see [How to: Use Parameters to Configure Deployment Settings When a Package is Installed](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="d2fa2-158">名为的过程**要用于 Web.config 文件设置的部署参数**提供分步说明。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-158">The procedure named **To use deployment parameters for Web.config file settings** provides step-by-step instructions.</span></span>

## <a name="modifying-the-setparametersxml-file"></a><span data-ttu-id="d2fa2-159">修改 SetParameters.xml 文件</span><span class="sxs-lookup"><span data-stu-id="d2fa2-159">Modifying the SetParameters.xml File</span></span>

<span data-ttu-id="d2fa2-160">如果您计划手动部署 web 应用程序包&#x2014;通过运行 *。 deploy.cmd*文件或通过从命令行运行 MSDeploy.exe&#x2014;没有要停止您手动编辑*SetParameters.xml*在部署前的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-160">If you plan to deploy the web application package manually&#x2014;either by running the *.deploy.cmd* file or by running MSDeploy.exe from the command line&#x2014;there's nothing to stop you manually editing the *SetParameters.xml* file prior to the deployment.</span></span> <span data-ttu-id="d2fa2-161">但是，如果您正在处理的企业级解决方案，您可能需要更大、 自动生成和部署过程的一部分部署的 web 应用程序包。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-161">However, if you're working on an enterprise-scale solution, you may need to deploy a web application package as part of a larger, automated build and deployment process.</span></span> <span data-ttu-id="d2fa2-162">在此方案中，您需要 Microsoft Build Engine (MSBuild) 来修改*SetParameters.xml*为你的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-162">In this scenario, you need the Microsoft Build Engine (MSBuild) to modify the *SetParameters.xml* file for you.</span></span> <span data-ttu-id="d2fa2-163">您可以执行此操作通过使用 MSBuild **XmlPoke**任务。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-163">You can do this by using the MSBuild **XmlPoke** task.</span></span>

<span data-ttu-id="d2fa2-164">[联系人管理器示例解决方案](the-contact-manager-solution.md)说明了此过程。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-164">The [Contact Manager sample solution](the-contact-manager-solution.md) illustrates this process.</span></span> <span data-ttu-id="d2fa2-165">下面的代码示例进行了编辑，显示与此示例的详细信息。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-165">The code examples that follow have been edited to show only the details that are relevant to this example.</span></span>

> [!NOTE]
> <span data-ttu-id="d2fa2-166">示例解决方案中与常规中的自定义项目文件的简介中的项目文件模型的更广泛概述，请参阅[了解项目文件](understanding-the-project-file.md)并[了解生成过程](understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-166">For a broader overview of the project file model in the sample solution, and an introduction to custom project files in general, see [Understanding the Project File](understanding-the-project-file.md) and [Understanding the Build Process](understanding-the-build-process.md).</span></span>


<span data-ttu-id="d2fa2-167">首先，将感兴趣的参数值定义为特定于环境的项目文件中的属性 (例如， *Env Dev.proj*)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-167">First, the parameter values of interest are defined as properties in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]


> [!NOTE]
> <span data-ttu-id="d2fa2-168">有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[为目标环境配置部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-168">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


<span data-ttu-id="d2fa2-169">下一步， *Publish.proj*文件导入这些属性。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-169">Next, the *Publish.proj* file imports these properties.</span></span> <span data-ttu-id="d2fa2-170">因为每个*SetParameters.xml*与文件关联 *。 deploy.cmd*文件，和我们最终希望调用每个项目文件 *。 deploy.cmd*文件，项目文件将创建 MSBuild*项*每个 *。 deploy.cmd*文件，并定义为感兴趣的属性*项元数据*。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-170">Because each *SetParameters.xml* file is associated with a *.deploy.cmd* file, and we ultimately want the project file to invoke each *.deploy.cmd* file, the project file creates an MSBuild *item* for each *.deploy.cmd* file and defines the properties of interest as *item metadata*.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]


<span data-ttu-id="d2fa2-171">这种情况下：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-171">In this case:</span></span>

- <span data-ttu-id="d2fa2-172">**ParametersXml**元数据值指示的位置*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-172">The **ParametersXml** metadata value indicates the location of the *SetParameters.xml* file.</span></span>
- <span data-ttu-id="d2fa2-173">**IisWebAppName**值是你想要部署 web 应用程序的 IIS 路径。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-173">The **IisWebAppName** value is the IIS path to which you want to deploy the web application.</span></span>
- <span data-ttu-id="d2fa2-174">**MembershipDBConnectionString**值是成员资格数据库的连接字符串和**MembershipDBConnectionName**值是**名称**属性中的相应参数*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-174">The **MembershipDBConnectionString** value is the connection string for the membership database, and the **MembershipDBConnectionName** value is the **name** attribute of the corresponding parameter in the *SetParameters.xml* file.</span></span>
- <span data-ttu-id="d2fa2-175">**ServiceEndpointValue**值是目标服务器上的 WCF 服务的终结点地址和**ServiceEndpointParamName**值是中的相应参数的名称属性*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-175">The **ServiceEndpointValue** value is the endpoint address for the WCF service on the destination server, and the **ServiceEndpointParamName** value is the name attribute of the corresponding parameter in the *SetParameters.xml* file.</span></span>

<span data-ttu-id="d2fa2-176">最后，在*Publish.proj*文件中， **PublishWebPackages**目标使用**XmlPoke**任务中修改这些值*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-176">Finally, in the *Publish.proj* file, the **PublishWebPackages** target uses the **XmlPoke** task to modify these values in the *SetParameters.xml* file.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]


<span data-ttu-id="d2fa2-177">可以看到，每个**XmlPoke**任务指定四个属性值：</span><span class="sxs-lookup"><span data-stu-id="d2fa2-177">You'll notice that each **XmlPoke** task specifies four attribute values:</span></span>

- <span data-ttu-id="d2fa2-178">**XmlInputPath**属性让任务在哪里可以找到你想要修改的文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-178">The **XmlInputPath** attribute tells the task where to find the file you want to modify.</span></span>
- <span data-ttu-id="d2fa2-179">**查询**属性是标识你想要更改的 XML 节点的 XPath 查询。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-179">The **Query** attribute is an XPath query that identifies the XML node you want to change.</span></span>
- <span data-ttu-id="d2fa2-180">**值**属性是你想要插入到所选的 XML 节点的新值。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-180">The **Value** attribute is the new value you want to insert into the selected XML node.</span></span>
- <span data-ttu-id="d2fa2-181">**条件**属性是该任务应在其运行或未运行的条件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-181">The **Condition** attribute is the criteria on which the task should run or not run.</span></span> <span data-ttu-id="d2fa2-182">在这些情况下，该条件可确保不尝试插入 null 或为空值*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-182">In these cases, the condition ensures that you don't try to insert a null or empty value into the *SetParameters.xml* file.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d2fa2-183">结束语</span><span class="sxs-lookup"><span data-stu-id="d2fa2-183">Conclusion</span></span>

<span data-ttu-id="d2fa2-184">本主题所述的角色*SetParameters.xml*文件，并介绍了在生成 web 应用程序项目时的生成方式。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-184">This topic described the role of the *SetParameters.xml* file and explained how it's generated when you build a web application project.</span></span> <span data-ttu-id="d2fa2-185">它介绍了如何通过添加参数化的其他设置*parameters.xml*到你的项目文件。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-185">It explained how you can parameterize additional settings by adding a *parameters.xml* file to your project.</span></span> <span data-ttu-id="d2fa2-186">它还介绍了如何修改*SetParameters.xml*较大的自动生成过程，通过使用文件**XmlPoke**项目文件中的任务。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-186">It also described how you can modify the *SetParameters.xml* file as part of a larger, automated build process, by using the **XmlPoke** task in your project files.</span></span>

<span data-ttu-id="d2fa2-187">下一主题[部署 Web 包](deploying-web-packages.md)，介绍如何部署 web 包通过运行 *。 deploy.cmd*文件，或者通过使用 MSDeploy.exe 命令直接。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-187">The next topic, [Deploying Web Packages](deploying-web-packages.md), describes how you can deploy a web package either by running the *.deploy.cmd* file or by using MSDeploy.exe commands directly.</span></span> <span data-ttu-id="d2fa2-188">在这两种情况下，您可以指定您*SetParameters.xml*文件作为部署参数。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-188">In both cases, you can specify your *SetParameters.xml* file as a deployment parameter.</span></span>

## <a name="further-reading"></a><span data-ttu-id="d2fa2-189">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="d2fa2-189">Further Reading</span></span>

<span data-ttu-id="d2fa2-190">有关如何创建 web 包的信息，请参阅[构建和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-190">For information on how to create web packages, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="d2fa2-191">有关如何实际部署 web 包的指南，请参阅[部署 Web 包](deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-191">For guidance on how to actually deploy a web package, see [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="d2fa2-192">有关如何创建的分步演练*parameters.xml*文件，请参阅[如何： 安装到配置部署设置包时使用参数](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-192">For a step-by-step walkthrough on how to create a *parameters.xml* file, see [How to: Use Parameters to Configure Deployment Settings When a Package is Installed](https://msdn.microsoft.com/library/ff398068.aspx).</span></span>

<span data-ttu-id="d2fa2-193">Web 部署中的参数化的更多常规信息，请参阅[Web 操作中部署的参数化](https://go.microsoft.com/?linkid=9805119)（博客文章）。</span><span class="sxs-lookup"><span data-stu-id="d2fa2-193">For more general information on parameterization in Web Deploy, see [Web Deploy Parameterization in Action](https://go.microsoft.com/?linkid=9805119) (blog post).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2fa2-194">[上一页](building-and-packaging-web-application-projects.md)
> [下一页](deploying-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d2fa2-194">[Previous](building-and-packaging-web-application-projects.md)
[Next](deploying-web-packages.md)</span></span>
