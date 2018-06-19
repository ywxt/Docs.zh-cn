---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 验证用户输入，在 ASP.NET Web 页 (Razor) 站点 |Microsoft 文档
author: tfitzmac
description: 此文章介绍了如何验证您获得用户的信息&mdash;也就是说，若要确保用户输入有效 HTML 中的信息在中窗体另存为...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 34f703e6db70ac79c22f4a50d4cfd4e2326b4c74
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30899173"
---
<a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="56cbf-103">验证在 ASP.NET Web 页 (Razor) 站点中的用户输入</span><span class="sxs-lookup"><span data-stu-id="56cbf-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="56cbf-104">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="56cbf-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="56cbf-105">此文章介绍了如何验证您获得用户的信息&mdash;也就是说，若要确保用户输入有效 HTML 中的信息窗体在 ASP.NET Web 页 (Razor) 站点。</span><span class="sxs-lookup"><span data-stu-id="56cbf-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="56cbf-106">你将学习：</span><span class="sxs-lookup"><span data-stu-id="56cbf-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="56cbf-107">如何检查用户的输入与你定义的验证条件匹配。</span><span class="sxs-lookup"><span data-stu-id="56cbf-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="56cbf-108">如何确定是否已通过所有验证测试。</span><span class="sxs-lookup"><span data-stu-id="56cbf-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="56cbf-109">如何显示验证错误 （以及如何设置它们的格式）。</span><span class="sxs-lookup"><span data-stu-id="56cbf-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="56cbf-110">如何验证不是直接来自用户的数据。</span><span class="sxs-lookup"><span data-stu-id="56cbf-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="56cbf-111">这些是 ASP.NET 的文章中介绍的编程概念：</span><span class="sxs-lookup"><span data-stu-id="56cbf-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="56cbf-112">`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="56cbf-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="56cbf-113">`Html.ValidationSummary`和`Html.ValidationMessage`方法。</span><span class="sxs-lookup"><span data-stu-id="56cbf-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="56cbf-114">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="56cbf-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="56cbf-115">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="56cbf-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="56cbf-116">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="56cbf-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="56cbf-117">本文包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="56cbf-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="56cbf-118">用户输入验证的概述</span><span class="sxs-lookup"><span data-stu-id="56cbf-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="56cbf-119">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="56cbf-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="56cbf-120">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="56cbf-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="56cbf-121">格式设置的验证错误</span><span class="sxs-lookup"><span data-stu-id="56cbf-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="56cbf-122">验证不是直接来自用户的数据</span><span class="sxs-lookup"><span data-stu-id="56cbf-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="56cbf-123">用户输入验证的概述</span><span class="sxs-lookup"><span data-stu-id="56cbf-123">Overview of User Input Validation</span></span>

<span data-ttu-id="56cbf-124">如果你要求用户在页中输入信息 — 例如，转换为格式-务必要确保他们输入的值有效。</span><span class="sxs-lookup"><span data-stu-id="56cbf-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="56cbf-125">例如，你不想要处理缺少关键信息的窗体。</span><span class="sxs-lookup"><span data-stu-id="56cbf-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="56cbf-126">当用户向 HTML 窗体中输入值时，则他们输入的值是字符串。</span><span class="sxs-lookup"><span data-stu-id="56cbf-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="56cbf-127">在许多情况下，你需要的值是某些其他数据类型，如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="56cbf-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="56cbf-128">因此，您还需要确保用户输入的值可以正确转换为适当的数据类型。</span><span class="sxs-lookup"><span data-stu-id="56cbf-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="56cbf-129">你还可能值具有某些限制。</span><span class="sxs-lookup"><span data-stu-id="56cbf-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="56cbf-130">即使用户正确输入一个整数，例如，你可能需要确保该值在某个特定范围。</span><span class="sxs-lookup"><span data-stu-id="56cbf-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="56cbf-132">**重要**验证用户输入也很重要的安全。</span><span class="sxs-lookup"><span data-stu-id="56cbf-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="56cbf-133">如果你限制用户可以在窗体中输入的值，则可以减少有人可以输入一个值，可能会危害你的站点的安全性的可能性。</span><span class="sxs-lookup"><span data-stu-id="56cbf-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>


<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="56cbf-134">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="56cbf-134">Validating User Input</span></span>

