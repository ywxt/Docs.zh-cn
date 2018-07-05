---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: 从控制器 (VB) 访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 0c0cdb7214b99908e4d64583e880fb03f69252c2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369297"
---
<a name="accessing-your-models-data-from-a-controller-vb"></a>从控制器 (VB) 访问模型的数据
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您愿意 C#，切换到[C# 版本](../cs/accessing-your-models-data-from-a-controller.md)本教程。


在本部分中，将创建一个新`MoviesController`类，并编写代码来检索电影数据并将其显示在浏览器中使用视图模板。 请确保生成继续操作之前应用程序。

右键单击*控制器*文件夹，并创建一个新`MoviesController`控制器。 选择以下选项：

- 控制器名称： **MoviesController**。 （这是默认值）。
- 模板：**控制器包含读/写操作和视图，使用 Entity Framework**。
- 模型类： **Movie (MvcMovie.Models)**。
- 数据上下文类： **MovieDBContext (MvcMovie.Models)**。
- 视图： **Razor (CSHTML)**。 （默认值。）

[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)

单击 **添加**。 Visual Web Developer 中创建以下文件和文件夹：

- *MoviesController.vb*在项目文件中的*控制器*文件夹。
- 一个*电影*文件夹中项目的*视图*文件夹。
- *Create.vbhtml，Delete.vbhtml，Details.vbhtml，Edit.vbhtml*，并*Index.vbhtml*中的新*视图 \ 电影*文件夹。

[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 基架机制自动创建 CRUD （创建、 读取、 更新和删除） 操作方法和为您的视图。 现可完全正常运行的 web 应用程序，可用于创建、 列出、 编辑和删除的电影条目。

运行应用程序，并浏览到`Movies`控制器通过追加 */Movies*到你的浏览器的地址栏中的 URL。 因为应用程序依赖于默认路由 (在中定义*Global.asax*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认`Index`操作方法的`Movies`控制器。 换而言之，将浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。 结果是空列表的电影，因为还未添加任何。

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a>创建电影

选择“新建”链接。 输入有关电影的一些详细信息，然后单击**创建**按钮。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

单击**创建**按钮后，窗体会发布到服务器，其中电影信息保存到数据库中。 然后，将重定向到 */Movies* URL，其中显示在列表中新创建的电影。

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)

再创建几个其他的电影条目。 试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。

## <a name="examining-the-generated-code"></a>检查生成的代码

打开*Controllers\MoviesController.vb*文件并检查生成`Index`方法。 与电影控制器的一部分`Index`方法如下所示。

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

以下代码行从`MoviesController`类实例化一个电影数据库上下文，如前面所述。 电影数据库上下文可用于查询、 编辑和删除电影。

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

对请求`Movies`控制器返回中的所有条目`Movies`电影数据库表，然后将传递到结果`Index`视图。

## <a name="strongly-typed-models-and-the-model-keyword"></a>强类型模型和@model关键字

前面在本教程中，您已了解如何在控制器可以传入数据或对象视图模板使用`ViewBag`对象。 `ViewBag`是一个动态对象，提供了方便的后期绑定方法将信息传递给视图。

ASP.NET MVC 还提供了能够传递强类型化数据或视图模板的对象。 此强类型化方法允许更好地进行编译时检查的代码和更丰富的 IntelliSense，Visual Web Developer 编辑器中。 我们将使用此方法与`MoviesController`类和*Index.vbhtml*视图模板。

请注意，该代码会创建如何[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它将调用`View`帮助器方法`Index`操作方法。 该代码，然后将此`Movies`从控制器到视图的列表：

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

通过包括`@ModelType`语句在视图模板文件的顶部，可以指定视图期望的对象的类型。 创建电影控制器时，Visual Web Developer 中自动包括以下`@model`顶部的语句*Index.vbhtml*文件：

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

这`@ModelType`指令使你能够访问控制器传递给视图使用的电影列表`Model`强类型化的对象。 例如，在*Index.vbhtml*模板，该代码循环访问电影通过这样做`foreach`语句通过强类型化`Model`对象：

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，每个`item`循环中的对象被类型化为`Movie`。 还具有其他优点，这意味着，获取编译时检查的代码，并完全在代码编辑器中的 IntelliSense 支持：

[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>通过 SQL Server Compact 的工作

提供数据库连接字符串指向实体框架 Code First 检测到`Movies`未尚未存在，因此 Code First 数据库自动创建的数据库。 你可以验证它已创建中查找*应用程序\_数据*文件夹。 如果没有看到*Movies.sdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏中，单击**刷新**按钮，，然后展开*应用程序\_数据*文件夹。

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)

双击*Movies.sdf*以打开**服务器资源管理器**。 然后展开**表**文件夹以查看已在数据库中创建的表。

> [!NOTE]
> 如果双击时将发生错误*Movies.sdf*，请确保已安装**Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**。 （有关该软件的链接，请参阅本系列教程的第 1 部分中的先决条件列表）。如果现在安装版本，您必须关闭并重新打开 Visual Web Developer。


[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)

有两个表，一个用于`Movie`实体集，然后`EdmMetadata`表。 `EdmMetadata`实体框架使用表来确定当模型和数据库位于同步。

右键单击`Movies`表，然后选择**显示表数据**若要查看你创建的数据。

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)

右键单击`Movies`表，然后选择**编辑表架构**。

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

请注意如何的架构`Movies`表映射到`Movie`前面创建的类。 实体框架 Code First 自动创建此架构根据你`Movie`类。

完成后，关闭连接。 （如果不关闭连接，您可能会遇到错误在下次运行项目时）。

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)

现在将具有对数据库和简单列表页，以显示从它的内容。 在下一步的教程中，我们将检查已搭建基架代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`使您可以搜索电影的此数据库的视图。

> [!div class="step-by-step"]
> [上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)
