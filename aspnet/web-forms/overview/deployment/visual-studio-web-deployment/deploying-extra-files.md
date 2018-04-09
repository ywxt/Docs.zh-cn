---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
title: 使用 Visual Studio 的 ASP.NET Web 部署： 部署额外文件 |Microsoft 文档
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/23/2015
ms.topic: article
ms.assetid: 1cd91055-84bc-42c6-9d80-646f41429d4d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files
msc.type: authoredcontent
ms.openlocfilehash: 5cefcedde7715844a7d7a9db1455193564ef9805
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="aspnet-web-deployment-using-visual-studio-deploying-extra-files"></a><span data-ttu-id="a785c-103">使用 Visual Studio 的 ASP.NET Web 部署： 部署额外文件</span><span class="sxs-lookup"><span data-stu-id="a785c-103">ASP.NET Web Deployment using Visual Studio: Deploying Extra Files</span></span>
====================
<span data-ttu-id="a785c-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a785c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="a785c-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="a785c-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="a785c-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="a785c-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="a785c-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a785c-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="a785c-108">概述</span><span class="sxs-lookup"><span data-stu-id="a785c-108">Overview</span></span>

<span data-ttu-id="a785c-109">本教程演示如何扩展 Visual Studio web 发布管道在部署过程中执行其他任务。</span><span class="sxs-lookup"><span data-stu-id="a785c-109">This tutorial shows how to extend the Visual Studio web publish pipeline to do an additional task during deployment.</span></span> <span data-ttu-id="a785c-110">任务是复制未向目标 web 站点的项目文件夹中的额外文件。</span><span class="sxs-lookup"><span data-stu-id="a785c-110">The task is to copy extra files that are not in the project folder to the destination web site.</span></span>

<span data-ttu-id="a785c-111">对于本教程中，你将复制一个额外的文件： *robots.txt*。</span><span class="sxs-lookup"><span data-stu-id="a785c-111">For this tutorial you'll copy one extra file: *robots.txt*.</span></span> <span data-ttu-id="a785c-112">你想要将此文件部署到过渡环境，但不适用于生产。</span><span class="sxs-lookup"><span data-stu-id="a785c-112">You want to deploy this file to staging but not to production.</span></span> <span data-ttu-id="a785c-113">在[到生产环境部署](deploying-to-production.md)教程，则此文件添加到项目，配置生产发布配置文件中排除它。</span><span class="sxs-lookup"><span data-stu-id="a785c-113">In [the Deploying to Production](deploying-to-production.md) tutorial, you added this file to the project and configured the Production publish profile to exclude it.</span></span> <span data-ttu-id="a785c-114">在本教程中，你将看到一种替代方法来处理此情况下，一个对于你想要部署，但不想在项目中包含的任何文件都很有用。</span><span class="sxs-lookup"><span data-stu-id="a785c-114">In this tutorial you'll see an alternative method to handle this situation, one that will be useful for any files that you want to deploy but don't want to include in the project.</span></span>

## <a name="move-the-robotstxt-file"></a><span data-ttu-id="a785c-115">移动 robots.txt 文件</span><span class="sxs-lookup"><span data-stu-id="a785c-115">Move the robots.txt file</span></span>

<span data-ttu-id="a785c-116">若要准备处理的不同方法*robots.txt*、 本教程的本部分中你将文件移动到未包含在项目中，文件夹和您删除*robots.txt*从暂存环境。</span><span class="sxs-lookup"><span data-stu-id="a785c-116">To prepare for a different method of handling *robots.txt*, in this section of the tutorial you move the file to a folder that is not included in the project, and you delete *robots.txt* from the staging environment.</span></span> <span data-ttu-id="a785c-117">它是删除该文件从过渡，以便你可以验证，你将文件部署到该环境的新方法能正常工作所需。</span><span class="sxs-lookup"><span data-stu-id="a785c-117">It is necessary to delete the file from staging so that you can verify that your new method of deploying the file to that environment is working correctly.</span></span>

