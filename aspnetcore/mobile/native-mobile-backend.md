---
title: "创建本地移动应用程序的后端服务"
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
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
# <a name="creating-backend-services-for-native-mobile-applications"></a>创建本地移动应用程序的后端服务

作者：[Steve Smith](https://ardalis.com/)

移动应用可以轻松地与 ASP.NET Core 后端服务进行通信。

[查看或下载后端服务的示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/mobile/native-mobile-backend/sample)

## <a name="the-sample-native-mobile-app"></a>示例本地移动应用程序

本教程演示如何使用 ASP.NET Core MVC 创建支持本地移动应用的后端服务。 它使用[Xamarin Forms ToDoRest 应用](https://developer.xamarin.com/guides/xamarin-forms/web-services/consuming/rest/)作为其本地客户端，包括 Android、 iOS、 Windows 通用和 Window Phone 设备的本地客户端。 你可以遵循链接的教程来创建本地应用程序 （并安装所需的可用 Xamarin 工具），也可以下载 Xamarin 示例解决方案。 Xamarin 示例包含一个 ASP.NET Web API 2 服务项目，本文中使用 ASP.NET Core 应用替换 （不需要更改客户端）。

![在 Android 智能手机上运行的执行操作的 Rest 应用程序](native-mobile-backend/_static/todo-android.png)

### <a name="features"></a>功能

ToDoRest 应用支持列出、 添加、 删除和更新待办事项。 每个项都有一个 ID、 名称、 说明以及指示该项是否已完成的属性。

待办事项的主视图，如上所说，列出每个项的名称，并用标记指示它是否完成。

点击`+`图标可打开添加项对话框：

![添加项对话框](native-mobile-backend/_static/todo-android-new-item.png)

点击主列表屏幕上的项将打开编辑对话框，可以在其中修改项的名称、 说明以及修改是否完成标识，或删除项目：

![编辑项对话框](native-mobile-backend/_static/todo-android-edit-item.png)

此示例默认使用托管在 developer.xamarin.com 的后端服务，是只读的。 若想在你的计算机上运行测试下一节创建的 ASP.NET Core 应用，你将需要更改应用程序的`RestUrl`常量。 转到`ToDoREST`项目，然后打开*Constants.cs*文件。 使用您的计算机 IP 的 URL 地址 （不 localhost 或 127.0.0.1，因为此地址用于从设备模拟器中访问，不是直接从您的计算机上访问）包括端口号 (5000) 替换`RestUrl`。 为了在测试设备中运行你的服务，请确保你的防火墙没有阻止访问此端口。

```csharp
// URL of REST service (Xamarin ReadOnly Service)
//public static string RestUrl = "http://developer.xamarin.com:8081/api/todoitems{0}";

// use your machine's IP address
public static string RestUrl = "http://192.168.1.207:5000/api/todoitems/{0}";
```

## <a name="creating-the-aspnet-core-project"></a>创建 ASP.NET Core 项目

在 Visual Studio 中创建一个新的 ASP.NET Core Web 应用程序。 选择 Web API 模板和无身份验证。 将项目命名为*ToDoApi*。

![与选择的 Web API 项目模板的新建 ASP.NET Web 应用程序对话框](native-mobile-backend/_static/web-api-template.png)

应用程序应响应发向 5000 端口的所有请求。 更改*Program.cs*加入`.UseUrls("http://*:5000")`来实现此目的：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Program.cs?range=10-16&highlight=3)]

> [!NOTE]
> 请确保您是直接运行而不是在 IIS Express 中运行应用程序，IIS Express 将默认忽略非本地请求。 从命令提示符处运行`dotnet run`，或从 Visual Studio 工具栏的调试目标下拉列表中选择以应用程序名称命名的配置文件。

添加一个模型类来表示待办事项。 使用`[Required]`特性标记所需字段：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Models/ToDoItem.cs)]

API 方法需要某种方式处理数据。 使用与 Xamarin 初始示例相同的`IToDoRepository`接口：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Interfaces/IToDoRepository.cs)]

为此示例中，接口的实现只需使用私有的待办事项集合：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Services/ToDoRepository.cs)]

在*Startup.cs*配置中的实现:

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Startup.cs?highlight=6&range=29-35)]

现在，你可以 创建*ToDoItemsController*。

> [!TIP]
> 了解更多有关创建 web Api 中的信息可参阅[构建您第一个 Web API 使用 ASP.NET Core MVC 和 Visual Studio](../tutorials/first-web-api.md)。

## <a name="creating-the-controller"></a>创建控制器

