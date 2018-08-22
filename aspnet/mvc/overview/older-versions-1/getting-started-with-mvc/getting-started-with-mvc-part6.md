---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 添加创建方法，并创建视图 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 546c3e0a24ecd0d916c79e9ad12f62b926c760c5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834956"
---
<a name="adding-a-create-method-and-create-view"></a>添加创建方法，并创建视图
====================
通过[Scott Hanselman](https://github.com/shanselman)

> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


在本部分中我们要实现使用户能够在我们的数据库中创建新电影所需的支持。 我们将通过实现电影/创建 URL 操作来执行此操作。

实现电影/创建 URL 是一个两步过程。 当用户首次访问电影/创建 URL 我们需要向他们展示他们可以填写输入新电影的 HTML 窗体。 然后，当用户提交窗体和数据返回到服务器的文章，我们想要检索已发布的内容并将其保存到我们的数据库。

我们为 MoviesController 类中，我们将实现两个 create （） 方法中的这两个步骤。 一种方法将显示&lt;窗体&gt;用户应填写创建新的电影。 第二种方法将处理处理已发布的数据，当用户提交&lt;窗体&gt;回服务器，并保存新电影中我们的数据库。

下面是代码我们将添加到我们为 MoviesController 类，以实现这一点：

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

上面的代码中包含的所有控制器中，我们需要代码。

现在让我们来实现，我们将使用向用户显示窗体创建视图模板。 我们将第一个 Create 方法中右键单击并选择"添加视图"，以创建电影窗体的视图模板。

我们将选择，我们要为其视图数据类，通过查看模板"电影"，并指出我们希望"搭建基架的"的"创建"模板。

[![添加视图](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

单击添加按钮后，将为您创建 \Movies\Create.aspx 视图模板。 由于我们从"视图内容"下拉列表中选择"创建"，添加视图对话框中自动"基架"一些默认内容为我们。 基架创建对应的 HTML&lt;窗体&gt;、 使验证错误消息，随时随地和基架了解的有关电影，因为它创建标签和字段我们的类的每个属性。

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

由于我们的数据库自动提供电影的 ID，让我们这些字段删除该引用模型。从我们创建视图的 id。 删除后的 7 几&lt;图例&gt;字段&lt;/legend&gt;如他们所示的 ID 字段，我们不希望。

现在让我们来创建新电影并将其添加到数据库。 我们将运行一次应用程序执行此操作，请访问"/ 电影"URL，然后单击"创建"链接以添加新电影。

[![创建的 Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

当我们单击创建按钮时，我们将进行回 （通过 HTTP POST) 的数据发布到我们刚刚创建的 /Movies/Create 方法此窗体上。 就像在系统自动执行在 url 的"numTimes"和"name"参数，并映射到在前面的方法的参数，系统将自动从帖子采取窗体字段，并将它们映射到一个对象。 在这种情况下，从"ReleaseDate"和"Title"等的 HTML 中的字段的值都将自动放入电影的新实例的正确属性。

让我们看一下第二个 Create 方法从我们为 MoviesController 试。 请注意如何需要"电影"对象作为参数：

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

然后此电影对象传递给我们创建的操作方法，[HttpPost] 版本和我们在数据库中保存和重定向回到 index （） 操作方法，它将在已保存的结果显示电影列表中的用户：

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

我们不会检查是否我们的电影是正确的不过，并且数据库不会使我们能够将电影保存与没有标题。 如果我们可以告诉用户的数据库之前引发了错误，它很好。 我们通过将验证支持添加到我们的应用程序执行此下一步。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part5.md)
> [下一页](getting-started-with-mvc-part7.md)
