---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: 执行简单的验证 (C#) |Microsoft 文档
author: StephenWalther
description: 了解如何在 ASP.NET MVC 应用程序中执行验证。 在本教程中，Stephen Walther 引入你为模型状态和验证 HTML 帮助程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: 7fc1dcc6935841382215f67a519cd241ac68931a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869655"
---
<a name="performing-simple-validation-c"></a><span data-ttu-id="55549-104">执行简单的验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="55549-104">Performing Simple Validation (C#)</span></span>
====================
<span data-ttu-id="55549-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="55549-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="55549-106">了解如何在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="55549-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="55549-107">在本教程中，Stephen Walther 引入你为模型状态和验证 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="55549-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>


<span data-ttu-id="55549-108">本教程旨在说明如何执行验证的 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="55549-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="55549-109">例如，你将了解如何防止别人提交窗体不包含所需字段的值。</span><span class="sxs-lookup"><span data-stu-id="55549-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="55549-110">了解如何使用模型状态和验证 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="55549-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="55549-111">了解模型状态</span><span class="sxs-lookup"><span data-stu-id="55549-111">Understanding Model State</span></span>

<span data-ttu-id="55549-112">使用模型状态-或更准确地说，模型状态字典-来表示验证错误。</span><span class="sxs-lookup"><span data-stu-id="55549-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="55549-113">例如，列表 1 中的 create （） 操作将产品类添加到数据库之前验证产品类的属性。</span><span class="sxs-lookup"><span data-stu-id="55549-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>


<span data-ttu-id="55549-114">我不建议将你验证或数据库的逻辑添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="55549-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="55549-115">控制器应包含仅与应用程序流控制相关的逻辑。</span><span class="sxs-lookup"><span data-stu-id="55549-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="55549-116">我们正在进行的快捷方式来为简单起见。</span><span class="sxs-lookup"><span data-stu-id="55549-116">We are taking a shortcut to keep things simple.</span></span>


<span data-ttu-id="55549-117">**Listing 1 - Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="55549-117">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

<span data-ttu-id="55549-118">在列出 1 中，产品类的名称、 说明和 UnitsInStock 属性进行验证。</span><span class="sxs-lookup"><span data-stu-id="55549-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="55549-119">如果上述任一属性未通过验证测试然后会将错误添加到模型状态字典 （由控制器类的 ModelState 属性表示）。</span><span class="sxs-lookup"><span data-stu-id="55549-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="55549-120">如果模型状态中有任何错误 ModelState.IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="55549-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="55549-121">在这种情况下，创建新产品的 HTML 窗体将重新显示。</span><span class="sxs-lookup"><span data-stu-id="55549-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="55549-122">否则，如果不不存在任何验证错误，则新的产品添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="55549-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="55549-123">使用的验证帮助器</span><span class="sxs-lookup"><span data-stu-id="55549-123">Using the Validation Helpers</span></span>

<span data-ttu-id="55549-124">ASP.NET MVC framework 包括两个验证帮助器： Html.ValidationMessage() 帮助器和 Html.ValidationSummary() 帮助器。</span><span class="sxs-lookup"><span data-stu-id="55549-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="55549-125">在视图中使用这些两个帮助器来显示验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="55549-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="55549-126">通过 ASP.NET MVC 基架自动生成的创建和编辑视图中使用的 Html.ValidationMessage() 和 Html.ValidationSummary() 帮助器。</span><span class="sxs-lookup"><span data-stu-id="55549-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="55549-127">按照这些步骤生成创建视图：</span><span class="sxs-lookup"><span data-stu-id="55549-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="55549-128">右键单击产品控制器中的 create （） 操作，然后选择菜单选项**添加视图**（请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="55549-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="55549-129">在**添加视图**对话框中，选中复选框标记为**创建强类型化视图**（请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="55549-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="55549-130">从**查看数据类**下拉列表中，选择产品类别。</span><span class="sxs-lookup"><span data-stu-id="55549-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="55549-131">从**查看内容**下拉列表中，选择创建。</span><span class="sxs-lookup"><span data-stu-id="55549-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="55549-132">单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="55549-132">Click the **Add** button.</span></span>


<span data-ttu-id="55549-133">请确保生成你的应用程序，然后添加视图。</span><span class="sxs-lookup"><span data-stu-id="55549-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="55549-134">否则，类的列表不会显示在**查看数据类**下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="55549-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>


<span data-ttu-id="55549-135">[![新项目对话框](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="55549-135">[![The New Project dialog box](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="55549-136">**图 01**： 添加视图 ([单击以查看实际尺寸的图像](performing-simple-validation-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="55549-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-cs/_static/image2.png))</span></span>


<span data-ttu-id="55549-137">[![新项目对话框](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="55549-137">[![The New Project dialog box](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span></span>

<span data-ttu-id="55549-138">**图 02**： 创建强类型化视图 ([单击以查看实际尺寸的图像](performing-simple-validation-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="55549-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-cs/_static/image4.png))</span></span>


<span data-ttu-id="55549-139">完成这些步骤后，你将收到列出 2 中创建视图。</span><span class="sxs-lookup"><span data-stu-id="55549-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="55549-140">**Listing 2 - Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="55549-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

<span data-ttu-id="55549-141">在列出 2 中，Html.ValidationSummary() 帮助器称为立即上方的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="55549-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="55549-142">此帮助器用于显示验证错误消息的列表。</span><span class="sxs-lookup"><span data-stu-id="55549-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="55549-143">Html.ValidationSummary() 帮助器呈现项目符号列表中的错误。</span><span class="sxs-lookup"><span data-stu-id="55549-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="55549-144">每个 HTML 窗体字段旁边称为 Html.ValidationMessage() 帮助器。</span><span class="sxs-lookup"><span data-stu-id="55549-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="55549-145">此帮助器用于显示一条错误消息的表单域的右边。</span><span class="sxs-lookup"><span data-stu-id="55549-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="55549-146">对于列出 2 Html.ValidationMessage() 帮助程序错误时显示一个星号。</span><span class="sxs-lookup"><span data-stu-id="55549-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="55549-147">图 3 中的页说明了在具有缺失字段和无效值提交表单时，验证帮助器所呈现的错误消息。</span><span class="sxs-lookup"><span data-stu-id="55549-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>


<span data-ttu-id="55549-148">[![新项目对话框](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="55549-148">[![The New Project dialog box](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span></span>

<span data-ttu-id="55549-149">**图 03**： 提交有问题的 Create view ([单击以查看实际尺寸的图像](performing-simple-validation-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="55549-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-cs/_static/image6.png))</span></span>


<span data-ttu-id="55549-150">请注意的 html 外观输入验证错误时，还会修改字段。</span><span class="sxs-lookup"><span data-stu-id="55549-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="55549-151">Html.TextBox() 帮助器呈现*类 ="输入验证错误"* 与呈现 Html.TextBox() 帮助程序属性关联的验证错误时的特性。</span><span class="sxs-lookup"><span data-stu-id="55549-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="55549-152">有用于控制验证错误的外观的三个级联样式表类：</span><span class="sxs-lookup"><span data-stu-id="55549-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="55549-153">输入验证错误的应用于&lt;输入&gt;Html.TextBox() 帮助程序呈现的标记。</span><span class="sxs-lookup"><span data-stu-id="55549-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="55549-154">字段验证错误的应用于&lt;跨越&gt;Html.ValidationMessage() 帮助程序呈现的标记。</span><span class="sxs-lookup"><span data-stu-id="55549-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="55549-155">验证摘要错误-应用于&lt;ul&gt; Html.ValidationSumamry() 帮助程序呈现的标记。</span><span class="sxs-lookup"><span data-stu-id="55549-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSumamry() helper.</span></span>

<span data-ttu-id="55549-156">可以修改这些级联样式表类，并因此通过修改 Site.css 文件内容的文件夹中修改的验证错误的外观。</span><span class="sxs-lookup"><span data-stu-id="55549-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="55549-157">HtmlHelper 类包括只读的静态属性，检索的验证的名称与相关的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="55549-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="55549-158">ValidationInputCssClassName、 ValidationFieldCssClassName 和 ValidationSummaryCssClassName 命名这些静态属性。</span><span class="sxs-lookup"><span data-stu-id="55549-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>


## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="55549-159">Prebinding 验证和 Postbinding 验证</span><span class="sxs-lookup"><span data-stu-id="55549-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="55549-160">如果提交的 HTML 窗体创建产品，并且你输入的无效值 price 字段而没有值 UnitsInStock 字段，你将获得显示在图 4 中的验证消息。</span><span class="sxs-lookup"><span data-stu-id="55549-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="55549-161">这些验证错误消息来自何处呢？</span><span class="sxs-lookup"><span data-stu-id="55549-161">Where do these validation error messages come from?</span></span>


<span data-ttu-id="55549-162">[![新项目对话框](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="55549-162">[![The New Project dialog box](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span></span>

<span data-ttu-id="55549-163">**图 04**: Prebinding 验证错误 ([单击以查看实际尺寸的图像](performing-simple-validation-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="55549-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-cs/_static/image8.png))</span></span>


<span data-ttu-id="55549-164">有两种类型实际的验证错误消息的这些生成的 HTML 窗体字段绑定到类和这些生成的窗体字段绑定到类之后之前。</span><span class="sxs-lookup"><span data-stu-id="55549-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="55549-165">换而言之，有 prebinding 验证错误和 postbinding 验证错误。</span><span class="sxs-lookup"><span data-stu-id="55549-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="55549-166">列表 1 中在产品控制器公开的 create （） 操作接受产品类的实例。</span><span class="sxs-lookup"><span data-stu-id="55549-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="55549-167">创建方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="55549-167">The signature of the Create method looks like this:</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

<span data-ttu-id="55549-168">创建窗体中的 HTML 窗体字段的值由称为模型联编程序绑定到 productToCreate 类。</span><span class="sxs-lookup"><span data-stu-id="55549-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="55549-169">默认的模型联编程序将添加一条错误消息到模型状态自动时它不能将窗体字段绑定到窗体属性。</span><span class="sxs-lookup"><span data-stu-id="55549-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="55549-170">默认的模型联编程序不能将字符串"apple"绑定到产品类的价格属性。</span><span class="sxs-lookup"><span data-stu-id="55549-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="55549-171">无法将字符串分配给十进制属性。</span><span class="sxs-lookup"><span data-stu-id="55549-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="55549-172">因此，模型联编程序将错误添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="55549-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="55549-173">此外，默认的模型联编程序不能将 null 值分配给不接受 null 值的属性。</span><span class="sxs-lookup"><span data-stu-id="55549-173">The default model binder also cannot assign a null value to a property that does not accept nulls.</span></span> <span data-ttu-id="55549-174">具体而言，模型联编程序不能将 null 值分配给 UnitsInStock 属性。</span><span class="sxs-lookup"><span data-stu-id="55549-174">In particular, the model binder cannot assign a null value to the UnitsInStock property.</span></span> <span data-ttu-id="55549-175">同样，模型联编程序放弃，并将一条错误消息添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="55549-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="55549-176">如果你想要自定义这些的外观 prebinding 错误消息，然后需要创建这些消息的资源字符串。</span><span class="sxs-lookup"><span data-stu-id="55549-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="55549-177">总结</span><span class="sxs-lookup"><span data-stu-id="55549-177">Summary</span></span>

<span data-ttu-id="55549-178">本教程的目标是验证的介绍用于在 ASP.NET MVC framework 中的基本机制。</span><span class="sxs-lookup"><span data-stu-id="55549-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="55549-179">您学习了如何使用模型状态和验证 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="55549-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="55549-180">我们还讨论了 prebinding 和 postbinding 验证之间的区别。</span><span class="sxs-lookup"><span data-stu-id="55549-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="55549-181">在其他教程中，我们将讨论各种移动你的控制器出来放入模型类验证代码的策略。</span><span class="sxs-lookup"><span data-stu-id="55549-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="55549-182">[上一页](displaying-a-table-of-database-data-cs.md)
> [下一页](validating-with-the-idataerrorinfo-interface-cs.md)</span><span class="sxs-lookup"><span data-stu-id="55549-182">[Previous](displaying-a-table-of-database-data-cs.md)
[Next](validating-with-the-idataerrorinfo-interface-cs.md)</span></span>
