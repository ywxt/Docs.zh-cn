运行标识基架：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 从**解决方案资源管理器**，右键单击该项目 >**添加** > **新建基架项**。
* 从左窗格**添加基架**对话框中，选择**标识** > **添加**。
* 在**添加标识**对话框中，选择所需的选项。
  * 选择现有的布局页上，或不正确的标记将被覆盖布局文件。 选择现有 _Layout.cshtml 文件时，它是**不**覆盖。

 例如`~/Pages/Shared/_Layout.cshtml`Razor 页`~/Views/Shared/_Layout.cshtml`对于 MVC 项目
* 若要使用你现有的数据上下文，选择要重写的至少一个文件。 必须选择至少一个文件以添加你的数据上下文。
  * 选择您的数据上下文类。
  * 选择**添加**。
* 若要创建新的用户上下文，并可能对标识创建自定义用户类：
  * 选择**+** 按钮以创建一个新**数据上下文类**。
  * 选择**添加**。

注意： 如果你要创建新的用户上下文，你无需选择要重写的文件。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

如果以前尚未安装 ASP.NET 基架，请立即进行安装：

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

添加对的包引用[Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/)到项目 (\*.csproj) 文件。 在项目目录中运行以下命令：

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

运行以下命令以列出标识基架选项：

```cli
dotnet aspnet-codegenerator identity -h
```

在项目文件夹中，使用所需的选项运行标识基架。 例如，若要安装过程中使用默认 UI 的标识和文件的最小的数，运行以下命令。 使用你的数据库上下文的正确完全限定的名：

```cli
dotnet aspnet-codegenerator identity -dc MyWeb.Data.ApplicationDbContext --files Account.Register
```

-------------
