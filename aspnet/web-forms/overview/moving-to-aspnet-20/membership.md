---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成员身份 |Microsoft Docs
author: microsoft
description: ASP.NET 成员身份基于窗体身份验证模型是否成功从 ASP.NET 1.x。 ASP.NET 窗体身份验证提供了方便的方式，以 incorp...
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: f776ed628e206c06543589767ba364af3c76ae16
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818212"
---
<a name="membership"></a><span data-ttu-id="d9d4e-104">成员资格</span><span class="sxs-lookup"><span data-stu-id="d9d4e-104">Membership</span></span>
====================
<span data-ttu-id="d9d4e-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d9d4e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d9d4e-106">ASP.NET 成员身份基于窗体身份验证模型是否成功从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="d9d4e-107">ASP.NET 窗体身份验证提供了方便地将一个登录窗体合并到 ASP.NET 应用程序和对针对数据库或其他数据存储区的用户进行验证。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>


<span data-ttu-id="d9d4e-108">ASP.NET 成员身份基于窗体身份验证模型是否成功从 ASP.NET 1.x。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="d9d4e-109">ASP.NET 窗体身份验证提供了方便地将一个登录窗体合并到 ASP.NET 应用程序和对针对数据库或其他数据存储区的用户进行验证。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="d9d4e-110">FormsAuthentication 类的成员，使其可以处理身份验证的 cookie，检查有效的登录名，登录将用户注销等。但是，在 ASP.NET 1.x 应用程序中实现窗体身份验证可能需要大量的代码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="d9d4e-111">在 ASP.NET 2.0 中的成员身份是通过使用单独的窗体身份验证的主要优势。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="d9d4e-112">（成员身份是最可靠与窗体身份验证结合使用时，但使用 Forms 身份验证并不要求）。正如您很快就会看到，您可以使用 ASP.NET Membership 和 login 控件在 ASP.NET 2.0 中根本无需太多的代码实现功能强大的成员身份系统。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="d9d4e-113">在 ASP.NET 2.0 中实现的成员身份</span><span class="sxs-lookup"><span data-stu-id="d9d4e-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="d9d4e-114">由以下四个步骤实现的成员身份。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="d9d4e-115">请记住，有许多子步骤也可以实现的可选配置以及所涉及的。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="d9d4e-116">这些步骤是为了说明配置成员身份的大图片。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="d9d4e-117">创建成员资格数据库 （如果 SQL Server 用作成员资格存储区。）</span><span class="sxs-lookup"><span data-stu-id="d9d4e-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="d9d4e-118">在应用程序配置文件中指定的成员身份选项。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="d9d4e-119">（成员身份已启用默认情况下。）</span><span class="sxs-lookup"><span data-stu-id="d9d4e-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="d9d4e-120">确定你想要使用的成员身份存储的类型。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="d9d4e-121">选项包括：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-121">Options are:</span></span> 

    - <span data-ttu-id="d9d4e-122">Microsoft SQL Server （版本 7.0 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="d9d4e-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="d9d4e-123">Active Directory 存储</span><span class="sxs-lookup"><span data-stu-id="d9d4e-123">Active Directory Store</span></span>
    - <span data-ttu-id="d9d4e-124">自定义成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="d9d4e-124">Custom membership provider</span></span>
4. <span data-ttu-id="d9d4e-125">配置 ASP.NET 窗体身份验证的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="d9d4e-126">再次重申，成员资格旨在利用的窗体身份验证，但使用 Forms 身份验证不是一项要求。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="d9d4e-127">定义成员资格的用户帐户并根据需要配置角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="d9d4e-128">创建成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="d9d4e-128">Creating the Membership Database</span></span>

<span data-ttu-id="d9d4e-129">如果您正在使用 SQL Server 7.0 或更高版本作为成员身份存储，可以使用 aspnet\_regsql 实用程序 （可非常轻松地从 Visual Studio.NET 2005年命令提示符） 将数据库配置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-129">If youre using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="d9d4e-130">Aspnet\_regsql 实用程序可以在命令提示符工具或通过 GUI 向导。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="d9d4e-131">向导方法是将数据库配置的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="d9d4e-132">若要访问该向导，只需运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="d9d4e-133">一旦运行该命令时，还能使用 ASP.NET SQL Server 安装向导，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>


