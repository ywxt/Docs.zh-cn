## <a name="register-the-database-context"></a><span data-ttu-id="7059c-101">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="7059c-101">Register the database context</span></span>

<span data-ttu-id="7059c-102">在该步骤中，向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="7059c-102">In this step, the database context is registered with the [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="7059c-103">向依赖关系注入 (DI) 容器注册的服务（例如数据库上下文）可供控制器使用。</span><span class="sxs-lookup"><span data-stu-id="7059c-103">Services (such as the DB context) that are registered with the dependency injection (DI) container are available to the controllers.</span></span>

<span data-ttu-id="7059c-104">使用[依赖关系注入](xref:fundamentals/dependency-injection)的内置支持将数据库上下文注册到服务容器。</span><span class="sxs-lookup"><span data-stu-id="7059c-104">Register the DB context with the service container using the built-in support for [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="7059c-105">将 Startup.cs 文件的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="7059c-105">Replace the contents of the *Startup.cs* file with the following code:</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7059c-106">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Startup.cs?highlight=3,5,13-14)]</span><span class="sxs-lookup"><span data-stu-id="7059c-106">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Startup.cs?highlight=3,5,13-14)]</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="7059c-107">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup.cs?highlight=2,4,12-13)]</span><span class="sxs-lookup"><span data-stu-id="7059c-107">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup.cs?highlight=2,4,12-13)]</span></span>

::: moniker-end  

<span data-ttu-id="7059c-108">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="7059c-108">The preceding code:</span></span>

* <span data-ttu-id="7059c-109">删除未使用的代码。</span><span class="sxs-lookup"><span data-stu-id="7059c-109">Removes the unused code.</span></span>
* <span data-ttu-id="7059c-110">指定将内存数据库注入到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="7059c-110">Specifies an in-memory database is injected into the service container.</span></span>