1. <span data-ttu-id="a785c-118">在**解决方案资源管理器**，右键单击*robots.txt*文件并单击**从项目中排除**。</span><span class="sxs-lookup"><span data-stu-id="a785c-118">In **Solution Explorer**, right-click the *robots.txt* file and click **Exclude From Project**.</span></span>
2. <span data-ttu-id="a785c-119">使用 Windows 文件资源管理器，在解决方案文件夹中创建一个新文件夹并将其命名*ExtraFiles*。</span><span class="sxs-lookup"><span data-stu-id="a785c-119">Using Windows File Explorer, create a new folder in the solution folder and name it *ExtraFiles*.</span></span>
3. <span data-ttu-id="a785c-120">移动*robots.txt*文件从*ContosoUniversity*到项目文件夹*ExtraFiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a785c-120">Move the *robots.txt* file from the *ContosoUniversity* project folder to the *ExtraFiles* folder.</span></span>

    ![ExtraFiles 文件夹](deploying-extra-files/_static/image1.png)
4. <span data-ttu-id="a785c-122">使用 FTP 工具，删除*robots.txt*从过渡网站上的文件。</span><span class="sxs-lookup"><span data-stu-id="a785c-122">Using your FTP tool, delete the *robots.txt* file from the staging web site.</span></span>

    <span data-ttu-id="a785c-123">作为替代方法，则可以选择**删除目标位置的其他文件**下**文件发布选项**上**设置**选项卡上的过渡发布配置文件，并重新发布到过渡环境。</span><span class="sxs-lookup"><span data-stu-id="a785c-123">As an alternative, you can select **Remove additional files at destination** under **File Publish Options** on the **Settings** tab of the Staging publish profile, and republish to staging.</span></span>

## <a name="update-the-publish-profile-file"></a><span data-ttu-id="a785c-124">更新发布配置文件</span><span class="sxs-lookup"><span data-stu-id="a785c-124">Update the publish profile file</span></span>

<span data-ttu-id="a785c-125">只需*robots.txt*暂存，因此暂存你需要更新，以便将其部署的唯一发布配置文件中。</span><span class="sxs-lookup"><span data-stu-id="a785c-125">You only need *robots.txt* in staging, so the only publish profile you need to update in order to deploy it is Staging.</span></span>

1. <span data-ttu-id="a785c-126">在 Visual Studio 中，打开*Staging.pubxml*。</span><span class="sxs-lookup"><span data-stu-id="a785c-126">In Visual Studio, open *Staging.pubxml*.</span></span>
2. <span data-ttu-id="a785c-127">在结束之前，在文件末尾`</Project>`标记中，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="a785c-127">At the end of the file, before the closing `</Project>` tag, add the following markup:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample1.xml)]

    <span data-ttu-id="a785c-128">此代码创建一个新*目标*，将收集要部署的其他文件。</span><span class="sxs-lookup"><span data-stu-id="a785c-128">This code creates a new *target* that will collect additional files to be deployed.</span></span> <span data-ttu-id="a785c-129">目标组成一个或多个 MSBuild 将执行的任务基于你指定的条件。</span><span class="sxs-lookup"><span data-stu-id="a785c-129">A target is composed of one or more tasks that MSBuild will execute based on conditions you specify.</span></span>

    <span data-ttu-id="a785c-130">`Include`属性指定在其中查找文件的文件夹为*ExtraFiles*、 位于项目文件夹与相同的级别。</span><span class="sxs-lookup"><span data-stu-id="a785c-130">The `Include` attribute specifies that the folder in which to find the files is *ExtraFiles*, located at the same level as the project folder.</span></span> <span data-ttu-id="a785c-131">MSBuild 将从该文件夹，然后从 （双精度的星号指定递归子文件夹） 的任何子文件夹以递归方式收集所有文件。</span><span class="sxs-lookup"><span data-stu-id="a785c-131">MSBuild will collect all files from that folder and recursively from any subfolders (the double asterisk specifies recursive subfolders).</span></span> <span data-ttu-id="a785c-132">此代码与你可能使多个文件和文件处于子文件夹内*ExtraFiles*将部署文件夹，以及所有。</span><span class="sxs-lookup"><span data-stu-id="a785c-132">With this code you could put multiple files, and files in subfolders inside the *ExtraFiles* folder, and all will be deployed.</span></span>

    <span data-ttu-id="a785c-133">`DestinationRelativePath`元素指定的文件夹和文件应复制到相同的文件和文件夹结构中的目标 web 站点的根文件夹中找到*ExtraFiles*文件夹。</span><span class="sxs-lookup"><span data-stu-id="a785c-133">The `DestinationRelativePath` element specifies that the folders and files should be copied to the root folder of the destination web site, in the same file and folder structure as they are found in the *ExtraFiles* folder.</span></span> <span data-ttu-id="a785c-134">如果你想要复制*ExtraFiles*文件夹本身，`DestinationRelativePath`值将为*ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*。</span><span class="sxs-lookup"><span data-stu-id="a785c-134">If you wanted to copy the *ExtraFiles* folder itself, the `DestinationRelativePath` value would be *ExtraFiles\%(RecursiveDir)%(Filename)%(Extension)*.</span></span>
