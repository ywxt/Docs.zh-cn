# <a name="aspnet-core-web-api-controller-sample"></a><span data-ttu-id="fd982-101">ASP.NET Core Web API 控制器示例</span><span class="sxs-lookup"><span data-stu-id="fd982-101">ASP.NET Core Web API Controller Sample</span></span>

<span data-ttu-id="fd982-102">本示例应用包含以下项目：</span><span class="sxs-lookup"><span data-stu-id="fd982-102">This sample app consists of the following projects:</span></span>

- <span data-ttu-id="fd982-103">WebApiSample.Api：面向 .NET Core 2.1 的 ASP.NET Core 2.1 项目。</span><span class="sxs-lookup"><span data-stu-id="fd982-103">**WebApiSample.Api**: An ASP.NET Core 2.1 project targeting .NET Core 2.1.</span></span>
- <span data-ttu-id="fd982-104">WebApiSample.Api.Pre21：面向 .NET Core 2.0 的 ASP.NET Core 2.0 项目。</span><span class="sxs-lookup"><span data-stu-id="fd982-104">**WebApiSample.Api.Pre21**: An ASP.NET Core 2.0 project targeting .NET Core 2.0.</span></span>
- <span data-ttu-id="fd982-105">WebApiSample.DataAccess：用作 2 个 Web API 项目的数据访问层的 .NET Standard 2.0 类库。</span><span class="sxs-lookup"><span data-stu-id="fd982-105">**WebApiSample.DataAccess**: A .NET Standard 2.0 class library serving as a data access tier for the 2 Web API projects.</span></span>

<span data-ttu-id="fd982-106">此示例说明 Web API 控制器的各种创建方式：</span><span class="sxs-lookup"><span data-stu-id="fd982-106">This sample illustrates variations of Web API controller creation:</span></span>

- [<span data-ttu-id="fd982-107">从 ControllerBase 派生类</span><span class="sxs-lookup"><span data-stu-id="fd982-107">Derive class from ControllerBase</span></span>](https://docs.microsoft.com/en-us/aspnet/core/web-api/define-controller#derive-class-from-controllerbase)
- [<span data-ttu-id="fd982-108">使用 ApiControllerAttribute 批注类</span><span class="sxs-lookup"><span data-stu-id="fd982-108">Annotate class with ApiControllerAttribute</span></span>](https://docs.microsoft.com/en-us/aspnet/core/web-api/define-controller#annotate-class-with-apicontrollerattribute)