---
uid: mvc/overview/older-versions/aspnet-mvc-4-mobile-features
title: ASP.NET MVC 4 移动功能 |Microsoft Docs
author: Rick-Anderson
description: 现在是通过在部署 ASP.NET MVC 5 移动 Web 应用程序在 Azure 网站的代码示例本教程的 MVC 5 版本。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 27dc4fc8-1b51-43b0-933f-fc1b52476523
msc.legacyurl: /mvc/overview/older-versions/aspnet-mvc-4-mobile-features
msc.type: authoredcontent
ms.openlocfilehash: a3cb2414775b2c29617296dcf0c2dc5729153cdd
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834959"
---
<a name="aspnet-mvc-4-mobile-features"></a>ASP.NET MVC 4 移动功能
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 现在没有的代码示例在本教程的 MVC 5 版本[部署 ASP.NET MVC 5 移动 Web 应用程序上 Azure Web Sites](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/)。


本教程将讲述如何使用 ASP.NET MVC 4 Web 应用程序中的移动功能的基础知识。 对于本教程中，可以使用[Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer 或 VWD&quot;)。 如果已有的可以使用 Visual Studio 的专业版。

在开始之前，请确保已安装以下列出的先决条件。

- [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) （推荐） 或 Visual Studio Web Developer Express SP1。 Visual Studio 2012 包含 ASP.NET MVC 4。 如果使用 Visual Web Developer 2010，则必须安装[ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)。

您还需要移动浏览器模拟器。 以下任何版本均可：

