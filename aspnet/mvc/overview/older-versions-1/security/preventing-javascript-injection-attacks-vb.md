---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: 阻止 JavaScript 注入攻击 (VB) |Microsoft 文档
author: StephenWalther
description: 防止 JavaScript 注入式攻击和跨站点脚本攻击发生给您。 在本教程中，Stephen Walther 解释了如何可以轻松地 de...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/19/2008
ms.topic: article
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: cb19236b22abd455472621ce74a8cddf9752d6c5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30871228"
---
<a name="preventing-javascript-injection-attacks-vb"></a><span data-ttu-id="64dd2-104">阻止 JavaScript 注入攻击 (VB)</span><span class="sxs-lookup"><span data-stu-id="64dd2-104">Preventing JavaScript Injection Attacks (VB)</span></span>
====================
<span data-ttu-id="64dd2-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="64dd2-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="64dd2-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="64dd2-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> <span data-ttu-id="64dd2-107">防止 JavaScript 注入式攻击和跨站点脚本攻击发生给您。</span><span class="sxs-lookup"><span data-stu-id="64dd2-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="64dd2-108">在本教程中，Stephen Walther 解释了如何轻松地让这些类型的通过 HTML 编码内容的攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>


<span data-ttu-id="64dd2-109">本教程旨在说明如何在 ASP.NET MVC 应用程序阻止 JavaScript 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="64dd2-110">本教程讨论了两种方法来保护你的网站对 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="64dd2-111">了解如何通过编码的数据，将其显示阻止 JavaScript 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="64dd2-112">你还了解了如何通过编码你接受的数据，防止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="64dd2-113">什么是 JavaScript 注入式攻击？</span><span class="sxs-lookup"><span data-stu-id="64dd2-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="64dd2-114">无论何时你接受用户输入，并重新显示用户输入，你将打开到 JavaScript 注入式攻击你的网站。</span><span class="sxs-lookup"><span data-stu-id="64dd2-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="64dd2-115">让我们检查的具体的应用程序可能会受到 JavaScript 注入式攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="64dd2-116">假设你已创建客户反馈网站 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="64dd2-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="64dd2-117">客户可以访问的网站，并输入使用您的产品其体验的反馈。</span><span class="sxs-lookup"><span data-stu-id="64dd2-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="64dd2-118">客户提交时将这些反馈，反馈将重新显示在反馈页上。</span><span class="sxs-lookup"><span data-stu-id="64dd2-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>


