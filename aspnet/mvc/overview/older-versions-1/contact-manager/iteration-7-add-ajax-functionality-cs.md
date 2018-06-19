---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
title: '迭代 #7-添加 Ajax 功能 (C#) |Microsoft 文档'
author: microsoft
description: 在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: f1b0809e-8909-444e-b6bb-a5cd1dea3f72
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
msc.type: authoredcontent
ms.openlocfilehash: 35d62383a571725749b2fc629bbb17954657b2f6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30875521"
---
<a name="iteration-7--add-ajax-functionality-c"></a><span data-ttu-id="88265-103">迭代 #7-添加 Ajax 功能 (C#)</span><span class="sxs-lookup"><span data-stu-id="88265-103">Iteration #7 – Add Ajax functionality (C#)</span></span>
====================
<span data-ttu-id="88265-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="88265-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="88265-105">下载代码</span><span class="sxs-lookup"><span data-stu-id="88265-105">Download Code</span></span>](iteration-7-add-ajax-functionality-cs/_static/contactmanager_7_cs1.zip)

> <span data-ttu-id="88265-106">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="88265-106">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="88265-107">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="88265-107">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="88265-108">在这一系列的教程，我们生成整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="88265-108">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="88265-109">联系人管理器应用程序，可存储的名称，电话号码和电子邮件地址的联系人信息有关的人员列表。</span><span class="sxs-lookup"><span data-stu-id="88265-109">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="88265-110">我们在多次迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-110">We build the application over multiple iterations.</span></span> <span data-ttu-id="88265-111">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-111">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="88265-112">此多个迭代方法旨在使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="88265-112">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="88265-113">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-113">Iteration #1 - Create the application.</span></span> <span data-ttu-id="88265-114">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="88265-114">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="88265-115">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="88265-115">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="88265-116">迭代 #2-使应用程序，看上去很好。</span><span class="sxs-lookup"><span data-stu-id="88265-116">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="88265-117">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="88265-117">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="88265-118">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="88265-118">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="88265-119">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="88265-119">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="88265-120">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="88265-120">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="88265-121">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="88265-121">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="88265-122">迭代 #4-请松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-122">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="88265-123">在此第三个迭代中，我们利用多个软件设计模式以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-123">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="88265-124">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="88265-124">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="88265-125">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="88265-125">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="88265-126">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="88265-126">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="88265-127">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="88265-127">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="88265-128">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="88265-128">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="88265-129">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="88265-129">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="88265-130">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="88265-130">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="88265-131">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="88265-131">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="88265-132">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="88265-132">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="88265-133">此迭代</span><span class="sxs-lookup"><span data-stu-id="88265-133">This Iteration</span></span>

<span data-ttu-id="88265-134">此迭代中的联系人管理器应用程序，我们将重构应用程序以利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="88265-134">In this iteration of the Contact Manager application, we refactor our application to make use of Ajax.</span></span> <span data-ttu-id="88265-135">通过利用 Ajax，我们使我们的应用程序更快地响应。</span><span class="sxs-lookup"><span data-stu-id="88265-135">By taking advantage of Ajax, we make our application more responsive.</span></span> <span data-ttu-id="88265-136">我们可以避免当我们需要更新某些区域在页面呈现整个页面。</span><span class="sxs-lookup"><span data-stu-id="88265-136">We can avoid rendering an entire page when we need to update only a certain region in a page.</span></span>

<span data-ttu-id="88265-137">以便我们不需要以重新显示整个页面，每当有人选择新的联系人组时，我们将重构我们索引视图。</span><span class="sxs-lookup"><span data-stu-id="88265-137">We'll refactor our Index view so that we don t need to redisplay the entire page whenever someone selects a new contact group.</span></span> <span data-ttu-id="88265-138">相反，当有人单击联系人的组时，我们将只需更新联系人的列表并保留单独网页的其余内容。</span><span class="sxs-lookup"><span data-stu-id="88265-138">Instead, when someone clicks a contact group, we'll just update the list of contacts and leave the rest of the page alone.</span></span>

<span data-ttu-id="88265-139">我们还将更改我们删除链接的工作原理的方式。</span><span class="sxs-lookup"><span data-stu-id="88265-139">We'll also change the way our delete link works.</span></span> <span data-ttu-id="88265-140">而不是显示一个单独的确认页面，我们将显示一个 JavaScript 确认对话框。</span><span class="sxs-lookup"><span data-stu-id="88265-140">Instead of displaying a separate confirmation page, we'll display a JavaScript confirmation dialog.</span></span> <span data-ttu-id="88265-141">如果你确认你想要删除联系人，针对要从数据库中删除联系人记录的服务器执行 HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="88265-141">If you confirm that you want to delete a contact, an HTTP DELETE operation is performed against the server to delete the contact record from the database.</span></span>

<span data-ttu-id="88265-142">此外，我们将利用 jQuery 将动画效果添加到我们的索引视图。</span><span class="sxs-lookup"><span data-stu-id="88265-142">Furthermore, we will take advantage of jQuery to add animation effects to our Index view.</span></span> <span data-ttu-id="88265-143">正在从服务器提取新的联系人列表时，我们将显示一种动画效果。</span><span class="sxs-lookup"><span data-stu-id="88265-143">We'll display an animation when the new list of contacts is being fetched from the server.</span></span>

