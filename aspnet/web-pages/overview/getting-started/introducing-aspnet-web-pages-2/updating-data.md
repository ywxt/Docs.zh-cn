---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: Introducing ASP.NET 网页-更新数据库的数据 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何使用 ASP.NET Web Pages (Razor) 时，更新 （更改） 的现有数据库条目。 它假定你已完成一系列第...
ms.author: aspnetcontent
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 948f5b5933669a43bf37dc0317ad644660dc67e9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37842897"
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="30928-104">ASP.NET 网页简介-更新数据库数据</span><span class="sxs-lookup"><span data-stu-id="30928-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>
====================
<span data-ttu-id="30928-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="30928-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="30928-106">本教程演示如何使用 ASP.NET Web Pages (Razor) 时，更新 （更改） 的现有数据库条目。</span><span class="sxs-lookup"><span data-stu-id="30928-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="30928-107">它假定你已完成通过时序[输入数据通过使用窗体使用 ASP.NET Web Pages](entering-data.md)。</span><span class="sxs-lookup"><span data-stu-id="30928-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="30928-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="30928-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="30928-109">如何选择中的单个记录`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="30928-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="30928-110">如何从数据库中读取一条记录。</span><span class="sxs-lookup"><span data-stu-id="30928-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="30928-111">如何预加载窗体中的数据库记录的值。</span><span class="sxs-lookup"><span data-stu-id="30928-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="30928-112">如何更新数据库中的现有记录。</span><span class="sxs-lookup"><span data-stu-id="30928-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="30928-113">如何在页面中存储信息，而不会显示它。</span><span class="sxs-lookup"><span data-stu-id="30928-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="30928-114">如何使用隐藏的字段来存储信息。</span><span class="sxs-lookup"><span data-stu-id="30928-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="30928-115">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="30928-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="30928-116">`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="30928-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="30928-117">SQL`Update`命令。</span><span class="sxs-lookup"><span data-stu-id="30928-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="30928-118">`Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="30928-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="30928-119">隐藏字段 (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="30928-119">Hidden fields (`<input type="hidden">`).</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="30928-120">你将生成</span><span class="sxs-lookup"><span data-stu-id="30928-120">What You'll Build</span></span>

<span data-ttu-id="30928-121">在前面的教程，您学习了如何将一条记录添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="30928-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="30928-122">在这里，您将了解如何以显示用于编辑的记录。</span><span class="sxs-lookup"><span data-stu-id="30928-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="30928-123">在中*电影*页上，你将更新`WebGrid`帮助程序，以便它显示**编辑**每部电影旁边的链接：</span><span class="sxs-lookup"><span data-stu-id="30928-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![WebGrid 显示包括每部电影的编辑链接](updating-data/_static/image1.png)

<span data-ttu-id="30928-125">当您单击**编辑**链接，它将您带入不同的页的电影信息已在窗体：</span><span class="sxs-lookup"><span data-stu-id="30928-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![编辑电影页面，其中显示要编辑的电影](updating-data/_static/image2.png)

<span data-ttu-id="30928-127">您可以更改的任何值。</span><span class="sxs-lookup"><span data-stu-id="30928-127">You can change any of the values.</span></span> <span data-ttu-id="30928-128">当提交所做的更改时，页面中的代码将更新数据库，并将影片列表返回。</span><span class="sxs-lookup"><span data-stu-id="30928-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="30928-129">此过程的一部分方法几乎完全相同*AddMovie.cshtml*因此本教程的大部分将熟悉在上一教程中，创建的页。</span><span class="sxs-lookup"><span data-stu-id="30928-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="30928-130">有几种方法可以实现编辑单个电影的方法。</span><span class="sxs-lookup"><span data-stu-id="30928-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="30928-131">选择显示的方法是因为它是易于实现且易于理解。</span><span class="sxs-lookup"><span data-stu-id="30928-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="30928-132">添加到电影列表的编辑链接</span><span class="sxs-lookup"><span data-stu-id="30928-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="30928-133">若要开始，你将更新*电影*页上，以便每个电影列表也包含**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="30928-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="30928-134">打开*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="30928-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="30928-135">在页面的正文中，更改`WebGrid`通过添加列的标记。</span><span class="sxs-lookup"><span data-stu-id="30928-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="30928-136">下面是修改后的标记：</span><span class="sxs-lookup"><span data-stu-id="30928-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="30928-137">新列是这样一个：</span><span class="sxs-lookup"><span data-stu-id="30928-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="30928-138">本专栏的重点是说明链接 (`<a>`元素) 的文本显示的是"编辑"。</span><span class="sxs-lookup"><span data-stu-id="30928-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="30928-139">我们所期望是创建页运行时，如以下所示的链接使用`id`每部电影的不同值：</span><span class="sxs-lookup"><span data-stu-id="30928-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="30928-140">此链接将调用一个名为页*EditMovie*，以及它将传递查询字符串`?id=7`到该页。</span><span class="sxs-lookup"><span data-stu-id="30928-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="30928-141">新列的语法可能看起来有点复杂，但这只是因为汇集多个元素。</span><span class="sxs-lookup"><span data-stu-id="30928-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="30928-142">每个元素非常简单。</span><span class="sxs-lookup"><span data-stu-id="30928-142">Each individual element is straightforward.</span></span> <span data-ttu-id="30928-143">如果您专注于只需`<a>`元素，请参阅此标记：</span><span class="sxs-lookup"><span data-stu-id="30928-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="30928-144">有关网格的工作方式的一些背景信息： 网格显示行，分别针对每个数据库记录，并显示数据库记录中的每个字段的列。</span><span class="sxs-lookup"><span data-stu-id="30928-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="30928-145">构造每个网格行时，虽然`item`对象包含该行的数据库记录 （项）。</span><span class="sxs-lookup"><span data-stu-id="30928-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="30928-146">此安排使代码来访问数据，为该行中一种方法。</span><span class="sxs-lookup"><span data-stu-id="30928-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="30928-147">这就是，请参阅此处： 表达式`item.ID`获取当前的数据库项的 ID 值。</span><span class="sxs-lookup"><span data-stu-id="30928-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="30928-148">您可以通过使用得到的任何数据库值 （标题、 genre 或年） 相同的方式`item.Title`， `item.Genre`，或`item.Year`。</span><span class="sxs-lookup"><span data-stu-id="30928-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="30928-149">表达式`"~/EditMovie?id=@item.ID`结合了硬编码一部分的目标 URL (`~/EditMovie?id=`) 与此动态派生的 id。</span><span class="sxs-lookup"><span data-stu-id="30928-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="30928-150">(您看到的那样`~`运算符在上一教程; 它是一个表示当前网站根目录的 ASP.NET 运算符。)</span><span class="sxs-lookup"><span data-stu-id="30928-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="30928-151">结果是标记的，这一部分的列中只是标记的生成类似于以下标记的内容在运行时：</span><span class="sxs-lookup"><span data-stu-id="30928-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="30928-152">当然，实际值的`id`将不同的每一行。</span><span class="sxs-lookup"><span data-stu-id="30928-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="30928-153">创建自定义显示的网格列</span><span class="sxs-lookup"><span data-stu-id="30928-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="30928-154">现在回网格列。</span><span class="sxs-lookup"><span data-stu-id="30928-154">Now back to the grid column.</span></span> <span data-ttu-id="30928-155">三个列最初必须显示网格的唯一数据值 （标题、 genre 和年份）。</span><span class="sxs-lookup"><span data-stu-id="30928-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="30928-156">通过将数据库列的名称传递指定此显示&mdash;例如， `grid.Column("Title")`。</span><span class="sxs-lookup"><span data-stu-id="30928-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="30928-157">这一新**编辑**链接列是不同。</span><span class="sxs-lookup"><span data-stu-id="30928-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="30928-158">指定列名称，而不传递`format`参数。</span><span class="sxs-lookup"><span data-stu-id="30928-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="30928-159">此参数允许你定义标记的`WebGrid`帮助器将呈现连同`item`列数据显示为粗体或绿色或在任何格式，您需要的值。</span><span class="sxs-lookup"><span data-stu-id="30928-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="30928-160">例如，如果您希望该标题以粗体显示，您可以创建如下例所示的列：</span><span class="sxs-lookup"><span data-stu-id="30928-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="30928-161">(的各种`@`中看到的字符`format`属性标记的标记和代码值之间的转换。)</span><span class="sxs-lookup"><span data-stu-id="30928-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="30928-162">一旦您知道的关于`format`属性，它是更轻松地了解如何新**编辑**链接列结合在一起：</span><span class="sxs-lookup"><span data-stu-id="30928-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="30928-163">列组成*仅*的呈现链接的标记，以及某些信息 (ID)，从提取的行的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="30928-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="30928-164">**命名的参数和一个方法的位置参数**</span><span class="sxs-lookup"><span data-stu-id="30928-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="30928-165">很多时候时调用的一个方法并传递给它的参数后，你只是已加入由逗号分隔的参数值。</span><span class="sxs-lookup"><span data-stu-id="30928-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="30928-166">以下为若干示例：</span><span class="sxs-lookup"><span data-stu-id="30928-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="30928-167">当第一次看到此代码中，但每种情况下，您要将参数传递给以特定顺序的方法时，我们没有提过问题&mdash;即，在该方法中定义参数的顺序。</span><span class="sxs-lookup"><span data-stu-id="30928-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="30928-168">有关`db.Execute`和`Validation.RequireFields`，如果您混您传递的值的顺序，则会得到一条错误消息页运行时或至少一些奇怪的结果。</span><span class="sxs-lookup"><span data-stu-id="30928-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="30928-169">很明显，您必须知道传递中的参数顺序。</span><span class="sxs-lookup"><span data-stu-id="30928-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="30928-170">（在 WebMatrix 中，IntelliSense 可帮助您了解出名称、 类型和参数的顺序图。）</span><span class="sxs-lookup"><span data-stu-id="30928-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="30928-171">作为按顺序将值传递的替代方法，你可以使用*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="30928-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="30928-172">(按顺序传递参数即为使用*位置参数*。)对于命名参数，则可以传递它的值时显式包括到参数的名称。</span><span class="sxs-lookup"><span data-stu-id="30928-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="30928-173">已命名的参数已多次在使用这些教程。</span><span class="sxs-lookup"><span data-stu-id="30928-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="30928-174">例如：</span><span class="sxs-lookup"><span data-stu-id="30928-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="30928-175">和</span><span class="sxs-lookup"><span data-stu-id="30928-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="30928-176">命名的参数可以方便地几个情况下的尤其是当某方法采用多个参数。</span><span class="sxs-lookup"><span data-stu-id="30928-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="30928-177">一个是当你想要传递只能将一个或两个参数，但你想要传递的值不是在参数列表中的第一个位置。</span><span class="sxs-lookup"><span data-stu-id="30928-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="30928-178">当你想要通过将参数传递给您最有利的顺序，使代码更具可读性时，另一种情况。</span><span class="sxs-lookup"><span data-stu-id="30928-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="30928-179">显然，若要使用命名的参数，您需要知道的参数的名称。</span><span class="sxs-lookup"><span data-stu-id="30928-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="30928-180">WebMatrix IntelliSense 可以*显示*您的名称，但它不能当前它们为你填充。</span><span class="sxs-lookup"><span data-stu-id="30928-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>


