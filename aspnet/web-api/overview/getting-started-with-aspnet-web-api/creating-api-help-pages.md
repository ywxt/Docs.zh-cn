---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: 创建用于 ASP.NET Web API 的帮助页 |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2013
ms.topic: article
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 37fd26ebaea192cb540c443eff8a07343ab8c15b
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "28037898"
---
<a name="creating-help-pages-for-aspnet-web-api"></a><span data-ttu-id="d9511-102">创建用于 ASP.NET Web API 的帮助页</span><span class="sxs-lookup"><span data-stu-id="d9511-102">Creating Help Pages for ASP.NET Web API</span></span>
====================
<span data-ttu-id="d9511-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="d9511-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="d9511-104">当创建 web API 时，通常很有用创建帮助页中，以便其他开发人员知道如何调用你的 API。</span><span class="sxs-lookup"><span data-stu-id="d9511-104">When you create a web API, it is often useful to create a help page, so that other developers will know how to call your API.</span></span> <span data-ttu-id="d9511-105">你可以手动创建所有文档，但最好自动生成尽可能多地。</span><span class="sxs-lookup"><span data-stu-id="d9511-105">You could create all of the documentation manually, but it is better to autogenerate as much as possible.</span></span>

<span data-ttu-id="d9511-106">为了简化此任务，ASP.NET Web API 提供一个库用于自动生成的帮助页在运行时。</span><span class="sxs-lookup"><span data-stu-id="d9511-106">To make this task easier, ASP.NET Web API provides a library for auto-generating help pages at run time.</span></span>

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a><span data-ttu-id="d9511-107">创建 API 帮助页</span><span class="sxs-lookup"><span data-stu-id="d9511-107">Creating API Help Pages</span></span>

