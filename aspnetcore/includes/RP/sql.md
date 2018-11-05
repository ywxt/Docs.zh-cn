# <a name="work-with-sqlite-in-an-aspnet-core-razor-pages-app"></a><span data-ttu-id="90bdf-101">在 ASP.NET Core Razor Pages 应用中使用 SQLite</span><span class="sxs-lookup"><span data-stu-id="90bdf-101">Work with SQLite in an ASP.NET Core Razor Pages app</span></span>

<span data-ttu-id="90bdf-102">作者：[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="90bdf-102">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="90bdf-103">`MovieContext` 对象处理连接到数据库并将 `Movie` 对象映射到数据库记录的任务。</span><span class="sxs-lookup"><span data-stu-id="90bdf-103">The `MovieContext` object handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="90bdf-104">在 Startup.cs 文件的 `ConfigureServices` 方法中向[依赖关系注入 (DI)](xref:fundamentals/dependency-injection) 容器注册数据库上下文：</span><span class="sxs-lookup"><span data-stu-id="90bdf-104">The database context is registered with the [Dependency Injection (DI)](xref:fundamentals/dependency-injection) container in the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](code/Startup.cs?name=snippet2&highlight=6-8)]

<span data-ttu-id="90bdf-105">有关配合使用 `DbContext` 和 DI 的详细信息，请参阅[配合使用 DbContext 和 DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection)。</span><span class="sxs-lookup"><span data-stu-id="90bdf-105">For more information on using `DbContext` with DI, see [Using DbContext with DI](/ef/core/miscellaneous/configuring-dbcontext#using-dbcontext-with-dependency-injection).</span></span>

## <a name="sqlite"></a><span data-ttu-id="90bdf-106">SQLite</span><span class="sxs-lookup"><span data-stu-id="90bdf-106">SQLite</span></span>

<span data-ttu-id="90bdf-107">[SQLite](https://www.sqlite.org/) 网站上表示：</span><span class="sxs-lookup"><span data-stu-id="90bdf-107">The [SQLite](https://www.sqlite.org/) website states:</span></span>

> <span data-ttu-id="90bdf-108">SQLite 是一个自包含、高可靠性、嵌入式、功能完整、公共域的 SQL 数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="90bdf-108">SQLite is a self-contained, high-reliability, embedded, full-featured, public-domain, SQL database engine.</span></span> <span data-ttu-id="90bdf-109">SQLite 是世界上使用最多的数据库引擎。</span><span class="sxs-lookup"><span data-stu-id="90bdf-109">SQLite is the most used database engine in the world.</span></span>

<span data-ttu-id="90bdf-110">可以下载许多第三方工具来管理并查看 SQLite 数据库。</span><span class="sxs-lookup"><span data-stu-id="90bdf-110">There are many third party tools you can download to manage and view a SQLite database.</span></span> <span data-ttu-id="90bdf-111">下面的图片来自 [DB Browser for SQLite](http://sqlitebrowser.org/)。</span><span class="sxs-lookup"><span data-stu-id="90bdf-111">The image below is from [DB Browser for SQLite](http://sqlitebrowser.org/).</span></span> <span data-ttu-id="90bdf-112">如果你有最喜欢的 SQLite 工具，请发表评论以分享你喜欢的方面。</span><span class="sxs-lookup"><span data-stu-id="90bdf-112">If you have a favorite SQLite tool, leave a comment on what you like about it.</span></span>

![显示电影数据库的 DB Browser for SQLite](../../tutorials/first-mvc-app-xplat/working-with-sql/_static/dbb.png)

## <a name="seed-the-database"></a><span data-ttu-id="90bdf-114">设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="90bdf-114">Seed the database</span></span>

<span data-ttu-id="90bdf-115">在 Models 文件夹中创建一个名为 `SeedData` 的新类。</span><span class="sxs-lookup"><span data-stu-id="90bdf-115">Create a new class named `SeedData` in the *Models* folder.</span></span> <span data-ttu-id="90bdf-116">将生成的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="90bdf-116">Replace the generated code with the following:</span></span>

[!code-csharp[](code/Models/SeedData.cs)]

<span data-ttu-id="90bdf-117">如果 DB 中没有任何电影，则会返回种子初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="90bdf-117">If there are any movies in the DB, the seed initializer returns.</span></span>

```csharp
if (context.Movie.Any())
{
    return;   // DB has been seeded.
}
```

<a name="si"></a>
### <a name="add-the-seed-initializer"></a><span data-ttu-id="90bdf-118">添加种子初始值设定项</span><span class="sxs-lookup"><span data-stu-id="90bdf-118">Add the seed initializer</span></span>

<span data-ttu-id="90bdf-119">将种子初始值设定项添加 Program.cs 文件中的 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="90bdf-119">Add the seed initializer to the `Main` method in the *Program.cs* file:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Program.cs)]

### <a name="test-the-app"></a><span data-ttu-id="90bdf-120">测试应用</span><span class="sxs-lookup"><span data-stu-id="90bdf-120">Test the app</span></span>

<span data-ttu-id="90bdf-121">删除 DB 中的所有记录（使种子方法运行）。</span><span class="sxs-lookup"><span data-stu-id="90bdf-121">Delete all the records in the DB (So the seed method will run).</span></span> <span data-ttu-id="90bdf-122">停止并启动应用以设定数据库种子。</span><span class="sxs-lookup"><span data-stu-id="90bdf-122">Stop and start the app to seed the database.</span></span>

<span data-ttu-id="90bdf-123">应用将显示设定为种子的数据。</span><span class="sxs-lookup"><span data-stu-id="90bdf-123">The app shows the seeded data.</span></span>
