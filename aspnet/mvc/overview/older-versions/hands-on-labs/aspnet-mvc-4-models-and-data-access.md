---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 模型和数据访问 |Microsoft Docs
author: rick-anderson
description: 注意： 此动手实验假定你的 ASP.NET MVC 基础知识。 如果你未使用过 ASP.NET MVC 之前，我们建议你通过 ASP.NET MVC 4...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 26896e6ee3c02e8f939296ecbfb8b7d500940765
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825278"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 模型和数据访问

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验假定你已了解的基础知识**ASP.NET MVC**。 如果您未使用过**ASP.NET MVC**之前，我们建议你超出**ASP.NET MVC 4 基础知识**动手实验。

此实验室将引导你通过前面所述通过将细微的更改应用于源文件夹中提供的示例 Web 应用的新功能和增强功能。

> [!NOTE]
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[ASP.NET MVC 4 模型和数据访问](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)。

在中**ASP.NET MVC 基础知识**动手实验中，您已经传递了硬编码数据从控制器到视图模板。 但是，若要生成实际的 Web 应用程序，你可能想要使用的实际数据库。

此动手实验室将演示如何为使用数据库引擎，以便存储和检索音乐应用商店应用程序所需的数据。 若要完成此操作，将启动使用现有的数据库并从中创建实体数据模型。 在此实验中，将满足**Database First**方法并将**Code First**方法。

但是，还可以使用**Model First**方法，创建相同的模型使用的工具，然后从其生成数据库。

