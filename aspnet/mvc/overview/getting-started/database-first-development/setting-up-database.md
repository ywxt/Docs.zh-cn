---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 开始使用 Entity Framework 6 Database First 通过 MVC 5 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
ms.date: 10/01/2014
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: 20e590ad1b3a59f93d1ba48a2564ddc1a5cbb315
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37836115"
---
<a name="getting-started-with-entity-framework-6-database-first-using-mvc-5"></a>使用 Entity Framework 6 Database First 通过 MVC 5 入门
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。 生成的代码对应于数据库表中的列。 在本系列的最后部分，会将站点和数据库部署到 Azure。
> 
> 本系列的此部分主要介绍在创建数据库和使用数据填充。
> 
> 这一系列已用的发布内容写入 Tom Dykstra 和 Rick Anderson。 它改进了基于注释部分中的用户的反馈。


## <a name="introduction"></a>介绍

本主题说明如何开始使用现有数据库并快速创建 web 应用程序，使用户能够与数据交互。 它使用 Entity Framework 6 和 MVC 5 构建 web 应用程序。 ASP.NET 基架功能可以自动生成用于显示、 更新、 创建和删除数据的代码。 使用 Visual Studio 中的发布工具，你可以轻松部署站点和数据库到 Azure。

本主题介绍这种情况，如果有数据库并且想要为 web 应用程序根据该数据库的字段生成代码。 这种方法称为数据库优先开发。 如果你还没有现有数据库，则可以改用方法称作 Code First 开发这涉及到定义数据类和类属性从生成数据库。

Code First 开发的介绍性示例，请参阅[Getting Started with ASP.NET MVC 5](../introduction/getting-started.md)。 有关更高级的示例，请参阅[为 ASP.NET MVC 4 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

选择要使用的实体框架方法的指导，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。

## <a name="prerequisites"></a>系统必备

Visual Studio 2013 或 Visual Studio Express 2013 for Web

## <a name="set-up-the-database"></a>将数据库设置

以模拟拥有现有的数据库的环境，你将首先使用一些预填充的数据，创建一个数据库，然后创建 web 应用程序连接到数据库。

本教程是使用 LocalDB 与 Visual Studio 2013 或 Visual Studio Express 2013 for Web 开发的。 您可以使用现有的数据库服务器，而不是 LocalDB，但具体取决于版本的 Visual Studio 和您的数据库的类型，所有 Visual Studio 中的数据工具可能不受支持。 如果这些工具不可用于你的数据库，您可能需要执行某些管理套件中的特定于数据库的步骤为你的数据库。

如果你的 Visual Studio 版本中有数据库工具的问题，请确保已安装的数据库工具的最新版本。 有关更新或安装数据库工具的信息，请参阅[Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027)。

启动 Visual Studio 并创建**SQL Server 数据库项目**。 将项目命名**ContosoUniversityData**。

![创建数据库项目](setting-up-database/_static/image1.png)

您现在有一个空数据库项目。 您将此数据库在部署到 Azure 以后本教程中，因此将需要将 Azure SQL Database 设置为项目的目标平台。 设置目标平台不实际部署该数据库。它只意味着数据库项目将验证数据库设计为与目标平台兼容。 若要设置目标平台，打开**属性**项目并选择**Microsoft Azure SQL 数据库**为目标平台。

![将目标平台设置](setting-up-database/_static/image2.png)

可以创建本教程中添加的定义的表的 SQL 脚本所需的表。 右键单击项目并添加新项。

![添加新项](setting-up-database/_static/image3.png)

添加名为学生的新表。

![添加 student 表](setting-up-database/_static/image4.png)

表文件中替换以下代码以创建表的 T-SQL 命令。

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

请注意，设计窗口会自动同步的代码。 您可以使用代码或设计器。

![显示代码和设计](setting-up-database/_static/image5.png)

添加另一个表。 这一次课程将其命名，并使用以下 T-SQL 命令。

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

然后，重复一次，以创建名为注册的表。

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

您可以在用数据填充数据库通过部署数据库后运行的脚本。 向项目添加后期部署脚本。 可以使用默认名称。

![添加后期部署脚本](setting-up-database/_static/image6.png)

将以下 T-SQL 代码添加到后期部署脚本。 此脚本只需将数据添加到数据库时找到没有匹配的记录。 不覆盖或删除您可能会输入到数据库的任何数据。

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

请务必注意每次部署您的数据库项目时，运行后期部署脚本。 因此，您需要编写此脚本时请仔细考虑您的要求。 在某些情况下，你可能想要从一组已知的数据开始，每次部署该项目。 在其他情况下，您可能不想要更改的现有数据以任何方式。 根据您的要求，可以决定是否需要后期部署脚本或需要在脚本中包括。 有关填充使用后期部署脚本在数据库的详细信息，请参阅[SQL Server 数据库项目中包括数据](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。

现在，您有 4 个 SQL 脚本文件不存在实际的表。 已准备好将您的数据库项目部署到 localdb。 在 Visual Studio 中，单击开始按钮 （或 F5） 以生成和部署数据库项目。 检查输出选项卡以验证成功的生成和部署。

![显示输出](setting-up-database/_static/image7.png)

若要查看已创建新数据库，请打开**SQL Server 对象资源管理器**并查找正确的本地数据库服务器中的项目的名称 (在这种情况下 **(localdb) \ProjectsV12**)。

![显示新的数据库](setting-up-database/_static/image8.png)

若要查看表中填充了数据，请右键单击某个表，并选择**查看数据**。

![显示表数据](setting-up-database/_static/image9.png)

显示表数据的可编辑视图。

![显示表数据的结果](setting-up-database/_static/image10.png)

现在设置和使用数据填充数据库。 在下一步的教程中，将创建数据库的 web 应用程序。

> [!div class="step-by-step"]
> [下一篇](creating-the-web-application.md)
