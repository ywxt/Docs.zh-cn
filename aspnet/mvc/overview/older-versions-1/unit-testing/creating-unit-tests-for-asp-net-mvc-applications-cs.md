---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: 为 ASP.NET MVC 应用程序 (C#) 中创建单元测试 |Microsoft 文档
author: StephenWalther
description: 了解如何创建单元测试的控制器操作。 在本教程中，Stephen Walther 演示如何测试是否控制器操作返回 parti...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: ccd9a1b3aee8379c23c01c5eb7f756a786f6359d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869707"
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="80601-104">为 ASP.NET MVC 应用程序 (C#) 中创建单元测试</span><span class="sxs-lookup"><span data-stu-id="80601-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>
====================
<span data-ttu-id="80601-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="80601-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="80601-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="80601-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="80601-107">了解如何创建单元测试的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="80601-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="80601-108">在本教程中，Stephen Walther 演示如何测试是否控制器操作返回的特定视图、 返回一组特定的数据，或返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="80601-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="80601-109">本教程的目标是演示如何编写单元测试控制器的 ASP.NET mvc 应用程序。</span><span class="sxs-lookup"><span data-stu-id="80601-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="80601-110">我们讨论如何生成三个不同类型的单元测试。</span><span class="sxs-lookup"><span data-stu-id="80601-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="80601-111">你了解如何测试控制器操作返回的视图、 如何测试的控制器操作，返回的视图数据以及如何测试一个控制器操作将你重定向到第二个控制器操作。</span><span class="sxs-lookup"><span data-stu-id="80601-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="80601-112">创建测试控制器</span><span class="sxs-lookup"><span data-stu-id="80601-112">Creating the Controller under Test</span></span>

<span data-ttu-id="80601-113">让我们首先创建我们想要测试的控制器。</span><span class="sxs-lookup"><span data-stu-id="80601-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="80601-114">控制器上，名为`ProductController`，包含在清单 1。</span><span class="sxs-lookup"><span data-stu-id="80601-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="80601-115">**列表 1 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="80601-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="80601-116">`ProductController`包含名为的两个操作方法`Index()`和`Details()`。</span><span class="sxs-lookup"><span data-stu-id="80601-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="80601-117">这两种操作方法返回的视图。</span><span class="sxs-lookup"><span data-stu-id="80601-117">Both action methods return a view.</span></span> <span data-ttu-id="80601-118">请注意，`Details()`操作接受一个参数，名为 id。</span><span class="sxs-lookup"><span data-stu-id="80601-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="80601-119">测试视图返回的控制器</span><span class="sxs-lookup"><span data-stu-id="80601-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="80601-120">假设我们想要测试是否`ProductController`返回右视图。</span><span class="sxs-lookup"><span data-stu-id="80601-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="80601-121">我们想要确保当`ProductController.Details()`调用操作，返回的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="80601-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="80601-122">列出 2 中的测试类包含用于测试返回的视图的单元测试`ProductController.Details()`操作。</span><span class="sxs-lookup"><span data-stu-id="80601-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="80601-123">**列出 2 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="80601-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="80601-124">列出 2 中的类包括一个名为的测试方法`TestDetailsView()`。</span><span class="sxs-lookup"><span data-stu-id="80601-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="80601-125">此方法将包含三行代码。</span><span class="sxs-lookup"><span data-stu-id="80601-125">This method contains three lines of code.</span></span> <span data-ttu-id="80601-126">第一行代码创建的新实例`ProductController`类。</span><span class="sxs-lookup"><span data-stu-id="80601-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="80601-127">代码的第二行时，将调用控制器的`Details()`操作方法。</span><span class="sxs-lookup"><span data-stu-id="80601-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="80601-128">最后，代码检查是否视图返回的最后一行`Details()`操作为详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="80601-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="80601-129">`ViewResult.ViewName`属性表示由控制器返回视图的名称。</span><span class="sxs-lookup"><span data-stu-id="80601-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="80601-130">有关测试此属性的一个大警告。</span><span class="sxs-lookup"><span data-stu-id="80601-130">One big warning about testing this property.</span></span> <span data-ttu-id="80601-131">有两个控制器可以返回视图的方法。</span><span class="sxs-lookup"><span data-stu-id="80601-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="80601-132">控制器可以显式返回的视图如下：</span><span class="sxs-lookup"><span data-stu-id="80601-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="80601-133">或者，可以如下的控制器操作的名称从推断出的视图名称：</span><span class="sxs-lookup"><span data-stu-id="80601-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="80601-134">此控制器操作还返回名为的视图`Details`。</span><span class="sxs-lookup"><span data-stu-id="80601-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="80601-135">但是，根据相应的操作名称进行推断的视图的名称。</span><span class="sxs-lookup"><span data-stu-id="80601-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="80601-136">如果你想要测试的视图名称，则必须从控制器操作显式返回视图名称。</span><span class="sxs-lookup"><span data-stu-id="80601-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="80601-137">可以列出 2 中运行单元测试，通过输入键盘组合**Ctrl R、 A**或通过单击**运行解决方案中的所有测试**按钮 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="80601-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="80601-138">如果测试通过，你将看到图 2 中的测试结果窗口。</span><span class="sxs-lookup"><span data-stu-id="80601-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


<span data-ttu-id="80601-139">[![在解决方案中运行所有测试](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="80601-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="80601-140">**图 01**： 在解决方案中运行所有测试 ([单击以查看实际尺寸的图像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="80601-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


<span data-ttu-id="80601-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="80601-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="80601-142">**图 02**： 成功 ！</span><span class="sxs-lookup"><span data-stu-id="80601-142">**Figure 02**: Success!</span></span> <span data-ttu-id="80601-143">([单击以查看实际尺寸的图像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="80601-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="80601-144">测试视图数据返回的控制器</span><span class="sxs-lookup"><span data-stu-id="80601-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="80601-145">一个 MVC 控制器，将数据传递给视图通过使用称为*`View Data`*。</span><span class="sxs-lookup"><span data-stu-id="80601-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="80601-146">例如，假设你想要显示特定产品的详细信息，在调用时`ProductController Details()`操作。</span><span class="sxs-lookup"><span data-stu-id="80601-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="80601-147">在这种情况下，你可以创建的实例`Product`类 （在你的模型中定义） 并将传递到实例`Details`视图，通过利用`View Data`。</span><span class="sxs-lookup"><span data-stu-id="80601-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="80601-148">已修改`ProductController`列出 3 中包括更新`Details()`返回产品的操作。</span><span class="sxs-lookup"><span data-stu-id="80601-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="80601-149">**列出 3 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="80601-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="80601-150">首先，`Details()`操作创建的新实例`Product`表示便携式计算机的类。</span><span class="sxs-lookup"><span data-stu-id="80601-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="80601-151">接下来，实例`Product`类作为第二个参数传递`View()`方法。</span><span class="sxs-lookup"><span data-stu-id="80601-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="80601-152">你可以编写单元测试来测试所需的数据是否包含在视图中的数据。</span><span class="sxs-lookup"><span data-stu-id="80601-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="80601-153">单元测试中列出 4 测试是否在调用时返回表示一台便携式计算机的产品`ProductController Details()`操作方法。</span><span class="sxs-lookup"><span data-stu-id="80601-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="80601-154">**列出 4 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="80601-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="80601-155">在列出 4 中，`TestDetailsView()`方法测试通过调用返回的视图数据`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="80601-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="80601-156">`ViewData`上作为属性公开`ViewResult`返回通过调用`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="80601-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="80601-157">`ViewData.Model`属性包含传递给视图的产品。</span><span class="sxs-lookup"><span data-stu-id="80601-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="80601-158">测试只需验证视图数据中包含的产品具有便携式计算机的名称。</span><span class="sxs-lookup"><span data-stu-id="80601-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="80601-159">测试操作结果返回的控制器</span><span class="sxs-lookup"><span data-stu-id="80601-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="80601-160">更复杂的控制器操作可能会返回不同类型的操作结果具体取决于值传递到的控制器操作的参数。</span><span class="sxs-lookup"><span data-stu-id="80601-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="80601-161">控制器操作可以返回的类型的操作的结果，包括各种`ViewResult`， `RedirectToRouteResult`，或`JsonResult`。</span><span class="sxs-lookup"><span data-stu-id="80601-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="80601-162">例如，修改`Details()`列出 5 中的操作返回`Details`查看有效的产品 Id 传递给操作时。</span><span class="sxs-lookup"><span data-stu-id="80601-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="80601-163">如果传递无效的产品 Id-Id 与一个值小于 1--则您将重定向到`Index()`操作。</span><span class="sxs-lookup"><span data-stu-id="80601-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="80601-164">**列出 5- `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="80601-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="80601-165">你可以测试的行为`Details()`列出 6 的单元测试的操作。</span><span class="sxs-lookup"><span data-stu-id="80601-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="80601-166">列出 6 中的单元测试验证你将重定向到`Index`查看时使用值-1 的 Id 传递给`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="80601-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="80601-167">**列出 6- `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="80601-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="80601-168">当调用`RedirectToAction()`方法的控制器操作中，控制器操作返回`RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="80601-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="80601-169">测试检查是否`RedirectToRouteResult`将用户重定向到名为的控制器操作`Index`。</span><span class="sxs-lookup"><span data-stu-id="80601-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="80601-170">总结</span><span class="sxs-lookup"><span data-stu-id="80601-170">Summary</span></span>

<span data-ttu-id="80601-171">在本教程中，您学习了如何生成 MVC 控制器操作的单元测试。</span><span class="sxs-lookup"><span data-stu-id="80601-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="80601-172">首先，您学习了如何验证是否由控制器操作返回与右视图。</span><span class="sxs-lookup"><span data-stu-id="80601-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="80601-173">你已了解如何使用`ViewResult.ViewName`属性以验证视图的名称。</span><span class="sxs-lookup"><span data-stu-id="80601-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="80601-174">接下来，我们探讨了如何测试的内容`View Data`。</span><span class="sxs-lookup"><span data-stu-id="80601-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="80601-175">您学习了如何检查是否在返回适当的产品`View Data`后调用的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="80601-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="80601-176">最后，我们讨论如何可以测试是否将不同类型的操作结果返回的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="80601-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="80601-177">你已了解如何测试控制器将返回是否`ViewResult`或`RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="80601-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="80601-178">下一篇</span><span class="sxs-lookup"><span data-stu-id="80601-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
