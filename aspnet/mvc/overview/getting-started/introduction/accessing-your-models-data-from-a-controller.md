---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: 从控制器访问模型的数据 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: a3f3f4a030650ff65b070528c5efa1605be764a0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37817546"
---
<a name="accessing-your-models-data-from-a-controller"></a>从控制器访问模型的数据
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

在本部分中，将创建一个新`MoviesController`类，并编写代码来检索电影数据并将其显示在浏览器中使用视图模板。

**生成应用程序**然后才能转到下一步。 如果不生成应用程序，您会添加一个控制器发生错误。

在解决方案资源管理器中右键单击*控制器*文件夹，然后单击**添加**，然后**控制器**。

![](accessing-your-models-data-from-a-controller/_static/image1.png)

在中**添加基架**对话框中，单击**包含的 MVC 5 控制器视图，使用实体框架**，然后单击**添加**。

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- 选择**Movie (MvcMovie.Models)** 模型类。
- 选择**MovieDBContext (MvcMovie.Models)** 为数据上下文类。
- 对于控制器名称输入**MoviesController**。

  下图显示了已完成的对话框。  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

单击 **添加**。 （如果遇到错误，您可能不生成应用程序开始将控制器添加之前。）Visual Studio 将创建以下文件和文件夹：

- *MoviesController.cs*文件中*控制器*文件夹。
- 一个*视图 \ 电影*文件夹。
- *Create.cshtml、 Delete.cshtml、 Details.cshtml、 Edit.cshtml*，并*Index.cshtml*中的新*视图 \ 电影*文件夹。

自动创建 visual Studio [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) （创建、 读取、 更新和删除） 操作方法和视图为您 （CRUD 操作方法和视图的自动创建被称为基架）。 现可完全正常运行的 web 应用程序，可用于创建、 列出、 编辑和删除的电影条目。

运行应用程序并单击**MVC 电影**链接 (或浏览至`Movies`控制器通过追加 */Movies*到你的浏览器的地址栏中的 URL)。 因为应用程序依赖于默认路由 (中定义*应用程序\_Start\RouteConfig.cs*文件)，浏览器请求`http://localhost:xxxxx/Movies`路由到默认`Index`的操作方法`Movies`控制器。 换而言之，将浏览器请求`http://localhost:xxxxx/Movies`实际上是浏览器请求相同`http://localhost:xxxxx/Movies/Index`。 结果是空列表的电影，因为还未添加任何。

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>创建电影

选择“新建”链接。 输入有关电影的一些详细信息，然后单击**创建**按钮。


