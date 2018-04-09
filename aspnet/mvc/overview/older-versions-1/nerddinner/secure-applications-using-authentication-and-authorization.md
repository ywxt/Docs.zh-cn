---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 保护应用程序使用身份验证和授权 |Microsoft 文档
author: microsoft
description: 步骤 9 演示如何添加身份验证和授权，以保护我们 NerdDinner 的应用程序，以便用户需要注册和登录到要创建的网站...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2010
ms.topic: article
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 4a9b1e6d7d453bd8dc5a61b1f1cec4617af7d693
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="a0dca-103">保护应用程序使用身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="a0dca-103">Secure Applications Using Authentication and Authorization</span></span>
====================
<span data-ttu-id="a0dca-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a0dca-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="a0dca-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a0dca-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="a0dca-106">这是个免费的步骤 9 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，查找步程取如何生成一个较小，但完成，使用 ASP.NET MVC 1 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0dca-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="a0dca-107">步骤 9 演示如何添加身份验证和授权，以保护我们 NerdDinner 的应用程序，以便用户需要注册和登录到站点创建新晚餐，而仅承载 dinner 的用户可在以后编辑它。</span><span class="sxs-lookup"><span data-stu-id="a0dca-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="a0dca-108">如果你使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC 音乐商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="a0dca-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="a0dca-109">NerdDinner 步骤 9： 身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="a0dca-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="a0dca-110">现在我们 NerdDinner 应用程序授予任何人访问站点能够创建和编辑任何 dinner 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a0dca-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="a0dca-111">将此项更改，以便用户需要注册和登录到要创建新晚餐和添加的限制，以便只有承载 dinner 的用户可以更高版本编辑的站点。</span><span class="sxs-lookup"><span data-stu-id="a0dca-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="a0dca-112">要启用此功能我们将使用身份验证和授权保护我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0dca-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="a0dca-113">了解身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="a0dca-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="a0dca-114">*身份验证*是标识和验证客户端访问应用程序的标识的过程。</span><span class="sxs-lookup"><span data-stu-id="a0dca-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="a0dca-115">更简单地说，它是有关标识""最终用户是谁在访问网站时。</span><span class="sxs-lookup"><span data-stu-id="a0dca-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="a0dca-116">ASP.NET 支持通过多种方式浏览器用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a0dca-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="a0dca-117">对于 Internet web 应用程序，使用的最常见的身份验证方法被称为"窗体身份验证"。</span><span class="sxs-lookup"><span data-stu-id="a0dca-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="a0dca-118">窗体身份验证使开发人员可以创作自己的应用程序中的 HTML 登录窗体，然后验证用户名/密码的最终用户提交针对数据库或其他密码凭据存储区。</span><span class="sxs-lookup"><span data-stu-id="a0dca-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="a0dca-119">如果用户名/密码组合均正确无误，开发人员然后可以要求 ASP.NET 颁发的加密的 HTTP cookie，用于标识用户跨今后的请求。</span><span class="sxs-lookup"><span data-stu-id="a0dca-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="a0dca-120">我们将使用与我们 NerdDinner 应用程序的窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="a0dca-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="a0dca-121">*授权*是确定已经过身份验证的用户是否有权限以访问特定的 URL/资源或执行某些操作的过程。</span><span class="sxs-lookup"><span data-stu-id="a0dca-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="a0dca-122">例如，我们 NerdDinner 应用程序中我们将需要授权，只有登录的用户可以访问*/晚餐/创建*URL 并创建新晚餐。</span><span class="sxs-lookup"><span data-stu-id="a0dca-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="a0dca-123">我们还需要添加授权逻辑，以便只有承载 dinner 的用户可以编辑它 – 和拒绝的所有其他用户编辑访问。</span><span class="sxs-lookup"><span data-stu-id="a0dca-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="a0dca-124">窗体身份验证和 AccountController 中</span><span class="sxs-lookup"><span data-stu-id="a0dca-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="a0dca-125">创建新的 ASP.NET MVC 应用程序时，ASP.NET MVC 的默认 Visual Studio 项目模板会自动启用表单身份验证。</span><span class="sxs-lookup"><span data-stu-id="a0dca-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="a0dca-126">它还会自动向项目 – 这使得真正轻松地集成在站点内的安全预建的帐户登录页的实现。</span><span class="sxs-lookup"><span data-stu-id="a0dca-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="a0dca-127">访问它的用户不进行身份验证时，默认 Site.master 母版页显示在右上角的站点的"登录"链接：</span><span class="sxs-lookup"><span data-stu-id="a0dca-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="a0dca-128">单击"登录"链接可转到用户*/帐户/登录*URL:</span><span class="sxs-lookup"><span data-stu-id="a0dca-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="a0dca-129">尚未注册者可以这样通过单击"注册"链接 – 这会将他们到*/帐户/注册*URL，并让他们输入帐户的详细信息：</span><span class="sxs-lookup"><span data-stu-id="a0dca-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="a0dca-130">单击"注册"按钮将创建一个新用户在 ASP.NET 成员资格系统中，并使用 forms 身份验证的站点到用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a0dca-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="a0dca-131">Site.master 登录的用户时，更改右上角的页后，可以输出"欢迎使用 [username] ！"</span><span class="sxs-lookup"><span data-stu-id="a0dca-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="a0dca-132">消息和呈现"注销"链接而不是"Log On"一个。</span><span class="sxs-lookup"><span data-stu-id="a0dca-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="a0dca-133">单击"注销"链接注销用户：</span><span class="sxs-lookup"><span data-stu-id="a0dca-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="a0dca-134">已添加到我们的项目由 Visual Studio 创建项目时 AccountController 类中实现上述的登录、 注销和注册功能。</span><span class="sxs-lookup"><span data-stu-id="a0dca-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="a0dca-135">使用 \Views\Account 目录中的视图模板实现 AccountController 中的 UI:</span><span class="sxs-lookup"><span data-stu-id="a0dca-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="a0dca-136">AccountController 类使用 ASP.NET 窗体身份验证系统以发出加密的身份验证 cookie 和 ASP.NET 成员资格 API 来存储和验证用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="a0dca-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="a0dca-137">ASP.NET 成员资格 API 可扩展，并允许使用任何密码凭据存储区。</span><span class="sxs-lookup"><span data-stu-id="a0dca-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="a0dca-138">ASP.NET 附带存储用户名/密码在 SQL 数据库中，或在 Active Directory 中的内置成员资格提供程序实现。</span><span class="sxs-lookup"><span data-stu-id="a0dca-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="a0dca-139">我们可以将配置我们 NerdDinner 应用程序应使用通过打开位于项目的根"web.config"文件和查找的成员资格提供程序&lt;成员资格&gt;其中的部分。</span><span class="sxs-lookup"><span data-stu-id="a0dca-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="a0dca-140">添加创建项目时的默认 web.config 注册 SQL 成员资格提供程序，并将其配置为使用名为"ApplicationServices"的连接字符串指定的数据库位置。</span><span class="sxs-lookup"><span data-stu-id="a0dca-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="a0dca-141">默认值"ApplicationServices"连接字符串 (其内指定&lt;connectionStrings&gt; web.config 文件的部分) 配置为使用 SQL Express。</span><span class="sxs-lookup"><span data-stu-id="a0dca-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="a0dca-142">它指向名为"ASPNETDB SQL Express 数据库。MDF"该应用程序下的"应用\_数据"目录。</span><span class="sxs-lookup"><span data-stu-id="a0dca-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="a0dca-143">如果此数据库不存在首次应用程序中使用成员资格 API，ASP.NET 将自动创建数据库，以及设置相应的成员关系数据库架构中它：</span><span class="sxs-lookup"><span data-stu-id="a0dca-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="a0dca-144">如果而不是使用 SQL Express 我们想要使用完整的 SQL Server 实例 （或连接到远程数据库），我们将需要待办事项是以更新 web.config 文件中的"ApplicationServices"连接字符串，请确保相应的成员关系架构具有已添加到它所指向的数据库。</span><span class="sxs-lookup"><span data-stu-id="a0dca-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="a0dca-145">你可以运行"aspnet\_regsql.exe"实用工具 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目录将用于成员身份和其他 ASP.NET 应用程序服务的相应架构添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="a0dca-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="a0dca-146">授权使用 [Authorize] 筛选器晚餐/创建 URL</span><span class="sxs-lookup"><span data-stu-id="a0dca-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="a0dca-147">我们无需编写任何代码来启用安全的身份验证和帐户管理实现 NerdDinner 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a0dca-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="a0dca-148">用户可以注册新帐户，使用我们的应用程序和登录/注销的站点。</span><span class="sxs-lookup"><span data-stu-id="a0dca-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="a0dca-149">现在我们可以将授权逻辑添加到该应用程序，并使用身份验证状态和用户名的访问者来控制他们可以并不能执行的站点内。</span><span class="sxs-lookup"><span data-stu-id="a0dca-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="a0dca-150">让我们首先将授权逻辑添加到我们 DinnersController 类的"创建"操作方法。</span><span class="sxs-lookup"><span data-stu-id="a0dca-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="a0dca-151">具体而言，我们将要求用户访问*/晚餐/创建*必须登录 URL。</span><span class="sxs-lookup"><span data-stu-id="a0dca-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="a0dca-152">如果在用户未登录我们会将它们重定向到登录页，以便它们可以在登录。</span><span class="sxs-lookup"><span data-stu-id="a0dca-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="a0dca-153">实现此逻辑是这么简单。</span><span class="sxs-lookup"><span data-stu-id="a0dca-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="a0dca-154">我们只需待办事项是将 [Authorize] 筛选器属性添加到我们创建的操作方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="a0dca-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="a0dca-155">ASP.NET MVC 支持的功能"操作，创建筛选器"可以用来实现能以声明方式应用于操作方法的可重用逻辑。</span><span class="sxs-lookup"><span data-stu-id="a0dca-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="a0dca-156">[Authorize] 筛选器是一个内置操作筛选器提供的 ASP.NET MVC，使开发人员能够以声明方式将授权规则应用于操作方法和控制器类。</span><span class="sxs-lookup"><span data-stu-id="a0dca-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="a0dca-157">应用不带任何参数 （如上所述） 时的 [Authorize] 筛选器会强制执行，发出操作方法请求的用户都必须登录 – 和它将自动将浏览器重定向到登录 URL 如果它们不是。</span><span class="sxs-lookup"><span data-stu-id="a0dca-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="a0dca-158">进行此重定向最初请求的 URL 传递作为查询字符串自变量时 (例如: / 帐户/登录？ReturnUrl = %2fDinners %2fcreate)。</span><span class="sxs-lookup"><span data-stu-id="a0dca-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="a0dca-159">AccountController 将然后将用户重定向回最初请求的 URL 后它们登录。</span><span class="sxs-lookup"><span data-stu-id="a0dca-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="a0dca-160">[Authorize] 筛选器可以选择支持的功能，可以指定可用于要求，用户都记录在中，在允许的用户或允许的安全角色的成员的列表的"用户"或"角色"属性。</span><span class="sxs-lookup"><span data-stu-id="a0dca-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="a0dca-161">例如，下面的代码仅允许两个特定用户、"scottgu"和"说比尔 · 盖茨"中，若要访问晚餐/创建 URL:</span><span class="sxs-lookup"><span data-stu-id="a0dca-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="a0dca-162">嵌入在代码中的特定用户名称往往是非常并且可维护未通过。</span><span class="sxs-lookup"><span data-stu-id="a0dca-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="a0dca-163">更好的方法是定义较高级别的"角色"，代码会检查对，然后将用户映射到使用数据库或 active directory 系统 （启用要从代码外部存储的实际用户映射列表） 的角色。</span><span class="sxs-lookup"><span data-stu-id="a0dca-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="a0dca-164">ASP.NET 包括内置角色管理 API，以及角色提供程序 （包括针对 SQL 和 Active Directory），可帮助执行此用户/角色映射一内置组。</span><span class="sxs-lookup"><span data-stu-id="a0dca-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="a0dca-165">然后，我们无法更新代码以仅允许特定的"admin"角色中的用户访问晚餐/创建 URL:</span><span class="sxs-lookup"><span data-stu-id="a0dca-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="a0dca-166">在创建时使用 User.Identity.Name 属性晚餐</span><span class="sxs-lookup"><span data-stu-id="a0dca-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="a0dca-167">我们可以检索使用控制器基类上公开的 User.Identity.Name 属性的请求当前登录的用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="a0dca-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="a0dca-168">前面我们实现了我们的 create （） 的操作方法的 HTTP POST 版本当我们具有硬编码为静态字符串 Dinner"HostedBy"属性。</span><span class="sxs-lookup"><span data-stu-id="a0dca-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="a0dca-169">我们可以现在更新此代码以改用 User.Identity.Name 属性，以及自动创建 Dinner 将主机添加的回复：</span><span class="sxs-lookup"><span data-stu-id="a0dca-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="a0dca-170">因为我们已添加到 create （） 方法的 [Authorize] 属性，则可以确保 ASP.NET MVC，操作方法才会执行站点上登录用户访问晚餐/创建 URL。</span><span class="sxs-lookup"><span data-stu-id="a0dca-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="a0dca-171">在这种情况下，User.Identity.Name 属性值将始终包含一个有效的用户名。</span><span class="sxs-lookup"><span data-stu-id="a0dca-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="a0dca-172">在编辑时使用 User.Identity.Name 属性晚餐</span><span class="sxs-lookup"><span data-stu-id="a0dca-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="a0dca-173">让我们现在将添加一些授权逻辑，可对用户的限制，以便它们只能编辑的晚餐它们本身托管的属性。</span><span class="sxs-lookup"><span data-stu-id="a0dca-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="a0dca-174">若要帮助实现这一点，我们将首先到我们 Dinner 对象 （在我们之前生成的 Dinner.cs 分部类） 中添加"IsHostedBy(username)"帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="a0dca-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="a0dca-175">此帮助器方法返回 true 或 false，具体取决于是否提供的用户名匹配 Dinner HostedBy 属性，并封装执行不区分大小写的字符串比较其中所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="a0dca-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="a0dca-176">然后，我们将添加 [Authorize] 属性对 edit （） 操作方法在我们 DinnersController 类中。</span><span class="sxs-lookup"><span data-stu-id="a0dca-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="a0dca-177">这将确保用户必须记录请求到*/Dinners/编辑 / [id]* URL。</span><span class="sxs-lookup"><span data-stu-id="a0dca-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="a0dca-178">然后，我们可以将代码添加到使用 Dinner.IsHostedBy(username) 帮助器方法来验证登录的用户匹配 Dinner 主机我们编辑方法。</span><span class="sxs-lookup"><span data-stu-id="a0dca-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="a0dca-179">如果用户不是主机，我们将显示"InvalidOwner"视图，并终止请求。</span><span class="sxs-lookup"><span data-stu-id="a0dca-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="a0dca-180">要执行此操作的代码类似于下面：</span><span class="sxs-lookup"><span data-stu-id="a0dca-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="a0dca-181">我们可以右键单击 \Views\Dinners 目录，然后选择添加-&gt;查看菜单命令以创建新的"InvalidOwner"视图。</span><span class="sxs-lookup"><span data-stu-id="a0dca-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="a0dca-182">我们将填充其与以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="a0dca-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="a0dca-183">并且，现在当用户尝试编辑它们不属于 dinner，它们将获取一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="a0dca-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="a0dca-184">我们可以在我们的控制器来锁定，删除晚餐并确保仅 Dinner 主机可以删除它的权限内的 delete （） 操作方法重复相同的步骤。</span><span class="sxs-lookup"><span data-stu-id="a0dca-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="a0dca-185">显示/隐藏编辑和删除链接</span><span class="sxs-lookup"><span data-stu-id="a0dca-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="a0dca-186">我们要从我们的详细信息 URL 链接到我们 DinnersController 类的编辑和删除操作方法：</span><span class="sxs-lookup"><span data-stu-id="a0dca-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="a0dca-187">目前我们展示，无论到详细信息的 URL 访问者是否 dinner 主机的编辑和删除操作链接。</span><span class="sxs-lookup"><span data-stu-id="a0dca-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="a0dca-188">将此项更改，以便仅显示链接，如果正在访问的用户是 dinner 的所有者。</span><span class="sxs-lookup"><span data-stu-id="a0dca-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="a0dca-189">在我们 DinnersController Details() 操作方法检索 Dinner 对象，然后将其作为模型对象中传递到我们的视图模板：</span><span class="sxs-lookup"><span data-stu-id="a0dca-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="a0dca-190">我们可以更新我们的视图模板，以便有条件地显示/隐藏的编辑和删除链接使用 Dinner.IsHostedBy() 帮助器方法与下面类似：</span><span class="sxs-lookup"><span data-stu-id="a0dca-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="a0dca-191">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a0dca-191">Next Steps</span></span>

<span data-ttu-id="a0dca-192">让我们现在看一下，我们可以如何启用到晚餐使用 AJAX 的回复的经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="a0dca-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a0dca-193">[上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="a0dca-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
