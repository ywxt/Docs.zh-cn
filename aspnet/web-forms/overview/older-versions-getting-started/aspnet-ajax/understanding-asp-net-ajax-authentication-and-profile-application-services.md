---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: 了解 ASP.NET AJAX 身份验证和配置文件应用程序服务 |Microsoft Docs
author: scottcate
description: 身份验证服务允许用户提供凭据才能接收身份验证 cookie，因此网关服务才能允许自定义用户...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/14/2008
ms.topic: article
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: 323fec56f18281b5b5a3d312a2e4c4c7133e3f03
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393056"
---
<a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>了解 ASP.NET AJAX 身份验证和配置文件应用程序服务
====================
通过[Scott Cate](https://github.com/scottcate)

[下载 PDF](http://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> 身份验证服务允许用户提供凭据才能接收身份验证 cookie，并由 ASP.NET 提供网关服务才能允许自定义用户配置文件。 ASP.NET AJAX 身份验证服务的使用是标准的 ASP.NET 窗体身份验证与兼容，因此当前使用窗体身份验证的应用程序 （如使用的登录名控制） 将不会断开通过升级到 AJAX 身份验证服务。


## <a name="introduction"></a>介绍

作为.NET Framework 3.5 的一部分，Microsoft 提供了一可调整大小的环境升级;不仅是一个新的开发环境可用，而且新的语言集成查询 (LINQ) 功能和其他语言增强功能是即将推出。 此外，一些常见的功能的其他工具集，值得注意的是 ASP.NET AJAX Extensions，都包含为.NET Framework 基类库的一流成员。 使用这些扩展，许多新的丰富的客户端功能，而无需整页刷新，通过客户端脚本 （包括 ASP.NET 分析 API） 和广泛的客户端 API 访问 Web 服务的功能包括部分呈现的页面用于镜像许多 ASP.NET 服务器端控件集所示的控制方案。

本白皮书中介绍的实现和使用 ASP.NET 分析和窗体身份验证服务因为它们由公开 Microsoft ASP.NET AJAX ExtensionsThe AJAX Extensions 使窗体身份验证非常简单支持，因为它 （以及分析服务中） 通过 Web 服务代理脚本公开。 AJAX 扩展还支持通过 AuthenticationServiceManager 类的自定义身份验证。

此白皮书基于 Visual Studio 2008 Beta 2 版本和.NET Framework 3.5。 本白皮书还假定你将使用 Visual Studio 2008 Beta 2，不 Visual Web Developer 速成版，并且将提供根据 Visual Studio 的用户界面的演练。 一些代码示例可使用项目模板在 Visual Web Developer 速成版中不可用。

## <a name="profiles-and-authentication"></a>*配置文件和身份验证*

Microsoft ASP.NET 配置文件和身份验证服务提供的 ASP.NET 窗体身份验证系统，和是标准的 ASP.NET 组件。 ASP.NET AJAX Extensions 提供脚本访问这些服务通过脚本代理，通过 Sys.Services 命名空间下的客户端 AJAX 库的非常简单的模型。

身份验证服务允许用户提供凭据才能接收身份验证 cookie，并由 ASP.NET 提供网关服务才能允许自定义用户配置文件。 ASP.NET AJAX 身份验证服务的使用是标准的 ASP.NET 窗体身份验证与兼容，因此当前使用窗体身份验证的应用程序 （如使用的登录名控制） 将不会断开通过升级到 AJAX 身份验证服务。

配置文件服务允许自动集成和基于成员身份，如身份验证服务所提供的用户数据的存储。 Web.config 文件中，指定存储的数据和各种分析服务提供程序处理的数据管理。 与身份验证服务，如 AJAX 配置文件服务是符合标准的 ASP.NET 配置文件服务，以便包括 AJAX 支持的应不会损坏页当前合并 ASP.NET 配置文件服务的功能。

将 ASP.NET 身份验证和分析服务本身合并到应用程序不在此白皮书的范围。 本主题的详细信息，请参阅 MSDN 库参考文章在使用成员资格管理用户[ https://msdn.microsoft.com/library/tw292whz.aspx ](https://msdn.microsoft.com/library/tw292whz.aspx)。 ASP.NET 还包括一个实用工具来自动设置使用 SQL Server，这是 ASP.NET 成员资格的默认身份验证服务提供程序的成员身份。 有关详细信息，请参阅文章 ASP.NET SQL Server 注册工具 (Aspnet\_regsql.exe) 处[ https://msdn.microsoft.com/library/ms229862(vs.80).aspx ](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)。

## <a name="using-the-aspnet-ajax-authentication-service"></a>*使用 ASP.NET AJAX 身份验证服务*

必须在 web.config 文件中启用 ASP.NET AJAX 身份验证服务：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

身份验证服务需要 ASP.NET 窗体身份验证启用并且 cookie 处于启用状态 （脚本不能启用无 cookie 会话由于无 cookie 会话需要 URL 参数） 的客户端浏览器上。

AJAX 身份验证服务是已启用并配置后，客户端脚本可以立即加以利用 Sys.Services.AuthenticationService 对象。 主要是，客户端脚本将想要充分利用`login`方法和`isLoggedIn`属性。 若要为登录方法，可以接受大量参数提供默认值不存在多个属性。

*Sys.Services.AuthenticationService 成员*

*登录方法：*

Login （） 方法开始的请求进行身份验证用户的凭据。 此方法是异步的不会阻止执行。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| userName | 必须的。 用于进行身份验证的用户名。 |
| 密码 | 可选 （默认值为 null）。 用户的密码。 |
| isPersistent | 可选 （默认值为 false）。 是否用户的身份验证 cookie 应保存各个会话中。 如果为 false，则在浏览器已关闭或会话过期时用户将可以注销。 |
| redirectUrl | 可选 （默认值为 null）。要重定向到身份验证成功后的在浏览器的 URL。 如果此参数为 null 或空字符串，则会不发生任何重定向。 |
| customInfo | 可选 （默认值为 null）。 此参数是当前未使用，并且是保留供将来使用。 |
| loginCompletedCallback | 可选 （默认值为 null）。要成功完成登录后调用的函数。 如果指定，此参数重写 defaultLoginCompleted 属性。 |
| failedCallback | 可选 （默认值为 null）。当登录已经失败时要调用该函数。 如果指定，此参数重写 defaultFailedCallback 属性。 |
| userContext | 可选 （默认值为 null）。 应传递给回调函数的自定义用户上下文数据。 |

*返回值：*

此函数不包括返回值。 但是，有多种行为都是调用的包含对此函数完成后：

- 当前页将进行刷新，或者如果更改`redirectUrl`参数是既不为 null，也不是空字符串。
- 但是，如果参数为 null 或空字符串，则`loginCompletedCallback`参数，或`defaultLoginCompletedCallback`调用属性。
- 如果对 web 服务的调用失败，`failedCallback`参数的`defaultFailedCallback`调用属性。

*注销方法：*

Logout （） 方法将移除凭据 cookie，并从 web 应用程序的当前用户。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| redirectUrl | 可选 （默认值为 null）。要重定向到身份验证成功后的在浏览器的 URL。 如果此参数为 null 或空字符串，则会不发生任何重定向。 |
| logoutCompletedCallback | 可选 （默认值为 null）。要注销已成功完成时调用的函数。 如果指定，此参数重写 defaultLogoutCompleted 属性。 |
| failedCallback | 可选 （默认值为 null）。当登录已经失败时要调用该函数。 如果指定，此参数重写 defaultFailedCallback 属性。 |
| userContext | 可选 （默认值为 null）。 应传递给回调函数的自定义用户上下文数据。 |

*返回值：*

此函数不包括返回值。 但是，有多种行为都是调用的包含对此函数完成后：

- 当前页将进行刷新，或者如果更改`redirectUrl`参数是既不为 null，也不是空字符串。
- 但是，如果参数为 null 或空字符串，则`logoutCompletedCallback`参数，或`defaultLogoutCompletedCallback`调用属性。
- 如果对 web 服务的调用失败，`failedCallback`参数的`defaultFailedCallback`调用属性。

*defaultFailedCallback 属性 （get、 组）：*

此属性指定应与 web 服务进行通信在失败时调用的函数。 它应接收的委托 （或函数参考）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| 错误 | 指定的错误信息。 |
| userContext | 指定登录或注销函数调用时提供的用户上下文信息。 |
| 方法名称 | 调用方法的名称。 |

*defaultLoginCompletedCallback 属性 （get、 组）：*

此属性指定登录名的 web 服务调用完成时，应调用的函数。 它应接收的委托 （或函数参考）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| validCredentials | 指定是否为用户提供有效的凭据。 `true` 如果用户成功登录;否则为`false`。 |
| userContext | 指定调用 login 函数时提供的用户上下文信息。 |
| 方法名称 | 调用方法的名称。 |

*defaultLogoutCompletedCallback 属性 （get、 组）：*

此属性指定注销的 web 服务调用完成时，应调用的函数。 它应接收的委托 （或函数参考）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| result | 此参数将始终为`null`; 保留供将来使用。 |
| userContext | 指定调用 login 函数时提供的用户上下文信息。 |
| 方法名称 | 调用方法的名称。 |

*isLoggedIn 属性 (get):*

此属性获取用户; 的当前身份验证状态它是 ScriptManager 对象在过程中设置的页面请求。

此属性返回`true`如果用户当前登录; 否则为它将返回`false`。

*路径属性 （get、 组）：*

此属性以编程方式确定身份验证 web 服务的位置。 它可用于重写默认身份验证提供程序，以及一个 ScriptManager 控件的 AuthenticationService 子节点的路径属性中以声明方式设置 (有关详细信息，请参阅使用自定义身份验证服务提供程序下面的主题）。

请注意，默认身份验证服务的位置不会更改。 但是，ASP.NET AJAX 允许您指定的位置提供了 ASP.NET AJAX 身份验证服务代理相同的类接口的 web 服务。

另请注意，不应此属性设置为一个值，指示从当前站点的脚本请求。 当前应用程序将不会收到身份验证凭据，因为它也将无用;此外，技术基础 AJAX 不应该发布跨站点请求，并可能在客户端浏览器中生成安全异常。

此属性是`String`对象，它表示身份验证 web 服务的路径。

*timeout 属性 （get、 组）：*

此属性确定失败的身份验证服务的登录请求前等待的时间长度。 如果在超时到期等待调用完成时，将调用请求失败回调，也将无法完成调用。

此属性是`Number`对象，表示要等待从身份验证服务的结果的毫秒数。

*登录到身份验证服务的代码示例：*

以下标记是通过简单的脚本调用的 AuthenticationService 类的登录和注销方法的示例 ASP.NET 页。

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>访问的 ASP.NET 分析数据通过 AJAX

通过 ASP.NET AJAX Extensions 还公开的 ASP.NET 分析服务。 由于 ASP.NET 分析服务提供丰富的精细的 API，通过要存储和检索用户数据，这可以是卓越的生产效率工具。

必须在 web.config 中; 启用配置文件服务它不是默认情况下。 若要执行此操作，请确保`profileService`子元素已启用 = true 中指定的 web.config 文件中，并指定哪些属性可读取或写入，如下所示：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

此外必须配置配置文件服务。 虽然分析服务的配置是本白皮书的范围之外，但值得注意，在配置文件配置设置中定义的组将组名称的子属性的可访问性。 例如，使用指定的以下配置文件部分：

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

客户端脚本可以访问作为 ProfileService 类的属性字段的属性的名称、 Address.Line1、 Address.Line2、 Address.City、 Address.State、 Address.Zip 和 BackgroundColor。

AJAX 分析服务配置后，它将可以立即在页面; 例如：但是，它必须在使用前一次加载。

*Sys.Services.ProfileService 成员*

*属性字段：*

属性字段公开为可由圆点运算符名称约定引用的子属性配置的配置文件的所有数据。 属性组的子级的属性称为 GroupName.PropertyName。 在上面介绍的示例配置文件配置中，以获取状态的用户，您可以使用以下标识符：

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*load 方法：*

从服务器加载所选的列表或所有属性。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| propertyNames | 可选 （默认值为 null）。 要从服务器加载的属性。 |
| loadCompletedCallback | 可选 （默认值为 null）。 要在加载时调用的函数已完成。 |
| failedCallback | 可选 （默认值为 null）。 如果发生错误，请调用函数。 |
| userContext | 可选 （默认值为 null）。 要传递给回调函数的上下文信息。 |

加载函数没有返回值。 如果已成功完成的调用，它将调用`loadCompletedCallback`参数或`defaultLoadCompletedCallback`属性。 如果调用失败或超时时间已到，要么`failedCallback`参数或`defaultFailedCallback`将调用属性。

如果`propertyNames`未提供参数，从服务器中检索所有读取配置属性。

*保存方法：*

Save （） 方法将指定的属性列表 （或所有属性） 保存到用户的 ASP.NET 配置文件。

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| propertyNames | 可选 （默认值为 null）。 要保存到服务器的属性。 |
| saveCompletedCallback | 可选 （默认值为 null）。 要保存时调用的函数已完成。 |
| failedCallback | 可选 （默认值为 null）。 如果发生错误，请调用函数。 |
| userContext | 可选 （默认值为 null）。 要传递给回调函数的上下文信息。 |

保存函数没有返回值。 如果调用成功完成，它将调用`saveCompletedCallback`参数或`defaultSaveCompletedCallback`属性。 如果调用失败或超时时间已到，要么`failedCallback`或`defaultFailedCallback`将调用属性。

如果`propertyNames`参数为 null，所有配置文件属性将发送到服务器，且服务器将决定可保存哪些属性以及哪些不能。

*defaultFailedCallback 属性 （get、 组）：*

此属性指定应与 web 服务进行通信在失败时调用的函数。 它应接收的委托 （或函数参考）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| Error | 指定的错误信息。 |
| userContext | 指定当提供的用户上下文信息加载或保存函数调用。 |
| 方法名称 | 调用方法的名称。 |

*defaultSaveCompleted 属性 （get、 组）：*

此属性指定应在保存用户的配置文件数据的完成时调用的函数。 它应接收的委托 （或函数参考）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| numPropsSaved | 指定已保存的属性的数目。 |
| userContext | 指定当提供的用户上下文信息加载或保存函数调用。 |
| 方法名称 | 调用方法的名称。 |

*defaultLoadCompleted 属性 （get、 组）：*

此属性指定的用户的配置文件数据加载完成后，应调用的函数。 它应接收的委托 （或函数参考）。

此属性指定的函数引用应具有以下签名：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*参数：*

| **参数名称** | **含义** |
| --- | --- |
| numPropsLoaded | 指定加载的属性的数目。 |
| userContext | 指定当提供的用户上下文信息加载或保存函数调用。 |
| 方法名称 | 调用方法的名称。 |

*路径属性 （get、 组）：*

此属性以编程方式确定配置文件 web 服务的位置。 它可用于重写默认配置文件服务提供程序，以及一个 ScriptManager 控件的 ProfileService 子节点的路径属性中以声明方式设置。

请注意，默认配置文件服务的位置不会更改。 但是，ASP.NET AJAX 允许您指定的位置提供了 ASP.NET AJAX 身份验证服务代理相同的类接口的 web 服务。

另请注意，不应此属性设置为一个值，指示从当前站点的脚本请求。 技术基础 AJAX 不应该发布跨站点请求，并可能在客户端浏览器中生成安全异常。

此属性是`String`对象，表示配置文件 web 服务的路径。

*timeout 属性 （get、 组）：*

此属性确定失败的负载前等待的配置文件服务或保存请求的时间长度。 如果在超时到期等待调用完成时，将调用请求失败回调，也将无法完成调用。

此属性是`Number`对象，表示要等待从配置文件服务的结果的毫秒数。

*代码示例： 加载在页面加载的配置文件数据*

下面的代码将检查是否用户进行身份验证，并且如果是这样，加载速度将用户的首选的背景色作为页面的。

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*使用自定义身份验证服务提供程序*

ASP.NET AJAX Extensions，可以创建自定义脚本身份验证服务提供程序公开您通过自定义 web 服务的功能。 若要使用你的 web 服务必须公开两种方法`Login`和`Logout`; 并且必须具有为默认 ASP.NET AJAX 身份验证 web 服务相同的方法签名指定这些方法。

一旦创建自定义 web 服务后，需要指定给它以声明方式在页中，路径，以编程方式在代码中，或通过客户端脚本。

*若要以声明方式设置的路径：*

若要以声明方式设置的路径，包括对您的 ASP.NET 页面的 ScriptManager 对象的 AuthenticationService 子级：

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*在代码中设置的路径：*

若要以编程方式设置路径，请指定通过脚本管理器的实例的路径：

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*若要在脚本中设置路径：*

若要在脚本中以编程方式设置路径，请利用`path`AuthenticationService 类的属性：

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*适用于自定义身份验证的示例 Web 服务*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>总结

ASP.NET 服务-特别是分析、 成员资格和身份验证服务-轻松地向 JavaScript 公开客户端浏览器上。 这允许开发人员及其客户端代码使用的身份验证机制无缝集成，而无需依赖等来执行繁重的工作的 Updatepanel 控件上。 可从客户端，通过利用 web 配置设置; 保护配置文件数据不会按默认情况下，提供的任何数据和开发人员必须选择在配置文件属性。

此外，通过使用等效方法签名中创建简化的 web 服务实现，开发人员可以创建自定义脚本的这些内部函数的 ASP.NET 服务的提供程序。 对这些技术的支持简化了开发丰富的客户端应用程序，同时为开发人员提供范围广泛的灵活性来满足特定需求。

## <a name="bio"></a>*个人简介*

Scott Cate 自 1997 年以来一直致力于 Microsoft Web 技术和 myKB.com 总裁 ([www.myKB.com](http://www.myKB.com)) 专门负责编写 ASP.NET 基于侧重于知识库软件解决方案的应用程序。 可以通过电子邮件联系 Scott [ scott.cate@myKB.com ](mailto:scott.cate@myKB.com)或他的博客[ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-updatepanel-triggers.md)
> [下一页](understanding-asp-net-ajax-localization.md)
