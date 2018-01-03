---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: "引入的 ASP.NET Web Pages-删除数据库数据 |Microsoft 文档"
author: tfitzmac
description: "本教程演示了如何删除单个数据库条目。 它假定你已完成的 ASP.NET Web pa。 在更新数据库数据通过一系列..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/02/2018
ms.topic: article
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: 5bc92b5d40e7a55dcd730d552c71031d913b277e
ms.sourcegitcommit: 281f0c614543a6c3db565ea4655b70fe49b61d84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2018
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="64d45-104">引入了 ASP.NET Web 页-删除数据库数据</span><span class="sxs-lookup"><span data-stu-id="64d45-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>
====================
<span data-ttu-id="64d45-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="64d45-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="64d45-106">本教程演示了如何删除单个数据库条目。</span><span class="sxs-lookup"><span data-stu-id="64d45-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="64d45-107">它假定你已完成通过系列[更新数据库数据中的 ASP.NET Web Pages](updating-data.md)。</span><span class="sxs-lookup"><span data-stu-id="64d45-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="64d45-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="64d45-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="64d45-109">如何从记录列表中选择单独的记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="64d45-110">如何从数据库中删除单个记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="64d45-111">如何检查特定按钮被单击窗体中。</span><span class="sxs-lookup"><span data-stu-id="64d45-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="64d45-112">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="64d45-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="64d45-113">`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="64d45-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="64d45-114">SQL`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="64d45-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="64d45-115">`Database.Execute`方法来运行 SQL`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="64d45-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="64d45-116">你将生成</span><span class="sxs-lookup"><span data-stu-id="64d45-116">What You'll Build</span></span>

<span data-ttu-id="64d45-117">在前面的教程，您学习了如何更新现有的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="64d45-118">本教程类似，但在于而不是更新记录，你将删除它。</span><span class="sxs-lookup"><span data-stu-id="64d45-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="64d45-119">进程是大致相同，只不过删除是更简单，因此本教程将会比较短。</span><span class="sxs-lookup"><span data-stu-id="64d45-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="64d45-120">在*电影*页上，你将更新`WebGrid`帮助器以便它显示**删除**旁边每个影片随附链接**编辑**前面添加的链接。</span><span class="sxs-lookup"><span data-stu-id="64d45-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![显示一个删除链接，以便每个电影的电影页](deleting-data/_static/image1.png)

<span data-ttu-id="64d45-122">包含编辑，当你单击**删除**链接，它将你带到不同的页的影片信息已在窗体：</span><span class="sxs-lookup"><span data-stu-id="64d45-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![删除具有显示一部电影的电影页](deleting-data/_static/image2.png)

<span data-ttu-id="64d45-124">然后，可以单击按钮以永久删除的记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="64d45-125">将删除链接添加到影片列表</span><span class="sxs-lookup"><span data-stu-id="64d45-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="64d45-126">你将首先，通过添加**删除**链接到`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="64d45-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="64d45-127">此链接是类似于**编辑**你在前面的教程中添加的链接。</span><span class="sxs-lookup"><span data-stu-id="64d45-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="64d45-128">打开*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="64d45-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="64d45-129">更改`WebGrid`页上通过添加列的正文中的标记。</span><span class="sxs-lookup"><span data-stu-id="64d45-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="64d45-130">下面是已修改的标记：</span><span class="sxs-lookup"><span data-stu-id="64d45-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="64d45-131">新的列是这样一个：</span><span class="sxs-lookup"><span data-stu-id="64d45-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="64d45-132">网格配置的方式，**编辑**列是在网格中最左侧和**删除**列是最右边。</span><span class="sxs-lookup"><span data-stu-id="64d45-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="64d45-133">(没有后的逗号`Year`列现在，如果你未注意到，。)无需进行任何特殊有关这些链接列从何处，并轻松无法将其放彼此相邻。</span><span class="sxs-lookup"><span data-stu-id="64d45-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="64d45-134">在这种情况下，它们单独以使它们难以获取混淆。</span><span class="sxs-lookup"><span data-stu-id="64d45-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![电影页，带有编辑和详细信息的链接标记以显示它们彼此不是](deleting-data/_static/image3.png)

