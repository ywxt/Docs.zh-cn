## <a name="implement-the-other-crud-operations"></a><span data-ttu-id="16e42-101">实现其他的 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="16e42-101">Implement the other CRUD operations</span></span>

<span data-ttu-id="16e42-102">在以下部分中，将 `Create`、`Update` 和 `Delete` 方法添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="16e42-102">In the following sections, `Create`, `Update`, and `Delete` methods are added to the controller.</span></span>

### <a name="create"></a><span data-ttu-id="16e42-103">创建</span><span class="sxs-lookup"><span data-stu-id="16e42-103">Create</span></span>

<span data-ttu-id="16e42-104">添加以下 `Create` 方法。</span><span class="sxs-lookup"><span data-stu-id="16e42-104">Add the following `Create` method.</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Create)]

<span data-ttu-id="16e42-105">前面的代码是 HTTP POST 方法，通过 [`[HttpPost]`](/aspnet/core/api/microsoft.aspnetcore.mvc.httppostattribute) 属性指示。</span><span class="sxs-lookup"><span data-stu-id="16e42-105">The preceding code is an HTTP POST method, indicated by the [`[HttpPost]`](/aspnet/core/api/microsoft.aspnetcore.mvc.httppostattribute) attribute.</span></span> <span data-ttu-id="16e42-106">[`[FromBody]`](/aspnet/core/api/microsoft.aspnetcore.mvc.frombodyattribute) 特性告诉 MVC 从 HTTP 请求正文获取待办事项的值。</span><span class="sxs-lookup"><span data-stu-id="16e42-106">The [`[FromBody]`](/aspnet/core/api/microsoft.aspnetcore.mvc.frombodyattribute) attribute tells MVC to get the value of the to-do item from the body of the HTTP request.</span></span>

<span data-ttu-id="16e42-107">`CreatedAtRoute` 方法：</span><span class="sxs-lookup"><span data-stu-id="16e42-107">The `CreatedAtRoute` method:</span></span>

* <span data-ttu-id="16e42-108">返回 201 响应。</span><span class="sxs-lookup"><span data-stu-id="16e42-108">Returns a 201 response.</span></span> <span data-ttu-id="16e42-109">HTTP 201 是在服务器上创建新资源的 HTTP POST 方法的标准响应。</span><span class="sxs-lookup"><span data-stu-id="16e42-109">HTTP 201 is the standard response for an HTTP POST method that creates a new resource on the server.</span></span>
* <span data-ttu-id="16e42-110">向响应添加位置标头。</span><span class="sxs-lookup"><span data-stu-id="16e42-110">Adds a Location header to the response.</span></span> <span data-ttu-id="16e42-111">位置标头指定新建的待办事项的 URI。</span><span class="sxs-lookup"><span data-stu-id="16e42-111">The Location header specifies the URI of the newly created to-do item.</span></span> <span data-ttu-id="16e42-112">请参阅 [10.2.2 201 已创建](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)。</span><span class="sxs-lookup"><span data-stu-id="16e42-112">See [10.2.2 201 Created](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).</span></span>
* <span data-ttu-id="16e42-113">使用名为 route 的“GetTodo”来创建 URL。</span><span class="sxs-lookup"><span data-stu-id="16e42-113">Uses the "GetTodo" named route to create the URL.</span></span> <span data-ttu-id="16e42-114">已在 `GetById` 中定义名为 route 的“GetTodo”：</span><span class="sxs-lookup"><span data-stu-id="16e42-114">The "GetTodo" named route is defined in `GetById`:</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]

### <a name="use-postman-to-send-a-create-request"></a><span data-ttu-id="16e42-115">使用 Postman 发送创建请求</span><span class="sxs-lookup"><span data-stu-id="16e42-115">Use Postman to send a Create request</span></span>

![Postman 控制台](../../tutorials/first-web-api/_static/pmc.png)

