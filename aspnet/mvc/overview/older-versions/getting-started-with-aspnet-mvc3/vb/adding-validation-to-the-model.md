---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
title: 将验证添加到模型 (VB) |Microsoft 文档
author: Rick-Anderson
description: 本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 878f6c31-972d-45f4-8849-5c633b511409
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 86058530aa00ecbc00aeebc6ed7b5cf019fdad72
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872918"
---
<a name="adding-validation-to-the-model-vb"></a><span data-ttu-id="5c4c0-103">将验证添加到模型 (VB)</span><span class="sxs-lookup"><span data-stu-id="5c4c0-103">Adding Validation to the Model (VB)</span></span>
====================
<span data-ttu-id="5c4c0-104">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="5c4c0-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> <span data-ttu-id="5c4c0-105">本教程将教您构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是 Microsoft Visual Studio 的免费版本的 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="5c4c0-106">在开始之前，请确保已安装下面列出的先决条件。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="5c4c0-107">你可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="5c4c0-108">或者，你可以单独安装系统必备组件，使用以下链接：</span><span class="sxs-lookup"><span data-stu-id="5c4c0-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="5c4c0-109">Visual Studio Web Developer Express SP1 系统必备</span><span class="sxs-lookup"><span data-stu-id="5c4c0-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="5c4c0-110">ASP.NET MVC 3 Tools 更新</span><span class="sxs-lookup"><span data-stu-id="5c4c0-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="5c4c0-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="5c4c0-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="5c4c0-112">如果你正在使用 Visual Studio 2010，而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 系统必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="5c4c0-113">Visual Web Developer 项目与 VB.NET 的源代码是可以附带本主题。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="5c4c0-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="5c4c0-115">如果你愿意 C#，切换到[C# 版本](../cs/adding-validation-to-the-model.md)本教程。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-115">If you prefer C#, switch to the [C# version](../cs/adding-validation-to-the-model.md) of this tutorial.</span></span>


<span data-ttu-id="5c4c0-116">在本部分中，你将添加到的验证逻辑`Movie`模型，且你将确保验证规则会实施任何时候用户试图创建或编辑使用应用程序的影片。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-116">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="5c4c0-117">保持操作干</span><span class="sxs-lookup"><span data-stu-id="5c4c0-117">Keeping Things DRY</span></span>

<span data-ttu-id="5c4c0-118">ASP.NET MVC 的核心设计原则之一是模拟 （"不重复自己"）。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-118">One of the core design tenets of ASP.NET MVC is DRY ("Don't Repeat Yourself").</span></span> <span data-ttu-id="5c4c0-119">ASP.NET MVC 鼓励您一次，指定功能或行为，然后使用它 everywhere 反映在应用程序。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-119">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="5c4c0-120">这可减少所需编写的代码的数量，并使你确实要编写更加容易维护的代码。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-120">This reduces the amount of code you need to write and makes the code you do write much easier to maintain.</span></span>

<span data-ttu-id="5c4c0-121">提供 ASP.NET MVC 和 Entity Framework Code First 的验证支持是在操作中原则出色示例。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-121">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="5c4c0-122">在一个位置 （在模型类中） 以声明方式指定验证规则，然后强制实施这些规则无处不在应用程序中。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-122">You can declaratively specify validation rules in one place (in the model class) and then those rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="5c4c0-123">让我们看一下影片应用程序中，你就可以充分利用此验证支持。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-123">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="5c4c0-124">将验证规则添加到影片模型</span><span class="sxs-lookup"><span data-stu-id="5c4c0-124">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="5c4c0-125">将通过添加到某些验证逻辑开始`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-125">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="5c4c0-126">打开*Movie.vb*文件。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-126">Open the *Movie.vb* file.</span></span> <span data-ttu-id="5c4c0-127">添加`Imports`语句引用的文件的顶部[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间：</span><span class="sxs-lookup"><span data-stu-id="5c4c0-127">Add a `Imports` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample1.vb)]

