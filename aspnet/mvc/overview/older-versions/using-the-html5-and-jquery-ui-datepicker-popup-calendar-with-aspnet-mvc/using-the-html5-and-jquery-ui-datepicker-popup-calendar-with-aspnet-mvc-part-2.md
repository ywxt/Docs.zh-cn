---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: 使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 2 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历 ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/29/2011
ms.topic: article
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 2818e69f912509a6392333bad8f5a1afa55884f6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375284"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 2 部分
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历中的 ASP.NET MVC Web 应用程序的基础知识。


## <a name="adding-an-automatic-datetime-template"></a>添加自动的 DateTime 模板

在本教程的第一部分，您了解了如何将属性添加到模型以显式指定的格式设置，以及如何可以显式指定用于呈现模型的模板。 例如， [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性在以下代码显式指定的格式设置`ReleaseDate`属性。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

在以下示例中，[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性，使用`Date`枚举，指定应使用日期模板来呈现模型。 如果在项目中没有日期模板，则使用内置日期模板。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

但是，ASP。MVC 可以通过查找匹配的类型名称的模板来使用约定于配置的类型匹配。 这允许您创建的模板，会自动设置数据格式不使用任何属性或代码在所有情况下。 在本教程的此部分中，你将创建自动应用于类型的模型属性的模板[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)。 无需使用一个属性或其他配置来指定应使用模板来呈现类型的所有模型属性[DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)。

您还将学习一种方法来自定义的单个属性或甚至是单个字段的显示。

若要开始，让我们删除现有的格式设置信息，并在应用程序中显示完整的日期。

打开*Movie.cs*文件并注释掉`DataType`特性，可以在`ReleaseDate`属性：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

按 Ctrl+F5 运行应用程序。

请注意，`ReleaseDate`属性现在将显示日期和时间，因为这是默认值时未不提供任何格式设置信息。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>用于测试新的模板添加 CSS 样式

创建用于设置日期格式的模板之前，你将添加一些 CSS 样式规则可应用于新的模板。 这些将帮助您验证在呈现的页面正在使用的新模板。

打开*Content\Site.cs*s 文件，并将以下 CSS 规则添加到文件的底部：

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>添加日期时间的显示模板

现在可以创建新模板。 在中*视图 \ 电影*文件夹中，创建*DisplayTemplates*文件夹。

在中*views/shared*文件夹中，创建*DisplayTemplates*文件夹和一个*EditorTemplates*文件夹。

中的显示模板*Views\Shared\DisplayTemplates*文件夹将由所有控制器。 中的显示模板*Views\Movie\DisplayTemplates*将仅可由使用文件夹`Movie`控制器。 (如果具有相同名称的模板出现在这两个文件夹中的模板*Views\Movie\DisplayTemplates*文件夹 — 也就是说，更具体的模板-将优先于返回的视图的`Movie`控制器。)

在中**解决方案资源管理器**，展开*视图*文件夹中，展开*共享*文件夹，，然后右键单击*Views\Shared\DisplayTemplates*文件夹。

单击**外**，然后单击**视图**。 **添加视图**显示对话框。

在中**视图名称**框中，键入`DateTime`。 （您必须使用此名称以匹配类型的名称。）

选择**创建为分部视图**复选框。 请确保**使用布局或母版页页**并**创建强类型化视图**不选中复选框。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

单击 **添加**。 一个*添加*在中创建模板*Views\Shared\DisplayTemplates*。

下图显示*视图*中的文件夹**解决方案资源管理器**后`DateTime`创建显示和编辑器的模板。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

打开*Views\Shared\DisplayTemplates\DateTime.cshtml*文件，并添加以下标记，使用[String.Format](https://msdn.microsoft.com/library/system.string.format.aspx)方法设置为不包括的时间日期的格式属性。 (`{0:d}`格式指定短日期格式。)

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

重复此步骤以创建`DateTime`中的模板*Views\Movie\DisplayTemplates*文件夹。 使用中的以下代码*Views\Movie\DisplayTemplates\DateTime.cshtml*文件。

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` CSS 类将导致日期显示为红色粗体文本。 您添加`loud-1`就像是暂时措施，以便你可以轻松查看此特定模板中使用时的 CSS 类。

所做的创建和自定义模板，ASP.NET 将用来显示日期。 更多常规模板 (在*Views\Shared\DisplayTemplates*文件夹) 显示简单的短日期。 专门用于模板`Movie`控制器 (在*Views\Movies\DisplayTemplates*文件夹) 也设置格式的短日期显示为红色粗体文本。

按 Ctrl+F5 运行应用程序。 在浏览器呈现应用程序的索引视图。

`ReleaseDate`属性现在以红色粗体不包括的时间显示的日期。这可帮助你确认`DateTime`中的模板化帮助器*Views\Movies\DisplayTemplates*转移选择文件夹`DateTime`共享文件夹中的模板化帮助器 (*Views\Shared\DisplayTemplates*)。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

现在重命名*Views\Movies\DisplayTemplates\DateTime.cshtml*的文件*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*。

按 Ctrl+F5 运行应用程序。

这一次`ReleaseDate`属性将显示日期不包括的时间，而无需红色粗体日期。 这说明了数据的名称的模板类型 (在这种情况下`DateTime`) 会自动使用来显示该类型的所有模型属性。 重命名后*添加*文件为*LoudDateTime.cshtml*，ASP.NET 无法再找到中的模板*Views\Movies\DisplayTemplates*文件夹中，因此使用它*添加*模板从 * Views\Movies\Shared\*文件夹。

（模板匹配是不区分大小写，因此无法创建模板文件的名称与任何大小写。 例如， *DATETIME.chstml，添加*，并*添加*将所有匹配`DateTime`类型。)

若要查看： 在此情况下，`ReleaseDate`正在使用显示字段*Views\Movies\DisplayTemplates\DateTime.cshtml*模板，其中使用短日期格式显示数据，但否则会添加任何特殊格式。

### <a name="using-uihint-to-specify-a-display-template"></a>使用 UIHint 指定显示模板

如果 web 应用程序具有许多`DateTime`字段和默认情况下你想要仅限日期的格式显示全部或大部分它们*添加*模板是一个不错的方法。 但是，如果您有几个日期想要显示完整的日期和时间？ 没问题。 可以创建其他模板，并使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性指定的完整的日期和时间格式设置。 然后，您可以有选择地应用该模板。 可以使用[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)属性在模型级别或您可以指定在视图内的模板。 在本部分中，您将了解如何使用`UIHint`特性来有选择地更改某些情况下的日期时间字段的格式设置。

打开*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*文件和现有代码替换为以下：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

这会导致要显示的完整的日期和时间，并将绿色和大型会使文本的 CSS 类。

打开*Movie.cs*文件，并添加[UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx)归于`ReleaseDate`属性，如下面的示例中所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

这将告知 ASP.NET MVC 的显示时`ReleaseDate`属性 (具体而言，并不只是任何`DateTime`对象)，它应使用*LoudDateTime.cshtml*模板。

按 Ctrl+F5 运行应用程序。

请注意，`ReleaseDate`属性现在显示的日期和时间，绿色字体大小。

返回到`UIHint`中的属性*Movie.cs*文件，并对它进行注释，因此*LoudDateTime.cshtml*不会使用模板。 再次运行该应用程序。 发布日期不会显示大型和绿色。 这将验证该*Views\Shared\DisplayTemplates\DateTime.cshtml* Index 和 Details 视图中使用模板。

前面曾提到，您还可以应用在视图中，这样就可以将模板应用到某些数据的单个实例模板。 打开*Views\Movies\Details.cshtml*视图。 添加`"LoudDateTime"`的第二个参数[Html.DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx)寻求`ReleaseDate`字段。 完整代码如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

此步骤指定`LoudDateTime`模板应该用于显示模型属性，而不考虑哪些属性应用于模型。

按 Ctrl+F5 运行应用程序。

验证是否正在使用影片索引页*Views\Shared\DisplayTemplates\DateTime.cshtml*模板 （红色粗体） 和*Movie\Details*网页使用的*Views\Movies\DisplayTemplates\LoudDateTime.cshtml*模板 （大型和绿色）。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

在下一部分中，将创建复杂类型的模板。

> [!div class="step-by-step"]
> [上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [下一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
