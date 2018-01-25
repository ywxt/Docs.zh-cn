---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: "引入的 ASP.NET Web Pages-HTML 窗体基础知识 |Microsoft 文档"
author: tfitzmac
description: "本教程演示如何创建的输入的窗体以及如何处理用户的输入，当你使用 ASP.NET Web 页 (Razor) 的基础知识。 和现在，您..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: 68056759b2e80230e5fd2c0f9b2d2a89b549cf37
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="introducing-aspnet-web-pages---html-form-basics"></a><span data-ttu-id="f1686-104">引入 ASP.NET Web 页的 HTML 窗体基础知识</span><span class="sxs-lookup"><span data-stu-id="f1686-104">Introducing ASP.NET Web Pages - HTML Form Basics</span></span>
====================
<span data-ttu-id="f1686-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f1686-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f1686-106">本教程演示如何创建的输入的窗体以及如何处理用户的输入，当你使用 ASP.NET Web 页 (Razor) 的基础知识。</span><span class="sxs-lookup"><span data-stu-id="f1686-106">This tutorial shows you the basics of how to create an input form and how to handle the user's input when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="f1686-107">现在，你已收到数据库，你将使用你窗体的技能让用户在数据库中查找特定电影。</span><span class="sxs-lookup"><span data-stu-id="f1686-107">And now that you've got a database, you'll use your form skills to let users find specific movies in the database.</span></span> <span data-ttu-id="f1686-108">它假定你已完成通过系列[简介到显示数据使用的 ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)。</span><span class="sxs-lookup"><span data-stu-id="f1686-108">It assumes you have completed the series through [Introduction to Displaying Data Using ASP.NET Web Pages](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).</span></span>
> 
> <span data-ttu-id="f1686-109">你将学习：</span><span class="sxs-lookup"><span data-stu-id="f1686-109">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f1686-110">如何通过使用标准的 HTML 元素创建的窗体。</span><span class="sxs-lookup"><span data-stu-id="f1686-110">How to create a form by using standard HTML elements.</span></span>
> - <span data-ttu-id="f1686-111">如何读取用户的窗体中输入。</span><span class="sxs-lookup"><span data-stu-id="f1686-111">How to read the user's input in a form.</span></span>
> - <span data-ttu-id="f1686-112">如何创建 SQL 查询，有选择地获取数据使用的搜索词的用户提供。</span><span class="sxs-lookup"><span data-stu-id="f1686-112">How to create a SQL query that selectively gets data by using a search term that the user supplies.</span></span>
> - <span data-ttu-id="f1686-113">如何在页中"记住"用户输入的字段。</span><span class="sxs-lookup"><span data-stu-id="f1686-113">How to have fields in the page "remember" what the user entered.</span></span>
>   
> 
> <span data-ttu-id="f1686-114">功能/技术讨论：</span><span class="sxs-lookup"><span data-stu-id="f1686-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="f1686-115">`Request` 对象。</span><span class="sxs-lookup"><span data-stu-id="f1686-115">The `Request` object.</span></span>
> - <span data-ttu-id="f1686-116">SQL`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="f1686-116">The SQL `Where` clause.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="f1686-117">你将生成</span><span class="sxs-lookup"><span data-stu-id="f1686-117">What You'll Build</span></span>

<span data-ttu-id="f1686-118">在以前的教程中，创建数据库，将数据添加到它，，然后使用`WebGrid`帮助器以显示数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-118">In the previous tutorial, you created a database, added data to it, and then used the `WebGrid` helper to display the data.</span></span> <span data-ttu-id="f1686-119">在本教程中，你将添加一个搜索框，可让你查找的特定风格的影片或其标题中包含你输入任何字符。</span><span class="sxs-lookup"><span data-stu-id="f1686-119">In this tutorial, you'll add a search box that lets you find movies of a specific genre or whose title contains whatever word you enter.</span></span> <span data-ttu-id="f1686-120">（例如，你将能够查找所有电影其风格是"操作"或其标题包含"Harry"Adventure"。）</span><span class="sxs-lookup"><span data-stu-id="f1686-120">(For example, you'll be able to find all movies whose genre is "Action" or whose title contains "Harry" or "Adventure.")</span></span>

<span data-ttu-id="f1686-121">完成本教程后，将会得到如下所示的页面：</span><span class="sxs-lookup"><span data-stu-id="f1686-121">When you're done with this tutorial, you'll have a page like this one:</span></span>

![电影 Genre 和标题搜索页](form-basics/_static/image1.png)

<span data-ttu-id="f1686-123">页的列表部分是与最后一个教程中的相同&mdash;网格。</span><span class="sxs-lookup"><span data-stu-id="f1686-123">The listing part of the page is the same as in the last tutorial &mdash; a grid.</span></span> <span data-ttu-id="f1686-124">将网格将显示仅电影您搜索的差异。</span><span class="sxs-lookup"><span data-stu-id="f1686-124">The difference will be that the grid will show only the movies that you searched for.</span></span>

## <a name="about-html-forms"></a><span data-ttu-id="f1686-125">有关 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="f1686-125">About HTML Forms</span></span>

<span data-ttu-id="f1686-126">(如果你具有与创建 HTML 窗体和之间的差异的体验`GET`和`POST`，则可以跳过此部分。)</span><span class="sxs-lookup"><span data-stu-id="f1686-126">(If you've got experience with creating HTML forms and with the difference between `GET` and `POST`, you can skip this section.)</span></span>

<span data-ttu-id="f1686-127">表单具有用户输入的元素&mdash;文本框、 按钮、 单选按钮、 复选框，下拉列表和等等。</span><span class="sxs-lookup"><span data-stu-id="f1686-127">A form has user input elements &mdash; text boxes, buttons, radio buttons, check boxes, drop-down lists, and so on.</span></span> <span data-ttu-id="f1686-128">用户填写这些控件或进行选择并单击一个按钮，然后提交窗体。</span><span class="sxs-lookup"><span data-stu-id="f1686-128">Users fill in these controls or make selections and then submit the form by clicking a button.</span></span>

<span data-ttu-id="f1686-129">此示例中所示的窗体的基本 HTML 语法：</span><span class="sxs-lookup"><span data-stu-id="f1686-129">The basic HTML syntax of a form is illustrated by this example:</span></span>

[!code-html[Main](form-basics/samples/sample1.html)]

<span data-ttu-id="f1686-130">在页中运行此标记，将创建一个简单窗体看上去像此图中：</span><span class="sxs-lookup"><span data-stu-id="f1686-130">When this markup runs in a page, it creates a simple form that looks like this illustration:</span></span>

![为呈现在浏览器中的基本 HTML 窗体](form-basics/_static/image2.png)

<span data-ttu-id="f1686-132">`<form>`元素包含要提交的 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="f1686-132">The `<form>` element encloses HTML elements to be submitted.</span></span> <span data-ttu-id="f1686-133">(若要使易犯错误是向页面添加元素，但然后忘记将它们放`<form>`元素。</span><span class="sxs-lookup"><span data-stu-id="f1686-133">(An easy mistake to make is to add elements to the page but then forget to put them inside a `<form>` element.</span></span> <span data-ttu-id="f1686-134">在这种情况下，执行任何操作提交。）`method`属性告知浏览器如何提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="f1686-134">In that case, nothing is submitted.) The `method` attribute tells the browser how to submit the user input.</span></span> <span data-ttu-id="f1686-135">将此设置为`post`如果要执行的更新服务器上或`get`如果你只需从服务器提取数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-135">You set this to `post` if you're performing an update on the server or to `get` if you're just fetching data from the server.</span></span>

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> <span data-ttu-id="f1686-136">**GET、 POST 和 HTTP 谓词安全性**</span><span class="sxs-lookup"><span data-stu-id="f1686-136">**GET, POST, and HTTP Verb Safety**</span></span>
> 
> <span data-ttu-id="f1686-137">HTTP，浏览器和服务器使用交换信息，该协议是非常简单的其基本操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-137">HTTP, the protocol that browsers and servers use to exchange information, is remarkably simple in its basic operations.</span></span> <span data-ttu-id="f1686-138">使用仅几个谓词的浏览器以向服务器发出请求。</span><span class="sxs-lookup"><span data-stu-id="f1686-138">Browsers use only a few verbs to make requests to servers.</span></span> <span data-ttu-id="f1686-139">当你编写适用于 web 的代码时，是有助于了解这些谓词和如何在浏览器和服务器使用它们。</span><span class="sxs-lookup"><span data-stu-id="f1686-139">When you write code for the web, it's helpful to understand these verbs and how the browser and server use them.</span></span> <span data-ttu-id="f1686-140">距离遥远的最常使用的谓词是这些：</span><span class="sxs-lookup"><span data-stu-id="f1686-140">Far and away the most commonly used verbs are these:</span></span>
> 
> - <span data-ttu-id="f1686-141">`GET`。</span><span class="sxs-lookup"><span data-stu-id="f1686-141">`GET`.</span></span> <span data-ttu-id="f1686-142">浏览器使用此谓词来从服务器提取的内容。</span><span class="sxs-lookup"><span data-stu-id="f1686-142">The browser uses this verb to fetch something from the server.</span></span> <span data-ttu-id="f1686-143">例如，当你键入 URL 在浏览器，浏览器将执行`GET`操作请求所需的页。</span><span class="sxs-lookup"><span data-stu-id="f1686-143">For example, when you type a URL into your browser, the browser performs a `GET` operation to request the page you want.</span></span> <span data-ttu-id="f1686-144">如果该页面包括图形，浏览器将执行其他`GET`获取映像的操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-144">If the page includes graphics, the browser performs additional `GET` operations to get the images.</span></span> <span data-ttu-id="f1686-145">如果`GET`操作具有要将信息传递给服务器，将信息传递作为查询字符串中的 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="f1686-145">If the `GET` operation has to pass information to the server, the information is passed as part of the URL in the query string.</span></span>
> - <span data-ttu-id="f1686-146">`POST`。</span><span class="sxs-lookup"><span data-stu-id="f1686-146">`POST`.</span></span> <span data-ttu-id="f1686-147">浏览器发送`POST`请求，以便提交要添加或更改服务器上的数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-147">The browser sends a `POST` request in order to submit data to be added or changed on the server.</span></span> <span data-ttu-id="f1686-148">例如，`POST`谓词用于在数据库中创建记录或更改现有的。</span><span class="sxs-lookup"><span data-stu-id="f1686-148">For example, the `POST` verb is used to create records in a database or change existing ones.</span></span> <span data-ttu-id="f1686-149">大多数情况下，当您填写表单，并单击提交按钮，浏览器执行`POST`操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-149">Most of the time, when you fill in a form and click the submit button, the browser performs a `POST` operation.</span></span> <span data-ttu-id="f1686-150">在`POST`操作，正在传递给服务器的数据位于页的正文。</span><span class="sxs-lookup"><span data-stu-id="f1686-150">In a `POST` operation, the data being passed to the server is in the body of the page.</span></span>
> 
> <span data-ttu-id="f1686-151">这些动词之间的一个重要区别在于，`GET`操作不应更改服务器上的任何内容，或将其放在稍微抽象的方式，`GET`操作未导致服务器上的状态的更改。</span><span class="sxs-lookup"><span data-stu-id="f1686-151">An important distinction between these verbs is that a `GET` operation is not supposed to change anything on the server — or to put it in a slightly more abstract way, a `GET` operation does not result in a change in state on the server.</span></span> <span data-ttu-id="f1686-152">你可以执行`GET`多次您喜欢，并且不会更改这些资源的同一资源上的操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-152">You can perform a `GET` operation on the same resources as many times as you like, and those resources don't change.</span></span> <span data-ttu-id="f1686-153">(A`GET`操作通常称为"安全，"或者可以使用技术术语，是*幂等*。)相反，当然，`POST`内容服务器上执行该操作每次时请求更改。</span><span class="sxs-lookup"><span data-stu-id="f1686-153">(A `GET` operation is often said to be "safe," or to use a technical term, is *idempotent*.) In contrast, of course, a `POST` request changes something on the server each time you perform the operation.</span></span>
> 
> <span data-ttu-id="f1686-154">两个示例将帮助阐释这一区别。</span><span class="sxs-lookup"><span data-stu-id="f1686-154">Two examples will help illustrate this distinction.</span></span> <span data-ttu-id="f1686-155">执行搜索时使用的引擎，如必应或 Google，填写包含一个文本框的窗体，然后单击搜索按钮。</span><span class="sxs-lookup"><span data-stu-id="f1686-155">When you perform a search using an engine like Bing or Google, you fill in a form that consists of one text box, and then you click the search button.</span></span> <span data-ttu-id="f1686-156">浏览器执行`GET`操作，作为 URL 的一部分传递在框中输入的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-156">The browser performs a `GET` operation, with the value you entered into the box passed as part of the URL.</span></span> <span data-ttu-id="f1686-157">使用`GET`操作为此类型的窗体不错，因为搜索操作不会更改服务器上的任何资源，它只提取信息。</span><span class="sxs-lookup"><span data-stu-id="f1686-157">Using a `GET` operation for this type of form is fine, because a search operation doesn't change any resources on the server, it just fetches information.</span></span>
> 
> <span data-ttu-id="f1686-158">现在考虑排序联机的内容的过程。</span><span class="sxs-lookup"><span data-stu-id="f1686-158">Now consider the process of ordering something online.</span></span> <span data-ttu-id="f1686-159">你填写订单详细信息，然后单击提交按钮。</span><span class="sxs-lookup"><span data-stu-id="f1686-159">You fill in the order details and then click the submit button.</span></span> <span data-ttu-id="f1686-160">此操作将`POST`请求，因为该操作将导致在服务器上，如新的顺序记录、 你的帐户信息中的更改和可能是许多其他更改的更改。</span><span class="sxs-lookup"><span data-stu-id="f1686-160">This operation will be a `POST` request, because the operation will result in changes on the server, such as a new order record, a change in your account information, and perhaps many other changes.</span></span> <span data-ttu-id="f1686-161">与不同`GET`操作，不能重复你`POST`请求-如果你这样做，重新提交请求，每次会生成服务器上的新订单。</span><span class="sxs-lookup"><span data-stu-id="f1686-161">Unlike the `GET` operation, you cannot repeat your `POST` request — if you did, each time you resubmitted the request, you'd generate a new order on the server.</span></span> <span data-ttu-id="f1686-162">（在这种情况下，网站通常将警告你不要单击提交按钮一次以上，或将禁用提交按钮，以便不会意外地重新提交窗体。）</span><span class="sxs-lookup"><span data-stu-id="f1686-162">(In cases like this, websites will often warn you not to click a submit button more than once, or will disable the submit button so that you don't resubmit the form accidentally.)</span></span>
> 
> <span data-ttu-id="f1686-163">在本教程的过程中你将使用同时`GET`操作和`POST`操作用于 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="f1686-163">In the course of this tutorial, you'll use both a `GET` operation and a `POST` operation to work with HTML forms.</span></span> <span data-ttu-id="f1686-164">我们将介绍在每个事例的原因你使用的谓词是适合的选项。</span><span class="sxs-lookup"><span data-stu-id="f1686-164">We'll explain in each case why the verb you use is the appropriate one.</span></span>
> 
> <span data-ttu-id="f1686-165">(若要了解有关 HTTP 谓词的详细信息，请参阅[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 网站上的文章。)</span><span class="sxs-lookup"><span data-stu-id="f1686-165">(To learn more about HTTP verbs, see the [Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site.)</span></span>


<span data-ttu-id="f1686-166">大多数用户输入的元素为 HTML`<input>`元素。</span><span class="sxs-lookup"><span data-stu-id="f1686-166">Most user input elements are HTML `<input>` elements.</span></span> <span data-ttu-id="f1686-167">它们看起来像`<input type="type" name="name">,`其中*类型*指示所需的用户输入控件的种类。</span><span class="sxs-lookup"><span data-stu-id="f1686-167">They look like `<input type="type" name="name">,` where *type* indicates the kind of user input control you want.</span></span> <span data-ttu-id="f1686-168">这些元素包括的常见事件：</span><span class="sxs-lookup"><span data-stu-id="f1686-168">These elements are the common ones:</span></span>

- <span data-ttu-id="f1686-169">文本框中：`<input type="text">`</span><span class="sxs-lookup"><span data-stu-id="f1686-169">Text box: `<input type="text">`</span></span>
- <span data-ttu-id="f1686-170">复选框：`<input type="check">`</span><span class="sxs-lookup"><span data-stu-id="f1686-170">Check box: `<input type="check">`</span></span>
- <span data-ttu-id="f1686-171">单选按钮：`<input type="radio">`</span><span class="sxs-lookup"><span data-stu-id="f1686-171">Radio button: `<input type="radio">`</span></span>
- <span data-ttu-id="f1686-172">按钮：`<input type="button">`</span><span class="sxs-lookup"><span data-stu-id="f1686-172">Button: `<input type="button">`</span></span>
- <span data-ttu-id="f1686-173">提交按钮：`<input type="submit">`</span><span class="sxs-lookup"><span data-stu-id="f1686-173">Submit button: `<input type="submit">`</span></span>

<span data-ttu-id="f1686-174">你还可以使用`<textarea>`元素以创建多行文本框和`<select>`元素来创建一个下拉列表或可滚动的列表。</span><span class="sxs-lookup"><span data-stu-id="f1686-174">You can also use the `<textarea>` element to create a multiline text box and the `<select>` element to create a drop-down list or scrollable list.</span></span> <span data-ttu-id="f1686-175">(有关更多关于 HTML 窗体元素中，请参阅[HTML 窗体和输入](http://www.w3schools.com/html/html_forms.asp)W3Schools 站点上。)</span><span class="sxs-lookup"><span data-stu-id="f1686-175">(For more about HTML form elements, see [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) on the W3Schools site.)</span></span>

<span data-ttu-id="f1686-176">`name`属性是非常重要，因为该名称是如何将获取更高版本，元素的值为很快就会看到。</span><span class="sxs-lookup"><span data-stu-id="f1686-176">The `name` attribute is very important, because the name is how you'll get the value of the element later, as you'll see shortly.</span></span>

<span data-ttu-id="f1686-177">有趣的一部分是你，即页开发人员，使用用户的输入所执行的操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-177">The interesting part is what you, the page developer, do with the user's input.</span></span> <span data-ttu-id="f1686-178">没有与这些元素关联的任何内置行为。</span><span class="sxs-lookup"><span data-stu-id="f1686-178">There's no built-in behavior associated with these elements.</span></span> <span data-ttu-id="f1686-179">相反，你需要获取用户输入或选择的值并使用它们执行某些操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-179">Instead, you have to get the values that the user has entered or selected and do something with them.</span></span> <span data-ttu-id="f1686-180">这是在本教程中将要掌握的内容。</span><span class="sxs-lookup"><span data-stu-id="f1686-180">That's what you'll learn in this tutorial.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="f1686-181">**HTML5 和输入的窗体**</span><span class="sxs-lookup"><span data-stu-id="f1686-181">**HTML5 and Input Forms**</span></span>
> 
> <span data-ttu-id="f1686-182">你可能知道，如 HTML 处于过渡状态，最新版本 (HTML5) 包括对更直观的方式将用户输入信息的支持。</span><span class="sxs-lookup"><span data-stu-id="f1686-182">As you might know, HTML is in transition and the latest version (HTML5) includes support for more intuitive ways for users to enter information.</span></span> <span data-ttu-id="f1686-183">例如，在 HTML5，你 （即页开发人员） 可以告诉页你希望用户输入的日期。</span><span class="sxs-lookup"><span data-stu-id="f1686-183">For example, in HTML5, you (the page developer) can tell the page that you want the user to enter a date.</span></span> <span data-ttu-id="f1686-184">然后可以自动显示浏览器，日历，而不是要求用户手动输入日期。</span><span class="sxs-lookup"><span data-stu-id="f1686-184">The browser can then automatically display a calendar rather than requiring the user to enter a date manually.</span></span> <span data-ttu-id="f1686-185">但是，HTML5 是新，并且尚不支持在所有浏览器中。</span><span class="sxs-lookup"><span data-stu-id="f1686-185">However, HTML5 is new and is not supported in all browsers yet.</span></span>
> 
> <span data-ttu-id="f1686-186">ASP.NET Web Pages 支持 HTML5 的范围内用户的浏览器未输入。</span><span class="sxs-lookup"><span data-stu-id="f1686-186">ASP.NET Web Pages supports HTML5 input to the extent that the user's browser does.</span></span> <span data-ttu-id="f1686-187">新特性的了解`<input>`元素 html5 格式，请参阅[HTML&lt;输入&gt;键入属性](http://www.w3schools.com/html/html_form_input_types.asp)W3Schools 站点上。</span><span class="sxs-lookup"><span data-stu-id="f1686-187">For an idea of the new attributes for the `<input>` element in HTML5, see [HTML &lt;input&gt; type Attribute](http://www.w3schools.com/html/html_form_input_types.asp) on the W3Schools site.</span></span>


## <a name="creating-the-form"></a><span data-ttu-id="f1686-188">创建窗体</span><span class="sxs-lookup"><span data-stu-id="f1686-188">Creating the Form</span></span>

<span data-ttu-id="f1686-189">在 WebMatrix 中，在**文件**工作区中，打开*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="f1686-189">In WebMatrix, in the **Files** workspace, open the *Movies.cshtml* page.</span></span>

<span data-ttu-id="f1686-190">之后，结束`</h1>`标记和在打开之前`<div>`标记`grid.GetHtml`调用，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="f1686-190">After the closing `</h1>` tag and before the opening `<div>` tag of the `grid.GetHtml` call, add the following markup:</span></span>

[!code-html[Main](form-basics/samples/sample2.html)]

<span data-ttu-id="f1686-191">此标记创建具有一个名为的文本框的窗体`searchGenre`和提交按钮。</span><span class="sxs-lookup"><span data-stu-id="f1686-191">This markup creates a form that has a text box named `searchGenre` and a submit button.</span></span> <span data-ttu-id="f1686-192">文本框中，并提交按钮括在`<form>`元素其`method`属性设置为`get`。</span><span class="sxs-lookup"><span data-stu-id="f1686-192">The text box and submit button are enclosed in a `<form>` element whose `method` attribute is set to `get`.</span></span> <span data-ttu-id="f1686-193">(请记住，如果你没有将文本框中，然后提交按钮位于内的`<form>`元素中，单击按钮时将提交执行任何操作。)你使用`GET`谓词此处因为你要创建窗体，不进行任何更改在服务器上-它只需在搜索结果。</span><span class="sxs-lookup"><span data-stu-id="f1686-193">(Remember that if you don't put the text box and submit button inside a `<form>` element, nothing will be submitted when you click the button.) You use the `GET` verb here because you're creating a form that does not make any changes on the server — it just results in a search.</span></span> <span data-ttu-id="f1686-194">(在前面的教程，你使用了`post`方法，即如何提交到服务器的更改。</span><span class="sxs-lookup"><span data-stu-id="f1686-194">(In the previous tutorial, you used a `post` method, which is how you submit changes to the server.</span></span> <span data-ttu-id="f1686-195">你将看到，在下一步教程再次。）</span><span class="sxs-lookup"><span data-stu-id="f1686-195">You'll see that in the next tutorial again.)</span></span>

<span data-ttu-id="f1686-196">运行页面。</span><span class="sxs-lookup"><span data-stu-id="f1686-196">Run the page.</span></span> <span data-ttu-id="f1686-197">虽然你尚未定义窗体的任何行为，但是你可以看到如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1686-197">Although you haven't defined any behavior for the form, you can see what it looks like:</span></span>

![电影页流派的搜索框](form-basics/_static/image3.png)

<span data-ttu-id="f1686-199">输入一个值，在文本框中，如"喜剧。"</span><span class="sxs-lookup"><span data-stu-id="f1686-199">Enter a value into the text box, like "Comedy."</span></span> <span data-ttu-id="f1686-200">然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="f1686-200">Then click **Search Genre**.</span></span>

<span data-ttu-id="f1686-201">记下页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="f1686-201">Take note of the URL of the page.</span></span> <span data-ttu-id="f1686-202">由于已将设置`<form>`元素的`method`属性设为`get`，您输入的值现在是在 URL 中，如下查询字符串的一部分：</span><span class="sxs-lookup"><span data-stu-id="f1686-202">Because you set the `<form>` element's `method` attribute to `get`, the value you entered is now part of the query string in the URL, like this:</span></span>

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a><span data-ttu-id="f1686-203">读取窗体值</span><span class="sxs-lookup"><span data-stu-id="f1686-203">Reading Form Values</span></span>

<span data-ttu-id="f1686-204">此页已包含一些代码，获取数据库数据并在网格中显示结果。</span><span class="sxs-lookup"><span data-stu-id="f1686-204">The page already contains some code that gets database data and displays the results in a grid.</span></span> <span data-ttu-id="f1686-205">现在，您需要添加一些代码，以便可以运行包括搜索词的 SQL 查询读取文本框的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-205">Now you have to add some code that reads the value of the text box so you can run a SQL query that includes the search term.</span></span>

<span data-ttu-id="f1686-206">因为窗体的方法设置为`get`，你可以读取已通过使用类似于下面的代码输入到文本框中的值：</span><span class="sxs-lookup"><span data-stu-id="f1686-206">Because you set the form's method to `get`, you can read the value that was entered into the text box by using code like the following:</span></span>

`var searchTerm = Request.QueryString["searchGenre"];`

<span data-ttu-id="f1686-207">`Request.QueryString`对象 (`QueryString`属性`Request`对象) 包括作为的一部分提交的元素的值`GET`操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-207">The `Request.QueryString` object (the `QueryString` property of the `Request` object) includes the values of elements that were submitted as part of the `GET` operation.</span></span> <span data-ttu-id="f1686-208">`Request.QueryString`属性包含*集合*（列表） 在窗体中提交的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-208">The `Request.QueryString` property contains a *collection* (a list) of the values that are submitted in the form.</span></span> <span data-ttu-id="f1686-209">若要获取任何单个值，你可以指定所需的元素的名称。</span><span class="sxs-lookup"><span data-stu-id="f1686-209">To get any individual value, you specify the name of the element that you want.</span></span> <span data-ttu-id="f1686-210">这就是为什么你必须拥有`name`属性`<input>`元素 (`searchTerm`) 创建文本框。</span><span class="sxs-lookup"><span data-stu-id="f1686-210">That's why you have to have a `name` attribute on the `<input>` element (`searchTerm`) that creates the text box.</span></span> <span data-ttu-id="f1686-211">(有关详细信息`Request`对象，请参阅[边栏](#BKMK_TheRequestObject)更高版本。)</span><span class="sxs-lookup"><span data-stu-id="f1686-211">(For more about the `Request` object, see the [sidebar](#BKMK_TheRequestObject) later.)</span></span>

<span data-ttu-id="f1686-212">它非常简单，可以读取的文本框中的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-212">It's simple enough to read the value of the text box.</span></span> <span data-ttu-id="f1686-213">但是，如果用户未输入任何内容根本在文本框中，但单击**搜索**，可以忽略该单击，因为无需进行任何搜索。</span><span class="sxs-lookup"><span data-stu-id="f1686-213">But if the user didn't enter anything at all in the text box but clicked **Search** anyway, you can ignore that click, since there's nothing to search.</span></span>

<span data-ttu-id="f1686-214">下面的代码是一个示例，演示如何实现这些条件。</span><span class="sxs-lookup"><span data-stu-id="f1686-214">The following code is an example that shows how to implement these conditions.</span></span> <span data-ttu-id="f1686-215">（无需尚未添加此代码; 你将在稍后执行的。）</span><span class="sxs-lookup"><span data-stu-id="f1686-215">(You don't have to add this code yet; you'll do that in a moment.)</span></span>

[!code-csharp[Main](form-basics/samples/sample3.cs)]

<span data-ttu-id="f1686-216">测试在这种方式中中断：</span><span class="sxs-lookup"><span data-stu-id="f1686-216">The test breaks down in this way:</span></span>

- <span data-ttu-id="f1686-217">获取的值`Request.QueryString["searchGenre"]`，即已输入到的值`<input>`元素名为`searchGenre`。</span><span class="sxs-lookup"><span data-stu-id="f1686-217">Get the value of `Request.QueryString["searchGenre"]`, namely the value that was entered into the `<input>` element named `searchGenre`.</span></span>
- <span data-ttu-id="f1686-218">了解它是否为空使用`IsEmpty`方法。</span><span class="sxs-lookup"><span data-stu-id="f1686-218">Find out if it's empty by using the `IsEmpty` method.</span></span> <span data-ttu-id="f1686-219">此方法是确定是否 （例如，窗体元素） 的内容包含值的标准方式。</span><span class="sxs-lookup"><span data-stu-id="f1686-219">This method is the standard way to determine whether something (for example, a form element) contains a value.</span></span> <span data-ttu-id="f1686-220">但是你确实关心只有在它*不*为空，因此...</span><span class="sxs-lookup"><span data-stu-id="f1686-220">But really, you care only if it's *not* empty, therefore ...</span></span>
- <span data-ttu-id="f1686-221">添加`!`前端中的运算符`IsEmpty`测试。</span><span class="sxs-lookup"><span data-stu-id="f1686-221">Add the `!` operator in front of the `IsEmpty` test.</span></span> <span data-ttu-id="f1686-222">(`!`运算符意味着逻辑非)。</span><span class="sxs-lookup"><span data-stu-id="f1686-222">(The `!` operator means logical NOT).</span></span>

<span data-ttu-id="f1686-223">在简单地说，整个`if`条件将以下转换：*如果窗体的 searchGenre 元素不为空，然后...*</span><span class="sxs-lookup"><span data-stu-id="f1686-223">In plain English, the entire `if` condition translates into the following: *If the form's searchGenre element is not empty, then ...*</span></span>

<span data-ttu-id="f1686-224">此块设置用于创建使用搜索词的查询的阶段。</span><span class="sxs-lookup"><span data-stu-id="f1686-224">This block sets the stage for creating a query that uses the search term.</span></span> <span data-ttu-id="f1686-225">在下一部分中，将执行该操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-225">You'll do that in the next section.</span></span>

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> <span data-ttu-id="f1686-226">**请求对象**</span><span class="sxs-lookup"><span data-stu-id="f1686-226">**The Request Object**</span></span>
> 
> <span data-ttu-id="f1686-227">`Request`对象包含请求或提交页时，浏览器发送给你的应用程序的所有信息。</span><span class="sxs-lookup"><span data-stu-id="f1686-227">The `Request` object contains all the information that the browser sends to your application when a page is requested or submitted.</span></span> <span data-ttu-id="f1686-228">此对象包括用户提供，如文本框值或要上载的文件的任何信息。</span><span class="sxs-lookup"><span data-stu-id="f1686-228">This object includes any information that the user provides, like text box values or a file to upload.</span></span> <span data-ttu-id="f1686-229">它还包括各种类型的其他信息，如 cookie，URL 查询字符串 （如果有） 中的值正在运行，浏览器的用户正在使用，在浏览器中设置的语言的列表类型页的文件路径等等。</span><span class="sxs-lookup"><span data-stu-id="f1686-229">It also includes all sorts of additional information, like cookies, values in the URL query string (if any), the file path of the page that is running, the type of browser that the user is using, the list of languages that are set in the browser, and much more.</span></span>
> 
> <span data-ttu-id="f1686-230">`Request`对象是*集合*（列表） 的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-230">The `Request` object is a *collection* (list) of values.</span></span> <span data-ttu-id="f1686-231">你可以通过指定其名称获取从该集合的单个值：</span><span class="sxs-lookup"><span data-stu-id="f1686-231">You get an individual value out of the collection by specifying its name:</span></span>
> 
> `var someValue = Request["name"];`
> 
> <span data-ttu-id="f1686-232">`Request`对象实际公开多个子集。</span><span class="sxs-lookup"><span data-stu-id="f1686-232">The `Request` object actually exposes several subsets.</span></span> <span data-ttu-id="f1686-233">例如:</span><span class="sxs-lookup"><span data-stu-id="f1686-233">For example:</span></span>
> 
> - <span data-ttu-id="f1686-234">`Request.Form`为你提供从内提交元素值`<form>`如果请求的元素`POST`请求。</span><span class="sxs-lookup"><span data-stu-id="f1686-234">`Request.Form` gives you values from elements inside the submitted `<form>` element if the request is a `POST` request.</span></span>
> - <span data-ttu-id="f1686-235">`Request.QueryString`为你提供的值只是中的 URL 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="f1686-235">`Request.QueryString` gives you just the values in the URL's query string.</span></span> <span data-ttu-id="f1686-236">(如 URL 中`http://mysite/myapp/page?searchGenre=action&page=2`、`?searchGenre=action&page=2`部分 URL 为查询字符串。)</span><span class="sxs-lookup"><span data-stu-id="f1686-236">(In a URL like `http://mysite/myapp/page?searchGenre=action&page=2`, the `?searchGenre=action&page=2` section of the URL is the query string.)</span></span>
> - <span data-ttu-id="f1686-237">`Request.Cookies`集合访问你的浏览器发送的 cookie。</span><span class="sxs-lookup"><span data-stu-id="f1686-237">`Request.Cookies` collection gives you access to cookies that the browser has sent.</span></span>
> 
> <span data-ttu-id="f1686-238">若要获取一个值，你知道是在提交窗体中，你可以使用`Request["name"]`。</span><span class="sxs-lookup"><span data-stu-id="f1686-238">To get a value that you know is in the submitted form, you can use `Request["name"]`.</span></span> <span data-ttu-id="f1686-239">或者，可以使用更具体版本`Request.Form["name"]`(有关`POST`请求) 或`Request.QueryString["name"]`(有关`GET`请求)。</span><span class="sxs-lookup"><span data-stu-id="f1686-239">Alternatively, you can use the more specific versions `Request.Form["name"]` (for `POST` requests) or `Request.QueryString["name"]` (for `GET` requests).</span></span> <span data-ttu-id="f1686-240">当然，*名称*是要获取的项的名称。</span><span class="sxs-lookup"><span data-stu-id="f1686-240">Of course, *name* is the name of the item to get.</span></span>
> 
> <span data-ttu-id="f1686-241">你想要获取的项的名称必须是唯一中正在使用的集合。</span><span class="sxs-lookup"><span data-stu-id="f1686-241">The name of the item you want to get has to be unique within the collection you're using.</span></span> <span data-ttu-id="f1686-242">这就是为什么`Request`对象提供子集喜欢`Request.Form`和`Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="f1686-242">That's why the `Request` object provides the subsets like `Request.Form` and `Request.QueryString`.</span></span> <span data-ttu-id="f1686-243">假设你的页面包含名为窗体元素`userName`和*还*包含名为一个 cookie `userName`。</span><span class="sxs-lookup"><span data-stu-id="f1686-243">Suppose that your page contains a form element named `userName` and *also* contains a cookie named `userName`.</span></span> <span data-ttu-id="f1686-244">如果你收到`Request["userName"]`，它是不明确所需的窗体值或 cookie。</span><span class="sxs-lookup"><span data-stu-id="f1686-244">If you get `Request["userName"]`, it's ambiguous whether you want the form value or the cookie.</span></span> <span data-ttu-id="f1686-245">但是，如果你收到`Request.Form["userName"]`或`Request.Cookie["userName"]`，要被明确要获取的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-245">However, if you get `Request.Form["userName"]` or `Request.Cookie["userName"]`, you're being explicit about which value to get.</span></span>
> 
> <span data-ttu-id="f1686-246">很好的做法进行特定并使用相同的子集`Request`你感兴趣，如`Request.Form`或`Request.QueryString`。</span><span class="sxs-lookup"><span data-stu-id="f1686-246">It's a good practice to be specific and use the subset of `Request` that you're interested in, like `Request.Form` or `Request.QueryString`.</span></span> <span data-ttu-id="f1686-247">对于你要在本教程中创建的简单页面，它可能不真正带来任何差异。</span><span class="sxs-lookup"><span data-stu-id="f1686-247">For the simple pages that you're creating in this tutorial, it probably doesn't really make any difference.</span></span> <span data-ttu-id="f1686-248">但是，当您创建更复杂的页，使用的显式版本`Request.Form`或`Request.QueryString`可帮助你避免时的页面包含窗体 （或多个窗体），可能出现的问题 cookie、 查询字符串值和等等。</span><span class="sxs-lookup"><span data-stu-id="f1686-248">However, as you create more complex pages, using the explicit version `Request.Form` or `Request.QueryString` can help you avoid problems that can arise when the page contains a form (or multiple forms), cookies, query string values, and so on.</span></span>


