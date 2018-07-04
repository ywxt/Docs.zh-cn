---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 验证用户输入在 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: tfitzmac
description: 本文介绍如何验证的信息从用户获取&mdash;，即以确保用户输入有效信息在 HTML 窗体中另存为...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 2a35e9895c5b711d5c6c5544987f99fe7e2e0085
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368222"
---
<a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>ASP.NET Web Pages (Razor) 站点中验证用户输入
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何验证的信息从用户获取&mdash;即，以确保用户输入有效信息以 html 格式窗体在 ASP.NET Web Pages (Razor) 站点中。
> 
> 你将学习：
> 
> - 如何检查用户的输入与你定义的验证条件匹配。
> - 如何确定是否已通过所有验证测试。
> - 如何显示验证错误 （以及如何对其进行格式）。
> - 如何验证不会直接来自用户的数据。
> 
> 这些是 ASP.NET 编程一文中介绍的概念：
> 
> - `Validation`帮助器。
> - `Html.ValidationSummary`和`Html.ValidationMessage`方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


本文包含以下各节：

- [用户输入验证的概述](#Overview_of_User_Input_Validation)
- [验证用户输入](#Validating_User_Input)
- [添加客户端验证](#Adding_Client-Side_Validation)
- [格式设置验证错误](#Formatting_Validation_Errors)
- [验证不会直接来自用户的数据](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>用户输入验证的概述

如果要求用户在页面中输入的信息 — 例如，到窗体，务必要确保他们输入的值有效。 例如，您不想处理缺少的关键信息的窗体。

当用户向 HTML 窗体中输入值时，则他们输入的值是字符串。 在许多情况下，所需的值是某些其他数据类型，如整数或日期。 因此，您还需要确保用户输入的值可以正确地转换为适当的数据类型。

此外可能的值具有某些限制。 即使用户正确输入一个整数，例如，您可能需要确保该值所属的特定范围内。

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **重要**验证用户输入也很重要的安全。 如果你限制用户可以在窗体中输入的值，则可以减少人可以输入一个值，可能损害您的网站的安全性的机会。


<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>验证用户输入

在 ASP.NET Web Pages 2 中，可以使用`Validator`帮助程序来测试用户输入。 基本的方法是执行以下操作：

1. 确定哪个输入你想要验证的元素 （字段）。

    通常验证中的值`<input>`窗体中的元素。 但是，它是一个好办法验证所有输入，即使输入来自受约束的元素，如`<select>`列表。 这有助于确保用户不绕过页面上的控件和提交窗体。
2. 对于每个输入元素使用的方法，则在网页代码中，添加各自的验证检查`Validation`帮助器。

    若要检查的必填字段，请使用`Validation.RequireField(field, [error message])`（适用于单个字段） 或`Validation.RequireFields(field1, field2, ...))`（有关字段的列表）。 对于其他类型的验证，请使用`Validation.Add(field, ValidationType)`。 有关`ValidationType`，可以使用这些选项：

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
3. 提交页面后，检查是否通过验证后通过检查`Validation.IsValid`:

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    如果有任何验证错误，则跳过正常页面处理。 例如，如果页面的目的是用于更新数据库，就不必这么做直到修复了所有验证错误。
4. 如果验证错误，错误消息中显示页面的标记使用`Html.ValidationSummary`或`Html.ValidationMessage`，和 / 或。

下面的示例显示了一个页面，说明了这些步骤。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

若要查看验证的工作原理，请运行此页并故意犯的错误。 例如，下面是什么如果您忘记输入门课程的名称，如果输入网页的外观，并且如果输入无效的日期：

![在呈现的页面中的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>添加客户端验证

默认情况下，用户输入进行验证，在用户提交页面后，即，在服务器代码中执行验证。 此方法的缺点是用户不知道它们已进行了错误直到后它们提交该页面。 如果窗体是长或者过于复杂，只有在提交页面后报告的错误可能会给用户带来不便。

可以添加支持以在客户端脚本中执行验证。 在这种情况下，用户在处理在浏览器中，将执行验证。 例如，假设您指定一个值应为整数。 如果用户输入一个非整数值，用户离开在输入字段时，会报告错误。 用户获得即时反馈，便于在它们。 基于客户端验证还可以减少用户必须提交表格，以更正多个错误的次数。

> [!NOTE]
> 即使使用客户端验证时，始终还在服务器代码中执行验证。 在服务器代码中执行验证是一种安全措施，以防用户绕过基于客户端验证。


1. 在页面中注册以下 JavaScript 库：  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   两个库是从内容传送网络 (CDN)，可加载的因此您不必对您的计算机或服务器。 但是，必须具有的本地副本*jquery.validate.unobtrusive.js*。 如果你没有已使用 WebMatrix 模板 (如**入门网站**) 包含在库中，创建基于 Web Pages 站点**入门网站**。 然后将复制 *.js*到当前站点的文件。
2. 在标记中，为你在验证每个元素添加到调用`Validation.For(field)`。 此方法会发出使用的客户端验证的属性。 (而不是发出实际 JavaScript 代码时，该方法发出之类的属性`data-val-...`。 这些属性支持使用 jQuery 来执行工作的非介入式客户端验证）。

以下页面显示了如何将客户端验证功能添加到前面所示的示例。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

并非所有客户端上运行的验证检查。 具体而言，数据类型验证 （整数、 日期等） 不在客户端上运行。 客户端和服务器上工作的以下检查：

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

在此示例中，是有效的日期的测试中的客户端代码不起作用。 但是，将在服务器代码中执行测试。

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>格式设置验证错误

您可以控制定义 CSS 类具有以下保留的名称的显示验证错误：

- `field-validation-error`。 定义的输出`Html.ValidationMessage`方法时显示错误。
- `field-validation-valid`。 定义的输出`Html.ValidationMessage`方法时没有错误。
- `input-validation-error`。 定义如何`<input>`元素呈现时出错。 (例如，可以使用此类设置的背景色&lt;输入&gt;为不同的颜色，如果其值为无效的元素。)仅在客户端验证 （在 ASP.NET Web Pages 2) 中使用此 CSS 类。
- `input-validation-valid`。 定义的外观`<input>`元素时没有错误。
- `validation-summary-errors`。 定义的输出`Html.ValidationSummary`方法，它显示错误的列表。
- `validation-summary-valid`。 定义的输出`Html.ValidationSummary`方法时没有错误。

以下`<style>`块显示了错误条件的规则。

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

如果在从本文前面的示例页中包含此样式块，错误显示的外观将类似于下图：

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> 如果您在 ASP.NET Web Pages 2 中不使用客户端验证的 CSS 类的`<input>`元素 (`input-validation-error`和`input-validation-valid`不产生任何影响。


### <a name="static-and-dynamic-error-display"></a>静态和动态错误显示

CSS 规则成对出现，如`validation-summary-errors`和`validation-summary-valid`。 这些对允许你定义的两个条件规则： 一个错误条件和"正常"（非错误） 条件。 请务必了解，始终呈现错误显示的标记时，即使没有任何错误。 例如，如果页面具有`Html.ValidationSummary`标记中的方法，即使在第一次请求页面时，页面源文件将包含以下标记：

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

换而言之，`Html.ValidationSummary`方法将始终呈现`<div>`元素和一个列表，即使错误列表为空。 同样，`Html.ValidationMessage`方法将始终呈现`<span>`元素作为单个字段错误，即使没有错误的占位符。

在某些情况下，程序显示一条错误消息可能会导致页后，可以重排和可能导致要移动的页上的元素。 在结束的 CSS 规则`-valid`允许你定义的布局，可帮助防止出现此问题。 例如，可以定义`field-validation-error`和`field-validation-valid`同时具有相同固定大小。 这样一来，该字段的显示区域是静态的且不会更改页面流，如果显示一条错误消息。

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>验证不会直接来自用户的数据

有时，您必须验证不会直接来自 HTML 窗体的信息。 一个典型示例是一个值，其中传入查询字符串，如以下示例所示的页面：

`http://server/myapp/EditClassInformation?classid=1022`

在这种情况下，你想要确保传递到页面的值 (此处的值的 1022年`classid`) 有效。 不能直接使用`Validation`帮助程序要执行此验证。 但是，可以使用验证系统，例如，若要显示验证错误消息的其他功能。

> [!NOTE] 
> 
> **重要**始终验证从获取的值*任何*源，包括窗体字段值、 查询字符串值和 cookie 值。 它是其他人能够更改这些值 （也许是出于恶意目的） 轻松。 因此您必须检查这些值才能保护你的应用程序。


下面的示例演示如何可能会验证查询字符串中传递一个值。 该代码会测试的值不为空，它是一个整数。

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

请注意，执行测试，如果请求不是提交窗体 (`if(!IsPost)`)。 此测试将通过第一次请求该页，但不是当请求提交窗体。

若要显示此错误，您可以将错误添加到验证错误的列表通过调用`Validation.AddFormError("message")`。 如果页面包含调用`Html.ValidationSummary`方法，该错误会在其中显示，就像用户输入验证错误。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他资源

[使用 ASP.NET Web Pages 站点中的 HTML 窗体](https://go.microsoft.com/fwlink/?LinkID=202892)
