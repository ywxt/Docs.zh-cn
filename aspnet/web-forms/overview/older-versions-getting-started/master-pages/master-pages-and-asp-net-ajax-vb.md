---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
title: 母版页和 ASP.NET AJAX (VB) |Microsoft Docs
author: rick-anderson
description: 讨论使用 ASP.NET AJAX 和母版页的选项。 查看使用 ScriptManagerProxy 类;讨论各种 JS 文件加载 dependi...
ms.author: aspnetcontent
ms.date: 07/11/2008
ms.assetid: 0ee9318c-29bb-4d58-b1dc-94e575b8ae10
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
msc.type: authoredcontent
ms.openlocfilehash: e0ec5359c83bf13398a8a935921cc2a319638ef1
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803293"
---
<a name="master-pages-and-aspnet-ajax-vb"></a>母版页和 ASP.NET AJAX (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_VB.zip)或[下载 PDF](http://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_VB.pdf)

> 讨论使用 ASP.NET AJAX 和母版页的选项。 查看使用 ScriptManagerProxy 类;讨论各种 JS 文件的加载方式具体取决于是否在 Master 中使用 ScriptManager 页面或内容页面。


## <a name="introduction"></a>介绍

在过去的几年里，越来越多的开发人员一直在构建启用 AJAX 的 web 应用程序。 一个启用了 AJAX 的网站使用大量相关的 web 技术来提供响应更及时的用户体验。 创建启用了 AJAX 的 ASP.NET 应用程序是非常容易归功于 Microsoft 的 ASP.NET AJAX 框架。 ASP.NET AJAX 内置于 ASP.NET 3.5 和 Visual Studio 2008;它还是作为单独的 ASP.NET 2.0 应用程序的下载可用。

构建使用 ASP.NET AJAX framework 启用了 AJAX 的 web 页面时，你必须将准确地说一个 ScriptManager 控件添加到使用 framework 的每个页面。 顾名思义，ScriptManager 管理启用了 AJAX 的网页中使用的客户端脚本。 至少，ScriptManager 发出指示浏览器下载该构成 ASP.NET AJAX 客户端库的 JavaScript 文件的 HTML。 此外可以用于注册自定义 JavaScript 文件、 支持脚本的 web 服务和自定义应用程序服务的功能。

如果你的站点使用主页面 （如应），您不一定需要将 ScriptManager 控件添加到每个单个内容页;相反，可以将一个 ScriptManager 控件添加到母版页。 本教程演示如何将 ScriptManager 控件添加到母版页。 它还介绍如何使用 ScriptManagerProxy 控件中的特定内容页面注册自定义脚本和脚本服务。

> [!NOTE]
> 本教程不会探讨设计或构建启用 AJAX 的 web 应用程序，ASP.NET AJAX 框架。 使用 AJAX 的详细信息请参阅 ASP.NET AJAX 视频和教程，以及在本教程末尾的更多参考资料部分中列出这些资源。


## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>检查发出 ScriptManager 控件的标记

ScriptManager 控件都会发出该构成 ASP.NET AJAX 客户端库会指示浏览器下载 JavaScript 文件的标记。 它还添加到初始化此库的页面的内联 JavaScript 的位。 以下标记显示了添加到包括 ScriptManager 控件的页面的呈现的输出的内容：


[!code-html[Main](master-pages-and-asp-net-ajax-vb/samples/sample1.html)]

`<script src="url"></script>`标记指示浏览器下载和执行的 JavaScript 文件*url*。 ScriptManager 发出三个此类标记;一个引用的文件`WebResource.axd`，而其他两个引用该文件`ScriptResource.axd`。 这些文件实际存在作为你的网站中的文件。 相反，当这些文件之一的请求到达 web 服务器，ASP.NET 引擎检查查询字符串，并返回适当的 JavaScript 内容。 通过这三个外部 JavaScript 文件提供的脚本构成 ASP.NET AJAX 框架的客户端库。 其他`<script>`标记发出的 ScriptManager 包括初始化此库的内联脚本。

用于使用 ASP.NET AJAX 框架，但不是需要为不使用 framework 的页面的页面至关重要的外部脚本引用和由 ScriptManager 发出的内联脚本。 因此，可能原因是只能将 ScriptManager 添加到这些使用 ASP.NET AJAX 框架的页的理想之选。 和这已足够，但如果必须使用框架的许多页面您就会将 ScriptManager 控件添加到所有页面的重复性任务，至少可以说。 或者，可以将 ScriptManager 添加到主页上，然后将此必要的脚本注入到所有内容页面。 使用此方法时，不需要请记住将 ScriptManager 添加到使用 ASP.NET AJAX 框架，因为它已包含在母版页的新页面。 步骤 1 将 ScriptManager 添加到母版页的演练。

> [!NOTE]
> 如果你计划包括到母版页的用户界面中的 AJAX 功能，然后在这个问题别无选择-必须包括 ScriptManager 母版页中。


将 ScriptManager 添加到母版页的一个缺点是上述脚本将在发出*每个*页上，而不考虑是否需要。 这显然会导致浪费带宽的这些页面的 ScriptManager 包含 （通过母版页） 而不使用 ASP.NET AJAX 框架的任何功能。 但是，带宽被浪费只是多少？

- 发出的 （如上所示） 将 ScriptManager 的实际内容进行合计稍有超过 1 KB。
- 所引用的三个外部脚本文件`<script>`元素，但是，包含大约 450 KB 的未压缩的数据; 使用 gzip 压缩的网站，在此总带宽可以减少近 100 KB。 但是，这些脚本文件为一年，这意味着，只需下载一次缓存由浏览器，然后可以重复使用站点上的其他页中。

在最佳情况下，然后，脚本文件的缓存，总成本时 1KB，这是可以忽略不计。 在最坏的情况下，但是-这当脚本文件具有尚未下载和 web 服务器未使用任何形式的压缩-带宽影响可以忽略不大约 450 KB，其中，可以从第二个或两个通过宽带连接到最多一分钟的任意位置添加 通过拨号调制解调器的用户。 值得高兴的是，由于外部脚本文件由浏览器缓存，因此此坏的情况下很少发生。

> [!NOTE]
> 如果您仍然觉得不舒服置于主页面的 ScriptManager 控件，请考虑 Web 窗体 (`<form runat="server">`母版页中的标记)。 每个 ASP.NET 页，使用回发模型必须包含准确地说是一个 Web 窗体。 添加 Web 窗体添加更多的内容： 一个隐藏的窗体字段的数字`<form>`标记本身，并且如有必要，JavaScript 函数适用于启动来自脚本的回发。 此标记是不必要的不回发的页面。 从母版页删除 Web 窗体并手动将其添加到此需求的每个内容页面可以消除此无关的标记。 但是，Web 窗体母版页中的好处大于让它添加到某些内容页面中不必要地缺点。


## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>步骤 1： 将 ScriptManager 控件添加到母版页

每个网页使用 ASP.NET AJAX 框架必须包含准确地说一个 ScriptManager 控件。 鉴于此要求，通常最好将单个 ScriptManager 控件在母版页上，以便所有内容页面包含自动包含在 ScriptManager 控件。 此外，ScriptManager 必须在任何 ASP.NET AJAX 服务器控件，如 UpdatePanel 和 UpdateProgress 控件之前。 因此，最好将放在 Web 窗体中任何 ContentPlaceHolder 控件之前 ScriptManager。

打开`Site.master`母版页和之前将 ScriptManager 控件添加到 Web 窗体中的页`<div id="topContent">`元素 （请参阅图 1）。 如果使用 Visual Web Developer 2008 或 Visual Studio 2008，ScriptManager 控件位于工具箱的 AJAX 扩展选项卡中。如果使用 Visual Studio 2005，您需要首先安装 ASP.NET AJAX 框架，并将控件添加到工具箱。 请访问 ASP.NET AJAX 下载页上，若要获取 ASP.NET 2.0 框架。

向页面添加 ScriptManager 后, 更改其`ID`从`ScriptManager1`到`MyManager`。


[![将 ScriptManager 添加到母版页](master-pages-and-asp-net-ajax-vb/_static/image2.png)](master-pages-and-asp-net-ajax-vb/_static/image1.png)

**图 01**： 将 ScriptManager 添加到母版页 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image3.png))


## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>步骤 2： 使用 ASP.NET AJAX 框架从内容页

使用 ScriptManager 控件添加到母版页我们现在可以向任何内容页添加 ASP.NET AJAX 框架功能。 让我们创建一个新的 ASP.NET 页面显示 Northwind 数据库中的随机选择的产品。 我们将使用 ASP.NET AJAX 框架的计时器控件来更新此显示每隔 15 秒，显示一个新的产品。

首先，在名为的根目录中创建一个新页面`ShowRandomProduct.aspx`。 别忘了将绑定到此新页`Site.master`母版页。


[![向网站添加新的 ASP.NET 页面](master-pages-and-asp-net-ajax-vb/_static/image5.png)](master-pages-and-asp-net-ajax-vb/_static/image4.png)

**图 02**： 向网站添加新的 ASP.NET 页面 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image6.png))


请记住，在指定标题、 元标记和其他 HTML 标头母版页 [SKM1] 本教程中我们创建一个名为的自定义基本页类`BasePage`如果显式设置生成了页面的标题。 转到`ShowRandomProduct.aspx`页面的代码隐藏类，并将其派生`BasePage`(而不是从`System.Web.UI.Page`)。

最后，更新`Web.sitemap`文件以便包括本课程中的一个条目。 添加以下标记下方`<siteMapNode>`到内容页交互课主机：


