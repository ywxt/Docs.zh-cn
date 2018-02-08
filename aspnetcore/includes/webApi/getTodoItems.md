[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController2.cs?name=snippet_todo1)]

<span data-ttu-id="83e13-101">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="83e13-101">The preceding code:</span></span>

* <span data-ttu-id="83e13-102">定义空控制器类。</span><span class="sxs-lookup"><span data-stu-id="83e13-102">Defines an empty controller class.</span></span> <span data-ttu-id="83e13-103">在接下来的部分中，将添加方法来实现 API。</span><span class="sxs-lookup"><span data-stu-id="83e13-103">In the next sections, methods are added to implement the API.</span></span>
* <span data-ttu-id="83e13-104">构造函数使用[依赖关系注入](xref:fundamentals/dependency-injection)将数据库上下文 (`TodoContext `) 注入到控制器中。</span><span class="sxs-lookup"><span data-stu-id="83e13-104">The constructor uses [Dependency Injection](xref:fundamentals/dependency-injection) to inject the database context (`TodoContext `) into the controller.</span></span> <span data-ttu-id="83e13-105">数据库上下文将在控制器中的每个 [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) 方法中使用。</span><span class="sxs-lookup"><span data-stu-id="83e13-105">The database context is used in each of the [CRUD](https://wikipedia.org/wiki/Create,_read,_update_and_delete) methods in the controller.</span></span>
* <span data-ttu-id="83e13-106">构造函数将一个项（如果不存在）添加到内存数据库。</span><span class="sxs-lookup"><span data-stu-id="83e13-106">The constructor adds an item to the in-memory database if one doesn't exist.</span></span>

## <a name="getting-to-do-items"></a><span data-ttu-id="83e13-107">获取待办事项</span><span class="sxs-lookup"><span data-stu-id="83e13-107">Getting to-do items</span></span>

<span data-ttu-id="83e13-108">若要获取待办事项，请将下面的方法添加到 `TodoController` 类中。</span><span class="sxs-lookup"><span data-stu-id="83e13-108">To get to-do items, add the following methods to the `TodoController` class.</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_GetAll)]

<span data-ttu-id="83e13-109">这些方法实现两种 GET 方法：</span><span class="sxs-lookup"><span data-stu-id="83e13-109">These methods implement the two GET methods:</span></span>

* `GET /api/todo`
* `GET /api/todo/{id}`

<span data-ttu-id="83e13-110">以下是 `GetAll` 方法的 HTTP 响应示例：</span><span class="sxs-lookup"><span data-stu-id="83e13-110">Here is an example HTTP response for the `GetAll` method:</span></span>

```
[
  {
    "id": 1,
    "name": "Item1",
    "isComplete": false
  }
]
   ```

<span data-ttu-id="83e13-111">稍后将在本教程中演示如何使用 [Postman](https://www.getpostman.com/) 或 [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html) 查看 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="83e13-111">Later in the tutorial I'll show how the HTTP response can be viewed with [Postman](https://www.getpostman.com/) or [curl](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/curl.1.html).</span></span>

### <a name="routing-and-url-paths"></a><span data-ttu-id="83e13-112">路由和 URL 路径</span><span class="sxs-lookup"><span data-stu-id="83e13-112">Routing and URL paths</span></span>

<span data-ttu-id="83e13-113">`[HttpGet]` 特性指定 HTTP GET 方法。</span><span class="sxs-lookup"><span data-stu-id="83e13-113">The `[HttpGet]` attribute specifies an HTTP GET method.</span></span> <span data-ttu-id="83e13-114">每个方法的 URL 路径构造如下所示：</span><span class="sxs-lookup"><span data-stu-id="83e13-114">The URL path for each method is constructed as follows:</span></span>

* <span data-ttu-id="83e13-115">在控制器的 `Route` 属性中采用模板字符串：</span><span class="sxs-lookup"><span data-stu-id="83e13-115">Take the template string in the controller's `Route` attribute:</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=TodoController&highlight=3)]

* <span data-ttu-id="83e13-116">将 `[controller]` 替换为控制器的名称，即在控制器类名称中去掉“Controller”后缀。</span><span class="sxs-lookup"><span data-stu-id="83e13-116">Replaces `[controller]` with the name of the controller, which is the controller class name minus the "Controller" suffix.</span></span> <span data-ttu-id="83e13-117">对于此示例，控制器类名称为“Todo”控制器，根名称为“todo”。</span><span class="sxs-lookup"><span data-stu-id="83e13-117">For this sample, the controller class name is **Todo**Controller and the root name is "todo".</span></span> <span data-ttu-id="83e13-118">ASP.NET Core [路由](xref:mvc/controllers/routing)不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="83e13-118">ASP.NET Core [routing](xref:mvc/controllers/routing) isn't case sensitive.</span></span>
* <span data-ttu-id="83e13-119">如果 `[HttpGet]` 特性具有路由模板（如 `[HttpGet("/products")]`），则将它追加到路径。</span><span class="sxs-lookup"><span data-stu-id="83e13-119">If the `[HttpGet]` attribute has a route template (such as `[HttpGet("/products")]`, append that to the path.</span></span> <span data-ttu-id="83e13-120">此示例不使用模板。</span><span class="sxs-lookup"><span data-stu-id="83e13-120">This sample doesn't use a template.</span></span> <span data-ttu-id="83e13-121">有关详细信息，请参阅[使用 Http [Verb] 特性的特性路由](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes)。</span><span class="sxs-lookup"><span data-stu-id="83e13-121">See [Attribute routing with Http[Verb] attributes](xref:mvc/controllers/routing#attribute-routing-with-httpverb-attributes) for more information.</span></span>

<span data-ttu-id="83e13-122">在 `GetById` 方法中：</span><span class="sxs-lookup"><span data-stu-id="83e13-122">In the `GetById` method:</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Controllers/TodoController.cs?name=snippet_GetByID&highlight=1-2)]