## <a name="creating-a-query-by-using-a-search-term"></a><span data-ttu-id="f1686-249">通过使用的搜索词创建查询</span><span class="sxs-lookup"><span data-stu-id="f1686-249">Creating a Query by Using a Search Term</span></span>

<span data-ttu-id="f1686-250">既然你知道如何获取用户输入搜索词，可以创建使用它的查询。</span><span class="sxs-lookup"><span data-stu-id="f1686-250">Now that you know how to get the search term that the user entered, you can create a query that uses it.</span></span> <span data-ttu-id="f1686-251">请记住，若要获取出数据库的所有影片项，你正在使用如下所示此语句的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="f1686-251">Remember that to get all the movie items out of the database, you're using a SQL query that looks like this statement:</span></span>

`SELECT * FROM Movies`

<span data-ttu-id="f1686-252">若要获取仅某些电影，你需要使用一个查询，包括`Where`子句。</span><span class="sxs-lookup"><span data-stu-id="f1686-252">To get only certain movies, you have to use a query that includes a `Where` clause.</span></span> <span data-ttu-id="f1686-253">此子句允许你设置由查询返回行的条件。</span><span class="sxs-lookup"><span data-stu-id="f1686-253">This clause lets you set a condition on which rows are returned by the query.</span></span> <span data-ttu-id="f1686-254">以下是一个示例：</span><span class="sxs-lookup"><span data-stu-id="f1686-254">Here's an example:</span></span>

