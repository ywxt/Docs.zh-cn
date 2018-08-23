---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 将验证添加到模型 (C#) |Microsoft Docs
author: Rick-Anderson
description: 创建控制器
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 14db6184d3edd584fe35529cd4cf1dba5b528ab1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834689"
---
<a name="adding-validation-to-the-model-c"></a>将验证添加到模型 (C#)
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。
> 
> 
> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 C# 源代码的 Visual Web Developer 项目。 [下载 C# 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您喜欢 Visual Basic，切换到[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)本教程。


在本部分中，你将添加到的验证逻辑`Movie`模型，并确保每次用户尝试创建或编辑电影使用应用程序时，强制的验证规则。

## <a name="keeping-things-dry"></a>DRY 地保管东西

ASP.NET MVC 的核心设计原则之一是 DRY （"不要自我重复"）。 ASP.NET MVC 支持你指定的功能或行为只有一次，然后让它应用到整个应用程序中。 这可以减少需要编写的代码量，并使您编写的代码执行操作变得更加容易维护。

由 ASP.NET MVC 和 Entity Framework Code First 提供的验证支持是 DRY 原则在操作中的一个极好示例。 在一个位置 （在模型类中） 以声明方式指定验证规则，然后这些规则是所有位置强制执行应用程序中。

让我们看看电影应用程序中，您就可以充分利用此验证支持。

## <a name="adding-validation-rules-to-the-movie-model"></a>向电影模型添加验证规则

您将首先添加到某些验证逻辑`Movie`类。

打开 Movie.cs 文件。 添加`using`语句引用的文件的顶部[ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

命名空间是.NET Framework 的一部分。 它提供了一组内置验证特性，可以以声明方式应用于任何类或属性。

现在，更新`Movie`类，以充分利用内置[ `Required` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)， [ `StringLength` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)，并且[ `Range` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性. 使用以下代码作为应用特性的位置的示例。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

验证特性指定要对应用这些特性的模型属性强制执行的行为。 `Required`属性指示属性必须具有一个值; 在此示例中，电影已具有值`Title`， `ReleaseDate`， `Genre`，和`Price`属性才有效。 `Range` 特性将值限制在指定范围内。 `StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。

代码首先确保之前应用程序将更改保存在数据库中实施的 model 类指定的验证规则。 例如，下面的代码将引发异常时`SaveChanges`调用方法，因为所需的几个`Movie`缺少属性值，价格为零 （即不在有效范围内）。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

具有自动强制执行由.NET Framework 的验证规则有助于使您的应用程序更可靠。 同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。

以下是列出了已更新的完整代码*Movie.cs*文件：

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>验证错误在 ASP.NET MVC 中的 UI

重新运行该应用程序并导航到 */Movies* URL。

单击**创建电影**链接以添加新电影。 填写表单的某些无效的值，然后单击**创建**按钮。

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

请注意如何在窗体具有自动使用背景色突出显示的文本框包含无效的数据和已发出每个适当的验证错误消息。 错误消息与指定带批注时的错误字符串匹配`Movie`类。 这些错误会强制客户端 （使用 JavaScript） 和服务器端执行，（如果用户已禁用 JavaScript）。

一个实际优点是不需要更改任何一行中的代码`MoviesController`类中或在*Create.cshtml*来启用此验证 UI 的视图。 控制器和自动在本教程前面创建的视图上选择的了验证规则上使用特性指定`Movie`的模型。

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>如何在中进行验证创建查看和创建操作方法

你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。 下一步列表显示什么`Create`中的方法`MovieController`类看起来像。 它们是如何在本教程前面创建它们相比没有变化。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

第一个操作方法显示初始创建窗体。 第二个处理窗体 post。 第二个`Create`方法调用`ModelState.IsValid`检查电影是否有任何验证错误。 调用此方法将评估已应用于对象的任何验证特性。 如果对象具有验证错误，`Create`方法重新显示该窗体。 如果没有错误，此方法则将新电影保存在数据库中。

下面是*Create.cshtml*基架在本教程前面部分中的视图模板。 以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

请注意代码如何使用`Html.EditorFor`帮助器输出`<input>`每个元素`Movie`属性。 此帮助器旁边是对的调用`Html.ValidationMessageFor`帮助器方法。 这两个帮助器方法使用由控制器传递给视图的模型对象 (在这种情况下，`Movie`对象)。 它们会自动查找适当的模型和显示错误消息中指定的验证特性。

有关此方法非常令人愉快的是，在控制器和创建视图模板都不知道任何有关强制实施的实际验证规则或显示的特定错误消息。 仅可在 `Movie` 类中指定验证规则和错误字符串。

如果你想要以后更改验证逻辑，就可以做到在同一个位置。 无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。 这使代码非常简洁，并且更易于维护和改进。 这意味着对 DRY 原则的完全遵守。

## <a name="adding-formatting-to-the-movie-model"></a>将格式添加到电影模型

打开 Movie.cs 文件。 [ `System.ComponentModel.DataAnnotations` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供除了一组内置验证特性的格式设置属性。 将应用[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性和一个[ `DataType` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)发布日期和价格字段的枚举值。 下面的代码演示`ReleaseDate`并`Price`具有适当[ `DisplayFormat` ](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

或者，您可以显式设置[ `DataFormatString` ](https://msdn.microsoft.com/library/system.string.format.aspx)值。 下面的代码演示了日期格式字符串的发行日期属性 (即，"d")。 将此位置用于指定你不想为时间发布日期的一部分。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

下面的代码格式`Price`属性设置为货币。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

完整`Movie`类如下所示。

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

运行应用程序，并浏览到`Movies`控制器。

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。

> [!div class="step-by-step"]
> [上一页](adding-a-new-field.md)
> [下一页](improving-the-details-and-delete-methods.md)
