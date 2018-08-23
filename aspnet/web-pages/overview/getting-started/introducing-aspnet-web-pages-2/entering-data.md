---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: Introducing ASP.NET 网页-通过使用窗体输入数据库的数据 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何创建输入窗体，然后输入数据时收到的窗体中插入数据库表使用 ASP.NET Web Pages （...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: 453ed888bc219175c5a3a25f857dfa79ab22b608
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825291"
---
<a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="6bf8c-103">Introducing ASP.NET 网页-通过使用窗体输入数据库数据</span><span class="sxs-lookup"><span data-stu-id="6bf8c-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>
====================
<span data-ttu-id="6bf8c-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6bf8c-105">本教程演示如何创建输入窗体，然后输入你从获取窗体到数据库表时使用 ASP.NET Web Pages (Razor) 的数据。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="6bf8c-106">它假定你已完成通过时序[基础知识的 HTML 窗体在 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581)。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="6bf8c-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="6bf8c-108">有关如何处理输入窗体的详细信息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="6bf8c-109">如何在数据库中添加数据 （插入）。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="6bf8c-110">如何确保用户具有在窗体 （如何验证用户输入） 中输入所需的值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="6bf8c-111">如何显示验证错误。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-111">How to display validation errors.</span></span>
> - <span data-ttu-id="6bf8c-112">如何从当前页跳转到另一个页面。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="6bf8c-113">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="6bf8c-114">`Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="6bf8c-115">SQL`Insert Into`语句</span><span class="sxs-lookup"><span data-stu-id="6bf8c-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="6bf8c-116">`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="6bf8c-117">`Response.Redirect` 方法。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-117">The `Response.Redirect` method.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="6bf8c-118">你将生成</span><span class="sxs-lookup"><span data-stu-id="6bf8c-118">What You'll Build</span></span>

<span data-ttu-id="6bf8c-119">通过编辑直接在 WebMatrix 中，使用数据库的数据库数据输入在本教程前面部分介绍了如何创建数据库，**数据库**工作区。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="6bf8c-120">在大多数应用中，这不是一个实用方法可将数据放入数据库，不过。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="6bf8c-121">因此在本教程中，您将创建一个基于 web 的界面，允许你或输入数据并将其保存到数据库的任何人。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="6bf8c-122">你将创建可在其中输入新影片的页面。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="6bf8c-123">该页将包含有您可以在其中输入电影标题、 genre 和年份字段 （文本框） 的输入窗体。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="6bf8c-124">页面将类似于此页：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-124">The page will look like this page:</span></span>

![在浏览器中添加电影页](entering-data/_static/image1.png)

<span data-ttu-id="6bf8c-126">文本框中将 HTML`<input>`元素看起来像此标记：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="6bf8c-127">创建基本的条目窗体</span><span class="sxs-lookup"><span data-stu-id="6bf8c-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="6bf8c-128">创建一个名为页*AddMovie.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="6bf8c-129">替换为以下标记文件中。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="6bf8c-130">覆盖所有内容;你稍后将在顶部添加代码块。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="6bf8c-131">此示例显示创建窗体的典型 HTML。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="6bf8c-132">它使用`<input>`元素的文本框和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="6bf8c-133">文本框中的标题通过使用标准创建`<label>`元素。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="6bf8c-134">`<fieldset>`和`<legend>`元素周围放置一个很好框窗体。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="6bf8c-135">请注意，在此页上，`<form>`元素使用`post`的值作为`method`属性。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="6bf8c-136">在上一教程中，创建使用窗体`get`方法。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="6bf8c-137">因为窗体提交到服务器的值，尽管请求未进行任何更改，这是正确的。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="6bf8c-138">它做不同的方式已提取数据。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="6bf8c-139">但是，在此页您*将*进行更改，您要添加新的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="6bf8c-140">因此，应使用此窗体`post`方法。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="6bf8c-141">(有关详细信息之间的差异`GET`和`POST`操作，请参阅[GET、 POST 和 HTTP 谓词安全](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)边栏上一教程中的。)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="6bf8c-142">请注意，每个文本框中有`name`元素 (`title`， `genre`， `year`)。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="6bf8c-143">正如您看到在上一教程，这些名称非常重要，因为您必须具有这些名称，以便稍后获取用户的输入。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="6bf8c-144">可以使用任何名称。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-144">You can use any names.</span></span> <span data-ttu-id="6bf8c-145">会有所帮助使用有意义名称帮助你记住您正在使用哪些数据。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="6bf8c-146">`value`属性的每个`<input>`元素包含的 Razor 代码 (例如， `Request.Form["title"]`)。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="6bf8c-147">提交窗体后，可以保留 （如果有） 在文本框中输入的值在上一教程中学习的这一技巧的版本。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="6bf8c-148">获取窗体值</span><span class="sxs-lookup"><span data-stu-id="6bf8c-148">Getting the Form Values</span></span>

