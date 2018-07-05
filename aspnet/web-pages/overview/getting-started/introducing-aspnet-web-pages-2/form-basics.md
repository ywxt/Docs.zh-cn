---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: 介绍 ASP.NET 网页的 HTML 窗体基础知识 |Microsoft Docs
author: tfitzmac
description: 本教程演示如何创建输入窗体以及如何处理用户的输入时使用 ASP.NET Web Pages (Razor) 的基础知识。 和现在，您...
ms.author: aspnetcontent
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: 609c1c06ed8f29db82b5dd565a935440d4430819
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37815390"
---
<a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="48065-104">介绍 ASP.NET 网页的 HTML 窗体基础知识</span><span class="sxs-lookup"><span data-stu-id="48065-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>
====================
<span data-ttu-id="48065-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="48065-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="48065-106">本教程演示如何创建输入窗体以及如何处理用户的输入时使用 ASP.NET Web Pages (Razor) 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="48065-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="48065-107">和现在，您有一个数据库，将使用您的窗体技能以使用户可以在数据库中查找特定电影。</span><span class="sxs-lookup"><span data-stu-id="48065-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="48065-108">它假定你已完成通过时序[简介到显示数据使用 ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。</span><span class="sxs-lookup"><span data-stu-id="48065-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="48065-109">你将学习：</span><span class="sxs-lookup"><span data-stu-id="48065-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="48065-110">如何通过使用标准 HTML 元素创建的窗体。</span><span class="sxs-lookup"><span data-stu-id="48065-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="48065-111">如何读取用户的输入窗体中。</span><span class="sxs-lookup"><span data-stu-id="48065-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="48065-112">如何创建 SQL 查询，有选择地获取数据使用的搜索词的用户提供。</span><span class="sxs-lookup"><span data-stu-id="48065-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="48065-113">如何在页中"记住"用户输入的字段。</span><span class="sxs-lookup"><span data-stu-id="48065-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="48065-114">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="48065-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="48065-115">`Request` 对象。</span><span class="sxs-lookup"><span data-stu-id="48065-115">The `Request` object.</span></span>
> - <span data-ttu-id="48065-116">SQL`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="48065-116">The SQL `Where` clause.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="48065-117">你将生成</span><span class="sxs-lookup"><span data-stu-id="48065-117">What You'll Build</span></span>

<span data-ttu-id="48065-118">在上一教程中，创建了一个数据库、 数据添加到它，然后使用`WebGrid`帮助器以显示数据。</span><span class="sxs-lookup"><span data-stu-id="48065-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="48065-119">在本教程中，将添加搜索框中，可以查找特定流派的电影或其标题包含您输入的任何单词。</span><span class="sxs-lookup"><span data-stu-id="48065-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="48065-120">（例如，你将能够找到所有电影流派"操作"或其标题包含"Harry"Adventure"。）</span><span class="sxs-lookup"><span data-stu-id="48065-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="48065-121">完成本教程后，将会得到类似此页：</span><span class="sxs-lookup"><span data-stu-id="48065-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![电影流派和标题搜索页](form-basics/_static/image1.png)

<span data-ttu-id="48065-123">页的列表部分是与最后一个教程中的相同&mdash;网格。</span><span class="sxs-lookup"><span data-stu-id="48065-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="48065-124">区别是，网格将显示仅电影的搜索。</span><span class="sxs-lookup"><span data-stu-id="48065-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="48065-125">有关 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="48065-125">About HTML Forms</span></span>

<span data-ttu-id="48065-126">(如果您有体验与创建 HTML 窗体和之间的差异`GET`和`POST`，可以跳过此部分。)</span><span class="sxs-lookup"><span data-stu-id="48065-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="48065-127">窗体上有用户输入的元素&mdash;文本框、 按钮、 单选按钮、 复选框、 下拉列表和等等。</span><span class="sxs-lookup"><span data-stu-id="48065-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="48065-128">用户填写这些控件或进行选择，然后通过单击按钮提交窗体。</span><span class="sxs-lookup"><span data-stu-id="48065-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="48065-129">此示例中的窗体的基本 HTML 语法进行了说明：</span><span class="sxs-lookup"><span data-stu-id="48065-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="48065-130">在页中运行此标记，将创建如图所示的简单窗体：</span><span class="sxs-lookup"><span data-stu-id="48065-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![作为在浏览器中呈现的基本 HTML 窗体](form-basics/_static/image2.png)

<span data-ttu-id="48065-132">`<form>`元素包含要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="48065-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="48065-133">(若要使易犯错误是将元素添加到页面，但然后忘了将它们放`<form>`元素。</span><span class="sxs-lookup"><span data-stu-id="48065-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="48065-134">在这种情况下，执行任何操作提交。）`method`属性告知浏览器如何提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="48065-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="48065-135">将其设置为`post`如果要执行的更新服务器上或`get`如果只从服务器提取数据。</span><span class="sxs-lookup"><span data-stu-id="48065-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="48065-136">**GET、 POST 和 HTTP 谓词安全**</span><span class="sxs-lookup"><span data-stu-id="48065-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="48065-137">HTTP，浏览器和服务器交换信息，而使用的协议是在其基本操作非常简单。</span><span class="sxs-lookup"><span data-stu-id="48065-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="48065-138">浏览器中使用只有几个谓词向服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="48065-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="48065-139">在编写 web 的代码，是有助于您了解这些谓词和如何在浏览器和服务器使用它们。</span><span class="sxs-lookup"><span data-stu-id="48065-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="48065-140">无疑最常使用的谓词是：</span><span class="sxs-lookup"><span data-stu-id="48065-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="48065-141">`GET`。</span><span class="sxs-lookup"><span data-stu-id="48065-141">`GET`.</span></span> <span data-ttu-id="48065-142">浏览器使用此谓词以从服务器提取的内容。</span><span class="sxs-lookup"><span data-stu-id="48065-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="48065-143">例如，当浏览器中键入 URL，浏览器执行`GET`操作来请求所需的页面。</span><span class="sxs-lookup"><span data-stu-id="48065-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="48065-144">如果页中包含图形，浏览器执行其他`GET`操作来获取映像。</span><span class="sxs-lookup"><span data-stu-id="48065-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="48065-145">如果`GET`操作必须将信息发送到服务器，作为查询字符串中的 URL 的一部分传递的信息。</span><span class="sxs-lookup"><span data-stu-id="48065-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="48065-146">`POST`。</span><span class="sxs-lookup"><span data-stu-id="48065-146">`POST`.</span></span> <span data-ttu-id="48065-147">浏览器发送`POST`请求，以便将数据要添加或更改服务器上提交。</span><span class="sxs-lookup"><span data-stu-id="48065-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="48065-148">例如，`POST`谓词用于在数据库中创建记录或更改现有的。</span><span class="sxs-lookup"><span data-stu-id="48065-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="48065-149">大多数情况下，如果窗体中填写，单击提交按钮，浏览器执行`POST`操作。</span><span class="sxs-lookup"><span data-stu-id="48065-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="48065-150">在`POST`操作中，传递给服务器的数据是在页的正文中。</span><span class="sxs-lookup"><span data-stu-id="48065-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="48065-151">这些动词之间的重要区别在于`GET`操作不应在服务器上进行任何更改，或将其放在更抽象的方式，`GET`操作不会导致在服务器上的状态的更改。</span><span class="sxs-lookup"><span data-stu-id="48065-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="48065-152">你可以执行`GET`无数次，您喜欢，也不会更改这些资源的同一资源上的操作。</span><span class="sxs-lookup"><span data-stu-id="48065-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="48065-153">(A`GET`为"安全，"或使用技术术语，常说操作是*幂等*。)与之相反，当然，`POST`请求更改了某些内容在服务器上每次执行该操作。</span><span class="sxs-lookup"><span data-stu-id="48065-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="48065-154">两个示例将帮助说明这一区别。</span><span class="sxs-lookup"><span data-stu-id="48065-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="48065-155">执行搜索时使用必应或 Google 等引擎包含一个文本框中，窗体中填充，然后单击搜索按钮。</span><span class="sxs-lookup"><span data-stu-id="48065-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="48065-156">浏览器执行`GET`操作，与作为 URL 的一部分传递在框中输入的值。</span><span class="sxs-lookup"><span data-stu-id="48065-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="48065-157">使用`GET`操作此类型的窗体是没问题，因为搜索操作不会更改服务器上的任何资源，只需提取信息。</span><span class="sxs-lookup"><span data-stu-id="48065-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="48065-158">现在，考虑排序某些在线内容的过程。</span><span class="sxs-lookup"><span data-stu-id="48065-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="48065-159">您填写订单详细信息，然后单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="48065-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="48065-160">此操作将为`POST`请求，因为该操作将导致在服务器上，如新的订单记录、 你的帐户信息中的更改和可能是许多其他更改的更改。</span><span class="sxs-lookup"><span data-stu-id="48065-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="48065-161">与不同`GET`操作，不能重复你`POST`请求 — 如果您这样做，重新提交请求，每次会生成服务器上的新订单。</span><span class="sxs-lookup"><span data-stu-id="48065-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="48065-162">（在这种情况下，网站通常会警告你不要超过一次单击提交按钮或将禁用提交按钮，以便不会意外地重新提交该窗体。）</span><span class="sxs-lookup"><span data-stu-id="48065-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="48065-163">在本教程的过程中将使用这两`GET`操作和一个`POST`操作以处理 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="48065-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="48065-164">我们将介绍在每个事例的原因你使用的谓词是一个合适。</span><span class="sxs-lookup"><span data-stu-id="48065-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="48065-165">(若要了解有关 HTTP 谓词的详细信息，请参阅[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 网站上的文章。)</span><span class="sxs-lookup"><span data-stu-id="48065-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>


<span data-ttu-id="48065-166">大多数用户输入的元素以 HTML 为`<input>`元素。</span><span class="sxs-lookup"><span data-stu-id="48065-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="48065-167">它们看起来像`<input type="type" name="name">,`其中*类型*指示所需的用户输入控件的类型。</span><span class="sxs-lookup"><span data-stu-id="48065-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="48065-168">这些元素是常见的：</span><span class="sxs-lookup"><span data-stu-id="48065-168">These elements are the common ones:</span></span>

- <span data-ttu-id="48065-169">文本框中： `<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="48065-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="48065-170">复选框： `<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="48065-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="48065-171">单选按钮： `<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="48065-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="48065-172">按钮： `<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="48065-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="48065-173">提交按钮： `<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="48065-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="48065-174">此外可以使用`<textarea>`元素以创建多行文本框和`<select>`元素来创建一个下拉列表或可滚动的列表。</span><span class="sxs-lookup"><span data-stu-id="48065-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="48065-175">(有关更多关于 HTML 窗体中的元素，请参阅[HTML 窗体和输入](http://www.w3schools.com/html/html_forms.asp)W3Schools 站点上。)</span><span class="sxs-lookup"><span data-stu-id="48065-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="48065-176">`name`属性是非常重要，因为该名称是如何将获取更高版本，该元素的值如稍后您将看到。</span><span class="sxs-lookup"><span data-stu-id="48065-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="48065-177">有趣的是你做些什么，页面开发人员，用户的输入。</span><span class="sxs-lookup"><span data-stu-id="48065-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="48065-178">没有与这些元素相关联的任何内置行为。</span><span class="sxs-lookup"><span data-stu-id="48065-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="48065-179">相反，您必须获取用户输入或选择的值并使用它们执行某些操作。</span><span class="sxs-lookup"><span data-stu-id="48065-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="48065-180">这就是将在本教程中了解的内容。</span><span class="sxs-lookup"><span data-stu-id="48065-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="48065-181">**HTML5 和输入窗体**</span><span class="sxs-lookup"><span data-stu-id="48065-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="48065-182">您可能知道，HTML 处于过渡状态，最新版本 (HTML5) 包括对更直观的方式将用户输入信息的支持。</span><span class="sxs-lookup"><span data-stu-id="48065-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="48065-183">例如，html5，您 （页面开发人员） 可以告诉页面所需用户输入日期。</span><span class="sxs-lookup"><span data-stu-id="48065-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="48065-184">然后可以自动显示在浏览器，日历，而不是要求用户手动输入日期。</span><span class="sxs-lookup"><span data-stu-id="48065-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="48065-185">但是，HTML5 新，尚不支持在所有浏览器中。</span><span class="sxs-lookup"><span data-stu-id="48065-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="48065-186">ASP.NET Web Pages 支持 HTML5 输入的范围内用户的浏览器 does。</span><span class="sxs-lookup"><span data-stu-id="48065-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="48065-187">新特性的了解`<input>`元素中 HTML5，请参阅[HTML&lt;输入&gt;键入属性](http://www.w3schools.com/html/html_form_input_types.asp)W3Schools 站点上。</span><span class="sxs-lookup"><span data-stu-id="48065-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>


## <a name="creating-the-form"></a><span data-ttu-id="48065-188">创建窗体</span><span class="sxs-lookup"><span data-stu-id="48065-188">Creating the Form</span></span>

<span data-ttu-id="48065-189">在 WebMatrix 中，在**文件**工作区中，打开*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="48065-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="48065-190">关闭之后`</h1>`标记并打开之前`<div>`标记的`grid.GetHtml`调用中，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="48065-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="48065-191">此标记创建具有一个名为文本框的窗体`searchGenre`和一个提交按钮。</span><span class="sxs-lookup"><span data-stu-id="48065-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="48065-192">文本框并将其提交按钮括在`<form>`元素的`method`属性设置为`get`。</span><span class="sxs-lookup"><span data-stu-id="48065-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="48065-193">(请记住，如果不将文本框中，提交按钮内的`<form>`元素中，单击此按钮时，将提交执行任何操作。)您使用`GET`谓词此处因为您将创建一个窗体的不进行任何更改在服务器上 — 它只需在搜索结果。</span><span class="sxs-lookup"><span data-stu-id="48065-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="48065-194">(在前面的教程，您使用`post`方法，它是如何提交对服务器的更改。</span><span class="sxs-lookup"><span data-stu-id="48065-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="48065-195">您会看到，在下一教程中再次。）</span><span class="sxs-lookup"><span data-stu-id="48065-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="48065-196">运行页。</span><span class="sxs-lookup"><span data-stu-id="48065-196">Run the page.</span></span> <span data-ttu-id="48065-197">尽管尚未定义窗体的任何行为，但您可以看到如下所示：</span><span class="sxs-lookup"><span data-stu-id="48065-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![使用搜索框中的流派的电影页面](form-basics/_static/image3.png)

<span data-ttu-id="48065-199">输入一个值，在文本框中，如"喜剧。"</span><span class="sxs-lookup"><span data-stu-id="48065-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="48065-200">然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="48065-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="48065-201">请注意页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="48065-201">Take note of the URL of the page.</span></span> <span data-ttu-id="48065-202">因为您设置`<form>`元素的`method`属性为`get`，您输入的值现在是类似如下的 URL 中的查询字符串的一部分：</span><span class="sxs-lookup"><span data-stu-id="48065-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="48065-203">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="48065-203">Reading Form Values</span></span>

<span data-ttu-id="48065-204">该页面已包含一些代码，获取数据库数据，并在网格中显示结果。</span><span class="sxs-lookup"><span data-stu-id="48065-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="48065-205">现在您必须添加一些代码来读取文本框中的值，因此你可以运行包含搜索词的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="48065-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="48065-206">因为窗体的方法设置为`get`，可以读取已通过使用如下所示的代码输入到文本框中的值：</span><span class="sxs-lookup"><span data-stu-id="48065-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="48065-207">`Request.QueryString`对象 (`QueryString`的属性`Request`对象) 包含的已提交的一部分的元素值`GET`操作。</span><span class="sxs-lookup"><span data-stu-id="48065-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="48065-208">`Request.QueryString`属性包含*集合*（列表） 的形式提交的值。</span><span class="sxs-lookup"><span data-stu-id="48065-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="48065-209">若要获取任何单个值，指定所需的元素的名称。</span><span class="sxs-lookup"><span data-stu-id="48065-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="48065-210">这就是为什么您必须拥有`name`特性，可以在`<input>`元素 (`searchTerm`) 创建文本框。</span><span class="sxs-lookup"><span data-stu-id="48065-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="48065-211">(有关详细信息`Request`对象，请参阅[侧栏](#BKMK_TheRequestObject)更高版本。)</span><span class="sxs-lookup"><span data-stu-id="48065-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="48065-212">它非常简单，可以读取的文本框中的值。</span><span class="sxs-lookup"><span data-stu-id="48065-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="48065-213">但是，如果用户未输入任何内容，在文本框中，但单击**搜索**不管怎样，可以忽略该单击，因为没有要搜索内容。</span><span class="sxs-lookup"><span data-stu-id="48065-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="48065-214">以下代码是一个示例，演示如何实现这些条件。</span><span class="sxs-lookup"><span data-stu-id="48065-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="48065-215">（无需尚未添加此代码; 稍后将执行该操作。）</span><span class="sxs-lookup"><span data-stu-id="48065-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="48065-216">测试以这种方式分解：</span><span class="sxs-lookup"><span data-stu-id="48065-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="48065-217">获取的值`Request.QueryString["searchGenre"]`，即输入到的值`<input>`名为元素`searchGenre`。</span><span class="sxs-lookup"><span data-stu-id="48065-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="48065-218">了解它是否为空使用`IsEmpty`方法。</span><span class="sxs-lookup"><span data-stu-id="48065-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="48065-219">此方法是确定是否某些内容 （例如，窗体元素） 包含值的标准方法。</span><span class="sxs-lookup"><span data-stu-id="48065-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="48065-220">但实际上，处理仅当它具有*不*为空，因此...</span><span class="sxs-lookup"><span data-stu-id="48065-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="48065-221">添加`!`前的运算符`IsEmpty`测试。</span><span class="sxs-lookup"><span data-stu-id="48065-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="48065-222">(`!`运算符表示逻辑非)。</span><span class="sxs-lookup"><span data-stu-id="48065-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="48065-223">用通俗易懂，整个`if`条件转换为以下：*如果窗体的 searchGenre 元素不为空，然后...*</span><span class="sxs-lookup"><span data-stu-id="48065-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="48065-224">此块创造了用于创建使用搜索词的查询。</span><span class="sxs-lookup"><span data-stu-id="48065-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="48065-225">下一节中，将执行该操作。</span><span class="sxs-lookup"><span data-stu-id="48065-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="48065-226">**请求对象**</span><span class="sxs-lookup"><span data-stu-id="48065-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="48065-227">`Request`对象包含请求或提交页面时浏览器发送到你的应用程序的所有信息。</span><span class="sxs-lookup"><span data-stu-id="48065-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="48065-228">此对象中包含用户提供，例如文本框值或要上载的文件的任何信息。</span><span class="sxs-lookup"><span data-stu-id="48065-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="48065-229">它还包括各种类型的其他信息，例如 cookie、 URL 查询字符串 （如果有） 中的值的页的正在运行的浏览器的用户正在使用，在浏览器中设置的语言的列表类型的文件路径以及更多。</span><span class="sxs-lookup"><span data-stu-id="48065-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="48065-230">`Request`对象是*集合*（列表） 的值。</span><span class="sxs-lookup"><span data-stu-id="48065-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="48065-231">通过指定其名称获取单个值超出集合：</span><span class="sxs-lookup"><span data-stu-id="48065-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="48065-232">`Request`对象实际上公开多个子集。</span><span class="sxs-lookup"><span data-stu-id="48065-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="48065-233">例如：</span><span class="sxs-lookup"><span data-stu-id="48065-233">For example:</span></span>
> 
> - <span data-ttu-id="48065-234">`Request.Form` 直观显示值中的元素内提交`<form>`元素，该请求是否`POST`请求。</span><span class="sxs-lookup"><span data-stu-id="48065-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="48065-235">`Request.QueryString` 在为您提供的值只是 URL 的查询字符串。</span><span class="sxs-lookup"><span data-stu-id="48065-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="48065-236">(如 URL 中`http://mysite/myapp/page?searchGenre=action&page=2`，则`?searchGenre=action&page=2`URL 的部分是查询字符串。)</span><span class="sxs-lookup"><span data-stu-id="48065-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="48065-237">`Request.Cookies` 集合使您可以访问到浏览器发送的 cookie。</span><span class="sxs-lookup"><span data-stu-id="48065-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="48065-238">若要获取一个值，您知道该值是在提交窗体中，可以使用`Request["name"]`。</span><span class="sxs-lookup"><span data-stu-id="48065-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="48065-239">或者，可以使用更具体的版本`Request.Form["name"]`(对于`POST`请求) 或`Request.QueryString["name"]`(对于`GET`请求)。</span><span class="sxs-lookup"><span data-stu-id="48065-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="48065-240">当然*名称*是要获取的项的名称。</span><span class="sxs-lookup"><span data-stu-id="48065-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="48065-241">你想要获取的项的名称必须是要将的集合中唯一的。</span><span class="sxs-lookup"><span data-stu-id="48065-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="48065-242">这就是为什么`Request`对象提供子集喜欢`Request.Form`和`Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="48065-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="48065-243">假设您的页面包含名为的窗体元素`userName`并*还*包含名为 cookie `userName`。</span><span class="sxs-lookup"><span data-stu-id="48065-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="48065-244">如果收到`Request["userName"]`，它是不明确所需的窗体值或 cookie。</span><span class="sxs-lookup"><span data-stu-id="48065-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="48065-245">但是，如果您收到`Request.Form["userName"]`或`Request.Cookie["userName"]`，您要对其显式要获取的值。</span><span class="sxs-lookup"><span data-stu-id="48065-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="48065-246">很好的做法是特定的使用的子集`Request`感兴趣，如`Request.Form`或`Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="48065-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="48065-247">对于要在本教程中创建的简单页面，它可能不会真正带来任何差异。</span><span class="sxs-lookup"><span data-stu-id="48065-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="48065-248">但是，当您创建更复杂的页，使用显式版本`Request.Form`或`Request.QueryString`可以帮助您避免出现问题时的页面包含一个窗体 （或多个窗体），可能出现的 cookie、 查询字符串值等。</span><span class="sxs-lookup"><span data-stu-id="48065-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>


## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="48065-249">使用搜索词创建查询</span><span class="sxs-lookup"><span data-stu-id="48065-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="48065-250">既然您知道如何获取用户输入的搜索词，可以创建使用它的查询。</span><span class="sxs-lookup"><span data-stu-id="48065-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="48065-251">请记住，为获取在数据库之外的所有电影项目，你使用类似于此语句的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="48065-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="48065-252">若要获取仅某些电影，您必须使用包含的查询`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="48065-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="48065-253">此子句允许您设置由查询返回行的条件。</span><span class="sxs-lookup"><span data-stu-id="48065-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="48065-254">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="48065-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="48065-255">基本格式`WHERE column = value`。</span><span class="sxs-lookup"><span data-stu-id="48065-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="48065-256">除了只是可以使用不同的运算符`=`，例如`>`（大于）、 `<` （小于）， `<>` （不等于）、 `<=` （小于或等于）、 等等，具体取决于要查找的内容。</span><span class="sxs-lookup"><span data-stu-id="48065-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="48065-257">如果您想知道，SQL 语句不是区分大小写&mdash;`SELECT`等同于`Select`(或甚至`select`)。</span><span class="sxs-lookup"><span data-stu-id="48065-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="48065-258">但是，人们通常将首字母大写关键字在 SQL 语句中，如`SELECT`和`WHERE`，以使其更易于读取。</span><span class="sxs-lookup"><span data-stu-id="48065-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="48065-259">作为参数传递的搜索词</span><span class="sxs-lookup"><span data-stu-id="48065-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="48065-260">搜索特定流派非常简单 (`WHERE Genre = 'Action'`)，但你想要搜索的用户输入的任何类型。</span><span class="sxs-lookup"><span data-stu-id="48065-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="48065-261">若要执行此操作，创建时为包含值的占位符，若要搜索的 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="48065-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="48065-262">它将类似此命令：</span><span class="sxs-lookup"><span data-stu-id="48065-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="48065-263">占位符是`@`字符后跟零。</span><span class="sxs-lookup"><span data-stu-id="48065-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="48065-264">您可能已经猜到，查询可以包含多个占位符，并将命名为`@0`， `@1`， `@2`，等等。</span><span class="sxs-lookup"><span data-stu-id="48065-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="48065-265">若要设置的查询和实际上将其传递值，您可以使用如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="48065-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="48065-266">此代码是类似于前面已的操作以在网格中显示数据。</span><span class="sxs-lookup"><span data-stu-id="48065-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="48065-267">唯一的区别是：</span><span class="sxs-lookup"><span data-stu-id="48065-267">The only differences are:</span></span>

- <span data-ttu-id="48065-268">查询包含一个占位符 (`WHERE Genre = @0"`)。</span><span class="sxs-lookup"><span data-stu-id="48065-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="48065-269">该查询将放入一个变量 (`selectCommand`); 之前，请直接传递查询`db.Query`方法。</span><span class="sxs-lookup"><span data-stu-id="48065-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="48065-270">当您调用`db.Query`方法，则传递查询和要使用的占位符的值。</span><span class="sxs-lookup"><span data-stu-id="48065-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="48065-271">(如果查询具有多个占位符，会将其传递所有作为单独值的方法。)</span><span class="sxs-lookup"><span data-stu-id="48065-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="48065-272">如果整理所有这些元素，将得到以下代码：</span><span class="sxs-lookup"><span data-stu-id="48065-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="48065-273">**重要提示！**</span><span class="sxs-lookup"><span data-stu-id="48065-273">**Important!**</span></span> <span data-ttu-id="48065-274">使用占位符 (如`@0`) 将值传递给 SQL 命令是*极其重要*的安全。</span><span class="sxs-lookup"><span data-stu-id="48065-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="48065-275">可以看到它，带有占位符变量数据的方法是应构造 SQL 命令的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="48065-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="48065-276">永远不会通过将组合在一起 （连接） 的文字文本和从用户获取的值来构造 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="48065-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="48065-277">连接到 SQL 语句中的用户输入将打开到站点*SQL 注入攻击*，恶意用户提交 hack 数据库页的值。</span><span class="sxs-lookup"><span data-stu-id="48065-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="48065-278">(您可以阅读更多文章中[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 网站。)</span><span class="sxs-lookup"><span data-stu-id="48065-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>


## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="48065-279">使用搜索代码更新电影页面</span><span class="sxs-lookup"><span data-stu-id="48065-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="48065-280">现在可以更新中的代码*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="48065-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="48065-281">若要开始，请将在页面顶部的代码块中的代码替换此代码：</span><span class="sxs-lookup"><span data-stu-id="48065-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="48065-282">此处的差别是您已放置到查询`selectCommand`变量，将传递给`db.Query`更高版本。</span><span class="sxs-lookup"><span data-stu-id="48065-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="48065-283">将放到一个变量中的 SQL 语句，可以更改语句，它将执行哪些操作来执行搜索。</span><span class="sxs-lookup"><span data-stu-id="48065-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="48065-284">您也删除了以下两行，您将放回中更高版本：</span><span class="sxs-lookup"><span data-stu-id="48065-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="48065-285">不想尚未运行查询 (也就是说，调用`db.Query`) 并且不想要初始化`WebGrid`帮助程序，但任何一个。</span><span class="sxs-lookup"><span data-stu-id="48065-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="48065-286">已经想到的 SQL 语句必须运行后，将执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="48065-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="48065-287">此重写块后可以添加用于处理搜索新的逻辑。</span><span class="sxs-lookup"><span data-stu-id="48065-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="48065-288">已完成的代码将如下所示。</span><span class="sxs-lookup"><span data-stu-id="48065-288">The completed code will look like the following.</span></span> <span data-ttu-id="48065-289">使其匹配此示例，请更新您的页面中的代码：</span><span class="sxs-lookup"><span data-stu-id="48065-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="48065-290">页面现在工作方式如下。</span><span class="sxs-lookup"><span data-stu-id="48065-290">The page now works like this.</span></span> <span data-ttu-id="48065-291">每次运行页面时，代码将打开的数据库和`selectCommand`变量设置为获取中的所有记录的 SQL 语句`Movies`表。</span><span class="sxs-lookup"><span data-stu-id="48065-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="48065-292">此代码还初始化`searchTerm`变量。</span><span class="sxs-lookup"><span data-stu-id="48065-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="48065-293">但是，如果当前请求中包含的值`searchGenre`元素，该代码设置`selectCommand`到另一个查询，即为包括`Where`子句来搜索的一种流派。</span><span class="sxs-lookup"><span data-stu-id="48065-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="48065-294">它还将设置`searchTerm`到任何传递的搜索框中 （这可能是执行任何操作）。</span><span class="sxs-lookup"><span data-stu-id="48065-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="48065-295">而不考虑哪些 SQL 语句位于`selectCommand`，然后，代码调用`db.Query`若要运行查询，并向其传递任何位于`searchTerm`。</span><span class="sxs-lookup"><span data-stu-id="48065-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="48065-296">如果中没有任何内容`searchTerm`，它并不重要，因为在这种情况下没有参数传递到值`selectCommand`是否仍要。</span><span class="sxs-lookup"><span data-stu-id="48065-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="48065-297">最后，代码将初始化`WebGrid`帮助器通过使用查询结果中的，像以前一样。</span><span class="sxs-lookup"><span data-stu-id="48065-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="48065-298">可以看到，通过将置于 SQL 语句和搜索词到变量中，你已向代码添加大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="48065-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="48065-299">正如您将看到更高版本在本教程中，您可以使用此基本框架，并继续添加用于不同类型的搜索逻辑。</span><span class="sxs-lookup"><span data-stu-id="48065-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="48065-300">测试按流派搜索功能</span><span class="sxs-lookup"><span data-stu-id="48065-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="48065-301">在 WebMatrix 中，运行*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="48065-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="48065-302">请参阅流派文本框中的页。</span><span class="sxs-lookup"><span data-stu-id="48065-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="48065-303">输入已输入一个你测试的记录，然后单击一种流派**搜索**。</span><span class="sxs-lookup"><span data-stu-id="48065-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="48065-304">此时会显示仅匹配该类型的电影的列表：</span><span class="sxs-lookup"><span data-stu-id="48065-304">This time you see a listing of just the movies that match that genre:</span></span>

![列出搜索流派 Comedies 后的电影页](form-basics/_static/image4.png)

<span data-ttu-id="48065-306">输入不同的流派，然后再次进行搜索。</span><span class="sxs-lookup"><span data-stu-id="48065-306">Enter a different genre and search again.</span></span> <span data-ttu-id="48065-307">请尝试使用所有小写字母或全部大写的字母，以便您可以看到，搜索不区分大小写输入类型。</span><span class="sxs-lookup"><span data-stu-id="48065-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="48065-308">"记住"用户输入的内容</span><span class="sxs-lookup"><span data-stu-id="48065-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="48065-309">您可能已经注意到，之后您输入一种流派，并单击**搜索流派**，看到了该类型的列表。</span><span class="sxs-lookup"><span data-stu-id="48065-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="48065-310">但是，在搜索文本框中为空&mdash;换而言之，它没有记住以前输入的内容。</span><span class="sxs-lookup"><span data-stu-id="48065-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="48065-311">请务必了解为什么会发生此行为。</span><span class="sxs-lookup"><span data-stu-id="48065-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="48065-312">当您提交一个页面时，在浏览器到 web 服务器发送请求。</span><span class="sxs-lookup"><span data-stu-id="48065-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="48065-313">当 ASP.NET 获取请求时，它创建页面的一个全新的实例，在中，运行代码，然后将重新呈现到浏览器页面。</span><span class="sxs-lookup"><span data-stu-id="48065-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="48065-314">实际上，不过，页面并不知道，刚刚使用与自身的以前的版本。</span><span class="sxs-lookup"><span data-stu-id="48065-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="48065-315">所有它知道它有都有一些的请求中它的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="48065-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="48065-316">每次请求页面&mdash;是第一次，还是通过提交它&mdash;可将一个新页面。</span><span class="sxs-lookup"><span data-stu-id="48065-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="48065-317">Web 服务器具有的最后一个请求的任何内存。</span><span class="sxs-lookup"><span data-stu-id="48065-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="48065-318">不能用 ASP.NET 中，也不能用浏览器。</span><span class="sxs-lookup"><span data-stu-id="48065-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="48065-319">页的这些单独的实例之间的唯一连接是它们之间传输任何数据。</span><span class="sxs-lookup"><span data-stu-id="48065-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="48065-320">如果提交的页面，例如，新的页实例可以获取由早期实例发送的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="48065-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="48065-321">（若要在页面之间传递数据的另一种方法是使用 cookie。）</span><span class="sxs-lookup"><span data-stu-id="48065-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="48065-322">正式地说这种情况下是说，web 页中找到*无状态*。</span><span class="sxs-lookup"><span data-stu-id="48065-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="48065-323">Web 服务器和页面本身和页面中的元素不维护有关页面的以前的状态的任何信息。</span><span class="sxs-lookup"><span data-stu-id="48065-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="48065-324">Web 被设计这种方式，因为维护各个请求的状态会快速耗尽资源的 web 服务器，通常可能处理数千个，甚至几十万个情况下，每秒的请求。</span><span class="sxs-lookup"><span data-stu-id="48065-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="48065-325">因此这就是为什么文本框为空。</span><span class="sxs-lookup"><span data-stu-id="48065-325">So that's why the text box was empty.</span></span> <span data-ttu-id="48065-326">提交页面后，ASP.NET 创建的页的新实例，并运行通过代码和标记。</span><span class="sxs-lookup"><span data-stu-id="48065-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="48065-327">执行任何操作中没有告诉 ASP.NET 将值放到文本框中的代码。</span><span class="sxs-lookup"><span data-stu-id="48065-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="48065-328">因此 ASP.NET 不执行任何操作，并在文本框中呈现而无需在其中一个值。</span><span class="sxs-lookup"><span data-stu-id="48065-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="48065-329">没有实际的简单办法解决这个问题。</span><span class="sxs-lookup"><span data-stu-id="48065-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="48065-330">在文本框中输入的流派*是*在代码中使用&mdash;处于`Request.QueryString["searchGenre"]`。</span><span class="sxs-lookup"><span data-stu-id="48065-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="48065-331">更新文本框中的标记，以便`value`属性获取其值从`searchTerm`，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="48065-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="48065-332">在此页中，你也可以还设置`value`属性为`searchTerm`输入变量，因为该变量还包含流派。</span><span class="sxs-lookup"><span data-stu-id="48065-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="48065-333">不过，使用`Request`对象，以设置`value`特性，如此处显示的标准方法来完成此任务。</span><span class="sxs-lookup"><span data-stu-id="48065-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="48065-334">(即使想要执行此操作假定&mdash;在某些情况下，你可能想要呈现的页面*而无需*中字段的值。</span><span class="sxs-lookup"><span data-stu-id="48065-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="48065-335">这完全取决于这怎么回事与你的应用。）</span><span class="sxs-lookup"><span data-stu-id="48065-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="48065-336">您不能"记住"用于密码的文本框中的值。</span><span class="sxs-lookup"><span data-stu-id="48065-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="48065-337">它会让人以填充密码字段中使用代码安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="48065-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>


<span data-ttu-id="48065-338">再次运行此页，输入一种流派，然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="48065-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="48065-339">这一次不只执行你看到的搜索结果，但会记住文本框中，输入上一次：</span><span class="sxs-lookup"><span data-stu-id="48065-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![页面显示，在文本框中具有记住以前的条目](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="48065-341">搜索标题中的任何字词</span><span class="sxs-lookup"><span data-stu-id="48065-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="48065-342">你现在可以搜索任何类型，但可能还想要搜索的标题。</span><span class="sxs-lookup"><span data-stu-id="48065-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="48065-343">很难获取标题完全正确，因此，您可以搜索单词出现在标题内的任意位置搜索时。</span><span class="sxs-lookup"><span data-stu-id="48065-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="48065-344">若要在 SQL 中执行的操作，应使用`LIKE`运算符和语法如下所示：</span><span class="sxs-lookup"><span data-stu-id="48065-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="48065-345">此命令将获取其标题包含"adventure"的所有电影。</span><span class="sxs-lookup"><span data-stu-id="48065-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="48065-346">当你使用`LIKE`运算符，包括通配符字符`%`作为搜索词的一部分。</span><span class="sxs-lookup"><span data-stu-id="48065-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="48065-347">搜索`LIKE 'adventure%'`意味着"开头 'adventure'"。</span><span class="sxs-lookup"><span data-stu-id="48065-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="48065-348">（从技术上讲，这意味着"字符串 'adventure' 跟任何内容。）同样，搜索词`LIKE '%adventure'`表示"任何内容后面是字符串 'adventure'"，这是另一种方法可以说"与 adventure 结束"。</span><span class="sxs-lookup"><span data-stu-id="48065-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="48065-349">搜索词`LIKE '%adventure%'`因此意味着"使用"adventure' 标题中的任意位置。"</span><span class="sxs-lookup"><span data-stu-id="48065-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="48065-350">（从技术上讲，"中的任何内容的标题后, 跟 'adventure'，跟任何内容。"）</span><span class="sxs-lookup"><span data-stu-id="48065-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="48065-351">内部`<form>`元素中，添加以下标记下右`</div>`流派搜索的标记 (只需在关闭前`</form>`元素):</span><span class="sxs-lookup"><span data-stu-id="48065-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="48065-352">代码来处理此搜索是类似于流派搜索代码，只不过你必须以组合`LIKE`搜索。</span><span class="sxs-lookup"><span data-stu-id="48065-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="48065-353">在代码块中的页的顶部，添加以下`if`之后阻止`if`流派搜索的块：</span><span class="sxs-lookup"><span data-stu-id="48065-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="48065-354">此代码使用更早版本，看到的相同逻辑，只搜索使用`LIKE`运算符，代码会使"`%`"之前和之后的搜索词。</span><span class="sxs-lookup"><span data-stu-id="48065-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="48065-355">请注意如何很容易就可以将另一个搜索添加到页。</span><span class="sxs-lookup"><span data-stu-id="48065-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="48065-356">您所要做的一切是：</span><span class="sxs-lookup"><span data-stu-id="48065-356">All you had to do was:</span></span>

- <span data-ttu-id="48065-357">创建`if`进行测试，查看相关的搜索框中是否具有值的块。</span><span class="sxs-lookup"><span data-stu-id="48065-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="48065-358">设置`selectCommand`变量到新的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="48065-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="48065-359">设置`searchTerm`变量指向要传递给查询的值。</span><span class="sxs-lookup"><span data-stu-id="48065-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="48065-360">下面是完整的代码块，其中包含标题搜索的新逻辑：</span><span class="sxs-lookup"><span data-stu-id="48065-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="48065-361">下面是此代码的作用的摘要：</span><span class="sxs-lookup"><span data-stu-id="48065-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="48065-362">变量`searchTerm`和`selectCommand`顶部初始化。</span><span class="sxs-lookup"><span data-stu-id="48065-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="48065-363">用户执行的页中根据相应的 SQL 命令和想要将这些变量设置为相应的搜索词 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="48065-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="48065-364">默认搜索是从数据库中获取所有电影的简单情况。</span><span class="sxs-lookup"><span data-stu-id="48065-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="48065-365">中的测试`searchGenre`并`searchTitle`，该代码设置`searchTerm`你想要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="48065-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="48065-366">这些代码块还设置`selectCommand`对该搜索的相应 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="48065-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="48065-367">`db.Query`方法使用任何 SQL 命令在只有一次调用`selectedCommand`并且任何值在`searchTerm`。</span><span class="sxs-lookup"><span data-stu-id="48065-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="48065-368">如果没有搜索词 （没有流派和没有标题 word） 的值`searchTerm`为空字符串。</span><span class="sxs-lookup"><span data-stu-id="48065-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="48065-369">但是，，并不重要，因为在这种情况下，查询不需要参数。</span><span class="sxs-lookup"><span data-stu-id="48065-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="48065-370">测试标题搜索功能</span><span class="sxs-lookup"><span data-stu-id="48065-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="48065-371">现在，你可以测试已完成的搜索页。</span><span class="sxs-lookup"><span data-stu-id="48065-371">Now you can test your completed search page.</span></span> <span data-ttu-id="48065-372">运行*Movies.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="48065-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="48065-373">输入一种流派，然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="48065-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="48065-374">网格显示电影的流派，如之前。</span><span class="sxs-lookup"><span data-stu-id="48065-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="48065-375">输入标题 word，然后单击**搜索标题**。</span><span class="sxs-lookup"><span data-stu-id="48065-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="48065-376">网格将显示在标题中包含该单词的电影。</span><span class="sxs-lookup"><span data-stu-id="48065-376">The grid displays movies that have that word in the title.</span></span>

![中搜索标题后列出的电影页](form-basics/_static/image6.png)

<span data-ttu-id="48065-378">将两个文本框留空，然后单击任一按钮。</span><span class="sxs-lookup"><span data-stu-id="48065-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="48065-379">网格显示所有电影。</span><span class="sxs-lookup"><span data-stu-id="48065-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="48065-380">合并查询</span><span class="sxs-lookup"><span data-stu-id="48065-380">Combining the Queries</span></span>

<span data-ttu-id="48065-381">您可能注意到可以执行的搜索，是互斥的。</span><span class="sxs-lookup"><span data-stu-id="48065-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="48065-382">您不能一次搜索的标题和流派即使这两个搜索框中都有值。</span><span class="sxs-lookup"><span data-stu-id="48065-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="48065-383">例如，不能搜索其标题包含"Adventure"的所有操作电影。</span><span class="sxs-lookup"><span data-stu-id="48065-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="48065-384">（如果流派和标题的输入值，现在，编码页面，如标题搜索获取优先顺序。）若要创建组合条件的搜索，您将必须创建具有如下所示的语法的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="48065-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="48065-385">和必须通过使用类似于以下语句来运行查询 （大体而言）：</span><span class="sxs-lookup"><span data-stu-id="48065-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="48065-386">如您所见，创建逻辑，以允许许多排列的搜索条件可以获取有点复杂。</span><span class="sxs-lookup"><span data-stu-id="48065-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="48065-387">因此，我们将就此打住。</span><span class="sxs-lookup"><span data-stu-id="48065-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="48065-388">即将推出下一步</span><span class="sxs-lookup"><span data-stu-id="48065-388">Coming Up Next</span></span>

<span data-ttu-id="48065-389">在下一步的教程中，你将创建使用窗体以使用户可以向数据库添加电影的页。</span><span class="sxs-lookup"><span data-stu-id="48065-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="48065-390">电影页面 （使用搜索更新） 的完整列表</span><span class="sxs-lookup"><span data-stu-id="48065-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="48065-391">其他资源</span><span class="sxs-lookup"><span data-stu-id="48065-391">Additional Resources</span></span>

- [<span data-ttu-id="48065-392">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="48065-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="48065-393">[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="48065-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="48065-394">[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 网站上的文章</span><span class="sxs-lookup"><span data-stu-id="48065-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="48065-395">[上一页](displaying-data.md)
> [下一页](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="48065-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>
