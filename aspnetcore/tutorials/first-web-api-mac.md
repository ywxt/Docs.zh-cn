---
title: 使用 ASP.NET Core 和 Visual Studio for Mac 创建 Web API
author: rick-anderson
description: 使用 ASP.NET Core MVC 和 Visual Studio for Mac 创建 Web API
helpviewer_heywords: ASP.NET Core, WebAPI, Web API, REST, mac, macOS, HTTP, Service, HTTP Service
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/08/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: tutorials/first-web-api-mac
ms.openlocfilehash: 699fbbf54abf1dc5c4156c559761110cdb375558
ms.sourcegitcommit: c867d7427bd4a88a78b2322e156367733b532730
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2018
ms.locfileid: "33923199"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-mac"></a>使用 ASP.NET Core 和 Visual Studio for Mac 创建 Web API

作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)

本教程将生成一个用于管理“待办事项”列表的 Web API。 不构造 UI。

本教程提供 3 个版本：

* macOS：使用 Visual Studio for Mac 创建 Web API（本教程）
* Windows：[使用 Visual Studio for Windows 创建 Web API](xref:tutorials/first-web-api)
* macOS、Linux、Windows：[使用 Visual Studio Code 创建 Web API](xref:tutorials/web-api-vsc)

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[template files](../includes/webApi/intro.md)]

请参阅 [macOS 或 Linux 上的 ASP.NET Core MVC 介绍](xref:tutorials/first-mvc-app-xplat/index)，获取使用永久数据库的示例。

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/net-core-prereqs-macos.md)]

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中，选择“文件” > “新建解决方案”。

![macOS 新建解决方案](first-web-api-mac/_static/sln.png)

选择“.NET Core App” > “ASP.NET Core Web API” > “下一步”。

![macOS“新建项目”对话框](first-web-api-mac/_static/1.png)

输入“TodoApi”作为“项目名称”，然后选择“创建”。

![配置对话框](first-web-api-mac/_static/2.png)

### <a name="launch-the-app"></a>启动应用

在 Visual Studio 中，选择“运行” > “开始执行(调试)”启动应用。 Visual Studio 启动浏览器并导航到 `http://localhost:5000`。 将收到 HTTP 404（未找到）错误。 将 URL 更改为 `http://localhost:<port>/api/values`。 `ValuesController` 数据已显示：

```json
["value1","value2"]
```

### <a name="add-support-for-entity-framework-core"></a>添加对 Entity Framework Core 的支持

安装 [Entity Framework Core InMemory](/ef/core/providers/in-memory/) 数据库提供程序。 此数据库提供程序允许将 Entity Framework Core 和内存数据库一起使用。

* 从“项目”菜单中，选择“添加 NuGet 包”。

  * 或者，可以右键单击“依赖项”，然后选择“添加包”。

* 在搜索框中输入 `EntityFrameworkCore.InMemory`。
* 选择 `Microsoft.EntityFrameworkCore.InMemory`，然后选择“添加包”。

### <a name="add-a-model-class"></a>添加模型类

模型是表示应用中的数据的对象。 在此示例中，唯一的模型是待办事项。

在解决方案资源管理器中，右键单击项目。 选择“添加” > “新建文件夹”。 将文件夹命名为“Models”。

![新建文件夹](first-web-api-mac/_static/folder.png)

> [!NOTE]
> 可将模型类置于项目的任意位置，但按照惯例会使用“模型”文件夹。

右键单击“Models”文件夹，然后选择“添加” > “新建文件” > “常规” > “空类”。 将类命名为“TodoItem”，然后单击“新建”。

将生成的代码替换为：

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

创建 `TodoItem` 时，数据库将生成 `Id`。

### <a name="create-the-database-context"></a>创建数据库上下文

数据库上下文是为给定数据模型协调 Entity Framework 功能的主类。 可以通过继承 `Microsoft.EntityFrameworkCore.DbContext` 类的方式创建此类。

将 `TodoContext` 类添加到“Models”文件夹。

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

