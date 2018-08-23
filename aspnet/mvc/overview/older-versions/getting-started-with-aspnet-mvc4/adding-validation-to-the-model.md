---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 向模型添加验证 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 01190b7bffc0258649373f3be0c75c41af80921d
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831669"
---
<a name="adding-validation-to-the-model"></a>向模型添加验证
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


在本部分中，你将添加到的验证逻辑`Movie`模型，并确保每次用户尝试创建或编辑电影使用应用程序时，强制的验证规则。

## <a name="keeping-things-dry"></a>DRY 地保管东西

ASP.NET MVC 的核心设计原则之一是 DRY (&quot;不要自我重复&quot;)。 ASP.NET MVC 支持你指定的功能或行为只有一次，然后让它应用到整个应用程序中。 这可以减少需要编写的代码量，并使您编写更少容易出错且更易于维护的代码。

由 ASP.NET MVC 和 Entity Framework Code First 提供的验证支持是 DRY 原则在操作中的一个极好示例。 在一个位置 （在模型类中） 以声明方式指定验证规则和规则所有位置强制执行应用程序中。

让我们看看电影应用程序中，您就可以充分利用此验证支持。

## <a name="adding-validation-rules-to-the-movie-model"></a>向电影模型添加验证规则

您将首先添加到某些验证逻辑`Movie`类。

