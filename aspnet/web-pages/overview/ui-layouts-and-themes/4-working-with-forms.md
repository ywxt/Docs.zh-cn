---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: 使用 ASP.NET Web Pages (Razor) 站点中的 HTML 窗体 |Microsoft Docs
author: tfitzmac
description: 窗体是用户输入控件，如文本框、 复选框、 单选按钮和下拉列表放置 HTML 文档的一部分。 使用窗体以下值时...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: 3f4effecb3b871f1bd7db1cd2a7aab6eeca80c50
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825243"
---
<a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>使用 ASP.NET Web Pages (Razor) 站点中的 HTML 窗体
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何处理 HTML 窗体 （使用文本框和按钮） 当你使用在 ASP.NET Web Pages (Razor) 的网站中。
> 
> **你将学习：** 
> 
> - 如何创建 HTML 窗体。
> - 如何从窗体中读取用户输入。
> - 如何验证用户输入。
> - 如何提交页面后还原窗体值。
> 
> 这些是 ASP.NET 编程一文中介绍的概念：
> 
> - `Request` 对象。
> - 输入的验证。
> - HTML 编码。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - ASP.NET 网页 (Razor) 3
>   
> 
> 本教程还适用于 ASP.NET Web Pages 2。


## <a name="creating-a-simple-html-form"></a>创建一个简单的 HTML 窗体

1. 创建新的网站。
2. 在根文件夹中，创建名为的网页*Form.cshtml*并输入以下标记：

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. 启动你的浏览器中的页。 (在 WebMatrix 中，在**文件**工作区中，右键单击该文件，然后选择**浏览器中启动**。)具有三个输入字段的简单窗体和一个**提交**显示按钮。

    ![具有三个文本框的窗体的屏幕截图。](4-working-with-forms/_static/image1.jpg)

    此时，如果您单击**提交**按钮，会执行任何操作。 若要使窗体非常有用，您必须添加一些代码将在服务器上运行。

## <a name="reading-user-input-from-the-form"></a>窗体中读取用户输入

若要处理窗体，你可以添加代码读取已提交的字段值并将其进行操作的。 此过程演示如何读取的字段，并在页面上显示用户输入。 （在生产应用程序中，您通常做一些更有趣的操作用户输入。 您将执行该操作中使用数据库有关的文章。）

1. 在顶部*Form.cshtml*文件中，输入以下代码：

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    当用户首次请求页面时，会显示仅空窗体。 （它将是您） 用户在填写窗体，然后单击**提交**。 这将提交 （篇帖子） 服务器的用户输入。 默认情况下，请求将转到同一页 (即*Form.cshtml*)。

    这一次提交页面时，你输入的值显示在窗体的正上方：

    ![显示您输入的值在页面上显示的屏幕截图。](4-working-with-forms/_static/image2.jpg)

    看一下页面代码。 首先使用`IsPost`方法，以确定是否正在发布页面&#8212;，即是用户在单击**提交**按钮。 如果这是 post， `IsPost` ，则返回 true。 这是标准方法在 ASP.NET Web Pages 以确定是否正在使用初始请求 （GET 请求） 或回发 （POST 请求）。 (有关 GET 和 POST 的详细信息，请参阅侧栏"HTTP GET 和 POST 和 IsPost 属性的"中[ASP.NET Web Pages 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)。)

    接下来，获取从用户填充的值`Request.Form`对象，并且您将其放在变量的更高版本。 `Request.Form`对象包含所有已提交页上，使用每个键标识的值。 该密钥是等效于`name`你想要读取的窗体字段的属性。 例如，若要阅读`companyname`字段 （文本框），则使用`Request.Form["companyname"]`。

    窗体值存储在`Request.Form`以字符串形式的对象。 因此，当您必须使用为的数字或日期或某些其他类型的一个值，必须将其从字符串转换为该类型。 在示例中，`AsInt`方法的`Request.Form`用于将员工字段 （其中包含员工计数） 的值转换为整数。