- [Windows 7 Phone 仿真程序](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。 （这是本教程中使用的大部分屏幕快照中的仿真程序）。
- 更改用户代理字符串以模拟 iPhone。 请参阅[这](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)博客文章。
- [Opera Mobile Emulator](http://www.opera.com/developer/tools/mobile/)
- [Apple Safari](http://www.apple.com/safari/download/)与用户代理设置为 iPhone。 有关如何将 Safari 中的用户代理设置为"iPhone"的说明，请参阅[如何让 Safari 模拟 IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) David Alison 的博文。

使用 C# 源代码的 visual Studio 项目是可随附于本主题：

- [初学者项目下载](https://go.microsoft.com/fwlink/?linkid=228307&amp;clcid=0x409)
- [已完成项目下载](https://go.microsoft.com/fwlink/?linkid=228306&amp;clcid=0x409)

### <a name="what-youll-build"></a>你将生成

本教程中，您将添加移动功能中提供的简单会议列表应用程序[初学者项目](https://go.microsoft.com/fwlink/?LinkId=228307)。 以下屏幕截图显示了完整的应用程序标记页上，如中所示[Windows 7 Phone Emulator](https://msdn.microsoft.com/library/ff402563(VS.92).aspx)。 请参阅[键盘映射为 Windows Phone 仿真程序](https://msdn.microsoft.com/library/ff754352(v=vs.92).aspx)从而简化了键盘输入。

[![p1_Tags_CompletedProj](aspnet-mvc-4-mobile-features/_static/image2.png)](aspnet-mvc-4-mobile-features/_static/image1.png)

可以使用 Internet Explorer 版本 9 或 10，可通过设置开发移动应用程序的 FireFox 或 Chrome[用户代理字符串](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)。 下图显示了已完成本教程使用模拟 iPhone 的 Internet Explorer。 可以使用 Internet Explorer F-12 开发人员工具和[Fiddler 工具](http://www.fiddler2.com/fiddler2/)来帮助调试应用程序。

![](aspnet-mvc-4-mobile-features/_static/image3.png)

### <a name="skills-youll-learn"></a>你将学习的技能

下面是你将了解：

- ASP.NET MVC 4 模板如何使用 HTML5`viewport`属性和自适应呈现来改善在移动设备上显示。
- 如何创建移动特定视图。
- 如何创建视图切换器之间移动视图与桌面应用程序的视图，允许用户切换。

### <a name="getting-started"></a>入门

下载会议列表应用程序初学者项目使用以下链接：[下载](https://go.microsoft.com/fwlink/?LinkId=228307)。 然后在 Windows 资源管理器中，右键单击*MvcMobile.zip*文件，然后选择**属性**。 在中**MvcMobile.zip 属性**对话框框中，选择**解除阻止**按钮。 (取消阻止您尝试使用的安全警告 *.zip*已从 web 下载的文件。)

![p1_unBlock](aspnet-mvc-4-mobile-features/_static/image4.png)

右键单击*MvcMobile.zip*文件，然后选择**全部提取**来解压缩该文件。 在 Visual Studio 中打开*MvcMobile.sln*文件。

按 CTRL + F5 运行应用程序，会将其显示在桌面浏览器中。 启动移动浏览器模拟器，将会议应用程序的 URL 复制到模拟器，，然后单击**按标记浏览**链接。 如果使用的 Windows Phone 仿真程序，在 URL 栏中单击，然后按暂停键来访问键盘。 下的图显示*AllTags*视图 (选择**按标记浏览**)。

[![p1_browseTag](aspnet-mvc-4-mobile-features/_static/image6.png)](aspnet-mvc-4-mobile-features/_static/image5.png)

显示为在移动设备上一目了然。 选择 ASP.NET 链接。

[![p1_tagged_ASPNET](aspnet-mvc-4-mobile-features/_static/image8.png)](aspnet-mvc-4-mobile-features/_static/image7.png)

ASP.NET 标签视图是显示非常混乱。 例如，**日期**列是很难阅读。 本教程的后面将创建的版本*AllTags*视图，它专门针对移动浏览器并将使显示易读。

注意： 目前存在一个 bug 中移动缓存引擎。 对于生产应用程序，必须安装[固定 DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes)有用的功能包。 请参阅[ASP.NET MVC 4 移动缓存 Bug 固定](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx)有关解决方法的详细信息。

## <a name="css-media-queries"></a>CSS 媒体查询

[CSS 媒体查询](http://www.w3.org/TR/css3-mediaqueries/)CSS 媒体类型的扩展。 它们允许你创建重写特定浏览器 （用户代理） 的默认 CSS 规则的规则。 面向移动浏览器的 CSS 的通用规则定义最大屏幕尺寸。 *Content\Site.css*时创建新的 ASP.NET MVC 4 Internet 项目创建的文件包含以下媒体查询：

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample1.css)]

如果浏览器窗口为 850 像素宽或更小，它将使用在此媒体块中的 CSS 规则。 此类的 CSS 媒体查询可用于更广泛的桌面浏览器显示在设计的默认 CSS 规则比小型 （如移动浏览器） 的浏览器提供 HTML 内容的更好地显示。

## <a name="the-viewport-meta-tag"></a>视区 Meta 标记

大多数移动浏览器定义虚拟浏览器窗口宽度 (*视区*) 这是比移动设备的实际宽度大得多。 这样，移动浏览器以适应整个 web 页内的虚拟显示器。 用户然后可以放大有趣的内容。 但是，如果视区宽度设置为实际设备宽度时，没有缩放是必需的因为内容适应移动浏览器中。

在视区`<meta>`ASP.NET MVC 4 布局文件中的标记将视区设置为设备宽。 以下行显示在视区`<meta>`ASP.NET MVC 4 布局文件中的标记。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample2.html)]

## <a name="examining-the-effect-of-css-media-queries-and-the-viewport-meta-tag"></a>检查 CSS 媒体查询和视区 Meta 标记的效果

打开*views/shared\\_Layout.cshtml*编辑器并注释掉视区中的文件`<meta>`标记。 以下标记显示了注释掉的行。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample3.cshtml)]

打开*MvcMobile\Content\Site.css*文件在编辑器中，并将媒体查询中的最大宽度更改为零像素。 这将防止在移动浏览器中使用的 CSS 规则。 以下行显示了修改后的媒体查询：

[!code-css[Main](aspnet-mvc-4-mobile-features/samples/sample4.css)]

保存所做的更改并浏览到移动浏览器模拟器中的会议应用程序。 在下图中的小文本是删除在视区的结果`<meta>`标记。 使用没有视区`<meta>`标记，在浏览器时将缩小为默认值视区宽度 (850 像素或宽为大多数移动浏览器。)

[![p1_noViewPort](aspnet-mvc-4-mobile-features/_static/image10.png)](aspnet-mvc-4-mobile-features/_static/image9.png)

撤消所做的更改，取消注释在视区`<meta>`布局文件中标记并还原为 850 像素中的媒体查询*Site.css*文件。 保存所做的更改并刷新移动浏览器中，若要验证已还原适合移动应用显示。

在视区`<meta>`标记和 CSS 媒体查询不特定于 ASP.NET MVC 4 中，而您可以在任何 web 应用程序中充分利用这些功能。 但现在被内置到您创建新的 ASP.NET MVC 4 项目时，将生成的文件。

有关视区的详细信息`<meta>`标记中，请参阅[神奇的两个视区 — 第二部分](http://www.quirksmode.org/mobile/viewports2.html)。

下一节中您将了解如何提供移动浏览器特定视图。

## <a name="overriding-views-layouts-and-partial-views"></a>重写视图、 布局和分部视图

在 ASP.NET MVC 4 中的一个重要新功能是针对移动浏览器一般情况下，为单个移动浏览器，或用于任何特定浏览器允许您重写任何视图 （包括布局和分部视图） 的简单机制。 若要提供移动特定视图，可以复制视图文件并添加 *。移动*到的文件的名称。 例如，若要创建移动*索引*视图中，复制*Views\Home\Index.cshtml*到*Views\Home\Index.Mobile.cshtml*。

在本部分中，将创建一个移动特定布局文件。

若要开始，请将复制*views/shared\\_Layout.cshtml*到*views/shared\\_Layout.Mobile.cshtml*。 打开 *\_Layout.Mobile.cshtml*并将更改从标题**MVC4 Conference**到**Conference (Mobile)**。

在每个`Html.ActionLink`调用中，删除"浏览者"中的每个链接*ActionLink*。 下面的代码显示移动布局文件的已完成的正文部分。

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample5.cshtml)]

复制*Views\Home\AllTags.cshtml*的文件*Views\Home\AllTags.Mobile.cshtml*。 打开新文件并更改`<h2>`元素从"Tags"到"Tags (M)":

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample6.html)]