## <a name="creating-the-edit-page"></a><span data-ttu-id="30928-181">创建编辑页</span><span class="sxs-lookup"><span data-stu-id="30928-181">Creating the Edit Page</span></span>

<span data-ttu-id="30928-182">现在，你可以创建*EditMovie*页。</span><span class="sxs-lookup"><span data-stu-id="30928-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="30928-183">当用户单击**编辑**链接，它们就会在此页上。</span><span class="sxs-lookup"><span data-stu-id="30928-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="30928-184">创建一个名为页*EditMovie.cshtml*和替换为以下标记文件中：</span><span class="sxs-lookup"><span data-stu-id="30928-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="30928-185">这种标记和代码是类似于中有*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="30928-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="30928-186">没有提交按钮的文本略有不同。</span><span class="sxs-lookup"><span data-stu-id="30928-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="30928-187">如同*AddMovie*页上，没有`Html.ValidationSummary`如果有的话，将显示验证错误的调用。</span><span class="sxs-lookup"><span data-stu-id="30928-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="30928-188">这次我们要离开掉调用`Validation.Message`，因为在验证摘要中将显示错误。</span><span class="sxs-lookup"><span data-stu-id="30928-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="30928-189">上一教程中所述，您可以在各种组合中使用验证摘要和单独的错误消息。</span><span class="sxs-lookup"><span data-stu-id="30928-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="30928-190">再次请注意，`method`的属性`<form>`元素设置为`post`。</span><span class="sxs-lookup"><span data-stu-id="30928-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="30928-191">如同*AddMovie.cshtml*页上，此页进行更改到数据库。</span><span class="sxs-lookup"><span data-stu-id="30928-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="30928-192">因此，此窗体中应执行`POST`操作。</span><span class="sxs-lookup"><span data-stu-id="30928-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="30928-193">(有关详细信息之间的差异`GET`和`POST`操作，请参阅[GET、 POST 和 HTTP 谓词安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)HTML 窗体上本教程中的边栏。)</span><span class="sxs-lookup"><span data-stu-id="30928-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="30928-194">正如在前面的教程，你看到`value`Razor 代码与预加载其设置属性的文本框。</span><span class="sxs-lookup"><span data-stu-id="30928-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="30928-195">这一次，不过，你使用的变量，诸如`title`并`genre`而不是该任务`Request.Form["title"]`:</span><span class="sxs-lookup"><span data-stu-id="30928-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="30928-196">为之前，此标记将预加载的电影值的文本框值。</span><span class="sxs-lookup"><span data-stu-id="30928-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="30928-197">为什么很方便地使用变量这一次而不是使用的稍后将看到`Request`对象。</span><span class="sxs-lookup"><span data-stu-id="30928-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="30928-198">此外，还有`<input type="hidden">`此页上的元素。</span><span class="sxs-lookup"><span data-stu-id="30928-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="30928-199">此元素而不使其可见的页上存储的电影 ID。</span><span class="sxs-lookup"><span data-stu-id="30928-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="30928-200">ID 最初传递到页上，通过使用查询字符串值 (`?id=7`或类似的 URL 中)。</span><span class="sxs-lookup"><span data-stu-id="30928-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="30928-201">通过将 ID 值放入隐藏的字段，您可以确保便可提交窗体时，即使不再有权访问调用页时使用了原始 URL。</span><span class="sxs-lookup"><span data-stu-id="30928-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="30928-202">与不同*AddMovie*页上的代码*EditMovie*页有两个不同的功能。</span><span class="sxs-lookup"><span data-stu-id="30928-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="30928-203">第一个函数是，在第一次显示的页时 (并*仅*然后)，代码从查询字符串获取电影 ID。</span><span class="sxs-lookup"><span data-stu-id="30928-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="30928-204">然后，此代码使用 ID 来读取相应电影移出数据库，并显示 （预先加载） 它在文本框中。</span><span class="sxs-lookup"><span data-stu-id="30928-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="30928-205">第二个函数是，当用户单击**提交更改**按钮，代码都需要读取的值的文本框和对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="30928-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="30928-206">代码还必须使用新值更新数据库项。</span><span class="sxs-lookup"><span data-stu-id="30928-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="30928-207">此技术是类似于添加一条记录中所示*AddMovie*。</span><span class="sxs-lookup"><span data-stu-id="30928-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="30928-208">添加代码来读取单个电影</span><span class="sxs-lookup"><span data-stu-id="30928-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="30928-209">若要执行的第一个函数，将此代码添加到页的顶部：</span><span class="sxs-lookup"><span data-stu-id="30928-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="30928-210">此代码的大部分是在启动块内`if(!IsPost)`。</span><span class="sxs-lookup"><span data-stu-id="30928-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="30928-211">`!`运算符表示"not，"因此，该表达式表示*如果此请求不是 post 提交*，这是说的间接方法*此请求是否已运行此页的第一个时间*。</span><span class="sxs-lookup"><span data-stu-id="30928-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="30928-212">如前文所述，应运行此代码*仅*首次运行时页面。</span><span class="sxs-lookup"><span data-stu-id="30928-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="30928-213">如果未将中的代码`if(!IsPost)`，它会运行每次页面调用时，是否第一次或响应按钮单击。</span><span class="sxs-lookup"><span data-stu-id="30928-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="30928-214">请注意，该代码包含`else`阻止这一次。</span><span class="sxs-lookup"><span data-stu-id="30928-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="30928-215">正如我们所说时我们引入了`if`块，有时你想要运行替代代码，如果您要测试的条件不是这样。</span><span class="sxs-lookup"><span data-stu-id="30928-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="30928-216">这是此处的示例。</span><span class="sxs-lookup"><span data-stu-id="30928-216">That's the case here.</span></span> <span data-ttu-id="30928-217">如果满足条件 （即，如果传递到页的 ID 为确定），您可以从数据库读取行。</span><span class="sxs-lookup"><span data-stu-id="30928-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="30928-218">但是，如果条件未通过，`else`块运行和代码设置一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="30928-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="30928-219">验证传递到页的值</span><span class="sxs-lookup"><span data-stu-id="30928-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="30928-220">该代码使用`Request.QueryString["id"]`获取传递到页面的 ID。</span><span class="sxs-lookup"><span data-stu-id="30928-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="30928-221">代码可确保实际 id 传递的值</span><span class="sxs-lookup"><span data-stu-id="30928-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="30928-222">如果不传递的任何值，该代码设置验证错误。</span><span class="sxs-lookup"><span data-stu-id="30928-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="30928-223">此代码显示了不同的方式来验证信息。</span><span class="sxs-lookup"><span data-stu-id="30928-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="30928-224">在上一教程中，您使用过`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="30928-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="30928-225">注册字段，若要验证，并且 ASP.NET 自动未验证，并通过使用显示的错误`Html.ValidationMessage`和`Html.ValidationSummary`。</span><span class="sxs-lookup"><span data-stu-id="30928-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="30928-226">在这种情况下，但是，你在实际上不验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="30928-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="30928-227">相反，你在验证从其他位置传递到页一个值。</span><span class="sxs-lookup"><span data-stu-id="30928-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="30928-228">`Validation`帮助程序不会为您做的。</span><span class="sxs-lookup"><span data-stu-id="30928-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="30928-229">因此，您自行检查值，通过测试其与`if(!Request.QueryString["ID"].IsEmpty()`)。</span><span class="sxs-lookup"><span data-stu-id="30928-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="30928-230">如果没有问题，可以通过使用显示错误`Html.ValidationSummary`，就像处理一样`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="30928-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="30928-231">若要执行此操作，请调用`Validation.AddFormError`并将其传递要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="30928-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="30928-232">`Validation.AddFormError` 为使您可以定义自定义消息，同时结合使用您已经熟悉了验证系统的内置方法。</span><span class="sxs-lookup"><span data-stu-id="30928-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="30928-233">（稍后在本教程中我们将介绍有关如何进行此验证过程更加强大。）</span><span class="sxs-lookup"><span data-stu-id="30928-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="30928-234">确保没有将电影的 ID 之后, 代码读取数据库，查找仅为单个数据库项。</span><span class="sxs-lookup"><span data-stu-id="30928-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="30928-235">(您可能已经注意到常规模式，用于数据库操作： 打开数据库，定义 SQL 语句，然后运行该语句。)这一次，SQL`Select`语句中包含`WHERE ID = @0`。</span><span class="sxs-lookup"><span data-stu-id="30928-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="30928-236">ID 是唯一的因为只有一条记录可能会返回。</span><span class="sxs-lookup"><span data-stu-id="30928-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="30928-237">通过执行查询`db.QuerySingle`(不`db.Query`，如用于电影列表)，然后代码将放入结果`row`变量。</span><span class="sxs-lookup"><span data-stu-id="30928-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="30928-238">名称`row`是任意的; 您喜欢的任何命名变量。</span><span class="sxs-lookup"><span data-stu-id="30928-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="30928-239">在顶部进行初始化的变量将然后填入电影详细信息，以便可以在文本框中显示这些值。</span><span class="sxs-lookup"><span data-stu-id="30928-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="30928-240">测试编辑页 （到目前为止）</span><span class="sxs-lookup"><span data-stu-id="30928-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="30928-241">如果你想要测试您的页面，运行*电影*现在页，然后单击**编辑**任何电影旁边的链接。</span><span class="sxs-lookup"><span data-stu-id="30928-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="30928-242">你将看到*EditMovie*为所选的电影的详细信息页填充：</span><span class="sxs-lookup"><span data-stu-id="30928-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![编辑电影页面，其中显示要编辑的电影](updating-data/_static/image3.png)

