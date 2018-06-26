## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="94544-101">实现其他的 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="94544-101">Implement the other CRUD operations</span></span>

<span data-ttu-id="94544-102">在以下部分中，将 `Create`、`Update` 和 `Delete` 方法添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="94544-102">In the following sections, `Create`, `Update`, and `Delete` methods are added to the controller.</span></span>

### <a name="create"></a><span data-ttu-id="94544-103">创建</span><span class="sxs-lookup"><span data-stu-id="94544-103">Create</span></span>

<span data-ttu-id="94544-104">添加以下 `Create` 方法：</span><span class="sxs-lookup"><span data-stu-id="94544-104">Add the following `Create` method:</span></span>

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="94544-105">正如 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性所指示，前面的代码是 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="94544-105">The preceding code is an HTTP POST method, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="94544-106">[[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) 特性告诉 MVC 从 HTTP 请求正文获取待办事项的值。</span><span class="sxs-lookup"><span data-stu-id="94544-106">The [[FromBody]](/dotnet/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="94544-107">正如 [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) 属性所指示，前面的代码是 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="94544-107">The preceding code is an HTTP POST method, as indicated by the [[HttpPost]](/dotnet/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="94544-108">MVC 从 HTTP 请求正文获取待办事项的值。</span><span class="sxs-lookup"><span data-stu-id="94544-108">MVC gets the value of the to-do item from the body of the HTTP request.</span></span>
::: moniker-end

<span data-ttu-id="94544-109">`CreatedAtRoute` 方法：</span><span class="sxs-lookup"><span data-stu-id="94544-109">The `CreatedAtRoute` method:</span></span>

* <span data-ttu-id="94544-110">返回 201 响应。</span><span class="sxs-lookup"><span data-stu-id="94544-110">Returns a 201 response.</span></span> <span data-ttu-id="94544-111">HTTP 201 是在服务器上创建新资源的 HTTP POST 方法的标准响应。</span><span class="sxs-lookup"><span data-stu-id="94544-111">HTTP 201 is the standard response for an HTTP POST method that creates a new resource on the server.</span></span>
* <span data-ttu-id="94544-112">向响应添加位置标头。</span><span class="sxs-lookup"><span data-stu-id="94544-112">Adds a Location header to the response.</span></span> <span data-ttu-id="94544-113">位置标头指定新建的待办事项的 URI。</span><span class="sxs-lookup"><span data-stu-id="94544-113">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="94544-114">请参阅 [10.2.2 201 已创建](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。</span><span class="sxs-lookup"><span data-stu-id="94544-114">See [10.2.2 201 Created](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>
* <span data-ttu-id="94544-115">使用名为 route 的“GetTodo”来创建 URL。</span><span class="sxs-lookup"><span data-stu-id="94544-115">Uses the "GetTodo" named route to create the URL.</span></span> <span data-ttu-id="94544-116">已在 `GetById` 中定义名为 route 的“GetTodo”：</span><span class="sxs-lookup"><span data-stu-id="94544-116">The "GetTodo" named route is defined in `GetById`:</span></span>

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]
::: moniker-end

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="94544-117">使用 Postman 发送创建请求</span><span class="sxs-lookup"><span data-stu-id="94544-117">Use Postman to send a Create request</span></span>

* <span data-ttu-id="94544-118">启动该应用程序。</span><span class="sxs-lookup"><span data-stu-id="94544-118">Start the app.</span></span>
* <span data-ttu-id="94544-119">打开 Postman。</span><span class="sxs-lookup"><span data-stu-id="94544-119">Open Postman.</span></span>

![Postman 控制台](../../tutorials/first-web-api/_static/pmc.png)

* <span data-ttu-id="94544-121">更新 localhost URL 中的端口号。</span><span class="sxs-lookup"><span data-stu-id="94544-121">Update the port number in the localhost URL.</span></span>
* <span data-ttu-id="94544-122">将 HTTP 方法设置为 POST。</span><span class="sxs-lookup"><span data-stu-id="94544-122">Set the HTTP method to *POST*.</span></span>
* <span data-ttu-id="94544-123">单击“正文”选项卡。</span><span class="sxs-lookup"><span data-stu-id="94544-123">Click the **Body** tab.</span></span>
* <span data-ttu-id="94544-124">选择“原始”单选按钮。</span><span class="sxs-lookup"><span data-stu-id="94544-124">Select the **raw** radio button.</span></span>
* <span data-ttu-id="94544-125">将类型设置为 JSON (application/json)</span><span class="sxs-lookup"><span data-stu-id="94544-125">Set the type to *JSON (application/json)*.</span></span>
* <span data-ttu-id="94544-126">输入包含待办事项的请求正文，类似以下 JSON：</span><span class="sxs-lookup"><span data-stu-id="94544-126">Enter a request body with a to-do item resembling the following JSON:</span></span>

```json
{
  "name":"walk dog",
  "isComplete":true
}
```

* <span data-ttu-id="94544-127">单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="94544-127">Click the **Send** button.</span></span>

::: moniker range=">= aspnetcore-2.1"
> [!TIP]
> <span data-ttu-id="94544-128">如果单击“发送”后没有响应，则禁用“SSL 证书验证”选项。</span><span class="sxs-lookup"><span data-stu-id="94544-128">If no response displays after clicking **Send**, disable the **SSL certification verification** option.</span></span> <span data-ttu-id="94544-129">在“文件” > “设置”下可以找到该选项</span><span class="sxs-lookup"><span data-stu-id="94544-129">This is found under **File** > **Settings**.</span></span> <span data-ttu-id="94544-130">在禁用该设置后，再次单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="94544-130">Click the **Send** button again after disabling the setting.</span></span>
::: moniker-end

<span data-ttu-id="94544-131">单击“响应”窗格中的“标头”选项卡，然后复制位置标头值：</span><span class="sxs-lookup"><span data-stu-id="94544-131">Click the **Headers** tab in the **Response** pane and copy the **Location** header value:</span></span>

![Postman 控制台的“标头”选项卡](../../tutorials/first-web-api/_static/pmc2.png)

<span data-ttu-id="94544-133">位置标头 URI 可用于访问新项。</span><span class="sxs-lookup"><span data-stu-id="94544-133">The Location header URI can be used to access the new item.</span></span>

### <a name="update"></a><span data-ttu-id="94544-134">更新</span><span class="sxs-lookup"><span data-stu-id="94544-134">Update</span></span>

<span data-ttu-id="94544-135">添加以下 `Update` 方法：</span><span class="sxs-lookup"><span data-stu-id="94544-135">Add the following `Update` method:</span></span>

::: moniker range="<= aspnetcore-2.0"
[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]
::: moniker-end

<span data-ttu-id="94544-136">`Update` 与 `Create` 类似，但是使用的是 HTTP PUT。</span><span class="sxs-lookup"><span data-stu-id="94544-136">`Update` is similar to `Create`, except it uses HTTP PUT.</span></span> <span data-ttu-id="94544-137">响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="94544-137">The response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="94544-138">根据 HTTP 规范，PUT 请求需要客户端发送整个更新的实体，而不仅仅是增量。</span><span class="sxs-lookup"><span data-stu-id="94544-138">According to the HTTP specification, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="94544-139">若要支持部分更新，请使用 HTTP PATCH。</span><span class="sxs-lookup"><span data-stu-id="94544-139">To support partial updates, use HTTP PATCH.</span></span>

<span data-ttu-id="94544-140">使用 Postman 将待办事项的名称更新为“带猫出去散步”：</span><span class="sxs-lookup"><span data-stu-id="94544-140">Use Postman to update the to-do item's name to "walk cat":</span></span>

![显示 204（无内容）响应的 Postman 控制台](../../tutorials/first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="94544-142">删除</span><span class="sxs-lookup"><span data-stu-id="94544-142">Delete</span></span>

<span data-ttu-id="94544-143">添加以下 `Delete` 方法：</span><span class="sxs-lookup"><span data-stu-id="94544-143">Add the following `Delete` method:</span></span>

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="94544-144">`Delete` 响应是 [204（无内容）](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="94544-144">The `Delete` response is [204 (No Content)](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

<span data-ttu-id="94544-145">使用 Postman 删除待办事项：</span><span class="sxs-lookup"><span data-stu-id="94544-145">Use Postman to delete the to-do item:</span></span>

![显示 204（无内容）响应的 Postman 控制台](../../tutorials/first-web-api/_static/pmd.png)
