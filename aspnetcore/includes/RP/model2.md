<span data-ttu-id="92ce1-101">向 `Movie` 类添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="92ce1-101">Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieNoEF.cs?name=snippet_MovieNoEF)]

<span data-ttu-id="92ce1-102">数据库需要 `ID` 字段作为主键。</span><span class="sxs-lookup"><span data-stu-id="92ce1-102">The `ID` field is required by the database for the primary key.</span></span>

<a name="dc"></a>
### <a name="add-a-database-context-class"></a><span data-ttu-id="92ce1-103">添加数据库上下文类</span><span class="sxs-lookup"><span data-stu-id="92ce1-103">Add a database context class</span></span>

<span data-ttu-id="92ce1-104">将以下 MovieContext.cs 类添加到“模型”文件夹：</span><span class="sxs-lookup"><span data-stu-id="92ce1-104">Add the following *MovieContext.cs* class to the *Models* folder:</span></span>  

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Models/MovieContext.cs)]

<span data-ttu-id="92ce1-105">前面的代码为实体集创建 `DbSet` 属性。</span><span class="sxs-lookup"><span data-stu-id="92ce1-105">The preceding code creates a `DbSet` property for the entity set.</span></span> <span data-ttu-id="92ce1-106">在实体框架术语中，实体集通常与数据库表相对应，实体与表中的行相对应。</span><span class="sxs-lookup"><span data-stu-id="92ce1-106">In Entity Framework terminology, an entity set typically corresponds to a database table, and an entity corresponds to a row in the table.</span></span>