`SELECT * FROM Movies WHERE Genre = 'Action'`

<span data-ttu-id="f1686-255">基本格式`WHERE column = value`。</span><span class="sxs-lookup"><span data-stu-id="f1686-255">The basic format is `WHERE column = value`.</span></span> <span data-ttu-id="f1686-256">除了只之外，可以使用不同运算符`=`、 like `>` （大于）、 `<` （小于）， `<>` （不等于）、 `<=` （小于或等于）、 等，具体取决于你正在寻找的内容。</span><span class="sxs-lookup"><span data-stu-id="f1686-256">You can use different operators besides just `=`, like `>` (greater than), `<` (less than), `<>` (not equal to), `<=` (less than or equal to), etc., depending on what you're looking for.</span></span>

<span data-ttu-id="f1686-257">如果您想知道，SQL 语句不区分大小写&mdash;`SELECT`相同`Select`(或甚至`select`)。</span><span class="sxs-lookup"><span data-stu-id="f1686-257">In case you're wondering, SQL statements are not case sensitive &mdash; `SELECT` is the same as `Select` (or even `select`).</span></span> <span data-ttu-id="f1686-258">但是，用户通常利用关键字在 SQL 语句中，如`SELECT`和`WHERE`，以使其更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="f1686-258">However, people often capitalize keywords in a SQL statement, like `SELECT` and `WHERE`, to make it easier to read.</span></span>

