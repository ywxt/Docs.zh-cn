---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Introducing ASP.NET 网页-正在删除数据库数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何删除单独的数据库条目。 它假定你已完成通过在 ASP.NET Web 的 pa。 中更新数据库数据系列...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: b2ef8fcc8cc534bd31fea83bf0b085b85995f417
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2018
ms.locfileid: "51020437"
---
<a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="9a5ac-104">ASP.NET 网页简介-正在删除数据库数据</span><span class="sxs-lookup"><span data-stu-id="9a5ac-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>
====================
<span data-ttu-id="9a5ac-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9a5ac-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9a5ac-106">本教程演示如何删除单独的数据库条目。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="9a5ac-107">它假定你已完成通过时序[更新数据库数据在 ASP.NET Web Pages](updating-data.md)。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="9a5ac-108">你将学习：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9a5ac-109">如何从记录列表中选择的单个记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="9a5ac-110">如何从数据库中删除一条记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="9a5ac-111">如何检查特定按钮被单击窗体中。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="9a5ac-112">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="9a5ac-113">`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="9a5ac-114">SQL`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="9a5ac-115">`Database.Execute`方法来运行 SQL`Delete`命令。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="9a5ac-116">你将生成</span><span class="sxs-lookup"><span data-stu-id="9a5ac-116">What You'll Build</span></span>

<span data-ttu-id="9a5ac-117">在前面的教程，您学习了如何更新现有的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="9a5ac-118">本教程是类似，只不过而不是更新记录，则会将其删除。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="9a5ac-119">进程是大致相同，只不过删除是更简单，因此本教程将会比较短。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="9a5ac-120">在*电影*页上，你将更新`WebGrid`帮助程序，以便它显示**删除**旁边伴随每个电影链接**编辑**前面添加的链接。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![电影页面，其中显示每个电影的删除链接](deleting-data/_static/image1.png)

<span data-ttu-id="9a5ac-122">使用编辑，单击**删除**链接，它将您带入不同的页的电影信息已在窗体：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![删除具有显示电影的电影页](deleting-data/_static/image2.png)

<span data-ttu-id="9a5ac-124">然后可以单击按钮后，若要永久删除的记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="9a5ac-125">将删除链接添加到电影列表</span><span class="sxs-lookup"><span data-stu-id="9a5ac-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="9a5ac-126">将首先添加**删除**链接到`WebGrid`帮助器。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="9a5ac-127">此链接是类似于**编辑**添加上一教程中的链接。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="9a5ac-128">打开*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="9a5ac-129">更改`WebGrid`通过添加列页的正文中的标记。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="9a5ac-130">下面是修改后的标记：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="9a5ac-131">新列是这样一个：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="9a5ac-132">在网格的配置的方式**编辑**列是在网格中最左侧并**删除**列是最右侧。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="9a5ac-133">(没有逗号之后`Year`列现在，如果您没有注意到的。)没有什么特别之处这些链接列在哪里，并可以轻松将其彼此。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="9a5ac-134">在这种情况下，它们是单独以使其难以搞乱套了。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![电影页面包含一个编辑和详细信息的链接标记以显示它们彼此不是](deleting-data/_static/image3.png)

<span data-ttu-id="9a5ac-136">新列将显示一个链接 (`<a>`元素) 的文本显示的是"删除"。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="9a5ac-137">链接的目标 (其`href`属性) 是具有最终解析为此 URL，类似的代码`id`每部电影的不同值：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="9a5ac-138">此链接将调用一个名为页*DeleteMovie*并将其传递所选的电影 ID。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="9a5ac-139">本教程不会详细介绍如何构造此链接，因为它几乎等同于**编辑**以前一教程的链接 ([更新数据库数据在 ASP.NET Web Pages](updating-data.md))。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="9a5ac-140">创建删除页</span><span class="sxs-lookup"><span data-stu-id="9a5ac-140">Creating the Delete Page</span></span>

