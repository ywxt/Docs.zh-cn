---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: 为 Web 包部署中配置参数 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何设置参数的值，如 Internet 信息服务 (IIS) web 应用程序名称、 连接字符串和服务终结点...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: 7be08f1a1fb7232911a44cf64e2e784dbb95ff48
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30880396"
---
<a name="configuring-parameters-for-web-package-deployment"></a><span data-ttu-id="936d7-103">为 Web 包部署中配置参数</span><span class="sxs-lookup"><span data-stu-id="936d7-103">Configuring Parameters for Web Package Deployment</span></span>
====================
<span data-ttu-id="936d7-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="936d7-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="936d7-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="936d7-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="936d7-106">本主题介绍如何在 web 包部署到远程 IIS web 服务器时设置参数的值，如 Internet 信息服务 (IIS) web 应用程序名称、 连接字符串和服务终结点。</span><span class="sxs-lookup"><span data-stu-id="936d7-106">This topic describes how to set parameter values, like Internet Information Services (IIS) web application names, connection strings, and service endpoints, when you deploy a web package to a remote IIS web server.</span></span>


<span data-ttu-id="936d7-107">生成的 web 应用程序项目、 生成和打包过程时生成三个关键文件：</span><span class="sxs-lookup"><span data-stu-id="936d7-107">When you build a web application project, the build and packaging process generates three key files:</span></span>

- <span data-ttu-id="936d7-108">A *[项目名称].zip*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-108">A *[project name].zip* file.</span></span> <span data-ttu-id="936d7-109">这是你的 web 应用程序项目的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="936d7-109">This is the web deployment package for your web application project.</span></span> <span data-ttu-id="936d7-110">此程序包包含所有程序集、 文件、 数据库脚本和重新创建远程 IIS web 服务器上的 web 应用程序所需资源。</span><span class="sxs-lookup"><span data-stu-id="936d7-110">This package contains all the assemblies, files, database scripts, and resources required to recreate your web application on a remote IIS web server.</span></span>
- <span data-ttu-id="936d7-111">A *[项目名称].deploy.cmd*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-111">A *[project name].deploy.cmd* file.</span></span> <span data-ttu-id="936d7-112">这包含一组将你的 web 部署包发布到远程的 IIS web 服务器的 Web Deploy (MSDeploy.exe) 的参数化命令。</span><span class="sxs-lookup"><span data-stu-id="936d7-112">This contains a set of parameterized Web Deploy (MSDeploy.exe) commands that publish your web deployment package to a remote IIS web server.</span></span>
- <span data-ttu-id="936d7-113">A *[项目名称]。SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-113">A *[project name].SetParameters.xml* file.</span></span> <span data-ttu-id="936d7-114">这提供了一套到 MSDeploy.exe 命令的参数值。</span><span class="sxs-lookup"><span data-stu-id="936d7-114">This provides a set of parameter values to the MSDeploy.exe command.</span></span> <span data-ttu-id="936d7-115">你可以更新此文件中的值，并将其传递给 Web 部署作为命令行参数部署 web 包时。</span><span class="sxs-lookup"><span data-stu-id="936d7-115">You can update the values in this file and pass it to Web Deploy as a command-line parameter when you deploy your web package.</span></span>

> [!NOTE]
> <span data-ttu-id="936d7-116">生成和打包过程的详细信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="936d7-116">For more information on the build and packaging process, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>


<span data-ttu-id="936d7-117">*SetParameters.xml*文件动态生成从你的 web 应用程序项目文件和你的项目中任何配置文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-117">The *SetParameters.xml* file is dynamically generated from your web application project file and any configuration files within your project.</span></span> <span data-ttu-id="936d7-118">当生成并打包你的项目，Web 发布管道 (WPP) 将自动检测大量倾向于部署环境，如目标 IIS web 应用程序和任何数据库连接字符串之间发生更改的变量。</span><span class="sxs-lookup"><span data-stu-id="936d7-118">When you build and package your project, the Web Publishing Pipeline (WPP) will automatically detect lots of the variables that are likely to change between deployment environments, like the destination IIS web application and any database connection strings.</span></span> <span data-ttu-id="936d7-119">这些值自动参数化 web 部署包中，添加到*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-119">These values are automatically parameterized in the web deployment package and added to the *SetParameters.xml* file.</span></span> <span data-ttu-id="936d7-120">例如，如果你添加的连接字符串*web.config*文件在 web 应用程序项目中，生成过程将检测此更改，并将添加到一个条目*SetParameters.xml*文件相应地。</span><span class="sxs-lookup"><span data-stu-id="936d7-120">For example, if you add a connection string to the *web.config* file in your web application project, the build process will detect this change and will add an entry to the *SetParameters.xml* file accordingly.</span></span>