### <a name="passing-the-search-term-as-a-parameter"></a><span data-ttu-id="f1686-259">作为参数传递的搜索词</span><span class="sxs-lookup"><span data-stu-id="f1686-259">Passing the search term as a parameter</span></span>

<span data-ttu-id="f1686-260">搜索特定风格也很简单 (`WHERE Genre = 'Action'`)，但你想要能够搜索任何用户输入的风格。</span><span class="sxs-lookup"><span data-stu-id="f1686-260">Searching for a specific genre is easy enough (`WHERE Genre = 'Action'`), but you want to be able to search for any genre that the user enters.</span></span> <span data-ttu-id="f1686-261">若要做到这一点，创建时为 SQL 查询，其中包含要搜索的值的占位符。</span><span class="sxs-lookup"><span data-stu-id="f1686-261">To do that, you create as SQL query that includes a placeholder for the value to search.</span></span> <span data-ttu-id="f1686-262">它将类似此命令：</span><span class="sxs-lookup"><span data-stu-id="f1686-262">It will look like this command:</span></span>

`SELECT * FROM Movies WHERE Genre = @0`

<span data-ttu-id="f1686-263">占位符所`@`字符跟零个。</span><span class="sxs-lookup"><span data-stu-id="f1686-263">The placeholder is the `@` character followed by zero.</span></span> <span data-ttu-id="f1686-264">您可能认为，查询可以包含多个占位符，它们将被命名为`@0`， `@1`， `@2`，等等。</span><span class="sxs-lookup"><span data-stu-id="f1686-264">As you might guess, a query can contain multiple placeholders, and they'd be named `@0`, `@1`, `@2`, etc.</span></span>

