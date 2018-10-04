---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: 将新字段添加到电影模型和数据库表 (VB) |Microsoft Docs
author: Rick-Anderson
description: 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是一个 ASP.NET MVC Web 应用程序的基础知识...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 8fb0fb5c1db24f1961bba08f7b1c2182caca39ca
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577426"
---
<a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a>将新字段添加到电影模型和数据库表 (VB)
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

> 本教程将讲述构建使用 Microsoft Visual Web Developer 2010 Express Service Pack 1，这是免费版本的 Microsoft Visual Studio 的 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装以下列出的先决条件。 可以通过单击以下链接安装所有这些： [Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，可以单独安装系统必备组件，使用以下链接：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时和工具支持）
> 
> 如果您使用 Visual Studio 2010 而不 Visual Web Developer 2010，通过单击以下链接安装必备组件： [Visual Studio 2010 必备软件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 可随附于此项目具有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果您愿意 C#，切换到[C# 版本](../cs/adding-a-new-field.md)本教程。


在本部分将对模型类进行一些更改，并了解如何更新数据库架构以匹配的模型更改。

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

首先，通过添加一个新`Rating`属性设置为现有`Movie`类。 打开*Movie.cs*文件，并添加`Rating`如下属性：

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

完整`Movie`类现在看起来如以下代码：

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

重新编译应用程序中使用**调试** &gt;**构建电影**菜单命令。

现在，已更新`Model`类，您还需要更新*\Views\Movies\Index.vbhtml*并 *\Views\Movies\Create.vbhtml* 查看模板以支持新`Rating`属性。

打开<em>\Views\Movies\Index.vbhtml</em>文件，并添加`<th>Rating</th>`列标题之后<strong>价格</strong>列。 然后添加`<td>`快要结束的模板来呈现列`@item.Rating`值。 下面是哪些更新<em>Index.vbhtml</em>视图模板如下所示：

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

接下来，打开 *\Views\Movies\Create.vbhtml* 文件，并添加以下标记窗体的结尾附近。 这会使文本框中，以便创建新电影时，可以指定一个级别。

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>管理模型和数据库架构差异

现已更新以支持新的应用程序代码`Rating`属性。

现在，运行该应用程序并导航到 */Movies* URL。 执行此操作，不过，将看到以下错误：

![](adding-a-new-field/_static/image1.png)

之所以看到此错误，因为已更新`Movie`应用程序中的 model 类现在与不同的架构`Movie`现有数据库表。 （数据库表中没有 `Rating` 列。）

默认情况下，当您使用 Entity Framework Code First 自动创建数据库，就像前面在本教程中，代码优先将表添加到数据库来帮助跟踪数据库的架构是否与从其中生成它的模型类同步。 如果它们不同步，实体框架将引发错误。 这使得更轻松地在开发时，你可能会否则仅发现 （通过奇怪的错误） 在运行时跟踪问题。 同步检查功能是哪些因素会导致要显示的错误消息，你刚才看到的。

有两种方法解决此错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 这种方法是非常方便时执行活动开发上测试数据库，因为它允许您一起快速改进模型和数据库架构。 缺点，不过，是会丢失数据库中的现有数据，因此您 *不* 需要生产数据库上使用此方法 ！
2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。

对于本教程中，我们将使用第一种方法，您必须 Entity Framework Code First 每当模型发生更改自动重新创建该数据库。

## <a name="automatically-re-creating-the-database-on-model-changes"></a>自动重新创建模型的更改上的数据库

让我们更新该应用程序，以便 Code First 自动删除并重新创建数据库，只要您更改应用程序的模型。

> [!NOTE] 
> 
> **警告**应该启用的自动删除并重新创建数据库，仅当你正在使用开发或测试数据库，这种方法和 *永远不会* 包含实际数据的生产数据库上。 使用生产服务器上可能会导致数据丢失。


在中**解决方案资源管理器**，右键单击 *模型* 文件夹，选择**添加**，然后选择**类**。

![](adding-a-new-field/_static/image2.png)

将类命名&quot;MovieInitializer&quot;。 更新`MovieInitializer`类，以包含以下代码：

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

`MovieInitializer`类指定应删除并自动重新创建如果发生变化的模型类使用该模型的数据库。 该代码包括`Seed`方法，以便指定一些默认数据会自动向数据库添加任何时间它具有创建 （或重新创建）。 这提供了有用的方式来使用填充数据库一些示例数据，而无需手动填充它每次进行更改的模型。

现在，已定义`MovieInitializer`类，您需要其绑定，以便每次应用程序运行时，它检查是否不同于数据库中架构的模型类。 如果是，您可以运行初始值设定项来重新创建数据库以匹配该模型，然后使用示例数据在数据库中填充。

打开 *Global.asax* 文件的根目录处`MvcMovies`项目：

*Global.asax* 文件包含的类定义整个应用程序项目，并包含`Application_Start`运行该应用程序首次启动时的事件处理程序。

查找`Application_Start`方法，并添加到调用`Database.SetInitializer`开头的方法，如下所示：

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

`Database.SetInitializer`刚添加的语句指示的数据库由`MovieDBContext`应自动删除并重新创建如果不匹配的架构和数据库实例。 如您所看到的它还会填充使用示例数据中指定的数据库和`MovieInitializer`类。

关闭 *Global.asax* 文件。

重新运行该应用程序并导航到 */Movies* URL。 应用程序启动时，它会检测模型结构不能再与数据库架构相匹配。 自动重新创建数据库，以匹配新的模型结构，并填充该数据库示例电影：

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

单击**创建新**链接以添加新电影。 请注意，您可以添加一个级别。

[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)

单击 **“创建”**。 新电影，包括分级，现在显示在列表的电影：

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

在本部分中您将看到如何修改模型对象并使数据库所做的更改同步。 你还了解了一种方法来填充新创建的数据库使用示例数据，这样您可以试用方案。 接下来，让我们看看如何将更丰富的验证逻辑添加到模型类并启用某些业务规则以强制实施。

> [!div class="step-by-step"]
> [上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)