<span data-ttu-id="88265-144">最后，我们将利用 ASP.NET AJAX 框架支持用于管理浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="88265-144">Finally, we'll take advantage of the ASP.NET AJAX framework support for managing browser history.</span></span> <span data-ttu-id="88265-145">每当我们执行通过 Ajax 调用才能更新联系人的列表，我们将创建历史时间点。</span><span class="sxs-lookup"><span data-stu-id="88265-145">We'll create history points whenever we perform an Ajax call to update the contact list.</span></span> <span data-ttu-id="88265-146">这样一来，浏览器向后和向前按钮将工作。</span><span class="sxs-lookup"><span data-stu-id="88265-146">That way, the browser backward and forward buttons will work.</span></span>

## <a name="why-use-ajax"></a><span data-ttu-id="88265-147">为何使用 Ajax？</span><span class="sxs-lookup"><span data-stu-id="88265-147">Why use Ajax?</span></span>

<span data-ttu-id="88265-148">使用 Ajax 具有诸多优点。</span><span class="sxs-lookup"><span data-stu-id="88265-148">Using Ajax has many benefits.</span></span> <span data-ttu-id="88265-149">首先，将 Ajax 功能添加到应用程序将导致更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="88265-149">First, adding Ajax functionality to an application results in a better user experience.</span></span> <span data-ttu-id="88265-150">在普通的 web 应用程序中，整个页面必须要回发到服务器每个用户执行的操作的时间。</span><span class="sxs-lookup"><span data-stu-id="88265-150">In a normal web application, the entire page must be posted back to the server each and every time a user performs an action.</span></span> <span data-ttu-id="88265-151">每当执行操作时，浏览器锁和用户必须等待，直到提取和重新显示整个页面。</span><span class="sxs-lookup"><span data-stu-id="88265-151">Whenever you perform an action, the browser locks and the user must wait until the entire page is fetched and redisplayed.</span></span>

<span data-ttu-id="88265-152">这将是不可接受的体验，对于桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-152">This would be an unacceptable experience in the case of a desktop application.</span></span> <span data-ttu-id="88265-153">但是，传统上，我们留存与在 web 应用程序的情况下此不良用户体验因为我们不知道，我们无法执行任何好。</span><span class="sxs-lookup"><span data-stu-id="88265-153">But, traditionally, we lived with this bad user experience in the case of a web application because we did not know that we could do any better.</span></span> <span data-ttu-id="88265-154">我们认为它是 web 应用程序的限制时，在现实中，它只是我们想象力的限制。</span><span class="sxs-lookup"><span data-stu-id="88265-154">We thought it was a limitation of web applications when, in actuality, it was just a limitation of our imaginations.</span></span>

<span data-ttu-id="88265-155">在 Ajax 应用程序，您不需要以使异常终止只是为了将更新页面的用户体验。</span><span class="sxs-lookup"><span data-stu-id="88265-155">In an Ajax application, you don t need to bring the user experience to a halt just to update a page.</span></span> <span data-ttu-id="88265-156">相反，您可以在后台以更新的页面中执行的异步请求。</span><span class="sxs-lookup"><span data-stu-id="88265-156">Instead, you can perform an asynchronous request in the background to update the page.</span></span> <span data-ttu-id="88265-157">您不 t 强制用户等待获取更新页面的一部分时。</span><span class="sxs-lookup"><span data-stu-id="88265-157">You don t force the user to wait while part of the page gets updated.</span></span>

<span data-ttu-id="88265-158">通过利用 Ajax，您还可以改善你的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="88265-158">By taking advantage of Ajax, you also can improve the performance of your application.</span></span> <span data-ttu-id="88265-159">请考虑联系人管理器应用程序工作原理稍后再试而无需将 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="88265-159">Consider how the Contact Manager application works right now without Ajax functionality.</span></span> <span data-ttu-id="88265-160">单击联系人的组时，整个索引视图必须重新显示。</span><span class="sxs-lookup"><span data-stu-id="88265-160">When you click a contact group, the entire Index view must be redisplayed.</span></span> <span data-ttu-id="88265-161">必须从数据库服务器检索的联系人列表和联系人的组的列表。</span><span class="sxs-lookup"><span data-stu-id="88265-161">The list of contacts and list of contact groups must be retrieved from the database server.</span></span> <span data-ttu-id="88265-162">所有这些数据必须传递跨网络从 web 服务器为 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="88265-162">All of this data must be passed across the wire from web server to web browser.</span></span>

<span data-ttu-id="88265-163">我们将 Ajax 功能添加到我们的应用程序之后，但是，我们可以避免重新显示整个页面，当用户单击联系人的组。</span><span class="sxs-lookup"><span data-stu-id="88265-163">After we add Ajax functionality to our application, however, we can avoid redisplaying the entire page when a user clicks a contact group.</span></span> <span data-ttu-id="88265-164">我们不再需要获取从数据库联系人的组。</span><span class="sxs-lookup"><span data-stu-id="88265-164">We no longer need to grab the contact groups from the database.</span></span> <span data-ttu-id="88265-165">我们还不 t 需要将整个索引视图推送到网络。</span><span class="sxs-lookup"><span data-stu-id="88265-165">We also don t need to push the entire Index view across the wire.</span></span> <span data-ttu-id="88265-166">通过利用 Ajax，我们减少的我们的数据库服务器必须执行的工作和我们减少所需的我们的应用程序的网络流量的量。</span><span class="sxs-lookup"><span data-stu-id="88265-166">By taking advantage of Ajax, we reduce the amount of work that our database server must perform and we reduce the amount of network traffic required by our application.</span></span>

## <a name="don-t-be-afraid-of-ajax"></a><span data-ttu-id="88265-167">不要将担心的 Ajax</span><span class="sxs-lookup"><span data-stu-id="88265-167">Don t be Afraid of Ajax</span></span>