<span data-ttu-id="f1686-265">若要设置的查询和实际传递的值，你可以使用代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1686-265">To set up the query and actually pass it the value, you use the code like the following:</span></span>

[!code-sql[Main](form-basics/samples/sample4.sql)]

<span data-ttu-id="f1686-266">此代码将类似于所已做的网格中显示数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-266">This code is similar to what you've already done to display data in the grid.</span></span> <span data-ttu-id="f1686-267">唯一的区别如下：</span><span class="sxs-lookup"><span data-stu-id="f1686-267">The only differences are:</span></span>

- <span data-ttu-id="f1686-268">该查询包含一个占位符 (`WHERE Genre = @0"`)。</span><span class="sxs-lookup"><span data-stu-id="f1686-268">The query contains a placeholder (`WHERE Genre = @0"`).</span></span>
- <span data-ttu-id="f1686-269">查询会被放置到一个变量 (`selectCommand`); 之前，你查询直接传递到`db.Query`方法。</span><span class="sxs-lookup"><span data-stu-id="f1686-269">The query is put into a variable (`selectCommand`); before, you passed the query directly to the `db.Query` method.</span></span>
- <span data-ttu-id="f1686-270">当调用`db.Query`方法，需传递查询和要使用的占位符的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-270">When you call the `db.Query` method, you pass both the query and the value to use for the placeholder.</span></span> <span data-ttu-id="f1686-271">(如果查询具有多个占位符，会将它们传递所有项作为对方法的单独值。)</span><span class="sxs-lookup"><span data-stu-id="f1686-271">(If the query had multiple placeholders, you'd pass them all as separate values to the method.)</span></span>

<span data-ttu-id="f1686-272">如果结合这些元素，将得到以下代码：</span><span class="sxs-lookup"><span data-stu-id="f1686-272">If you put all these elements together, you get the following code:</span></span>

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="f1686-273">**重要 ！**</span><span class="sxs-lookup"><span data-stu-id="f1686-273">**Important!**</span></span> <span data-ttu-id="f1686-274">使用占位符 (如`@0`) 若要将值传递给 SQL 命令*极其重要*的安全性。</span><span class="sxs-lookup"><span data-stu-id="f1686-274">Using placeholders (like `@0`) to pass values to a SQL command is *extremely important* for security.</span></span> <span data-ttu-id="f1686-275">你看到它在这里，带有占位符变量数据的方式是你应该构建 SQL 命令的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="f1686-275">The way you see it here, with placeholders for variable data, is the only way you should construct SQL commands.</span></span>
> 
> <span data-ttu-id="f1686-276">永远不会通过将放在一起 （串联） 的文字文本和从用户获取的值来构造 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="f1686-276">Never construct a SQL statement by putting together (concatenating) literal text and values you get from the user.</span></span> <span data-ttu-id="f1686-277">连接到 SQL 语句的用户输入打开网站*SQL 注入式攻击*其中恶意用户提交到你的页 hack 你的数据库的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-277">Concatenating user input into a SQL statement opens your site to a *SQL injection attack* where a malicious user submits values to your page that hack your database.</span></span> <span data-ttu-id="f1686-278">(你可以阅读更多的文章中[SQL 注入](https://msdn.microsoft.com/library/ms161953.aspx)MSDN 网站。)</span><span class="sxs-lookup"><span data-stu-id="f1686-278">(You can read more in the article [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx) the MSDN website.)</span></span>


## <a name="updating-the-movies-page-with-search-code"></a><span data-ttu-id="f1686-279">使用搜索代码更新电影页</span><span class="sxs-lookup"><span data-stu-id="f1686-279">Updating the Movies Page with Search Code</span></span>

<span data-ttu-id="f1686-280">现在你可以更新中的代码*Movies.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="f1686-280">Now you can update the code in the *Movies.cshtml* file.</span></span> <span data-ttu-id="f1686-281">若要开始，请将在页面顶部的代码块中的代码替换此代码：</span><span class="sxs-lookup"><span data-stu-id="f1686-281">To begin, replace the code in the code block at the top of the page with this code:</span></span>

[!code-csharp[Main](form-basics/samples/sample6.cs)]

<span data-ttu-id="f1686-282">此处的差异是你没有将放到查询`selectCommand`变量不同，后者将传递给`db.Query`更高版本。</span><span class="sxs-lookup"><span data-stu-id="f1686-282">The difference here is that you've put the query into the `selectCommand` variable, which you'll pass to `db.Query` later.</span></span> <span data-ttu-id="f1686-283">将放置到一个变量中的 SQL 语句允许您更改语句，它将执行哪些操作来执行搜索。</span><span class="sxs-lookup"><span data-stu-id="f1686-283">Putting the SQL statement into a variable lets you change the statement, which is what you'll do to perform the search.</span></span>

<span data-ttu-id="f1686-284">你还删除了这两行，你将放回中更高版本：</span><span class="sxs-lookup"><span data-stu-id="f1686-284">You've also removed these two lines, which you'll put back in later:</span></span>

[!code-csharp[Main](form-basics/samples/sample7.cs)]