## <a name="add-a-controller"></a>添加控制器

在解决方案资源管理器的“控制器”文件夹中，添加 `TodoController` 类。

将生成的代码替换为以下代码：

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a>启动应用

在 Visual Studio 中，选择“运行” > “开始执行(调试)”启动应用。 Visual Studio 启动浏览器并导航到 `http://localhost:<port>`，其中 `<port>` 是随机选择的端口号。 将收到 HTTP 404（未找到）错误。 将 URL 更改为 `http://localhost:<port>/api/values`。 `ValuesController` 数据已显示：

```json
["value1","value2"]
```

导航到位于 `http://localhost:<port>/api/todo` 的 `Todo` 控制器。 会返回以下 JSON：

```json
[{"key":1,"name":"Item1","isComplete":false}]
```

## <a name="implement-the-other-crud-operations"></a>实现其他的 CRUD 操作

我们将向控制器添加 `Create`、`Update` 和 `Delete` 方法。 这些方法是主题的变体，因此在这里只提供代码并突出显示主要的差异。 添加或更改代码后生成项目。

### <a name="create"></a>创建

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

上述方法响应至 HTTP POST，由 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性指示。 [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 特性告诉 MVC 从 HTTP 请求正文获取待办事项的值。
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

上述方法响应至 HTTP POST，由 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性指示。 MVC 从 HTTP 请求正文获取待办事项的值。
::: moniker-end

`CreatedAtRoute` 方法返回 201 响应。 201 响应是在服务器上创建新资源的 HTTP POST 方法的标准响应。 `CreatedAtRoute` 还会向响应添加位置标头。 位置标头指定新建的待办事项的 URI。 请参阅 [10.2.2 201 已创建](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。

### <a name="use-postman-to-send-a-create-request"></a>使用 Postman 发送创建请求

* 启动应用（“运行” > “开始执行(调试)”）。
* 打开 Postman。

![Postman 控制台](first-web-api/_static/pmc.png)

* 更新 localhost URL 中的端口号。
* 将 HTTP 方法设置为 POST。
* 单击“正文”选项卡。
* 选择“原始”单选按钮。
* 将类型设置为 JSON (application/json)
* 输入包含待办事项的请求正文，类似以下 JSON：

```json
{
  "name":"walk dog",
  "isComplete":true
}
```

* 单击“发送”按钮。

::: moniker range=">= aspnetcore-2.1"
> [!TIP]
> 如果单击“发送”后没有响应，则禁用“SSL 证书验证”选项。 在“文件” > “设置”下可以找到该选项 在禁用该设置后，再次单击“发送”按钮。
::: moniker-end

单击“响应”窗格中的“标头”选项卡，然后复制位置标头值：

![Postman 控制台的“标头”选项卡](first-web-api/_static/pmc2.png)

可以使用此位置标头 URI 访问创建的资源。 `Create` 方法返回 [CreatedAtRoute](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.createdatroute#Microsoft_AspNetCore_Mvc_ControllerBase_CreatedAtRoute_System_String_System_Object_System_Object_)。 传递至 `CreatedAtRoute` 的第一个参数代表用于生成 URL 的命名路由。 请回想一下，`GetById` 方法创建的 `"GetTodo"` 命令路由：

```csharp
[HttpGet("{id}", Name = "GetTodo")]
```

### <a name="update"></a>更新

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end

`Update` 与 `Create` 类似，但是使用的是 HTTP PUT。 响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。 根据 HTTP 规范，PUT 请求需要客户端发送整个更新的实体，而不仅仅是增量。 若要支持部分更新，请使用 HTTP PATCH。

```json
{
  "key": 1,
  "name": "walk dog",
  "isComplete": true
}
```

![显示 204（无内容）响应的 Postman 控制台](first-web-api/_static/pmcput.png)

### <a name="delete"></a>删除

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。

![显示 204（无内容）响应的 Postman 控制台](first-web-api/_static/pmd.png)

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