<span data-ttu-id="64d45-136">新的列显示一个链接 (`<a>`元素) 的文本显示的是"删除"。</span><span class="sxs-lookup"><span data-stu-id="64d45-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="64d45-137">链接目标的 (其`href`特性) 是具有最终解析为此 URL，类似于下面的代码`id`为每个电影不同的值：</span><span class="sxs-lookup"><span data-stu-id="64d45-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="64d45-138">此链接将调用一个名为页*DeleteMovie*并将其传递所选电影的 ID。</span><span class="sxs-lookup"><span data-stu-id="64d45-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="64d45-139">本教程将不会进行此链接的构造方式，有关详细信息，因为它是几乎与**编辑**从前面的教程的链接 ([更新数据库数据中的 ASP.NET Web Pages](updating-data.md))。</span><span class="sxs-lookup"><span data-stu-id="64d45-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="64d45-140">创建删除页</span><span class="sxs-lookup"><span data-stu-id="64d45-140">Creating the Delete Page</span></span>

<span data-ttu-id="64d45-141">现在，你可以创建将为目标的页面**删除**在网格中的链接。</span><span class="sxs-lookup"><span data-stu-id="64d45-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="64d45-142">**重要**首先选择要删除的记录，然后使用单独的页面和按钮以确认该过程的方法便非常重要的安全。</span><span class="sxs-lookup"><span data-stu-id="64d45-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="64d45-143">因为你已阅读在前面的教程，使*任何*到你的网站的更改排序应*始终*进行使用窗体&mdash;，即，使用 HTTP POST 操作。</span><span class="sxs-lookup"><span data-stu-id="64d45-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="64d45-144">如果你进行可能只需通过单击的链接 （即使用 GET 操作） 更改的站点，人员无法向网站发出简单请求和删除你的数据。</span><span class="sxs-lookup"><span data-stu-id="64d45-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="64d45-145">即使为搜索引擎爬网程序，那么编制索引的你的站点可能无意中删除数据，只需通过按照以下链接。</span><span class="sxs-lookup"><span data-stu-id="64d45-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="64d45-146">当你的应用程序允许用户更改的记录时，你必须以进行编辑仍向用户显示该记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="64d45-147">但你可能想要跳过此步骤中的删除一条记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="64d45-148">不要通过跳过该步骤。</span><span class="sxs-lookup"><span data-stu-id="64d45-148">Don't skip that step, though.</span></span> <span data-ttu-id="64d45-149">（它也是很有帮助的用户，请参阅记录并确认它们要删除的记录，应将它们。）</span><span class="sxs-lookup"><span data-stu-id="64d45-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="64d45-150">在后续教程组中，你将了解如何添加登录功能，因此用户将需要在删除一条记录之前登录。</span><span class="sxs-lookup"><span data-stu-id="64d45-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>


