---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: 引入的 ASP.NET Web Pages-更新数据库数据 |Microsoft 文档
author: tfitzmac
description: 本教程演示如何使用 ASP.NET Web 页 (Razor) 时 （更改） 的现有数据库条目更新。 它假定你已完成序列 th...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: e889cd27e2267a08f7b6ea708c92e35edbdd7a1a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="28a4d-104">引入了 ASP.NET Web 页-更新数据库数据</span><span class="sxs-lookup"><span data-stu-id="28a4d-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>
====================
<span data-ttu-id="28a4d-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="28a4d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="28a4d-106">本教程演示如何使用 ASP.NET Web 页 (Razor) 时 （更改） 的现有数据库条目更新。</span><span class="sxs-lookup"><span data-stu-id="28a4d-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="28a4d-107">它假定你已完成通过系列[输入数据通过使用窗体使用的 ASP.NET Web Pages](entering-data.md)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="28a4d-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="28a4d-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="28a4d-109">如何选择中的单个记录`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="28a4d-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="28a4d-110">如何从数据库中读取单个记录。</span><span class="sxs-lookup"><span data-stu-id="28a4d-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="28a4d-111">如何预加载的窗体具有来自数据库记录的值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="28a4d-112">如何更新数据库中的现有记录。</span><span class="sxs-lookup"><span data-stu-id="28a4d-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="28a4d-113">如何在页中存储的信息，而不显示它。</span><span class="sxs-lookup"><span data-stu-id="28a4d-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="28a4d-114">如何使用隐藏的字段来存储信息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="28a4d-115">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="28a4d-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="28a4d-116">`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="28a4d-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="28a4d-117">SQL`Update`命令。</span><span class="sxs-lookup"><span data-stu-id="28a4d-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="28a4d-118">`Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="28a4d-119">隐藏字段 (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-119">Hidden fields (`<input type="hidden">`).</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="28a4d-120">你将生成</span><span class="sxs-lookup"><span data-stu-id="28a4d-120">What You'll Build</span></span>

<span data-ttu-id="28a4d-121">在前面的教程，您学习了如何将记录添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="28a4d-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="28a4d-122">在这里，您将学习如何显示一条记录以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="28a4d-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="28a4d-123">在*电影*页上，你将更新`WebGrid`帮助器以便它显示**编辑**每个影片旁边的链接：</span><span class="sxs-lookup"><span data-stu-id="28a4d-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![WebGrid 显示包括每个影片的编辑链接](updating-data/_static/image1.png)

<span data-ttu-id="28a4d-125">当你单击**编辑**链接，它将你带到不同的页的影片信息已在窗体：</span><span class="sxs-lookup"><span data-stu-id="28a4d-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![编辑显示要编辑的电影的电影页](updating-data/_static/image2.png)

<span data-ttu-id="28a4d-127">你可以更改的任何值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-127">You can change any of the values.</span></span> <span data-ttu-id="28a4d-128">当提交所做的更改时，在页中的代码将更新数据库，并将影片列表返回。</span><span class="sxs-lookup"><span data-stu-id="28a4d-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="28a4d-129">此过程的一部分工作原理几乎完全与*AddMovie.cshtml*你创建在以前的教程中，因此，很多本教程将会熟悉页面。</span><span class="sxs-lookup"><span data-stu-id="28a4d-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="28a4d-130">有几种方法无法实现一种方法编辑单个影片。</span><span class="sxs-lookup"><span data-stu-id="28a4d-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="28a4d-131">因为它易于实施且易于理解，已选择显示的方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="28a4d-132">添加到影片列表的编辑链接</span><span class="sxs-lookup"><span data-stu-id="28a4d-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="28a4d-133">若要开始，你将更新*电影*页，以便还列出每个影片包含**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="28a4d-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="28a4d-134">打开*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="28a4d-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="28a4d-135">在页的正文中，更改`WebGrid`通过添加的列的标记。</span><span class="sxs-lookup"><span data-stu-id="28a4d-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="28a4d-136">下面是已修改的标记：</span><span class="sxs-lookup"><span data-stu-id="28a4d-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="28a4d-137">新的列是这样一个：</span><span class="sxs-lookup"><span data-stu-id="28a4d-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="28a4d-138">此列的点是显示的链接 (`<a>`元素) 的文本显示"编辑"。</span><span class="sxs-lookup"><span data-stu-id="28a4d-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="28a4d-139">我们后已是创建一个链接，以页运行时，如下所示使用`id`为每个电影不同的值：</span><span class="sxs-lookup"><span data-stu-id="28a4d-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="28a4d-140">此链接将调用一个名为页*EditMovie*，它将通过查询字符串和`?id=7`到该页面。</span><span class="sxs-lookup"><span data-stu-id="28a4d-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="28a4d-141">新列的语法可能看起来有点复杂，但这只是因为它汇集了几个元素。</span><span class="sxs-lookup"><span data-stu-id="28a4d-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="28a4d-142">每个单独元素非常简单。</span><span class="sxs-lookup"><span data-stu-id="28a4d-142">Each individual element is straightforward.</span></span> <span data-ttu-id="28a4d-143">如果你专注于仅`<a>`元素，请参阅此标记：</span><span class="sxs-lookup"><span data-stu-id="28a4d-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="28a4d-144">有关网格的工作方式一些背景信息： 在网格中显示行，分别针对每个数据库记录，而且它会显示数据库记录中的每个字段的列。</span><span class="sxs-lookup"><span data-stu-id="28a4d-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="28a4d-145">构造的每个网格行，而`item`对象包含该行的数据库记录 （项）。</span><span class="sxs-lookup"><span data-stu-id="28a4d-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="28a4d-146">这种安排为你提供一种方法中代码，使该行的数据。</span><span class="sxs-lookup"><span data-stu-id="28a4d-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="28a4d-147">你在此处看到的那样： 表达式`item.ID`获取当前数据库项的 ID 值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="28a4d-148">你无法通过使用获取任何数据库的值 （标题、 genre 或年） 相同的方式`item.Title`， `item.Genre`，或`item.Year`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="28a4d-149">表达式`"~/EditMovie?id=@item.ID`将合并目标 URL 的硬编码部分 (`~/EditMovie?id=`) 替换为此动态派生的 id。</span><span class="sxs-lookup"><span data-stu-id="28a4d-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="28a4d-150">(你已了解`~`运算符在以前的教程中; 它是一个表示当前的网站根目录的 ASP.NET 运算符。)</span><span class="sxs-lookup"><span data-stu-id="28a4d-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="28a4d-151">结果是标记的，这一部分的列中只需生成类似以下的标记在运行时：</span><span class="sxs-lookup"><span data-stu-id="28a4d-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="28a4d-152">当然，实际值的`id`每一行都有所不同。</span><span class="sxs-lookup"><span data-stu-id="28a4d-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="28a4d-153">创建自定义显示为网格列</span><span class="sxs-lookup"><span data-stu-id="28a4d-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="28a4d-154">现在回网格列。</span><span class="sxs-lookup"><span data-stu-id="28a4d-154">Now back to the grid column.</span></span> <span data-ttu-id="28a4d-155">三列最初已将在显示的网格数据值只有 （标题、 genre 和年）。</span><span class="sxs-lookup"><span data-stu-id="28a4d-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="28a4d-156">通过将数据库列的名称传递指定此显示&mdash;例如`grid.Column("Title")`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="28a4d-157">此新**编辑**链接列是不同。</span><span class="sxs-lookup"><span data-stu-id="28a4d-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="28a4d-158">您传递指定列名称，而不`format`参数。</span><span class="sxs-lookup"><span data-stu-id="28a4d-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="28a4d-159">此参数，您可以定义标记，`WebGrid`帮助器将呈现连同`item`要显示为粗体或绿色的列数据或的任何格式所需值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="28a4d-160">例如，如果你想要显示加粗的标题，你可以创建如下例所示的列：</span><span class="sxs-lookup"><span data-stu-id="28a4d-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="28a4d-161">(各种`@`中看到的字符`format`属性标记的标记和代码值之间的转换。)</span><span class="sxs-lookup"><span data-stu-id="28a4d-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="28a4d-162">一旦你了解了有关`format`属性，它是更易于理解如何新**编辑**链接列结合在一起：</span><span class="sxs-lookup"><span data-stu-id="28a4d-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="28a4d-163">列包含*仅*的呈现链接的标记，加上一些信息 (ID)，从提取数据库记录的行。</span><span class="sxs-lookup"><span data-stu-id="28a4d-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="28a4d-164">**命名的参数和方法的位置参数**</span><span class="sxs-lookup"><span data-stu-id="28a4d-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="28a4d-165">多次时调用方法并传递给它的参数后，你只需已列出并用逗号隔开的参数值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="28a4d-166">以下为若干示例：</span><span class="sxs-lookup"><span data-stu-id="28a4d-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="28a4d-167">当你第一次看到此代码中，但在每个情况下，你要将参数传递给以特定顺序的方法时，我们没有提到问题&mdash;也就是说，在该参数在该方法中定义的顺序。</span><span class="sxs-lookup"><span data-stu-id="28a4d-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="28a4d-168">有关`db.Execute`和`Validation.RequireFields`，如果你混合传递的值的顺序，你将收到一条错误消息页运行时或至少一些奇怪的结果。</span><span class="sxs-lookup"><span data-stu-id="28a4d-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="28a4d-169">显然，你必须知道传递中的参数顺序。</span><span class="sxs-lookup"><span data-stu-id="28a4d-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="28a4d-170">（在 WebMatrix 中，IntelliSense 可帮助你了解算出名称、 类型和参数的顺序。）</span><span class="sxs-lookup"><span data-stu-id="28a4d-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="28a4d-171">作为按顺序传递值的替代方法，你可以使用*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="28a4d-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="28a4d-172">(按顺序传递参数被称为使用*位置参数*。)对于命名参数，你可以将其值传递时显式包括到参数的名称。</span><span class="sxs-lookup"><span data-stu-id="28a4d-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="28a4d-173">你使用命名的参数已多次这些教程中。</span><span class="sxs-lookup"><span data-stu-id="28a4d-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="28a4d-174">例如：</span><span class="sxs-lookup"><span data-stu-id="28a4d-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="28a4d-175">和</span><span class="sxs-lookup"><span data-stu-id="28a4d-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="28a4d-176">命名的参数是功能几个情况下，可以提供便利，尤其是在某方法采用多个参数。</span><span class="sxs-lookup"><span data-stu-id="28a4d-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="28a4d-177">其中一个是当你想要传递只能将一个或两个参数，但你想要传递的值不在参数列表中的第一个位置之间。</span><span class="sxs-lookup"><span data-stu-id="28a4d-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="28a4d-178">另一种情况是当你想要通过将参数传递给你最有利的顺序，使你的代码更具可读性。</span><span class="sxs-lookup"><span data-stu-id="28a4d-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="28a4d-179">显然，若要使用命名的参数，你必须知道这些参数的名称。</span><span class="sxs-lookup"><span data-stu-id="28a4d-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="28a4d-180">WebMatrix IntelliSense 可以*显示*你名称，但它不能当前填充它们为你。</span><span class="sxs-lookup"><span data-stu-id="28a4d-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>


## <a name="creating-the-edit-page"></a><span data-ttu-id="28a4d-181">创建编辑页</span><span class="sxs-lookup"><span data-stu-id="28a4d-181">Creating the Edit Page</span></span>

<span data-ttu-id="28a4d-182">现在，你可以创建*EditMovie*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="28a4d-183">当用户单击**编辑**链接，它们将显示此页上。</span><span class="sxs-lookup"><span data-stu-id="28a4d-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="28a4d-184">创建一个名为页*EditMovie.cshtml* ，并将替换为以下标记文件中：</span><span class="sxs-lookup"><span data-stu-id="28a4d-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="28a4d-185">此标记和代码是类似于中有*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="28a4d-186">没有略有不同的提交按钮的文本。</span><span class="sxs-lookup"><span data-stu-id="28a4d-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="28a4d-187">与*AddMovie*页上，没有`Html.ValidationSummary`将显示验证错误，如果有任何的调用。</span><span class="sxs-lookup"><span data-stu-id="28a4d-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="28a4d-188">此时我们要离开掉调用`Validation.Message`，因为错误将显示在摘要的验证。</span><span class="sxs-lookup"><span data-stu-id="28a4d-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="28a4d-189">如前面的教程中所述，你可以在各种组合中使用验证摘要和单独的错误消息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="28a4d-190">再次请注意，`method`属性`<form>`元素设置为`post`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="28a4d-191">与*AddMovie.cshtml*页上，此页进行更改到数据库。</span><span class="sxs-lookup"><span data-stu-id="28a4d-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="28a4d-192">因此，应执行此窗体`POST`操作。</span><span class="sxs-lookup"><span data-stu-id="28a4d-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="28a4d-193">(有关详细信息之间的差异`GET`和`POST`操作，请参阅[GET、 POST 和 HTTP 谓词安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)边栏在教程中 HTML 窗体上。)</span><span class="sxs-lookup"><span data-stu-id="28a4d-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="28a4d-194">正如你在前面的教程中，看到`value`的文本框中的属性正在设置 Razor 代码使用了预加载它们。</span><span class="sxs-lookup"><span data-stu-id="28a4d-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="28a4d-195">这一次，不过，你使用的变量，如`title`和`genre`而不是该任务的`Request.Form["title"]`:</span><span class="sxs-lookup"><span data-stu-id="28a4d-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="28a4d-196">为之前，此标记将预加载的影片值文本框值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="28a4d-197">你将看到在稍后为方便起见，可以使用变量而不使用这一次`Request`对象。</span><span class="sxs-lookup"><span data-stu-id="28a4d-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="28a4d-198">此外，还有`<input type="hidden">`此页上的元素。</span><span class="sxs-lookup"><span data-stu-id="28a4d-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="28a4d-199">此元素而不使其可见的页上存储的电影 ID。</span><span class="sxs-lookup"><span data-stu-id="28a4d-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="28a4d-200">ID 最初传递到页上通过使用查询字符串值 (`?id=7`或类似的 URL 中)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="28a4d-201">通过将 ID 值放入隐藏的字段，你可以确保便可提交表单时，即使你不再有权页使用调用的原始 URL。</span><span class="sxs-lookup"><span data-stu-id="28a4d-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="28a4d-202">与不同*AddMovie*页上的代码*EditMovie*页有两个不同的功能。</span><span class="sxs-lookup"><span data-stu-id="28a4d-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="28a4d-203">第一个函数是，如果首次显示的页面 (和*仅*然后)，此代码可查询字符串中获取的电影 ID。</span><span class="sxs-lookup"><span data-stu-id="28a4d-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="28a4d-204">然后，此代码使用 ID 来读取出数据库对应的电影和显示 （预加载） 它在文本框中。</span><span class="sxs-lookup"><span data-stu-id="28a4d-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="28a4d-205">第二个函数是，当用户单击**提交更改**按钮，代码必须读取的值的文本框中，并对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="28a4d-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="28a4d-206">也必须对代码以使用新值更新的数据库项目。</span><span class="sxs-lookup"><span data-stu-id="28a4d-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="28a4d-207">这种技术很类似于添加记录，正如你在看到*AddMovie*。</span><span class="sxs-lookup"><span data-stu-id="28a4d-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="28a4d-208">添加代码以读取单个电影</span><span class="sxs-lookup"><span data-stu-id="28a4d-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="28a4d-209">若要执行的第一个函数，请将此代码添加到页的顶部：</span><span class="sxs-lookup"><span data-stu-id="28a4d-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="28a4d-210">此代码的大多数是在启动一个块内`if(!IsPost)`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="28a4d-211">`!`运算符意味着"不，"因此表达式意味着*如果此请求不是 post 提交*，即，显示的间接方法*此请求如果是首次运行此页的*。</span><span class="sxs-lookup"><span data-stu-id="28a4d-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="28a4d-212">如前文所述，应运行此代码*仅*首次运行页面。</span><span class="sxs-lookup"><span data-stu-id="28a4d-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="28a4d-213">如果你未将包含中的代码`if(!IsPost)`，它将运行每次页调用时，是否第一次，或者在响应至一个按钮单击。</span><span class="sxs-lookup"><span data-stu-id="28a4d-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="28a4d-214">请注意，代码包含`else`阻止这一次。</span><span class="sxs-lookup"><span data-stu-id="28a4d-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="28a4d-215">正如我们所说当我们引入了`if`块，有时你想要运行替代代码，如果您要测试的条件不是如此。</span><span class="sxs-lookup"><span data-stu-id="28a4d-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="28a4d-216">这是这种情况。</span><span class="sxs-lookup"><span data-stu-id="28a4d-216">That's the case here.</span></span> <span data-ttu-id="28a4d-217">如果该条件通过 （即，如果传递到页面的 ID 为确定），你可以从数据库读取行。</span><span class="sxs-lookup"><span data-stu-id="28a4d-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="28a4d-218">但是，如果不满足条件，`else`运行块和代码设置一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="28a4d-219">验证传递到页面的值</span><span class="sxs-lookup"><span data-stu-id="28a4d-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="28a4d-220">该代码使用`Request.QueryString["id"]`获取传递给页面的 ID。</span><span class="sxs-lookup"><span data-stu-id="28a4d-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="28a4d-221">代码可确保实际 id 传入的值</span><span class="sxs-lookup"><span data-stu-id="28a4d-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="28a4d-222">如果不传递任何值，该代码将设置验证错误。</span><span class="sxs-lookup"><span data-stu-id="28a4d-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="28a4d-223">此代码演示不同的方式，以验证信息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="28a4d-224">在前面的教程，你使用过`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="28a4d-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="28a4d-225">你注册字段，若要验证，并 ASP.NET 自动未验证，并通过使用显示错误`Html.ValidationMessage`和`Html.ValidationSummary`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="28a4d-226">在这种情况下，但是，你要实际上不验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="28a4d-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="28a4d-227">相反，你要验证一个值，从其他位置传递到页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="28a4d-228">`Validation`帮助器不会将出此为您。</span><span class="sxs-lookup"><span data-stu-id="28a4d-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="28a4d-229">因此，你自行检查值，通过测试它与`if(!Request.QueryString["ID"].IsEmpty()`)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="28a4d-230">如果没有问题，你可以通过使用显示错误`Html.ValidationSummary`，就像处理`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="28a4d-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="28a4d-231">若要做到这一点，你调用`Validation.AddFormError`并将其传递要显示的消息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="28a4d-232">`Validation.AddFormError` 是，您可以定义自定义消息，同时结合使用你已经熟悉了验证系统的内置方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="28a4d-233">（本教程中稍后我们将讨论如何使此验证过程变得更加可靠。）</span><span class="sxs-lookup"><span data-stu-id="28a4d-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="28a4d-234">确保电影的 ID 后, 的代码读取数据库，为单个数据库项查找。</span><span class="sxs-lookup"><span data-stu-id="28a4d-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="28a4d-235">(你可能已经注意到数据库操作的常规模式： 打开数据库，定义 SQL 语句，然后运行该语句。)这一次，SQL`Select`语句包括`WHERE ID = @0`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="28a4d-236">因为该 ID 是唯一的则可以返回只有一条记录。</span><span class="sxs-lookup"><span data-stu-id="28a4d-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="28a4d-237">查询执行使用`db.QuerySingle`(不`db.Query`，如用于影片列表)，并代码将放入结果`row`变量。</span><span class="sxs-lookup"><span data-stu-id="28a4d-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="28a4d-238">名称`row`是任意; 您喜欢的任何名称变量。</span><span class="sxs-lookup"><span data-stu-id="28a4d-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="28a4d-239">在顶部初始化的变量然后填入电影详细信息，以便可以在文本框中显示这些值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="28a4d-240">测试的编辑页 （为止）</span><span class="sxs-lookup"><span data-stu-id="28a4d-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="28a4d-241">如果你想要测试你的页面，运行*电影*现在页上，单击**编辑**任何电影旁边的链接。</span><span class="sxs-lookup"><span data-stu-id="28a4d-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="28a4d-242">你将看到*EditMovie*具有详细信息页填充为所选的电影：</span><span class="sxs-lookup"><span data-stu-id="28a4d-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![编辑显示要编辑的电影的电影页](updating-data/_static/image3.png)

<span data-ttu-id="28a4d-244">请注意，页面的 URL 将包含类似`?id=10`（或其他一些号码）。</span><span class="sxs-lookup"><span data-stu-id="28a4d-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="28a4d-245">到目前为止，你已测试的**编辑**链接*电影*页上工作、 从查询字符串中，你的页面进行读取 ID 和数据库查询以获取单个影片记录是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="28a4d-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="28a4d-246">你可以更改影片信息中，但不执行任何操作时你单击**提交更改**。</span><span class="sxs-lookup"><span data-stu-id="28a4d-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="28a4d-247">添加代码以使用用户的更改更新电影</span><span class="sxs-lookup"><span data-stu-id="28a4d-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="28a4d-248">在*EditMovie.cshtml*文件中，若要实现 （保存更改） 的第二个函数，添加下面的代码内的右大括号`@`块。</span><span class="sxs-lookup"><span data-stu-id="28a4d-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="28a4d-249">(如果你不确定如何将代码放，你可以查看[完整代码清单编辑影片页](#Complete_Page_Listing_for_EditMovie)显示在本教程末尾上。)</span><span class="sxs-lookup"><span data-stu-id="28a4d-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="28a4d-250">同样，此标记和代码是类似于中的代码*AddMovie*。</span><span class="sxs-lookup"><span data-stu-id="28a4d-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="28a4d-251">代码位于`if(IsPost)`阻止，因为此代码仅在用户单击时，才运行**提交更改**按钮&mdash;，即，当 （并仅当） 发送窗体。</span><span class="sxs-lookup"><span data-stu-id="28a4d-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="28a4d-252">在这种情况下，你不使用如测试`if(IsPost && Validation.IsValid())`— 也就是说，您将不进行合并两个测试均通过使用 and。</span><span class="sxs-lookup"><span data-stu-id="28a4d-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="28a4d-253">在此页上，你首先确定是否存在窗体提交 (`if(IsPost)`)，并仅然后注册以进行验证的字段。</span><span class="sxs-lookup"><span data-stu-id="28a4d-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="28a4d-254">然后你可以测试将验证结果 (`if(Validation.IsValid()`)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="28a4d-255">流的方向是与中略有不同*AddMovie.cshtml*页上，但效果的方式相同。</span><span class="sxs-lookup"><span data-stu-id="28a4d-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="28a4d-256">使用获取的值的文本框中`Request.Form["title"]`和其他的类似代码`<input>`元素。</span><span class="sxs-lookup"><span data-stu-id="28a4d-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="28a4d-257">请注意，此时，代码获取的电影 ID 外的隐藏字段 (`<input type="hidden">`)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="28a4d-258">当页上运行时第一次时，代码将收到查询字符串外的 ID。</span><span class="sxs-lookup"><span data-stu-id="28a4d-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="28a4d-259">从隐藏的字段，以确保您将获得的影片的最初所显示的 ID，以防从那时起以某种方式更改查询字符串中获取的值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="28a4d-260">确实太重要区别*AddMovie*代码和此代码是在此代码中使用 SQL`Update`语句而不是`Insert Into`语句。</span><span class="sxs-lookup"><span data-stu-id="28a4d-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="28a4d-261">下面的示例演示的 sql 语法`Update`语句：</span><span class="sxs-lookup"><span data-stu-id="28a4d-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="28a4d-262">还可以按任意顺序指定任何列并不一定必须更新在每个列`Update`操作。</span><span class="sxs-lookup"><span data-stu-id="28a4d-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="28a4d-263">(因为，实际上将记录保存为一个新的记录，并且不允许的无法更新 ID 本身，`Update`操作。)</span><span class="sxs-lookup"><span data-stu-id="28a4d-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="28a4d-264">**重要**`Where`子句中的 ID 为非常重要，因为这是如何数据库知道哪个数据库记录你想要更新。</span><span class="sxs-lookup"><span data-stu-id="28a4d-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="28a4d-265">如果您离开`Where`子句，数据库将更新*每个*记录在数据库中。</span><span class="sxs-lookup"><span data-stu-id="28a4d-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="28a4d-266">在大多数情况下，这个位置是灾难。</span><span class="sxs-lookup"><span data-stu-id="28a4d-266">In most cases, that would be a disaster.</span></span>


<span data-ttu-id="28a4d-267">在代码中，通过使用占位符要更新的值传递给 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="28a4d-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="28a4d-268">若要重复我们之前讲： 出于安全原因，*仅*占位符用于将值传递给 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="28a4d-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="28a4d-269">该代码使用后`db.Execute`运行`Update`语句，它将重定向回列表页上，你可以在其中看到更改。</span><span class="sxs-lookup"><span data-stu-id="28a4d-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="28a4d-270">**不同的 SQL 语句，不同的方法**</span><span class="sxs-lookup"><span data-stu-id="28a4d-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="28a4d-271">你可能已经注意到使用略有不同的方法运行不同的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="28a4d-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="28a4d-272">若要运行`Select`查询，它可能返回多个记录，则使用`Query`方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="28a4d-273">若要运行`Select`你知道的查询将返回只有一个数据库项目，则使用`QuerySingle`方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="28a4d-274">若要运行的命令进行更改，但是，不返回数据库项目，你可以使用`Execute`方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="28a4d-275">你必须具有不同的方法，因为每个返回不同的结果，正如你已看到之间的差异`Query`和`QuerySingle`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="28a4d-276">(`Execute`方法实际上也返回一个值&mdash;即受该命令的数据库行数&mdash;但你已被忽略，到目前为止。)</span><span class="sxs-lookup"><span data-stu-id="28a4d-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="28a4d-277">当然，`Query`方法可能返回只有一行的数据库。</span><span class="sxs-lookup"><span data-stu-id="28a4d-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="28a4d-278">但是，ASP.NET 始终会将结果`Query`作为集合的方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="28a4d-279">即使该方法返回一个行，必须从集合中提取该单个行。</span><span class="sxs-lookup"><span data-stu-id="28a4d-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="28a4d-280">因此，在情况下，你*知道*您就会得到只有一个行，它就会执行更方便地使用`QuerySingle`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="28a4d-281">有几个其他执行特定类型的数据库操作的方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="28a4d-282">你可以查找数据库中的方法的列表[ASP.NET 网页 API 快速参考](../../api-reference/asp-net-web-pages-api-reference.md#Data)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>


## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="28a4d-283">使验证 ID 更可靠</span><span class="sxs-lookup"><span data-stu-id="28a4d-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="28a4d-284">页将运行，第一次你的电影 ID 从获取查询字符串，以便你可以从数据库中获取该影片。</span><span class="sxs-lookup"><span data-stu-id="28a4d-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="28a4d-285">做确保存在实际的值转查找，未使用此代码：</span><span class="sxs-lookup"><span data-stu-id="28a4d-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="28a4d-286">此代码用于可以确保，如果用户获取到*EditMovies*页，不需要先选择中的一个影片*电影*页上，页面将显示用户友好错误消息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="28a4d-287">（否则，用户将看到一个错误，也许只需将它们混淆。）</span><span class="sxs-lookup"><span data-stu-id="28a4d-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="28a4d-288">但是，此验证不十分可靠。</span><span class="sxs-lookup"><span data-stu-id="28a4d-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="28a4d-289">此外可能出现这些错误调用页：</span><span class="sxs-lookup"><span data-stu-id="28a4d-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="28a4d-290">ID 不是数字。</span><span class="sxs-lookup"><span data-stu-id="28a4d-290">The ID isn't a number.</span></span> <span data-ttu-id="28a4d-291">例如，页上，也可以调用，如将 URL `http://localhost:nnnnn/EditMovie?id=abc`。</span><span class="sxs-lookup"><span data-stu-id="28a4d-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="28a4d-292">ID 是一个数字，但是它引用不存在一部电影 (例如， `http://localhost:nnnnn/EditMovie?id=100934`)。</span><span class="sxs-lookup"><span data-stu-id="28a4d-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="28a4d-293">如果你想要查看从这些 Url，运行产生的错误*电影*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="28a4d-294">选择一部电影，若要编辑，，然后更改的 URL *EditMovie*向包含字母的 URL page 的 ID 或不存在电影 ID。</span><span class="sxs-lookup"><span data-stu-id="28a4d-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="28a4d-295">因此，你该怎么办？</span><span class="sxs-lookup"><span data-stu-id="28a4d-295">So what should you do?</span></span> <span data-ttu-id="28a4d-296">第一个解决方法是确保，不仅能将 ID 传递到页中，但 ID 是一个整数。</span><span class="sxs-lookup"><span data-stu-id="28a4d-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="28a4d-297">更改的代码`!IsPost`测试看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="28a4d-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="28a4d-298">你已添加到第二个条件`IsEmpty`测试，与链接`&&`（逻辑与）：</span><span class="sxs-lookup"><span data-stu-id="28a4d-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="28a4d-299">您可能还记得从[为 ASP.NET 网页编程的介绍](../introducing-razor-syntax-c.md)等方法的教程`AsBool``AsInt`将字符字符串转换为其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="28a4d-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="28a4d-300">`IsInt`方法 (和等其他一些`IsBool`和`IsDateTime`) 类似。</span><span class="sxs-lookup"><span data-stu-id="28a4d-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="28a4d-301">但是，它们仅用于测试是否你*可以*转换为字符串，而不实际执行转换。</span><span class="sxs-lookup"><span data-stu-id="28a4d-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="28a4d-302">这里基本上就*如果查询字符串值可以转换为整数...*.</span><span class="sxs-lookup"><span data-stu-id="28a4d-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="28a4d-303">不存在一部电影查找其他潜在问题。</span><span class="sxs-lookup"><span data-stu-id="28a4d-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="28a4d-304">若要获取一部电影的代码看起来像此代码：</span><span class="sxs-lookup"><span data-stu-id="28a4d-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="28a4d-305">如果你通过`movieId`值赋给`QuerySingle`不对应于实际的电影的方法，未返回任何内容且符合语句 (例如， `title=row.Title`) 会产生错误。</span><span class="sxs-lookup"><span data-stu-id="28a4d-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="28a4d-306">同样是简单的解决方法。</span><span class="sxs-lookup"><span data-stu-id="28a4d-306">Again there's an easy fix.</span></span> <span data-ttu-id="28a4d-307">如果`db.QuerySingle`方法会返回任何结果，`row`变量将为 null。</span><span class="sxs-lookup"><span data-stu-id="28a4d-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="28a4d-308">这样你就可以检查是否`row`变量为 null，再尝试从其获取值。</span><span class="sxs-lookup"><span data-stu-id="28a4d-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="28a4d-309">下面的代码添加`if`围绕获取外的值的语句块`row`对象：</span><span class="sxs-lookup"><span data-stu-id="28a4d-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="28a4d-310">利用这些两个其他验证测试时，页面将成为更防护。</span><span class="sxs-lookup"><span data-stu-id="28a4d-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="28a4d-311">完整代码`!IsPost`分支现在看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="28a4d-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="28a4d-312">此任务是一个很好用法。 我们将需要再次注意`else`块。</span><span class="sxs-lookup"><span data-stu-id="28a4d-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="28a4d-313">如果测试未通过，`else`块设置错误消息。</span><span class="sxs-lookup"><span data-stu-id="28a4d-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="28a4d-314">添加的链接以返回电影页</span><span class="sxs-lookup"><span data-stu-id="28a4d-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="28a4d-315">最终且有帮助的详细信息是将链接添加回*电影*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="28a4d-316">在普通的事件流中，用户将开始在*电影*页上，单击**编辑**链接。</span><span class="sxs-lookup"><span data-stu-id="28a4d-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="28a4d-317">将用户带到*EditMovie*页上，它们可以在其中编辑电影并单击按钮。</span><span class="sxs-lookup"><span data-stu-id="28a4d-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="28a4d-318">代码处理此更改后，它将重定向回*电影*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="28a4d-319">但是：</span><span class="sxs-lookup"><span data-stu-id="28a4d-319">However:</span></span>

- <span data-ttu-id="28a4d-320">用户可能会决定不更改任何内容。</span><span class="sxs-lookup"><span data-stu-id="28a4d-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="28a4d-321">用户可能收到此页面没有先单击**编辑**中链接*电影*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="28a4d-322">无论哪种方式，你想要使其可以方便地返回到主列表。</span><span class="sxs-lookup"><span data-stu-id="28a4d-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="28a4d-323">很容易修复&mdash;结束之后添加以下标记`</form>`标记中的标记：</span><span class="sxs-lookup"><span data-stu-id="28a4d-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="28a4d-324">此标记使用的相同语法`<a>`在其他位置，你已了解的元素。</span><span class="sxs-lookup"><span data-stu-id="28a4d-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="28a4d-325">URL 包含`~`表示"在网站的根目录。"</span><span class="sxs-lookup"><span data-stu-id="28a4d-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="28a4d-326">测试电影更新过程</span><span class="sxs-lookup"><span data-stu-id="28a4d-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="28a4d-327">现在，你可以测试。</span><span class="sxs-lookup"><span data-stu-id="28a4d-327">Now you can test.</span></span> <span data-ttu-id="28a4d-328">运行*电影*页，然后单击**编辑**旁边影片。</span><span class="sxs-lookup"><span data-stu-id="28a4d-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="28a4d-329">当*EditMovie*页出现时，更改到电影，然后单击**提交更改**。</span><span class="sxs-lookup"><span data-stu-id="28a4d-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="28a4d-330">影片列表出现时，请确保所做的更改，将显示。</span><span class="sxs-lookup"><span data-stu-id="28a4d-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="28a4d-331">若要确保验证正常工作，请单击**编辑**为另一个的电影。</span><span class="sxs-lookup"><span data-stu-id="28a4d-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="28a4d-332">当你到达*EditMovie*页上，清除**流派**字段 (或**年**字段，或两者)，然后尝试提交所做的更改。</span><span class="sxs-lookup"><span data-stu-id="28a4d-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="28a4d-333">如你所料，你将看到一个错误：</span><span class="sxs-lookup"><span data-stu-id="28a4d-333">You'll see an error, as you'd expect:</span></span>

![编辑显示验证错误的影片页](updating-data/_static/image4.png)

<span data-ttu-id="28a4d-335">单击**返回到影片列表**链接以放弃所做的更改并返回到*电影*页。</span><span class="sxs-lookup"><span data-stu-id="28a4d-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="28a4d-336">接下来</span><span class="sxs-lookup"><span data-stu-id="28a4d-336">Coming Up Next</span></span>

<span data-ttu-id="28a4d-337">在下一步的教程中，你将了解如何删除电影记录。</span><span class="sxs-lookup"><span data-stu-id="28a4d-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="28a4d-338">电影页 （经过更新带有编辑链接） 的完整列表</span><span class="sxs-lookup"><span data-stu-id="28a4d-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="28a4d-339">完成编辑影片页的页列表</span><span class="sxs-lookup"><span data-stu-id="28a4d-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="28a4d-340">其他资源</span><span class="sxs-lookup"><span data-stu-id="28a4d-340">Additional Resources</span></span>

- [<span data-ttu-id="28a4d-341">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="28a4d-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="28a4d-342">[SQL UPDATE 语句](http://www.w3schools.com/sql/sql_update.asp)W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="28a4d-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="28a4d-343">[上一页](entering-data.md)
> [下一页](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="28a4d-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