浏览到标签页使用桌面浏览器和移动浏览器模拟器。 移动浏览器模拟器显示你所做的两个更改。

[![p2m_layoutTags.mobile](aspnet-mvc-4-mobile-features/_static/image12.png)](aspnet-mvc-4-mobile-features/_static/image11.png)

与此相反，桌面显示并未变化。

[![p2_layoutTagsDesktop](aspnet-mvc-4-mobile-features/_static/image14.png)](aspnet-mvc-4-mobile-features/_static/image13.png)

## <a name="browser-specific-views"></a>特定于浏览器视图

除了移动特定和特定于桌面的视图中，可以创建单个浏览器的视图。 例如，您可以创建专门针对 iPhone 浏览器的视图。 在本部分中，您将创建为 iPhone 浏览器和 iPhone 版本的布局*AllTags*视图。

打开*Global.asax*文件，并将以下代码添加到`Application_Start`方法。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample7.cs)]

此代码定义名为"iPhone"，将针对每个传入请求匹配的新显示模式。 如果传入请求与定义 （即，如果用户代理包含字符串"iPhone"） 的条件相匹配，ASP.NET MVC 将查找名称中包含"iPhone"后缀的视图。

在代码中，右键单击`DefaultDisplayMode`，选择**解决**，然后选择`using System.Web.WebPages;`。 这会添加对的引用`System.Web.WebPages`命名空间，它正是`DisplayModes`和`DefaultDisplayMode`类型定义。

[![p2_resolve](aspnet-mvc-4-mobile-features/_static/image16.png)](aspnet-mvc-4-mobile-features/_static/image15.png)

或者，只需手动添加以下行将对`using`文件部分。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample8.cs)]

完整内容*Global.asax*文件如下所示。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample9.cs)]

保存更改。 复制*MvcMobile\Views\Shared\\_Layout.Mobile.cshtml*的文件*MvcMobile\Views\Shared\\_Layout.iPhone.cshtml*。 打开新文件，然后将更改`h1`从标题`Conference (Mobile)`到`Conference (iPhone)`。

