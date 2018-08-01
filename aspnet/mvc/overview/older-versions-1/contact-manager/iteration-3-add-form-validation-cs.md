---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 迭代 3 – 添加表单验证 (C#) |Microsoft Docs
author: microsoft
description: 在第三个迭代中，我们将添加基本窗体验证。 我们阻止用户提交窗体而无法完成所需的窗体字段。 我们还验证 emai...
ms.author: aspnetcontent
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: d7f5d183b98ea123a780714dec2d806e4e794c2d
ms.sourcegitcommit: a25b572eaed21791230c85416f449f66a405ec19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2018
ms.locfileid: "39396071"
---
<a name="iteration-3--add-form-validation-c"></a><span data-ttu-id="220ce-105">迭代 3 – 添加表单验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="220ce-105">Iteration #3 – Add form validation (C#)</span></span>
====================
<span data-ttu-id="220ce-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="220ce-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="220ce-107">下载代码</span><span class="sxs-lookup"><span data-stu-id="220ce-107">Download Code</span></span>](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> <span data-ttu-id="220ce-108">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="220ce-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="220ce-109">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="220ce-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="220ce-110">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="220ce-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="220ce-111">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="220ce-111">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="220ce-112">在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="220ce-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="220ce-113">联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。</span><span class="sxs-lookup"><span data-stu-id="220ce-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="220ce-114">我们通过多个迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="220ce-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="220ce-115">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="220ce-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="220ce-116">此多个迭代方法的目标是帮助你了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="220ce-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="220ce-117">迭代 1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="220ce-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="220ce-118">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="220ce-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="220ce-119">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="220ce-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="220ce-120">迭代 2 – 使应用程序看上去更美观。</span><span class="sxs-lookup"><span data-stu-id="220ce-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="220ce-121">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="220ce-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="220ce-122">迭代 3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="220ce-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="220ce-123">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="220ce-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="220ce-124">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="220ce-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="220ce-125">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="220ce-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="220ce-126">迭代 4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="220ce-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="220ce-127">在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="220ce-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="220ce-128">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="220ce-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="220ce-129">迭代 5 — 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="220ce-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="220ce-130">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="220ce-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="220ce-131">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="220ce-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="220ce-132">迭代 6-使用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="220ce-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="220ce-133">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="220ce-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="220ce-134">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="220ce-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="220ce-135">迭代 7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="220ce-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="220ce-136">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="220ce-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="220ce-137">此迭代</span><span class="sxs-lookup"><span data-stu-id="220ce-137">This Iteration</span></span>

<span data-ttu-id="220ce-138">在联系人管理器应用程序的此第二个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="220ce-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="220ce-139">我们阻止用户提交联系人而无需为所需的窗体字段输入值。</span><span class="sxs-lookup"><span data-stu-id="220ce-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="220ce-140">我们还验证电话号码和电子邮件地址 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="220ce-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="220ce-141">[![新建项目对话框](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="220ce-141">[![The New Project dialog box](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="220ce-142">**图 01**： 带有验证的窗体 ([单击以查看实际尺寸的图像](iteration-3-add-form-validation-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="220ce-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-cs/_static/image2.png))</span></span>


<span data-ttu-id="220ce-143">在此迭代中，我们直接向控制器操作添加验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="220ce-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="220ce-144">一般情况下，这不是将验证添加到 ASP.NET MVC 应用程序的建议的方法。</span><span class="sxs-lookup"><span data-stu-id="220ce-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="220ce-145">更好的方法是将应用程序的验证逻辑放在单独[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)。</span><span class="sxs-lookup"><span data-stu-id="220ce-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="220ce-146">在下一个迭代中，我们将重构要使应用程序更易于维护的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="220ce-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="220ce-147">在此迭代中，为简便起见，我们编写验证代码的所有手动。</span><span class="sxs-lookup"><span data-stu-id="220ce-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="220ce-148">而不是自己编写验证代码，我们无法充分利用验证框架。</span><span class="sxs-lookup"><span data-stu-id="220ce-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="220ce-149">例如，可以使用 Microsoft 企业库验证应用程序块 (VAB) 要为 ASP.NET MVC 应用程序中实现验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="220ce-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="220ce-150">若要了解有关验证应用程序块的详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="220ce-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="220ce-151">将验证添加到 Create 视图</span><span class="sxs-lookup"><span data-stu-id="220ce-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="220ce-152">让我们来首先将验证逻辑添加到 Create 视图。</span><span class="sxs-lookup"><span data-stu-id="220ce-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="220ce-153">幸运的是，由于我们生成的 Create 视图使用 Visual Studio，创建视图已包含的所有必要的用户界面逻辑，以显示验证消息。</span><span class="sxs-lookup"><span data-stu-id="220ce-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="220ce-154">在列表 1 中包含创建视图。</span><span class="sxs-lookup"><span data-stu-id="220ce-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="220ce-155">**代码清单 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="220ce-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