<span data-ttu-id="64d45-151">创建一个名为页*DeleteMovie.cshtml* ，并将替换为以下标记文件中：</span><span class="sxs-lookup"><span data-stu-id="64d45-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="64d45-152">此标记就像是*EditMovie*页，而不是使用文本框的只不过 (`<input type="text">`)，标记包括`<span>`元素。</span><span class="sxs-lookup"><span data-stu-id="64d45-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="64d45-153">此处没有任何可编辑。</span><span class="sxs-lookup"><span data-stu-id="64d45-153">There's nothing here to edit.</span></span> <span data-ttu-id="64d45-154">你所要做的只是显示，以便用户可以确保它们正在删除右电影的电影详细信息。</span><span class="sxs-lookup"><span data-stu-id="64d45-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="64d45-155">标记已包含允许用户返回到影片列表页的链接。</span><span class="sxs-lookup"><span data-stu-id="64d45-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="64d45-156">作为 in *EditMovie*隐藏字段中存储页上，选中的电影的 ID。</span><span class="sxs-lookup"><span data-stu-id="64d45-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="64d45-157">（它传递到页面首先作为查询字符串值。）没有`Html.ValidationSummary`将显示验证错误的调用。</span><span class="sxs-lookup"><span data-stu-id="64d45-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="64d45-158">在这种情况下，错误可能是没有电影 ID 已传递到页或电影 ID 无效。</span><span class="sxs-lookup"><span data-stu-id="64d45-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="64d45-159">如果有人运行而不事先选择中的一个影片的此页可能出现此情况*电影*页。</span><span class="sxs-lookup"><span data-stu-id="64d45-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="64d45-160">该按钮标题**删除电影**，并且其名称属性设置为`buttonDelete`。</span><span class="sxs-lookup"><span data-stu-id="64d45-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="64d45-161">`name`属性将使用在代码中，用于标识提交了表单的按钮。</span><span class="sxs-lookup"><span data-stu-id="64d45-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="64d45-162">你将需要编写代码以 1） 时将首先显示的页读取电影详细信息，并且用户单击按钮时，2） 实际删除影片。</span><span class="sxs-lookup"><span data-stu-id="64d45-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="64d45-163">添加代码以读取单个电影</span><span class="sxs-lookup"><span data-stu-id="64d45-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="64d45-164">在顶部*DeleteMovie.cshtml*页上，添加下面的代码块：</span><span class="sxs-lookup"><span data-stu-id="64d45-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="64d45-165">此标记是中的相应代码相同*EditMovie*页。</span><span class="sxs-lookup"><span data-stu-id="64d45-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="64d45-166">它获取查询字符串外的电影 ID，并使用 ID 来从数据库中读取一条记录。</span><span class="sxs-lookup"><span data-stu-id="64d45-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="64d45-167">代码包含验证测试 (`IsInt()`和`row != null`) 若要确保传递到页面的电影 ID 是否有效。</span><span class="sxs-lookup"><span data-stu-id="64d45-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="64d45-168">请记住，此代码仅应运行第一次运行页面。</span><span class="sxs-lookup"><span data-stu-id="64d45-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="64d45-169">你不想要重新读取从数据库的电影记录，当用户单击**删除电影**按钮。</span><span class="sxs-lookup"><span data-stu-id="64d45-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="64d45-170">因此，用于读取电影位于显示测试的代码`if(!IsPost)` &mdash; ，即*如果请求不是 post 操作 （提交窗体）*。</span><span class="sxs-lookup"><span data-stu-id="64d45-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="64d45-171">添加代码以删除所选的电影</span><span class="sxs-lookup"><span data-stu-id="64d45-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="64d45-172">若要删除的电影，用户单击按钮时，添加以下代码的右大括号内`@`块：</span><span class="sxs-lookup"><span data-stu-id="64d45-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="64d45-173">此代码是相似的代码更新现有记录，但更简单。</span><span class="sxs-lookup"><span data-stu-id="64d45-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="64d45-174">基本上，代码将运行 SQL`Delete`语句。</span><span class="sxs-lookup"><span data-stu-id="64d45-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="64d45-175">作为 in *EditMovie*页上，代码都处于`if(IsPost)`块。</span><span class="sxs-lookup"><span data-stu-id="64d45-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="64d45-176">此时，`if()`条件是稍微有些复杂：</span><span class="sxs-lookup"><span data-stu-id="64d45-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="64d45-177">有以下两种情况。</span><span class="sxs-lookup"><span data-stu-id="64d45-177">There are two conditions here.</span></span> <span data-ttu-id="64d45-178">第一种是，在正在提交页面，如你所见之前&mdash; `if(IsPost)`。</span><span class="sxs-lookup"><span data-stu-id="64d45-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="64d45-179">第二个条件是`!Request["buttonDelete"].IsEmpty()`，表示的请求都有一个名为对象`buttonDelete`。</span><span class="sxs-lookup"><span data-stu-id="64d45-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="64d45-180">不可否认，它是一种测试哪个按钮提交了表单的间接方法。</span><span class="sxs-lookup"><span data-stu-id="64d45-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="64d45-181">如果窗体包含多个提交按钮，则只有被单击的按钮名称将出现在请求中。</span><span class="sxs-lookup"><span data-stu-id="64d45-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="64d45-182">因此，在逻辑上，如果特定的按钮的名称将出现在请求&mdash;规定在代码中，如果该按钮不为空或&mdash;即提交了表单的按钮。</span><span class="sxs-lookup"><span data-stu-id="64d45-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="64d45-183">`&&`运算符表示"和"（逻辑与）。</span><span class="sxs-lookup"><span data-stu-id="64d45-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="64d45-184">因此整个`if`条件是...</span><span class="sxs-lookup"><span data-stu-id="64d45-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="64d45-185">*此请求是 post （而不是第一次请求）*</span><span class="sxs-lookup"><span data-stu-id="64d45-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="64d45-186">AND</span><span class="sxs-lookup"><span data-stu-id="64d45-186">AND</span></span>  
  
