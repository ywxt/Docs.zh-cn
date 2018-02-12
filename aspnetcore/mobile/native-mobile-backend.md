---
title: "为本机移动应用程序创建后端服务"
author: ardalis
description: 
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mobile/native-mobile-backend
ms.openlocfilehash: ff09f331cff5cca7b42fa89bff55c0ed5c7d82f4
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2018
---
# <a name="creating-backend-services-for-native-mobile-applications"></a>为本机移动应用程序创建后端服务

作者：[Steve Smith](https://ardalis.com/)

移动应用可与 ASP.NET Core 后端服务轻松通信。

[查看或下载后端服务代码示例](https://github.com/aspnet/Docs/tree/master/aspnetcore/mobile/native-mobile-backend/sample)

## <a name="the-sample-native-mobile-app"></a>本机移动应用示例

本教程演示如何使用 ASP.NET Core MVC 创建后端服务以支持本机移动应用。 它使用 [Xamarin Forms ToDoRest 应用](https://developer.xamarin.com/guides/xamarin-forms/web-services/consuming/rest/)作为其本机客户端，其中包括 Android、iOS、Windows 通用和 Windows Phone 设备各自的本机客户端。 可按照链接的教程创建本机应用（并安装必要的免费 Xamarin 工具），还可下载 Xamarin 示例解决方案。 Xamarin 示例中有一个 ASP.NET Web API 2 服务项目，该项目替换为本文的 ASP.NET Core 应用（客户端无需更改）。

![在 Android 智能手机上运行的 ToDoRest 应用程序](native-mobile-backend/_static/todo-android.png)

### <a name="features"></a>功能

ToDoRest 应用可用于列出、添加、删除和更新待办事项。 每一项都有 ID、名称、备注，还有一个指示该项是否完成的属性。

如上图所示，项的主视图列出每一项的名称，并用勾号指示该项是否完成。

点击 `+` 图标打开“添加项”对话框：

![“添加项”对话框](native-mobile-backend/_static/todo-android-new-item.png)

点击主列表屏幕上的项时，可打开“编辑”对话框，可在此处修改该项的名称、备注和完成状态设置，或删除该项：

![“编辑项”对话框](native-mobile-backend/_static/todo-android-edit-item.png)

此示例默认配置为使用 developer.xamarin.com 上托管的后端服务，该服务可用于只读操作。 若要针对计算机上运行的 ASP.NET Core 应用（在下一节中创建）对其进行测试，需要更新应用的 `RestUrl` 常数。 导航到 `ToDoREST` 项目并打开 Constants.cs 文件。 将 `RestUrl` 替换为具有计算机 IP 地址的 URL（非 localhost 或 127.0.0.1，因此从设备模拟器中使用此地址，而非从计算机上）。 同时还包括端口号 (5000)。 为测试设备能否使用你的服务，请保证活动的防火墙均未阻止此端口的访问。

```csharp
// URL of REST service (Xamarin ReadOnly Service)
//public static string RestUrl = "http://developer.xamarin.com:8081/api/todoitems{0}";

// use your machine's IP address
public static string RestUrl = "http://192.168.1.207:5000/api/todoitems/{0}";
```

## <a name="creating-the-aspnet-core-project"></a>创建 ASP.NET Core 项目

在 Visual Studio 中创建新的 ASP.NET Core Web 应用程序。 选择 Web API 模板和无身份验证。 将项目命名为 ToDoApi。

![“新建 ASP.NET Web 应用程序”对话框，其中已选中 Web API 项目模板](native-mobile-backend/_static/web-api-template.png)

对于向端口 5000 进行的请求，应用程序均需作出响应。 更新 Program.cs，使其包含 `.UseUrls("http://*:5000")`，以便实现以下操作：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Program.cs?range=10-16&highlight=3)]

> [!NOTE]
> 请务必直接运行应用程序，而不是通过 IIS Express 运行（该操作默认忽视非本地请求）。 从命令提示符处运行 `dotnet run`或者从 Visual Studio 工具栏的“调试目标”下拉列表中选择应用程序名称配置文件。

添加一个表示待办事项的模型类。 使用 `[Required]` 属性标记必填字段：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Models/ToDoItem.cs)]

API 方法需采用某种方式来处理数据。 使用原始 Xamarin 示例所用的 `IToDoRepository` 接口：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Interfaces/IToDoRepository.cs)]

在本例中，实现仅使用专用的项集合：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Services/ToDoRepository.cs)]

在 Startup.cs 中配置实现：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Startup.cs?highlight=6&range=29-35)]

现可创建 ToDoItemsController。

> [!TIP]
> 要深入了解如何创建 web API，请参阅[使用 ASP.NET Core MVC 和 Visual Studio 生成第一个 Web API](../tutorials/first-web-api.md)。

