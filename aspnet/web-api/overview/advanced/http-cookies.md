---
uid: web-api/overview/advanced/http-cookies
title: ASP.NET Web API 中的 HTTP Cookie |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 09/17/2012
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 21ba186c11f39bbeedd1c320b98476ba13af27e2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819155"
---
<a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="11685-102">ASP.NET Web API 中的 HTTP Cookie</span><span class="sxs-lookup"><span data-stu-id="11685-102">HTTP Cookies in ASP.NET Web API</span></span>
====================
<span data-ttu-id="11685-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="11685-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="11685-104">本主题介绍如何发送和接收 Web API 中的 HTTP cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-104">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="11685-105">HTTP Cookie 的背景信息</span><span class="sxs-lookup"><span data-stu-id="11685-105">Background on HTTP Cookies</span></span>

<span data-ttu-id="11685-106">本部分提供 cookie 在 HTTP 级别的实现方式的简要的概述。</span><span class="sxs-lookup"><span data-stu-id="11685-106">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="11685-107">有关详细信息，请查阅[RFC 6265](http://tools.ietf.org/html/rfc6265)。</span><span class="sxs-lookup"><span data-stu-id="11685-107">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="11685-108">Cookie 是一种服务器发送的 HTTP 响应中的数据。</span><span class="sxs-lookup"><span data-stu-id="11685-108">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="11685-109">客户端 （可选） 将存储在 cookie，并返回对 subsequet 请求。</span><span class="sxs-lookup"><span data-stu-id="11685-109">The client (optionally) stores the cookie and returns it on subsequet requests.</span></span> <span data-ttu-id="11685-110">这允许客户端和服务器共享状态。</span><span class="sxs-lookup"><span data-stu-id="11685-110">This allows the client and server to share state.</span></span> <span data-ttu-id="11685-111">若要设置一个 cookie，服务器在响应中包含的 Set-cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="11685-111">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="11685-112">Cookie 的格式是一个名称-值对，具有可选特性。</span><span class="sxs-lookup"><span data-stu-id="11685-112">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="11685-113">例如：</span><span class="sxs-lookup"><span data-stu-id="11685-113">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="11685-114">下面是包含属性的一个示例：</span><span class="sxs-lookup"><span data-stu-id="11685-114">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="11685-115">若要返回到服务器的 cookie，客户端在更高版本的请求中包括 Cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="11685-115">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="11685-116">HTTP 响应可以包括多个 Set-cookie 标头。</span><span class="sxs-lookup"><span data-stu-id="11685-116">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="11685-117">客户端返回使用单一的 Cookie 标头的多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-117">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="11685-118">作用域和 cookie 的持续时间受 Set-cookie 标头中的以下属性：</span><span class="sxs-lookup"><span data-stu-id="11685-118">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="11685-119">**域**： 告知客户端的域应接收 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-119">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="11685-120">例如，如果域为"example.com"，客户端将 cookie 返回给每个子域 example.com。</span><span class="sxs-lookup"><span data-stu-id="11685-120">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="11685-121">如果未指定，域是源服务器。</span><span class="sxs-lookup"><span data-stu-id="11685-121">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="11685-122">**路径**： 将 cookie 限制为在域中指定的路径。</span><span class="sxs-lookup"><span data-stu-id="11685-122">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="11685-123">如果未指定，则使用请求 URI 的路径。</span><span class="sxs-lookup"><span data-stu-id="11685-123">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="11685-124">**过期**： 设置 cookie 的到期日期。</span><span class="sxs-lookup"><span data-stu-id="11685-124">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="11685-125">当它过期时，客户端删除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-125">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="11685-126">**最大期限**： 设置 cookie 的最大生存期。</span><span class="sxs-lookup"><span data-stu-id="11685-126">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="11685-127">当它达到最大期限时，客户端删除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-127">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="11685-128">如果这两个`Expires`并`Max-Age`设置，`Max-Age`优先。</span><span class="sxs-lookup"><span data-stu-id="11685-128">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="11685-129">如果未设置，客户端将在当前会话结束时删除的 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-129">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="11685-130">（"会话"的确切含义由确定用户代理。）</span><span class="sxs-lookup"><span data-stu-id="11685-130">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="11685-131">但是，请注意，客户端可能会忽略 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-131">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="11685-132">例如，用户可能会禁用 cookie 出于隐私原因。</span><span class="sxs-lookup"><span data-stu-id="11685-132">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="11685-133">客户端可能会删除 cookie 之前到期，或限制 cookie 存储数。</span><span class="sxs-lookup"><span data-stu-id="11685-133">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="11685-134">出于隐私原因，客户端通常会拒绝"第三方"cookie，其中域与源服务器不匹配。</span><span class="sxs-lookup"><span data-stu-id="11685-134">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="11685-135">简单地说，服务器不应依赖于取回其设置的 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-135">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="11685-136">Web API 中的 cookie</span><span class="sxs-lookup"><span data-stu-id="11685-136">Cookies in Web API</span></span>

<span data-ttu-id="11685-137">若要添加到 HTTP 响应 cookie，创建**CookieHeaderValue**实例，它表示 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-137">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="11685-138">然后调用**AddCookies**扩展方法，它定义在**System.Net.Http。HttpResponseHeadersExtensions**类中，以添加该 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-138">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="11685-139">例如，下面的代码将添加的 cookie 中的控制器操作：</span><span class="sxs-lookup"><span data-stu-id="11685-139">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="11685-140">请注意， **AddCookies**采用的数组**CookieHeaderValue**实例。</span><span class="sxs-lookup"><span data-stu-id="11685-140">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="11685-141">若要从客户端请求中提取 cookie，调用**GetCookies**方法：</span><span class="sxs-lookup"><span data-stu-id="11685-141">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="11685-142">一个**CookieHeaderValue**包含一系列**CookieState**实例。</span><span class="sxs-lookup"><span data-stu-id="11685-142">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="11685-143">每个**CookieState**表示一个 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-143">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="11685-144">使用索引器方法来获取**CookieState**按名称，如所示。</span><span class="sxs-lookup"><span data-stu-id="11685-144">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="11685-145">结构化的 Cookie 数据</span><span class="sxs-lookup"><span data-stu-id="11685-145">Structured Cookie Data</span></span>

<span data-ttu-id="11685-146">很多浏览器限制它们将存储多少 cookie&#8212;总数，以及每个域数。</span><span class="sxs-lookup"><span data-stu-id="11685-146">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="11685-147">因此，它可用于结构化的数据置于单个 cookie，而不是设置多个 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-147">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="11685-148">RFC 6265 未定义 cookie 数据的结构。</span><span class="sxs-lookup"><span data-stu-id="11685-148">RFC 6265 does not define the structure of cookie data.</span></span>


<span data-ttu-id="11685-149">使用**CookieHeaderValue**类，您可以将传递 cookie 数据的名称-值对的列表。</span><span class="sxs-lookup"><span data-stu-id="11685-149">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="11685-150">这些名称 / 值对编码为 URL 编码格式的 Set-cookie 标头中的数据：</span><span class="sxs-lookup"><span data-stu-id="11685-150">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="11685-151">前面的代码生成以下的 Set-cookie 标头：</span><span class="sxs-lookup"><span data-stu-id="11685-151">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="11685-152">**CookieState**类提供了索引器的方法： 从请求消息中的 cookie 中读取子值：</span><span class="sxs-lookup"><span data-stu-id="11685-152">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="11685-153">示例： 设置和检索消息处理程序中的 Cookie</span><span class="sxs-lookup"><span data-stu-id="11685-153">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="11685-154">前面的示例显示如何使用从 Web API 控制器中的 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-154">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="11685-155">另一种方法是使用[消息处理程序](http-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="11685-155">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="11685-156">前面在控制器与管道中调用的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="11685-156">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="11685-157">消息处理程序可以请求到达控制器之前, 从请求中读取 cookie 或控制器生成响应后向响应添加 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-157">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="11685-158">下面的代码演示创建的会话 Id 的消息处理程序。</span><span class="sxs-lookup"><span data-stu-id="11685-158">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="11685-159">会话 ID 存储在 cookie 中。</span><span class="sxs-lookup"><span data-stu-id="11685-159">The session ID is stored in a cookie.</span></span> <span data-ttu-id="11685-160">处理程序进行检查的会话 cookie 的请求。</span><span class="sxs-lookup"><span data-stu-id="11685-160">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="11685-161">如果请求不包含 cookie，该处理程序将生成一个新的会话 id。</span><span class="sxs-lookup"><span data-stu-id="11685-161">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="11685-162">在任一情况下，处理程序存储中的会话 ID **HttpRequestMessage.Properties**属性包。</span><span class="sxs-lookup"><span data-stu-id="11685-162">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="11685-163">它还添加到 HTTP 响应的会话 cookie。</span><span class="sxs-lookup"><span data-stu-id="11685-163">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="11685-164">此实现不会验证从客户端的会话 ID 实际上由服务器颁发。</span><span class="sxs-lookup"><span data-stu-id="11685-164">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="11685-165">不将其用作形式的身份验证 ！</span><span class="sxs-lookup"><span data-stu-id="11685-165">Don't use it as a form of authentication!</span></span> <span data-ttu-id="11685-166">此示例的重点是显示 HTTP cookie 管理。</span><span class="sxs-lookup"><span data-stu-id="11685-166">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="11685-167">控制器可以获取会话 ID **HttpRequestMessage.Properties**属性包。</span><span class="sxs-lookup"><span data-stu-id="11685-167">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]