<span data-ttu-id="f1686-285">你不想尚未运行的查询 (也就是说，调用`db.Query`) 并且你不想要初始化`WebGrid`帮助程序，但请。</span><span class="sxs-lookup"><span data-stu-id="f1686-285">You don't want to run the query yet (that is, call `db.Query`) and you don't want to initialize the `WebGrid` helper yet either.</span></span> <span data-ttu-id="f1686-286">你已理解的 SQL 语句都必须运行后，你将执行这些操作。</span><span class="sxs-lookup"><span data-stu-id="f1686-286">You'll do those things after you've figured out which SQL statement has to run.</span></span>

<span data-ttu-id="f1686-287">在此重写块后可以添加用于处理搜索新的逻辑。</span><span class="sxs-lookup"><span data-stu-id="f1686-287">After this rewritten block, you can add the new logic for handling the search.</span></span> <span data-ttu-id="f1686-288">已完成的代码将如下所示。</span><span class="sxs-lookup"><span data-stu-id="f1686-288">The completed code will look like the following.</span></span> <span data-ttu-id="f1686-289">使其匹配此示例，请更新你的页面中的代码：</span><span class="sxs-lookup"><span data-stu-id="f1686-289">Update the code in your page so it matches this example:</span></span>

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

<span data-ttu-id="f1686-290">现在的页工作原理如下。</span><span class="sxs-lookup"><span data-stu-id="f1686-290">The page now works like this.</span></span> <span data-ttu-id="f1686-291">每次运行页面，代码将打开的数据库和`selectCommand`变量设置为获取中的所有记录的 SQL 语句`Movies`表。</span><span class="sxs-lookup"><span data-stu-id="f1686-291">Every time the page runs, the code opens the database and the `selectCommand` variable is set to the SQL statement that gets all the records from the `Movies` table.</span></span> <span data-ttu-id="f1686-292">此代码还初始化`searchTerm`变量。</span><span class="sxs-lookup"><span data-stu-id="f1686-292">The code also initializes the `searchTerm` variable.</span></span>

<span data-ttu-id="f1686-293">但是，如果当前请求中包含的值`searchGenre`元素，该代码设置`selectCommand`到另一个查询 — 也就是说，为包含`Where`子句来搜索一种风格。</span><span class="sxs-lookup"><span data-stu-id="f1686-293">However, if the current request includes a value for the `searchGenre` element, the code sets `selectCommand` to a different query — namely, to one that includes the `Where` clause to search for a genre.</span></span> <span data-ttu-id="f1686-294">它还将设置`searchTerm`到任何传递的搜索框中 （这可能是执行任何操作）。</span><span class="sxs-lookup"><span data-stu-id="f1686-294">It also sets `searchTerm` to whatever was passed for the search box (which might be nothing).</span></span>

<span data-ttu-id="f1686-295">而不考虑哪些 SQL 语句不在`selectCommand`，然后，代码调用`db.Query`要运行查询，将其传递任何点在`searchTerm`。</span><span class="sxs-lookup"><span data-stu-id="f1686-295">Regardless of which SQL statement is in `selectCommand`, the code then calls `db.Query` to run the query, passing it whatever is in `searchTerm`.</span></span> <span data-ttu-id="f1686-296">如果中没有任何`searchTerm`，它并不重要，因为在这种情况下没有参数传递到值`selectCommand`仍。</span><span class="sxs-lookup"><span data-stu-id="f1686-296">If there's nothing in `searchTerm`, it doesn't matter, because in that case there's no parameter to pass the value to `selectCommand` anyway.</span></span>

<span data-ttu-id="f1686-297">最后，此代码初始化`WebGrid`帮助器通过使用查询结果，像之前一样。</span><span class="sxs-lookup"><span data-stu-id="f1686-297">Finally, the code initializes the `WebGrid` helper by using the query results, just like before.</span></span>

<span data-ttu-id="f1686-298">你可以看到，通过将放在 SQL 语句和搜索词到变量中，你已向代码添加的灵活性。</span><span class="sxs-lookup"><span data-stu-id="f1686-298">You can see that by putting the SQL statement and the search term into variables, you've added flexibility to the code.</span></span> <span data-ttu-id="f1686-299">正如您将看到更高版本在本教程中，你可以使用此基本框架，并且保留添加的搜索结果的不同类型的逻辑。</span><span class="sxs-lookup"><span data-stu-id="f1686-299">As you'll see later in this tutorial, you can use this basic framework and keep adding logic for different types of searches.</span></span>

## <a name="testing-the-search-by-genre-feature"></a><span data-ttu-id="f1686-300">测试通过流派搜索功能</span><span class="sxs-lookup"><span data-stu-id="f1686-300">Testing the Search-by-Genre Feature</span></span>

<span data-ttu-id="f1686-301">在 WebMatrix 中，运行*Movies.cshtml*页。</span><span class="sxs-lookup"><span data-stu-id="f1686-301">In WebMatrix, run the *Movies.cshtml* page.</span></span> <span data-ttu-id="f1686-302">你看到流派的文本框中的页。</span><span class="sxs-lookup"><span data-stu-id="f1686-302">You see the page with the text box for genre.</span></span>

<span data-ttu-id="f1686-303">输入已输入一个你测试的记录，然后单击一种风格**搜索**。</span><span class="sxs-lookup"><span data-stu-id="f1686-303">Enter a genre that you've entered for one of your test records, then click **Search**.</span></span> <span data-ttu-id="f1686-304">此时会显示仅匹配的影片电影的列表：</span><span class="sxs-lookup"><span data-stu-id="f1686-304">This time you see a listing of just the movies that match that genre:</span></span>

![列出搜索 genre Comedies 后的电影页](form-basics/_static/image4.png)

<span data-ttu-id="f1686-306">输入不同的流派，然后再次搜索。</span><span class="sxs-lookup"><span data-stu-id="f1686-306">Enter a different genre and search again.</span></span> <span data-ttu-id="f1686-307">请尝试使用所有小写字母或全部大写的字母，这样您可以看到搜索不区分大小写输入风格。</span><span class="sxs-lookup"><span data-stu-id="f1686-307">Try entering the genre by using all lowercase or all uppercase letters so that you can see that the search is not case sensitive.</span></span>

## <a name="remembering-what-the-user-entered"></a><span data-ttu-id="f1686-308">"记住"用户输入</span><span class="sxs-lookup"><span data-stu-id="f1686-308">"Remembering" What the User Entered</span></span>

<span data-ttu-id="f1686-309">你可能已经注意到，之后您输入流派，并单击**搜索流派**，你看到的影片列表。</span><span class="sxs-lookup"><span data-stu-id="f1686-309">You might have noticed that after you entered a genre and clicked **Search Genre**, you saw a listing for that genre.</span></span> <span data-ttu-id="f1686-310">但是，搜索文本框中为空&mdash;换而言之，它未请记住您以前输入。</span><span class="sxs-lookup"><span data-stu-id="f1686-310">However, the search text box was empty &mdash; in other words, it didn't remember what you'd entered.</span></span>

<span data-ttu-id="f1686-311">请务必了解为何发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="f1686-311">It's important to understand why this behavior occurs.</span></span> <span data-ttu-id="f1686-312">当你提交的页面时，浏览器会将请求发送到 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f1686-312">When you submit a page, the browser sends a request to the web server.</span></span> <span data-ttu-id="f1686-313">时 ASP.NET 获取请求，它将创建页的全新实例、 运行的代码中，并随后将呈现到浏览器页面。</span><span class="sxs-lookup"><span data-stu-id="f1686-313">When ASP.NET gets the request, it creates a brand-new instance of the page, runs the code in it, and then renders the page to the browser again.</span></span> <span data-ttu-id="f1686-314">实际上，不过，页不知道你正在只需处理与自身的以前的版本。</span><span class="sxs-lookup"><span data-stu-id="f1686-314">In effect, though, the page doesn't know that you were just working with a previous version of itself.</span></span> <span data-ttu-id="f1686-315">所有它知道它有得到了一些的请求中它的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-315">All it knows is that it got a request that had some form data in it.</span></span>

<span data-ttu-id="f1686-316">每次请求页&mdash;是第一次还是通过提交它&mdash;你获取一个新页。</span><span class="sxs-lookup"><span data-stu-id="f1686-316">Every time you request a page &mdash; whether for the first time or by submitting it &mdash; you're getting a new page.</span></span> <span data-ttu-id="f1686-317">Web 服务器包含您上次的请求没有内存。</span><span class="sxs-lookup"><span data-stu-id="f1686-317">The web server has no memory of your last request.</span></span> <span data-ttu-id="f1686-318">不能用 ASP.NET，也不能用浏览器。</span><span class="sxs-lookup"><span data-stu-id="f1686-318">Neither does ASP.NET, and neither does the browser.</span></span> <span data-ttu-id="f1686-319">这些单独的页实例之间的唯一连接是它们之间传输任何数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-319">The only connection between these separate instances of the page is any data that you transmit between them.</span></span> <span data-ttu-id="f1686-320">如果提交页面，例如，新的页实例可以由早期实例发送的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="f1686-320">If you submit a page, for example, the new page instance can get the form data that was sent by the earlier instance.</span></span> <span data-ttu-id="f1686-321">（在页面之间传递数据另一种方法是使用 cookie。）</span><span class="sxs-lookup"><span data-stu-id="f1686-321">(Another way to pass data between pages is to use cookies.)</span></span>