## <a name="creating-the-controller"></a>创建控制器

将新的控制器添加到项目 ToDoItemsController 中。 该项目应继承自 Microsoft.AspNetCore.Mvc.Controller。 添加 `Route` 属性，用于指示控制器将对以 `api/todoitems` 开头的路径的请求进行处理。 路由中的 `[controller]` 令牌替换为控制器名称（省略 `Controller` 后缀），该令牌特别适合全局路由。 详细了解[路由](../fundamentals/routing.md)。

控制器需要 `IToDoRepository` 才能正常运行；请通过控制器的构造函数请求此类型的实例。 运行时，将通过框架对[依赖关系注入](../fundamentals/dependency-injection.md)的支持提供此实例。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=1-17&highlight=9,14)]

该 API 支持 4 种不同的 Http 谓词在数据源上执行 CRUD（创建、读取、更新、删除）操作。 最简单的操作是读取，它响应 HTTP GET 请求。

### <a name="reading-items"></a>读取项目

通过向 `List` 方法发出 GET 请求来请求项目列表。 `List` 方法的 `[HttpGet]` 属性指示此操作应仅处理 GET 请求。 此操作的路由是控制器上指定的路由。 无需将操作名称用作路由的一部分。 只需确保每个操作均具有唯一且明确的路由。 可在控制器和方法级别上使用路由属性来生成特定的路由。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=19-23)]

`List` 方法返回 200 OK 响应代码和所有待办事项（序列化为 JSON）。

可使用多种工具（如 [Postman](https://www.getpostman.com/docs/)）来测试新的 API 方法，如下所示：

![Postman 控制台，其中显示一个 todoitem 的 GET 请求，以及显示所返回的三个项目的 JSON 的响应正文](native-mobile-backend/_static/postman-get.png)

### <a name="creating-items"></a>创建项目

按照约定，新建数据项即是映射到 HTTP POST 谓词。 `Create` 方法上应用了 `[HttpPost]` 属性并接受 `ToDoItem` 实例。 由于 `item` 实参将传递到 POST 正文中，因此该形参通过 `[FromBody]` 属性修饰。

在此方法中，检查项目是否有效以及之前是否存在于数据库中；如果未出现问题，则使用存储库添加此项目。 检查 `ModelState.IsValid` 时会检查[模型有效性](../mvc/models/validation.md)，且此操作在接受用户输入的每个 API 方法中执行。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=25-46)]

示例中使用一个枚举，后者包含传递到移动客户端的错误代码：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=91-99)]

通过选择在请求正文中以 JSON 格式提供新对象的 POST 谓词，测试能否使用 Postman 添加新项。 还应添加一个请求标头，该标头指定 `application/json` 的 `Content-Type`。

![显示 POST 和响应的 Postman 控制台](native-mobile-backend/_static/postman-post.png)

该方法返回在响应中新建的项。

### <a name="updating-items"></a>更新项目

使用 HTTP PUT 请求修改记录。 除了此项更改，`Edit` 方法与 `Create` 几乎相同。 请注意，如果未找到记录，`Edit` 操作将返回 `NotFound` (404) 响应。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=48-69)]

要使用 Postman 进行测试，请将谓词更改为 PUT。 在请求正文中指定更新后的对象数据。

![显示 PUT 和响应的 Postman 控制台](native-mobile-backend/_static/postman-put.png)

如果成功，此方法返回 `NoContent` (204) 响应，与预先存在的 API 保持一致。

### <a name="deleting-items"></a>删除项目

通过对服务做出 DELETE 请求并传递要删除的项的 ID 来删除项目。 与更新一样，请求不存在的项目将收到 `NotFound` 响应。 否则，成功的请求将收到 `NoContent` (204) 响应。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=71-88)]

请注意，测试删除功能时，请求正文中无需任何内容。

![显示 DELETE 和响应的 Postman 控制台](native-mobile-backend/_static/postman-delete.png)

## <a name="common-web-api-conventions"></a>常见的 Web API 约定

在为应用开发后端服务时，需要一套统一的约定或策略来处理相关问题。 例如，在以上所示的服务中，针对未找到的特定记录的请求收到了 `NotFound` 响应，而非 `BadRequest` 响应。 同样，针对在模型绑定类型中传递的服务发出的命令始终检查 `ModelState.IsValid` 并返回 `BadRequest` 以表示无效模型类型。

为 API 标识通用策略之后，通常可将其封装在[筛选器](../mvc/controllers/filters.md)中。 详细了解[如何将通用 API 策略封装在 ASP.NET Core MVC 应用程序中](https://msdn.microsoft.com/magazine/mt767699.aspx)。