<span data-ttu-id="5c4c0-128">命名空间是.NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-128">The namespace is part of the .NET Framework.</span></span> <span data-ttu-id="5c4c0-129">它提供了可以以声明方式应用于任何类或属性的验证属性内置组。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-129">It provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="5c4c0-130">现在更新`Movie`类以利用内置[ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)， [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)，和[ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性.</span><span class="sxs-lookup"><span data-stu-id="5c4c0-130">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="5c4c0-131">使用以下代码作为示例，了解将特性应用的位置。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-131">Use the following code as an example of where to apply the attributes.</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample2.vb)]

<span data-ttu-id="5c4c0-132">验证特性指定要对应用这些特性的模型属性强制执行的行为。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-132">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="5c4c0-133">`Required`属性指示属性必须具有一个值; 在此示例中，一部电影必须具有值`Title`， `ReleaseDate`， `Genre`，和`Price`属性才有效。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-133">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="5c4c0-134">`Range` 特性将值限制在指定范围内。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-134">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="5c4c0-135">`StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-135">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span>

<span data-ttu-id="5c4c0-136">代码首先将确保： 在一个模型类指定的验证规则之前应用程序将更改保存在数据库会强制实施。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-136">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="5c4c0-137">例如，下面的代码将引发异常时`SaveChanges`调用方法，因为几个需要`Movie`属性值为缺失，价格为零 （这是超出了有效范围）。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-137">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample3.vb)]

<span data-ttu-id="5c4c0-138">具有自动由.NET Framework 强制执行的验证规则有助于使你的应用程序更可靠。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-138">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="5c4c0-139">同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-139">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="5c4c0-140">下面是完整的代码列出了已更新的*Movie.vb*文件：</span><span class="sxs-lookup"><span data-stu-id="5c4c0-140">Here's a complete code listing for the updated *Movie.vb* file:</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample4.vb)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="5c4c0-141">验证错误在 ASP.NET MVC UI</span><span class="sxs-lookup"><span data-stu-id="5c4c0-141">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="5c4c0-142">重新运行该应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-142">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="5c4c0-143">单击**创建电影**链接添加新的影片。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-143">Click the **Create Movie** link to add a new movie.</span></span> <span data-ttu-id="5c4c0-144">填写表单的某些无效的值，然后单击**创建**按钮。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-144">Fill out the form with some invalid values and then click the **Create** button.</span></span>

<span data-ttu-id="5c4c0-145">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5c4c0-145">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span></span>

<span data-ttu-id="5c4c0-146">请注意如何窗体具有自动使用背景色来突出显示的文本框中，它包含无效的数据，并且已发出旁边每个相应的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-146">Notice how the form has automatically used a background color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="5c4c0-147">错误消息匹配的错误字符串，指定当批注`Movie`类。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-147">The error messages match the error strings you specified when you annotated the `Movie` class.</span></span> <span data-ttu-id="5c4c0-148">错误会强制客户端 （使用 JavaScript） 和服务器端执行，（如果用户已禁用 JavaScript）。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-148">The errors are enforced both client-side (using JavaScript) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="5c4c0-149">实际的好处是，你不需要更改单个行中的代码`MoviesController`类或在*Create.vbhtml*以启用此验证 UI 的视图。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-149">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.vbhtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="5c4c0-150">控制器和自动创建本教程中前面的视图中选取验证规则，指定在使用属性的向上`Movie`模型类。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-150">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified using attributes on the `Movie` model class.</span></span>

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="5c4c0-151">如何验证发生在创建查看和创建操作方法</span><span class="sxs-lookup"><span data-stu-id="5c4c0-151">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="5c4c0-152">你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-152">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="5c4c0-153">下一步的列表显示什么`Create`中的方法`MovieController`类如下所示。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-153">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="5c4c0-154">这些更改将从你创建这些此前在本教程不变。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-154">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample5.vb)]

<span data-ttu-id="5c4c0-155">第一种操作方法显示初始创建窗体。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-155">The first action method displays the initial Create form.</span></span> <span data-ttu-id="5c4c0-156">第二个处理窗体发布请求。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-156">The second handles the form post.</span></span> <span data-ttu-id="5c4c0-157">第二个`Create`方法调用`ModelState.IsValid`若要检查的影片是否有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-157">The second `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="5c4c0-158">调用此方法将评估已应用于对象的任何验证特性。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-158">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="5c4c0-159">如果该对象具有验证错误`Create`方法重新显示窗体。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-159">If the object has validation errors, the `Create` method redisplays the form.</span></span> <span data-ttu-id="5c4c0-160">如果没有错误，此方法则将新电影保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-160">If there are no errors, the method saves the new movie in the database.</span></span>