<span data-ttu-id="30928-244">请注意，页面的 URL 包含类似于`?id=10`（或其他一些号码）。</span><span class="sxs-lookup"><span data-stu-id="30928-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="30928-245">到目前为止您已测试**编辑**中的链接*电影*页上工作，您的页面从查询字符串读取 ID 和查询数据库以获取单个电影记录是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="30928-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="30928-246">可以更改电影信息，但当您单击时没有任何反应**提交更改**。</span><span class="sxs-lookup"><span data-stu-id="30928-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="30928-247">添加代码以使用用户的更改更新电影</span><span class="sxs-lookup"><span data-stu-id="30928-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="30928-248">在中*EditMovie.cshtml*文件中，若要实现第二个函数 （保存更改），添加以下代码置于右大括号的`@`块。</span><span class="sxs-lookup"><span data-stu-id="30928-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="30928-249">(如果不确定如何将代码放在则可以查看[完整代码列表的编辑电影页面](#Complete_Page_Listing_for_EditMovie)，在本教程的最后阶段显示。)</span><span class="sxs-lookup"><span data-stu-id="30928-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="30928-250">同样，此标记和代码是类似于中的代码*AddMovie*。</span><span class="sxs-lookup"><span data-stu-id="30928-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="30928-251">代码位于`if(IsPost)`阻止，因为仅当用户单击时，在运行此代码**提交更改**按钮&mdash;，即当 （和仅当） 发送窗体。</span><span class="sxs-lookup"><span data-stu-id="30928-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="30928-252">在这种情况下，不使用像测试`if(IsPost && Validation.IsValid())`— 也就是说，在不合并这两个测试通过使用 and。</span><span class="sxs-lookup"><span data-stu-id="30928-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="30928-253">在此页上，您首先确定是否提交窗体 (`if(IsPost)`)，然后仅注册用于验证的字段。</span><span class="sxs-lookup"><span data-stu-id="30928-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="30928-254">然后可以测试验证结果 (`if(Validation.IsValid()`)。</span><span class="sxs-lookup"><span data-stu-id="30928-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="30928-255">流的方向是中略有不同*AddMovie.cshtml*页上，但效果是相同。</span><span class="sxs-lookup"><span data-stu-id="30928-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="30928-256">使用获取的值的文本框`Request.Form["title"]`和其他类似的代码`<input>`元素。</span><span class="sxs-lookup"><span data-stu-id="30928-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="30928-257">请注意，这一次，此代码可获取电影 ID 移出隐藏字段 (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="30928-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="30928-258">当页面运行了第一次时，代码必须从查询字符串的 ID。</span><span class="sxs-lookup"><span data-stu-id="30928-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="30928-259">从隐藏的字段，以确保在从那时起，查询字符串以某种方式更改的情况下您将获得的最初所显示的电影 ID 获取的值。</span><span class="sxs-lookup"><span data-stu-id="30928-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="30928-260">真正重要区别*AddMovie*代码和此代码是在此代码中使用 SQL`Update`语句而不是`Insert Into`语句。</span><span class="sxs-lookup"><span data-stu-id="30928-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="30928-261">下面的示例显示了 SQL 的语法`Update`语句：</span><span class="sxs-lookup"><span data-stu-id="30928-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="30928-262">可以按任意顺序指定的任何列，则不一定必须更新期间的每个列`Update`操作。</span><span class="sxs-lookup"><span data-stu-id="30928-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="30928-263">(不能更新与 ID 本身，因为这实际上将保存该记录为一个新的记录，并为不允许的`Update`操作。)</span><span class="sxs-lookup"><span data-stu-id="30928-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="30928-264">**重要**`Where`子句具有 ID 是非常重要，因为这是数据库如何知道哪个数据库记录你想要更新。</span><span class="sxs-lookup"><span data-stu-id="30928-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="30928-265">如果您离开`Where`子句中，数据库将更新*每个*记录在数据库中。</span><span class="sxs-lookup"><span data-stu-id="30928-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="30928-266">在大多数情况下，会是一场灾难。</span><span class="sxs-lookup"><span data-stu-id="30928-266">In most cases, that would be a disaster.</span></span>


