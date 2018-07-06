---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 创建的连接字符串和使用 SQL Server LocalDB |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
ms.date: 10/17/2013
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: 8c8db3fc121b2ff263ab033404211e167e19cd71
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820238"
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>创建的连接字符串和使用 SQL Server LocalDB
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>创建的连接字符串和使用 SQL Server LocalDB

`MovieDBContext`创建的类处理连接到数据库以及映射任务`Movie`数据库记录的对象。 您可能会问的一个问题，是如何指定将连接到的数据库。 您实际上不必指定要使用的数据库，实体框架将默认使用[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。 在本部分中我们将显式添加中的连接字符串*Web.config*应用程序文件。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)是 SQL Server Express 数据库引擎的按需启动并在用户模式下运行的轻型版本。 中的 SQL Server Express，使您可以使用数据库作为特殊执行模式运行 LocalDB *.mdf*文件。 通常情况下，LocalDB 数据库文件保存在*应用程序\_数据*web 项目的文件夹。

不建议在生产 web 应用程序中使用 SQL Server Express。 LocalDB 特别不应为生产 web 应用程序因为它不旨在与 IIS 配合使用。 但是，LocalDB 数据库可以轻松地迁移到 SQL Server 或 SQL Azure。

在 Visual Studio 2017 中，默认情况下，使用 Visual Studio 安装 LocalDB。

默认情况下，实体框架将查找名为对象上下文类相同的连接字符串 (`MovieDBContext`此项目)。 有关详细信息请参阅[ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。

打开应用程序根目录*Web.config*文件如下所示。 (未*Web.config*中的文件*视图*文件夹。)

![](creating-a-connection-string/_static/image1.png)

查找`<connectionStrings>`元素：

![](creating-a-connection-string/_static/image2.png)

添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

下面的示例显示了一部分*Web.config*文件添加的新连接字符串：

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

两个连接字符串都非常相似。 第一个连接字符串名为`DefaultConnection`和用于成员资格数据库中控制可以访问该应用程序。 已添加的连接字符串指定一个名为的 LocalDB 数据库*Movie.mdf*位于*应用\_数据*文件夹。 我们不会在本教程中，为成员资格、 身份验证和安全的详细信息中使用成员资格数据库，请参阅我的教程[使用身份验证和 SQL 数据库创建 ASP.NET MVC 应用并将其部署到 Azure 应用服务](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。

连接字符串的名称必须与匹配的名称[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类。

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

实际上不需要添加`MovieDBContext`连接字符串。 如果未指定连接字符串，实体框架将 LocalDB 数据库目录中创建用户的完全限定名称[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类 (在这种情况下`MvcMovie.Models.MovieDBContext`)。 可以对数据库命名您喜欢的任何，只要它具有 *。MDF*后缀。 例如，我们无法将数据库命名*MyFilms.mdf*。

接下来，你将生成一个新`MoviesController`类，该类可以用于显示电影数据并允许用户创建新的影片列表。

> [!div class="step-by-step"]
> [上一页](adding-a-model.md)
> [下一页](accessing-your-models-data-from-a-controller.md)
