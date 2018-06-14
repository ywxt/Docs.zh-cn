生成的标识数据库代码需要[Entity Framework 核心迁移](/ef/core/managing-schemas/migrations/)。 创建迁移并更新数据库。 例如，运行以下命令：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

在 Visual Studio**程序包管理器控制台**:

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

有关"CreateIdentitySchema"name 参数`Add-Migration`命令是任意的。 `"CreateIdentitySchema"` 描述迁移。