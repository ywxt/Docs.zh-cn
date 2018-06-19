---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成员身份 |Microsoft 文档
author: microsoft
description: ASP.NET 成员资格生成的窗体身份验证模型成功从 ASP.NET 1.x。 ASP.NET 窗体身份验证提供 incorp 到一种简便方式...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: 1a5a495845b60f9aac51c9776311af67f5dc8767
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
ms.locfileid: "28885551"
---
<a name="membership"></a><span data-ttu-id="0c20b-104">成员身份</span><span class="sxs-lookup"><span data-stu-id="0c20b-104">Membership</span></span>
====================
<span data-ttu-id="0c20b-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0c20b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0c20b-106">ASP.NET 成员资格生成的窗体身份验证模型成功从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="0c20b-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="0c20b-107">ASP.NET 窗体身份验证可以方便地将一个登录窗体合并到 ASP.NET 应用程序并验证针对数据库或其他数据存储的用户。</span><span class="sxs-lookup"><span data-stu-id="0c20b-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>


<span data-ttu-id="0c20b-108">ASP.NET 成员资格生成的窗体身份验证模型成功从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="0c20b-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="0c20b-109">ASP.NET 窗体身份验证可以方便地将一个登录窗体合并到 ASP.NET 应用程序并验证针对数据库或其他数据存储的用户。</span><span class="sxs-lookup"><span data-stu-id="0c20b-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="0c20b-110">FormsAuthentication 类的成员，使能够处理身份验证的 cookie、 检查有效的登录名、 出等用户直接登录。但是，在 ASP.NET 1.x 应用程序中实现窗体身份验证可能需要大量的代码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="0c20b-111">在 ASP.NET 2.0 中的成员身份是通过使用单独的窗体身份验证一次重大进步。</span><span class="sxs-lookup"><span data-stu-id="0c20b-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="0c20b-112">（成员身份是最强健结合了窗体身份验证，但使用 Forms 身份验证并不是必需）。正如您很快将看到，你可以使用 ASP.NET 成员资格和登录控件中 ASP.NET 2.0 来实现功能强大的成员身份系统而无需在所有编写大量的代码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="0c20b-113">在 ASP.NET 2.0 中实现的成员身份</span><span class="sxs-lookup"><span data-stu-id="0c20b-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="0c20b-114">成员身份由以下四个步骤来实现。</span><span class="sxs-lookup"><span data-stu-id="0c20b-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="0c20b-115">请记住，有许多子步骤，以及可以以及实现的可选配置涉及。</span><span class="sxs-lookup"><span data-stu-id="0c20b-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="0c20b-116">这些步骤是为了演示的配置成员资格的大体形势。</span><span class="sxs-lookup"><span data-stu-id="0c20b-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="0c20b-117">创建成员资格数据库 （如果使用的 SQL Server 作为成员资格存储。）</span><span class="sxs-lookup"><span data-stu-id="0c20b-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="0c20b-118">在你的应用程序配置文件中指定的成员身份选项。</span><span class="sxs-lookup"><span data-stu-id="0c20b-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="0c20b-119">（成员资格启用默认情况下中）。</span><span class="sxs-lookup"><span data-stu-id="0c20b-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="0c20b-120">确定你想要使用的成员身份存储的类型。</span><span class="sxs-lookup"><span data-stu-id="0c20b-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="0c20b-121">选项包括：</span><span class="sxs-lookup"><span data-stu-id="0c20b-121">Options are:</span></span> 

    - <span data-ttu-id="0c20b-122">Microsoft SQL Server （版本 7.0 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="0c20b-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="0c20b-123">Active Directory Store</span><span class="sxs-lookup"><span data-stu-id="0c20b-123">Active Directory Store</span></span>
    - <span data-ttu-id="0c20b-124">自定义成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="0c20b-124">Custom membership provider</span></span>
4. <span data-ttu-id="0c20b-125">配置 ASP.NET 表单身份验证的应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c20b-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="0c20b-126">同样，成员身份旨在充分利用 Forms 身份验证，但使用 Forms 身份验证并不是必需。</span><span class="sxs-lookup"><span data-stu-id="0c20b-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="0c20b-127">定义成员身份的用户帐户和配置角色，如果需要。</span><span class="sxs-lookup"><span data-stu-id="0c20b-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="0c20b-128">创建成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="0c20b-128">Creating the Membership Database</span></span>

