## <a name="register-the-database-context"></a><span data-ttu-id="e0007-101">注册数据库上下文</span><span class="sxs-lookup"><span data-stu-id="e0007-101">Register the database context</span></span>

<span data-ttu-id="e0007-102">在该步骤中，向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="e0007-102">In this step, the database context is registered with the [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="e0007-103">向依赖关系注入 (DI) 容器注册的服务（例如数据库上下文）可供控制器使用。</span><span class="sxs-lookup"><span data-stu-id="e0007-103">Services (such as the DB context) that are registered with the dependency injection (DI) container are available to the controllers.</span></span>

<span data-ttu-id="e0007-104">使用[依赖关系注入](xref:fundamentals/dependency-injection)的内置支持将数据库上下文注册到服务容器。</span><span class="sxs-lookup"><span data-stu-id="e0007-104">Register the DB context with the service container using the built-in support for [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="e0007-105">将 Startup.cs 文件的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e0007-105">Replace the contents of the *Startup.cs* file with the following code:</span></span>

[!code-csharp[Main](../../tutorials/first-web-api/sample/TodoApi/Startup.cs?highlight=2,4,12)]

<span data-ttu-id="e0007-106">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="e0007-106">The preceding code:</span></span>

* <span data-ttu-id="e0007-107">删除未使用的代码。</span><span class="sxs-lookup"><span data-stu-id="e0007-107">Removes the code that's not used.</span></span>
* <span data-ttu-id="e0007-108">指定将内存数据库注入到服务容器中。</span><span class="sxs-lookup"><span data-stu-id="e0007-108">Specifies an in-memory database is injected into the service container.</span></span>