<span data-ttu-id="88265-168">一些开发人员避免使用 Ajax，因为他们担心下层浏览器。</span><span class="sxs-lookup"><span data-stu-id="88265-168">Some developers avoid using Ajax because they worry about downlevel browsers.</span></span> <span data-ttu-id="88265-169">他们想要确保其 web 应用程序由不支持 JavaScript 的浏览器访问时仍将起作用。</span><span class="sxs-lookup"><span data-stu-id="88265-169">They want to make sure that their web applications will still work when accessed by a browser that does not support JavaScript.</span></span> <span data-ttu-id="88265-170">由于 Ajax 依赖于 JavaScript，一些开发人员应避免使用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="88265-170">Because Ajax depends on JavaScript, some developers avoid using Ajax.</span></span>

<span data-ttu-id="88265-171">但是，如果你非常小心有关如何实现 Ajax 然后可以生成使用上层和下层浏览器应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-171">However, if you are careful about how you implement Ajax then you can build applications that work with both uplevel and downlevel browsers.</span></span> <span data-ttu-id="88265-172">我们的联系人管理器应用程序会使用支持 JavaScript 的浏览器和浏览器不这样做。</span><span class="sxs-lookup"><span data-stu-id="88265-172">Our Contact Manager application will work with browsers that support JavaScript and browsers that do not.</span></span>

<span data-ttu-id="88265-173">如果支持 JavaScript 的浏览器中使用联系人管理器的应用程序，然后将具有更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="88265-173">If you use the Contact Manager application with a browser that supports JavaScript then you will have a better user experience.</span></span> <span data-ttu-id="88265-174">例如，当你单击联系人的组，则将更新仅显示联系人的页的区域。</span><span class="sxs-lookup"><span data-stu-id="88265-174">For example, when you click a contact group, only the region of the page that displays contacts will be updated.</span></span>

<span data-ttu-id="88265-175">如果使用浏览器不支持 JavaScript （或已禁用 JavaScript） 使用联系人管理器应用程序在另一方面，你将具有略有不太理想的用户体验。</span><span class="sxs-lookup"><span data-stu-id="88265-175">If, on the other hand, you use the Contact Manager application with a browser that does not support JavaScript (or that has JavaScript disabled) then you will have a slightly less desirable user experience.</span></span> <span data-ttu-id="88265-176">例如，当你单击联系人的组，整个索引视图必须将发送回浏览器以显示匹配的联系人列表。</span><span class="sxs-lookup"><span data-stu-id="88265-176">For example, when you click a contact group, the entire Index view must be posted back to the browser in order to display the matching list of contacts.</span></span>

## <a name="adding-the-required-javascript-files"></a><span data-ttu-id="88265-177">添加所需的 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="88265-177">Adding the Required JavaScript Files</span></span>

<span data-ttu-id="88265-178">我们将需要使用三个 JavaScript 文件将 Ajax 功能添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="88265-178">We'll need to use three JavaScript files to add Ajax functionality to our application.</span></span> <span data-ttu-id="88265-179">新的 ASP.NET MVC 应用程序的脚本文件夹中包含这些文件的所有三个。</span><span class="sxs-lookup"><span data-stu-id="88265-179">All three of these files are included in the Scripts folder of a new ASP.NET MVC application.</span></span>

<span data-ttu-id="88265-180">如果你计划在你的应用程序在多个页面中使用 Ajax 然后其意义要包含在你应用程序的视图母版页中的所需的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="88265-180">If you plan to use Ajax in multiple pages in your application then it makes sense to include the required JavaScript files in your application s view master page.</span></span> <span data-ttu-id="88265-181">这样一来，JavaScript 文件都将包括所有在你的应用程序页中自动。</span><span class="sxs-lookup"><span data-stu-id="88265-181">That way, the JavaScript files will be included in all of the pages in your application automatically.</span></span>

<span data-ttu-id="88265-182">将添加以下 JavaScript 包含内部&lt;头&gt;视图母版页的标记：</span><span class="sxs-lookup"><span data-stu-id="88265-182">Add the following JavaScript includes inside the &lt;head&gt; tag of your view master page:</span></span>

