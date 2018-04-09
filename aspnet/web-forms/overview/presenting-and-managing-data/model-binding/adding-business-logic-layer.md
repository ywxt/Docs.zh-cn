---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 添加到使用模型绑定和 web 窗体的项目的业务逻辑层 |Microsoft 文档
author: tfitzmac
description: 本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互详细直接-...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: 25e887bdc316abf65c780bb6c8d075e938e85064
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="c0682-104">添加到使用模型绑定和 web 窗体的项目的业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="c0682-104">Adding business logic layer to a project that uses model binding and web forms</span></span>
====================
<span data-ttu-id="c0682-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c0682-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="c0682-106">本系列教程演示使用模型绑定的 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="c0682-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="c0682-107">模型绑定使数据交互更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource）。</span><span class="sxs-lookup"><span data-stu-id="c0682-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="c0682-108">这一系列开头介绍性材料，更高版本的教程中移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="c0682-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="c0682-109">本教程演示如何使用业务逻辑层模型绑定。</span><span class="sxs-lookup"><span data-stu-id="c0682-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="c0682-110">你将设置要指定除当前页的对象用于调用数据方法的 OnCallingDataMethods 成员。</span><span class="sxs-lookup"><span data-stu-id="c0682-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="c0682-111">本教程中创建的项目上[早期](retrieving-data.md)的序列部分。</span><span class="sxs-lookup"><span data-stu-id="c0682-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="c0682-112">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)在 C# 或 VB.完整项目</span><span class="sxs-lookup"><span data-stu-id="c0682-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="c0682-113">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="c0682-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="c0682-114">它使用 Visual Studio 2012 模板，这是本教程中所示的 Visual Studio 2013 模板过程稍有不同。</span><span class="sxs-lookup"><span data-stu-id="c0682-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="c0682-115">你将生成</span><span class="sxs-lookup"><span data-stu-id="c0682-115">What you'll build</span></span>

<span data-ttu-id="c0682-116">模型绑定，可将数据交互代码放在 web 页的代码隐藏文件中或在单独的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="c0682-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="c0682-117">前面的教程已经演示了如何对数据交互代码中使用代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="c0682-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="c0682-118">此方法适用于小型站点，但它可能会导致大型站点进行维护时代码重复和面临更大困难。</span><span class="sxs-lookup"><span data-stu-id="c0682-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="c0682-119">这也可以是很难以编程方式测试驻留在代码隐藏文件，因为没有抽象层的代码。</span><span class="sxs-lookup"><span data-stu-id="c0682-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="c0682-120">若要集中的数据交互代码，可以创建包含所有与数据进行交互的逻辑业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="c0682-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="c0682-121">然后，你会从你的 web 页面调用业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="c0682-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="c0682-122">本教程演示如何移动的所有代码都写入到业务逻辑层，前面的教程中，然后使用该代码从页。</span><span class="sxs-lookup"><span data-stu-id="c0682-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="c0682-123">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="c0682-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="c0682-124">将代码从代码隐藏文件移到业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="c0682-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="c0682-125">更改你的数据绑定控件，以调用业务逻辑层中的方法</span><span class="sxs-lookup"><span data-stu-id="c0682-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="c0682-126">创建业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="c0682-126">Create business logic layer</span></span>

<span data-ttu-id="c0682-127">现在，你将创建从 web 页调用的类。</span><span class="sxs-lookup"><span data-stu-id="c0682-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="c0682-128">此类中的方法类似于你在前面的教程中使用的方法，并且包括值提供程序属性。</span><span class="sxs-lookup"><span data-stu-id="c0682-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="c0682-129">首先，添加一个名为的新文件夹**BLL**。</span><span class="sxs-lookup"><span data-stu-id="c0682-129">First, add a new folder called **BLL**.</span></span>