<span data-ttu-id="0c20b-129">如果您正在使用 SQL Server 7.0 或更高版本作为成员资格存储，可以使用 aspnet\_regsql 实用程序 （可非常轻松地从 Visual Studio.NET 2005年命令提示） 来配置你的数据库。</span><span class="sxs-lookup"><span data-stu-id="0c20b-129">If youre using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="0c20b-130">Aspnet\_作为命令提示符工具或通过 GUI 向导，可以使用 regsql 实用工具。</span><span class="sxs-lookup"><span data-stu-id="0c20b-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="0c20b-131">向导方法是配置你的数据库的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="0c20b-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="0c20b-132">若要访问该向导，只需运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="0c20b-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="0c20b-133">一旦你运行该命令，就将如下所示显示与 ASP.NET SQL Server 安装向导。</span><span class="sxs-lookup"><span data-stu-id="0c20b-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>


![](membership/_static/image1.jpg)

<span data-ttu-id="0c20b-134">**图 1**</span><span class="sxs-lookup"><span data-stu-id="0c20b-134">**Figure 1**</span></span>


<span data-ttu-id="0c20b-135">ASP.NET SQL Server 安装向导在向导中指定的实例中创建网站。</span><span class="sxs-lookup"><span data-stu-id="0c20b-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="0c20b-136">但是，ASP.NET 将使用连接字符串在 machine.config 文件中连接到你的数据库。</span><span class="sxs-lookup"><span data-stu-id="0c20b-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="0c20b-137">默认情况下，此连接字符串将指向的 SQL Server 2005 实例，因此如果你使用的 SQL Server 2000 或 SQL Server 7.0 实例，你将需要修改 machine.config 文件中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="0c20b-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="0c20b-138">该连接字符串可以位于此处：</span><span class="sxs-lookup"><span data-stu-id="0c20b-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="0c20b-139">遗憾的是，如果你无需修改连接字符串，ASP.NET 将不为你提供描述性错误。</span><span class="sxs-lookup"><span data-stu-id="0c20b-139">Unfortunately, if you dont modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="0c20b-140">它将只需继续抱怨说你尚未创建数据库。</span><span class="sxs-lookup"><span data-stu-id="0c20b-140">It will just continue to complain saying that you havent created the database.</span></span> <span data-ttu-id="0c20b-141">在上面的示例中，我已修改为指向我的本地 SQL Server 2000 实例的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="0c20b-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="0c20b-142">指定配置和添加用户和角色</span><span class="sxs-lookup"><span data-stu-id="0c20b-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="0c20b-143">配置成员资格的下一步是将所需的信息添加到应用程序的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="0c20b-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="0c20b-144">在 ASP.NET 1.x，修改 web.config 文件是有时很困难由于 lowerCamelCase 利用和缺少的 Intellisense 问题。</span><span class="sxs-lookup"><span data-stu-id="0c20b-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="0c20b-145">Visual Studio.NET 2005年使任务可以更加容易与 Intellisense 一起配置文件，但 ASP.NET 2.0 就更进一步提供进行编辑配置文件的 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="0c20b-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="0c20b-146">你可以通过单击如下所示的解决方案资源管理器工具栏上的 ASP.NET 配置按钮启动 Web 接口。</span><span class="sxs-lookup"><span data-stu-id="0c20b-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="0c20b-147">你也可以启动通过插入登录控件时显示的弹出窗口的 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="0c20b-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>


![](membership/_static/image2.jpg)

<span data-ttu-id="0c20b-148">**图 2**</span><span class="sxs-lookup"><span data-stu-id="0c20b-148">**Figure 2**</span></span>


<span data-ttu-id="0c20b-149">这将启动 ASP.NET 网站管理工具如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c20b-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="0c20b-150">ASP.NET 网站管理是一个四个选项卡接口，可以轻松地管理应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="0c20b-151">提供了以下选项卡：</span><span class="sxs-lookup"><span data-stu-id="0c20b-151">The following tabs are available:</span></span>