![数据库第一个 vs。模型优先](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs。模型优先")

*数据库第一个 vs。模型优先*

生成模型之后, 将 StoreController 存储视图提供从数据库中，而不是使用硬编码数据中获取的数据中进行适当调整。 不需要对进行任何更改视图模板由于 StoreController 将返回相同的 Viewmodel 对视图模板中，尽管这一次的数据将来自该数据库。

**代码第一种方法**

代码第一种方法允许我们定义的代码模型而不会生成通常结合了框架的类。

在代码中首先，模型对象定义 Poco，与&quot;Plain Old CLR Objects&quot;。 Poco 是简单的普通类不继承并不实现接口。 我们可以自动生成数据库，从它们，也可以使用现有数据库并从代码生成的类映射。

使用此方法的好处是模型仍独立于持久性框架 （在本例中为实体框架），与 Poco 类不结合映射框架。

> [!NOTE]
> 此实验室基于 ASP.NET MVC 4 和音乐应用商店示例应用程序的版本自定义和最小化以适合仅在此动手实验中所示的功能。
> 
> 如果你想要浏览整个**音乐应用商店**教程应用程序可以找到它在[MVC Music 商店](https://github.com/evilDave/MVC-Music-Store)。


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

必须具有要完成本实验的以下项：

- [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。 若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 c： 使用代码片段](#AppendixC)&quot;。

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包含由以下练习：

1. [练习 1： 添加数据库](#Exercise1)
2. [练习 2： 创建使用 Code First 数据库](#Exercise2)
3. [练习 3： 查询具有参数的数据库](#Exercise3)

> [!NOTE]
> 每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。


估计的时间才能完成此实验： **35 だ 牧**。

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>练习 1： 添加数据库

在此练习中，您将学习如何添加具有 MusicStore 应用程序，向解决方案以便使用其数据的表的数据库。 一旦使用该模型生成数据库并将其添加到解决方案中，将修改 StoreController 类，以查看模板提供从数据库中，而不是使用硬编码的值中获取的数据。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>任务 1-添加数据库

在本任务中，您将添加到解决方案 MusicStore 应用程序的主表已创建的数据库。

1. 打开**开始**解决方案位于**源/Ex1-AddingADatabaseDBFirst/开始/** 文件夹。

   1. 需要先下载某些缺少的 NuGet 包然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 添加**MvcMusicStore**数据库文件。 在本动手实验中，你将使用名为已创建的数据库**MvcMusicStore.mdf**。 为此，请右键单击**应用程序\_数据**文件夹，指向**添加**，然后单击**现有项**。 浏览到**\Source\Assets** ，然后选择**MvcMusicStore.mdf**文件。

    ![添加现有项目](aspnet-mvc-4-models-and-data-access/_static/image2.png "添加现有项目")

    *添加现有项目*

    ![MvcMusicStore.mdf 数据库文件](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf 数据库文件")

    *MvcMusicStore.mdf 数据库文件*

    数据库已添加到项目。 即使数据库所在的解决方案内，可以查询和更新它，因为它托管在不同的数据库服务器中。

    ![在解决方案资源管理器中的 MvcMusicStore 数据库](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore 数据库在解决方案资源管理器")

    *在解决方案资源管理器中的 MvcMusicStore 数据库*
3. 验证到数据库的连接。 若要执行此操作，请双击**MvcMusicStore.mdf**建立的连接。

    ![连接到 MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "连接到 MvcMusicStore.mdf")

    *连接到 MvcMusicStore.mdf*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>任务 2-创建数据模型

在本任务中，将创建数据模型与上一任务中添加的数据库进行交互。

1. 创建将表示的数据库的数据模型。 为此，请在解决方案资源管理器中右击**模型**文件夹，指向**添加**，然后单击**新项**。 在中**添加新项**对话框中，选择**数据**模板，然后**ADO.NET 实体数据模型**项。 将数据模型名称更改为**StoreDB.edmx**然后单击**添加**。

    ![添加 StoreDB ADO.NET 实体数据模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "添加 StoreDB ADO.NET 实体数据模型")

    *添加 StoreDB ADO.NET 实体数据模型*
2. **实体数据模型向导**将出现。 此向导将引导您完成创建模型层。 由于该模型应创建基于现有的数据库 recentyl 添加，因此选择**从数据库生成**然后单击**下一步**。

    ![选择模型内容](aspnet-mvc-4-models-and-data-access/_static/image7.png "选择模型内容")

    *选择模型内容*
3. 由于您从数据库生成模型，需要指定要使用的连接。 单击**新的连接**。
4. 选择**Microsoft SQL Server 数据库文件**然后单击**继续**。

    ![选择数据源](aspnet-mvc-4-models-and-data-access/_static/image8.png "选择数据源")

    *选择数据源对话框*
5. 单击**浏览**，然后选择数据库**MvcMusicStore.mdf**你在中找到**应用\_数据**文件夹，然后单击**确定**。

    ![连接属性](aspnet-mvc-4-models-and-data-access/_static/image9.png "连接属性")

    *连接属性*
6. 生成的类应该具有与实体连接字符串相同的名称，因此其名称更改为**MusicStoreEntities**然后单击**下一步**。

    ![选择数据连接](aspnet-mvc-4-models-and-data-access/_static/image10.png "选择数据连接")

    *选择数据连接*
7. 选择要使用的数据库对象。 因为实体模型将使用只是数据库的表，选择**表**选项，并确保选中**在模型中包含外键列**和**确定的单复数生成对象名**选项也将被选中。 更改到模型 Namespace **MvcMusicStore.Model**然后单击**完成**。

    ![选择数据库对象](aspnet-mvc-4-models-and-data-access/_static/image11.png "选择数据库对象")

    *选择数据库对象*

    > [!NOTE]
    > 如果显示安全警告对话框，单击**确定**运行该模板并生成模型实体的类。
8. 用于数据库的实体关系图将显示，而将创建一个单独的类映射到数据库的每个表。 例如，**相册**表将由表示**唱片集**类，其中每个表中的列将映射到类属性。 这样，您可以查询和使用这些对象表示数据库中的行。

    ![实体关系图](aspnet-mvc-4-models-and-data-access/_static/image12.png "实体关系图")

    *实体关系图*

    > [!NOTE]
    > T4 模板 (.tt) 运行代码，以生成实体类，并将覆盖具有相同名称的现有类。 在此示例中，类&quot;唱片集&quot;，&quot;流派&quot;并&quot;艺术家&quot;覆盖与生成的代码。


<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>任务 3-生成应用程序

在本任务中，您将检查，尽管模型生成已删除**唱片集**，**流派**并**艺术家**模型类，成功生成项目通过使用新的数据模型类。

1. 通过选择生成项目**构建**菜单项，然后**生成 MvcMusicStore**。

    ![生成项目](aspnet-mvc-4-models-and-data-access/_static/image13.png "生成项目")

    *生成项目*
2. 成功生成项目。 为什么它仍工作？ 它有效，因为数据库表具有已删除的类中包含已使用的属性字段**唱片集**并**流派**。

    ![生成成功](aspnet-mvc-4-models-and-data-access/_static/image14.png "生成成功")

    *生成成功*
3. 尽管在设计器关系图格式显示实体，它们实际上是 C# 类。 展开**StoreDB.edmx**在解决方案资源管理器中的节点，然后**StoreDB.tt**，你将看到新生成的实体。

    ![生成的文件](aspnet-mvc-4-models-and-data-access/_static/image15.png "生成的文件")

    *生成的文件*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>任务 4-查询数据库

在此任务中，将更新 StoreController 类，以便不使用硬编码数据，它将查询数据库以检索信息。

1. 打开**Controllers\StoreController.cs**并将以下字段添加到要保存的实例的类**MusicStoreEntities**类，名为**storeDB**:

    (代码段-*模型和数据访问权限的 Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **MusicStoreEntities**类公开数据库中每个表的集合属性。 更新**浏览**操作方法来检索所有流派**相册**。

    (代码段-*模型和数据访问-Ex1 应用商店浏览*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > 使用.NET 调用的一项功能**LINQ** （语言集成查询） 来编写强类型化查询表达式对这些集合-将执行对数据库的代码并返回对象，您可以进行编程作用。
    > 
    > 有关 LINQ 的详细信息，请访问[msdn 站点](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。
3. 更新**索引**操作方法来检索所有流派。

    (代码段-*模型和数据访问-Ex1 存储索引*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. 更新**索引**操作方法来检索所有流派和转换列表的集合。

    (代码段-*模型和数据访问-Ex1 存储 GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，将检查存储索引页现在将显示存储在数据库而不是硬编码的流派。 若要更改视图模板，因为无需**StoreController**返回相同的实体与之前一样，尽管这一次的数据将来自该数据库。

1. 重新生成解决方案并按**F5**运行该应用程序。
2. 在主页页面中启动项目。 验证的菜单**流派**不再是硬编码列表，并直接从数据库检索的数据。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *从数据库中浏览类型*
3. 现在浏览到任何类型，并验证从数据库中填充唱片集。

    ![从数据库中浏览相册](aspnet-mvc-4-models-and-data-access/_static/image17.png "浏览数据库中的唱片集")

    *从数据库中浏览唱片集*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>练习 2： 创建使用 Code First 数据库

在此练习中，您将学习如何使用代码第一种方法来创建具有 MusicStore 应用程序的表的数据库以及如何访问其数据。

模型生成后，您将修改 StoreController 视图模板提供从数据库中，而不是使用硬编码值中获取的数据。

> [!NOTE]
> 如果已完成练习 1 中，已处理过数据库第一种方法，将现在了解如何获取与不同的进程相同的结果。 已标记与练习 1 中相同的任务以方便您阅读。 如果尚未完成练习 1，但想要了解代码第一种方法，可以从本练习中启动，并获取该主题的完整的覆盖范围。


<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>任务 1-填充示例数据

在此任务中，将开始创建使用代码优先时填充示例数据的数据库。

1. 打开**开始**解决方案位于**源/Ex2-CreatingADatabaseCodeFirst/开始/** 文件夹。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 添加**SampleData.cs**的文件**模型**文件夹。 为此，请右键单击**模型**文件夹，指向**添加**，然后单击**现有项**。 浏览到**\Source\Assets** ，然后选择**SampleData.cs**文件。

    ![示例数据填充代码](aspnet-mvc-4-models-and-data-access/_static/image18.png "示例数据填充代码")

    *示例数据填充代码*
3. 打开**Global.asax.cs**文件，并添加以下*使用*语句。

    (代码段-*模型和数据访问-Ex2 全局 Asax Using*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. 在中**应用程序\_start （)** 方法添加以下行以设置数据库初始值设定项。

    (代码段-*模型和数据访问-Ex2 全局 Asax SetInitializer*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>任务 2-配置数据库的连接

现在，已将数据库加入我们的项目，将在中编写**Web.config**文件的连接字符串。

1. 添加在连接字符串**Web.config**。为此，请打开**Web.config**在项目根和替换连接字符串中的此行与名为 DefaultConnection **&lt;connectionStrings&gt;** 部分：

    ![Web.config 文件位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 文件位置")

    *Web.config 文件位置*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>任务 3-使用的模型

现在，已配置数据库的连接，将链接的模型与数据库表。 在本任务中，将创建将链接到的数据库使用 Code First 的类。 请记住，应修改的现有 POCO 模型类。

> [!NOTE]
> 如果你完成练习 1 中，您会注意此步骤由一个向导。 通过执行 Code First，您将手动创建将链接到数据实体的类。

1. 打开 POCO 模型类**流派**从**模型**项目文件夹，并包含一个 id。 使用整型属性以名称**GenreId**。

    (代码段-*模型和数据访问-Ex2 代码的第一个流派*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > 若要使用 Code First 约定，类类型必须具有主键属性，将自动检测到。
    > 
    > 你可以阅读更多有关在此代码优先约定[msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)。
2. 现在，打开 POCO 模型类**唱片集**从**模型**项目文件夹和包含外键，创建属性的名称**GenreId**和**ArtistId**。 此类已有**GenreId**为主键。

    (代码段-*模型和数据访问-Ex2 代码第一个唱片集*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. 打开 POCO 模型类**艺术家**和包含**ArtistId**属性。

    (代码段-*模型和数据访问-Ex2 代码的第一个艺术家*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. 右键单击**模型**项目文件夹，然后选择**添加 |类**。 将文件命名**MusicStoreEntities.cs**。 然后，单击**添加。**

    ![添加类](aspnet-mvc-4-models-and-data-access/_static/image20.png "添加类")

    *添加新项*

    ![添加 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "添加 class2")

    *添加类*
5. 打开您刚创建的类**MusicStoreEntities.cs**，并包括命名空间**System.Data.Entity**并**System.Data.Entity.Infrastructure**。

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. 替换为要扩展的类声明**DbContext**类： 声明一个公共**DBSet**并重写**OnModelCreating**方法。 在此步骤后，你将收到您的模型使用实体框架将链接的域类。 为此，将为与以下的类代码：

    (代码段-*模型和数据访问-Ex2 代码的第一个 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> 使用实体框架**DbContext**并**DBSet**可以查询 POCO 类流派。 通过扩展**OnModelCreating**中指定的方法，**代码**如何类型将映射到数据库表。 可以在此 msdn 文章中找到有关 DBContext 和 DBSet 的详细信息：[链接](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>任务 4-查询数据库

在此任务中，将更新 StoreController 类，以便不使用硬编码数据，它将其从数据库中检索。

> [!NOTE]
> 此任务是与练习 1 中相同。
> 
> 如果你完成练习 1 中您将注意这些步骤都在这两种方法中相同的 (数据库优先或代码优先)。 它们是不同中如何将数据链接模型，但对数据实体的访问权限是尚未从控制器透明的。


1. 打开**Controllers\StoreController.cs**并将以下字段添加到要保存的实例的类**MusicStoreEntities**类，名为**storeDB**:

    (代码段-*模型和数据访问权限的 Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **MusicStoreEntities**类公开数据库中每个表的集合属性。 更新**浏览**操作方法来检索所有流派**相册**。

    (代码段-*模型和数据访问-Ex2 应用商店浏览*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > 使用.NET 调用的一项功能**LINQ** （语言集成查询） 来编写强类型化查询表达式对这些集合-将执行对数据库的代码并返回对象，您可以进行编程作用。
    > 
    > 有关 LINQ 的详细信息，请访问[msdn 站点](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。
3. 更新**索引**操作方法来检索所有流派。

    (代码段-*模型和数据访问-Ex2 存储索引*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. 更新**索引**操作方法来检索所有流派和转换列表的集合。

    (代码段-*模型和数据访问-Ex2 存储 GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，将检查存储索引页现在将显示存储在数据库而不是硬编码的流派。 若要更改视图模板，因为无需**StoreController**返回相同**StoreIndexViewModel**与之前一样，但这一次的数据将来自该数据库。

1. 重新生成解决方案并按**F5**运行该应用程序。
2. 在主页页面中启动项目。 验证的菜单**流派**不再是硬编码列表，并直接从数据库检索的数据。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *从数据库中浏览类型*
3. 现在浏览到任何类型，并验证从数据库中填充唱片集。

    ![从数据库中浏览相册](aspnet-mvc-4-models-and-data-access/_static/image23.png "浏览数据库中的唱片集")

    *从数据库中浏览唱片集*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>练习 3： 查询具有参数的数据库

在此练习中，您将了解如何使用参数，在数据库中查询以及如何使用查询结果调整，一项功能，减少了数字数据库以更有效地访问中检索数据。

> [!NOTE]
> 查询结果调整的详细信息，请访问以下[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>任务 1-修改 StoreController 从数据库检索相册

在本任务中，您将更改**StoreController**类来访问数据库以检索特定流派的唱片集。

1. 打开**开始**解决方案位于**Source\Ex3 QueryingTheDatabaseWithParametersCodeFirst\Begin**文件夹，如果想要使用代码优先方法或**Source\Ex3 QueryingTheDatabaseWithParametersDBFirst\Begin**文件夹，如果想要使用数据库为先的方法。 否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。

   1. 如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。 若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。
   2. 在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。
   3. 最后，通过单击生成解决方案**构建** | **生成解决方案**。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。 使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。 这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。
2. 打开**StoreController**类，以更改**浏览**操作方法。 若要执行此操作，在**解决方案资源管理器**，展开**控制器**文件夹，然后双击**StoreController.cs**。
3. 更改**浏览**操作方法来检索特定流派的唱片集。 若要执行此操作，将以下代码：

    (代码段-*模型和数据访问-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> 若要填充的实体的集合，您需要使用**Include**方法，以指定你想要过检索相册。 可以使用。**Single （)** 中 LINQ 的扩展因为在这种情况下只有一个流派预期唱片集。 **Single （)** 方法采用 Lambda 表达式作为参数，在这种情况下指定单个流派对象，以便其名称不匹配定义的值。
> 
> 将充分利用一项功能，可用于指示检索该类型对象时，你需要同时加载其他相关的实体。 此功能被称为**查询结果调整**，并使您可以减少访问数据库以检索信息所需的次数。 在此方案中，你将想要预提取检索的流派唱片集。
> 
> 该查询包含**Genres.Include (&quot;相册&quot;)** 以指示要以及相关的唱片集。 这将导致更高效的应用程序，因为它会检索中的单个数据库请求流派和唱片集的数据。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在本任务中，将运行该应用程序，并从数据库中检索的特定流派的唱片集。

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/Store/浏览？ genre = Pop**以验证从数据库检索到结果。

    ![浏览按流派](aspnet-mvc-4-models-and-data-access/_static/image24.png "按流派浏览")

    *浏览/Store/浏览？ genre = Pop*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>任务 3-访问唱片集的 Id

在此任务中，将重复前面的过程，以获取唱片集由其 id。

1. 关闭浏览器，如果需要可以返回到 Visual Studio。 打开**StoreController**类，以更改**详细信息**操作方法。 若要执行此操作，在**解决方案资源管理器**，展开**控制器**文件夹，然后双击**StoreController.cs**。
2. 更改**详细信息**操作方法来检索相册详细信息，根据其**Id**。若要执行此操作，将以下代码：

    (代码段-*模型和数据访问-Ex3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在本任务中，将在 web 浏览器中运行应用程序并获取由其 id 的唱片集详细信息

1. 按**F5**运行该应用程序。
2. 在主页页面中启动项目。 将 URL 更改为 **/Store/Details/51**或浏览流派，并选择某个唱片集以验证从数据库检索到结果。

    ![浏览的详细信息](aspnet-mvc-4-models-and-data-access/_static/image25.png "浏览详细信息")

    *浏览 /Store/Details/51*

> [!NOTE]
> 此外，可以部署此应用程序到 Windows Azure Web Sites 以下[附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署](#AppendixB)。

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

通过完成本动手实验介绍了 ASP.NET MVC 模型和数据访问的基础知识，请使用**Database First**方法并将**Code First**方法：

- 如何将数据库添加到解决方案，以便使用其数据
- 如何更新控制器，以提供从而不是硬编码一个数据库中获取的数据视图模板
- 如何使用参数在数据库中查询
- 如何使用查询结果调整，一项功能，用于减少数据库访问中更有效地检索数据
- 如何在 Microsoft Entity Framework 中使用数据库优先和代码优先方法，用于链接的模型数据库

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/?linkid=9810169 ](https://go.microsoft.com/?linkid=9810169) ](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 b： 发布 ASP.NET MVC 4 应用程序使用 Web 部署

本附录将演示如何从 Windows Azure 管理门户创建新的网站和发布应用程序获取按照本实验中，利用 Windows Azure 提供的 Web 部署发布功能。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-创建新的 Web 站点从 Windows Azure 门户

1. 转到[Windows Azure 管理门户](https://manage.windowsazure.com/)并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 使用 Windows Azure 可以免费托管 10 个 ASP.NET 网站，然后随着流量增长情况。 你可以注册[此处](http://aka.ms/aspnet-hol-azure)。

    ![登录到 Windows Azure 门户](aspnet-mvc-4-models-and-data-access/_static/image31.png "登录到 Windows Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击**新建**命令栏上。

    ![创建新的 Web 站点](aspnet-mvc-4-models-and-data-access/_static/image32.png "创建新的 Web 站点")

    *创建新的 Web 站点*
3. 单击**计算** | **网站**。 然后选择**快速创建**选项。 为新网站提供可用的 URL，然后单击**创建网站**。

    > [!NOTE]
    > Windows Azure 网站是可以控制和管理在云中运行的 web 应用程序主机。 快速创建选项，可将已完成的 web 应用程序到 Windows Azure 网站从门户外部的部署。 它不包括用于设置数据库的步骤。

    ![创建新的网站使用快速创建](aspnet-mvc-4-models-and-data-access/_static/image33.png "创建新的网站使用快速创建")

    *创建新的网站使用快速创建*
4. 等到新**网站**创建。
5. 创建网站后，单击下面的链接**URL**列。 检查新的 Web 站点正常工作。

    ![浏览到新的 web 站点](aspnet-mvc-4-models-and-data-access/_static/image34.png "浏览到新的 web 站点")

    *浏览到新的 web 站点*

    ![正在运行的网站](aspnet-mvc-4-models-and-data-access/_static/image35.png "正在运行的网站")

    *正在运行的网站*
6. 返回到门户并单击下的 web 站点的名称**名称**列中显示的管理页。

    ![打开网站管理页](aspnet-mvc-4-models-and-data-access/_static/image36.png "打开网站管理页")

    *打开网站管理页*
7. 在中**仪表板**页面上，在**速览**部分中，单击**下载发布配置文件**链接。

    > [!NOTE]
    > *发布配置文件*包含所有发布到每个启用的发布方法的 Windows Azure 网站的 web 应用程序所需的信息。 发布配置文件包含 Url、 用户凭据和连接到并对每个发布方法启用的终结点进行身份验证所需的数据库字符串。 **Microsoft WebMatrix 2**， **Microsoft Visual Studio Express for Web**并**Microsoft Visual Studio 2012**支持读取发布配置文件，以自动执行这些计划的配置web 应用程序发布到 Windows Azure 网站。

    ![正在下载网站发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image37.png "下载网站发布配置文件")

    *正在下载网站发布配置文件*
8. 下载发布配置文件到已知位置。 进一步在此练习中将了解如何使用此文件从 Visual Studio 的 web 应用程序到 Windows Azure 网站发布。

    ![保存发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image38.png "保存发布配置文件")

    *保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果你的应用程序将使用的 SQL Server 数据库将需要创建 SQL 数据库服务器。 如果你想要部署的简单应用程序不使用 SQL Server 可能会跳过此任务。

1. 用于存储应用程序数据库，将需要 SQL 数据库服务器。 可以从在 Windows Azure 管理门户在订阅中查看 SQL 数据库服务器**Sql 数据库** | **服务器** | **服务器的仪表板**。 如果没有创建的服务器，则可以创建一个使用**添加**命令栏上的按钮。 请注意**服务器名称和 URL、 管理员登录名和密码**，因为你将在下一任务中使用它们。 不创建数据库，因为它将在后面的阶段中创建。

    ![SQL 数据库服务器仪表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一个任务将测试从 Visual Studio 中，数据库连接，因此您需要在服务器的列表中包括你的本地 IP 地址**允许的 IP 地址**。 若要执行此操作，请单击**配置**，选择中的 IP 地址**当前客户端 IP 地址**并将其粘贴在上**起始 IP 地址**和**结束 IP 地址**文本框中，然后单击![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png)按钮。

    ![添加客户端 IP 地址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *添加客户端 IP 地址*
3. 一次**客户端 IP 地址**添加到允许的 IP 地址列表中，单击**保存**以确认所做的更改。

    ![确认更改](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-ASP.NET MVC 4 应用程序使用 Web 部署发布

1. 返回到 ASP.NET MVC 4 解决方案。 在中**解决方案资源管理器**，右键单击网站项目并选择**发布**。

    ![发布应用程序](aspnet-mvc-4-models-and-data-access/_static/image43.png "发布应用程序")

    *发布此网站*
2. 导入发布配置文件保存在第一个任务。

    ![导入发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image44.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击**验证连接**。 验证完成后单击**下一步**。

    > [!NOTE]
    > 请参阅验证连接按钮旁边会出现一个绿色复选标记后，验证已完成。

    ![验证连接](aspnet-mvc-4-models-and-data-access/_static/image45.png "验证连接")

    *验证连接*
4. 在中**设置**页面上，在**数据库**部分中，单击您的数据库连接的文本框旁边的按钮 (即**DefaultConnection**)。

    ![Web 部署配置](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web 部署配置")

    *Web 部署配置*
5. 配置数据库连接，如下所示：

   - 在中**服务器名称**键入 SQL 数据库服务器 URL 使用*tcp:* 前缀。
   - 在中**用户名**键入服务器管理员登录名。
   - 在中**密码**键入服务器管理员登录密码。
   - 键入新的数据库名称。

     ![配置目标连接字符串](aspnet-mvc-4-models-and-data-access/_static/image47.png "配置目标连接字符串")

     *配置目标连接字符串*
6. 然后单击“确定” 。 当系统提示你创建数据库时，单击**是**。

    ![创建数据库](aspnet-mvc-4-models-and-data-access/_static/image48.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串是显示在默认连接文本框内。 然后，单击 **“下一步”**。

    ![连接字符串指向 SQL 数据库](aspnet-mvc-4-models-and-data-access/_static/image49.png "指向 SQL 数据库连接字符串")

    *连接字符串指向 SQL 数据库*
8. 在中**预览版**页上，单击**发布**。

    ![Web 应用程序发布](aspnet-mvc-4-models-and-data-access/_static/image50.png "发布 web 应用程序")

    *Web 应用程序发布*
9. 在发布过程完成后，在默认浏览器将打开已发布的网站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 c： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-models-and-data-access/_static/image51.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](aspnet-mvc-4-models-and-data-access/_static/image52.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-models-and-data-access/_static/image55.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-models-and-data-access/_static/image56.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
