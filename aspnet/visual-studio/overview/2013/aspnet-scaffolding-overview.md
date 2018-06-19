---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: 在 Visual Studio 2013 的 ASP.NET 基架 |Microsoft 文档
author: tfitzmac
description: ASP.NET 基架是包含在 Visual Studio 2013 中的新功能。
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/09/2014
ms.topic: article
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: 425983c1ffff6369276f0723a9947a411a4617eb
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26506726"
---
<a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="c1bb7-103">在 Visual Studio 2013 的 ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="c1bb7-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>
====================
<span data-ttu-id="c1bb7-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c1bb7-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c1bb7-105">ASP.NET 基架是包含在 Visual Studio 2013 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>


## <a name="overview"></a><span data-ttu-id="c1bb7-106">概述</span><span class="sxs-lookup"><span data-stu-id="c1bb7-106">Overview</span></span>

<span data-ttu-id="c1bb7-107">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="c1bb7-108">Visual Studio 2013 包含为 MVC 和 Web API 项目的预安装的代码生成器。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="c1bb7-109">当你想要快速添加与数据模型交互的代码时将基架添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="c1bb7-110">使用基架，则可以减少开发项目中的标准数据操作的时间量。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="c1bb7-111">默认情况下，Visual Studio 2013 不支持 Web 窗体项目中，生成代码，但可以通过向项目添加 MVC 依赖项或安装扩展与 Web 窗体使用基架。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="c1bb7-112">下面显示了这两种方法。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-112">Both approaches are shown below.</span></span>

<span data-ttu-id="c1bb7-113">Visual Studio 2013 Update 2 (当前 RC) 提供的功能来扩展 ASP.NET 基架以满足你的方案的要求。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="c1bb7-114">使用此功能，可以创建自定义的基架模板并将其添加到对话框中添加新的基架。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="c1bb7-115">在自定义模板中，你可以指定添加基架的项时生成的代码。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="c1bb7-116">有关详细信息，请参阅[for Visual Studio 中创建自定义基架](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1bb7-117">先决条件</span><span class="sxs-lookup"><span data-stu-id="c1bb7-117">Prerequisites</span></span>

<span data-ttu-id="c1bb7-118">若要使用 ASP.NET 基架，你必须具有：</span><span class="sxs-lookup"><span data-stu-id="c1bb7-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="c1bb7-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c1bb7-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="c1bb7-120">Web 开发人员工具 （默认 Visual Studio 2013 安装的一部分）</span><span class="sxs-lookup"><span data-stu-id="c1bb7-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="c1bb7-121">ASP.NET Web 框架和工具 2013 （默认 Visual Studio 2013 安装的一部分）</span><span class="sxs-lookup"><span data-stu-id="c1bb7-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="c1bb7-122">将基架的项添加到 MVC 或 Web API</span><span class="sxs-lookup"><span data-stu-id="c1bb7-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="c1bb7-123">若要添加基架，请右键单击项目或在项目中，文件夹，然后选择**添加**–**新建基架项**，如以下图像中所示。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![添加基架项](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="c1bb7-125">从**添加基架**窗口中，选择的基架添加的类型。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![选择基架的类型](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="c1bb7-127">**添加控制器**窗口使你有机会选择用于生成控制器上，包括你是否想要使用 Entity Framework 6 中的新异步功能的选项。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![添加控制器](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="c1bb7-129">为你的方案创建的相关类和页面。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="c1bb7-130">例如下, 图显示的 MVC 控制器和通过一个名为电影的模型类的基架创建的视图。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![创建的文件](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="c1bb7-132">将基架的项添加到 Web 窗体</span><span class="sxs-lookup"><span data-stu-id="c1bb7-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="c1bb7-133">若要添加基架生成 Web 窗体代码，必须安装到 Visual Studio 扩展或添加 MVC 依赖项。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="c1bb7-134">这两种方法如下所示，但只需执行这些方法之一。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="c1bb7-135">Web 窗体基架扩展</span><span class="sxs-lookup"><span data-stu-id="c1bb7-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="c1bb7-136">你可以安装 Visual Studio 扩展，可用于与 Web 窗体项目中使用基架。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="c1bb7-137">在 Visual Studio 中，选择**工具**然后**扩展和更新**。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="c1bb7-138">从该对话框 Visual Studio 库中搜索有关**Web 窗体基架**。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![安装 web 窗体基架](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="c1bb7-140">有关详细信息，请参阅[Web 窗体基架](https://go.microsoft.com/fwlink/p/?LinkId=396478)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="c1bb7-141">MVC 依赖项</span><span class="sxs-lookup"><span data-stu-id="c1bb7-141">MVC Dependencies</span></span>

<span data-ttu-id="c1bb7-142">若要添加 MVC 依赖项，请选择**添加** - **新建基架项**。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="c1bb7-143">在添加基架窗口中，选择**MVC 依赖项**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![添加 MVC 依赖项](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="c1bb7-145">有两个选项的基架 MVC;最小和完整。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="c1bb7-146">如果你选择最小，只有的 NuGet 包和 ASP.NET MVC 的引用添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="c1bb7-147">如果选择完整选项，添加最小依赖关系，以及对于 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="c1bb7-148">若要轻松地使用基架，请选择完整的依赖项。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-148">To easily use scaffolding, select Full dependencies.</span></span>

![选择完整的依赖关系](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="c1bb7-150">添加依赖项之后, 你将看到**readme.txt**文件。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="c1bb7-151">认真遵循此文件中的说明，确保你的项目正常运行。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="c1bb7-152">完成的 readme.txt 文件中的步骤后，可以添加新的基架的项，如关于 MVC 和 Web API 上一节中所示。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="c1bb7-153">自动生成的视图和控制器将您的项目中正常工作。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="c1bb7-154">教程</span><span class="sxs-lookup"><span data-stu-id="c1bb7-154">Tutorials</span></span>

<span data-ttu-id="c1bb7-155">若要创建自定义的基架，请参阅[for Visual Studio 中创建自定义基架](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="c1bb7-156">若要自定义生成的文件，请参阅[如何自定义生成的文件从新建基架项对话框](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="c1bb7-157">有关的使用与基架示例**Database First 开发**，请参阅[EF 数据库第一家 ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="c1bb7-158">有关使用中的基架示例**MVC**项目，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="c1bb7-159">有关使用中的基架示例**Web API**项目，请参阅[使用 Web API 2 中的属性路由创建 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="c1bb7-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