[!code-html[Main](iteration-7-add-ajax-functionality-cs/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a><span data-ttu-id="88265-183">重构要使用 Ajax 的索引视图</span><span class="sxs-lookup"><span data-stu-id="88265-183">Refactoring the Index View to use Ajax</span></span>

<span data-ttu-id="88265-184">让我们来首先修改我们索引视图，以便显示联系人的视图的区域，仅单击联系人的组更新。</span><span class="sxs-lookup"><span data-stu-id="88265-184">Let s start by modifying our Index view so that clicking a contact group only updates the region of the view that displays contacts.</span></span> <span data-ttu-id="88265-185">图 1 中的红色框包含我们想要更新的区域。</span><span class="sxs-lookup"><span data-stu-id="88265-185">The red box in Figure 1 contains the region that we want to update.</span></span>


<span data-ttu-id="88265-186">[![更新仅联系人](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="88265-186">[![Updating only contacts](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)</span></span>

<span data-ttu-id="88265-187">**图 01**： 更新仅联系人 ([单击以查看实际尺寸的图像](iteration-7-add-ajax-functionality-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="88265-187">**Figure 01**: Updating only contacts([Click to view full-size image](iteration-7-add-ajax-functionality-cs/_static/image2.png))</span></span>


<span data-ttu-id="88265-188">第一步是视图的将我们想要以异步方式更新到单独的部分 （视图用户控件） 的一部分。</span><span class="sxs-lookup"><span data-stu-id="88265-188">The first step is to separate the part of the view that we want to update asynchronously into a separate partial (view user control).</span></span> <span data-ttu-id="88265-189">显示的联系人的表的索引视图的部分已移动到列表 1 中部分。</span><span class="sxs-lookup"><span data-stu-id="88265-189">The section of the Index view that displays the table of contacts has been moved into the partial in Listing 1.</span></span>

<span data-ttu-id="88265-190">**Listing 1 - Views\Contact\ContactList.ascx**</span><span class="sxs-lookup"><span data-stu-id="88265-190">**Listing 1 - Views\Contact\ContactList.ascx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample2.aspx)]

<span data-ttu-id="88265-191">请注意，列表 1 中的部分不同于索引视图的模型。</span><span class="sxs-lookup"><span data-stu-id="88265-191">Notice that the partial in Listing 1 has a different model than the Index view.</span></span> <span data-ttu-id="88265-192">*Inherits*属性中&lt;%@ 页 %&gt;指令指定分部继承 ViewUserControl&lt;组&gt;类。</span><span class="sxs-lookup"><span data-stu-id="88265-192">The *Inherits* attribute in the &lt;%@ Page %&gt; directive specifies that the partial inherits from the ViewUserControl&lt;Group&gt; class.</span></span>

<span data-ttu-id="88265-193">更新的索引视图包含在清单 2。</span><span class="sxs-lookup"><span data-stu-id="88265-193">The updated Index view is contained in Listing 2.</span></span>

<span data-ttu-id="88265-194">**Listing 2 - Views\Contact\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="88265-194">**Listing 2 - Views\Contact\Index.aspx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample3.aspx)]

<span data-ttu-id="88265-195">有您应注意到了更新的视图，列出 2 中的两个项。</span><span class="sxs-lookup"><span data-stu-id="88265-195">There are two things that you should notice about the updated view in Listing 2.</span></span> <span data-ttu-id="88265-196">首先，请注意，则将所有内容已移动到分部替换通过 Html.RenderPartial() 调用。</span><span class="sxs-lookup"><span data-stu-id="88265-196">First, notice that all of the content moved into the partial is replaced with a call to Html.RenderPartial().</span></span> <span data-ttu-id="88265-197">为了显示联系人的初始设置首次请求的索引视图时调用 Html.RenderPartial() 方法。</span><span class="sxs-lookup"><span data-stu-id="88265-197">The Html.RenderPartial() method is called when the Index view is first requested in order to display the initial set of contacts.</span></span>

<span data-ttu-id="88265-198">其次，请注意，用来显示联系人组 Html.ActionLink() 已替换为 Ajax.ActionLink()。</span><span class="sxs-lookup"><span data-stu-id="88265-198">Second, notice that the Html.ActionLink() used to display contact groups has been replaced with an Ajax.ActionLink().</span></span> <span data-ttu-id="88265-199">使用以下参数调用 Ajax.ActionLink():</span><span class="sxs-lookup"><span data-stu-id="88265-199">The Ajax.ActionLink() is called with the following parameters:</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample4.aspx)]

<span data-ttu-id="88265-200">第一个参数表示要显示的链接的文本、 第二个参数表示路由值和第三个参数表示 Ajax 的选项。</span><span class="sxs-lookup"><span data-stu-id="88265-200">The first parameter represents the text to display for the link, the second parameter represents the route values, and the third parameter represents the Ajax options.</span></span> <span data-ttu-id="88265-201">在这种情况下，我们使用 UpdateTargetId Ajax 选项指向 HTML &lt;div&gt;我们想要更新在 Ajax 请求完成之后的标记。</span><span class="sxs-lookup"><span data-stu-id="88265-201">In this case, we use the UpdateTargetId Ajax option to point to the HTML &lt;div&gt; tag that we want to update after the Ajax request completes.</span></span> <span data-ttu-id="88265-202">我们想要更新&lt;div&gt;标记中使用新的联系人列表。</span><span class="sxs-lookup"><span data-stu-id="88265-202">We want to update the &lt;div&gt; tag with the new list of contacts.</span></span>

<span data-ttu-id="88265-203">列出 3 中包含的联系人控制器更新的 index （） 方法。</span><span class="sxs-lookup"><span data-stu-id="88265-203">The updated Index() method of the Contact controller is contained in Listing 3.</span></span>

<span data-ttu-id="88265-204">**列出 3-Controllers\ContactController.cs （Index 方法）**</span><span class="sxs-lookup"><span data-stu-id="88265-204">**Listing 3 - Controllers\ContactController.cs (Index method)**</span></span>

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample5.cs)]

<span data-ttu-id="88265-205">更新后的 index （） 操作有条件地返回以下两种含义。</span><span class="sxs-lookup"><span data-stu-id="88265-205">The updated Index() action conditionally returns one of two things.</span></span> <span data-ttu-id="88265-206">如果通过 Ajax 请求调用 index （） 操作则控制器将返回部分。</span><span class="sxs-lookup"><span data-stu-id="88265-206">If the Index() action is invoked by an Ajax request then the controller returns a partial.</span></span> <span data-ttu-id="88265-207">否则，index （） 操作返回的整个视图。</span><span class="sxs-lookup"><span data-stu-id="88265-207">Otherwise, the Index() action returns an entire view.</span></span>

<span data-ttu-id="88265-208">请注意 index （） 操作不需要返回多调用 Ajax 请求时的数据。</span><span class="sxs-lookup"><span data-stu-id="88265-208">Notice that the Index() action does not need to return as much data when invoked by an Ajax request.</span></span> <span data-ttu-id="88265-209">在正常的请求的上下文中，索引操作返回的所有联系人的组和所选联系人的组的列表。</span><span class="sxs-lookup"><span data-stu-id="88265-209">In the context of a normal request, the Index action returns a list of all of the contact groups and the selected contact group.</span></span> <span data-ttu-id="88265-210">Ajax 请求的上下文，在 index （） 操作将返回选定的组。</span><span class="sxs-lookup"><span data-stu-id="88265-210">In the context of an Ajax request, the Index() action returns only the selected group.</span></span> <span data-ttu-id="88265-211">Ajax 意味着在你的数据库服务器上的工作较少。</span><span class="sxs-lookup"><span data-stu-id="88265-211">Ajax means less work on your database server.</span></span>