3. <span data-ttu-id="a785c-135">在结束之前，在文件末尾`</Project>`标记中，添加以下标记，指定何时执行新的目标。</span><span class="sxs-lookup"><span data-stu-id="a785c-135">At the end of the file, before the closing `</Project>` tag, add the following markup that specifies when to execute the new target.</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample2.xml)]

    <span data-ttu-id="a785c-136">此代码会导致新`CustomCollectFiles`每当执行将文件复制到目标文件夹的目标时将执行的目标。</span><span class="sxs-lookup"><span data-stu-id="a785c-136">This code causes the new `CustomCollectFiles` target to be executed whenever the target that copies files to the destination folder is executed.</span></span> <span data-ttu-id="a785c-137">没有与创建部署包发布的单独目标和新目标注入到这两个目标，以防你决定使用部署包，而不发布部署。</span><span class="sxs-lookup"><span data-stu-id="a785c-137">There is a separate target for publish versus deployment package creation, and the new target is injected in both targets in case you decide to deploy by using a deployment package instead of publishing.</span></span>

    <span data-ttu-id="a785c-138">*.Pubxml*文件现在看起来像下面的示例：</span><span class="sxs-lookup"><span data-stu-id="a785c-138">The *.pubxml* file now looks like the following example:</span></span>

    [!code-xml[Main](deploying-extra-files/samples/sample3.xml?highlight=53-71)]
4. <span data-ttu-id="a785c-139">保存并关闭*Staging.pubxml*文件。</span><span class="sxs-lookup"><span data-stu-id="a785c-139">Save and close the *Staging.pubxml* file.</span></span>

## <a name="publish-to-staging"></a><span data-ttu-id="a785c-140">发布到过渡环境</span><span class="sxs-lookup"><span data-stu-id="a785c-140">Publish to staging</span></span>

<span data-ttu-id="a785c-141">使用一键式发布或命令行，通过使用临时配置文件中发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="a785c-141">Using one-click publish or the command line, publish the application by using the Staging profile.</span></span>

<span data-ttu-id="a785c-142">如果你使用一键式发布，你可以验证在**预览**窗口， *robots.txt*将被复制。</span><span class="sxs-lookup"><span data-stu-id="a785c-142">If you use one-click publish, you can verify in the **Preview** window that *robots.txt* will be copied.</span></span> <span data-ttu-id="a785c-143">否则，使用 FTP 工具来验证*robots.txt*文件是在部署后的网站的根文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a785c-143">Otherwise, use your FTP tool to verify that the *robots.txt* file is in the root folder of the web site after deployment.</span></span>

## <a name="summary"></a><span data-ttu-id="a785c-144">总结</span><span class="sxs-lookup"><span data-stu-id="a785c-144">Summary</span></span>

