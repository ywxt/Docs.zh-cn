## <a name="register-the-database-context"></a>注册数据库上下文

在该步骤中，向[依赖关系注入](xref:fundamentals/dependency-injection)容器注册数据库上下文。 向依赖关系注入 (DI) 容器注册的服务（例如数据库上下文）可供控制器使用。

使用[依赖关系注入](xref:fundamentals/dependency-injection)的内置支持将数据库上下文注册到服务容器。 将 Startup.cs 文件的内容替换为以下代码：

::: moniker range=">= aspnetcore-2.1"

[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Startup.cs?highlight=3,5,13-14)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup.cs?highlight=2,4,12-13)]

::: moniker-end  

前面的代码：

* 删除未使用的代码。
* 指定将内存数据库注入到服务容器中。
