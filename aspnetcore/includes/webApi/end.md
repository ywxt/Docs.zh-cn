## <a name="implement-the-other-crud-operations"></a>实现其他的 CRUD 操作

在以下部分中，将 `Create`、`Update` 和 `Delete` 方法添加到控制器。

### <a name="create"></a>创建

添加以下 `Create` 方法：

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

正如 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性所指示，前面的代码是 HTTP POST 方法。 [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 特性告诉 MVC 从 HTTP 请求正文获取待办事项的值。
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

正如 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性所指示，前面的代码是 HTTP POST 方法。 MVC 从 HTTP 请求正文获取待办事项的值。
::: moniker-end

`CreatedAtRoute` 方法：

* 返回 201 响应。 HTTP 201 是在服务器上创建新资源的 HTTP POST 方法的标准响应。
* 向响应添加位置标头。 位置标头指定新建的待办事项的 URI。 请参阅 [10.2.2 201 已创建](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。
* 使用名为 route 的“GetTodo”来创建 URL。 已在 `GetById` 中定义名为 route 的“GetTodo”：

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end

### <a name="use-postman-to-send-a-create-request"></a>使用 Postman 发送创建请求

* 启动该应用程序。
* 打开 Postman。

![Postman 控制台](../../tutorials/first-web-api/_static/pmc.png)

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

![Postman 控制台的“标头”选项卡](../../tutorials/first-web-api/_static/pmc2.png)

位置标头 URI 可用于访问新项。

### <a name="update"></a>更新

添加以下 `Update` 方法：

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end

`Update` 与 `Create` 类似，但是使用的是 HTTP PUT。 响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。 根据 HTTP 规范，PUT 请求需要客户端发送整个更新的实体，而不仅仅是增量。 若要支持部分更新，请使用 HTTP PATCH。

使用 Postman 将待办事项的名称更新为“带猫出去散步”：

![显示 204（无内容）响应的 Postman 控制台](../../tutorials/first-web-api/_static/pmcput.png)

### <a name="delete"></a>删除

添加以下 `Delete` 方法：

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

`Delete` 响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。

使用 Postman 删除待办事项：

![显示 204（无内容）响应的 Postman 控制台](../../tutorials/first-web-api/_static/pmd.png)
