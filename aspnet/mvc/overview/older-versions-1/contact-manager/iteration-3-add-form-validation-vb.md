---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '迭代 #3 – 添加窗体验证 (VB) |Microsoft 文档'
author: microsoft
description: 在第三个迭代中，我们将添加基本窗体验证。 我们可以防止人员提交窗体，但不完成需要的表单域。 我们还验证 emai...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 8e30e247bd31dfb800eea517d195025f9e881cd3
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="e4a6c-105">迭代 #3 – 添加窗体验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="e4a6c-105">Iteration #3 – Add form validation (VB)</span></span>
====================
<span data-ttu-id="e4a6c-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e4a6c-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e4a6c-107">下载代码</span><span class="sxs-lookup"><span data-stu-id="e4a6c-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="e4a6c-108">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="e4a6c-109">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="e4a6c-110">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="e4a6c-111">生成联系人管理 ASP.NET MVC 应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="e4a6c-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="e4a6c-112">在这一系列的教程，我们生成整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="e4a6c-113">联系人管理器应用程序，可存储的名称，电话号码和电子邮件地址的联系人信息有关的人员列表。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="e4a6c-114">我们在多次迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="e4a6c-115">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="e4a6c-116">此多个迭代方法旨在使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="e4a6c-117">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="e4a6c-118">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="e4a6c-119">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="e4a6c-120">迭代 #2-使应用程序，看上去很好。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="e4a6c-121">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="e4a6c-122">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="e4a6c-123">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="e4a6c-124">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="e4a6c-125">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="e4a6c-126">迭代 #4-请松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="e4a6c-127">在此第三个迭代中，我们利用多个软件设计模式以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-127">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="e4a6c-128">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="e4a6c-129">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="e4a6c-130">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="e4a6c-131">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="e4a6c-132">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="e4a6c-133">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="e4a6c-134">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="e4a6c-135">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="e4a6c-136">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="e4a6c-137">此迭代</span><span class="sxs-lookup"><span data-stu-id="e4a6c-137">This Iteration</span></span>

