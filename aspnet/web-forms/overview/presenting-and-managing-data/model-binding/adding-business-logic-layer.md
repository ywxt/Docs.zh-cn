---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 使用模型绑定和 web 窗体的项目添加业务逻辑层 |Microsoft Docs
author: Rick-Anderson
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: 4ba1830ce51f257e18880f752b249dbeb77f504e
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021646"
---
<a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="39fa4-104">使用模型绑定和 web 窗体的项目添加业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="39fa4-104">Adding business logic layer to a project that uses model binding and web forms</span></span>
====================
<span data-ttu-id="39fa4-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="39fa4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="39fa4-106">本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。</span><span class="sxs-lookup"><span data-stu-id="39fa4-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="39fa4-107">模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。</span><span class="sxs-lookup"><span data-stu-id="39fa4-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="39fa4-108">本系列开始介绍性材料，后续教程将移动到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="39fa4-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="39fa4-109">本教程演示如何使用业务逻辑层模型绑定。</span><span class="sxs-lookup"><span data-stu-id="39fa4-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="39fa4-110">您将设置 OnCallingDataMethods 成员以指定当前页以外的其他对象用于调用数据方法。</span><span class="sxs-lookup"><span data-stu-id="39fa4-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="39fa4-111">本教程中创建的项目为基础[早期](retrieving-data.md)在本系列的部分。</span><span class="sxs-lookup"><span data-stu-id="39fa4-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="39fa4-112">你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。</span><span class="sxs-lookup"><span data-stu-id="39fa4-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="39fa4-113">可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="39fa4-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="39fa4-114">它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。</span><span class="sxs-lookup"><span data-stu-id="39fa4-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="39fa4-115">你将生成</span><span class="sxs-lookup"><span data-stu-id="39fa4-115">What you'll build</span></span>

<span data-ttu-id="39fa4-116">模型绑定，可将数据交互代码放在 web 页的代码隐藏文件中或在单独的业务逻辑类中。</span><span class="sxs-lookup"><span data-stu-id="39fa4-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="39fa4-117">前面的教程已经演示了如何使用代码隐藏文件进行数据交互的代码。</span><span class="sxs-lookup"><span data-stu-id="39fa4-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="39fa4-118">此方法适用于小型站点，但它可能导致时维护大型站点代码重复和面临更大困难。</span><span class="sxs-lookup"><span data-stu-id="39fa4-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="39fa4-119">它可以是以编程方式测试由于没有抽象层驻留在代码隐藏文件中的代码非常困难。</span><span class="sxs-lookup"><span data-stu-id="39fa4-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="39fa4-120">若要集中进行数据交互代码，可以创建包含所有与数据进行交互的逻辑将业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="39fa4-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="39fa4-121">然后从您的 web 页面中调用业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="39fa4-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="39fa4-122">本教程介绍如何将所有已在前面的教程到业务逻辑层，编写的代码移动，然后使用该代码从页中。</span><span class="sxs-lookup"><span data-stu-id="39fa4-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="39fa4-123">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="39fa4-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="39fa4-124">将代码从代码隐藏文件移到业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="39fa4-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="39fa4-125">更改数据绑定控件，以调用业务逻辑层中的方法</span><span class="sxs-lookup"><span data-stu-id="39fa4-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="39fa4-126">创建业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="39fa4-126">Create business logic layer</span></span>

<span data-ttu-id="39fa4-127">现在，您将创建在 web 页面中调用的类。</span><span class="sxs-lookup"><span data-stu-id="39fa4-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="39fa4-128">此类中的方法看起来类似于前面教程中使用的方法，并包括值提供程序属性。</span><span class="sxs-lookup"><span data-stu-id="39fa4-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="39fa4-129">首先，添加一个名为的新文件夹**BLL**。</span><span class="sxs-lookup"><span data-stu-id="39fa4-129">First, add a new folder called **BLL**.</span></span>

