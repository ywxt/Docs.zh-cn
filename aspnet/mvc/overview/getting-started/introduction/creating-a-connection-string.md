---
uid: mvc/overview/getting-started/introduction/creating-a-connection-string
title: 创建连接字符串和使用 SQL Server LocalDB |Microsoft 文档
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/17/2013
ms.topic: article
ms.assetid: 6127804d-c1a9-414d-8429-7f3dd0f56e97
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/getting-started/introduction/creating-a-connection-string
msc.type: authoredcontent
ms.openlocfilehash: edbd46ef8a03670f0cb7527142babe9bd5846c7a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="62980-102">创建连接字符串和使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="62980-102">Creating a Connection String and Working with SQL Server LocalDB</span></span>
====================
<span data-ttu-id="62980-103">通过[Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="62980-103">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a><span data-ttu-id="62980-104">创建连接字符串和使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="62980-104">Creating a Connection String and Working with SQL Server LocalDB</span></span>

<span data-ttu-id="62980-105">`MovieDBContext`你创建的类处理任务连接到数据库并映射`Movie`数据库记录的对象。</span><span class="sxs-lookup"><span data-stu-id="62980-105">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="62980-106">一个问题可能会问，不过，是如何指定它将连接到的数据库。</span><span class="sxs-lookup"><span data-stu-id="62980-106">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="62980-107">您不必实际来指定要使用的数据库，实体框架将默认为使用[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。</span><span class="sxs-lookup"><span data-stu-id="62980-107">You don't actually have to specify which database to use, Entity Framework will default to using [LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span></span> <span data-ttu-id="62980-108">在本部分中我们将显式添加中的连接字符串*Web.config*应用程序文件。</span><span class="sxs-lookup"><span data-stu-id="62980-108">In this section we'll explicitly add a connection string in the *Web.config* file of the application.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="62980-109">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="62980-109">SQL Server Express LocalDB</span></span>

<span data-ttu-id="62980-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)是 SQL Server Express 数据库引擎的按需启动并在用户模式下运行的轻量版本。</span><span class="sxs-lookup"><span data-stu-id="62980-110">[LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) is a lightweight version of the SQL Server Express Database Engine that starts on demand and runs in user mode.</span></span> <span data-ttu-id="62980-111">LocalDB 运行中的 SQL Server Express，可用于处理数据库作为一种特殊的执行模式*.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="62980-111">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="62980-112">通常，将 LocalDB 数据库文件保存在*应用\_数据*web 项目的文件夹。</span><span class="sxs-lookup"><span data-stu-id="62980-112">Typically, LocalDB database files are kept in the *App\_Data* folder of a web project.</span></span>

<span data-ttu-id="62980-113">不建议在生产 web 应用程序中使用 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="62980-113">SQL Server Express is not recommended for use in production web applications.</span></span> <span data-ttu-id="62980-114">LocalDB 尤其应不用于与 web 应用程序的生产因为它不是使用 IIS。</span><span class="sxs-lookup"><span data-stu-id="62980-114">LocalDB in particular should not be used for production with a web application because it is not designed to work with IIS.</span></span> <span data-ttu-id="62980-115">但是，LocalDB 数据库可以轻松地迁移到 SQL Server 或 SQL Azure。</span><span class="sxs-lookup"><span data-stu-id="62980-115">However, a LocalDB database can be easily migrated to SQL Server or SQL Azure.</span></span>

<span data-ttu-id="62980-116">在 Visual Studio 2017，默认情况下，使用 Visual Studio 安装 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="62980-116">In Visual Studio 2017, LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="62980-117">默认情况下，实体框架将查找名为与对象上下文类相同的连接字符串 (`MovieDBContext`为此项目)。</span><span class="sxs-lookup"><span data-stu-id="62980-117">By default, the Entity Framework looks for a connection string named the same as the object context class (`MovieDBContext` for this project).</span></span> <span data-ttu-id="62980-118">有关详细信息请参阅[ASP.NET Web 应用程序的 SQL Server 连接字符串](https://msdn.microsoft.com/library/jj653752.aspx)。</span><span class="sxs-lookup"><span data-stu-id="62980-118">For more information see [SQL Server Connection Strings for ASP.NET Web Applications](https://msdn.microsoft.com/library/jj653752.aspx).</span></span>

<span data-ttu-id="62980-119">打开应用程序根目录*Web.config*文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="62980-119">Open the application root *Web.config* file shown below.</span></span> <span data-ttu-id="62980-120">(不*Web.config*文件中*视图*文件夹。)</span><span class="sxs-lookup"><span data-stu-id="62980-120">(Not the *Web.config* file in the *Views* folder.)</span></span>

![](creating-a-connection-string/_static/image1.png)

<span data-ttu-id="62980-121">查找`<connectionStrings>`元素：</span><span class="sxs-lookup"><span data-stu-id="62980-121">Find the `<connectionStrings>` element:</span></span>

![](creating-a-connection-string/_static/image2.png)

<span data-ttu-id="62980-122">添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="62980-122">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample1.xml)]

<span data-ttu-id="62980-123">下面的示例显示的一部分*Web.config*文件以添加新的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="62980-123">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](creating-a-connection-string/samples/sample2.xml)]