<span data-ttu-id="e4a6c-138">此第二个迭代中的联系人管理器应用程序，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="e4a6c-139">我们可以防止人员而无需为所需的窗体字段中输入值提交联系人。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="e4a6c-140">我们还验证电话号码和电子邮件地址 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="e4a6c-141">[![新项目对话框](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e4a6c-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="e4a6c-142">**图 01**： 带有验证的窗体 ([单击以查看实际尺寸的图像](iteration-3-add-form-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="e4a6c-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>


<span data-ttu-id="e4a6c-143">在此迭代中，我们直接向控制器操作添加验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="e4a6c-144">一般情况下，这不是将验证添加到 ASP.NET MVC 应用程序的建议的方法。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="e4a6c-145">更好的方法是将在单独的应用程序的验证逻辑[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="e4a6c-146">在下一步的迭代中，我们将重构联系人管理器应用程序，使应用程序更易于维护。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="e4a6c-147">在此迭代中，若要为简便起见，我们编写验证代码的所有手动。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="e4a6c-148">而不是自己编写验证代码，我们无法充分利用验证框架。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="e4a6c-149">例如，可以使用 Microsoft 企业库验证应用程序块 (VAB) 为你的 ASP.NET MVC 应用程序中实现验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="e4a6c-150">若要了解有关验证应用程序块的详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="e4a6c-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="e4a6c-151">将验证添加到创建视图</span><span class="sxs-lookup"><span data-stu-id="e4a6c-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="e4a6c-152">让我们来开始通过将验证逻辑添加到创建视图。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="e4a6c-153">幸运的是，由于我们生成具有 Visual Studio 的创建视图，创建视图已包含的所有必要的用户界面逻辑，以显示验证消息。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="e4a6c-154">列表 1 中包含创建视图。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="e4a6c-155">**列表 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="e4a6c-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="e4a6c-156">字段验证错误类用于设置样式的 Html.ValidationMessage() 帮助程序呈现的输出。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="e4a6c-157">输入验证错误类用于设置样式呈现 Html.TextBox() 帮助程序文本框中 （输入）。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="e4a6c-158">验证摘要错误类用于设置样式呈现 Html.ValidationSummary() 帮助程序未经排序的列表。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e4a6c-159">你可以修改自定义的验证错误消息的外观此部分中所述的样式表类。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="e4a6c-160">添加验证逻辑，以创建操作</span><span class="sxs-lookup"><span data-stu-id="e4a6c-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="e4a6c-161">现在，创建视图永远不会显示验证错误消息，因为我们不可以编写逻辑来生成任何消息。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="e4a6c-162">若要显示验证错误消息，你需要向 ModelState 添加错误消息。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e4a6c-163">UpdateModel() 方法将错误消息添加到 ModelState 自动错误的表单域的值分配到属性时。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="e4a6c-164">例如，如果你尝试将字符串"apple"分配到的出生日期属性。 接受 DateTime 值，然后 UpdateModel() 方法将错误添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="e4a6c-165">列出 2 中修改后的 create （） 方法包含一个新部分，将新的联系人插入到数据库之前验证联系人类的属性。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="e4a6c-166">**列出 2-Controllers\ContactController.vb （创建与验证）**</span><span class="sxs-lookup"><span data-stu-id="e4a6c-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="e4a6c-167">验证部分强制执行四个不同的验证规则：</span><span class="sxs-lookup"><span data-stu-id="e4a6c-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="e4a6c-168">FirstName 属性必须大于零的长度 （和它不能只由空格）</span><span class="sxs-lookup"><span data-stu-id="e4a6c-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="e4a6c-169">LastName 属性必须大于零的长度 （和它不能只由空格）</span><span class="sxs-lookup"><span data-stu-id="e4a6c-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="e4a6c-170">如果电话属性的值 （长度大于 0） 则 Phone 属性必须与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="e4a6c-171">如果电子邮件属性的值 （长度大于 0） 则电子邮件属性必须与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="e4a6c-172">如果没有验证规则违规，则将一条错误消息添加到 ModelState AddModelError() 方法的帮助。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="e4a6c-173">当你将一条消息添加到 ModelState 时，需要提供属性的名称和验证错误消息的文本。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="e4a6c-174">Html.ValidationSummary() 和 Html.ValidationMessage() 帮助器方法的情况下，此错误消息显示在视图中。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="e4a6c-175">执行验证规则后，将检查 ModelState IsValid 属性。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="e4a6c-176">在任意验证错误消息添加到 ModelState 后，IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="e4a6c-177">如果验证失败，则会将创建表单重新显示的错误消息。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e4a6c-178">我收到了用于验证在正则表达式存储库中的电话号码和电子邮件地址的正则表达式 [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="e4a6c-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="e4a6c-179">将验证逻辑添加到的编辑操作</span><span class="sxs-lookup"><span data-stu-id="e4a6c-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="e4a6c-180">Edit （） 操作会更新联系人。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="e4a6c-181">Edit （） 操作必须执行的 create （） 操作的验证完全相同。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="e4a6c-182">而不是复制相同的验证代码时，我们应重构联系人控制器以便 create （） 和 edit （） 操作调用相同的验证方法。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="e4a6c-183">修改的联系人控制器类包含在清单 3。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="e4a6c-184">此类已在 create （） 和 edit （） 操作中调用的新 ValidateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="e4a6c-185">**Listing 3 - Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="e4a6c-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="e4a6c-186">总结</span><span class="sxs-lookup"><span data-stu-id="e4a6c-186">Summary</span></span>

<span data-ttu-id="e4a6c-187">在此迭代中，我们将添加基本窗体验证到我们的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="e4a6c-188">我们验证逻辑阻止用户提交新的联系人或编辑现有联系人，无需提供 FirstName 和 LastName 属性的值。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="e4a6c-189">此外，用户必须提供有效的电话号码和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="e4a6c-190">在此迭代中，我们添加验证逻辑到我们的联系人管理器应用程序中可能的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="e4a6c-191">但是，到我们控制器逻辑混合我们验证逻辑将问题为创建我们在长期内。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="e4a6c-192">我们的应用程序将会更加难以维护，并随着时间的推移修改。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="e4a6c-193">在下一步的迭代中，我们将重构我们的验证逻辑和数据库访问逻辑外我们控制器。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="e4a6c-194">我们将充分利用多个软件设计原则，以便能够创建一个更松散耦合，且更易于维护，应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4a6c-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e4a6c-195">[上一页](iteration-2-make-the-application-look-nice-vb.md)
> [下一页](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="e4a6c-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