复制*MvcMobile\Views\Home\AllTags.Mobile.cshtml*的文件*MvcMobile\Views\Home\AllTags.iPhone.cshtml*。 在新的文件中，更改`<h2>`元素从"Tags (M)"为"Tags (iPhone)"。

运行该应用程序。 运行移动浏览器模拟器，请确保其用户代理设置为"iPhone"，并浏览到*AllTags*视图。 以下屏幕截图显示*AllTags*视图中呈现[Safari](http://www.apple.com/safari/download/)浏览器。 您可以下载有关 Windows Safari[此处](https://support.apple.com/kb/DL1531)。

[![p2_iphoneView](aspnet-mvc-4-mobile-features/_static/image18.png)](aspnet-mvc-4-mobile-features/_static/image17.png)

在本部分中我们已了解如何创建移动布局和视图以及如何创建布局和用于特定设备，例如 iPhone 视图。 下一节中您将了解如何利用 jQuery Mobile 的多个极具吸引力的移动视图。

## <a name="using-jquery-mobile"></a>使用 jQuery Mobile

[的 jQuery Mobile](http://jquerymobile.com/demos/1.0b3/#/demos/1.0b3/docs/about/intro.html)库提供了适用于所有主要移动浏览器用户界面框架。 jQuery Mobile 适用*渐进式增强*对支持 CSS 和 JavaScript 的移动浏览器。 渐进增强允许所有浏览器显示网页的基本内容，同时允许更强大的浏览器和设备拥有更丰富的显示。 附带的 jQuery Mobile 的 JavaScript 和 CSS 文件的样式来适应移动浏览器，无需对标记做任何更改的许多元素。

在本部分中，你将安装*jQuery.Mobile.MVC* NuGet 包，可安装 jQuery Mobile 和视图切换器小组件。

若要开始，删除*共享\\_Layout.Mobile.cshtml*并*共享\\_Layout.iPhone.cshtml*前面创建的文件。

重命名*Views\Home\AllTags.Mobile.cshtml*并*Views\Home\AllTags.iPhone.cshtml*文件到*Views\Home\AllTags.iPhone.cshtml.hide*和*Views\Home\AllTags.Mobile.cshtml.hide*。 因为文件不再具有 *.cshtml*扩展，它们不会用于 ASP.NET MVC 运行时呈现*AllTags*视图。

安装*jQuery.Mobile.MVC* NuGet 包通过执行此操作：

1. 从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。

    [![p3_packageMgr](aspnet-mvc-4-mobile-features/_static/image20.png)](aspnet-mvc-4-mobile-features/_static/image19.png)
2. 在中**程序包管理器控制台**，输入 `Install-Package jQuery.Mobile.MVC -version 1.0.0`

下图显示了添加和更改到 MvcMobile 项目 jQuery.Mobile.MVC NuGet 包的文件。 [添加] 追加的文件的名称后添加的文件。 图像不会显示 GIF 和 PNG 文件添加到*Content\images*文件夹。

![](aspnet-mvc-4-mobile-features/_static/image21.png)

JQuery.Mobile.MVC NuGet 程序包将安装以下：

- *应用程序\_Start\BundleMobileConfig.cs*文件，该引用添加的 jQuery JavaScript 和 CSS 文件所需文件。 必须按照下面的说明并引用该文件中定义的移动捆绑。
- jQuery Mobile CSS 文件。
- 一个`ViewSwitcher`控制器小组件 (*Controllers\ViewSwitcherController.cs*)。
- jQuery Mobile JavaScript 文件。
- JQuery Mobile 样式的布局文件 (*views/shared\\_Layout.Mobile.cshtml*)。
- 视图切换器分部视图 *(MvcMobile\Views\Shared\\_ViewSwitcher.cshtml*)，它提供要从桌面视图，反之亦然和移动视图切换每个页面顶部的链接。
- 多个<em>.png</em>并<em>.gif</em>图像中的文件<em>Content\images</em>文件夹。

打开*Global.asax*文件，并添加以下代码的最后一行作为`Application_Start`方法。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample10.cs)]

下面的代码演示的完整*Global.asax*文件。

[!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample11.cs?highlight=26)]