<span data-ttu-id="88265-212">我们已修改的索引视图的工作原理在上层和下层浏览器的情况下。</span><span class="sxs-lookup"><span data-stu-id="88265-212">Our modified Index view works in the case of both uplevel and downlevel browsers.</span></span> <span data-ttu-id="88265-213">如果您单击某个联系人的组，并且你的浏览器支持 JavaScript，则更新仅包含联系人列表中的视图的区域。</span><span class="sxs-lookup"><span data-stu-id="88265-213">If you click a contact group, and your browser supports JavaScript, then only the region of the view that contains the list of contacts is updated.</span></span> <span data-ttu-id="88265-214">如果在另一方面，你的浏览器不支持 JavaScript，则更新整个视图。</span><span class="sxs-lookup"><span data-stu-id="88265-214">If, on the other hand, your browser does not support JavaScript, then the entire view is updated.</span></span>


<span data-ttu-id="88265-215">我们已更新的索引视图都有一个问题。</span><span class="sxs-lookup"><span data-stu-id="88265-215">Our updated Index view has one problem.</span></span> <span data-ttu-id="88265-216">单击联系人的组时，所选的组不会突出显示。</span><span class="sxs-lookup"><span data-stu-id="88265-216">When you click a contact group, the selected group is not highlighted.</span></span> <span data-ttu-id="88265-217">在更新期间 Ajax 请求的区域之外显示的组列表，因为不获取突出显示正确的组。</span><span class="sxs-lookup"><span data-stu-id="88265-217">Because the list of groups is displayed outside of the region that is updated during an Ajax request, the right group does not get highlighted.</span></span> <span data-ttu-id="88265-218">我们将在下一部分中修复此问题。</span><span class="sxs-lookup"><span data-stu-id="88265-218">We'll fix this issue in the next section.</span></span>


## <a name="adding-jquery-animation-effects"></a><span data-ttu-id="88265-219">添加 jQuery 动画效果</span><span class="sxs-lookup"><span data-stu-id="88265-219">Adding jQuery Animation Effects</span></span>

<span data-ttu-id="88265-220">通常情况下，当您单击网页中的链接，你可以使用浏览器进度栏检测浏览器主动提取更新的内容。</span><span class="sxs-lookup"><span data-stu-id="88265-220">Normally, when you click a link in a web page, you can use the browser progress bar to detect whether or not the browser is actively fetching the updated content.</span></span> <span data-ttu-id="88265-221">在执行 Ajax 请求时，另一方面，浏览器进度栏不显示任何进度。</span><span class="sxs-lookup"><span data-stu-id="88265-221">When performing an Ajax request, on the other hand, the browser progress bar does not show any progress.</span></span> <span data-ttu-id="88265-222">这可以使用户紧张。</span><span class="sxs-lookup"><span data-stu-id="88265-222">This can make users nervous.</span></span> <span data-ttu-id="88265-223">如何知道是否已冻结浏览器？</span><span class="sxs-lookup"><span data-stu-id="88265-223">How do you know whether the browser has frozen?</span></span>

<span data-ttu-id="88265-224">有多种方法，你可以向表明用户需在执行 Ajax 请求时执行工作。</span><span class="sxs-lookup"><span data-stu-id="88265-224">There are several ways that you can indicate to a user that work is being performed while performing an Ajax request.</span></span> <span data-ttu-id="88265-225">一种方法是显示一个简单动画。</span><span class="sxs-lookup"><span data-stu-id="88265-225">One approach is to display a simple animation.</span></span> <span data-ttu-id="88265-226">例如，你可以淡入淡出出区域 Ajax 请求开始和淡出该区域，而在请求完成时。</span><span class="sxs-lookup"><span data-stu-id="88265-226">For example, you can fade out a region when an Ajax request begins and fade in the region when the request completes.</span></span>

<span data-ttu-id="88265-227">我们将使用 jQuery 库包含在 Microsoft ASP.NET MVC framework 中，若要创建的动画效果。</span><span class="sxs-lookup"><span data-stu-id="88265-227">We'll use the jQuery library which is included with the Microsoft ASP.NET MVC framework, to create the animation effects.</span></span> <span data-ttu-id="88265-228">更新的索引视图包含在清单 4。</span><span class="sxs-lookup"><span data-stu-id="88265-228">The updated Index view is contained in Listing 4.</span></span>

<span data-ttu-id="88265-229">**列出 4-Views\Contact\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="88265-229">**Listing 4 - Views\Contact\Index.aspx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample6.aspx)]

<span data-ttu-id="88265-230">请注意，更新的索引视图包含三个新的 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="88265-230">Notice that the updated Index view contains three new JavaScript functions.</span></span> <span data-ttu-id="88265-231">前两个函数使用 jQuery 淡出和淡入淡出的联系人列表中单击新的联系人组时。</span><span class="sxs-lookup"><span data-stu-id="88265-231">The first two functions use jQuery to fade out and fade in the list of contacts when you click a new contact group.</span></span> <span data-ttu-id="88265-232">第三个函数中出现错误 （例如，网络超时） 显示一条错误消息时 Ajax 请求结果。</span><span class="sxs-lookup"><span data-stu-id="88265-232">The third function displays an error message when an Ajax request results in an error (for example, network timeout).</span></span>