- <span data-ttu-id="0c20b-152">**主页**</span><span class="sxs-lookup"><span data-stu-id="0c20b-152">**Home**</span></span>
- <span data-ttu-id="0c20b-153">**安全**配置用户、 角色和访问。</span><span class="sxs-lookup"><span data-stu-id="0c20b-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="0c20b-154">**应用程序**配置应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="0c20b-155">**提供程序**配置和测试应用程序成员资格提供程序。</span><span class="sxs-lookup"><span data-stu-id="0c20b-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="0c20b-156">网站管理工具，可以轻松地创建新用户，创建新的角色，以及管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="0c20b-157">此功能在 Windows 界面中不可用。</span><span class="sxs-lookup"><span data-stu-id="0c20b-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="0c20b-158">Windows 界面，您可以轻松地定义授权设置和添加、 删除和管理提供程序，不在网站管理工具的功能。</span><span class="sxs-lookup"><span data-stu-id="0c20b-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="0c20b-159">若要启动 Windows 界面，打开 Internet Information Services 管理单元，右键单击你的应用程序，然后选择属性。</span><span class="sxs-lookup"><span data-stu-id="0c20b-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="0c20b-160">单击 ASP.NET 选项卡，然后单击编辑配置按钮。</span><span class="sxs-lookup"><span data-stu-id="0c20b-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="0c20b-161">（若要启用编辑配置按钮的 ASP.NET 2.0 下必须运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c20b-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="0c20b-162">你可以配置 ASP.NET 版本在 ASP.NET 对话框。）ASP.NET 配置设置对话框将显示如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c20b-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>


![](membership/_static/image3.jpg)

<span data-ttu-id="0c20b-163">**图 3**</span><span class="sxs-lookup"><span data-stu-id="0c20b-163">**Figure 3**</span></span>


<span data-ttu-id="0c20b-164">在常规选项卡上列出了连接字符串和应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="0c20b-165">在父配置文件 （machine.config 或在较高级别 web.config） 中定义将以斜体显示的任何设置，并不将以斜体显示的设置从应用程序配置文件。</span><span class="sxs-lookup"><span data-stu-id="0c20b-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="0c20b-166">如果添加设置，则已删除或编辑应用程序级别中，ASP.NET 将添加、 删除或修改在应用程序级别 web.config 而不是从它继承的配置文件中删除该设置的设置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="0c20b-167">身份验证选项卡如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c20b-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="0c20b-168">这是你将在其中配置成员身份设置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="0c20b-169">窗体身份验证设置，成员资格提供程序和角色提供程序可以在此处配置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>


![](membership/_static/image4.jpg)

<span data-ttu-id="0c20b-170">**图 4**</span><span class="sxs-lookup"><span data-stu-id="0c20b-170">**Figure 4**</span></span>


## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="0c20b-171">在你的应用程序中实现的成员身份</span><span class="sxs-lookup"><span data-stu-id="0c20b-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="0c20b-172">在你的应用程序中实现 ASP.NET 2.0 成员身份的最简单方法是使用提供的登录控件。</span><span class="sxs-lookup"><span data-stu-id="0c20b-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="0c20b-173">此方法可以实现 ASP.NET 2.0 成员资格的基础知识，而无需编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="0c20b-174">以下的登录控件是在 ASP.NET 2.0 中可用：</span><span class="sxs-lookup"><span data-stu-id="0c20b-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="0c20b-175">登录控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-175">Login Control</span></span>