[!code-xml[Main](master-pages-and-asp-net-ajax-vb/samples/sample2.xml)]

此加法`<siteMapNode>`元素反映在课程列表 （请参阅图 5）。

### <a name="displaying-a-randomly-selected-product"></a>显示随机选择的产品

返回到`ShowRandomProduct.aspx`。 从设计器中，UpdatePanel 控件从工具箱中拖动到`MainContent`内容控件并设置其`ID`属性设置为`ProductPanel`。 UpdatePanel 表示可通过部分页面回发以异步方式更新在屏幕上的区域。

我们的第一个任务是显示在 UpdatePanel 中随机选择产品的信息。 通过将 DetailsView 控件拖动到 UpdatePanel 启动。 设置 DetailsView 控件`ID`属性设置为`ProductInfo`并将清除其`Height`和`Width`属性。 展开 DetailsView 的智能标记，然后从选择数据源下拉列表，选择要绑定到名为的新 SqlDataSource 控件的 DetailsView `RandomProductDataSource`。


[![绑定到新的 SqlDataSource 控件的 DetailsView](master-pages-and-asp-net-ajax-vb/_static/image8.png)](master-pages-and-asp-net-ajax-vb/_static/image7.png)

**图 03**： 将 DetailsView 绑定到新的 SqlDataSource 控件 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image9.png))


配置要通过连接到 Northwind 数据库的 SqlDataSource 控件`NorthwindConnectionString`（这与从内容页 [SKM2] 教程母版页交互中创建）。 当配置 select 语句选择指定一个自定义 SQL 语句，然后输入以下查询：


[!code-sql[Main](master-pages-and-asp-net-ajax-vb/samples/sample3.sql)]

`TOP 1`中的关键字`SELECT`子句将返回仅由查询返回的第一个记录。 `NEWID()`函数将生成一个新的全局唯一标识符值 (GUID) 并可在`ORDER BY`子句按随机顺序返回表的记录。


[![配置 SqlDataSource 返回单一的随机选择记录](master-pages-and-asp-net-ajax-vb/_static/image11.png)](master-pages-and-asp-net-ajax-vb/_static/image10.png)

**图 04**： 配置 SqlDataSource 以返回一个随机选择记录 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image12.png))


