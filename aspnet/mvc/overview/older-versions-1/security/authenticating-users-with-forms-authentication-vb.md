---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 与用户进行身份验证 Forms 身份验证 (VB) |Microsoft 文档
author: microsoft
description: 了解如何使用 [Authorize] 属性用密码保护 MVC 应用程序中的特定页。 了解如何使用网站管理太...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/27/2009
ms.topic: article
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ff425a4c9728de2eec3d0c94e76cb51a15de487
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="authenticating-users-with-forms-authentication-vb"></a><span data-ttu-id="dd4ac-104">使用 Forms 身份验证 (VB) 的用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="dd4ac-104">Authenticating Users with Forms Authentication (VB)</span></span>
====================
<span data-ttu-id="dd4ac-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="dd4ac-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="dd4ac-106">了解如何使用 [Authorize] 属性用密码保护 MVC 应用程序中的特定页。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="dd4ac-107">了解如何使用网站管理工具来创建和管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="dd4ac-108">你还了解了如何配置用户帐户和角色信息的存储位置。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-108">You also learn how to configure where user account and role information is stored.</span></span>


<span data-ttu-id="dd4ac-109">本教程旨在说明如何使用窗体身份验证保护 ASP.NET MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="dd4ac-110">了解如何使用网站管理工具来创建用户和角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="dd4ac-111">你还了解了如何防止未经授权的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="dd4ac-112">最后，你将了解如何配置存储用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="dd4ac-113">使用网站管理工具</span><span class="sxs-lookup"><span data-stu-id="dd4ac-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="dd4ac-114">我们执行任何其他操作之前，我们应首先创建一些用户和角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="dd4ac-115">创建新用户和角色的最简单方法是利用 Visual Studio 2008 网站管理工具。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="dd4ac-116">你可以通过选择菜单选项来启动此工具**项目中，ASP.NET 配置**。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="dd4ac-117">或者，你可以通过单击命中将显示在解决方案资源管理器窗口顶部世界 hammer （某种程度上可怕） 图标来启动网站管理工具 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="dd4ac-118">**图 1 – 启动网站管理工具**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

<span data-ttu-id="dd4ac-120">在网站管理工具，你创建新用户和角色通过选择安全选项卡。单击**创建用户**链接创建一个名为 Stephen 的新用户 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="dd4ac-121">Stephen 用户提供所需的任何密码 (例如，*机密*)。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="dd4ac-122">**图 2 – 创建新用户**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

<span data-ttu-id="dd4ac-124">通过第一个启用角色并定义一个或多个角色创建新的角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="dd4ac-125">通过单击启用角色**启用角色**链接。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="dd4ac-126">接下来，创建名为的角色*管理员*通过单击**创建或管理角色**链接 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="dd4ac-127">**图 3 – 创建一个新角色**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

<span data-ttu-id="dd4ac-129">最后，创建名为 Sally 的新用户并将 Sally 相关联具有管理员角色，通过单击创建用户链接并选择管理员创建 Sally 时 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="dd4ac-130">**图 4 – 向角色添加用户**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

<span data-ttu-id="dd4ac-132">当所有是说，而且完成时，你应具有名为 Stephen 和 Sally 的两个新用户。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="dd4ac-133">你还应具有名为管理员的新角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="dd4ac-134">Sally 是管理员角色的成员，并且 Stephen 不是。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="dd4ac-135">需要授权</span><span class="sxs-lookup"><span data-stu-id="dd4ac-135">Requiring Authorization</span></span>

<span data-ttu-id="dd4ac-136">你可以要求用户进行身份验证的用户通过将 [Authorize] 属性添加到操作调用的控制器操作之前。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="dd4ac-137">你可以将 [Authorize] 特性应用于单个控制器操作或可以将此特性应用于整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="dd4ac-138">例如，列表 1 中的控制器公开名为 CompanySecrets() 的操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="dd4ac-139">因为此操作带有 [Authorize] 属性修饰的除非用户进行身份验证，不能调用此操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="dd4ac-140">**列表 1 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-140">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