添加*ToDoItemsController*新控制器到项目中 。 它应继承自 Microsoft.AspNetCore.Mvc.Controller。 添加`Route`特性以指示控制器将处理路径以`api/todoitems`开头的请求。 路由中的`[controller]`标记会取代为控制器的名称 (省略`Controller`后缀)，对全局路由特别有用。 可以详细了解[路由](../fundamentals/routing.md)。

控制器构造函数需要`IToDoRepository`类型的实例。 在运行时，此实例将由框架支持的[依赖注入](../fundamentals/dependency-injection.md)提供。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=1-17&highlight=9,14)]

此 API 支持四个不同的 HTTP 方法对数据源执行 CRUD （创建、 读取、 更新、 删除） 操作。 其中最简单的是读取操作，它对应于 HTTP GET 请求。

### <a name="reading-items"></a>正在读取项目

可使用导向 `List` 方法的 GET 请求得到项列表。 `[HttpGet]`特性指出`List`操作方法应仅处理 GET 请求。 此操作的路由就是在控制器上指定的路由。 你不一定需要将操作名称用作的路由的一部分。 你只需确保每个操作都有唯一且明确的路由。 路由特性可以应用在控制器和方法级别来生成特定的路由的。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=19-23)]

`List`方法返回 200 OK 响应代码和所有序列化为 JSON 的 ToDo 项。

你可以使用多种工具测试新 API 方法，如此处所示的[Postman](https://www.getpostman.com/docs/)：

![显示 todoitems 以及显示三个项返回的 JSON 响应正文的 GET 请求的 postman 控制台](native-mobile-backend/_static/postman-get.png)

### <a name="creating-items"></a>创建项

按照约定，创建新数据项对应 HTTP POST 方法。 `Create`方法具有`[HttpPost]`特性，并接受`ToDoItem`实例。 由于`item`将在 POST 正文中传递，所以此参数用`[FromBody]`特性修饰。

在方法中，会检查项的有效性和之前存在于数据存储，如果不出现任何问题，就会添加到使用中的存储库。 每个接受用户输入的 API 方法都应该使用`ModelState.IsValid`执行[模型验证](../mvc/models/validation.md)。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=25-46)]

该示例使用枚举保存传递到移动客户端的错误代码：

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=91-99)]

使用 Postman 选择 POST 方法测试添加新项，在请求正文中输入 JSON 格式的新对象。 你还应添加一个请求头指定`Content-Type`为`application/json`。

![显示 POST 和响应的 postman 控制台](native-mobile-backend/_static/postman-post.png)

该方法会在响应中返回新创建的项。

### <a name="updating-items"></a>更新项

修改记录使用 HTTP PUT 请求。 除此之外`Edit`方法是几乎与`Create`方法一样。 请注意，如果未找到记录，`Edit`操作方法将返回`NotFound`(404) 响应。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=48-69)]

使用 Postman 进行测试，更改为 PUT 方法。 在请求正文中指定的更新的对象数据。

![显示 PUT 和响应的 postman 控制台](native-mobile-backend/_static/postman-put.png)

为了与预先存在的 API 保持一致，执行成功时此方法返回`NoContent`(204) 响应，。

### <a name="deleting-items"></a>删除项目

删除记录可以通过向服务发出 DELETE 请求并传递要删除项的 ID 完成。 和更新项一样，当请求的项不存在，将返回`NotFound`响应。 请求成功则返回`NoContent`(204) 响应。

[!code-csharp[Main](native-mobile-backend/sample/ToDoApi/src/ToDoApi/Controllers/ToDoItemsController.cs?range=71-88)]

请注意，在测试的删除功能时，没有任何要求在请求正文中。

![显示一个删除和响应的 postman 控制台](native-mobile-backend/_static/postman-delete.png)

## <a name="common-web-api-conventions"></a>常见的 Web API 约定

开发你的应用程序后端服务时，你将想要附带一组一致的约定或策略来处理跨领域问题。 例如，在上面所示服务中，无法找到为请求特定的记录时返回`NotFound`响应，而不是`BadRequest`响应。 同样，对通过绑定的模型类型传递到此服务中命令始终检查`ModelState.IsValid`，并对无效的模型类型返回`BadRequest`。

一旦您为您的 Api 标识通用策略，你通常可以封装在[筛选器](../mvc/controllers/filters.md)中。 详细了解[如何封装 ASP.NET Core MVC 应用程序中的公用 API 策略](https://msdn.microsoft.com/magazine/mt767699.aspx)。
