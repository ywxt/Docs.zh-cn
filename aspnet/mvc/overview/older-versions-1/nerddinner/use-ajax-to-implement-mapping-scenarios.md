---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: 使用 AJAX 实现映射方案 |Microsoft Docs
author: microsoft
description: 步骤 11 显示了如何将 AJAX 映射支持集成到我们 NerdDinner 的应用程序，使得创建、 编辑或查看 dinners，若要查看 l 的用户...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 173ba551ca453ad46dbfd83ce1a2eb4a9b8eba3f
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374287"
---
<a name="use-ajax-to-implement-mapping-scenarios"></a>使用 AJAX 实现映射方案
====================
by [Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是一种免费的步骤 11 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。
> 
> 步骤 11 显示了如何将 AJAX 映射支持集成到我们 NerdDinner 的应用程序，使得创建、 编辑或查看 dinners，若要以图形方式查看 dinner 的位置的用户。
> 
> 如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。


## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner 步骤 11： 将集成的 AJAX 映射

我们现在将使我们的应用程序一些更直观地令人兴奋的通过集成的 AJAX 映射支持。 这将使创建、 编辑或查看 dinners，若要以图形方式查看 dinner 的位置的用户。

### <a name="creating-a-map-partial-view"></a>创建映射分部视图

我们将在我们的应用程序的多个位置中使用映射功能。 保留我们的代码 DRY 我们将封装在单一的部分模板，我们可以重新使用跨多个控制器操作和视图中的常见映射功能。 我们将此分部视图"map.ascx"命名和创建 \Views\Dinners 目录中。

我们可以创建 map.ascx 部分 \Views\Dinners 目录上右键单击并选择添加-&gt;查看菜单命令。 我们将视图命名为"Map.ascx"，检查为分部视图，并指示我们要将其传递强类型化"Dinner"model 类：

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

当我们单击"添加"按钮时将创建我们部分的模板。 然后，我们将更新 Map.ascx 文件具有以下内容：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

第一个&lt;脚本&gt;引用指向 Microsoft 虚拟地球 6.2 映射库。 第二个&lt;脚本&gt;引用到 map.js 我们稍后将创建该文件将封装我们常见的 Javascript 映射逻辑点。 &lt;D i v id ="theMap"&gt;元素是 Virtual Earth 将用于承载该映射的 HTML 容器。

然后，我们嵌入&lt;脚本&gt;包含特定于此视图的两个 JavaScript 函数的块。 第一个函数使用 jQuery 来布置页面准备好运行客户端脚本时执行的函数。 调用 LoadMap() 帮助器函数，我们将在我们 Map.js 的脚本文件加载 virtual earth 地图控件内定义。 第二个函数是将 pin 添加到标识的位置映射一个回调事件处理程序。

请注意我们如何使用服务器端&lt;%= %&gt;要嵌入的纬度和经度的 Dinner 我们想要将映射到 JavaScript 的客户端脚本块内的块。 这是输出可由客户端脚本 （而无需单独 AJAX 调用回发到服务器中检索值 – 这可以更快） 的动态值的有用技术。 &lt;%= %&gt;块将执行服务器 – 上呈现视图时，并因此的 html 输出只是最终将有嵌入的 JavaScript 值 (例如： var 纬度 = 47.64312;)。

### <a name="creating-a-mapjs-utility-library"></a>创建 Map.js 的实用程序库

让我们现在创建 Map.js 文件，我们可以用来封装我们的地图的 JavaScript 功能 （并实现更高版本的 LoadMap 和 LoadPin 方法）。 我们可以执行此操作上的 \Scripts 目录中我们的项目，右键单击，然后选择"添加-&gt;新项"菜单命令，选择 JScript 项目，并将其命名为"Map.js"。

下面是我们将添加的 JavaScript 代码将与 Virtual Earth 可以显示我们的地图和为我们 dinners 向其添加位置 pin 进行交互的 Map.js 文件：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>与创建和编辑窗体集成映射

我们现在将与我们现有的创建和编辑方案集成映射支持。 好消息是这是非常简单的待办事项，并且不需要我们要更改任何控制器代码。 由于我们创建和编辑的视图共享常见"DinnerForm"分部视图来实现 dinner 窗体用户界面，我们可以在一个位置添加映射，并让使用它的这两种我们创建和编辑方案。

我们只需待办事项是打开 \Views\Dinners\DinnerForm.ascx 分部视图，并将其更新为包括新地图部分。 下面是添加映射后更新的 DinnerForm 外观 (注意： 为简洁起见以下代码段中省略了 HTML 窗体元素):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

上面部分 DinnerForm 采用"DinnerFormViewModel"类型的对象作为其模型类型，（因为它需要一个 Dinner 对象，以及 SelectList 来填充 dropdownlist 的国家/地区）。 我们的地图部分只是需要类型"Dinner"的对象作为其模型的类型，并因此时呈现地图部分我们将仅的 Dinner 子属性 DinnerFormViewModel 向其传递：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

我们添加到要附加到"地址"HTML 文本框的"模糊"事件部分使用 jQuery 的 JavaScript 函数。 您可能听说过"焦点"激发事件，当用户单击或选项卡在文本框。 相反是激发用户退出文本框时的"模糊"事件。 当发生此情况，而绘制地图上的新地址位置时，上述事件处理程序清除纬度和经度文本框值。 然后，我们 map.js 文件内定义一个回调事件处理程序将更新我们使用基于我们赋给它的地址的虚拟地球返回值的窗体上的经度和纬度的 textbox。

和现在我们我们再次运行应用程序并单击"主机 Dinner"选项卡将介绍的默认值将映射与我们的标准 Dinner 窗体元素一起显示：

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

后，我们键入一个地址，然后按 tab 离开，映射将动态更新以显示该位置，然后我们的事件处理程序将填充的位置值的纬度/经度文本框：

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

如果保存新 dinner，然后重新打开以进行编辑，我们会发现在页面加载时显示的映射位置：

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

每次更改地址字段时，将更新映射和纬度/经度坐标。

现在，该地图显示 Dinner 位置，我们还可以从正在可见文本框以改为隐藏的元素 （因为映射自动更新其每次输入一个地址时） 更改的纬度和经度的窗体字段。 待办事项此我们将切换从使用 Html.TextBox() HTML 帮助器使用 Html.Hidden() 帮助器方法：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

和现在我们窗体更具用户友好性并避免显示原始纬度/经度 （此时，仍将它们存储在数据库中每个 Dinner 使用）：

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>将地图集成的详细信息视图

现在，我们已让我们与我们创建和编辑的方案，集成还将其与我们的详细信息方案集成的映射。 我们需要待办事项，只需调用&lt;%html.renderpartial("map"); %&gt;的详细信息视图中。

下面是完整的详细信息视图 （具有映射的集成） 的源代码如下所示：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

现在当用户导航到 /Dinners/详细信息 / [id] URL 他们将看到有关 dinner dinner 在地图上的位置的详细信息 （完成，但一个图钉，当悬停在显示的 dinner 标题和它的地址），并且具有指向 RSVP fo 的 AJAX 链接r 它：

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>在我们的数据库和存储库中实现位置搜索

为了完成我们的 AJAX 实现，让我们将映射添加到允许用户以图形方式搜索 dinners 接近的人们的应用程序的主页。

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

我们将首先实现我们有效地执行 Dinners 的基于位置的 radius 搜索的数据库和数据的存储库层中的支持。 我们可以使用新[地理空间功能的 SQL 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx)来实现此操作，或者我们可以使用 Gary Dryden 讨论文章中的 SQL 函数方法或： [ http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx ](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx)和 Rob conery 专攻有关使用 LINQ to SQL 使用此处发表： [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

若要实现这种技术，我们将打开"服务器资源管理器"在 Visual Studio 中，选择 NerdDinner 的数据库，然后右键单击"函数"下的子节点并选择要创建一个新"标量值函数":

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

然后粘贴以下 DistanceBetween 函数中：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

然后，我们将在 SQL Server 中，我们将调用"NearestDinners"创建新的表值函数：

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

此"NearestDinners"表函数使用 DistanceBetween 帮助器函数来返回所有 Dinners 内 100 英里的纬度和经度我们提供它：

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

若要调用此函数，我们将首先打开 LINQ to SQL 设计器通过双击我们 \Models 目录内 NerdDinner.dbml 文件：

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

然后，我们会将 NearestDinners 和 DistanceBetween 函数拖到 LINQ 到 SQL 设计器中，这将导致它们要作为我们 LINQ 的方法添加到 SQL NerdDinnerDataContext 类：

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

我们可以在我们使用 NearestDinner 函数以返回即将推出的 DinnerRepository 类公开"FindByLocation"查询方法内的指定位置的 100 英里的 Dinners:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>实现基于 JSON 的 AJAX 搜索操作方法

我们现在将实现控制器操作方法都使用了新的 FindByLocation() 存储库方法以返回可用于填充地图的 Dinner 数据的列表。 我们将使此操作方法返回返回 Dinner 数据采用 JSON （JavaScript 对象表示法） 格式，以便它可以轻松地操作客户端上使用 JavaScript。

若要实现这一点，我们将创建一个新"SearchController"类 \Controllers 目录上右键单击并选择添加-&gt;控制器菜单命令。 然后，我们将实现内新 SearchController 类，如下面的"SearchByLocation"操作方法：

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

SearchController SearchByLocation 操作方法在内部调用 DinnerRespository 获取一系列附近 dinners FindByLocation 方法。 而不是 Dinner 对象直接返回到客户端，不过，它改为返回 JsonDinner 对象。 JsonDinner 类公开了一部分 Dinner 属性 (例如： 出于安全原因，它并不公开为 dinner 已接受的人员的名称)。 它还包括一个 RSVPCount 属性不存在上 Dinner – 和其动态计算通过关联与特定 dinner 的 RSVP 对象的计数。

我们然后控制器基类上使用 json （） 帮助器方法返回 dinners 使用基于 JSON 的传输格式的序列。 JSON 是用于表示简单的数据结构以标准文本格式。 下面是 JSON 格式的两个 JsonDinner 对象列表如下所示从我们的操作方法返回时的示例：

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>调用使用 jQuery 的基于 JSON 的 AJAX 方法

我们现已准备好更新主页上的 NerdDinner 应用程序使用 SearchController SearchByLocation 操作方法。 待办事项，我们将打开 /Views/Home/Index.aspx 视图模板并将其更新为具有一个 textbox，搜索按钮，我们的地图，和一个&lt;div&gt;名为 dinnerList 元素：

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

然后，我们可以将两个 JavaScript 函数添加到页面：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

首次加载页面时，第一个 JavaScript 函数将加载映射。 JavaScript 第二个 JavaScript 函数绑定单击搜索按钮上的事件处理程序。 当按钮按下它将调用我们将添加到我们的 Map.js 文件的 FindDinnersGivenLocation() JavaScript 函数：

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

此 FindDinnersGivenLocation() 函数将调用映射。在要居中于输入的位置的虚拟地球控件 find （)。 当虚拟地球地图服务返回时，该映射。Find （） 方法调用我们作为最后一个参数传递它 callbackUpdateMapDinners 回调方法。

CallbackUpdateMapDinners() 方法是在其中完成实际工作。 它使用 jQuery 的 $.post() 帮助器方法来执行对我们 SearchController SearchByLocation() 操作方法-将其传递的纬度和经度的新居中后的地图的 AJAX 调用。 它定义 $.post() 帮助器方法完成时，将调用一个内联函数，并且从操作方法将传递它使用名为"dinners"的变量 SearchByLocation() 返回 JSON 格式的 dinner 结果。 然后在各个每个返回 dinner foreach，并使用 dinner 的纬度和经度和其他属性在地图上添加一个新的 pin。 它还添加到 HTML 列表右侧的映射 dinners 的 dinner 条目。 它然后电线向上图钉和 HTML 列表在悬停事件，以便当用户悬停其上时显示有关 dinner 的详细信息：

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

和现在我们运行该应用程序并访问主页上我们将看到一幅地图。 当我们进入的城市名称映射将显示办公电话附近即将推出的 dinners:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

将鼠标悬停 dinner 将显示其详细信息。

单击 Dinner 标题在气泡或 HTML 列表中的右侧端上将导航我们到 dinner – 我们可以然后根据需要响应：

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>下一步

我们现在实现了所有我们 NerdDinner 应用程序的应用程序功能。 让我们现在看如何可以启用自动单元测试它。

> [!div class="step-by-step"]
> [上一页](use-ajax-to-deliver-dynamic-updates.md)
> [下一页](enable-automated-unit-testing.md)