<span data-ttu-id="9a5ac-141">现在，你可以创建将用于目标的页面**删除**网格中的链接。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9a5ac-142">**重要**首先选择要删除的记录，然后使用一个单独的页面和按钮以确认该过程的方法是非常重要的安全。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="9a5ac-143">如您所读在前面的教程，使*任何*更改对你的网站的排序应*始终*来完成使用窗体&mdash;使用 HTTP POST 操作。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="9a5ac-144">如果您成为可能只需通过单击的链接 （即使用 GET 操作） 更改的站点，人员无法向你的站点发出简单请求和删除你的数据。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="9a5ac-145">甚至一个搜索引擎爬网程序，索引您的网站可能无意中删除数据，只需通过以下链接。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="9a5ac-146">当你的应用让他人更改记录时，必须编辑仍要向用户显示该记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="9a5ac-147">但您可能想要跳过此步骤中的删除一条记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="9a5ac-148">不但是跳过该步骤。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-148">Don't skip that step, though.</span></span> <span data-ttu-id="9a5ac-149">（该技术还有助于用户可以看到记录，并确认他们要删除它们的记录。）</span><span class="sxs-lookup"><span data-stu-id="9a5ac-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="9a5ac-150">在后续教程集中，您将了解如何添加登录功能，因此用户需要登录，然后再删除记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>


<span data-ttu-id="9a5ac-151">创建一个名为页*DeleteMovie.cshtml*和替换为以下标记文件中：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="9a5ac-152">此标记就像*EditMovie*页中的，不同之处在于而不是使用文本框 (`<input type="text">`)，标记包括`<span>`元素。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="9a5ac-153">此处没有任何编辑。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-153">There's nothing here to edit.</span></span> <span data-ttu-id="9a5ac-154">只需是显示电影详细信息，以便用户可以确保它们要删除右电影。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="9a5ac-155">标记已包含允许用户返回到影片列表页的链接。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="9a5ac-156">在中作为*EditMovie*页上，将所选电影 ID 存储在隐藏字段中。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="9a5ac-157">（它传递到页中第一个位置中作为查询字符串值。）没有`Html.ValidationSummary`将显示验证错误的调用。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="9a5ac-158">在这种情况下，该错误可能是任何电影 ID 已传递到页或电影 ID 无效。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="9a5ac-159">如果有人运行而无需首先选择电影中的此页，可能会发生这种情况下*电影*页。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="9a5ac-160">该按钮标题**删除电影**，并且其名称属性设置为`buttonDelete`。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="9a5ac-161">`name`属性将使用在代码中，用于标识提交窗体的按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="9a5ac-162">您必须编写代码以 1） 当第一次显示页面时读取电影详细信息，以及 2） 实际删除此电影，当用户单击按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="9a5ac-163">添加代码来读取单个电影</span><span class="sxs-lookup"><span data-stu-id="9a5ac-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="9a5ac-164">在顶部*DeleteMovie.cshtml*页上，添加以下代码块：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="9a5ac-165">此标记是中的相应代码相同*EditMovie*页。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="9a5ac-166">获取查询字符串外的电影 ID，并使用 ID 来从数据库读取一条记录。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="9a5ac-167">该代码包括验证测试 (`IsInt()`和`row != null`) 以确保传递到页电影 ID 是否有效。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="9a5ac-168">请记住此代码应仅运行该页面运行第一次。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="9a5ac-169">不想要重新读取电影记录数据库中的，当用户单击**删除电影**按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="9a5ac-170">因此，代码读取电影是内部测试表明`if(!IsPost)` &mdash; ，即*如果请求不是 post 操作 （表单提交）*。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="9a5ac-171">添加代码以删除所选的电影</span><span class="sxs-lookup"><span data-stu-id="9a5ac-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="9a5ac-172">若要删除电影，当用户单击按钮时，添加以下代码置于右大括号的`@`块：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="9a5ac-173">此代码是类似的代码更新现有记录，但更简单。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="9a5ac-174">基本上，代码将运行 SQL`Delete`语句。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="9a5ac-175">在中作为*EditMovie*页上，代码都位于`if(IsPost)`块。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="9a5ac-176">这一次，`if()`条件是稍微复杂一些：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="9a5ac-177">有以下两个条件。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-177">There are two conditions here.</span></span> <span data-ttu-id="9a5ac-178">第一种是，正在提交页面，如您所见之前&mdash; `if(IsPost)`。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="9a5ac-179">第二个条件是`!Request["buttonDelete"].IsEmpty()`，这意味着该请求具有一个名为`buttonDelete`。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="9a5ac-180">不可否认，它是测试哪个按钮提交窗体的间接方法。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="9a5ac-181">如果窗体包含多个提交按钮，只有被单击的按钮的名称将显示在请求中。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="9a5ac-182">因此，在逻辑上，如果特定按钮的名称将出现在请求&mdash;如所述在代码中，如果该按钮不为空或&mdash;是提交窗体的按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="9a5ac-183">`&&`运算符表示"和"（逻辑与）。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="9a5ac-184">因此整个`if`条件是...</span><span class="sxs-lookup"><span data-stu-id="9a5ac-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="9a5ac-185">*此请求为 post （而不是首次请求）*</span><span class="sxs-lookup"><span data-stu-id="9a5ac-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="9a5ac-186">AND</span><span class="sxs-lookup"><span data-stu-id="9a5ac-186">AND</span></span>  
  