![添加文件夹](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="39fa4-131">在 BLL 文件夹中，创建一个名为的新类**SchoolBL.cs**。</span><span class="sxs-lookup"><span data-stu-id="39fa4-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="39fa4-132">它将包含所有原先位于代码隐藏文件中的数据操作。</span><span class="sxs-lookup"><span data-stu-id="39fa4-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="39fa4-133">方法是在代码隐藏文件中，方法几乎相同，但将包括一些更改。</span><span class="sxs-lookup"><span data-stu-id="39fa4-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="39fa4-134">请注意，最重要的更改是无法再执行中的实例中的代码**页**类。</span><span class="sxs-lookup"><span data-stu-id="39fa4-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="39fa4-135">页类包含**TryUpdateModel**方法并**ModelState**属性。</span><span class="sxs-lookup"><span data-stu-id="39fa4-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="39fa4-136">当此代码移到业务逻辑层中时，再也不调用这些成员的页类的实例。</span><span class="sxs-lookup"><span data-stu-id="39fa4-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="39fa4-137">若要解决此问题，必须添加**ModelMethodContext**访问 TryUpdateModel 或 ModelState 任何方法参数。</span><span class="sxs-lookup"><span data-stu-id="39fa4-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="39fa4-138">使用此 ModelMethodContext 参数来调用 TryUpdateModel 或检索 ModelState。</span><span class="sxs-lookup"><span data-stu-id="39fa4-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="39fa4-139">不需要更改 web 页后，可以为此新参数帐户中的任何内容。</span><span class="sxs-lookup"><span data-stu-id="39fa4-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="39fa4-140">将以下代码替换为 SchoolBL.cs 中的代码。</span><span class="sxs-lookup"><span data-stu-id="39fa4-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="39fa4-141">修改现有页面以从业务逻辑层中检索数据</span><span class="sxs-lookup"><span data-stu-id="39fa4-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="39fa4-142">最后，将从在使用业务逻辑层的代码隐藏文件中使用查询来转换 Students.aspx、 AddStudent.aspx 和 Courses.aspx 的页。</span><span class="sxs-lookup"><span data-stu-id="39fa4-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="39fa4-143">面向学生、 AddStudent 和课程的代码隐藏文件，在删除或注释掉以下的查询方法：</span><span class="sxs-lookup"><span data-stu-id="39fa4-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="39fa4-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="39fa4-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="39fa4-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="39fa4-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="39fa4-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="39fa4-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="39fa4-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="39fa4-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="39fa4-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="39fa4-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="39fa4-149">现在应在与数据操作相关的代码隐藏文件中具有任何代码。</span><span class="sxs-lookup"><span data-stu-id="39fa4-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="39fa4-150">**OnCallingDataMethods**事件处理程序，您可以指定要用于数据方法的对象。</span><span class="sxs-lookup"><span data-stu-id="39fa4-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="39fa4-151">Students.aspx，在添加该事件处理程序的值并将数据方法的名称更改为业务逻辑类中方法的名称。</span><span class="sxs-lookup"><span data-stu-id="39fa4-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="39fa4-152">在 Students.aspx 的代码隐藏文件，定义 CallingDataMethods 事件的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="39fa4-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="39fa4-153">在此事件处理程序中，指定数据操作的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="39fa4-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="39fa4-154">在 AddStudent.aspx，进行类似更改。</span><span class="sxs-lookup"><span data-stu-id="39fa4-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="39fa4-155">在 Courses.aspx，进行类似更改。</span><span class="sxs-lookup"><span data-stu-id="39fa4-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="39fa4-156">运行应用程序，并注意到的所有页函数与在其之前。</span><span class="sxs-lookup"><span data-stu-id="39fa4-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="39fa4-157">验证逻辑也可以正常工作。</span><span class="sxs-lookup"><span data-stu-id="39fa4-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="39fa4-158">结束语</span><span class="sxs-lookup"><span data-stu-id="39fa4-158">Conclusion</span></span>

<span data-ttu-id="39fa4-159">在本教程中，你重新结构化应用程序以使用数据访问层和业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="39fa4-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="39fa4-160">指定数据控件使用不是当前页的数据操作的对象。</span><span class="sxs-lookup"><span data-stu-id="39fa4-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="39fa4-161">上一篇</span><span class="sxs-lookup"><span data-stu-id="39fa4-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