<span data-ttu-id="220ce-156">请注意，正上方的 HTML 窗体的 Html.ValidationSummary() 帮助器方法的调用。</span><span class="sxs-lookup"><span data-stu-id="220ce-156">Notice the call to the Html.ValidationSummary() helper method that appears immediately above the HTML form.</span></span> <span data-ttu-id="220ce-157">如果有验证错误消息，此方法对项目符号列表中显示验证消息。</span><span class="sxs-lookup"><span data-stu-id="220ce-157">If there are validation error messages, then this method displays validation messages in a bulleted list.</span></span>

<span data-ttu-id="220ce-158">请注意，此外，每个窗体字段旁边显示对 Html.ValidationMessage() 的调用。</span><span class="sxs-lookup"><span data-stu-id="220ce-158">Notice, furthermore, the calls to Html.ValidationMessage() that appear next to each form field.</span></span> <span data-ttu-id="220ce-159">ValidationMessage() 帮助器显示各自的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="220ce-159">The ValidationMessage() helper displays an individual validation error message.</span></span> <span data-ttu-id="220ce-160">在列表 1 中，验证错误时显示一个星号。</span><span class="sxs-lookup"><span data-stu-id="220ce-160">In the case of Listing 1, an asterisk is displayed when there is a validation error.</span></span>

<span data-ttu-id="220ce-161">最后，Html.TextBox() 帮助程序会自动呈现的级联样式表类与显示的帮助程序属性关联的验证错误时。</span><span class="sxs-lookup"><span data-stu-id="220ce-161">Finally, the Html.TextBox() helper automatically renders a Cascading Style Sheet class when there is a validation error associated with the property displayed by the helper.</span></span> <span data-ttu-id="220ce-162">Html.TextBox() 帮助器将呈现一个名为类**输入验证错误**。</span><span class="sxs-lookup"><span data-stu-id="220ce-162">The Html.TextBox() helper renders a class named **input-validation-error**.</span></span>

<span data-ttu-id="220ce-163">当创建新的 ASP.NET MVC 应用程序时，名为 Site.css 的样式表是自动创建的内容文件夹中。</span><span class="sxs-lookup"><span data-stu-id="220ce-163">When you create a new ASP.NET MVC application, a style sheet named Site.css is created in the Content folder automatically.</span></span> <span data-ttu-id="220ce-164">此样式表包含相关的验证错误消息外观的 CSS 类的以下定义：</span><span class="sxs-lookup"><span data-stu-id="220ce-164">This style sheet contains the following definitions for CSS classes related to the appearance of validation error messages:</span></span>

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

<span data-ttu-id="220ce-165">字段验证错误类用于设置样式由 Html.ValidationMessage() 帮助器呈现的输出。</span><span class="sxs-lookup"><span data-stu-id="220ce-165">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="220ce-166">输入验证错误类用于设置样式由 Html.TextBox() 帮助器呈现的文本框 （输入）。</span><span class="sxs-lookup"><span data-stu-id="220ce-166">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="220ce-167">验证摘要错误类用于设置样式呈现 Html.ValidationSummary() 帮助程序的未排序的列表。</span><span class="sxs-lookup"><span data-stu-id="220ce-167">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="220ce-168">您可以修改自定义验证错误消息的外观此部分中所述的样式表类。</span><span class="sxs-lookup"><span data-stu-id="220ce-168">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="220ce-169">添加到的验证逻辑创建操作</span><span class="sxs-lookup"><span data-stu-id="220ce-169">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="220ce-170">现在，创建视图永远不会显示验证错误消息，因为我们不编写逻辑来生成的任何消息。</span><span class="sxs-lookup"><span data-stu-id="220ce-170">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="220ce-171">为了显示验证错误消息，您需要错误消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="220ce-171">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="220ce-172">UpdateModel() 方法将错误消息添加到 ModelState 自动错误窗体字段的值分配到属性时。</span><span class="sxs-lookup"><span data-stu-id="220ce-172">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="220ce-173">例如，如果尝试将字符串"apple"分配给接受的日期时间值的 BirthDate 属性，然后 UpdateModel() 方法向错误 ModelState。</span><span class="sxs-lookup"><span data-stu-id="220ce-173">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="220ce-174">代码清单 2 中的已修改 create （） 方法包含新的联系人插入到数据库之前会验证 Contact 类的属性的新部分。</span><span class="sxs-lookup"><span data-stu-id="220ce-174">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="220ce-175">**代码清单 2-Controllers\ContactController.cs （创建于验证）**</span><span class="sxs-lookup"><span data-stu-id="220ce-175">**Listing 2 - Controllers\ContactController.cs (Create with validation)**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