<span data-ttu-id="62980-124">两个连接字符串是非常相似。</span><span class="sxs-lookup"><span data-stu-id="62980-124">The two connection strings are very similar.</span></span> <span data-ttu-id="62980-125">第一个连接字符串命名为`DefaultConnection`和用于成员资格数据库以控制可以访问应用程序。</span><span class="sxs-lookup"><span data-stu-id="62980-125">The first connection string is named `DefaultConnection` and is used for the membership database to control who can access the application.</span></span> <span data-ttu-id="62980-126">你已添加的连接字符串指定一个名为的 LocalDB 数据库*Movie.mdf*位于*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="62980-126">The connection string you've added specifies a LocalDB database named *Movie.mdf* located in the *App\_Data* folder.</span></span> <span data-ttu-id="62980-127">我们不会在本教程中，有关详细信息成员身份、 身份验证和安全中使用成员资格数据库，请参阅我的教程[使用身份验证和 SQL 数据库中创建的 ASP.NET MVC 应用并部署到 Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="62980-127">We won't use the membership database in this tutorial, for more information on membership, authentication and security, see my tutorial [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>

<span data-ttu-id="62980-128">连接字符串的名称必须与匹配的名称[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类。</span><span class="sxs-lookup"><span data-stu-id="62980-128">The name of the connection string must match the name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class.</span></span>

[!code-csharp[Main](creating-a-connection-string/samples/sample3.cs?highlight=15)]

<span data-ttu-id="62980-129">你实际上不需要添加`MovieDBContext`连接字符串。</span><span class="sxs-lookup"><span data-stu-id="62980-129">You don't actually need to add the `MovieDBContext` connection string.</span></span> <span data-ttu-id="62980-130">如果未指定连接字符串，实体框架将带有完全限定名称的用户目录中创建 LocalDB 数据库[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)类 (在这种情况下`MvcMovie.Models.MovieDBContext`)。</span><span class="sxs-lookup"><span data-stu-id="62980-130">If you don't specify a connection string, Entity Framework will create a LocalDB database in the users directory with the fully qualified name of the [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) class (in this case `MvcMovie.Models.MovieDBContext`).</span></span> <span data-ttu-id="62980-131">你可以将数据库命名您喜欢的任何，只要它具有*。MDF*后缀。</span><span class="sxs-lookup"><span data-stu-id="62980-131">You can name the database anything you like, as long as it has the *.MDF* suffix.</span></span> <span data-ttu-id="62980-132">例如，我们无法将数据库命名*MyFilms.mdf*。</span><span class="sxs-lookup"><span data-stu-id="62980-132">For example, we could name the database *MyFilms.mdf*.</span></span>

<span data-ttu-id="62980-133">接下来，你将生成一个新`MoviesController`类，该类可以用于显示影片数据，并允许用户创建新的影片列表。</span><span class="sxs-lookup"><span data-stu-id="62980-133">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="62980-134">[上一页](adding-a-model.md)
> [下一页](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="62980-134">[Previous](adding-a-model.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>
