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
ms.openlocfilehash: 733b1c343d774e5fa8757808be07a9ae67481d84
ms.sourcegitcommit: a4dcca4f1cb81227c5ed3c92dc0e28be6e99447b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2018
ms.locfileid: "48910494"
---
<a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="662d6-102">使用 Code First 迁移以设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="662d6-102">Use Code First Migrations to Seed the Database</span></span>
====================
<span data-ttu-id="662d6-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="662d6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="662d6-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="662d6-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="662d6-105">在本部分中，你将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)EF 植入到使用测试数据的数据库中。</span><span class="sxs-lookup"><span data-stu-id="662d6-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="662d6-106">从**工具**菜单中，选择**NuGet 包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="662d6-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="662d6-107">在包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="662d6-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="662d6-108">此命令将添加到项目中，名为迁移的文件夹以及名为 Configuration.cs Migrations 文件夹中的代码文件。</span><span class="sxs-lookup"><span data-stu-id="662d6-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="662d6-109">打开 Configuration.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="662d6-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="662d6-110">添加以下**使用**语句。</span><span class="sxs-lookup"><span data-stu-id="662d6-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="662d6-111">然后将以下代码添加到**Configuration.Seed**方法：</span><span class="sxs-lookup"><span data-stu-id="662d6-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="662d6-112">在包管理器控制台窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="662d6-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="662d6-113">第一个命令生成代码来创建数据库，并第二个命令执行该代码。</span><span class="sxs-lookup"><span data-stu-id="662d6-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="662d6-114">数据库在本地创建，使用[LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)。</span><span class="sxs-lookup"><span data-stu-id="662d6-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="662d6-115">探索 API （可选）</span><span class="sxs-lookup"><span data-stu-id="662d6-115">Explore the API (Optional)</span></span>

<span data-ttu-id="662d6-116">按 F5 在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="662d6-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="662d6-117">Visual Studio 启动 IIS Express，并运行你的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="662d6-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="662d6-118">然后，visual Studio 启动浏览器并打开应用的主页。</span><span class="sxs-lookup"><span data-stu-id="662d6-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="662d6-119">Visual Studio 运行时 web 项目，它将分配一个端口号。</span><span class="sxs-lookup"><span data-stu-id="662d6-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="662d6-120">下图中的端口号是 50524。</span><span class="sxs-lookup"><span data-stu-id="662d6-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="662d6-121">当您运行该应用程序时，您将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="662d6-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="662d6-122">使用 ASP.NET MVC 实现主页。</span><span class="sxs-lookup"><span data-stu-id="662d6-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="662d6-123">在页面的顶部，是一个链接，显示"API"。</span><span class="sxs-lookup"><span data-stu-id="662d6-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="662d6-124">此链接将您可以自动生成的帮助页，对 web API。</span><span class="sxs-lookup"><span data-stu-id="662d6-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="662d6-125">(若要了解如何生成此帮助页，以及如何将您自己的文档添加到页面，请参阅[创建 ASP.NET Web api 的帮助页](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。)您可以单击帮助页链接，以查看有关此 API，包括请求和响应格式的详细信息。</span><span class="sxs-lookup"><span data-stu-id="662d6-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="662d6-126">此 API 支持对数据库的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="662d6-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="662d6-127">下表汇总了 API。</span><span class="sxs-lookup"><span data-stu-id="662d6-127">The following summarizes the API.</span></span>

| <span data-ttu-id="662d6-128">作者</span><span class="sxs-lookup"><span data-stu-id="662d6-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="662d6-129">获取 api/作者</span><span class="sxs-lookup"><span data-stu-id="662d6-129">GET api/authors</span></span> | <span data-ttu-id="662d6-130">获取所有作者。</span><span class="sxs-lookup"><span data-stu-id="662d6-130">Get all authors.</span></span> |
| <span data-ttu-id="662d6-131">获取 api/作者 / {id}</span><span class="sxs-lookup"><span data-stu-id="662d6-131">GET api/authors/{id}</span></span> | <span data-ttu-id="662d6-132">获取作者的 id。</span><span class="sxs-lookup"><span data-stu-id="662d6-132">Get an author by ID.</span></span> |
| <span data-ttu-id="662d6-133">POST/api/作者</span><span class="sxs-lookup"><span data-stu-id="662d6-133">POST /api/authors</span></span> | <span data-ttu-id="662d6-134">创建新的作者。</span><span class="sxs-lookup"><span data-stu-id="662d6-134">Create a new author.</span></span> |
| <span data-ttu-id="662d6-135">PUT/api/作者 / {id}</span><span class="sxs-lookup"><span data-stu-id="662d6-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="662d6-136">更新现有作者。</span><span class="sxs-lookup"><span data-stu-id="662d6-136">Update an existing author.</span></span> |
| <span data-ttu-id="662d6-137">删除/api/作者 / {id}</span><span class="sxs-lookup"><span data-stu-id="662d6-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="662d6-138">删除作者。</span><span class="sxs-lookup"><span data-stu-id="662d6-138">Delete an author.</span></span> |

