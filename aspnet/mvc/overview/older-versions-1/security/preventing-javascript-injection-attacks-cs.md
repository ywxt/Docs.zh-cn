---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
title: 阻止 JavaScript 注入攻击 (C#) |Microsoft Docs
author: StephenWalther
description: 阻止 JavaScript 注入攻击和跨站点脚本攻击发生给你。 在本教程中，Stephen Walther 解释了如何轻松地 de...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d0136da6-81a4-4815-b002-baa84744c09e
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-cs
msc.type: authoredcontent
ms.openlocfilehash: 77d0f0346e9eff756cd74c64c310918f3c367ab1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823533"
---
<a name="preventing-javascript-injection-attacks-c"></a><span data-ttu-id="3704e-104">阻止 JavaScript 注入攻击 (C#)</span><span class="sxs-lookup"><span data-stu-id="3704e-104">Preventing JavaScript Injection Attacks (C#)</span></span>
====================
<span data-ttu-id="3704e-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="3704e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="3704e-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="3704e-106">Download PDF</span></span>](http://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_CS.pdf)

> <span data-ttu-id="3704e-107">阻止 JavaScript 注入攻击和跨站点脚本攻击发生给你。</span><span class="sxs-lookup"><span data-stu-id="3704e-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="3704e-108">在本教程中，Stephen Walther 解释了如何轻松地抵御这些类型的 html 编码内容的攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>


<span data-ttu-id="3704e-109">本教程的目的是说明如何在 ASP.NET MVC 应用程序中防止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="3704e-110">本教程讨论了两种方法可以保护你的网站对 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="3704e-111">了解如何防止 JavaScript 注入攻击进行编码，显示的数据。</span><span class="sxs-lookup"><span data-stu-id="3704e-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="3704e-112">你还了解如何进行编码的数据，即表示你接受阻止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="3704e-113">什么是 JavaScript 注入攻击？</span><span class="sxs-lookup"><span data-stu-id="3704e-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="3704e-114">无论何时接受用户输入并重新显示用户输入，打开你的网站到 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="3704e-115">让我们看一个具体的应用程序打开到 JavaScript 注入攻击的。</span><span class="sxs-lookup"><span data-stu-id="3704e-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="3704e-116">设想您创建了客户反馈网站 （参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="3704e-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="3704e-117">客户可以访问的网站，并输入他们使用您的产品的体验反馈。</span><span class="sxs-lookup"><span data-stu-id="3704e-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="3704e-118">当客户提交其反馈时，反馈将重新显示反馈页面上。</span><span class="sxs-lookup"><span data-stu-id="3704e-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>


<span data-ttu-id="3704e-119">[![客户反馈网站](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3704e-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-cs/_static/image2.png)](preventing-javascript-injection-attacks-cs/_static/image1.png)</span></span>

<span data-ttu-id="3704e-120">**图 01**： 客户反馈网站 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="3704e-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image3.png))</span></span>


<span data-ttu-id="3704e-121">客户反馈网站使用`controller`列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="3704e-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="3704e-122">这`controller`包含名为两个操作`Index()`和`Create()`。</span><span class="sxs-lookup"><span data-stu-id="3704e-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="3704e-123">**代码清单 1 – `HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="3704e-123">**Listing 1 – `HomeController.cs`**</span></span>

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample1.cs)]

<span data-ttu-id="3704e-124">`Index()`方法将显示`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="3704e-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="3704e-125">此方法将传递到以前的客户反馈的所有`Index`通过 （使用 LINQ to SQL 查询） 从数据库检索反馈的视图。</span><span class="sxs-lookup"><span data-stu-id="3704e-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="3704e-126">`Create()`方法创建新的反馈项并将其添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="3704e-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="3704e-127">在窗体中输入客户的消息传递给`Create()`消息参数中的方法。</span><span class="sxs-lookup"><span data-stu-id="3704e-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="3704e-128">创建了一个反馈项并将消息分配给反馈项目`Message`属性。</span><span class="sxs-lookup"><span data-stu-id="3704e-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="3704e-129">反馈项目提交到与数据库`DataContext.SubmitChanges()`方法调用。</span><span class="sxs-lookup"><span data-stu-id="3704e-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="3704e-130">最后，访问者被重定向回`Index`视图的所有反馈的显示位置。</span><span class="sxs-lookup"><span data-stu-id="3704e-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="3704e-131">`Index`视图包含在代码清单 2。</span><span class="sxs-lookup"><span data-stu-id="3704e-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="3704e-132">**代码清单 2 – `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="3704e-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample2.aspx)]

<span data-ttu-id="3704e-133">`Index`视图具有两个部分。</span><span class="sxs-lookup"><span data-stu-id="3704e-133">The `Index` view has two sections.</span></span> <span data-ttu-id="3704e-134">顶端部分包含实际的客户反馈窗体。</span><span class="sxs-lookup"><span data-stu-id="3704e-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="3704e-135">下半部分包含一个 For...每个循环，循环遍历所有以前的客户反馈项并显示每个反馈项目的 EntryDate 和消息属性。</span><span class="sxs-lookup"><span data-stu-id="3704e-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="3704e-136">客户反馈网站是一个简单的网站。</span><span class="sxs-lookup"><span data-stu-id="3704e-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="3704e-137">遗憾的是，该网站已打开到 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="3704e-138">假设在客户的反馈表单中输入以下文本：</span><span class="sxs-lookup"><span data-stu-id="3704e-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-cs/samples/sample3.html)]

<span data-ttu-id="3704e-139">此文本表示显示警告消息框的 JavaScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="3704e-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="3704e-140">有人将此脚本提交到反馈后窗体中，消息<em>Boo ！</em>将显示时的任何人访问客户反馈网站将来 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="3704e-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>


<span data-ttu-id="3704e-141">[![JavaScript 注入](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3704e-141">[![JavaScript Injection](preventing-javascript-injection-attacks-cs/_static/image5.png)](preventing-javascript-injection-attacks-cs/_static/image4.png)</span></span>

<span data-ttu-id="3704e-142">**图 02**: JavaScript 注入 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="3704e-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image6.png))</span></span>


<span data-ttu-id="3704e-143">现在，对 JavaScript 注入攻击的初始响应可能才自傲。</span><span class="sxs-lookup"><span data-stu-id="3704e-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="3704e-144">您可能认为 JavaScript 注入攻击是只是一种*篡改*攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="3704e-145">你可能会认为，没有人可以任何操作真正邪恶通过提交 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="3704e-146">遗憾的是，黑客可以执行一些真正，通过将 JavaScript 注入到网站的真正恶意操作。</span><span class="sxs-lookup"><span data-stu-id="3704e-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="3704e-147">JavaScript 注入攻击可用于执行跨站点脚本 (XSS) 攻击。</span><span class="sxs-lookup"><span data-stu-id="3704e-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="3704e-148">在跨站点脚本攻击中，您可以窃取用户机密信息并将信息发送到另一个网站。</span><span class="sxs-lookup"><span data-stu-id="3704e-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="3704e-149">例如，黑客可以使用 JavaScript 注入攻击来窃取其他用户的浏览器 cookie 的值。</span><span class="sxs-lookup"><span data-stu-id="3704e-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="3704e-150">如果在浏览器 cookie 中存储敏感信息，如密码、 信用卡号或社会安全号码 –，然后黑客可以使用 JavaScript 注入攻击来窃取此信息。</span><span class="sxs-lookup"><span data-stu-id="3704e-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="3704e-151">或者，如果用户在使用 JavaScript 攻击已遭到破坏的页中包含的窗体字段中输入的敏感信息，然后黑客可以使用注入的 JavaScript 来获取窗体数据并将其发送到另一个网站。</span><span class="sxs-lookup"><span data-stu-id="3704e-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="3704e-152">*请将被困难所吓倒*。</span><span class="sxs-lookup"><span data-stu-id="3704e-152">*Please be scared*.</span></span> <span data-ttu-id="3704e-153">JavaScript 注入攻击非常重视和保护用户的机密信息。</span><span class="sxs-lookup"><span data-stu-id="3704e-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="3704e-154">在接下来的两部分中，我们将讨论您可以使用来保护 ASP.NET MVC 应用程序从 JavaScript 注入攻击的两种方法。</span><span class="sxs-lookup"><span data-stu-id="3704e-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="3704e-155">方法 #1： 在视图中 HTML 编码</span><span class="sxs-lookup"><span data-stu-id="3704e-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="3704e-156">一个阻止 JavaScript 注入攻击的简单方法是以 html 格式进行编码时重新显示在视图中的数据由网站的用户输入的任何数据。</span><span class="sxs-lookup"><span data-stu-id="3704e-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="3704e-157">已更新`Index`清单 3 中的视图遵循这种方法。</span><span class="sxs-lookup"><span data-stu-id="3704e-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="3704e-158">**代码清单 3 – `Index.aspx` (HTML 编码)**</span><span class="sxs-lookup"><span data-stu-id="3704e-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample4.aspx)]

<span data-ttu-id="3704e-159">请注意，值`feedback.Message`是 HTML 编码之前使用以下代码显示的值：</span><span class="sxs-lookup"><span data-stu-id="3704e-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-cs/samples/sample5.aspx)]

<span data-ttu-id="3704e-160">它以 html 格式的平均值对字符串进行编码？</span><span class="sxs-lookup"><span data-stu-id="3704e-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="3704e-161">HTML 编码字符串，危险字符如`<`并`>`替换为 HTML 实体引用，如`&lt;`和`&gt;`。</span><span class="sxs-lookup"><span data-stu-id="3704e-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="3704e-162">因此，在将字符串`<script>alert("Boo!")</script>`是 HTML 编码，它将转换为`&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。</span><span class="sxs-lookup"><span data-stu-id="3704e-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="3704e-163">作为 JavaScript 脚本时由浏览器进行解释，不再执行编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="3704e-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="3704e-164">相反，图 3 中获得无害的页。</span><span class="sxs-lookup"><span data-stu-id="3704e-164">Instead, you get the harmless page in Figure 3.</span></span>


<span data-ttu-id="3704e-165">[![大大降低的 JavaScript 攻击](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="3704e-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-cs/_static/image8.png)](preventing-javascript-injection-attacks-cs/_static/image7.png)</span></span>

<span data-ttu-id="3704e-166">**图 03**： 大大降低 JavaScript 攻击 ([单击以查看实际尺寸的图像](preventing-javascript-injection-attacks-cs/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="3704e-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-cs/_static/image9.png))</span></span>


<span data-ttu-id="3704e-167">请注意，在`Index`查看清单 3 中的值`feedback.Message`进行编码。</span><span class="sxs-lookup"><span data-stu-id="3704e-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="3704e-168">值`feedback.EntryDate`不进行编码。</span><span class="sxs-lookup"><span data-stu-id="3704e-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="3704e-169">只需对用户输入的数据进行编码。</span><span class="sxs-lookup"><span data-stu-id="3704e-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="3704e-170">因为 EntryDate 的值在控制器中生成时，你不需要为 HTML 编码此值。</span><span class="sxs-lookup"><span data-stu-id="3704e-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="3704e-171">方法 2： 在控制器中编码的 HTML</span><span class="sxs-lookup"><span data-stu-id="3704e-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="3704e-172">而不是 HTML 编码的数据在视图中显示数据时，你可以 HTML 提交到数据库的数据之前对数据进行编码。</span><span class="sxs-lookup"><span data-stu-id="3704e-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="3704e-173">此第二种方法执行的情况下`controller`列表 4 中。</span><span class="sxs-lookup"><span data-stu-id="3704e-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="3704e-174">**列表 4 – `HomeController.cs` (HTML 编码)**</span><span class="sxs-lookup"><span data-stu-id="3704e-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-csharp[Main](preventing-javascript-injection-attacks-cs/samples/sample6.cs)]

<span data-ttu-id="3704e-175">请注意，消息的值是 HTML 编码，然后将值提交到该数据库在`Create()`操作。</span><span class="sxs-lookup"><span data-stu-id="3704e-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="3704e-176">当消息将重新显示在视图中时，消息是 HTML 编码，并且不执行消息中注入任何 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="3704e-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="3704e-177">通常情况下，你应更倾向于通过此第二种方法在本教程中讨论的第一个方法。</span><span class="sxs-lookup"><span data-stu-id="3704e-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="3704e-178">此第二种方法的问题是，您最终得到的 HTML 编码的数据在数据库中。</span><span class="sxs-lookup"><span data-stu-id="3704e-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="3704e-179">换而言之，你数据库的数据是变脏的有趣的外观字符。</span><span class="sxs-lookup"><span data-stu-id="3704e-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="3704e-180">为什么这是错误的？</span><span class="sxs-lookup"><span data-stu-id="3704e-180">Why is this bad?</span></span> <span data-ttu-id="3704e-181">如果您需要在 web 页面以外的内容中显示数据库数据，您将遇到问题。</span><span class="sxs-lookup"><span data-stu-id="3704e-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="3704e-182">例如，可以在 Windows 窗体应用程序中无法轻而易举地显示数据。</span><span class="sxs-lookup"><span data-stu-id="3704e-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="3704e-183">总结</span><span class="sxs-lookup"><span data-stu-id="3704e-183">Summary</span></span>

<span data-ttu-id="3704e-184">本教程的目的是被吓有关 JavaScript 注入攻击的潜在客户。</span><span class="sxs-lookup"><span data-stu-id="3704e-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="3704e-185">本教程中讨论过防御针对 JavaScript 注入攻击您的 ASP.NET MVC 应用程序的两种方法： 可以是 HTML 编码用户提交中的视图或你的数据可以 HTML 编码用户提交的控制器中的数据。</span><span class="sxs-lookup"><span data-stu-id="3704e-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3704e-186">[上一页](authenticating-users-with-windows-authentication-cs.md)
> [下一页](authenticating-users-with-forms-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3704e-186">[Previous](authenticating-users-with-windows-authentication-cs.md)
[Next](authenticating-users-with-forms-authentication-vb.md)</span></span>
