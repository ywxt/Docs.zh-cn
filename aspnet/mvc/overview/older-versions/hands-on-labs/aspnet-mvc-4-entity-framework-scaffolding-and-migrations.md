---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 基架和迁移 |Microsoft Docs
author: rick-anderson
description: 如果您熟悉 ASP.NET MVC 4 控制器方法中，或已完成&quot;帮助器、 窗体和验证&quot;动手实验中，您应该知道...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/18/2013
ms.topic: article
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: a385ffd3f0067d4ac56d592b0f2bf151fc0f8dd4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37394198"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework 基架和迁移

通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

如果您熟悉 ASP.NET MVC 4 控制器方法中，或已完成&quot;帮助器、 窗体和验证&quot;动手实验中，您应注意许多逻辑来创建、 更新、 列出和删除重复它的任何数据实体在应用程序。 更不必说，如果您的模型具有多个类来处理，您将有可能花费相当长的时间编写每个实体操作，以及每个视图的 POST 和 GET 操作方法。

在此实验室中将了解如何使用 ASP.NET MVC 4 基架自动生成的应用程序的 CRUD （创建、 读取、 更新和删除） 基线。 开始从简单的模型类，而无需编写一行代码，将创建将包含所有 CRUD 操作，以及所有必要视图的控制器。 生成和运行简单的解决方案后, 将已生成，以及 MVC 逻辑和视图的数据操作的应用程序数据库。

此外，您将学习使用实体框架迁移执行模型更新在整个应用是多么容易。 Entity Framework 迁移将让你修改你的数据库后的模型已更改简单的步骤。 与所有这些记住，将能够构建和维护 web 应用程序更有效地利用 ASP.NET MVC 4 的最新功能。

