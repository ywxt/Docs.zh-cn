---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: 在具有 ASP.NET Web Pages (Razor) 的图表中显示数据 |Microsoft Docs
author: microsoft
description: 这一章介绍了如何在图表中显示数据。 在上一章节中，您学习了如何以手动，并在网格中显示数据。 这一章介绍了...
ms.author: aspnetcontent
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 161dfa1b2c0676c79baebb00e303e8cb9df1d4e8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812576"
---
<a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>在具有 ASP.NET 网页 (Razor) 的图表中显示数据
====================
by [Microsoft](https://github.com/microsoft)

> 本文介绍如何使用图表来使用 ASP.NET Web Pages (Razor) 网站中显示数据`Chart`帮助器。
> 
> **你将了解**:
> 
> - 如何在图表中显示数据。
> - 如何设置图表使用内置的主题的样式。
> - 如何保存图表以及如何其缓存以提高性能。
> 
> 这些是 ASP.NET 编程一文中引入的功能：
> 
> - `Chart`帮助器。
> 
> > [!NOTE]
> > 在本文中的信息适用于 ASP.NET Web Pages 1.0 和 Web Pages 2。


<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>图表帮助程序

当你想要以图形方式显示数据时，可以使用`Chart`帮助器。 `Chart`帮助器可以呈现在不同的图表类型中显示数据的图像。 格式设置和标签，它支持很多选项。 `Chart`帮助器可以呈现 30 多个类型的图表，其中包括所有类型的图表，您可能熟悉的 Microsoft Excel 或其他工具&#8212;面积图、 条形图、 柱形图、 折线图和饼图中，以及的详细信息专用的图表，如股价图。

| **面积图**![说明： 面积图类型的图片](7-displaying-data-in-a-chart/_static/image1.jpg) | **条形图**![说明： 条形图类型的图片](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **柱形图**![说明： 柱形图类型的图片](7-displaying-data-in-a-chart/_static/image3.jpg) | **折线图**![说明： 行图表类型的图片](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **饼图**![说明： 饼形图类型的图片](7-displaying-data-in-a-chart/_static/image5.jpg) | **股价图**![说明： 股价图类型的图片](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>图表元素

图表显示数据和其他元素，如图例、 轴、 系列和等等。 下图显示了许多你可以自定义时使用的图表元素`Chart`帮助器。 本文演示如何设置一些 （并非所有） 的这些元素。

![显示图表元素的说明： 图片](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>从数据创建图表

在图表中显示的数据可以是从一个数组，从数据库中，从返回的结果或从 XML 文件中的数据。

### <a name="using-an-array"></a>使用数组

中所述[ASP.NET Web Pages 编程使用 Razor 语法简介](https://go.microsoft.com/fwlink/?LinkId=202890)，数组可让您在单个变量中存储类似项的集合。 可以使用数组以包含你想要在图表中包括的数据。

此过程演示如何创建图表数据在数组中，从使用默认图表类型。 它还演示如何显示在页面内的图表。

1. 创建一个名为的新文件*ChartArrayBasic.cshtml*。
2. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    代码首先创建一个新图表，并设置其宽度和高度。 使用指定图表标题`AddTitle`方法。 若要添加数据，请使用`AddSeries`方法。 在此示例中，使用`name`， `xValue`，并`yValues`的参数`AddSeries`方法。 `name`参数显示在图表图例中。 `xValue`参数包含沿图表水平轴显示的数据的数组。 `yValues`参数包含用于绘制图表的垂直点的数据的数组。

    `Write`方法实际将呈现图表。 在这种情况下，这是因为未指定图表类型，`Chart`帮助器将呈现其默认图表，这是柱形图。
3. 在浏览器中运行页。 浏览器将显示图表。 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>使用图表数据的数据库查询

如果要制作图表的信息是在数据库中，您可以运行数据库查询，然后使用结果中的数据创建图表。 此过程演示如何读取和显示项目中创建的数据库中的数据[使用 ASP.NET Web Pages 站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893)。

1. 添加*应用程序\_数据*如果文件夹尚不存在的网站的根文件夹。
2. 在中*应用程序\_数据*文件夹中，添加名为的数据库文件*SmallBakery.sdf*中描述的[使用 ASP.NET Web Pages 站点中的数据库简介](https://go.microsoft.com/fwlink/?LinkId=202893).
3. 创建一个名为的新文件*ChartDataQuery.cshtml*。
4. 使用以下内容替换现有内容：   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    该代码首先打开 SmallBakery 数据库，并将其分配给一个名为变量`db`。 此变量表示`Database`可用于读取和写入到数据库的对象。 接下来，代码将运行 SQL 查询以获取名称和每个产品的价格。 该代码创建一个新图表，并向其传递数据库查询，通过调用图表的`DataBindTable`方法。 此方法采用两个参数：`dataSource`参数是用于查询中的数据和`xField`参数允许您设置的数据列用于图表的 x 轴。

    为使用的替代方法`DataBindTable`方法中，可以使用`AddSeries`方法的`Chart`帮助器。 `AddSeries`方法允许您设置`xValue`和`yValues`参数。 例如，而不是使用`DataBindTable`方法如下：

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    可以使用`AddSeries`方法如下：

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    都呈现相同的结果。 `AddSeries`方法是更灵活，因为你可以更明确指定的图表类型和数据，但`DataBindTable`方法可更轻松地使用如果不需要额外的灵活性。
5. 在浏览器中运行页。 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>使用 XML 数据

用于绘制图表的第三个选项是一个 XML 文件用作图表的数据。 这要求 XML 文件还具有某一架构文件 (*.xsd*文件) 描述的 XML 结构。 此过程演示如何从 XML 文件读取数据。

1. 在中*应用程序\_数据*文件夹中，创建名为的新 XML 文件*data.xml*。
2. 现有的 XML 替换为以下内容，这是一个虚构的公司中的员工有关的一些 XML 数据。 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. 在中*应用程序\_数据*文件夹中，创建名为的新 XML 文件*data.xsd*。 (请注意，扩展此时间是 *.xsd*。)
4. 使用以下内容替换现有的 XML: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. 在该网站的根目录中创建名为的新文件*ChartDataXML.cshtml*。
6. 使用以下内容替换现有内容： 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    代码首先创建`DataSet`对象。 此对象用于管理的数据，从 XML 文件中读取并将其组织根据架构文件中的信息。 (请注意，代码的顶部包含该语句`using SystemData`。 这必需的可以使用`DataSet`对象。 有关详细信息，请参阅[ &quot;Using&quot;语句和完全限定的名称](#SB_UsingStatements)这篇文章中更高版本。)

    接下来，该代码会创建`DataView`对象基于数据集。 数据视图提供了一个对象，该图表可以绑定到&#8212;，它是读取，并绘制。 图表绑定到数据`AddSeries`方法中，为你前面看到的图表数组数据，不同之处在于这一次时`xValue`并`yValues`参数设置为`DataView`对象。

    此示例还演示了如何指定特定图表类型。 在添加数据时`AddSeries`方法，`chartType`参数也设置为显示饼图。
7. 在浏览器中运行页。 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>"Using"语句和完全限定的名称
> 
> 使用 Razor 语法的 ASP.NET Web Pages 基于.NET Framework 包含数以千计的组件 （类）。 若要对它进行管理，可以使用所有这些类，它们的结构到*命名空间*，哪些是有些类似于库。 例如，`System.Web`命名空间包含支持浏览器/服务器通信的类`System.Xml`命名空间包含用于创建和读取 XML 文件的类和`System.Data`命名空间包含用于工作的类使用数据。
> 
> 若要访问.NET Framework 中的任何给定的类，代码需要知道不只是类名，但还的类的命名空间。 例如，若要使用`Chart`帮助器，代码需要查找`System.Web.Helpers.Chart`类，它结合了命名空间 (`System.Web.Helpers`) 与类名称 (`Chart`)。 这称为类的*完全限定*名称&#8212;其完整、 明确位置 vastness 中的.NET framework。 在代码中，这将显示如下：
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> 但是，非常麻烦 （和容易出错） 必须使用这些长、 完全限定的名称，每次想要引用的类或帮助器。 因此，若要使其更易于使用的类名，您可以*导入*你感兴趣，这通常是命名空间是只需少量从.NET Framework 中的多个命名空间。 如果您已导入命名空间，则可以使用只是类名称 (`Chart`) 而不是完全限定名称 (`System.Web.Helpers.Chart`)。 在你的代码运行并遇到一个类名称，它可以查看在只需导入若要查找此类的命名空间中。
> 
> 在您使用 ASP.NET Web Pages 使用 Razor 语法创建网页，通常使用同一组类每次包括`WebPage`类、 各种帮助程序，等等。 若要保存的工作的导入相关命名空间，每次创建网站时，ASP.NET 配置以便自动导入一组核心命名空间为每个网站。 这就是为什么没有处理命名空间或导入到现在; 为止您使用过的所有类都都已为您导入的命名空间中。
> 
> 但是，有时您需要使用不会自动为您导入的命名空间中的类。 这种情况下，您可以使用该类的完全限定的名称，也可以手动导入的命名空间包含类。 若要导入命名空间，请使用`using`语句 (`import`在 Visual Basic 中)，如前面在示例中看到一文。
> 
> 例如，`DataSet`类位于`System.Data`命名空间。 `System.Data`命名空间不是自动提供给 ASP.NET Razor 页面。 因此，若要使用`DataSet`类使用完全限定的名称，则可以使用如下代码：
> 
> `var dataSet = new System.Data.DataSet();`
> 
> 如果您必须使用`DataSet`重复类可以导入此类的命名空间，然后使用在代码中的只是类名称：
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> 您可以添加`using`有你想要引用任何其他.NET Framework 命名空间的语句。 但是，如所述，您无需执行此操作通常情况下，因为您将使用的类的大部分都是自动导入由 ASP.NET 在中使用的命名空间中 *.cshtml*并 *.vbhtml*页。


<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>显示在网页上的图表

在示例中您已了解到目前为止，创建一个图表，然后再直接向浏览器作为图形呈现图表。 在许多情况下，不过，你想要显示的图表作为一部分的页上，而不仅仅是通过在浏览器本身。 若要执行此操作需要两步过程。 第一步是创建图表中，将生成的页面，如您所见。

第二步是在另一页中显示生成的映像。 若要显示的图像，应使用对应的 HTML`<img>`元素，在相同的方式来显示任何图像。 但是，而不是引用 *.jpg*或 *.png*文件中，`<img>`元素引用 *.cshtml*文件，其中包含`Chart`帮助程序，创建的图表。 显示页的运行时，则`<img>`元素获得的输出`Chart`帮助程序，并将呈现图表。

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. 创建名为的文件*ShowChart.cshtml*。
2. 使用以下内容替换现有内容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    该代码使用`<img>`元素以显示你前面创建的图表*ChartArrayBasic.cshtml*文件。
3. 在浏览器中运行 web 页。 *ShowChart.cshtml*文件将显示图表图像中包含的代码基础*ChartArrayBasic.cshtml*文件。

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>设置图表的样式

`Chart`帮助器支持大量的选项允许你自定义图表的外观。 可以设置颜色、 字体、 边框和等等。 若要自定义图表的外观的简单方法是使用*主题*。 主题是信息的指定如何呈现使用字体、 颜色、 标签、 调色板、 边框和效果的图表的集合。 （请注意图表的样式并不表示图表的类型。）

下表列出了内置的主题。

| 主题 | 描述 |
| --- | --- |
| `Vanilla` | 白色背景上显示红色柱形。 |
| `Blue` | 显示蓝色蓝色的渐变背景上的列。 |
| `Green` | 显示蓝绿色渐变背景上的列。 |
| `Yellow` | 显示黄色的渐变背景的橙色列。 |
| `Vanilla3D` | 白色背景上显示三维红色的列。 |

您可以指定要在创建新图表时使用的主题。

1. 创建一个名为的新文件*ChartStyleGreen.cshtml*。
2. 在页中的现有内容替换为以下：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    此代码等同于前面的示例使用的数据库的数据，但将添加`theme`参数创建时`Chart`对象。 下面显示了更改后的代码：

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. 在浏览器中运行页。 你看到与之前相同的数据，但该图表看上去更加完善： 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>保存图表

当你使用`Chart`作为您的帮助器就目前而言此文章介绍了帮助程序在每次调用时它都会重新创建从零开始的图表。 如有必要，该图表的代码还重新查询数据库或重新读取 XML 文件来获取的数据。 在某些情况下，执行此操作可以是一个复杂的操作，例如如果你要查询的数据库很大，或 XML 文件包含大量数据。 即使在图表不会涉及大量数据，动态创建映像的过程将占用服务器资源，并且如果很多人请求的页显示图表，可以有影响对你的网站的性能。

若要帮助你减少创建图表的潜在性能影响，可以创建图表第一次需要它，然后将其保存。 当图表再次需要时，而不是重新生成它，可以只是提取已保存的版本和呈现的。

可以将图表保存在以下方面：

- 缓存中 （在服务器上） 的计算机内存的图表。
- 将图表保存为图像文件。
- 将图表保存为 XML 文件。 此选项可以修改图表，然后将其保存。

### <a name="caching-a-chart"></a>缓存图表

创建图表后，可以对其进行缓存。 缓存图表意味着，它不一定是重新创建，如果需要再次显示。 时将图表保存在缓存中时，你向其提供一个键，它必须是唯一的该图表。

如果在服务器内存不足，可能会去除图表保存到缓存。 此外，如果出于任何原因重新启动你的应用程序清除了缓存。 因此，若要使用缓存图表的标准方法是以始终首先检查在缓存中，是可用，以及如果没有，则若要创建或重新创建它。

1. 在你的网站的根目录，创建名为的文件*ShowCachedChart.cshtml*。
2. 使用以下内容替换现有内容： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    `<img>`标记包含`src`属性，指向*ChartSaveToCache.cshtml*文件，并将密钥传递给查询字符串形式的页。 项包含值&quot;myChartKey&quot;。 *ChartSaveToCache.cshtml*文件包含`Chart`帮助程序创建的图表。 稍后，你将创建此页。

    在页面末尾是一个名为页的链接*ClearCache.cshtml*。 这是还将稍后创建的页。 所需*ClearCache.cshtml*仅以测试此示例中的缓存，不是链接或使用缓存图表时您通常要包括的页面。
3. 在你的网站的根目录，创建名为的新文件*ChartSaveToCache.cshtml*。
4. 使用以下内容替换现有内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    代码首先检查是否任何内容传递作为查询字符串中的密钥值。 因此，该代码尝试通过调用读取缓存图表如果`GetFromCache`方法并将其传递该密钥。 如果事实证明，没有任何缓存下该密钥 （后者会发生第一次请求图表） 中，代码会像往常一样创建图表。 完成图表后，代码将其保存到缓存通过调用`SaveToCache`。 该方法要求的密钥 （因此，图表可以请求更高版本），并且应在缓存中保存图表的时间量。 （将缓存图表的确切时间将取决于何种频率认为它所代表的数据可能会更改。）`SaveToCache`方法还需要`slidingExpiration`参数&#8212;如果将其设置为 true 时，超时计数器将重置每次访问图表。 在这种情况下，这实际上意味着图表的缓存条目过期后用户访问图表的最后一个时间 2 分钟。 （可调过期的替代方法是绝对到期，这意味着缓存项何时过期恰好在 2 分钟后已放入缓存，无论何种频率必须被访问。）

    最后，代码使用`WriteFromCache`方法来提取并呈现来自缓存的图表。 请注意，此方法是外部`if`检查缓存中，因为它将从缓存获取图表，该图表已最初要使用还是必须生成并保存在缓存中的块。

    请注意，在此示例中，`AddTitle`方法包含时间戳。 (它将添加的当前日期和时间&#8212; `DateTime.Now` &#8212;为标题。)
5. 创建一个名为的新页*ClearCache.cshtml*和其内容替换为以下代码：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    使用此页`WebCache`帮助器来删除缓存中的图表*ChartSaveToCache.cshtml*。 如前文所述，通常不必像这样的页面。 要创建在此处仅以使其更易于测试缓存。
6. 运行*ShowCachedChart.cshtml*网页在浏览器中。 该页面显示图表图像基于中包含的代码*ChartSaveToCache.cshtml*文件。 记下的时间戳显示图表标题中。 

    ![说明： 时间戳为图表标题中的基本图表图片](7-displaying-data-in-a-chart/_static/image13.jpg)
7. 关闭浏览器。
8. 运行*ShowCachedChart.cshtml*试。 请注意，时间戳相同与之前一样，这表示图表未重新生成，但已改为从缓存中读取。
9. 在中*ShowCachedChart.cshtml*，单击**清除缓存**链接。 将进入*ClearCache.cshtml*，报告已清除的缓存。
10. 单击**返回到 ShowCachedChart.cshtml**链接，或重新运行*ShowCachedChart.cshtml*从 WebMatrix。 请注意，此时间已更改的时间戳，因为清除缓存。 因此，代码必须重新生成图表，并将其放回缓存。

### <a name="saving-a-chart-as-an-image-file"></a>将图表另存为图像文件

此外可以将图表保存为图像文件 (例如，作为 *.jpg*文件) 的服务器上。 然后可以使用图像文件的任何图像的方式。 优点是该文件是存储而不是保存到临时缓存。 可以将新的图表图像保存在不同时间 （例如每隔一小时），然后保留永久性记录随着时间的推移发生的更改。 请注意，您必须确保 web 应用程序具有你想要将图像文件放在服务器上将文件保存到文件夹的权限。

1. 在你的网站的根目录，创建名为的文件夹 *\_ChartFiles*如果尚不存在。
2. 在你的网站的根目录，创建名为的新文件*ChartSave.cshtml*。
3. 使用以下内容替换现有内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    代码首先检查以查看是否 *.jpg*文件存在通过调用`File.Exists`方法。 如果该文件不存在，代码会创建一个新`Chart`数组中。 这一次，该代码调用`Save`方法，并传递`path`参数来指定文件路径和保存图表的文件名。 在页的正文`<img>`元素使用的路径以指向 *.jpg*文件以显示。
4. 运行*ChartSave.cshtml*文件。
5. 返回到 WebMatrix。 请注意，名为图像文件*chart01.jpg*已保存在 *\_ChartFiles*文件夹。

### <a name="saving-a-chart-as-an-xml-file"></a>将图表另存为 XML 文件

最后，可以将图表保存为服务器上的 XML 文件。 通过缓存图表或将图表保存到文件中使用此方法的一个优点是可以如果想要显示图表之前修改的 XML。 你的应用程序必须具有你想要将图像文件放在服务器上文件夹的读/写权限。

1. 在你的网站的根目录，创建名为的新文件*ChartSaveXml.cshtml*。
2. 使用以下内容替换现有内容：

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    此代码是类似于你此前看到的用于存储在缓存中，一个图表，但它使用 XML 文件的代码。 代码首先检查以查看 XML 文件是否存在通过调用`File.Exists`方法。 如果文件确实存在，代码会创建一个新`Chart`对象，并将文件名作为传递`themePath`参数。 这将创建基于无论是在 XML 文件中的图表。 如果 XML 文件尚不存在，代码创建示例一样正常的图表，然后调用`SaveXml`将其保存。 使用呈现图表`Write`方法中，为你前面所见。

    与显示缓存的页面，此代码在图表标题中包含时间戳。
3. 创建一个名为的新页*ChartDisplayXMLChart.cshtml*并向其添加以下标记： 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. 运行*ChartDisplayXMLChart.cshtml*页。 显示图表。 记下在图表的标题中时间戳。
5. 关闭浏览器。
6. 在 WebMatrix 中，右键单击 *\_ChartFiles*文件夹中，单击**刷新**，然后打开该文件夹。 *XMLChart.xml*此文件夹中的文件由创建`Chart`帮助器。 

    ![说明： _ChartFiles 文件夹显示 XMLChart.xml 文件创建的图表帮助器。](7-displaying-data-in-a-chart/_static/image14.jpg)
7. 运行*ChartDisplayXMLChart.cshtml*页。 该图表显示相同的时间戳作为第一次运行页面。 这是因为正在从以前保存的 XML 生成图表。
8. 在 WebMatrix 中，打开 *\_ChartFiles*文件夹并删除*XMLChart.xml*文件。
9. 运行*ChartDisplayXMLChart.cshtml*页上一次。 这一次，更新时间戳，因为`Chart`帮助程序不得不重新创建 XML 文件。 如果你想，检查 *\_ChartFiles*文件夹，然后请注意，XML 文件又回来了。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [介绍使用数据库中 ASP.NET Web Pages 站点](https://go.microsoft.com/fwlink/?LinkId=202893)
- [使用缓存在 ASP.NET Web Pages 站点中以提高性能](https://go.microsoft.com/fwlink/?LinkId=202903)
- [图表类](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99))（MSDN 上的 ASP.NET Web Pages API 参考）