> [!NOTE]
> 如果使用 Internet Explorer 9，并且未看到`BundleMobileConfig`黄色突出显示上面一行中，单击[兼容性视图按钮](https://windows.microsoft.com/windows7/How-to-use-Compatibility-View-in-Internet-Explorer-9)![（关闭） 的兼容性视图按钮的图片](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "（关闭） 的兼容性视图按钮的图片")在 IE 中来使图标更改大纲![（关闭） 的兼容性视图按钮的图片](http://res2.windows.microsoft.com/resbox/en/Windows 7/main/f080e77f-9b66-4ac8-9af0-803c4f8a859c_15.jpg "（关闭） 的兼容性视图按钮的图片")为纯色![（上） 的兼容性视图按钮的图片](http://res1.windows.microsoft.com/resbox/en/Windows 7/main/156805ff-3130-481b-a12d-4d3a96470f36_14.jpg "（上） 的兼容性视图按钮的图片")。 另外，还可以在 FireFox 或 Chrome 中查看本教程。


打开*MvcMobile\Views\Shared\\_Layout.Mobile.cshtml*文件，并添加以下标记直接后的`Html.Partial`调用：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample12.cshtml)]

完整*MvcMobile\Views\Shared\\_Layout.Mobile.cshtml*文件如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample13.cshtml)]

生成应用程序，并在移动浏览器模拟器浏览到*AllTags*视图。 你看到以下信息：

[![p3_afterNuGet](aspnet-mvc-4-mobile-features/_static/image23.png)](aspnet-mvc-4-mobile-features/_static/image22.png)

> [!NOTE]
> 您可以调试移动特定代码通过[将用户代理字符串设置](http://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)对于 IE 或 Chrome 到 iPhone，然后使用 F-12 开发人员工具。 如果在移动浏览器不会显示**主页**，**演讲者**，**标记**，以及**日期**链接，为按钮、 对 jQuery Mobile 的引用脚本和 CSS 文件可能不会正确。


除了样式发生改变，则请参阅**显示移动视图**以及允许您从移动视图切换到桌面视图的链接。 选择**桌面视图**显示链接和桌面视图。

[![p3_desktopView](aspnet-mvc-4-mobile-features/_static/image25.png)](aspnet-mvc-4-mobile-features/_static/image24.png)

桌面视图不提供一种方法来直接导航回移动视图。 你将立即解决的问题。 打开*views/shared\\_Layout.cshtml*文件。 只需在页面下`body`元素中，添加以下代码来呈现视图切换器小组件：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample14.cshtml)]

刷新*AllTags*移动浏览器中的视图。 你现在可以桌面和移动视图间导航。

[![p3_desktopViewWithMobileLink](aspnet-mvc-4-mobile-features/_static/image27.png)](aspnet-mvc-4-mobile-features/_static/image26.png)

> [!NOTE]
> 调试注意： 您可以将以下代码添加到 views/shared 末尾\\_ViewSwitcher.cshtml 来帮助调试视图时使用的浏览器用户代理字符串设置为移动设备。
> 
> [!code-csharp[Main](aspnet-mvc-4-mobile-features/samples/sample15.cs)]
> 
>  并添加以下发往*views/shared\\_Layout.cshtml*文件。  
> 
> [!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample16.html)]


浏览到*AllTags*桌面浏览器中的页。 视图切换器小组件不在桌面浏览器中显示，因为它仅添加到了移动布局页面。 本教程的后面将看到如何将视图切换器小组件添加到桌面视图。

[![p3_desktopBrowser](aspnet-mvc-4-mobile-features/_static/image29.png)](aspnet-mvc-4-mobile-features/_static/image28.png)

## <a name="improving-the-speakers-list"></a>改进发言人列表

在移动浏览器中，选择**扬声器**链接。 因为没有移动视图 (*AllSpeakers.Mobile.cshtml*)，默认发言人 (*AllSpeakers.cshtml*) 使用移动布局视图呈现 ( *\_Layout.Mobile.cshtml*)。

[![p3_speakersDeskTop](aspnet-mvc-4-mobile-features/_static/image31.png)](aspnet-mvc-4-mobile-features/_static/image30.png)

