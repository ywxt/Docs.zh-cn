---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 创建一个新的 ASP.NET MVC 项目 |Microsoft Docs
author: microsoft
description: 步骤 1 说明了如何制定基本 NerdDinner 应用程序结构。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 3f34f17aa35dbfed2d52daf615c8dc81be6e7847
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825813"
---
<a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="f839b-103">创建一个新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="f839b-103">Create a New ASP.NET MVC Project</span></span>
====================
<span data-ttu-id="f839b-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="f839b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="f839b-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="f839b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="f839b-106">这是一种免费的步骤 1 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f839b-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="f839b-107">步骤 1 说明了如何制定基本 NerdDinner 应用程序结构。</span><span class="sxs-lookup"><span data-stu-id="f839b-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="f839b-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="f839b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="f839b-109">NerdDinner 步骤 1： 文件-&gt;新项目</span><span class="sxs-lookup"><span data-stu-id="f839b-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="f839b-110">我们将首先选择我们 NerdDinner 的应用程序**文件-&gt;新建项目**Visual Studio 2008 或免费的 Visual Web Developer 2008 Express 中的菜单项。</span><span class="sxs-lookup"><span data-stu-id="f839b-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="f839b-111">这将显示"新建项目"对话框。</span><span class="sxs-lookup"><span data-stu-id="f839b-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="f839b-112">若要创建新的 ASP.NET MVC 应用程序，我们将选择对话框左侧的"Web"节点，然后选择右侧"ASP.NET MVC Web 应用程序"项目模板：</span><span class="sxs-lookup"><span data-stu-id="f839b-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="f839b-113">*重要说明： 请确保已下载并安装 ASP.NET MVC-否则为它不会显示在新建项目对话框。可以使用的 V2 [Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)如果您尚未安装程序 (ASP.NET MVC 是中提供"Web 平台的&gt;框架和运行时"部分)。*</span><span class="sxs-lookup"><span data-stu-id="f839b-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="f839b-114">我们将的项目命名为新我们要创建"NerdDinner"，然后单击"确定"按钮以创建它。</span><span class="sxs-lookup"><span data-stu-id="f839b-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="f839b-115">当我们单击"确定"时 Visual Studio 将显示其他对话框，提示我们根据需要创建新应用程序的单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="f839b-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="f839b-116">此单元测试项目使我们能够创建自动的测试以验证功能和我们的应用程序的行为 (我们将介绍的内容如何更高版本在本教程中的待办事项)。</span><span class="sxs-lookup"><span data-stu-id="f839b-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="f839b-117">上面的对话框中的"测试框架"下拉列表会填充所有可用 ASP.NET MVC 单元测试项目模板在计算机上安装。</span><span class="sxs-lookup"><span data-stu-id="f839b-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="f839b-118">可以为 NUnit、 MBUnit 和 XUnit 下载版本。</span><span class="sxs-lookup"><span data-stu-id="f839b-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="f839b-119">也支持内置的 Visual Studio 单元测试框架。</span><span class="sxs-lookup"><span data-stu-id="f839b-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="f839b-120">*注意： Visual Studio 单元测试框架才可用于 Visual Studio 2008 Professional 和更高版本。如果你使用 VS 2008 Standard Edition 或 Visual Web Developer 2008 Express 需要先下载并安装 NUnit、 MBUnit 或 XUnit 扩展为 ASP.NET MVC 中要显示此对话框的顺序。如果没有安装任何测试框架，不会显示该对话框。*</span><span class="sxs-lookup"><span data-stu-id="f839b-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="f839b-121">我们将使用我们创建的测试项目的默认"NerdDinner.Tests"名称，并使用"Visual Studio 单元测试"框架选项。</span><span class="sxs-lookup"><span data-stu-id="f839b-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="f839b-122">当我们单击 Visual Studio 的"确定"按钮将具有两个项目中的一个 web 应用程序，以进行单元测试的另一个为我们创建一个解决方案：</span><span class="sxs-lookup"><span data-stu-id="f839b-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="f839b-123">检查 NerdDinner 目录结构</span><span class="sxs-lookup"><span data-stu-id="f839b-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="f839b-124">当使用 Visual Studio 创建新的 ASP.NET MVC 应用程序时，它自动将大量文件和目录添加到项目：</span><span class="sxs-lookup"><span data-stu-id="f839b-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="f839b-125">默认情况下的 ASP.NET MVC 项目具有六个顶级目录：</span><span class="sxs-lookup"><span data-stu-id="f839b-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="f839b-126">**目录**</span><span class="sxs-lookup"><span data-stu-id="f839b-126">**Directory**</span></span> | <span data-ttu-id="f839b-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="f839b-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="f839b-128">**/ 控制器**</span><span class="sxs-lookup"><span data-stu-id="f839b-128">**/Controllers**</span></span> | <span data-ttu-id="f839b-129">处理 URL 请求的控制器类的放置位置</span><span class="sxs-lookup"><span data-stu-id="f839b-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="f839b-130">**/ 模型**</span><span class="sxs-lookup"><span data-stu-id="f839b-130">**/Models**</span></span> | <span data-ttu-id="f839b-131">类表示和操作数据的放置位置</span><span class="sxs-lookup"><span data-stu-id="f839b-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="f839b-132">**/ 视图**</span><span class="sxs-lookup"><span data-stu-id="f839b-132">**/Views**</span></span> | <span data-ttu-id="f839b-133">负责呈现输出的 UI 模板文件的放置位置</span><span class="sxs-lookup"><span data-stu-id="f839b-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="f839b-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="f839b-134">**/Scripts**</span></span> | <span data-ttu-id="f839b-135">JavaScript 库文件和脚本 (.js) 的放置位置</span><span class="sxs-lookup"><span data-stu-id="f839b-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="f839b-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="f839b-136">**/Content**</span></span> | <span data-ttu-id="f839b-137">CSS 和图像文件和其他非动态/非-JavaScript 内容的放置位置</span><span class="sxs-lookup"><span data-stu-id="f839b-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="f839b-138">**/ 应用\_数据**</span><span class="sxs-lookup"><span data-stu-id="f839b-138">**/App\_Data**</span></span> | <span data-ttu-id="f839b-139">存储数据文件在你想要读/写。</span><span class="sxs-lookup"><span data-stu-id="f839b-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="f839b-140">ASP.NET MVC 不需要此结构。</span><span class="sxs-lookup"><span data-stu-id="f839b-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="f839b-141">事实上，在大型应用程序上工作的开发人员将通常对应用程序分区注册跨多个项目，以使其更易于管理 (例如： 数据通常模型类可以在一个单独的类库项目中从 web 应用程序)。</span><span class="sxs-lookup"><span data-stu-id="f839b-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="f839b-142">默认项目结构，但是，提供可用于保留我们的应用程序主要关注干净的很好的默认目录约定。</span><span class="sxs-lookup"><span data-stu-id="f839b-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="f839b-143">当我们展开 /Controllers 目录我们会发现 Visual Studio 添加默认情况下两个控制器类 – HomeController 和 AccountController – 到项目：</span><span class="sxs-lookup"><span data-stu-id="f839b-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="f839b-144">当我们展开 /Views 目录时，我们会发现三个子目录 – /Home、 /Account /Shared – 以及其中的文件也默认情况下添加到项目的多个模板：</span><span class="sxs-lookup"><span data-stu-id="f839b-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="f839b-145">当我们展开 /Content 和 /Scripts 目录时，我们会发现用于设置所有 HTML 都样式在站点上的 Site.css 文件，以及可以启用 ASP.NET AJAX 和 jQuery JavaScript 库支持应用程序中：</span><span class="sxs-lookup"><span data-stu-id="f839b-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="f839b-146">我们展开 NerdDinner.Tests 项目时，我们将会包含单元测试为控制器类的两个类：</span><span class="sxs-lookup"><span data-stu-id="f839b-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="f839b-147">运行的应用程序的完成，但主页上，有关页、 帐户注册/注销/登录信息页和 （所有连接和现成的工作） 的未处理的错误页面中，由 Visual Studio 添加这些默认文件向我们提供的基本结构。</span><span class="sxs-lookup"><span data-stu-id="f839b-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="f839b-148">运行 NerdDinner 应用程序</span><span class="sxs-lookup"><span data-stu-id="f839b-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="f839b-149">我们可以通过选择运行该项目**调试-&gt;启动调试**或**调试-&gt;启动但不调试**菜单项：</span><span class="sxs-lookup"><span data-stu-id="f839b-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="f839b-150">这将启动内置 ASP.NET Web 服务器随附 Visual Studio 中，并运行我们的应用程序：</span><span class="sxs-lookup"><span data-stu-id="f839b-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="f839b-151">下面是我们的新项目的主页 (URL:"/") 运行时：</span><span class="sxs-lookup"><span data-stu-id="f839b-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="f839b-152">单击"关于"选项卡显示有关页面 (URL:"/ Home/关于"):</span><span class="sxs-lookup"><span data-stu-id="f839b-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="f839b-153">单击右上角的"登录"链接将我们带到登录页 (URL:"/ 帐户/登录")</span><span class="sxs-lookup"><span data-stu-id="f839b-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="f839b-154">如果我们还没有登录帐户，我们可以单击注册链接 (URL:"/ 帐户/注册") 创建一个：</span><span class="sxs-lookup"><span data-stu-id="f839b-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="f839b-155">有关，实现上述主页、 代码和注销 / 注册功能默认情况下创建新项目时添加。</span><span class="sxs-lookup"><span data-stu-id="f839b-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="f839b-156">我们将使用它作为我们的应用程序的起始点。</span><span class="sxs-lookup"><span data-stu-id="f839b-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="f839b-157">测试 NerdDinner 应用程序</span><span class="sxs-lookup"><span data-stu-id="f839b-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="f839b-158">如果我们使用专业版或更高版本的 Visual Studio 2008，我们可以使用内置测试 Visual Studio 中的 IDE 支持的单元测试项目：</span><span class="sxs-lookup"><span data-stu-id="f839b-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="f839b-159">选择上述选项之一，将打开"测试结果"窗格中的，在 IDE 中，并向我们提供我们新的项目中包含的、 介绍内置功能 27 单元测试的通过/失败状态：</span><span class="sxs-lookup"><span data-stu-id="f839b-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="f839b-160">本教程中稍后我们将详细介绍自动测试，并添加其他单元测试以涵盖应用程序功能，我们实现。</span><span class="sxs-lookup"><span data-stu-id="f839b-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="f839b-161">下一步</span><span class="sxs-lookup"><span data-stu-id="f839b-161">Next Step</span></span>

<span data-ttu-id="f839b-162">我们在位置现在有一个基本的应用程序结构。</span><span class="sxs-lookup"><span data-stu-id="f839b-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="f839b-163">让我们现在[创建一个数据库来存储应用程序数据](create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="f839b-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f839b-164">[上一页](introducing-the-nerddinner-tutorial.md)
> [下一页](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="f839b-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
