---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: 使用 Code First 迁移以设定数据库种子 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 533d3a6e9a69584fb2523b2c0a604755e372f031
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41832536"
---
<a name="use-code-first-migrations-to-seed-the-database"></a>使用 Code First 迁移以设定数据库种子
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，你将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)EF 植入到使用测试数据的数据库中。

从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。 在包管理器控制台窗口中，输入以下命令：

[!code-console[Main](part-3/samples/sample1.cmd)]

此命令将添加到项目中，名为迁移的文件夹以及名为 Configuration.cs Migrations 文件夹中的代码文件。

![](part-3/_static/image1.png)

打开 Configuration.cs 文件。 添加以下**使用**语句。

[!code-csharp[Main](part-3/samples/sample2.cs)]

然后将以下代码添加到**Configuration.Seed**方法：

[!code-csharp[Main](part-3/samples/sample3.cs)]

在包管理器控制台窗口中，键入以下命令：

[!code-console[Main](part-3/samples/sample4.cmd)]

第一个命令生成代码来创建数据库，并第二个命令执行该代码。 数据库在本地创建，使用[LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)。

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>探索 API （可选）

按 F5 在调试模式下运行应用程序。 Visual Studio 启动 IIS Express，并运行你的 web 应用。 然后，visual Studio 启动浏览器并打开应用的主页。

Visual Studio 运行时 web 项目，它将分配一个端口号。 下图中的端口号是 50524。 当您运行该应用程序时，您将看到不同的端口号。

![](part-3/_static/image3.png)

使用 ASP.NET MVC 实现主页。 在页面的顶部，是一个链接，显示"API"。 此链接将您可以自动生成的帮助页，对 web API。 (若要了解如何生成此帮助页，以及如何将您自己的文档添加到页面，请参阅[创建 ASP.NET Web api 的帮助页](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。)您可以单击帮助页链接，以查看有关此 API，包括请求和响应格式的详细信息。

![](part-3/_static/image4.png)

此 API 支持对数据库的 CRUD 操作。 下表汇总了 API。

| 作者 |  |
| --- | -- |
| 获取 api/作者 | 获取所有作者。 |
| 获取 api/作者 / {id} | 获取作者的 id。 |
| POST/api/作者 | 创建新的作者。 |
| PUT/api/作者 / {id} | 更新现有作者。 |
| 删除/api/作者 / {id} | 删除作者。 |

| 图书 |  |
| --- | -- |
| 获取 /api/books | 获取所有书籍。 |
| 获取/api/丛书 / {id} | 获取的 id。 |
| 发布/api/丛书 | 创建新的书籍。 |
| PUT/api/丛书 / {id} | 更新现有书籍。 |
| 删除/api/丛书 / {id} | 删除一本书。 |

## <a name="view-the-database-optional"></a>查看数据库 （可选）

当运行 Update-database 命令时，EF 创建数据库，并调用`Seed`方法。 在本地运行应用程序时，使用 EF [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。 在 Visual Studio 中，可以查看数据库。 从**视图**菜单中，选择**SQL Server 对象资源管理器**。

![](part-3/_static/image5.png)

在中**连接到服务器**对话框中**服务器名称**编辑框中，键入"(localdb) \v11.0"。 将保留**身份验证**选项作为"Windows 身份验证"。 单击“连接” 。

![](part-3/_static/image6.png)

Visual Studio 连接到 LocalDB 和 SQL Server 对象资源管理器窗口中显示现有的数据库。 您可以展开节点以查看 EF 创建的表。

![](part-3/_static/image7.png)

若要查看的数据，右键单击某个表并选择**查看数据**。

![](part-3/_static/image8.png)

以下屏幕截图显示了丛书表的结果。 请注意，EF 填充数据库种子数据，并且该表包含作者表的外键。

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [上一页](part-2.md)
> [下一页](part-4.md)