<span data-ttu-id="d9511-108">安装[ASP.NET 和 Web 工具 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="d9511-108">Install [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="d9511-109">此更新将集成到 Web API 项目模板的帮助页。</span><span class="sxs-lookup"><span data-stu-id="d9511-109">This update integrates help pages into the Web API project template.</span></span>

<span data-ttu-id="d9511-110">接下来，创建新的 ASP.NET MVC 4 项目并选择 Web API 项目模板。</span><span class="sxs-lookup"><span data-stu-id="d9511-110">Next, create a new ASP.NET MVC 4 project and select the Web API project template.</span></span> <span data-ttu-id="d9511-111">项目模板创建名为示例 API 控制器`ValuesController`。</span><span class="sxs-lookup"><span data-stu-id="d9511-111">The project template creates an example API controller named `ValuesController`.</span></span> <span data-ttu-id="d9511-112">此模板还创建 API 帮助页。</span><span class="sxs-lookup"><span data-stu-id="d9511-112">The template also creates the API help pages.</span></span> <span data-ttu-id="d9511-113">所有的帮助页的代码文件放置在项目的区域文件夹中。</span><span class="sxs-lookup"><span data-stu-id="d9511-113">All of the code files for the help page are placed in the Areas folder of the project.</span></span>

![](creating-api-help-pages/_static/image2.png)

<span data-ttu-id="d9511-114">运行应用程序时，主页页面包含的 API 帮助页的链接。</span><span class="sxs-lookup"><span data-stu-id="d9511-114">When you run the application, the home page contains a link to the API help page.</span></span> <span data-ttu-id="d9511-115">从主页页面的相对路径是 /Help。</span><span class="sxs-lookup"><span data-stu-id="d9511-115">From the home page, the relative path is /Help.</span></span>

![](creating-api-help-pages/_static/image3.png)

<span data-ttu-id="d9511-116">此链接将你带到 API 摘要页。</span><span class="sxs-lookup"><span data-stu-id="d9511-116">This link brings you to an API summary page.</span></span>

![](creating-api-help-pages/_static/image4.png)

<span data-ttu-id="d9511-117">为此页的 MVC 视图 Areas/HelpPage/Views/Help/Index.cshtml 中定义。</span><span class="sxs-lookup"><span data-stu-id="d9511-117">The MVC view for this page is defined in Areas/HelpPage/Views/Help/Index.cshtml.</span></span> <span data-ttu-id="d9511-118">你可以编辑此页后，可以修改布局、 简介、 标题、 样式和等。</span><span class="sxs-lookup"><span data-stu-id="d9511-118">You can edit this page to modify the layout, introduction, title, styles, and so forth.</span></span>

<span data-ttu-id="d9511-119">页的主要部分是 Api，由控制器分组的表。</span><span class="sxs-lookup"><span data-stu-id="d9511-119">The main part of the page is a table of APIs, grouped by controller.</span></span> <span data-ttu-id="d9511-120">表条目动态生成的使用**IApiExplorer**接口。</span><span class="sxs-lookup"><span data-stu-id="d9511-120">The table entries are generated dynamically, using the **IApiExplorer** interface.</span></span> <span data-ttu-id="d9511-121">（我将详细讨论关于此界面更高版本。）如果你添加一个新的 API 控制器，在运行时自动更新表。</span><span class="sxs-lookup"><span data-stu-id="d9511-121">(I'll talk more about this interface later.) If you add a new API controller, the table is automatically updated at run time.</span></span>

<span data-ttu-id="d9511-122">"API"列列出的 HTTP 方法和相对 URI。</span><span class="sxs-lookup"><span data-stu-id="d9511-122">The "API" column lists the HTTP method and relative URI.</span></span> <span data-ttu-id="d9511-123">"说明"列包含每个 API 的文档。</span><span class="sxs-lookup"><span data-stu-id="d9511-123">The "Description" column contains documentation for each API.</span></span> <span data-ttu-id="d9511-124">最初，文档并不仅仅是占位符文本。</span><span class="sxs-lookup"><span data-stu-id="d9511-124">Initially, the documentation is just placeholder text.</span></span> <span data-ttu-id="d9511-125">在下一步的部分中，我将向你演示如何从 XML 注释中添加文档。</span><span class="sxs-lookup"><span data-stu-id="d9511-125">In the next section, I'll show you how to add documentation from XML comments.</span></span>

<span data-ttu-id="d9511-126">每个 API 提供到具有更多详细信息，包括示例请求和响应正文页的链接。</span><span class="sxs-lookup"><span data-stu-id="d9511-126">Each API has a link to a page with more detailed information, including example request and response bodies.</span></span>

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a><span data-ttu-id="d9511-127">向现有项目添加帮助页</span><span class="sxs-lookup"><span data-stu-id="d9511-127">Adding Help Pages to an Existing Project</span></span>

<span data-ttu-id="d9511-128">可以使用 NuGet 包管理器将帮助页面添加到现有的 Web API 项目中。</span><span class="sxs-lookup"><span data-stu-id="d9511-128">You can add help pages to an existing Web API project by using NuGet Package Manager.</span></span> <span data-ttu-id="d9511-129">此选项可从比"Web API"模板不同的项目模板开始。</span><span class="sxs-lookup"><span data-stu-id="d9511-129">This option is useful you start from a different project template than the "Web API" template.</span></span>

<span data-ttu-id="d9511-130">从**工具**菜单上，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="d9511-130">From the **Tools** menu, select **Library Package Manager**, and then select **Package Manager Console**.</span></span> <span data-ttu-id="d9511-131">在[程序包管理器控制台](http://docs.nuget.org/docs/start-here/using-the-package-manager-console)窗口中，键入以下命令之一：</span><span class="sxs-lookup"><span data-stu-id="d9511-131">In the [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) window, type one of the following commands:</span></span>

<span data-ttu-id="d9511-132">有关**C#** 应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span><span class="sxs-lookup"><span data-stu-id="d9511-132">For a **C#** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage`</span></span>

<span data-ttu-id="d9511-133">有关**Visual Basic**应用程序： `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span><span class="sxs-lookup"><span data-stu-id="d9511-133">For a **Visual Basic** application: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`</span></span>

<span data-ttu-id="d9511-134">有两个包，一个用于 C# 和 Visual Basic 的一个。</span><span class="sxs-lookup"><span data-stu-id="d9511-134">There are two packages, one for C# and one for Visual Basic.</span></span> <span data-ttu-id="d9511-135">请确保使用与你的项目匹配的一个。</span><span class="sxs-lookup"><span data-stu-id="d9511-135">Make sure to use the one that matches your project.</span></span>

<span data-ttu-id="d9511-136">此命令将安装必需的程序集并添加 （位于的区域/HelpPage 文件夹中） 的帮助页的 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="d9511-136">This command installs the necessary assemblies and adds the MVC views for the help pages (located in the Areas/HelpPage folder).</span></span> <span data-ttu-id="d9511-137">你将需要手动添加的帮助页的链接。</span><span class="sxs-lookup"><span data-stu-id="d9511-137">You'll need to manually add a link to the Help page.</span></span> <span data-ttu-id="d9511-138">URI 是 /Help。</span><span class="sxs-lookup"><span data-stu-id="d9511-138">The URI is /Help.</span></span> <span data-ttu-id="d9511-139">若要在 razor 视图中创建一个链接，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="d9511-139">To create a link in a razor view, add the following:</span></span>

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

<span data-ttu-id="d9511-140">此外，请确保注册区域。</span><span class="sxs-lookup"><span data-stu-id="d9511-140">Also, make sure to register areas.</span></span> <span data-ttu-id="d9511-141">在 Global.asax 文件中，添加以下代码到**应用程序\_启动**方法，如果它尚不存在：</span><span class="sxs-lookup"><span data-stu-id="d9511-141">In the Global.asax file, add the following code to the **Application\_Start** method, if it is not there already:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a><span data-ttu-id="d9511-142">添加 API 文档</span><span class="sxs-lookup"><span data-stu-id="d9511-142">Adding API Documentation</span></span>

<span data-ttu-id="d9511-143">默认情况下，帮助页具有文档的占位符字符串。</span><span class="sxs-lookup"><span data-stu-id="d9511-143">By default, the help pages have placeholder strings for documentation.</span></span> <span data-ttu-id="d9511-144">你可以使用[XML 文档注释](https://msdn.microsoft.com/library/b2s063f7.aspx)创建文档。</span><span class="sxs-lookup"><span data-stu-id="d9511-144">You can use [XML documentation comments](https://msdn.microsoft.com/library/b2s063f7.aspx) to create the documentation.</span></span> <span data-ttu-id="d9511-145">若要启用此功能，打开文件应用程序区域/HelpPage\_Start/HelpPageConfig.cs 并取消注释以下行：</span><span class="sxs-lookup"><span data-stu-id="d9511-145">To enable this feature, open the file Areas/HelpPage/App\_Start/HelpPageConfig.cs and uncomment the following line:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

<span data-ttu-id="d9511-146">现在启用 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="d9511-146">Now enable XML documentation.</span></span> <span data-ttu-id="d9511-147">在解决方案资源管理器，右键单击该项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="d9511-147">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="d9511-148">选择**生成**页。</span><span class="sxs-lookup"><span data-stu-id="d9511-148">Select the **Build** page.</span></span>

![](creating-api-help-pages/_static/image6.png)

<span data-ttu-id="d9511-149">下**输出**，检查**XML 文档文件**。</span><span class="sxs-lookup"><span data-stu-id="d9511-149">Under **Output**, check **XML documentation file**.</span></span> <span data-ttu-id="d9511-150">在编辑框中，键入"应用\_Data/XmlDocument.xml"。</span><span class="sxs-lookup"><span data-stu-id="d9511-150">In the edit box, type "App\_Data/XmlDocument.xml".</span></span>

![](creating-api-help-pages/_static/image7.png)

<span data-ttu-id="d9511-151">接下来，打开的代码`ValuesController`/Controllers/ValuesControler.cs 中定义的 API 控制器。</span><span class="sxs-lookup"><span data-stu-id="d9511-151">Next, open the code for the `ValuesController` API controller, which is defined in /Controllers/ValuesControler.cs.</span></span> <span data-ttu-id="d9511-152">将文档注释添加到控制器方法。</span><span class="sxs-lookup"><span data-stu-id="d9511-152">Add some documentation comments to the controller methods.</span></span> <span data-ttu-id="d9511-153">例如：</span><span class="sxs-lookup"><span data-stu-id="d9511-153">For example:</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="d9511-154">提示： 如果你将插入符号放置在上方方法的行，然后键入三个正斜杠，Visual Studio 自动插入的 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="d9511-154">Tip: If you position the caret on the line above the method and type three forward slashes, Visual Studio automatically inserts the XML elements.</span></span> <span data-ttu-id="d9511-155">然后你可以填写中的空格。</span><span class="sxs-lookup"><span data-stu-id="d9511-155">Then you can fill in the blanks.</span></span>


<span data-ttu-id="d9511-156">现在生成和运行一次，应用程序并导航到的帮助页。</span><span class="sxs-lookup"><span data-stu-id="d9511-156">Now build and run the application again, and navigate to the help pages.</span></span> <span data-ttu-id="d9511-157">文档字符串应出现在 API 表中。</span><span class="sxs-lookup"><span data-stu-id="d9511-157">The documentation strings should appear in the API table.</span></span>

![](creating-api-help-pages/_static/image8.png)

<span data-ttu-id="d9511-158">帮助页读取 XML 文件在运行时的字符串。</span><span class="sxs-lookup"><span data-stu-id="d9511-158">The help page reads the strings from the XML file at run time.</span></span> <span data-ttu-id="d9511-159">（在部署应用程序时，请确保部署的 XML 文件。）</span><span class="sxs-lookup"><span data-stu-id="d9511-159">(When you deploy the application, make sure to deploy the XML file.)</span></span>

## <a name="under-the-hood"></a><span data-ttu-id="d9511-160">揭秘</span><span class="sxs-lookup"><span data-stu-id="d9511-160">Under the Hood</span></span>

<span data-ttu-id="d9511-161">帮助页的顶部生成**ApiExplorer**类，该类是 Web API framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="d9511-161">The help pages are built on top of the **ApiExplorer** class, which is part of the Web API framework.</span></span> <span data-ttu-id="d9511-162">**ApiExplorer**类提供了原材料创建帮助页。</span><span class="sxs-lookup"><span data-stu-id="d9511-162">The **ApiExplorer** class provides the raw material for creating a help page.</span></span> <span data-ttu-id="d9511-163">对于每个 API， **ApiExplorer**包含**ApiDescription**介绍 API。</span><span class="sxs-lookup"><span data-stu-id="d9511-163">For each API, **ApiExplorer** contains an **ApiDescription** that describes the API.</span></span> <span data-ttu-id="d9511-164">为此目的，"API"被指 HTTP 方法和相对 URI 的组合。</span><span class="sxs-lookup"><span data-stu-id="d9511-164">For this purpose, an "API" is defined as the combination of HTTP method and relative URI.</span></span> <span data-ttu-id="d9511-165">例如，下面是一些不同的 Api:</span><span class="sxs-lookup"><span data-stu-id="d9511-165">For example, here are some distinct APIs:</span></span>

- <span data-ttu-id="d9511-166">获取 /api/Products</span><span class="sxs-lookup"><span data-stu-id="d9511-166">GET /api/Products</span></span>
- <span data-ttu-id="d9511-167">获取 /api/产品 / {id}</span><span class="sxs-lookup"><span data-stu-id="d9511-167">GET /api/Products/{id}</span></span>
- <span data-ttu-id="d9511-168">发布/api/产品</span><span class="sxs-lookup"><span data-stu-id="d9511-168">POST /api/Products</span></span>

<span data-ttu-id="d9511-169">如果控制器操作支持多个 HTTP 方法， **ApiExplorer**每种方法将其视为不同的 API。</span><span class="sxs-lookup"><span data-stu-id="d9511-169">If a controller action supports multiple HTTP methods, the **ApiExplorer** treats each method as a distinct API.</span></span>

<span data-ttu-id="d9511-170">若要隐藏的 API **ApiExplorer**，添加**ApiExplorerSettings**属性设为操作和组*IgnoreApi*为 true。</span><span class="sxs-lookup"><span data-stu-id="d9511-170">To hide an API from the **ApiExplorer**, add the **ApiExplorerSettings** attribute to the action and set *IgnoreApi* to true.</span></span>

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

<span data-ttu-id="d9511-171">你还可以向控制器，以排除整个控制器中添加此属性。</span><span class="sxs-lookup"><span data-stu-id="d9511-171">You can also add this attribute to the controller, to exclude the entire controller.</span></span>

<span data-ttu-id="d9511-172">ApiExplorer 类获取从文档字符串**IDocumentationProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="d9511-172">The ApiExplorer class gets documentation strings from the **IDocumentationProvider** interface.</span></span> <span data-ttu-id="d9511-173">如前面看到的帮助页库提供了**IDocumentationProvider** ，从 XML 文档字符串获取文档。</span><span class="sxs-lookup"><span data-stu-id="d9511-173">As you saw earlier, the Help Pages library provides an **IDocumentationProvider** that gets documentation from XML documentation strings.</span></span> <span data-ttu-id="d9511-174">代码位于 /Areas/HelpPage/XmlDocumentationProvider.cs。</span><span class="sxs-lookup"><span data-stu-id="d9511-174">The code is located in /Areas/HelpPage/XmlDocumentationProvider.cs.</span></span> <span data-ttu-id="d9511-175">你可以获取文档从其他源通过编写您自己**IDocumentationProvider**。</span><span class="sxs-lookup"><span data-stu-id="d9511-175">You can get documentation from another source by writing your own **IDocumentationProvider**.</span></span> <span data-ttu-id="d9511-176">若要连接它，调用**SetDocumentationProvider**中定义的扩展方法**HelpPageConfigurationExtensions**</span><span class="sxs-lookup"><span data-stu-id="d9511-176">To wire it up, call the **SetDocumentationProvider** extension method, defined in **HelpPageConfigurationExtensions**</span></span>

<span data-ttu-id="d9511-177">**ApiExplorer**自动调入**IDocumentationProvider**接口可以获取每个 API 文档字符串。</span><span class="sxs-lookup"><span data-stu-id="d9511-177">**ApiExplorer** automatically calls into the **IDocumentationProvider** interface to get documentation strings for each API.</span></span> <span data-ttu-id="d9511-178">它将它们存储在**文档**属性**ApiDescription**和**ApiParameterDescription**对象。</span><span class="sxs-lookup"><span data-stu-id="d9511-178">It stores them in the **Documentation** property of the **ApiDescription** and **ApiParameterDescription** objects.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9511-179">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d9511-179">Next Steps</span></span>

<span data-ttu-id="d9511-180">你不限于使用此处显示的帮助页。</span><span class="sxs-lookup"><span data-stu-id="d9511-180">You aren't limited to the help pages shown here.</span></span> <span data-ttu-id="d9511-181">事实上， **ApiExplorer**并不局限于创建帮助页。</span><span class="sxs-lookup"><span data-stu-id="d9511-181">In fact, **ApiExplorer** is not limited to creating help pages.</span></span> <span data-ttu-id="d9511-182">钥 Huang 链接具有写入一些出色的博客文章可帮助你想在初始状态：</span><span class="sxs-lookup"><span data-stu-id="d9511-182">Yao Huang Lin has written some great blog posts to get you thinking out of the box:</span></span>

- [<span data-ttu-id="d9511-183">将一个简单的测试客户端添加到 ASP.NET Web API 帮助页</span><span class="sxs-lookup"><span data-stu-id="d9511-183">Adding a simple Test Client to ASP.NET Web API Help Page</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [<span data-ttu-id="d9511-184">使 ASP.NET Web API 帮助页在自承载服务上工作</span><span class="sxs-lookup"><span data-stu-id="d9511-184">Making ASP.NET Web API Help Page work on self-hosted services</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [<span data-ttu-id="d9511-185">设计时生成的 ASP.NET Web API 的帮助页 （或客户端）</span><span class="sxs-lookup"><span data-stu-id="d9511-185">Design-time generation of help page (or client) for ASP.NET Web API</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [<span data-ttu-id="d9511-186">高级帮助页自定义项</span><span class="sxs-lookup"><span data-stu-id="d9511-186">Advanced Help Page customizations</span></span>](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
