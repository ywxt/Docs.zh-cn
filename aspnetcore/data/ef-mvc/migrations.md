---
title: "ASP.NET 核心 MVC 与 EF 核心-迁移-4 的 10"
author: tdykstra
description: "在本教程中，你开始使用 EF 核心迁移功能用于管理 ASP.NET 核心 MVC 应用程序中的数据模型更改。"
manager: wpickett
ms.author: tdykstra
ms.date: 03/15/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-mvc/migrations
ms.openlocfilehash: fd466af8a73bf4c568fafe7e7fdcaa82021624da
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="migrations---ef-core-with-aspnet-core-mvc-tutorial-4-of-10"></a>使用 EF Core 和 ASP.NET Core MVC 的迁移功能(4 / 10)



作者：[Tom Dykstra](https://github.com/tdykstra)和[Rick Anderson](https://twitter.com/RickAndMSFT)

Contoso 大学示例 web 应用程序演示如何使用 Entity Framework Core 和 Visual Studio 创建 ASP.NET Core MVC web 应用程序。 想要获取有关系列教程的信息，请参阅[第一个教程](intro.md)。

在本教程中，你会使用 EF Core 的迁移功能来管理数据模型的更改。 在之后的教程中，你将使用多个迁移来应对数据模型的更改。

## <a name="introduction-to-migrations"></a>迁移简介
当开发新应用程序的时候，需要频繁的更改数据模型，每次更改数据模型后，应用的数据模型会和数据库的数据模型不同步。通过之前的教程，已经学会了配置 Entity Framework 来创建一个不存在的数据库。之后每次更改数据模型——添加，删除或修改实体类或修改 DbContext 类，你都需要删除原有的数据库，然后使用 EF 的特性来创建一个新的和当前数据模型匹配的数据库，然后填充测试数据

这种保持数据库与数据模型匹配的方法在你将应用部署到生产环境之前简单实用。但一旦应用被部署到生产环境中，数据库通常保存着一些重要的数据，这些数据不能轻易删除，而且作为开发者也不愿意在每次向数据表添加一列新属性的情况下执行删表重建的操作。EF Core 的迁移功能能够很好的解决这个痛点。迁移功能能够使得 EF 更新数据库模式而不是创建一个全新的数据库。

## <a name="entity-framework-core-nuget-packages-for-migrations"></a>用于实现迁移功能的 Entity Framework Core NuGet 包

若要使用迁移，你可以使用**程序包管理器控制台**(PMC) 或命令行 (CLI)。  本教程介绍如何使用 CLI 命令。 有关 PMC 的信息位于[本教程末尾](#pmc)。

[Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) 中提供了适用于命令行接口 (CLI) 的 EF 工具。 若要安装此包，编辑*.csproj*文件中的`DotNetCliToolReference`将其添加到项目中，如下所示。 注意：必须通过编辑 .csproj 文件来安装此包；不能使用 `install-package` 命令或程序包管理器 GUI。 在**解决方案资源管理器**中右键单击项目名称并选择**编辑 ContosoUniversity.csproj**来编辑*.csproj*文件

[!code-xml[](intro/samples/cu/ContosoUniversity.csproj?range=12-15&highlight=2)]
  
（在此示例中的版本号为撰写本教程时最新的版本号。） 

## <a name="change-the-connection-string"></a>更改连接字符串

在*appsettings.json*文件，将连接字符串中数据库的名称更改为 ContosoUniversity2 或其他尚未使用的名称。

[!code-json[Main](intro/samples/cu/appsettings2.json?range=1-4)]

这项设置会使得项目在第一次迁移时创建一个新的数据库。 虽然实现迁移不需要新建一个新数据库，但之后你会理解这是一个不错的主意。

> [!NOTE]
> 作为选择，你也可以不改变数据库连接字符串而是删除数据库。 使用**SQL Server 对象资源管理器**(SSOX) 或`database drop`CLI 命令：
> ```console
> dotnet ef database drop
> ```
> 接下来会介绍如何执行 CLI 命令。

## <a name="create-an-initial-migration"></a>创建初始迁移

保存所做的更改并生成项目。 然后打开命令窗口并导航到项目文件夹。 下面是快速办法做到这一点：

* 在**解决方案资源管理器**，右键单击项目，然后选择**在文件资源管理器中打开**。

  ![在文件资源管理器菜单项中打开](migrations/_static/open-in-file-explorer.png)

* 在地址栏中输入"cmd"，然后按 Enter。

  ![打开命令窗口](migrations/_static/open-command-window.png)

在命令窗口中输入以下命令：

```console
dotnet ef migrations add InitialCreate
```

你看到类似命令窗口中的以下输出：

```console
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
Done. To undo this action, use 'ef migrations remove'
```

> [!NOTE]
> 如果你看到一条错误消息*No executable found matching command  dotnet-ef*，请参阅[这篇博客文章](http://thedatafarm.com/data-access/no-executable-found-matching-command-dotnet-ef/)以进行故障排除。

如果你看到一条错误消息"*cannot access the file ... ContosoUniversity.dll because it is being used by another process.*"，在 Windows 系统任务栏中，查找 IIS Express 图标并右键单击它，然后单击**ContosoUniversity > 停止站点**。

## <a name="examine-the-up-and-down-methods"></a>检查 Up 和 Down 方法

当执行`migrations add`命令时，EF 将生成创建数据库的代码。 此代码位于*Migrations*文件夹中，在名为*\<时间戳 > _InitialCreate.cs*的文件内。 `InitialCreate`类中的`Up`方法创建对应数据模型实体集的数据表，而`Down`方法删除对应的表，如下面的示例中所示。

[!code-csharp[Main](intro/samples/cu/Migrations/20170215220724_InitialCreate.cs?range=92-118)]

迁移通过调用`Up`方法来实现数据模型的更改。 当你输入命令回滚时，迁移调用`Down`方法。

当输入`migrations add InitialCreate`命令命令时，此代码被用于初始化迁移。迁移的 name 参数 (如在示例中的"InitialCreate") 仅仅用作文件名称，因而可以取任何名称。 最好选择能够概括迁移内容的单词或短语。 例如，你可能会将之后的迁移吗命名为"AddDepartmentTable"。

如果创建初始迁移时数据库已存在，依然会生成数据库创建代码但不会被运行，因为数据库已与数据模型相匹配。 当应用部署到另一个环境中，并且数据库不存在时，此代码将被执行并用于创建数据库，因此事先测试该方法是有必要的。 这就是为什么在之前更改了数据库连接字符串（测试从头开始创建数据库）。

## <a name="examine-the-data-model-snapshot"></a>检查数据模型快照

迁移还会对当前数据库模式创建*快照*，并保存在*Migrations/SchoolContextModelSnapshot.cs*中。 代码如下所示：

[!code-csharp[Main](intro/samples/cu/Migrations/SchoolContextModelSnapshot1.cs?name=snippet_Truncate)]

以代码表示当前的数据库模式， EF Core 不需要与数据库交互就能够创建迁移。当添加迁移时，EF 通过比较快照文件的数据模型确定更改的内容。 当数据库需要更新时，EF 才会与数据库交互。 

快照文件会和创建它的迁移保持同步，因此不能只删除名为*\<时间戳 > _\<migrationname >.cs*的文件来删除迁移。 如果你只删除该文件，剩余的迁移将与数据库快照文件不同步。 若要删除你最后添加的迁移，可以使用[dotnet ef migrations remove](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet#dotnet-ef-migrations-remove)命令。

## <a name="apply-the-migration-to-the-database"></a>对数据库应用迁移

在命令窗口中，输入以下命令创建数据库和表。

```console
dotnet ef database update
```

该命令的输出和`migrations add`命令的输出类似时，除此之外你还可以看到设置数据库的 SQL 命令的日志。 在下面的示例输出中，大部分日志被省略。 如果你不希望查看如此详细的日志消息，你可以修改*appsettings.Development.json*文件来更改日志级别。 有关详细信息，请参阅[日志记录简介](xref:fundamentals/logging)。

```text
info: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[0]
      User profile is available. Using 'C:\Users\username\AppData\Local\ASP.NET\DataProtection-Keys' as key repository and Windows DPAPI to encrypt keys at rest.
info: Microsoft.EntityFrameworkCore.Infrastructure[100403]
      Entity Framework Core 2.0.0-rtm-26452 initialized 'SchoolContext' using provider 'Microsoft.EntityFrameworkCore.SqlServer' with options: None
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (467ms) [Parameters=[], CommandType='Text', CommandTimeout='60']
      CREATE DATABASE [ContosoUniversity2];
info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (20ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      CREATE TABLE [__EFMigrationsHistory] (
          [MigrationId] nvarchar(150) NOT NULL,
          [ProductVersion] nvarchar(32) NOT NULL,
          CONSTRAINT [PK___EFMigrationsHistory] PRIMARY KEY ([MigrationId])
      );

<logs omitted for brevity>

info: Microsoft.EntityFrameworkCore.Database.Command[200101]
      Executed DbCommand (3ms) [Parameters=[], CommandType='Text', CommandTimeout='30']
      INSERT INTO [__EFMigrationsHistory] ([MigrationId], [ProductVersion])
      VALUES (N'20170816151242_InitialCreate', N'2.0.0-rtm-26452');
Done.
```

使用**SQL Server 对象资源管理器**检查数据库。  你会注意到 __EFMigrationsHistory 表，这张表用于跟踪已应用于数据库的迁移。 查看该表中的数据，你将看到第一次迁移的行。 （前面 CLI 输出的日志示例中演示了创建此行的 INSERT 语句。）

运行应用程序验证内容和之前相同。

![学生索引页](migrations/_static/students-index.png)

<a id="pmc"></a>
## <a name="command-line-interface-cli-vs-package-manager-console-pmc"></a>命令行界面 (CLI) vs. 程序包管理器控制台 (PMC)

管理迁移的 EF 工具可从.NET Core CLI 命令或从 Visual Studio **程序包管理器控制台**(PMC) 窗口中的 PowerShell cmdlet 中运行。 本教程演示如何使用 CLI，也可以根据自己的喜好使用 PMC。

PMC 命令中的 EF 命令在[Microsoft.EntityFrameworkCore.Tools](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools)包中。 此包已包含在[Microsoft.AspNetCore.All](xref:fundamentals/metapackage) 的包中，因此你不必安装它。

**重要说明：**这和通过编辑*.csproj*文件为 cli 安装的包不相同。 此包名以`Tools`结尾，与以`Tools.DotNet`结尾的 CLI 包名称不同。

有关 CLI 命令的详细信息，请参阅[.NET Core CLI](https://docs.microsoft.com/ef/core/miscellaneous/cli/dotnet)。 

有关 PMC 命令的详细信息，请参阅[Package Manager Console (Visual Studio)](https://docs.microsoft.com/ef/core/miscellaneous/cli/powershell)。

## <a name="summary"></a>总结

在本教程中，你已了解如何创建并应用迁移。 在下一个的教程中，将会开始通过扩展数据模型来学习更高级的主题。 此过程将创建并应用其他的迁移。

>[!div class="step-by-step"]
[上一页](sort-filter-page.md)
[下一页](complex-data-model.md)  
