---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 检索和显示数据与模型绑定和 web 窗体 |Microsoft Docs
author: tfitzmac
description: 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定使数据交互...更多直接-
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: c04e4c94378c8143c919e83af90312dd003b8c84
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830852"
---
<a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a>检索和使用模型绑定和 web 窗体显示数据
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本系列教程演示了一个 ASP.NET Web 窗体项目中使用模型绑定的基本方面。 模型绑定可以更直接的比处理数据源对象 （如 ObjectDataSource 或 SqlDataSource） 的数据交互。 本系列开始介绍性材料，后续教程将移动到更高级的概念。
> 
> 模型绑定模式适用于任何数据访问技术。 在本教程中，将使用实体框架中，但您可以使用最熟悉的数据访问技术。 从数据绑定服务器控件，如 GridView、 ListView、 detailsview 和 FormView 控件，指定要用于选择、 更新、 删除和创建数据的方法的名称。 在本教程中，将 SelectMethod 为指定值。
> 
> 在该方法中，您提供用于检索数据的逻辑。 在下一步的教程中，将为 UpdateMethod、 DeleteMethod 和 InsertMethod 设置值。
> 
> 你可以[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整的项目 C# 或 vb。 可下载代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，为在本教程中所示的 Visual Studio 2013 模板稍有不同。
> 
> 在本教程在 Visual Studio 中运行应用程序。 您还可以让应用程序访问 Internet 上通过将其部署到托管提供商。 Microsoft 提供了免费的 web 宿主中的最多 10 个网站  
>  [Azure 免费试用帐户](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。 有关如何将 Visual Studio web 项目部署到 Azure 应用服务 Web 应用的信息，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)系列。 该教程还演示如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Azure SQL 数据库。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Microsoft Visual Studio 2013 或 Microsoft Visual Studio Express 2013 for Web
>   
> 
> 本教程还适用于 Visual Studio 2012，但将在用户界面和项目模板中的一些差异。


## <a name="what-youll-build"></a>你将生成

在本教程中，你将：

1. 生成与注册的课程的学生反映一所大学的数据对象
2. 生成从对象的数据库表
3. 使用测试数据填充数据库
4. 在 web 窗体中显示数据

## <a name="set-up-project"></a>设置项目

在 Visual Studio 2013 中，创建一个新**ASP.NET Web 应用程序**称为**ContosoUniversityModelBinding**。

![创建项目](retrieving-data/_static/image2.png)

选择 Web 窗体模板，并保留其他默认选项。 单击确定以设置项目。

![选择 web 窗体](retrieving-data/_static/image3.png)

首先，您将几个较小的更改以自定义该站点的外观。 打开**Site.Master**文件，并更改要包括 Contoso University 而不是我的 ASP.NET 应用程序的标题。

[!code-aspx[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

然后，将更改从标头文本**应用程序名称**到**Contoso University**。

[!code-aspx[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

此外在 Site.Master 中，更改以反映与此站点相关的页面的标头中显示的导航链接。 将不需要以下两者之一**有关**页或**联系人**页，以便可以删除这些链接。 相反，您将需要调用一个页面的链接**学生**。 尚未创建此页。

[!code-aspx[Main](retrieving-data/samples/sample3.aspx)]

保存并关闭 Site.Master。

现在，你将创建 web 窗体，用于显示学生数据。 右键单击项目，并**外****新项**。 选择**包含母版页的 Web 窗体**模板，并将其命名**Students.aspx**。

![创建页](retrieving-data/_static/image5.png)

选择**Site.Master**作为新 web 窗体的母版页。

## <a name="create-the-data-models-and-database"></a>创建数据模型和数据库

Code First 迁移将用于创建对象和相应的数据库表。 这些表将存储有关学生和他们的课程的信息。

在 Models 文件夹中，添加一个名为的新类**UniversityModels.cs**。

![创建模型类](retrieving-data/_static/image7.png)

在此文件中，定义 SchoolContext、 学生、 登记和 Course 类，如下所示：

[!code-csharp[Main](retrieving-data/samples/sample4.cs)]

SchoolContext 类派生自 DbContext，管理数据库连接和数据中的更改。

在学生类中，请注意，已应用于的特性**FirstName**， **LastName**，并**年**属性。 这些属性将用于本教程中的数据验证。 若要简化此演示项目的代码，只对这些属性都是使用数据验证特性标记。 在实际项目中，会将验证特性应用到需要验证的数据，如注册和 Course 类中的属性的所有属性。

保存 UniversityModels.cs。

将使用 Code First 迁移的工具来设置基于这些类上的数据库。

在中**程序包管理器控制台**，运行命令：  
`enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

如果命令成功完成将收到一条消息表明已启用迁移，

![启用迁移](retrieving-data/_static/image8.png)

请注意，新文件命名为**Configuration.cs**已创建。 在 Visual Studio 中，在创建后将自动打开此文件。 配置类包含**种子**方法使你以预填充数据库表中的使用测试数据。

将以下代码添加到 Seed 方法。 将需要添加**使用**语句**ContosoUniversityModelBinding.Models**命名空间。

[!code-csharp[Main](retrieving-data/samples/sample5.cs)]

保存 Configuration.cs。

在包管理器控制台中，运行命令`add-migration initial`。

然后，运行命令`update-database`。

如果运行此命令时收到异常，，就可以 StudentID 和 CourseID 的值具有各种从 Seed 方法中的值。 在数据库中打开这些表，并查找 StudentID 和 CourseID 现有值。 在种子设定注册表的代码中添加这些值。

已添加的数据库文件，但它当前项目中处于隐藏状态。 单击**显示所有文件**以显示该文件。

![显示所有文件](retrieving-data/_static/image10.png)

请注意，.mdf 文件现在将显示在应用\_数据文件夹。

![数据库文件](retrieving-data/_static/image12.png)

双击.mdf 文件，打开服务器资源管理器。 现在，表存在，并使用数据填充。

![数据库表](retrieving-data/_static/image14.png)

## <a name="display-data-from-students-and-related-tables"></a>显示学生和相关的表中的数据

与数据库中的数据，您现在可以以检索该数据并将其显示在网页中。 将使用**GridView**控件以显示行和列中的数据。

打开 Students.aspx，并找到**MainContent**占位符。 该占位符，在添加**GridView**包括下面的代码的控制。

[!code-aspx[Main](retrieving-data/samples/sample6.aspx)]

有几个在此标记代码中为您要注意的重要概念。 首先，请注意，用于将设置为值**SelectMethod** GridView 元素中的属性。 此值指定用于检索数据的 GridView 方法的名称。 您将在下一步中创建此方法。 其次，注意**ItemType**属性设置为前面创建的 Student 类。 通过设置此值，您可以参考该标记的代码中的类的属性。 例如，学生类包含名为注册的集合。 可以使用**Item.Enrollments**来检索该集合，并使用 LINQ 语法来检索每个学生的已注册的信用额度的总和。

在代码隐藏文件中，您需要添加为指定的方法**SelectMethod**值。 打开**Students.aspx.cs**，并添加**使用**语句**ContosoUniversityModelBinding.Models**和**System.Data.Entity**命名空间。

[!code-csharp[Main](retrieving-data/samples/sample7.cs)]

然后，添加以下方法。 请注意，此方法的名称与为 SelectMethod 提供的名称相匹配。

[!code-csharp[Main](retrieving-data/samples/sample8.cs)]

**Include**子句可以提高此查询的性能，但不是必需的查询工作。 Include 子句中，不会使用延迟加载后，这涉及到将发送到数据库的单独查询每个与时间相关的检索数据检索的数据。 通过提供的 Include 子句，使用预先加载，这意味着通过单个数据库的查询检索的所有相关数据检索的数据。 在大多数相关数据的不是情况下使用的预先加载可能效率较低，因为检索更多的数据。 但是，在这种情况下，预先加载提供最佳性能由于针对每条记录显示相关的数据。

了解有关加载时的性能注意事项的详细信息相关的数据，请参阅以下节**延迟、 预先和显式加载相关数据的**中[使用实体框架在 ASP 中读取相关数据.NET MVC 应用程序](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)主题。

默认情况下，数据按标记为键属性的值。 可以添加一个 OrderBy 子句，以指定不同的值进行排序。 在此示例中，默认 StudentID 属性用于排序。 在中[排序、 分页和筛选数据](sorting-paging-and-filtering-data.md)主题中，将使用户能够选择列进行排序。

运行 web 应用程序，并导航到学生页。 学生页上显示以下学生信息。

![显示数据](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a>自动生成的模型绑定方法

学习本系列教程中，当您可以只需复制代码从本教程到你的项目。 但是，此方法的一个缺点是功能的，您可能会意识到的 Visual Studio 以自动生成的模型绑定方法代码提供。 您自己的项目上工作时，自动代码生成可以节省时间并获得如何实现的操作的某种意义上的帮助。 本部分介绍自动代码生成功能。 本部分只是信息性并不包含任何您需要在项目中实现的代码。

设置的值时**SelectMethod**， **UpdateMethod**， **InsertMethod**，或者**DeleteMethod**标记代码中的属性可以选择**创建新方法**选项。

![创建新的方法](retrieving-data/_static/image18.png)

Visual Studio 不仅具有正确签名的代码隐藏中创建一个方法，而且还会生成实现代码，以帮助您执行该操作。 如果首次设置**ItemType**属性前使用自动代码生成功能生成的代码将使用该类型的操作。 例如，设置 UpdateMethod 属性时，会自动生成以下代码：

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

同样，上面的代码不需要添加到你的项目。 在下一步的教程中，将实现用于更新、 删除和添加新数据的方法。

## <a name="conclusion"></a>结束语

在本教程中，将创建数据模型类，并基于这些类生成数据库。 使用测试数据填充数据库表。 模型绑定用于从数据库检索数据，然后在 GridView 中显示数据。

在接下来[教程](updating-deleting-and-creating-data.md)在本系列中，将启用更新、 删除和创建数据。

> [!div class="step-by-step"]
> [下一篇](updating-deleting-and-creating-data.md)