* <span data-ttu-id="16e42-117">将 HTTP 方法设置为 `POST`</span><span class="sxs-lookup"><span data-stu-id="16e42-117">Set the HTTP method to `POST`</span></span>
* <span data-ttu-id="16e42-118">选择“Body”单选按钮</span><span class="sxs-lookup"><span data-stu-id="16e42-118">Select the **Body** radio button</span></span>
* <span data-ttu-id="16e42-119">选择“raw”单选按钮</span><span class="sxs-lookup"><span data-stu-id="16e42-119">Select the **raw** radio button</span></span>
* <span data-ttu-id="16e42-120">将类型设置为 JSON</span><span class="sxs-lookup"><span data-stu-id="16e42-120">Set the type to JSON</span></span>
* <span data-ttu-id="16e42-121">在键值编辑器中，输入一个待办事项，例如</span><span class="sxs-lookup"><span data-stu-id="16e42-121">In the key-value editor, enter a Todo item such as</span></span>

```json
{
    "name":"walk dog",
    "isComplete":true
}
```

* <span data-ttu-id="16e42-122">选择“Send”</span><span class="sxs-lookup"><span data-stu-id="16e42-122">Select **Send**</span></span>
* <span data-ttu-id="16e42-123">选择下窗格中的“Header”选项卡，然后复制“Location”标头：</span><span class="sxs-lookup"><span data-stu-id="16e42-123">Select the Headers tab in the lower pane and copy the **Location** header:</span></span>

![Postman 控制台的“标头”选项卡](../../tutorials/first-web-api/_static/pmget.png)

<span data-ttu-id="16e42-125">位置标头 URI 可用于访问新项。</span><span class="sxs-lookup"><span data-stu-id="16e42-125">The Location header URI can be used to access the new item.</span></span>

### <a name="update"></a><span data-ttu-id="16e42-126">更新</span><span class="sxs-lookup"><span data-stu-id="16e42-126">Update</span></span>

<span data-ttu-id="16e42-127">添加以下 `Update` 方法：</span><span class="sxs-lookup"><span data-stu-id="16e42-127">Add the following `Update` method:</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Update)]

<span data-ttu-id="16e42-128">`Update` 与 `Create` 类似，但是使用的是 HTTP PUT。</span><span class="sxs-lookup"><span data-stu-id="16e42-128">`Update` is similar to `Create`, but uses HTTP PUT.</span></span> <span data-ttu-id="16e42-129">响应是 [204（无内容）](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="16e42-129">The response is [204 (No Content)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span> <span data-ttu-id="16e42-130">根据 HTTP 规范，PUT 请求需要客户端发送整个更新的实体，而不仅仅是增量。</span><span class="sxs-lookup"><span data-stu-id="16e42-130">According to the HTTP spec, a PUT request requires the client to send the entire updated entity, not just the deltas.</span></span> <span data-ttu-id="16e42-131">若要支持部分更新，请使用 HTTP PATCH。</span><span class="sxs-lookup"><span data-stu-id="16e42-131">To support partial updates, use HTTP PATCH.</span></span>

![显示 204（无内容）响应的 Postman 控制台](../../tutorials/first-web-api/_static/pmcput.png)

### <a name="delete"></a><span data-ttu-id="16e42-133">删除</span><span class="sxs-lookup"><span data-stu-id="16e42-133">Delete</span></span>

<span data-ttu-id="16e42-134">添加以下 `Delete` 方法：</span><span class="sxs-lookup"><span data-stu-id="16e42-134">Add the following `Delete` method:</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_Delete)]

<span data-ttu-id="16e42-135">`Delete` 响应是 [204（无内容）](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)。</span><span class="sxs-lookup"><span data-stu-id="16e42-135">The `Delete` response is [204 (No Content)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html).</span></span>

<span data-ttu-id="16e42-136">测试 `Delete`：</span><span class="sxs-lookup"><span data-stu-id="16e42-136">Test `Delete`:</span></span> 

![显示 204（无内容）响应的 Postman 控制台](../../tutorials/first-web-api/_static/pmd.png)