<span data-ttu-id="5c4c0-161">下面是*Create.vbhtml*了教程前面的基架的视图模板。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-161">Below is the *Create.vbhtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="5c4c0-162">以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-162">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-vbhtml[Main](adding-validation-to-the-model/samples/sample6.vbhtml)]

<span data-ttu-id="5c4c0-163">请注意代码如何使用`Html.EditorFor`帮助器输出`<input>`每个元素`Movie`属性。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-163">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="5c4c0-164">此帮助器的旁边是调用`Html.ValidationMessageFor`帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-164">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="5c4c0-165">这两个帮助器方法使用由控制器传递给视图的模型对象 (在这种情况下，`Movie`对象)。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-165">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="5c4c0-166">它们在自动显示为相应的模型和显示错误消息上指定的验证特性。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-166">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="5c4c0-167">有关这种方法非常令人愉快的是，在控制器和创建视图模板都不知道任何有关强制实施的实际的验证规则或显示的特定错误消息。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-167">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="5c4c0-168">仅可在 `Movie` 类中指定验证规则和错误字符串。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-168">The validation rules and the error strings are specified only in the `Movie` class.</span></span>

<span data-ttu-id="5c4c0-169">如果你想要以后更改验证逻辑，你可以这样在一个位置。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-169">If you want to change the validation logic later, you can do so in exactly one place.</span></span> <span data-ttu-id="5c4c0-170">无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-170">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="5c4c0-171">这使代码非常简洁，并且更易于维护和改进。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-171">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="5c4c0-172">这意味着对 DRY 原则的完全遵守。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-172">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="5c4c0-173">添加到影片模型格式设置</span><span class="sxs-lookup"><span data-stu-id="5c4c0-173">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="5c4c0-174">打开*Movie.vb*文件。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-174">Open the *Movie.vb* file.</span></span> <span data-ttu-id="5c4c0-175">[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供内置集以及验证特性的格式设置属性。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-175">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="5c4c0-176">将应用[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性和[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)枚举值到发布日期和价格字段。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-176">You'll apply the [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute and a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="5c4c0-177">下面的代码演示`ReleaseDate`和`Price`使用相应的属性[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-177">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample7.vb)]

<span data-ttu-id="5c4c0-178">或者，你可以显式设置[ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx)值。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-178">Alternatively, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="5c4c0-179">下面的代码演示具有日期格式字符串的发行日期属性 (也就是说，"d")。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-179">The following code shows the release date property with a date format string (namely, "d").</span></span> <span data-ttu-id="5c4c0-180">将使用此参数来指定你不想为时间作为发布日期的一部分。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-180">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample8.vb)]

<span data-ttu-id="5c4c0-181">下面的代码格式`Price`属性作为货币。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-181">The following code formats the `Price` property as currency.</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample9.vb)]

<span data-ttu-id="5c4c0-182">完整`Movie`类如下所示。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-182">The complete `Movie` class is shown below.</span></span>

[!code-vb[Main](adding-validation-to-the-model/samples/sample10.vb)]

<span data-ttu-id="5c4c0-183">运行应用程序，并浏览到`Movies`控制器。</span><span class="sxs-lookup"><span data-stu-id="5c4c0-183">Run the application and browse to the `Movies` controller.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

<span data-ttu-id="5c4c0-185">在序列的下一步部分中，我们将查看应用程序并进行一些改进的自动生成`Details`和`Delete`方法...</span><span class="sxs-lookup"><span data-stu-id="5c4c0-185">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods..</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5c4c0-186">[上一页](adding-a-new-field.md)
> [下一页](improving-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="5c4c0-186">[Previous](adding-a-new-field.md)
[Next](improving-the-details-and-delete-methods.md)</span></span>