<span data-ttu-id="0c20b-176">该登录控件提供一个接口，使用户能够登录到成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="0c20b-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="0c20b-177">它提供的用户名和密码 textboxt 和登录按钮。</span><span class="sxs-lookup"><span data-stu-id="0c20b-177">It provides you with a username and password textboxt and a login button.</span></span> <span data-ttu-id="0c20b-178">许多其他常见功能，如将其注册为那些尚未完成使一个复选框，使用户可以自动在后续的访问的登录名的用户的链接、 密码提示，等等的链接。登录控件的所有功能都都通过控件的属性可自定义。</span><span class="sxs-lookup"><span data-stu-id="0c20b-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="0c20b-179">在 ASP.NET 中 1.x，开发人员必须编写大量代码以使用窗体身份验证时执行查找。</span><span class="sxs-lookup"><span data-stu-id="0c20b-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="0c20b-180">具有 ASP.NET 2.0 成员身份，你可以无需编写任何代码在所有验证用户。</span><span class="sxs-lookup"><span data-stu-id="0c20b-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="0c20b-181">ASP.NET 自动将为您完成用户的查找。</span><span class="sxs-lookup"><span data-stu-id="0c20b-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="0c20b-182">(如果使用 Login 控件，而不使用 ASP.NET 成员资格，则可以使用**OnAuthenticate**方法以验证此用户。)</span><span class="sxs-lookup"><span data-stu-id="0c20b-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="0c20b-183">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-183">LoginView Control</span></span>

<span data-ttu-id="0c20b-184">LoginView 控件是一个模板化控件，默认情况下; 提供两个模板AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="0c20b-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="0c20b-185">显示的模板取决于将用户登录到成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="0c20b-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="0c20b-186">此控件通常用于显示用户尚未登录时的登录控件和 LoginStatus 控制和/或其他登录控件时，用户已登录。</span><span class="sxs-lookup"><span data-stu-id="0c20b-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="0c20b-187">如果你正在使用 ASP.NET 应用程序中的角色管理，LoginView 控件可以显示特定的模板基于用户角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="0c20b-188">（更多关于 ASP.NET 角色管理将在后面说明。）</span><span class="sxs-lookup"><span data-stu-id="0c20b-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="0c20b-189">取回控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-189">PasswordRecovery Control</span></span>

<span data-ttu-id="0c20b-190">取回控件允许用户收到一封电子邮件使用他或她的当前密码或重置他或她的密码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="0c20b-191">明文形式和加密的密码可以恢复并且通过电子邮件发送给用户。</span><span class="sxs-lookup"><span data-stu-id="0c20b-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="0c20b-192">如果密码哈希处理，将无法恢复。</span><span class="sxs-lookup"><span data-stu-id="0c20b-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="0c20b-193">而是用户将需要以执行密码重置。</span><span class="sxs-lookup"><span data-stu-id="0c20b-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="0c20b-194">LoginStatus 控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-194">LoginStatus Control</span></span>

<span data-ttu-id="0c20b-195">LoginStatus 控件用于向当前登录用户显示的用户未登录的登录名指示器和注销指示器。</span><span class="sxs-lookup"><span data-stu-id="0c20b-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="0c20b-196">Request.IsAuthenticated 属性用于确定哪些标记，以显示。</span><span class="sxs-lookup"><span data-stu-id="0c20b-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="0c20b-197">LoginStatus 控件显示的指示器可以是文本 (通过实现**LoginText**和**LogoutText**属性) 或图像 (通过实现**LoginImageUrl**和**LogoutImageUrl**属性。)</span><span class="sxs-lookup"><span data-stu-id="0c20b-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="0c20b-198">当用户注销通过 LoginStatus 控制时，他或她将重定向到指定的 URL **LogoutPageUrl**属性。</span><span class="sxs-lookup"><span data-stu-id="0c20b-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="0c20b-199">如果未设置该属性，则会刷新当前页。</span><span class="sxs-lookup"><span data-stu-id="0c20b-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="0c20b-200">站点可能受窗体身份验证，因为当前页的刷新将用户重定向到该网站的登录页。</span><span class="sxs-lookup"><span data-stu-id="0c20b-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="0c20b-201">LoginName 控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-201">LoginName Control</span></span>

<span data-ttu-id="0c20b-202">LoginName 控件显示当前登录到网站的用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="0c20b-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="0c20b-203">通过</span><span class="sxs-lookup"><span data-stu-id="0c20b-203">CreateUserWizard Control</span></span>

