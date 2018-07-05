---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用身份验证和授权保护应用程序 |Microsoft Docs
author: microsoft
description: 步骤 9 显示了如何添加身份验证和授权来保护我们 NerdDinner 的应用程序，以便用户需要注册并登录到要创建的网站...
ms.author: aspnetcontent
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 0005b99dbf7d59e96313f025880c46cdec4838b6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37801387"
---
<a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="9ad15-103">使用身份验证和授权保护应用程序</span><span class="sxs-lookup"><span data-stu-id="9ad15-103">Secure Applications Using Authentication and Authorization</span></span>
====================
<span data-ttu-id="9ad15-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9ad15-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9ad15-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="9ad15-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="9ad15-106">这是一种免费的步骤 9 ["NerdDinner"应用程序教程](introducing-the-nerddinner-tutorial.md)，演练如何构建一个较小，但完成，使用 ASP.NET MVC 1 中的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9ad15-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="9ad15-107">步骤 9 显示了如何添加身份验证和授权来保护我们 NerdDinner 的应用程序，以便用户需要注册并登录到站点创建新 dinners，以及仅承载 dinner 的用户可以更高版本编辑它。</span><span class="sxs-lookup"><span data-stu-id="9ad15-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="9ad15-108">如果使用的 ASP.NET MVC 3，我们建议你遵循[获取启动使用 MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[MVC Music 商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程。</span><span class="sxs-lookup"><span data-stu-id="9ad15-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>


## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="9ad15-109">NerdDinner 步骤 9： 身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="9ad15-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="9ad15-110">现在我们 NerdDinner 应用程序授予任何人访问站点能够创建和编辑任何 dinner 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="9ad15-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="9ad15-111">此项更改，以便用户需要注册并登录到要创建新 dinners，以便只有承载 dinner 的用户可以更高版本编辑添加的限制的站点。</span><span class="sxs-lookup"><span data-stu-id="9ad15-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="9ad15-112">若要启用此我们将使用身份验证和授权来保护我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9ad15-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="9ad15-113">了解身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="9ad15-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="9ad15-114">*身份验证*是标识和验证客户端访问应用程序身份的过程。</span><span class="sxs-lookup"><span data-stu-id="9ad15-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="9ad15-115">它更简单地说，是指确定""最终用户是谁在访问网站时。</span><span class="sxs-lookup"><span data-stu-id="9ad15-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="9ad15-116">ASP.NET 支持通过多种方式浏览器用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9ad15-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="9ad15-117">对于 Internet web 应用程序，使用最常用的身份验证方法称为"窗体身份验证"。</span><span class="sxs-lookup"><span data-stu-id="9ad15-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="9ad15-118">窗体身份验证使开发人员能够编写自己的应用程序中的 HTML 登录窗体，然后验证最终用户提交针对数据库或其他密码凭据存储区的用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="9ad15-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="9ad15-119">如果用户名/密码组合不正确，开发人员然后可以要求 ASP.NET 发出的加密的 HTTP cookie，若要识别跨今后的请求的用户。</span><span class="sxs-lookup"><span data-stu-id="9ad15-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="9ad15-120">我们将通过与我们 NerdDinner 应用程序使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="9ad15-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="9ad15-121">*授权*是确定身份验证的用户是否有权限访问特定的 URL/资源或执行某些操作的过程。</span><span class="sxs-lookup"><span data-stu-id="9ad15-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="9ad15-122">例如，我们 NerdDinner 应用程序中我们将想要授权登录的用户可以访问 */Dinners/创建*URL，并创建新 Dinners。</span><span class="sxs-lookup"><span data-stu-id="9ad15-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="9ad15-123">我们还需要添加授权逻辑，以便只有承载 dinner 的用户可以其进行编辑，并拒绝所有其他用户编辑访问权限。</span><span class="sxs-lookup"><span data-stu-id="9ad15-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="9ad15-124">窗体身份验证和 AccountController</span><span class="sxs-lookup"><span data-stu-id="9ad15-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="9ad15-125">创建新的 ASP.NET MVC 应用程序时，ASP.NET MVC 的默认 Visual Studio 项目模板会自动启用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="9ad15-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="9ad15-126">它还会自动向项目 – 可以非常轻松地将站点内的安全集成的预建的帐户登录页实现。</span><span class="sxs-lookup"><span data-stu-id="9ad15-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="9ad15-127">未经身份验证的用户可以访问它时，默认 Site.master 母版页在右上角站点显示"登录"链接：</span><span class="sxs-lookup"><span data-stu-id="9ad15-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="9ad15-128">单击"登录"链接可转到用户 */帐户/登录*URL:</span><span class="sxs-lookup"><span data-stu-id="9ad15-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="9ad15-129">尚未注册的访问者可以通过单击"注册"链接 – 这些链接将转到此， */帐户/注册*URL，使他们可以输入帐户的详细信息：</span><span class="sxs-lookup"><span data-stu-id="9ad15-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="9ad15-130">单击"注册"按钮将创建新的用户在 ASP.NET 成员资格系统中，并使用窗体身份验证的站点到用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="9ad15-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="9ad15-131">Site.master 登录的用户时，更改要输出"欢迎 [username] ！"的页的右上方</span><span class="sxs-lookup"><span data-stu-id="9ad15-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="9ad15-132">消息和呈现"注销"链接而不是"登录"一。</span><span class="sxs-lookup"><span data-stu-id="9ad15-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="9ad15-133">单击"注销"链接注销用户：</span><span class="sxs-lookup"><span data-stu-id="9ad15-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="9ad15-134">已添加到我们的项目的 Visual Studio 创建项目时的 AccountController 类中实现更高版本的登录、 注销和注册功能。</span><span class="sxs-lookup"><span data-stu-id="9ad15-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="9ad15-135">AccountController 的 UI 是使用视图模板 \Views\Account 目录中的实现的：</span><span class="sxs-lookup"><span data-stu-id="9ad15-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="9ad15-136">AccountController 类使用 ASP.NET 窗体身份验证系统发出加密的身份验证 cookie 和 ASP.NET 成员资格 API 来存储和验证用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="9ad15-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="9ad15-137">ASP.NET 成员资格 API 可扩展，并允许使用任何密码凭据存储区。</span><span class="sxs-lookup"><span data-stu-id="9ad15-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="9ad15-138">ASP.NET 附带了存储用户名/密码在 SQL 数据库中，或在 Active Directory 中的内置成员资格提供程序实现。</span><span class="sxs-lookup"><span data-stu-id="9ad15-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="9ad15-139">我们可以配置哪些成员资格提供程序，我们 NerdDinner 的应用程序应使用通过打开项目的根目录处的"web.config"文件并查找&lt;成员身份&gt;在其中的部分。</span><span class="sxs-lookup"><span data-stu-id="9ad15-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="9ad15-140">添加创建项目时的默认 web.config 注册 SQL 成员资格提供程序，并将其配置为使用名为"ApplicationServices"的连接字符串指定的数据库位置。</span><span class="sxs-lookup"><span data-stu-id="9ad15-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="9ad15-141">默认"ApplicationServices"连接字符串 (其内指定&lt;connectionStrings&gt; web.config 文件的部分) 配置为使用 SQL Express。</span><span class="sxs-lookup"><span data-stu-id="9ad15-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="9ad15-142">它指向 SQL Express 数据库名为"ASPNETDB。MDF"的应用程序下"应用\_数据"目录。</span><span class="sxs-lookup"><span data-stu-id="9ad15-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="9ad15-143">如果此数据库不存在第一次应用程序中使用成员资格 API，ASP.NET 会自动创建数据库和在其中将适当的成员身份数据库架构设置：</span><span class="sxs-lookup"><span data-stu-id="9ad15-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="9ad15-144">如果不使用 SQL Express 我们想要使用完整的 SQL Server 实例 （或连接到远程数据库），我们需要待办事项是更新 web.config 文件中的"ApplicationServices"连接字符串，请确保适当的成员身份架构已添加到它所指向的数据库。</span><span class="sxs-lookup"><span data-stu-id="9ad15-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="9ad15-145">你可以运行"aspnet\_regsql.exe"实用工具 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目录将成员身份和其他 ASP.NET 应用程序服务的相应架构添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="9ad15-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="9ad15-146">授权使用 [Authorize] 筛选器的 Dinners/创建 URL</span><span class="sxs-lookup"><span data-stu-id="9ad15-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="9ad15-147">我们无需编写任何代码即可启用安全的身份验证和 NerdDinner 应用程序的帐户管理实现。</span><span class="sxs-lookup"><span data-stu-id="9ad15-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="9ad15-148">用户可以使用我们的应用程序和登录/注销的站点注册新帐户。</span><span class="sxs-lookup"><span data-stu-id="9ad15-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="9ad15-149">现在我们可以将授权逻辑添加到应用程序，并使用的身份验证状态和用户名的访问者的控制他们可以和不能在站点内执行操作。</span><span class="sxs-lookup"><span data-stu-id="9ad15-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="9ad15-150">让我们首先将授权逻辑添加到我们的 DinnersController 类的"创建"操作方法。</span><span class="sxs-lookup"><span data-stu-id="9ad15-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="9ad15-151">具体而言，我们将需要访问的用户 */Dinners/创建*必须登录 URL。</span><span class="sxs-lookup"><span data-stu-id="9ad15-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="9ad15-152">如果它们不会记录在我们将重定向，它们到登录页以便他们可以登录。</span><span class="sxs-lookup"><span data-stu-id="9ad15-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="9ad15-153">实现此逻辑是这么简单。</span><span class="sxs-lookup"><span data-stu-id="9ad15-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="9ad15-154">我们需要待办事项，只需将 [Authorize] 筛选器特性添加到我们创建的操作方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="9ad15-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="9ad15-155">ASP.NET MVC 支持的功能，可创建"操作筛选器"可用于实现可以以声明方式应用于操作方法的可重用逻辑。</span><span class="sxs-lookup"><span data-stu-id="9ad15-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="9ad15-156">[Authorize] 筛选器是一个由 ASP.NET MVC 提供的内置操作筛选器，它使开发人员能够以声明方式将授权规则应用于操作方法和控制器类。</span><span class="sxs-lookup"><span data-stu-id="9ad15-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="9ad15-157">不带任何参数 （如上所述） 应用时执行操作方法请求的用户都必须登录 –，并且它会自动将浏览器重定向到登录名 URL 如果它们不是，强制实施的 [Authorize] 筛选器。</span><span class="sxs-lookup"><span data-stu-id="9ad15-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="9ad15-158">在执行此重定向最初请求的 URL 将作为查询字符串参数传递时 (例如: / 帐户/登录？ReturnUrl = %2fDinners %2fcreate)。</span><span class="sxs-lookup"><span data-stu-id="9ad15-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="9ad15-159">AccountController 将然后将用户重定向回最初请求的 URL 后登录。</span><span class="sxs-lookup"><span data-stu-id="9ad15-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="9ad15-160">[Authorize] 筛选器可以选择支持的功能，可以指定可用于要求，用户同时登录位于允许的用户或允许的安全角色的成员的列表中的"用户"或"角色"属性。</span><span class="sxs-lookup"><span data-stu-id="9ad15-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="9ad15-161">例如，下面的代码仅允许两个特定用户、"scottgu"和"billg"来访问 Dinners/创建 URL:</span><span class="sxs-lookup"><span data-stu-id="9ad15-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="9ad15-162">嵌入代码中的特定用户名称通常不过是相当不易于维护。</span><span class="sxs-lookup"><span data-stu-id="9ad15-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="9ad15-163">更好的方法是定义更高级别的"角色"，检查代码，然后将用户映射到角色使用数据库或 active directory 系统 （启用要从代码外部存储的实际用户映射列表）。</span><span class="sxs-lookup"><span data-stu-id="9ad15-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="9ad15-164">ASP.NET 包括内置的角色管理 API，以及一组内置角色提供程序 （其中包括用于 SQL 和 Active Directory），可帮助执行此用户/角色映射。</span><span class="sxs-lookup"><span data-stu-id="9ad15-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="9ad15-165">然后，我们无法更新代码以仅允许特定的"管理员"角色中的用户访问 Dinners/创建 URL:</span><span class="sxs-lookup"><span data-stu-id="9ad15-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="9ad15-166">创建时使用 User.Identity.Name 属性 Dinners</span><span class="sxs-lookup"><span data-stu-id="9ad15-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="9ad15-167">我们可以检索使用控制器基类上公开的 User.Identity.Name 属性的请求的当前登录的用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="9ad15-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="9ad15-168">前面我们实现我们 create （） 操作方法的 HTTP POST 版本时我们具有硬编码为静态字符串 Dinner"HostedBy"属性。</span><span class="sxs-lookup"><span data-stu-id="9ad15-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="9ad15-169">我们可以立即更新此代码以改用 User.Identity.Name 属性，以及自动添加为主机创建 Dinner 的 RSVP:</span><span class="sxs-lookup"><span data-stu-id="9ad15-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="9ad15-170">因为我们已添加到 create （） 方法的 [Authorize] 特性，可确保 ASP.NET MVC，操作方法才会执行用户访问 Dinners/创建 URL 中记录在站点上。</span><span class="sxs-lookup"><span data-stu-id="9ad15-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="9ad15-171">在这种情况下，User.Identity.Name 属性值将始终包含一个有效的用户名。</span><span class="sxs-lookup"><span data-stu-id="9ad15-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="9ad15-172">编辑时使用 User.Identity.Name 属性 Dinners</span><span class="sxs-lookup"><span data-stu-id="9ad15-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="9ad15-173">现在让我们添加一些授权逻辑，可将用户限制，以便它们只能编辑他们自己承载的 dinners 属性。</span><span class="sxs-lookup"><span data-stu-id="9ad15-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="9ad15-174">若要帮助实现此目的，我们将首先到我们的 Dinner 对象 （在我们之前生成的 Dinner.cs 分部类） 中添加一个"IsHostedBy(username)"帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="9ad15-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="9ad15-175">此帮助器方法返回 true 或 false 具体取决于是否提供的用户名匹配的 Dinner HostedBy 属性，并封装执行不区分大小写的字符串比较它们所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="9ad15-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="9ad15-176">我们然后将我们 DinnersController 类中对 edit （） 操作方法添加 [Authorize] 特性。</span><span class="sxs-lookup"><span data-stu-id="9ad15-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="9ad15-177">这将确保用户必须登录请求 */Dinners/编辑 / [id]* URL。</span><span class="sxs-lookup"><span data-stu-id="9ad15-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="9ad15-178">然后，我们可以将代码添加到我们使用 Dinner.IsHostedBy(username) 帮助器方法来验证登录的用户与 Dinner 主机的编辑方法。</span><span class="sxs-lookup"><span data-stu-id="9ad15-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="9ad15-179">如果用户不是主机，我们将显示"InvalidOwner"视图，并终止请求。</span><span class="sxs-lookup"><span data-stu-id="9ad15-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="9ad15-180">若要执行此操作的代码类似于下面：</span><span class="sxs-lookup"><span data-stu-id="9ad15-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="9ad15-181">我们可以右键单击 \Views\Dinners 目录，然后选择添加-&gt;查看菜单命令来创建新的"InvalidOwner"视图。</span><span class="sxs-lookup"><span data-stu-id="9ad15-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="9ad15-182">我们将填充与该错误消息如下：</span><span class="sxs-lookup"><span data-stu-id="9ad15-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="9ad15-183">和现在当用户尝试编辑不拥有 dinner，他们将获得一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="9ad15-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="9ad15-184">控制器可以锁定，删除 Dinners，并确保只有 Dinner 主持人可以删除它的权限中，我们可以 delete （） 操作方法的重复相同的步骤。</span><span class="sxs-lookup"><span data-stu-id="9ad15-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="9ad15-185">显示/隐藏编辑和删除链接</span><span class="sxs-lookup"><span data-stu-id="9ad15-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="9ad15-186">我们要链接到我们的 DinnersController 类的编辑和删除操作方法的详细信息 url:</span><span class="sxs-lookup"><span data-stu-id="9ad15-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="9ad15-187">目前，我们将演示不考虑到详细信息 URL 的访问者是否 dinner 的主机的编辑和删除操作链接。</span><span class="sxs-lookup"><span data-stu-id="9ad15-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="9ad15-188">让我们更改，以便只显示链接，如果正在访问的用户是 dinner 的所有者。</span><span class="sxs-lookup"><span data-stu-id="9ad15-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="9ad15-189">Details() 操作方法中我们 DinnersController 检索 Dinner 对象，然后将其作为模型对象中传递给视图模板：</span><span class="sxs-lookup"><span data-stu-id="9ad15-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="9ad15-190">我们可以更新视图模板来有条件地显示/隐藏编辑和删除链接使用 Dinner.IsHostedBy() 帮助器方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9ad15-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="9ad15-191">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9ad15-191">Next Steps</span></span>

<span data-ttu-id="9ad15-192">让我们现在看看如何启用对使用 AJAX 的 dinner 的 RSVP 的已经过身份验证的用户。</span><span class="sxs-lookup"><span data-stu-id="9ad15-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ad15-193">[上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="9ad15-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