完成向导后，Visual Studio 创建上述查询返回的两个列的 BoundField。 此时页面的声明性标记应类似于下面：


[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample4.aspx)]

图 5 显示了`ShowRandomProduct.aspx`页面的浏览器查看时。 单击浏览器的刷新按钮以重新加载页面;应会看到`ProductName`和`UnitPrice`提供新的随机选择记录的值。


[![显示随机产品的名称和价格](master-pages-and-asp-net-ajax-vb/_static/image14.png)](master-pages-and-asp-net-ajax-vb/_static/image13.png)

**图 05**： 显示随机产品的名称和价格 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image15.png))


### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>自动显示的新产品，每隔 15 秒

ASP.NET AJAX 框架包括在指定的时间; 执行回发的计时器控件在回发计时器的`Tick`引发事件。 如果计时器控件放置在 UpdatePanel 内就会触发部分页面回发时，在此期间，我们可以重新绑定数据到 DetailsView 以显示新的随机选择的产品。

若要实现此目的，计时器从工具箱拖放到 UpdatePanel。 更改计时器`ID`从`Timer1`到`ProductTimer`并将其`Interval`从 60000 到 15000 之间的属性。 `Interval`属性指示回发之间的毫秒数; 将其设置为 15000 导致计时器来触发每隔 15 秒的部分页面回发。 此时计时器的声明性标记应类似于下面：


[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample5.aspx)]

创建计时器的事件处理程序`Tick`事件。 在此事件处理程序需要通过调用 DetailsView 的重新绑定数据到 DetailsView`DataBind`方法。 执行此操作会指示 DetailsView 重新检索其数据源控件中的数据以选择并显示一个新的随机选择记录 （就像时重新加载该页面，通过单击浏览器的刷新按钮）。


[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample6.vb)]

这就是一切就这么简单 ！ 重新访问通过浏览器页面。 最初，显示随机产品的信息。 如果耐心地观察屏幕就会发现，15 秒后，新产品的信息奇迹般地将替换现有的显示。

若要更好地查看这里会发生什么，让我们将添加到显示的时间显示上次更新的 UpdatePanel 的标签控件。 添加 UpdatePanel 内的标签 Web 控件，将其`ID`到`LastUpdateTime`，并清除其`Text`属性。 接下来，为 UpdatePanel 的创建事件处理程序`Load`事件和显示的标签中的当前时间。 (UpdatePanel 的`Load`上每个完整或部分页面回发触发事件。)


[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample7.vb)]

完成此更改后，使用此页包含已加载当前显示的产品的时间。 图 6 显示了页面在首次访问时。 图 7 显示的页更高版本 15 秒后计时器控件具有"勾选了"和 UpdatePanel 刷新以显示有关新产品的信息。


[![随机选择的产品显示在页面加载](master-pages-and-asp-net-ajax-vb/_static/image17.png)](master-pages-and-asp-net-ajax-vb/_static/image16.png)

**图 06**: 随机选择的产品显示在加载页 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image18.png))


[![一个新随机选择的产品，系统会每隔 15 秒](master-pages-and-asp-net-ajax-vb/_static/image20.png)](master-pages-and-asp-net-ajax-vb/_static/image19.png)

**图 07**： 一种新随机选择产品，系统会每隔 15 秒 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image21.png))


## <a name="step-3-using-the-scriptmanagerproxy-control"></a>步骤 3： 使用 ScriptManagerProxy 控件

包括对 ASP.NET AJAX framework 客户端库所需的脚本，以及 ScriptManager 还可以注册自定义 JavaScript 文件，对启用脚本的 Web 服务和自定义身份验证、 授权和配置文件服务的引用。 此类自定义项通常特定于某些页面。 但是，如果在母版页中 ScriptManager 中引用自定义脚本文件、 Web 服务引用或身份验证、 授权或配置文件服务则它们将包括在网站中的所有页中。

