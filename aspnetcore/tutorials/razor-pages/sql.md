---
title: "使用 SQL Server LocalDB 和 ASP.NET Core"
author: rick-anderson
description: "说明如何使用 SQL Server LocalDB 和 ASP.NET Core"
ms.author: riande
manager: wpickett
ms.date: 08/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: aspnet-core
uid: tutorials/razor-pages/sql
ms.openlocfilehash: 07f024e2e178828c4488adfd866fc6eec3b251dd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="working-with-sql-server-localdb-and-aspnet-core"></a><span data-ttu-id="b2c32-103">使用 SQL Server LocalDB 和 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="b2c32-103">Working with SQL Server LocalDB and ASP.NET Core</span></span>

<span data-ttu-id="b2c32-104">作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="b2c32-104">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span> 

<span data-ttu-id="b2c32-105">`MovieContext` 对象处理连接到数据库并将 `Movie` 对象映射到数据库记录的任务。</span><span class="sxs-lookup"><span data-stu-id="b2c32-105">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="b2c32-106">在 Startup.cs 文件的 `ConfigureServices` 方法中向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="b2c32-106">The database context is registered with the [Dependency Injection](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices&highlight=7-8)]

<span data-ttu-id="b2c32-107">ASP.NET Core [配置](xref:fundamentals/configuration/index)系统会读取 `ConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="b2c32-107">The ASP.NET Core [Configuration](xref:fundamentals/configuration/index) system reads the `ConnectionString`.</span></span> <span data-ttu-id="b2c32-108">为了进行本地开发，它会从 appsettings.json 文件获取连接字符串：</span><span class="sxs-lookup"><span data-stu-id="b2c32-108">For local development, it gets the connection string from the *appsettings.json* file:</span></span>

[!code-json[Main](razor-pages-start/sample/RazorPagesMovie/appsettings.json?highlight=2&range=8-10)]

<span data-ttu-id="b2c32-109">将应用部署到测试或生产服务器时，可使用环境变量或另一种方法将连接字符串设置为实际的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b2c32-109">When you deploy the app to a test or production server, you can use an environment variable or another approach to set the connection string to a real SQL Server.</span></span> <span data-ttu-id="b2c32-110">有关详细信息，请参阅[配置](xref:fundamentals/configuration/index)。</span><span class="sxs-lookup"><span data-stu-id="b2c32-110">See [Configuration](xref:fundamentals/configuration/index) for more information.</span></span>

## <a name="sql-server-express-localdb"></a><span data-ttu-id="b2c32-111">SQL Server Express LocalDB</span><span class="sxs-lookup"><span data-stu-id="b2c32-111">SQL Server Express LocalDB</span></span>

<span data-ttu-id="b2c32-112">LocalDB 是轻型版的 SQL Server Express 数据库引擎，以程序开发为目标。</span><span class="sxs-lookup"><span data-stu-id="b2c32-112">LocalDB is a lightweight version of the SQL Server Express Database Engine that's targeted for program development.</span></span> <span data-ttu-id="b2c32-113">LocalDB 按需启动并在用户模式下运行，因此没有复杂的配置。</span><span class="sxs-lookup"><span data-stu-id="b2c32-113">LocalDB starts on demand and runs in user mode, so there's no complex configuration.</span></span> <span data-ttu-id="b2c32-114">默认情况下，LocalDB 数据库在 C:/Users/\<user\> 目录中创建“\*.mdf”文件。</span><span class="sxs-lookup"><span data-stu-id="b2c32-114">By default, LocalDB database creates "\*.mdf" files in the *C:/Users/\<user\>* directory.</span></span>

<a name="ssox"></a>
* <span data-ttu-id="b2c32-115">从“视图”菜单中，打开“SQL Server 对象资源管理器”(SSOX)。</span><span class="sxs-lookup"><span data-stu-id="b2c32-115">From the **View** menu, open **SQL Server Object Explorer** (SSOX).</span></span>

  ![“视图”菜单](sql/_static/ssox.png)

* <span data-ttu-id="b2c32-117">右键单击 `Movie` 表，然后选择“视图设计器”：</span><span class="sxs-lookup"><span data-stu-id="b2c32-117">Right click on the `Movie` table and select **View Designer**:</span></span>

  ![Movie 表上打开的上下文菜单](sql/_static/design.png)

  ![设计器中打开的 Movie 表](sql/_static/dv.png)

<span data-ttu-id="b2c32-120">请注意 `ID` 旁边的密钥图标。</span><span class="sxs-lookup"><span data-stu-id="b2c32-120">Note the key icon next to `ID`.</span></span> <span data-ttu-id="b2c32-121">默认情况下，EF 为该主键创建一个名为 `ID` 的属性。</span><span class="sxs-lookup"><span data-stu-id="b2c32-121">By default, EF creates a property named `ID` for the primary key.</span></span>

* <span data-ttu-id="b2c32-122">右键单击 `Movie` 表，然后选择“查看数据”：</span><span class="sxs-lookup"><span data-stu-id="b2c32-122">Right click on the `Movie` table and select **View Data**:</span></span>

  ![显示表数据的打开的 Movie 表](sql/_static/vd22.png)

## <a name="seed-the-database"></a><span data-ttu-id="b2c32-124">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="b2c32-124">Seed the database</span></span>

<span data-ttu-id="b2c32-125">在 Models 文件夹中创建一个名为 `SeedData` 的新类。</span><span class="sxs-lookup"><span data-stu-id="b2c32-125">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="b2c32-126">将生成的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="b2c32-126">Replace the generated code with the following:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Models/SeedData.cs?name=snippet_1)]

<span data-ttu-id="b2c32-127">如果 DB 中没有任何电影，则会返回种子初始值设定项，并且不会添加任何电影。</span><span class="sxs-lookup"><span data-stu-id="b2c32-127">If there are any movies in the DB, the seed initializer returns and no movies are added.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```
<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="b2c32-128">添加种子初始值设定项</span><span class="sxs-lookup"><span data-stu-id="b2c32-128">Add the seed initializer</span></span>