<span data-ttu-id="88265-233">第一个函数还负责的突出显示所选的组。</span><span class="sxs-lookup"><span data-stu-id="88265-233">The first function also takes care of highlighting the selected group.</span></span> <span data-ttu-id="88265-234">一个类 = 所选的属性添加到单击的元素的父元素 （LI 元素）。</span><span class="sxs-lookup"><span data-stu-id="88265-234">A class= selected attribute is added to the parent element (the LI element) of the element clicked.</span></span> <span data-ttu-id="88265-235">同样，jQuery 可以轻松选择正确元素并添加 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="88265-235">Again, jQuery makes it easy to select the right element and add the CSS class.</span></span>

<span data-ttu-id="88265-236">这些脚本被绑定到 Ajax.ActionLink() AjaxOptions 参数的帮助的组链接。</span><span class="sxs-lookup"><span data-stu-id="88265-236">These scripts are tied to the group links with the help of the Ajax.ActionLink() AjaxOptions parameter.</span></span> <span data-ttu-id="88265-237">更新的 Ajax.ActionLink() 方法调用类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="88265-237">The updated Ajax.ActionLink() method call looks like this:</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a><span data-ttu-id="88265-238">添加浏览器历史记录支持</span><span class="sxs-lookup"><span data-stu-id="88265-238">Adding Browser History Support</span></span>

<span data-ttu-id="88265-239">通常情况下，单击更新页的链接时，将更新你的浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="88265-239">Normally, when you click a link to update a page, your browser history is updated.</span></span> <span data-ttu-id="88265-240">这样一来，你可以单击浏览器后退按钮以将移回及时页的前一状态。</span><span class="sxs-lookup"><span data-stu-id="88265-240">That way, you can click the browser Back button to move back in time to the previous state of the page.</span></span> <span data-ttu-id="88265-241">例如，如果您单击的好友联系人组，然后单击业务联系人组，你可以单击浏览器后退按钮导航回页的状态时未选择的好友联系人组。</span><span class="sxs-lookup"><span data-stu-id="88265-241">For example, if you click the Friends contact group and then click the Business contact group, you can click the browser Back button to navigate back to the state of the page when the Friends contact group was selected.</span></span>

<span data-ttu-id="88265-242">遗憾的是，执行 Ajax 请求不浏览器历史记录自动更新。</span><span class="sxs-lookup"><span data-stu-id="88265-242">Unfortunately, performing an Ajax request does not update browser history automatically.</span></span> <span data-ttu-id="88265-243">如果您单击某个联系人的组，并且使用 Ajax 请求检索匹配联系人的列表，则不会更新的浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="88265-243">If you click a contact group, and the list of matching contacts is retrieved with an Ajax request, then the browser history is not updated.</span></span> <span data-ttu-id="88265-244">浏览器的后退按钮不能用于在选择新的联系人组后导航回联系人的组。</span><span class="sxs-lookup"><span data-stu-id="88265-244">You cannot use the browser Back button to navigate back to a contact group after selecting a new contact group.</span></span>

<span data-ttu-id="88265-245">如果你希望用户能够使用浏览器返回按钮执行 Ajax 请求后然后你需要执行一些工作。</span><span class="sxs-lookup"><span data-stu-id="88265-245">If you want users to be able to use the browser Back button after performing Ajax requests then you need to perform a little more work.</span></span> <span data-ttu-id="88265-246">你需要充分利用 ASP.NET AJAX 框架中内置的浏览器历史记录管理功能。</span><span class="sxs-lookup"><span data-stu-id="88265-246">You need to take advantage of the browser history management functionality built in the ASP.NET AJAX Framework.</span></span>

<span data-ttu-id="88265-247">ASP.NET AJAX 浏览器历史记录，你需要做三件事：</span><span class="sxs-lookup"><span data-stu-id="88265-247">ASP.NET AJAX browser history, you need to do three things:</span></span>

1. <span data-ttu-id="88265-248">通过将 enableBrowserHistory 属性设置为 true 来启用浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="88265-248">Enable Browser History by setting the enableBrowserHistory property to true.</span></span>
2. <span data-ttu-id="88265-249">通过调用 addHistoryPoint() 方法的视图状态更改时，请保存历史时间点。</span><span class="sxs-lookup"><span data-stu-id="88265-249">Save history points when the state of a view changes by calling the addHistoryPoint() method.</span></span>
3. <span data-ttu-id="88265-250">引发导航事件时，重新构造的视图状态。</span><span class="sxs-lookup"><span data-stu-id="88265-250">Reconstruct the state of the view when the navigate event is raised.</span></span>

<span data-ttu-id="88265-251">更新的索引视图包含在列出 5。</span><span class="sxs-lookup"><span data-stu-id="88265-251">The updated Index view is contained in Listing 5.</span></span>

<span data-ttu-id="88265-252">**列出 5-Views\Contact\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="88265-252">**Listing 5 - Views\Contact\Index.aspx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample8.aspx)]

<span data-ttu-id="88265-253">在列出 5 中，pageInit() 函数中启用了浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="88265-253">In Listing 5, Browser History is enabled in the pageInit() function.</span></span> <span data-ttu-id="88265-254">PageInit() 函数还用于设置导航事件的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="88265-254">The pageInit() function is also used to set up the event handler for the navigate event.</span></span> <span data-ttu-id="88265-255">转发的浏览器或后退按钮会导致页后，可以更改的状态时，将引发导航事件。</span><span class="sxs-lookup"><span data-stu-id="88265-255">The navigate event is raised whenever the browser Forward or Back button causes the state of the page to change.</span></span>