![](membership/_static/image1.jpg)

<span data-ttu-id="d9d4e-134">**图 1**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-134">**Figure 1**</span></span>


<span data-ttu-id="d9d4e-135">ASP.NET SQL Server 安装向导在向导中指定的实例中创建该网站。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="d9d4e-136">但是，ASP.NET 将使用连接字符串在 machine.config 文件中连接到你的数据库。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="d9d4e-137">默认情况下，此连接字符串将指向的 SQL Server 2005 实例，因此如果使用的 SQL Server 2000 或 SQL Server 7.0 实例，您将需要修改 machine.config 文件中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="d9d4e-138">此处可以找到该连接字符串：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="d9d4e-139">遗憾的是，如果你无需修改连接字符串，ASP.NET 将不为您提供描述性错误。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-139">Unfortunately, if you dont modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="d9d4e-140">它只需将继续抱怨说尚未创建数据库。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-140">It will just continue to complain saying that you havent created the database.</span></span> <span data-ttu-id="d9d4e-141">在上面的示例中，我已修改为指向我的本地 SQL Server 2000 实例的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="d9d4e-142">指定配置和添加用户和角色</span><span class="sxs-lookup"><span data-stu-id="d9d4e-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="d9d4e-143">配置成员身份的下一步是将所需的信息添加到应用程序的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="d9d4e-144">在 ASP.NET 1.x 中，修改 web.config 文件是有时很难由于 lowerCamelCase 使用和缺少的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="d9d4e-145">Visual Studio.NET 2005年使任务更容易通过 Intellisense 配置文件，但 ASP.NET 2.0 更进一步通过编辑配置文件的提供的 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="d9d4e-146">可以通过单击在解决方案资源管理器工具栏上，如下所示的 ASP.NET 配置按钮来启动 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="d9d4e-147">此外可以启动的登录名控件插入时，将显示弹出式窗口通过 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>


![](membership/_static/image2.jpg)

<span data-ttu-id="d9d4e-148">**图 2**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-148">**Figure 2**</span></span>


<span data-ttu-id="d9d4e-149">这将启动 ASP.NET 网站管理工具如下所示。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="d9d4e-150">ASP.NET 网站管理是一个四个选项卡界面，它可以更轻松地管理应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="d9d4e-151">提供了以下选项卡：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-151">The following tabs are available:</span></span>

- <span data-ttu-id="d9d4e-152">**主文件夹**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-152">**Home**</span></span>
- <span data-ttu-id="d9d4e-153">**安全**配置用户、 角色和访问权限。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="d9d4e-154">**应用程序**配置应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="d9d4e-155">**提供程序**配置和测试应用程序成员资格提供程序。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="d9d4e-156">网站管理工具，可以轻松地创建新用户，创建新的角色，以及管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="d9d4e-157">在 Windows 界面中不提供此功能。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="d9d4e-158">Windows 界面允许您可以轻松地定义授权设置要添加、 删除和管理提供程序，无法在网站管理工具中的功能。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="d9d4e-159">若要启动 Windows 界面，打开 Internet Information Services 管理单元、 应用程序中，右键单击并选择属性。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="d9d4e-160">单击 ASP.NET 选项卡，然后单击编辑配置按钮。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="d9d4e-161">（若要启用编辑配置按钮的 ASP.NET 2.0 下必须运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="d9d4e-162">你可以配置 ASP.NET 版本在 ASP.NET 对话框。）如下所示，将显示 ASP.NET 配置设置对话框。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>


![](membership/_static/image3.jpg)

<span data-ttu-id="d9d4e-163">**图 3**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-163">**Figure 3**</span></span>


<span data-ttu-id="d9d4e-164">在常规选项卡上列出连接字符串和应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="d9d4e-165">在父配置文件 （machine.config 或更高级别的 web.config） 中定义以斜体显示的任何设置，不以斜体显示的设置是从应用程序配置文件。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="d9d4e-166">如果添加一个设置，已删除或编辑应用程序级别中，ASP.NET 将添加、 删除或修改在应用程序级别 web.config 而不是从它继承的配置文件中删除该设置的设置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="d9d4e-167">身份验证选项卡如下所示。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="d9d4e-168">这是在将配置你的成员身份设置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="d9d4e-169">窗体身份验证设置，成员资格提供程序，并在此处配置角色提供程序。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>