<span data-ttu-id="220ce-176">验证部分会强制执行四个不同的验证规则：</span><span class="sxs-lookup"><span data-stu-id="220ce-176">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="220ce-177">FirstName 属性必须具有的长度大于零 （和它不能只由空格）</span><span class="sxs-lookup"><span data-stu-id="220ce-177">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="220ce-178">姓氏属性必须具有的长度大于零 （和它不能只由空格）</span><span class="sxs-lookup"><span data-stu-id="220ce-178">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="220ce-179">如果电话属性具有值 （具有的长度大于 0） 则 Phone 属性必须与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="220ce-179">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="220ce-180">如果电子邮件属性具有值 （具有的长度大于 0） 则电子邮件属性必须与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="220ce-180">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="220ce-181">如果验证规则冲突，则将一条错误消息添加到 ModelState AddModelError() 方法的帮助。</span><span class="sxs-lookup"><span data-stu-id="220ce-181">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="220ce-182">时向 ModelState 添加一条消息，提供的属性名称和验证错误消息的文本。</span><span class="sxs-lookup"><span data-stu-id="220ce-182">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="220ce-183">Html.ValidationSummary() 和 Html.ValidationMessage() 帮助器方法的情况下，此错误消息显示在视图中。</span><span class="sxs-lookup"><span data-stu-id="220ce-183">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="220ce-184">执行验证规则后，检查 ModelState IsValid 属性。</span><span class="sxs-lookup"><span data-stu-id="220ce-184">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="220ce-185">当任何验证错误消息都已添加到 ModelState IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="220ce-185">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="220ce-186">如果验证失败，错误消息与重新创建窗体。</span><span class="sxs-lookup"><span data-stu-id="220ce-186">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="220ce-187">我收到了用于验证的正则表达式存储库中的电话号码和电子邮件地址的正则表达式 [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="220ce-187">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="220ce-188">将验证逻辑添加到编辑操作</span><span class="sxs-lookup"><span data-stu-id="220ce-188">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="220ce-189">Edit （） 操作更新联系人。</span><span class="sxs-lookup"><span data-stu-id="220ce-189">The Edit() action updates a Contact.</span></span> <span data-ttu-id="220ce-190">Edit （） 操作需要对其执行完全相同的验证作为 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="220ce-190">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="220ce-191">而不是重复相同的验证代码，我们应重构联系人控制器以便 create （） 和 edit （） 操作调用相同的验证方法。</span><span class="sxs-lookup"><span data-stu-id="220ce-191">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="220ce-192">修改后的 Contact 控制器类都包含在清单 3。</span><span class="sxs-lookup"><span data-stu-id="220ce-192">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="220ce-193">此类有一个新的 ValidateContact() 方法调用中的 create （） 和 edit （） 操作。</span><span class="sxs-lookup"><span data-stu-id="220ce-193">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="220ce-194">**代码清单 3-Controllers\ContactController.cs**</span><span class="sxs-lookup"><span data-stu-id="220ce-194">**Listing 3 - Controllers\ContactController.cs**</span></span>

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a><span data-ttu-id="220ce-195">总结</span><span class="sxs-lookup"><span data-stu-id="220ce-195">Summary</span></span>

<span data-ttu-id="220ce-196">在此迭代中，我们添加到我们的联系人管理器应用程序基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="220ce-196">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="220ce-197">我们的验证逻辑可阻止用户提交新的联系人或编辑现有联系人，无需提供的 FirstName 和 LastName 属性的值。</span><span class="sxs-lookup"><span data-stu-id="220ce-197">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="220ce-198">此外，用户必须提供有效的电话号码和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="220ce-198">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="220ce-199">在此迭代中，我们添加验证逻辑到我们的联系人管理器应用程序中可能的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="220ce-199">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="220ce-200">但是，到我们的控制器逻辑混合我们验证逻辑将创建问题对我们在长期内。</span><span class="sxs-lookup"><span data-stu-id="220ce-200">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="220ce-201">我们的应用程序将会更难维护和随着时间的推移修改。</span><span class="sxs-lookup"><span data-stu-id="220ce-201">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="220ce-202">在下一个迭代中，我们将带我们控制器重构我们的验证逻辑和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="220ce-202">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="220ce-203">我们将充分利用多个软件设计原则，使我们能够创建一个更松散耦合，且更易于维护，应用程序。</span><span class="sxs-lookup"><span data-stu-id="220ce-203">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="220ce-204">[上一页](iteration-2-make-the-application-look-nice-cs.md)
> [下一页](iteration-4-make-the-application-loosely-coupled-cs.md)</span><span class="sxs-lookup"><span data-stu-id="220ce-204">[Previous](iteration-2-make-the-application-look-nice-cs.md)
[Next](iteration-4-make-the-application-loosely-coupled-cs.md)</span></span>
