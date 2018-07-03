---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 将列添加到模型 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/14/2010
ms.topic: article
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 241f9108394561fecb15db5b6efa2661fdb128d6
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37361755"
---
<a name="adding-a-column-to-the-model"></a>向模型添加列
====================
通过[Scott Hanselman](https://github.com/shanselman)

> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


在本部分中我们将引导完成如何对我们的数据库的架构进行更改并处理我们的应用程序中所做的更改。

让我们将"评级"列添加到的 Movie 表。 返回到 IDE，并单击数据库资源管理器。 右键单击的 Movie 表并选择打开表定义。

添加"Rating"列，如下所示。 我们现在没有任何分级，因为此列可以允许 null 值。 单击保存。

[![编辑电影表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

接下来，返回到解决方案资源管理器并打开 Movies.edmx 文件 （这是 \Models 文件夹中）。 右键单击设计图面 （白色区域） 上，然后选择从数据库更新模型。

[![电影-Microsoft Visual Web Developer 2010 速成版 (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

这将启动"更新向导"。 单击刷新选项卡中的，单击完成。 然后将新列更新我们的 Movie 模型类。

![更新向导 (2)](getting-started-with-mvc-part8/_static/image5.png)

单击完成后, 可以看到新的评级列已添加到我们的模型中的电影实体。

[![电影实体](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

我们已在数据库模型中，添加一个列，但视图不知道它。

## <a name="update-views-with-model-changes"></a>使用模型更改更新视图

有几种方法我们无法更新我们的视图模板以反映新的 Rating 列。 由于我们通过生成它们通过添加视图对话框来创建这些视图，我们可以将其删除并再次重新创建它们。 但是，通常人们将已进行了修改到其视图模板从初始的基架生成并且将想要添加或删除字段，请手动，只需与使用 ID 字段用于创建。

打开 \Views\Movies\Index.aspx 模板和添加&lt;th&gt;评级&lt;/th&gt;到开头的 Movie 表。 我添加我的流派之后。 然后，在相同的列位置但较低位置添加一个行，以输出我们新的分级。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

我们最终 Index.aspx 模板将如下所示：

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

让我们再打开 \Views\Movies\Create.aspx 模板，并为我们的新分级属性添加标签和文本框：

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

我们最终 Create.aspx 模板将如下所示，并让我们更改浏览器的标题和辅助数据库&lt;h2&gt;标题为类似于"创建电影"虽然我们在这里 ！

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

运行您的应用程序，现在你已生成的数据库的已添加到创建页中的新字段。 添加新电影-这次使用一个级别的并单击创建。

[![创建电影的 Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

单击创建后，你将被转到索引页在你新电影列出与数据库中新的评级列

[![电影列表-Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

这一基本教程能满足你的启动使控制器，将它们与视图相关联并传递硬编码数据。 然后，创建和设计数据库并将一些数据中。 我们从数据库中检索数据并显示在 HTML 表。 然后，我们添加了允许用户将数据添加到数据库本身从 Web 应用程序中创建窗体。 我们添加验证，然后进行客户端上使用 JavaScript 的验证。 最后，我们更改了数据库，以包括新列的数据，然后更新我们的两个页，以创建并显示此新数据。

我现在鼓励您转到我们的中级教程"[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"以及许多的视频和资源，请访问[ https://asp.net/mvc ](https://asp.net/mvc)甚至更多地了解 ASP.NET MVC ！

请尽情体验吧！

- Scott Hanselman- [ http://hanselman.com ](http://hanselman.com)并[ @shanselman ](http://twitter.com/shanselman) Twitter 上。

> [!div class="step-by-step"]
> [上一篇](getting-started-with-mvc-part7.md)
