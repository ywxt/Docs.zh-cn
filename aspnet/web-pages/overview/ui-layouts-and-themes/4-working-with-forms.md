---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: "使用 ASP.NET Web 页 (Razor) 站点中的 HTML 窗体 |Microsoft 文档"
author: tfitzmac
description: "窗体是用户输入控件，如文本框、 复选框、 单选按钮和下拉列表的放置位置的 HTML 文档的节。 使用窗体疑问词..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/10/2014
ms.topic: article
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: 8579c444fd19d1a366349cc09f9f768de23055f8
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="3af10-104">使用 ASP.NET Web 页 (Razor) 站点中的 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="3af10-104">Working with HTML Forms in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="3af10-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="3af10-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="3af10-106">本文介绍如何处理 HTML 窗体 （使用文本框和按钮） 当你使用在 ASP.NET Web 页 (Razor) 网站中。</span><span class="sxs-lookup"><span data-stu-id="3af10-106">This article describes how to process an HTML form (with text boxes and buttons) when you are working in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="3af10-107">**你将学习：**</span><span class="sxs-lookup"><span data-stu-id="3af10-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="3af10-108">如何创建的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="3af10-108">How to create an HTML form.</span></span>
> - <span data-ttu-id="3af10-109">如何从窗体中读取用户输入。</span><span class="sxs-lookup"><span data-stu-id="3af10-109">How to read user input from the form.</span></span>
> - <span data-ttu-id="3af10-110">如何验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="3af10-110">How to validate user input.</span></span>
> - <span data-ttu-id="3af10-111">如何还原窗体值提交页面后。</span><span class="sxs-lookup"><span data-stu-id="3af10-111">How to restore form values after the page is submitted.</span></span>
> 
> <span data-ttu-id="3af10-112">这些是 ASP.NET 的文章中介绍的编程概念：</span><span class="sxs-lookup"><span data-stu-id="3af10-112">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="3af10-113">`Request` 对象。</span><span class="sxs-lookup"><span data-stu-id="3af10-113">The `Request` object.</span></span>
> - <span data-ttu-id="3af10-114">输入的验证。</span><span class="sxs-lookup"><span data-stu-id="3af10-114">Input validation.</span></span>
> - <span data-ttu-id="3af10-115">HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="3af10-115">HTML encoding.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3af10-116">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3af10-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="3af10-117">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="3af10-117">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="3af10-118">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="3af10-118">This tutorial also works with ASP.NET Web Pages 2.</span></span>


## <a name="creating-a-simple-html-form"></a><span data-ttu-id="3af10-119">创建简单的 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="3af10-119">Creating a Simple HTML Form</span></span>

1. <span data-ttu-id="3af10-120">创建新网站。</span><span class="sxs-lookup"><span data-stu-id="3af10-120">Create a new website.</span></span>
2. <span data-ttu-id="3af10-121">在根文件夹中，创建一个名为的 web 页*Form.cshtml*并输入以下标记：</span><span class="sxs-lookup"><span data-stu-id="3af10-121">In the root folder, create a web page named *Form.cshtml* and enter the following markup:</span></span>

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. <span data-ttu-id="3af10-122">启动你的浏览器中的页。</span><span class="sxs-lookup"><span data-stu-id="3af10-122">Launch the page in your browser.</span></span> <span data-ttu-id="3af10-123">(在 WebMatrix 中，在**文件**工作区中，右键单击该文件，然后选择**在浏览器中启动**。)一种简单形式具有三个输入字段和**提交**显示按钮。</span><span class="sxs-lookup"><span data-stu-id="3af10-123">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.) A simple form with three input fields and a **Submit** button is displayed.</span></span>

    ![带有三个文本框的窗体的屏幕截图。](4-working-with-forms/_static/image1.jpg)

    <span data-ttu-id="3af10-125">此时，如果你单击**提交**按钮时，会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="3af10-125">At this point, if you click the **Submit** button, nothing happens.</span></span> <span data-ttu-id="3af10-126">若要使表单有用，必须添加将在服务器运行某些代码。</span><span class="sxs-lookup"><span data-stu-id="3af10-126">To make the form useful, you have to add some code that will run on the server.</span></span>

