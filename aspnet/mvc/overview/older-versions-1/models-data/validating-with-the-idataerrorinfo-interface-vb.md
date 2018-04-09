---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: 验证 IDataErrorInfo 接口 (VB) |Microsoft 文档
author: StephenWalther
description: Stephen Walther 演示了如何通过模型类中实现该 IDataErrorInfo 接口显示自定义的验证错误消息。
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 60df0f934432484e0c97e0caef25c15605beb14f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="validating-with-the-idataerrorinfo-interface-vb"></a><span data-ttu-id="c7f0c-103">验证 IDataErrorInfo 接口 (VB)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-103">Validating with the IDataErrorInfo Interface (VB)</span></span>
====================
<span data-ttu-id="c7f0c-104">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="c7f0c-105">Stephen Walther 演示了如何通过模型类中实现该 IDataErrorInfo 接口显示自定义的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>


<span data-ttu-id="c7f0c-106">本教程旨在向 ASP.NET MVC 应用程序中执行验证说明一种方法。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="c7f0c-107">了解如何防止别人提交一个 HTML 表单，而无需为所需的窗体字段提供值。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="c7f0c-108">在本教程中，你将了解如何通过使用 IErrorDataInfo 界面执行验证。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="c7f0c-109">假设</span><span class="sxs-lookup"><span data-stu-id="c7f0c-109">Assumptions</span></span>

<span data-ttu-id="c7f0c-110">在本教程中，我将使用 MoviesDB 数据库和电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="c7f0c-111">此表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="c7f0c-111">This table has the following columns:</span></span>

<a id="0.6_table01"></a>


| <span data-ttu-id="c7f0c-112">**列名称**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-112">**Column Name**</span></span> | <span data-ttu-id="c7f0c-113">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-113">**Data Type**</span></span> | <span data-ttu-id="c7f0c-114">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c7f0c-115">Id</span><span class="sxs-lookup"><span data-stu-id="c7f0c-115">Id</span></span> | <span data-ttu-id="c7f0c-116">Int</span><span class="sxs-lookup"><span data-stu-id="c7f0c-116">Int</span></span> | <span data-ttu-id="c7f0c-117">False</span><span class="sxs-lookup"><span data-stu-id="c7f0c-117">False</span></span> |
| <span data-ttu-id="c7f0c-118">标题</span><span class="sxs-lookup"><span data-stu-id="c7f0c-118">Title</span></span> | <span data-ttu-id="c7f0c-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-119">Nvarchar(100)</span></span> | <span data-ttu-id="c7f0c-120">False</span><span class="sxs-lookup"><span data-stu-id="c7f0c-120">False</span></span> |
| <span data-ttu-id="c7f0c-121">控制器</span><span class="sxs-lookup"><span data-stu-id="c7f0c-121">Director</span></span> | <span data-ttu-id="c7f0c-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-122">Nvarchar(100)</span></span> | <span data-ttu-id="c7f0c-123">False</span><span class="sxs-lookup"><span data-stu-id="c7f0c-123">False</span></span> |
| <span data-ttu-id="c7f0c-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="c7f0c-124">DateReleased</span></span> | <span data-ttu-id="c7f0c-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="c7f0c-125">DateTime</span></span> | <span data-ttu-id="c7f0c-126">False</span><span class="sxs-lookup"><span data-stu-id="c7f0c-126">False</span></span> |


<span data-ttu-id="c7f0c-127">在本教程中，我可以使用 Microsoft 实体框架生成我的数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="c7f0c-128">实体框架生成的电影类如图 1 所示。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>