<span data-ttu-id="dd4ac-141">如果通过在浏览器中的地址栏中输入 URL /Home/CompanySecrets 调用 CompanySecrets() 操作并且你不是经过身份验证的用户，则你将重定向到登录视图自动 （参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="dd4ac-142">**图 5-登录视图**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-142">**Figure 5 – The Login view**</span></span>

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

<span data-ttu-id="dd4ac-144">登录视图可用于输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="dd4ac-145">如果你不是已注册的用户，则可以单击**注册**链接以导航到注册查看 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="dd4ac-146">注册视图可用于创建新的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="dd4ac-147">**图 6-注册视图**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

<span data-ttu-id="dd4ac-149">成功登录后，你可以看到 CompanySecrets 查看 （请参阅图 7）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="dd4ac-150">默认情况下，你将继续登录状态，直到关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="dd4ac-151">**图 7-CompanySecrets 视图**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="dd4ac-153">用户名或用户角色授权</span><span class="sxs-lookup"><span data-stu-id="dd4ac-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="dd4ac-154">[Authorize] 属性可用于限制对为特定的一组的用户或一组特定的用户角色的控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="dd4ac-155">例如，列出 2 中修改后的主控制器包含名为 StephenSecrets() 和 AdministratorSecrets() 的两个新操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="dd4ac-156">**Listing 2 – Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-156">**Listing 2 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

<span data-ttu-id="dd4ac-157">只有具有用户名 Stephen 的用户可以调用 StephenSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="dd4ac-158">所有其他用户获取重定向到登录视图。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="dd4ac-159">用户属性接受用户帐户名称的逗号分隔的列表。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="dd4ac-160">只有管理员角色中的用户可以调用 AdministratorSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="dd4ac-161">例如，因为 Sally 是 Administrators 组的成员，她可以调用 AdministratorSecrets() 操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="dd4ac-162">所有其他用户获取重定向到登录视图。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="dd4ac-163">角色属性接受以逗号分隔列表的角色的名称。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="dd4ac-164">配置身份验证</span><span class="sxs-lookup"><span data-stu-id="dd4ac-164">Configuring Authentication</span></span>

<span data-ttu-id="dd4ac-165">此时，你可能想知道存储用户帐户和角色信息。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="dd4ac-166">默认情况下，信息存储在命名的 ASPNETDB.mdf 位于在 MVC 应用程序的应用程序中的 (RANU) SQL Express 的数据库\_数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="dd4ac-167">此数据库是由 ASP.NET 框架时自动生成你开始使用成员资格。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="dd4ac-168">若要查看 ASPNETDB.mdf 数据库在解决方案资源管理器窗口中的，首先需要选择菜单选项项目中，显示所有文件。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="dd4ac-169">开发应用程序时，使用默认 SQL Express 数据库是允许的。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="dd4ac-170">最有可能，但是，不会想要使用的默认 ASPNETDB.mdf 数据库对生产应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="dd4ac-171">在这种情况下，你可以更改用户帐户信息通过完成以下两个步骤的存储位置：</span><span class="sxs-lookup"><span data-stu-id="dd4ac-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="dd4ac-172">将应用程序服务数据库对象添加到你的生产数据库-更改应用程序连接字符串，以指向您的生产数据库</span><span class="sxs-lookup"><span data-stu-id="dd4ac-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="dd4ac-173">第一步是添加所有必要的数据库对象 （表和存储的过程） 到你的生产数据库。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="dd4ac-174">将这些对象添加到新数据库的最简单方法是利用 ASP.NET SQL Server 安装向导 （请参阅图 8）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="dd4ac-175">可以通过从 Microsoft Visual Studio 2008 程序组中打开 Visual Studio 2008 命令提示并从命令提示符下执行以下命令来启动此工具：</span><span class="sxs-lookup"><span data-stu-id="dd4ac-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="dd4ac-176">aspnet\_regsql</span><span class="sxs-lookup"><span data-stu-id="dd4ac-176">aspnet\_regsql</span></span>

<span data-ttu-id="dd4ac-177">**图 8-ASP.NET SQL Server 安装向导**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