![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> 您不能在价格字段中输入小数点或逗号。 若要支持 jQuery 验证的非英语区域设置，请使用逗号 (&quot;，&quot;) 必须包含小数点，和非美国英语日期格式， *globalize.js*和您的特定*cultures/globalize.cultures.js*文件 (从[ https://github.com/jquery/globalize ](https://github.com/jquery/globalize) ) 和 JavaScript 使用`Globalize.parseFloat`。 我将介绍如何执行此操作在下一步的教程。 目前只能输入整数，例如 10。


单击**创建**按钮后，窗体会发布到服务器，其中电影信息保存到数据库中。 然后，将重定向到 */Movies* URL，其中显示在列表中新创建的电影。

![](accessing-your-models-data-from-a-controller/_static/image6.png)

再创建几个其他的电影条目。 试用“编辑”、“详细信息”和“删除”链接，它们均可正常工作。

## <a name="examining-the-generated-code"></a>检查生成的代码

打开*Controllers\MoviesController.cs*文件并检查生成`Index`方法。 与电影控制器的一部分`Index`方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

对请求`Movies`控制器返回中的所有条目`Movies`表，然后将传递到结果`Index`视图。 以下代码行从`MoviesController`类实例化一个电影数据库上下文，如前面所述。 电影数据库上下文可用于查询、 编辑和删除电影。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>强类型模型和@model关键字

前面在本教程中，您已了解如何在控制器可以传入数据或对象视图模板使用`ViewBag`对象。 `ViewBag`是一个动态对象，提供了方便的后期绑定方法将信息传递给视图。

MVC 还提供了将传递的功能*强*类型化视图模板的对象。 使用此强类型化的方法，更好地编译时检查的代码和更丰富[IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) Visual Studio 编辑器中。 在 Visual Studio 中的基架机制使用这种方法 (即传递*强*类型化的模型) 与`MoviesController`类和视图模板时将其创建方法和视图。

在中*Controllers\MoviesController.cs*文件检查生成`Details`方法。 `Details`方法如下所示。

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id`参数通常作为路由数据传递，例如`http://localhost:1234/movies/details/1`将设置为电影控制器，对指定的操作的控制器`details`和`id`为 1。 您还可以传入查询字符串的 id，如下所示：

`http://localhost:1234/movies/details?id=1`

如果`Movie`找到的实例`Movie`的模型传递给`Details`视图：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

检查的内容*Views\Movies\Details.cshtml*文件：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

通过包括`@model`语句在视图模板文件的顶部，可以指定视图期望的对象的类型。 创建电影控制器时，Visual Studio 会自动在 Details.cshtml 文件的顶端包括以下 `@model` 语句：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

此 `@model` 指令使你能够使用强类型的 `Model` 对象访问控制器传递给视图的电影。 例如，在*Details.cshtml*模板，代码将传递到每个电影字段`DisplayNameFor`并[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 帮助器与强类型化`Model`对象。 `Create`和`Edit`方法和视图模板还将传递电影模型对象。

检查*Index.cshtml*视图模板和`Index`中的方法*MoviesController.cs*文件。 请注意，该代码会创建如何[ `List` ](https://msdn.microsoft.com/library/6sh2ey19.aspx)对象时它将调用`View`帮助器方法`Index`操作方法。 该代码，然后将这`Movies`列表从`Index`到视图的操作方法：

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

创建电影控制器时，Visual Studio 自动包括以下`@model`顶部的语句*Index.cshtml*文件：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

这`@model`指令使你能够访问控制器传递给视图使用的电影列表`Model`强类型化的对象。 例如，在*Index.cshtml*模板，该代码循环访问电影通过这样做`foreach`语句通过强类型化`Model`对象：

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

因为`Model`对象被强类型 (作为`IEnumerable<Movie>`对象)，每个`item`循环中的对象被类型化为`Movie`。 还具有其他优点，这意味着，获取编译时检查的代码，并完全在代码编辑器中的 IntelliSense 支持：

![ModelIntellisene](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>使用 SQL Server LocalDB

提供数据库连接字符串指向实体框架 Code First 检测到`Movies`未尚未存在，因此 Code First 数据库自动创建的数据库。 你可以验证它已创建中查找*应用程序\_数据*文件夹。 如果没有看到*Movies.mdf*文件中，单击**显示所有文件**按钮**解决方案资源管理器**工具栏中，单击**刷新**按钮，，然后展开*应用程序\_数据*文件夹。

![](accessing-your-models-data-from-a-controller/_static/image9.png)

双击*Movies.mdf*以打开**服务器资源管理器**，然后展开**表**文件夹，以查看电影表。 请注意旁密钥的 id。 默认情况下，EF 将名为 ID 的主键的属性。 EF 和 MVC 的详细信息，请参阅 Tom Dykstra 的绝佳教程上[MVC 和 EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

右键单击`Movies`表，然后选择**显示表数据**若要查看你创建的数据。

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

右键单击`Movies`表，然后选择**打开表定义**若要查看结构，该实体框架 Code First 为你创建的表。

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

请注意如何的架构`Movies`表映射到`Movie`前面创建的类。 实体框架 Code First 自动创建此架构根据你`Movie`类。

完成后，通过右键单击关闭连接*MovieDBContext* ，然后选择**关闭连接**。 （如果不关闭连接，您可能会遇到错误在下次运行项目时）。

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

现在你已拥有用于显示、编辑、更新和删除数据的数据库和页面。 在下一步的教程中，我们将检查已搭建基架代码的其余部分并添加`SearchIndex`方法和一个`SearchIndex`使您可以搜索电影的此数据库的视图。 与 MVC 结合使用实体框架的详细信息，请参阅[为 ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

> [!div class="step-by-step"]
> [上一页](creating-a-connection-string.md)
> [下一页](examining-the-edit-methods-and-edit-view.md)