<span data-ttu-id="6bf8c-149">接下来，你添加代码，用于处理窗体。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="6bf8c-150">在大纲中，将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="6bf8c-151">检查是否正在发布页面 （已提交）。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="6bf8c-152">要为你的代码仅时用户已单击按钮，不是在页面首次运行时运行。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="6bf8c-153">获取用户在文本框中输入的值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="6bf8c-154">在这种情况下，因为使用窗体`POST`谓词，则获取从窗体值`Request.Form`集合。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="6bf8c-155">将值插入新记录中作为*电影*数据库表。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="6bf8c-156">在文件顶部，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="6bf8c-157">前几行创建变量 (`title`， `genre`，和`year`) 以从文本框中保存的值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="6bf8c-158">在行`if(IsPost)`可确保设置变量*仅*当用户单击**添加电影**按钮 — 也就是说，当窗体已发布。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="6bf8c-159">正如您看到在前面的教程，获取文本框的值使用之类的表达式`Request.Form["name"]`，其中*名称*的名称`<input>`元素。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="6bf8c-160">变量的名称 (`title`， `genre`，和`year`) 是任意的。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="6bf8c-161">喜欢将分配给名称`<input>`元素，您可以您喜欢的任何调用它们。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="6bf8c-162">(变量的名称并不必一致的名称属性`<input>`窗体上的元素。)但是，如使用`<input>`元素，它是一个好办法使用反映它们所包含的数据的变量名称。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="6bf8c-163">当你编写代码时，采用一致的名称轻松记住您正在使用哪些数据。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="6bf8c-164">向数据库添加数据</span><span class="sxs-lookup"><span data-stu-id="6bf8c-164">Adding Data to the Database</span></span>

<span data-ttu-id="6bf8c-165">你只需添加了，只需在代码中分组*内*右大括号 ( `}` ) 的`if`块 （而不仅仅是在代码块中） 中，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="6bf8c-166">此示例中是类似于前面的教程，提取和显示数据中使用的代码。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="6bf8c-167">开头的行`db =`此时会打开数据库，如前面一样，和下一步的行定义 SQL 语句，再次为您之前看到的一样。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="6bf8c-168">但是，这次它定义 SQL`Insert Into`语句。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="6bf8c-169">下面的示例演示的常规语法`Insert Into`语句：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="6bf8c-170">换而言之，你指定的表将插入，然后列出的列将插入，并列出要插入的值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="6bf8c-171">（如前面提到的 SQL 不区分大小写，但有些人首字母大写要更加轻松地阅读命令的关键字。）</span><span class="sxs-lookup"><span data-stu-id="6bf8c-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="6bf8c-172">在命令中将已列出中的插入的列 — `(Title, Genre, Year)`。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="6bf8c-173">有趣的部分是如何从到文本框中获取值`VALUES`命令的一部分。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="6bf8c-174">而不是实际值，请参阅`@0`， `@1`，和`@2`，这当然是占位符。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="6bf8c-175">运行命令时 (在`db.Execute`行)，传递从文本框中获取的值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="6bf8c-176">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="6bf8c-176">**Important!**</span></span> <span data-ttu-id="6bf8c-177">请记住，您应包含输入的 SQL 语句中的用户的联机数据的唯一方法是使用占位符，如下所示 (`VALUES(@0, @1, @2)`)。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="6bf8c-178">如果连接到 SQL 语句中的用户输入，则打开自己容易受到 SQL 注入攻击，如中所述[窗体基础知识在 ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) （上一个教程）。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="6bf8c-179">仍内`if`块中，添加以下行后的`db.Execute`行：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="6bf8c-180">新电影已插入到数据库后，此行将跳转 （重定向） 到*电影*页，以便您可以看到刚才输入的电影。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="6bf8c-181">`~`运算符表示"root 的网站。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="6bf8c-182">(`~`运算符只能在 ASP.NET 页中，不在 HTML 中通常运行。)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="6bf8c-183">完整的代码块如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="6bf8c-184">测试插入命令 （到目前为止）</span><span class="sxs-lookup"><span data-stu-id="6bf8c-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="6bf8c-185">您还未完成，但现在是测试的好时机。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="6bf8c-186">在 WebMatrix 中的文件树视图中，右键单击*AddMovie.cshtml*页，然后单击**浏览器中启动**。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![在浏览器中添加电影页](entering-data/_static/image2.png)