<span data-ttu-id="88265-256">单击联系人的组时，被调用 beginContactList() 方法。</span><span class="sxs-lookup"><span data-stu-id="88265-256">The beginContactList() method is called when you click a contact group.</span></span> <span data-ttu-id="88265-257">此方法通过调用 addHistoryPoint() 方法创建新的历史时间点。</span><span class="sxs-lookup"><span data-stu-id="88265-257">This method creates a new history point by calling the addHistoryPoint() method.</span></span> <span data-ttu-id="88265-258">单击联系人组的 id 添加到历史记录。</span><span class="sxs-lookup"><span data-stu-id="88265-258">The id of the contact group clicked is added to history.</span></span>

<span data-ttu-id="88265-259">从联系人组链接的 expando 属性检索组 id。</span><span class="sxs-lookup"><span data-stu-id="88265-259">The group id is retrieved from an expando attribute on the contact group link.</span></span> <span data-ttu-id="88265-260">则链接呈现与对 Ajax.ActionLink() 的以下调用。</span><span class="sxs-lookup"><span data-stu-id="88265-260">The link is rendered with the following call to Ajax.ActionLink().</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample9.aspx)]

<span data-ttu-id="88265-261">传递给 Ajax.ActionLink() 的最后一个参数将添加一个名为 groupid （XHTML 兼容性为小写） 链接到的 expando 特性。</span><span class="sxs-lookup"><span data-stu-id="88265-261">The last parameter passed to the Ajax.ActionLink() adds an expando attribute named groupid to the link (lowercase for XHTML compatibility).</span></span>

<span data-ttu-id="88265-262">当用户点击回浏览器或前进按钮时，将引发导航事件和调用 navigate() 方法。</span><span class="sxs-lookup"><span data-stu-id="88265-262">When a user hits the browser Back or Forward button, the navigate event is raised and the navigate() method is called.</span></span> <span data-ttu-id="88265-263">此方法将更新以匹配到浏览器历史记录点传递给 navigate 方法对应的页的状态的页中显示的联系人。</span><span class="sxs-lookup"><span data-stu-id="88265-263">This method updates the contacts displayed in the page to match the state of the page that corresponds to the browser history point passed to the navigate method.</span></span>

## <a name="performing-ajax-deletes"></a><span data-ttu-id="88265-264">执行 Ajax 删除</span><span class="sxs-lookup"><span data-stu-id="88265-264">Performing Ajax Deletes</span></span>

<span data-ttu-id="88265-265">目前，若要删除联系人，你需要单击删除链接，然后单击删除确认页中显示删除按钮 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="88265-265">Currently, in order to delete a contact, you need to click on the Delete link and then click the Delete button displayed in the delete confirmation page (see Figure 2).</span></span> <span data-ttu-id="88265-266">这看起来像大量的页请求来完成更简单如删除的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="88265-266">This seems like a lot of page requests to do something simple like deleting a database record.</span></span>


