向 `Movie` 类添加以下属性：

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Models/MovieNoEF.cs?name=snippet_MovieNoEF)]

数据库需要 `ID` 字段作为主键。

<a name="dc"></a>
### <a name="add-a-database-context-class"></a>添加数据库上下文类

将以下 MovieContext.cs 类添加到“模型”文件夹：  

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/snapshot_sample/RazorPagesMovie/Models/MovieContext.cs)]

前面的代码为实体集创建 `DbSet` 属性。 在实体框架术语中，实体集通常与数据库表相对应，实体与表中的行相对应。
