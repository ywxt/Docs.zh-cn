---
title: 在 ASP.NET Core 中向 Razor 页面应用添加模型
author: rick-anderson
description: 了解如何使用 Entity Framework Core (EF Core) 添加用于管理数据库中的影片的类。
ms.author: riande
ms.date: 05/30/2018
uid: tutorials/razor-pages/model
ms.openlocfilehash: 5cd1e08ac52d352be23a280419d7456f685a03ad
ms.sourcegitcommit: 317f9be24db600499e79d25872d743af74bd86c0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48045596"
---
# <a name="add-a-model-to-a-razor-pages-app-in-aspnet-core"></a>在 ASP.NET Core 中向 Razor 页面应用添加模型

::: moniker range=">= aspnetcore-2.1"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a>添加数据模型

在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。 将文件夹命名为“Models”。

右键单击“Models”文件夹。 选择“添加” > “类”。 将该类命名为 Movie 并将 `Movie` 内容替换为以下代码：

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie21/Models/Movie1.cs?name=snippet)]

## <a name="scaffold-the-movie-model"></a>搭建“电影”模型的基架

在此部分，将搭建“电影”模型的基架。 确切地说，基架工具将生成页面，用于对“电影”模型执行创建、读取、更新和删除 (CRUD) 操作。

创建“Pages/Movies”文件夹：

* 在解决方案资源管理器中，右键单击“Pages”文件夹 >“添加”>“新建文件夹”。
* 将文件夹命名为“Movies”

在解决方案资源管理器中，右键单击“Pages/Movies”文件夹 >“添加”>“新搭建基架的项目”。

![上述说明的图像。](model/_static/sca.png)

在“添加基架”对话框中，选择“使用实体框架生成 Razor Pages (CRUD)”>“添加”。

![上述说明的图像。](model/_static/add_scaffold.png)

完成“使用实体框架(CRUD)添加 Razor Pages”对话框：

* 在“模型类”下拉列表中，选择“Movie (RazorPagesMovie.Models)。
* 在“数据上下文类”行中，选择 +（加号）并接受生成的名称“RazorPagesMovie.Models.RazorPagesMovieContext”。
* 在“数据上下文类”下拉列表中，选择“RazorPagesMovie.Models.RazorPagesMovieContext”
* 选择“添加”。

![上述说明的图像。](model/_static/arp.png)

搭建基架的过程会创建并更改以下文件：

### <a name="files-created"></a>创建的文件

* Pages/Movies：“创建”、“删除”、“详细信息”、“编辑”、“索引”。 将在下一教程中详细介绍这些页面。
* Data/RazorPagesMovieContext.cs

### <a name="file-updates"></a>文件更新

* Startup.cs：下一部分详细介绍对此文件所作的更改。
* appsettings.json：添加用于连接到本地数据的连接字符串。

## <a name="examine-the-context-registered-with-dependency-injection"></a>检查通过依赖关系注入注册的上下文

ASP.NET Core 通过[依赖关系注入](xref:fundamentals/dependency-injection)进行生成。 服务（例如 EF Core 数据库上下文）在应用程序启动期间通过依赖关系注入进行注册。 需要这些服务（如 Razor 页面）的组件通过构造函数提供相应服务。 本教程的后续部分介绍了用于获取 DB 上下文实例的构造函数代码。

基架工具自动创建 DB 上下文并将其注册到依赖关系注入容器。

检查 `Startup.ConfigureServices` 方法。 基架添加了突出显示的行：

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Startup.cs?name=snippet_ConfigureServices&highlight=12-13)]

数据库上下文类是为给定数据模型协调 EF Core 功能的主类。 数据上下文派生自 [Microsoft.EntityFrameworkCore.DbContext](/dotnet/api/microsoft.entityframeworkcore.dbcontext)。 数据上下文指定数据模型中包含哪些实体。 在此项目中将数据库上下文类命名为 `RazorPagesMovieContext`。

[!code-csharp[](razor-pages-start/sample/RazorPagesMovie21/Data/RazorPagesMovieContext.cs)]

前面的代码为实体集创建 [DbSet\<Movie>](/dotnet/api/microsoft.entityframeworkcore.dbset-1) 属性。 在实体框架术语中，实体集通常与数据表相对应。 实体对应表中的行。

通过调用 [DbContextOptions](/dotnet/api/microsoft.entityframeworkcore.dbcontextoptions) 对象中的一个方法将连接字符串名称传递到上下文。 进行本地开发时， [ASP.NET Core 配置系统](xref:fundamentals/configuration/index) 在 *appsettings.json* 文件中读取数据库连接字符串。