<span data-ttu-id="6bf8c-188">(如果您最终在浏览器中的其他页，请确保该 URL 是否`http://localhost:nnnnn/AddMovie`)，其中*nnnnn*是正在使用的端口号。)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="6bf8c-189">遇到一个错误页面吗？</span><span class="sxs-lookup"><span data-stu-id="6bf8c-189">Did you get an error page?</span></span> <span data-ttu-id="6bf8c-190">如果是这样，请仔细阅读，并确保，代码看上去完全什么已在前面列出。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="6bf8c-191">在表单中输入电影&mdash;例如，使用"公民 Kane"、"剧本"和"1941"。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="6bf8c-192">（或任何内容。）然后单击**添加电影**。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="6bf8c-193">如果一切顺利，将重定向到*电影*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="6bf8c-194">请确保新电影已列出。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-194">Make sure that your new movie is listed.</span></span>

![显示新电影页面添加电影](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="6bf8c-196">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="6bf8c-196">Validating User Input</span></span>

<span data-ttu-id="6bf8c-197">返回到*AddMovie*页上，或再次运行。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="6bf8c-198">输入另一个 movie，但这次，输入仅标题&mdash;例如，输入"上线 ' 中 Rain"。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="6bf8c-199">然后单击**添加电影**。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="6bf8c-200">将重定向到*电影*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="6bf8c-201">您可以找到新电影，但不完整。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-201">You can find the new movie, but it's incomplete.</span></span>

![电影页上显示缺少某些值的新电影](entering-data/_static/image4.png)

<span data-ttu-id="6bf8c-203">在创建时*电影*表中，你显式所说的任何字段可以为 null。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="6bf8c-204">在此有新电影的输入窗体和要将字段留空。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="6bf8c-205">这是一个错误。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-205">That's an error.</span></span>

<span data-ttu-id="6bf8c-206">在这种情况下，数据库没有实际引发 (或*引发*) 错误。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="6bf8c-207">不能因此提供流派或两年中的代码*AddMovie*页被作为所谓处理这些值*空字符串*。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="6bf8c-208">当 SQL`Insert Into`运行命令、 流派和年份字段中，没有有用的数据，但它们并不为 null。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="6bf8c-209">显然，您不想让用户输入到数据库中每半空电影信息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="6bf8c-210">解决方案是验证用户的输入。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="6bf8c-211">最初，验证将只需确保用户具有的所有字段中都输入的值 （也就是说，该其中任何一个包含空字符串）。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP]
> 
> <span data-ttu-id="6bf8c-212">**Null 和空字符串**</span><span class="sxs-lookup"><span data-stu-id="6bf8c-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="6bf8c-213">在编程中，是区分不同的"空值。"概念</span><span class="sxs-lookup"><span data-stu-id="6bf8c-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="6bf8c-214">一般情况下，当值*null*如果它永远不会设置或已以任何方式初始化。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="6bf8c-215">与此相反，需要字符数据 （字符串） 的变量可以设置为*空字符串*。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="6bf8c-216">在这种情况下，值不是 null。它只是已显式设置为其长度为零的字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="6bf8c-217">这两个语句显示的差异：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="6bf8c-218">它具有更复杂一些，但重要的一点是`null`表示一种不确定状态。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="6bf8c-219">现在，然后务必了解完全值为 null 时，只是空字符串时。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="6bf8c-220">中的代码*AddMovie*页中，您通过使用获取的值的文本框`Request.Form["title"]`，依此类推。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="6bf8c-221">当页面第一次运行 （在您单击的按钮） 之前，值`Request.Form["title"]`为 null。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="6bf8c-222">当您提交窗体，但是`Request.Form["title"]`获取的值`title`文本框。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="6bf8c-223">它不是显而易见的但一个空文本框不为 null;它只是在其中具有空字符串。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="6bf8c-224">因此在代码运行以响应该按钮时单击，`Request.Form["title"]`中有一个空字符串。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="6bf8c-225">为什么这一区别很重要？</span><span class="sxs-lookup"><span data-stu-id="6bf8c-225">Why is this distinction important?</span></span> <span data-ttu-id="6bf8c-226">在创建时*电影*表中，你显式所说的任何字段可以为 null。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="6bf8c-227">在此有新电影的输入窗体，但要将字段留空。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="6bf8c-228">合理地预期要抱怨尝试保存新影片，但没有流派或年份的值时的数据库。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="6bf8c-229">但关键在于&mdash;即使将这些文本框留空，值不为 null; 它们是空字符串。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="6bf8c-230">因此，您可以将新电影保存到具有这些列空数据库&mdash;但不是为 null ！</span><span class="sxs-lookup"><span data-stu-id="6bf8c-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="6bf8c-231">&mdash; 值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-231">&mdash; values.</span></span> <span data-ttu-id="6bf8c-232">因此，您必须确保用户不提交空字符串，可以通过验证用户的输入来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>