> [!NOTE]
> 在 Web 训练营培训工具包中，在可从包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。 特定于此实验室项目位于[ASP.NET MVC 4 Entity Framework 基架和迁移](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，你将了解如何：

- 使用 ASP.NET 基架的控制器中的 CRUD 操作。
- 更改使用 Entity Framework 迁移的数据库模型。

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

如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 b： 使用代码片段](#AppendixB)&quot;。

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

以下练习中构成本动手实验：

1. [使用 ASP.NET MVC 4 基架和实体框架迁移](#Exercise1)

> [!NOTE]
> 此练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。 如果您需要在完成该练习的更多帮助，可以使用此解决方案作为指南。


估计的时间才能完成此实验： **30 分钟**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>练习 1： 使用 ASP.NET MVC 4 基架和实体框架迁移

ASP.NET MVC 基架提供了一种标准化方法，创建必要的逻辑，可让您与数据库层进行交互的应用程序生成的 CRUD 操作的快速方法。

在此练习中，您将学习如何使用 ASP.NET MVC 4 基架代码首先创建 CRUD 方法。 然后，您将学习如何更新您的模型使用 Entity Framework 迁移应用中数据库的更改。

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>任务 1-创建新的 ASP.NET MVC 4 项目使用基架

1. 如果尚未打开，启动**Visual Studio 2012**。
2. 选择**文件 |新的项目**。 在新建项目对话框中，在**Visual C# |Web**部分中，选择**ASP.NET MVC 4 Web 应用程序**。 为项目命名为**MVC4andEFMigrations**并将位置设置为**Source\Ex1 UsingMVC4ScaffoldingEFMigrations**本实验的文件夹。 设置**解决方案名称**到**开始**，并确保**创建解决方案目录**检查。 单击 **“确定”**。

    ![新建 ASP.NET MVC 4 项目对话框](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "新建 ASP.NET MVC 4 项目对话框")

    *新建 ASP.NET MVC 4 项目对话框*
3. 在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Internet 应用程序**模板，并确保选中**Razor**是所选**视图引擎**. 单击“确定”，创建项目。

    ![新的 ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新 ASP.NET MVC 4 Internet 应用程序")

    *新的 ASP.NET MVC 4 Internet 应用程序*
4. 在解决方案资源管理器，右键单击**模型**，然后选择**添加 |类**创建简单的类人员 (POCO)。 其命名为**Person**然后单击**确定**。
5. 打开 Person 类，并插入以下属性。

    (代码段- *ASP.NET MVC 4 和 Entity Framework 迁移-Ex1 人员属性*)

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. 单击**生成 |生成解决方案**以保存所做的更改并生成项目。

    ![生成应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "生成应用程序")

    *生成应用程序*
7. 在解决方案资源管理器，右键单击 controllers 文件夹并选择**添加 |控制器**。
8. 将控制器命名*PersonController*并完成**基架选项**使用以下值。

   1. 在中**模板**下拉列表中，选择**读/写操作和视图使用 Entity Framework 的 MVC 控制器**选项。
   2. 在中**模型类**下拉列表中，选择**人员**类。
   3. 在中**数据上下文类**列表中，选择**&lt;新建数据上下文...&gt;**. 选择任何名称，然后单击**确定**。
   4. 在中**视图**下拉列表中，请确保**Razor**处于选中状态。

      ![添加人员控制器使用基架](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "添加基架的人员控制器")

      *添加基架的人员控制器*
9. 单击**添加**人员使用基架创建的新控制器。 您现在已经生成的控制器操作，以及视图。

    ![之后使用基架创建 Person 控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "后使用基架创建 Person 控制器")

    *之后使用基架创建 Person 控制器*
10. 打开**PersonController**类。 请注意，自动生成完整的 CRUD 操作方法。

   ![内部人员控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "内部人员控制器")

   *内部人员控制器*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>任务 2-运行应用程序

此时，将不创建数据库。 在此任务中，将运行第一次该应用程序和测试的 CRUD 操作。 将使用 Code First 动态创建数据库。

1. 按 **F5** 运行该应用程序。
2. 在浏览器中，添加 **/Person**到 URL 以打开人员页。

    ![首次运行的应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "首次运行的应用程序")

    *首次运行应用程序：*
3. 现在，您将浏览人员页和测试的 CRUD 操作。

    1. 单击**创建新**以添加新人员。 输入名字和姓氏，然后单击**创建**。

        ![添加新人员](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "添加新人员")

        *添加新人员*
    2. 在此人的列表中，可以删除、 编辑或添加项。

        ![个人列表](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "人员列表")

        *个人列表*
    3. 单击**详细信息**打开联系人的详细信息。

        ![人员的详细信息](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人员的详细信息")

        *人员的详细信息*
4. 关闭浏览器并返回到 Visual Studio。 请注意，你已创建人员实体的整个 CRUD 在整个-从到视图的视图模型的应用程序而无需编写一行代码 ！

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>任务 3-更新使用 Entity Framework 迁移的数据库

在此任务将更新使用 Entity Framework 迁移的数据库。 你会发现更改的模型并使用 Entity Framework 迁移功能反映数据库中的更改是多么容易。

1. 打开包管理器控制台。 选择**工具 |库包管理器 |包管理器控制台**。
2. 在包管理器控制台中，输入以下命令：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![启用迁移](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "启用迁移")

    *启用迁移*

    启用迁移命令将创建**迁移**文件夹，其中包含用于初始化数据库的脚本。

    ![Migrations 文件夹](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations 文件夹")

    *Migrations 文件夹*
3. 打开**Configuration.cs** Migrations 文件夹中的文件。 找到的类构造函数并将更改**AutomaticMigrationsEnabled**值设置为*true*。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. 打开 Person 类并添加的联系人的中间名的属性。 使用此新属性，在更改模型。

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. 选择**生成 |生成解决方案**上生成应用程序的菜单。

    ![生成应用程序](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "生成应用程序")

    *生成应用程序*
6. 在包管理器控制台中，输入以下命令：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    此命令将查找的数据对象中的更改，然后，它将添加必要的命令来相应地修改数据库。

    ![添加中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "添加中间名")

    *添加中间名*
7. （可选）可以运行以下命令以生成一个包含差异更新的 SQL 脚本。 这样就可以手动更新数据库 （在这种情况下它不需要），或应用中其他数据库的更改：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![生成 SQL 脚本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "生成 SQL 脚本")

    *生成 SQL 脚本*

    ![SQL 脚本更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 脚本更新")

    *SQL 脚本更新*
8. 在包管理器控制台中，输入以下命令以更新数据库：

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![更新数据库](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "更新数据库")

    *更新数据库*

    这将添加**MiddleName**中的列**人**表以匹配的当前定义**人员**类。
9. 一旦更新数据库，右键单击控制器文件夹并选择**添加 |控制器**人员将控制器添加再次 （使用相同的值完成）。 这将更新的现有方法和视图添加新属性。

    ![添加控制器更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "添加控制器更新")

    *更新控制器*
10. 单击 **添加**。 然后，选择的值**覆盖 PersonController.cs**并**覆盖关联视图**然后单击**确定**。

   ![添加控制器覆盖](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *更新控制器*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>任务 4-运行应用程序

1. 按 **F5** 运行该应用程序。
2. 打开 **/Person**。 请注意已保留的数据时将中间名列添加。

    ![添加的中间名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "添加的中间名")

    *添加的中间名*
3. 如果单击**编辑**，可以将中间名添加到当前的人员。

    ![中间名 edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "中间名版本")

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>总结

在本动手实验介绍了简单的步骤来使用 ASP.NET MVC 4 基架使用任意模型类创建 CRUD 操作。 然后，您学习了如何使用 Entity Framework 迁移-从数据库到视图的应用程序中执行的端到端的更新。

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 a： 安装 Visual Studio Express 2012 for Web

你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**. 以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。

1. 转到[ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。
2. 单击**立即安装**。 如果还没有**Web 平台安装程序**将重定向以下载并安装。
3. 一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，然后单击**我接受**以继续。

    ![接受许可条款](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *接受许可条款*
5. 等待，直到下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *安装进度*
6. 安装完成后，单击**完成**。

    ![安装已完成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *安装已完成*
7. 单击**退出**以关闭 Web 平台安装程序。
8. 若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附录 b： 使用代码片段

使用代码段，可以轻松获得相关所需的所有代码。 实验室文档将告诉您完全何时可以使用它们，如下图中所示。

![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "使用 Visual Studio 代码段代码插入到你的项目")

*使用 Visual Studio 代码段代码插入到你的项目*

***若要添加代码段使用键盘 (仅限 C#)***

1. 将光标置于要插入的代码。
2. 开始键入代码片段名称 （不带空格或连字符）。
3. 观看作为 IntelliSense 显示匹配的代码段的名称。
4. 选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。
5. 按 Tab 键两次，以在光标位置插入代码段。

![开始键入代码段名称](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "开始键入代码段名称")

*开始键入代码段名称*

![按 tab 键以选择突出显示代码段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "按选项卡以选择突出显示代码段")

*按 tab 键以选择突出显示代码段*

![再次按 Tab 和代码段将 expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "再次按 Tab 和代码段将扩展")

*再次按 Tab 和代码段将扩展*

***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。 右键单击你想要插入的代码片段。

1. 选择**插入代码段**跟**我的代码片段**。
2. 通过单击选择列表中中的相关代码片段。

![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "右键单击你想要插入代码段和选择插入代码段")

*右键单击你想要插入代码段和选择插入代码段*

![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "通过单击选择列表中中的相关代码片段")

*通过单击选择列表中中的相关代码片段*
