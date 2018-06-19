---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 成员资格和管理 |Microsoft 文档
author: Erikre
description: 本系列教程将教您生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/08/2014
ms.topic: article
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: 166bc642ea2083f455be0648e424f0b0ae3b082c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/10/2018
ms.locfileid: "30889626"
---
<a name="membership-and-administration"></a><span data-ttu-id="eae12-103">成员资格和管理</span><span class="sxs-lookup"><span data-stu-id="eae12-103">Membership and Administration</span></span>
====================
<span data-ttu-id="eae12-104">通过[艾力克 Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="eae12-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="eae12-105">[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="eae12-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="eae12-106">本系列教程将教您构建使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="eae12-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="eae12-107">Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)是可以附带本系列教程。</span><span class="sxs-lookup"><span data-stu-id="eae12-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>


<span data-ttu-id="eae12-108">本教程演示了如何更新 Wingtip Toys 示例应用程序来添加自定义角色并使用 ASP.NET 标识。</span><span class="sxs-lookup"><span data-stu-id="eae12-108">This tutorial shows you how to update the Wingtip Toys sample application to add a custom role and use ASP.NET Identity.</span></span> <span data-ttu-id="eae12-109">它还演示如何实现自定义角色的用户可以从中添加和删除从网站的产品的管理页。</span><span class="sxs-lookup"><span data-stu-id="eae12-109">It also shows you how to implement an administration page from which the user with a custom role can add and remove products from the website.</span></span>

<span data-ttu-id="eae12-110">[ASP.NET 标识](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)是用于生成 ASP.NET web 应用程序的成员身份系统，可以在 ASP.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="eae12-110">[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) is the membership system used to build ASP.NET web application and is available in ASP.NET 4.5.</span></span> <span data-ttu-id="eae12-111">在 Visual Studio 2013 Web 窗体项目模板，以及的模板使用 ASP.NET 标识[ASP.NET MVC](../../../../mvc/index.md)， [ASP.NET Web API](../../../../web-api/index.md)，和[ASP.NET 单页面应用程序](../../../../single-page-application/index.md).</span><span class="sxs-lookup"><span data-stu-id="eae12-111">ASP.NET Identity is used in the Visual Studio 2013 Web Forms project template, as well as the templates for [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web API](../../../../web-api/index.md), and [ASP.NET Single Page Application](../../../../single-page-application/index.md).</span></span> <span data-ttu-id="eae12-112">你还可以安装使用 NuGet，当你开始与空 Web 应用程序的 ASP.NET 标识系统。</span><span class="sxs-lookup"><span data-stu-id="eae12-112">You can also specifically install the ASP.NET Identity system using NuGet when you start with an empty Web application.</span></span> <span data-ttu-id="eae12-113">但是，在本教程系列你使用**Web 窗体**projecttemplate，包括 ASP.NET 标识系统。</span><span class="sxs-lookup"><span data-stu-id="eae12-113">However, in this tutorial series you use the **Web Forms**projecttemplate, which includes the ASP.NET Identity system.</span></span> <span data-ttu-id="eae12-114">ASP.NET 标识容易地将特定于用户的配置文件的数据集成与应用程序数据。</span><span class="sxs-lookup"><span data-stu-id="eae12-114">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="eae12-115">此外，ASP.NET 标识，可选择你的应用程序中的用户配置文件的持久性模型。</span><span class="sxs-lookup"><span data-stu-id="eae12-115">Also, ASP.NET Identity allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="eae12-116">你可以将数据存储在 SQL Server 数据库或其他数据存储，包括*NoSQL*数据存储 Windows Azure 存储表等。</span><span class="sxs-lookup"><span data-stu-id="eae12-116">You can store the data in a SQL Server database or another data store, including *NoSQL* data stores such as Windows Azure Storage Tables.</span></span>

<span data-ttu-id="eae12-117">本教程以前一教程 Wingtip Toys 教程系列中标题为"签出和付款与 PayPal"上。</span><span class="sxs-lookup"><span data-stu-id="eae12-117">This tutorial builds on the previous tutorial titled "Checkout and Payment with PayPal" in the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="eae12-118">你将学习：</span><span class="sxs-lookup"><span data-stu-id="eae12-118">What you'll learn:</span></span>

- <span data-ttu-id="eae12-119">如何使用代码将自定义角色和用户添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-119">How to use code to add a custom role and a user to the application.</span></span>
- <span data-ttu-id="eae12-120">如何限制对管理文件夹和页的访问。</span><span class="sxs-lookup"><span data-stu-id="eae12-120">How to restrict access to the administration folder and page.</span></span>
- <span data-ttu-id="eae12-121">如何提供自定义角色所属的用户的导航。</span><span class="sxs-lookup"><span data-stu-id="eae12-121">How to provide navigation for the user that belongs to the custom role.</span></span>
- <span data-ttu-id="eae12-122">如何使用模型绑定填充[DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)产品类别的控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-122">How to use model binding to populate a [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) control with product categories.</span></span>
- <span data-ttu-id="eae12-123">如何将文件上载到 web 应用程序使用[FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-123">How to upload a file to the web application using the [FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx) control.</span></span>
- <span data-ttu-id="eae12-124">如何验证控件用于实现输入的验证。</span><span class="sxs-lookup"><span data-stu-id="eae12-124">How to use validation controls to implement input validation.</span></span>
- <span data-ttu-id="eae12-125">如何添加和删除从应用程序的产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-125">How to add and remove products from the application.</span></span>

## <a name="these-features-are-included-in-the-tutorial"></a><span data-ttu-id="eae12-126">本教程中包括这些功能：</span><span class="sxs-lookup"><span data-stu-id="eae12-126">These features are included in the tutorial:</span></span>

- <span data-ttu-id="eae12-127">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="eae12-127">ASP.NET Identity</span></span>
- <span data-ttu-id="eae12-128">配置和授权</span><span class="sxs-lookup"><span data-stu-id="eae12-128">Configuration and Authorization</span></span>
- <span data-ttu-id="eae12-129">模型绑定</span><span class="sxs-lookup"><span data-stu-id="eae12-129">Model Binding</span></span>
- <span data-ttu-id="eae12-130">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="eae12-130">Unobtrusive Validation</span></span>

<span data-ttu-id="eae12-131">ASP.NET Web 窗体提供了成员资格功能。</span><span class="sxs-lookup"><span data-stu-id="eae12-131">ASP.NET Web Forms provides membership capabilities.</span></span> <span data-ttu-id="eae12-132">通过使用默认模板，你会获得应用程序运行时，可以立即使用的内置成员资格功能。</span><span class="sxs-lookup"><span data-stu-id="eae12-132">By using the default template, you have built-in membership functionality that you can immediately use when the application runs.</span></span> <span data-ttu-id="eae12-133">本教程演示如何使用 ASP.NET 标识添加自定义角色，并将用户分配给该角色。</span><span class="sxs-lookup"><span data-stu-id="eae12-133">This tutorial shows you how to use ASP.NET Identity to add a custom role and assign a user to that role.</span></span> <span data-ttu-id="eae12-134">您将学习如何限制对管理文件夹的访问。</span><span class="sxs-lookup"><span data-stu-id="eae12-134">You will learn how to restrict access to the administration folder.</span></span> <span data-ttu-id="eae12-135">你将添加到允许具有自定义角色的用户添加和删除产品，以及预览产品后已添加的管理文件夹页。</span><span class="sxs-lookup"><span data-stu-id="eae12-135">You'll add a page to the administration folder that allows a user with a custom role to add and remove products, and to preview a product after it has been added.</span></span>

## <a name="adding-a-custom-role"></a><span data-ttu-id="eae12-136">添加自定义角色</span><span class="sxs-lookup"><span data-stu-id="eae12-136">Adding a Custom Role</span></span>

<span data-ttu-id="eae12-137">使用 ASP.NET 标识，可以添加自定义角色，并将用户分配给该角色使用代码。</span><span class="sxs-lookup"><span data-stu-id="eae12-137">Using ASP.NET Identity, you can add a custom role and assign a user to that role using code.</span></span>

1. <span data-ttu-id="eae12-138">在**解决方案资源管理器**，右键单击*逻辑*文件夹并创建一个新类。</span><span class="sxs-lookup"><span data-stu-id="eae12-138">In **Solution Explorer**, right-click on the *Logic* folder and create a new class.</span></span>
2. <span data-ttu-id="eae12-139">将新类*RoleActions.cs*。</span><span class="sxs-lookup"><span data-stu-id="eae12-139">Name the new class *RoleActions.cs*.</span></span>
3. <span data-ttu-id="eae12-140">修改代码，以使其显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eae12-140">Modify the code so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. <span data-ttu-id="eae12-141">在**解决方案资源管理器**，打开*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-141">In **Solution Explorer**, open the *Global.asax.cs* file.</span></span>
5. <span data-ttu-id="eae12-142">修改*Global.asax.cs*文件添加代码以黄色突出显示，以使其显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eae12-142">Modify the *Global.asax.cs* file by adding the code highlighted in yellow so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. <span data-ttu-id="eae12-143">请注意，`AddUserAndRole`以红色下划线标记。</span><span class="sxs-lookup"><span data-stu-id="eae12-143">Notice that `AddUserAndRole` is underlined in red.</span></span> <span data-ttu-id="eae12-144">双击 AddUserAndRole 代码。</span><span class="sxs-lookup"><span data-stu-id="eae12-144">Double-click the AddUserAndRole code.</span></span>  
   <span data-ttu-id="eae12-145">将带有下划线的字母"A"突出显示方法的开头。</span><span class="sxs-lookup"><span data-stu-id="eae12-145">The letter "A" at the beginning of the highlighted method will be underlined.</span></span>
7. <span data-ttu-id="eae12-146">将鼠标悬停在字母"A"，然后单击用户界面，可用于生成方法存根出于`AddUserAndRole`方法。</span><span class="sxs-lookup"><span data-stu-id="eae12-146">Hover over the letter "A" and click the UI that allows you to generate a method stub for the `AddUserAndRole` method.</span></span> 

    ![成员资格和 Advministration-生成方法存根 （stub）](membership-and-administration/_static/image1.png)
8. <span data-ttu-id="eae12-148">单击标题为的选项：</span><span class="sxs-lookup"><span data-stu-id="eae12-148">Click the option titled:</span></span>  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. <span data-ttu-id="eae12-149">打开*RoleActions.cs*文件从*逻辑*文件夹。</span><span class="sxs-lookup"><span data-stu-id="eae12-149">Open the *RoleActions.cs* file from the *Logic* folder.</span></span>  
   <span data-ttu-id="eae12-150">`AddUserAndRole`方法也已添加到类文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-150">The `AddUserAndRole` method has been added to the class file.</span></span>
10. <span data-ttu-id="eae12-151">修改*RoleActions.cs*通过删除文件`NotImplementedeException`和添加以黄色，突出显示的代码，以使其显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eae12-151">Modify the *RoleActions.cs* file by removing the `NotImplementedeException` and adding the code highlighted in yellow, so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

<span data-ttu-id="eae12-152">上面的代码首先建立用于成员资格数据库的数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="eae12-152">The above code first establishes a database context for the membership database.</span></span> <span data-ttu-id="eae12-153">成员资格数据库也存储为 *.mdf*文件中*应用\_数据*文件夹。</span><span class="sxs-lookup"><span data-stu-id="eae12-153">The membership database is also stored as an *.mdf* file in the *App\_Data* folder.</span></span> <span data-ttu-id="eae12-154">你将能够查看此数据库后的第一个用户已登录到此 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-154">You will be able to view this database once the first user has signed in to this web application.</span></span> 

> [!NOTE] 
> 
> <span data-ttu-id="eae12-155">如果你想要存储以及产品的数据的成员身份数据，则可以考虑使用相同**DbContext**用于将产品数据存储在上面的代码。</span><span class="sxs-lookup"><span data-stu-id="eae12-155">If you wish to store the membership data along with the product data, you can consider using the same **DbContext** that you used to store the product data in the above code.</span></span>


 <span data-ttu-id="eae12-156">*内部*关键字是类型 （例如类） 和 （如方法或属性） 的类型成员的访问修饰符。</span><span class="sxs-lookup"><span data-stu-id="eae12-156">The *internal* keyword is an access modifier for types (such as classes) and type members (such as methods or properties).</span></span> <span data-ttu-id="eae12-157">内部类型或成员是只能在同一程序集中包含的文件中访问 *(.dll*文件)。</span><span class="sxs-lookup"><span data-stu-id="eae12-157">Internal types or members are accessible only within files contained in the same assembly *(.dll* file).</span></span> <span data-ttu-id="eae12-158">当你生成应用程序，程序集文件 *(.dll*) 创建包含运行你的应用程序时执行的代码。</span><span class="sxs-lookup"><span data-stu-id="eae12-158">When you build your application, an assembly file *(.dll*) is created that contains the code that is executed when you run your application.</span></span> 

<span data-ttu-id="eae12-159">A`RoleStore`对象，它提供角色管理，创建基于数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="eae12-159">A `RoleStore` object, which provides role management, is created based on the database context.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="eae12-160">请注意，当`RoleStore`创建对象它使用泛型`IdentityRole`类型。</span><span class="sxs-lookup"><span data-stu-id="eae12-160">Notice that when the `RoleStore` object is created it uses a Generic `IdentityRole` type.</span></span> <span data-ttu-id="eae12-161">这意味着，`RoleStore`则仅允许包含`IdentityRole`对象。</span><span class="sxs-lookup"><span data-stu-id="eae12-161">This means that the `RoleStore` is only allowed to contain `IdentityRole` objects.</span></span> <span data-ttu-id="eae12-162">此外通过使用泛型，在内存中的资源的更好地处理。</span><span class="sxs-lookup"><span data-stu-id="eae12-162">Also by using Generics, resources in memory are handled better.</span></span>


<span data-ttu-id="eae12-163">接下来，`RoleManager`对象，基于创建`RoleStore`刚创建的对象。</span><span class="sxs-lookup"><span data-stu-id="eae12-163">Next, the `RoleManager` object, is created based on the `RoleStore` object that you just created.</span></span> <span data-ttu-id="eae12-164">`RoleManager`对象公开角色相关 API 可以用于自动将更改保存至`RoleStore`。</span><span class="sxs-lookup"><span data-stu-id="eae12-164">the `RoleManager` object exposes role related API which can be used to automatically save changes to the `RoleStore`.</span></span> <span data-ttu-id="eae12-165">`RoleManager`则仅允许包含`IdentityRole`对象，因为该代码使用`<IdentityRole>`泛型类型。</span><span class="sxs-lookup"><span data-stu-id="eae12-165">The `RoleManager` is only allowed to contain `IdentityRole` objects because the code uses the `<IdentityRole>` Generic type.</span></span>

<span data-ttu-id="eae12-166">你调用`RoleExists`方法来确定是否存在成员资格数据库中的"canEdit"角色。</span><span class="sxs-lookup"><span data-stu-id="eae12-166">You call the `RoleExists` method to determine if the "canEdit" role is present in the membership database.</span></span> <span data-ttu-id="eae12-167">如果不是这样，在创建角色。</span><span class="sxs-lookup"><span data-stu-id="eae12-167">If it is not, you create the role.</span></span>

<span data-ttu-id="eae12-168">创建`UserManager`对象看起来更复杂比`RoleManager`控制，但是它是几乎相同。</span><span class="sxs-lookup"><span data-stu-id="eae12-168">Creating the `UserManager` object appears to be more complicated than the `RoleManager` control, however it is nearly the same.</span></span> <span data-ttu-id="eae12-169">它只是上一个行，而不是多个编码的。</span><span class="sxs-lookup"><span data-stu-id="eae12-169">It is just coded on one line rather than several.</span></span> <span data-ttu-id="eae12-170">在这里，您要传递的参数作为包含在括号中的新对象实例化。</span><span class="sxs-lookup"><span data-stu-id="eae12-170">Here, the parameter that you are passing is instantiating as a new object contained in the parenthesis.</span></span>

<span data-ttu-id="eae12-171">接下来通过创建一个新创建的"canEditUser"用户`ApplicationUser`对象。</span><span class="sxs-lookup"><span data-stu-id="eae12-171">Next you create the "canEditUser" user by creating a new `ApplicationUser` object.</span></span> <span data-ttu-id="eae12-172">然后，如果你已成功创建用户，你将用户添加到新的角色。</span><span class="sxs-lookup"><span data-stu-id="eae12-172">Then, if you successfully create the user, you add the user to the new role.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="eae12-173">错误处理将在稍后在本教程系列"ASP.NET 错误处理"本教程期间更新。</span><span class="sxs-lookup"><span data-stu-id="eae12-173">The error handling will be updated during the "ASP.NET Error Handling" tutorial later in this tutorial series.</span></span>


<span data-ttu-id="eae12-174">下次应用程序启动时，将作为名为应用程序的"canEdit"角色添加名为"canEditUser"的用户。</span><span class="sxs-lookup"><span data-stu-id="eae12-174">The next time the application starts, the user named "canEditUser" will be added as the role named "canEdit" of the application.</span></span> <span data-ttu-id="eae12-175">稍后在本教程中，你将登录为"canEditUser"用户以显示将在本教程过程中添加的其他功能。</span><span class="sxs-lookup"><span data-stu-id="eae12-175">Later in this tutorial, you will login as the "canEditUser" user to display additional capabilities that you will added during this tutorial.</span></span> <span data-ttu-id="eae12-176">有关 API 有关 ASP.NET Identity 的详细信息，请参阅[Microsoft.AspNet.Identity Namespace](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="eae12-176">For API details about ASP.NET Identity, see the [Microsoft.AspNet.Identity Namespace](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx).</span></span> <span data-ttu-id="eae12-177">有关初始化的 ASP.NET 标识系统的其他详细信息，请参阅[AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)。</span><span class="sxs-lookup"><span data-stu-id="eae12-177">For additional details about initializing the ASP.NET Identity system, see the [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs).</span></span>

### <a name="restricting-access-to-the-administration-page"></a><span data-ttu-id="eae12-178">将访问限制为管理页</span><span class="sxs-lookup"><span data-stu-id="eae12-178">Restricting Access to the Administration Page</span></span>

<span data-ttu-id="eae12-179">Wingtip Toys 示例应用程序允许匿名用户和登录的用户都能查看和购买产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-179">The Wingtip Toys sample application allows both anonymous users and logged-in users to view and purchase products.</span></span> <span data-ttu-id="eae12-180">但是，有自定义的"canEdit"角色的登录的用户可以访问受限制的页面以便添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-180">However, the logged-in user that has the custom "canEdit" role can access a restricted page in order to add and remove products.</span></span>

#### <a name="add-an-administration-folder-and-page"></a><span data-ttu-id="eae12-181">添加管理文件夹和页</span><span class="sxs-lookup"><span data-stu-id="eae12-181">Add an Administration Folder and Page</span></span>

<span data-ttu-id="eae12-182">接下来，将创建名为的文件夹*管理员*"canEditUser"用户属于 Wingtip Toys 的自定义角色示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-182">Next, you will create a folder named *Admin* for the "canEditUser" user belonging to the custom role of the Wingtip Toys sample application.</span></span>

1. <span data-ttu-id="eae12-183">右键单击项目名称 (**Wingtip Toys**) 中**解决方案资源管理器**和选择**添加** - &gt; **新文件夹**.</span><span class="sxs-lookup"><span data-stu-id="eae12-183">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Folder**.</span></span>
2. <span data-ttu-id="eae12-184">将新文件夹命名*管理员*。</span><span class="sxs-lookup"><span data-stu-id="eae12-184">Name the new folder *Admin*.</span></span>
3. <span data-ttu-id="eae12-185">右键单击*管理员*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="eae12-185">Right-click the *Admin* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="eae12-186">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="eae12-186">The **Add New Item** dialog box is displayed.</span></span>
4. <span data-ttu-id="eae12-187">选择<strong>Visual C#</strong> - &gt; <strong>Web</strong>左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="eae12-187">Select the <strong>Visual C#</strong>-&gt; <strong>Web</strong> templates group on the left.</span></span> <span data-ttu-id="eae12-188">从中间列表中选择<strong>包含母版页的 Web 窗体</strong>，将其命名为<em>AdminPage.aspx</em><strong>，</strong> ，然后选择<strong>添加</strong>。</span><span class="sxs-lookup"><span data-stu-id="eae12-188">From the middle list, select <strong>Web Form with Master Page</strong>,name it <em>AdminPage.aspx</em><strong>,</strong> and then select <strong>Add</strong>.</span></span>
5. <span data-ttu-id="eae12-189">选择*Site.Master*文件作为主页上，，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="eae12-189">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>

#### <a name="add-a-webconfig-file"></a><span data-ttu-id="eae12-190">添加 Web.config 文件</span><span class="sxs-lookup"><span data-stu-id="eae12-190">Add a Web.config File</span></span>

<span data-ttu-id="eae12-191">通过添加*Web.config*文件为*管理员*文件夹中，你可以限制对访问文件夹中包含的页。</span><span class="sxs-lookup"><span data-stu-id="eae12-191">By adding a *Web.config* file to the *Admin* folder, you can restrict access to the page contained in the folder.</span></span>

1. <span data-ttu-id="eae12-192">右键单击*管理员*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="eae12-192">Right-click the *Admin* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="eae12-193">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="eae12-193">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="eae12-194">从 Visual C# web 模板列表中，选择<strong>Web 配置文件</strong>从中间列表中，接受默认名称<em>Web.config</em><strong>，</strong> ，然后选择<strong>添加</strong>。</span><span class="sxs-lookup"><span data-stu-id="eae12-194">From the list of Visual C# web templates, select <strong>Web Configuration File</strong>from the middle list, accept the default name of <em>Web.config</em><strong>,</strong> and then select <strong>Add</strong>.</span></span>
3. <span data-ttu-id="eae12-195">替换的现有 XML 内容中*Web.config*替换为以下文件：</span><span class="sxs-lookup"><span data-stu-id="eae12-195">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

<span data-ttu-id="eae12-196">保存*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-196">Save the *Web.config* file.</span></span> <span data-ttu-id="eae12-197">*Web.config*文件指定属于"canEdit"角色的应用程序的唯一用户可以访问此页中包含*管理员*文件夹。</span><span class="sxs-lookup"><span data-stu-id="eae12-197">The *Web.config* file specifies that only user belonging to the "canEdit" role of the application can access the page contained in the *Admin* folder.</span></span>

### <a name="including-custom-role-navigation"></a><span data-ttu-id="eae12-198">包括自定义角色导航</span><span class="sxs-lookup"><span data-stu-id="eae12-198">Including Custom Role Navigation</span></span>

<span data-ttu-id="eae12-199">若要启用自定义的"canEdit"角色的用户导航到应用程序的管理部分，你必须添加一个链接到*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="eae12-199">To enable the user of the custom "canEdit" role to navigate to the administration section of the application, you must add a link to the *Site.Master* page.</span></span> <span data-ttu-id="eae12-200">只有属于"canEdit"角色的用户将能够看到**管理员**链接并访问管理部分。</span><span class="sxs-lookup"><span data-stu-id="eae12-200">Only users that belong to the "canEdit" role will be able to see the **Admin** link and access the administration section.</span></span>

1. <span data-ttu-id="eae12-201">在解决方案资源管理器，找到并打开*Site.Master*页。</span><span class="sxs-lookup"><span data-stu-id="eae12-201">In Solution Explorer, find and open the *Site.Master* page.</span></span>
2. <span data-ttu-id="eae12-202">若要创建的"canEdit"角色的用户的链接，将添加在黄色再到以下未经排序的列表中突出显示的标记`<ul>`元素以便，列表显示为如下所示：</span><span class="sxs-lookup"><span data-stu-id="eae12-202">To create a link for the user of the "canEdit" role, add the markup highlighted in yellow to the following unordered list `<ul>` element so that the list appears as follows:</span></span>  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. <span data-ttu-id="eae12-203">打开*Site.Master.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-203">Open the *Site.Master.cs* file.</span></span> <span data-ttu-id="eae12-204">请**管理员**链接仅对通过添加代码以到黄色突出显示"canEditUser"用户可见`Page_Load`处理程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-204">Make the **Admin** link visible only to the "canEditUser" user by adding the code highlighted in yellow to the `Page_Load` handler.</span></span> <span data-ttu-id="eae12-205">`Page_Load`处理程序将显示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="eae12-205">The `Page_Load` handler will appear as follows:</span></span>   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

<span data-ttu-id="eae12-206">加载页面，代码将检查是否已登录的用户具有的"canEdit"角色。</span><span class="sxs-lookup"><span data-stu-id="eae12-206">When the page loads, the code checks whether the logged-in user has the role of "canEdit".</span></span> <span data-ttu-id="eae12-207">如果用户属于"canEdit"角色，其中包含到链接的 span 元素*AdminPage.aspx*页 （并因此范围内的链接） 均可见。</span><span class="sxs-lookup"><span data-stu-id="eae12-207">If the user belongs to the "canEdit" role, the span element containing the link to the *AdminPage.aspx* page (and consequently the link inside the span) is made visible.</span></span>

### <a name="enabling-product-administration"></a><span data-ttu-id="eae12-208">启用产品管理</span><span class="sxs-lookup"><span data-stu-id="eae12-208">Enabling Product Administration</span></span>

<span data-ttu-id="eae12-209">到目前为止，你已创建"canEdit"角色，并添加"canEditUser"用户、 管理文件夹和管理页。</span><span class="sxs-lookup"><span data-stu-id="eae12-209">So far, you have created the "canEdit" role and added an "canEditUser" user, an administration folder, and an administration page.</span></span> <span data-ttu-id="eae12-210">你已设置为管理文件夹和页的访问权限，并已添加到应用程序的"canEdit"角色的用户的导航链接。</span><span class="sxs-lookup"><span data-stu-id="eae12-210">You have set access rights for the administration folder and page, and have added a navigation link for the user of the "canEdit" role to the application.</span></span> <span data-ttu-id="eae12-211">接下来，你将添加到标记*AdminPage.aspx*页上和代码设为*AdminPage.aspx.cs*将启用"canEdit"角色的用户添加和删除产品的代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-211">Next, you will add markup to the *AdminPage.aspx* page and code to the *AdminPage.aspx.cs* code-behind file that will enable the user with the "canEdit" role to add and remove products.</span></span>

1. <span data-ttu-id="eae12-212">在**解决方案资源管理器**，打开*AdminPage.aspx*文件从*管理员*文件夹。</span><span class="sxs-lookup"><span data-stu-id="eae12-212">In **Solution Explorer**, open the *AdminPage.aspx* file from the *Admin* folder.</span></span>
2. <span data-ttu-id="eae12-213">现有的标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="eae12-213">Replace the existing markup with the following:</span></span>  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. <span data-ttu-id="eae12-214">接下来，打开*AdminPage.aspx.cs*代码隐藏文件，请右键单击*AdminPage.aspx*并单击**查看代码**。</span><span class="sxs-lookup"><span data-stu-id="eae12-214">Next, open the *AdminPage.aspx.cs* code-behind file by right-clicking the *AdminPage.aspx* and clicking **View Code**.</span></span>
4. <span data-ttu-id="eae12-215">中的现有代码替换*AdminPage.aspx.cs*代码隐藏文件替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="eae12-215">Replace the existing code in the *AdminPage.aspx.cs* code-behind file with the following code:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

<span data-ttu-id="eae12-216">在代码中为输入*AdminPage.aspx.cs*代码隐藏文件中，一个名为类`AddProducts`执行将产品添加到数据库的实际工作。</span><span class="sxs-lookup"><span data-stu-id="eae12-216">In the code that you entered for the *AdminPage.aspx.cs* code-behind file, a class called `AddProducts` does the actual work of adding products to the database.</span></span> <span data-ttu-id="eae12-217">此类尚不存在，因此现在你将创建它。</span><span class="sxs-lookup"><span data-stu-id="eae12-217">This class doesn't exist yet, so you will create it now.</span></span>

1. <span data-ttu-id="eae12-218">在**解决方案资源管理器**，右键单击*逻辑*文件夹，然后选择**添加** - &gt; **新项**。</span><span class="sxs-lookup"><span data-stu-id="eae12-218">In **Solution Explorer**, right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="eae12-219">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="eae12-219">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="eae12-220">选择**Visual C#**  - &gt; **代码**左侧的模板组。</span><span class="sxs-lookup"><span data-stu-id="eae12-220">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="eae12-221">然后，选择**类**从中间列表并将其命名*AddProducts.cs*。</span><span class="sxs-lookup"><span data-stu-id="eae12-221">Then, select **Class**from the middle list and name it *AddProducts.cs*.</span></span>   
   <span data-ttu-id="eae12-222">将显示新的类文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-222">The new class file is displayed.</span></span>
3. <span data-ttu-id="eae12-223">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="eae12-223">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

<span data-ttu-id="eae12-224">*AdminPage.aspx*页允许用户属于"canEdit"角色添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-224">The *AdminPage.aspx* page allows the user belonging to the "canEdit" role to add and remove products.</span></span> <span data-ttu-id="eae12-225">添加新产品后，有关该产品的详细信息验证，然后输入到数据库。</span><span class="sxs-lookup"><span data-stu-id="eae12-225">When a new product is added, the details about the product are validated and then entered into the database.</span></span> <span data-ttu-id="eae12-226">新的产品是立即可供所有用户的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-226">The new product is immediately available to all users of the web application.</span></span>

#### <a name="unobtrusive-validation"></a><span data-ttu-id="eae12-227">非介入式验证</span><span class="sxs-lookup"><span data-stu-id="eae12-227">Unobtrusive Validation</span></span>

<span data-ttu-id="eae12-228">用户在提供的产品详细信息*AdminPage.aspx*页使用验证控件验证 (`RequiredFieldValidator`和`RegularExpressionValidator`)。</span><span class="sxs-lookup"><span data-stu-id="eae12-228">The product details that the user provides on the *AdminPage.aspx* page are validated using validation controls (`RequiredFieldValidator` and `RegularExpressionValidator`).</span></span> <span data-ttu-id="eae12-229">这些控件自动使用非介入式验证。</span><span class="sxs-lookup"><span data-stu-id="eae12-229">These controls automatically use unobtrusive validation.</span></span> <span data-ttu-id="eae12-230">非介入式验证允许使用 JavaScript 客户端验证逻辑，这意味着页不需要到要验证的服务器的行程的验证控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-230">Unobtrusive validation allows the validation controls to use JavaScript for client-side validation logic, which means the page does not require a trip to the server to be validated.</span></span> <span data-ttu-id="eae12-231">默认情况下，非介入式验证包括在*Web.config*文件基于以下配置设置：</span><span class="sxs-lookup"><span data-stu-id="eae12-231">By default, unobtrusive validation is included in the *Web.config* file based on the following configuration setting:</span></span>

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a><span data-ttu-id="eae12-232">正则表达式</span><span class="sxs-lookup"><span data-stu-id="eae12-232">Regular Expressions</span></span>

<span data-ttu-id="eae12-233">上的产品价格*AdminPage.aspx*使用验证页**RegularExpressionValidator**控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-233">The product price on the *AdminPage.aspx* page is validated using a **RegularExpressionValidator** control.</span></span> <span data-ttu-id="eae12-234">此控件验证是否关联的输入控件 （"AddProductPrice"文本框中） 的值与指定正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="eae12-234">This control validates whether the value of the associated input control (the "AddProductPrice" TextBox) matches the pattern specified by the regular expression.</span></span> <span data-ttu-id="eae12-235">正则表达式是一个模式匹配表示法，可用于快速查找和匹配特定的字符模式。</span><span class="sxs-lookup"><span data-stu-id="eae12-235">A regular expression is a pattern-matching notation that enables you to quickly find and match specific character patterns.</span></span> <span data-ttu-id="eae12-236">**RegularExpressionValidator**控件包含一个名为属性`ValidationExpression`包含用来验证价格输入，如下所示的正则表达式：</span><span class="sxs-lookup"><span data-stu-id="eae12-236">The **RegularExpressionValidator** control includes a property named `ValidationExpression` that contains the regular expression used to validate price input, as shown below:</span></span>

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a><span data-ttu-id="eae12-237">FileUpload 控件</span><span class="sxs-lookup"><span data-stu-id="eae12-237">FileUpload Control</span></span>

<span data-ttu-id="eae12-238">除了输入和验证控件中，你添加**FileUpload**控制转移到*AdminPage.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="eae12-238">In addition to the input and validation controls, you added the **FileUpload** control to the *AdminPage.aspx* page.</span></span> <span data-ttu-id="eae12-239">此控件提供功能以将文件上载。</span><span class="sxs-lookup"><span data-stu-id="eae12-239">This control provides the capability to upload files.</span></span> <span data-ttu-id="eae12-240">在这种情况下，你仅允许要上载的图像文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-240">In this case, you are only allowing image files to be uploaded.</span></span> <span data-ttu-id="eae12-241">中的代码隐藏文件 (*AdminPage.aspx.cs*)，当`AddProductButton`单击后，代码将检查`HasFile`属性**FileUpload**控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-241">In the code-behind file (*AdminPage.aspx.cs*), when the `AddProductButton` is clicked, the code checks the `HasFile` property of the **FileUpload** control.</span></span> <span data-ttu-id="eae12-242">如果控件有一个文件，并且如果允许 （基于文件扩展名） 的文件类型，将图像保存到*映像*文件夹和*映像/拇指*应用程序文件夹。</span><span class="sxs-lookup"><span data-stu-id="eae12-242">If the control has a file and if the file type (based on file extension) is allowed, the image is saved to the *Images* folder and the *Images/Thumbs* folder of the application.</span></span>

#### <a name="model-binding"></a><span data-ttu-id="eae12-243">模型绑定</span><span class="sxs-lookup"><span data-stu-id="eae12-243">Model Binding</span></span>

<span data-ttu-id="eae12-244">本系列教程中前面你使用模型绑定来填充**ListView**控件， **FormsView**控件， **GridView**控件，和一个**DetailView**控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-244">Earlier in this tutorial series you used model binding to populate a **ListView** control, a **FormsView** control, a **GridView** control, and a **DetailView** control.</span></span> <span data-ttu-id="eae12-245">在本教程中，你使用模型绑定来填充**DropDownList**具有的产品类别列表控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-245">In this tutorial, you use model binding to populate a **DropDownList** control with a list of product categories.</span></span>

<span data-ttu-id="eae12-246">添加到的标记*AdminPage.aspx*文件包含**DropDownList**控件称为`DropDownAddCategory`:</span><span class="sxs-lookup"><span data-stu-id="eae12-246">The markup that you added to the *AdminPage.aspx* file contains a **DropDownList** control called `DropDownAddCategory`:</span></span>

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

<span data-ttu-id="eae12-247">使用模型绑定来填充此**DropDownList**通过设置`ItemType`属性和`SelectMethod`属性。</span><span class="sxs-lookup"><span data-stu-id="eae12-247">You use model binding to populate this **DropDownList** by setting the `ItemType` attribute and the `SelectMethod` attribute.</span></span> <span data-ttu-id="eae12-248">`ItemType`属性指定使用`WingtipToys.Models.Category`键入填充控件时。</span><span class="sxs-lookup"><span data-stu-id="eae12-248">The `ItemType` attribute specifies that you use the `WingtipToys.Models.Category` type when populating the control.</span></span> <span data-ttu-id="eae12-249">通过创建定义这种类型的开头的本系列教程`Category`类 （如下所示）。</span><span class="sxs-lookup"><span data-stu-id="eae12-249">You defined this type at the beginning of this tutorial series by creating the `Category` class (shown below).</span></span> <span data-ttu-id="eae12-250">`Category`类位于*模型*内的文件夹*Category.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="eae12-250">The `Category` class is in the *Models* folder inside the *Category.cs* file.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

<span data-ttu-id="eae12-251">`SelectMethod`属性**DropDownList**控件指定使用`GetCategories`方法 （如下所示），它是包含在代码隐藏文件 (*AdminPage.aspx.cs*)。</span><span class="sxs-lookup"><span data-stu-id="eae12-251">The `SelectMethod` attribute of the **DropDownList** control specifies that you use the `GetCategories` method (shown below) that is included in the code-behind file (*AdminPage.aspx.cs*).</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

<span data-ttu-id="eae12-252">此方法指定`IQueryable`接口用于针对查询的计算结果`Category`类型。</span><span class="sxs-lookup"><span data-stu-id="eae12-252">This method specifies that an `IQueryable` interface is used to evaluate a query against a `Category` type.</span></span> <span data-ttu-id="eae12-253">返回的值用于填充**DropDownList**中页的标记 (*AdminPage.aspx*)。</span><span class="sxs-lookup"><span data-stu-id="eae12-253">The returned value is used to populate the **DropDownList** in the markup of the page (*AdminPage.aspx*).</span></span>

<span data-ttu-id="eae12-254">通过将设置指定列表中的每个项的显示文本`DataTextField`属性。</span><span class="sxs-lookup"><span data-stu-id="eae12-254">The text displayed for each item in the list is specified by setting the `DataTextField` attribute.</span></span> <span data-ttu-id="eae12-255">`DataTextField`属性使用`CategoryName`的`Category`（上面所示） 以显示每个类别中的类**DropDownList**控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-255">The `DataTextField` attribute uses the `CategoryName` of the `Category` class (shown above) to display each category in the **DropDownList** control.</span></span> <span data-ttu-id="eae12-256">中选择一项时传递的实际值**DropDownList**控件基于`DataValueField`属性。</span><span class="sxs-lookup"><span data-stu-id="eae12-256">The actual value that is passed when an item is selected in the **DropDownList** control is based on the `DataValueField` attribute.</span></span> <span data-ttu-id="eae12-257">`DataValueField`属性设置为`CategoryID`中定义`Category`类 （如上所示）。</span><span class="sxs-lookup"><span data-stu-id="eae12-257">The `DataValueField` attribute is set to the `CategoryID` as define in the `Category` class (shown above).</span></span>

### <a name="how-the-application-will-work"></a><span data-ttu-id="eae12-258">应用程序将如何工作</span><span class="sxs-lookup"><span data-stu-id="eae12-258">How the Application Will Work</span></span>

<span data-ttu-id="eae12-259">当属于"canEdit"角色的用户首次导航到页面`DropDownAddCategory` **DropDownList**控件中填充上文所述。</span><span class="sxs-lookup"><span data-stu-id="eae12-259">When the user belonging to the "canEdit" role navigates to the page for the first time, the `DropDownAddCategory`**DropDownList** control is populated as described above.</span></span> <span data-ttu-id="eae12-260">`DropDownRemoveProduct` **DropDownList**控件还使用相同的方法的产品中填充。</span><span class="sxs-lookup"><span data-stu-id="eae12-260">The `DropDownRemoveProduct`**DropDownList** control is also populated with products using the same approach.</span></span> <span data-ttu-id="eae12-261">属于"canEdit"角色的用户选定的类别类型，并添加产品详细信息 (**名称**，**说明**，**价格**，和**映像文件**).</span><span class="sxs-lookup"><span data-stu-id="eae12-261">The user belonging to the "canEdit" role selects the category type and adds product details (**Name**, **Description**, **Price**, and **Image File**).</span></span> <span data-ttu-id="eae12-262">当用户属于"canEdit"角色单击**添加产品**按钮，`AddProductButton_Click`触发事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-262">When the user belonging to the "canEdit" role clicks the **Add Product** button, the `AddProductButton_Click` event handler is triggered.</span></span> <span data-ttu-id="eae12-263">`AddProductButton_Click`事件处理程序位于的代码隐藏文件 (*AdminPage.aspx.cs*) 检查要确保它匹配允许的文件类型的图像文件 *(.gif*， *.png*， *.jpeg*，或 *.jpg*)。</span><span class="sxs-lookup"><span data-stu-id="eae12-263">The `AddProductButton_Click` event handler located in the code-behind file (*AdminPage.aspx.cs*) checks the image file to make sure it matches the allowed file types *(.gif*, *.png*, *.jpeg*, or *.jpg*).</span></span> <span data-ttu-id="eae12-264">然后，该图像文件保存到 Wingtip Toys 示例应用程序的文件夹。</span><span class="sxs-lookup"><span data-stu-id="eae12-264">Then, the image file is saved into a folder of the Wingtip Toys sample application.</span></span> <span data-ttu-id="eae12-265">接下来，将新的产品添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="eae12-265">Next, the new product is added to the database.</span></span> <span data-ttu-id="eae12-266">若要完成添加一个新的产品的新实例`AddProducts`类被创建并命名为产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-266">To accomplish adding a new product, a new instance of the `AddProducts` class is created and named products.</span></span> <span data-ttu-id="eae12-267">`AddProducts`类具有一个名为方法`AddProduct`，和产品对象调用此方法以将产品添加到数据库。</span><span class="sxs-lookup"><span data-stu-id="eae12-267">The `AddProducts` class has a method named `AddProduct`, and the products object calls this method to add products to the database.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

<span data-ttu-id="eae12-268">查询字符串值如果代码成功向数据库添加新的产品，都会重新加载页面`ProductAction=add`。</span><span class="sxs-lookup"><span data-stu-id="eae12-268">If the code successfully adds the new product to the database, the page is reloaded with the query string value `ProductAction=add`.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

<span data-ttu-id="eae12-269">时将重新加载页面，则会将查询字符串包含在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="eae12-269">When the page reloads, the query string is included in the URL.</span></span> <span data-ttu-id="eae12-270">通过重新加载该页面，属于"canEdit"角色的用户可以立即查看中的更新**DropDownList**上的控件*AdminPage.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="eae12-270">By reloading the page, the user belonging to the "canEdit" role can immediately see the updates in the **DropDownList** controls on the *AdminPage.aspx* page.</span></span> <span data-ttu-id="eae12-271">此外，通过包括查询字符串的 url，页可以显示一条成功消息给用户属于"canEdit"角色。</span><span class="sxs-lookup"><span data-stu-id="eae12-271">Also, by including the query string with the URL, the page can display a success message to the user belonging to the "canEdit" role.</span></span>

<span data-ttu-id="eae12-272">当*AdminPage.aspx*页上的重新加载需要，`Page_Load`事件时调用。</span><span class="sxs-lookup"><span data-stu-id="eae12-272">When the *AdminPage.aspx* page reloads, the `Page_Load` event is called.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

<span data-ttu-id="eae12-273">`Page_Load`事件处理程序检查查询字符串值，并确定是否显示一条成功消息。</span><span class="sxs-lookup"><span data-stu-id="eae12-273">The `Page_Load` event handler checks the query string value and determines whether to show a success message.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="eae12-274">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="eae12-274">Running the Application</span></span>

<span data-ttu-id="eae12-275">你可以在购物车中运行应用程序现在以查看如何添加、 删除和更新项目。</span><span class="sxs-lookup"><span data-stu-id="eae12-275">You can run the application now to see how you can add, delete, and update items in the shopping cart.</span></span> <span data-ttu-id="eae12-276">购物车总计将反映在购物车中的所有项的总成本。</span><span class="sxs-lookup"><span data-stu-id="eae12-276">The shopping cart total will reflect the total cost of all items in the shopping cart.</span></span>

1. <span data-ttu-id="eae12-277">在解决方案资源管理器，按**F5**运行 Wingtip Toys 示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="eae12-277">In Solution Explorer, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="eae12-278">浏览器将打开并显示*Default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="eae12-278">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="eae12-279">单击**登录**页顶部的链接。</span><span class="sxs-lookup"><span data-stu-id="eae12-279">Click the **Log in** link at the top of the page.</span></span> 

    ![成员资格和管理的登录链接](membership-and-administration/_static/image2.png)

   <span data-ttu-id="eae12-281">*Login.aspx*显示页。</span><span class="sxs-lookup"><span data-stu-id="eae12-281">The *Login.aspx* page is displayed.</span></span>
3. <span data-ttu-id="eae12-282">使用以下用户名和密码：</span><span class="sxs-lookup"><span data-stu-id="eae12-282">Use the following user name and password:</span></span>  
   <span data-ttu-id="eae12-283">用户名： canEditUser@wingtiptoys.com</span><span class="sxs-lookup"><span data-stu-id="eae12-283">User name: canEditUser@wingtiptoys.com</span></span>  
   <span data-ttu-id="eae12-284">密码： Pa $$ word1</span><span class="sxs-lookup"><span data-stu-id="eae12-284">Password: Pa$$word1</span></span> 

    ![成员资格和管理的登录页](membership-and-administration/_static/image3.png)
4. <span data-ttu-id="eae12-286">单击**登录**附近页面底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="eae12-286">Click the **Log in** button near the bottom of the page.</span></span>
5. <span data-ttu-id="eae12-287">在下一步的页的顶部，选择**管理员**链接以导航到*AdminPage.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="eae12-287">At the top of the next page, select the **Admin** link to navigate to the *AdminPage.aspx* page.</span></span> 

    ![成员资格和管理-管理员链接](membership-and-administration/_static/image4.png)
6. <span data-ttu-id="eae12-289">若要测试输入的验证，请单击**添加产品**而无需添加任何产品详细信息的按钮。</span><span class="sxs-lookup"><span data-stu-id="eae12-289">To test the input validation, click the **Add Product** button without adding any product details.</span></span> 

    ![成员资格和管理-管理员页](membership-and-administration/_static/image5.png)

   <span data-ttu-id="eae12-291">请注意，会显示必填的字段消息。</span><span class="sxs-lookup"><span data-stu-id="eae12-291">Notice that the required field messages are displayed.</span></span>
7. <span data-ttu-id="eae12-292">添加新产品的详细信息，然后单击**添加产品**按钮。</span><span class="sxs-lookup"><span data-stu-id="eae12-292">Add the details for a new product, and then click the **Add Product** button.</span></span> 

    ![成员资格和管理-添加产品](membership-and-administration/_static/image6.png)
8. <span data-ttu-id="eae12-294">选择**产品**添加从顶部导航菜单中查看新的产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-294">Select **Products** from the top navigation menu to view the new product you added.</span></span> 

    ![成员资格和管理-显示新产品](membership-and-administration/_static/image7.png)
9. <span data-ttu-id="eae12-296">单击**管理员**链接以返回到管理页。</span><span class="sxs-lookup"><span data-stu-id="eae12-296">Click the **Admin** link to return to the administration page.</span></span>
10. <span data-ttu-id="eae12-297">在**删除产品**部分的页上，选择你在中添加新产品**DropDownListBox**。</span><span class="sxs-lookup"><span data-stu-id="eae12-297">In the **Remove Product** section of the page, select the new product you added in the **DropDownListBox**.</span></span>
11. <span data-ttu-id="eae12-298">单击**删除产品**按钮可以从应用程序中删除新的产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-298">Click the **Remove Product** button to remove the new product from the application.</span></span> 

    ![成员资格和管理-删除产品](membership-and-administration/_static/image8.png)
12. <span data-ttu-id="eae12-300">选择**产品**从顶部导航菜单以确认已删除产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-300">Select **Products** from the top navigation menu to confirm that the product has been removed.</span></span>
13. <span data-ttu-id="eae12-301">单击**注销**存在管理模式。</span><span class="sxs-lookup"><span data-stu-id="eae12-301">Click **Log off** to exist administration mode.</span></span>   
    <span data-ttu-id="eae12-302">请注意，顶部导航窗格中将不再显示**管理员**菜单项。</span><span class="sxs-lookup"><span data-stu-id="eae12-302">Notice that the top navigation pane no longer shows the **Admin** menu item.</span></span>

## <a name="summary"></a><span data-ttu-id="eae12-303">总结</span><span class="sxs-lookup"><span data-stu-id="eae12-303">Summary</span></span>

<span data-ttu-id="eae12-304">在本教程中，你将添加自定义角色和用户属于的自定义角色，对管理文件夹和页上，访问受到限制并提供属于自定义角色的用户的导航。</span><span class="sxs-lookup"><span data-stu-id="eae12-304">In this tutorial, you added a custom role and a user belonging to the custom role, restricted access to the administration folder and page, and provided navigation for the user belonging to the custom role.</span></span> <span data-ttu-id="eae12-305">使用模型绑定来填充**DropDownList**与数据的控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-305">You used model binding to populate a **DropDownList** control with data.</span></span> <span data-ttu-id="eae12-306">你实现**FileUpload**控件和验证控件。</span><span class="sxs-lookup"><span data-stu-id="eae12-306">You implemented the **FileUpload** control and validation controls.</span></span> <span data-ttu-id="eae12-307">此外，你已学习如何添加和从数据库中删除产品。</span><span class="sxs-lookup"><span data-stu-id="eae12-307">Also, you have learned how to add and remove products from a database.</span></span> <span data-ttu-id="eae12-308">在下一步的教程中，你将了解如何实现 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="eae12-308">In the next tutorial, you'll learn how to implement ASP.NET routing.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eae12-309">其他资源</span><span class="sxs-lookup"><span data-stu-id="eae12-309">Additional Resources</span></span>

<span data-ttu-id="eae12-310">[Web.config 的授权元素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="eae12-310">[Web.config - authorization Element](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="eae12-311">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="eae12-311">ASP.NET Identity</span></span>](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[<span data-ttu-id="eae12-312">将包含成员资格、 OAuth 和 SQL 数据库的安全的 ASP.NET Web 窗体应用程序部署到 Azure 网站</span><span class="sxs-lookup"><span data-stu-id="eae12-312">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="eae12-313">Microsoft Azure 的免费试用版</span><span class="sxs-lookup"><span data-stu-id="eae12-313">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="eae12-314">[上一页](checkout-and-payment-with-paypal.md)
> [下一页](url-routing.md)</span><span class="sxs-lookup"><span data-stu-id="eae12-314">[Previous](checkout-and-payment-with-paypal.md)
[Next](url-routing.md)</span></span>