您可以通过设置全局禁止默认 （非移动） 视图在移动布局内呈现`RequireConsistentDisplayMode`到`true`中*视图\\_ViewStart.cshtml*文件，如下：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample17.cshtml)]

当`RequireConsistentDisplayMode`设置为`true`，移动布局 (<em>\_Layout.Mobile.cshtml</em>) 只用于移动视图。 (即，视图文件仅在窗体<em>* * ViewName</em><em>。Mobile.cshtml</em>。)你可能想要设置`RequireConsistentDisplayMode`到`true`如果你的移动布局不太适合你的非移动视图。 以下屏幕截图显示了如何<em>扬声器</em>呈现页面时`RequireConsistentDisplayMode`设置为`true`。

[![p3_speakersConsistent](aspnet-mvc-4-mobile-features/_static/image33.png)](aspnet-mvc-4-mobile-features/_static/image32.png)

可以通过设置禁用视图中一致的显示模式`RequireConsistentDisplayMode`到`false`视图文件中。 中的以下标记*Views\Home\AllSpeakers.cshtml*文件中设置`RequireConsistentDisplayMode`到`false`:

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample18.cshtml)]

## <a name="creating-a-mobile-speakers-view"></a>创建移动发言人视图

正如您刚才看到*扬声器*视图虽然可读，但链接字迹小，不易在移动设备上点击。 在本部分中，您将创建一个移动特定*扬声器*视图看起来像一个现代移动应用程序 — 字迹大、 易于点击链接，而且包含可快速查找发言人的搜索框。

复制*AllSpeakers.cshtml*到*AllSpeakers.Mobile.cshtml*。 打开*AllSpeakers.Mobile.cshtml*文件，移除`<h2>`标题元素。

在中`<ul>`标记中，添加`data-role`属性，并将其值设置为`listview`。 像其他[`data-*`特性](http://html5doctor.com/html5-custom-data-attributes/)，`data-role="listview"`使大型列表项更易于点击。 这是完成的标记如下所示：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample19.cshtml)]

刷新移动浏览器。 更新的视图如下所示：

[![p3_updatedSpeakerView1](aspnet-mvc-4-mobile-features/_static/image35.png)](aspnet-mvc-4-mobile-features/_static/image34.png)

尽管移动视图得到了改进，但很难导航长的发言人列表。 若要解决此问题，在`<ul>`标记中，添加`data-filter`属性，并将其设置为`true`。 下面的代码显示`ul`标记。

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample20.html)]

下图显示了在得到的页面顶部的搜索筛选器框`data-filter`属性。

[![ps_Data_Filter](aspnet-mvc-4-mobile-features/_static/image37.png)](aspnet-mvc-4-mobile-features/_static/image36.png)

在搜索框中键入每个字母，jQuery Mobile 将筛选显示的列表，如下图中所示。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image39.png)](aspnet-mvc-4-mobile-features/_static/image38.png)

## <a name="improving-the-tags-list"></a>改进标签列表

类似于默认*扬声器*视图中，*标记*视图虽然可读，但链接字迹小，不易在移动设备上点击。 在本部分中，需要修复*标记*视图相同的方式已修复*扬声器*视图。

删除&quot;隐藏&quot;后缀*Views\Home\AllTags.Mobile.cshtml.hide*文件，这样的名称是*Views\Home\AllTags.Mobile.cshtml*。 打开重命名的文件，移除`<h2>`元素。

添加`data-role`并`data-filter`属性到`<ul>`标签，如下所示：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample21.html)]

下图显示了标记页上筛选字母`J`。

[![p3_tags_J](aspnet-mvc-4-mobile-features/_static/image41.png)](aspnet-mvc-4-mobile-features/_static/image40.png)

## <a name="improving-the-dates-list"></a>改进日期列表

可以提高*日期*查看像改进*扬声器*并*标记*视图，以便更轻松地在移动设备上使用。

复制*Views\Home\AllDates.cshtml*的文件*Views\Home\AllDates.Mobile.cshtml*。 打开新文件，移除`<h2>`元素。

添加`data-role="listview"`到`<ul>`标记，如下：

[!code-html[Main](aspnet-mvc-4-mobile-features/samples/sample22.html)]

下图显示了什么**日期**页面的外观`data-role`添加属性。

