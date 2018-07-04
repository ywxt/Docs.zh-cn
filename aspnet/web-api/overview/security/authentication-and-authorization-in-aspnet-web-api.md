---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: 身份验证和 ASP.NET Web API 中的授权 |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 中提供身份验证和授权的一般的概述。
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/27/2012
ms.topic: article
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 981eebeaa1daaf85cb90a52f073c88cb71099edb
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365615"
---
<a name="authentication-and-authorization-in-aspnet-web-api"></a>身份验证和 ASP.NET Web API 中的授权
====================
通过[Mike Wasson](https://github.com/MikeWasson)

您已经创建的 web API，但现在你想要控制对它的访问。 在本系列的文章，我们将介绍一些选项用于保护 web API 从未经授权的用户。 本系列教程将介绍身份验证和授权。

- *身份验证*知道用户的标识。 例如，Alice 使用她的用户名和密码，登录和服务器使用密码进行身份验证 Alice。
- *授权*确定是否允许用户执行的操作。 例如，Alice 有权获取资源，但不是创建资源。

序列中的第一篇文章为 ASP.NET Web API 中提供了身份验证和授权的一般概述。 其他主题介绍的 Web API 的常见身份验证方案。

> [!NOTE]
> 衷心感谢查看这一系列和提供有价值的反馈的人员： Rick Anderson、 Levi Broderick、 Barry Dorrans、 Tom Dykstra、 Hongmei Ge、 David Matson、 Daniel Roth、 Tim Teebken。


## <a name="authentication"></a>身份验证

Web API 假定该身份验证发生在主机中。 对于 web 承载的该主机是 IIS，使用 HTTP 模块进行身份验证。 可以将项目配置为使用任何 IIS 或 ASP.NET 中，在中内置的身份验证模块，也可以编写自己的 HTTP 模块来执行自定义身份验证。

当主机对用户进行身份验证时，它会创建*主体*，即[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)表示运行代码的安全上下文的对象。 主机的设置将主体附加到当前线程**Thread.CurrentPrincipal**。 主体包含一个关联**标识**对象，其中包含有关用户的信息。 如果用户进行身份验证， **Identity.IsAuthenticated**属性将返回**true**。 对于匿名请求，请**IsAuthenticated**返回**false**。 有关主体的详细信息，请参阅[基于角色的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。

### <a name="http-message-handlers-for-authentication"></a>HTTP 消息处理程序进行身份验证

而不是使用主机进行身份验证，您可以将身份验证逻辑注入[HTTP 消息处理程序](../advanced/http-message-handlers.md)。 在这种情况下，消息处理程序将检查 HTTP 请求和设置的主体。

何时应使用消息处理程序进行身份验证？ 下面是一些相关的利弊：

- 一个 HTTP 模块，会看到通过 ASP.NET 管道的所有请求。 消息处理程序只看到路由到 Web API 的请求。
- 可以该对话框允许你将身份验证方案应用于特定的路由设置每个路由消息处理程序。
- HTTP 模块是特定于 IIS。 消息处理程序主机不可知的以便它们可以与 web 宿主和自承载使用。
- HTTP 模块加入 IIS 日志记录、 审核和等等。
- HTTP 模块前面在管道中运行。 如果处理消息处理程序中的身份验证，该主体不会不获取或设置处理程序运行之前。 此外，该主体会还原为以前的主体时在响应离开消息处理程序。

通常情况下，如果您不需要以支持自托管，HTTP 模块是更好的选择。 如果你需要支持自托管，请考虑消息处理程序。

### <a name="setting-the-principal"></a>设置主体

如果你的应用程序执行的任何自定义身份验证逻辑，则必须在两个位置上设置主体：

- **Thread.CurrentPrincipal**。 此属性是在.NET 中设置线程的主体的标准方法。
- **HttpContext.Current.User**。 此属性是特定于 ASP.NET。

下面的代码演示如何设置主体：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

对于 web 承载的必须设置主体，在这两个位置;否则的安全上下文可能会变得不一致。 对于自承载，但是， **HttpContext.Current**为 null。 若要确保你的代码与主机无关，因此之前, 检查 null 分配到**HttpContext.Current**，如下所示。

## <a name="authorization"></a>授权

授权发生在管道中，更高版本更接近于该控制器。 允许您授予对资源的访问时进行更精细的选择。

- *授权筛选器*控制器操作之前运行。 如果请求未获得授权，筛选器返回错误响应，并不调用操作。
- 中的控制器操作，可以获取从当前的主体**ApiController.User**属性。 例如，您可能会筛选基于用户名称的资源的列表返回属于该用户的资源。

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a>使用 [授权] 属性

Web API 提供了内置的授权筛选器， [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。 此筛选器检查用户进行身份验证。 如果没有，它将返回 HTTP 状态代码 401 （未经授权），而无需调用该操作。

您可以应用筛选器全局范围内，在控制器级别，或在单个操作级别。

**全局**： 若要限制访问的每个 Web API 控制器，请添加**AuthorizeAttribute**向全局筛选器列表的筛选器：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

**控制器**： 若要限制访问特定控制器，请添加筛选器作为属性到控制器：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

**操作**： 若要限制特定操作的访问权限，请将属性添加到操作方法：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

或者，可以限制控制器并再允许匿名访问特定操作使用`[AllowAnonymous]`属性。 在以下示例中，`Post`方法受到限制，但`Get`方法允许匿名访问。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

在上一示例中，筛选器允许任何经过身份验证的用户访问受限制的方法;仅匿名用户进行。您还可以限制对特定用户或特定角色的用户访问：

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> **AuthorizeAttribute** Web API 控制器的筛选器位于**System.Web.Http**命名空间。 还有一个类似的筛选器中的 MVC 控制器**System.Web.Mvc**命名空间，与 Web API 控制器不兼容。


### <a name="custom-authorization-filters"></a>自定义授权筛选器

若要编写自定义授权筛选器，派生自其中一种类型：

- **AuthorizeAttribute**。 扩展此类来执行基于当前用户和用户的角色的授权逻辑。
- **AuthorizationFilterAttribute**。 扩展此类来执行不一定是基于当前用户或角色的同步的授权逻辑。
- **IAuthorizationFilter**。 实现此接口可执行异步授权逻辑;例如，如果你的授权逻辑执行异步 I/O 或网络调用。 (如果授权逻辑是 CPU 绑定的它会更易于派生自**AuthorizationFilterAttribute**，因为不需要编写异步方法。)

下图显示的类层次结构**AuthorizeAttribute**类。

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a>在控制器操作中的授权

在某些情况下，可能允许继续，但更改行为基于主体的请求。 例如，返回的信息可能会更改具体取决于用户的角色。 在控制器方法中，可以获取从当前的原则**ApiController.User**属性。

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
