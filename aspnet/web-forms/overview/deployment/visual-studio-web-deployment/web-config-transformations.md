---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用 Visual Studio 的 ASP.NET Web 部署： Web.config 文件转换 |Microsoft 文档
author: tdykstra
description: 本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，使用的...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: 77ed0d8b2fe85adb009a3f4759030b7fba8fb9d7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30880500"
---
<a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a><span data-ttu-id="cc559-103">使用 Visual Studio 的 ASP.NET Web 部署： Web.config 文件转换</span><span class="sxs-lookup"><span data-stu-id="cc559-103">ASP.NET Web Deployment using Visual Studio: Web.config File Transformations</span></span>
====================
<span data-ttu-id="cc559-104">通过[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="cc559-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="cc559-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="cc559-105">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="cc559-106">本系列教程演示如何部署 （发布） ASP.NET web 应用程序到 Azure App Service Web Apps 或第三方托管提供程序，通过使用 Visual Studio 2012 或 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="cc559-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="cc559-107">有关序列的信息，请参阅[序列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="cc559-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="cc559-108">概述</span><span class="sxs-lookup"><span data-stu-id="cc559-108">Overview</span></span>

<span data-ttu-id="cc559-109">本教程演示如何自动执行更改的过程*Web.config*文件时将其部署到不同的目标环境。</span><span class="sxs-lookup"><span data-stu-id="cc559-109">This tutorial shows you how to automate the process of changing the *Web.config* file when you deploy it to different destination environments.</span></span> <span data-ttu-id="cc559-110">大多数应用程序具有设置*Web.config*时部署应用程序必须是不同的文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-110">Most applications have settings in the *Web.config* file that must be different when the application is deployed.</span></span> <span data-ttu-id="cc559-111">自动化进行这些更改的过程，可以防止你无需手动执行它们，每次部署，这会非常单调乏味，而且容易出错。</span><span class="sxs-lookup"><span data-stu-id="cc559-111">Automating the process of making these changes keeps you from having to do them manually every time you deploy, which would be tedious and error prone.</span></span>

<span data-ttu-id="cc559-112">提示： 如果你收到如下错误消息，或当你完成本教程的内容不起作用，请务必检查[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="cc559-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a><span data-ttu-id="cc559-113">与 Web 部署参数的 Web.config 转换</span><span class="sxs-lookup"><span data-stu-id="cc559-113">Web.config transformations versus Web Deploy parameters</span></span>

<span data-ttu-id="cc559-114">有两种方法来自动执行更改的过程*Web.config*文件设置： [Web.config 转换](https://msdn.microsoft.com/library/dd465326.aspx)和[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc559-114">There are two ways to automate the process of changing *Web.config* file settings: [Web.config transformations](https://msdn.microsoft.com/library/dd465326.aspx) and [Web Deploy parameters](https://msdn.microsoft.com/library/ff398068.aspx).</span></span> <span data-ttu-id="cc559-115">A *Web.config*转换文件包含指定如何更改的 XML 标记*Web.config*文件部署时。</span><span class="sxs-lookup"><span data-stu-id="cc559-115">A *Web.config* transformation file contains XML markup that specifies how to change the *Web.config* file when it is deployed.</span></span> <span data-ttu-id="cc559-116">你可以指定不同的更改特定生成配置和特定发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-116">You can specify different changes for specific build configurations and for specific publish profiles.</span></span> <span data-ttu-id="cc559-117">默认值生成配置调试和发布，而且你可以创建自定义生成配置。</span><span class="sxs-lookup"><span data-stu-id="cc559-117">The default build configurations are Debug and Release, and you can create custom build configurations.</span></span> <span data-ttu-id="cc559-118">发布配置文件通常对应于目标环境中。</span><span class="sxs-lookup"><span data-stu-id="cc559-118">A publish profile typically corresponds to a destination environment.</span></span> <span data-ttu-id="cc559-119">(有关详细信息发布中的配置文件，您将学习[作为测试环境部署到 IIS](deploying-to-iis.md)教程。)</span><span class="sxs-lookup"><span data-stu-id="cc559-119">(You'll learn more about publish profiles in the [Deploying to IIS as a Test Environment](deploying-to-iis.md) tutorial.)</span></span>

<span data-ttu-id="cc559-120">可以使用 web 部署参数来指定许多不同类型的设置必须在部署，包括在中找到的设置过程中配置*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-120">Web Deploy parameters can be used to specify many different kinds of settings that must be configured during deployment, including settings that are found in *Web.config* files.</span></span> <span data-ttu-id="cc559-121">用于指定当*Web.config*文件更改时，Web 部署参数是更复杂的设置，但不是知道要部署之前设置的值时，它们会很有用。</span><span class="sxs-lookup"><span data-stu-id="cc559-121">When used to specify *Web.config* file changes, Web Deploy parameters are more complex to set up, but they are useful when you do not know the value to be set until you deploy.</span></span> <span data-ttu-id="cc559-122">例如，在企业环境中，你可能会造成*部署包*并将其提供给的人员在 IT 部门要将安装在生产环境，并该用户有能够输入连接字符串或不希望这样做的密码知道。</span><span class="sxs-lookup"><span data-stu-id="cc559-122">For example, in an enterprise environment, you might create a *deployment package* and give it to a person in the IT department to install in production, and that person has to be able to enter connection strings or passwords that you do not know.</span></span>

<span data-ttu-id="cc559-123">对于本系列教程涵盖方案，您事先知道所必须采取的措施的一切*Web.config*文件，因此不需要使用 Web 部署参数。</span><span class="sxs-lookup"><span data-stu-id="cc559-123">For the scenario that this tutorial series covers, you know in advance everything that has to be done to the *Web.config* file, so you do not need to use Web Deploy parameters.</span></span> <span data-ttu-id="cc559-124">你将配置某些转换，具体取决于生成配置使用，存在不同，并且一些与不同，具体取决于使用的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-124">You'll configure some transformations that differ depending on the build configuration used, and some that differ depending on the publish profile used.</span></span>

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a><span data-ttu-id="cc559-125">在 Azure 中的指定 Web.config 设置</span><span class="sxs-lookup"><span data-stu-id="cc559-125">Specifying Web.config settings in Azure</span></span>

<span data-ttu-id="cc559-126">如果*Web.config*你想要更改的文件设置位于`<connectionStrings>`或`<appSettings>`元素，以及将部署到 Azure App Service 中 Web Apps，您是否自动执行过程中的更改的另一种方法部署。</span><span class="sxs-lookup"><span data-stu-id="cc559-126">If the *Web.config* file settings that you want to change are in the `<connectionStrings>` or the `<appSettings>` element, and if you are deploying to Web Apps in Azure App Service, you have another option for automating changes during deployment.</span></span> <span data-ttu-id="cc559-127">你可以输入你想要在 Azure 中生效设置**配置**你的 web 应用的管理门户页面的选项卡 (向下滚动到**应用设置**和**连接字符串**部分)。</span><span class="sxs-lookup"><span data-stu-id="cc559-127">You can enter the settings that you want to take effect in Azure in the **Configure** tab of the management portal page for your web app (scroll down to the **app settings** and **connection strings** sections).</span></span> <span data-ttu-id="cc559-128">部署项目时，Azure 将自动应用所做的更改。</span><span class="sxs-lookup"><span data-stu-id="cc559-128">When you deploy the project, Azure automatically applies the changes.</span></span> <span data-ttu-id="cc559-129">有关详细信息，请参阅[Windows Azure 网站： 应用程序字符串和连接字符串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc559-129">For more information, see [Windows Azure Web Sites: How Application Strings and Connection Strings Work](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx).</span></span>

## <a name="default-transformation-files"></a><span data-ttu-id="cc559-130">默认转换文件</span><span class="sxs-lookup"><span data-stu-id="cc559-130">Default transformation files</span></span>

<span data-ttu-id="cc559-131">在**解决方案资源管理器**，展开*Web.config*若要查看*Web.Debug.config*和*Web.Release.config*转换文件默认情况下，对两个默认的生成配置创建。</span><span class="sxs-lookup"><span data-stu-id="cc559-131">In **Solution Explorer**, expand *Web.config* to see the *Web.Debug.config* and *Web.Release.config* transformation files that are created by default for the two default build configurations.</span></span>

![Web.config_transform_files](web-config-transformations/_static/image1.png)

<span data-ttu-id="cc559-133">你可以通过右键单击 Web.config 文件并选择创建的自定义生成配置的转换文件**添加配置转换**从上下文菜单。</span><span class="sxs-lookup"><span data-stu-id="cc559-133">You can create transformation files for custom build configurations by right-clicking the Web.config file and choosing **Add Config Transforms** from the context menu.</span></span> <span data-ttu-id="cc559-134">本教程中，不需要为此，请并且禁用菜单选项，因为你尚未创建任何自定义生成配置。</span><span class="sxs-lookup"><span data-stu-id="cc559-134">For this tutorial you don't need to do that, and the menu option is disabled, because you haven't created any custom build configurations.</span></span>

<span data-ttu-id="cc559-135">稍后你将创建三个详细转换文件，每个测试，用于暂存，和生产发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-135">Later you'll create three more transformation files, one each for the test, staging, and production publish profiles.</span></span> <span data-ttu-id="cc559-136">处理在发布配置文件转换文件因为它依赖于目标环境的一个典型示例是设置的不同的测试中和生产的 WCF 终结点。</span><span class="sxs-lookup"><span data-stu-id="cc559-136">A typical example of a setting that you would handle in a publish profile transformation file because it depends on the destination environment is a WCF endpoint that is different for test versus production.</span></span> <span data-ttu-id="cc559-137">你将创建发布配置文件转换文件中更高版本的教程后创建的发布配置文件，可以随。</span><span class="sxs-lookup"><span data-stu-id="cc559-137">You'll create publish profile transformation files in later tutorials after you create the publish profiles that they go with.</span></span>

## <a name="disable-debug-mode"></a><span data-ttu-id="cc559-138">禁用调试模式</span><span class="sxs-lookup"><span data-stu-id="cc559-138">Disable debug mode</span></span>

<span data-ttu-id="cc559-139">取决于生成配置，而不是目标环境的设置的示例`debug`属性。</span><span class="sxs-lookup"><span data-stu-id="cc559-139">An example of a setting that depends on build configuration rather than destination environment is the `debug` attribute.</span></span> <span data-ttu-id="cc559-140">为发布版本，则通常想调试禁用无论的环境部署到。</span><span class="sxs-lookup"><span data-stu-id="cc559-140">For a Release build, you typically want debugging disabled regardless of which environment you are deploying to.</span></span> <span data-ttu-id="cc559-141">因此，默认情况下，Visual Studio 项目模板创建*Web.Release.config*将带中删除的代码文件转换`debug`属性从`compilation`元素。</span><span class="sxs-lookup"><span data-stu-id="cc559-141">Therefore, by default the Visual Studio project templates create *Web.Release.config* transform files with code that removes the `debug` attribute from the `compilation` element.</span></span> <span data-ttu-id="cc559-142">下面是默认值*Web.Release.config*： 除了一些注释掉的示例转换代码，它包括中的代码`compilation`中移除的元素`debug`属性：</span><span class="sxs-lookup"><span data-stu-id="cc559-142">Here is the default *Web.Release.config*: in addition to some sample transformation code that is commented out, it includes code in the `compilation` element that removes the `debug` attribute:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

<span data-ttu-id="cc559-143">`xdt:Transform="RemoveAttributes(debug)"`属性指定你想`debug`属性从移除`system.web/compilation`中部署元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-143">The `xdt:Transform="RemoveAttributes(debug)"` attribute specifies that you want the `debug` attribute to be removed from the `system.web/compilation` element in the deployed *Web.config* file.</span></span> <span data-ttu-id="cc559-144">这将进行每次部署发布版本。</span><span class="sxs-lookup"><span data-stu-id="cc559-144">This will be done every time you deploy a Release build.</span></span>

## <a name="limit-error-log-access-to-administrators"></a><span data-ttu-id="cc559-145">限制对管理员的错误日志访问</span><span class="sxs-lookup"><span data-stu-id="cc559-145">Limit error log access to administrators</span></span>

<span data-ttu-id="cc559-146">如果没有错误，应用程序运行时，应用程序将显示常规错误页面代替系统生成的错误页，并且它使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)错误日志记录和报表。</span><span class="sxs-lookup"><span data-stu-id="cc559-146">If there's an error while the application runs, the application displays a generic error page in place of the system-generated error page, and it uses the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) for error logging and reporting.</span></span> <span data-ttu-id="cc559-147">`customErrors`应用程序中的元素*Web.config*文件指定的错误页：</span><span class="sxs-lookup"><span data-stu-id="cc559-147">The `customErrors` element in the application *Web.config* file specifies the error page:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

<span data-ttu-id="cc559-148">若要查看错误页，暂时更改`mode`属性`customErrors`元素从"RemoteOnly"到"On"和运行 Visual Studio 中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="cc559-148">To see the error page, temporarily change the `mode` attribute of the `customErrors` element from "RemoteOnly" to "On" and run the application from Visual Studio.</span></span> <span data-ttu-id="cc559-149">导致错误通过请求 URL 无效，如*Studentsxxx.aspx*。</span><span class="sxs-lookup"><span data-stu-id="cc559-149">Cause an error by requesting an invalid URL, such as *Studentsxxx.aspx*.</span></span> <span data-ttu-id="cc559-150">而不是 IIS 生成"无法找到资源"错误页上，你看到*GenericErrorPage.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="cc559-150">Instead of an IIS-generated "The resource cannot be found" error page, you see the *GenericErrorPage.aspx* page.</span></span>

![错误页](web-config-transformations/_static/image2.png)

<span data-ttu-id="cc559-152">若要查看错误日志，替换 URL 中的所有内容后使用的端口号*elmah.axd* (例如， `http://localhost:51130/elmah.axd`)，然后按 Enter:</span><span class="sxs-lookup"><span data-stu-id="cc559-152">To see the error log, replace everything in the URL after the port number with *elmah.axd* (for example, `http://localhost:51130/elmah.axd`) and press Enter:</span></span>

![ELMAH 页](web-config-transformations/_static/image3.png)

<span data-ttu-id="cc559-154">不要忘记设置`customErrors`回"RemoteOnly"模式完成后的元素。</span><span class="sxs-lookup"><span data-stu-id="cc559-154">Don't forget to set the `customErrors` element back to "RemoteOnly" mode when you're done.</span></span>

<span data-ttu-id="cc559-155">你的开发计算机上很方便地允许免费访问错误日志页中，但在生产环境中将会带来安全风险。</span><span class="sxs-lookup"><span data-stu-id="cc559-155">On your development computer it's convenient to allow free access to the error log page, but in production that would be a security risk.</span></span> <span data-ttu-id="cc559-156">对于生产站点中，你想要添加授权规则，将错误日志访问限制为管理员，并确保限制工作你希望在测试和过渡还中。</span><span class="sxs-lookup"><span data-stu-id="cc559-156">For the production site, you want to add an authorization rule that restricts error log access to administrators, and to make sure that the restriction works you want it in test and staging also.</span></span> <span data-ttu-id="cc559-157">因此，这是你想要实现，每次部署发布版本，因此在其所属的另一个更改*Web.Release.config*文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-157">Therefore this is another change that you want to implement every time you deploy a Release build, and so it belongs in the *Web.Release.config* file.</span></span>

<span data-ttu-id="cc559-158">打开*Web.Release.config*和添加新`location`立即在关闭前的元素`configuration`标记，如下所示。</span><span class="sxs-lookup"><span data-stu-id="cc559-158">Open *Web.Release.config* and add a new `location` element immediately before the closing `configuration` tag, as shown here.</span></span>

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

<span data-ttu-id="cc559-159">`Transform`属性值为"插入"，则这`location`元素要作为同级添加到任何现有`location`中的元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-159">The `Transform` attribute value of "Insert" causes this `location` element to be added as a sibling to any existing `location` elements in the *Web.config* file.</span></span> <span data-ttu-id="cc559-160">(已存在一个`location`元素，它指定授权规则的**更新信用额度**页。)</span><span class="sxs-lookup"><span data-stu-id="cc559-160">(There is already one `location` element that specifies authorization rules for the **Update Credits** page.)</span></span>

<span data-ttu-id="cc559-161">现在你可以预览转换后，若要确保你正确编码。</span><span class="sxs-lookup"><span data-stu-id="cc559-161">Now you can preview the transform to make sure that you coded it correctly.</span></span>

<span data-ttu-id="cc559-162">在**解决方案资源管理器**，右键单击*Web.Release.config*单击**预览转换**。</span><span class="sxs-lookup"><span data-stu-id="cc559-162">In **Solution Explorer**, right-click *Web.Release.config* and click **Preview Transform**.</span></span>

![预览转换菜单](web-config-transformations/_static/image4.png)

<span data-ttu-id="cc559-164">演示如何开发页面将打开*Web.config*上的左窗格和内容文件已部署*Web.config*文件将如下所示在右侧，突出显示的更改。</span><span class="sxs-lookup"><span data-stu-id="cc559-164">A page opens that shows you the development *Web.config* file on the left and what the deployed *Web.config* file will look like on the right, with changes highlighted.</span></span>

![调试转换的预览](web-config-transformations/_static/image5.png)

![位置转换的预览](web-config-transformations/_static/image6.png)

<span data-ttu-id="cc559-167">(在预览版中，你可能会发现自己编写一些附加更改转换为： 这些通常涉及不会影响功能的空白区域中删除。)</span><span class="sxs-lookup"><span data-stu-id="cc559-167">( In the preview, you might notice some additional changes that you didn't write transforms for: these typically involve the removal of white space that doesn't affect functionality.)</span></span>

<span data-ttu-id="cc559-168">当你在部署后测试站点时，还将测试来验证授权规则有效。</span><span class="sxs-lookup"><span data-stu-id="cc559-168">When you test the site after deployment, you'll also test to verify that the authorization rule is effective.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cc559-169">**安全说明**永远不会显示错误详细信息为公共在生产应用程序，或将该信息存储在公共位置。</span><span class="sxs-lookup"><span data-stu-id="cc559-169">**Security Note** Never display error details to the public in a production application, or store that information in a public location.</span></span> <span data-ttu-id="cc559-170">攻击者可以使用错误信息发现站点中的漏洞。</span><span class="sxs-lookup"><span data-stu-id="cc559-170">Attackers can use error information to discover vulnerabilities in a site.</span></span> <span data-ttu-id="cc559-171">如果你在自己的应用程序中使用 ELMAH，配置 ELMAH 来尽量降低安全风险。</span><span class="sxs-lookup"><span data-stu-id="cc559-171">If you use ELMAH in your own application, configure ELMAH to minimize security risks.</span></span> <span data-ttu-id="cc559-172">本教程中的 ELMAH 示例不应视为是建议的配置。</span><span class="sxs-lookup"><span data-stu-id="cc559-172">The ELMAH example in this tutorial should not be considered a recommended configuration.</span></span> <span data-ttu-id="cc559-173">它是一个示例： 所选为了演示如何处理应用程序必须能够在其中创建文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="cc559-173">It is an example that was chosen in order to illustrate how to handle a folder that the application must be able to create files in.</span></span> <span data-ttu-id="cc559-174">有关详细信息，请参阅[保护 ELMAH 终结点](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。</span><span class="sxs-lookup"><span data-stu-id="cc559-174">For more information, see [securing the ELMAH endpoint](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages).</span></span>


## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a><span data-ttu-id="cc559-175">将在中处理的设置发布配置文件转换文件</span><span class="sxs-lookup"><span data-stu-id="cc559-175">A setting that you'll handle in publish profile transformation files</span></span>

<span data-ttu-id="cc559-176">一种常见方案是让*Web.config*文件必须将部署到每个环境中不同的设置。</span><span class="sxs-lookup"><span data-stu-id="cc559-176">A common scenario is to have *Web.config* file settings that must be different in each environment that you deploy to.</span></span> <span data-ttu-id="cc559-177">例如，调用 WCF 服务的应用程序可能需要在测试和生产环境的不同终结点。</span><span class="sxs-lookup"><span data-stu-id="cc559-177">For example, an application that calls a WCF service might need a different endpoint in test and production environments.</span></span> <span data-ttu-id="cc559-178">Contoso 大学应用程序还包括这种类型的设置。</span><span class="sxs-lookup"><span data-stu-id="cc559-178">The Contoso University application includes a setting of this kind also.</span></span> <span data-ttu-id="cc559-179">此设置控制可见的指示符站点的页上，告诉你要在中，如开发、 测试或生产的环境。</span><span class="sxs-lookup"><span data-stu-id="cc559-179">This setting controls a visible indicator on a site's pages that tells you which environment you are in, such as development, test, or production.</span></span> <span data-ttu-id="cc559-180">设置值确定是否应用程序都将追加"（开发）"或"（测试）"中的主要标题*Site.Master*母版页：</span><span class="sxs-lookup"><span data-stu-id="cc559-180">The setting value determines whether the application will append "(Dev)" or "(Test)" to the main heading in the *Site.Master* master page:</span></span>

![环境指示器](web-config-transformations/_static/image7.png)

<span data-ttu-id="cc559-182">当应用程序运行在过渡环境还是生产省略环境指示器。</span><span class="sxs-lookup"><span data-stu-id="cc559-182">The environment indicator is omitted when the application is running in staging or production.</span></span>

<span data-ttu-id="cc559-183">Contoso 大学 web 页读取在中设置一个值`appSettings`中*Web.config*以确定哪些环境中运行该应用程序的文件：</span><span class="sxs-lookup"><span data-stu-id="cc559-183">The Contoso University web pages read a value that is set in `appSettings` in the *Web.config* file in order to determine what environment the application is running in:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

<span data-ttu-id="cc559-184">值应在测试环境中，将"Test"和"生产"过渡和生产。</span><span class="sxs-lookup"><span data-stu-id="cc559-184">The value should be "Test" in the test environment, and "Prod" for staging and production.</span></span>

<span data-ttu-id="cc559-185">转换文件中的以下代码将实现此转换：</span><span class="sxs-lookup"><span data-stu-id="cc559-185">The following code in a transform file will implement this transformation:</span></span>

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

<span data-ttu-id="cc559-186">`xdt:Transform`属性的值"SetAttributes"指示此转换旨在更改中的现有元素的属性值*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-186">The `xdt:Transform` attribute value "SetAttributes" indicates that the purpose of this transform is to change attribute values of an existing element in the *Web.config* file.</span></span> <span data-ttu-id="cc559-187">`xdt:Locator`属性的值"Match(key)"指示要修改的元素是一个其`key`属性匹配`key`此处指定的属性。</span><span class="sxs-lookup"><span data-stu-id="cc559-187">The `xdt:Locator` attribute value "Match(key)" indicates that the element to be modified is the one whose `key` attribute matches the `key` attribute specified here.</span></span> <span data-ttu-id="cc559-188">仅另一个属性的`add`元素是`value`，这也将更改的内容中部署*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-188">The only other attribute of the `add` element is `value`, and that is what will be changed in the deployed *Web.config* file.</span></span> <span data-ttu-id="cc559-189">此处显示的原因代码`value`属性`Environment``appSettings`元素设置为"Test" *Web.config*部署的文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-189">The code shown here causes the `value` attribute of the `Environment` `appSettings` element to be set to "Test" in the *Web.config* file that is deployed.</span></span>

<span data-ttu-id="cc559-190">此转换属于你尚未创建发布配置文件转换文件。</span><span class="sxs-lookup"><span data-stu-id="cc559-190">This transform belongs in the publish profile transform files, which you haven't created yet.</span></span> <span data-ttu-id="cc559-191">你将创建并更新转换文件，当你创建的测试、 过渡和生产环境的发布配置文件，则实现此更改。</span><span class="sxs-lookup"><span data-stu-id="cc559-191">You'll create and update the transform files that implement this change when you create the publish profiles for the test, staging, and production environments.</span></span> <span data-ttu-id="cc559-192">你将在执行该操作[将部署到 IIS](deploying-to-iis.md)和[部署到生产环境](deploying-to-production.md)教程。</span><span class="sxs-lookup"><span data-stu-id="cc559-192">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

> [!NOTE]
> <span data-ttu-id="cc559-193">因为此设置处于`<appSettings>`元素，必须在要部署到 Azure 应用程序服务，请参阅中的 Web Apps 时指定转换所需的另一种可选[在 Azure 中的指定 Web.config 设置](#watransforms)前面的本主题中。</span><span class="sxs-lookup"><span data-stu-id="cc559-193">Because this setting is in the `<appSettings>` element, you have another alternative for specifying the transformation when you're deploying to Web Apps in Azure App Service See [Specifying Web.config settings in Azure](#watransforms) earlier in this topic.</span></span>


## <a name="setting-connection-strings"></a><span data-ttu-id="cc559-194">设置连接字符串</span><span class="sxs-lookup"><span data-stu-id="cc559-194">Setting connection strings</span></span>

<span data-ttu-id="cc559-195">虽然默认转换文件包含的示例，演示如何更新连接字符串，但在大多数情况下你不必设置连接字符串转换，因为你可以发布配置文件中指定连接字符串。</span><span class="sxs-lookup"><span data-stu-id="cc559-195">Although the default transform file contains an example that shows how to update a connection string, in most cases you do not need to set up connection string transformations, because you can specify connection strings in the publish profile.</span></span> <span data-ttu-id="cc559-196">你将在执行该操作[将部署到 IIS](deploying-to-iis.md)和[部署到生产环境](deploying-to-production.md)教程。</span><span class="sxs-lookup"><span data-stu-id="cc559-196">You'll do that in the [deploy to IIS](deploying-to-iis.md) and [deploy to production](deploying-to-production.md) tutorials.</span></span>

## <a name="summary"></a><span data-ttu-id="cc559-197">总结</span><span class="sxs-lookup"><span data-stu-id="cc559-197">Summary</span></span>

<span data-ttu-id="cc559-198">你现在要做尽可能多可以按照与*Web.config*转换之前创建的发布配置文件中，并已了解的内容将在已部署的 Web.config 文件中预览。</span><span class="sxs-lookup"><span data-stu-id="cc559-198">You have now done as much as you can with *Web.config* transformations before you create the publish profiles, and you've seen a preview of what will be in the deployed Web.config file.</span></span>

![位置转换的预览](web-config-transformations/_static/image8.png)

<span data-ttu-id="cc559-200">在以下教程中，你将负责设置项目属性所需的部署设置任务。</span><span class="sxs-lookup"><span data-stu-id="cc559-200">In the following tutorial, you'll take care of deployment set-up tasks that require setting project properties.</span></span>

## <a name="more-information"></a><span data-ttu-id="cc559-201">详细信息</span><span class="sxs-lookup"><span data-stu-id="cc559-201">More Information</span></span>

<span data-ttu-id="cc559-202">有关本教程所涵盖主题的详细信息，请参阅[使用 Web.config 转换在部署过程中更改目标 Web.config 文件或 app.config 文件中设置](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)的 Web 部署内容映射中Visual Studio 和 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="cc559-202">For more information about topics covered by this tutorial, see [Using Web.config transformations to change settings in the destination Web.config file or app.config file during deployment](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cc559-203">[上一页](preparing-databases.md)
> [下一页](project-properties.md)</span><span class="sxs-lookup"><span data-stu-id="cc559-203">[Previous](preparing-databases.md)
[Next](project-properties.md)</span></span>