<span data-ttu-id="64d45-187"> `buttonDelete`*按钮已提交了表单的按钮。*</span><span class="sxs-lookup"><span data-stu-id="64d45-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="64d45-188">（事实上，此页） 此表单包含只包含一个按钮，因此的其他测试`buttonDelete`从技术上讲不是必需的。</span><span class="sxs-lookup"><span data-stu-id="64d45-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="64d45-189">但是，你将要执行的操作将永久删除数据。</span><span class="sxs-lookup"><span data-stu-id="64d45-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="64d45-190">因此，你想要为确保尽可能只在用户显式请求它时要执行该操作。</span><span class="sxs-lookup"><span data-stu-id="64d45-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="64d45-191">例如，假设你展开此页更高版本，并向其添加其他按钮。</span><span class="sxs-lookup"><span data-stu-id="64d45-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="64d45-192">仅当删除电影的代码将运行即使如此，`buttonDelete`按钮被单击。</span><span class="sxs-lookup"><span data-stu-id="64d45-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="64d45-193">作为 in *EditMovie*页上，从隐藏的字段中获取的 ID，然后运行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="64d45-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="64d45-194">语法`Delete`语句是：</span><span class="sxs-lookup"><span data-stu-id="64d45-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="64d45-195">务必包括`WHERE`子句和 id。</span><span class="sxs-lookup"><span data-stu-id="64d45-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="64d45-196">如果您忽略 WHERE 子句，*将删除表中的所有记录*。</span><span class="sxs-lookup"><span data-stu-id="64d45-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="64d45-197">如您所见，你向 SQL 命令的 ID 值通过使用占位符传递。</span><span class="sxs-lookup"><span data-stu-id="64d45-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="64d45-198">测试电影删除过程</span><span class="sxs-lookup"><span data-stu-id="64d45-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="64d45-199">现在，你可以测试。</span><span class="sxs-lookup"><span data-stu-id="64d45-199">Now you can test.</span></span> <span data-ttu-id="64d45-200">运行*电影*页，然后单击**删除**旁边影片。</span><span class="sxs-lookup"><span data-stu-id="64d45-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="64d45-201">当*DeleteMovie*页出现时，单击**删除电影**。</span><span class="sxs-lookup"><span data-stu-id="64d45-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![突出显示的删除电影按钮删除影片页](deleting-data/_static/image4.png)

<span data-ttu-id="64d45-203">单击按钮时，代码删除电影，并返回到影片列表。</span><span class="sxs-lookup"><span data-stu-id="64d45-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="64d45-204">存在可以搜索已删除的电影并确认它已被删除。</span><span class="sxs-lookup"><span data-stu-id="64d45-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="64d45-205">接下来</span><span class="sxs-lookup"><span data-stu-id="64d45-205">Coming Up Next</span></span>

<span data-ttu-id="64d45-206">下一教程演示如何在你的站点上提供的所有页，常见的外观和布局。</span><span class="sxs-lookup"><span data-stu-id="64d45-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="64d45-207">电影页 （经过更新带有删除链接） 的完整列表</span><span class="sxs-lookup"><span data-stu-id="64d45-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="64d45-208">DeleteMovie 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="64d45-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="64d45-209">其他资源</span><span class="sxs-lookup"><span data-stu-id="64d45-209">Additional Resources</span></span>

- [<span data-ttu-id="64d45-210">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="64d45-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="64d45-211">[SQL DELETE 语句](http://www.w3schools.com/sql/sql_delete.asp)W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="64d45-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="64d45-212">[上一页](updating-data.md)
[下一页](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="64d45-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