| <span data-ttu-id="662d6-139">图书</span><span class="sxs-lookup"><span data-stu-id="662d6-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="662d6-140">获取 /api/books</span><span class="sxs-lookup"><span data-stu-id="662d6-140">GET /api/books</span></span> | <span data-ttu-id="662d6-141">获取所有书籍。</span><span class="sxs-lookup"><span data-stu-id="662d6-141">Get all books.</span></span> |
| <span data-ttu-id="662d6-142">获取/api/丛书 / {id}</span><span class="sxs-lookup"><span data-stu-id="662d6-142">GET /api/books/{id}</span></span> | <span data-ttu-id="662d6-143">获取的 id。</span><span class="sxs-lookup"><span data-stu-id="662d6-143">Get a book by ID.</span></span> |
| <span data-ttu-id="662d6-144">发布/api/丛书</span><span class="sxs-lookup"><span data-stu-id="662d6-144">POST /api/books</span></span> | <span data-ttu-id="662d6-145">创建新的书籍。</span><span class="sxs-lookup"><span data-stu-id="662d6-145">Create a new book.</span></span> |
| <span data-ttu-id="662d6-146">PUT/api/丛书 / {id}</span><span class="sxs-lookup"><span data-stu-id="662d6-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="662d6-147">更新现有书籍。</span><span class="sxs-lookup"><span data-stu-id="662d6-147">Update an existing book.</span></span> |
| <span data-ttu-id="662d6-148">删除/api/丛书 / {id}</span><span class="sxs-lookup"><span data-stu-id="662d6-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="662d6-149">删除一本书。</span><span class="sxs-lookup"><span data-stu-id="662d6-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="662d6-150">查看数据库 （可选）</span><span class="sxs-lookup"><span data-stu-id="662d6-150">View the Database (Optional)</span></span>

<span data-ttu-id="662d6-151">当运行 Update-database 命令时，EF 创建数据库，并调用`Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="662d6-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="662d6-152">在本地运行应用程序时，使用 EF [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。</span><span class="sxs-lookup"><span data-stu-id="662d6-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="662d6-153">在 Visual Studio 中，可以查看数据库。</span><span class="sxs-lookup"><span data-stu-id="662d6-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="662d6-154">从**视图**菜单中，选择**SQL Server 对象资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="662d6-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="662d6-155">在中**连接到服务器**对话框中**服务器名称**编辑框中，键入"(localdb) \v11.0"。</span><span class="sxs-lookup"><span data-stu-id="662d6-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="662d6-156">将保留**身份验证**选项作为"Windows 身份验证"。</span><span class="sxs-lookup"><span data-stu-id="662d6-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="662d6-157">单击“连接” 。</span><span class="sxs-lookup"><span data-stu-id="662d6-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="662d6-158">Visual Studio 连接到 LocalDB 和 SQL Server 对象资源管理器窗口中显示现有的数据库。</span><span class="sxs-lookup"><span data-stu-id="662d6-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="662d6-159">您可以展开节点以查看 EF 创建的表。</span><span class="sxs-lookup"><span data-stu-id="662d6-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="662d6-160">若要查看的数据，右键单击某个表并选择**查看数据**。</span><span class="sxs-lookup"><span data-stu-id="662d6-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="662d6-161">以下屏幕截图显示了丛书表的结果。</span><span class="sxs-lookup"><span data-stu-id="662d6-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="662d6-162">请注意，EF 填充数据库种子数据，并且该表包含作者表的外键。</span><span class="sxs-lookup"><span data-stu-id="662d6-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="662d6-163">[上一页](part-2.md)
> [下一页](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="662d6-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