<span data-ttu-id="30928-267">在代码中，要更新的值传递到 SQL 语句使用占位符。</span><span class="sxs-lookup"><span data-stu-id="30928-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="30928-268">若要重复我们曾经说过： 出于安全原因*仅*占位符用于将值传递给 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="30928-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="30928-269">该代码使用后`db.Execute`运行`Update`语句，它将重定向回列表页，其中可以看到所做的更改。</span><span class="sxs-lookup"><span data-stu-id="30928-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="30928-270">**不同的 SQL 语句，不同的方法**</span><span class="sxs-lookup"><span data-stu-id="30928-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="30928-271">您可能已经注意到使用略有不同的方法来运行不同的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="30928-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="30928-272">若要运行`Select`查询，它可能返回多个记录，则使用`Query`方法。</span><span class="sxs-lookup"><span data-stu-id="30928-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="30928-273">若要运行`Select`您知道的查询将返回一个数据库项，则使用`QuerySingle`方法。</span><span class="sxs-lookup"><span data-stu-id="30928-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="30928-274">若要运行的命令进行更改，但不返回数据库项，请使用`Execute`方法。</span><span class="sxs-lookup"><span data-stu-id="30928-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="30928-275">您必须具有不同的方法，因为每个返回不同的结果，正如您已看到之间的差异`Query`和`QuerySingle`。</span><span class="sxs-lookup"><span data-stu-id="30928-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="30928-276">(`Execute`方法实际上返回一个值还&mdash;即的数据库行受影响的命令数&mdash;但您忽略了，到目前为止。)</span><span class="sxs-lookup"><span data-stu-id="30928-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="30928-277">当然，`Query`方法可能返回只有一个数据库行。</span><span class="sxs-lookup"><span data-stu-id="30928-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="30928-278">但是，ASP.NET 始终处理的结果`Query`作为集合的方法。</span><span class="sxs-lookup"><span data-stu-id="30928-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="30928-279">即使该方法返回一个行，您必须从集合中提取这一行。</span><span class="sxs-lookup"><span data-stu-id="30928-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="30928-280">因此，在情况下，你*知道*您就会得到只包含一行，它就会更方便地使用`QuerySingle`。</span><span class="sxs-lookup"><span data-stu-id="30928-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="30928-281">有几个其他执行特定类型的数据库操作的方法。</span><span class="sxs-lookup"><span data-stu-id="30928-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="30928-282">您可以查找数据库中的方法的列表[ASP.NET Web Pages API 快速参考](../../api-reference/asp-net-web-pages-api-reference.md#Data)。</span><span class="sxs-lookup"><span data-stu-id="30928-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>


## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="30928-283">使稳健，验证 ID 详细信息</span><span class="sxs-lookup"><span data-stu-id="30928-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="30928-284">第一次运行页面时，你获取电影 ID 从查询字符串，以便您可以从数据库中获取该电影。</span><span class="sxs-lookup"><span data-stu-id="30928-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="30928-285">您已确保实际时出现的值去寻找机会，未使用此代码：</span><span class="sxs-lookup"><span data-stu-id="30928-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="30928-286">此代码用于可以确保，如果用户到达*EditMovies*页，但没有首先选择电影*电影*页上，页面将显示一条用户友好错误消息。</span><span class="sxs-lookup"><span data-stu-id="30928-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="30928-287">（否则，用户会看到一个错误，将可能只需将它们混淆。）</span><span class="sxs-lookup"><span data-stu-id="30928-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="30928-288">但是，此验证不太可靠。</span><span class="sxs-lookup"><span data-stu-id="30928-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="30928-289">页面也可能使用这些错误的调用：</span><span class="sxs-lookup"><span data-stu-id="30928-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="30928-290">ID 不是一个数字。</span><span class="sxs-lookup"><span data-stu-id="30928-290">The ID isn't a number.</span></span> <span data-ttu-id="30928-291">例如，页面可能调用使用的 URL，例如`http://localhost:nnnnn/EditMovie?id=abc`。</span><span class="sxs-lookup"><span data-stu-id="30928-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="30928-292">ID 是一个数字，但它引用了不存在的电影 (例如， `http://localhost:nnnnn/EditMovie?id=100934`)。</span><span class="sxs-lookup"><span data-stu-id="30928-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="30928-293">如果您想要查看从这些 Url，运行产生的错误*电影*页。</span><span class="sxs-lookup"><span data-stu-id="30928-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="30928-294">选择要编辑的电影，然后更改的 URL *EditMovie* ID 或不存在电影 ID 到包含字母的 URL 页上。</span><span class="sxs-lookup"><span data-stu-id="30928-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="30928-295">因此，您该怎么办？</span><span class="sxs-lookup"><span data-stu-id="30928-295">So what should you do?</span></span> <span data-ttu-id="30928-296">第一个解决方法是确保该不只一个 ID 传递到页上，但 ID 是一个整数。</span><span class="sxs-lookup"><span data-stu-id="30928-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="30928-297">更改的代码`!IsPost`测试看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="30928-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="30928-298">已添加到第二个条件`IsEmpty`测试与链接`&&`（逻辑与）：</span><span class="sxs-lookup"><span data-stu-id="30928-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="30928-299">可能会从记得[ASP.NET Web Pages 编程介绍](../introducing-razor-syntax-c.md)等方法的教程`AsBool``AsInt`将字符字符串转换为其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="30928-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="30928-300">`IsInt`方法 (和其他人，喜欢`IsBool`和`IsDateTime`) 类似。</span><span class="sxs-lookup"><span data-stu-id="30928-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="30928-301">但是，它们仅用于测试是否您*可以*转换的字符串，而不实际执行转换。</span><span class="sxs-lookup"><span data-stu-id="30928-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="30928-302">因此，在这里基本上就*如果查询字符串值可以转换为整数...*.</span><span class="sxs-lookup"><span data-stu-id="30928-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="30928-303">其他潜在问题正在寻求不存在的电影。</span><span class="sxs-lookup"><span data-stu-id="30928-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="30928-304">若要获取电影的代码如下所示代码所示：</span><span class="sxs-lookup"><span data-stu-id="30928-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="30928-305">如果传递`movieId`值设为`QuerySingle`不对应于任何实际电影的方法，未返回任何内容且后面的语句 (例如， `title=row.Title`) 导致的错误。</span><span class="sxs-lookup"><span data-stu-id="30928-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="30928-306">同样是容易解决此问题。</span><span class="sxs-lookup"><span data-stu-id="30928-306">Again there's an easy fix.</span></span> <span data-ttu-id="30928-307">如果`db.QuerySingle`方法会返回任何结果，`row`变量将为 null。</span><span class="sxs-lookup"><span data-stu-id="30928-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="30928-308">这样您就可以检查是否`row`变量为 null，然后再尝试从其获取值。</span><span class="sxs-lookup"><span data-stu-id="30928-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="30928-309">下面的代码添加`if`获取的值的语句周围的块`row`对象：</span><span class="sxs-lookup"><span data-stu-id="30928-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="30928-310">使用这两个其他验证测试，页面变得更高防护。</span><span class="sxs-lookup"><span data-stu-id="30928-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="30928-311">完整代码`!IsPost`分支现在看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="30928-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="30928-312">我们注意一次此任务是有关充分利用`else`块。</span><span class="sxs-lookup"><span data-stu-id="30928-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="30928-313">如果测试未通过，`else`块设置错误消息。</span><span class="sxs-lookup"><span data-stu-id="30928-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="30928-314">添加用于返回到电影页面的链接</span><span class="sxs-lookup"><span data-stu-id="30928-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="30928-315">最后一个也是很有帮助的详细信息将添加一个链接回*电影*页。</span><span class="sxs-lookup"><span data-stu-id="30928-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="30928-316">在普通的事件流中，用户将开始处*电影*页上，单击**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="30928-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="30928-317">将用户带到*EditMovie*页上，它们可以在其中编辑电影并单击按钮。</span><span class="sxs-lookup"><span data-stu-id="30928-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="30928-318">代码已处理更改后，它将重定向回到*电影*页。</span><span class="sxs-lookup"><span data-stu-id="30928-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="30928-319">但是：</span><span class="sxs-lookup"><span data-stu-id="30928-319">However:</span></span>