[![p3_dates1](aspnet-mvc-4-mobile-features/_static/image43.png)](aspnet-mvc-4-mobile-features/_static/image42.png)的内容替换为*Views\Home\AllDates.Mobile.cshtml*文件使用以下代码：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample23.cshtml)]

此代码按日期分组的所有会话。 它为每个新日期创建的列表分隔符，并列出的下一个分隔线的每一天的所有会话。 下面是当此代码运行如下所示：

[![p3_dates2](aspnet-mvc-4-mobile-features/_static/image45.png)](aspnet-mvc-4-mobile-features/_static/image44.png)

## <a name="improving-the-sessionstable-view"></a>改进 SessionsTable 视图

在本部分中，将创建一个移动特定的会话视图。 我们做的更改将比在我们创建的其他视图中更广泛。

在移动浏览器中，点击**演讲者**按钮，然后输入`Sc`在搜索框中。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image47.png)](aspnet-mvc-4-mobile-features/_static/image46.png)

点击**Scott Hanselman**链接。

[![p3_scottHa](aspnet-mvc-4-mobile-features/_static/image49.png)](aspnet-mvc-4-mobile-features/_static/image48.png)

正如您所看到的很难读取在移动浏览器显示。 日期列难以阅读和标签列也超出了视图。 若要解决此问题，将复制*Views\Home\SessionsTable.cshtml*到*Views\Home\SessionsTable.Mobile.cshtml*，然后使用以下代码替换文件的内容：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample24.cshtml)]

该代码移除了 room 和 tag 列，然后竖式标题、 发言人和日期，以便在移动浏览器中阅读所有此类信息。 下图反映了代码更改。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image51.png)](aspnet-mvc-4-mobile-features/_static/image50.png)

## <a name="improving-the-sessionbycode-view"></a>改进 SessionByCode 视图

最后，将创建一个移动特定的视图*SessionByCode*视图。 在移动浏览器中，点击**演讲者**按钮，然后输入`Sc`在搜索框中。

[![ps_data_filter_SC](aspnet-mvc-4-mobile-features/_static/image53.png)](aspnet-mvc-4-mobile-features/_static/image52.png)

点击**Scott Hanselman**链接。 将显示 Scott Hanselman 的会话。

[![ps_SessionsByScottHa](aspnet-mvc-4-mobile-features/_static/image55.png)](aspnet-mvc-4-mobile-features/_static/image54.png)

选择**An Overview of MS Web Stack of Love**链接。

[![ps_love](aspnet-mvc-4-mobile-features/_static/image57.png)](aspnet-mvc-4-mobile-features/_static/image56.png)

默认桌面视图虽然不错，但仍可以改进。

复制*Views\Home\SessionByCode.cshtml*到*Views\Home\SessionByCode.Mobile.cshtml*的内容替换为和*Views\Home\SessionByCode.Mobile.cshtml*文件使用以下标记：

[!code-cshtml[Main](aspnet-mvc-4-mobile-features/samples/sample25.cshtml)]

新的标记使用`data-role`属性改进视图的布局。

刷新移动浏览器。 下图反映你刚才所做的代码更改：

[![p3_love2](aspnet-mvc-4-mobile-features/_static/image59.png)](aspnet-mvc-4-mobile-features/_static/image58.png)

## <a name="wrapup-and-review"></a>便捷和评审

本教程已介绍了 ASP.NET MVC 4 开发者预览版的新移动功能。 移动功能包括：

- 能够在全局以及针对单个视图重写布局、 视图和分部视图。
- 控制布局和分部重写强制使用`RequireConsistentDisplayMode`属性。
- 移动视图切换器小组件视图比还可以在桌面视图中显示。
- 支持特定浏览器，如 iPhone 浏览器的支持。

## <a name="see-also"></a>请参阅

- [jQuery Mobile](http://jquerymobile.com)站点。
- [jQuery Mobile 概述](http://jquerymobile.com/demos/1.0b3/docs/about/intro.html)
- [W3C 建议移动 Web 应用程序的最佳做法](http://www.w3.org/TR/mwabp/)
- [用于媒体查询的 W3C 候选建议](http://www.w3.org/TR/css3-mediaqueries/)
