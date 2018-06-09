---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: 拍摄 Web 应用程序脱机与 Web 部署 |Microsoft 文档
author: jrjlee
description: 本主题介绍如何采用脱机用于自动部署使用 Internet 信息服务 (IIS) Web 部署的持续时间的 web 应用程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: 511201dc5646340b21023430fa319417f2b53ae2
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "30883009"
---
<a name="taking-web-applications-offline-with-web-deploy"></a><span data-ttu-id="8a26a-103">拍摄 Web 应用程序脱机与 Web 部署</span><span class="sxs-lookup"><span data-stu-id="8a26a-103">Taking Web Applications Offline with Web Deploy</span></span>
====================
<span data-ttu-id="8a26a-104">通过[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8a26a-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="8a26a-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="8a26a-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="8a26a-106">本主题介绍如何采用脱机用于自动部署使用 Internet 信息服务 (IIS) Web 部署工具 （Web 部署） 的持续时间的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8a26a-106">This topic describes how to take a web application offline for the duration of an automated deployment using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="8a26a-107">浏览到 web 应用程序的用户将重定向到*应用\_offline.htm*文件之前部署已完成。</span><span class="sxs-lookup"><span data-stu-id="8a26a-107">Users who browse to the web application are redirected to an *App\_offline.htm* file until the deployment is complete.</span></span>


<span data-ttu-id="8a26a-108">本主题窗体的基于名为 Fabrikam，Inc.的虚构公司的企业部署要求的教程系列中的一部分本系列教程使用的示例解决方案&#x2014;[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有现实级别的复杂性，包括 ASP.NET MVC 3 应用程序，Windows 通信的 web 应用程序Foundation (WCF) 服务和数据库项目。</span><span class="sxs-lookup"><span data-stu-id="8a26a-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="8a26a-109">这些教程的核心的部署方法取决于中介绍的拆分项目文件方法[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)，两个项目文件中的生成过程控制通过&#x2014;另一个包含生成适用于每种目标环境和一个包含特定于环境的生成和部署设置的说明。</span><span class="sxs-lookup"><span data-stu-id="8a26a-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="8a26a-110">在生成期间，特定于环境的项目文件合并到环境无关的项目文件中以形成一组完整的生成说明。</span><span class="sxs-lookup"><span data-stu-id="8a26a-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="8a26a-111">任务概述</span><span class="sxs-lookup"><span data-stu-id="8a26a-111">Task Overview</span></span>

<span data-ttu-id="8a26a-112">在许多方案，你将想要使 web 应用程序脱机时对相关的组件，如数据库或 web 服务进行更改。</span><span class="sxs-lookup"><span data-stu-id="8a26a-112">In a lot of scenarios, you'll want to take a web application offline while you make changes to related components, like databases or web services.</span></span> <span data-ttu-id="8a26a-113">通常情况下，在 IIS 和 ASP.NET 中，你完成此操作通过将名为的文件*应用\_offline.htm*的 IIS 网站或 web 应用程序的根文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8a26a-113">Typically, in IIS and ASP.NET, you accomplish this by placing a file named *App\_offline.htm* in the root folder of the IIS website or web application.</span></span> <span data-ttu-id="8a26a-114">*应用\_offline.htm*文件是一个标准的 HTML 文件，通常包含一种简单消息，通知用户该站点是否由于维护而暂时不可用。</span><span class="sxs-lookup"><span data-stu-id="8a26a-114">The *App\_offline.htm* file is a standard HTML file and will usually contain a simple message advising the user that the site is temporarily unavailable due to maintenance.</span></span> <span data-ttu-id="8a26a-115">虽然*应用\_offline.htm*文件是否存在于网站的根文件夹，IIS 将自动任何将请求重定向到文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-115">While the *App\_offline.htm* file exists in the root folder of the website, IIS will automatically redirect any requests to the file.</span></span> <span data-ttu-id="8a26a-116">当你已进行更新时，也就删除*应用\_offline.htm*文件和网站恢复照常为请求提供服务。</span><span class="sxs-lookup"><span data-stu-id="8a26a-116">When you've finished making updates, you remove the *App\_offline.htm* file and the website resumes serving requests as usual.</span></span>

<span data-ttu-id="8a26a-117">当使用 Web 部署来执行自动进行的或单步执行到目标环境的部署时，你可能想要合并添加和删除*应用\_offline.htm*文件到你的部署过程。</span><span class="sxs-lookup"><span data-stu-id="8a26a-117">When you use Web Deploy to perform automated or single-step deployments to a target environment, you may want to incorporate adding and removing the *App\_offline.htm* file into your deployment process.</span></span> <span data-ttu-id="8a26a-118">若要执行此操作，你将需要完成这些高级任务：</span><span class="sxs-lookup"><span data-stu-id="8a26a-118">To do this, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="8a26a-119">在 Microsoft Build Engine (MSBuild) 项目文件中用于控制在部署过程，创建的 MSBuild 目标复制*应用\_offline.htm*到之前的任何部署任务在目标服务器的文件开始。</span><span class="sxs-lookup"><span data-stu-id="8a26a-119">In the Microsoft Build Engine (MSBuild) project file that you use to control the deployment process, create an MSBuild target that copies an *App\_offline.htm* file to the destination server before any deployment tasks begin.</span></span>
- <span data-ttu-id="8a26a-120">添加另一个中移除的 MSBuild 目标*应用\_offline.htm*从目标服务器时所有的部署任务都已完成的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-120">Add another MSBuild target that removes the *App\_offline.htm* file from the destination server when all deployment tasks are complete.</span></span>
- <span data-ttu-id="8a26a-121">在 web 应用程序项目中，创建 *。 wpp.targets*文件，它可确保*应用\_offline.htm* Web 部署调用时，将文件添加到部署包。</span><span class="sxs-lookup"><span data-stu-id="8a26a-121">In the web application project, create a *.wpp.targets* file that ensures that an *App\_offline.htm* file is added to the deployment package when Web Deploy is invoked.</span></span>

<span data-ttu-id="8a26a-122">本主题将演示如何执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="8a26a-122">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="8a26a-123">任务和本主题中的演练假定你已创建了包含至少一个 web 应用程序项目中，一个解决方案和使用自定义项目文件来控制部署过程中所述[中的 Web 部署企业](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="8a26a-123">The tasks and walkthroughs in this topic assume that you've already created a solution that contains at least one web application project, and that you use a custom project file to control the deployment process as described in [Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="8a26a-124">或者，可以使用[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案遵循主题中的示例。</span><span class="sxs-lookup"><span data-stu-id="8a26a-124">Alternatively, you can use the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution to follow the examples in the topic.</span></span>

## <a name="adding-an-appoffline-file-to-a-web-application-project"></a><span data-ttu-id="8a26a-125">添加应用\_到 Web 应用程序项目的脱机文件</span><span class="sxs-lookup"><span data-stu-id="8a26a-125">Adding an App\_Offline File to a Web Application Project</span></span>

<span data-ttu-id="8a26a-126">你需要完成的第一个任务是添加*应用\_脱机*文件到你的 web 应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="8a26a-126">The first task you need to complete is to add an *App\_offline* file to your web application project:</span></span>

- <span data-ttu-id="8a26a-127">若要防止文件干扰开发过程 （不希望永久脱机使应用程序），你应将其称为以外*应用\_offline.htm*。</span><span class="sxs-lookup"><span data-stu-id="8a26a-127">To prevent the file from interfering with the development process (you don't want your application to be permanently offline), you should call it something other than *App\_offline.htm*.</span></span> <span data-ttu-id="8a26a-128">例如，你无法将文件*应用\_脱机 template.htm*。</span><span class="sxs-lookup"><span data-stu-id="8a26a-128">For example, you could name the file *App\_offline-template.htm*.</span></span>
- <span data-ttu-id="8a26a-129">若要防止文件作为部署的是，你应将生成操作设置为**无**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-129">To prevent the file from being deployed as-is, you should set the build action to **None**.</span></span>

<span data-ttu-id="8a26a-130">**添加一个应用程序\_到 web 应用程序项目的脱机文件**</span><span class="sxs-lookup"><span data-stu-id="8a26a-130">**To add an App\_offline file to a web application project**</span></span>

1. <span data-ttu-id="8a26a-131">在 Visual Studio 2010 中打开你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a26a-131">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="8a26a-132">在**解决方案资源管理器**窗口中，右键单击你的 web 应用程序项目，指向**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-132">In the **Solution Explorer** window, right-click your web application project, point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="8a26a-133">在**添加新项**对话框中，选择**HTML 页**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-133">In the **Add New Item** dialog box, select **HTML Page**.</span></span>
4. <span data-ttu-id="8a26a-134">在**名称**框中，键入**应用\_脱机 template.htm**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-134">In the **Name** box, type **App\_offline-template.htm**, and then click **Add**.</span></span>

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. <span data-ttu-id="8a26a-135">添加一些简单的 HTML，以通知用户应用程序已不可用，，然后保存该文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-135">Add some simple HTML to inform users that the application is unavailable, and then save the file.</span></span> <span data-ttu-id="8a26a-136">不包括任何服务器端标记 (例如，任何带有前缀的标记"asp:")。</span><span class="sxs-lookup"><span data-stu-id="8a26a-136">Do not include any server-side tags (for example, any tags that are prefixed with "asp:").</span></span> 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. <span data-ttu-id="8a26a-137">在**解决方案资源管理器**窗口中，右键单击新的文件，并依次**属性**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-137">In the **Solution Explorer** window, right-click the new file, and then click **Properties**.</span></span>
7. <span data-ttu-id="8a26a-138">在**属性**窗口，请在**生成操作**行中，选中**无**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-138">In the **Properties** window, in the **Build Action** row, select **None**.</span></span>

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-appoffline-file"></a><span data-ttu-id="8a26a-139">部署和删除应用\_脱机文件</span><span class="sxs-lookup"><span data-stu-id="8a26a-139">Deploying and Deleting an App\_Offline File</span></span>

<span data-ttu-id="8a26a-140">下一步是修改你部署逻辑来将文件复制到目标服务器部署过程的开头和末尾删除它。</span><span class="sxs-lookup"><span data-stu-id="8a26a-140">The next step is to modify your deployment logic to copy the file to the destination server at the start of the deployment process and remove it at the end.</span></span>

> [!NOTE]
> <span data-ttu-id="8a26a-141">下一步过程假设你正在使用自定义 MSBuild 项目文件来控制你的部署过程中所述[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="8a26a-141">The next procedure assumes that you're using a custom MSBuild project file to control your deployment process, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="8a26a-142">如果你正在部署直接从 Visual Studio，你将需要使用不同的方法。</span><span class="sxs-lookup"><span data-stu-id="8a26a-142">If you're deploying direct from Visual Studio, you'll need to use a different approach.</span></span> <span data-ttu-id="8a26a-143">Sayed Ibrahim Hashimi 介绍中的一个此类方法[如何采用您 Web 应用程序脱机期间发布](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8a26a-143">Sayed Ibrahim Hashimi describes one such approach in [How to Take Your Web App Offline During Publishing](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx).</span></span>


<span data-ttu-id="8a26a-144">若要部署*应用\_脱机*文件到目标的 IIS 网站，你需要调用 MSDeploy.exe 使用[Web 部署**contentPath**提供程序](https://technet.microsoft.com/library/dd569034(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="8a26a-144">To deploy an *App\_offline* file to a destination IIS website, you need to invoke MSDeploy.exe using the [Web Deploy **contentPath** provider](https://technet.microsoft.com/library/dd569034(WS.10).aspx).</span></span> <span data-ttu-id="8a26a-145">**ContentPath**提供程序支持的物理目录路径和 IIS 网站或应用程序路径，使其同步 Visual Studio 项目文件夹和 IIS web 应用程序之间的文件的最佳选择。</span><span class="sxs-lookup"><span data-stu-id="8a26a-145">The **contentPath** provider supports both physical directory paths and IIS website or application paths, which makes it the ideal choice for synchronizing a file between a Visual Studio project folder and an IIS web application.</span></span> <span data-ttu-id="8a26a-146">若要部署该文件，MSDeploy 命令应类似如下：</span><span class="sxs-lookup"><span data-stu-id="8a26a-146">To deploy the file, your MSDeploy command should resemble this:</span></span>


[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]


<span data-ttu-id="8a26a-147">若要从目标站点，在部署过程结束时删除该文件，MSDeploy 命令应类似如下：</span><span class="sxs-lookup"><span data-stu-id="8a26a-147">To remove the file from the destination site at the end of the deployment process, your MSDeploy command should resemble this:</span></span>


[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]


<span data-ttu-id="8a26a-148">若要生成和部署过程的一部分自动运行这些命令，你需要将其集成到自定义 MSBuild 项目文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-148">To automate these commands as part of a build and deployment process, you need to integrate them into your custom MSBuild project file.</span></span> <span data-ttu-id="8a26a-149">下一步的过程描述如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8a26a-149">The next procedure describes how to do this.</span></span>

<span data-ttu-id="8a26a-150">**若要部署和删除应用\_脱机文件**</span><span class="sxs-lookup"><span data-stu-id="8a26a-150">**To deploy and delete an App\_offline file**</span></span>

1. <span data-ttu-id="8a26a-151">在 Visual Studio 2010 中，打开控制您的部署过程的 MSBuild 项目文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-151">In Visual Studio 2010, open the MSBuild project file that controls your deployment process.</span></span> <span data-ttu-id="8a26a-152">在[联系人管理器](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)示例解决方案中，这是*Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-152">In the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, this is the *Publish.proj* file.</span></span>
2. <span data-ttu-id="8a26a-153">根目录中**项目**元素，创建一个新**PropertyGroup**元素存储变量*应用\_脱机*部署：</span><span class="sxs-lookup"><span data-stu-id="8a26a-153">In the root **Project** element, create a new **PropertyGroup** element to store variables for the *App\_offline* deployment:</span></span>

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. <span data-ttu-id="8a26a-154">**SourceRoot**属性中其他位置定义*Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-154">The **SourceRoot** property is defined elsewhere in the *Publish.proj* file.</span></span> <span data-ttu-id="8a26a-155">它指示相对于当前路径的源内容的根文件夹的位置&#x2014;位置相对换而言之， *Publish.proj*文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-155">It indicates the location of the root folder for the source content relative to the current path&#x2014;in other words, relative to the location of the *Publish.proj* file.</span></span>
4. <span data-ttu-id="8a26a-156">**ContentPath**提供程序将不会接受相对文件路径，因此你需要获取到你的源代码文件的绝对路径，然后将其部署。</span><span class="sxs-lookup"><span data-stu-id="8a26a-156">The **contentPath** provider will not accept relative file paths, so you need to get an absolute path to your source file before you can deploy it.</span></span> <span data-ttu-id="8a26a-157">你可以使用[ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx)任务以执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8a26a-157">You can use the [ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx) task to do this.</span></span>
5. <span data-ttu-id="8a26a-158">添加新**目标**元素名为**GetAppOfflineAbsolutePath**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-158">Add a new **Target** element named **GetAppOfflineAbsolutePath**.</span></span> <span data-ttu-id="8a26a-159">在此目标使用**ConvertToAbsolutePath**任务来获取到的绝对路径*应用\_脱机模板*项目文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-159">Within this target, use the **ConvertToAbsolutePath** task to get an absolute path to the *App\_offline-template* file in your project folder.</span></span>

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. <span data-ttu-id="8a26a-160">此目标中，采用的相对路径*应用\_脱机模板*项目文件夹中的文件并将其保存到新的属性为绝对文件路径。</span><span class="sxs-lookup"><span data-stu-id="8a26a-160">This target takes the relative path to the *App\_offline-template* file in your project folder and saves it to a new property as an absolute file path.</span></span> <span data-ttu-id="8a26a-161">**BeforeTargets**属性指定你想要执行之前此目标**DeployAppOffline**目标，你将在下一步中创建。</span><span class="sxs-lookup"><span data-stu-id="8a26a-161">The **BeforeTargets** attribute specifies that you want this target to execute before the **DeployAppOffline** target, which you'll create in the next step.</span></span>
7. <span data-ttu-id="8a26a-162">添加名为的新目标**DeployAppOffline**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-162">Add a new target named **DeployAppOffline**.</span></span> <span data-ttu-id="8a26a-163">在此目标内调用 MSDeploy.exe 命令以部署你*应用\_脱机*到目标 web 服务器的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-163">Within this target, invoke the MSDeploy.exe command that deploys your *App\_offline* file to the destination web server.</span></span>

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. <span data-ttu-id="8a26a-164">在此示例中， **ContactManagerIisPath**属性在项目文件中其他位置定义。</span><span class="sxs-lookup"><span data-stu-id="8a26a-164">In this example, the **ContactManagerIisPath** property is defined elsewhere in the project file.</span></span> <span data-ttu-id="8a26a-165">这是只需一个 IIS 应用程序路径的形式 *[IIS 网站名称] / [应用程序名称]*。</span><span class="sxs-lookup"><span data-stu-id="8a26a-165">This is simply an IIS application path, in the form *[IIS Website Name]/[Application Name]*.</span></span> <span data-ttu-id="8a26a-166">目标中包括条件使用户能够切换*应用\_脱机*部署打开或关闭通过更改属性值或提供命令行参数。</span><span class="sxs-lookup"><span data-stu-id="8a26a-166">Including a condition in the target enables users to switch the *App\_offline* deployment on or off by changing a property value or providing a command-line parameter.</span></span>
9. <span data-ttu-id="8a26a-167">添加名为的新目标**DeleteAppOffline**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-167">Add a new target named **DeleteAppOffline**.</span></span> <span data-ttu-id="8a26a-168">在此目标内调用 MSDeploy.exe 命令删除你*应用\_脱机*从目标 web 服务器的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-168">Within this target, invoke the MSDeploy.exe command that removes your *App\_offline* file from the destination web server.</span></span>

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. <span data-ttu-id="8a26a-169">最后一项任务是在你的项目文件的执行过程中调用这些新的目标在适当的位置。</span><span class="sxs-lookup"><span data-stu-id="8a26a-169">The final task is to invoke these new targets at appropriate points during the execution of your project file.</span></span> <span data-ttu-id="8a26a-170">可以通过多种方式来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8a26a-170">You can do this in various ways.</span></span> <span data-ttu-id="8a26a-171">例如，在*Publish.proj*文件， **FullPublishDependsOn**属性指定必须执行的目标的列表在排序时**FullPublish**默认调用目标。</span><span class="sxs-lookup"><span data-stu-id="8a26a-171">For example, in the *Publish.proj* file, the **FullPublishDependsOn** property specifies a list of targets that must be executed in order when the **FullPublish** default target is invoked.</span></span>
11. <span data-ttu-id="8a26a-172">修改 MSBuild 项目文件调用**DeployAppOffline**和**DeleteAppOffline**在发布过程中适当点的目标。</span><span class="sxs-lookup"><span data-stu-id="8a26a-172">Modify your MSBuild project file to invoke the **DeployAppOffline** and **DeleteAppOffline** targets at appropriate points in the publishing process.</span></span>

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

<span data-ttu-id="8a26a-173">当你运行自定义 MSBuild 项目文件，*应用\_脱机*文件将成功生成后立即部署到服务器。</span><span class="sxs-lookup"><span data-stu-id="8a26a-173">When you run your custom MSBuild project file, the *App\_offline* file will be deployed to the server immediately after a successful build.</span></span> <span data-ttu-id="8a26a-174">它将然后从服务器删除后部署的所有任务都都已完成。</span><span class="sxs-lookup"><span data-stu-id="8a26a-174">It will then be deleted from the server once all the deployment tasks are complete.</span></span>

## <a name="adding-an-appoffline-file-to-deployment-packages"></a><span data-ttu-id="8a26a-175">添加应用\_到部署包的脱机文件</span><span class="sxs-lookup"><span data-stu-id="8a26a-175">Adding an App\_Offline File to Deployment Packages</span></span>

<span data-ttu-id="8a26a-176">根据你的部署的配置方式，任何现有内容在目标 IIS web 应用程序&#x2014;如*应用\_offline.htm*文件&#x2014;部署 web 时可能会自动删除到目标的包。</span><span class="sxs-lookup"><span data-stu-id="8a26a-176">Depending on how you configure your deployment, any existing content at the destination IIS web application&#x2014;like the *App\_offline.htm* file&#x2014;may be deleted automatically when you deploy a web package to the destination.</span></span> <span data-ttu-id="8a26a-177">若要确保*应用\_offline.htm*文件仍保持就地部署的持续时间内，你需要将该文件中的 web 部署包本身此外包括到部署直接开头的文件部署过程中。</span><span class="sxs-lookup"><span data-stu-id="8a26a-177">To ensure that the *App\_offline.htm* file remains in place for the duration of the deployment, you need to include the file within the web deployment package itself in addition to deploying the file directly at the start of the deployment process.</span></span>

- <span data-ttu-id="8a26a-178">如果你已按照本主题中前面的任务，你将已添加*应用\_offline.htm*到你 web 应用程序项目的其他文件名的文件 (我们使用*应用\_脱机 template.htm*) 并且你将安装的生成操作**无**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-178">If you've followed the previous tasks in this topic, you'll have added the *App\_offline.htm* file to your web application project under a different filename (we used *App\_offline-template.htm*) and you'll have set the build action to **None**.</span></span> <span data-ttu-id="8a26a-179">不需要以防止干扰开发和调试中的文件进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="8a26a-179">These changes are necessary to prevent the file from interfering with development and debugging.</span></span> <span data-ttu-id="8a26a-180">因此，你需要自定义以确保在打包过程*应用\_offline.htm* web 部署包中包含了文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-180">As a result, you need to customize the packaging process to ensure that the *App\_offline.htm* file is included in the web deployment package.</span></span>

<span data-ttu-id="8a26a-181">Web 发布管道 (WPP) 使用名为的项列表**FilesForPackagingFromProject**生成的文件应包含在 web 部署包的列表。</span><span class="sxs-lookup"><span data-stu-id="8a26a-181">The Web Publishing Pipeline (WPP) uses an item list named **FilesForPackagingFromProject** to build a list of files that should be included in the web deployment package.</span></span> <span data-ttu-id="8a26a-182">你可以将您自己的项添加到此列表自定义 web 包的内容。</span><span class="sxs-lookup"><span data-stu-id="8a26a-182">You can customize the contents of your web packages by adding your own items to this list.</span></span> <span data-ttu-id="8a26a-183">若要执行此操作，你需要完成以下高级步骤：</span><span class="sxs-lookup"><span data-stu-id="8a26a-183">To do this, you need to complete these high-level steps:</span></span>

1. <span data-ttu-id="8a26a-184">创建一个名为的自定义项目文件 *[项目名称].wpp.targets*项目文件所在的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8a26a-184">Create a custom project file named *[project name].wpp.targets* in the same folder as your project file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8a26a-185">*。 Wpp.targets*文件需要在你的 web 应用程序项目文件所在的文件夹中转&#x2014;例如*ContactManager.Mvc.csproj*&#x2014;而不是任何自定义所在的文件夹中你使用来控制生成和部署过程的项目文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-185">The *.wpp.targets* file needs to go in the same folder as your web application project file&#x2014;for example, *ContactManager.Mvc.csproj*&#x2014;rather than in the same folder as any custom project files you use to control the build and deployment process.</span></span>
2. <span data-ttu-id="8a26a-186">在 *。 wpp.targets*文件中，创建新的 MSBuild 目标执行*之前* **CopyAllFilesToSingleFolderForPackage**目标。</span><span class="sxs-lookup"><span data-stu-id="8a26a-186">In the *.wpp.targets* file, create a new MSBuild target that executes *before* the **CopyAllFilesToSingleFolderForPackage** target.</span></span> <span data-ttu-id="8a26a-187">这是生成要在包中包括的事项列表的 WPP 目标。</span><span class="sxs-lookup"><span data-stu-id="8a26a-187">This is the WPP target that builds a list of things to include in the package.</span></span>
3. <span data-ttu-id="8a26a-188">在新的目标中，创建**ItemGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="8a26a-188">In the new target, create an **ItemGroup** element.</span></span>
4. <span data-ttu-id="8a26a-189">在**ItemGroup**元素中，添加**FilesForPackagingFromProject**项并指定*应用\_offline.htm*文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-189">In the **ItemGroup** element, add a **FilesForPackagingFromProject** item and specify the *App\_offline.htm* file.</span></span>

<span data-ttu-id="8a26a-190">*。 Wpp.targets*文件应类似如下：</span><span class="sxs-lookup"><span data-stu-id="8a26a-190">The *.wpp.targets* file should resemble this:</span></span>


[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]


<span data-ttu-id="8a26a-191">这些是在此示例中注意的要点：</span><span class="sxs-lookup"><span data-stu-id="8a26a-191">These are the key points of note in this example:</span></span>

- <span data-ttu-id="8a26a-192">**BeforeTargets**属性将插入它应立即之前执行通过指定 WPP 到此目标**CopyAllFilesToSingleFolderForPackage**目标。</span><span class="sxs-lookup"><span data-stu-id="8a26a-192">The **BeforeTargets** attribute inserts this target into the WPP by specifying that it should be executed immediately before the **CopyAllFilesToSingleFolderForPackage** target.</span></span>
- <span data-ttu-id="8a26a-193">**FilesForPackagingFromProject**项使用**DestinationRelativePath**要重命名的文件的元数据值*应用\_脱机 template.htm*到*应用\_offline.htm*被添加到列表。</span><span class="sxs-lookup"><span data-stu-id="8a26a-193">The **FilesForPackagingFromProject** item uses the **DestinationRelativePath** metadata value to rename the file from *App\_offline-template.htm* to *App\_offline.htm* as it's added to the list.</span></span>

<span data-ttu-id="8a26a-194">下一个过程演示如何添加此 *。 wpp.targets*到 web 应用程序项目的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-194">The next procedure shows you how to add this *.wpp.targets* file to a web application project.</span></span>

<span data-ttu-id="8a26a-195">**若要添加。 web 部署包的 wpp.targets 文件**</span><span class="sxs-lookup"><span data-stu-id="8a26a-195">**To add a .wpp.targets file to a web deployment package**</span></span>

1. <span data-ttu-id="8a26a-196">在 Visual Studio 2010 中打开你的解决方案。</span><span class="sxs-lookup"><span data-stu-id="8a26a-196">Open your solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="8a26a-197">在**解决方案资源管理器**窗口中，右键单击你的 web 应用程序项目节点 (例如， **ContactManager.Mvc**)，指向**添加**，然后单击**新项**。</span><span class="sxs-lookup"><span data-stu-id="8a26a-197">In the **Solution Explorer** window, right-click your web application project node (for example, **ContactManager.Mvc**), point to **Add**, and then click **New Item**.</span></span>
3. <span data-ttu-id="8a26a-198">在**添加新项**对话框中，选择**XML 文件**模板。</span><span class="sxs-lookup"><span data-stu-id="8a26a-198">In the **Add New Item** dialog box, select the **XML File** template.</span></span>
4. <span data-ttu-id="8a26a-199">在 **名称** 框中，键入 *[项目名称]***.wpp.targets** (例如， **ContactManager.Mvc.wpp.targets**)，然后单击 **添加**.</span><span class="sxs-lookup"><span data-stu-id="8a26a-199">In the **Name** box, type *[project name]***.wpp.targets** (for example, **ContactManager.Mvc.wpp.targets**), and then click **Add**.</span></span>

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="8a26a-200">如果你将新项添加到项目的根节点时，会在项目文件所在的文件夹中创建文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-200">If you add a new item to the root node of a project, the file is created in the same folder as the project file.</span></span> <span data-ttu-id="8a26a-201">可以通过在 Windows 资源管理器中打开文件夹对此进行验证。</span><span class="sxs-lookup"><span data-stu-id="8a26a-201">You can verify this by opening the folder in Windows Explorer.</span></span>
5. <span data-ttu-id="8a26a-202">在文件中，添加前面所述的 MSBuild 标记。</span><span class="sxs-lookup"><span data-stu-id="8a26a-202">In the file, add the MSBuild markup described previously.</span></span>

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. <span data-ttu-id="8a26a-203">保存并关闭 *[项目名称].wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-203">Save and close the *[project name].wpp.targets* file.</span></span>

<span data-ttu-id="8a26a-204">下一次你生成和包你的 web 应用程序项目，将自动检测 WPP *。 wpp.targets*文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-204">The next time you build and package your web application project, the WPP will automatically detect the *.wpp.targets* file.</span></span> <span data-ttu-id="8a26a-205">*应用\_脱机 template.htm*将作为生成的 web 部署包中包含文件*应用\_offline.htm*。</span><span class="sxs-lookup"><span data-stu-id="8a26a-205">The *App\_offline-template.htm* file will be included in the resulting web deployment package as *App\_offline.htm*.</span></span>

> [!NOTE]
> <span data-ttu-id="8a26a-206">如果你的部署失败，*应用\_offline.htm*文件将保留在原位和你的应用程序将保持脱机状态。</span><span class="sxs-lookup"><span data-stu-id="8a26a-206">If your deployment fails, the *App\_offline.htm* file will remain in place and your application will remain offline.</span></span> <span data-ttu-id="8a26a-207">这通常是所需的行为。</span><span class="sxs-lookup"><span data-stu-id="8a26a-207">This is typically the desired behavior.</span></span> <span data-ttu-id="8a26a-208">若要使你的应用程序重新联机，你可以删除*应用\_offline.htm*从你的 web 服务器的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-208">To bring your application back online, you can delete the *App\_offline.htm* file from your web server.</span></span> <span data-ttu-id="8a26a-209">或者，如果更正任何错误，运行成功的部署，*应用\_offline.htm*将删除文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-209">Alternatively, if you correct any errors and run a successful deployment, the *App\_offline.htm* file will be removed.</span></span>


## <a name="conclusion"></a><span data-ttu-id="8a26a-210">结束语</span><span class="sxs-lookup"><span data-stu-id="8a26a-210">Conclusion</span></span>

<span data-ttu-id="8a26a-211">本主题描述如何采用通过发布的 web 应用程序脱机的持续时间的部署，*应用\_offline.htm*到目标服务器在部署过程中启动文件并将其在删除结束日期。</span><span class="sxs-lookup"><span data-stu-id="8a26a-211">This topic described how to take a web application offline for the duration of a deployment, by publishing an *App\_offline.htm* file to the destination server at the start of the deployment process and removing it at the end.</span></span> <span data-ttu-id="8a26a-212">它还介绍了如何包括*应用\_offline.htm* web 部署包中的文件。</span><span class="sxs-lookup"><span data-stu-id="8a26a-212">It also covered how to include an *App\_offline.htm* file in a web deployment package.</span></span>

## <a name="further-reading"></a><span data-ttu-id="8a26a-213">其他阅读材料</span><span class="sxs-lookup"><span data-stu-id="8a26a-213">Further Reading</span></span>

<span data-ttu-id="8a26a-214">打包和部署过程的详细信息，请参阅[生成和打包 Web 应用程序项目](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)， [Web 包部署的配置参数](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)，和[部署 Web 包](../web-deployment-in-the-enterprise/deploying-web-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="8a26a-214">For more information on the packaging and deployment process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Configuring Parameters for Web Package Deployment](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md), and [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md).</span></span>

<span data-ttu-id="8a26a-215">如果发布 web 应用程序直接从 Visual Studio 中，而不使用这些教程中所述的自定义 MSBuild 项目文件方法，你将需要使用稍有不同的方法来执行你的应用程序脱机在发布过程过程。</span><span class="sxs-lookup"><span data-stu-id="8a26a-215">If you publish your web applications directly from Visual Studio, rather than using the custom MSBuild project file approach described in these tutorials, you'll need to use a slightly different approach to take your application offline during the publishing process.</span></span> <span data-ttu-id="8a26a-216">有关详细信息，请参阅[如何在发布过程中执行 web 应用程序脱机](https://go.microsoft.com/?linkid=9805135)（博客文章）。</span><span class="sxs-lookup"><span data-stu-id="8a26a-216">For more information, see [How to take your web app offline during publishing](https://go.microsoft.com/?linkid=9805135) (blog post).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8a26a-217">[上一页](excluding-files-and-folders-from-deployment.md)
> [下一页](running-windows-powershell-scripts-from-msbuild-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="8a26a-217">[Previous](excluding-files-and-folders-from-deployment.md)
[Next](running-windows-powershell-scripts-from-msbuild-project-files.md)</span></span>
