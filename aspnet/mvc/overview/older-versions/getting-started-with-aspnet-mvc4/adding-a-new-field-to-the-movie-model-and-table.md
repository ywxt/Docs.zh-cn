---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 将新字段添加到电影模型和表 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/28/2012
ms.topic: article
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: 25a29e783f02e66e1713d8120eb526e1a02961a3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366471"
---
<a name="adding-a-new-field-to-the-movie-model-and-table"></a>将新字段添加到电影模型和表
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


在本部分中将使用 Entity Framework Code First 迁移来迁移到模型类的一些更改，因此更改被应用到数据库。

默认情况下，当您使用 Entity Framework Code First 自动创建数据库，就像前面在本教程中，代码优先将表添加到数据库来帮助跟踪数据库的架构是否与从其中生成它的模型类同步。 如果它们不同步，实体框架将引发错误。 这使得更轻松地在开发时，你可能会否则仅发现 （通过奇怪的错误） 在运行时跟踪问题。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>为模型更改设置 Code First 迁移

如果使用 Visual Studio 2012，双击*Movies.mdf*从解决方案资源管理器中打开数据库工具的文件。 Visual Studio Express for Web 将显示数据库资源管理器，Visual Studio 2012 将显示服务器资源管理器。 如果使用 Visual Studio 2010，使用 SQL Server 对象资源管理器。

在数据库工具 （数据库资源管理器、 服务器资源管理器或 SQL Server 对象资源管理器） 中，右键单击`MovieDBContext`，然后选择**删除**以删除电影数据库。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

导航回到解决方案资源管理器。 右键单击*Movies.mdf*文件，然后选择**删除**删除电影数据库。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

生成应用程序以确保没有任何错误。

从**工具**菜单上，单击**库程序包管理器**，然后**程序包管理器控制台**。

