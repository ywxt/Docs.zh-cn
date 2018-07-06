---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 验证用户输入在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何验证的信息从用户获取&mdash;，即以确保用户输入有效信息在 HTML 窗体中另存为...
ms.author: aspnetcontent
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: d412f3fa4ca144a8a9107c971279f7bf2663cfe5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819255"
---
<a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="41542-103">ASP.NET Web Pages (Razor) 站点中验证用户输入</span><span class="sxs-lookup"><span data-stu-id="41542-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="41542-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="41542-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="41542-105">本文介绍如何验证的信息从用户获取&mdash;即，以确保用户输入有效信息以 html 格式窗体在 ASP.NET Web Pages (Razor) 站点中。</span><span class="sxs-lookup"><span data-stu-id="41542-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="41542-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="41542-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="41542-107">如何检查用户的输入与你定义的验证条件匹配。</span><span class="sxs-lookup"><span data-stu-id="41542-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="41542-108">如何确定是否已通过所有验证测试。</span><span class="sxs-lookup"><span data-stu-id="41542-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="41542-109">如何显示验证错误 （以及如何对其进行格式）。</span><span class="sxs-lookup"><span data-stu-id="41542-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="41542-110">如何验证不会直接来自用户的数据。</span><span class="sxs-lookup"><span data-stu-id="41542-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="41542-111">这些是 ASP.NET 编程一文中介绍的概念：</span><span class="sxs-lookup"><span data-stu-id="41542-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="41542-112">`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="41542-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="41542-113">`Html.ValidationSummary`和`Html.ValidationMessage`方法。</span><span class="sxs-lookup"><span data-stu-id="41542-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="41542-114">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="41542-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="41542-115">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="41542-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="41542-116">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="41542-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="41542-117">本文包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="41542-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="41542-118">用户输入验证的概述</span><span class="sxs-lookup"><span data-stu-id="41542-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="41542-119">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="41542-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="41542-120">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="41542-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="41542-121">格式设置验证错误</span><span class="sxs-lookup"><span data-stu-id="41542-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="41542-122">验证不会直接来自用户的数据</span><span class="sxs-lookup"><span data-stu-id="41542-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="41542-123">用户输入验证的概述</span><span class="sxs-lookup"><span data-stu-id="41542-123">Overview of User Input Validation</span></span>

<span data-ttu-id="41542-124">如果要求用户在页面中输入的信息 — 例如，到窗体，务必要确保他们输入的值有效。</span><span class="sxs-lookup"><span data-stu-id="41542-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="41542-125">例如，您不想处理缺少的关键信息的窗体。</span><span class="sxs-lookup"><span data-stu-id="41542-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="41542-126">当用户向 HTML 窗体中输入值时，则他们输入的值是字符串。</span><span class="sxs-lookup"><span data-stu-id="41542-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="41542-127">在许多情况下，所需的值是某些其他数据类型，如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="41542-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="41542-128">因此，您还需要确保用户输入的值可以正确地转换为适当的数据类型。</span><span class="sxs-lookup"><span data-stu-id="41542-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="41542-129">此外可能的值具有某些限制。</span><span class="sxs-lookup"><span data-stu-id="41542-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="41542-130">即使用户正确输入一个整数，例如，您可能需要确保该值所属的特定范围内。</span><span class="sxs-lookup"><span data-stu-id="41542-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="41542-132">**重要**验证用户输入也很重要的安全。</span><span class="sxs-lookup"><span data-stu-id="41542-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="41542-133">如果你限制用户可以在窗体中输入的值，则可以减少人可以输入一个值，可能损害您的网站的安全性的机会。</span><span class="sxs-lookup"><span data-stu-id="41542-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>


<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="41542-134">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="41542-134">Validating User Input</span></span>