<span data-ttu-id="0c20b-204">通过向用户提供一种简便方式注册你的成员身份系统。</span><span class="sxs-lookup"><span data-stu-id="0c20b-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="0c20b-205">你可以通过如下所示的界面添加步骤 （实现为一个 WizardSteps 的集合）。</span><span class="sxs-lookup"><span data-stu-id="0c20b-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>


![](membership/_static/image5.jpg)

<span data-ttu-id="0c20b-206">**图 5**</span><span class="sxs-lookup"><span data-stu-id="0c20b-206">**Figure 5**</span></span>


<span data-ttu-id="0c20b-207">CreateUserWizard 是一个模板化控件，从向导类派生并提供了以下模板：</span><span class="sxs-lookup"><span data-stu-id="0c20b-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="0c20b-208">**HeaderTemplate**此模板控制的标头的向导的外观。</span><span class="sxs-lookup"><span data-stu-id="0c20b-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="0c20b-209">**SidebarTemplate**此模板控制的侧栏向导的外观。</span><span class="sxs-lookup"><span data-stu-id="0c20b-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="0c20b-210">**StartNavigationTemplate**在导航窗格的外观开始步骤在向导的此模板控制。</span><span class="sxs-lookup"><span data-stu-id="0c20b-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="0c20b-211">**StepNavigationTemplate**此模板控制在不启动或完成步骤时的导航区域的外观。</span><span class="sxs-lookup"><span data-stu-id="0c20b-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="0c20b-212">**FinishNavigationTemplate**此模板控制时在完成步骤的导航区域中的外观。</span><span class="sxs-lookup"><span data-stu-id="0c20b-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="0c20b-213">此外，对于为向导添加每个步骤，ASP.NET 将创建包含 ContentTemplate 和为该步骤 CustomNavigationTemplate 的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="0c20b-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="0c20b-214">有关自定义 CreateUserWizard 的完整详细信息，请参阅 VS.NET 2005 文档：</span><span class="sxs-lookup"><span data-stu-id="0c20b-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="0c20b-215">ChangePassword 控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-215">ChangePassword Control</span></span>

<span data-ttu-id="0c20b-216">ChangePassword 控件允许用户更改其密码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="0c20b-217">如果 DisplayUserName 属性为 true （它位于 false 默认情况下），用户可以在用户未登录时更改他或她的密码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="0c20b-218">如果用户*是*已登录和 DisplayUserName 属性为 true 时，用户将能够更改不记录在提供他们知道该用户的用户 ID 的另一个用户的密码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="0c20b-219">请记住，如果你希望用户能够更改密码，而无需登录，你将需要确保 ChangePassword 控件显示在其的页面允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="0c20b-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="0c20b-220">显然，用户将必须提供旧密码，以更改其密码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="0c20b-221">角色管理</span><span class="sxs-lookup"><span data-stu-id="0c20b-221">Role Management</span></span>

<span data-ttu-id="0c20b-222">角色管理，可将用户分配到特定角色，然后限制对特定文件或文件夹基于该角色的访问。</span><span class="sxs-lookup"><span data-stu-id="0c20b-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="0c20b-223">角色管理还提供一个 API，以便你可以以编程方式确定 someones 角色或确定对特定角色中的所有用户并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="0c20b-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="0c20b-224">角色管理不是 ASP.NET 成员身份要求也不是为了使用角色管理要求的成员身份。</span><span class="sxs-lookup"><span data-stu-id="0c20b-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="0c20b-225">但是，这两个很好地对相互进行补充，以及有可能，开发人员将使用这些与相互结合使用。</span><span class="sxs-lookup"><span data-stu-id="0c20b-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="0c20b-226">若要启用应用程序中的角色管理，请在 web.config 文件中进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="0c20b-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="0c20b-227">当**cacheRolesInCookie**属性设置为 true，ASP.NET 缓存客户端的 cookie 中的用户角色的成员身份。</span><span class="sxs-lookup"><span data-stu-id="0c20b-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="0c20b-228">这允许角色查找，以调入 RoleProvider 的情况下发生。</span><span class="sxs-lookup"><span data-stu-id="0c20b-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="0c20b-229">当使用此属性，开发人员建议确保**cookieProtection**属性将设为 All。</span><span class="sxs-lookup"><span data-stu-id="0c20b-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="0c20b-230">（这是默认设置）。这可确保 cookie 数据进行加密，并可帮助确保的 cookie 内容尚未被更改。</span><span class="sxs-lookup"><span data-stu-id="0c20b-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents havent been altered.</span></span> <span data-ttu-id="0c20b-231">可以使用网站管理工具添加角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="0c20b-232">它允许你轻松地定义角色、 配置的访问权限的基于这些角色的站点部分并将用户分配到角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>


