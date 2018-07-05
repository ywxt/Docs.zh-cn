---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 从控制器访问模型的数据 |Microsoft Docs
author: shanselman
description: 这是介绍 ASP.NET MVC 的基础知识初学者教程。 创建一个简单的 web 应用程序读取和写入数据库中。
ms.author: aspnetcontent
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 556eed77cbd9e81c0a2a1334bb0a8ee56abafd34
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814995"
---
<a name="accessing-your-models-data-from-a-controller"></a>从控制器访问模型的数据
====================
通过[Scott Hanselman](https://github.com/shanselman)

> 这是介绍 ASP.NET MVC 的基础知识初学者教程。 将创建一个简单的 web 应用程序读取和写入数据库中。 请访问[ASP.NET MVC 学习中心](../../../index.md)来查找其他 ASP.NET MVC 教程和示例。


在本部分中我们将创建新的 MoviesController 类，并编写一些代码来检索电影数据，并显示返回到浏览器中使用视图模板。

右键单击 Controllers 文件夹，并使新 MoviesController。

[![添加控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

这将创建我们的项目中我们 \Controllers 文件夹下的新"MoviesController.cs"文件。 让我们更新 MovieController 从我们的新填充数据库中检索的影片列表。

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

我们正在执行 LINQ 查询，以便我们仅检索在 1984 年夏天之后发布的电影。 我们将需要视图模板能够呈现电影返回此列表，因此在方法中右键单击并选择添加视图来创建它。

在添加视图对话框将指示我们传递的列表&lt;Movies.Models.Movie&gt;向视图模板。 与上一次我们使用添加视图对话框中，选择创建一个"空"模板，我们将指示这次我们希望 Visual Studio 自动"搭建基架"视图模板为我们使用一些默认内容。 我们将执行此操作选择的"列表"项中的"视图内容的下拉列表菜单。

请记住，您可以创建一个新类，你将需要编译为其显示在添加的视图对话框的应用程序。

![添加视图](getting-started-with-mvc-part5/_static/image3.png)

单击添加，系统将自动生成的代码用于视图为我们显示我们的电影列表。 这是更改的好时机&lt;h2&gt;标题为"My Movie List"类似，我们之前使用 Hello World 视图。

[![电影-Microsoft Visual Web Developer 2010 速成版](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

运行应用程序并在地址栏中访问 /Movies。 现在我们使用基本控制器中的查询从数据库检索数据并将数据返回到了解的有关电影的视图。 该视图然后旋转的电影列表，并会为我们创建包含数据的表。

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

因此我们无需为我们创建了基架模板的默认链接，我们不会将实现与此应用程序的编辑、 详细信息和删除功能。 打开 /Movies/Index.aspx 文件并将其删除。

下面是什么我们已更新的视图模板应如下所示我们做这些更改后的源代码：

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

它创建我们不需要的链接，因此对于此示例将删除它们。 但是，因为这是下一步，我们将保留我们新创建的链接 ！ 下面是我们的应用程序中删除的列的外观。

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

我们现在有了我们的电影数据的简单列表。 但是，如果我们单击"新建"链接时，我们将会出错，因为它不挂起 ！ 让我们实现创建操作方法，并使用户能够在我们的数据库输入新影片。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part4.md)
> [下一页](getting-started-with-mvc-part6.md)
