---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: 使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 3 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历 ASP.NET MV 中的基础知识...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: 184d93323ac6f2cb7f14d32b401cf6a400eb79a6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834584"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 3 部分
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历中的 ASP.NET MVC Web 应用程序的基础知识。


## <a name="working-with-complex-types"></a>使用复杂类型

在本部分将创建 address 类，并了解如何创建模板，以显示它。

在中*模型*文件夹中，创建名为的新类文件*Person.cs*放置两种类型：`Person`类和一个`Address`类。 `Person`类将包含一个属性，它被类型化为`Address`。 `Address`类型是复杂类型，这意味着它不属于内置类型，如`int`， `string`，或`double`。 相反，它具有多个属性。 新的类的代码如下所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

在中`Movie`控制器中，添加以下`PersonDetail`操作以显示 person 实例：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

然后将以下代码添加到`Movie`控制器来填充`Person`具有一些示例数据的模型：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

打开*Views\Movies\PersonDetail.cshtml*文件，并添加以下标记为`PersonDetail`视图。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

按 Ctrl + F5 运行应用程序并导航到*电影/PersonDetail*。

`PersonDetail`视图不包含`Address`复杂类型，可以看出，在此屏幕截图。 （不显示为任何地址。）

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

`Address`因为它是一种复杂类型，不显示模型数据。 若要显示的地址信息，请打开*Views\Movies\PersonDetail.cshtml*再次文件，并添加以下标记。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

完整标记`PersonDetail`现在视图如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

运行一次应用程序并显示`PersonDetail`视图。 现在显示的地址信息：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>为复杂类型创建模板

在本部分将创建将用于呈现模板`Address`复杂类型。 当你创建的模板`Address`类型，ASP.NET MVC 可自动使用它来设置应用程序中的任意位置的地址模型的格式。 这提供了一种方法来控制的呈现`Address`从一个地方即可在应用程序中的类型。

在中*Views\Shared\DisplayTemplates*文件夹中，创建名为的强类型化分部视图**地址**:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

单击**外**，然后打开新*Views\Shared\DisplayTemplates\Address.cshtml*文件。 新视图包含以下生成的标记：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

运行应用程序并显示`PersonDetail`视图。 这一次，`Address`刚创建的模板用于显示`Address`复杂类型，以便显示看起来如下所示：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>指定的模型显示格式和模板摘要： 方法

您所见，您可以通过使用以下方法指定的格式或模型属性的模板：

- 将应用`DisplayFormat`属性为模型中的属性。 例如，下面的代码会导致没有时间的情况下显示的日期：

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- 将应用[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性中的模型和指定的数据类型的属性。 例如，下面的代码会导致没有时间的情况下显示的日期。

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    如果应用程序包含*date.cshtml*中的模板*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*文件夹中，该模板将用于呈现`DateTime`属性。 否则内置的 ASP.NET 模板化系统将显示为日期属性。
- 创建中的显示模板*Views\Shared\DisplayTemplates*文件夹或*Views\Movies\DisplayTemplates*其名称与你想要设置格式的数据类型相匹配的文件夹。 例如，您会看到*Views\Shared\DisplayTemplates\DateTime.cshtml*用于呈现`DateTime`模型，而无需添加到模型属性，而无需将任何标记添加到视图中的属性。
- 使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)模型以指定要显示的模型属性的模板的属性。
- 显式添加到的显示模板名称[Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)在视图中调用。

您使用的方法取决于您需要在你的应用程序中执行操作。 不少见混合使用这些方法以获取确切的类型的格式设置所需的。

在下一步部分中，将切换话题有点并从自定义如何向自定义输入的方式显示数据移动。 将挂接到应用程序，以便提供用于指定日期的巧妙方法中的编辑视图 jQuery datepicker。

> [!div class="step-by-step"]
> [上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