<span data-ttu-id="f1686-322">一种正式的方式来描述这种情况下是说，web 页中找到*无状态*。</span><span class="sxs-lookup"><span data-stu-id="f1686-322">A formal way to describe this situation is to say that web pages are *stateless*.</span></span> <span data-ttu-id="f1686-323">Web 服务器和页面本身和页面中的元素则不会维护有关页面的前一状态的任何信息。</span><span class="sxs-lookup"><span data-stu-id="f1686-323">Web servers and the pages themselves and the elements in the page do not maintain any information about the previous state of a page.</span></span> <span data-ttu-id="f1686-324">Web 旨在这种方式，因为维护的各个请求的状态将快速耗尽的资源的 web 服务器，通常可能处理数千，甚至几十万个情况下，每秒的请求。</span><span class="sxs-lookup"><span data-stu-id="f1686-324">The web was designed this way because maintaining state for individual requests would quickly exhaust the resources of web servers, which often handle thousands, maybe even hundreds of thousands, of requests per second.</span></span>

<span data-ttu-id="f1686-325">因此，这就是为什么文本框为空。</span><span class="sxs-lookup"><span data-stu-id="f1686-325">So that's why the text box was empty.</span></span> <span data-ttu-id="f1686-326">提交页面后，ASP.NET 创建的页的新实例，并运行通过代码和标记。</span><span class="sxs-lookup"><span data-stu-id="f1686-326">After you submitted the page, ASP.NET created a new instance of the page and ran through the code and markup.</span></span> <span data-ttu-id="f1686-327">没有执行任何操作在该代码中，是它告诉 ASP.NET，将值放在文本框中。</span><span class="sxs-lookup"><span data-stu-id="f1686-327">There was nothing in that code that told ASP.NET to put a value into the text box.</span></span> <span data-ttu-id="f1686-328">因此 ASP.NET 不执行任何操作，并且文本框呈现而无需在其中一个值。</span><span class="sxs-lookup"><span data-stu-id="f1686-328">So ASP.NET didn't do anything, and the text box was rendered without a value in it.</span></span>

<span data-ttu-id="f1686-329">没有实际的简单办法获取解决此问题。</span><span class="sxs-lookup"><span data-stu-id="f1686-329">There's actually an easy way to get around this issue.</span></span> <span data-ttu-id="f1686-330">在文本框中输入流派*是*可供你在代码中&mdash;在`Request.QueryString["searchGenre"]`。</span><span class="sxs-lookup"><span data-stu-id="f1686-330">The genre that you entered into the text box *is* available to you in code &mdash; it's in `Request.QueryString["searchGenre"]`.</span></span>

<span data-ttu-id="f1686-331">更新在文本框中的标记，以便`value`属性获取其值从`searchTerm`，如下例所示：</span><span class="sxs-lookup"><span data-stu-id="f1686-331">Update the markup for the text box so that the `value` attribute gets its value from `searchTerm`, like this example:</span></span>

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