<a name="pmc"></a>
## <a name="perform-initial-migration"></a>添加初始迁移

在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：

* 添加初始迁移。
* 使用初始迁移来更新数据库。

从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

在 PMC 中，输入以下命令：

```PMC
Add-Migration Initial
Update-Database
```

或者，可在项目文件夹中使用以下 .NET Core CLI 命令：

```console
dotnet ef migrations add Initial
dotnet ef database update
```

忽略以下警告消息，后续教程将对此进行修复：

`Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'.*

`Add-Migration` 命令生成用于创建初始数据库架构的代码。 此架构的依据为 `RazorPagesMovieContext` 中指定的模型（在 Data/RazorPagesMovieContext.cs 文件中）。 `Initial` 参数用于为迁移命名。 可以使用任意名称，但是按照惯例应选择描述迁移的名称。 有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。

`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。

如果收到错误：

`SqlException: Cannot open database "RazorPagesMovieContext-GUID" requested by the login. The login failed.
Login failed for user 'User-name'.`

缺少[迁移步骤](#pmc)。

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[!INCLUDE [model1](~/includes/RP/model1.md)]

## <a name="add-a-data-model"></a>添加数据模型

在解决方案资源管理器中，右键单击“RazorPagesMovie”项目 >“添加” > “新建文件夹”。 将文件夹命名为“Models”。

右键单击“Models”文件夹。 选择“添加” > “类”。 将类命名为“Movie”，并添加以下属性：

[!INCLUDE [model 2](~/includes/RP/model2.md)]

<a name="cs"></a>
### <a name="add-a-database-connection-string"></a>添加数据库连接字符串

将连接字符串添加到 appsettings.json 文件。

[!code-json[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=8-10)]

<a name="reg"></a>
###  <a name="register-the-database-context"></a>注册数据库上下文

在 [Startup 类的 ConfigureServices 方法](xref:fundamentals/startup#the-startup-class) (Startup.cs) 中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=3-5,7-9)]

生成项目以验证有没有任何错误存在。

<a name="pmc"></a>
## <a name="add-scaffold-tooling-and-perform-initial-migration"></a>添加基架工具并执行初始迁移

在本部分中，使用程序包管理器控制台 (PMC) 执行以下操作：

* 添加 Visual Studio Web 代码生成包。 必须添加此包才能运行基架引擎。
* 添加初始迁移。
* 使用初始迁移来更新数据库。

从“工具”菜单中，选择“NuGet 程序包管理器”>“包管理器控制台”。

  ![PMC 菜单](../first-mvc-app/adding-model/_static/pmc.png)

在 PMC 中，输入以下命令：

```powershell
Install-Package Microsoft.VisualStudio.Web.CodeGeneration.Design -Version 2.0.3
Add-Migration Initial
Update-Database
```

或者，可使用以下 .NET Core CLI 命令：

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet ef migrations add Initial
dotnet ef database update
```

忽略以下消息：

    `Microsoft.EntityFrameworkCore.Model.Validation[30000]`

      *No type was specified for the decimal column 'Price' on entity type 'Movie'. This will cause values to be silently truncated if they do not fit in the default precision and scale. Explicitly specify the SQL server column type that can accommodate all the values using 'ForHasColumnType()'*

下一教程将对此进行修复。

`Install-Package` 命令安装运行基架引擎所需的工具。

`Add-Migration` 命令生成用于创建初始数据库架构的代码。 此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。 `Initial` 参数用于为迁移命名。 可以使用任意名称，但是按照惯例应选择描述迁移的名称。 有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。

`Update-Database` 命令在用于创建数据库的 Migrations/{time-stamp}_InitialCreate.cs 文件中运行 `Up` 方法。

[!INCLUDE [model 4windows](~/includes/RP/model4Win.md)]

[!INCLUDE [model 4](~/includes/RP/model4tbl.md)]

::: moniker-end

<a name="test"></a>

### <a name="test-the-app"></a>测试应用

* 运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。
* 测试“创建”链接。

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* 测试“编辑”、“详细信息”和“删除”链接。

如果收到 SQL 异常，则验证是否已运行迁移并更新了数据库。

下一个教程介绍由基架创建的文件。

> [!div class="step-by-step"]
> [上一篇：入门](xref:tutorials/razor-pages/razor-pages-start)
> [下一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)
