::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]

前面的代码定义了没有方法的 API 控制器类。 在接下来的部分中，将添加方法来实现 API。
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]

前面的代码定义了没有方法的 API 控制器类。 在接下来的部分中，将添加方法来实现 API。 采用 `[ApiController]` 特性批注类，以启用一些方便的功能。 若要详细了解由这些特性启用的功能，请参阅[使用 ApiControllerAttribute 批注类](xref:web-api/index#annotate-class-with-apicontrollerattribute)。
::: moniker-end

控制器的构造函数使用[依赖关系注入](xref:fundamentals/dependency-injection)将数据库上下文 (`TodoContext`) 注入到控制器中。 数据库上下文将在控制器中的每个 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 方法中使用。 构造函数将一个项（如果不存在）添加到内存数据库。

## <a name="get-to-do-items"></a>获取待办事项

若要获取待办事项，请将下面的方法添加到 `TodoController` 类中：

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]
::: moniker-end

这些方法实现两种 GET 方法：

* `GET /api/todo`
* `GET /api/todo/{id}`

以下是 `GetAll` 方法的 HTTP 响应示例：

```json
[
  {
    "id": 1,
    "name": "Item1",
    "isComplete": false
  }
]
```

稍后将在本教程中演示如何使用 [Postman](https://www.getpostman.com/) 或 [curl](https://curl.haxx.se/docs/manpage.html) 查看 HTTP 响应。

### <a name="routing-and-url-paths"></a>路由和 URL 路径

`[HttpGet]` 特性表示对 HTTP GET 请求进行响应的方法。 每个方法的 URL 路径构造如下所示：

* 在控制器的 `Route` 属性中采用模板字符串：

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]
::: moniker-end

* 将 `[controller]` 替换为控制器的名称，即在控制器类名称中去掉“Controller”后缀。 对于此示例，控制器类名称为“Todo”控制器，根名称为“todo”。 ASP.NET Core [路由](xref:mvc/controllers/routing)不区分大小写。
* 如果 `[HttpGet]` 特性具有路由模板（如 `[HttpGet("/products")]`），则将它追加到路径。 此示例不使用模板。 有关详细信息，请参阅[使用 Http [Verb] 特性的特性路由](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes)。

在下面的 `GetById` 方法中，`"{id}"` 是待办事项的唯一标识符的占位符变量。 调用 `GetById` 时，它会将 URL 中 `"{id}"` 的值分配给方法的 `id` 参数。

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end

`Name = "GetTodo"` 创建具名路由。 具名路由：

* 使应用程序使用路由名称创建 HTTP 链接。
* 将在本教程的后续部分中介绍。

### <a name="return-values"></a>返回值

`GetAll` 方法返回一个 `TodoItem` 对象的集合。 MVC 自动将对象序列化为 [JSON](https://www.json.org/)，并将 JSON 写入响应消息的正文中。 在假设没有未经处理的异常的情况下，此方法的响应代码为 200。 未经处理的异常将转换为 5xx 错误。

::: moniker range="<= aspnetcore-2.0"
相反，`GetById` 方法返回多个常规的 [IActionResult 类型](xref:web-api/action-return-types#iactionresult-type)，它表示一系列返回类型。 `GetById` 具有两个不同的返回类型：

* 如果没有任何项与请求的 ID 匹配，此方法将返回 404 错误。 返回 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 可以返回 HTTP 404 响应。
* 否则，此方法将返回具有 JSON 响应正文的 200。 返回 [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok)，则产生 HTTP 200 响应。
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
相反，`GetById` 方法返回多个 [ActionResult\<T> 类型](xref:web-api/action-return-types#actionresultt-type)，它表示一系列返回类型。 `GetById` 具有两个不同的返回类型：

* 如果没有任何项与请求的 ID 匹配，此方法将返回 404 错误。 返回 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 可以返回 HTTP 404 响应。
* 否则，此方法将返回具有 JSON 响应正文的 200。 返回 `item` 则产生 HTTP 200 响应。
::: moniker-end