### <a name="the-validation-helper"></a><span data-ttu-id="6bf8c-233">验证帮助程序</span><span class="sxs-lookup"><span data-stu-id="6bf8c-233">The Validation Helper</span></span>

<span data-ttu-id="6bf8c-234">ASP.NET Web 页面包括一个帮助程序&mdash;`Validation`帮助器&mdash;可用于确保用户输入符合你要求的数据。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="6bf8c-235">`Validation`帮助器是一个内置到 ASP.NET Web Pages 中，因此无需将其作为安装包使用 NuGet，在前面的教程安装 Gravatar 帮助程序的方式的帮助器。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="6bf8c-236">若要验证用户的输入，将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="6bf8c-237">使用代码来指定你希望要求页面上的文本框中的值。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="6bf8c-238">代码中插入一个测试，以便仅当所有内容正确验证，电影信息添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="6bf8c-239">将代码添加到标记以显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="6bf8c-240">在中的代码块*AddMovie*页上，向右向上变量声明前，顶部添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="6bf8c-241">在调用`Validation.RequireField`一次针对每个字段 (`<input>`元素) 想要要求一个条目。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="6bf8c-242">此外可以添加的自定义错误消息的每个调用，如所示。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="6bf8c-243">（我们不同的消息只是为了说明，可以将您喜欢的任何那里）。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="6bf8c-244">如果没有问题，你想要防止新电影信息插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="6bf8c-245">在中`if(IsPost)`块中，使用`&&`（逻辑与） 添加另一个条件，它测试`Validation.IsValid()`。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="6bf8c-246">完成后，整个`if(IsPost)`块代码所示：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="6bf8c-247">如果没有任何使用注册的字段的验证错误`Validation`帮助器，`Validation.IsValid`方法返回 false。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="6bf8c-248">而这种情况下，在该块中的代码都不会运行，因此任何无效的电影条目将不插入到数据库。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="6bf8c-249">当然您在不重定向到*电影*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="6bf8c-250">完整的代码块，包括验证代码，现在看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="6bf8c-251">显示验证错误</span><span class="sxs-lookup"><span data-stu-id="6bf8c-251">Displaying Validation Errors</span></span>

<span data-ttu-id="6bf8c-252">最后一步是要显示任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-252">The last step is to display any error messages.</span></span> <span data-ttu-id="6bf8c-253">可以显示各个消息的每个验证错误时，也可以显示和 / 或摘要。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="6bf8c-254">对于本教程，您将执行这两，以便您可以看到其工作原理。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="6bf8c-255">每旁边`<input>`要验证的元素，请调用`Html.ValidationMessage`方法并将其传递的名称`<input>`你在验证的元素。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="6bf8c-256">您将放`Html.ValidationMessage`方法右想要显示的错误消息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="6bf8c-257">当该页运行时，则`Html.ValidationMessage`方法还呈现`<span>`会验证错误的元素。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="6bf8c-258">(如果没有错误，`<span>`元素呈现，但其中没有任何文本。)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="6bf8c-259">更改页面中的标记，以便它包含`Html.ValidationMessage`方法的三个`<input>`元素在页面上，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="6bf8c-260">若要查看摘要的工作原理，还添加以下标记和代码之后`<h1>Add a Movie</h1>`页面上的元素：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="6bf8c-261">默认情况下`Html.ValidationSummary`方法以列表形式显示所有验证消息 (`<ul>`内元素`<div>`元素)。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="6bf8c-262">与使用`Html.ValidationMessage`方法，始终呈现验证摘要的标记; 如果没有任何错误，没有列表项呈现。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="6bf8c-263">摘要可以是一种方法来显示验证消息，而不是通过使用`Html.ValidationMessage`方法来显示每个特定于字段的错误。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="6bf8c-264">或者，可以使用摘要和详细信息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="6bf8c-265">也可以使用`Html.ValidationSummary`方法以显示一般错误，然后使用单个`Html.ValidationMessage`调用以显示详细信息。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="6bf8c-266">完成页现在看起来如下例所示：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="6bf8c-267">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-267">That's it.</span></span> <span data-ttu-id="6bf8c-268">现在可以通过添加电影，但是省去一个或多个字段来测试页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="6bf8c-269">执行操作时，您将看到显示了以下错误：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-269">When you do, you see the following error display:</span></span>

