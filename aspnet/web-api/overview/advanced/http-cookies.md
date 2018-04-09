---
uid: web-api/overview/advanced/http-cookies
title: 在 ASP.NET Web API 的 HTTP Cookie |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/17/2012
ms.topic: article
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 363ca975cf75b635b766a53eeda87cf957eed60c
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
<a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="174db-102">在 ASP.NET Web API 的 HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="174db-102">HTTP Cookies in ASP.NET Web API</span></span>
====================
<span data-ttu-id="174db-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="174db-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="174db-104">本主题介绍如何发送和接收 Web API 中的 HTTP cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-104">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="174db-105">HTTP Cookie 的背景信息</span><span class="sxs-lookup"><span data-stu-id="174db-105">Background on HTTP Cookies</span></span>

<span data-ttu-id="174db-106">本部分提供了 cookie 在 HTTP 级别的实现方式的简要概述。</span><span class="sxs-lookup"><span data-stu-id="174db-106">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="174db-107">有关详细信息，请查阅[RFC 6265](http://tools.ietf.org/html/rfc6265)。</span><span class="sxs-lookup"><span data-stu-id="174db-107">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="174db-108">Cookie 是一种服务器发送的 HTTP 响应中的数据。</span><span class="sxs-lookup"><span data-stu-id="174db-108">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="174db-109">客户端 （可选） 将存储在 cookie 并根据 subsequet 请求对其进行返回。</span><span class="sxs-lookup"><span data-stu-id="174db-109">The client (optionally) stores the cookie and returns it on subsequet requests.</span></span> <span data-ttu-id="174db-110">这允许客户端和服务器共享状态。</span><span class="sxs-lookup"><span data-stu-id="174db-110">This allows the client and server to share state.</span></span> <span data-ttu-id="174db-111">若要设置一个 cookie，服务器，请在响应中包含集 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="174db-111">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="174db-112">Cookie 的格式是名称 / 值对，具有可选特性。</span><span class="sxs-lookup"><span data-stu-id="174db-112">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="174db-113">例如：</span><span class="sxs-lookup"><span data-stu-id="174db-113">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="174db-114">下面是包含属性的一个示例：</span><span class="sxs-lookup"><span data-stu-id="174db-114">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="174db-115">若要返回到服务器的 cookie，客户端，请在更高版本的请求中包含 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="174db-115">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="174db-116">HTTP 响应可以包括多个集 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="174db-116">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="174db-117">客户端返回使用单个 Cookie 标头的多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-117">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="174db-118">作用域和持续时间 cookie 受集 Cookie 标头中的以下属性：</span><span class="sxs-lookup"><span data-stu-id="174db-118">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="174db-119">**域**： 告知客户端的域应接收的 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-119">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="174db-120">例如，如果"example.com"域，则客户端会将 cookie 返回给每个子域 example.com。如果未指定，则域是源服务器。</span><span class="sxs-lookup"><span data-stu-id="174db-120">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com. If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="174db-121">**路径**： 将 cookie 限制为在域中指定的路径。</span><span class="sxs-lookup"><span data-stu-id="174db-121">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="174db-122">如果未指定，则使用请求 URI 的路径。</span><span class="sxs-lookup"><span data-stu-id="174db-122">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="174db-123">**过期**： 设置的 cookie 的到期日期。</span><span class="sxs-lookup"><span data-stu-id="174db-123">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="174db-124">当它过期时，客户端将删除 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-124">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="174db-125">**最大有效期**： 设置的 cookie 的最长时间。</span><span class="sxs-lookup"><span data-stu-id="174db-125">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="174db-126">在到达最大存留期时，客户端将删除 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-126">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="174db-127">如果这两个`Expires`和`Max-Age`设置，`Max-Age`优先。</span><span class="sxs-lookup"><span data-stu-id="174db-127">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="174db-128">如果两者均未设置，客户端将在当前会话结束时删除 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-128">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="174db-129">（"会话"的确切含义确定用户代理中）。</span><span class="sxs-lookup"><span data-stu-id="174db-129">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="174db-130">但是，请注意客户端可能会忽略 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-130">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="174db-131">例如，用户可能会禁用隐私原因的 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-131">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="174db-132">客户端可能会删除 cookie 之前到期，或限制的存储的 cookie 数。</span><span class="sxs-lookup"><span data-stu-id="174db-132">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="174db-133">出于隐私原因，客户端通常拒绝"第三方"cookie，其中域与源服务器不匹配。</span><span class="sxs-lookup"><span data-stu-id="174db-133">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="174db-134">简单地说，服务器不应依赖于取回它所设置的 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="174db-134">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="174db-135">Web API 中的 cookie</span><span class="sxs-lookup"><span data-stu-id="174db-135">Cookies in Web API</span></span>

<span data-ttu-id="174db-136">若要将 cookie 添加到 HTTP 响应中，创建**CookieHeaderValue**表示该 cookie 的实例。</span><span class="sxs-lookup"><span data-stu-id="174db-136">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="174db-137">然后调用**AddCookies**中定义的扩展方法**System.Net.Http。HttpResponseHeadersExtensions**类中，以添加该 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-137">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="174db-138">例如，下面的代码将添加一个 cookie 中的控制器操作：</span><span class="sxs-lookup"><span data-stu-id="174db-138">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="174db-139">请注意， **AddCookies**采用的数组**CookieHeaderValue**实例。</span><span class="sxs-lookup"><span data-stu-id="174db-139">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="174db-140">若要从客户端请求中提取 cookie，调用**GetCookies**方法：</span><span class="sxs-lookup"><span data-stu-id="174db-140">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="174db-141">A **CookieHeaderValue**包含一套**CookieState**实例。</span><span class="sxs-lookup"><span data-stu-id="174db-141">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="174db-142">每个**CookieState**表示一个 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-142">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="174db-143">使用索引器方法来获取**CookieState**按名称，如所示。</span><span class="sxs-lookup"><span data-stu-id="174db-143">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="174db-144">结构化的 Cookie 数据</span><span class="sxs-lookup"><span data-stu-id="174db-144">Structured Cookie Data</span></span>

<span data-ttu-id="174db-145">很多浏览器限制它们将存储的多少 cookie&#8212;总数，以及每个域的数量。</span><span class="sxs-lookup"><span data-stu-id="174db-145">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="174db-146">因此，它可用于将结构化的数据置于一个 cookie，而不是设置多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-146">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="174db-147">RFC 6265 未定义 cookie 数据的结构。</span><span class="sxs-lookup"><span data-stu-id="174db-147">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="174db-148">使用**CookieHeaderValue**类，你可以将传递 cookie 数据的名称-值对的列表。</span><span class="sxs-lookup"><span data-stu-id="174db-148">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="174db-149">这些名称-值对被编码为 URL 编码格式集 Cookie 标头中的数据：</span><span class="sxs-lookup"><span data-stu-id="174db-149">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="174db-150">前面的代码生成以下集 Cookie 标头：</span><span class="sxs-lookup"><span data-stu-id="174db-150">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="174db-151">**CookieState**类提供了用于从请求消息的 cookie 中读取子值的索引器方法：</span><span class="sxs-lookup"><span data-stu-id="174db-151">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="174db-152">示例： 设置和检索在消息处理程序的 Cookie</span><span class="sxs-lookup"><span data-stu-id="174db-152">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="174db-153">前面的示例显示如何使用从 Web API 控制器中的 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-153">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="174db-154">另一个选项是使用[消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="174db-154">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="174db-155">在比控制器管道的前面部分中都调用消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="174db-155">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="174db-156">消息处理程序可以读取请求的 cookie 之前请求到达控制器，, 或添加到响应的 cookie，控制器将生成响应后。</span><span class="sxs-lookup"><span data-stu-id="174db-156">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="174db-157">下面的代码演示的消息处理程序创建的会话 Id。</span><span class="sxs-lookup"><span data-stu-id="174db-157">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="174db-158">会话 ID 存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="174db-158">The session ID is stored in a cookie.</span></span> <span data-ttu-id="174db-159">处理程序检查会话 cookie 的请求。</span><span class="sxs-lookup"><span data-stu-id="174db-159">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="174db-160">如果请求不包括该 cookie，该处理程序将生成一个新的会话 id。</span><span class="sxs-lookup"><span data-stu-id="174db-160">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="174db-161">在任一情况下，该处理程序存储中的会话 ID **HttpRequestMessage.Properties**属性包。</span><span class="sxs-lookup"><span data-stu-id="174db-161">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="174db-162">它还添加到 HTTP 响应的会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="174db-162">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="174db-163">此实现不会验证服务器实际颁发从客户端的会话 ID。</span><span class="sxs-lookup"><span data-stu-id="174db-163">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="174db-164">不使用它为窗体的身份验证 ！</span><span class="sxs-lookup"><span data-stu-id="174db-164">Don't use it as a form of authentication!</span></span> <span data-ttu-id="174db-165">该示例的点是显示 HTTP cookie 管理。</span><span class="sxs-lookup"><span data-stu-id="174db-165">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="174db-166">控制器可以获取会话 ID 从**HttpRequestMessage.Properties**属性包。</span><span class="sxs-lookup"><span data-stu-id="174db-166">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
