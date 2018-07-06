---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 创建 MVC 3 应用程序使用 Razor 和非介入式 JavaScript |Microsoft Docs
author: microsoft
description: 用户列表示例 web 应用程序演示如何创建使用 Razor 视图引擎的 ASP.NET MVC 3 应用程序是多么简单。 示例应用程序 s...
ms.author: aspnetcontent
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: 136c87cba70525da53c1f74576c50c12f8759539
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840457"
---
<a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="d266e-104">创建 MVC 3 应用程序使用 Razor 和非介入式 JavaScript</span><span class="sxs-lookup"><span data-stu-id="d266e-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>
====================
<span data-ttu-id="d266e-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d266e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d266e-106">用户列表示例 web 应用程序演示如何创建使用 Razor 视图引擎的 ASP.NET MVC 3 应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="d266e-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="d266e-107">示例应用程序演示如何使用 ASP.NET mvc 版本 3 的新 Razor 视图引擎和 Visual Studio 2010 创建一个虚构的用户列表网站，包括功能，例如创建、 显示、 编辑和删除用户。</span><span class="sxs-lookup"><span data-stu-id="d266e-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="d266e-108">本教程介绍为了构建用户列表示例 ASP.NET MVC 3 应用程序已执行的步骤。</span><span class="sxs-lookup"><span data-stu-id="d266e-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="d266e-109">包含 C# 和 VB 源代码的 Visual Studio 项目是可随附于本主题：[下载](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。</span><span class="sxs-lookup"><span data-stu-id="d266e-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="d266e-110">如果您有关于本教程的问题，请将其发布到[MVC 论坛](https://forums.asp.net/1146.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d266e-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>


## <a name="overview"></a><span data-ttu-id="d266e-111">概述</span><span class="sxs-lookup"><span data-stu-id="d266e-111">Overview</span></span>

<span data-ttu-id="d266e-112">你将构建的应用程序是一个简单的用户列表网站。</span><span class="sxs-lookup"><span data-stu-id="d266e-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="d266e-113">用户可以输入、 查看和更新用户信息。</span><span class="sxs-lookup"><span data-stu-id="d266e-113">Users can enter, view, and update user information.</span></span>

![示例站点](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="d266e-115">您可以下载 VB 和 C# 已完成的项目[此处](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)。</span><span class="sxs-lookup"><span data-stu-id="d266e-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="d266e-116">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="d266e-116">Creating the Web Application</span></span>

<span data-ttu-id="d266e-117">若要开始本教程，请打开 Visual Studio 2010 并创建新项目使用*ASP.NET MVC 3 Web 应用程序*模板。</span><span class="sxs-lookup"><span data-stu-id="d266e-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="d266e-118">该应用程序命名&quot;Mvc3Razor&quot;。</span><span class="sxs-lookup"><span data-stu-id="d266e-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="d266e-119">[![新的 MVC 3 项目](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="d266e-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="d266e-120">在中**新的 ASP.NET MVC 3 项目**对话框中，选择**Internet 应用程序**，选择 Razor 视图引擎，，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="d266e-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![新建 ASP.NET MVC 3 项目对话框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="d266e-122">在本教程中你将不使用 ASP.NET 成员资格提供程序，因此可以删除与登录名和成员身份相关联的所有文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="d266e-123">在中**解决方案资源管理器**，删除以下文件和目录：</span><span class="sxs-lookup"><span data-stu-id="d266e-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="d266e-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="d266e-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="d266e-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="d266e-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="d266e-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="d266e-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="d266e-127">*Views\Account* （和此目录中的所有文件）</span><span class="sxs-lookup"><span data-stu-id="d266e-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="d266e-129">编辑 <em>\_Layout.cshtml</em>文件，然后替换中的标记`<div>`名为元素`logindisplay`并显示消息 <em>&quot;</em>登录名已禁用&quot;.</span><span class="sxs-lookup"><span data-stu-id="d266e-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="d266e-130">下面的示例显示了新的标记：</span><span class="sxs-lookup"><span data-stu-id="d266e-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="d266e-131">添加模型</span><span class="sxs-lookup"><span data-stu-id="d266e-131">Adding the Model</span></span>

<span data-ttu-id="d266e-132">在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后单击**类**。</span><span class="sxs-lookup"><span data-stu-id="d266e-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![新用户 Mdl 类](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="d266e-134">将此类命名为 `UserModel`。</span><span class="sxs-lookup"><span data-stu-id="d266e-134">Name the class `UserModel`.</span></span> <span data-ttu-id="d266e-135">内容替换为*UserModel*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="d266e-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="d266e-136">`UserModel`类表示的用户。</span><span class="sxs-lookup"><span data-stu-id="d266e-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="d266e-137">类的每个成员添加批注[所需](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性从[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间。</span><span class="sxs-lookup"><span data-stu-id="d266e-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="d266e-138">中的属性[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间提供的 web 应用程序的自动客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="d266e-139">打开`HomeController`类，并添加`using`指令，以便可以访问`UserModel`和`Users`类：</span><span class="sxs-lookup"><span data-stu-id="d266e-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="d266e-140">后面`HomeController`声明中，添加下面的注释以及对引用`Users`类：</span><span class="sxs-lookup"><span data-stu-id="d266e-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="d266e-141">`Users`类是将在本教程中使用的简化的内存中数据存储。</span><span class="sxs-lookup"><span data-stu-id="d266e-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="d266e-142">在实际的应用程序将使用数据库来存储用户信息。</span><span class="sxs-lookup"><span data-stu-id="d266e-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="d266e-143">前的几行`HomeController`文件显示在下面的示例：</span><span class="sxs-lookup"><span data-stu-id="d266e-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="d266e-144">生成应用程序，以便用户模型将可供下一步中的基架向导。</span><span class="sxs-lookup"><span data-stu-id="d266e-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="d266e-145">创建的默认视图</span><span class="sxs-lookup"><span data-stu-id="d266e-145">Creating the Default View</span></span>

<span data-ttu-id="d266e-146">下一步是添加一个操作方法和视图以显示用户。</span><span class="sxs-lookup"><span data-stu-id="d266e-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="d266e-147">删除现有*Views\Home\Index*文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="d266e-148">您将创建一个新*索引*文件以显示用户。</span><span class="sxs-lookup"><span data-stu-id="d266e-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="d266e-149">在中`HomeController`类中的内容替换为`Index`方法使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="d266e-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="d266e-150">内右击`Index`方法，然后单击**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="d266e-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![添加视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="d266e-152">选择**创建强类型化视图**选项。</span><span class="sxs-lookup"><span data-stu-id="d266e-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="d266e-153">有关**查看数据类**，选择**Mvc3Razor.Models.UserModel**。</span><span class="sxs-lookup"><span data-stu-id="d266e-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="d266e-154">(如果看不到**Mvc3Razor.Models.UserModel**中**查看数据类**框中，您需要生成项目。)请确保视图引擎设置为**Razor**。</span><span class="sxs-lookup"><span data-stu-id="d266e-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="d266e-155">设置**查看内容**到**列表**，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="d266e-155">Set **View content** to **List** and then click **Add**.</span></span>

![添加索引视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="d266e-157">新视图自动搭建基架以传递给的用户数据`Index`视图。</span><span class="sxs-lookup"><span data-stu-id="d266e-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="d266e-158">检查新生成*Views\Home\Index*文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="d266e-159">**创建新**，**编辑**，**详细信息**，以及**删除**链接不起作用，但页的其余部分将正常运行。</span><span class="sxs-lookup"><span data-stu-id="d266e-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="d266e-160">运行页。</span><span class="sxs-lookup"><span data-stu-id="d266e-160">Run the page.</span></span> <span data-ttu-id="d266e-161">请参阅用户的列表。</span><span class="sxs-lookup"><span data-stu-id="d266e-161">You see a list of users.</span></span>

![索引页](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="d266e-163">打开*Index.cshtml*文件，然后替换`ActionLink`标记**编辑**，**详细信息**，并**删除**用下面的代码:</span><span class="sxs-lookup"><span data-stu-id="d266e-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="d266e-164">用户名称用作 ID 查找中的所选的记录**编辑**，**详细信息**，并**删除**链接。</span><span class="sxs-lookup"><span data-stu-id="d266e-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="d266e-165">创建详细信息视图</span><span class="sxs-lookup"><span data-stu-id="d266e-165">Creating the Details View</span></span>

<span data-ttu-id="d266e-166">下一步是添加`Details`操作方法和视图以显示用户详细信息。</span><span class="sxs-lookup"><span data-stu-id="d266e-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="d266e-168">以下代码添加到`Details`向主控制器的方法：</span><span class="sxs-lookup"><span data-stu-id="d266e-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="d266e-169">内右击`Details`方法，然后选择<strong>添加视图</strong>。</span><span class="sxs-lookup"><span data-stu-id="d266e-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="d266e-170">确认<strong>查看数据类</strong>框中包含<strong>Mvc3Razor.Models.UserModel</strong><em>。</em></span><span class="sxs-lookup"><span data-stu-id="d266e-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="d266e-171">设置<strong>查看内容</strong>到<strong>详细信息</strong>，然后单击<strong>添加</strong>。</span><span class="sxs-lookup"><span data-stu-id="d266e-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![添加详细信息视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="d266e-173">运行应用程序并选择详细信息链接。</span><span class="sxs-lookup"><span data-stu-id="d266e-173">Run the application and select a details link.</span></span> <span data-ttu-id="d266e-174">自动基架显示模型中的每个属性。</span><span class="sxs-lookup"><span data-stu-id="d266e-174">The automatic scaffolding shows each property in the model.</span></span>

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="d266e-176">创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="d266e-176">Creating the Edit View</span></span>

<span data-ttu-id="d266e-177">以下代码添加到`Edit`向主控制器的方法。</span><span class="sxs-lookup"><span data-stu-id="d266e-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="d266e-178">添加一个视图，如下所示的上一步骤，但设置**查看内容**到**编辑**。</span><span class="sxs-lookup"><span data-stu-id="d266e-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![添加编辑视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="d266e-180">运行应用程序和编辑的一个用户的第一个和最后一个名称。</span><span class="sxs-lookup"><span data-stu-id="d266e-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="d266e-181">如果您违反`DataAnnotation`已应用于的约束`UserModel`类，当您提交窗体中，您将看到所生成的服务器代码的验证错误。</span><span class="sxs-lookup"><span data-stu-id="d266e-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="d266e-182">例如，如果您更改名字&quot;Ann&quot;到&quot;A&quot;，当您提交窗体中，在窗体上显示以下错误：</span><span class="sxs-lookup"><span data-stu-id="d266e-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="d266e-183">在本教程中，要将用户名称，视为主键。</span><span class="sxs-lookup"><span data-stu-id="d266e-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="d266e-184">因此，无法更改用户名属性。</span><span class="sxs-lookup"><span data-stu-id="d266e-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="d266e-185">在中*Edit.cshtml*文件，之后`Html.BeginForm`语句中，设置要隐藏的字段的用户名称。</span><span class="sxs-lookup"><span data-stu-id="d266e-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="d266e-186">这会导致要在模型中传递的属性。</span><span class="sxs-lookup"><span data-stu-id="d266e-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="d266e-187">以下代码片段演示的放置`Hidden`语句：</span><span class="sxs-lookup"><span data-stu-id="d266e-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="d266e-188">替换`TextBoxFor`并`ValidationMessageFor`标记的用户名称和`DisplayFor`调用。</span><span class="sxs-lookup"><span data-stu-id="d266e-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="d266e-189">`DisplayFor`方法显示的属性为只读的元素。</span><span class="sxs-lookup"><span data-stu-id="d266e-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="d266e-190">下面的示例显示了完成的标记。</span><span class="sxs-lookup"><span data-stu-id="d266e-190">The following example shows the completed markup.</span></span> <span data-ttu-id="d266e-191">原始`TextBoxFor`并`ValidationMessageFor`调用注释掉使用 Razor 注释开始和结束注释字符 (`@* *@`)</span><span class="sxs-lookup"><span data-stu-id="d266e-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="d266e-192">启用客户端验证</span><span class="sxs-lookup"><span data-stu-id="d266e-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="d266e-193">若要在 ASP.NET MVC 3 中的客户端验证，必须设置两个标记，并且必须包含三个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="d266e-194">打开应用程序的*Web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="d266e-195">验证是否`that ClientValidationEnabled`和`UnobtrusiveJavaScriptEnabled`设置为 true 的应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="d266e-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="d266e-196">以下片段中根*Web.config*文件显示了正确的设置：</span><span class="sxs-lookup"><span data-stu-id="d266e-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="d266e-197">设置`UnobtrusiveJavaScriptEnabled`为 true 启用非介入式 Ajax 和非介入式客户端验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="d266e-198">当您使用非介入式验证时，验证规则转变成 HTML5 属性。</span><span class="sxs-lookup"><span data-stu-id="d266e-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="d266e-199">HTML5 属性名称可以包含小写字母、 数字和短划线。</span><span class="sxs-lookup"><span data-stu-id="d266e-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="d266e-200">设置`ClientValidationEnabled`为 true，则启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="d266e-201">通过在应用程序中设置这些密钥*Web.config*文件中，启用客户端验证和整个应用程序的非介入式 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="d266e-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="d266e-202">您还可以启用或禁用这些设置在单个视图中或在控制器方法中使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="d266e-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="d266e-203">此外需要在呈现的视图中包含多个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="d266e-204">若要在所有视图中包括 JavaScript 的简单方法是将其添加到*views/shared\\_Layout.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="d266e-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="d266e-205">替换`<head>`的元素 *\_Layout.cshtml*文件使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="d266e-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="d266e-206">前两个 jQuery 脚本托管的 Microsoft Ajax 内容交付网络 (CDN)。</span><span class="sxs-lookup"><span data-stu-id="d266e-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="d266e-207">通过利用 Microsoft Ajax CDN，可以显著提高你的应用程序的第一个命中性能。</span><span class="sxs-lookup"><span data-stu-id="d266e-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="d266e-208">运行应用程序，并单击编辑链接。</span><span class="sxs-lookup"><span data-stu-id="d266e-208">Run the application and click an edit link.</span></span> <span data-ttu-id="d266e-209">在浏览器中查看页面的源。</span><span class="sxs-lookup"><span data-stu-id="d266e-209">View the page's source in the browser.</span></span> <span data-ttu-id="d266e-210">浏览器源将显示在窗体的多个属性`data-val`（用于数据验证）。</span><span class="sxs-lookup"><span data-stu-id="d266e-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="d266e-211">当启用了客户端验证和非介入式 JavaScript 时，与客户端验证规则的输入的字段包含`data-val="true"`属性触发非介入式客户端验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="d266e-212">例如，`City`模型中的字段使用修饰[所需](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性，这会导致以下示例所示的 HTML:</span><span class="sxs-lookup"><span data-stu-id="d266e-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="d266e-213">对于每个客户端验证规则，将添加属性，其形式`data-val-rulename="message"`。</span><span class="sxs-lookup"><span data-stu-id="d266e-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="d266e-214">使用`City`更早版本，显示所需的客户端验证规则将生成的字段示例`data-val-required`属性和消息&quot;City 字段是必填&quot;。</span><span class="sxs-lookup"><span data-stu-id="d266e-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="d266e-215">运行应用程序，编辑一个用户，并清除`City`字段。</span><span class="sxs-lookup"><span data-stu-id="d266e-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="d266e-216">当您 tab 键跳出字段时，您将看到客户端验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="d266e-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![所需的城市](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="d266e-218">同样，对于客户端验证规则中每个参数，将添加属性，其形式`data-val-rulename-paramname=paramvalue`。</span><span class="sxs-lookup"><span data-stu-id="d266e-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="d266e-219">例如，`FirstName`属性将批注[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性，并指定 3 的最小长度和最大长度为 8。</span><span class="sxs-lookup"><span data-stu-id="d266e-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="d266e-220">名为的数据验证规则`length`具有参数的名称`max`和参数值 8。</span><span class="sxs-lookup"><span data-stu-id="d266e-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="d266e-221">下面的示例演示为生成的 HTML`FirstName`字段的一个用户编辑时：</span><span class="sxs-lookup"><span data-stu-id="d266e-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="d266e-222">有关非介入式客户端验证的详细信息，请参阅文章[在 ASP.NET MVC 3 中的非介入式客户端验证](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)Brad Wilson 的博客中。</span><span class="sxs-lookup"><span data-stu-id="d266e-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="d266e-223">在 ASP.NET MVC 3 Beta，有时需要提交窗体，以便启动客户端验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="d266e-224">这可能会更改的最终版本。</span><span class="sxs-lookup"><span data-stu-id="d266e-224">This might be changed for the final release.</span></span>


## <a name="creating-the-create-view"></a><span data-ttu-id="d266e-225">创建创建视图</span><span class="sxs-lookup"><span data-stu-id="d266e-225">Creating the Create View</span></span>

<span data-ttu-id="d266e-226">下一步是添加`Create`操作方法和视图以使用户能够创建新的用户。</span><span class="sxs-lookup"><span data-stu-id="d266e-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="d266e-227">以下代码添加到`Create`向主控制器的方法：</span><span class="sxs-lookup"><span data-stu-id="d266e-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="d266e-228">添加一个视图，如下所示的上一步骤，但设置**查看内容**到**创建**。</span><span class="sxs-lookup"><span data-stu-id="d266e-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![创建视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="d266e-230">运行应用程序中，选择**创建**链接，并添加新用户。</span><span class="sxs-lookup"><span data-stu-id="d266e-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="d266e-231">`Create`方法自动利用的客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="d266e-232">尝试输入的用户名称，包含空格，如&quot;Ben X&quot;。</span><span class="sxs-lookup"><span data-stu-id="d266e-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="d266e-233">当带用户名称字段中，客户端验证错误选项卡 (`White space is not allowed`) 显示。</span><span class="sxs-lookup"><span data-stu-id="d266e-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="d266e-234">添加 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="d266e-234">Add the Delete method</span></span>

<span data-ttu-id="d266e-235">若要完成本教程，添加以下`Delete`向主控制器的方法：</span><span class="sxs-lookup"><span data-stu-id="d266e-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="d266e-236">添加`Delete`视图，如前面的步骤，设置中所示**查看内容**到**删除**。</span><span class="sxs-lookup"><span data-stu-id="d266e-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![删除视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="d266e-238">现可简单但功能完备的 ASP.NET MVC 3 应用程序，进行验证。</span><span class="sxs-lookup"><span data-stu-id="d266e-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