![](membership/_static/image4.jpg)

<span data-ttu-id="d9d4e-170">**图 4**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-170">**Figure 4**</span></span>


## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="d9d4e-171">在你的应用程序中实现的成员身份</span><span class="sxs-lookup"><span data-stu-id="d9d4e-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="d9d4e-172">在你的应用程序中实现 ASP.NET 2.0 成员身份的最简单方法是使用提供的登录控件。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="d9d4e-173">此方法可以实现 ASP.NET 2.0 成员身份的基础知识，而无需编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="d9d4e-174">以下的登录控件是 ASP.NET 2.0 中提供：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="d9d4e-175">Login 控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-175">Login Control</span></span>

<span data-ttu-id="d9d4e-176">Login 控件提供一个接口，使用户能够登录到成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="d9d4e-177">你提供用户名和密码 textboxt 和登录按钮。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-177">It provides you with a username and password textboxt and a login button.</span></span> <span data-ttu-id="d9d4e-178">许多其他常见功能，如将其注册为那些尚未做这样一个复选框，允许在后续的访问会自动登录到用户的用户的链接、 密码提示等的链接。登录名控件的所有功能都都可自定义通过控件的属性。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="d9d4e-179">在 ASP.NET 1.x 中，开发人员必须编写大量的代码以使用窗体身份验证时执行搜索。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="d9d4e-180">ASP.NET 2.0 成员身份，你可以对用户进行验证而无需编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="d9d4e-181">ASP.NET 会自动为您执行用户执行的查找。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="d9d4e-182">(如果不使用 ASP.NET 成员资格将登录控件，则可以使用**OnAuthenticate**方法来验证用户。)</span><span class="sxs-lookup"><span data-stu-id="d9d4e-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="d9d4e-183">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-183">LoginView Control</span></span>

<span data-ttu-id="d9d4e-184">LoginView 控件是默认情况下; 提供两个模板的模板化控件AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="d9d4e-185">用户登录到成员资格系统确定将显示该模板。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="d9d4e-186">此控件通常用于显示登录控件时，用户尚未登录，LoginStatus 控件和/或其他登录控件，当用户已登录。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="d9d4e-187">如果在 ASP.NET 应用程序中使用角色管理，LoginView 控件可显示特定的模板基于用户角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="d9d4e-188">（更多关于 ASP.NET 角色管理将在后面。）</span><span class="sxs-lookup"><span data-stu-id="d9d4e-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="d9d4e-189">PasswordRecovery 控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-189">PasswordRecovery Control</span></span>

<span data-ttu-id="d9d4e-190">PasswordRecovery 控件允许用户收到电子邮件，其当前密码或重置其密码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="d9d4e-191">明文和加密的密码可以恢复并通过电子邮件发送给用户。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="d9d4e-192">如果密码哈希处理，它不能恢复。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="d9d4e-193">而是用户将需要执行密码重置。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="d9d4e-194">登录状态控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-194">LoginStatus Control</span></span>

<span data-ttu-id="d9d4e-195">LoginStatus 控件用于显示当前登录的用户未登录的用户的登录名指示器和注销指示器。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="d9d4e-196">Request.IsAuthenticated 属性用于确定要显示的指示器。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="d9d4e-197">LoginStatus 控件显示的指示器可以是文本 (通过实现**LoginText**并**LogoutText**属性) 或图像 (通过实现**LoginImageUrl**并**LogoutImageUrl**属性。)</span><span class="sxs-lookup"><span data-stu-id="d9d4e-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="d9d4e-198">当用户注销通过 LoginStatus 控件时，他或她将重定向到指定的 URL **LogoutPageUrl**属性。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="d9d4e-199">如果未设置该属性，会刷新当前页。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="d9d4e-200">站点可能受窗体身份验证，因为当前页的刷新将用户重定向到该站点的登录页。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="d9d4e-201">登录名控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-201">LoginName Control</span></span>

<span data-ttu-id="d9d4e-202">LoginName 控件显示当前已登录到该站点的用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="d9d4e-203">CreateUserWizard 控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-203">CreateUserWizard Control</span></span>

