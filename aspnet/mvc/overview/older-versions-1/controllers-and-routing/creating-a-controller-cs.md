---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 创建控制器 (C#) |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 演示了如何将控制器添加到 ASP.NET MVC 应用程序。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6fe880775a5d477aefcf0fe6cedb3e719760ed90
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833473"
---
<a name="creating-a-controller-c"></a><span data-ttu-id="142be-103">创建控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="142be-103">Creating a Controller (C#)</span></span>
====================
<span data-ttu-id="142be-104">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="142be-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="142be-105">在本教程中，Stephen Walther 演示了如何将控制器添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="142be-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>


<span data-ttu-id="142be-106">本教程的目的是说明如何创建新的 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="142be-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="142be-107">了解如何创建控制器通过使用 Visual Studio 添加的控制器菜单选项，以及通过手动创建的类文件。</span><span class="sxs-lookup"><span data-stu-id="142be-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="142be-108">使用添加控制器菜单选项</span><span class="sxs-lookup"><span data-stu-id="142be-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="142be-109">若要创建新的控制器的最简单方法是右键单击 Visual Studio 解决方案资源管理器窗口中的 Controllers 文件夹并选择**添加、 控制器**菜单选项 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="142be-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="142be-110">选择此菜单选项将打开**添加控制器**对话框 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="142be-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>


<span data-ttu-id="142be-111">[![新建项目对话框](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="142be-111">[![The New Project dialog box](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span></span>

<span data-ttu-id="142be-112">**图 01**： 添加新的控制器 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="142be-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-cs/_static/image2.png))</span></span>


<span data-ttu-id="142be-113">[![新建项目对话框](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="142be-113">[![The New Project dialog box](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span></span>

<span data-ttu-id="142be-114">**图 02**: 添加控制器对话框 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="142be-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-cs/_static/image4.png))</span></span>


<span data-ttu-id="142be-115">请注意，以突出显示，控制器名称的第一部分**添加控制器**对话框。</span><span class="sxs-lookup"><span data-stu-id="142be-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="142be-116">每个控制器名称必须以后缀结尾*控制器*。</span><span class="sxs-lookup"><span data-stu-id="142be-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="142be-117">例如，可以创建名为的控制器*ProductController*但不是名为的控制器*产品*。</span><span class="sxs-lookup"><span data-stu-id="142be-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>


<span data-ttu-id="142be-118">如果您创建一个控制器缺失*控制器*后缀，然后你将无法调用控制器。</span><span class="sxs-lookup"><span data-stu-id="142be-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="142be-119">不执行此操作，我已经浪费无数小时的人生旅途之后再犯此错误。</span><span class="sxs-lookup"><span data-stu-id="142be-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>


<span data-ttu-id="142be-120">**代码清单 1-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="142be-120">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

<span data-ttu-id="142be-121">您应始终创建 Controllers 文件夹中的控制器。</span><span class="sxs-lookup"><span data-stu-id="142be-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="142be-122">否则为将会违反 ASP.NET MVC 的约定和其他开发人员会更加困难时间来了解你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="142be-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="142be-123">操作方法的基架</span><span class="sxs-lookup"><span data-stu-id="142be-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="142be-124">当你创建一个控制器时，您可以选择自动生成创建、 更新和的详细信息的操作方法 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="142be-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="142be-125">如果选择此选项，则会生成代码清单 2 中的控制器类。</span><span class="sxs-lookup"><span data-stu-id="142be-125">If you select this option then the controller class in Listing 2 is generated.</span></span>


<span data-ttu-id="142be-126">[![自动创建的操作方法](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="142be-126">[![Creating action methods automatically](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span></span>

<span data-ttu-id="142be-127">**图 03**： 自动创建的操作方法 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="142be-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-cs/_static/image6.png))</span></span>


<span data-ttu-id="142be-128">**代码清单 2-Controllers\CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="142be-128">**Listing 2 - Controllers\CustomerController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

<span data-ttu-id="142be-129">这些生成的方法是存根 （stub） 方法。</span><span class="sxs-lookup"><span data-stu-id="142be-129">These generated methods are stub methods.</span></span> <span data-ttu-id="142be-130">必须添加用于创建、 更新和显示详细信息的客户自己的实际逻辑。</span><span class="sxs-lookup"><span data-stu-id="142be-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="142be-131">但是，存根 （stub） 方法为您提供很好的起点。</span><span class="sxs-lookup"><span data-stu-id="142be-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="142be-132">创建控制器类</span><span class="sxs-lookup"><span data-stu-id="142be-132">Creating a Controller Class</span></span>

<span data-ttu-id="142be-133">ASP.NET MVC 控制器是只是一个类。</span><span class="sxs-lookup"><span data-stu-id="142be-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="142be-134">如果您愿意，可以忽略方便 Visual Studio 控制器基架和手动创建的控制器类。</span><span class="sxs-lookup"><span data-stu-id="142be-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="142be-135">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="142be-135">Follow these steps:</span></span>

1. <span data-ttu-id="142be-136">右键单击 Controllers 文件夹，然后选择菜单选项**添加、 新建项**，然后选择**类**模板 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="142be-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="142be-137">命名新类 PersonController.cs，然后单击**添加**按钮。</span><span class="sxs-lookup"><span data-stu-id="142be-137">Name the new class PersonController.cs and click the **Add** button.</span></span>
3. <span data-ttu-id="142be-138">修改生成的类文件，使类继承自基 system.web.mvc.controller 中衍生类 （请参阅代码清单 3）。</span><span class="sxs-lookup"><span data-stu-id="142be-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>


<span data-ttu-id="142be-139">[![创建一个新类](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="142be-139">[![Creating a new class](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span></span>

<span data-ttu-id="142be-140">**图 04**： 创建一个新类 ([单击以查看实际尺寸的图像](creating-a-controller-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="142be-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-cs/_static/image8.png))</span></span>


<span data-ttu-id="142be-141">**代码清单 3-Controllers\PersonController.cs**</span><span class="sxs-lookup"><span data-stu-id="142be-141">**Listing 3 - Controllers\PersonController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

<span data-ttu-id="142be-142">在清单 3 中的控制器公开一个名为 index （） 返回字符串"Hello World ！"的操作。</span><span class="sxs-lookup"><span data-stu-id="142be-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="142be-143">你可以通过运行应用程序并请求的 URL 如下所示调用此控制器操作：</span><span class="sxs-lookup"><span data-stu-id="142be-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="142be-144">ASP.NET 开发服务器使用一个随机端口号 (例如，40071)。</span><span class="sxs-lookup"><span data-stu-id="142be-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="142be-145">当输入时要调用控制器的 URL，你将需要提供正确的端口号。</span><span class="sxs-lookup"><span data-stu-id="142be-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="142be-146">可以通过鼠标悬停在该图标在 Windows 通知区域 （在屏幕的右下方） 中的 ASP.NET 开发服务器确定端口号。</span><span class="sxs-lookup"><span data-stu-id="142be-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="142be-147">[上一页](adding-dynamic-content-to-a-cached-page-cs.md)
> [下一页](creating-an-action-cs.md)</span><span class="sxs-lookup"><span data-stu-id="142be-147">[Previous](adding-dynamic-content-to-a-cached-page-cs.md)
[Next](creating-an-action-cs.md)</span></span>