<span data-ttu-id="83e13-123">`"{id}"` 是 `todo` 项 的 ID 的占位符变量。</span><span class="sxs-lookup"><span data-stu-id="83e13-123">`"{id}"` is a placeholder variable for the ID of the `todo` item.</span></span> <span data-ttu-id="83e13-124">调用 `GetById` 时，它会将 URL 中“{id}”的值分配给方法的 `id` 参数。</span><span class="sxs-lookup"><span data-stu-id="83e13-124">When `GetById` is invoked, it assigns the value of "{id}" in the URL to the method's `id` parameter.</span></span>

<span data-ttu-id="83e13-125">`Name = "GetTodo"` 创建具名路由。</span><span class="sxs-lookup"><span data-stu-id="83e13-125">`Name = "GetTodo"` creates a named route.</span></span> <span data-ttu-id="83e13-126">具名路由：</span><span class="sxs-lookup"><span data-stu-id="83e13-126">Named routes:</span></span>

* <span data-ttu-id="83e13-127">使应用程序使用路由名称创建 HTTP 链接。</span><span class="sxs-lookup"><span data-stu-id="83e13-127">Enable the app to create an HTTP link using the route name.</span></span>
* <span data-ttu-id="83e13-128">将在本教程的后续部分中介绍。</span><span class="sxs-lookup"><span data-stu-id="83e13-128">Are explained later in the tutorial.</span></span>

### <a name="return-values"></a><span data-ttu-id="83e13-129">返回值</span><span class="sxs-lookup"><span data-stu-id="83e13-129">Return values</span></span>

<span data-ttu-id="83e13-130">`GetAll` 方法返回 `IEnumerable`。</span><span class="sxs-lookup"><span data-stu-id="83e13-130">The `GetAll` method returns an `IEnumerable`.</span></span> <span data-ttu-id="83e13-131">MVC 自动将对象序列化为 [JSON](http://www.json.org/)，并将 JSON 写入响应消息的正文中。</span><span class="sxs-lookup"><span data-stu-id="83e13-131">MVC automatically serializes the object to [JSON](http://www.json.org/) and writes the JSON into the body of the response message.</span></span> <span data-ttu-id="83e13-132">在假设没有未经处理的异常的情况下，此方法的响应代码为 200。</span><span class="sxs-lookup"><span data-stu-id="83e13-132">The response code for this method is 200, assuming there are no unhandled exceptions.</span></span> <span data-ttu-id="83e13-133">（未经处理的异常将转换为 5xx 错误。）</span><span class="sxs-lookup"><span data-stu-id="83e13-133">(Unhandled exceptions are translated into 5xx errors.)</span></span>

<span data-ttu-id="83e13-134">相反，`GetById` 方法返回多个常规的 `IActionResult` 类型，它表示一系列返回类型。</span><span class="sxs-lookup"><span data-stu-id="83e13-134">In contrast, the `GetById` method returns the more general `IActionResult` type, which represents a wide range of return types.</span></span> <span data-ttu-id="83e13-135">`GetById` 具有两个不同的返回类型：</span><span class="sxs-lookup"><span data-stu-id="83e13-135">`GetById` has two different return types:</span></span>

* <span data-ttu-id="83e13-136">如果没有任何项与请求的 ID 匹配，此方法将返回 404 错误。</span><span class="sxs-lookup"><span data-stu-id="83e13-136">If no item matches the requested ID, the method returns a 404 error.</span></span> <span data-ttu-id="83e13-137">返回 `NotFound` 可以返回 HTTP 404 响应。</span><span class="sxs-lookup"><span data-stu-id="83e13-137">Returning `NotFound` returns an HTTP 404 response.</span></span>

* <span data-ttu-id="83e13-138">否则，此方法将返回具有 JSON 响应正文的 200。</span><span class="sxs-lookup"><span data-stu-id="83e13-138">Otherwise, the method returns 200 with a JSON response body.</span></span> <span data-ttu-id="83e13-139">返回 `ObjectResult` 可以返回 HTTP 200 响应。</span><span class="sxs-lookup"><span data-stu-id="83e13-139">Returning `ObjectResult` returns an HTTP 200 response.</span></span>