<span data-ttu-id="9a5ac-187">`buttonDelete` *按钮已提交窗体的按钮。*</span><span class="sxs-lookup"><span data-stu-id="9a5ac-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="9a5ac-188">（事实上，此页） 此窗体包含只有一个按钮，因此其他测试`buttonDelete`从技术上讲不是必需的。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="9a5ac-189">尽管如此，您要执行的操作将永久删除数据。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="9a5ac-190">因此，你想要为确保尽可能仅当用户已显式请求时要执行该操作。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="9a5ac-191">例如，假设您稍后扩展此页，并向其添加其他按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="9a5ac-192">仅当删除电影的代码将运行即使如此，`buttonDelete`所单击的按钮。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="9a5ac-193">在中作为*EditMovie*页上，从隐藏字段获取 ID，然后运行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="9a5ac-194">语法`Delete`语句是：</span><span class="sxs-lookup"><span data-stu-id="9a5ac-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="9a5ac-195">务必包括`WHERE`子句和 id。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="9a5ac-196">如果省略 WHERE 子句中，*表中的所有记录将被都删除*。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="9a5ac-197">如您所见，您的 ID 值传递给 SQL 命令使用占位符。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="9a5ac-198">测试电影删除过程</span><span class="sxs-lookup"><span data-stu-id="9a5ac-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="9a5ac-199">现在，可以测试。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-199">Now you can test.</span></span> <span data-ttu-id="9a5ac-200">运行*电影*页，然后单击**删除**旁边电影。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="9a5ac-201">当*DeleteMovie*页面出现后，单击**删除电影**。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![删除突出显示的按钮删除电影的电影页](deleting-data/_static/image4.png)

<span data-ttu-id="9a5ac-203">当单击按钮时，代码将删除电影，并返回到影片列表。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="9a5ac-204">可以在曲终搜索已删除的电影，并确认它已被删除。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="9a5ac-205">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="9a5ac-205">Coming Up Next</span></span>

<span data-ttu-id="9a5ac-206">下一步的教程演示了如何授予您的站点上的所有页面，常见的外观和布局。</span><span class="sxs-lookup"><span data-stu-id="9a5ac-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="9a5ac-207">电影页面 （使用删除链接，更新） 的完整列表</span><span class="sxs-lookup"><span data-stu-id="9a5ac-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="9a5ac-208">DeleteMovie 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="9a5ac-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="9a5ac-209">其他资源</span><span class="sxs-lookup"><span data-stu-id="9a5ac-209">Additional Resources</span></span>

- [<span data-ttu-id="9a5ac-210">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="9a5ac-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="9a5ac-211">[SQL DELETE 语句](http://www.w3schools.com/sql/sql_delete.asp)W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="9a5ac-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9a5ac-212">[上一页](updating-data.md)
> [下一页](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="9a5ac-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