<span data-ttu-id="936d7-121">在许多情况下，此自动参数化将足够。</span><span class="sxs-lookup"><span data-stu-id="936d7-121">In a lot of cases, this automatic parameterization will be sufficient.</span></span> <span data-ttu-id="936d7-122">但是，如果你的用户需要更改其他设置之间部署环境，如应用程序设置或服务终结点 Url，你需要告诉 WPP 参数化部署包中的这些值并将相应的项添加到*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-122">However, if your users need to vary other settings between deployment environments, like application settings or service endpoint URLs, you need to tell the WPP to parameterize these values in the deployment package and add corresponding entries to the *SetParameters.xml* file.</span></span> <span data-ttu-id="936d7-123">以下各节说明如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="936d7-123">The sections that follow explain how to do this.</span></span>

### <a name="automatic-parameterization"></a><span data-ttu-id="936d7-124">自动参数化</span><span class="sxs-lookup"><span data-stu-id="936d7-124">Automatic Parameterization</span></span>

<span data-ttu-id="936d7-125">当生成和打包 web 应用程序时，WPP 将自动参数化以下操作：</span><span class="sxs-lookup"><span data-stu-id="936d7-125">When you build and package a web application, the WPP will automatically parameterize these things:</span></span>

- <span data-ttu-id="936d7-126">目标 IIS web 应用程序路径和名称。</span><span class="sxs-lookup"><span data-stu-id="936d7-126">The destination IIS web application path and name.</span></span>
- <span data-ttu-id="936d7-127">中的任何连接字符串你*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-127">Any connection strings in your *web.config* file.</span></span>
- <span data-ttu-id="936d7-128">你将添加到任何数据库的连接字符串**打包/发布 SQL**在项目属性页中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="936d7-128">Connection strings for any databases you add to the **Package/Publish SQL** tab in the project property pages.</span></span>

<span data-ttu-id="936d7-129">例如，如果你打算生成并打包[联系人管理器](the-contact-manager-solution.md)而无需触摸以任何方式，WPP 的参数化过程的示例解决方案也会生成此*ContactManager.Mvc.SetParameters.xml*文件：</span><span class="sxs-lookup"><span data-stu-id="936d7-129">For example, if you were to build and package the [Contact Manager](the-contact-manager-solution.md) sample solution without touching the parameterization process in any way, the WPP would generate this *ContactManager.Mvc.SetParameters.xml* file:</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]


<span data-ttu-id="936d7-130">这种情况下：</span><span class="sxs-lookup"><span data-stu-id="936d7-130">In this case:</span></span>