![添加文件夹](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="c0682-131">在 BLL 文件夹中，创建一个名为的新类**SchoolBL.cs**。</span><span class="sxs-lookup"><span data-stu-id="c0682-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="c0682-132">它将包含所有原先在代码隐藏文件中的数据操作。</span><span class="sxs-lookup"><span data-stu-id="c0682-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="c0682-133">方法代码隐藏文件中的方法几乎相同，但会包括一些更改。</span><span class="sxs-lookup"><span data-stu-id="c0682-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="c0682-134">要注意的最重要更改是不再执行中的实例内的代码**页**类。</span><span class="sxs-lookup"><span data-stu-id="c0682-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="c0682-135">页类包含**TryUpdateModel**方法和**ModelState**属性。</span><span class="sxs-lookup"><span data-stu-id="c0682-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="c0682-136">当此代码移到业务逻辑层中时，你不再有页类来调用这些成员的实例。</span><span class="sxs-lookup"><span data-stu-id="c0682-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="c0682-137">若要获取解决此问题，你必须添加**ModelMethodContext**访问 TryUpdateModel 或 ModelState 任何方法参数。</span><span class="sxs-lookup"><span data-stu-id="c0682-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="c0682-138">使用此 ModelMethodContext 参数调用 TryUpdateModel 或检索 ModelState。</span><span class="sxs-lookup"><span data-stu-id="c0682-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="c0682-139">不需要更改 web 页后，可以为此新参数帐户中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="c0682-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="c0682-140">SchoolBL.cs 中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="c0682-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="c0682-141">修改现有的页面，从业务逻辑层检索数据</span><span class="sxs-lookup"><span data-stu-id="c0682-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="c0682-142">最后，你将从代码隐藏文件使用业务逻辑层中使用查询转换 Students.aspx、 AddStudent.aspx 和 Courses.aspx 的页。</span><span class="sxs-lookup"><span data-stu-id="c0682-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="c0682-143">学生、 AddStudent 和课程的代码隐藏文件，删除或注释掉以下的查询方法：</span><span class="sxs-lookup"><span data-stu-id="c0682-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="c0682-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="c0682-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="c0682-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="c0682-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="c0682-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="c0682-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="c0682-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="c0682-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="c0682-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="c0682-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="c0682-149">现在应与数据操作的代码隐藏文件中将出现任何代码。</span><span class="sxs-lookup"><span data-stu-id="c0682-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="c0682-150">**OnCallingDataMethods**事件处理程序，可指定要使用的数据方法的对象。</span><span class="sxs-lookup"><span data-stu-id="c0682-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="c0682-151">Students.aspx，在为该事件处理程序添加一个值，并将数据方法的名称更改为业务逻辑类中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="c0682-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="c0682-152">在 Students.aspx 代码隐藏文件中，定义的事件处理程序 CallingDataMethods 事件。</span><span class="sxs-lookup"><span data-stu-id="c0682-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="c0682-153">在此事件处理程序中，你可以指定数据操作的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="c0682-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="c0682-154">在 AddStudent.aspx，进行类似更改。</span><span class="sxs-lookup"><span data-stu-id="c0682-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="c0682-155">在 Courses.aspx，进行类似更改。</span><span class="sxs-lookup"><span data-stu-id="c0682-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="c0682-156">运行应用程序，并注意的所有页函数与在其之前。</span><span class="sxs-lookup"><span data-stu-id="c0682-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="c0682-157">验证逻辑还可以正常工作。</span><span class="sxs-lookup"><span data-stu-id="c0682-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c0682-158">结束语</span><span class="sxs-lookup"><span data-stu-id="c0682-158">Conclusion</span></span>

<span data-ttu-id="c0682-159">在本教程中，你重新构建应用程序使用的数据访问层和业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="c0682-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="c0682-160">你指定数据控件使用一个对象，它不数据操作的当前页。</span><span class="sxs-lookup"><span data-stu-id="c0682-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c0682-161">上一篇</span><span class="sxs-lookup"><span data-stu-id="c0682-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
