---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 4 部分 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历 ASP.NET MV 中的基础知识...
ms.author: aspnetcontent
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: d50ce517df9bd834203cbd026d31db038cd02038
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835727"
---
<a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>使用 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第 4 部分
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程将讲述如何使用编辑器模板、 显示模板和 jQuery UI datepicker 快捷日历中的 ASP.NET MVC Web 应用程序的基础知识。


### <a name="adding-a-template-for-editing-dates"></a>将模板添加以进行编辑日期

在本部分将创建用于编辑 ASP.NET MVC 显示用于编辑模型属性标记的 UI 时要采用的日期的模板**日期**的枚举[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性。 该模板将呈现仅显示日期;将不显示时间。 在模板中将使用[jQuery UI Datepicker](http://jqueryui.com/demos/datepicker/)弹出日历，以提供一种方法来编辑日期。

若要开始，请打开*Movie.cs*文件，并添加[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性**日期**枚举`ReleaseDate`属性，如下面的代码中所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

此代码会导致`ReleaseDate`没有在这种时间显示模板和编辑模板要显示的字段。 如果你的应用程序包含*date.cshtml*中的模板*Views\Shared\EditorTemplates*文件夹中或在*Views\Movies\EditorTemplates*文件夹中，该模板将用于呈现任何`DateTime`编辑时的属性。 否则内置的 ASP.NET 模板化系统将显示为日期属性。

按 Ctrl+F5 运行应用程序。 选择要验证的发布日期输入的字段显示仅显示日期的编辑链接。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

在中**解决方案资源管理器**，展开*视图*文件夹中，展开*共享*文件夹，，然后右键单击*Views\Shared\EditorTemplates*文件夹。

单击**外**，然后单击**视图**。 **添加视图**显示对话框。

在中**视图名称**框中，键入&quot;日期&quot;。

选择**创建为分部视图**复选框。 请确保**使用布局或母版页页**并**创建强类型化视图**不选中复选框。

单击 **添加**。 *Views\Shared\EditorTemplates\Date.cshtml*创建模板。

将以下代码添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

第一行代码声明的模型要`DateTime`类型。 尽管不需要声明中编辑的模型类型和显示模板，但它是一种最佳做法，以便进行编译时检查传递给视图的模型。 （另一个好处是然后获取 IntelliSense，以在 Visual Studio 中的视图模型。）ASP.NET MVC 如果未声明的模型类型，将其视为[动态](https://msdn.microsoft.com/library/dd264741.aspx)类型，并且没有任何编译时类型检查。 如果声明的模型要`DateTime`类型，它将成为强类型化。

第二行是只需文本显示的 HTML 标记&quot;使用日期模板&quot;之前的日期字段。 你将暂时使用这行以验证正在使用此日期模板。

下一行是[Html.TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)帮助器呈现`input`是文本框中的字段。 帮助程序的第三个参数使用匿名类型设置为文本框中的类`datefield`和类型设置为`date`。 (因为`class`是保留在 C# 中，您需要使用`@`字符来转义`class`C# 分析器中的属性。)

`date`类型为 HTML5 输入的类型，使识别 HTML5 的浏览器可以呈现的 HTML5 日历控件。 稍后将添加一些 JavaScript 以便挂接到 jQuery datepicker`Html.TextBox`元素使用`datefield`类。

按 Ctrl+F5 运行应用程序。 你可以验证`ReleaseDate`编辑视图中的属性使用编辑模板，因为该模板将显示&quot;使用日期模板&quot;之前`ReleaseDate`文本输入框中，此图中所示：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

在浏览器中查看页面的源代码。 (例如，右键单击页并选择**查看源**。)以下示例显示了一些页的标记演示`class`和`type`中呈现的 HTML 属性。

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

返回到*Views\Shared\EditorTemplates\Date.cshtml*模板和删除&quot;使用日期模板&quot;标记。 现在已完成的模板如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>添加 jQuery UI Datepicker 快捷日历使用 NuGet

在本部分中将添加[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)弹出日历到日期编辑模板。 [JQuery UI](http://jqueryui.com/)库对于动画，高级效果和可自定义小组件提供支持。 因为它是基于 jQuery JavaScript 库。 Datepicker 快捷日历，就能轻松自然地输入而不输入字符串中使用的日历的日期。 弹出式日历还限制这些用户法律日期 — 普通文本输入的日期，您可以输入类似`2/33/1999`(年 2 月 33rd，1999年)，但[jQuery UI datepicker](http://jqueryui.com/demos/datepicker/)弹出式日历不允许的。

首先，您必须安装 jQuery UI 库。 若要执行此操作，将使用 NuGet，这是 SP1 版本的 Visual Studio 2010 和 Visual Web Developer 中包含的程序包管理器。

在 Visual Web Developer 中，从**工具**菜单中，选择**库程序包管理器**，然后选择**管理 NuGet 包**。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

注意： 如果**工具**不会显示菜单**库程序包管理器**命令，你需要通过以下上的说明安装 NuGet[安装 NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)页NuGet 网站。   
  
如果使用 Visual Studio 而不是 Visual Web Developer 中，从**工具**菜单中，选择**库程序包管理器**，然后选择**添加库程序包引用**。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

在中**MVCMovie-管理 NuGet 包**对话框中，单击**联机**在左侧选项卡，然后输入&quot;jQuery.UI&quot;在搜索框中。 选择 j**查询 UI 小组件： Datepicker**，然后选择**安装**按钮。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet 会将这些调试版本和缩小的版本的 jQuery UI 核心和 jQuery UI 日期选取器添加到你的项目：

- *jquery.ui.core.js*
- *jquery.ui.core.min.js*
- *jquery.ui.datepicker.js*
- *jquery.ui.datepicker.min.js*

注意： 调试版本 (不包含的文件 *。 min.js*扩展) 可用于调试，但在生产站点中，应包括仅的缩减的版本。

若要实际使用 jQuery 日期选取器，您需要创建将挂接到编辑模板日历小组件的 jQuery 脚本。 在中**解决方案资源管理器**，右键单击*脚本*文件夹，然后选择**添加**，然后**新项**，，然后**JScript文件**。 将文件命名*DatePickerReady.js*。

将以下代码添加到*DatePickerReady.js*文件：

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

如果您不熟悉 jQuery，下面提供了这一功能的简要说明： 第一行是&quot;jQuery 就绪&quot;函数，当已将加载一个页面中的所有 DOM 元素时调用。 第二行选择所有具有类名称的 DOM 元素`datefield`，然后调用`datepicker`为每个函数。 (请记住你添加`datefield`类来*Views\Shared\EditorTemplates\Date.cshtml*本教程前面部分的模板。)

接下来，打开*views/shared\\_Layout.cshtml*文件。 您需要添加对以下文件，以便可以使用日期选取器都是必需的引用：

- *Content/themes/base/jquery.ui.core.css*
- *Content/themes/base/jquery.ui.datepicker.css*
- *Content/themes/base/jquery.ui.theme.css*
- *jquery.ui.core.min.js*
- *jquery.ui.datepicker.min.js*
- *DatePickerReady.js*

下面的示例演示的实际代码应将添加在底部`head`中的元素*Views\Shared\\_Layout.cshtml*文件。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

完整`head`部分如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL 内容帮助器](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法将资源路径转换为绝对路径。 必须使用`@URL.Content`IIS 上运行应用程序时正确引用这些资源。

按 Ctrl+F5 运行应用程序。 选择的编辑链接，然后将插入点定位到**ReleaseDate**字段。 显示的 jQuery UI 快捷日历。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

大多数 jQuery 控件，如 datepicker 可以广泛地自定义。 有关信息，请参阅[可视的自定义： 设计 jQuery UI 主题](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)上[jQuery UI](http://learn.jquery.com/jquery-ui/getting-started/)站点。

### <a name="supporting-the-html5-date-input-control"></a>支持 HTML5 日期输入的控件

因为更多浏览器支持 HTML5，您将想要使用本机 HTML5 输入，如`date`输入元素，并不使用 jQuery UI 日历。 可以将逻辑添加到应用程序以自动使用 HTML5 控件，如果浏览器支持它们。 若要执行此操作，替换的内容*DatePickerReady.js*具有以下文件：

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

此脚本的第一行使用 Modernizr 来验证支持 HTML5 日期输入。 如果不支持，jQuery UI 日期选取器已改为挂钩。 ([Modernizr](http://www.modernizr.com/docs/)是开放源代码 JavaScript 库，检测到的本地实现 HTML5 和 CSS3 的可用性。 Modernizr 包含在您创建任何新 ASP.NET MVC 项目中。）

进行此更改之后，可以通过使用支持 HTML5，如 Opera 11 的浏览器对其进行测试。 运行应用程序使用了 HTML5 兼容的浏览器并编辑电影条目。 HTML5 日期控件代替 jQuery UI 快捷日历：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

由于浏览器的新版本以增量方式实现 HTML5，现在的一个好方法是将代码添加到你的网站可容纳各种各样的 HTML5 支持。 例如，更可靠*DatePickerReady.js*脚本如下所示，可仅部分支持 HTML5 日期控件的你站点的支持浏览器。

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

此脚本选择 HTML5`input`类型的元素`date`不完全支持 HTML5 日期控件。 对于这些元素，它挂接的 jQuery UI 快捷日历，然后改变`type`属性从`date`到`text`。 通过更改`type`属性从`date`到`text`，消除了 HTML5 日期的部分支持。 更加可靠*DatePickerReady.js*脚本，请参阅[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)。

### <a name="adding-nullable-dates-to-the-templates"></a>将为 Null 的日期添加到模板

如果你使用其中一个现有的日期模板，并传递 null 的日期，您将收到运行时错误。 若要使日期模板更可靠，你将更改它们来处理 null 值。 若要支持为 null 的日期，更改中的代码*Views\Shared\DisplayTemplates\DateTime.cshtml*所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

代码模型时也会返回空字符串**null**。

中的代码更改*Views\Shared\EditorTemplates\Date.cshtml*到以下文件：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

当此代码运行时，如果模型不为 null，该模型的`DateTime`使用值。 如果模型为 null，则改为使用当前日期。

### <a name="wrapup"></a>便捷

本教程已介绍 ASP.NET 模板化帮助器的基础知识，并演示如何在 ASP.NET MVC 应用程序中使用 jQuery UI datepicker 快捷日历。 有关详细信息，请尝试以下资源：

- 本地化的信息，请参阅 Rajeesh 的博客[JQueryUI Datepicker 在 ASP.NET MVC 中](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。
- 有关的 jQuery UI 的信息，请参阅[jQuery UI](http://docs.jquery.com/UI)。
- 有关如何将本地化 datepicker 控件的信息，请参阅[UI/Datepicker/本地化](http://docs.jquery.com/UI/Datepicker/Localization)。
- 有关 ASP.NET MVC 模板的详细信息，请参阅 Brad Wilson 的博客系列上[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。 序列针对 ASP.NET MVC 2 编写的尽管材料仍适用于 ASP.NET MVC 的当前版本。

> [!div class="step-by-step"]
> [上一篇](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