![添加包 Man](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

在中**程序包管理器控制台**处窗口`PM>`提示符处输入"Enable-migrations ContextTypeName MvcMovie.Models.MovieDBContext"。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

**Enable-migrations** （如上所示） 的命令将创建*Configuration.cs*文件中的新*迁移*文件夹。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio 将打开*Configuration.cs*文件。 替换`Seed`中的方法*Configuration.cs*文件使用以下代码：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

右键单击下的红色波浪线`Movie`，然后选择**解决**然后**使用** **MvcMovie.Models;**

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

执行此操作将添加以下 using 语句：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> 代码优先迁移调用`Seed`每个迁移后的方法 (即，调用**更新数据库**程序包管理器控制台)，，此方法更新行，具有已插入，或将其插入，如果它们尚不存在。


**按 CTRL-SHIFT-B 以生成项目。**(以下步骤将失败，如果你不在此时生成。)

下一步是创建`DbMigration`类适用于初始迁移。 为此迁移过程将创建一个新的数据库，这就是为什么你删除*movie.mdf*上一步中的文件。

在中**程序包管理器控制台**窗口中，输入命令"add-migration Initial"若要创建初始迁移。 "初始"的名称是任意参数并用于命名创建的迁移文件。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First 迁移创建另一个类文件中的*迁移*文件夹 (具有名称 *{日期戳}\_Initial.cs* )，并且此类包含创建数据库架构的代码。 预先使用时间戳修复迁移文件名以帮助进行排序。 检查 *{日期戳}\_Initial.cs*文件，它包含为电影数据库创建电影表的说明进行操作。 更新以下，这说明中的数据库时 *{日期戳}\_Initial.cs*文件将运行并创建数据库架构。 然后**种子**方法将运行以填充具有测试数据的数据库。

在中**程序包管理器控制台**，输入命令"更新数据库"以创建数据库并运行**种子**方法。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

如果收到一个错误，指示表已存在，无法创建，则可能是因为删除了该数据库后，您在执行前运行应用程序`update-database`。 在这种情况下，删除*Movies.mdf*再次文件，然后重试`update-database`命令。 如果仍遇到错误，删除的 migrations 文件夹和内容，然后开始在此页顶部的说明进行操作 (这是 delete *Movies.mdf*文件，然后转到 Enable-migrations)。

运行应用程序并导航到 */Movies* URL。 将显示种子数据。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

首先，通过添加一个新`Rating`属性设置为现有`Movie`类。 打开*Models\Movie.cs*文件，并添加`Rating`如下属性：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

完整`Movie`类现在看起来如以下代码：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

生成应用程序中使用**构建** &gt;**构建电影**菜单命令或通过按 CTRL-B SHIFT。

现在，已更新`Model`类，您还需要更新*\Views\Movies\Index.cshtml*并*\Views\Movies\Create.cshtml*查看模板以显示新`Rating`浏览器视图中的属性。

打开<em>\Views\Movies\Index.cshtml</em>文件，并添加`<th>Rating</th>`列标题之后<strong>价格</strong>列。 然后添加`<td>`快要结束的模板来呈现列`@item.Rating`值。 下面是哪些更新<em>Index.cshtml</em>视图模板如下所示：

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

接下来，打开*\Views\Movies\Create.cshtml*文件，并添加以下标记窗体的结尾附近。 这会使文本框中，以便创建新电影时，可以指定一个级别。

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

现已更新以支持新的应用程序代码`Rating`属性。

现在，运行该应用程序并导航到 */Movies* URL。 执行此操作，不过，将看到以下错误之一：

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

之所以看到此错误，因为已更新`Movie`应用程序中的 model 类现在与不同的架构`Movie`现有数据库表。 （数据库表中没有 `Rating` 列。）


可通过几种方法解决此错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 这种方法就是很方便时测试数据库; 上进行开发它可以一起快速改进模型和数据库架构。 缺点，不过，是会丢失数据库中的现有数据，因此您*不*需要生产数据库上使用此方法 ！ 使用初始值设定项以自动设定种子使用测试数据的数据库通常是开发的应用程序的有效方式。 有关实体框架数据库初始值设定项的详细信息，请参阅 Tom Dykstra [ASP.NET MVC/实体框架教程](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。
3. 使用 Code First 迁移更新数据库架构。


本教程使用 Code First 迁移。

更新 Seed 方法，使它向新列提供值。 打开 Migrations\Configuration.cs 文件并将评级字段添加到每个电影对象。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

生成解决方案，然后打开**程序包管理器控制台**窗口并输入以下命令：

`add-migration AddRatingMig`

`add-migration`命令会通知迁移框架以检查当前电影模型与当前的电影数据库架构并创建必要的代码以将数据库迁移到新模型。 AddRatingMig 是任意参数并用于命名迁移文件。 最好使用迁移步骤有意义的名称。

此命令完成后，Visual Studio 会打开定义新的类文件`DbMIgration`派生的类，然后在`Up`方法您可以看到创建的新列的代码。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

生成解决方案，并输入中的"更新数据库"命令**程序包管理器控制台**窗口。

下图显示了中的输出**程序包管理器控制台**窗口 （预先计算 AddRatingMig 的日期戳将与此不同。）

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

重新运行该应用程序并导航到 /Movies URL。 您可以看到新的评级字段。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

单击**创建新**链接以添加新电影。 请注意，您可以添加一个级别。

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

单击 **“创建”**。 新电影，包括分级，现在显示在列表的电影：

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

您还应添加`Rating`字段编辑、 详细信息和 SearchIndex 视图模板。

可以输入中的"更新数据库"命令**程序包管理器控制台**再次窗口和任何更改将会发生，因为该架构与模型相匹配。

在本部分中您将看到如何修改模型对象并使数据库所做的更改同步。 你还了解了一种方法来填充新创建的数据库使用示例数据，这样您可以试用方案。 接下来，让我们看看如何将更丰富的验证逻辑添加到模型类并启用某些业务规则以强制实施。

> [!div class="step-by-step"]
> [上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)
