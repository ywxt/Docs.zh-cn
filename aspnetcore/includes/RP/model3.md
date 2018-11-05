<a name="cli"></a>

## <a name="add-scaffold-tooling-and-perform-initial-migration"></a><span data-ttu-id="84e3d-101">添加基架工具并执行初始迁移</span><span class="sxs-lookup"><span data-stu-id="84e3d-101">Add scaffold tooling and perform initial migration</span></span>

<span data-ttu-id="84e3d-102">将以下行添加到 RazorPagesMovie.csproj 文件，具体位于末尾的 `</Project>` 标记前面：</span><span class="sxs-lookup"><span data-stu-id="84e3d-102">Add the following lines to the *RazorPagesMovie.csproj* file, just before the closing `</Project>` tag:</span></span>

```xml
<ItemGroup>
  <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.1.0-preview1-final"/>
</ItemGroup>
```
  
<span data-ttu-id="84e3d-103">从命令行运行以下 .NET Core CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="84e3d-103">From the command line, run the following .NET Core CLI commands:</span></span>

```console
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
dotnet ef migrations add InitialCreate
dotnet ef database update
```

<span data-ttu-id="84e3d-104">`DotNetCliToolReference` 元素和 `add package` 命令安装运行基架引擎所需的工具。</span><span class="sxs-lookup"><span data-stu-id="84e3d-104">The `DotNetCliToolReference` element and the `add package` command install the tooling required to run the scaffolding engine.</span></span>

<span data-ttu-id="84e3d-105">`ef migrations add InitialCreate` 命令生成用于创建初始数据库架构的代码。</span><span class="sxs-lookup"><span data-stu-id="84e3d-105">The `ef migrations add InitialCreate` command generates code to create the initial database schema.</span></span> <span data-ttu-id="84e3d-106">此架构以（Models/MovieContext.cs 文件中的）`DbContext` 中指定的模型为基础。</span><span class="sxs-lookup"><span data-stu-id="84e3d-106">The schema is based on the model specified in the `DbContext` (In the *Models/MovieContext.cs* file).</span></span> <span data-ttu-id="84e3d-107">`InitialCreate` 参数用于为迁移命名。</span><span class="sxs-lookup"><span data-stu-id="84e3d-107">The `InitialCreate` argument is used to name the migrations.</span></span> <span data-ttu-id="84e3d-108">可以使用任意名称，但是按照惯例应选择描述迁移的名称。</span><span class="sxs-lookup"><span data-stu-id="84e3d-108">You can use any name, but by convention you choose a name that describes the migration.</span></span> <span data-ttu-id="84e3d-109">有关详细信息，请参阅[迁移简介](xref:data/ef-mvc/migrations#introduction-to-migrations)。</span><span class="sxs-lookup"><span data-stu-id="84e3d-109">See [Introduction to migrations](xref:data/ef-mvc/migrations#introduction-to-migrations) for more information.</span></span>

<span data-ttu-id="84e3d-110">`ef database update` 命令在用于创建数据库的 Migrations/\<time-stamp>_InitialCreate.cs 文件中运行 `Up` 方法。</span><span class="sxs-lookup"><span data-stu-id="84e3d-110">The `ef database update` command runs the `Up` method in the *Migrations/\<time-stamp>_InitialCreate.cs* file, which creates the database.</span></span>