<span data-ttu-id="64dd2-119">[![客户反馈网站](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="64dd2-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span></span>

<span data-ttu-id="64dd2-120">**图 01**： 客户反馈网站 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="64dd2-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image3.png))</span></span>


<span data-ttu-id="64dd2-121">客户反馈网站使用`controller`列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="64dd2-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="64dd2-122">这`controller`包含名为的两个操作`Index()`和`Create()`。</span><span class="sxs-lookup"><span data-stu-id="64dd2-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="64dd2-123">**列表 1 – `HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="64dd2-123">**Listing 1 – `HomeController.vb`**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

<span data-ttu-id="64dd2-124">`Index()`方法显示`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="64dd2-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="64dd2-125">此方法将传递所有以前的客户反馈到`Index`通过 （使用 LINQ to SQL 查询） 从数据库检索反馈的视图。</span><span class="sxs-lookup"><span data-stu-id="64dd2-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="64dd2-126">`Create()`方法创建一个新的反馈项并将其添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="64dd2-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="64dd2-127">在窗体中输入客户的消息传递给`Create()`消息参数中的方法。</span><span class="sxs-lookup"><span data-stu-id="64dd2-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="64dd2-128">将创建一个反馈项和消息分配给反馈项`Message`属性。</span><span class="sxs-lookup"><span data-stu-id="64dd2-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="64dd2-129">反馈项提交到与数据库`DataContext.SubmitChanges()`方法调用。</span><span class="sxs-lookup"><span data-stu-id="64dd2-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="64dd2-130">最后，在距访客重定向回`Index`视图显示所有的反馈。</span><span class="sxs-lookup"><span data-stu-id="64dd2-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="64dd2-131">`Index`视图包含在清单 2。</span><span class="sxs-lookup"><span data-stu-id="64dd2-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="64dd2-132">**列出 2 – `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="64dd2-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

<span data-ttu-id="64dd2-133">`Index`视图具有两个部分。</span><span class="sxs-lookup"><span data-stu-id="64dd2-133">The `Index` view has two sections.</span></span> <span data-ttu-id="64dd2-134">顶部的部分包含的实际客户反馈表单。</span><span class="sxs-lookup"><span data-stu-id="64dd2-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="64dd2-135">下半部分包含一个 For...每个循环循环遍历所有以前的客户反馈项并显示每个反馈项的 EntryDate 和消息属性。</span><span class="sxs-lookup"><span data-stu-id="64dd2-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="64dd2-136">客户反馈网站是一个简单的网站。</span><span class="sxs-lookup"><span data-stu-id="64dd2-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="64dd2-137">遗憾的是，网站是 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="64dd2-138">假设在客户反馈表单中输入以下文本：</span><span class="sxs-lookup"><span data-stu-id="64dd2-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

<span data-ttu-id="64dd2-139">此文本表示显示警报消息框中的 JavaScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="64dd2-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="64dd2-140">某人为反馈提交此脚本后窗体中，消息<em>Boo ！</em>将显示时的任何人访问客户反馈网站将来 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="64dd2-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>


<span data-ttu-id="64dd2-141">[![JavaScript 注入](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="64dd2-141">[![JavaScript Injection](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span></span>

<span data-ttu-id="64dd2-142">**图 02**: JavaScript 注入 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="64dd2-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image6.png))</span></span>


<span data-ttu-id="64dd2-143">现在，您对 JavaScript 注入式攻击的初始响应可能 apathy。</span><span class="sxs-lookup"><span data-stu-id="64dd2-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="64dd2-144">您可能会认为 JavaScript 注入式攻击是只需一类型的*篡改*攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="64dd2-145">你可能会认为，没有人可以任何操作真正恶魔通过提交 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="64dd2-146">遗憾的是，黑客可以执行一些实际上，通过将 JavaScript 注入到网站的实际恶意操作。</span><span class="sxs-lookup"><span data-stu-id="64dd2-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="64dd2-147">JavaScript 注入攻击可用于执行跨站点脚本 (XSS) 攻击。</span><span class="sxs-lookup"><span data-stu-id="64dd2-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="64dd2-148">在跨站点脚本攻击中，你将窃取用户机密信息，并将信息发送到另一个网站。</span><span class="sxs-lookup"><span data-stu-id="64dd2-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="64dd2-149">例如，黑客可以使用 JavaScript 注入攻击来窃取来自其他用户的浏览器 cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="64dd2-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="64dd2-150">如果敏感信息-如密码、 信用卡号或身份证号 – 存储在浏览器 cookie，然后黑客可以使用 JavaScript 注入攻击来窃取此信息。</span><span class="sxs-lookup"><span data-stu-id="64dd2-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="64dd2-151">或者，如果用户在已受威胁与 JavaScript 攻击页中包含窗体字段中输入敏感信息，然后黑客可以使用插入的 JavaScript 获取窗体数据并将其发送到另一个网站。</span><span class="sxs-lookup"><span data-stu-id="64dd2-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="64dd2-152">*请将害怕*。</span><span class="sxs-lookup"><span data-stu-id="64dd2-152">*Please be scared*.</span></span> <span data-ttu-id="64dd2-153">认真对待 JavaScript 注入式攻击和保护用户的机密信息。</span><span class="sxs-lookup"><span data-stu-id="64dd2-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="64dd2-154">在接下来的两部分中，我们将讨论你可以使用来保护从 JavaScript 注入式攻击你的 ASP.NET MVC 应用程序的两种技术。</span><span class="sxs-lookup"><span data-stu-id="64dd2-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="64dd2-155">方法 #1: HTML 编码的视图中</span><span class="sxs-lookup"><span data-stu-id="64dd2-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="64dd2-156">一种阻止 JavaScript 注入攻击的简单方法是 html 编码在重新显示在视图中的数据时，网站用户输入的任何数据。</span><span class="sxs-lookup"><span data-stu-id="64dd2-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="64dd2-157">已更新`Index`列出 3 中的视图遵循这种方法。</span><span class="sxs-lookup"><span data-stu-id="64dd2-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="64dd2-158">**列出 3 – `Index.aspx` (HTML 编码)**</span><span class="sxs-lookup"><span data-stu-id="64dd2-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

<span data-ttu-id="64dd2-159">请注意，值`feedback.Message`为 HTML 编码之前的值显示替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="64dd2-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

<span data-ttu-id="64dd2-160">所带来的平均值为 HTML 编码字符串？</span><span class="sxs-lookup"><span data-stu-id="64dd2-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="64dd2-161">一个字符串进行编码时 HTML，危险字符如`<`和`>`如 HTML 实体引用替换为`&lt;`和`&gt;`。</span><span class="sxs-lookup"><span data-stu-id="64dd2-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="64dd2-162">因此，在字符串`<script>alert("Boo!")</script>`为 HTML 编码，它将转换为`&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。</span><span class="sxs-lookup"><span data-stu-id="64dd2-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="64dd2-163">为 JavaScript 脚本由浏览器解释时不再执行编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="64dd2-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="64dd2-164">相反，图 3 中获得无害的页。</span><span class="sxs-lookup"><span data-stu-id="64dd2-164">Instead, you get the harmless page in Figure 3.</span></span>


<span data-ttu-id="64dd2-165">[![失效的 JavaScript 攻击](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="64dd2-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span></span>

<span data-ttu-id="64dd2-166">**图 03**： 失效的 JavaScript 攻击 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="64dd2-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image9.png))</span></span>


<span data-ttu-id="64dd2-167">请注意，在`Index`查看列出 3 中的值`feedback.Message`进行编码。</span><span class="sxs-lookup"><span data-stu-id="64dd2-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="64dd2-168">值`feedback.EntryDate`未编码。</span><span class="sxs-lookup"><span data-stu-id="64dd2-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="64dd2-169">只需对用户输入的数据进行编码。</span><span class="sxs-lookup"><span data-stu-id="64dd2-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="64dd2-170">因为 EntryDate 的值在与控制器中生成时，你不需要为 HTML 编码此值。</span><span class="sxs-lookup"><span data-stu-id="64dd2-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="64dd2-171">方法 2： 在控制器中编码的 HTML</span><span class="sxs-lookup"><span data-stu-id="64dd2-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="64dd2-172">而不是 HTML 编码数据在视图中显示数据时，你可以 HTML 提交到数据库的数据之前对数据进行编码。</span><span class="sxs-lookup"><span data-stu-id="64dd2-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="64dd2-173">此第二种方法均的情况下`controller`列出 4 中。</span><span class="sxs-lookup"><span data-stu-id="64dd2-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="64dd2-174">**列出 4 – `HomeController.cs` (HTML 编码)**</span><span class="sxs-lookup"><span data-stu-id="64dd2-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

<span data-ttu-id="64dd2-175">请注意，消息的值是 HTML 编码值提交到该数据库在之前`Create()`操作。</span><span class="sxs-lookup"><span data-stu-id="64dd2-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="64dd2-176">当消息将重新显示在视图中时，消息为 HTML 编码，并且不执行任何插入的消息中的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="64dd2-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="64dd2-177">通常情况下，你应该倾向于通过此第二种方法在本教程中讨论的第一个方法。</span><span class="sxs-lookup"><span data-stu-id="64dd2-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="64dd2-178">此第二种方法的问题是，你结束，HTML 编码数据在数据库中。</span><span class="sxs-lookup"><span data-stu-id="64dd2-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="64dd2-179">换而言之，你数据库的数据是变脏与有趣查找的字符。</span><span class="sxs-lookup"><span data-stu-id="64dd2-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="64dd2-180">为什么这是错误的？</span><span class="sxs-lookup"><span data-stu-id="64dd2-180">Why is this bad?</span></span> <span data-ttu-id="64dd2-181">如果您需要在以外的网页中显示的数据库数据，则将遇到问题。</span><span class="sxs-lookup"><span data-stu-id="64dd2-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="64dd2-182">例如，可以在 Windows 窗体应用程序不再方便地显示数据。</span><span class="sxs-lookup"><span data-stu-id="64dd2-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="64dd2-183">总结</span><span class="sxs-lookup"><span data-stu-id="64dd2-183">Summary</span></span>

<span data-ttu-id="64dd2-184">本教程的目的是让你有关 JavaScript 注入攻击的潜在客户。</span><span class="sxs-lookup"><span data-stu-id="64dd2-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="64dd2-185">本教程讨论防护 JavaScript 注入式攻击 ASP.NET MVC 应用程序的两种方法： 可以是 HTML 编码用户提交中的视图或你的数据可以 HTML 编码用户提交在控制器中的数据。</span><span class="sxs-lookup"><span data-stu-id="64dd2-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="64dd2-186">上一篇</span><span class="sxs-lookup"><span data-stu-id="64dd2-186">Previous</span></span>](authenticating-users-with-windows-authentication-vb.md)