打开 Movie.cs 文件。 添加`using`语句引用的文件的顶部[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

请注意，命名空间不包含`System.Web`。 DataAnnotations 提供一组内置验证特性，可以以声明方式应用于任何类或属性。

现在，更新`Movie`类，以充分利用内置[ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)， [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)，并且[ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性. 使用以下代码作为应用特性的位置的示例。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

运行应用程序，则也会收到以下运行的时错误：

***创建数据库后，支持 MovieDBContext 上下文的模型已更改。请考虑使用 Code First 迁移来更新数据库 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。***

我们将使用迁移来更新架构。 生成解决方案，然后打开**程序包管理器控制台**窗口并输入以下命令：

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

此命令完成后，Visual Studio 会打开定义新的类文件`DbMIgration`派生类指定的名称 (*AddDataAnnotationsMig*)，然后在`Up`方法您可以看到更新的代码架构的约束。 `Title`并`Genre`字段不再可以为 null （即，您必须输入一个值） 和`Rating`字段具有最大长度为 5。

验证特性指定要对应用这些特性的模型属性强制执行的行为。 `Required`属性指示属性必须具有一个值; 在此示例中，电影已具有值`Title`， `ReleaseDate`， `Genre`，和`Price`属性才有效。 `Range` 特性将值限制在指定范围内。 `StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。 内部类型 (如`decimal, int, float, DateTime`) 所需的默认值，而无须`Required`属性。

代码首先确保之前应用程序将更改保存在数据库中实施的 model 类指定的验证规则。 例如，下面的代码将引发异常时`SaveChanges`调用方法，因为所需的几个`Movie`缺少属性值，价格为零 （即不在有效范围内）。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

具有自动强制执行由.NET Framework 的验证规则有助于使您的应用程序更可靠。 同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。

以下是列出了已更新的完整代码*Movie.cs*文件：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>验证错误在 ASP.NET MVC 中的 UI

重新运行该应用程序并导航到 */Movies* URL。

单击**创建新**链接以添加新电影。 填写表单的某些无效的值，然后单击**创建**按钮。

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 若要支持 jQuery 验证的非英语区域设置，请使用逗号 (&quot;，&quot;) 必须包含小数点， *globalize.js*和您的特定*cultures/globalize.cultures.js*文件 (从[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和 JavaScript 使用`Globalize.parseFloat`。 下面的代码演示对 Views\Movies\Edit.cshtml 文件用于修改&quot;-FR&quot;区域性：


[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

请注意如何在窗体具有自动使用红色边框颜色突出显示的文本框包含无效的数据和已发出每个适当的验证错误消息。 客户端（使用 JavaScript 和 jQuery）和服务器端（若用户禁用 JavaScript）都必定会遇到这些错误。

一个实际优点是不需要更改任何一行中的代码`MoviesController`类中或在*Create.cshtml*来启用此验证 UI 的视图。 在本教程前面创建的控制器和视图会自动选取验证规则，这些规则是通过在 `Movie` 模型类的属性上使用验证特性所指定的。

您可能已经注意到的属性`Title`并`Genre`，不强制执行所需的属性，直到在提交表单 (命中**创建**按钮)，或输入字段中输入文本并将其删除。 字段即最初为空 （如 Create 视图上的字段），并且具有所需的属性和任何其他验证属性，可以执行以下操作来触发验证：

1. 字段中的选项卡。
2. 输入一些文本。
3. 退出选项卡。
4. 返回到该字段的选项卡。
5. 删除的文本。
6. 退出选项卡。

上面的顺序将触发所需的验证，而不会达到提交按钮。 只需点击提交按钮而无需输入的任何字段都将触发客户端验证。 存在客户端验证错误时，不会将表单数据发送到服务器。 可以通过 HTTP Post 方法中放置一个断点或使用测试这[fiddler 工具](http://fiddler2.com/fiddler2/)或 IE 9 [F12 开发人员工具](https://msdn.microsoft.com/ie/aa740478)。

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在中进行验证创建查看和创建操作方法

你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。 下一步列表显示什么`Create`中的方法`MovieController`类看起来像。 它们是如何在本教程前面创建它们相比没有变化。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

第一个 (HTTP GET) `Create` 操作方法显示初始的“创建”表单。 第二个 (`[HttpPost]`) 版本处理表单发布。 第二个 `Create` 方法（`HttpPost` 版本）调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。 调用此方法将评估已应用于对象的任何验证特性。 如果对象有验证错误，则 `Create` 方法会重新显示此表单。 如果没有错误，此方法则将新电影保存在数据库中。 在我们的电影示例中我们将使用**窗体不会发布到服务器时有验证错误在客户端; 上检测到第二个** `Create`**永远不会调用方法**。 如果在浏览器中禁用 JavaScript，请禁用客户端验证和 HTTP POST`Create`方法调用`ModelState.IsValid`检查电影是否有任何验证错误。

可以在 `HttpPost Create` 方法中设置断点，并验证方法从未被调用，客户端验证在检测到存在验证错误时不会提交表单数据。 如果在浏览器中禁用 JavaScript，然后提交错误的表单，将触发断点。 在没有 JavaScript 的情况下仍然可以进行完整的验证。 下图显示了如何禁用 Internet Explorer 中的 JavaScript。

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

以下图片显示如何在 FireFox 浏览器中禁用 JavaScript。

![](adding-validation-to-the-model/_static/image5.png)

下图显示了如何使用 Chrome 浏览器中禁用 JavaScript。

![](adding-validation-to-the-model/_static/image6.png)

下面是*Create.cshtml*基架在本教程前面部分中的视图模板。 以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

请注意代码如何使用`Html.EditorFor`帮助器输出`<input>`每个元素`Movie`属性。 此帮助器旁边是对的调用`Html.ValidationMessageFor`帮助器方法。 这两个帮助器方法使用由控制器传递给视图的模型对象 (在这种情况下，`Movie`对象)。 它们会自动查找适当的模型和显示错误消息中指定的验证特性。

有关此方法非常令人愉快的是，在控制器和创建视图模板都不知道任何有关强制实施的实际验证规则或显示的特定错误消息。 仅可在 `Movie` 类中指定验证规则和错误字符串。 这些相同的验证规则自动应用于编辑视图和任何其他视图模板可能会创建用于编辑模型中。

如果你想要以后更改验证逻辑，就可以做到在同一个位置通过向模型添加验证特性 (在此示例中，`movie`类)。 无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。 这使代码非常简洁，并且更易于维护和改进。 这意味着对 DRY 原则的完全遵守。

## <a name="adding-formatting-to-the-movie-model"></a>将格式添加到电影模型

打开 Movie.cs 文件并检查 `Movie` 类。 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供除了一组内置验证特性的格式设置属性。 我们已应用[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)发布日期和价格字段的枚举值。 下面的代码演示`ReleaseDate`并`Price`具有适当[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性不是验证特性，它们用于告知如何呈现的 HTML 的视图引擎。 在上述示例中，`DataType.Date`属性不包括时间显示为日期，电影日期。 例如，以下[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性不验证数据的格式：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

上面列出的特性仅提供提示帮助视图引擎设置数据的格式 (如提供属性和&lt;&gt; url 并&lt;a =&quot;mailto:EmailAddress.com&quot; &gt;电子邮件。 可以使用[正则表达式](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)特性验证数据的格式。

一种方法来使用`DataType`属性，您可以显式设置[ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下面的代码演示了日期格式字符串的发行日期属性 (即&quot;d&quot;)。 将此位置用于指定你不想为时间发布日期的一部分。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

完整`Movie`类如下所示。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

运行应用程序，并浏览到`Movies`控制器。 发布日期和价格可以很好地进行格式化。 下图显示的发布日期和使用价格&quot;-FR&quot;与区域性。

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

下图显示了与默认区域性 （美国英语） 显示的相同数据。

![](adding-validation-to-the-model/_static/image8.png)

在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。

> [!div class="step-by-step"]
> [上一页](adding-a-new-field-to-the-movie-model-and-table.md)
> [下一页](examining-the-details-and-delete-methods.md)