<span data-ttu-id="88265-267">[![删除确认页](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="88265-267">[![The delete confirmation page](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)</span></span>

<span data-ttu-id="88265-268">**图 02**: 删除确认页 ([单击以查看实际尺寸的图像](iteration-7-add-ajax-functionality-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="88265-268">**Figure 02**: The delete confirmation page([Click to view full-size image](iteration-7-add-ajax-functionality-cs/_static/image4.png))</span></span>


<span data-ttu-id="88265-269">它很容易跳过删除确认页并直接从索引视图中删除联系人。</span><span class="sxs-lookup"><span data-stu-id="88265-269">It is tempting to skip the delete confirmation page and delete a contact directly from the Index view.</span></span> <span data-ttu-id="88265-270">应当避免此倾向做法，因为采用此方法将打开应用程序以便对安全漏洞。</span><span class="sxs-lookup"><span data-stu-id="88265-270">You should avoid this temptation because taking this approach opens your application to security holes.</span></span> <span data-ttu-id="88265-271">一般情况下，don t 想要调用的操作修改 web 应用程序的状态时执行一个 HTTP GET 操作。</span><span class="sxs-lookup"><span data-stu-id="88265-271">In general, you don t want to perform an HTTP GET operation when invoking an action that modifies the state of your web application.</span></span> <span data-ttu-id="88265-272">当执行 delete，你想要执行 HTTP POST，或者更好的尚未，HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="88265-272">When performing a delete, you want to perform an HTTP POST, or better yet, an HTTP DELETE operation.</span></span>

<span data-ttu-id="88265-273">删除链接包含在部分联系人列表。</span><span class="sxs-lookup"><span data-stu-id="88265-273">The Delete link is contained in the ContactList partial.</span></span> <span data-ttu-id="88265-274">在列出 6 中包含部分 ContactList 的更新的版本。</span><span class="sxs-lookup"><span data-stu-id="88265-274">An updated version of the ContactList partial is contained in Listing 6.</span></span>

<span data-ttu-id="88265-275">**Listing 6 - Views\Contact\ContactList.ascx**</span><span class="sxs-lookup"><span data-stu-id="88265-275">**Listing 6 - Views\Contact\ContactList.ascx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample10.aspx)]

<span data-ttu-id="88265-276">删除链接来呈现与对 Ajax.ImageActionLink() 方法的以下调用：</span><span class="sxs-lookup"><span data-stu-id="88265-276">The Delete link is rendered with the following call to the Ajax.ImageActionLink() method:</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample11.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="88265-277">Ajax.ImageActionLink() 不是 ASP.NET MVC framework 的标准部分。</span><span class="sxs-lookup"><span data-stu-id="88265-277">The Ajax.ImageActionLink() is not a standard part of the ASP.NET MVC framework.</span></span> <span data-ttu-id="88265-278">Ajax.ImageActionLink() 是 Contact Manager 项目中包含自定义帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="88265-278">The Ajax.ImageActionLink() is a custom helper methods included in the Contact Manager project.</span></span>


<span data-ttu-id="88265-279">AjaxOptions 参数具有两个属性。</span><span class="sxs-lookup"><span data-stu-id="88265-279">The AjaxOptions parameter has two properties.</span></span> <span data-ttu-id="88265-280">首先，确认属性用于显示一个弹出窗口 JavaScript 确认对话框。</span><span class="sxs-lookup"><span data-stu-id="88265-280">First, the Confirm property is used to display a popup JavaScript confirmation dialog.</span></span> <span data-ttu-id="88265-281">其次，HttpMethod 属性用于执行 HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="88265-281">Second, the HttpMethod property is used to perform an HTTP DELETE operation.</span></span>

<span data-ttu-id="88265-282">列出 7 包含新 AjaxDelete() 操作已添加到联系人控制器。</span><span class="sxs-lookup"><span data-stu-id="88265-282">Listing 7 contains a new AjaxDelete() action that has been added to the Contact controller.</span></span>

<span data-ttu-id="88265-283">**Listing 7 - Controllers\ContactController.cs (AjaxDelete)**</span><span class="sxs-lookup"><span data-stu-id="88265-283">**Listing 7 - Controllers\ContactController.cs (AjaxDelete)**</span></span>

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample12.cs)]

<span data-ttu-id="88265-284">AjaxDelete() 操作是使用 AcceptVerbs 属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="88265-284">The AjaxDelete() action is decorated with an AcceptVerbs attribute.</span></span> <span data-ttu-id="88265-285">此属性可防止调用除 HTTP DELETE 操作以外的任何 HTTP 操作的操作。</span><span class="sxs-lookup"><span data-stu-id="88265-285">This attribute prevents the action from being invoked except by any HTTP operation other than an HTTP DELETE operation.</span></span> <span data-ttu-id="88265-286">具体而言，不能调用此操作使用 HTTP GET。</span><span class="sxs-lookup"><span data-stu-id="88265-286">In particular, you cannot invoke this action with an HTTP GET.</span></span>

<span data-ttu-id="88265-287">删除数据库记录后，你需要显示的联系人不包含已删除的记录更新的列表。</span><span class="sxs-lookup"><span data-stu-id="88265-287">After you delete database record, you need to display the updated list of contacts that does not contain the deleted record.</span></span> <span data-ttu-id="88265-288">AjaxDelete() 方法返回部分 ContactList 和更新的联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="88265-288">The AjaxDelete() method returns the ContactList partial and the updated list of contacts.</span></span>

## <a name="summary"></a><span data-ttu-id="88265-289">总结</span><span class="sxs-lookup"><span data-stu-id="88265-289">Summary</span></span>

<span data-ttu-id="88265-290">在此迭代中，我们添加到我们的联系人管理器应用程序 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="88265-290">In this iteration, we added Ajax functionality to our Contact Manager application.</span></span> <span data-ttu-id="88265-291">我们使用 Ajax 提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="88265-291">We used Ajax to improve the responsiveness and performance of our application.</span></span>

<span data-ttu-id="88265-292">首先，我们将重构索引视图，以便单击联系人的组不会更新整个视图。</span><span class="sxs-lookup"><span data-stu-id="88265-292">First, we refactored the Index view so that clicking a contact group does not update the entire view.</span></span> <span data-ttu-id="88265-293">相反，单击所需联系组只会更新联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="88265-293">Instead, clicking a contact group only updates the list of contacts.</span></span>

<span data-ttu-id="88265-294">接下来，我们使用 jQuery 动画效果淡出和淡入联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="88265-294">Next, we used jQuery animation effects to fade out and fade in the list of contacts.</span></span> <span data-ttu-id="88265-295">将动画添加到 Ajax 应用程序可以用于提供与浏览器进度栏的等效项应用程序的用户。</span><span class="sxs-lookup"><span data-stu-id="88265-295">Adding animation to an Ajax application can be used to provide users of the application with the equivalent of a browser progress bar.</span></span>

<span data-ttu-id="88265-296">我们还添加到我们 Ajax 应用程序的浏览器历史记录支持。</span><span class="sxs-lookup"><span data-stu-id="88265-296">We also added browser history support to our Ajax application.</span></span> <span data-ttu-id="88265-297">我们已启用的用户单击浏览器返回并将转发按钮，以更改索引视图的状态。</span><span class="sxs-lookup"><span data-stu-id="88265-297">We enabled users to click the browser Back and Forward buttons to change the state of the Index view.</span></span>

<span data-ttu-id="88265-298">最后，我们创建一个删除链接，以支持 HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="88265-298">Finally, we created a delete link that supports HTTP DELETE operations.</span></span> <span data-ttu-id="88265-299">通过执行 Ajax 删除，我们使用户能够删除数据库记录，而无需用户请求其他删除确认页。</span><span class="sxs-lookup"><span data-stu-id="88265-299">By performing Ajax deletes, we enable users to delete database records without requiring the user to request an additional delete confirmation page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="88265-300">[上一页](iteration-6-use-test-driven-development-cs.md)
> [下一页](iteration-1-create-the-application-vb.md)</span><span class="sxs-lookup"><span data-stu-id="88265-300">[Previous](iteration-6-use-test-driven-development-cs.md)
[Next](iteration-1-create-the-application-vb.md)</span></span>
