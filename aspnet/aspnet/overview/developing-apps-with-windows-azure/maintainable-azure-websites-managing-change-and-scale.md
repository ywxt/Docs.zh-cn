---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 动手实验： 可维护 Azure 网站： 管理更改和缩放 |Microsoft Docs
author: rick-anderson
description: 在此实验中，了解如何 Microsoft Azure 轻松生成和部署到生产环境的网站。
ms.author: aspnetcontent
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: 3a118cdd7e3f3878976e4f8480ce2236b8d3ba88
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37824791"
---
<a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>动手实验： 可维护 Azure 网站： 管理更改和缩放
====================
通过[Web 训练营团队](https://twitter.com/webcamps)

[下载 Web 训练营培训工具包](http://aka.ms/webcamps-training-kit)

> Microsoft Azure 轻松生成和部署到生产环境的网站。 但你还未完成实时应用程序时，您只是开始 ！ 你将需要处理不断变化的要求、 数据库更新、 缩放性和的详细信息。 幸运的是，Azure 应用服务提供你的需求，并提供充足的功能，可帮助您保留你的网站平稳运行。
> 
> Azure 提供安全而灵活的开发、 部署和扩展任何规模的 web 应用程序的选项。 利用现有工具创建和部署应用程序，无需费力管理基础结构。
> 
> 通过预配生产 web 应用程序自己在几分钟内轻松地部署使用你最喜欢的开发工具创建的内容。 可以部署现有网站直接从源代码管理支持**Git**， **GitHub**， **Bitbucket**， **TFS**，并甚至**DropBox**。 直接从你喜爱的 IDE 或使用脚本部署**PowerShell**在 Windows 中或**CLI**任何操作系统上运行的工具。 部署完成后，可以保留你的网站同时支持连续部署持续保持最新状态。
> 
> 大型或小型，azure 会为任何数据，提供规模可变、 耐用的云存储、 备份和恢复解决方案。 当应用程序部署到生产环境，如表、 Blob 和 SQL 数据库的存储服务，帮助您缩放云应用程序。
> 
> 使用 SQL 数据库，务必使您提高工作效率的数据库部署新版本的应用程序时保持最新。 为感谢**Entity Framework Code First 迁移**，已简化的开发和部署你的数据模型以在几分钟内更新你的环境。 本动手实验中将显示在 web 应用部署到 Microsoft Azure 中的生产环境时，可能会遇到的不同主题。
> 
> 在 Web 训练营培训工具包中，可在包含所有示例代码和代码段[ http://aka.ms/webcamps-training-kit ](http://aka.ms/webcamps-training-kit)。
> 
> 本主题的更多深入介绍，请参阅[构建实际云应用程序与 Azure 的电子书](building-real-world-cloud-apps-with-windows-azure/introduction.md)。


<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验，您将学习如何：

- 让 Entity Framework 迁移使用现有模型
- 更新对象模型和相应地使用 Entity Framework 迁移数据库
- 将部署到 Azure 应用服务中使用 Git
- 回滚到以前的部署使用 Azure 管理门户
- 使用 Azure 存储来缩放 web 应用
- 配置使用 Azure 管理门户的 web 应用程序的自动缩放
- 创建和配置 Visual Studio 中负载测试项目

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下：

- [Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/)或更高版本
- [Azure SDK for.NET 2.2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT 版本控制系统](http://git-scm.com/download)
- Microsoft Azure 订阅 

    - 注册[免费试用版](http://aka.ms/watk-freetrial)
    - 如果你是 Visual Studio Professional、 Test Professional、 Premium 或 Ultimate with MSDN 或 MSDN 平台订户，激活你[MSDN 权益](http://aka.ms/watk-msdn)现在以开始开发和测试 Azure 上
    - [BizSpark](http://aka.ms/watk-bizspark)成员自动获得 Azure 通过其 Visual Studio Ultimate with MSDN 订阅权益
    - 成员[Microsoft 合作伙伴网络](http://aka.ms/watk-mpn)Cloud Essentials 计划接收免费的月度 Azure 额度

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行本动手实验中练习，需要先设置你的环境。

1. 打开 Windows 资源管理器并浏览到实验室**源**文件夹。
2. 右键单击**Setup.cmd** ，然后选择**以管理员身份运行**以启动将配置你的环境并安装本实验的 Visual Studio 代码段的安装过程。
3. 如果显示用户帐户控制对话框中，确认要继续执行的操作。

> [!NOTE]
> 请确保您运行安装程序之前已为此实验室的所有依赖项。


<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码片段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分以 Visual Studio 代码段，可以在 Visual Studio 2013，为了避免必须手动添加访问从形式提供。

> [!NOTE]
> 每个练习均附带位于中的开始解决方案**开始**本练习，您可以按照独立于其他每个练习的文件夹。 请注意在练习期间添加的代码片段缺少这些开始解决方案中，并且可能无法工作，直到完成该练习。 在练习的源代码，您将发现**最终**包含具有无法完成相应练习中的步骤得到的代码的 Visual Studio 解决方案文件夹。 如果您在演练本动手实验需要更多帮助，可以使用这些解决方案作为指南。


* * *

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [使用 Entity Framework 迁移](#Exercise1)
2. [Web 应用部署到过渡环境](#Exercise2)
3. [在生产环境中执行部署回滚](#Exercise3)
4. [使用 Azure 存储进行缩放](#Exercise4)
5. [使用适用于 Web 应用自动缩放](#Exercise5)（对于 Visual Studio 2013 旗舰版中的可选）

估计的时间才能完成此实验： **75 分钟**

> [!NOTE]
> 在首次启动 Visual Studio，您必须选择一个预定义的设置集合。 每个预定义的集合旨在符合特定的开发风格，并确定窗口布局、 编辑器行为、 IntelliSense 代码段和对话框选项。 此实验中的过程描述了完成给定的任务在 Visual Studio 中使用时所需的操作**常规开发设置**集合。 如果您为您的开发环境选择不同的设置集合，可能会中应考虑到的步骤有所不同。


<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>练习 1： 使用 Entity Framework 迁移

当正在开发的应用时，你的数据模型可能随时间变化。 （如果要创建新的版本），这些更改可能会影响你的数据库中的现有模型，必须使数据库保持最新的以防止出现错误。

若要简化您的模型，这些更改跟踪**Entity Framework Code First 迁移**会自动检测更改比较您的模型与数据库架构并生成特定的代码来更新您的数据库，创建新*版本*的数据库。

此练习展示如何能够**迁移**你的应用程序以及如何可以轻松地检测和生成更改来更新您的数据库。

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>任务 1 – 启用迁移

在此任务中，您将了解到启用的步骤**Entity Framework Code First 迁移**到**极客测验**数据库更改的模型和了解如何将这些更改反映在数据库。

1. 打开 Visual Studio 并打开**GeekQuiz.sln**解决方案文件从**Source\Ex1 UsingEntityFrameworkMigrations\Begin**。
2. 生成解决方案，若要下载和安装**NuGet**包的依赖关系。 若要执行此操作，右键单击解决方案，然后单击**生成解决方案**或按**Ctrl + Shift + B**。
3. 从**工具**在 Visual Studio 中，选择菜单**库程序包管理器**，然后单击**程序包管理器控制台**。
4. 在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。 将创建基于现有模型的初始迁移。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![启用迁移](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "启用迁移")

    *启用迁移*

    > [!NOTE]
    > 此命令将添加**迁移**文件夹，对包含文件的极客测验项目名为**Configuration.cs**。 **配置**类允许您配置的迁移对于您的上下文的行为方式。
5. 你需要使用已启用迁移，更新**配置**类，以使用初始数据填充数据库的**极客测验**要求。 下**迁移**，替换**Configuration.cs**与文件位于**Source\Assets**本实验的文件夹。

    > [!NOTE]
    > 由于**迁移**将调用**种子**与每个数据库更新方法，您需要以确保在数据库中的用户不能重复记录。 **AddOrUpdate**方法将有助于防止重复的数据。
6. 若要添加初始迁移，输入以下命令，然后按**Enter**。

    > [!NOTE]
    > 请确保没有名为数据库&quot;GeekQuizProd&quot; LocalDB 实例中。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![添加基础架构迁移](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "添加基础架构迁移")

    *添加基础架构迁移*

    > [!NOTE]
    > **添加迁移**将基于之后创建的最后一个迁移对您的模型所做的更改下一步迁移搭建基架。 在这种情况下，由于它是项目的初始迁移时，它将添加用于创建中定义的所有表的脚本**TriviaContext**类。
7. 执行迁移后，通过运行以下命令来更新数据库。 此命令将指定**Verbose**标志以查看要应用到目标数据库的 SQL 语句。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![创建初始数据库](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "创建初始数据库")

    *创建初始数据库*

    > [!NOTE]
    > **更新数据库**应用所有挂起的迁移到数据库。 在这种情况下，它将创建使用 web.config 文件中定义的连接字符串的数据库。
8. 转到**视图**菜单，然后打开**SQL Server 对象资源管理器**。

    ![在 SQL Server 对象资源管理器中打开](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "在 SQL Server 对象资源管理器中打开")

    *在 SQL Server 对象资源管理器中打开*
9. 在中**SQL Server 对象资源管理器**窗口中，右键单击连接到 LocalDB 实例**SQL Server**节点并选择**添加 SQL Server...** 选项。

    ![添加 SQL Server 实例](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "添加 SQL Server 实例")

    *将 SQL Server 实例添加到 SQL Server 对象资源管理器*
10. 设置**服务器名称**到 *(localdb) \v11.0*并保留**Windows 身份验证**作为身份验证模式。 单击**Connect**以继续。

    ![连接到 LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "连接到 LocalDB")

    *连接到 LocalDB*
11. 打开**GeekQuizProd**数据库中，展开**表**节点。 正如您所看到的**Update-database**命令生成中定义的所有表**TriviaContext**类。 找到**dbo。TriviaQuestions**表，然后打开列节点。 将在下一任务中，将新列添加到此表并更新数据库使用**迁移**。

    ![琐碎内容问题列](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "琐碎内容问题列")

    *琐碎内容问题列*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>任务 2 – 使用迁移更新数据库架构

在本任务中，您将使用**Entity Framework Code First 迁移**检测您的模型中的更改并生成所需的代码来更新数据库。 你将更新**TriviaQuestions**通过向其添加一个新的属性的实体。 然后，将运行命令以创建新的迁移在表中包含的新列。

1. 在中**解决方案资源管理器**，双击**TriviaQuestion.cs**文件位于内部**模型**文件夹。
2. 添加名为的新属性**提示**，如以下代码片段中所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. 在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。 将专用于反映将我们的模型中的更改创建新的迁移。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![添加迁移](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "添加迁移")

    *添加迁移*

    > [!NOTE]
    > 迁移文件组成的两种方法**向上**并**向下**。
    > 
    > - **向上**方法将用于指定哪些更改我们的应用程序需要将应用于数据库的当前版本。
    > - **向下**用于撤消所做的更改我们已添加到**向上**方法。
    > 
    > 当数据库迁移更新数据库时，将所有迁移都运行中的时间戳顺序，且只有自上次更新以来未使用过 (\_跟踪已应用哪些迁移的 MigrationHistory 表)。 **向上**所有迁移的方法将调用，并将使我们具有指定数据库的更改。 如果返回到先前的迁移，我们决定**向下**将调用方法以重做以反向顺序进行更改。
4. 在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. 输出**Update-database**生成命令**Alter Table** SQL 语句，以添加到一个新列**TriviaQuestions**表，如下图中所示。

    ![添加列生成的 SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "添加列生成的 SQL 语句")

    *添加列生成的 SQL 语句*
6. 在中**SQL Server 对象资源管理器**，刷新**dbo。TriviaQuestions**表，以检查新**提示**显示列。

    ![显示新的提示列](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "显示新的提示列")

    *显示新的提示列*
7. 回到**TriviaQuestion.cs**编辑器中，添加**StringLength**约束*提示*属性，如下面的代码段中所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. 在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. 在中**程序包管理器控制台**，输入以下命令，然后按**Enter**。

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. 输出**Update-database**生成命令**Alter Table** SQL 语句，以更新*提示*类型的列**TriviaQuestions**表，如下图中所示。

    ![更改列生成的 SQL 语句](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 语句生成")

    *更改列生成的 SQL 语句*
11. 在中**SQL Server 对象资源管理器**，刷新**dbo。TriviaQuestions**表，然后检查**提示**列的类型**nvarchar(150)**。

    ![显示新约束](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "显示新约束")

    *显示新约束*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>练习 2： 将 Web 应用部署到过渡环境

**Azure 应用服务中的 web 应用**使您可以执行分阶段的发布。 过渡的发布创建的每个默认生产站点过渡站点槽，便于你以交换这些槽，但无需停机时间。 这是非常适用于向公众发布之前验证更改，以增量方式集成站点内容，并回滚任何更改都不会按预期工作。

在此练习中，你将部署**极客测验**应用程序到 web 应用使用 Git 源代码管理的过渡环境。 若要执行此操作，将创建 web 应用和预配在管理门户所需的组件，配置**Git**的源存储库和推送应用程序代码从本地计算机到过渡槽。 你还将更新与生产数据库**Code First 迁移**你在上一练习中创建。 然后，您将在此测试环境以验证其操作中执行应用程序。 后它按预期正常工作，将升级到生产环境的应用程序。

> [!NOTE]
> 若要启用暂存的发布，web 应用必须处于**标准模式**。 请注意是否你的 web 应用更改为标准模式将产生额外的费用。 有关定价的详细信息，请参阅[应用服务定价](https://azure.microsoft.com/pricing/details/app-service/)。


<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>任务 1 – 在 Azure 应用服务中创建 Web 应用

在本任务中，您将创建中的 web 应用**Azure 应用服务**从管理门户。 你还将配置**SQL 数据库**以持久保存应用程序数据，并配置本地 Git 存储库进行源代码管理。

1. 转到[Azure 管理门户](https://manage.windowsazure.com)并使用与你的订阅关联的 Microsoft 帐户登录。

    ![登录到 Azure 管理门户](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *登录到 Azure 管理门户*
2. 单击**新建**在页面底部的命令栏中。

    ![创建新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "创建新的 web 应用")

    *创建新的 web 应用*
3. 单击**计算**，**网站**，然后**自定义创建**。

    ![创建新的 web 应用使用自定义创建](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "创建使用自定义创建新的 web 应用")

    *创建使用自定义创建新的 web 应用*
4. 在中**新建网站-自定义创建**对话框框中，提供一个可用**URL** (例如*极客测验*)，选择中的某个位置**区域**下拉列表，然后选择**创建新的 SQL 数据库**中**数据库**下拉列表。 最后，选择**从源控制发布**复选框，然后单击**下一步**。

    ![自定义新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *自定义新的 web 应用*
5. 指定数据库设置的以下信息：

   - 在中**名称**文字框中，输入数据库名称 (例如*geekquiz\_db*)
   - 在服务器中**下拉**列表中，选择**新建 SQL 数据库服务器**。 或者，可以选择现有的服务器。
   - 在中**数据库用户名**并**数据库密码**框中，SQL 数据库服务器输入管理员用户名和密码。 如果选择一个服务器已创建，系统将提示输入密码。

     ![指定数据库设置](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *指定数据库设置*
6. 单击 **“下一步”** 以继续。
7. 选择**本地 Git 存储库**源控件使用，并单击**下一步**。

    > [!NOTE]
    > 您可能会提示输入部署凭据 （用户名和密码）。

    ![创建 Git 存储库](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *创建 Git 存储库*
8. 等待，直到创建新的 web 应用。

    > [!NOTE]
    > 默认情况下，Azure 提供在域*azurewebsites.net*但还可以设置自定义域使用 Azure 管理门户的可能性。 但是，如果您使用的某些 Azure 应用服务模式下，仅可以管理自定义域。
    > 
    > Azure 应用服务有免费、 共享、 基本、 标准和高级版本。 在免费和共享模式下，所有 web 应用在多租户环境中运行，并针对 CPU、 内存和网络使用情况采用的配额。 免费的应用程序的最大数目可能会因你的计划。 在标准模式下，您可以选择到标准 Azure 相对应的专用虚拟机上运行的应用的计算资源。 您可以发现中的 web 应用模式下配置**规模**web 应用的菜单。
    > 
    > ![Azure 应用服务模式](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure 应用服务模式")
    > 
    > 如果使用的**共享**或**标准**模式下，你将能够通过转到您的应用程序管理 web 应用的自定义域**配置**菜单，然后单击**管理域**下*域名*。
    > 
    > ![管理域](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "管理域")
    > 
    > ![管理自定义域](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "管理自定义域")
9. 创建 web 应用后，单击下面的链接**URL**列来检查新的 web 应用正在运行。

    ![浏览到新的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *浏览到新的 web 应用*

    ![运行 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *运行 web 应用*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>任务 2 – 创建生产 SQL 数据库

在本任务中，您将使用**Entity Framework Code First 迁移**若要创建的数据库目标**Azure SQL 数据库**你在上一任务中创建的实例。

1. 在管理门户中，导航到上一个任务中创建的 web 应用并转到其**仪表板**。
2. 在中**仪表板**页上，单击**查看连接字符串**下链接**速览**部分。

    ![查看连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "查看连接字符串")

    *查看连接字符串*
3. 复制**连接字符串**值，并关闭对话框。

    ![在 Azure 管理门户中的连接字符串](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 管理门户中的连接字符串")

    *在 Azure 管理门户中的连接字符串*
4. 单击**SQL 数据库**若要查看在 Azure 中的 SQL 数据库的列表

    ![SQL 数据库菜单](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL 数据库菜单")

    *SQL 数据库菜单*
5. 找到在上一任务中创建的数据库并单击该服务器。

    ![SQL 数据库服务器](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL 数据库服务器")

    *SQL 数据库服务器*
6. 在中**快速启动**页上的服务器上，单击**配置**。

    ![配置菜单](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "配置菜单")

    *配置菜单*
7. 在中**允许的 IP 地址**部分中，单击**将添加到允许的 IP 地址**链接，以启用你的 IP 连接到 SQL 数据库服务器。

    ![允许的 IP 地址](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "允许的 IP 地址")

    *允许的 IP 地址*
8. 单击**保存**要完成该步骤的页的底部。
9. 切换回 Visual Studio。
10. 在中**程序包管理器控制台**，执行以下命令替换 *[YOUR CONNECTION STRING]* 占位符替换为从 Azure 复制连接字符串

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![针对 Windows Azure SQL 数据库更新数据库](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "面向 Windows Azure SQL 数据库更新数据库")

    *更新目标 Azure SQL 数据库的数据库*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>任务 3 – 部署到过渡环境使用 Git 的极客测验

在本任务中，将 web 应用程序中启用过渡的发布。 然后，将使用 Git 发布极客测验应用程序直接从本地计算机到你的 web 应用的过渡环境。

1. 返回到门户并单击下的 web 应用名称**名称**列中显示的管理页。

    ![打开 web 应用程序管理页面](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *打开 web 应用程序管理页面*
2. 导航到**规模**页。 下**常规**部分中，选择**标准**作为配置，然后单击**保存**命令栏中。

    > [!NOTE]
    > 若要在当前区域和订阅中的运行的所有 web 应用**标准**模式下，保留**全**中所选的复选框**选择站点**配置。 否则，请清除**全**复选框。

    ![升级到标准模式的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "升级到标准模式的 web 应用")

    *升级到标准模式的 Web 应用*
3. 单击**是**以确认所做的更改。

    ![确认更改为标准模式](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "继续执行更改的 web 应用程序模式")

    *确认更改为标准模式*
4. 转到**仪表板**页上，单击**启用过渡发布**下**速览**部分。

    ![启用过渡的发布](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "启用过渡发布")

    *启用过渡的发布*
5. 单击**是**才能启用过渡的发布。

    ![确认过渡发布](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "单击是以启用暂存的发布")

    *确认过渡的发布*
6. 在 web 应用程序的列表中，展开左侧的 web 应用的名称以显示过渡站点槽的标记。 它具有的应用，然后在 web 应用名称 ***（过渡）***。 单击以转到管理页面的临时站点。

    ![导航到过渡 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "导航到过渡 web 应用")

    *导航到过渡应用*
7. 请注意，他管理页面看起来像任何其他 web 应用程序的管理页面。 导航到**部署**页并复制**Git URL**值。 稍后在本练习中，将使用它。

    ![复制 Git URL 值](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *复制 Git URL 值*
8. 打开一个新**Git Bash**控制台并执行以下命令。 更新 *[您的应用程序的路径]* 占位符替换为路径**GeekQuiz**解决方案中，位于**Source\Ex1 DeployingWebSiteToStaging\Begin**文件夹此实验室中。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 初始化和第一次提交](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 初始化和第一次提交*
9. 运行以下命令以将你的 web 应用推送到远程**Git**存储库。 将占位符替换为从管理门户获取的 URL。 系统会提示输入部署密码。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![将推送到 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *将推送到 Azure*

    > [!NOTE]
    > 当将内容部署到的 FTP 主机或 GIT 存储库的 web 应用时，您必须使用进行身份验证**部署凭据**创建的 web 应用**快速启动**或**仪表板**管理页。 如果不知道你的部署凭据，可以轻松地重置它们使用管理门户。 打开 web 应用**仪表板**页上，单击**重置部署凭据**链接。 提供新密码，然后单击**确定**。 部署凭据可用于与你的订阅相关联的所有 web 应用。
10. 若要验证 web 应用已成功推送到 Azure，请返回到管理门户并单击**网站**。
11. 找到你的 web 应用并展开以显示过渡站点槽的条目。 单击其**名称**转到管理页。
12. 单击**部署**若要查看**部署历史记录**。 验证是否有**活动的部署**与你*&quot;初始提交&quot;*。

    ![活动部署](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *活动部署*
13. 最后，单击**浏览**以转到 web 应用的命令栏中。

    ![浏览 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *浏览 web 应用*
14. 如果已成功部署应用程序，您将看到的极客测验登录页。

    > [!NOTE]
    > 部署的应用程序的地址 URL 包含后跟 web 应用的名称 *-暂存*。

    ![在过渡环境中运行的应用程序](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *在过渡环境中运行的应用程序*
15. 如果你想要浏览应用程序，请单击**注册**注册一个新用户。 通过输入用户名、 电子邮件地址和密码来填写帐户详细信息。 接下来，该应用程序显示测验的第一个问题。 回答几个问题，请确保按预期工作。

    ![应用程序可供使用](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *应用程序可供使用*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>任务 4 – 将提升到生产 Web 应用

现在，已验证 web 应用在过渡环境中正常运行，你现可提升到生产环境。 在此任务中，将交换过渡站点槽与生产站点槽。

1. 返回到管理门户并选择过渡站点槽。 单击**交换**命令栏中。

    ![切换到生产环境](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *切换到生产环境*
2. 单击**是**在确认对话框中，若要继续进行交换操作。 Azure 会立即交换的暂存站点内容的生产站点内容。

    > [!NOTE]
    > 某些设置从暂存版本将自动复制到生产版本 （例如连接字符串替代、 处理程序映射等），但其他设置将不会更改 （例如 DNS 终结点、 SSL 绑定等）。

    ![确认交换操作](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *确认交换操作*
3. 交换完成后，选择生产槽，然后单击**浏览**命令栏中打开生产站点中。 请注意地址栏中的 URL。

    > [!NOTE]
    > 您可能需要刷新浏览器以清除缓存。 在 Internet Explorer 中，您可以执行此操作通过按**CTRL + R**。

    ![在生产环境中运行的 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. 在中**GitBash**控制台中，更新本地 Git 存储库的远程 URL 以面向生产槽。 若要执行此操作，运行以下命令将占位符替换为部署用户名和 web 应用的名称。

    > [!NOTE]
    > 在以下练习中，会将更改推送到生产站点，而不是过渡环境，实验室起见。 在实际方案中，建议以提升到生产环境之前验证在过渡环境中的更改。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>练习 3： 在生产环境中执行部署回滚

您不产生的过渡槽以热之间执行交换过渡和生产环境，例如，如果你正在使用的情况下**免费**或**共享**模式。 在这些情况下，你应测试应用程序在测试环境中 （本地或远程站点中） 部署到生产环境之前。 但是，有可能在测试阶段未检测到的问题可能会出现在生产站点中。 在这种情况下，务必要有一种机制来轻松地尽可能快地切换到上一个和更稳定版本的应用程序。

在中**Azure 应用服务**，从源代码管理的连续部署功能可使此可能要归功于**重新部署**管理门户中提供的操作。 Azure 跟踪与推送到存储库的提交相关联的部署，并提供了一个选项以重新部署在任何时间使用任何以前部署的应用程序。

在此练习中将执行中的代码的更改**极客测验**有意注入的应用程序*bug*。 将部署到生产应用程序，以查看错误，，然后您将利用重新部署功能，请返回到以前的状态。

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>任务 1 – 极客测验应用程序更新

在此任务中，将重构代码的一小段**TriviaController**类提取到一个新的方法从数据库中检索所选的测验选项的逻辑的一部分。

1. 切换到包含 Visual Studio 实例**GeekQuiz**从上一练习的解决方案。
2. 在中**解决方案资源管理器**，打开**TriviaController.cs**文件**控制器**文件夹。
3. 找到**StoreAsync**方法，然后选择下图中突出显示的代码。

    ![选择的代码](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *选择的代码*
4. 右键单击所选的代码中，展开**重构**菜单，然后选择**提取方法...**.

    ![作为新方法提取代码](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *选择提取方法*
5. 在中**提取方法**对话框中，名称的新方法*MatchesOption*然后单击**确定**。

    ![指定方法名称](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *指定提取的方法的名称*
6. 所选的代码然后提取到**MatchesOption**方法。 生成的代码如以下代码片段所示。

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. 按**CTRL + S**以保存所做的更改。

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>任务 2 – 重新部署极客测验应用程序

现在将推送到存储库，这将触发新部署到生产环境前一个任务中所做的更改。 然后，您将使用诊断的故障问题**F12 开发工具**提供的 Internet Explorer，然后执行回滚到以前的部署从 Azure 管理门户。

1. 打开一个新**Git Bash**控制台部署到 Azure 应用服务更新的应用程序。
2. 执行以下命令以将所做的更改推送到 Azure。 更新 *[您的应用程序的路径]* 占位符替换为路径**GeekQuiz**解决方案。 系统会提示输入部署密码。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![将重构的代码推送到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *将重构的代码推送到 Azure*
3. 打开 Internet Explorer 并导航到你的 web 应用 (例如`http://<your-web-site>.azurewebsites.net`)。 使用前面创建的凭据登录。
4. 按**F12**若要启动的开发工具，选择**网络**选项卡，单击**播放**按钮开始录制。

    ![启动网络录制](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "启动网络录制")

    *启动网络录制*
5. 选择任何选项测验。 你将看到没有任何反应。
6. 在中**F12**窗口中，与 POST HTTP 请求对应的条目显示了 HTTP **500**结果。

    ![HTTP 500 错误](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 错误*
7. 选择**控制台**选项卡。可能的原因的详细信息记录错误。

    ![记录的错误](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *记录的错误*
8. 找到错误的详细信息部分。 很明显，重构您的上一步骤中提交的代码导致此错误。

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`。
9. 不要关闭浏览器。
10. 在新浏览器实例中，导航到[Azure 管理门户](https://manage.windowsazure.com)并使用与你的订阅关联的 Microsoft 帐户登录。
11. 选择**网站**单击在练习 2 中创建的 web 应用。
12. 导航到**部署**页。 请注意，所有提交都执行部署历史记录中列出。

    ![现有部署的列表](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *现有部署的列表*
13. 选择上一个提交，然后单击**重新部署**命令栏上。

    ![重新部署以前的提交](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *重新部署以前的提交*
14. 当系统提示你确认，单击**是**。

    ![确认重新部署](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. 部署完成后，切换回浏览器实例与您的 web 应用和按**CTRL + F5**。
16. 单击任一选项。 翻转动画现在需要的位置并将结果 (*正确/错误*) 将显示。
17. （可选）切换到**Git Bash**控制台并执行以下命令，以恢复到上一个提交。

    > [!NOTE]
    > 这些命令创建新的提交，撤消中 Git 存储库中的错误提交所做的所有更改。 然后，azure 将重新部署应用程序使用新的提交。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>练习 4： 使用 Azure 存储进行缩放

**Blob**是最简单的方式来存储大量非结构化的文本或二进制数据，例如视频、 音频和图像。 移动应用程序以存储静态内容，可通过直接向浏览器提供图像或文档中缩放应用程序。

在此练习中，将移动到 Blob 容器的应用程序的静态内容。 然后将配置应用程序以添加**ASP.NET URL 重写规则**中**Web.config**重定向到 Blob 容器的内容。

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>任务 1 – 创建一个 Azure 存储帐户

在此任务中，您将学习如何创建新的存储帐户使用管理门户。

1. 导航到[Azure 管理门户](https://manage.windowsazure.com)并使用与你的订阅关联的 Microsoft 帐户登录。
2. 选择**新 |数据服务 |存储 |快速创建**开始创建新的存储帐户。 输入该帐户，然后选择的唯一名称**区域**从列表中。 单击**创建存储帐户**以继续。

    ![创建新的存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "创建新的存储帐户")

    *创建新的存储帐户*
3. 在中**存储**部分中，等到新存储帐户的状态更改为*联机*才能继续执行以下步骤。

    ![创建存储帐户](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "创建存储帐户")

    *创建存储帐户*
4. 单击存储帐户名称，然后单击**仪表板**在页面顶部的链接。 **仪表板**页为您提供的帐户，而且可以在你的应用程序中使用的服务终结点的状态信息。

    ![显示存储帐户仪表板](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "显示存储帐户仪表板")

    *显示存储帐户仪表板*
5. 单击**管理访问密钥**导航栏中的按钮。

    ![管理访问密钥按钮](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "管理访问密钥按钮")

    *管理访问密钥按钮*
6. 在中**管理访问密钥**对话框中，复制**存储帐户名称**并**主访问密钥**因为你将在以下练习中需要它们。 然后，关闭对话框。

    ![管理访问密钥对话框](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "管理访问密钥对话框")

    *管理访问密钥对话框*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>任务 2 – 将资产上传到 Azure Blob 存储

在此任务中，将使用从 Visual Studio 服务器资源管理器窗口连接到你的存储帐户。 然后，将创建 blob 容器，并将具有极客测验徽标的文件上传到容器。

1. 切换到包含 Visual Studio 实例**GeekQuiz**从上一练习的解决方案。
2. 从菜单栏中，选择**视图**，然后单击**服务器资源管理器**。
3. 在中**服务器资源管理器**，右键单击**Azure**节点，然后选择**连接到 Azure...**.使用与你的订阅关联的 Microsoft 帐户登录。

    ![连接到 Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *连接到 Azure*
4. 展开**Azure**节点，右键单击**存储**，然后选择**附加外部存储...**.
5. 在中**添加新的存储帐户**对话框框中，输入**帐户名称**并**帐户密钥**获取在上一任务和单击**确定**.

    ![新的存储帐户添加对话框](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *新的存储帐户添加对话框*
6. 应显示你的存储帐户**存储**节点。 展开你的存储帐户中，右键单击**Blob** ，然后选择**创建 Blob 容器...**.

    ![创建 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "创建 Blob 容器")

    *创建 Blob 容器*
7. 在中**创建 Blob 容器**对话框中，输入 blob 容器的名称，单击**确定**。

    ![创建 Blob 容器对话框](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "创建 Blob 容器对话框")

    *创建 Blob 容器对话框的*
8. 新的 blob 容器应添加到**Blob**节点。 更改容器中的访问权限，以使容器公开。 若要执行此操作，右键单击**映像**容器，然后选择**属性**。

    ![映像容器属性](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "映像容器属性")

    *图像容器属性*
9. 在中**属性**窗口中，将**公共读取访问权限**到**容器**。

    ![更改公共读取访问权限属性](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "更改公共读取访问权限属性")

    *更改公共读取访问权限属性*
10. 当系统提示你是否确实要更改的公共访问权限属性，请单击**是**。

    ![Microsoft Visual Studio 警告](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 警告")

    *Microsoft Visual Studio 警告*
11. 在中**服务器资源管理器**，右键单击**映像**blob 容器，然后选择**查看 Blob 容器**。

    ![查看 Blob 容器](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "查看 Blob 容器")

    *查看 Blob 容器*
12. 图像容器应在新窗口中打开，并应显示图例没有项。 单击**上传**图标以将文件上传到 blob 容器。

    ![没有任何项的图像容器](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "没有任何项的图像容器")

    *没有任何项的图像容器*
13. 在中**上传 Blob**对话框框中，导航到**资产**实验室的文件夹。 选择**徽标 big.png**文件，并单击**打开**。
14. 等待，直到上传文件。 上传完成后，应在图像容器中列出该文件。 右键单击文件条目，然后选择**复制 URL**。

    ![复制 blob URL](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "复制 blob 文件 URL")

    *复制 blob URL*
15. 打开 Internet Explorer 并粘贴该 URL。 下图应在浏览器中所示。

    ![徽标 big.png 图像从 Windows Blob 存储](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "徽标 big.png 图像从存储")

    *从 Azure Blob 存储的徽标 big.png 图像*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>任务 3 – 正在更新解决方案来使用从 Azure Blob 存储的静态内容

在本任务中，您将配置**GeekQuiz**解决方案，以使用该映像上传到 Azure Blob 存储 （而不是位于 web 应用中的映像） 通过添加在 ASP.NET URL 重写规则**web.config**文件。

1. 在 Visual Studio 中打开**Web.config**文件内**GeekQuiz**项目，然后找到**&lt;system.webServer&gt;** 元素。
2. 添加以下代码以添加一个 URL 重写规则，更新存储帐户名称的占位符。

    (代码段- *WebSitesInProduction-Ex4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 重写是侦听传入 Web 请求并将请求重定向到不同的资源的过程。 URL 重写规则可以使一个请求时需要重定向，并应它们在其中重定向，重写的引擎。 重写规则两个字符串组成： 要在所请求 URL 中查找的模式 （通常情况下，使用正则表达式），并找到要替换的模式，如果该字符串。 有关详细信息，请参阅[在 ASP.NET 中 URL 重写](https://msdn.microsoft.com/library/ms972974.aspx)。
3. 按**CTRL + S**以保存所做的更改。
4. 打开一个新**Git Bash**控制台部署到 Azure 应用服务更新的应用程序。
5. 执行以下命令以将所做的更改推送到 Azure。 更新 *[您的应用程序的路径]* 占位符替换为路径**GeekQuiz**解决方案。 系统会提示输入部署密码。

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![将更新部署到 Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *将更新部署到 Azure*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>任务 4 – 验证

在此任务将使用**Internet Explorer**若要浏览**极客测验**应用程序并检查 URL 重写规则映像有效并且你将重定向到上托管的映像**Azure Blob存储**。

1. 打开 Internet Explorer 并导航到你的 web 应用 (例如`http://<your-web-site>.azurewebsites.net`)。 使用前面创建的凭据登录。

    ![显示与映像极客测验 web 应用](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "显示与映像极客测验 web 应用")

    *显示与映像极客测验 web 应用*
2. 按**F12**若要启动的开发工具，选择**网络**选项卡上，并开始记录。

    ![启动网络录制](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "启动网络录制")

    *启动网络录制*
3. 按**CTRL + F5**刷新 web 页面。
4. 页面完成加载后，应看到的 HTTP 请求 **/img/logo-big.png**的 HTTP URL **301**结果 （重定向） 和另一个请求`http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png`URL 的 HTTP **200**结果。

    ![验证 URL 重定向](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "显示开发人员工具中的重定向")

    *验证 URL 重定向*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>练习 5： 使用自动缩放 Web 应用

> [!NOTE]
> 本练习中是可选的因为它需要支持的 Web 负载&amp;性能测试，仅可用于**Visual Studio 2013 Ultimate Edition**。 有关特定 Visual Studio 2013 功能的详细信息，比较版本[此处](https://www.microsoft.com/visualstudio/eng/products/compare)。


**Azure 应用服务 Web 应用**提供的自动缩放功能的 web 应用中运行**标准模式**。 自动缩放可以让 Azure 自动缩放根据负载 web 应用的实例计数。 启用自动缩放后，Azure 一次每 5 分钟检查 web 应用的 CPU，并根据需要在某个时间点添加实例。 如果 CPU 使用率较低，Azure 将删除实例一次每隔两小时以确保你的 web 应用的性能不会降低。

在此练习中您将了解到配置所需的步骤**自动缩放**的功能**极客测验**web 应用。 通过运行 Visual Studio 负载测试，以生成足够的 CPU 负载在要触发实例升级的应用程序，你将验证此功能。

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>任务 1 – 根据 CPU 指标配置自动缩放

在此任务将使用 Azure 管理门户来启用您在练习 2 中创建的 web 应用的自动缩放功能。

1. 在中[Azure 管理门户](https://manage.windowsazure.com/)，选择**网站**单击在练习 2 中创建的 web 应用。
2. 导航到**规模**页。 下**容量**部分中，选择**CPU**有关**按度量值缩放**配置。

    > [!NOTE]
    > 时通过 CPU 进行缩放，Azure 会动态调整应用程序使用的 CPU 使用率更改的实例数。

    ![选择按 CPU 进行缩放](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "选择的 CPU 指标的自动缩放")

    *选择按 CPU 进行缩放*
3. 更改**目标 CPU**配置到**20**-**40** %。

    > [!NOTE]
    > 此范围表示你的 web 应用的平均 CPU 使用率。 Azure 将添加或删除实例以使您的 web 应用程序保持在此范围内。 中指定最小值和最大缩放所用的实例数**实例计数**配置。 Azure 将永远不会高于或超过该限制。
    > 
    > 默认值**目标 CPU**只是为了本实验的目的而修改的值。 通过使用小的值配置 CPU 范围，你将要在中等负载放置在应用程序时增加触发自动缩放的可能性。

    ![更改目标必须介于 20 和 40%的 CPU](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "更改要介于 20 到 40%的目标 CPU")

    *更改目标 CPU 必须介于 20 和 40%*
4. 单击**保存**以保存所做的更改的命令栏中。

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>任务 2 – 通过 Visual Studio 负载测试

既然**自动缩放**已配置，您将创建**Web 性能和负载测试项目**在 Visual Studio 生成 web 应用上的一些 CPU 负载。

1. 打开**Visual Studio Ultimate 2013** ，然后选择**文件 |新 |项目...** 启动一个新的解决方案。

    ![创建新的项目](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "创建新的项目")

    *创建新的项目*
2. 在中**新的项目**对话框中，选择**Web 性能和负载测试项目**下**Visual C# |测试**选项卡。请确保 **.NET Framework 4.5**已选中，将项目命名*WebAndLoadTestProject*，选择**位置**然后单击**确定**。

    ![创建新的 Web 和负载测试项目](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "创建新的 Web 和负载测试项目")

    *创建新的 Web 和负载测试项目*
3. 在中**WebTest1.webtest**右键单击**WebTest1**节点，然后单击**添加请求**。

    ![将请求添加到 WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "将请求添加到 WebTest1")

    *将请求添加到 WebTest1*
4. 在中**属性**窗口中的新的请求节点中，更新**Url**属性以指向你的 web 应用的 URL (例如*[ http://geek-quiz.azurewebsites.net/ ](http://geek-quiz.azurewebsites.net/)*).

    ![更改 Url 属性](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "更改 Url 属性")

    *更改 Url 属性*
5. 在中**WebTest1.webtest**窗口中，右键单击**WebTest1**单击**添加循环...**.

    ![将循环添加到 WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "向 WebTest1 中添加循环")

    *向 WebTest1 中添加循环*
6. 在中**向循环添加条件规则和项**对话框中，选择**For 循环**规则，并修改以下属性。

   1. **终止值：** 1000年
   2. **上下文参数名称：** 迭代器
   3. **增量值：** 1

      ![选中该 For 循环规则，更新的属性](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "选中该 For 循环规则，更新属性")

      *选中该 For 循环规则，更新属性*
7. 下**循环中的项**部分中，选择你之前创建为 for 循环的第一个和最后一个项的请求。 单击“确定”  继续。

    ![选择循环的第一个和最后一项](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "选择循环的第一个和最后一个项")

    *选择循环的第一个和最后一个项*
8. 在中**解决方案资源管理器**，右键单击**WebAndLoadTestProject**项目中，展开**添加**菜单，然后选择**负载测试...**.

    ![将负载测试添加到 WebAndLoadTestProject 项目](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "将负载测试添加到 WebAndLoadTestProject 项目")

    *将负载测试添加到 WebAndLoadTestProject 项目*
9. 在中**新建负载测试向导**对话框中，单击**下一步**。

    ![新建负载测试向导](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "新建负载测试向导")

    *新建负载测试向导*
10. 在中**方案**页上，选择**不使用思考时间**然后单击**下一步**。

    ![选择不应使用思考时间](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "选择不应使用思考时间")

    *选择不使用思考时间*
11. 在中**负载模式**页上，请确保**常量负载**选择选项。 更改**用户计数**将设置为**250**用户，然后单击**下一步**。

    ![更改的用户计数为 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "为 250 更改的用户计数")

    *更改的用户计数为 250*
12. 在中**测试组合模型**页上，选择**基于顺序测试顺序**然后单击**下一步**。

    ![选择测试组合模型](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "选择测试组合模型")

    *选择测试组合模型*
13. 在中**测试组合模型**页上，单击**添加...** 添加到组合的测试。

    ![将测试添加到测试组合](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "将测试添加到测试组合")

    *将测试添加到测试组合*
14. 在中**添加测试**对话框中，双击**WebTest1**若要添加到测试**选定的测试**列表。 单击“确定”  继续。

    ![添加 WebTest1 测试](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "添加 WebTest1 测试")

    *添加 WebTest1 测试*
15. 回到**测试组合**页上，单击**下一步**。

    ![完成测试组合页](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "完成测试组合页")

    *完成测试组合页*
16. 在中**网络组合**页上，单击**下一步**。

    ![单击网络组合页中的下一个](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "接下来在网络组合页上单击")

    *单击网络组合页中的下一步*
17. 在中**浏览器组合**页上，选择**Internet Explorer 10.0**作为浏览器类型，然后单击**下一步**。

    ![选择浏览器类型](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "选择浏览器类型")

    *选择浏览器类型*
18. 在中**计数器集**页上，单击**下一步**。

    ![在计数器集页中单击下一步](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "单击下一步中计数器集页")

    *在计数器集页中单击下一步*
19. 在中**运行设置**页上，将**负载测试持续时间**到**5 分钟**然后单击**完成**。

    ![将负载测试持续时间设置为 5 分钟](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "将负载测试持续时间设置为 5 分钟")

    *将负载测试持续时间设置为 5 分钟*
20. 在中**解决方案资源管理器**，双击**Local.settings**要探索测试设置文件。 默认情况下，Visual Studio 使用本地计算机以运行测试。

    > [!NOTE]
    > 或者，您可以将测试项目配置为运行在云中使用负载测试**Visual Studio Online (VSO)**。 VSO 提供基于云的负载测试模拟实际负载的服务，避免本地环境约束，例如 CPU 容量、 可用内存和网络带宽。 有关使用 VSO 运行负载测试的详细信息，请参阅[这篇文章](https://www.visualstudio.com/get-started/load-test-your-app-vs)。

    ![测试设置](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>任务 3 – 自动缩放验证

现在将执行你在上一任务中创建负载测试，请参阅你的 web 应用在负载下的行为方式。

1. 在中**解决方案资源管理器**，双击**LoadTest1.loadtest**以打开负载测试。

    ![打开 LoadTest1.loadtest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "打开 LoadTest1.loadtest")

    *打开 LoadTest1.loadtest*
2. 在中**LoadTest1.loadtest**窗口中，单击工具箱以运行负载测试中的第一个按钮。

    ![运行负载测试](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "运行负载测试")

    *运行负载测试*
3. 等待，直到负载测试完成。

    > [!NOTE]
    > 负载测试模拟多个用户同时将请求发送到 web 应用。 当运行测试时，可以监视可用的计数器以检测任何错误、 警告或与你的负载测试运行相关的其他信息。

    ![负载测试运行](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "等待，直到完成加载测试")

    *负载测试运行*
4. 完成测试后，请返回到管理门户并导航到**规模**web 应用的页面。 下**容量**部分中，您应在图形中看到已自动部署的新实例。

    ![自动部署的新实例](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *自动部署的新实例*

    > [!NOTE]
    > 它可能需要几分钟时间才会显示在图中的更改 (按**CTRL + F5**定期以刷新页面)。 如果没有看到任何更改，可以尝试以下：
    > 
    > - 增加的负载测试的持续时间 (例如**10 分钟**)
    > - 减少的最大和最小值**目标 CPU**范围中的 web 应用自动缩放配置
    > - 在云中运行负载测试**Visual Studio Online**。 详细信息[此处](https://www.visualstudio.com/get-started/load-test-your-app-vs.aspx)

* * *

<a id="Summary"></a>
## <a name="summary"></a>总结

在本动手实验，您学习了如何设置和应用程序部署到 Azure 中的生产 web 应用。 通过检测并更新数据库启动**Entity Framework Code First 迁移**，然后继续通过部署新版本的站点使用**Git**和执行回滚到你的站点的最新稳定版本。 此外，您学习了如何缩放应用程序使用存储将静态内容移动到 Blob 容器。