- <span data-ttu-id="30928-320">用户可能会决定不需进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="30928-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="30928-321">用户可能没有先单击此页收到**编辑**中的链接*电影*页。</span><span class="sxs-lookup"><span data-stu-id="30928-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="30928-322">无论哪种方式，你想要使其能够方便地返回到主列表。</span><span class="sxs-lookup"><span data-stu-id="30928-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="30928-323">很容易解决此问题&mdash;恰好在关闭后添加以下标记`</form>`标记的标记中：</span><span class="sxs-lookup"><span data-stu-id="30928-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="30928-324">此标记使用的相同语法`<a>`您所见到其他位置的元素。</span><span class="sxs-lookup"><span data-stu-id="30928-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="30928-325">URL 中包括`~`来表示"root 的网站。</span><span class="sxs-lookup"><span data-stu-id="30928-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="30928-326">测试电影更新过程</span><span class="sxs-lookup"><span data-stu-id="30928-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="30928-327">现在，可以测试。</span><span class="sxs-lookup"><span data-stu-id="30928-327">Now you can test.</span></span> <span data-ttu-id="30928-328">运行*电影*页，然后单击**编辑**旁边电影。</span><span class="sxs-lookup"><span data-stu-id="30928-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="30928-329">当*EditMovie*页出现后，更改到电影，然后单击**提交更改**。</span><span class="sxs-lookup"><span data-stu-id="30928-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="30928-330">电影列表出现时，请确保显示所做的更改。</span><span class="sxs-lookup"><span data-stu-id="30928-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="30928-331">若要确保验证正常工作，请单击**编辑**为另一个的电影。</span><span class="sxs-lookup"><span data-stu-id="30928-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="30928-332">转到*EditMovie*页上，清除**流派**字段 (或**年**字段，或两者) 并尝试提交所做的更改。</span><span class="sxs-lookup"><span data-stu-id="30928-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="30928-333">如您所料，将看到一个错误：</span><span class="sxs-lookup"><span data-stu-id="30928-333">You'll see an error, as you'd expect:</span></span>

![编辑电影页面，其中显示验证错误](updating-data/_static/image4.png)

<span data-ttu-id="30928-335">单击**返回到的电影列表**链接以放弃所做的更改并返回到*电影*页。</span><span class="sxs-lookup"><span data-stu-id="30928-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="30928-336">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="30928-336">Coming Up Next</span></span>

<span data-ttu-id="30928-337">在下一步的教程中，您将了解如何删除电影记录。</span><span class="sxs-lookup"><span data-stu-id="30928-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="30928-338">电影页面 （使用编辑链接更新） 的完整列表</span><span class="sxs-lookup"><span data-stu-id="30928-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="30928-339">完成编辑电影页的页列表</span><span class="sxs-lookup"><span data-stu-id="30928-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="30928-340">其他资源</span><span class="sxs-lookup"><span data-stu-id="30928-340">Additional Resources</span></span>

- [<span data-ttu-id="30928-341">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="30928-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="30928-342">[SQL UPDATE 语句](http://www.w3schools.com/sql/sql_update.asp)W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="30928-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="30928-343">[上一页](entering-data.md)
> [下一页](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="30928-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