<span data-ttu-id="d9d4e-204">CreateUserWizard 控件为用户提供注册成员身份系统的简便方法。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="d9d4e-205">你可以通过如下所示的接口添加步骤 （实现为一系列 WizardSteps）。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>


![](membership/_static/image5.jpg)

<span data-ttu-id="d9d4e-206">**图 5**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-206">**Figure 5**</span></span>


<span data-ttu-id="d9d4e-207">CreateUserWizard 是模板化控件，用于从向导类派生并提供以下模板：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="d9d4e-208">**HeaderTemplate**此模板控制向导的标头的外观。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="d9d4e-209">**SidebarTemplate**此模板控制向导边栏的外观。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="d9d4e-210">**StartNavigationTemplate**导航的外观是在开始步骤向导的此模板控件。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="d9d4e-211">**StepNavigationTemplate**此模板控制在不启动或完成步骤时的导航区域的外观。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="d9d4e-212">**FinishNavigationTemplate**此模板控制时在完成步骤的导航区域的外观。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="d9d4e-213">此外，对于每个添加到向导的步骤，ASP.NET 将创建包含 ContentTemplate 和为该步骤 CustomNavigationTemplate 的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="d9d4e-214">自定义 CreateUserWizard 的完整详细信息，请参阅 VS.NET 2005 文档：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="d9d4e-215">ChangePassword 控件</span><span class="sxs-lookup"><span data-stu-id="d9d4e-215">ChangePassword Control</span></span>

<span data-ttu-id="d9d4e-216">ChangePassword 控件允许用户更改其密码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="d9d4e-217">如果 DisplayUserName 属性为 true （它是默认值为 false），用户可以更改其密码时不将它们记录。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="d9d4e-218">如果用户*是*已登录和 DisplayUserName 属性为 true，用户将能够更改不记录在提供他们知道该用户的用户 ID 的另一个用户的密码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="d9d4e-219">请记住，如果你希望用户能够更改密码，而无需登录，你将需要确保 ChangePassword 控件显示在其的页面允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="d9d4e-220">显然，用户将必须提供旧密码，以更改其密码。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="d9d4e-221">角色管理</span><span class="sxs-lookup"><span data-stu-id="d9d4e-221">Role Management</span></span>

<span data-ttu-id="d9d4e-222">角色管理，可将用户分配到特定角色，然后限制对某些文件或文件夹基于该角色的访问。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="d9d4e-223">角色管理还提供了一个 API，以便可以以编程方式确定，方便用户角色或确定特定角色中的所有用户并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="d9d4e-224">角色管理不是在 ASP.NET 成员资格要求也不是为了使用角色管理要求的成员身份。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="d9d4e-225">但是，这两个很好地补充彼此并很可能，开发人员会使用它们与相互结合使用。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="d9d4e-226">若要启用应用程序中的角色管理，请在 web.config 文件中进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="d9d4e-227">当**cacheRolesInCookie**属性设置为 true，ASP.NET 缓存客户端的 cookie 中的用户角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="d9d4e-228">这允许角色查找，以调入 RoleProvider 的情况下发生。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="d9d4e-229">使用此属性时，建议，请确保开发人员将**cookieProtection**属性设置为 All。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="d9d4e-230">（这是默认设置。）这可确保 cookie 数据进行加密，并有助于确保 cookie 内容尚未更改。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents havent been altered.</span></span> <span data-ttu-id="d9d4e-231">可以使用网站管理工具添加角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="d9d4e-232">它允许您轻松地定义角色、 配置的访问权限的基于这些角色的站点部分并将用户分配到角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>


![](membership/_static/image6.jpg)

<span data-ttu-id="d9d4e-233">**图 6**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-233">**Figure 6**</span></span>


<span data-ttu-id="d9d4e-234">如上所示，可以通过只需输入角色的名称，然后单击添加角色添加新的角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="d9d4e-235">可以管理或通过单击相应的链接的现有角色列表中删除现有角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="d9d4e-236">当你管理角色时，可以添加或删除用户，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-236">When you manage a role, you can add or remove users as shown below.</span></span>


![](membership/_static/image7.jpg)

<span data-ttu-id="d9d4e-237">**图 7**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-237">**Figure 7**</span></span>


