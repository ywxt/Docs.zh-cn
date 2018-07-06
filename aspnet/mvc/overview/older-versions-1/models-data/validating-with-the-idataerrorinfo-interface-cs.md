---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: 验证使用 IDataErrorInfo 接口 (C#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何通过在 model 类中实现 IDataErrorInfo 接口显示自定义验证错误消息。
ms.author: aspnetcontent
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: d3d3e379e5b2cfdd1385d724c0d9bf2a83ce339a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836022"
---
<a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="6df69-103">使用 IDataErrorInfo 接口 (C#) 进行验证</span><span class="sxs-lookup"><span data-stu-id="6df69-103">Validating with the IDataErrorInfo Interface (C#)</span></span>
====================
<span data-ttu-id="6df69-104">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="6df69-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="6df69-105">Stephen Walther 演示了如何通过在 model 类中实现 IDataErrorInfo 接口显示自定义验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="6df69-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>


<span data-ttu-id="6df69-106">本教程的目的是说明一种方法在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="6df69-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="6df69-107">了解如何防止有人将 HTML 窗体提交而无需为所需的窗体字段提供值。</span><span class="sxs-lookup"><span data-stu-id="6df69-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="6df69-108">在本教程中，您将学习如何使用 IErrorDataInfo 接口来执行验证。</span><span class="sxs-lookup"><span data-stu-id="6df69-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="6df69-109">假设</span><span class="sxs-lookup"><span data-stu-id="6df69-109">Assumptions</span></span>

<span data-ttu-id="6df69-110">在本教程中，我将使用 MoviesDB 数据库和电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="6df69-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="6df69-111">此表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="6df69-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>


| <span data-ttu-id="6df69-112">**列名称**</span><span class="sxs-lookup"><span data-stu-id="6df69-112">**Column Name**</span></span> | <span data-ttu-id="6df69-113">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="6df69-113">**Data Type**</span></span> | <span data-ttu-id="6df69-114">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="6df69-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6df69-115">Id</span><span class="sxs-lookup"><span data-stu-id="6df69-115">Id</span></span> | <span data-ttu-id="6df69-116">Int</span><span class="sxs-lookup"><span data-stu-id="6df69-116">Int</span></span> | <span data-ttu-id="6df69-117">False</span><span class="sxs-lookup"><span data-stu-id="6df69-117">False</span></span> |
| <span data-ttu-id="6df69-118">标题</span><span class="sxs-lookup"><span data-stu-id="6df69-118">Title</span></span> | <span data-ttu-id="6df69-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="6df69-119">Nvarchar(100)</span></span> | <span data-ttu-id="6df69-120">False</span><span class="sxs-lookup"><span data-stu-id="6df69-120">False</span></span> |
| <span data-ttu-id="6df69-121">主管</span><span class="sxs-lookup"><span data-stu-id="6df69-121">Director</span></span> | <span data-ttu-id="6df69-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="6df69-122">Nvarchar(100)</span></span> | <span data-ttu-id="6df69-123">False</span><span class="sxs-lookup"><span data-stu-id="6df69-123">False</span></span> |
| <span data-ttu-id="6df69-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="6df69-124">DateReleased</span></span> | <span data-ttu-id="6df69-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="6df69-125">DateTime</span></span> | <span data-ttu-id="6df69-126">False</span><span class="sxs-lookup"><span data-stu-id="6df69-126">False</span></span> |


<span data-ttu-id="6df69-127">在本教程中，我可以使用 Microsoft 实体框架来生成我的数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="6df69-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="6df69-128">实体框架生成的 Movie 类显示在图 1 中。</span><span class="sxs-lookup"><span data-stu-id="6df69-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>


<span data-ttu-id="6df69-129">[![电影实体](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6df69-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span></span>

<span data-ttu-id="6df69-130">**图 01**: 电影实体 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="6df69-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="6df69-131">若要了解有关使用实体框架生成您的数据库模型类的详细信息，请参阅我的教程，标题为使用 Entity Framework 创建模型类。</span><span class="sxs-lookup"><span data-stu-id="6df69-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>


## <a name="the-controller-class"></a><span data-ttu-id="6df69-132">控制器类</span><span class="sxs-lookup"><span data-stu-id="6df69-132">The Controller Class</span></span>

<span data-ttu-id="6df69-133">我们使用主控制器到列表的电影，并创建新影片。</span><span class="sxs-lookup"><span data-stu-id="6df69-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="6df69-134">此类的代码包含在列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="6df69-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="6df69-135">**代码清单 1-Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="6df69-135">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="6df69-136">在列表 1 中的 Home 控制器类包含两个 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="6df69-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="6df69-137">第一个操作会显示用于创建新的电影的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="6df69-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="6df69-138">第二个 create （） 操作执行新电影的实际插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="6df69-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="6df69-139">显示的第一个 create （） 操作的窗体提交到服务器时，将调用第二个 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="6df69-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="6df69-140">请注意第二个 create （） 操作中包含以下代码行：</span><span class="sxs-lookup"><span data-stu-id="6df69-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="6df69-141">验证错误时，IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="6df69-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="6df69-142">在这种情况下，重新创建视图，它包含用于创建电影的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="6df69-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="6df69-143">创建一个分部类</span><span class="sxs-lookup"><span data-stu-id="6df69-143">Creating a Partial Class</span></span>

<span data-ttu-id="6df69-144">由实体框架生成的 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="6df69-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="6df69-145">展开解决方案资源管理器窗口中的 MoviesDBModel.edmx 文件并在代码编辑器中打开 MoviesDBModel.Designer.cs 文件访问时，可以看到 Movie 类的代码 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="6df69-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>


<span data-ttu-id="6df69-146">[![电影实体的代码](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="6df69-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span></span>

<span data-ttu-id="6df69-147">**图 02**： 电影实体的代码 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="6df69-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>


<span data-ttu-id="6df69-148">Movie 类是分部类。</span><span class="sxs-lookup"><span data-stu-id="6df69-148">The Movie class is a partial class.</span></span> <span data-ttu-id="6df69-149">这意味着，我们可以添加具有相同名称的扩展的 Movie 类功能的另一个分部类。</span><span class="sxs-lookup"><span data-stu-id="6df69-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="6df69-150">我们将向新的分部类添加我们的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="6df69-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="6df69-151">向 Models 文件夹中添加清单 2 中的类。</span><span class="sxs-lookup"><span data-stu-id="6df69-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="6df69-152">**代码清单 2-Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="6df69-152">**Listing 2 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="6df69-153">请注意，代码清单 2 中的类包含*分部*修饰符。</span><span class="sxs-lookup"><span data-stu-id="6df69-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="6df69-154">任何方法或属性将添加到此类成为由实体框架生成的 Movie 类的一部分。</span><span class="sxs-lookup"><span data-stu-id="6df69-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="6df69-155">添加 OnChanging 和 OnChanged 分部方法</span><span class="sxs-lookup"><span data-stu-id="6df69-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="6df69-156">当实体框架生成的实体类时，实体框架分部方法向类添加了自动。</span><span class="sxs-lookup"><span data-stu-id="6df69-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="6df69-157">实体框架生成 OnChanging 和 OnChanged 对应于每个属性的类的分部方法。</span><span class="sxs-lookup"><span data-stu-id="6df69-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="6df69-158">对于 Movie 类，实体框架将创建以下方法：</span><span class="sxs-lookup"><span data-stu-id="6df69-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="6df69-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="6df69-159">OnIdChanging</span></span>
- <span data-ttu-id="6df69-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="6df69-160">OnIdChanged</span></span>
- <span data-ttu-id="6df69-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="6df69-161">OnTitleChanging</span></span>
- <span data-ttu-id="6df69-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="6df69-162">OnTitleChanged</span></span>
- <span data-ttu-id="6df69-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="6df69-163">OnDirectorChanging</span></span>
- <span data-ttu-id="6df69-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="6df69-164">OnDirectorChanged</span></span>
- <span data-ttu-id="6df69-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="6df69-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="6df69-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="6df69-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="6df69-167">相应的属性发生更改之前，OnChanging 方法称为右。</span><span class="sxs-lookup"><span data-stu-id="6df69-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="6df69-168">OnChanged 方法调用正确后更改的属性。</span><span class="sxs-lookup"><span data-stu-id="6df69-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="6df69-169">您可以利用这些分部方法以将验证逻辑添加到电影类。</span><span class="sxs-lookup"><span data-stu-id="6df69-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="6df69-170">更新列表 3 中的 Movie 类验证的标题和主管属性分配非空值。</span><span class="sxs-lookup"><span data-stu-id="6df69-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="6df69-171">分部方法是不需要实现的类中定义的方法。</span><span class="sxs-lookup"><span data-stu-id="6df69-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="6df69-172">如果未实现分部方法，编译器会删除方法签名，并因此方法的所有调用都是没有与分部方法关联的运行时成本。</span><span class="sxs-lookup"><span data-stu-id="6df69-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="6df69-173">在 Visual Studio 代码编辑器中，您可以通过键入关键字添加的分部方法*分部*跟一个空格，若要查看的部分实现列表。</span><span class="sxs-lookup"><span data-stu-id="6df69-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>


<span data-ttu-id="6df69-174">**代码清单 3-Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="6df69-174">**Listing 3 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="6df69-175">例如，如果尝试将空字符串分配到的 Title 属性，然后一条错误消息分配给一个名为词典\_错误。</span><span class="sxs-lookup"><span data-stu-id="6df69-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="6df69-176">在此情况下，执行任何操作实际上将空字符串分配到的 Title 属性，但发生错误添加到私有\_错误字段。</span><span class="sxs-lookup"><span data-stu-id="6df69-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="6df69-177">我们需要实现 IDataErrorInfo 接口来公开这些验证错误到 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="6df69-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="6df69-178">实现 IDataErrorInfo 接口</span><span class="sxs-lookup"><span data-stu-id="6df69-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="6df69-179">自第一个版本，IDataErrorInfo 接口已经成为.NET framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="6df69-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="6df69-180">此接口是一个非常简单的接口：</span><span class="sxs-lookup"><span data-stu-id="6df69-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="6df69-181">如果一个类实现 IDataErrorInfo 接口，ASP.NET MVC 框架将创建类的实例时使用此接口。</span><span class="sxs-lookup"><span data-stu-id="6df69-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="6df69-182">例如，主页控制器 create （） 操作接受 Movie 类的实例：</span><span class="sxs-lookup"><span data-stu-id="6df69-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="6df69-183">ASP.NET MVC 框架创建电影使用模型联编程序 (DefaultModelBinder) 传递给 create （） 操作的实例。</span><span class="sxs-lookup"><span data-stu-id="6df69-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="6df69-184">模型联编程序负责通过将 HTML 窗体字段绑定到 Movie 对象的实例创建电影对象的实例。</span><span class="sxs-lookup"><span data-stu-id="6df69-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="6df69-185">DefaultModelBinder 检测类实现 IDataErrorInfo 接口。</span><span class="sxs-lookup"><span data-stu-id="6df69-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="6df69-186">如果一个类实现此接口的模型联编程序会调用类的每个属性的 IDataErrorInfo.this 索引器。</span><span class="sxs-lookup"><span data-stu-id="6df69-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="6df69-187">如果索引器返回一条错误消息的模型联编程序将添加到模型状态自动此错误消息。</span><span class="sxs-lookup"><span data-stu-id="6df69-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="6df69-188">DefaultModelBinder 还会检查 IDataErrorInfo.Error 属性。</span><span class="sxs-lookup"><span data-stu-id="6df69-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="6df69-189">此属性用于表示与类关联的非属性特定验证错误。</span><span class="sxs-lookup"><span data-stu-id="6df69-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="6df69-190">例如，你可能想要强制实施依赖于的 Movie 类的多个属性的值的验证规则。</span><span class="sxs-lookup"><span data-stu-id="6df69-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="6df69-191">在这种情况下，您将从错误属性返回验证错误。</span><span class="sxs-lookup"><span data-stu-id="6df69-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="6df69-192">列表 4 中更新的 Movie 类实现 IDataErrorInfo 接口。</span><span class="sxs-lookup"><span data-stu-id="6df69-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="6df69-193">**列表 4-Models\Movie.cs （实现 IDataErrorInfo）**</span><span class="sxs-lookup"><span data-stu-id="6df69-193">**Listing 4 - Models\Movie.cs (implements IDataErrorInfo)**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="6df69-194">列表 4 中的索引器属性检查\_错误集合，以查看它是否包含属性名称对应的密钥传递给索引器。</span><span class="sxs-lookup"><span data-stu-id="6df69-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="6df69-195">如果没有与属性关联的验证错误则返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="6df69-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="6df69-196">不需要修改主控制器，以任何方式使用修改后的 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="6df69-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="6df69-197">图 3 中显示的页说明了当标题或总监窗体字段中不输入任何值时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="6df69-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>


<span data-ttu-id="6df69-198">[![自动创建的操作方法](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="6df69-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span></span>

<span data-ttu-id="6df69-199">**图 03**： 具有缺失值的窗体 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6df69-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>


<span data-ttu-id="6df69-200">请注意 DateReleased 值自动进行验证。</span><span class="sxs-lookup"><span data-stu-id="6df69-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="6df69-201">因为 DateReleased 属性不接受 NULL 值，DefaultModelBinder 验证错误，此属性会自动生成时它不具有值。</span><span class="sxs-lookup"><span data-stu-id="6df69-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="6df69-202">如果你想要修改的错误消息的 DateReleased 属性，则需要创建自定义模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="6df69-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="6df69-203">总结</span><span class="sxs-lookup"><span data-stu-id="6df69-203">Summary</span></span>

<span data-ttu-id="6df69-204">在本教程中，您学习了如何使用 IDataErrorInfo 接口生成验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="6df69-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="6df69-205">首先，我们创建了部分的 Movie 类的部分实体框架所生成的 Movie 类功能进行扩展。</span><span class="sxs-lookup"><span data-stu-id="6df69-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="6df69-206">接下来，我们的 Movie 类 OnTitleChanging() 和 OnDirectorChanging() 分部方法添加验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="6df69-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="6df69-207">最后，我们实现了 IDataErrorInfo 接口以便公开这些验证消息到 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="6df69-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6df69-208">[上一页](performing-simple-validation-cs.md)
> [下一页](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="6df69-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>