2. 启动页面在浏览器中的，填写窗体字段，然后单击**提交**。 该页面显示您输入的值。

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>HTML 编码的外观和安全
> 
> HTML 具有特殊用途的字符，如`<`， `>`，和`&`。 如果这些特殊字符显示，它们不预期，他们可以未免的外观和功能的网页。 例如，在浏览器解释`<`为开头的 HTML 元素，如字符 （除非它后跟一个空格）`<b>`或`<input ...>`。 如果浏览器无法识别的元素，它只需放弃开头的字符串`<`直到它达到某些内容，它再次识别。 显然，这可能导致一些奇怪的页中呈现。
> 
> HTML 编码用浏览器将解释为正确的符号的代码替换这些保留的字符。 例如，`<`字符被替换为与`&lt;`并`>`字符替换为`&gt;`。 在浏览器将这些替换字符串呈现为你想要查看的字符。
> 
> 它是一个不错的主意，若要使用 HTML 编码的随时显示字符串 （输入） 所获取的用户。 如果不这样做，用户可以尝试获取网页以运行恶意脚本或执行其他操作这影响了您站点的安全或只是不想。 (这一点特别重要的如果需要用户输入，将其存储位置，然后将其显示更高版本&#8212;例如，如博客评论、 用户审阅或像这样的功能。)
> 
> 若要帮助防止这些问题，ASP.NET Web Pages 自动进行 HTML 编码的任何文本内容的输出在代码中。 例如，当显示的变量或表达式中使用的代码如内容`@MyVar`，ASP.NET Web Pages 自动对输出进行编码。


## <a name="validating-user-input"></a>验证用户输入

用户造成的错误。 请求他们填写字段，和他们忘了，或要求他们输入的员工数和这些改为键入的名称。 若要确保，窗体填入正确处理它之前，您可以验证用户的输入。

此过程演示如何验证所有三个窗体字段，以确保用户没有将其留空。 您还检查员工计数值是一个数字。 如果有错误，则将显示错误消息，告知用户哪些值未通过验证。

1. 在中*Form.cshtml*文件中，第一个代码块替换为以下代码： 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    若要验证用户输入，请使用`Validation`帮助器。 通过调用注册必填的字段`Validation.RequireField`。 通过调用注册其他类型的验证`Validation.Add`，并指定要验证的字段和要执行的验证类型。

    页运行时，ASP.NET 执行的操作为你的所有验证。 你可以通过调用检查结果`Validation.IsValid`，它返回如果传递的所有内容，则返回 true 和 false 如果验证失败的任何字段。 通常情况下，调用`Validation.IsValid`上输入的用户执行任何处理之前。
2. 更新`<body>`元素中添加三个调用`Html.ValidationMessage`方法，如下：

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    若要显示验证错误消息，可以调用 Html。`ValidationMessage` 并将其传递所需的消息的字段的名称。
3. 运行页。 将字段留空，然后单击**提交**。 你看到错误消息。

    ![显示错误消息显示用户输入未通过验证的屏幕截图。](4-working-with-forms/_static/image3.jpg)
4. 将字符串 (例如，"ABC") 添加到**员工计数**字段，然后单击**提交**试。 这一次看到一个错误，指示字符串未采用正确的格式，也就是说，一个整数。

    ![显示错误消息显示了是否用户输入员工字段的字符串的屏幕截图。](4-working-with-forms/_static/image4.jpg)

ASP.NET Web Pages 提供了更多选项可用于验证用户输入，包括能够自动执行验证使用客户端脚本，以便用户获取在浏览器中的即时反馈。 请参阅[其他资源](#Additional_Resources)更高版本的详细信息部分。

## <a name="restoring-form-values-after-postbacks"></a>在回发后还原窗体值

在上一节中测试页面，您可能已经注意到，如果遇到验证错误，输入 （而不仅仅是无效的数据） 的所有内容已消失，并且您必须重新输入所有字段的值。 这说明了很重要的一点： 时提交的页面、 其进行处理，然后再次呈现的页面，页面是从零开始重新创建。 如您所见，这意味着它提交时的页面中的所有值都都会丢失。

您可以解决此问题，但是。 有权访问已提交的值 (在`Request.Form`对象，因此您可以返回到窗体字段填充这些值，当呈现页面。

1. 在中*Form.cshtml*文件中，替换`value`的属性`<input>`元素使用`value`属性。: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    `value`的属性`<input>`元素已设置为动态读取字段值出`Request.Form`对象。 第一次请求页面时中的值`Request.Form`对象均为空。 这没什么关系，因为这种方式在窗体为空。
2. 启动页面在浏览器中的，填写窗体字段或将其留空，然后单击**提交**。 显示页面，其中显示已提交的值。

    ![窗体 5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [获取从 Web 用户输入另外 1001 方法](https://msdn.microsoft.com/library/ms971057.aspx)
- [使用窗体和处理用户输入](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [在 ASP.NET 网站中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)
- [HTML 窗体中使用自动完成功能](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