![](membership/_static/image6.jpg)

<span data-ttu-id="0c20b-233">**图 6**</span><span class="sxs-lookup"><span data-stu-id="0c20b-233">**Figure 6**</span></span>


<span data-ttu-id="0c20b-234">如上所示，可以通过只需输入角色的名称，然后单击添加角色添加新角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="0c20b-235">可以管理或通过单击相应的链接的现有角色列表中删除现有的角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="0c20b-236">当你管理角色时，你可以添加或删除用户，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c20b-236">When you manage a role, you can add or remove users as shown below.</span></span>


![](membership/_static/image7.jpg)

<span data-ttu-id="0c20b-237">**图 7**</span><span class="sxs-lookup"><span data-stu-id="0c20b-237">**Figure 7**</span></span>


<span data-ttu-id="0c20b-238">通过检查角色中用户是复选框，可以轻松地将用户添加到特定角色中。</span><span class="sxs-lookup"><span data-stu-id="0c20b-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="0c20b-239">ASP.NET 将使用适当的项自动更新成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="0c20b-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="0c20b-240">你还需要配置你的应用程序的访问规则。</span><span class="sxs-lookup"><span data-stu-id="0c20b-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="0c20b-241">ASP.NET 1.x 开发人员熟悉这样通过&lt;授权&gt;web.config 文件中和该选项中的元素是 ASP.NET 2.0 中仍然可用。</span><span class="sxs-lookup"><span data-stu-id="0c20b-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="0c20b-242">但是，轻松地管理访问权限的规则使用网站管理工具如图所示下面。</span><span class="sxs-lookup"><span data-stu-id="0c20b-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>


![](membership/_static/image8.jpg)

<span data-ttu-id="0c20b-243">**图 8**</span><span class="sxs-lookup"><span data-stu-id="0c20b-243">**Figure 8**</span></span>


<span data-ttu-id="0c20b-244">在这种情况下，突出显示的管理文件夹 （其难看到，因为该工具使其突出显示以浅灰色） 并且已被管理员角色授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="0c20b-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="0c20b-245">将拒绝所有其他用户。</span><span class="sxs-lookup"><span data-stu-id="0c20b-245">All other users are denied.</span></span> <span data-ttu-id="0c20b-246">你可以单击头图标以选择一个规则，然后使用上移和下移按钮将规则调整。</span><span class="sxs-lookup"><span data-stu-id="0c20b-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="0c20b-247">ASP.NET 与&lt;授权&gt;元素，它们出现的顺序处理规则。</span><span class="sxs-lookup"><span data-stu-id="0c20b-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="0c20b-248">换而言之，如果在上面的截图中的规则的顺序被取消，没有人就可以访问管理文件夹因为 ASP.NET 将会遇到的第一个规则将拒绝所有人的文件夹的规则。</span><span class="sxs-lookup"><span data-stu-id="0c20b-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="0c20b-249">ASP.NET 2.0 将 web.config 文件添加到要为其指定访问规则的文件夹。</span><span class="sxs-lookup"><span data-stu-id="0c20b-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="0c20b-250">通过配置文件或网站管理工具，可以编辑访问规则。</span><span class="sxs-lookup"><span data-stu-id="0c20b-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="0c20b-251">换而言之，网站管理工具是只需通过其可以在用户友好的环境中编辑配置文件的接口。</span><span class="sxs-lookup"><span data-stu-id="0c20b-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="0c20b-252">在代码中使用角色</span><span class="sxs-lookup"><span data-stu-id="0c20b-252">Using Roles in Code</span></span>

