---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第 7 部分： 成员身份和授权 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 7 部分介绍了成员身份和授权。
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/13/2010
ms.topic: article
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: 41b17315cbe1f6d93001a736bc24bf003df24061
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393165"
---
<a name="part-7-membership-and-authorization"></a><span data-ttu-id="32a81-104">第 7 部分： 成员身份和授权</span><span class="sxs-lookup"><span data-stu-id="32a81-104">Part 7: Membership and Authorization</span></span>
====================
<span data-ttu-id="32a81-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="32a81-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="32a81-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="32a81-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="32a81-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="32a81-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="32a81-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="32a81-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="32a81-109">第 7 部分介绍了成员身份和授权。</span><span class="sxs-lookup"><span data-stu-id="32a81-109">Part 7 covers Membership and Authorization.</span></span>


<span data-ttu-id="32a81-110">Store Manager 控制器是当前访问我们的站点的任何人都可访问。</span><span class="sxs-lookup"><span data-stu-id="32a81-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="32a81-111">让我们更改此设置以限制对网站管理员的权限。</span><span class="sxs-lookup"><span data-stu-id="32a81-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="32a81-112">添加 AccountController 和视图</span><span class="sxs-lookup"><span data-stu-id="32a81-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="32a81-113">完整的 ASP.NET MVC 3 Web 应用程序模板和 ASP.NET MVC 3 空 Web 应用程序模板之间的一个区别是空的模板不包括帐户控制器。</span><span class="sxs-lookup"><span data-stu-id="32a81-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="32a81-114">我们将通过复制几个文件从完整的 ASP.NET MVC 3 Web 应用程序模板创建新的 ASP.NET MVC 应用程序来添加帐户控制器。</span><span class="sxs-lookup"><span data-stu-id="32a81-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="32a81-115">创建新的 ASP.NET MVC 应用程序使用完整的 ASP.NET MVC 3 Web 应用程序模板并将以下文件复制到项目中的同一个目录：</span><span class="sxs-lookup"><span data-stu-id="32a81-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="32a81-116">在 Controllers 目录中复制 AccountController.cs</span><span class="sxs-lookup"><span data-stu-id="32a81-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="32a81-117">在 Models 目录中复制 AccountModels</span><span class="sxs-lookup"><span data-stu-id="32a81-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="32a81-118">创建 Views 目录帐户目录并复制中的所有四个视图</span><span class="sxs-lookup"><span data-stu-id="32a81-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="32a81-119">更改控制器和模型类的命名空间，以便它们开头 MvcMusicStore。</span><span class="sxs-lookup"><span data-stu-id="32a81-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="32a81-120">AccountController 类应使用 MvcMusicStore.Controllers 命名空间，并且 AccountModels 类应使用 MvcMusicStore.Models 命名空间。</span><span class="sxs-lookup"><span data-stu-id="32a81-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="32a81-121">*注意： 这些文件也是从中我们复制站点设计文件在本教程开始 MvcMusicStore Assets.zip 下载中提供的。成员资格文件位于代码目录中。*</span><span class="sxs-lookup"><span data-stu-id="32a81-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="32a81-122">更新后的解决方案应如以下所示：</span><span class="sxs-lookup"><span data-stu-id="32a81-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="32a81-123">添加了管理用户与 ASP.NET 配置网站</span><span class="sxs-lookup"><span data-stu-id="32a81-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="32a81-124">我们要求在我们的网站授权之前，我们将需要创建具有访问权限的用户。</span><span class="sxs-lookup"><span data-stu-id="32a81-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="32a81-125">若要创建的用户的最简单方法是使用内置的 ASP.NET 配置网站。</span><span class="sxs-lookup"><span data-stu-id="32a81-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="32a81-126">通过单击以下解决方案资源管理器中的图标启动 ASP.NET 配置网站。</span><span class="sxs-lookup"><span data-stu-id="32a81-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="32a81-127">这将启动配置网站。</span><span class="sxs-lookup"><span data-stu-id="32a81-127">This launches a configuration website.</span></span> <span data-ttu-id="32a81-128">单击主屏幕上的安全选项卡，然后单击"启用角色"中的链接，在屏幕的中心。</span><span class="sxs-lookup"><span data-stu-id="32a81-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="32a81-129">单击"创建或管理角色"链接。</span><span class="sxs-lookup"><span data-stu-id="32a81-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="32a81-130">输入"管理员"角色名称，然后按添加角色按钮。</span><span class="sxs-lookup"><span data-stu-id="32a81-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="32a81-131">单击后退按钮，然后单击左侧和右侧的创建用户链接。</span><span class="sxs-lookup"><span data-stu-id="32a81-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="32a81-132">填写用户信息字段在左侧使用以下信息：</span><span class="sxs-lookup"><span data-stu-id="32a81-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="32a81-133">**字段**</span><span class="sxs-lookup"><span data-stu-id="32a81-133">**Field**</span></span> | <span data-ttu-id="32a81-134">**值**</span><span class="sxs-lookup"><span data-stu-id="32a81-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="32a81-135">**用户名**</span><span class="sxs-lookup"><span data-stu-id="32a81-135">**User Name**</span></span> | <span data-ttu-id="32a81-136">管理员</span><span class="sxs-lookup"><span data-stu-id="32a81-136">Administrator</span></span> |
| <span data-ttu-id="32a81-137">**密码**</span><span class="sxs-lookup"><span data-stu-id="32a81-137">**Password**</span></span> | <span data-ttu-id="32a81-138">password123 ！</span><span class="sxs-lookup"><span data-stu-id="32a81-138">password123!</span></span> |
| <span data-ttu-id="32a81-139">**确认密码**</span><span class="sxs-lookup"><span data-stu-id="32a81-139">**Confirm Password**</span></span> | <span data-ttu-id="32a81-140">password123 ！</span><span class="sxs-lookup"><span data-stu-id="32a81-140">password123!</span></span> |
| <span data-ttu-id="32a81-141">**电子邮件**</span><span class="sxs-lookup"><span data-stu-id="32a81-141">**E-mail**</span></span> | <span data-ttu-id="32a81-142">（也适用任何电子邮件地址）</span><span class="sxs-lookup"><span data-stu-id="32a81-142">(any email address will work)</span></span> |
| <span data-ttu-id="32a81-143">**安全提示问题**</span><span class="sxs-lookup"><span data-stu-id="32a81-143">**Security Question**</span></span> | <span data-ttu-id="32a81-144">（任意）</span><span class="sxs-lookup"><span data-stu-id="32a81-144">(whatever you like)</span></span> |
| <span data-ttu-id="32a81-145">**安全提示问题的答案**</span><span class="sxs-lookup"><span data-stu-id="32a81-145">**Security Answer**</span></span> | <span data-ttu-id="32a81-146">（任意）</span><span class="sxs-lookup"><span data-stu-id="32a81-146">(whatever you like)</span></span> |

