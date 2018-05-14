---
title: NSwag 和 ASP.NET Core 入门
author: zuckerthoben
description: 了解如何使用 NSwag 为 ASP.NET Core Web API 应用生成文档和帮助页面。
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 03/15/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: tutorials/get-started-with-nswag
ms.openlocfilehash: 80e6a9e1702d8f68d139d2ff9c3a01a27c40cecb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="get-started-with-nswag-and-aspnet-core"></a>NSwag 和 ASP.NET Core 入门

作者：[Christoph Nienaber](https://twitter.com/zuckerthoben) 和 [Rico Suter](https://rsuter.com)

在 ASP.NET Core 中间件中使用 [NSwag](https://github.com/RSuter/NSwag) 需要 [NSwag.AspNetCore](https://www.nuget.org/packages/NSwag.AspNetCore/) NuGet 包。 该包由 Swagger 生成器、Swagger UI（v2 和 v3）和 [ReDoc UI](https://github.com/Rebilly/ReDoc) 组成。

强烈建议使用 NSwag 的代码生成功能。 请为代码生成选择下列选项之一：

* 使用 [NSwagStudio](https://github.com/NSwag/NSwag/wiki/NSwagStudio)，这是一款 Windows 桌面应用，用于在 C# 和 TypeScript 中为 API 生成客户端代码
* 使用 [NSwag.CodeGeneration.CSharp](https://www.nuget.org/packages/NSwag.CodeGeneration.CSharp/) 或 [NSwag.CodeGeneration.TypeScript](https://www.nuget.org/packages/NSwag.CodeGeneration.TypeScript/) NuGet 包在项目中执行代码生成
* 使用[命令行](https://github.com/NSwag/NSwag/wiki/CommandLine)中的 NSwag
* 使用 [NSwag.MSBuild](https://github.com/NSwag/NSwag/wiki/MSBuild) NuGet 包

## <a name="features"></a>功能

使用 NSwag 的主要原因是它不仅能引入 Swagger UI 和 Swagger 生成器，还能利用灵活的代码生成功能。 无需现有API &mdash; 可使用包含 Swagger 的第三方 API 并让 NSwag 生成客户端实现。 无论哪种方式，开发周期都会加快，可以更轻松地适应 API 更改。

## <a name="package-installation"></a>包安装

可使用以下方法添加 NuGet 包：

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 从“程序包管理器控制台”窗口：

    ```powershell
    Install-Package NSwag.AspNetCore
    ```

* 从“管理 NuGet 程序包”对话框中：
  * 右键单击“解决方案资源管理器” > “管理 NuGet 包”中的项目
  * 将“包源”设置为“nuget.org”
  * 在搜索框中输入“NSwag.AspNetCore”
  * 从“浏览”选项卡中选择“NSwag.AspNetCore”包，然后单击“安装”

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[Visual Studio for Mac](#tab/visual-studio-mac)

* 右键单击“Solution Pad” > “添加包...”中的“包”文件夹
* 将“添加包”窗口的“源”下拉列表设置为“nuget.org”
* 在搜索框中输入 NSwag.AspNetCore
* 从结果窗格中选择“NSwag.AspNetCore”包，然后单击“添加包”

# <a name="visual-studio-codetabvisual-studio-code"></a>[Visual Studio Code](#tab/visual-studio-code)

从“集成终端”中运行以下命令：

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

运行下面的命令：

```console
dotnet add TodoApi.NSwag.csproj package NSwag.AspNetCore
```

---

## <a name="add-and-configure-swagger-middleware"></a>添加并配置 Swagger 中间件

在 `Info` 类中导入以下命名空间：

```csharp
using NSwag.AspNetCore;
using System.Reflection;
using NJsonSchema;
```

在 `Startup.Configure` 方法中，启用中间件为生成的 Swagger 规范和 Swagger UI 提供服务：

[!code-cs[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/Startup.cs?name=snippet_Configure&highlight=4,7-10)]

启动应用。 导航到 `/swagger` 查看 Swagger UI。 导航到 `/swagger/v1/swagger.json` 查看 Swagger 规范。

## <a name="code-generation"></a>代码生成

### <a name="via-nswagstudio"></a>通过 NSwagStudio

* 从官方 [GitHub 存储库](https://github.com/RSuter/NSwag/wiki/NSwagStudio)安装 `NSwagStudio`。

* 启动 NSwagStudio。 输入 swagger.json 的位置或直接复制它：

![NSwagStudio](web-api-help-pages-using-swagger/_static/NSwagStudio.png)

* 指示所需的客户端输出类型。 选项包括“TypeScript 客户端”、“CSharp 客户端”或“CSharp Web API 控制器”。 使用 Web API 控制器基本上是一种反向生成。 它使用服务的规范来重新生成服务。

* 单击“生成输出”。

* 可在此处看到 C# 中的 TodoApi.NSwag 示例的完整客户端实现：

![NSwagStudio-Output](web-api-help-pages-using-swagger/_static/NSwagStudio-Output.png)

* 将该文件放入客户端项目（例如，[Xamarin.Forms](/xamarin/xamarin-forms/) 应用）。 开始使用 API：

```csharp
var todoClient = new TodoClient();

// Gets all Todos from the Api
var allTodos = await todoClient.GetAllAsync();

// Create a new TodoItem and save it in the Api
var createdTodo = await todoClient.CreateAsync(new TodoItem);

// Get a single Todo by Id
var foundTodo = await todoClient.GetByIdAsync(1);
```

> [!NOTE]
> 可将基 URL 和/或 HTTP 客户端注入 API 客户端。 最佳做法是始终[重复使用 HttpClient](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/)。

现在可开始轻松地将 API 实施到客户端项目中。

### <a name="other-ways-to-generate-client-code"></a>生成客户端代码的其他方法

可通过其他更适合你的工作流的方式生成代码：

* [MSBuild](https://www.nuget.org/packages/NSwag.MSBuild/)

* [在代码中生成](https://github.com/NSwag/NSwag/wiki/SwaggerToCSharpClientGenerator)

* [通过 T4 模板生成](https://github.com/NSwag/NSwag/wiki/T4)

## <a name="customization"></a>自定义

### <a name="xml-comments"></a>XML 注释

可使用以下方法启用 XML 注释：

#### <a name="visual-studiotabvisual-studio-xml"></a>[Visual Studio](#tab/visual-studio-xml/)
* 右键单击“解决方案资源管理器”中的项目，然后选择“属性”
* 查看“生成”选项卡的“输出”部分下的“XML 文档文件”框：

![项目属性的“生成”选项卡](web-api-help-pages-using-swagger/_static/swagger-xml-comments.png)

#### <a name="visual-studio-for-mactabvisual-studio-mac-xml"></a>[Visual Studio for Mac](#tab/visual-studio-mac-xml/)
* 打开“项目选项”对话框 >“生成” > “编译器”
* 查看“常规选项”部分下的“生成 xml 文档”框：

![项目选项的“常规选项”部分](web-api-help-pages-using-swagger/_static/swagger-xml-comments-mac.png)

#### <a name="visual-studio-codetabvisual-studio-code-xml"></a>[Visual Studio Code](#tab/visual-studio-code-xml/)
将以下代码片段手动添加到 .csproj 文件：

[!code-xml[](../tutorials/web-api-help-pages-using-swagger/samples/TodoApi.NSwag/TodoApiNSwag.csproj?range=7-9)]

* * *
## <a name="data-annotations"></a>数据注释

NSwag 使用[反射](/dotnet/csharp/programming-guide/concepts/reflection)，Web API 操作的最佳做法是返回 [IActionResult](/dotnet/api/microsoft.aspnetcore.mvc.iactionresult)。 因此，NSwag 无法推断正在执行的操作和返回的结果。 请看下面的示例：

```csharp
public IActionResult Create([FromBody] TodoItem item)
{
    if (item == null)
    {
        return BadRequest();
    }

    _context.TodoItems.Add(item);
    _context.SaveChanges();

     return CreatedAtRoute("GetTodo", new { id = item.Id }, item);
}
```

上述操作返回 `IActionResult`，但在操作内部返回 [CreatedAtRoute](/dotnet/api/system.web.http.apicontroller.createdatroute) 或 [BadRequest](/dotnet/api/system.web.http.apicontroller.badrequest)。 使用数据注释告知客户端此操作返回的 HTTP 响应。 使用以下属性修饰该操作：

```csharp
[HttpPost]
[ProducesResponseType(typeof(TodoItem), 201)] // Created
[ProducesResponseType(typeof(TodoItem), 400)] // BadRequest
public IActionResult Create([FromBody] TodoItem item)
```

Swagger 生成器现在可准确地描述此操作，且生成的客户端知道调用终结点时收到的内容。 强烈建议使用这些属性来修饰所有操作。 有关 API 操作应返回的 HTTP 响应的指导原则，请参阅 [RFC 7231 规范](https://tools.ietf.org/html/rfc7231#section-4.3)。