<span data-ttu-id="c7f0c-129">[![电影实体](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)</span></span>

<span data-ttu-id="c7f0c-130">**图 01**: 电影实体 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c7f0c-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="c7f0c-131">若要了解有关使用实体框架生成你的数据库模型类的详细信息，请参阅我的教程标题为与实体框架创建模型类。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>


## <a name="the-controller-class"></a><span data-ttu-id="c7f0c-132">控制器类</span><span class="sxs-lookup"><span data-stu-id="c7f0c-132">The Controller Class</span></span>

<span data-ttu-id="c7f0c-133">我们将使用到列表的电影的主页控制器，并创建新影片。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="c7f0c-134">列表 1 中包含此类代码。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="c7f0c-135">**Listing 1 - Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-135">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

<span data-ttu-id="c7f0c-136">列表 1 中的主页控制器类包含两个 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="c7f0c-137">第一项操作显示用于创建新的影片的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="c7f0c-138">第二个 create （） 操作执行新的影片实际插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="c7f0c-139">显示的第一个 create （） 操作的窗体提交到服务器时，将调用第二个 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="c7f0c-140">请注意，第二个 create （） 操作包含以下代码行：</span><span class="sxs-lookup"><span data-stu-id="c7f0c-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

<span data-ttu-id="c7f0c-141">验证错误时，IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="c7f0c-142">在这种情况下，创建视图，其中包含用于创建一部电影的 HTML 窗体将重新显示。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="c7f0c-143">创建分部类</span><span class="sxs-lookup"><span data-stu-id="c7f0c-143">Creating a Partial Class</span></span>

<span data-ttu-id="c7f0c-144">电影类由实体框架生成。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="c7f0c-145">如果你展开解决方案资源管理器窗口中的 MoviesDBModel.edmx 文件并打开 MoviesDBModel.Designer.vb 文件在代码编辑器中，你可以看到电影类的代码 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.vb file in the Code Editor (see Figure 2).</span></span>


<span data-ttu-id="c7f0c-146">[![电影实体的代码](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)</span></span>

<span data-ttu-id="c7f0c-147">**图 02**： 电影实体的代码 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="c7f0c-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png))</span></span>


<span data-ttu-id="c7f0c-148">电影类是分部类。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-148">The Movie class is a partial class.</span></span> <span data-ttu-id="c7f0c-149">这意味着，我们可以添加具有相同名称来扩展电影类的功能的另一个分部类。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="c7f0c-150">我们将添加到新的分部类的我们验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="c7f0c-151">将列出 2 中的类添加到 Models 文件夹。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="c7f0c-152">**列出 2-Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-152">**Listing 2 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

<span data-ttu-id="c7f0c-153">请注意，列出 2 中的类包括*部分*修饰符。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="c7f0c-154">任何方法或属性添加到此类成为生成实体框架的电影类的一部分。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="c7f0c-155">添加 OnChanging 和 OnChanged 分部方法</span><span class="sxs-lookup"><span data-stu-id="c7f0c-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="c7f0c-156">当实体框架生成实体类时，实体框架分部方法与类会自动添加。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="c7f0c-157">实体框架生成 OnChanging 和 OnChanged 对应于每个属性类的分部方法。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="c7f0c-158">对于电影类中，实体框架将创建以下方法：</span><span class="sxs-lookup"><span data-stu-id="c7f0c-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="c7f0c-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="c7f0c-159">OnIdChanging</span></span>
- <span data-ttu-id="c7f0c-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="c7f0c-160">OnIdChanged</span></span>
- <span data-ttu-id="c7f0c-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="c7f0c-161">OnTitleChanging</span></span>
- <span data-ttu-id="c7f0c-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="c7f0c-162">OnTitleChanged</span></span>
- <span data-ttu-id="c7f0c-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="c7f0c-163">OnDirectorChanging</span></span>
- <span data-ttu-id="c7f0c-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="c7f0c-164">OnDirectorChanged</span></span>
- <span data-ttu-id="c7f0c-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="c7f0c-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="c7f0c-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="c7f0c-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="c7f0c-167">对应的属性发生更改之前，称为右 OnChanging 方法。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="c7f0c-168">OnChanged 方法调用右后更改的属性。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="c7f0c-169">你可以利用这些分部方法，以向电影类添加验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="c7f0c-170">更新列出 3 中的电影类验证的标题和控制器属性分配非空值。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="c7f0c-171">分部方法是你不需要实现的类中定义的方法。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="c7f0c-172">如果不实现分部方法然后编译器移除方法签名，并对存在的方法的所有调用都是分部方法不运行时收费。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="c7f0c-173">在 Visual Studio 代码编辑器中，你可以通过键入关键字添加分部方法*部分*跟一个空格，以查看它们实现的列表。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>


<span data-ttu-id="c7f0c-174">**Listing 3 - Models\Movie.vb**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-174">**Listing 3 - Models\Movie.vb**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

<span data-ttu-id="c7f0c-175">例如，如果你尝试将一个空字符串分配给 Title 属性，则一条错误消息分配给一个名为词典\_错误。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="c7f0c-176">此时，会执行任何操作实际时将一个空字符串分配给 Title 属性和错误添加到私有\_错误字段。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="c7f0c-177">我们需要实现 IDataErrorInfo 接口可公开的 ASP.NET MVC framework 这些验证错误。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="c7f0c-178">实现 IDataErrorInfo 接口</span><span class="sxs-lookup"><span data-stu-id="c7f0c-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="c7f0c-179">IDataErrorInfo 接口起的第一个版本已是.NET framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="c7f0c-180">此接口是一个非常简单的接口：</span><span class="sxs-lookup"><span data-stu-id="c7f0c-180">This interface is a very simple interface:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

<span data-ttu-id="c7f0c-181">如果一个类实现 IDataErrorInfo 接口，则 ASP.NET MVC framework 创建类的实例时将使用此接口。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="c7f0c-182">例如，create （） 操作中的主页控制器接受电影类的实例：</span><span class="sxs-lookup"><span data-stu-id="c7f0c-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

<span data-ttu-id="c7f0c-183">ASP.NET MVC framework 创建影片通过使用模型联编程序 (DefaultModelBinder) 传递给 create （） 操作的实例。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="c7f0c-184">模型联编程序负责通过将 HTML 窗体字段绑定到影片对象的实例创建电影对象的实例。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="c7f0c-185">DefaultModelBinder 检测类实现 IDataErrorInfo 接口。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="c7f0c-186">如果一个类实现此接口模型联编程序调用类的每个属性的 IDataErrorInfo.this 索引器。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="c7f0c-187">如果索引器返回一条错误消息模型联编程序将添加此错误消息，以自动模型状态。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="c7f0c-188">DefaultModelBinder 还检查 IDataErrorInfo.Error 属性。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="c7f0c-189">此属性用于表示与类关联的非属性特定验证错误。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="c7f0c-190">例如，你可能想要执行验证规则依赖于电影类的多个属性的值。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="c7f0c-191">在这种情况下，你将从错误属性返回验证错误。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="c7f0c-192">列出 4 中更新后的电影类实现 IDataErrorInfo 接口。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="c7f0c-193">**列出 4-Models\Movie.vb （实现 IDataErrorInfo）**</span><span class="sxs-lookup"><span data-stu-id="c7f0c-193">**Listing 4 - Models\Movie.vb (implements IDataErrorInfo)**</span></span>

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

<span data-ttu-id="c7f0c-194">在列出 4 中，检查索引器属性\_errors 集合，可以查看它是否包含对应于的属性名称的密钥传递给索引器。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="c7f0c-195">如果没有任何与属性关联的验证错误则返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="c7f0c-196">你不需要修改任何方式来使用修改后的电影类中的主页控制器。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="c7f0c-197">图 3 中显示的页面说明了用于标题或控制器窗体字段中不输入任何值时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>


<span data-ttu-id="c7f0c-198">[![自动创建操作方法](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)</span></span>

<span data-ttu-id="c7f0c-199">**图 03**： 的窗体具有缺失值 ([单击以查看实际尺寸的图像](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c7f0c-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png))</span></span>


<span data-ttu-id="c7f0c-200">请注意，自动验证 DateReleased 值。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="c7f0c-201">因为 DateReleased 属性不接受 NULL 值，DefaultModelBinder 验证错误，此属性会自动生成时它不具有值。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="c7f0c-202">如果你想要修改 DateReleased 属性的错误消息，则需要创建自定义模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="c7f0c-203">总结</span><span class="sxs-lookup"><span data-stu-id="c7f0c-203">Summary</span></span>

<span data-ttu-id="c7f0c-204">在本教程中，您学习了如何使用 IDataErrorInfo 接口生成验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="c7f0c-205">首先，我们创建扩展的功能由实体框架生成的部分电影类的分部电影类。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="c7f0c-206">接下来，我们验证逻辑添加到的电影类 OnTitleChanging() 和 OnDirectorChanging() 分部方法。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="c7f0c-207">最后，我们实现 IDataErrorInfo 接口才能公开的 ASP.NET MVC framework 这些验证消息。</span><span class="sxs-lookup"><span data-stu-id="c7f0c-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c7f0c-208">[上一页](performing-simple-validation-vb.md)
> [下一页](validating-with-a-service-layer-vb.md)</span><span class="sxs-lookup"><span data-stu-id="c7f0c-208">[Previous](performing-simple-validation-vb.md)
[Next](validating-with-a-service-layer-vb.md)</span></span>
