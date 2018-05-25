---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: 从部署中排除文件和文件夹 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何时，你可以排除文件和文件夹从 web 部署包生成并打包 web 应用程序项目。
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: c435448bf057bbef9127d66ffda24a07729f2322
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="excluding-files-and-folders-from-deployment"></a><span data-ttu-id="20a9e-103">从部署中排除文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="20a9e-103">Excluding Files and Folders from Deployment</span></span>
====================
<span data-ttu-id="20a9e-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="20a9e-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="20a9e-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="20a9e-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="20a9e-106">本主题介绍如何时，你可以排除文件和文件夹从 web 部署包生成并打包 web 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="20a9e-106">This topic describes how you can exclude files and folders from a web deployment package when you build and package a web application project.</span></span>


<span data-ttu-id="20a9e-107">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案&#x2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="20a9e-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="20a9e-108">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中的生成过程控制通过&#x2014;另一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="20a9e-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="20a9e-109">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="20a9e-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="overview"></a><span data-ttu-id="20a9e-110">概述</span><span class="sxs-lookup"><span data-stu-id="20a9e-110">Overview</span></span>

<span data-ttu-id="20a9e-111">生成 Visual Studio 2010 中的 web 应用程序项目时，可以使用 Web 发布管道 (WPP) 通过打包编译的 web 应用程序可部署 web 包来扩展此生成过程。</span><span class="sxs-lookup"><span data-stu-id="20a9e-111">When you build a web application project in Visual Studio 2010, the Web Publishing Pipeline (WPP) lets you extend this build process by packaging your compiled web application into a deployable web package.</span></span> <span data-ttu-id="20a9e-112">然后，你可以使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 将此 web 包部署到远程 IIS web 服务器，或导入 web 包手动通过 IIS 管理器中。</span><span class="sxs-lookup"><span data-stu-id="20a9e-112">You can then use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy this web package to a remote IIS web server, or import the web package manually through IIS Manager.</span></span> <span data-ttu-id="20a9e-113">中介绍了此打包过程[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="20a9e-113">This packaging process is explained in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="20a9e-114">如何执行控制你的 web 中包含的内容获取包？</span><span class="sxs-lookup"><span data-stu-id="20a9e-114">So how do you control what gets included in your web package?</span></span> <span data-ttu-id="20a9e-115">在 Visual Studio 中，通过基础的项目文件中，项目设置为大量方案提供控制不足以满足。</span><span class="sxs-lookup"><span data-stu-id="20a9e-115">The project settings in Visual Studio, through the underlying project file, provide sufficient control for a lot of scenarios.</span></span> <span data-ttu-id="20a9e-116">但是，在某些情况下你可能想要定制到特定目标环境你 web 包的内容。</span><span class="sxs-lookup"><span data-stu-id="20a9e-116">However, in some cases you may want to tailor the contents of your web package to specific destination environments.</span></span> <span data-ttu-id="20a9e-117">例如，你可能想要包括日志文件的文件夹，当你应用程序部署到测试环境，但是当你将应用部署到过渡或生产环境中排除的文件夹。</span><span class="sxs-lookup"><span data-stu-id="20a9e-117">For example, you might want to include a folder for log files when you deploy your application to a test environment but exclude the folder when you deploy the application to a staging or production environment.</span></span> <span data-ttu-id="20a9e-118">本主题将演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="20a9e-118">This topic will show you how to do this.</span></span>

## <a name="what-gets-included-by-default"></a><span data-ttu-id="20a9e-119">默认情况下获取获得的内容</span><span class="sxs-lookup"><span data-stu-id="20a9e-119">What Gets Included by Default?</span></span>

<span data-ttu-id="20a9e-120">当你在 Visual Studio 中，配置你的 web 应用程序项目属性**项部署**列表上**打包/发布 Web**页允许你指定想要包括在你的 web 部署包。</span><span class="sxs-lookup"><span data-stu-id="20a9e-120">When you configure your web application project properties in Visual Studio, the **Items to deploy** list on the **Package/Publish Web** page lets you specify what you want to include in your web deployment package.</span></span> <span data-ttu-id="20a9e-121">默认情况下，这设置为**仅运行此应用程序所需的文件**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-121">By default, this is set to **Only files needed to run this application**.</span></span>

![](excluding-files-and-folders-from-deployment/_static/image1.png)

<span data-ttu-id="20a9e-122">当你选择**仅运行此应用程序所需的文件**，WPP 将尝试确定应将哪些文件添加到 web 包。</span><span class="sxs-lookup"><span data-stu-id="20a9e-122">When you choose **Only files needed to run this application**, the WPP will try to determine which files should be added to the web package.</span></span> <span data-ttu-id="20a9e-123">这包括：</span><span class="sxs-lookup"><span data-stu-id="20a9e-123">This includes:</span></span>

- <span data-ttu-id="20a9e-124">所有生成的项目都输出。</span><span class="sxs-lookup"><span data-stu-id="20a9e-124">All the build outputs for the project.</span></span>
- <span data-ttu-id="20a9e-125">生成操作的任何文件标记**内容**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-125">Any files marked with a build action of **Content**.</span></span>

> [!NOTE]
> <span data-ttu-id="20a9e-126">确定要包括的文件的逻辑包含在此文件中：</span><span class="sxs-lookup"><span data-stu-id="20a9e-126">The logic that determines which files to include is contained in this file:</span></span>   
> <span data-ttu-id="20a9e-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span><span class="sxs-lookup"><span data-stu-id="20a9e-127">*%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft.Web.Publishing.OnlyFilesToRunTheApp.targets*</span></span>


## <a name="excluding-specific-files-and-folders"></a><span data-ttu-id="20a9e-128">排除特定文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="20a9e-128">Excluding Specific Files and Folders</span></span>

<span data-ttu-id="20a9e-129">在某些情况下，你将需要对其部署文件和文件夹的更细化的控制。</span><span class="sxs-lookup"><span data-stu-id="20a9e-129">In some cases, you'll want more fine-grained control over which files and folders are deployed.</span></span> <span data-ttu-id="20a9e-130">如果你知道你想要提前排除的文件时间，并且排除适用于所有目标环境，你可以只需设置**生成操作**每个文件**无**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-130">If you know which files you want to exclude ahead of time, and the exclusion applies to all destination environments, you can simply set the **Build Action** of each file to **None**.</span></span>

<span data-ttu-id="20a9e-131">**若要从部署中排除特定文件**</span><span class="sxs-lookup"><span data-stu-id="20a9e-131">**To exclude specific files from deployment**</span></span>

1. <span data-ttu-id="20a9e-132">在**解决方案资源管理器**窗口中，右键单击文件，并依次**属性**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-132">In the **Solution Explorer** window, right-click the file, and then click **Properties**.</span></span>
2. <span data-ttu-id="20a9e-133">在**属性**窗口，请在**生成操作**行中，选中**无**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-133">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

<span data-ttu-id="20a9e-134">但是，这种方法并不总是方便。</span><span class="sxs-lookup"><span data-stu-id="20a9e-134">However, this approach is not always convenient.</span></span> <span data-ttu-id="20a9e-135">例如，你可能想要不同的文件和文件夹是根据你的目标环境，和从 Visual Studio 外部包含。</span><span class="sxs-lookup"><span data-stu-id="20a9e-135">For example, you may want to vary which files and folders are included according to your destination environment, and from outside Visual Studio.</span></span> <span data-ttu-id="20a9e-136">例如，在联系人管理器示例解决方案中，一下 ContactManager.Mvc 项目的内容：</span><span class="sxs-lookup"><span data-stu-id="20a9e-136">For example, in the Contact Manager sample solution, take a look at the contents of the ContactManager.Mvc project:</span></span>

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- <span data-ttu-id="20a9e-137">内部文件夹包含一些开发人员用来创建、 删除，并填充出于开发目的的本地数据库的 SQL 脚本。</span><span class="sxs-lookup"><span data-stu-id="20a9e-137">The Internal folder contains some SQL scripts that the developer uses to create, drop, and populate local databases for development purposes.</span></span> <span data-ttu-id="20a9e-138">在此文件夹中为 nothing 应部署到过渡或生产环境。</span><span class="sxs-lookup"><span data-stu-id="20a9e-138">Nothing in this folder should be deployed to a staging or production environment.</span></span>
- <span data-ttu-id="20a9e-139">脚本文件夹包含多个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-139">The Scripts folder contains several JavaScript files.</span></span> <span data-ttu-id="20a9e-140">许多这些文件是只是为了支持调试，或者提供 Visual Studio 中的 IntelliSense，包含。</span><span class="sxs-lookup"><span data-stu-id="20a9e-140">A lot of these files are included purely to support debugging or provide IntelliSense in Visual Studio.</span></span> <span data-ttu-id="20a9e-141">其中某些文件不应部署到过渡环境或生产环境。</span><span class="sxs-lookup"><span data-stu-id="20a9e-141">Some of these files should not be deployed to staging or production environments.</span></span> <span data-ttu-id="20a9e-142">但是，你可能想要将它们部署到开发人员测试环境有助于进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="20a9e-142">However, you may want to deploy them to a developer test environment to facilitate troubleshooting.</span></span>

<span data-ttu-id="20a9e-143">尽管你可能会将项目文件中排除特定文件和文件夹操作，但是没有更简单的方法。</span><span class="sxs-lookup"><span data-stu-id="20a9e-143">Although you could manipulate your project files to exclude specific files and folders, there is an easier way.</span></span> <span data-ttu-id="20a9e-144">WPP 包括一种机制来通过构建名为的项列表中排除文件和文件夹**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-144">The WPP includes a mechanism to exclude files and folders by building item lists named **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles**.</span></span> <span data-ttu-id="20a9e-145">你可以通过将你自己的项添加到这些列表来扩展此机制。</span><span class="sxs-lookup"><span data-stu-id="20a9e-145">You can extend this mechanism by adding your own items to these lists.</span></span> <span data-ttu-id="20a9e-146">若要执行此操作，你需要完成以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="20a9e-146">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="20a9e-147">创建一个名为的自定义项目文件 *[项目名称].wpp.targets*项目文件所在的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="20a9e-147">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="20a9e-148">*。 Wpp.targets*文件需要在你的 web 应用程序项目文件所在的文件夹中转&#x2014;例如*ContactManager.Mvc.csproj*&#x2014;而不是任何自定义所在的文件夹中你使用来控制生成和部署过程的项目文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-148">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="20a9e-149">在 *。 wpp.targets*文件中，添加**ItemGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="20a9e-149">In the *.wpp.targets* file, add an **ItemGroup** element.</span></span>
3. <span data-ttu-id="20a9e-150">在**ItemGroup**元素中，添加**ExcludeFromPackageFolders**和**ExcludeFromPackageFiles**要排除特定文件和文件夹所需项。</span><span class="sxs-lookup"><span data-stu-id="20a9e-150">In the **ItemGroup** element, add **ExcludeFromPackageFolders** and **ExcludeFromPackageFiles** items to exclude specific files and folders as required.</span></span>

<span data-ttu-id="20a9e-151">这是此基本结构 *。 wpp.targets*文件：</span><span class="sxs-lookup"><span data-stu-id="20a9e-151">This is the basic structure of this *.wpp.targets* file:</span></span>


[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]


<span data-ttu-id="20a9e-152">请注意，每个项包括名为的项元数据元素**FromTarget**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-152">Note that each item includes an item metadata element named **FromTarget**.</span></span> <span data-ttu-id="20a9e-153">这是一个可选值，不会影响生成过程中;它只是用于指示特定文件或文件夹已省略为什么如果有人查看生成日志。</span><span class="sxs-lookup"><span data-stu-id="20a9e-153">This is an optional value that doesn't affect the build process; it simply serves to indicate why particular files or folders were omitted if someone reviews the build logs.</span></span>

## <a name="excluding-files-and-folders-from-a-web-package"></a><span data-ttu-id="20a9e-154">从 Web 包中排除文件和文件夹</span><span class="sxs-lookup"><span data-stu-id="20a9e-154">Excluding Files and Folders from a Web Package</span></span>

<span data-ttu-id="20a9e-155">下一个过程演示如何将添加 *。 wpp.targets* web 应用程序项目以及如何使用文件来生成你的项目时从 web 包排除特定文件和文件夹的文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-155">The next procedure shows you how to add a *.wpp.targets* file to a web application project and how to use the file to exclude specific files and folders from the web package when you build your project.</span></span>

<span data-ttu-id="20a9e-156">**若要从 web 部署包中排除文件和文件夹**</span><span class="sxs-lookup"><span data-stu-id="20a9e-156">**To exclude files and folders from a web deployment package**</span></span>

1. <span data-ttu-id="20a9e-157">在 Visual Studio 2010 中打开你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="20a9e-157">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="20a9e-158">在**解决方案资源管理器**窗口中，右键单击你的 web 应用程序项目节点 (例如， **ContactManager.Mvc**)，指向**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="20a9e-158">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="20a9e-159">在**添加新项**对话框中，选择**XML 文件**模板。</span><span class="sxs-lookup"><span data-stu-id="20a9e-159">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="20a9e-160">在 **名称** 框中，键入 *[项目名称]***.wpp.targets** (例如， **ContactManager.Mvc.wpp.targets**)，然后单击 **添加**.</span><span class="sxs-lookup"><span data-stu-id="20a9e-160">In the **Name** box, type *[project name]***.wpp.targets** (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="20a9e-161">如果你将新项添加到项目的根节点时，会在项目文件所在的文件夹中创建文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-161">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="20a9e-162">可以通过在 Windows 资源管理器中打开文件夹对此进行验证。</span><span class="sxs-lookup"><span data-stu-id="20a9e-162">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="20a9e-163">在文件中，添加**项目**元素和**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="20a9e-163">In the file, add a **Project** element and an **ItemGroup** element:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. <span data-ttu-id="20a9e-164">如果你想要从 web 包中排除文件夹，将添加**ExcludeFromPackageFolders**元素**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="20a9e-164">If you want to exclude folders from the web package, add an **ExcludeFromPackageFolders** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="20a9e-165">在**包括**特性，提供你想要排除的文件夹中的分号分隔的列表。</span><span class="sxs-lookup"><span data-stu-id="20a9e-165">In the **Include** attribute, provide a semicolon-separated list of the folders you want to exclude.</span></span>
   2. <span data-ttu-id="20a9e-166">在**FromTarget**元数据元素提供一个有意义的值以指示原因文件夹中排除，如名 *。 wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-166">In the **FromTarget** metadata element, provide a meaningful value to indicate why the folders are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. <span data-ttu-id="20a9e-167">如果你想要从 web 包中排除文件，添加**ExcludeFromPackageFiles**元素**ItemGroup**元素：</span><span class="sxs-lookup"><span data-stu-id="20a9e-167">If you want to exclude files from the web package, add an **ExcludeFromPackageFiles** element to the **ItemGroup** element:</span></span>

   1. <span data-ttu-id="20a9e-168">在**包括**特性，提供你想要排除的文件之间用分号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="20a9e-168">In the **Include** attribute, provide a semicolon-separated list of the files you want to exclude.</span></span>
   2. <span data-ttu-id="20a9e-169">在**FromTarget**元数据元素提供一个有意义的值以指示原因文件中排除，如名 *。 wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-169">In the **FromTarget** metadata element, provide a meaningful value to indicate why the files are being excluded, like the name of the *.wpp.targets* file.</span></span>

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. <span data-ttu-id="20a9e-170">*[项目名称].wpp.targets*文件现在应类似如下：</span><span class="sxs-lookup"><span data-stu-id="20a9e-170">The *[project name].wpp.targets* file should now resemble this:</span></span>

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. <span data-ttu-id="20a9e-171">保存并关闭 *[项目名称].wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-171">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="20a9e-172">下一次你生成和包你的 web 应用程序项目，将自动检测 WPP *。 wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-172">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="20a9e-173">不将 web 包中包括任何文件和你指定的文件夹。</span><span class="sxs-lookup"><span data-stu-id="20a9e-173">Any files and folders you specified will not be included in the web package.</span></span>

## <a name="conclusion"></a><span data-ttu-id="20a9e-174">结束语</span><span class="sxs-lookup"><span data-stu-id="20a9e-174">Conclusion</span></span>

<span data-ttu-id="20a9e-175">本主题描述如何创建自定义生成 web 包时, 排除特定文件和文件夹 *。 wpp.targets*与你的 web 应用程序项目文件相同的文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="20a9e-175">This topic described how to exclude specific files and folders when you build a web package, by creating a custom *.wpp.targets* file in the same folder as your web application project file.</span></span>

## <a name="further-reading"></a><span data-ttu-id="20a9e-176">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="20a9e-176">Further Reading</span></span>

<span data-ttu-id="20a9e-177">使用自定义 Microsoft Build Engine (MSBuild) 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解该生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="20a9e-177">For more information on using custom Microsoft Build Engine (MSBuild) project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="20a9e-178">打包和部署过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)， [Web 包部署的配置参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)，和[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="20a9e-178">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="20a9e-179">[上一页](deploying-membership-databases-to-enterprise-environments.md)
> [下一页](taking-web-applications-offline-with-web-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="20a9e-179">[Previous](deploying-membership-databases-to-enterprise-environments.md)
[Next](taking-web-applications-offline-with-web-deploy.md)</span></span>
