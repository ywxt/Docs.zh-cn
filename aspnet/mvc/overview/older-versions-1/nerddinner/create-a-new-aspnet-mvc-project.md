---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: "创建新的 ASP.NET MVC 项目 |Microsoft 文档"
author: microsoft
description: "步骤 1 演示了如何将基本 NerdDinner 应用程序结构放在位置。"
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 4d30a6803b1478014a2afb814ac317df27394446
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
<a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="ba698-103">创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="ba698-103">Create a New ASP.NET MVC Project</span></span>
====================
<span data-ttu-id="ba698-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ba698-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="ba698-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="ba698-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="ba698-106">这是一个免费的第 1 步["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ba698-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="ba698-107">步骤 1 演示了如何将基本 NerdDinner 应用程序结构放在位置。</span><span class="sxs-lookup"><span data-stu-id="ba698-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="ba698-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="ba698-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="ba698-109">NerdDinner 步骤 1： 文件-&gt;新项目</span><span class="sxs-lookup"><span data-stu-id="ba698-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="ba698-110">我们将首先我们 NerdDinner 的应用程序通过选择**文件-&gt;新项目**Visual Studio 2008 或可用 Visual Web Developer 2008 速成版中的菜单项。</span><span class="sxs-lookup"><span data-stu-id="ba698-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="ba698-111">这将显示"新建项目"对话框。</span><span class="sxs-lookup"><span data-stu-id="ba698-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="ba698-112">若要创建新的 ASP.NET MVC 应用程序，我们选择对话框左侧的"Web"节点，然后选择右侧的"ASP.NET MVC Web 应用程序"项目模板：</span><span class="sxs-lookup"><span data-stu-id="ba698-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="ba698-113">*重要说明： 请确保你已下载并安装 ASP.NET MVC-否则为它不会显示在新项目对话框。你可以使用的 V2 [Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)如果您尚未安装程序 (ASP.NET MVC 内可用时"Web 平台-&gt;框架和运行时"部分)。*</span><span class="sxs-lookup"><span data-stu-id="ba698-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="ba698-114">我们将将新的项目，我们将创建"NerdDinner"，然后单击"确定"按钮创建它。</span><span class="sxs-lookup"><span data-stu-id="ba698-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="ba698-115">当我们单击"确定"Visual Studio 将显示其他对话框，提示我们可以根据需要创建新应用程序的单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="ba698-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="ba698-116">此单元测试项目使我们能够创建验证的功能和行为的我们的应用程序的自动的测试 (我们将介绍的内容如何更高版本在本教程中的待办事项)。</span><span class="sxs-lookup"><span data-stu-id="ba698-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="ba698-117">使用所有可用 ASP.NET MVC 单元测试项目模板在计算机上安装，填充中上述对话框的"测试框架"下拉列表。</span><span class="sxs-lookup"><span data-stu-id="ba698-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="ba698-118">可以为 NUnit、 MBUnit 和 XUnit 下载版本。</span><span class="sxs-lookup"><span data-stu-id="ba698-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="ba698-119">也支持内置的 Visual Studio 单元测试框架。</span><span class="sxs-lookup"><span data-stu-id="ba698-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="ba698-120">*注意： Visual Studio 单元测试框架时才可以使用 Visual Studio 2008 专业版和更高版本。如果你正在使用 VS 2008 标准版或 Visual Web Developer 2008 速成版将需要下载并安装针对 ASP.NET MVC NUnit、 MBUnit 或 XUnit 扩展，此对话框显示的顺序。如果没有安装任何测试框架，将不显示对话框。*</span><span class="sxs-lookup"><span data-stu-id="ba698-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="ba698-121">我们将使用我们创建的测试项目的默认"NerdDinner.Tests"名称，然后使用"Visual Studio 单元测试"框架选项。</span><span class="sxs-lookup"><span data-stu-id="ba698-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="ba698-122">当我们单击"正常"按钮 Visual Studio 将创建解决方案为我们具有在其中的一个用于我们的 web 应用程序，一个以进行单元测试的两个项目：</span><span class="sxs-lookup"><span data-stu-id="ba698-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="ba698-123">检查 NerdDinner 目录结构</span><span class="sxs-lookup"><span data-stu-id="ba698-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="ba698-124">当使用 Visual Studio 创建新的 ASP.NET MVC 应用程序时，它会自动将大量的文件和目录添加到项目：</span><span class="sxs-lookup"><span data-stu-id="ba698-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="ba698-125">默认情况下的 ASP.NET MVC 项目具有六个顶级目录：</span><span class="sxs-lookup"><span data-stu-id="ba698-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="ba698-126">**Directory**</span><span class="sxs-lookup"><span data-stu-id="ba698-126">**Directory**</span></span> | <span data-ttu-id="ba698-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="ba698-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="ba698-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="ba698-128">**/Controllers**</span></span> | <span data-ttu-id="ba698-129">处理 URL 请求的控制器类的放置位置</span><span class="sxs-lookup"><span data-stu-id="ba698-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="ba698-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="ba698-130">**/Models**</span></span> | <span data-ttu-id="ba698-131">类表示和操作数据的放置位置</span><span class="sxs-lookup"><span data-stu-id="ba698-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="ba698-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="ba698-132">**/Views**</span></span> | <span data-ttu-id="ba698-133">放置负责呈现输出的 UI 模板文件的位置</span><span class="sxs-lookup"><span data-stu-id="ba698-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="ba698-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="ba698-134">**/Scripts**</span></span> | <span data-ttu-id="ba698-135">JavaScript 库文件和脚本 (.js) 的放置位置</span><span class="sxs-lookup"><span data-stu-id="ba698-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="ba698-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="ba698-136">**/Content**</span></span> | <span data-ttu-id="ba698-137">CSS 和图像文件与其他非-动态/非-JavaScript 内容的放置位置</span><span class="sxs-lookup"><span data-stu-id="ba698-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="ba698-138">**/App\_Data**</span><span class="sxs-lookup"><span data-stu-id="ba698-138">**/App\_Data**</span></span> | <span data-ttu-id="ba698-139">存储数据文件在你想要读/写。</span><span class="sxs-lookup"><span data-stu-id="ba698-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="ba698-140">ASP.NET MVC 不需要此结构。</span><span class="sxs-lookup"><span data-stu-id="ba698-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="ba698-141">事实上，开发人员处理大型应用程序将通常对应用程序分区向上跨多个项目，以使其更易于管理 (例如： 数据模型类通常在一个单独的类库项目中从转 web 应用程序)。</span><span class="sxs-lookup"><span data-stu-id="ba698-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="ba698-142">默认项目结构，但是，提供我们可用于保持我们的应用程序主要关注干净的很好的默认目录约定。</span><span class="sxs-lookup"><span data-stu-id="ba698-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="ba698-143">当我们扩展 /Controllers 目录我们将找到 Visual Studio 添加默认情况下两个控制器类 – HomeController 和 AccountController – 到项目：</span><span class="sxs-lookup"><span data-stu-id="ba698-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="ba698-144">当我们扩展 /Views 目录时，我们将找到三个子目录 – /Home、 /Account /Shared – 以及其中的文件也已按默认添加到项目的多个模板：</span><span class="sxs-lookup"><span data-stu-id="ba698-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="ba698-145">当我们扩展 /Content 和 /Scripts 目录时，我们将找到用于在站点上，设置样式所有 HTML Site.css 文件，以及 JavaScript 库，可以使 ASP.NET AJAX 和 jQuery 支持应用程序中：</span><span class="sxs-lookup"><span data-stu-id="ba698-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="ba698-146">我们展开 NerdDinner.Tests 项目时，我们将会包含我们控制器类的单元测试的两个类：</span><span class="sxs-lookup"><span data-stu-id="ba698-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="ba698-147">为工作应用程序的完成，但主页上，有关页、 帐户注册/注销/登录信息页，和 （所有有线上移和现成的工作） 的未处理的错误页中，由 Visual Studio 添加这些默认文件提供我们的基本结构。</span><span class="sxs-lookup"><span data-stu-id="ba698-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="ba698-148">运行 NerdDinner 应用程序</span><span class="sxs-lookup"><span data-stu-id="ba698-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="ba698-149">我们可以通过选择运行该项目**调试-&gt;启动调试**或**调试-&gt;启动但不调试**菜单项：</span><span class="sxs-lookup"><span data-stu-id="ba698-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="ba698-150">这将启动内置 ASP.NET Web 服务器附带 Visual Studio 中，并运行我们的应用程序：</span><span class="sxs-lookup"><span data-stu-id="ba698-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="ba698-151">下面是我们新的项目的主页 (URL:"/") 运行时：</span><span class="sxs-lookup"><span data-stu-id="ba698-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="ba698-152">单击"关于"选项卡显示有关页面 (URL:"/ Home/有关"):</span><span class="sxs-lookup"><span data-stu-id="ba698-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="ba698-153">单击右上角的"登录"链接，我们将转到登录页 (URL:"/ 帐户/登录")</span><span class="sxs-lookup"><span data-stu-id="ba698-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="ba698-154">如果我们没有登录帐户，我们可以单击注册链接 (URL:"/ 帐户/注册") 创建一个：</span><span class="sxs-lookup"><span data-stu-id="ba698-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="ba698-155">代码以实现更高版本的主页中，有关和注销 / 注册我们创建我们的新项目时，已按默认添加功能。</span><span class="sxs-lookup"><span data-stu-id="ba698-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="ba698-156">我们将使用它作为我们的应用程序的起始点。</span><span class="sxs-lookup"><span data-stu-id="ba698-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="ba698-157">测试 NerdDinner 应用程序</span><span class="sxs-lookup"><span data-stu-id="ba698-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="ba698-158">如果我们使用的专业版或更高版本的 Visual Studio 2008，我们可以使用内置的单元测试在 Visual Studio 中的 IDE 支持测试项目：</span><span class="sxs-lookup"><span data-stu-id="ba698-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="ba698-159">选择上述选项之一，将打开 IDE 中的"测试结果"窗格，并向我们提供的新项目中包括涵盖的内置功能 27 单元测试的通过/失败状态：</span><span class="sxs-lookup"><span data-stu-id="ba698-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="ba698-160">本教程中稍后我们将详细介绍自动测试并添加其他单元测试以涵盖我们实现应用程序功能。</span><span class="sxs-lookup"><span data-stu-id="ba698-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="ba698-161">下一步</span><span class="sxs-lookup"><span data-stu-id="ba698-161">Next Step</span></span>

<span data-ttu-id="ba698-162">我们现在就地提供基本应用程序结构。</span><span class="sxs-lookup"><span data-stu-id="ba698-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="ba698-163">让我们现在[创建一个数据库来存储我们的应用程序数据](create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="ba698-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="ba698-164">[上一页](introducing-the-nerddinner-tutorial.md)
[下一页](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="ba698-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