<span data-ttu-id="56cbf-135">在 ASP.NET 网页 2 中，你可以使用`Validator`用于测试用户输入帮助程序。</span><span class="sxs-lookup"><span data-stu-id="56cbf-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="56cbf-136">基本的方法是执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="56cbf-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="56cbf-137">确定哪些输入你想要验证的元素 （字段）。</span><span class="sxs-lookup"><span data-stu-id="56cbf-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="56cbf-138">通常验证中的值`<input>`窗体中的元素。</span><span class="sxs-lookup"><span data-stu-id="56cbf-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="56cbf-139">但是，它是一个好办法验证所有输入，即使输入来自如约束元素`<select>`列表。</span><span class="sxs-lookup"><span data-stu-id="56cbf-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="56cbf-140">这有助于确保用户不绕过页上的控件和提交窗体。</span><span class="sxs-lookup"><span data-stu-id="56cbf-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="56cbf-141">为每个输入元素使用的方法，则在网页代码中，添加单独的验证检查`Validation`帮助器。</span><span class="sxs-lookup"><span data-stu-id="56cbf-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="56cbf-142">若要检查的必填字段，请使用`Validation.RequireField(field, [error message])`（为单个字段） 或`Validation.RequireFields(field1, field2, ...))`（有关字段的列表）。</span><span class="sxs-lookup"><span data-stu-id="56cbf-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="56cbf-143">对于其他类型的验证，使用`Validation.Add(field, ValidationType)`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="56cbf-144">有关`ValidationType`，你可以使用这些选项：</span><span class="sxs-lookup"><span data-stu-id="56cbf-144">For `ValidationType`, you can use these options:</span></span>

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
3. <span data-ttu-id="56cbf-145">当提交页面时，检查是否通过检查已通过验证`Validation.IsValid`:</span><span class="sxs-lookup"><span data-stu-id="56cbf-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="56cbf-146">如果不存在任何验证错误，则跳过正常的页处理。</span><span class="sxs-lookup"><span data-stu-id="56cbf-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="56cbf-147">例如，如果该页面的用途是更新数据库，不执行操作，直到在修复所有验证错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="56cbf-148">如果有验证错误，显示错误消息中页面的标记使用`Html.ValidationSummary`或`Html.ValidationMessage`，和/或文件名。</span><span class="sxs-lookup"><span data-stu-id="56cbf-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="56cbf-149">下面的示例演示一个页，演示了这些步骤。</span><span class="sxs-lookup"><span data-stu-id="56cbf-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="56cbf-150">若要查看验证的工作原理，运行此页，并有意犯的错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="56cbf-151">例如，下面是什么如果您忘记输入过程名称时，如果输入页的外观，并且如果输入无效的日期：</span><span class="sxs-lookup"><span data-stu-id="56cbf-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![呈现的页面中的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="56cbf-153">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="56cbf-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="56cbf-154">默认情况下，用户输入进行验证，在用户提交页后，即，在服务器代码中执行验证。</span><span class="sxs-lookup"><span data-stu-id="56cbf-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="56cbf-155">此方法的缺点是用户不知道他们进行后的出现错误直到它们提交页面。</span><span class="sxs-lookup"><span data-stu-id="56cbf-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="56cbf-156">如果窗体是长或者过于复杂，则报告错误，只有在提交页面后，才可以将向用户很不方便。</span><span class="sxs-lookup"><span data-stu-id="56cbf-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="56cbf-157">你可以添加支持，以在客户端脚本中执行验证。</span><span class="sxs-lookup"><span data-stu-id="56cbf-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="56cbf-158">在这种情况下，用户在浏览器中工作，则不执行验证。</span><span class="sxs-lookup"><span data-stu-id="56cbf-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="56cbf-159">例如，假设你指定的值应为整数。</span><span class="sxs-lookup"><span data-stu-id="56cbf-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="56cbf-160">如果用户输入一个非整数值，用户离开输入字段时，会报告错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="56cbf-161">用户获取将为它们提供方便的即时反馈。</span><span class="sxs-lookup"><span data-stu-id="56cbf-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="56cbf-162">基于客户端验证还可以减少的用户必须提交表单更正多个错误的次数。</span><span class="sxs-lookup"><span data-stu-id="56cbf-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="56cbf-163">即使你使用客户端验证，始终也是在服务器代码中执行验证。</span><span class="sxs-lookup"><span data-stu-id="56cbf-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="56cbf-164">在服务器代码中执行验证是一种安全措施，以防用户跳过基于客户端的验证。</span><span class="sxs-lookup"><span data-stu-id="56cbf-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>