## <a name="reading-user-input-from-the-form"></a><span data-ttu-id="3af10-127">从窗体中读取用户输入</span><span class="sxs-lookup"><span data-stu-id="3af10-127">Reading User Input from the Form</span></span>

<span data-ttu-id="3af10-128">若要处理窗体，你可以添加代码用于读取提交的字段值并进行某项操作它们。</span><span class="sxs-lookup"><span data-stu-id="3af10-128">To process the form, you add code that reads the submitted field values and does something with them.</span></span> <span data-ttu-id="3af10-129">此过程演示了如何读取的字段，并显示在页面上的用户输入。</span><span class="sxs-lookup"><span data-stu-id="3af10-129">This procedure shows you how to read the fields and display the user input on the page.</span></span> <span data-ttu-id="3af10-130">（在生产应用程序中，你通常执行更值得关注操作需要用户输入。</span><span class="sxs-lookup"><span data-stu-id="3af10-130">(In a production application, you generally do more interesting things with user input.</span></span> <span data-ttu-id="3af10-131">你将执行该操作中使用数据库有关的文章。）</span><span class="sxs-lookup"><span data-stu-id="3af10-131">You'll do that in the article about working with databases.)</span></span>

1. <span data-ttu-id="3af10-132">在顶部*Form.cshtml*文件中，输入以下代码：</span><span class="sxs-lookup"><span data-stu-id="3af10-132">At the top of the *Form.cshtml* file, enter the following code:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    <span data-ttu-id="3af10-133">当用户第一次请求页时，将显示仅空窗体。</span><span class="sxs-lookup"><span data-stu-id="3af10-133">When the user first requests the page, only the empty form is displayed.</span></span> <span data-ttu-id="3af10-134">（它将是你） 用户在填写窗体，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="3af10-134">The user (which will be you) fills in the form and then clicks **Submit**.</span></span> <span data-ttu-id="3af10-135">这将 (post) 提交到服务器的用户输入。</span><span class="sxs-lookup"><span data-stu-id="3af10-135">This submits (posts) the user input to the server.</span></span> <span data-ttu-id="3af10-136">默认情况下，请求将转到同一页 (即*Form.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="3af10-136">By default, the request goes to the same page (namely, *Form.cshtml*).</span></span>

    <span data-ttu-id="3af10-137">当提交页面此时，窗体的正上方显示你输入的值：</span><span class="sxs-lookup"><span data-stu-id="3af10-137">When you submit the page this time, the values you entered are displayed just above the form:</span></span>

    ![显示页面上显示您输入的值的屏幕截图。](4-working-with-forms/_static/image2.jpg)

    <span data-ttu-id="3af10-139">查看页的代码。</span><span class="sxs-lookup"><span data-stu-id="3af10-139">Look at the code for the page.</span></span> <span data-ttu-id="3af10-140">首次使用`IsPost`方法来确定是否正在发页面 &#8212; 也就是说，用户单击按钮是否**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="3af10-140">You first use the `IsPost` method to determine whether the page is being posted &#8212; that is, whether a user clicked the **Submit** button.</span></span> <span data-ttu-id="3af10-141">如果这是 post， `IsPost` ，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="3af10-141">If this is a post, `IsPost` returns true.</span></span> <span data-ttu-id="3af10-142">这是标准方法中的 ASP.NET Web Pages 以确定是否你正在使用的初始请求 （GET 请求） 或回发 （POST 请求）。</span><span class="sxs-lookup"><span data-stu-id="3af10-142">This is the standard way in ASP.NET Web Pages to determine whether you're working with an initial request (a GET request) or a postback (a POST request).</span></span> <span data-ttu-id="3af10-143">(有关 GET 和 POST 的详细信息，请参阅"HTTP GET 和 POST 和 IsPost 属性的"边栏中[ASP.NET 网页编程使用 Razor 语法的简介](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)。)</span><span class="sxs-lookup"><span data-stu-id="3af10-143">(For more information about GET and POST, see the sidebar "HTTP GET and POST and the IsPost Property" in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span></span>

    <span data-ttu-id="3af10-144">接下来，获取从用户填充的值`Request.Form`对象，并且你将它们放在变量为更高版本。</span><span class="sxs-lookup"><span data-stu-id="3af10-144">Next, you get the values that the user filled in from the `Request.Form` object, and you put them in variables for later.</span></span> <span data-ttu-id="3af10-145">`Request.Form`对象包含所有已提交的页面中，每个键标识的值。</span><span class="sxs-lookup"><span data-stu-id="3af10-145">The `Request.Form` object contains all the values that were submitted with the page, each identified by a key.</span></span> <span data-ttu-id="3af10-146">键是等效于`name`你想要读取的表单域的属性。</span><span class="sxs-lookup"><span data-stu-id="3af10-146">The key is the equivalent to the `name` attribute of the form field that you want to read.</span></span> <span data-ttu-id="3af10-147">例如，若要读取`companyname`字段 （文本框中），你使用`Request.Form["companyname"]`。</span><span class="sxs-lookup"><span data-stu-id="3af10-147">For example, to read the `companyname` field (text box), you use `Request.Form["companyname"]`.</span></span>

    <span data-ttu-id="3af10-148">窗体值存储在`Request.Form`对象作为字符串。</span><span class="sxs-lookup"><span data-stu-id="3af10-148">Form values are stored in the `Request.Form` object as strings.</span></span> <span data-ttu-id="3af10-149">因此，你必须使用与数字、 日期或某些其他类型的一个值，必须将其从字符串转换为该类型。</span><span class="sxs-lookup"><span data-stu-id="3af10-149">Therefore, when you have to work with a value as a number or a date or some other type, you have to convert it from a string to that type.</span></span> <span data-ttu-id="3af10-150">在示例中，`AsInt`方法`Request.Form`用于将员工字段 （其中包含员工计数） 的值转换为整数。</span><span class="sxs-lookup"><span data-stu-id="3af10-150">In the example, the `AsInt` method of the `Request.Form` is used to convert the value of the employees field (which contains an employee count) to an integer.</span></span>
2. <span data-ttu-id="3af10-151">启动你的浏览器中的页、 填充窗体字段中，并单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="3af10-151">Launch the page in your browser, fill in the form fields, and click **Submit**.</span></span> <span data-ttu-id="3af10-152">页面显示您输入的值。</span><span class="sxs-lookup"><span data-stu-id="3af10-152">The page displays the values you entered.</span></span>

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a><span data-ttu-id="3af10-153">HTML 编码的外观和安全</span><span class="sxs-lookup"><span data-stu-id="3af10-153">HTML Encoding for Appearance and Security</span></span>
> 
> <span data-ttu-id="3af10-154">HTML 有特殊字符，如用于`<`， `>`，和`&`。</span><span class="sxs-lookup"><span data-stu-id="3af10-154">HTML has special uses for characters like `<`, `>`, and `&`.</span></span> <span data-ttu-id="3af10-155">如果这些特殊字符出现不认为它们不其中，他们可以破坏的外观和功能的网页。</span><span class="sxs-lookup"><span data-stu-id="3af10-155">If these special characters appear where they're not expected, they can ruin the appearance and functionality of your web page.</span></span> <span data-ttu-id="3af10-156">例如，浏览器解释`<`愿意为 HTML 元素，开始字符 （除非它后面跟一个空格）`<b>`或`<input ...>`。</span><span class="sxs-lookup"><span data-stu-id="3af10-156">For example, the browser interprets the `<` character (unless it's followed by a space) as the beginning of an HTML element, like `<b>` or `<input ...>`.</span></span> <span data-ttu-id="3af10-157">如果浏览器无法识别的元素，它只需放弃开头的字符串`<`直至其达到的内容，它将再次识别。</span><span class="sxs-lookup"><span data-stu-id="3af10-157">If the browser doesn't recognize the element, it simply discards the string that begins with `<` until it reaches something that it again recognizes.</span></span> <span data-ttu-id="3af10-158">显然，这可能导致某些太怪异呈现在页中。</span><span class="sxs-lookup"><span data-stu-id="3af10-158">Obviously, this can result in some weird rendering in the page.</span></span>
> 
> <span data-ttu-id="3af10-159">HTML 编码用浏览器将解释为正确的符号的代码替换以下保留的字符。</span><span class="sxs-lookup"><span data-stu-id="3af10-159">HTML encoding replaces these reserved characters with a code that browsers interpret as the correct symbol.</span></span> <span data-ttu-id="3af10-160">例如，`<`字符替换`&lt;`和`>`字符替换`&gt;`。</span><span class="sxs-lookup"><span data-stu-id="3af10-160">For example, the `<` character is replaced with `&lt;` and the `>` character is replaced with `&gt;`.</span></span> <span data-ttu-id="3af10-161">浏览器呈现的字符，你想要查看这些替换字符串。</span><span class="sxs-lookup"><span data-stu-id="3af10-161">The browser renders these replacement strings as the characters that you want to see.</span></span>
> 
> <span data-ttu-id="3af10-162">它是使用 HTML 编码显示字符串的任何时间 （输入） 你从用户获取一个好主意。</span><span class="sxs-lookup"><span data-stu-id="3af10-162">It's a good idea to use HTML encoding any time you display strings (input) that you got from a user.</span></span> <span data-ttu-id="3af10-163">如果没有，用户可尝试获取你 web 页后，可以运行恶意脚本或做其他事情这影响了你站点的安全或不想。</span><span class="sxs-lookup"><span data-stu-id="3af10-163">If you don't, a user can try to get your web page to run a malicious script or do something else that compromises your site security or that's just not what you intend.</span></span> <span data-ttu-id="3af10-164">（这一点特别重要，如果你需要较长用户输入，将其存储某个地方，，然后显示其更高版本 &#8212; 例如，博客注释，作为用户查看，或类似的。）</span><span class="sxs-lookup"><span data-stu-id="3af10-164">(This is particularly important if you take user input, store it someplace, and then display it later &#8212; for example, as a blog comment, user review, or something like that.)</span></span>
> 
> <span data-ttu-id="3af10-165">为了帮助防止这些问题，ASP.NET 网页自动进行 HTML 编码的任何文本内容，您在代码中输出。</span><span class="sxs-lookup"><span data-stu-id="3af10-165">To help prevent these problems, ASP.NET Web Pages automatically HTML-encodes any text content that you output from your code.</span></span> <span data-ttu-id="3af10-166">例如，当你显示变量或使用代码类似于的表达式的内容时，才`@MyVar`，ASP.NET 网页自动对输出进行编码。</span><span class="sxs-lookup"><span data-stu-id="3af10-166">For example, when you display the content of a variable or an expression using code such as `@MyVar`, ASP.NET Web Pages automatically encodes the output.</span></span>


## <a name="validating-user-input"></a><span data-ttu-id="3af10-167">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="3af10-167">Validating User Input</span></span>

<span data-ttu-id="3af10-168">用户犯的错误。</span><span class="sxs-lookup"><span data-stu-id="3af10-168">Users make mistakes.</span></span> <span data-ttu-id="3af10-169">要求他们填写字段，并在忘记，或要求其输入的雇员数和它们而是键入的名称。</span><span class="sxs-lookup"><span data-stu-id="3af10-169">You ask them to fill in a field, and they forget to, or you ask them to enter the number of employees and they type a name instead.</span></span> <span data-ttu-id="3af10-170">若要确保，窗体具有已正确填写处理它之前，你可以验证用户的输入。</span><span class="sxs-lookup"><span data-stu-id="3af10-170">To make sure that a form has been filled in correctly before you process it, you validate the user's input.</span></span>

<span data-ttu-id="3af10-171">此过程演示如何验证所有三个窗体字段，以确保用户未将其留空。</span><span class="sxs-lookup"><span data-stu-id="3af10-171">This procedure shows how to validate all three form fields to make sure the user didn't leave them blank.</span></span> <span data-ttu-id="3af10-172">你还检查员工计数值是一个数字。</span><span class="sxs-lookup"><span data-stu-id="3af10-172">You also check that the employee count value is a number.</span></span> <span data-ttu-id="3af10-173">如果不存在错误，则将显示错误消息，告诉用户哪些值未通过验证。</span><span class="sxs-lookup"><span data-stu-id="3af10-173">If there are errors, you'll display an error message that tells the user what values didn't pass validation.</span></span>

1. <span data-ttu-id="3af10-174">在*Form.cshtml*文件中，将第一个代码块替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="3af10-174">In the *Form.cshtml* file, replace the first block of code with the following code:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    <span data-ttu-id="3af10-175">若要验证用户输入，你可以使用`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="3af10-175">To validate user input, you use the `Validation` helper.</span></span> <span data-ttu-id="3af10-176">通过调用注册必填的字段`Validation.RequireField`。</span><span class="sxs-lookup"><span data-stu-id="3af10-176">You register required fields by calling `Validation.RequireField`.</span></span> <span data-ttu-id="3af10-177">通过调用注册其他类型的验证`Validation.Add`，并指定要验证的字段和要执行的验证类型。</span><span class="sxs-lookup"><span data-stu-id="3af10-177">You register other types of validation by calling `Validation.Add` and specifying the field to validate and the type of validation to perform.</span></span>

    <span data-ttu-id="3af10-178">页运行时，ASP.NET 将执行为你的所有验证。</span><span class="sxs-lookup"><span data-stu-id="3af10-178">When the page runs, ASP.NET does all the validation for you.</span></span> <span data-ttu-id="3af10-179">你可以通过调用检查结果`Validation.IsValid`，它返回的所有内容传递如果为 true 和 false 如果验证失败的任何字段。</span><span class="sxs-lookup"><span data-stu-id="3af10-179">You can check the results by calling `Validation.IsValid`, which returns true if everything passed and false if any field failed validation.</span></span> <span data-ttu-id="3af10-180">通常，你可以调用`Validation.IsValid`输入对用户执行任何处理之前。</span><span class="sxs-lookup"><span data-stu-id="3af10-180">Typically, you call `Validation.IsValid` before you perform any processing on the user input.</span></span>
2. <span data-ttu-id="3af10-181">更新`<body>`元素通过添加的三个调用`Html.ValidationMessage`方法，如下：</span><span class="sxs-lookup"><span data-stu-id="3af10-181">Update the `<body>` element by adding three calls to the `Html.ValidationMessage` method, like this:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    <span data-ttu-id="3af10-182">若要显示验证错误消息，你可以调用 Html。`ValidationMessage`</span><span class="sxs-lookup"><span data-stu-id="3af10-182">To display validation error messages, you can call Html.`ValidationMessage`</span></span> <span data-ttu-id="3af10-183">并将其传递所需的消息的字段的名称。</span><span class="sxs-lookup"><span data-stu-id="3af10-183">and pass it the name of the field that you want the message for.</span></span>
3. <span data-ttu-id="3af10-184">运行页面。</span><span class="sxs-lookup"><span data-stu-id="3af10-184">Run the page.</span></span> <span data-ttu-id="3af10-185">将字段留空并单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="3af10-185">Leave the fields blank and click **Submit**.</span></span> <span data-ttu-id="3af10-186">你看到错误消息。</span><span class="sxs-lookup"><span data-stu-id="3af10-186">You see error messages.</span></span>

    ![显示显示的错误消息，是否用户输入未通过验证的屏幕截图。](4-working-with-forms/_static/image3.jpg)
4. <span data-ttu-id="3af10-188">将字符串 (例如，"ABC") 添加到**员工计数**字段，然后单击**提交**试。</span><span class="sxs-lookup"><span data-stu-id="3af10-188">Add a string (for example, "ABC") to the **Employee Count** field and click **Submit** again.</span></span> <span data-ttu-id="3af10-189">你看到错误，该值指示此时间字符串未采用正确的格式，即一个整数。</span><span class="sxs-lookup"><span data-stu-id="3af10-189">This time you see an error that indicates that the string isn't in the right format, namely, an integer.</span></span>

    ![显示用户是否输入字符串为员工字段显示的错误消息的屏幕截图。](4-working-with-forms/_static/image4.jpg)

<span data-ttu-id="3af10-191">ASP.NET Web 页提供了更多用于验证用户输入，包括能够自动执行验证使用客户端脚本，以便用户在浏览器中获取的即时反馈选项。</span><span class="sxs-lookup"><span data-stu-id="3af10-191">ASP.NET Web Pages provides more options for validating user input, including the ability to automatically perform validation using client script, so that users get immediate feedback in the browser.</span></span> <span data-ttu-id="3af10-192">请参阅[其他资源](#Additional_Resources)更高版本的详细信息的部分。</span><span class="sxs-lookup"><span data-stu-id="3af10-192">See the [Additional Resources](#Additional_Resources) section later for more information.</span></span>

## <a name="restoring-form-values-after-postbacks"></a><span data-ttu-id="3af10-193">在回发后还原窗体值</span><span class="sxs-lookup"><span data-stu-id="3af10-193">Restoring Form Values After Postbacks</span></span>

<span data-ttu-id="3af10-194">在上一节中测试页面，你可能已注意到，如果有验证错误，输入 （而不仅仅是无效的数据） 的所有内容已消失，并且你必须重新输入的所有字段的值。</span><span class="sxs-lookup"><span data-stu-id="3af10-194">When you tested the page in the previous section, you might have noticed that if you had a validation error, everything you entered (not just the invalid data) was gone, and you had to re-enter values for all the fields.</span></span> <span data-ttu-id="3af10-195">这说明了重要的一点： 提交页面，其进行处理，并随后再次呈现页时都会从头重新创建此页面。</span><span class="sxs-lookup"><span data-stu-id="3af10-195">This illustrates an important point: when you submit a page, process it, and then render the page again, the page is re-created from scratch.</span></span> <span data-ttu-id="3af10-196">如你所看到的这意味着时提交页中的所有值都都会丢失。</span><span class="sxs-lookup"><span data-stu-id="3af10-196">As you saw, this means that any values that were in the page when it was submitted are lost.</span></span>

<span data-ttu-id="3af10-197">你可以解决此问题，但是。</span><span class="sxs-lookup"><span data-stu-id="3af10-197">You can fix this easily, however.</span></span> <span data-ttu-id="3af10-198">您有权访问已提交的值 (在`Request.Form`对象，因此你可以返回到窗体的字段中填充这些值，当呈现页面。</span><span class="sxs-lookup"><span data-stu-id="3af10-198">You have access to the values that were submitted (in the `Request.Form` object, so you can fill those values back into the form fields when the page is rendered.</span></span>

1. <span data-ttu-id="3af10-199">在*Form.cshtml*文件中，将`value`属性`<input>`元素使用`value`属性。:</span><span class="sxs-lookup"><span data-stu-id="3af10-199">In the *Form.cshtml* file, replace the `value` attributes of the `<input>` elements using the `value` attribute.:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    <span data-ttu-id="3af10-200">`value`属性`<input>`元素已设置为动态读取字段值外的`Request.Form`对象。</span><span class="sxs-lookup"><span data-stu-id="3af10-200">The `value` attribute of the `<input>` elements has been set to dynamically read the field value out of the `Request.Form` object.</span></span> <span data-ttu-id="3af10-201">第一次请求页时中的值`Request.Form`对象均是空。</span><span class="sxs-lookup"><span data-stu-id="3af10-201">The first time that the page is requested, the values in the `Request.Form` object are all empty.</span></span> <span data-ttu-id="3af10-202">这没什么关系，因为这样的形式是空白。</span><span class="sxs-lookup"><span data-stu-id="3af10-202">This is fine, because that way the form is blank.</span></span>
2. <span data-ttu-id="3af10-203">启动你的浏览器中，填写窗体字段或将其留空，然后单击**提交**。</span><span class="sxs-lookup"><span data-stu-id="3af10-203">Launch the page in your browser, fill in the form fields or leave them blank, and click **Submit**.</span></span> <span data-ttu-id="3af10-204">将显示页面，其中显示已提交的值。</span><span class="sxs-lookup"><span data-stu-id="3af10-204">A page that shows the submitted values is displayed.</span></span>

    ![forms-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="3af10-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="3af10-206">Additional Resources</span></span>

- [<span data-ttu-id="3af10-207">从 Web 用户获取输入另外 1001 方法</span><span class="sxs-lookup"><span data-stu-id="3af10-207">1,001 Ways to Get Input from Web Users</span></span>](https://msdn.microsoft.com/library/ms971057.aspx)
- <span data-ttu-id="3af10-208">[使用窗体和处理用户输入](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span><span class="sxs-lookup"><span data-stu-id="3af10-208">[Using Forms and Processing User Input](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span></span>
- [<span data-ttu-id="3af10-209">在 ASP.NET 网站中验证用户输入</span><span class="sxs-lookup"><span data-stu-id="3af10-209">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
- <span data-ttu-id="3af10-210">[在 HTML 窗体中使用自动完成](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="3af10-210">[Using AutoComplete in HTML Forms](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span></span>
