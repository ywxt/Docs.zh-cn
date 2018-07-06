---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第 4 部分： 模型和数据访问 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 4 部分介绍了模型和数据访问。
ms.author: aspnetcontent
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 023350e882afe049ce3800921825b1b2bec8e415
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818948"
---
<a name="part-4-models-and-data-access"></a>第 4 部分： 模型和数据访问
====================
通过[Jon Galloway](https://github.com/jongalloway)

> MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。  
>   
> MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。
> 
> 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 4 部分介绍了模型和数据访问。


到目前为止，我们已只已传递"虚拟数据"从我们控制器到我们的视图模板。 现在我们已准备好挂接的实际数据库。 在本教程中我们将讨论如何使用 SQL Server Compact Edition （通常称为 SQL CE） 作为我们的数据库引擎。 SQL CE 是基于的免费、 嵌入式、 文件的数据库，不需要任何安装或配置，使其真正方便本地开发。

## <a name="database-access-with-entity-framework-code-first"></a>数据库访问使用 Entity Framework 代码优先

我们将使用 ASP.NET MVC 3 项目来查询和更新数据库中包含的 Entity Framework (EF) 支持。 EF 是一个灵活的对象关系映射 (ORM) 数据的 API，使开发人员能够以一种面向对象的方式存储在数据库中的查询和更新数据。

实体框架版本 4 支持称为代码优先开发模式。 代码的第一个，可通过编写简单的类 (也称为 POCO 从"纯旧式"CLR 对象)，创建模型对象，甚至可以从您的类动态创建数据库。

### <a name="changes-to-our-model-classes"></a>对我们模型类的更改

在本教程中，我们将使用实体框架中的数据库创建功能。 我们执行该操作之前，不过，让我们进行一些小的更改到我们模型类中我们将更高版本使用的一些事项添加。

#### <a name="adding-the-artist-model-classes"></a>添加艺术家模型类

因此，我们将添加一个简单的模型类来描述艺术家，我们唱片集将与艺术家，相关联。 将新类添加到模型文件夹名为 Artist.cs 使用如下所示的代码。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>更新了模型类

更新唱片集类，如下所示。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

接下来，对流派类进行以下更新。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-appdata-folder"></a>将应用添加\_数据文件夹

我们将添加应用\_到我们的项目来存放我们的 SQL Server Express 数据库文件的数据目录。 应用\_数据是在 ASP.NET 中已有数据库访问权限的正确的安全访问权限的特殊目录。 从项目菜单中，选择添加 ASP.NET 文件夹，然后应用\_数据。

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>在 web.config 文件中创建的连接字符串

我们将对网站的配置文件添加几行，以便实体框架知道如何连接到我们的数据库。 双击 Web.config 文件位于项目根目录中。

![](mvc-music-store-part-4/_static/image2.png)

滚动到此文件的底部，添加&lt;connectionStrings&gt;部分的正上方的最后一行，如下所示。

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>添加上下文类

右键单击模型文件夹并添加一个名为 MusicStoreEntities.cs 的新类。

![](mvc-music-store-part-4/_static/image3.png)

此类将表示实体框架数据库上下文，并将处理我们创建、 读取、 更新和删除用于我们的操作。 此类的代码如下所示。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

就这么简单-没有任何其他配置、 特殊的接口，等等。通过扩展 DbContext 基类，我们 MusicStoreEntities 类是能够处理我们为我们的数据库操作。 现在，我们已得到挂接了，让我们将多个属性添加到我们的模型类以利用我们的数据库中的一些其他信息。

### <a name="adding-our-store-catalog-data"></a>添加存储目录数据

将"种子"数据添加到新创建的数据库实体框架中，我们将充分利用一项功能。 这将预填充了存储目录，流派、 艺术家和唱片集的列表。 MvcMusicStore Assets.zip 下载-包含我们之前在本教程中使用的站点设计文件-具有此种子数据，位于名为代码的文件夹中的类文件。

在代码内 / Models 文件夹中，找到 SampleData.cs 文件并将其放到我们的项目中的 Models 文件夹中，如下所示。

![](mvc-music-store-part-4/_static/image4.png)

现在，我们需要添加一行代码需要了解的有关该 SampleData 类实体框架。 双击要打开它，并添加以下行到顶部应用程序的项目的根目录中的 Global.asax 文件\_Start 方法。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

此时，我们已完成为我们的项目配置实体框架所必需的工作。

## <a name="querying-the-database"></a>查询数据库

现在让我们更新我们 StoreController 以便而不是使用"虚拟数据"改为调用到我们的数据库来查询其所有的信息。 我们将开始通过声明一个字段上**StoreController**来托管实例的名为 storeDB MusicStoreEntities 类：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>正在更新存储索引查询数据库

MusicStoreEntities 类由实体框架维护并公开数据库中每个表的集合属性。 让我们更新我们 StoreController 索引操作来检索所有流派在我们的数据库。 以前我们是通过硬编码字符串数据。 现在我们可以只需使用实体框架上下文 Generes 集合：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

不需要由于仍将返回同一 StoreIndexViewModel 之前-只需将返回实时数据从我们的数据库现在我们返回到我们的视图模板会发生任何更改。

如果我们再次运行该项目并访问 URL"/ 存储"，我们现在看到所有影片类型列表在我们的数据库：

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>更新浏览应用商店和详细信息，以使用实时数据

与应用商店/浏览？ genre =*[某些流派]* 操作方法中，我们要搜索的一种流派的名称。 我们仅预期结果，因为我们不应拥有相同的类型名称的两个项目，因此我们可以使用。在 LINQ 中查询此类的适当流派对象的 single （） 扩展 （不要键入这尚未）：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

一个方法采用 Lambda 表达式作为参数，它指定我们想单个流派对象，以便其名称不匹配，我们已定义的值。 在上面的示例中，我们在加载单个流派对象与匹配的 Disco 名称值。

我们将利用一 Entity Framework 功能，使我们能够指示检索流派对象时，我们希望还加载其他相关的实体。 此功能称为查询结果调整，并且使我们能够减少我们需要访问数据库以检索所有需要的信息的次数。 我们想要预提取相册的流派我们检索，因此我们将更新我们的查询以包含从 Genres.Include("Albums") 以指示我们要以及相关的唱片集。 这是更高效，因为它会检索中的单个数据库请求我们的流派和唱片集数据。

使用开的说明，下面是我们已更新的浏览控制器操作的外观：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

我们现在可以更新应用商店浏览视图以显示每个类型中可用的唱片集。 打开视图模板 (在中找到 /Views/Store/Browse.cshtml) 并添加唱片集的项目符号列表，如下所示。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

运行我们的应用程序并浏览到/Store/浏览？ genre = Jazz 显示我们的结果现在正在从数据库中，在我们所选流派中显示的所有相册拉取。

![](mvc-music-store-part-4/_static/image2.jpg)

我们将使相同的地址更改为我们 /Store/详细信息 / [id] URL，和我们虚构数据替换为数据库查询，这将加载其 ID 与参数值匹配的相册。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

运行我们的应用程序并浏览至 /Store/Details/1 显示了我们的结果从数据库正在请求。

![](mvc-music-store-part-4/_static/image5.png)

现在，我们存储详细信息的页设置要显示的唱片集 ID 的唱片集，让我们更新**浏览**视图，以链接到详细信息视图。 我们将使用 Html.ActionLink，我们要从存储区索引链接到应用商店浏览在上一节末尾的样子。 浏览视图的完整源如下所示。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

我们现在能够从我们的应用商店页浏览到流派页上，其中列出了可用的唱片集，并通过单击唱片集，我们可以查看该唱片集的详细信息。

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-3.md)
> [下一页](mvc-music-store-part-5.md)
