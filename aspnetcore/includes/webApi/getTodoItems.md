::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3b6f0-101">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-101">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span></span>

<span data-ttu-id="3b6f0-102">前面的代码定义了没有方法的 API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-102">The preceding code defines an API controller class without methods.</span></span> <span data-ttu-id="3b6f0-103">在接下来的部分中，将添加方法来实现 API。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-103">In the next sections, methods are added to implement the API.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3b6f0-104">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-104">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]</span></span>

<span data-ttu-id="3b6f0-105">前面的代码定义了没有方法的 API 控制器类。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-105">The preceding code defines an API controller class without methods.</span></span> <span data-ttu-id="3b6f0-106">在接下来的部分中，将添加方法来实现 API。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-106">In the next sections, methods are added to implement the API.</span></span> <span data-ttu-id="3b6f0-107">采用 `[ApiController]` 特性批注类，以启用一些方便的功能。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-107">The class is annotated with an `[ApiController]` attribute to enable some convenient features.</span></span> <span data-ttu-id="3b6f0-108">若要详细了解由这些特性启用的功能，请参阅[使用 ApiControllerAttribute 批注类](xref:web-api/index#annotate-class-with-apicontrollerattribute)。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-108">For information on features enabled by the attribute, see [Annotate class with ApiControllerAttribute](xref:web-api/index#annotate-class-with-apicontrollerattribute).</span></span>
::: moniker-end

<span data-ttu-id="3b6f0-109">控制器的构造函数使用[依赖关系注入](xref:fundamentals/dependency-injection)将数据库上下文 (`TodoContext`) 注入到控制器中。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-109">The controller's constructor uses [Dependency Injection](xref:fundamentals/dependency-injection) to inject the database context (`TodoContext`) into the controller.</span></span> <span data-ttu-id="3b6f0-110">数据库上下文将在控制器中的每个 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 方法中使用。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-110">The database context is used in each of the [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) methods in the controller.</span></span> <span data-ttu-id="3b6f0-111">构造函数将一个项（如果不存在）添加到内存数据库。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-111">The constructor adds an item to the in-memory database if one doesn't exist.</span></span>

## <a name="get-to-do-items"></a><span data-ttu-id="3b6f0-112">获取待办事项</span><span class="sxs-lookup"><span data-stu-id="3b6f0-112">Get to-do items</span></span>

<span data-ttu-id="3b6f0-113">若要获取待办事项，请将下面的方法添加到 `TodoController` 类中：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-113">To get to-do items, add the following methods to the `TodoController` class:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3b6f0-114">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-114">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3b6f0-115">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-115">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]</span></span>
::: moniker-end

<span data-ttu-id="3b6f0-116">这些方法实现两种 GET 方法：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-116">These methods implement the two GET methods:</span></span>

* `GET /api/todo`
* `GET /api/todo/{id}`

<span data-ttu-id="3b6f0-117">以下是 `GetAll` 方法的 HTTP 响应示例：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-117">Here's a sample HTTP response for the `GetAll` method:</span></span>

```json
[
  {
    "id": 1,
    "name": "Item1",
    "isComplete": false
  }
]
```

<span data-ttu-id="3b6f0-118">稍后将在本教程中演示如何使用 [Postman](https://www.getpostman.com/) 或 [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html) 查看 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-118">Later in the tutorial, I'll show how the HTTP response can be viewed with [Postman](https://www.getpostman.com/) or [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html).</span></span>

### <a name="routing-and-url-paths"></a><span data-ttu-id="3b6f0-119">路由和 URL 路径</span><span class="sxs-lookup"><span data-stu-id="3b6f0-119">Routing and URL paths</span></span>

<span data-ttu-id="3b6f0-120">`[HttpGet]` 特性表示对 HTTP GET 请求进行响应的方法。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-120">The `[HttpGet]` attribute denotes a method that responds to an HTTP GET request.</span></span> <span data-ttu-id="3b6f0-121">每个方法的 URL 路径构造如下所示：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-121">The URL path for each method is constructed as follows:</span></span>

* <span data-ttu-id="3b6f0-122">在控制器的 `Route` 属性中采用模板字符串：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-122">Take the template string in the controller's `Route` attribute:</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3b6f0-123">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-123">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3b6f0-124">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-124">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]</span></span>
::: moniker-end

* <span data-ttu-id="3b6f0-125">将 `[controller]` 替换为控制器的名称，即在控制器类名称中去掉“Controller”后缀。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-125">Replace `[controller]` with the name of the controller, which is the controller class name minus the "Controller" suffix.</span></span> <span data-ttu-id="3b6f0-126">对于此示例，控制器类名称为“Todo”控制器，根名称为“todo”。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-126">For this sample, the controller class name is **Todo**Controller and the root name is "todo".</span></span> <span data-ttu-id="3b6f0-127">ASP.NET Core [路由](xref:mvc/controllers/routing)不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-127">ASP.NET Core [routing](xref:mvc/controllers/routing) is case insensitive.</span></span>
* <span data-ttu-id="3b6f0-128">如果 `[HttpGet]` 特性具有路由模板（如 `[HttpGet("/products")]`），则将它追加到路径。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-128">If the `[HttpGet]` attribute has a route template (such as `[HttpGet("/products")]`, append that to the path.</span></span> <span data-ttu-id="3b6f0-129">此示例不使用模板。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-129">This sample doesn't use a template.</span></span> <span data-ttu-id="3b6f0-130">有关详细信息，请参阅[使用 Http [Verb] 特性的特性路由](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes)。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-130">For more information, see [Attribute routing with Http[Verb] attributes](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes).</span></span>

<span data-ttu-id="3b6f0-131">在下面的 `GetById` 方法中，`"{id}"` 是待办事项的唯一标识符的占位符变量。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-131">In the following `GetById` method, `"{id}"` is a placeholder variable for the unique identifier of the to-do item.</span></span> <span data-ttu-id="3b6f0-132">调用 `GetById` 时，它会将 URL 中 `"{id}"` 的值分配给方法的 `id` 参数。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-132">When `GetById` is invoked, it assigns the value of `"{id}"` in the URL to the method's `id` parameter.</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3b6f0-133">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-133">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3b6f0-134">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span><span class="sxs-lookup"><span data-stu-id="3b6f0-134">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]</span></span>
::: moniker-end

<span data-ttu-id="3b6f0-135">`Name = "GetTodo"` 创建具名路由。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-135">`Name = "GetTodo"` creates a named route.</span></span> <span data-ttu-id="3b6f0-136">具名路由：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-136">Named routes:</span></span>

* <span data-ttu-id="3b6f0-137">使应用程序使用路由名称创建 HTTP 链接。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-137">Enable the app to create an HTTP link using the route name.</span></span>
* <span data-ttu-id="3b6f0-138">将在本教程的后续部分中介绍。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-138">Are explained later in the tutorial.</span></span>

### <a name="return-values"></a><span data-ttu-id="3b6f0-139">返回值</span><span class="sxs-lookup"><span data-stu-id="3b6f0-139">Return values</span></span>

<span data-ttu-id="3b6f0-140">`GetAll` 方法返回一个 `TodoItem` 对象的集合。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-140">The `GetAll` method returns a collection of `TodoItem` objects.</span></span> <span data-ttu-id="3b6f0-141">MVC 自动将对象序列化为 [JSON](https://www.json.org/)，并将 JSON 写入响应消息的正文中。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-141">MVC automatically serializes the object to [JSON](https://www.json.org/) and writes the JSON into the body of the response message.</span></span> <span data-ttu-id="3b6f0-142">在假设没有未经处理的异常的情况下，此方法的响应代码为 200。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-142">The response code for this method is 200, assuming there are no unhandled exceptions.</span></span> <span data-ttu-id="3b6f0-143">未经处理的异常将转换为 5xx 错误。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-143">Unhandled exceptions are translated into 5xx errors.</span></span>

::: moniker range="<= aspnetcore-2.0"
<span data-ttu-id="3b6f0-144">相反，`GetById` 方法返回多个常规的 [IActionResult 类型](xref:web-api/action-return-types#iactionresult-type)，它表示一系列返回类型。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-144">In contrast, the `GetById` method returns the more general [IActionResult type](xref:web-api/action-return-types#iactionresult-type), which represents a wide range of return types.</span></span> <span data-ttu-id="3b6f0-145">`GetById` 具有两个不同的返回类型：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-145">`GetById` has two different return types:</span></span>

* <span data-ttu-id="3b6f0-146">如果没有任何项与请求的 ID 匹配，此方法将返回 404 错误。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-146">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="3b6f0-147">返回 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 可以返回 HTTP 404 响应。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-147">Returning [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) returns an HTTP 404 response.</span></span>
* <span data-ttu-id="3b6f0-148">否则，此方法将返回具有 JSON 响应正文的 200。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-148">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="3b6f0-149">返回 [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok)，则产生 HTTP 200 响应。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-149">Returning [Ok](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.ok) results in an HTTP 200 response.</span></span>
::: moniker-end
::: moniker range=">= aspnetcore-2.1"
<span data-ttu-id="3b6f0-150">相反，`GetById` 方法返回多个 [ActionResult\<T> 类型](xref:web-api/action-return-types#actionresultt-type)，它表示一系列返回类型。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-150">In contrast, the `GetById` method returns the [ActionResult\<T> type](xref:web-api/action-return-types#actionresultt-type), which represents a wide range of return types.</span></span> <span data-ttu-id="3b6f0-151">`GetById` 具有两个不同的返回类型：</span><span class="sxs-lookup"><span data-stu-id="3b6f0-151">`GetById` has two different return types:</span></span>

* <span data-ttu-id="3b6f0-152">如果没有任何项与请求的 ID 匹配，此方法将返回 404 错误。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-152">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="3b6f0-153">返回 [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) 可以返回 HTTP 404 响应。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-153">Returning [NotFound](/dotnet/api/microsoft.aspnetcore.mvc.controllerbase.notfound) returns an HTTP 404 response.</span></span>
* <span data-ttu-id="3b6f0-154">否则，此方法将返回具有 JSON 响应正文的 200。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-154">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="3b6f0-155">返回 `item` 则产生 HTTP 200 响应。</span><span class="sxs-lookup"><span data-stu-id="3b6f0-155">Returning `item` results in an HTTP 200 response.</span></span>
::: moniker-end