<span data-ttu-id="41542-135">在 ASP.NET Web Pages 2 中，可以使用`Validator`帮助程序来测试用户输入。</span><span class="sxs-lookup"><span data-stu-id="41542-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="41542-136">基本的方法是执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="41542-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="41542-137">确定哪个输入你想要验证的元素 （字段）。</span><span class="sxs-lookup"><span data-stu-id="41542-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="41542-138">通常验证中的值`<input>`窗体中的元素。</span><span class="sxs-lookup"><span data-stu-id="41542-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="41542-139">但是，它是一个好办法验证所有输入，即使输入来自受约束的元素，如`<select>`列表。</span><span class="sxs-lookup"><span data-stu-id="41542-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="41542-140">这有助于确保用户不绕过页面上的控件和提交窗体。</span><span class="sxs-lookup"><span data-stu-id="41542-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="41542-141">对于每个输入元素使用的方法，则在网页代码中，添加各自的验证检查`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="41542-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="41542-142">若要检查的必填字段，请使用`Validation.RequireField(field, [error message])`（适用于单个字段） 或`Validation.RequireFields(field1, field2, ...))`（有关字段的列表）。</span><span class="sxs-lookup"><span data-stu-id="41542-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="41542-143">对于其他类型的验证，请使用`Validation.Add(field, ValidationType)`。</span><span class="sxs-lookup"><span data-stu-id="41542-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="41542-144">有关`ValidationType`，可以使用这些选项：</span><span class="sxs-lookup"><span data-stu-id="41542-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="41542-145">提交页面后，检查是否通过验证后通过检查`Validation.IsValid`:</span><span class="sxs-lookup"><span data-stu-id="41542-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="41542-146">如果有任何验证错误，则跳过正常页面处理。</span><span class="sxs-lookup"><span data-stu-id="41542-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="41542-147">例如，如果页面的目的是用于更新数据库，就不必这么做直到修复了所有验证错误。</span><span class="sxs-lookup"><span data-stu-id="41542-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="41542-148">如果验证错误，错误消息中显示页面的标记使用`Html.ValidationSummary`或`Html.ValidationMessage`，和 / 或。</span><span class="sxs-lookup"><span data-stu-id="41542-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="41542-149">下面的示例显示了一个页面，说明了这些步骤。</span><span class="sxs-lookup"><span data-stu-id="41542-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="41542-150">若要查看验证的工作原理，请运行此页并故意犯的错误。</span><span class="sxs-lookup"><span data-stu-id="41542-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="41542-151">例如，下面是什么如果您忘记输入门课程的名称，如果输入网页的外观，并且如果输入无效的日期：</span><span class="sxs-lookup"><span data-stu-id="41542-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![在呈现的页面中的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="41542-153">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="41542-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="41542-154">默认情况下，用户输入进行验证，在用户提交页面后，即，在服务器代码中执行验证。</span><span class="sxs-lookup"><span data-stu-id="41542-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="41542-155">此方法的缺点是用户不知道它们已进行了错误直到后它们提交该页面。</span><span class="sxs-lookup"><span data-stu-id="41542-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="41542-156">如果窗体是长或者过于复杂，只有在提交页面后报告的错误可能会给用户带来不便。</span><span class="sxs-lookup"><span data-stu-id="41542-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="41542-157">可以添加支持以在客户端脚本中执行验证。</span><span class="sxs-lookup"><span data-stu-id="41542-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="41542-158">在这种情况下，用户在处理在浏览器中，将执行验证。</span><span class="sxs-lookup"><span data-stu-id="41542-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="41542-159">例如，假设您指定一个值应为整数。</span><span class="sxs-lookup"><span data-stu-id="41542-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="41542-160">如果用户输入一个非整数值，用户离开在输入字段时，会报告错误。</span><span class="sxs-lookup"><span data-stu-id="41542-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="41542-161">用户获得即时反馈，便于在它们。</span><span class="sxs-lookup"><span data-stu-id="41542-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="41542-162">基于客户端验证还可以减少用户必须提交表格，以更正多个错误的次数。</span><span class="sxs-lookup"><span data-stu-id="41542-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="41542-163">即使使用客户端验证时，始终还在服务器代码中执行验证。</span><span class="sxs-lookup"><span data-stu-id="41542-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="41542-164">在服务器代码中执行验证是一种安全措施，以防用户绕过基于客户端验证。</span><span class="sxs-lookup"><span data-stu-id="41542-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>


1. <span data-ttu-id="41542-165">在页面中注册以下 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="41542-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="41542-166">两个库是从内容传送网络 (CDN)，可加载的因此您不必对您的计算机或服务器。</span><span class="sxs-lookup"><span data-stu-id="41542-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="41542-167">但是，必须具有的本地副本*jquery.validate.unobtrusive.js*。</span><span class="sxs-lookup"><span data-stu-id="41542-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="41542-168">如果你没有已使用 WebMatrix 模板 (如**入门网站**) 包含在库中，创建基于 Web Pages 站点**入门网站**。</span><span class="sxs-lookup"><span data-stu-id="41542-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="41542-169">然后将复制 *.js*到当前站点的文件。</span><span class="sxs-lookup"><span data-stu-id="41542-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="41542-170">在标记中，为你在验证每个元素添加到调用`Validation.For(field)`。</span><span class="sxs-lookup"><span data-stu-id="41542-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="41542-171">此方法会发出使用的客户端验证的属性。</span><span class="sxs-lookup"><span data-stu-id="41542-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="41542-172">(而不是发出实际 JavaScript 代码时，该方法发出之类的属性`data-val-...`。</span><span class="sxs-lookup"><span data-stu-id="41542-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="41542-173">这些属性支持使用 jQuery 来执行工作的非介入式客户端验证）。</span><span class="sxs-lookup"><span data-stu-id="41542-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="41542-174">以下页面显示了如何将客户端验证功能添加到前面所示的示例。</span><span class="sxs-lookup"><span data-stu-id="41542-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="41542-175">并非所有客户端上运行的验证检查。</span><span class="sxs-lookup"><span data-stu-id="41542-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="41542-176">具体而言，数据类型验证 （整数、 日期等） 不在客户端上运行。</span><span class="sxs-lookup"><span data-stu-id="41542-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="41542-177">客户端和服务器上工作的以下检查：</span><span class="sxs-lookup"><span data-stu-id="41542-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="41542-178">在此示例中，是有效的日期的测试中的客户端代码不起作用。</span><span class="sxs-lookup"><span data-stu-id="41542-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="41542-179">但是，将在服务器代码中执行测试。</span><span class="sxs-lookup"><span data-stu-id="41542-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="41542-180">格式设置验证错误</span><span class="sxs-lookup"><span data-stu-id="41542-180">Formatting Validation Errors</span></span>

<span data-ttu-id="41542-181">您可以控制定义 CSS 类具有以下保留的名称的显示验证错误：</span><span class="sxs-lookup"><span data-stu-id="41542-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="41542-182">`field-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="41542-182">`field-validation-error`.</span></span> <span data-ttu-id="41542-183">定义的输出`Html.ValidationMessage`方法时显示错误。</span><span class="sxs-lookup"><span data-stu-id="41542-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="41542-184">`field-validation-valid`。</span><span class="sxs-lookup"><span data-stu-id="41542-184">`field-validation-valid`.</span></span> <span data-ttu-id="41542-185">定义的输出`Html.ValidationMessage`方法时没有错误。</span><span class="sxs-lookup"><span data-stu-id="41542-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="41542-186">`input-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="41542-186">`input-validation-error`.</span></span> <span data-ttu-id="41542-187">定义如何`<input>`元素呈现时出错。</span><span class="sxs-lookup"><span data-stu-id="41542-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="41542-188">(例如，可以使用此类设置的背景色&lt;输入&gt;为不同的颜色，如果其值为无效的元素。)仅在客户端验证 （在 ASP.NET Web Pages 2) 中使用此 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="41542-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="41542-189">`input-validation-valid`。</span><span class="sxs-lookup"><span data-stu-id="41542-189">`input-validation-valid`.</span></span> <span data-ttu-id="41542-190">定义的外观`<input>`元素时没有错误。</span><span class="sxs-lookup"><span data-stu-id="41542-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="41542-191">`validation-summary-errors`。</span><span class="sxs-lookup"><span data-stu-id="41542-191">`validation-summary-errors`.</span></span> <span data-ttu-id="41542-192">定义的输出`Html.ValidationSummary`方法，它显示错误的列表。</span><span class="sxs-lookup"><span data-stu-id="41542-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="41542-193">`validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="41542-193">`validation-summary-valid`.</span></span> <span data-ttu-id="41542-194">定义的输出`Html.ValidationSummary`方法时没有错误。</span><span class="sxs-lookup"><span data-stu-id="41542-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="41542-195">以下`<style>`块显示了错误条件的规则。</span><span class="sxs-lookup"><span data-stu-id="41542-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="41542-196">如果在从本文前面的示例页中包含此样式块，错误显示的外观将类似于下图：</span><span class="sxs-lookup"><span data-stu-id="41542-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="41542-198">如果您在 ASP.NET Web Pages 2 中不使用客户端验证的 CSS 类的`<input>`元素 (`input-validation-error`和`input-validation-valid`不产生任何影响。</span><span class="sxs-lookup"><span data-stu-id="41542-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>


### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="41542-199">静态和动态错误显示</span><span class="sxs-lookup"><span data-stu-id="41542-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="41542-200">CSS 规则成对出现，如`validation-summary-errors`和`validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="41542-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="41542-201">这些对允许你定义的两个条件规则： 一个错误条件和"正常"（非错误） 条件。</span><span class="sxs-lookup"><span data-stu-id="41542-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="41542-202">请务必了解，始终呈现错误显示的标记时，即使没有任何错误。</span><span class="sxs-lookup"><span data-stu-id="41542-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="41542-203">例如，如果页面具有`Html.ValidationSummary`标记中的方法，即使在第一次请求页面时，页面源文件将包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="41542-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="41542-204">换而言之，`Html.ValidationSummary`方法将始终呈现`<div>`元素和一个列表，即使错误列表为空。</span><span class="sxs-lookup"><span data-stu-id="41542-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="41542-205">同样，`Html.ValidationMessage`方法将始终呈现`<span>`元素作为单个字段错误，即使没有错误的占位符。</span><span class="sxs-lookup"><span data-stu-id="41542-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="41542-206">在某些情况下，程序显示一条错误消息可能会导致页后，可以重排和可能导致要移动的页上的元素。</span><span class="sxs-lookup"><span data-stu-id="41542-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="41542-207">在结束的 CSS 规则`-valid`允许你定义的布局，可帮助防止出现此问题。</span><span class="sxs-lookup"><span data-stu-id="41542-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="41542-208">例如，可以定义`field-validation-error`和`field-validation-valid`同时具有相同固定大小。</span><span class="sxs-lookup"><span data-stu-id="41542-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="41542-209">这样一来，该字段的显示区域是静态的且不会更改页面流，如果显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="41542-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="41542-210">验证不会直接来自用户的数据</span><span class="sxs-lookup"><span data-stu-id="41542-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="41542-211">有时，您必须验证不会直接来自 HTML 窗体的信息。</span><span class="sxs-lookup"><span data-stu-id="41542-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="41542-212">一个典型示例是一个值，其中传入查询字符串，如以下示例所示的页面：</span><span class="sxs-lookup"><span data-stu-id="41542-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="41542-213">在这种情况下，你想要确保传递到页面的值 (此处的值的 1022年`classid`) 有效。</span><span class="sxs-lookup"><span data-stu-id="41542-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="41542-214">不能直接使用`Validation`帮助程序要执行此验证。</span><span class="sxs-lookup"><span data-stu-id="41542-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="41542-215">但是，可以使用验证系统，例如，若要显示验证错误消息的其他功能。</span><span class="sxs-lookup"><span data-stu-id="41542-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="41542-216">**重要**始终验证从获取的值*任何*源，包括窗体字段值、 查询字符串值和 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="41542-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="41542-217">它是其他人能够更改这些值 （也许是出于恶意目的） 轻松。</span><span class="sxs-lookup"><span data-stu-id="41542-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="41542-218">因此您必须检查这些值才能保护你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="41542-218">So you must check these values in order to protect your application.</span></span>


<span data-ttu-id="41542-219">下面的示例演示如何可能会验证查询字符串中传递一个值。</span><span class="sxs-lookup"><span data-stu-id="41542-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="41542-220">该代码会测试的值不为空，它是一个整数。</span><span class="sxs-lookup"><span data-stu-id="41542-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="41542-221">请注意，执行测试，如果请求不是提交窗体 (`if(!IsPost)`)。</span><span class="sxs-lookup"><span data-stu-id="41542-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="41542-222">此测试将通过第一次请求该页，但不是当请求提交窗体。</span><span class="sxs-lookup"><span data-stu-id="41542-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="41542-223">若要显示此错误，您可以将错误添加到验证错误的列表通过调用`Validation.AddFormError("message")`。</span><span class="sxs-lookup"><span data-stu-id="41542-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="41542-224">如果页面包含调用`Html.ValidationSummary`方法，该错误会在其中显示，就像用户输入验证错误。</span><span class="sxs-lookup"><span data-stu-id="41542-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="41542-225">其他资源</span><span class="sxs-lookup"><span data-stu-id="41542-225">Additional Resources</span></span>

[<span data-ttu-id="41542-226">使用 ASP.NET Web Pages 站点中的 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="41542-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