<span data-ttu-id="f1686-332">在此页中，你也可以还设置`value`属性设为`searchTerm`输入变量，因为该变量还包含风格。</span><span class="sxs-lookup"><span data-stu-id="f1686-332">In this page, you could have also set the `value` attribute to the `searchTerm` variable, since that variable also contains the genre you entered.</span></span> <span data-ttu-id="f1686-333">但使用`Request`对象以设置`value`属性如下所示下面是完成此任务的标准方式。</span><span class="sxs-lookup"><span data-stu-id="f1686-333">But using the `Request` object to set the `value` attribute as shown here is the standard way to accomplish this task.</span></span> <span data-ttu-id="f1686-334">(假设即使想要执行此操作&mdash;在某些情况下，你可能想要呈现页*而无需*字段中的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-334">(Assuming you even want to do this &mdash; in some situations, you might want to render the page *without* values in the fields.</span></span> <span data-ttu-id="f1686-335">其所有依赖于当前进行的操作与你的应用。）</span><span class="sxs-lookup"><span data-stu-id="f1686-335">It all depends on what's going on with your app.)</span></span>

> [!NOTE]
> <span data-ttu-id="f1686-336">你不能"记住"用于密码的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-336">You can't "remember" the value of a text box that's used for passwords.</span></span> <span data-ttu-id="f1686-337">它将安全漏洞，允许用户通过使用代码填写密码字段。</span><span class="sxs-lookup"><span data-stu-id="f1686-337">It would be a security hole to allow people to fill in a password field by using code.</span></span>


<span data-ttu-id="f1686-338">再次运行此页，输入一种风格，然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="f1686-338">Run the page again, enter a genre, and click **Search Genre**.</span></span> <span data-ttu-id="f1686-339">这次不只执行您看到的搜索的结果，但文本框会记住你所输入上一次：</span><span class="sxs-lookup"><span data-stu-id="f1686-339">This time not only do you see the results of the search, but the text box remembers what you entered last time:</span></span>

![页面显示，文本框中具有记住以前的条目](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a><span data-ttu-id="f1686-341">搜索标题中的任何词语</span><span class="sxs-lookup"><span data-stu-id="f1686-341">Searching for Any Word in the Title</span></span>

<span data-ttu-id="f1686-342">你现在可以搜索任何流派，但你可能也要搜索标题。</span><span class="sxs-lookup"><span data-stu-id="f1686-342">You can now search for any genre, but you might also want to search for a title.</span></span> <span data-ttu-id="f1686-343">很难获取标题完全正确，在搜索时，因此，你可以搜索随即显示在标题的任意位置使用的字符。</span><span class="sxs-lookup"><span data-stu-id="f1686-343">It's hard to get a title exactly right when you search, so instead you can search for a word that appears anywhere inside a title.</span></span> <span data-ttu-id="f1686-344">若要在 SQL 中执行的操作，请使用`LIKE`运算符和语法如下：</span><span class="sxs-lookup"><span data-stu-id="f1686-344">To do that in SQL, you use the `LIKE` operator and syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

<span data-ttu-id="f1686-345">此命令获取其标题包含"adventure"的所有影片。</span><span class="sxs-lookup"><span data-stu-id="f1686-345">This command gets all the movies whose titles contain "adventure".</span></span> <span data-ttu-id="f1686-346">当你使用`LIKE`运算符，你可以包括通配符`%`作为搜索词的一部分。</span><span class="sxs-lookup"><span data-stu-id="f1686-346">When you use the `LIKE` operator, you include the wildcard character `%` as part of the search term.</span></span> <span data-ttu-id="f1686-347">搜索`LIKE 'adventure%'`意味着"从 adventure 开始"。</span><span class="sxs-lookup"><span data-stu-id="f1686-347">The search `LIKE 'adventure%'` means "starting with 'adventure'".</span></span> <span data-ttu-id="f1686-348">（从技术上讲，它表示"string adventure 后面接任何内容。"）同样，搜索词`LIKE '%adventure'`意味着"的任何内容跟字符串 adventure"，这是另一种方法可以显示为"与 adventure 结束"。</span><span class="sxs-lookup"><span data-stu-id="f1686-348">(Technically, it means "The string 'adventure' followed by anything.") Similarly, the search term `LIKE '%adventure'` means "anything followed by the string 'adventure'", which is another way to say "ending with 'adventure'".</span></span>

<span data-ttu-id="f1686-349">搜索词`LIKE '%adventure%'`因此意味着"处理 adventure 标题中的任意位置。"</span><span class="sxs-lookup"><span data-stu-id="f1686-349">The search term `LIKE '%adventure%'` therefore means "with 'adventure' anywhere in the title."</span></span> <span data-ttu-id="f1686-350">（从技术上讲，"的任何内容在标题跟 adventure，后面接任何内容。"）</span><span class="sxs-lookup"><span data-stu-id="f1686-350">(Technically, "anything in the title, followed by 'adventure', followed by anything.")</span></span>

<span data-ttu-id="f1686-351">内部`<form>`元素，添加以下标记在结束之下`</div>`流派搜索标记 (只需在关闭前`</form>`元素):</span><span class="sxs-lookup"><span data-stu-id="f1686-351">Inside the `<form>` element, add the following markup right under the closing `</div>` tag for the genre search (just before the closing `</form>` element):</span></span>

[!code-html[Main](form-basics/samples/sample10.html)]

<span data-ttu-id="f1686-352">代码来处理此搜索是类似于流派搜索代码，只不过你必须以组合`LIKE`搜索。</span><span class="sxs-lookup"><span data-stu-id="f1686-352">The code to handle this search is similar to the code for the genre search, except that you have to assemble the `LIKE` search.</span></span> <span data-ttu-id="f1686-353">在页顶部的代码块中，添加此`if`紧后面阻止`if`流派搜索的块：</span><span class="sxs-lookup"><span data-stu-id="f1686-353">Inside the code block at the top of the page, add this `if` block just after the `if` block for the genre search:</span></span>

[!code-csharp[Main](form-basics/samples/sample11.cs)]

<span data-ttu-id="f1686-354">此代码使用更早版本，看到的相同逻辑，只不过使用的搜索`LIKE`运算符和代码将"`%`"之前和之后的搜索词。</span><span class="sxs-lookup"><span data-stu-id="f1686-354">This code uses the same logic you saw earlier, except that the search uses a `LIKE` operator and the code puts "`%`" before and after the search term.</span></span>

<span data-ttu-id="f1686-355">请注意如何很容易向页面添加另一次搜索。</span><span class="sxs-lookup"><span data-stu-id="f1686-355">Notice how it was easy to add another search to the page.</span></span> <span data-ttu-id="f1686-356">你所要做时：</span><span class="sxs-lookup"><span data-stu-id="f1686-356">All you had to do was:</span></span>

- <span data-ttu-id="f1686-357">创建`if`测试以查看相关的搜索框中是否具有值的块。</span><span class="sxs-lookup"><span data-stu-id="f1686-357">Create an `if` block that tested to see whether the relevant search box had a value.</span></span>
- <span data-ttu-id="f1686-358">设置`selectCommand`变量与新的 SQL 语句。</span><span class="sxs-lookup"><span data-stu-id="f1686-358">Set the `selectCommand` variable to a new SQL statement.</span></span>
- <span data-ttu-id="f1686-359">设置`searchTerm`变量要传递给查询的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-359">Set the `searchTerm` variable to the value to pass to the query.</span></span>

<span data-ttu-id="f1686-360">下面是完整的代码块，其中包含为标题搜索新的逻辑：</span><span class="sxs-lookup"><span data-stu-id="f1686-360">Here's the complete code block, which contains the new logic for a title search:</span></span>

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

<span data-ttu-id="f1686-361">下面是这段代码执行的摘要：</span><span class="sxs-lookup"><span data-stu-id="f1686-361">Here's a summary of what this code does:</span></span>

- <span data-ttu-id="f1686-362">变量`searchTerm`和`selectCommand`顶部初始化。</span><span class="sxs-lookup"><span data-stu-id="f1686-362">The variables `searchTerm` and `selectCommand` are initialized at the top.</span></span> <span data-ttu-id="f1686-363">用户在页面中的作用根据相应的 SQL 命令和你要将这些变量设置为相应的搜索词 （如果有）。</span><span class="sxs-lookup"><span data-stu-id="f1686-363">You're going to set these variables to the appropriate search term (if any) and appropriate SQL command based on what the user does in the page.</span></span> <span data-ttu-id="f1686-364">默认搜索是从数据库中获取所有电影的简单的情况。</span><span class="sxs-lookup"><span data-stu-id="f1686-364">The default search is the simple case of getting all the movies from the database.</span></span>
- <span data-ttu-id="f1686-365">中的测试`searchGenre`和`searchTitle`，代码集`searchTerm`到你想要搜索的值。</span><span class="sxs-lookup"><span data-stu-id="f1686-365">In the tests for `searchGenre` and `searchTitle`, the code sets `searchTerm` to the value you want to search for.</span></span> <span data-ttu-id="f1686-366">这些代码块还设置`selectCommand`对此搜索的相应 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="f1686-366">Those code blocks also set `selectCommand` to an appropriate SQL command for that search.</span></span>
- <span data-ttu-id="f1686-367">`db.Query`方法只调用一次，使用任何 SQL 命令处于`selectedCommand`并且任何值在`searchTerm`。</span><span class="sxs-lookup"><span data-stu-id="f1686-367">The `db.Query` method is invoked only once, using whatever SQL command is in `selectedCommand` and whatever value is in `searchTerm`.</span></span> <span data-ttu-id="f1686-368">如果没有任何搜索词 （没有 genre 和没有标题 word） 的值`searchTerm`为空字符串。</span><span class="sxs-lookup"><span data-stu-id="f1686-368">If there is no search term (no genre and no title word), the value of `searchTerm` is an empty string.</span></span> <span data-ttu-id="f1686-369">但是，，并不重要，因为在这种情况下查询不需要参数。</span><span class="sxs-lookup"><span data-stu-id="f1686-369">However, that doesn't matter, because in that case the query doesn't require a parameter.</span></span>

## <a name="testing-the-title-search-feature"></a><span data-ttu-id="f1686-370">测试标题搜索功能</span><span class="sxs-lookup"><span data-stu-id="f1686-370">Testing the Title Search Feature</span></span>

<span data-ttu-id="f1686-371">现在，你可以测试已完成的搜索页。</span><span class="sxs-lookup"><span data-stu-id="f1686-371">Now you can test your completed search page.</span></span> <span data-ttu-id="f1686-372">运行*Movies.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="f1686-372">Run *Movies.cshtml*.</span></span>

<span data-ttu-id="f1686-373">输入一种风格，然后单击**搜索流派**。</span><span class="sxs-lookup"><span data-stu-id="f1686-373">Enter a genre and click **Search Genre**.</span></span> <span data-ttu-id="f1686-374">网格显示电影的影片，如之前。</span><span class="sxs-lookup"><span data-stu-id="f1686-374">The grid displays movies of that genre, like before.</span></span>

<span data-ttu-id="f1686-375">输入标题词，然后单击**搜索标题**。</span><span class="sxs-lookup"><span data-stu-id="f1686-375">Enter a title word and click **Search Title**.</span></span> <span data-ttu-id="f1686-376">网格将显示在标题中包含该单词的电影。</span><span class="sxs-lookup"><span data-stu-id="f1686-376">The grid displays movies that have that word in the title.</span></span>

![在标题中搜索有关 ' 后列出的电影页](form-basics/_static/image6.png)

<span data-ttu-id="f1686-378">将两个文本框内留空，单击任一按钮。</span><span class="sxs-lookup"><span data-stu-id="f1686-378">Leave both text boxes blank and click either button.</span></span> <span data-ttu-id="f1686-379">网格显示所有影片。</span><span class="sxs-lookup"><span data-stu-id="f1686-379">The grid displays all the movies.</span></span>

## <a name="combining-the-queries"></a><span data-ttu-id="f1686-380">组合查询</span><span class="sxs-lookup"><span data-stu-id="f1686-380">Combining the Queries</span></span>

<span data-ttu-id="f1686-381">你可能注意到，你可以执行的搜索并排斥。</span><span class="sxs-lookup"><span data-stu-id="f1686-381">You might notice that the searches you can perform are exclusive.</span></span> <span data-ttu-id="f1686-382">你不能在同一时间，搜索标题和风格即使这两个搜索框中都有值。</span><span class="sxs-lookup"><span data-stu-id="f1686-382">You can't search the title and the genre at the same time, even if both search boxes have values in them.</span></span> <span data-ttu-id="f1686-383">例如，你不能搜索其标题包含"Adventure"的所有操作电影。</span><span class="sxs-lookup"><span data-stu-id="f1686-383">For example, you can't search for all action movies whose title contains "Adventure".</span></span> <span data-ttu-id="f1686-384">（如果值输入 genre 和标题，现在，编码页，如标题搜索获取优先。）若要创建组合条件搜索，你将必须创建具有如下所示的语法的 SQL 查询：</span><span class="sxs-lookup"><span data-stu-id="f1686-384">(As the page is coded now, if you enter values for both genre and title, the title search gets precedence.) To create a search that combines the conditions, you would have to create a SQL query that has syntax like the following:</span></span>

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

<span data-ttu-id="f1686-385">您必须使用类似于下面的语句运行查询 （大致上说）：</span><span class="sxs-lookup"><span data-stu-id="f1686-385">And you'd have to run the query by using a statement like the following (roughly speaking):</span></span>

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

<span data-ttu-id="f1686-386">如你所见，创建逻辑，以允许多个屏蔽的搜索条件可以获取有点复杂。</span><span class="sxs-lookup"><span data-stu-id="f1686-386">Creating logic to allow many permutations of search criteria can get a bit involved, as you can see.</span></span> <span data-ttu-id="f1686-387">因此，我们将停止此处。</span><span class="sxs-lookup"><span data-stu-id="f1686-387">Therefore, we'll stop here.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="f1686-388">接下来</span><span class="sxs-lookup"><span data-stu-id="f1686-388">Coming Up Next</span></span>

<span data-ttu-id="f1686-389">在下一步的教程中，你将创建使用窗体以使用户可以向数据库添加电影的页。</span><span class="sxs-lookup"><span data-stu-id="f1686-389">In the next tutorial, you'll create a page that uses a form to let users add movies to the database.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-search"></a><span data-ttu-id="f1686-390">（使用搜索更新） 的电影页的完整列表</span><span class="sxs-lookup"><span data-stu-id="f1686-390">Complete Listing for Movie Page (Updated with Search)</span></span>

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="f1686-391">其他资源</span><span class="sxs-lookup"><span data-stu-id="f1686-391">Additional Resources</span></span>

- [<span data-ttu-id="f1686-392">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="f1686-392">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="f1686-393">[SQL WHERE 子句](http://www.w3schools.com/sql/sql_where.asp)W3Schools 站点上</span><span class="sxs-lookup"><span data-stu-id="f1686-393">[SQL WHERE Clause](http://www.w3schools.com/sql/sql_where.asp) on the W3Schools site</span></span>
- <span data-ttu-id="f1686-394">[方法定义](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)W3C 网站上的文章</span><span class="sxs-lookup"><span data-stu-id="f1686-394">[Method Definitions](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) article on the W3C site</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f1686-395">[上一页](displaying-data.md)
[下一页](entering-data.md)</span><span class="sxs-lookup"><span data-stu-id="f1686-395">[Previous](displaying-data.md)
[Next](entering-data.md)</span></span>