![添加电影页面，其中显示验证错误消息](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="6bf8c-271">设置验证错误消息的样式</span><span class="sxs-lookup"><span data-stu-id="6bf8c-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="6bf8c-272">您可以看到的错误消息，但它们不真正与众不同很好。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="6bf8c-273">没有错误消息，但设置样式的简单方法。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="6bf8c-274">通过显示的单个错误消息的样式`Html.ValidationMessage`，创建一个名为的 CSS 样式类`field-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="6bf8c-275">若要定义验证摘要的外观，请创建一个名为的 CSS 样式类`validation-summary-errors`。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="6bf8c-276">若要查看此技术的工作原理，请添加`<style>`元素内的`<head>`页部分。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="6bf8c-277">然后定义名为的样式类`field-validation-error`和`validation-summary-errors`包含以下规则：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="6bf8c-278">通常情况下您可能会将放到单独的样式信息 *.css*文件，但为简单起见，可以将其放在页面现在。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="6bf8c-279">(稍后在本教程系列中将移动到一个单独的 CSS 规则 *.css*文件。)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="6bf8c-280">如果没有验证错误时，`Html.ValidationMessage`方法还呈现`<span>`元素包含`class="field-validation-error"`。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="6bf8c-281">通过添加该类的样式定义，可以配置消息如下所示。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="6bf8c-282">如果有错误，`ValidationSummary`方法将同样动态呈现属性`class="validation-summary-errors"`。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="6bf8c-283">再次运行该页并有意遗漏了几个字段。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="6bf8c-284">错误现更明显。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-284">The errors are now more noticeable.</span></span> <span data-ttu-id="6bf8c-285">（事实上，它们过度，但这是只是为了说明可以执行的操作。）</span><span class="sxs-lookup"><span data-stu-id="6bf8c-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![添加电影页面，其中显示已设置样式的验证错误](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="6bf8c-287">将链接添加到电影页面</span><span class="sxs-lookup"><span data-stu-id="6bf8c-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="6bf8c-288">最后一步是使其可以方便地到达*AddMovie*页上从原始的电影列表。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="6bf8c-289">打开*电影*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-289">Open the *Movies* page again.</span></span> <span data-ttu-id="6bf8c-290">关闭之后`</div>`标记后面`WebGrid`帮助器，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="6bf8c-291">正如您看到之前，ASP.NET 将解释`~`运算符用作在网站的根目录。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="6bf8c-292">无需使用`~`运算符; 您可以使用标记`<a href="./AddMovie">Add a movie</a>`或通过其他方式来定义 HTML 能够理解的路径。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="6bf8c-293">但`~`运算符是一个好常规方法时创建链接，了解 Razor 页面，因为它使站点更灵活，如果当前页移动到子文件夹时，该链接将仍请转到*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="6bf8c-294">(请记住，`~`运算符仅适用于 *.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="6bf8c-295">ASP.NET 理解它，但它不是标准 HTML）。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="6bf8c-296">完成后，运行*电影*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="6bf8c-297">它将类似此页：</span><span class="sxs-lookup"><span data-stu-id="6bf8c-297">It will look like this page:</span></span>

![电影页面，其中包含指向添加电影页](entering-data/_static/image7.png)

<span data-ttu-id="6bf8c-299">单击**添加电影**链接，以确保它进入*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="6bf8c-300">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="6bf8c-300">Coming Up Next</span></span>

<span data-ttu-id="6bf8c-301">在下一步的教程中，您将了解如何让用户编辑已在数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="6bf8c-302">AddMovie 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="6bf8c-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="6bf8c-303">其他资源</span><span class="sxs-lookup"><span data-stu-id="6bf8c-303">Additional Resources</span></span>

- [<span data-ttu-id="6bf8c-304">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="6bf8c-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="6bf8c-305">[INTO 语句中插入的 SQL](http://www.w3schools.com/sql/sql_insert.asp) W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="6bf8c-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="6bf8c-306">[验证用户输入在 ASP.NET Web Pages 站点](https://go.microsoft.com/fwlink/?LinkId=253002)。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="6bf8c-307">详细了解如何使用`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="6bf8c-307">More information about working with the `Validation` helper.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6bf8c-308">[上一页](form-basics.md)
> [下一页](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="6bf8c-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
