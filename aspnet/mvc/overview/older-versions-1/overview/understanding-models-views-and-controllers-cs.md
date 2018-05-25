---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: 了解模型、 视图和控制器 (C#) |Microsoft 文档
author: StephenWalther
description: 感到迷惑的模型、 视图和控制器？ 在本教程中，Stephen Walther 引入你对 ASP.NET MVC 应用程序的不同部分。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c9a0cbbf6f786944d7892fbb14859939f21bdd5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
---
<a name="understanding-models-views-and-controllers-c"></a><span data-ttu-id="ac1e9-104">了解模型、 视图和控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-104">Understanding Models, Views, and Controllers (C#)</span></span>
====================
<span data-ttu-id="ac1e9-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="ac1e9-106">感到迷惑的模型、 视图和控制器？</span><span class="sxs-lookup"><span data-stu-id="ac1e9-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="ac1e9-107">在本教程中，Stephen Walther 引入你对 ASP.NET MVC 应用程序的不同部分。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>


<span data-ttu-id="ac1e9-108">本教程提供与 ASP.NET MVC 的高级概述模型、 视图和控制器也是如此。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="ac1e9-109">换而言之，它还说明了 M，V，和 C 在 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="ac1e9-110">在阅读本教程后，你应该了解 ASP.NET MVC 应用程序的不同部分如何协同工作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="ac1e9-111">您还应了解 ASP.NET MVC 应用程序的体系结构有何不同从 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="ac1e9-112">示例 ASP.NET MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="ac1e9-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="ac1e9-113">用于创建 ASP.NET MVC Web 应用程序的默认 Visual Studio 模板包括可用于了解 ASP.NET MVC 应用程序的不同部分的极其简单的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="ac1e9-114">我们充分利用在本教程中此简单应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="ac1e9-115">使用 MVC 模板中启动 Visual Studio 2008 创建了新的 ASP.NET MVC 应用程序并选择文件菜单选项，新建项目 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="ac1e9-116">在新建项目对话框中，选择您最喜欢的编程语言，在项目类型 （Visual Basic 或 C#） 下，选择**ASP.NET MVC Web 应用程序**下模板。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="ac1e9-117">单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-117">Click the OK button.</span></span>


<span data-ttu-id="ac1e9-118">[![新建项目对话框](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-118">[![New Project Dialog](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span></span>

<span data-ttu-id="ac1e9-119">**图 01**: 新建项目对话框 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="ac1e9-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image2.png))</span></span>


<span data-ttu-id="ac1e9-120">当你创建一个新的 ASP.NET MVC 应用程序，**创建单元测试项目**对话框 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="ac1e9-121">此对话框使你可以在测试 ASP.NET MVC 应用程序解决方案中创建一个单独的项目。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="ac1e9-122">选择选项**否，不创建单元测试项目**单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>


<span data-ttu-id="ac1e9-123">[![创建单元测试对话框](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span></span>

<span data-ttu-id="ac1e9-124">**图 02**： 创建单元测试对话框 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="ac1e9-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image4.png))</span></span>


<span data-ttu-id="ac1e9-125">创建后新的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="ac1e9-126">你将看到几个文件夹和解决方案资源管理器窗口中的文件。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="ac1e9-127">具体而言，你将看到名为模型、 视图和控制器的三个文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="ac1e9-128">您可能已经猜到的文件夹名称，这些文件夹包含用于实现模型、 视图和控制器的文件。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="ac1e9-129">如果你展开 Controllers 文件夹，你应看到一个名为 AccountController.cs 文件和一个名为 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-129">If you expand the Controllers folder, you should see a file named AccountController.cs and a file named HomeController.cs.</span></span> <span data-ttu-id="ac1e9-130">如果展开视图文件夹，你应看到三个名为帐户，主页和共享的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="ac1e9-131">如果您展开主文件夹，你将看到名为 About.aspx 和 Index.aspx （请参见图 3） 的两个其他文件。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="ac1e9-132">这些文件构成了默认的 ASP.NET MVC 模板中包含的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>


<span data-ttu-id="ac1e9-133">[![解决方案资源管理器窗口](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span></span>

<span data-ttu-id="ac1e9-134">**图 03**： 的解决方案资源管理器窗口 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="ac1e9-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image6.png))</span></span>


<span data-ttu-id="ac1e9-135">你可以通过选择菜单选项来运行示例应用程序**调试、 启动调试**。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="ac1e9-136">或者，你可以按 F5 键。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="ac1e9-137">当你首次运行 ASP.NET 应用程序时，此时将显示在图 4 对话框，建议你启用调试模式。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="ac1e9-138">单击确定按钮，然后运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-138">Click the OK button and the application will run.</span></span>


<span data-ttu-id="ac1e9-139">[![调试未启用对话框](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span></span>

<span data-ttu-id="ac1e9-140">**图 04**： 未启用调试对话框 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="ac1e9-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image8.png))</span></span>


<span data-ttu-id="ac1e9-141">当你运行的 ASP.NET MVC 应用程序时，Visual Studio 将启动 web 浏览器中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="ac1e9-142">示例应用程序只有两个页组成： 索引页和关于页面。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="ac1e9-143">当第一次启动应用程序时，索引页面显示 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="ac1e9-144">你可以通过单击顶部的菜单链接导航到关于页面右侧的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>


<span data-ttu-id="ac1e9-145">[![索引页面](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ac1e9-145">[![The Index Page](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span></span>

<span data-ttu-id="ac1e9-146">**图 05**: 索引页 ([单击以查看实际尺寸的图像](understanding-models-views-and-controllers-cs/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="ac1e9-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image11.png))</span></span>


<span data-ttu-id="ac1e9-147">请注意您的浏览器的地址栏中的 Url。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="ac1e9-148">例如，当你单击关于菜单链接时，浏览器地址栏中的 URL 更改为 **/Home/有关**。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="ac1e9-149">如果你关闭浏览器窗口，并返回到 Visual Studio，你将无法使用路径主页 / 关于查找的文件。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="ac1e9-150">文件不存在。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-150">The files don't exist.</span></span> <span data-ttu-id="ac1e9-151">如何这是可能的？</span><span class="sxs-lookup"><span data-stu-id="ac1e9-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="ac1e9-152">URL 不等于页</span><span class="sxs-lookup"><span data-stu-id="ac1e9-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="ac1e9-153">传统的 ASP.NET Web 窗体应用程序或 Active Server Pages 应用程序生成时，没有一个 URL，另一个页面之间的一一对应关系。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="ac1e9-154">如果请求一个名为从服务器的 SomePage.aspx 页，然后有具有更好地能页在磁盘上名为 SomePage.aspx。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="ac1e9-155">如果 SomePage.aspx 文件不存在，则获取极差**404-找不到页面**错误。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="ac1e9-156">在生成 ASP.NET MVC 应用程序时，与此相反，你的浏览器地址栏中键入 URL 和应用程序中查找的文件之间没有对应关系。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="ac1e9-157">在 ASP.NET MVC 应用程序 URL 对应于而不是在磁盘上页面的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="ac1e9-158">在传统 ASP.NET 或 ASP 应用程序中，浏览器请求将映射到页。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="ac1e9-159">在 ASP.NET MVC 应用程序，与此相反，浏览器请求将映射到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="ac1e9-160">ASP.NET Web 窗体应用程序是以内容为中心。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="ac1e9-161">ASP.NET MVC 应用程序与此相反，是以为中心的应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="ac1e9-162">了解 ASP.NET 路由</span><span class="sxs-lookup"><span data-stu-id="ac1e9-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="ac1e9-163">浏览器请求获取映射到通过一项功能的 ASP.NET 框架调用的控制器操作*ASP.NET 路由*。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="ac1e9-164">ASP.NET 路由使用 ASP.NET MVC framework*路由*到控制器操作的传入请求。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="ac1e9-165">ASP.NET 路由使用路由表来处理传入请求。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="ac1e9-166">Web 应用程序首次启动时创建此路由表。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="ac1e9-167">路由表是在 Global.asax 文件中的安装程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="ac1e9-168">默认 MVC Global.asax 文件包含在清单 1。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="ac1e9-169">**列表 1-Global.asax**</span><span class="sxs-lookup"><span data-stu-id="ac1e9-169">**Listing 1 - Global.asax**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

<span data-ttu-id="ac1e9-170">当 ASP.NET 应用程序第一次启动时，应用程序\_调用 start （） 方法。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="ac1e9-171">在列出 1 中，此方法调用 RegisterRoutes() 方法和 RegisterRoutes() 方法创建的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="ac1e9-172">默认路由表都包含一个路由。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-172">The default route table consists of one route.</span></span> <span data-ttu-id="ac1e9-173">此默认路由分成三个段 （URL 段是正斜杠之间的任何内容） 的所有传入请求。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="ac1e9-174">第一条线段映射到的控制器名称、 第二个段映射到操作名称，和最后一个段映射到传递到名为 id。 操作的参数</span><span class="sxs-lookup"><span data-stu-id="ac1e9-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="ac1e9-175">例如，考虑以下 URL:</span><span class="sxs-lookup"><span data-stu-id="ac1e9-175">For example, consider the following URL:</span></span>

<span data-ttu-id="ac1e9-176">/ 产品/详细信息/3</span><span class="sxs-lookup"><span data-stu-id="ac1e9-176">/Product/Details/3</span></span>

<span data-ttu-id="ac1e9-177">此 URL 解析为三个参数如下：</span><span class="sxs-lookup"><span data-stu-id="ac1e9-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="ac1e9-178">控制器 = 产品</span><span class="sxs-lookup"><span data-stu-id="ac1e9-178">Controller = Product</span></span>

<span data-ttu-id="ac1e9-179">操作 = 详细信息</span><span class="sxs-lookup"><span data-stu-id="ac1e9-179">Action = Details</span></span>

<span data-ttu-id="ac1e9-180">id = 3</span><span class="sxs-lookup"><span data-stu-id="ac1e9-180">Id = 3</span></span>

<span data-ttu-id="ac1e9-181">在 Global.asax 文件中定义的默认路由包括所有三个参数的默认值。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="ac1e9-182">默认值控制器是主页、 默认操作是索引，和默认 Id 为空字符串。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="ac1e9-183">记住这些默认值，应考虑以下 URL 的分析方式：</span><span class="sxs-lookup"><span data-stu-id="ac1e9-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="ac1e9-184">/ 员工</span><span class="sxs-lookup"><span data-stu-id="ac1e9-184">/Employee</span></span>

<span data-ttu-id="ac1e9-185">此 URL 解析为三个参数如下：</span><span class="sxs-lookup"><span data-stu-id="ac1e9-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="ac1e9-186">控制器 = 员工</span><span class="sxs-lookup"><span data-stu-id="ac1e9-186">Controller = Employee</span></span>

<span data-ttu-id="ac1e9-187">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="ac1e9-187">Action = Index</span></span>

<span data-ttu-id="ac1e9-188">Id =</span><span class="sxs-lookup"><span data-stu-id="ac1e9-188">Id = ��</span></span>

<span data-ttu-id="ac1e9-189">最后，如果你打开 ASP.NET MVC 应用程序而无需提供任何 URL (例如， `http://localhost`)，则将 URL 解析如下：</span><span class="sxs-lookup"><span data-stu-id="ac1e9-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="ac1e9-190">控制器 = 主页</span><span class="sxs-lookup"><span data-stu-id="ac1e9-190">Controller = Home</span></span>

<span data-ttu-id="ac1e9-191">操作 = 索引</span><span class="sxs-lookup"><span data-stu-id="ac1e9-191">Action = Index</span></span>

<span data-ttu-id="ac1e9-192">Id =</span><span class="sxs-lookup"><span data-stu-id="ac1e9-192">Id = ��</span></span>

<span data-ttu-id="ac1e9-193">请求路由到 HomeController 类上的 index （） 操作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="ac1e9-194">了解控制器</span><span class="sxs-lookup"><span data-stu-id="ac1e9-194">Understanding Controllers</span></span>

<span data-ttu-id="ac1e9-195">控制器负责控制用户与 MVC 应用程序交互的方式。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="ac1e9-196">控制器包含一个 ASP.NET MVC 应用程序的流控制逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="ac1e9-197">控制器将确定哪些响应，以便当用户进行浏览器请求将发送回用户。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="ac1e9-198">控制器是只是一个类 （例如，Visual Basic 或 C# 类）。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="ac1e9-199">此示例 ASP.NET MVC 应用程序包含名为 HomeController.cs 控制器文件夹中的控制器。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-199">The sample ASP.NET MVC application includes a controller named HomeController.cs located in the Controllers folder.</span></span> <span data-ttu-id="ac1e9-200">HomeController.cs 文件的内容将列出 2 中重现。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-200">The content of the HomeController.cs file is reproduced in Listing 2.</span></span>

<span data-ttu-id="ac1e9-201">**列出 2-HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="ac1e9-201">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

<span data-ttu-id="ac1e9-202">请注意，HomeController 命名 index （） 和 About() 的两个方法。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="ac1e9-203">这两种方法对应于在控制器公开的两个操作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="ac1e9-204">URL /Home/索引调用 HomeController.Index() 方法和 URL /Home/About 调用 HomeController.About() 方法。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="ac1e9-205">控制器中的任何公共方法公开为控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="ac1e9-206">你需要有关此谨慎。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-206">You need to be careful about this.</span></span> <span data-ttu-id="ac1e9-207">这意味着控制器中包含任何公共方法可由有权访问 Internet 的任何人都调用通过在浏览器中输入正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="ac1e9-208">了解视图</span><span class="sxs-lookup"><span data-stu-id="ac1e9-208">Understanding Views</span></span>

<span data-ttu-id="ac1e9-209">由 HomeController 类，index （） 和 About()，公开的两个控制器操作两者都返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="ac1e9-210">视图包含的 HTML 标记和发送到浏览器的内容。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="ac1e9-211">使用 ASP.NET MVC 应用程序时，视图是单页的等效项。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="ac1e9-212">必须在正确的位置中创建你的视图。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-212">You must create your views in the right location.</span></span> <span data-ttu-id="ac1e9-213">HomeController.Index() 操作返回位于以下路径下的视图：</span><span class="sxs-lookup"><span data-stu-id="ac1e9-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="ac1e9-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="ac1e9-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="ac1e9-215">HomeController.About() 操作返回位于以下路径下的视图：</span><span class="sxs-lookup"><span data-stu-id="ac1e9-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="ac1e9-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="ac1e9-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="ac1e9-217">一般情况下，如果你想要返回的控制器操作的视图，然后你需要在与你的控制器同名的 Views 文件夹中创建一个子文件夹。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="ac1e9-218">在子文件夹，必须使用与控制器操作相同的名称来创建一个.aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="ac1e9-219">列出 3 中的文件包含 About.aspx 视图。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="ac1e9-220">**列出 3-About.aspx**</span><span class="sxs-lookup"><span data-stu-id="ac1e9-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

<span data-ttu-id="ac1e9-221">如果您忽略列出 3 中的第一行，大部分视图的其余部分由标准 HTML 组成。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="ac1e9-222">可以通过输入你想此处任何 HTML 来修改视图的内容。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="ac1e9-223">视图是非常类似于 Active Server Pages 或 ASP.NET Web 窗体中的页。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="ac1e9-224">视图可以包含 HTML 内容和脚本。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="ac1e9-225">你可以编写的脚本中你最喜欢的.NET 编程语言 (例如，C# 或 Visual Basic.NET）。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="ac1e9-226">您可以使用脚本来显示如数据库数据的动态内容。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="ac1e9-227">了解模型</span><span class="sxs-lookup"><span data-stu-id="ac1e9-227">Understanding Models</span></span>

<span data-ttu-id="ac1e9-228">我们已经讨论了控制器和我们已经讨论了视图。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="ac1e9-229">我们需要讨论的最后一个主题是模型。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="ac1e9-230">MVC 模型是什么？</span><span class="sxs-lookup"><span data-stu-id="ac1e9-230">What is an MVC model?</span></span>

<span data-ttu-id="ac1e9-231">MVC 模型包含所有未包含在视图或控制器你应用程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="ac1e9-232">此模型应包含的所有应用程序业务逻辑、 验证逻辑和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="ac1e9-233">例如，如果你使用 Microsoft 实体框架访问你的数据库，然后你将你 Entity Framework 类 （您的.edmx 文件） 的文件夹中创建模型。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="ac1e9-234">视图应包含仅与生成的用户界面相关的逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="ac1e9-235">控制器应仅包含逻辑返回右视图或将用户重定向到另一项操作 （流控制） 所需的最低的要求。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="ac1e9-236">该模型中，应包含其他任何内容。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="ac1e9-237">一般情况下，也应尽可能 fat 模型和小控制器。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="ac1e9-238">控制器方法应包含只几行代码。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="ac1e9-239">如果控制器操作获取太 fat，则应考虑通过将逻辑移动到 Models 文件夹中的新类。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="ac1e9-240">摘要</span><span class="sxs-lookup"><span data-stu-id="ac1e9-240">Summary</span></span>

<span data-ttu-id="ac1e9-241">本教程向您提供的高级别概述的不同部分的 ASP.NET MVC web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="ac1e9-242">你已了解如何 ASP.NET 路由传入浏览器将请求映射到特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="ac1e9-243">你已了解如何控制器安排如何将视图返回到浏览器。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="ac1e9-244">最后，您学习了如何模型包含应用程序业务、 验证和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="ac1e9-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>
