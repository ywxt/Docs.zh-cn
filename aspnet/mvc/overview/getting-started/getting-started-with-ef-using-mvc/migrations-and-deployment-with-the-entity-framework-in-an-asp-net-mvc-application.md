---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: 代码优先迁移和部署使用实体框架中的 ASP.NET MVC 应用程序 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 的 ASP.NET MVC 5 应用程序...
ms.author: aspnetcontent
ms.date: 11/07/2014
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 7c7092b770231b26fd666786af2e202acd70bc8a
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838681"
---
<a name="code-first-migrations-and-deployment-with-the-entity-framework-in-an-aspnet-mvc-application"></a>代码优先迁移和部署使用实体框架中的 ASP.NET MVC 应用程序
====================
通过[Tom Dykstra](https://github.com/tdykstra)

[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)或[下载 PDF](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20Entity%20Framework%206%20Code%20First%20using%20MVC%205.pdf)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 6 Code First 和 Visual Studio 2013 的 ASP.NET MVC 5 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

到目前为止该应用程序已经运行本地 IIS Express 中在开发计算机上。 若要使实际的应用程序可供其他人通过 Internet 使用，必须将其部署到 web 宿主提供程序。 在本教程中，你将部署到 Azure 中云 Contoso 大学应用程序。

本教程包含以下部分：

- 启用 Code First 迁移。 迁移功能，可更改数据模型并将其部署到生产环境所做的更改，通过更新数据库架构，而无需删除并重新创建数据库。
- 将部署到 Azure。 此步骤是可选的;无部署项目的情况下，可以继续剩余的教程。

我们建议使用持续集成过程使用源代码管理进行部署，但本教程不会介绍这些主题。 有关详细信息，请参阅[源代码管理](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)并[持续集成](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)章[使用 Azure 构建实际云应用](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)电子书。

## <a name="enable-code-first-migrations"></a>启用 Code First 迁移

开发新应用程序时，数据模型会频繁更改。每当模型更改时，模型都无法与数据库保持同步。 你已配置实体框架会自动删除并重新创建每次更改数据模型的数据库。 当添加、 删除或更改实体类或更改你`DbContext`类，在下次运行应用程序时自动删除您现有的数据库，创建一个新的匹配该模型，并使用测试数据为其设定种子。

这种使数据库与数据模型保持同步的方法适用于多种情况，但将应用程序部署到生产环境的情况除外。 当在生产环境中运行应用程序时，它通常会存储你想要保留，并且不想丢失所有每次进行一次更改如添加新列的数据。 [Code First 迁移](https://msdn.microsoft.com/data/jj591621)功能可解决此问题，通过启用 Code First 来更新数据库架构而不是删除并重新创建数据库。 在本教程中，你将部署该应用程序，并准备为此，将启用迁移。

1. 禁用之前设置通过注释掉或删除的初始值设定项`contexts`元素添加到应用程序 Web.config 文件。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. 在应用程序中还*Web.config*文件中，将连接字符串中的数据库的名称更改为 ContosoUniversity2。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    此更改将设置项目，以便初始迁移创建新的数据库。 这不是必需，但稍后您将看到它是一个不错的主意的原因。
3. 从**工具**菜单上，单击**库程序包管理器**，然后**程序包管理器控制台**。

    ![Selecting_Package_Manager_Console](https://asp.net/media/4336350/1pm.png)
4. 在`PM>`提示符处输入以下命令：

    `enable-migrations`  
    `add-migration InitialCreate`

    ![enable-migrations 命令](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

    `enable-migrations`命令创建*迁移*文件夹中的 ContosoUniversity 项目中，在该文件夹中放入*Configuration.cs*可编辑以配置 Migrations 的文件。

    (如果你错过了前面的步骤，指示您要更改数据库名称，迁移将查找现有数据库并自动执行`add-migration`命令。 这是确定，它只意味着在部署数据库之前，不会运行一次测试迁移代码。 在运行时，更高版本`update-database`命令不会发生因为数据库已存在。)

    ![Migrations 文件夹](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    如您在前面，看到的初始值设定项类`Configuration`类包括`Seed`方法。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    目的[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法是，可以插入或更新后 Code First 创建或更新数据库测试数据。 创建数据库和每次更新数据库架构时，数据模型更改后调用方法。

### <a name="set-up-the-seed-method"></a>设置种子方法

当你删除并重新创建每个数据模型更改的数据库，使用初始值设定项类的`Seed`方法插入测试数据，因为该数据库删除每个模型更改后，将所有测试数据会丢失。 使用 Code First 迁移，数据库发生更改后保留数据的测试，因此包括中的测试数据[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法通常不是必需。 事实上，您不希望`Seed`方法插入测试数据，如果您将使用迁移来将数据库部署到生产环境，因为`Seed`方法将在生产环境中运行。 在这种情况下你想`Seed`方法插入到数据库所需的数据在生产环境中。 例如，可能想要包括在实际系名称的数据库`Department`表应用程序变得可用在生产环境中时。

对于本教程，你将在使用迁移部署，但你`Seed`方法将是否仍要插入测试数据，以使其更轻松地了解应用程序功能而无需手动插入大量数据的工作原理。

1. 内容替换为*Configuration.cs*文件使用以下代码，将测试数据加载到新数据库。 

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法采用数据库上下文对象作为输入参数，并在方法中的代码使用该对象来将新实体添加到数据库。 对于每个实体类型，代码创建新实体的集合，将它们添加到适当[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)属性，然后单击保存到数据库的更改。 但并不需要调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)后的实体的每个组的方法，正如在这里，但这样做可帮助您找到问题的根源，如果向数据库写入代码时出现异常。

    某些插入数据的语句使用[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法来执行"upsert"操作。 因为`Seed`方法运行每次执行`update-database`命令时，通常每个迁移后，您不能只是插入数据，因为你尝试添加的行已存在后将创建数据库的初始迁移。 "Upsert"操作可以防止当你尝试插入的行已存在，但它将会发生的错误***重写***对测试应用程序时可能已做的数据的任何更改。 使用测试数据的某些表中您可能不希望发生这种情况： 在某些情况下测试时更改数据时所需数据库更新后保留所做的更改。 在这种情况下想要执行条件插入操作： 插入行，仅当它尚不存在。 Seed 方法使用这两种方法。

    第一个参数传递给[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法指定要用于检查行是否已存在的属性。 提供的，测试学生数据`LastName`属性可用于此目的，因为每个列表中的最后一个名称是唯一的：

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    此代码假定最后一个名称唯一。 如果你手动添加的学生使用重复的最后一个名称，将得到以下异常执行迁移的下一个时间。

    序列包含多个元素

    有关如何处理冗余数据，例如名为"Alexander Carson"的两个学生的信息，请参阅[种子设定和调试 Entity Framework (EF) 数据库](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx)Rick Anderson 的博客上。 有关详细信息`AddOrUpdate`方法，请参阅[负责使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)Julie Lerman 的博客上。

    创建的代码`Enrollment`实体假定你已`ID`中的实体中的值`students`集合，但未在创建集合的代码中设置该属性。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    可以使用`ID`此处属性因为`ID`值设置在调用时`SaveChanges`为`students`集合。 EF 会自动获取的主键值时它将实体插入到数据库，而它更新`ID`在内存中的实体的属性。

    将每个添加的代码`Enrollment`到实体`Enrollments`实体集不使用`AddOrUpdate`方法。 它检查实体是否已存在并插入该实体，如果不存在。 此方法将会保留对注册级通过使用应用程序 UI 所做的更改。 此代码循环访问的每个成员`Enrollment`[列表](https://msdn.microsoft.com/library/6sh2ey19.aspx)，如果在数据库中找不到注册，它将注册添加到数据库。 第一次更新数据库，数据库将为空，因此它会将添加每个注册。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]
2. 生成项目。

### <a name="execute-the-first-migration"></a>执行第一次迁移

当您执行`add-migration`命令时，迁移生成的代码，将从头开始创建数据库。 此代码也是在*迁移*文件夹中，在名为的文件*&lt;时间戳&gt;\_InitialCreate.cs*。 `Up`方法`InitialCreate`类创建与数据模型实体集相对应的数据库表和`Down`方法中删除它们。

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

迁移调用 `Up` 方法为迁移实现数据模型更改。 输入用于回退更新的命令时，迁移调用 `Down` 方法。

这是你输入时创建的初始迁移`add-migration InitialCreate`命令。 参数 (`InitialCreate`在示例中) 用于文件命名，可以是任何所需内容; 通常选择的单词或短语汇总了迁移做什么。 例如，你可能会命名为更高版本迁移&quot;AddDepartmentTable&quot;。

如果创建初始迁移时已存在数据库，则会生成数据库创建代码，但此代码不必运行，因为数据库已与数据库模型相匹配。 将应用部署到其中尚不存在数据库的其他环境时，此代码将运行以创建数据库，因此最好提前进行测试。 这也是提前更改连接字符串中数据库的名称的原因，这样迁移才能从头创建新数据库。

1. 在中**程序包管理器控制台**窗口中，输入以下命令：

    `update-database`

    ![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    `update-database`命令将运行`Up`方法来创建数据库，然后将它运行`Seed`方法来填充该数据库。 相同的过程将自动运行在生产环境中部署应用程序之后, 您将看到以下部分中。
2. 使用**服务器资源管理器**一样在第一个教程中，检查数据库并运行应用程序以验证一切仍然正常相同像以前一样。

## <a name="deploy-to-azure"></a>部署到 Azure

到目前为止该应用程序已经运行本地 IIS Express 中在开发计算机上。 若要使其可供其他人通过 Internet 使用，必须将其部署到 web 宿主提供程序。 在本教程的本部分会将其部署到 Azure。 本部分是可选的;您可以跳过此，请继续学习以下教程中，也可以适应不同的宿主提供程序所选的本部分中说明。

### <a name="using-code-first-migrations-to-deploy-the-database"></a>使用 Code First 迁移部署数据库

若要部署的数据库将使用 Code First 迁移。 在创建发布配置文件，用于从 Visual Studio 部署的配置设置时，将选择一个复选框**更新数据库**。 此设置会导致部署过程会自动配置应用程序*Web.config*文件在目标服务器上，以便使用 Code First`MigrateDatabaseToLatestVersion`初始值设定项类。

Visual Studio 不会执行任何操作与数据库在部署过程中时它正在将项目复制到目标服务器。 当运行已部署应用程序时，它会在部署后首次访问数据库时，Code First 检查数据库是否与数据模型匹配。 如果不匹配，Code First 自动创建数据库 （如果尚不存在） 或 （如果数据库存在，但与模型不匹配） 到最新版本更新数据库架构。 如果应用程序实现迁移`Seed`方法，方法运行后创建的数据库或更新的模式。

迁移`Seed`方法插入测试数据。 如果在部署到生产环境，您将必须更改`Seed`方法，使其仅插入想要插入到您的生产数据库的数据。 例如，在当前数据模型中可能想要开发数据库中具有真实的课程，但虚构的学生。 您可以编写`Seed`方法负载皆在开发中，并在部署到生产环境之前然后注释虚构的学生。 也可以编写`Seed`方法加载仅课程，并通过使用应用程序的 UI 手动测试数据库中输入虚构的学生。

### <a name="get-an-azure-account"></a>获取 Azure 帐户

你将需要一个 Azure 帐户。 如果还没有一个，但你有 Visual Studio 订阅，可以[激活您的订阅权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。 否则，可以只需几分钟内创建一个免费试用帐户。 有关详细信息，请参阅[Azure 免费试用版](https://azure.microsoft.com/free/)。

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>在 Azure 中创建网站和 SQL 数据库

Azure 中的 web 应用将在共享宿主环境，这意味着它在运行与其他 Azure 客户端共享的虚拟机 (Vm) 上运行。 共享宿主环境是开始在云中低成本方法。 更高版本，如果你的 web 流量的增加，应用程序可以缩放以满足的需求的专用 Vm 上运行。 若要了解 Azure 应用服务定价选项的详细信息，请阅读的文档上[Azure Docs](https://azure.microsoft.com/pricing/details/app-service/)

会将数据库部署到 Azure SQL 数据库。 SQL 数据库是基于 SQL Server 技术构建的基于云的关系数据库服务。 工具和适用于 SQL Server 的应用程序还可用于 SQL 数据库。

1. 在中[Azure 管理门户](https://portal.azure.com)，单击**新建**左侧选项卡中，单击**查看所有**在新边栏选项卡，然后单击**Web 应用和 SQL**中**Web**部分中，最后**创建**。

    ![管理门户中的新按钮](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/CreateWeb-Sql.png)

   **新的 Web 应用和 SQL-创建**向导随即打开。

2. 在边栏选项卡中，输入中的字符串**应用名称**框，以用作你的应用程序的唯一 URL。 完整的 URL 将包含你在此处输入的以及 Azure 应用服务的默认域的 (。 azurewebsites.net)。 如果**应用名称**已被使用，该向导将通知你这些带有红色*应用程序名称不可用*消息。 如果**应用名称**是可用，你将获得一个绿色复选标记。

    ![使用管理门户中的数据库链接创建](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Create-WebApp.png)

3. 在中**订阅**下拉列表中，请选择要在其中的 Azure 订阅**应用服务**驻留。

4. 在中**资源组**文本框中，选择一个资源组或新建一个。 此设置指定你的网站将运行在哪个数据中心。 有关资源组的详细信息，请继续阅读文档[Azure Docs](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)。
5. 创建一个新**应用服务计划**通过单击*应用服务部分*，**新建**，然后填写**应用服务计划**（可以是相同的名称应用服务中），**位置**，并**定价层**（没有可用的选项）。

    ![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Create-AppService.png)
6. 单击**SQL 数据库**，然后选择*创建新*或选择现有的数据库

    ![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Create-Database.png)

7. 在中**名称**框中，输入你的数据库的名称。
8. 单击**目标服务器**框中，选择**创建新的服务器**。 或者，如果你之前创建一个服务器，您可以从可用服务器列表中选择该服务器。
9. 选择**定价层**部分中，选择*免费*。 如果需要更多资源，数据库可以纵向扩展在任何时间。 若要了解有关 Azure SQL 定价的详细信息，请阅读的文档上[Azure Docs](https://azure.microsoft.com/pricing/details/sql-database/)。
10. 修改[排序规则](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support)根据需要。
11. 输入管理员**SQL 管理员用户名**并**SQL 管理员密码**。 如果所选**新的 SQL 数据库服务器**，不要输入现有名称和密码在此处，应输入新名称和密码，你现在定义以后访问数据库时使用。 如果你选择之前创建的服务器，您将为该服务器输入凭据。
12. 可以为应用服务中使用 Application Insights 启用遥测数据收集。 使用小配置的 application Insights 收集有价值的事件、 异常、 依赖项、 请求和跟踪信息。 若要了解有关 Application Insights 的详细信息，开始[Azure Docs](https://azure.microsoft.com/services/application-insights/)。
13. 单击**创建**底部的边栏选项卡，以指示你已完成。
  
    管理门户返回到仪表板页上，并**通知**边栏选项卡页的顶部显示正在创建网站。 （通常不到一分钟），一段时间后将部署是否成功的通知。 在左侧导航栏中的新**应用服务**将出现在*应用服务*部分和新**SQL 数据库**将出现在*SQL 数据库*部分。

### <a name="deploy-the-application-to-azure"></a>部署到 Azure 应用程序

1. 在 Visual Studio 中，右键单击该项目中的**解决方案资源管理器**，然后选择**发布**从上下文菜单。
  
    ![在项目上下文菜单中发布](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)
2. 在中**配置文件**选项卡**发布 Web**向导中，单击**Microsoft Azure 应用服务**。
  
    ![导入发布设置](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-ChooseTarget.png)
3. 如果之前未添加你的 Azure 订阅在 Visual Studio 中，在屏幕上执行步骤。 以下步骤启用 Visual Studio 以连接到 Azure 订阅这样的一系列**应用服务**将包括您的网站。
 
4. 选择**订阅**应用服务添加到，然后**应用服务计划**你的应用服务是的一部分的文件夹和最后**应用服务**本身后跟**确定**。

    ![选择应用服务](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-AppService.png)
5. 配置配置文件后，**连接**将显示选项卡。 单击**验证连接**以确保设置正确无误

    ![验证连接](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Connection.png)
6. 当已验证的连接时，旁边会出现一个绿色复选标记**验证连接**按钮。 单击 **“下一步”**。
  
    ![已成功验证的连接](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-SettingsValidated.png)
7. 打开**远程连接字符串**下拉列表下的**SchoolContext** ，然后选择你创建的数据库的连接字符串。
8. 选择**更新数据库**。

    ![设置选项卡](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Settings.png)

    此设置会导致部署过程会自动配置应用程序*Web.config*文件在目标服务器上，以便使用 Code First`MigrateDatabaseToLatestVersion`初始值设定项类。
9. 单击 **“下一步”**。
10. 在中**预览版**选项卡上，单击**开始预览**。
  
    ![在预览选项卡中的开始预览按钮](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Preview.png)
  
    该选项卡显示将复制到服务器的文件的列表。 显示预览不需要发布应用程序，但是需要注意的一个有用的函数。 在这种情况下，不需要使用显示的文件列表执行任何操作。 下一次部署此应用程序，只有已更改的文件会出现在此列表中。
    ![开始预览文件输出](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-PreviewLoaded.png)

11. 单击“发布” 。
    Visual Studio 开始执行将文件复制到 Azure 服务器的过程。
12. **输出**窗口将显示已执行的部署操作并报告成功完成部署。
  
    ![报告部署成功的输出窗口](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-BuildOutput.png)
13. 成功完成部署后的默认浏览器会自动打开指向已部署的 web 站点的 URL。
    您创建的应用程序现在在云中运行。 
  
    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Publish-Site.png)

此时您*SchoolContext*已在 Azure SQL 数据库中创建了数据库因为所选**执行 Code First 迁移 （在应用启动时运行）**。 *Web.config*已部署的 web 站点中的文件已更改，以便[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项在运行第一次你的代码读取或写入数据库 （这种情况中的数据如果选择了**学生**选项卡):

![](https://asp.net/media/4367421/mig.png)

部署过程还创建了新的连接字符串 *(SchoolContext\_DatabasePublish*) 的代码优先迁移来更新数据库架构和数据库的种子设定使用。

![Database_Publish 连接字符串](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

您可以找到在计算机上的 Web.config 文件的已部署的版本*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*。您可以访问已部署*Web.config*文件本身通过使用 FTP。 有关说明，请参阅[使用 Visual Studio 的 ASP.NET Web 部署： 部署代码更新](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)。 按照说明开头的"若要使用 FTP 工具，需要以下三项： FTP URL、 用户名和密码。"

> [!NOTE]
> Web 应用不会实现安全性，以便找到 URL 的任何人可以更改的数据。 有关如何保护网站上的说明，请参阅[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 应用部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。 可以阻止其他人使用该站点，通过 Azure 管理门户或**服务器资源管理器**Visual Studio 可停止站点中。


![](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/Stop-Service.png)

## <a name="advanced-migrations-scenarios"></a>高级的迁移方案

如果根据本教程中显示自动运行迁移部署数据库和要部署到多个服务器运行的 web 站点，您可以获取多个服务器尝试在同一时间运行的迁移。 迁移是原子的因此，如果两个服务器尝试运行相同的迁移，其中一个将成功，并且另将失败 （假设不能两次执行的操作）。 在这种情况下如果您想要避免这些问题，可以手动调用迁移并设置自己的代码，使其只发生一次。 有关详细信息，请参阅[运行和代码从脚本迁移](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/)Rowan Miller 的博客上和[Migrate.exe](https://msdn.microsoft.com/data/jj618307) （适用于从命令行执行迁移） 在 MSDN 上。

有关其他迁移方案的信息，请参阅[迁移截屏视频系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。

## <a name="code-first-initializers"></a>代码的第一个初始值设定项

在部署部分中看到[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始值设定项正在使用。 代码首先还提供其他初始值设定项，包括[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) （默认值）， [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) （它使用前面部分） 和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。 `DropCreateAlways`初始值设定项也可用于设置单元测试的条件。 您还可以编写您自己初始值设定项，并且如果不想等待，直到应用程序从读取或写入数据库，您可以显式调用初始值设定项。 在 2013 年 11 月撰写本教程时您只能使用 Create 和 DropCreate 初始值设定项之前启用迁移。 实体框架团队正在努力使这些初始值设定项的迁移也可用。

有关初始值设定项的详细信息，请参阅[了解数据库初始值设定项中 Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)和一书的第 6 章[Programming Entity Framework: Code First](http://shop.oreilly.com/product/0636920022220.do)作者： Julie Lerman和 Rowan Miller。

## <a name="summary"></a>总结

在本教程中已了解如何启用迁移和部署应用程序。 在下一教程将开始通过展开数据模型来查看更高级的主题。

请在你喜欢本教程的内容，我们可以提高上留下反馈。 此外可以请求新主题[教我代码](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code)。

其他实体框架资源的链接可在[ASP.NET 数据访问-推荐的资源](xref:whitepapers/aspnet-data-access-content-map)。

> [!div class="step-by-step"]
> [上一页](xref:mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)
> [下一页](xref:mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application)
