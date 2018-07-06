---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: 启用 ASP.NET Web API 2 中的跨域请求 |Microsoft Docs
author: MikeWasson
description: 演示如何在 ASP.NET Web API 中支持跨域资源共享 (CORS)。
ms.author: aspnetcontent
ms.date: 07/15/2014
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7ac6158c2365aa324cefe97db044f568a1a43795
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805407"
---
<a name="enabling-cross-origin-requests-in-aspnet-web-api-2"></a><span data-ttu-id="1cdde-103">启用 ASP.NET Web API 2 中的跨域请求</span><span class="sxs-lookup"><span data-stu-id="1cdde-103">Enabling Cross-Origin Requests in ASP.NET Web API 2</span></span>
====================
<span data-ttu-id="1cdde-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1cdde-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="1cdde-105">浏览器安全策略阻止 Web 页向另一个域发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-105">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="1cdde-106">此限制称为“同源策略”，可防止恶意站点读取另一个站点中的敏感数据。</span><span class="sxs-lookup"><span data-stu-id="1cdde-106">This restriction is called the *same-origin policy*, and prevents a malicious site from reading sensitive data from another site.</span></span> <span data-ttu-id="1cdde-107">但是，有时你可能想要让调用 web API 的其他站点。</span><span class="sxs-lookup"><span data-stu-id="1cdde-107">However, sometimes you might want to let other sites call your web API.</span></span>
> 
> <span data-ttu-id="1cdde-108">[跨域资源共享](http://www.w3.org/TR/cors/)(CORS) 是一种 W3C 标准，允许服务器放宽同源策略。</span><span class="sxs-lookup"><span data-stu-id="1cdde-108">[Cross Origin Resource Sharing](http://www.w3.org/TR/cors/) (CORS) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="1cdde-109">使用 CORS，服务器可以在显式允许某些跨域请求时拒绝其他跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-109">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span> <span data-ttu-id="1cdde-110">CORS 比早期技术（例如 [JSONP](http://en.wikipedia.org/wiki/JSONP)）更安全、更灵活。</span><span class="sxs-lookup"><span data-stu-id="1cdde-110">CORS is safer and more flexible than earlier techniques such as [JSONP](http://en.wikipedia.org/wiki/JSONP).</span></span> <span data-ttu-id="1cdde-111">本教程演示如何在 Web API 应用程序中启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="1cdde-111">This tutorial shows how to enable CORS in your Web API application.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1cdde-112">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="1cdde-112">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="1cdde-113">Visual Studio 2013 Update 2</span><span class="sxs-lookup"><span data-stu-id="1cdde-113">Visual Studio 2013 Update 2</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="1cdde-114">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="1cdde-114">Web API 2.2</span></span>


<a id="intro"></a>
## <a name="introduction"></a><span data-ttu-id="1cdde-115">介绍</span><span class="sxs-lookup"><span data-stu-id="1cdde-115">Introduction</span></span>

<span data-ttu-id="1cdde-116">本教程演示了在 ASP.NET Web API 中的 CORS 支持。</span><span class="sxs-lookup"><span data-stu-id="1cdde-116">This tutorial demonstrates CORS support in ASP.NET Web API.</span></span> <span data-ttu-id="1cdde-117">我们将首先创建两个 ASP.NET 项目-一个名为"web 服务"，它承载 Web API 控制器，以及其他名为"WebClient"，后者调用 web 服务。</span><span class="sxs-lookup"><span data-stu-id="1cdde-117">We'll start by creating two ASP.NET projects – one called "WebService", which hosts a Web API controller, and the other called "WebClient", which calls WebService.</span></span> <span data-ttu-id="1cdde-118">由于两个应用程序承载在不同的域中，从 WebClient 对 web 服务的 AJAX 请求是跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-118">Because the two applications are hosted at different domains, an AJAX request from WebClient to WebService is a cross-origin request.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a><span data-ttu-id="1cdde-119">什么是"相同的原点"？</span><span class="sxs-lookup"><span data-stu-id="1cdde-119">What is "Same Origin"?</span></span>

<span data-ttu-id="1cdde-120">如果它们具有相同方案、 主机和端口，两个 Url 将具有相同的原点。</span><span class="sxs-lookup"><span data-stu-id="1cdde-120">Two URLs have the same origin if they have identical schemes, hosts, and ports.</span></span> <span data-ttu-id="1cdde-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span><span class="sxs-lookup"><span data-stu-id="1cdde-121">([RFC 6454](http://tools.ietf.org/html/rfc6454))</span></span>

<span data-ttu-id="1cdde-122">以下两个 Url 具有相同的原点：</span><span class="sxs-lookup"><span data-stu-id="1cdde-122">These two URLs have the same origin:</span></span>

- `http://example.com/foo.html`
- `http://example.com/bar.html`

<span data-ttu-id="1cdde-123">这些 Url 有两个相对上一不同的源：</span><span class="sxs-lookup"><span data-stu-id="1cdde-123">These URLs have different origins than the previous two:</span></span>

- <span data-ttu-id="1cdde-124">`http://example.net` -不同的域</span><span class="sxs-lookup"><span data-stu-id="1cdde-124">`http://example.net` - Different domain</span></span>
- <span data-ttu-id="1cdde-125">`http://example.com:9000/foo.html` -不同的端口</span><span class="sxs-lookup"><span data-stu-id="1cdde-125">`http://example.com:9000/foo.html` - Different port</span></span>
- <span data-ttu-id="1cdde-126">`https://example.com/foo.html` -不同的方案</span><span class="sxs-lookup"><span data-stu-id="1cdde-126">`https://example.com/foo.html` - Different scheme</span></span>
- <span data-ttu-id="1cdde-127">`http://www.example.com/foo.html` -不同的子域</span><span class="sxs-lookup"><span data-stu-id="1cdde-127">`http://www.example.com/foo.html` - Different subdomain</span></span>

> [!NOTE]
> <span data-ttu-id="1cdde-128">在比较源时，Internet Explorer 不考虑端口。</span><span class="sxs-lookup"><span data-stu-id="1cdde-128">Internet Explorer does not consider the port when comparing origins.</span></span>


<a id="create-webapi-project"></a>
## <a name="create-the-webservice-project"></a><span data-ttu-id="1cdde-129">创建 web 服务项目</span><span class="sxs-lookup"><span data-stu-id="1cdde-129">Create the WebService Project</span></span>

> [!NOTE]
> <span data-ttu-id="1cdde-130">本部分假定您已经知道如何创建 Web API 项目。</span><span class="sxs-lookup"><span data-stu-id="1cdde-130">This section assumes you already know how to create Web API projects.</span></span> <span data-ttu-id="1cdde-131">如果没有，请参阅[Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="1cdde-131">If not, see [Getting Started with ASP.NET Web API](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>


<span data-ttu-id="1cdde-132">启动 Visual Studio 并创建一个新**ASP.NET Web 应用程序**项目。</span><span class="sxs-lookup"><span data-stu-id="1cdde-132">Start Visual Studio and create a new **ASP.NET Web Application** project.</span></span> <span data-ttu-id="1cdde-133">选择**空**项目模板。</span><span class="sxs-lookup"><span data-stu-id="1cdde-133">Select the **Empty** project template.</span></span> <span data-ttu-id="1cdde-134">在"添加文件夹和核心引用"，选择**Web API**复选框。</span><span class="sxs-lookup"><span data-stu-id="1cdde-134">Under "Add folders and core references for", select the **Web API** checkbox.</span></span> <span data-ttu-id="1cdde-135">（可选） 选择"在云中托管"选项将应用部署到 Mircosoft Azure。</span><span class="sxs-lookup"><span data-stu-id="1cdde-135">Optionally, select the "Host in Cloud" option to deploy the app to Mircosoft Azure.</span></span> <span data-ttu-id="1cdde-136">Microsoft 提供了免费的 web 承载的最多 10 个网站[Azure 免费试用帐户](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="1cdde-136">Microsoft offers free web hosting for up to 10 websites in a [free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

[![](enabling-cross-origin-requests-in-web-api/_static/image3.png)](enabling-cross-origin-requests-in-web-api/_static/image2.png)

<span data-ttu-id="1cdde-137">添加名为的 Web API 控制器`TestController`使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="1cdde-137">Add a Web API controller named `TestController` with the following code:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

<span data-ttu-id="1cdde-138">可以在本地运行应用程序或部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="1cdde-138">You can run the application locally or deploy to Azure.</span></span> <span data-ttu-id="1cdde-139">（对于本教程中的屏幕截图，我已部署到 Azure 应用服务 Web 应用。）若要验证的 web API 是否正常工作，请导航到`http://hostname/api/test/`，其中*主机名*是在其中部署应用程序的域。</span><span class="sxs-lookup"><span data-stu-id="1cdde-139">(For the screenshots in this tutorial, I deployed to Azure App Service Web Apps.) To verify that the web API is working, navigate to `http://hostname/api/test/`, where *hostname* is the domain where you deployed the application.</span></span> <span data-ttu-id="1cdde-140">你应看到响应文本中，&quot;获取： 测试消息&quot;。</span><span class="sxs-lookup"><span data-stu-id="1cdde-140">You should see the response text, &quot;GET: Test Message&quot;.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image4.png)

<a id="create-client"></a>
## <a name="create-the-webclient-project"></a><span data-ttu-id="1cdde-141">创建 WebClient 项目</span><span class="sxs-lookup"><span data-stu-id="1cdde-141">Create the WebClient Project</span></span>

<span data-ttu-id="1cdde-142">创建另一个 ASP.NET Web 应用程序项目，然后选择**MVC**项目模板。</span><span class="sxs-lookup"><span data-stu-id="1cdde-142">Create another ASP.NET Web Application project and select the **MVC** project template.</span></span> <span data-ttu-id="1cdde-143">（可选） 选择**更改身份验证** > **无身份验证**。</span><span class="sxs-lookup"><span data-stu-id="1cdde-143">Optionally, select **Change Authentication** > **No Authentication**.</span></span> <span data-ttu-id="1cdde-144">对于本教程中，不需要身份验证。</span><span class="sxs-lookup"><span data-stu-id="1cdde-144">You don't need authentication for this tutorial.</span></span>

[![](enabling-cross-origin-requests-in-web-api/_static/image6.png)](enabling-cross-origin-requests-in-web-api/_static/image5.png)

<span data-ttu-id="1cdde-145">在解决方案资源管理器中打开文件 Views/Home/Index.cshtml。</span><span class="sxs-lookup"><span data-stu-id="1cdde-145">In Solution Explorer, open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="1cdde-146">此文件中的代码替换为以下：</span><span class="sxs-lookup"><span data-stu-id="1cdde-146">Replace the code in this file with the following:</span></span>

[!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

<span data-ttu-id="1cdde-147">有关*serviceUrl*变量，请使用 web 服务应用程序的 URI。</span><span class="sxs-lookup"><span data-stu-id="1cdde-147">For the *serviceUrl* variable, use the URI of the WebService app.</span></span> <span data-ttu-id="1cdde-148">现在在本地运行 WebClient 应用或将其发布到另一个网站。</span><span class="sxs-lookup"><span data-stu-id="1cdde-148">Now run the WebClient app locally or publish it to another website.</span></span>

<span data-ttu-id="1cdde-149">单击"试用"按钮时将提交到 web 服务应用程序中，使用中列出的 HTTP 方法的 AJAX 请求 （GET、 POST 或 PUT） 的下拉列表框。</span><span class="sxs-lookup"><span data-stu-id="1cdde-149">Clicking the "Try It" button submits an AJAX request to the WebService app, using the HTTP method listed in the dropdown box (GET, POST, or PUT).</span></span> <span data-ttu-id="1cdde-150">这可以让我们检查不同跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-150">This lets us examine different cross-origin requests.</span></span> <span data-ttu-id="1cdde-151">现在，web 服务应用程序不支持 CORS，因此如果单击按钮时，你会收到错误。</span><span class="sxs-lookup"><span data-stu-id="1cdde-151">Right now, the WebService app does not support CORS, so if you click the button, you will get an error.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="1cdde-152">如果监视工具中的 HTTP 流量喜欢[Fiddler](http://www.telerik.com/fiddler)，你将看到，在浏览器 does 发送 GET 请求，并请求成功，但 AJAX 调用将返回错误。</span><span class="sxs-lookup"><span data-stu-id="1cdde-152">If you watch the HTTP traffic in a tool like [Fiddler](http://www.telerik.com/fiddler), you will see that the browser does send the GET request, and the request succeeds, but the AJAX call returns an error.</span></span> <span data-ttu-id="1cdde-153">务必了解同域策略不会阻止浏览器中的从*发送*请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-153">It's important to understand that same-origin policy does not prevent the browser from *sending* the request.</span></span> <span data-ttu-id="1cdde-154">相反，它会阻止应用程序不能看到*响应*。</span><span class="sxs-lookup"><span data-stu-id="1cdde-154">Instead, it prevents the application from seeing the *response*.</span></span>


![](enabling-cross-origin-requests-in-web-api/_static/image8.png)

<a id="enable-cors"></a>
## <a name="enable-cors"></a><span data-ttu-id="1cdde-155">启用 CORS</span><span class="sxs-lookup"><span data-stu-id="1cdde-155">Enable CORS</span></span>

<span data-ttu-id="1cdde-156">现在让我们在 web 服务应用程序中启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="1cdde-156">Now let's enable CORS in the WebService app.</span></span> <span data-ttu-id="1cdde-157">首先，添加 CORS NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="1cdde-157">First, add the CORS NuGet package.</span></span> <span data-ttu-id="1cdde-158">在 Visual Studio 中，从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="1cdde-158">In Visual Studio, from the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="1cdde-159">在包管理器控制台窗口中，键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="1cdde-159">In the Package Manager Console window, type the following command:</span></span>

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

<span data-ttu-id="1cdde-160">此命令安装最新的包和更新所有依赖项，其中包括核心 Web API 库。</span><span class="sxs-lookup"><span data-stu-id="1cdde-160">This command installs the latest package and updates all dependencies, including the core Web API libraries.</span></span> <span data-ttu-id="1cdde-161">用户以面向特定版本的版本标志。</span><span class="sxs-lookup"><span data-stu-id="1cdde-161">User the -Version flag to target a specific version.</span></span> <span data-ttu-id="1cdde-162">CORS 包，需要 Web API 2.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="1cdde-162">The CORS package requires Web API 2.0 or later.</span></span>

<span data-ttu-id="1cdde-163">打开文件应用\_Start/WebApiConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="1cdde-163">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="1cdde-164">将以下代码添加到**WebApiConfig.Register**方法。</span><span class="sxs-lookup"><span data-stu-id="1cdde-164">Add the following code to the **WebApiConfig.Register** method.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

<span data-ttu-id="1cdde-165">接下来，添加 **[EnableCors]** 属性为`TestController`类：</span><span class="sxs-lookup"><span data-stu-id="1cdde-165">Next, add the **[EnableCors]** attribute to the `TestController` class:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

<span data-ttu-id="1cdde-166">有关*来源*参数，请使用 WebClient 应用程序的部署位置的 URI。</span><span class="sxs-lookup"><span data-stu-id="1cdde-166">For the *origins* parameter, use the URI where you deployed the WebClient application.</span></span> <span data-ttu-id="1cdde-167">这允许跨域请求从 WebClient，同时仍不允许其他所有跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-167">This allows cross-origin requests from WebClient, while still disallowing all other cross-domain requests.</span></span> <span data-ttu-id="1cdde-168">更高版本，我将介绍的参数 **[EnableCors]** 中更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="1cdde-168">Later, I'll describe the parameters for **[EnableCors]** in more detail.</span></span>

<span data-ttu-id="1cdde-169">不包括末尾的正斜杠*来源*URL。</span><span class="sxs-lookup"><span data-stu-id="1cdde-169">Do not include a forward slash at the end of the *origins* URL.</span></span>

<span data-ttu-id="1cdde-170">重新部署更新的 web 服务应用程序。</span><span class="sxs-lookup"><span data-stu-id="1cdde-170">Redeploy the updated WebService application.</span></span> <span data-ttu-id="1cdde-171">不需要更新 WebClient。</span><span class="sxs-lookup"><span data-stu-id="1cdde-171">You don't need to update WebClient.</span></span> <span data-ttu-id="1cdde-172">现在应该成功从 WebClient AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-172">Now the AJAX request from WebClient should succeed.</span></span> <span data-ttu-id="1cdde-173">所有允许使用 GET、 PUT 和 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="1cdde-173">The GET, PUT, and POST methods are all allowed.</span></span>

![](enabling-cross-origin-requests-in-web-api/_static/image9.png)

<a id="how-it-works"></a>
## <a name="how-cors-works"></a><span data-ttu-id="1cdde-174">CORS 的工作原理</span><span class="sxs-lookup"><span data-stu-id="1cdde-174">How CORS Works</span></span>

<span data-ttu-id="1cdde-175">本部分介绍在 CORS 请求中，在 HTTP 消息的级别会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="1cdde-175">This section describes what happens in a CORS request, at the level of the HTTP messages.</span></span> <span data-ttu-id="1cdde-176">务必要了解 CORS 的工作原理，以便你可以配置 **[EnableCors]** 属性是否正确，并按预期功能不正常工作时进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="1cdde-176">It's important to understand how CORS works, so that you can configure the **[EnableCors]** attribute correctly, and troubleshoot if things don't work as you expect.</span></span>

<span data-ttu-id="1cdde-177">CORS 规范引入了几个新的 HTTP 标头启用跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-177">The CORS specification introduces several new HTTP headers that enable cross-origin requests.</span></span> <span data-ttu-id="1cdde-178">如果浏览器支持 CORS，则将设置自动跨域请求; 这些标头您不必执行任何特殊的 JavaScript 代码中。</span><span class="sxs-lookup"><span data-stu-id="1cdde-178">If a browser supports CORS, it sets these headers automatically for cross-origin requests; you don't need to do anything special in your JavaScript code.</span></span>

<span data-ttu-id="1cdde-179">下面是跨域请求的示例。</span><span class="sxs-lookup"><span data-stu-id="1cdde-179">Here is an example of a cross-origin request.</span></span> <span data-ttu-id="1cdde-180">"源"标头提供发出请求的站点的域。</span><span class="sxs-lookup"><span data-stu-id="1cdde-180">The "Origin" header gives the domain of the site that is making the request.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

<span data-ttu-id="1cdde-181">如果服务器允许该请求，则将设置访问控制的允许的域标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-181">If the server allows the request, it sets the Access-Control-Allow-Origin header.</span></span> <span data-ttu-id="1cdde-182">此标头的值匹配 Origin 标头，或为通配符值"\*"，允许任何源的含义。</span><span class="sxs-lookup"><span data-stu-id="1cdde-182">The value of this header either matches the Origin header, or is the wildcard value "\*", meaning that any origin is allowed.</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

<span data-ttu-id="1cdde-183">如果响应不包括访问控制的允许的域标头，AJAX 请求失败。</span><span class="sxs-lookup"><span data-stu-id="1cdde-183">If the response does not include the Access-Control-Allow-Origin header, the AJAX request fails.</span></span> <span data-ttu-id="1cdde-184">具体而言，在浏览器不允许该请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-184">Specifically, the browser disallows the request.</span></span> <span data-ttu-id="1cdde-185">即使服务器返回成功的响应，请在浏览器不会将响应提供给客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="1cdde-185">Even if the server returns a successful response, the browser does not make the response available to the client application.</span></span>

<span data-ttu-id="1cdde-186">**预检请求**</span><span class="sxs-lookup"><span data-stu-id="1cdde-186">**Preflight Requests**</span></span>

<span data-ttu-id="1cdde-187">对于某些 CORS 请求，浏览器发送额外的请求，名为"预检请求，"，再发送实际请求的资源。</span><span class="sxs-lookup"><span data-stu-id="1cdde-187">For some CORS requests, the browser sends an additional request, called a "preflight request", before it sends the actual request for the resource.</span></span>

<span data-ttu-id="1cdde-188">在浏览器可以跳过预检请求，如果满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="1cdde-188">The browser can skip the preflight request if the following conditions are true:</span></span>

- <span data-ttu-id="1cdde-189">请求方法是 GET、 HEAD 或 POST，*和*</span><span class="sxs-lookup"><span data-stu-id="1cdde-189">The request method is GET, HEAD, or POST, *and*</span></span>
- <span data-ttu-id="1cdde-190">应用程序不会设置之外接受，接受语言的内容语言，任何请求标头内容类型或最后一个事件 ID、*和*</span><span class="sxs-lookup"><span data-stu-id="1cdde-190">The application does not set any request headers other than Accept, Accept-Language, Content-Language, Content-Type, or Last-Event-ID, *and*</span></span>
- <span data-ttu-id="1cdde-191">内容类型标头 (如果设置) 是以下之一：</span><span class="sxs-lookup"><span data-stu-id="1cdde-191">The Content-Type header (if set) is one of the following:</span></span> 

    - <span data-ttu-id="1cdde-192">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="1cdde-192">application/x-www-form-urlencoded</span></span>
    - <span data-ttu-id="1cdde-193">多部分/窗体数据</span><span class="sxs-lookup"><span data-stu-id="1cdde-193">multipart/form-data</span></span>
    - <span data-ttu-id="1cdde-194">文本/无格式</span><span class="sxs-lookup"><span data-stu-id="1cdde-194">text/plain</span></span>

<span data-ttu-id="1cdde-195">有关请求标头规则适用于通过调用来设置应用程序的标头**setRequestHeader**上**XMLHttpRequest**对象。</span><span class="sxs-lookup"><span data-stu-id="1cdde-195">The rule about request headers applies to headers that the application sets by calling **setRequestHeader** on the **XMLHttpRequest** object.</span></span> <span data-ttu-id="1cdde-196">（CORS 规范调用这些"作者请求标头"。）此规则不适用于标头*浏览器*可以设置，例如用户代理、 主机或内容长度。</span><span class="sxs-lookup"><span data-stu-id="1cdde-196">(The CORS specification calls these "author request headers".) The rule does not apply to headers the *browser* can set, such as User-Agent, Host, or Content-Length.</span></span>

<span data-ttu-id="1cdde-197">下面是预检请求的示例：</span><span class="sxs-lookup"><span data-stu-id="1cdde-197">Here is an example of a preflight request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

<span data-ttu-id="1cdde-198">预检请求使用 HTTP OPTIONS 方法。</span><span class="sxs-lookup"><span data-stu-id="1cdde-198">The pre-flight request uses the HTTP OPTIONS method.</span></span> <span data-ttu-id="1cdde-199">它包括两个特殊的标头：</span><span class="sxs-lookup"><span data-stu-id="1cdde-199">It includes two special headers:</span></span>

- <span data-ttu-id="1cdde-200">访问控制的请求的方法： 将用作实际请求 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="1cdde-200">Access-Control-Request-Method: The HTTP method that will be used for the actual request.</span></span>
- <span data-ttu-id="1cdde-201">访问的控件的请求的标头： 请求标头的列表，*应用程序*实际请求上设置。</span><span class="sxs-lookup"><span data-stu-id="1cdde-201">Access-Control-Request-Headers: A list of request headers that the *application* set on the actual request.</span></span> <span data-ttu-id="1cdde-202">（同样，这不包括在浏览器设置的标头。）</span><span class="sxs-lookup"><span data-stu-id="1cdde-202">(Again, this does not include headers that the browser sets.)</span></span>

<span data-ttu-id="1cdde-203">下面是示例响应中，假定服务器允许请求：</span><span class="sxs-lookup"><span data-stu-id="1cdde-203">Here is an example response, assuming that the server allows the request:</span></span>

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

<span data-ttu-id="1cdde-204">响应包括访问的控制的允许的方法标头，其中列出了允许的方法，和 （可选） 访问的控制的允许的标头标头，其中列出了允许的标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-204">The response includes an Access-Control-Allow-Methods header that lists the allowed methods, and optionally an Access-Control-Allow-Headers header, which lists the allowed headers.</span></span> <span data-ttu-id="1cdde-205">如果预检请求成功，则浏览器发送实际请求，如前面所述。</span><span class="sxs-lookup"><span data-stu-id="1cdde-205">If the preflight request succeeds, the browser sends the actual request, as described earlier.</span></span>

<a id="scope"></a>
## <a name="scope-rules-for-enablecors"></a><span data-ttu-id="1cdde-206">[EnableCors] 的范围规则</span><span class="sxs-lookup"><span data-stu-id="1cdde-206">Scope Rules for [EnableCors]</span></span>

<span data-ttu-id="1cdde-207">可以在应用程序中每个操作，每个控制器，或全局范围内的所有 Web API 控制器启用 CORS。</span><span class="sxs-lookup"><span data-stu-id="1cdde-207">You can enable CORS per action, per controller, or globally for all Web API controllers in your application.</span></span>

<span data-ttu-id="1cdde-208">**每个操作**</span><span class="sxs-lookup"><span data-stu-id="1cdde-208">**Per Action**</span></span>

<span data-ttu-id="1cdde-209">若要为单个操作中启用 CORS，请设置 **[EnableCors]** 操作方法上的属性。</span><span class="sxs-lookup"><span data-stu-id="1cdde-209">To enable CORS for a single action, set the **[EnableCors]** attribute on the action method.</span></span> <span data-ttu-id="1cdde-210">下面的示例启用 CORS 的`GetItem`仅限方法。</span><span class="sxs-lookup"><span data-stu-id="1cdde-210">The following example enables CORS for the `GetItem` method only.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

<span data-ttu-id="1cdde-211">**每个控制器**</span><span class="sxs-lookup"><span data-stu-id="1cdde-211">**Per Controller**</span></span>

<span data-ttu-id="1cdde-212">如果您设置 **[EnableCors]** 控制器类，它适用于在控制器上的所有操作。</span><span class="sxs-lookup"><span data-stu-id="1cdde-212">If you set **[EnableCors]** on the controller class, it applies to all the actions on the controller.</span></span> <span data-ttu-id="1cdde-213">若要操作禁用 CORS，请添加 **[DisableCors]** 属性为该操作。</span><span class="sxs-lookup"><span data-stu-id="1cdde-213">To disable CORS for an action, add the **[DisableCors]** attribute to the action.</span></span> <span data-ttu-id="1cdde-214">下面的示例为每个方法，但启用 CORS `PutItem`。</span><span class="sxs-lookup"><span data-stu-id="1cdde-214">The following example enables CORS for every method except `PutItem`.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

<span data-ttu-id="1cdde-215">**全局**</span><span class="sxs-lookup"><span data-stu-id="1cdde-215">**Globally**</span></span>

<span data-ttu-id="1cdde-216">若要为应用程序中的所有 Web API 控制器中启用 CORS，请将传递**EnableCorsAttribute**实例向**EnableCors**方法：</span><span class="sxs-lookup"><span data-stu-id="1cdde-216">To enable CORS for all Web API controllers in your application, pass an **EnableCorsAttribute** instance to the **EnableCors** method:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

<span data-ttu-id="1cdde-217">如果在多个作用域设置属性，优先顺序是：</span><span class="sxs-lookup"><span data-stu-id="1cdde-217">If you set the attribute at more than one scope, the order of precedence is:</span></span>

1. <span data-ttu-id="1cdde-218">操作</span><span class="sxs-lookup"><span data-stu-id="1cdde-218">Action</span></span>
2. <span data-ttu-id="1cdde-219">控制器</span><span class="sxs-lookup"><span data-stu-id="1cdde-219">Controller</span></span>
3. <span data-ttu-id="1cdde-220">Global</span><span class="sxs-lookup"><span data-stu-id="1cdde-220">Global</span></span>

<a id="allowed-origins"></a>
## <a name="set-the-allowed-origins"></a><span data-ttu-id="1cdde-221">设置允许的来源</span><span class="sxs-lookup"><span data-stu-id="1cdde-221">Set the Allowed Origins</span></span>

<span data-ttu-id="1cdde-222">*来源*的参数 **[EnableCors]** 属性指定允许哪些域访问资源。</span><span class="sxs-lookup"><span data-stu-id="1cdde-222">The *origins* parameter of the **[EnableCors]** attribute specifies which origins are allowed to access the resource.</span></span> <span data-ttu-id="1cdde-223">值为逗号分隔的允许的来源列表。</span><span class="sxs-lookup"><span data-stu-id="1cdde-223">The value is a comma-separated list of the allowed origins.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

<span data-ttu-id="1cdde-224">此外可以使用通配符值"\*"若要允许来自任何来源的请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-224">You can also use the wildcard value "\*" to allow requests from any origins.</span></span>

<span data-ttu-id="1cdde-225">允许任何来源的请求之前，请仔细考虑。</span><span class="sxs-lookup"><span data-stu-id="1cdde-225">Consider carefully before allowing requests from any origin.</span></span> <span data-ttu-id="1cdde-226">这意味着几乎任何网站可以向你的 web API 的 AJAX 调用。</span><span class="sxs-lookup"><span data-stu-id="1cdde-226">It means that literally any website can make AJAX calls to your web API.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

<a id="allowed-methods"></a>
## <a name="set-the-allowed-http-methods"></a><span data-ttu-id="1cdde-227">设置允许的 HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="1cdde-227">Set the Allowed HTTP Methods</span></span>

<span data-ttu-id="1cdde-228">*方法*的参数 **[EnableCors]** 属性指定的 HTTP 方法允许访问资源。</span><span class="sxs-lookup"><span data-stu-id="1cdde-228">The *methods* parameter of the **[EnableCors]** attribute specifies which HTTP methods are allowed to access the resource.</span></span> <span data-ttu-id="1cdde-229">若要允许所有方法，使用通配符值"\*"。</span><span class="sxs-lookup"><span data-stu-id="1cdde-229">To allow all methods, use the wildcard value "\*".</span></span> <span data-ttu-id="1cdde-230">以下示例允许只有 GET 和 POST 的请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-230">The following example allows only GET and POST requests.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

<a id="allowed-request-headers"></a>
## <a name="set-the-allowed-request-headers"></a><span data-ttu-id="1cdde-231">设置允许的请求标头</span><span class="sxs-lookup"><span data-stu-id="1cdde-231">Set the Allowed Request Headers</span></span>

<span data-ttu-id="1cdde-232">前面我介绍了如何预检请求可能包括访问控制的请求标头的标头，列出应用程序设置的 HTTP 标头 (所谓"author 请求标头")。</span><span class="sxs-lookup"><span data-stu-id="1cdde-232">Earlier I described how a preflight request might include an Access-Control-Request-Headers header, listing the HTTP headers set by the application (the so-called "author request headers").</span></span> <span data-ttu-id="1cdde-233">*标头*的参数 **[EnableCors]** 属性指定允许哪些作者请求标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-233">The *headers* parameter of the **[EnableCors]** attribute specifies which author request headers are allowed.</span></span> <span data-ttu-id="1cdde-234">若要允许任何标头，设置*标头*到"\*"。</span><span class="sxs-lookup"><span data-stu-id="1cdde-234">To allow any headers, set *headers* to "\*".</span></span> <span data-ttu-id="1cdde-235">到允许列表特定的标头，设置*标头*以逗号分隔列表的允许的标头：</span><span class="sxs-lookup"><span data-stu-id="1cdde-235">To whitelist specific headers, set *headers* to a comma-separated list of the allowed headers:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

<span data-ttu-id="1cdde-236">但是，浏览器不是它们如何设置访问控制的请求标头中完全一致的。</span><span class="sxs-lookup"><span data-stu-id="1cdde-236">However, browsers are not entirely consistent in how they set Access-Control-Request-Headers.</span></span> <span data-ttu-id="1cdde-237">例如，Chrome 当前包括"origin";虽然 FireFox 不包括标准标头，如"接受"，即使应用程序将它们设置在脚本中。</span><span class="sxs-lookup"><span data-stu-id="1cdde-237">For example, Chrome currently includes "origin"; while FireFox does not include standard headers such as "Accept", even when the application sets them in script.</span></span>

<span data-ttu-id="1cdde-238">如果您设置*标头*以外的其他任何内容"\*"，您至少应包含"接受"，"内容类型"，，和"源"，以及你想要支持任何自定义标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-238">If you set *headers* to anything other than "\*", you should include at least "accept", "content-type", and "origin", plus any custom headers that you want to support.</span></span>

<a id="allowed-response-headers"></a>
## <a name="set-the-allowed-response-headers"></a><span data-ttu-id="1cdde-239">设置允许的响应标头</span><span class="sxs-lookup"><span data-stu-id="1cdde-239">Set the Allowed Response Headers</span></span>

<span data-ttu-id="1cdde-240">默认情况下，在浏览器不公开所有向应用程序的响应标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-240">By default, the browser does not expose all of the response headers to the application.</span></span> <span data-ttu-id="1cdde-241">默认情况下可用的响应标头是：</span><span class="sxs-lookup"><span data-stu-id="1cdde-241">The response headers that are available by default are:</span></span>

- <span data-ttu-id="1cdde-242">Cache-Control</span><span class="sxs-lookup"><span data-stu-id="1cdde-242">Cache-Control</span></span>
- <span data-ttu-id="1cdde-243">内容语言</span><span class="sxs-lookup"><span data-stu-id="1cdde-243">Content-Language</span></span>
- <span data-ttu-id="1cdde-244">Content-Type</span><span class="sxs-lookup"><span data-stu-id="1cdde-244">Content-Type</span></span>
- <span data-ttu-id="1cdde-245">过期</span><span class="sxs-lookup"><span data-stu-id="1cdde-245">Expires</span></span>
- <span data-ttu-id="1cdde-246">上次修改</span><span class="sxs-lookup"><span data-stu-id="1cdde-246">Last-Modified</span></span>
- <span data-ttu-id="1cdde-247">杂注</span><span class="sxs-lookup"><span data-stu-id="1cdde-247">Pragma</span></span>

<span data-ttu-id="1cdde-248">CORS 规范调用这些[简单响应标头](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)。</span><span class="sxs-lookup"><span data-stu-id="1cdde-248">The CORS spec calls these [simple response headers](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header).</span></span> <span data-ttu-id="1cdde-249">若要使其他标头可用于应用程序，设置*exposedHeaders*的参数 **[EnableCors]**。</span><span class="sxs-lookup"><span data-stu-id="1cdde-249">To make other headers available to the application, set the *exposedHeaders* parameter of **[EnableCors]**.</span></span>

<span data-ttu-id="1cdde-250">在以下示例中，控制器的`Get`方法设置名为 X-自定义的标头的自定义标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-250">In the following example, the controller's `Get` method sets a custom header named ‘X-Custom-Header'.</span></span> <span data-ttu-id="1cdde-251">默认情况下，在浏览器将公开此标头中的跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-251">By default, the browser will not expose this header in a cross-origin request.</span></span> <span data-ttu-id="1cdde-252">若要使标头，包括 X-自定义的标头中*exposedHeaders*。</span><span class="sxs-lookup"><span data-stu-id="1cdde-252">To make the header available, include ‘X-Custom-Header' in *exposedHeaders*.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

<a id="credentials"></a>
## <a name="passing-credentials-in-cross-origin-requests"></a><span data-ttu-id="1cdde-253">跨域请求中传递凭据</span><span class="sxs-lookup"><span data-stu-id="1cdde-253">Passing Credentials in Cross-Origin Requests</span></span>

<span data-ttu-id="1cdde-254">凭据要求特殊处理 CORS 请求中。</span><span class="sxs-lookup"><span data-stu-id="1cdde-254">Credentials require special handling in a CORS request.</span></span> <span data-ttu-id="1cdde-255">默认情况下，在浏览器不发送任何凭据与跨域请求。</span><span class="sxs-lookup"><span data-stu-id="1cdde-255">By default, the browser does not send any credentials with a cross-origin request.</span></span> <span data-ttu-id="1cdde-256">凭据包含 cookie，以及 HTTP 身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="1cdde-256">Credentials include cookies as well as HTTP authentication schemes.</span></span> <span data-ttu-id="1cdde-257">若要将发送具有跨源请求的凭据，客户端必须设置**XMLHttpRequest.withCredentials**为 true。</span><span class="sxs-lookup"><span data-stu-id="1cdde-257">To send credentials with a cross-origin request, the client must set **XMLHttpRequest.withCredentials** to true.</span></span>

<span data-ttu-id="1cdde-258">使用**XMLHttpRequest**直接：</span><span class="sxs-lookup"><span data-stu-id="1cdde-258">Using **XMLHttpRequest** directly:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

<span data-ttu-id="1cdde-259">在 jQuery 中：</span><span class="sxs-lookup"><span data-stu-id="1cdde-259">In jQuery:</span></span>

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

<span data-ttu-id="1cdde-260">此外，服务器必须允许凭据。</span><span class="sxs-lookup"><span data-stu-id="1cdde-260">In addition, the server must allow the credentials.</span></span> <span data-ttu-id="1cdde-261">若要允许 Web API 中的跨域凭据，请设置**SupportsCredentials**属性设置为 true **[EnableCors]** 属性：</span><span class="sxs-lookup"><span data-stu-id="1cdde-261">To allow cross-origin credentials in Web API, set the **SupportsCredentials** property to true on the **[EnableCors]** attribute:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

<span data-ttu-id="1cdde-262">如果此属性为 true，HTTP 响应将包括一个访问控制的允许的凭据标头。</span><span class="sxs-lookup"><span data-stu-id="1cdde-262">If this property is true, the HTTP response will include an Access-Control-Allow-Credentials header.</span></span> <span data-ttu-id="1cdde-263">此标头告知浏览器的服务器允许跨域请求凭据。</span><span class="sxs-lookup"><span data-stu-id="1cdde-263">This header tells the browser that the server allows credentials for a cross-origin request.</span></span>

<span data-ttu-id="1cdde-264">如果浏览器发送的凭据，但响应不包含有效的访问控制的允许的凭据标头，在浏览器并不会对该应用程序的响应和 AJAX 请求失败。</span><span class="sxs-lookup"><span data-stu-id="1cdde-264">If the browser sends credentials, but the response does not include a valid Access-Control-Allow-Credentials header, the browser will not expose the response to the application, and the AJAX request fails.</span></span>

<span data-ttu-id="1cdde-265">要设置非常谨慎**SupportsCredentials**为 true，因为这意味着在另一个域的网站可以不在用户不知情的情况下对用户的名义，Web API 发送登录的用户的凭据。</span><span class="sxs-lookup"><span data-stu-id="1cdde-265">Be very careful about setting **SupportsCredentials** to true, because it means a website at another domain can send a logged-in user's credentials to your Web API on the user's behalf, without the user being aware.</span></span> <span data-ttu-id="1cdde-266">CORS 规范还会说明该设置*来源*到&quot; \* &quot;无效如果**SupportsCredentials**为 true。</span><span class="sxs-lookup"><span data-stu-id="1cdde-266">The CORS spec also states that setting *origins* to &quot;\*&quot; is invalid if **SupportsCredentials** is true.</span></span>

<a id="cors-policy-providers"></a>
## <a name="custom-cors-policy-providers"></a><span data-ttu-id="1cdde-267">自定义 CORS 策略提供程序</span><span class="sxs-lookup"><span data-stu-id="1cdde-267">Custom CORS Policy Providers</span></span>

<span data-ttu-id="1cdde-268">**[EnableCors]** 特性实现**ICorsPolicyProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="1cdde-268">The **[EnableCors]** attribute implements the **ICorsPolicyProvider** interface.</span></span> <span data-ttu-id="1cdde-269">您可以通过创建派生的类提供您自己的实现**特性**并实现**ICorsProlicyProvider**。</span><span class="sxs-lookup"><span data-stu-id="1cdde-269">You can provide your own implementation by creating a class that derives from **Attribute** and implements **ICorsProlicyProvider**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

<span data-ttu-id="1cdde-270">现在可以应用任何位置，可使该属性 **[EnableCors]**。</span><span class="sxs-lookup"><span data-stu-id="1cdde-270">Now you can apply the attribute any place that you would put **[EnableCors]**.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

<span data-ttu-id="1cdde-271">例如，自定义 CORS 策略提供程序无法从配置文件读取设置。</span><span class="sxs-lookup"><span data-stu-id="1cdde-271">For example, a custom CORS policy provider could read the settings from a configuration file.</span></span>

<span data-ttu-id="1cdde-272">作为使用属性的替代方法，可以注册**ICorsPolicyProviderFactory**创建的对象**ICorsPolicyProvider**对象。</span><span class="sxs-lookup"><span data-stu-id="1cdde-272">As an alternative to using attributes, you can register an **ICorsPolicyProviderFactory** object that creates **ICorsPolicyProvider** objects.</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

<span data-ttu-id="1cdde-273">若要设置**ICorsPolicyProviderFactory**，调用**SetCorsPolicyProviderFactory**扩展方法在启动时，按如下所示：</span><span class="sxs-lookup"><span data-stu-id="1cdde-273">To set the **ICorsPolicyProviderFactory**, call the **SetCorsPolicyProviderFactory** extension method at startup, as follows:</span></span>

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

<a id="browser-support"></a>
## <a name="browser-support"></a><span data-ttu-id="1cdde-274">浏览器支持</span><span class="sxs-lookup"><span data-stu-id="1cdde-274">Browser Support</span></span>

<span data-ttu-id="1cdde-275">Web API CORS 包是一种服务器端技术。</span><span class="sxs-lookup"><span data-stu-id="1cdde-275">The Web API CORS package is a server-side technology.</span></span> <span data-ttu-id="1cdde-276">用户的浏览器还需要支持 CORS。</span><span class="sxs-lookup"><span data-stu-id="1cdde-276">The user's browser also needs to support CORS.</span></span> <span data-ttu-id="1cdde-277">幸运的是，所有主要浏览器的当前版本包括[CORS 的支持](http://caniuse.com/cors)。</span><span class="sxs-lookup"><span data-stu-id="1cdde-277">Fortunately, the current versions of all major browsers include [support for CORS](http://caniuse.com/cors).</span></span>

<span data-ttu-id="1cdde-278">Internet Explorer 8 和 Internet Explorer 9 具有部分支持 CORS，而不 XMLHttpRequest 使用旧的 XDomainRequest 对象。</span><span class="sxs-lookup"><span data-stu-id="1cdde-278">Internet Explorer 8 and Internet Explorer 9 have partial support for CORS, using the legacy XDomainRequest object instead of XMLHttpRequest.</span></span> <span data-ttu-id="1cdde-279">有关详细信息，请参阅[XDomainRequest-限制、 限制和解决方法](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1cdde-279">For more information, see [XDomainRequest - Restrictions, Limitations and Workarounds](https://blogs.msdn.com/b/ieinternals/archive/2010/05/13/xdomainrequest-restrictions-limitations-and-workarounds.aspx).</span></span>
