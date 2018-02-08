# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="cd984-101">ASP.NET Core URL 重写示例 (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="cd984-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="cd984-102">本示例演示 ASP.NET Core 2.x URL 重写中间件的用法。</span><span class="sxs-lookup"><span data-stu-id="cd984-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="cd984-103">该应用程序演示 URL 重定向和 URL 重写选项。</span><span class="sxs-lookup"><span data-stu-id="cd984-103">The application demonstrates URL redirect and URL rewriting options.</span></span> <span data-ttu-id="cd984-104">有关 ASP.NET Core 1.x 示例，请参阅 [ASP.NET Core URL 重写示例 (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/1.x)。</span><span class="sxs-lookup"><span data-stu-id="cd984-104">For the ASP.NET Core 1.x sample, see [ASP.NET Core URL Rewriting Sample (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/1.x).</span></span>

<span data-ttu-id="cd984-105">运行示例时，将会提供响应，显示将其中一个规则应用于请求 URL 时重写或重定向的 URL。</span><span class="sxs-lookup"><span data-stu-id="cd984-105">When running the sample, a response will be served that shows the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="cd984-106">此示例中的示例</span><span class="sxs-lookup"><span data-stu-id="cd984-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="cd984-107">成功状态代码：302 (已找到)</span><span class="sxs-lookup"><span data-stu-id="cd984-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="cd984-108">示例（重定向）：/redirect-rule/{capture_group} 到 /redirected/{capture_group}</span><span class="sxs-lookup"><span data-stu-id="cd984-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="cd984-109">成功状态代码：200 (正常)</span><span class="sxs-lookup"><span data-stu-id="cd984-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="cd984-110">示例（重写）：/rewrite-rule/{capture_group_1}/{capture_group_2} 到 /rewritten?var1={capture_group_1}&var2={capture_group_2}</span><span class="sxs-lookup"><span data-stu-id="cd984-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="cd984-111">成功状态代码：302 (已找到)</span><span class="sxs-lookup"><span data-stu-id="cd984-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="cd984-112">示例（重定向）：/apache-mod-rules-redirect/{capture_group} 到 /redirected?id={capture_group}</span><span class="sxs-lookup"><span data-stu-id="cd984-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="cd984-113">成功状态代码：200 (正常)</span><span class="sxs-lookup"><span data-stu-id="cd984-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="cd984-114">示例（重写）：/iis-rules-rewrite/{capture_group} 到 /rewritten?id={capture_group}</span><span class="sxs-lookup"><span data-stu-id="cd984-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXMLRequests)`
  - <span data-ttu-id="cd984-115">成功状态代码：301 (永久移动)</span><span class="sxs-lookup"><span data-stu-id="cd984-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="cd984-116">示例（重定向）：/file.xml 到 /xmlfiles/file.xml</span><span class="sxs-lookup"><span data-stu-id="cd984-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(new RedirectPNGRequests(".png", "/png-images")))`<br>`Add(new RedirectPNGRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="cd984-117">成功状态代码：301 (永久移动)</span><span class="sxs-lookup"><span data-stu-id="cd984-117">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="cd984-118">示例（重定向）：/image.png 到 /png-images/image.png</span><span class="sxs-lookup"><span data-stu-id="cd984-118">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="cd984-119">示例（重定向）：/image.jpg 到 /jpg-images/image.jpg</span><span class="sxs-lookup"><span data-stu-id="cd984-119">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="using-a-physicalfileprovider"></a><span data-ttu-id="cd984-120">使用 `PhysicalFileProvider`</span><span class="sxs-lookup"><span data-stu-id="cd984-120">Using a `PhysicalFileProvider`</span></span>
<span data-ttu-id="cd984-121">也可通过创建 `PhysicalFileProvider` 以传递给 `AddApacheModRewrite()` 和 `AddIISUrlRewrite()` 方法来获取 `IFileProvider`：</span><span class="sxs-lookup"><span data-stu-id="cd984-121">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>
```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```
## <a name="secure-redirection-extensions"></a><span data-ttu-id="cd984-122">安全的重定向扩展</span><span class="sxs-lookup"><span data-stu-id="cd984-122">Secure redirection extensions</span></span>
<span data-ttu-id="cd984-123">此示例包含应用的 `WebHostBuilder` 配置以使用 URL（https://localhost:5001、https://localhost）和测试证书 (testCert.pfx)，来帮助了解这些重定向方法。</span><span class="sxs-lookup"><span data-stu-id="cd984-123">This sample includes `WebHostBuilder` configuration for the app to use URLs (**https://localhost:5001**, **https://localhost**) and a test certificate (**testCert.pfx**) to assist you in exploring these redirect methods.</span></span> <span data-ttu-id="cd984-124">将其中任何一个添加到 Startup.cs 的 `RewriteOptions()` 中以研究其行为。</span><span class="sxs-lookup"><span data-stu-id="cd984-124">Add any of them to the `RewriteOptions()` in **Startup.cs** to study their behavior.</span></span>

<span data-ttu-id="cd984-125">方法</span><span class="sxs-lookup"><span data-stu-id="cd984-125">Method</span></span> | <span data-ttu-id="cd984-126">状态代码</span><span class="sxs-lookup"><span data-stu-id="cd984-126">Status Code</span></span> | <span data-ttu-id="cd984-127">端口</span><span class="sxs-lookup"><span data-stu-id="cd984-127">Port</span></span>
--- | :---: | :---:
`.AddRedirectToHttpsPermanent()` | <span data-ttu-id="cd984-128">301</span><span class="sxs-lookup"><span data-stu-id="cd984-128">301</span></span> | <span data-ttu-id="cd984-129">null (465)</span><span class="sxs-lookup"><span data-stu-id="cd984-129">null (465)</span></span>
`.AddRedirectToHttps()` | <span data-ttu-id="cd984-130">302</span><span class="sxs-lookup"><span data-stu-id="cd984-130">302</span></span> | <span data-ttu-id="cd984-131">null (465)</span><span class="sxs-lookup"><span data-stu-id="cd984-131">null (465)</span></span>
`.AddRedirectToHttps(301)` | <span data-ttu-id="cd984-132">301</span><span class="sxs-lookup"><span data-stu-id="cd984-132">301</span></span> | <span data-ttu-id="cd984-133">null (465)</span><span class="sxs-lookup"><span data-stu-id="cd984-133">null (465)</span></span>
`.AddRedirectToHttps(301, 5001)` | <span data-ttu-id="cd984-134">301</span><span class="sxs-lookup"><span data-stu-id="cd984-134">301</span></span> | <span data-ttu-id="cd984-135">5001</span><span class="sxs-lookup"><span data-stu-id="cd984-135">5001</span></span>