<span data-ttu-id="0c20b-253">用于角色管理的 API 不自从版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="0c20b-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="0c20b-254">**IsInRole**方法用于确定用户是否对特定角色中。</span><span class="sxs-lookup"><span data-stu-id="0c20b-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="0c20b-255">为当前上下文的成员，ASP.NET 还创建 RolePrincipal 实例。</span><span class="sxs-lookup"><span data-stu-id="0c20b-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="0c20b-256">RolePrincipal 对象可以用于获取所有角色与用户所属，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c20b-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="0c20b-257">RoleGroups 使用 LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="0c20b-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="0c20b-258">现在，你已了解角色管理和成员身份，允许简要讨论如何 LoginView 控件利用此功能在 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="0c20b-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="0c20b-259">如前面所述，LoginView 控件是一个模板化的控件，默认情况下; 包含两个模板AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="0c20b-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="0c20b-260">LoginView 任务对话框是 （如下所示） 的链接，您可以编辑 RoleGroups。</span><span class="sxs-lookup"><span data-stu-id="0c20b-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>


![](membership/_static/image9.jpg)

<span data-ttu-id="0c20b-261">**图 9**</span><span class="sxs-lookup"><span data-stu-id="0c20b-261">**Figure 9**</span></span>


<span data-ttu-id="0c20b-262">每个 RoleGroup 对象包含定义 RoleGroup 适用于哪些角色的字符串数组。</span><span class="sxs-lookup"><span data-stu-id="0c20b-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="0c20b-263">若要将新 RoleGroup 添加到 LoginView 控件，请单击编辑 RoleGroups 链接。</span><span class="sxs-lookup"><span data-stu-id="0c20b-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="0c20b-264">在上图中，你可以看到我已将添加为管理员新 RoleGroup。</span><span class="sxs-lookup"><span data-stu-id="0c20b-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="0c20b-265">通过选择该 RoleGroup （RoleGroup[0]) 从视图下拉列表中，可以配置将仅显示管理员角色的成员的模板。</span><span class="sxs-lookup"><span data-stu-id="0c20b-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="0c20b-266">在下图中，我添加了新 RoleGroup 适用于 Sales 角色和分发角色的成员。</span><span class="sxs-lookup"><span data-stu-id="0c20b-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="0c20b-267">这会向登录视图任务对话框中的视图下拉列表中添加第二个 RoleGroup 而不显示任何内容添加到该模板中的销售或分发的任何用户角色。</span><span class="sxs-lookup"><span data-stu-id="0c20b-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>


![](membership/_static/image10.jpg)

<span data-ttu-id="0c20b-268">**图 10**</span><span class="sxs-lookup"><span data-stu-id="0c20b-268">**Figure 10**</span></span>


## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="0c20b-269">重写现有成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="0c20b-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="0c20b-270">有几种方法，你可以扩展的 ASP.NET 成员资格功能。</span><span class="sxs-lookup"><span data-stu-id="0c20b-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="0c20b-271">首先，您可以通过从它继承并重写其方法显然更改 SqlMembershipProvider 类的现有功能。</span><span class="sxs-lookup"><span data-stu-id="0c20b-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="0c20b-272">例如，如果你想要实现您自己的功能，在创建用户时，你可以创建您自己的类继承自 SqlMembershipProvider，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c20b-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="0c20b-273">如果在另一方面，你想要创建自己的提供程序 （用于在访问数据库中，存储成员身份信息，例如所示），你可以创建自己的提供程序。</span><span class="sxs-lookup"><span data-stu-id="0c20b-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="0c20b-274">创建你自己的成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="0c20b-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="0c20b-275">若要创建你自己的成员资格提供程序，首先需要创建从 MembershipProvider 类继承的类。</span><span class="sxs-lookup"><span data-stu-id="0c20b-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="0c20b-276">如果使用 VB.NET，Visual Studio 2005 将添加所有需要重写的方法存根。</span><span class="sxs-lookup"><span data-stu-id="0c20b-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="0c20b-277">如果你使用的 C#，其最多可以添加存根 （stub）。</span><span class="sxs-lookup"><span data-stu-id="0c20b-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="0c20b-278">你将需要重写以下：</span><span class="sxs-lookup"><span data-stu-id="0c20b-278">You will need to override the following:</span></span>

