---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: 在 Visual Studio 2013 的 ASP.NET 基架 |Microsoft Docs
author: tfitzmac
description: ASP.NET 基架是包括在 Visual Studio 2013 的新功能。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: c554f592e57f2e6017f7fcfcc9b4c98051e21b37
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824871"
---
<a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="b042e-103">在 Visual Studio 2013 的 ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="b042e-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>
====================
<span data-ttu-id="b042e-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b042e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b042e-105">ASP.NET 基架是包括在 Visual Studio 2013 的新功能。</span><span class="sxs-lookup"><span data-stu-id="b042e-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>


## <a name="overview"></a><span data-ttu-id="b042e-106">概述</span><span class="sxs-lookup"><span data-stu-id="b042e-106">Overview</span></span>

<span data-ttu-id="b042e-107">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="b042e-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="b042e-108">Visual Studio 2013 包括 MVC 和 Web API 项目的预安装的代码生成器。</span><span class="sxs-lookup"><span data-stu-id="b042e-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="b042e-109">当你想要快速添加与数据模型交互的代码基架添加到项目。</span><span class="sxs-lookup"><span data-stu-id="b042e-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="b042e-110">使用基架可以减少开发你的项目中的标准数据操作的时间量。</span><span class="sxs-lookup"><span data-stu-id="b042e-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="b042e-111">默认情况下，Visual Studio 2013 不支持的 Web 窗体项目，生成代码，但可以使用 Web 窗体中使用基架通过向项目添加 MVC 依赖项或安装扩展。</span><span class="sxs-lookup"><span data-stu-id="b042e-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="b042e-112">下面显示了这两种方法。</span><span class="sxs-lookup"><span data-stu-id="b042e-112">Both approaches are shown below.</span></span>

<span data-ttu-id="b042e-113">Visual Studio 2013 Update 2 (当前 RC) 提供的功能来扩展 ASP.NET 基架以满足你的方案的要求。</span><span class="sxs-lookup"><span data-stu-id="b042e-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="b042e-114">使用此功能，可以创建自定义基架模板并将其添加到对话框中添加新的基架。</span><span class="sxs-lookup"><span data-stu-id="b042e-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="b042e-115">在自定义模板中，指定将添加基架的项时生成的代码。</span><span class="sxs-lookup"><span data-stu-id="b042e-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="b042e-116">有关详细信息，请参阅[用于 Visual Studio 中创建自定义基架](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="b042e-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b042e-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="b042e-117">Prerequisites</span></span>