若要添加 ScriptManager 相关自定义项在页面的页面基础上使用 ScriptManagerProxy 控件。 可以将 ScriptManagerProxy 添加到内容页并注册自定义 JavaScript 文件、 Web 服务引用时，或身份验证、 授权或从 ScriptManagerProxy; 的配置文件服务注册这些服务的特定内容页效果。

> [!NOTE]
> ASP.NET 页只能存在一个 ScriptManager 控件。 因此，不能将 ScriptManager 控件添加到内容页中，如果 ScriptManager 控件已在母版页中定义。 ScriptManagerProxy 的唯一目的是提供一种方法，开发人员能够在母版页中定义 ScriptManager，但仍具有按页基础上添加 ScriptManager 自定义项的功能。


若要查看操作中的 ScriptManagerProxy 控件，让我们来增强在 UpdatePanel`ShowRandomProduct.aspx`包括使用客户端脚本来暂停或继续计时器控件的按钮。 计时器控件有三个我们可以使用来实现此所需的功能的客户端的方法：

- `_startTimer()` -启动计时器控件
- `_raiseTick()` -从而导致"刻度"的计时器控件回发和引发 Tick 事件在服务器上
- `_stopTimer()` -停止计时器控件

让我们创建一个 JavaScript 文件具有一个名为变量`timerEnabled`和一个名为函数`ToggleTimer`。 `timerEnabled`变量指示计时器控件当前是启用还是禁用; 默认为 true。 `ToggleTimer`函数接受两个输入参数: 暂停/恢复按钮和客户端的参考`id`计时器控件的值。 此函数切换的值`timerEnabled`，则获取计时器控件的引用、 启动或停止计时器 (具体取决于值`timerEnabled`)，并更新到"暂停"或"恢复"按钮的显示文本。 每次单击暂停/恢复按钮时，将调用此函数。

首先创建一个新的文件夹中名为的网站`Scripts`。 接下来，将新文件添加到名为脚本文件夹`TimerScript.js`的 JScript 文件类型。


[![将新的 JavaScript 文件添加到脚本文件夹](master-pages-and-asp-net-ajax-vb/_static/image23.png)](master-pages-and-asp-net-ajax-vb/_static/image22.png)

**图 08**： 添加到新的 JavaScript 文件`Scripts`文件夹 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image24.png))


[![新的 JavaScript 文件已添加到网站](master-pages-and-asp-net-ajax-vb/_static/image26.png)](master-pages-and-asp-net-ajax-vb/_static/image25.png)

**图 09**: 新的 JavaScript 文件已添加到网站 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image27.png))


接下来，添加以下脚本到`TimerScript.js`文件：


[!code-csharp[Main](master-pages-and-asp-net-ajax-vb/samples/sample8.cs)]

现在，我们需要注册此自定义 JavaScript 文件`ShowRandomProduct.aspx`。 返回到`ShowRandomProduct.aspx`和 ScriptManagerProxy 控件添加到页面; 设置其`ID`到`MyManagerProxy`。 若要注册自定义 JavaScript 文件在设计器中选择 ScriptManagerProxy 控件，然后转到属性窗口。 其中一个属性的标题为脚本。 选择此属性将显示在图 10 所示的 ScriptReference 集合编辑器。 单击添加按钮以包括新的脚本引用，然后输入路径属性中的脚本文件路径： `~/Scripts/TimerScript.js`。


[![添加对 ScriptManagerProxy 控件的脚本引用](master-pages-and-asp-net-ajax-vb/_static/image29.png)](master-pages-and-asp-net-ajax-vb/_static/image28.png)

**图 10**： 添加对 ScriptManagerProxy 控件的脚本引用 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image30.png))


添加脚本引用 ScriptManagerProxy 控件的声明性后更新标记，包括`<Scripts>`与单个集合`ScriptReference`条目，为以下代码片段的标记演示：


[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample9.aspx)]

`ScriptReference`条目指示 ScriptManagerProxy 若要在其呈现的标记中包含对 JavaScript 文件的引用。 也就是说，通过注册的自定义脚本中 ScriptManagerProxy`ShowRandomProduct.aspx`页面的呈现的输出现在包括另一个`<script src="url"></script>`标记： `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`。