<span data-ttu-id="d9d4e-238">通过检查用户属于角色复选框，可以轻松地将用户添加到特定角色中。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="d9d4e-239">使用适当的项，ASP.NET 将自动更新成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="d9d4e-240">此外需要配置你的应用程序的访问规则。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="d9d4e-241">ASP.NET 1.x 开发人员都熟悉通过这样做&lt;授权&gt;web.config 文件中，该选项中的元素是在 ASP.NET 2.0 中仍然可用。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="d9d4e-242">但是，轻松地管理访问权限的规则使用网站管理工具如图所示下面。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>


![](membership/_static/image8.jpg)

<span data-ttu-id="d9d4e-243">**图 8**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-243">**Figure 8**</span></span>


<span data-ttu-id="d9d4e-244">在这种情况下，突出显示管理文件夹 （将很难看到，因为该工具使其突出显示以浅灰色） 以及管理员角色是否已授予访问权限。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="d9d4e-245">将拒绝所有其他用户。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-245">All other users are denied.</span></span> <span data-ttu-id="d9d4e-246">您可以单击头图标以选择一个规则，然后使用上移和下移按钮来排列规则。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="d9d4e-247">与 ASP.NET 一样&lt;授权&gt;元素，它们出现的顺序处理规则。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="d9d4e-248">换而言之，如果上面截图中的规则的顺序已反转，没有人将可以访问对管理文件夹因为 ASP.NET 将会遇到的第一个规则将会拒绝所有人的文件夹的规则。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="d9d4e-249">ASP.NET 2.0 将 web.config 文件添加到要为其指定访问规则的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="d9d4e-250">访问规则可以通过配置文件或通过网站管理工具进行编辑。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="d9d4e-251">换而言之，网站管理工具是只需通过它可以在用户友好的环境中编辑配置文件的接口。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="d9d4e-252">在代码中使用角色</span><span class="sxs-lookup"><span data-stu-id="d9d4e-252">Using Roles in Code</span></span>

<span data-ttu-id="d9d4e-253">用于角色管理 API 一直没有更改版本 1.x。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="d9d4e-254">**IsInRole**方法用于确定用户是否属于特定角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="d9d4e-255">ASP.NET 还为当前上下文的成员创建 RolePrincipal 实例。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="d9d4e-256">RolePrincipal 对象可用于获取所有给用户，如下所示所属的角色：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="d9d4e-257">用 LoginView 控件使用 RoleGroups</span><span class="sxs-lookup"><span data-stu-id="d9d4e-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="d9d4e-258">现在，已了解角色管理和成员身份，让我们如何 LoginView 控件利用此功能在 ASP.NET 2.0 中简要讨论一下。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="d9d4e-259">如前面所述，LoginView 控件是默认设置。 包含两个模板的模板化控件AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="d9d4e-260">在 LoginView 任务对话框是一个链接 （如下所示），您可以编辑 RoleGroups。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>


![](membership/_static/image9.jpg)

<span data-ttu-id="d9d4e-261">**图 9**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-261">**Figure 9**</span></span>


<span data-ttu-id="d9d4e-262">每个 RoleGroup 对象包含一个字符串数组，用于定义 RoleGroup 适用于哪些角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="d9d4e-263">若要添加新 RoleGroup LoginView 控件，单击编辑 RoleGroups 链接。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="d9d4e-264">在上图中，可以看到我已添加了新 RoleGroup 为管理员。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="d9d4e-265">通过选择该 RoleGroup （RoleGroup[0]) 从视图下拉列表中，我可以将模板配置的管理员角色的成员才会显示。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="d9d4e-266">在下图中，我添加了适用于 Sales 角色和分发角色的成员的新 RoleGroup。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="d9d4e-267">这会向登录视图任务对话框中的视图下拉列表中添加第二个 RoleGroup 而不显示任何内容添加到该模板中的销售或分发的任何用户角色。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>


![](membership/_static/image10.jpg)

<span data-ttu-id="d9d4e-268">**图 10**</span><span class="sxs-lookup"><span data-stu-id="d9d4e-268">**Figure 10**</span></span>


## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="d9d4e-269">重写现有成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="d9d4e-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="d9d4e-270">有两种方法可以扩展的 ASP.NET 成员资格功能。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="d9d4e-271">首先，您可以通过从它继承和重写其方法显然更改 SqlMembershipProvider 类的现有功能。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="d9d4e-272">例如，如果你想要实现您自己的功能创建用户时，可以创建自己的类继承自 SqlMembershipProvider，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="d9d4e-273">如果，但是，你想要创建自己的提供程序 （用于存储成员资格信息在访问数据库中，例如所示），可以创建自己的提供程序。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="d9d4e-274">创建你自己的成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="d9d4e-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="d9d4e-275">若要创建你自己的成员资格提供程序，首先需要创建一个继承自 MembershipProvider 类的类。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="d9d4e-276">如果正在使用 VB.NET，Visual Studio 2005 将添加所有需要重写的方法存根。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="d9d4e-277">如果使用的 C#，则取决于您要添加存根 （stub）。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="d9d4e-278">你将需要重写以下：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-278">You will need to override the following:</span></span>

- <span data-ttu-id="d9d4e-279">应用程序名称属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-279">ApplicationName property</span></span>
- <span data-ttu-id="d9d4e-280">ChangePassword 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-280">ChangePassword function</span></span>
- <span data-ttu-id="d9d4e-281">ChangePasswordQuestionAndAnswer 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="d9d4e-282">CreateUser 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-282">CreateUser function</span></span>
- <span data-ttu-id="d9d4e-283">DeleteUser 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-283">DeleteUser function</span></span>
- <span data-ttu-id="d9d4e-284">EnablePasswordReset 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="d9d4e-285">EnablePasswordRetrieval 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="d9d4e-286">FindUsersByEmail 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="d9d4e-287">FindUsersByName 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-287">FindUsersByName function</span></span>
- <span data-ttu-id="d9d4e-288">GetAllUsers 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-288">GetAllUsers function</span></span>
- <span data-ttu-id="d9d4e-289">GetNumberOfUsersOnline 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="d9d4e-290">GetPassword 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-290">GetPassword function</span></span>
- <span data-ttu-id="d9d4e-291">GetUser 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-291">GetUser function</span></span>
- <span data-ttu-id="d9d4e-292">GetUserNameByEmail 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="d9d4e-293">MaxInvalidPasswordAttempts 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="d9d4e-294">MinRequiredNonAlphanumericCharacters 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="d9d4e-295">MinRequiredPasswordLength 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="d9d4e-296">PasswordAttemptWindow 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="d9d4e-297">PasswordFormat 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-297">PasswordFormat property</span></span>
- <span data-ttu-id="d9d4e-298">PasswordStrengthRegularExpression 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="d9d4e-299">RequiresQuestionAndAnswer 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="d9d4e-300">RequiresUniqueEmail 属性</span><span class="sxs-lookup"><span data-stu-id="d9d4e-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="d9d4e-301">ResetPassword 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-301">ResetPassword function</span></span>
- <span data-ttu-id="d9d4e-302">解锁用户函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-302">Unlock user function</span></span>
- <span data-ttu-id="d9d4e-303">UpdateUser 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-303">UpdateUser function</span></span>
- <span data-ttu-id="d9d4e-304">ValidateUser 函数</span><span class="sxs-lookup"><span data-stu-id="d9d4e-304">ValidateUser function</span></span>

<span data-ttu-id="d9d4e-305">这会很多列表作为 C# 开发人员来实现。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="d9d4e-306">您可能会发现更轻松地在 VB.NET 中创建类，而无需任何实现，然后使用.NET Reflector 或类似的工具将代码转换为 C#。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="d9d4e-307">连接字符串和其他属性应设置为它们的 Initialize 方法中的默认值。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="d9d4e-308">（Initialize 方法时触发的提供程序是在运行时加载。）Initialize 方法的第二个参数的类型 System.Collections.Specialized.NameValueCollection 和是对的引用&lt;添加&gt;与您的 web.config 文件中的自定义提供程序相关联的元素。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="d9d4e-309">该条目如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9d4e-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="d9d4e-310">下面是 Initialize 方法的示例。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="d9d4e-311">若要验证用户在提交登录窗体时，你将需要使用 ValidateUser 方法。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="d9d4e-312">当用户单击登录控件中的登录按钮时，会触发此方法。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="d9d4e-313">会将你的代码执行此方法中的用户查找。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="d9d4e-314">如您所见，编写你自己的成员资格提供程序并不困难，并可以扩展此强大的功能的 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="d9d4e-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>