<span data-ttu-id="32a81-147">*注意： 当然可以使用您希望的任何密码。默认密码安全设置需要 7 个字符长，并且包含一个非字母数字字符的密码。*</span><span class="sxs-lookup"><span data-stu-id="32a81-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="32a81-148">选择此用户的管理员角色，然后单击创建用户按钮。</span><span class="sxs-lookup"><span data-stu-id="32a81-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="32a81-149">此时，应看到一条消息指出已成功创建用户。</span><span class="sxs-lookup"><span data-stu-id="32a81-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="32a81-150">现在可以关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="32a81-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="32a81-151">基于角色的授权</span><span class="sxs-lookup"><span data-stu-id="32a81-151">Role-based Authorization</span></span>

<span data-ttu-id="32a81-152">现在我们可以使用 [Authorize] 特性，指定用户必须管理员角色才能访问类中的任何控制器操作 StoreManagerController 限制访问。</span><span class="sxs-lookup"><span data-stu-id="32a81-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="32a81-153">*注意： 可以放置 [Authorize] 特性，以及在控制器类级别上的特定操作方法。*</span><span class="sxs-lookup"><span data-stu-id="32a81-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="32a81-154">现在浏览到 /StoreManager 会出现一个登录对话框：</span><span class="sxs-lookup"><span data-stu-id="32a81-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="32a81-155">登录后使用这个新的管理员帐户，我们可以转到唱片集编辑屏幕之前。</span><span class="sxs-lookup"><span data-stu-id="32a81-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32a81-156">[上一页](mvc-music-store-part-6.md)
> [下一页](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="32a81-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