现在，我们可以调用`ToggleTimer`中定义的函数`TimerScript.js`中的客户端脚本从`ShowRandomProduct.aspx`页。 添加 UpdatePanel 内的以下 HTML:


[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample10.aspx)]

这将显示一个具有文本"暂停"按钮。 每当它单击时，JavaScript 函数`ToggleTimer`调用时，对该按钮的引用传递并`id`计时器控件的值 (`ProductTimer`)。 请注意语法以获取`id`计时器控件的值。 `<%=ProductTimer.ClientID%>` 发出的值`ProductTimer`计时器控件`ClientID`属性。 在内容页 [SKM3] 教程中的控件 ID 命名在我们讨论了服务器端之间的差异`ID`值和生成的客户端`id`值，以及如何`ClientID`返回客户端`id`。

图 11 显示了当首次通过浏览器访问此页。 计时器当前正在运行，并更新显示的产品信息每隔 15 秒。 图 12 显示了屏幕后单击暂停按钮。 单击暂停按钮停止计时器并更新到"恢复"按钮的文本。 产品信息将刷新 （并继续每隔 15 秒刷新一次） 后在用户单击恢复。


[![单击暂停按钮来停止计时器控件](master-pages-and-asp-net-ajax-vb/_static/image32.png)](master-pages-and-asp-net-ajax-vb/_static/image31.png)

**图 11**： 单击暂停按钮来停止计时器控件 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image33.png))


[![单击恢复按钮以重新启动计时器](master-pages-and-asp-net-ajax-vb/_static/image35.png)](master-pages-and-asp-net-ajax-vb/_static/image34.png)

**图 12**： 单击恢复按钮以重新启动计时器 ([单击以查看实际尺寸的图像](master-pages-and-asp-net-ajax-vb/_static/image36.png))


## <a name="summary"></a>总结

构建启用 AJAX 的 web 应用程序使用 ASP.NET AJAX 框架时，命令性每个启用了 AJAX 的 web 页面包括一个 ScriptManager 控件。 为推进此过程，我们可以将 ScriptManager 添加到母版页，而无需记住要添加到每个内容页面的 ScriptManager。 介绍了如何将 ScriptManager 添加母版页时介绍了在内容页面中实现 AJAX 功能的步骤 2 到步骤 1。

如果您需要添加自定义脚本，对启用脚本的 Web 服务的引用或自定义身份验证、 授权或配置文件服务添加到特定的内容页上，为内容页添加 ScriptManagerProxy 控件，然后配置自定义项存在。 步骤 3 介绍了如何使用 ScriptManagerProxy 在特定的内容页面中注册的自定义 JavaScript 文件。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET AJAX 框架](../../../../ajax/index.md)
- [ASP.NET AJAX 教程](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX 视频](../../../videos/aspnet-ajax/index.md)
- [使用 Microsoft ASP.NET AJAX 构建交互式用户界面](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [使用 NEWID 随机排序记录](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [使用计时器控件](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，作者的多个部 asp/ASP.NET 书籍并创办了 4GuysFromRolla.com，一直从事 Microsoft Web 技术自 1998 年起。 Scott 是独立的顾问、 培训师和编写器。 他最新著作是[ *Sams Teach 自己 ASP.NET 3.5 24 小时内*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以在达到 Scott [ mitchell@4GuysFromRolla.com ](mailto:mitchell@4GuysFromRolla.com)或通过他的博客[ http://ScottOnWriting.NET ](http://scottonwriting.net/)。

### <a name="special-thanks-to"></a>特别感谢

很多有用的审阅者已评审本系列教程。 是否有兴趣查看我即将推出的 MSDN 文章？ 如果是这样，给我在行 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](interacting-with-the-content-page-from-the-master-page-vb.md)
> [下一页](specifying-the-master-page-programmatically-vb.md)