<span data-ttu-id="b042e-118">若要使用 ASP.NET 基架，您必须具有：</span><span class="sxs-lookup"><span data-stu-id="b042e-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="b042e-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b042e-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="b042e-120">Web 开发人员工具 （默认 Visual Studio 2013 安装的一部分）</span><span class="sxs-lookup"><span data-stu-id="b042e-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="b042e-121">ASP.NET Web 框架和工具 2013 （默认 Visual Studio 2013 安装的一部分）</span><span class="sxs-lookup"><span data-stu-id="b042e-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="b042e-122">将基架的项添加到 MVC 或 Web API</span><span class="sxs-lookup"><span data-stu-id="b042e-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="b042e-123">若要添加基架，请右键单击项目或在项目中，一个文件夹并选择**外**–**新基架项**下, 图中所示。</span><span class="sxs-lookup"><span data-stu-id="b042e-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![添加基架项](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="b042e-125">从**添加基架**窗口中，选择的基架添加的类型。</span><span class="sxs-lookup"><span data-stu-id="b042e-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![选择类型的基架](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="b042e-127">**添加控制器**窗口使您能够选择用于生成控制器，包括是否想要使用 Entity Framework 6 的新异步功能的选项。</span><span class="sxs-lookup"><span data-stu-id="b042e-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![添加控制器](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="b042e-129">你的方案为创建相关的类和页面。</span><span class="sxs-lookup"><span data-stu-id="b042e-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="b042e-130">例如下, 图显示了 MVC 控制器和视图通过名为电影模型类的基架创建的。</span><span class="sxs-lookup"><span data-stu-id="b042e-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![创建的文件](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="b042e-132">将基架的项添加到 Web 窗体</span><span class="sxs-lookup"><span data-stu-id="b042e-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="b042e-133">若要添加基架生成 Web 窗体代码，必须安装到 Visual Studio 扩展或添加 MVC 依赖项。</span><span class="sxs-lookup"><span data-stu-id="b042e-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="b042e-134">这两种方法如下所示，但只需执行其中一种方法。</span><span class="sxs-lookup"><span data-stu-id="b042e-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="b042e-135">Web 窗体基架扩展</span><span class="sxs-lookup"><span data-stu-id="b042e-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="b042e-136">你可以安装 Visual Studio 扩展中，您可以使用 Web 窗体项目中使用基架。</span><span class="sxs-lookup"><span data-stu-id="b042e-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="b042e-137">在 Visual Studio 中，选择**工具**，然后**扩展和更新**。</span><span class="sxs-lookup"><span data-stu-id="b042e-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="b042e-138">在此对话框中搜索有关 Visual Studio 库**Web 窗体基架**。</span><span class="sxs-lookup"><span data-stu-id="b042e-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![安装 web 窗体基架](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="b042e-140">有关详细信息，请参阅[Web 窗体基架](https://go.microsoft.com/fwlink/p/?LinkId=396478)。</span><span class="sxs-lookup"><span data-stu-id="b042e-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="b042e-141">MVC 依赖项</span><span class="sxs-lookup"><span data-stu-id="b042e-141">MVC Dependencies</span></span>

<span data-ttu-id="b042e-142">若要添加 MVC 依赖项，请选择**外** - **新基架项**。</span><span class="sxs-lookup"><span data-stu-id="b042e-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="b042e-143">在添加基架窗口中，选择**MVC 依赖项**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b042e-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![添加 MVC 依赖项](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="b042e-145">有两个选项基架 MVC;最小和完全。</span><span class="sxs-lookup"><span data-stu-id="b042e-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="b042e-146">如果你选择最小，NuGet 包和 ASP.NET MVC 的引用添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="b042e-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="b042e-147">如果选择完全选项，添加最小依赖项，以及对于 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="b042e-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="b042e-148">若要轻松地使用基架，请选择完整的依赖项。</span><span class="sxs-lookup"><span data-stu-id="b042e-148">To easily use scaffolding, select Full dependencies.</span></span>

![选择全部依赖项](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="b042e-150">添加依赖项之后, 您将看到**readme.txt**文件。</span><span class="sxs-lookup"><span data-stu-id="b042e-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="b042e-151">请仔细按照此文件中的说明，以确保你的项目正常运行。</span><span class="sxs-lookup"><span data-stu-id="b042e-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="b042e-152">完成 readme.txt 文件中的步骤后，可以添加新的基架的项，如有关 MVC 和 Web API 在上一部分中所示。</span><span class="sxs-lookup"><span data-stu-id="b042e-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="b042e-153">自动生成的视图和控制器将在项目中正常工作。</span><span class="sxs-lookup"><span data-stu-id="b042e-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="b042e-154">教程</span><span class="sxs-lookup"><span data-stu-id="b042e-154">Tutorials</span></span>

<span data-ttu-id="b042e-155">若要创建自定义基架，请参阅[用于 Visual Studio 中创建自定义基架](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="b042e-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="b042e-156">若要自定义生成的文件，请参阅[如何自定义生成的文件从新建基架项对话框](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b042e-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="b042e-157">有关使用与基架的示例**Database First 开发**，请参阅[EF Database First 使用 ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。</span><span class="sxs-lookup"><span data-stu-id="b042e-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="b042e-158">有关使用中的基架的示例**MVC**项目，请参阅[Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b042e-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="b042e-159">有关使用中的基架的示例**Web API**项目，请参阅[使用 Web API 2 中的属性路由创建 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="b042e-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