1. <span data-ttu-id="56cbf-165">在页中注册以下 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="56cbf-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="56cbf-166">两个库是内容交付网络 (CDN)，从加载的因此你不一定对您的计算机或服务器。</span><span class="sxs-lookup"><span data-stu-id="56cbf-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="56cbf-167">但是，你必须具有的本地副本*jquery.validate.unobtrusive.js*。</span><span class="sxs-lookup"><span data-stu-id="56cbf-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="56cbf-168">如果你不已正在使用 WebMatrix 模板 (如**入门站点**) 包含库中，创建基于一个网页站点**入门站点**。</span><span class="sxs-lookup"><span data-stu-id="56cbf-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="56cbf-169">然后将复制 *.js*给当前站点的文件。</span><span class="sxs-lookup"><span data-stu-id="56cbf-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="56cbf-170">标记，您要验证，每个元素中添加对的调用`Validation.For(field)`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="56cbf-171">此方法会发出由客户端验证的属性。</span><span class="sxs-lookup"><span data-stu-id="56cbf-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="56cbf-172">(而不是发出实际的 JavaScript 代码时，该方法发出这样的属性`data-val-...`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="56cbf-173">这些属性支持使用 jQuery 来执行工作的非介入式客户端验证）。</span><span class="sxs-lookup"><span data-stu-id="56cbf-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="56cbf-174">以下页面演示如何将客户端验证功能添加到前面所示的示例。</span><span class="sxs-lookup"><span data-stu-id="56cbf-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="56cbf-175">并非所有客户端上运行的验证检查。</span><span class="sxs-lookup"><span data-stu-id="56cbf-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="56cbf-176">具体而言，数据类型验证 （整数、 日期和等等） 不在客户端上运行。</span><span class="sxs-lookup"><span data-stu-id="56cbf-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="56cbf-177">在客户端和服务器上工作的以下检查：</span><span class="sxs-lookup"><span data-stu-id="56cbf-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="56cbf-178">在此示例中，是有效的日期的测试无法运行在客户端代码。</span><span class="sxs-lookup"><span data-stu-id="56cbf-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="56cbf-179">但是，测试将在服务器代码中执行。</span><span class="sxs-lookup"><span data-stu-id="56cbf-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="56cbf-180">格式设置的验证错误</span><span class="sxs-lookup"><span data-stu-id="56cbf-180">Formatting Validation Errors</span></span>

<span data-ttu-id="56cbf-181">你可以控制定义 CSS 类具有以下保留的名称显示验证错误：</span><span class="sxs-lookup"><span data-stu-id="56cbf-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="56cbf-182">`field-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-182">`field-validation-error`.</span></span> <span data-ttu-id="56cbf-183">定义的输出`Html.ValidationMessage`方法时它显示一条错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="56cbf-184">`field-validation-valid`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-184">`field-validation-valid`.</span></span> <span data-ttu-id="56cbf-185">定义的输出`Html.ValidationMessage`方法时没有错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="56cbf-186">`input-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-186">`input-validation-error`.</span></span> <span data-ttu-id="56cbf-187">定义如何`<input>`元素呈现时出错。</span><span class="sxs-lookup"><span data-stu-id="56cbf-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="56cbf-188">(例如，你可以使用此类设置的背景色&lt;输入&gt;元素为不同的颜色，如果其值无效。)（在 ASP.NET 网页 2) 的客户端验证期间仅使用此 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="56cbf-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="56cbf-189">`input-validation-valid`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-189">`input-validation-valid`.</span></span> <span data-ttu-id="56cbf-190">定义的外观`<input>`元素时没有错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="56cbf-191">`validation-summary-errors`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-191">`validation-summary-errors`.</span></span> <span data-ttu-id="56cbf-192">定义的输出`Html.ValidationSummary`它显示的错误列表的方法。</span><span class="sxs-lookup"><span data-stu-id="56cbf-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="56cbf-193">`validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-193">`validation-summary-valid`.</span></span> <span data-ttu-id="56cbf-194">定义的输出`Html.ValidationSummary`方法时没有错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="56cbf-195">以下`<style>`块显示错误条件规则。</span><span class="sxs-lookup"><span data-stu-id="56cbf-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="56cbf-196">如果你在从与本文前面的示例页包含此样式块，错误显示的外观将类似于下图：</span><span class="sxs-lookup"><span data-stu-id="56cbf-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="56cbf-198">如果你不在 ASP.NET 网页 2 中使用客户端验证，CSS 类为`<input>`元素 (`input-validation-error`和`input-validation-valid`不产生任何影响。</span><span class="sxs-lookup"><span data-stu-id="56cbf-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>


### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="56cbf-199">静态和动态错误显示</span><span class="sxs-lookup"><span data-stu-id="56cbf-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="56cbf-200">CSS 规则成对出现，如`validation-summary-errors`和`validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="56cbf-201">这些对允许你定义这两个条件的规则： 一个错误条件和"正常"（非错误） 条件。</span><span class="sxs-lookup"><span data-stu-id="56cbf-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="56cbf-202">请务必了解，始终呈现错误显示的标记，即使没有错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="56cbf-203">例如，如果页具有`Html.ValidationSummary`标记中的方法，即使第一次请求页时，页面源文件将包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="56cbf-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="56cbf-204">换而言之，`Html.ValidationSummary`方法始终呈现`<div>`元素和列表，即使错误列表为空。</span><span class="sxs-lookup"><span data-stu-id="56cbf-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="56cbf-205">同样，`Html.ValidationMessage`方法始终呈现`<span>`作为单个字段错误，即使没有错误占位符的元素。</span><span class="sxs-lookup"><span data-stu-id="56cbf-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="56cbf-206">在某些情况下，程序显示一条错误消息可能会导致页后，可以重新排列并可能导致在页上进行来回移动的元素。</span><span class="sxs-lookup"><span data-stu-id="56cbf-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="56cbf-207">以结尾的 CSS 规则`-valid`使你能够定义可以帮助防止此问题的布局。</span><span class="sxs-lookup"><span data-stu-id="56cbf-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="56cbf-208">例如，你可以定义`field-validation-error`和`field-validation-valid`两者都具有相同固定大小。</span><span class="sxs-lookup"><span data-stu-id="56cbf-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="56cbf-209">这样一来，该字段的显示区域是静态的不会显示一条错误消息的情况下更改页面流。</span><span class="sxs-lookup"><span data-stu-id="56cbf-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="56cbf-210">验证不是直接来自用户的数据</span><span class="sxs-lookup"><span data-stu-id="56cbf-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="56cbf-211">有时，你必须以验证不会直接从 HTML 窗体的信息。</span><span class="sxs-lookup"><span data-stu-id="56cbf-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="56cbf-212">一个典型示例是的单页其中传递值，则在查询字符串内，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="56cbf-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="56cbf-213">在这种情况下，你想要确保传递到页的值 (这里，值的 1022年`classid`) 无效。</span><span class="sxs-lookup"><span data-stu-id="56cbf-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="56cbf-214">不能直接使用`Validation`帮助程序要执行此验证。</span><span class="sxs-lookup"><span data-stu-id="56cbf-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="56cbf-215">但是，你可以使用验证系统，如显示验证错误消息的功能的其他功能。</span><span class="sxs-lookup"><span data-stu-id="56cbf-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="56cbf-216">**重要**始终验证您获得的值*任何*源，包括窗体字段值、 查询字符串值和 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="56cbf-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="56cbf-217">很容易让人有机会 （可能是出于恶意目的） 更改这些值。</span><span class="sxs-lookup"><span data-stu-id="56cbf-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="56cbf-218">因此，你必须为了保护你的应用程序中检查这些值。</span><span class="sxs-lookup"><span data-stu-id="56cbf-218">So you must check these values in order to protect your application.</span></span>


<span data-ttu-id="56cbf-219">下面的示例演示如何可能验证查询字符串中传递一个值。</span><span class="sxs-lookup"><span data-stu-id="56cbf-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="56cbf-220">代码测试的值不为空，以及它是一个整数。</span><span class="sxs-lookup"><span data-stu-id="56cbf-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="56cbf-221">请注意执行测试，如果请求不提交窗体 (`if(!IsPost)`)。</span><span class="sxs-lookup"><span data-stu-id="56cbf-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="56cbf-222">此测试将通过请求页时，第一次，但不是请求时提交窗体。</span><span class="sxs-lookup"><span data-stu-id="56cbf-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="56cbf-223">若要显示此错误，你可以将错误添加到验证错误的列表通过调用`Validation.AddFormError("message")`。</span><span class="sxs-lookup"><span data-stu-id="56cbf-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="56cbf-224">如果该页面包含调用`Html.ValidationSummary`方法，该错误会在其中显示一样用户输入验证错误。</span><span class="sxs-lookup"><span data-stu-id="56cbf-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="56cbf-225">其他资源</span><span class="sxs-lookup"><span data-stu-id="56cbf-225">Additional Resources</span></span>

[<span data-ttu-id="56cbf-226">使用 ASP.NET Web 页站点中的 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="56cbf-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