- <span data-ttu-id="936d7-131">**IIS Web 应用程序名称**参数是你想要部署 web 应用程序的 IIS 路径。</span><span class="sxs-lookup"><span data-stu-id="936d7-131">The **IIS Web Application Name** parameter is the IIS path where you want to deploy the web application.</span></span> <span data-ttu-id="936d7-132">默认值取自**打包/发布 Web**在项目属性页中的页。</span><span class="sxs-lookup"><span data-stu-id="936d7-132">The default value is taken from the **Package/Publish Web** page in the project property pages.</span></span>
- <span data-ttu-id="936d7-133">**ApplicationServices Web.config 连接字符串**参数从生成**添加 connectionStrings/** 中的元素*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-133">The **ApplicationServices-Web.config Connection String** parameter was generated from a **connectionStrings/add** element in the *web.config* file.</span></span> <span data-ttu-id="936d7-134">它表示应用程序应使用联系成员资格数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="936d7-134">It represents the connection string that the application should use to contact the membership database.</span></span> <span data-ttu-id="936d7-135">此处将提供的值替换到部署*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-135">The value you provide here will be substituted into the deployed *web.config* file.</span></span> <span data-ttu-id="936d7-136">默认值取自预部署*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-136">The default value is taken from the pre-deployment *web.config* file.</span></span>

<span data-ttu-id="936d7-137">WPP 还使它生成的部署包中的这些属性进行参数化。</span><span class="sxs-lookup"><span data-stu-id="936d7-137">The WPP also parameterizes these properties in the deployment package it generates.</span></span> <span data-ttu-id="936d7-138">当你安装的部署包时，你可以为这些属性提供值。</span><span class="sxs-lookup"><span data-stu-id="936d7-138">You can provide values for these properties when you install the deployment package.</span></span> <span data-ttu-id="936d7-139">如果你安装包手动通过 IIS 管理器中所述[手动安装 Web 包](manually-installing-web-packages.md)，安装向导会提示您提供任何参数的值。</span><span class="sxs-lookup"><span data-stu-id="936d7-139">If you install the package manually through IIS Manager, as described in [Manually Installing Web Packages](manually-installing-web-packages.md), the installation wizard prompts you to provide values for any parameters.</span></span> <span data-ttu-id="936d7-140">当你安装使用远程包 *。 deploy.cmd*文件，如下所述[部署 Web 包](deploying-web-packages.md)，Web 部署将此查找*SetParameters.xml*到文件提供参数值。</span><span class="sxs-lookup"><span data-stu-id="936d7-140">If you install the package remotely using the *.deploy.cmd* file, as described in [Deploying Web Packages](deploying-web-packages.md), Web Deploy will look to this *SetParameters.xml* file to provide the parameter values.</span></span> <span data-ttu-id="936d7-141">你可以编辑中的值*SetParameters.xml*文件手动，或可以自定义自动化的生成和部署过程的一部分的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-141">You can edit the values in the *SetParameters.xml* file manually, or you can customize the file as part of an automated build and deployment process.</span></span> <span data-ttu-id="936d7-142">本主题中后面的更详细地描述了此过程。</span><span class="sxs-lookup"><span data-stu-id="936d7-142">This process is described in more detail later in this topic.</span></span>

### <a name="custom-parameterization"></a><span data-ttu-id="936d7-143">自定义参数化</span><span class="sxs-lookup"><span data-stu-id="936d7-143">Custom Parameterization</span></span>

<span data-ttu-id="936d7-144">在更复杂的部署方案中，通常需要在部署你的项目之前，参数化的其他属性。</span><span class="sxs-lookup"><span data-stu-id="936d7-144">In more complex deployment scenarios, you'll often want to parameterize additional properties before you deploy your project.</span></span> <span data-ttu-id="936d7-145">通常情况下，你应参数化的任何属性和将改变目标环境之间的设置。</span><span class="sxs-lookup"><span data-stu-id="936d7-145">Generally speaking, you should parameterize any properties and settings that will vary between destination environments.</span></span> <span data-ttu-id="936d7-146">这些错误可能包括：</span><span class="sxs-lookup"><span data-stu-id="936d7-146">These can include:</span></span>

- <span data-ttu-id="936d7-147">服务中的终结点*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-147">Service endpoints in the *web.config* file.</span></span>
- <span data-ttu-id="936d7-148">应用程序设置中的*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-148">Application settings in the *web.config* file.</span></span>
- <span data-ttu-id="936d7-149">你希望的任何其他声明性属性提示用户指定。</span><span class="sxs-lookup"><span data-stu-id="936d7-149">Any other declarative properties that you want to prompt users to specify.</span></span>

<span data-ttu-id="936d7-150">参数化这些属性的最简单方法是添加*parameters.xml*到你的 web 应用程序项目的根文件夹的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-150">The easiest way to parameterize these properties is to add a *parameters.xml* file to the root folder of your web application project.</span></span> <span data-ttu-id="936d7-151">例如，解决方案中的联系人管理器、 ContactManager.Mvc 项目包括*parameters.xml*的根文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-151">For example, in the Contact Manager solution, the ContactManager.Mvc project includes a *parameters.xml* file in the root folder.</span></span>

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

<span data-ttu-id="936d7-152">如果打开此文件，你将看到它包含单个**参数**条目。</span><span class="sxs-lookup"><span data-stu-id="936d7-152">If you open this file, you'll see that it contains a single **parameter** entry.</span></span> <span data-ttu-id="936d7-153">该条目使用 XML 路径语言 (XPath) 查询来查找并参数化中的 ContactService Windows Communication Foundation (WCF) 服务的终结点 URL *web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-153">The entry uses an XML Path Language (XPath) query to locate and parameterize the endpoint URL of the ContactService Windows Communication Foundation (WCF) service in the *web.config* file.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]


<span data-ttu-id="936d7-154">除了部署包中的终结点 URL 中参数化，WPP 还添加到一个对应的条目*SetParameters.xml*与部署包一起获取生成的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-154">In addition to parameterizing the endpoint URL in the deployment package, the WPP also adds a corresponding entry to the *SetParameters.xml* file that gets generated alongside the deployment package.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]


<span data-ttu-id="936d7-155">如果你手动安装的部署包，IIS 管理器将提示你自动参数化的属性旁边的服务终结点地址。</span><span class="sxs-lookup"><span data-stu-id="936d7-155">If you install the deployment package manually, IIS Manager will prompt you for the service endpoint address alongside the properties that were parameterized automatically.</span></span> <span data-ttu-id="936d7-156">当你通过运行安装了部署包 *。 deploy.cmd*文件，你可以编辑*SetParameters.xml*文件服务终结点地址以及为值提供的值自动参数化的属性。</span><span class="sxs-lookup"><span data-stu-id="936d7-156">If you install the deployment package by running the *.deploy.cmd* file, you can edit the *SetParameters.xml* file to provide a value for the service endpoint address together with values for the properties that were parameterized automatically.</span></span>

<span data-ttu-id="936d7-157">有关如何创建的完整详细信息*parameters.xml*文件，请参阅[如何： 安装到配置部署设置包时使用参数](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="936d7-157">For full details on how to create a *parameters.xml* file, see [How to: Use Parameters to Configure Deployment Settings When a Package is Installed](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="936d7-158">名为的过程**要用于 Web.config 文件设置的部署参数**提供分步说明。</span><span class="sxs-lookup"><span data-stu-id="936d7-158">The procedure named **To use deployment parameters for Web.config file settings** provides step-by-step instructions.</span></span>

## <a name="modifying-the-setparametersxml-file"></a><span data-ttu-id="936d7-159">修改 SetParameters.xml 文件</span><span class="sxs-lookup"><span data-stu-id="936d7-159">Modifying the SetParameters.xml File</span></span>

<span data-ttu-id="936d7-160">如果你计划手动部署 web 应用程序包&#x2014;通过运行 *。 deploy.cmd*文件或通过从命令行运行 MSDeploy.exe&#x2014;无需进行任何停止你手动编辑*SetParameters.xml*之前部署的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-160">If you plan to deploy the web application package manually&#x2014;either by running the *.deploy.cmd* file or by running MSDeploy.exe from the command line&#x2014;there's nothing to stop you manually editing the *SetParameters.xml* file prior to the deployment.</span></span> <span data-ttu-id="936d7-161">但是，如果你正在对企业级解决方案，你可能需要将 web 应用程序包部署更大、 自动生成和部署过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="936d7-161">However, if you're working on an enterprise-scale solution, you may need to deploy a web application package as part of a larger, automated build and deployment process.</span></span> <span data-ttu-id="936d7-162">在此方案中，你需要 Microsoft Build Engine (MSBuild) 修改*SetParameters.xml*为你的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-162">In this scenario, you need the Microsoft Build Engine (MSBuild) to modify the *SetParameters.xml* file for you.</span></span> <span data-ttu-id="936d7-163">你可以执行此操作使用 MSBuild **XmlPoke**任务。</span><span class="sxs-lookup"><span data-stu-id="936d7-163">You can do this by using the MSBuild **XmlPoke** task.</span></span>

<span data-ttu-id="936d7-164">[联系人管理器示例解决方案](the-contact-manager-solution.md)阐释了此过程。</span><span class="sxs-lookup"><span data-stu-id="936d7-164">The [Contact Manager sample solution](the-contact-manager-solution.md) illustrates this process.</span></span> <span data-ttu-id="936d7-165">下面的代码示例进行了编辑，显示与此示例相关的详细信息。</span><span class="sxs-lookup"><span data-stu-id="936d7-165">The code examples that follow have been edited to show only the details that are relevant to this example.</span></span>

> [!NOTE]
> <span data-ttu-id="936d7-166">示例解决方案中，以及对自定义项目文件的常规介绍中的项目文件模型的更广泛概述，请参阅[了解项目文件](understanding-the-project-file.md)和[了解该生成过程](understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="936d7-166">For a broader overview of the project file model in the sample solution, and an introduction to custom project files in general, see [Understanding the Project File](understanding-the-project-file.md) and [Understanding the Build Process](understanding-the-build-process.md).</span></span>


<span data-ttu-id="936d7-167">首先，感兴趣的参数值指特定于环境的项目文件中的属性 (例如， *Env Dev.proj*)。</span><span class="sxs-lookup"><span data-stu-id="936d7-167">First, the parameter values of interest are defined as properties in the environment-specific project file (for example, *Env-Dev.proj*).</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]


> [!NOTE]
> <span data-ttu-id="936d7-168">有关如何自定义服务器环境的特定于环境的项目文件的指南，请参阅[配置为目标环境的部署属性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="936d7-168">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>


<span data-ttu-id="936d7-169">接下来， *Publish.proj*文件导入这些属性。</span><span class="sxs-lookup"><span data-stu-id="936d7-169">Next, the *Publish.proj* file imports these properties.</span></span> <span data-ttu-id="936d7-170">因为每个*SetParameters.xml*文件关联 *。 deploy.cmd*文件和我们最终需要调用每个项目文件 *。 deploy.cmd*文件，项目文件将创建 MSBuild*项*每个 *。 deploy.cmd*文件，并定义为感兴趣的属性*项元数据*。</span><span class="sxs-lookup"><span data-stu-id="936d7-170">Because each *SetParameters.xml* file is associated with a *.deploy.cmd* file, and we ultimately want the project file to invoke each *.deploy.cmd* file, the project file creates an MSBuild *item* for each *.deploy.cmd* file and defines the properties of interest as *item metadata*.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]


<span data-ttu-id="936d7-171">这种情况下：</span><span class="sxs-lookup"><span data-stu-id="936d7-171">In this case:</span></span>

- <span data-ttu-id="936d7-172">**ParametersXml**元数据的值指示的位置*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-172">The **ParametersXml** metadata value indicates the location of the *SetParameters.xml* file.</span></span>
- <span data-ttu-id="936d7-173">**IisWebAppName**值是你想要部署 web 应用程序的 IIS 路径。</span><span class="sxs-lookup"><span data-stu-id="936d7-173">The **IisWebAppName** value is the IIS path to which you want to deploy the web application.</span></span>
- <span data-ttu-id="936d7-174">**MembershipDBConnectionString**值是成员资格数据库的连接字符串和**MembershipDBConnectionName**值是**名称**属性中的相应参数*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-174">The **MembershipDBConnectionString** value is the connection string for the membership database, and the **MembershipDBConnectionName** value is the **name** attribute of the corresponding parameter in the *SetParameters.xml* file.</span></span>
- <span data-ttu-id="936d7-175">**ServiceEndpointValue**值是目标服务器上的 WCF 服务的终结点地址和**ServiceEndpointParamName**值中的相应参数的名称属性*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-175">The **ServiceEndpointValue** value is the endpoint address for the WCF service on the destination server, and the **ServiceEndpointParamName** value is the name attribute of the corresponding parameter in the *SetParameters.xml* file.</span></span>

<span data-ttu-id="936d7-176">最后，在*Publish.proj*文件， **PublishWebPackages**目标使用**XmlPoke**任务要修改这些值在*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-176">Finally, in the *Publish.proj* file, the **PublishWebPackages** target uses the **XmlPoke** task to modify these values in the *SetParameters.xml* file.</span></span>


[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]


<span data-ttu-id="936d7-177">你将会发现，每个**XmlPoke**任务指定四个属性值：</span><span class="sxs-lookup"><span data-stu-id="936d7-177">You'll notice that each **XmlPoke** task specifies four attribute values:</span></span>

- <span data-ttu-id="936d7-178">**XmlInputPath**属性告知任务在哪里可以找到你想要修改的文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-178">The **XmlInputPath** attribute tells the task where to find the file you want to modify.</span></span>
- <span data-ttu-id="936d7-179">**查询**属性是一个标识你想要更改的 XML 节点的 XPath 查询。</span><span class="sxs-lookup"><span data-stu-id="936d7-179">The **Query** attribute is an XPath query that identifies the XML node you want to change.</span></span>
- <span data-ttu-id="936d7-180">**值**属性是你想要插入到所选的 XML 节点的新值。</span><span class="sxs-lookup"><span data-stu-id="936d7-180">The **Value** attribute is the new value you want to insert into the selected XML node.</span></span>
- <span data-ttu-id="936d7-181">**条件**属性是该任务应在其运行或未运行的条件。</span><span class="sxs-lookup"><span data-stu-id="936d7-181">The **Condition** attribute is the criteria on which the task should run or not run.</span></span> <span data-ttu-id="936d7-182">在这些情况下，该条件可确保不尝试插入 null 或为空值*SetParameters.xml*文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-182">In these cases, the condition ensures that you don't try to insert a null or empty value into the *SetParameters.xml* file.</span></span>

## <a name="conclusion"></a><span data-ttu-id="936d7-183">结束语</span><span class="sxs-lookup"><span data-stu-id="936d7-183">Conclusion</span></span>

<span data-ttu-id="936d7-184">本主题所述的角色*SetParameters.xml*文件并且说明了在生成 web 应用程序项目时的生成方式。</span><span class="sxs-lookup"><span data-stu-id="936d7-184">This topic described the role of the *SetParameters.xml* file and explained how it's generated when you build a web application project.</span></span> <span data-ttu-id="936d7-185">它说明如何通过添加参数化的其他设置*parameters.xml*到你的项目文件。</span><span class="sxs-lookup"><span data-stu-id="936d7-185">It explained how you can parameterize additional settings by adding a *parameters.xml* file to your project.</span></span> <span data-ttu-id="936d7-186">它还介绍了如何修改*SetParameters.xml*文件作为更大、 自动生成过程，通过使用的一部分**XmlPoke**项目文件中的任务。</span><span class="sxs-lookup"><span data-stu-id="936d7-186">It also described how you can modify the *SetParameters.xml* file as part of a larger, automated build process, by using the **XmlPoke** task in your project files.</span></span>

<span data-ttu-id="936d7-187">下一主题[部署 Web 包](deploying-web-packages.md)，描述你如何可以部署 web 包通过运行 *。 deploy.cmd*文件，或者通过使用 MSDeploy.exe 命令直接。</span><span class="sxs-lookup"><span data-stu-id="936d7-187">The next topic, [Deploying Web Packages](deploying-web-packages.md), describes how you can deploy a web package either by running the *.deploy.cmd* file or by using MSDeploy.exe commands directly.</span></span> <span data-ttu-id="936d7-188">在这两种情况下，你可以指定你*SetParameters.xml*文件作为部署参数。</span><span class="sxs-lookup"><span data-stu-id="936d7-188">In both cases, you can specify your *SetParameters.xml* file as a deployment parameter.</span></span>

## <a name="further-reading"></a><span data-ttu-id="936d7-189">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="936d7-189">Further Reading</span></span>

<span data-ttu-id="936d7-190">有关如何创建 web 包的信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="936d7-190">For information on how to create web packages, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="936d7-191">有关如何实际部署 web 包的指南，请参阅[部署 Web 包](deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="936d7-191">For guidance on how to actually deploy a web package, see [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="936d7-192">有关如何创建的分步演练*parameters.xml*文件，请参阅[如何： 安装到配置部署设置包时使用参数](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="936d7-192">For a step-by-step walkthrough on how to create a *parameters.xml* file, see [How to: Use Parameters to Configure Deployment Settings When a Package is Installed](https://msdn.microsoft.com/library/ff398068.aspx).</span></span>

<span data-ttu-id="936d7-193">有关 Web 部署中的参数化的更多常规信息，请参阅[Web 操作中的部署参数化](https://go.microsoft.com/?linkid=9805119)（博客文章）。</span><span class="sxs-lookup"><span data-stu-id="936d7-193">For more general information on parameterization in Web Deploy, see [Web Deploy Parameterization in Action](https://go.microsoft.com/?linkid=9805119) (blog post).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="936d7-194">[上一页](building-and-packaging-web-application-projects.md)
> [下一页](deploying-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="936d7-194">[Previous](building-and-packaging-web-application-projects.md)
[Next](deploying-web-packages.md)</span></span>
