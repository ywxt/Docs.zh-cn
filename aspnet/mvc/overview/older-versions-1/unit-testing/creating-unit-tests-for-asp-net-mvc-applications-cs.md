---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: 创建单元测试为 ASP.NET MVC 应用程序 (C#) |Microsoft Docs
author: StephenWalther
description: 了解如何创建单元测试控制器操作。 在本教程中，Stephen Walther 演示了如何测试控制器操作返回 parti 是否...
ms.author: aspnetcontent
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: f9e6945a379d37f1539c7135041f50dcc7041750
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826674"
---
<a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="e330d-104">为 ASP.NET MVC 应用程序 (C#) 创建单元测试</span><span class="sxs-lookup"><span data-stu-id="e330d-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>
====================
<span data-ttu-id="e330d-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e330d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="e330d-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="e330d-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="e330d-107">了解如何创建单元测试控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="e330d-108">在本教程中，Stephen Walther 演示了如何测试是否控制器操作返回的特定视图，返回一组特定的数据，或返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="e330d-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>


<span data-ttu-id="e330d-109">本教程的目的是演示如何编写单元测试的控制器在 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e330d-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="e330d-110">我们讨论如何构建三种不同类型的单元测试。</span><span class="sxs-lookup"><span data-stu-id="e330d-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="e330d-111">介绍如何测试控制器操作返回的视图、 如何测试控制器操作，返回的视图数据以及如何测试一个控制器操作可以重定向到第二个控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="e330d-112">创建测试控制器</span><span class="sxs-lookup"><span data-stu-id="e330d-112">Creating the Controller under Test</span></span>

<span data-ttu-id="e330d-113">让我们首先创建我们想要测试的控制器。</span><span class="sxs-lookup"><span data-stu-id="e330d-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="e330d-114">控制器，名为`ProductController`，包含在列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="e330d-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="e330d-115">**代码清单 1 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="e330d-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="e330d-116">`ProductController`包含名为两个操作方法`Index()`和`Details()`。</span><span class="sxs-lookup"><span data-stu-id="e330d-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="e330d-117">这两个操作方法返回一个视图。</span><span class="sxs-lookup"><span data-stu-id="e330d-117">Both action methods return a view.</span></span> <span data-ttu-id="e330d-118">请注意，`Details()`操作接受一个参数，名为 id。</span><span class="sxs-lookup"><span data-stu-id="e330d-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="e330d-119">测试该视图返回的控制器</span><span class="sxs-lookup"><span data-stu-id="e330d-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="e330d-120">假设我们想要测试是否`ProductController`返回右视图。</span><span class="sxs-lookup"><span data-stu-id="e330d-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="e330d-121">我们想要确保，当`ProductController.Details()`调用操作，则返回的详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="e330d-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="e330d-122">代码清单 2 中的测试类包含用于测试返回的视图的单元测试`ProductController.Details()`操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="e330d-123">**代码清单 2 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="e330d-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="e330d-124">代码清单 2 中的类包括一个名为测试方法`TestDetailsView()`。</span><span class="sxs-lookup"><span data-stu-id="e330d-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="e330d-125">此方法包含三行代码。</span><span class="sxs-lookup"><span data-stu-id="e330d-125">This method contains three lines of code.</span></span> <span data-ttu-id="e330d-126">第一行代码创建的新实例`ProductController`类。</span><span class="sxs-lookup"><span data-stu-id="e330d-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="e330d-127">第二行代码将调用控制器的`Details()`操作方法。</span><span class="sxs-lookup"><span data-stu-id="e330d-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="e330d-128">最后，代码检查是否在视图返回的最后一行`Details()`操作是详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="e330d-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="e330d-129">`ViewResult.ViewName`属性表示返回由控制器的视图的名称。</span><span class="sxs-lookup"><span data-stu-id="e330d-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="e330d-130">有关测试此属性的一个大警告。</span><span class="sxs-lookup"><span data-stu-id="e330d-130">One big warning about testing this property.</span></span> <span data-ttu-id="e330d-131">有两种方法是控制器可以返回视图。</span><span class="sxs-lookup"><span data-stu-id="e330d-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="e330d-132">控制器可以显式返回视图，如下：</span><span class="sxs-lookup"><span data-stu-id="e330d-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="e330d-133">或者，可以从控制器操作，此类的名称推断的视图的名称：</span><span class="sxs-lookup"><span data-stu-id="e330d-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="e330d-134">此控制器操作也会返回一个名为视图`Details`。</span><span class="sxs-lookup"><span data-stu-id="e330d-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="e330d-135">但是，从操作名称推断的视图的名称。</span><span class="sxs-lookup"><span data-stu-id="e330d-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="e330d-136">如果你想要测试的视图名称，然后必须从控制器操作显式返回视图名称。</span><span class="sxs-lookup"><span data-stu-id="e330d-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="e330d-137">可以在代码清单 2 中运行单元测试，通过输入键盘组合**Ctrl-R、 A**或单击**运行解决方案中的所有测试**按钮 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="e330d-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="e330d-138">如果测试通过，您将看到图 2 中的测试结果窗口。</span><span class="sxs-lookup"><span data-stu-id="e330d-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>


<span data-ttu-id="e330d-139">[![在解决方案中运行所有测试](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e330d-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="e330d-140">**图 01**： 在解决方案中运行所有测试 ([单击以查看实际尺寸的图像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="e330d-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>


<span data-ttu-id="e330d-141">[![成功 ！](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="e330d-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="e330d-142">**图 02**： 成功 ！</span><span class="sxs-lookup"><span data-stu-id="e330d-142">**Figure 02**: Success!</span></span> <span data-ttu-id="e330d-143">([单击此项可查看原尺寸图像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e330d-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>


## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="e330d-144">测试视图数据返回的控制器</span><span class="sxs-lookup"><span data-stu-id="e330d-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="e330d-145">一个 MVC 控制器将数据传递给视图通过使用所谓*`View Data`*。</span><span class="sxs-lookup"><span data-stu-id="e330d-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="e330d-146">例如，假设你想要显示某一特定产品的详细信息，当你调用`ProductController Details()`操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="e330d-147">在这种情况下，可以创建的实例`Product`类 （在您的模型中定义），并将传递到实例`Details`视图通过利用`View Data`。</span><span class="sxs-lookup"><span data-stu-id="e330d-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="e330d-148">已修改`ProductController`清单 3 中包括的已更新`Details()`返回产品的操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="e330d-149">**代码清单 3 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="e330d-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="e330d-150">首先，`Details()`操作将创建的新实例`Product`类表示便携式计算机。</span><span class="sxs-lookup"><span data-stu-id="e330d-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="e330d-151">接下来，实例`Product`类作为第二个参数传递给`View()`方法。</span><span class="sxs-lookup"><span data-stu-id="e330d-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="e330d-152">您可以编写单元测试来测试是否为预期的数据包含在视图中的数据。</span><span class="sxs-lookup"><span data-stu-id="e330d-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="e330d-153">列表 4 测试中的单元测试是否在调用时返回表示便携式计算机的产品`ProductController Details()`操作方法。</span><span class="sxs-lookup"><span data-stu-id="e330d-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="e330d-154">**列表 4 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="e330d-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="e330d-155">列表 4 中`TestDetailsView()`方法测试通过调用返回的视图数据`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="e330d-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="e330d-156">`ViewData`上作为属性公开`ViewResult`返回通过调用`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="e330d-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="e330d-157">`ViewData.Model`属性包含传递给视图的产品。</span><span class="sxs-lookup"><span data-stu-id="e330d-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="e330d-158">此测试只需将验证视图数据中包含该产品具有便携式计算机的名称。</span><span class="sxs-lookup"><span data-stu-id="e330d-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="e330d-159">测试操作结果返回的控制器</span><span class="sxs-lookup"><span data-stu-id="e330d-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="e330d-160">更复杂的控制器操作可能会返回不同类型的具体值取决于传递到控制器操作的参数的操作结果。</span><span class="sxs-lookup"><span data-stu-id="e330d-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="e330d-161">控制器操作可以返回各种类型的操作的结果，包括`ViewResult`， `RedirectToRouteResult`，或`JsonResult`。</span><span class="sxs-lookup"><span data-stu-id="e330d-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="e330d-162">例如，修改`Details()`列表 5 中的操作返回`Details`查看有效的产品 Id 传递给该操作时。</span><span class="sxs-lookup"><span data-stu-id="e330d-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="e330d-163">如果传递无效的产品 Id-的 Id 值小于 1 则将重定向到`Index()`操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="e330d-164">**列表 5 – `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="e330d-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="e330d-165">可以测试的行为`Details()`列表 6 中的单元测试的操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="e330d-166">列表 6 中的单元测试验证是否将重定向到`Index`查看时具有的值为-1 的 Id 传递给`Details()`方法。</span><span class="sxs-lookup"><span data-stu-id="e330d-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="e330d-167">**代码清单 6 – `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="e330d-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="e330d-168">当您调用`RedirectToAction()`方法的控制器操作中，控制器操作返回`RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="e330d-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="e330d-169">测试检查是否`RedirectToRouteResult`将用户重定向到名为的控制器操作`Index`。</span><span class="sxs-lookup"><span data-stu-id="e330d-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="e330d-170">总结</span><span class="sxs-lookup"><span data-stu-id="e330d-170">Summary</span></span>

<span data-ttu-id="e330d-171">在本教程中，您学习了如何生成单元测试的 MVC 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="e330d-172">首先，您学习了如何验证是否由控制器操作返回了正确的视图。</span><span class="sxs-lookup"><span data-stu-id="e330d-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="e330d-173">您学习了如何使用`ViewResult.ViewName`属性以验证视图的名称。</span><span class="sxs-lookup"><span data-stu-id="e330d-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="e330d-174">接下来，我们探讨了如何测试的内容`View Data`。</span><span class="sxs-lookup"><span data-stu-id="e330d-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="e330d-175">您学习了如何检查是否已在中返回正确的产品`View Data`后调用的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="e330d-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="e330d-176">最后，我们讨论了如何测试是否从控制器操作返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="e330d-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="e330d-177">您学习了如何测试控制器将返回是否`ViewResult`或`RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="e330d-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e330d-178">下一篇</span><span class="sxs-lookup"><span data-stu-id="e330d-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