<span data-ttu-id="a785c-145">这将完成这一系列的 ASP.NET web 应用程序部署到第三方托管提供商的教程。</span><span class="sxs-lookup"><span data-stu-id="a785c-145">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="a785c-146">有关任何这些教程中所涵盖的主题的详细信息，请参阅[ASP.NET 部署内容映射](https://go.microsoft.com/fwlink/p/?LinkId=282413)。</span><span class="sxs-lookup"><span data-stu-id="a785c-146">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://go.microsoft.com/fwlink/p/?LinkId=282413).</span></span>

## <a name="more-information"></a><span data-ttu-id="a785c-147">详细信息</span><span class="sxs-lookup"><span data-stu-id="a785c-147">More information</span></span>

<span data-ttu-id="a785c-148">如果你知道如何使用 MSBuild 文件，你可以通过在编写代码来自动处理许多其他部署任务*.pubxml*文件 （针对特定配置文件的任务） 或项目*。 wpp.targets*文件 （的任务适用于所有配置文件）。</span><span class="sxs-lookup"><span data-stu-id="a785c-148">If you know how to work with MSBuild files, you can automate many other deployment tasks by writing code in *.pubxml* files (for profile-specific tasks) or the project *.wpp.targets* file (for tasks that apply to all profiles).</span></span> <span data-ttu-id="a785c-149">有关详细信息*.pubxml*和*。 wpp.targets*文件，请参阅[如何： 编辑发布配置文件 (.pubxml) 文件中的部署设置与。 wpp.targets 在 Visual Studio Web 的文件项目](https://msdn.microsoft.com/library/ff398069)。</span><span class="sxs-lookup"><span data-stu-id="a785c-149">For more information about *.pubxml* and *.wpp.targets* files, see [How to: Edit Deployment Settings in Publish Profile (.pubxml) Files and the .wpp.targets File in Visual Studio Web Projects](https://msdn.microsoft.com/library/ff398069).</span></span> <span data-ttu-id="a785c-150">有关 MSBuild 的代码的基本介绍，请参阅**剖析项目文件**中[企业部署系列： 了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。</span><span class="sxs-lookup"><span data-stu-id="a785c-150">For a basic introduction to MSBuild code, see **The Anatomy of a Project File** in [Enterprise Deployment Series: Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="a785c-151">若要了解如何使用 MSBuild 文件为你自己的方案执行任务，请参阅本书：[内 Microsoft 生成引擎： 使用 MSBuild 和 Team Foundation Build](http://msbuildbook.com) Sayed Ibraham Hashimi 和 William Bartholomew。</span><span class="sxs-lookup"><span data-stu-id="a785c-151">To learn how to work with MSBuild files to perform tasks for your own scenarios, see this book: [Inside the Microsoft Build Engine: Using MSBuild and Team Foundation Build](http://msbuildbook.com) by Sayed Ibraham Hashimi and William Bartholomew.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="a785c-152">致谢</span><span class="sxs-lookup"><span data-stu-id="a785c-152">Acknowledgements</span></span>

<span data-ttu-id="a785c-153">我要特别感谢以下人员执行了巨大的内容的本系列教程的贡献：</span><span class="sxs-lookup"><span data-stu-id="a785c-153">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="a785c-154">Alberto Poblacion、 MVP &amp; MCT、 西班牙</span><span class="sxs-lookup"><span data-stu-id="a785c-154">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="a785c-155">Jarod Ferguson，数据平台开发 MVP，美国</span><span class="sxs-lookup"><span data-stu-id="a785c-155">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="a785c-156">恶劣 Mittal，Microsoft</span><span class="sxs-lookup"><span data-stu-id="a785c-156">Harsh Mittal, Microsoft</span></span>
- <span data-ttu-id="a785c-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="a785c-157">[Jon Galloway](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- [<span data-ttu-id="a785c-158">Kristina Olson, Microsoft</span><span class="sxs-lookup"><span data-stu-id="a785c-158">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="a785c-159">Mike Pope Microsoft</span><span class="sxs-lookup"><span data-stu-id="a785c-159">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="a785c-160">Mohit Srivastava Microsoft</span><span class="sxs-lookup"><span data-stu-id="a785c-160">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="a785c-161">Raffaele Rialdi，意大利</span><span class="sxs-lookup"><span data-stu-id="a785c-161">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="a785c-162">Rick Anderson Microsoft</span><span class="sxs-lookup"><span data-stu-id="a785c-162">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="a785c-163">[Sayed Hashimi、 Microsoft](http://sedodream.com/default.aspx)(twitter: [ @sayedihashimi ](http://twitter.com/sayedihashimi))</span><span class="sxs-lookup"><span data-stu-id="a785c-163">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="a785c-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](http://twitter.com/shanselman))</span><span class="sxs-lookup"><span data-stu-id="a785c-164">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="a785c-165">[Scott 搜寻、 Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [ @coolcsh ](http://twitter.com/coolcsh))</span><span class="sxs-lookup"><span data-stu-id="a785c-165">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="a785c-166">Srđan Božović、 塞尔维亚共和国</span><span class="sxs-lookup"><span data-stu-id="a785c-166">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="a785c-167">[Vishal Joshi、 Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [ @vishalrjoshi ](http://twitter.com/vishalrjoshi))</span><span class="sxs-lookup"><span data-stu-id="a785c-167">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a785c-168">[上一页](command-line-deployment.md)
> [下一页](troubleshooting.md)</span><span class="sxs-lookup"><span data-stu-id="a785c-168">[Previous](command-line-deployment.md)
[Next](troubleshooting.md)</span></span>