<span data-ttu-id="dd4ac-179">ASP.NET SQL Server 安装向导，可选择你的网络上的 SQL Server 数据库并安装所有所需的 ASP.NET 应用程序服务数据库对象。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="dd4ac-180">数据库服务器不需要位于要在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="dd4ac-181">如果你不想使用 ASP.NET SQL Server 安装向导，然后你可以找到 SQL 脚本的以下文件夹中添加应用程序服务数据库对象：</span><span class="sxs-lookup"><span data-stu-id="dd4ac-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> 
> <span data-ttu-id="dd4ac-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="dd4ac-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>


<span data-ttu-id="dd4ac-183">创建必要的数据库对象后，你需要修改 MVC 应用程序使用的数据库连接。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="dd4ac-184">修改你的 web 配置 (web.config) 文件中的 ApplicationServices 连接字符串，使它指向生产数据库。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="dd4ac-185">例如，列出 3 中修改后的连接指向名为的 MyProductionDB （原始 ApplicationServices 连接字符串已被注释掉） 的数据库。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="dd4ac-186">**列出 3 – Web.config**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="dd4ac-187">配置数据库权限</span><span class="sxs-lookup"><span data-stu-id="dd4ac-187">Configuring Database Permissions</span></span>

<span data-ttu-id="dd4ac-188">如果你使用集成安全性连接到你的数据库将需要将正确的 Windows 用户帐户作为登录名添加到你的数据库。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="dd4ac-189">正确的帐户取决于作为 web 服务器使用的 Internet 信息服务的 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="dd4ac-190">正确的用户帐户还取决于你的操作系统。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="dd4ac-191">如果正在使用 ASP.NET 开发服务器 （由 Visual Studio 使用的默认 web 服务器） 你的应用程序将在您的 Windows 用户帐户的上下文中执行。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="dd4ac-192">在这种情况下，你需要将您的 Windows 用户帐户添加为数据库服务器登录名。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="dd4ac-193">或者，如果你使用 Internet 信息服务然后你需要添加 ASPNET 帐户或 NT 机构/网络服务帐户作为数据库服务器登录名。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="dd4ac-194">如果你正在使用 Windows XP，请将 ASPNET 帐户作为登录名添加到你的数据库。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="dd4ac-195">如果你正在使用较新操作系统，如 Windows Vista 或 Windows Server 2008 中，请将 NT 机构/网络服务帐户添加为数据库登录名。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="dd4ac-196">可以通过使用 Microsoft SQL Server Management Studio 到你的数据库中添加新的用户帐户 （请参阅图 9）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="dd4ac-197">**图 9-创建新的 Microsoft SQL Server 登录名**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

<span data-ttu-id="dd4ac-199">创建所需的登录名后，你需要登录名映射到具有正确的数据库角色的数据库用户。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="dd4ac-200">双击该登录名并选择用户映射选项卡。选择一个或多个应用程序服务数据库角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="dd4ac-201">例如，若要对用户进行身份验证，你需要启用 aspnet\_成员资格\_BasicAccess 数据库角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="dd4ac-202">若要创建新用户，你需要启用 aspnet\_成员资格\_FullAccess 数据库角色 （请参阅图 10）。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="dd4ac-203">**图 10 – 添加应用程序服务数据库角色**</span><span class="sxs-lookup"><span data-stu-id="dd4ac-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="dd4ac-205">总结</span><span class="sxs-lookup"><span data-stu-id="dd4ac-205">Summary</span></span>

<span data-ttu-id="dd4ac-206">在本教程中，您学习了如何构建一个 ASP.NET MVC 应用程序时，使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="dd4ac-207">首先，您学习了如何通过利用网站管理工具创建新用户和角色。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="dd4ac-208">接下来，您学习了如何使用 [Authorize] 属性以防止未经授权的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="dd4ac-209">最后，您学习了如何配置你的 MVC 应用程序在生产数据库中存储用户和角色信息。</span><span class="sxs-lookup"><span data-stu-id="dd4ac-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="dd4ac-210">[上一页](preventing-javascript-injection-attacks-cs.md)
> [下一页](authenticating-users-with-windows-authentication-vb.md)</span><span class="sxs-lookup"><span data-stu-id="dd4ac-210">[Previous](preventing-javascript-injection-attacks-cs.md)
[Next](authenticating-users-with-windows-authentication-vb.md)</span></span>