- <span data-ttu-id="0c20b-279">应用程序名称属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-279">ApplicationName property</span></span>
- <span data-ttu-id="0c20b-280">ChangePassword 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-280">ChangePassword function</span></span>
- <span data-ttu-id="0c20b-281">ChangePasswordQuestionAndAnswer 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="0c20b-282">CreateUser 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-282">CreateUser function</span></span>
- <span data-ttu-id="0c20b-283">DeleteUser 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-283">DeleteUser function</span></span>
- <span data-ttu-id="0c20b-284">EnablePasswordReset 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="0c20b-285">EnablePasswordRetrieval 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="0c20b-286">FindUsersByEmail 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="0c20b-287">FindUsersByName 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-287">FindUsersByName function</span></span>
- <span data-ttu-id="0c20b-288">GetAllUsers 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-288">GetAllUsers function</span></span>
- <span data-ttu-id="0c20b-289">GetNumberOfUsersOnline 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="0c20b-290">GetPassword 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-290">GetPassword function</span></span>
- <span data-ttu-id="0c20b-291">GetUser 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-291">GetUser function</span></span>
- <span data-ttu-id="0c20b-292">GetUserNameByEmail 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="0c20b-293">MaxInvalidPasswordAttempts 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="0c20b-294">MinRequiredNonAlphanumericCharacters 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="0c20b-295">MinRequiredPasswordLength 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="0c20b-296">PasswordAttemptWindow 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="0c20b-297">PasswordFormat 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-297">PasswordFormat property</span></span>
- <span data-ttu-id="0c20b-298">PasswordStrengthRegularExpression 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="0c20b-299">RequiresQuestionAndAnswer 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="0c20b-300">RequiresUniqueEmail 属性</span><span class="sxs-lookup"><span data-stu-id="0c20b-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="0c20b-301">ResetPassword 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-301">ResetPassword function</span></span>
- <span data-ttu-id="0c20b-302">解锁用户函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-302">Unlock user function</span></span>
- <span data-ttu-id="0c20b-303">UpdateUser 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-303">UpdateUser function</span></span>
- <span data-ttu-id="0c20b-304">ValidateUser 函数</span><span class="sxs-lookup"><span data-stu-id="0c20b-304">ValidateUser function</span></span>

<span data-ttu-id="0c20b-305">这是要作为 C# 开发人员实现相当多的列表。</span><span class="sxs-lookup"><span data-stu-id="0c20b-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="0c20b-306">你可能会发现更轻松地在 VB.NET 中创建类，而无需任何实现，然后使用.NET 反射器或类似的工具将代码转换为 C#。</span><span class="sxs-lookup"><span data-stu-id="0c20b-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="0c20b-307">连接字符串和其他属性应设置为各自的 Initialize 方法中的默认值。</span><span class="sxs-lookup"><span data-stu-id="0c20b-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="0c20b-308">（Initialize 方法时激发的提供程序是在运行时加载。）Initialize 方法的第二个参数是类型 System.Collections.Specialized.NameValueCollection 并且是指&lt;添加&gt;web.config 文件中的自定义提供程序与关联的元素。</span><span class="sxs-lookup"><span data-stu-id="0c20b-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="0c20b-309">该条目如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c20b-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="0c20b-310">下面是初始化方法的示例。</span><span class="sxs-lookup"><span data-stu-id="0c20b-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="0c20b-311">若要验证用户在提交登录窗体时，你将需要使用 ValidateUser 方法。</span><span class="sxs-lookup"><span data-stu-id="0c20b-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="0c20b-312">当用户单击 Login 控件中的登录按钮，将引发此方法。</span><span class="sxs-lookup"><span data-stu-id="0c20b-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="0c20b-313">请将你执行此方法中的用户查找的代码。</span><span class="sxs-lookup"><span data-stu-id="0c20b-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="0c20b-314">如你所见，编写您自己的成员资格提供程序并不困难，并允许你将扩展此功能强大的功能的 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="0c20b-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>