<span data-ttu-id="b2c32-129">将种子初始值设定项添加 Program.cs 文件中的 `Main` 方法末端：</span><span class="sxs-lookup"><span data-stu-id="b2c32-129">Add the seed initializer to the end of the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[Main](razor-pages-start/sample/RazorPagesMovie/Program.cs)]

<span data-ttu-id="b2c32-130">测试应用</span><span class="sxs-lookup"><span data-stu-id="b2c32-130">Test the app</span></span>

* <span data-ttu-id="b2c32-131">删除 DB 中的所有记录。</span><span class="sxs-lookup"><span data-stu-id="b2c32-131">Delete all the records in the DB.</span></span> <span data-ttu-id="b2c32-132">可以使用浏览器中的删除链接，也可以从 [SSOX](xref:tutorials/razor-pages/new-field#ssox) 执行此操作</span><span class="sxs-lookup"><span data-stu-id="b2c32-132">You can do this with the delete links in the browser or from [SSOX](xref:tutorials/razor-pages/new-field#ssox)</span></span>
* <span data-ttu-id="b2c32-133">强制应用初始化（调用 `Startup` 类中的方法），使种子方法能够正常运行。</span><span class="sxs-lookup"><span data-stu-id="b2c32-133">Force the app to initialize (call the methods in the `Startup` class) so the seed method runs.</span></span> <span data-ttu-id="b2c32-134">若要强制进行初始化，必须先停止 IIS Express，然后再重新启动它。</span><span class="sxs-lookup"><span data-stu-id="b2c32-134">To force initialization, IIS Express must be stopped and restarted.</span></span> <span data-ttu-id="b2c32-135">可以使用以下任一方法来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="b2c32-135">You can do this with any of the following approaches:</span></span>

  * <span data-ttu-id="b2c32-136">右键单击通知区域中的 IIS Express 系统任务栏图标，然后点击“退出”或“停止站点”：</span><span class="sxs-lookup"><span data-stu-id="b2c32-136">Right click the IIS Express system tray icon in the notification area and tap **Exit** or **Stop Site**:</span></span>

    ![IIS Express 系统任务栏图标](../first-mvc-app/working-with-sql/_static/iisExIcon.png)

    ![上下文菜单](sql/_static/stopIIS.png)

   * <span data-ttu-id="b2c32-139">如果是在非调试模式下运行 VS 的，请按 F5 以在调试模式下运行。</span><span class="sxs-lookup"><span data-stu-id="b2c32-139">If you were running VS in non-debug mode, press F5 to run in debug mode.</span></span>
   * <span data-ttu-id="b2c32-140">如果是在调试模式下运行 VS 的，请停止调试程序并按 F5。</span><span class="sxs-lookup"><span data-stu-id="b2c32-140">If you were running VS in debug mode, stop the debugger and press F5.</span></span>
   
<span data-ttu-id="b2c32-141">应用将显示设定为种子的数据：</span><span class="sxs-lookup"><span data-stu-id="b2c32-141">The app shows the seeded data:</span></span>

![在 Chrome 中打开的显示电影数据的电影应用程序](sql/_static/m55.png)

<span data-ttu-id="b2c32-143">在下一教程中将对数据的展示进行整理。</span><span class="sxs-lookup"><span data-stu-id="b2c32-143">The next tutorial will clean up the presentation of the data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b2c32-144">[上一篇：已搭建基架的 Razor 页面](xref:tutorials/razor-pages/page)
[下一篇：更新页面](xref:tutorials/razor-pages/da1)</span><span class="sxs-lookup"><span data-stu-id="b2c32-144">[Previous: Scaffolded Razor Pages](xref:tutorials/razor-pages/page)
[Next: Updating the pages](xref:tutorials/razor-pages/da1)</span></span>
