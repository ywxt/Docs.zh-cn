---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2b5747f49a31a6f3559609bbae765025e43c650b
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832488"
---
<a name="accessing-your-models-data-from-a-controller"></a>从控制器访问模型的数据
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


在本部分中，将创建一个新`MoviesController`类，并编写代码来检索电影数据并将其显示在浏览器中使用视图模板。

**生成应用程序**然后才能转到下一步。

右键单击*控制器*文件夹，并创建一个新`MoviesController`控制器。 生成应用程序之前，不会显示以下选项。 选择以下选项：

- 控制器名称： **MoviesController**。 （这是默认值。 )
- 模板：**使用实体框架包含读/写操作和视图的 MVC 控制器**。
- 模型类： **Movie (MvcMovie.Models)**。
- 数据上下文类： **MovieDBContext (MvcMovie.Models)**。
- 视图： **Razor (CSHTML)**。 （默认值。）

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

单击 **添加**。 Visual Studio 速成版创建以下文件和文件夹：

- *MoviesController.cs*在项目文件中的*控制器*文件夹。
- 一个*电影*文件夹中项目的*视图*文件夹。
- *Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml*，并*Index.cshtml*中的新*视图 \ 电影*文件夹。

ASP.NET MVC 4 自动创建 CRUD （创建、 读取、 更新和删除） 操作方法和视图为您 （CRUD 操作方法和视图的自动创建被称为基架）。 现可完全正常运行的 web 应用程序，可用于创建、 列出、 编辑和删除的电影条目。

运行应用程序，并浏览到`Movies`控制器通过追加 */Movies*到你的浏览器的地址栏中的 URL。 因为应用程序依赖于默认路由 (在中定义*Global.asax*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认`Index`操作方法的`Movies`控制器。 换而言之，将浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。 结果是空列表的电影，因为还未添加任何。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>创建电影

选择“新建”链接。 输入有关电影的一些详细信息，然后单击**创建**按钮。

![](accessing-your-models-data-from-a-controller/_static/image3.png)

单击**创建**按钮后，窗体会发布到服务器，其中电影信息保存到数据库中。 然后，将重定向到 */Movies* URL，其中显示在列表中新创建的电影。

![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")

再创建几个其他的电影条目。 试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。

## <a name="examining-the-generated-code"></a>检查生成的代码

打开*Controllers\MoviesController.cs*文件并检查生成`Index`方法。 与电影控制器的一部分`Index`方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

以下代码行从`MoviesController`类实例化一个电影数据库上下文，如前面所述。 电影数据库上下文可用于查询、 编辑和删除电影。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

对请求`Movies`控制器返回中的所有条目`Movies`电影数据库表，然后将传递到结果`Index`视图。

## <a name="strongly-typed-models-and-the-model-keyword"></a>强类型模型和@model关键字

前面在本教程中，您已了解如何在控制器可以传入数据或对象视图模板使用`ViewBag`对象。 `ViewBag`是一个动态对象，提供了方便的后期绑定方法将信息传递给视图。

ASP.NET MVC 还提供了能够传递强类型化数据或视图模板的对象。 此强类型化方法允许更好地进行编译时检查的代码和更丰富的 IntelliSense，Visual Studio 编辑器中。 在 Visual Studio 中的基架机制使用此方法`MoviesController`类和视图模板时将其创建方法和视图。

在中*Controllers\MoviesController.cs*文件检查生成`Details`方法。 与电影控制器的一部分`Details`方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

如果`Movie`找到，则实例`Movie`的模型传递到详细信息视图。 检查的内容*Views\Movies\Details.cshtml*文件。

通过包括`@model`语句在视图模板文件的顶部，可以指定视图期望的对象的类型。 创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。 例如，在*Details.cshtml*模板，代码将传递到每个电影字段`DisplayNameFor`并[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助器与强类型化`Model`对象。 创建和编辑方法和视图模板还传递电影模型对象。

检查*Index.cshtml*视图模板和`Index`中的方法*MoviesController.cs*文件。 请注意，该代码会创建如何[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它将调用`View`帮助器方法`Index`操作方法。 该代码，然后将此`Movies`从控制器到视图的列表：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

创建电影控制器时，Visual Studio Express 自动包括以下`@model`顶部的语句*Index.cshtml*文件：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

这`@model`指令使你能够访问控制器传递给视图使用的电影列表`Model`强类型化的对象。 例如，在*Index.cshtml*模板，该代码循环访问电影通过这样做`foreach`语句通过强类型化`Model`对象：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，每个`item`循环中的对象被类型化为`Movie`。 还具有其他优点，这意味着，获取编译时检查的代码，并完全在代码编辑器中的 IntelliSense 支持：

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

提供数据库连接字符串指向实体框架 Code First 检测到`Movies`未尚未存在，因此 Code First 数据库自动创建的数据库。 你可以验证它已创建中查找*应用程序\_数据*文件夹。 如果没有看到*Movies.mdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏中，单击**刷新**按钮，，然后展开*应用程序\_数据*文件夹。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

双击*Movies.mdf*以打开**数据库资源管理器**，然后展开**表**文件夹，以查看电影表。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> 如果未出现数据库资源管理器，从**工具**菜单中，选择**连接到数据库**，然后取消**选择数据源**对话框。 这将强制打开数据库资源管理器。


> [!NOTE]
> 如果您正在使用 VWD 或 Visual Studio 2010 并遇到错误类似于以下的以下任何：
> 
> - 数据库 C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES。MDF 无法打开，因为它是 706 的版本。 此服务器支持 655 及更早版本。 不支持降级路径。
> - &quot;用户代码未处理 InvalidOperation 异常&quot;提供的 SqlConnection 未指定初始目录。
> 
> 你需要安装[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)并[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)。 验证`MovieDBContext`前一页上指定的连接字符串。


右键单击`Movies`表，然后选择**显示表数据**若要查看你创建的数据。

![](accessing-your-models-data-from-a-controller/_static/image8.png)

右键单击`Movies`表，然后选择**打开表定义**若要查看结构，该实体框架 Code First 为你创建的表。

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

请注意如何的架构`Movies`表映射到`Movie`前面创建的类。 实体框架 Code First 自动创建此架构根据你`Movie`类。

完成后，通过右键单击关闭连接*MovieDBContext* ，然后选择**关闭连接**。 （如果不关闭连接，您可能会遇到错误在下次运行项目时）。

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

现在将具有对数据库和简单列表页，以显示从它的内容。 在下一步的教程中，我们将检查已搭建基架代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`使您可以搜索电影的此数据库的视图。

> [!div class="step-by-step"]
> [上一页](adding-a-model.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)
