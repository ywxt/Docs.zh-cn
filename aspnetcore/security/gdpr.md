---
title: 在 ASP.NET 核心中的常规数据保护法规 (GDPR) 支持
author: rick-anderson
description: 了解如何访问 ASP.NET 核心 web 应用中的 GDPR 扩展点。
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.custom: mvc
ms.date: 05/29/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/gdpr
ms.openlocfilehash: eb9173bfe554b8b00ef8deb255e8347a534e7ba3
ms.sourcegitcommit: 9a35906446af7ffd4ccfc18daec38874b5abbef7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35725791"
---
# <a name="eu-general-data-protection-regulation-gdpr-support-in-aspnet-core"></a>在 ASP.NET Core 欧洲常规数据保护法规 (GDPR) 支持

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

ASP.NET Core 提供 Api 和模板，以帮助满足一些[欧洲常规数据保护法规 (GDPR)](https://www.eugdpr.org/)要求：

* 项目模板包含扩展点以及可以将替换为您的隐私和 cookie 的使用策略的存根的标记。
* 用于存储的个人信息中，cookie 同意功能允许你以寻求 （和跟踪） 同意的情况下从你的用户。 如果用户不与数据收集同意和应用程序设置[CheckConsentNeeded](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions.checkconsentneeded)到`true`，不重要 cookie 将不会发送到浏览器。
* 可以将 cookie 标记为重要。 基本 cookie 发送到浏览器中，即使用户不同意，并且已禁用跟踪。
* [TempData 和会话 cookie](#tempdata)禁用跟踪时不起作用。
* [标识管理](#pd)页提供的链接下载和删除用户数据。

[示例应用程序](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample)允许你测试的大多数 GDPR 扩展点和 Api 添加到 ASP.NET 核心 2.1 模板。 请参阅[自述文件](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample)测试说明文件。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/gdpr/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="aspnet-core-gdpr-support-in-template-generated-code"></a>模板中的 ASP.NET Core GDPR 支持生成的代码

Razor 页和 MVC 项目模板创建的项目包括以下 GDPR 支持：

* [CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions)和[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy)中设置`Startup`。
* *_CookieConsentPartial.cshtml* [分部视图](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)。
* *Pages/Privacy.cshtml*或*Home/Privacy.cshtml*视图提供页详细介绍站点的隐私策略。 *_CookieConsentPartial.cshtml*文件生成隐私页的链接。
* 对于使用单个用户帐户创建的应用程序，管理页提供了用于下载和删除链接[个人用户数据](#pd)。

### <a name="cookiepolicyoptions-and-usecookiepolicy"></a>CookiePolicyOptions 和 UseCookiePolicy

[CookiePolicyOptions](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyoptions)中初始化`Startup`类`ConfigureServices`方法：

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=14-20)]

[UseCookiePolicy](/dotnet/api/microsoft.aspnetcore.builder.cookiepolicyappbuilderextensions.usecookiepolicy)中称为`Startup`类`Configure`方法：

[!code-csharp[Main](gdpr/sample/Startup.cs?name=snippet1&highlight=49)]

### <a name="cookieconsentpartialcshtml-partial-view"></a>_CookieConsentPartial.cshtml 分部视图

*_CookieConsentPartial.cshtml*分部视图：

[!code-html[Main](gdpr/sample/RP/Pages/Shared/_CookieConsentPartial.cshtml)]

此部分中：

* 获取跟踪的用户的状态。 如果应用程序配置为需要之前可以跟踪 cookie，用户必须同意的同意。 如果需要同意的情况下，在顶部导航栏中创建固定 cookie 同意 chrome *Pages/Shared/_Layout.cshtml*文件。
* 提供一个 HTML`<p>`元素汇总隐私和 cookie 使用策略。
* 提供的链接*Pages/Privacy.cshtml*其中详细介绍站点的隐私策略。

## <a name="essential-cookies"></a>基本 cookie

如果不提供同意的情况下，仅标记为重要的 cookie 被发送到浏览器。 下面的代码使 cookie 重要：

[!code-csharp[Main](gdpr/sample/RP/Pages/Cookie.cshtml.cs?name=snippet1&highlight=5)]

<a name="tempdata"></a>

## <a name="tempdata-provider-and-session-state-cookies-are-not-essential"></a>Tempdata 提供程序和会话状态的 cookie 不重要

[Tempdata 提供程序](xref:fundamentals/app-state#tempdata)cookie 不是必需的。 如果禁用了跟踪，则 Tempdata 提供程序不起作用。 若要禁用跟踪时，请启用 Tempdata 提供程序，将 TempData cookie 标记为关键`ConfigureServices`:

[!code-csharp[Main](gdpr/sample/RP/Startup.cs?name=snippet1)]

[会话状态](xref:fundamentals/app-state)cookie 不重要。 禁用跟踪时，会话状态不起作用。

<a name="pd"></a>

## <a name="personal-data"></a>个人数据

ASP.NET 核心应用程序使用单个用户帐户创建包含代码，从而下载和删除个人数据。

选择的用户名称，然后选择**个人数据**:

![管理个人数据页](gdpr/_static/pd.png)

注意：

* 若要生成`Account/Manage`代码，请参阅[基架标识](xref:security/authentication/scaffold-identity)。
* 删除并下载仅影响的默认标识数据。 应用程序创建自定义用户数据必须进行扩展，以删除/下载自定义用户数据。 GitHub 问题[如何添加/删除到标识的自定义用户数据](https://github.com/aspnet/Docs/issues/6226)跟踪上创建自定义/删除/下载自定义用户数据的建议的文章。 如果你想要查看该主题按优先级排列，将向上反应拇指保留为问题。
* 保存用户标识数据库表中存储的令牌`AspNetUserTokens`时由于的级联删除行为通过删除该用户会被删除[外键](https://github.com/aspnet/Identity/blob/release/2.1/src/EF/IdentityUserContext.cs#L152)。

## <a name="encryption-at-rest"></a>静态加密

某些数据库和存储机制允许进行静态加密。 静态加密：

* 自动加密存储的数据。
* 加密而无需配置、 编程中或访问数据的软件的其他工作。
* 是最简单且最安全选项。
* 允许管理密钥和加密的数据库。

例如：

* Microsoft SQL 和 Azure SQL 提供[透明数据加密](/sql/relational-databases/security/encryption/transparent-data-encryption)(TDE)。
* [SQL Azure 默认情况下加密数据库](https://azure.microsoft.com/updates/newly-created-azure-sql-databases-encrypted-by-default/)
* [默认情况下加密 azure Blob、 文件、 表和队列存储](https://azure.microsoft.com/blog/announcing-default-encryption-for-azure-blobs-files-table-and-queue-storage/)。

对于不提供内置加密对静止的数据库，你可能能够使用磁盘加密提供相同的保护。 例如：

* [Windows Server 的 BitLocker](/windows/security/information-protection/bitlocker/bitlocker-how-to-deploy-on-windows-server)
* Linux:
  * [eCryptfs](https://launchpad.net/ecryptfs)
  * [EncFS](https://github.com/vgough/encfs)。

## <a name="additional-resources"></a>其他资源

* [Microsoft.com/GDPR](https://www.microsoft.com/en-us/trustcenter/Privacy/GDPR)
