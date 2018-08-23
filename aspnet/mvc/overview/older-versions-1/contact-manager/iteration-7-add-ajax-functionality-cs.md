---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
title: 迭代 7 – 添加 Ajax 功能 (C#) |Microsoft Docs
author: microsoft
description: 在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1b0809e-8909-444e-b6bb-a5cd1dea3f72
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
msc.type: authoredcontent
ms.openlocfilehash: a51713e57872ccfc3a76cf91fec728fdb6fa1eac
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834583"
---
<a name="iteration-7--add-ajax-functionality-c"></a><span data-ttu-id="7ead7-103">迭代 7 – 添加 Ajax 功能 (C#)</span><span class="sxs-lookup"><span data-stu-id="7ead7-103">Iteration #7 – Add Ajax functionality (C#)</span></span>
====================
<span data-ttu-id="7ead7-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7ead7-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="7ead7-105">下载代码</span><span class="sxs-lookup"><span data-stu-id="7ead7-105">Download Code</span></span>](iteration-7-add-ajax-functionality-cs/_static/contactmanager_7_cs1.zip)

> <span data-ttu-id="7ead7-106">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-106">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="7ead7-107">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="7ead7-107">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="7ead7-108">在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="7ead7-108">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="7ead7-109">联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-109">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="7ead7-110">我们通过多个迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-110">We build the application over multiple iterations.</span></span> <span data-ttu-id="7ead7-111">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-111">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="7ead7-112">此多个迭代方法的目标是帮助你了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="7ead7-112">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="7ead7-113">迭代 1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-113">Iteration #1 - Create the application.</span></span> <span data-ttu-id="7ead7-114">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-114">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="7ead7-115">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="7ead7-115">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="7ead7-116">迭代 2 – 使应用程序看上去更美观。</span><span class="sxs-lookup"><span data-stu-id="7ead7-116">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="7ead7-117">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="7ead7-117">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="7ead7-118">迭代 3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="7ead7-118">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="7ead7-119">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="7ead7-119">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="7ead7-120">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="7ead7-120">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="7ead7-121">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="7ead7-121">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="7ead7-122">迭代 4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="7ead7-122">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="7ead7-123">在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-123">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="7ead7-124">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="7ead7-124">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="7ead7-125">迭代 5 — 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="7ead7-125">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="7ead7-126">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="7ead7-126">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="7ead7-127">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="7ead7-127">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="7ead7-128">迭代 6-使用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="7ead7-128">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="7ead7-129">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="7ead7-129">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="7ead7-130">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-130">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="7ead7-131">迭代 7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-131">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="7ead7-132">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-132">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="7ead7-133">此迭代</span><span class="sxs-lookup"><span data-stu-id="7ead7-133">This Iteration</span></span>

<span data-ttu-id="7ead7-134">在此迭代的联系人管理器应用程序中，我们将重构应用程序以充分利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="7ead7-134">In this iteration of the Contact Manager application, we refactor our application to make use of Ajax.</span></span> <span data-ttu-id="7ead7-135">通过利用 Ajax，我们使我们的应用程序响应速度更快。</span><span class="sxs-lookup"><span data-stu-id="7ead7-135">By taking advantage of Ajax, we make our application more responsive.</span></span> <span data-ttu-id="7ead7-136">我们可以避免当我们需要更新某些区域在页面中的呈现整个页面。</span><span class="sxs-lookup"><span data-stu-id="7ead7-136">We can avoid rendering an entire page when we need to update only a certain region in a page.</span></span>

<span data-ttu-id="7ead7-137">我们将重构索引视图，以便我们不需要重新显示整个页面，只要有人选择新联系人组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-137">We'll refactor our Index view so that we don t need to redisplay the entire page whenever someone selects a new contact group.</span></span> <span data-ttu-id="7ead7-138">相反，当某人单击联系人组时，我们将只需更新的联系人列表并保留单独的页的其余部分。</span><span class="sxs-lookup"><span data-stu-id="7ead7-138">Instead, when someone clicks a contact group, we'll just update the list of contacts and leave the rest of the page alone.</span></span>

<span data-ttu-id="7ead7-139">我们还将更改我们删除链接的工作原理的方式。</span><span class="sxs-lookup"><span data-stu-id="7ead7-139">We'll also change the way our delete link works.</span></span> <span data-ttu-id="7ead7-140">而不是显示一个单独的确认页面，我们将显示一个 JavaScript 确认对话框。</span><span class="sxs-lookup"><span data-stu-id="7ead7-140">Instead of displaying a separate confirmation page, we'll display a JavaScript confirmation dialog.</span></span> <span data-ttu-id="7ead7-141">如果您确认要删除联系人，则对要从数据库中删除联系人记录的服务器执行 HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-141">If you confirm that you want to delete a contact, an HTTP DELETE operation is performed against the server to delete the contact record from the database.</span></span>

<span data-ttu-id="7ead7-142">此外，我们将利用 jQuery 将动画效果添加到我们的索引视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-142">Furthermore, we will take advantage of jQuery to add animation effects to our Index view.</span></span> <span data-ttu-id="7ead7-143">正在从服务器提取新的联系人列表时，我们将显示动画。</span><span class="sxs-lookup"><span data-stu-id="7ead7-143">We'll display an animation when the new list of contacts is being fetched from the server.</span></span>

<span data-ttu-id="7ead7-144">最后，我们将利用 ASP.NET AJAX framework 支持管理浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-144">Finally, we'll take advantage of the ASP.NET AJAX framework support for managing browser history.</span></span> <span data-ttu-id="7ead7-145">每当我们执行的 Ajax 调用以更新联系人列表，我们将创建历史时间点。</span><span class="sxs-lookup"><span data-stu-id="7ead7-145">We'll create history points whenever we perform an Ajax call to update the contact list.</span></span> <span data-ttu-id="7ead7-146">这样一来，在浏览器向后和向前按钮将起作用。</span><span class="sxs-lookup"><span data-stu-id="7ead7-146">That way, the browser backward and forward buttons will work.</span></span>

## <a name="why-use-ajax"></a><span data-ttu-id="7ead7-147">为何使用 Ajax？</span><span class="sxs-lookup"><span data-stu-id="7ead7-147">Why use Ajax?</span></span>

<span data-ttu-id="7ead7-148">使用 Ajax 具有诸多优点。</span><span class="sxs-lookup"><span data-stu-id="7ead7-148">Using Ajax has many benefits.</span></span> <span data-ttu-id="7ead7-149">首先，将 Ajax 功能添加到应用程序导致更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="7ead7-149">First, adding Ajax functionality to an application results in a better user experience.</span></span> <span data-ttu-id="7ead7-150">在普通的 web 应用程序中，整个页面必须为回发到服务器每个用户执行的操作的时间。</span><span class="sxs-lookup"><span data-stu-id="7ead7-150">In a normal web application, the entire page must be posted back to the server each and every time a user performs an action.</span></span> <span data-ttu-id="7ead7-151">每当执行的操作，浏览器锁和用户必须等待，直到提取并重新显示整个页面。</span><span class="sxs-lookup"><span data-stu-id="7ead7-151">Whenever you perform an action, the browser locks and the user must wait until the entire page is fetched and redisplayed.</span></span>

<span data-ttu-id="7ead7-152">这将是在桌面应用程序的情况下不能接受体验。</span><span class="sxs-lookup"><span data-stu-id="7ead7-152">This would be an unacceptable experience in the case of a desktop application.</span></span> <span data-ttu-id="7ead7-153">但是，一直以来，我们一直与在 web 应用程序的情况下此不良用户体验因为我们不知道我们能做任何越好。</span><span class="sxs-lookup"><span data-stu-id="7ead7-153">But, traditionally, we lived with this bad user experience in the case of a web application because we did not know that we could do any better.</span></span> <span data-ttu-id="7ead7-154">我们认为它是 web 应用程序的限制时，实际上，它只是我们想象力的限制。</span><span class="sxs-lookup"><span data-stu-id="7ead7-154">We thought it was a limitation of web applications when, in actuality, it was just a limitation of our imaginations.</span></span>

<span data-ttu-id="7ead7-155">在 Ajax 应用程序，您不需要停止只是为了将更新页面，使用户体验。</span><span class="sxs-lookup"><span data-stu-id="7ead7-155">In an Ajax application, you don t need to bring the user experience to a halt just to update a page.</span></span> <span data-ttu-id="7ead7-156">相反，您可以在后台更新页面执行的异步请求。</span><span class="sxs-lookup"><span data-stu-id="7ead7-156">Instead, you can perform an asynchronous request in the background to update the page.</span></span> <span data-ttu-id="7ead7-157">您不 t 强制用户等待获取更新的页的一部分时。</span><span class="sxs-lookup"><span data-stu-id="7ead7-157">You don t force the user to wait while part of the page gets updated.</span></span>

<span data-ttu-id="7ead7-158">通过利用 Ajax，您还可以提高应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-158">By taking advantage of Ajax, you also can improve the performance of your application.</span></span> <span data-ttu-id="7ead7-159">请考虑联系人管理器应用程序的工作原理现在不具有 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-159">Consider how the Contact Manager application works right now without Ajax functionality.</span></span> <span data-ttu-id="7ead7-160">当您单击联系人组时，则必须重新显示整个索引视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-160">When you click a contact group, the entire Index view must be redisplayed.</span></span> <span data-ttu-id="7ead7-161">必须从数据库服务器检索的联系人列表和联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-161">The list of contacts and list of contact groups must be retrieved from the database server.</span></span> <span data-ttu-id="7ead7-162">所有这些数据必须是通过线缆从 web 服务器传递到 web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="7ead7-162">All of this data must be passed across the wire from web server to web browser.</span></span>

<span data-ttu-id="7ead7-163">我们将 Ajax 功能添加到我们的应用程序后，但是，我们可以避免在用户单击联系人组时重新显示整个页面。</span><span class="sxs-lookup"><span data-stu-id="7ead7-163">After we add Ajax functionality to our application, however, we can avoid redisplaying the entire page when a user clicks a contact group.</span></span> <span data-ttu-id="7ead7-164">我们不再需要获取数据库中联系人的组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-164">We no longer need to grab the contact groups from the database.</span></span> <span data-ttu-id="7ead7-165">我们也不需要通过网络推送整个索引视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-165">We also don t need to push the entire Index view across the wire.</span></span> <span data-ttu-id="7ead7-166">通过利用 Ajax，我们减少我们的数据库服务器必须执行的工作量和我们减少所需的应用程序的网络流量的量。</span><span class="sxs-lookup"><span data-stu-id="7ead7-166">By taking advantage of Ajax, we reduce the amount of work that our database server must perform and we reduce the amount of network traffic required by our application.</span></span>

## <a name="don-t-be-afraid-of-ajax"></a><span data-ttu-id="7ead7-167">不要将担心的 Ajax</span><span class="sxs-lookup"><span data-stu-id="7ead7-167">Don t be Afraid of Ajax</span></span>

<span data-ttu-id="7ead7-168">一些开发人员避免使用 Ajax，因为他们担心低级浏览器。</span><span class="sxs-lookup"><span data-stu-id="7ead7-168">Some developers avoid using Ajax because they worry about downlevel browsers.</span></span> <span data-ttu-id="7ead7-169">他们想要确保其 web 应用程序不支持 JavaScript 的浏览器进行访问时仍将起作用。</span><span class="sxs-lookup"><span data-stu-id="7ead7-169">They want to make sure that their web applications will still work when accessed by a browser that does not support JavaScript.</span></span> <span data-ttu-id="7ead7-170">由于 Ajax 依赖于 JavaScript，一些开发人员避免使用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="7ead7-170">Because Ajax depends on JavaScript, some developers avoid using Ajax.</span></span>

<span data-ttu-id="7ead7-171">但是，如果你非常小心有关如何实现 Ajax，则可生成适用于上级和下层浏览器应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-171">However, if you are careful about how you implement Ajax then you can build applications that work with both uplevel and downlevel browsers.</span></span> <span data-ttu-id="7ead7-172">我们的联系人管理器应用程序将使用支持 JavaScript 的浏览器和浏览器不这样做。</span><span class="sxs-lookup"><span data-stu-id="7ead7-172">Our Contact Manager application will work with browsers that support JavaScript and browsers that do not.</span></span>

<span data-ttu-id="7ead7-173">如果联系人管理器应用程序使用支持 JavaScript 的浏览器，然后将具有更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="7ead7-173">If you use the Contact Manager application with a browser that supports JavaScript then you will have a better user experience.</span></span> <span data-ttu-id="7ead7-174">例如，当您单击联系人组时，将更新仅显示联系人的页面的区域。</span><span class="sxs-lookup"><span data-stu-id="7ead7-174">For example, when you click a contact group, only the region of the page that displays contacts will be updated.</span></span>

<span data-ttu-id="7ead7-175">另一方面，如果您使用的浏览器不支持 JavaScript （或已禁用 JavaScript） 的联系人管理器应用程序，然后将具有略有不太理想的用户体验。</span><span class="sxs-lookup"><span data-stu-id="7ead7-175">If, on the other hand, you use the Contact Manager application with a browser that does not support JavaScript (or that has JavaScript disabled) then you will have a slightly less desirable user experience.</span></span> <span data-ttu-id="7ead7-176">例如，当单击联系人组时，整个索引视图必须为回发到浏览器以显示匹配的联系人列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-176">For example, when you click a contact group, the entire Index view must be posted back to the browser in order to display the matching list of contacts.</span></span>

## <a name="adding-the-required-javascript-files"></a><span data-ttu-id="7ead7-177">添加所需的 JavaScript 文件</span><span class="sxs-lookup"><span data-stu-id="7ead7-177">Adding the Required JavaScript Files</span></span>

<span data-ttu-id="7ead7-178">我们将需要使用三个 JavaScript 文件将 Ajax 功能添加到我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-178">We'll need to use three JavaScript files to add Ajax functionality to our application.</span></span> <span data-ttu-id="7ead7-179">所有这三个这些文件包含在新的 ASP.NET MVC 应用程序的 Scripts 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="7ead7-179">All three of these files are included in the Scripts folder of a new ASP.NET MVC application.</span></span>

<span data-ttu-id="7ead7-180">如果你打算在应用程序中的多个页中使用 Ajax 然后最好在应用程序的视图主页面中包含所需的 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="7ead7-180">If you plan to use Ajax in multiple pages in your application then it makes sense to include the required JavaScript files in your application s view master page.</span></span> <span data-ttu-id="7ead7-181">这样一来，JavaScript 文件将在所有应用程序中的页面中自动都包含。</span><span class="sxs-lookup"><span data-stu-id="7ead7-181">That way, the JavaScript files will be included in all of the pages in your application automatically.</span></span>

<span data-ttu-id="7ead7-182">添加以下 JavaScript 包括内部&lt;head&gt;视图母版页的标记：</span><span class="sxs-lookup"><span data-stu-id="7ead7-182">Add the following JavaScript includes inside the &lt;head&gt; tag of your view master page:</span></span>

[!code-html[Main](iteration-7-add-ajax-functionality-cs/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a><span data-ttu-id="7ead7-183">重构要使用 Ajax 的索引视图</span><span class="sxs-lookup"><span data-stu-id="7ead7-183">Refactoring the Index View to use Ajax</span></span>

<span data-ttu-id="7ead7-184">让我们来首先修改索引视图，以便显示联系人的视图的区域，仅单击联系人组更新。</span><span class="sxs-lookup"><span data-stu-id="7ead7-184">Let s start by modifying our Index view so that clicking a contact group only updates the region of the view that displays contacts.</span></span> <span data-ttu-id="7ead7-185">图 1 中的红色框包含我们想要更新的区域。</span><span class="sxs-lookup"><span data-stu-id="7ead7-185">The red box in Figure 1 contains the region that we want to update.</span></span>


<span data-ttu-id="7ead7-186">[![更新仅联系人](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7ead7-186">[![Updating only contacts](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)</span></span>

<span data-ttu-id="7ead7-187">**图 01**： 更新仅联系人 ([单击以查看实际尺寸的图像](iteration-7-add-ajax-functionality-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="7ead7-187">**Figure 01**: Updating only contacts([Click to view full-size image](iteration-7-add-ajax-functionality-cs/_static/image2.png))</span></span>


<span data-ttu-id="7ead7-188">第一步是视图的将我们想要以异步方式更新到单独的部分 （视图用户控件） 的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ead7-188">The first step is to separate the part of the view that we want to update asynchronously into a separate partial (view user control).</span></span> <span data-ttu-id="7ead7-189">显示的联系人的索引视图的一部分已被移动到在列表 1 中部分。</span><span class="sxs-lookup"><span data-stu-id="7ead7-189">The section of the Index view that displays the table of contacts has been moved into the partial in Listing 1.</span></span>

<span data-ttu-id="7ead7-190">**代码清单 1-Views\Contact\ContactList.ascx**</span><span class="sxs-lookup"><span data-stu-id="7ead7-190">**Listing 1 - Views\Contact\ContactList.ascx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample2.aspx)]

<span data-ttu-id="7ead7-191">请注意，在列表 1 中部分包含与索引视图不同的模型。</span><span class="sxs-lookup"><span data-stu-id="7ead7-191">Notice that the partial in Listing 1 has a different model than the Index view.</span></span> <span data-ttu-id="7ead7-192">*Inherits*属性中&lt;%@ 页 %&gt;指令指定分部继承 ViewUserControl&lt;组&gt;类。</span><span class="sxs-lookup"><span data-stu-id="7ead7-192">The *Inherits* attribute in the &lt;%@ Page %&gt; directive specifies that the partial inherits from the ViewUserControl&lt;Group&gt; class.</span></span>

<span data-ttu-id="7ead7-193">列表 2 中包含更新的索引视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-193">The updated Index view is contained in Listing 2.</span></span>

<span data-ttu-id="7ead7-194">**代码清单 2-Views\Contact\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="7ead7-194">**Listing 2 - Views\Contact\Index.aspx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample3.aspx)]

<span data-ttu-id="7ead7-195">有两件事，您会注意到有关清单 2 中更新的视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-195">There are two things that you should notice about the updated view in Listing 2.</span></span> <span data-ttu-id="7ead7-196">首先，注意到的所有内容移到分部替换 Html.RenderPartial() 调用。</span><span class="sxs-lookup"><span data-stu-id="7ead7-196">First, notice that all of the content moved into the partial is replaced with a call to Html.RenderPartial().</span></span> <span data-ttu-id="7ead7-197">Html.RenderPartial() 方法称为索引视图首次请求以便显示联系人的初始设置时。</span><span class="sxs-lookup"><span data-stu-id="7ead7-197">The Html.RenderPartial() method is called when the Index view is first requested in order to display the initial set of contacts.</span></span>

<span data-ttu-id="7ead7-198">其次，请注意，用于显示联系人组 Html.ActionLink() 已替换为 Ajax.ActionLink()。</span><span class="sxs-lookup"><span data-stu-id="7ead7-198">Second, notice that the Html.ActionLink() used to display contact groups has been replaced with an Ajax.ActionLink().</span></span> <span data-ttu-id="7ead7-199">使用以下参数调用 Ajax.ActionLink():</span><span class="sxs-lookup"><span data-stu-id="7ead7-199">The Ajax.ActionLink() is called with the following parameters:</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample4.aspx)]

<span data-ttu-id="7ead7-200">第一个参数表示要显示的链接的文本、 第二个参数表示路由值和第三个参数表示的 Ajax 选项。</span><span class="sxs-lookup"><span data-stu-id="7ead7-200">The first parameter represents the text to display for the link, the second parameter represents the route values, and the third parameter represents the Ajax options.</span></span> <span data-ttu-id="7ead7-201">在这种情况下，我们使用 UpdateTargetId Ajax 选项指向 HTML &lt;div&gt;我们想要在 Ajax 请求完成后更新的标记。</span><span class="sxs-lookup"><span data-stu-id="7ead7-201">In this case, we use the UpdateTargetId Ajax option to point to the HTML &lt;div&gt; tag that we want to update after the Ajax request completes.</span></span> <span data-ttu-id="7ead7-202">我们想要更新&lt;div&gt;新联系人列表的标记。</span><span class="sxs-lookup"><span data-stu-id="7ead7-202">We want to update the &lt;div&gt; tag with the new list of contacts.</span></span>

<span data-ttu-id="7ead7-203">请联系控制器的更新的 index （） 方法包含在清单 3。</span><span class="sxs-lookup"><span data-stu-id="7ead7-203">The updated Index() method of the Contact controller is contained in Listing 3.</span></span>

<span data-ttu-id="7ead7-204">**代码清单 3-Controllers\ContactController.cs （Index 方法）**</span><span class="sxs-lookup"><span data-stu-id="7ead7-204">**Listing 3 - Controllers\ContactController.cs (Index method)**</span></span>

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample5.cs)]

<span data-ttu-id="7ead7-205">更新后的 index （） 操作有条件地返回两个条件之一。</span><span class="sxs-lookup"><span data-stu-id="7ead7-205">The updated Index() action conditionally returns one of two things.</span></span> <span data-ttu-id="7ead7-206">如果由 Ajax 请求调用 index （） 操作控制器返回部分。</span><span class="sxs-lookup"><span data-stu-id="7ead7-206">If the Index() action is invoked by an Ajax request then the controller returns a partial.</span></span> <span data-ttu-id="7ead7-207">否则，index （） 操作返回整个视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-207">Otherwise, the Index() action returns an entire view.</span></span>

<span data-ttu-id="7ead7-208">请注意，index （） 操作不需要返回尽可能多的数据时调用的 Ajax 请求。</span><span class="sxs-lookup"><span data-stu-id="7ead7-208">Notice that the Index() action does not need to return as much data when invoked by an Ajax request.</span></span> <span data-ttu-id="7ead7-209">在正常的请求的上下文中，索引操作返回的所有联系人组和所选联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-209">In the context of a normal request, the Index action returns a list of all of the contact groups and the selected contact group.</span></span> <span data-ttu-id="7ead7-210">在 Ajax 请求的上下文，index （） 操作返回只为所选的组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-210">In the context of an Ajax request, the Index() action returns only the selected group.</span></span> <span data-ttu-id="7ead7-211">Ajax 意味着数据库服务器上的工作较少。</span><span class="sxs-lookup"><span data-stu-id="7ead7-211">Ajax means less work on your database server.</span></span>

<span data-ttu-id="7ead7-212">我们已修改的索引视图在上级和下层浏览器的情况下适用。</span><span class="sxs-lookup"><span data-stu-id="7ead7-212">Our modified Index view works in the case of both uplevel and downlevel browsers.</span></span> <span data-ttu-id="7ead7-213">如果单击联系人组，并在浏览器支持 JavaScript，然后更新只有包含的联系人列表的视图的区域。</span><span class="sxs-lookup"><span data-stu-id="7ead7-213">If you click a contact group, and your browser supports JavaScript, then only the region of the view that contains the list of contacts is updated.</span></span> <span data-ttu-id="7ead7-214">如果，但是，你的浏览器不支持 JavaScript，然后更新整个视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-214">If, on the other hand, your browser does not support JavaScript, then the entire view is updated.</span></span>


<span data-ttu-id="7ead7-215">我们已更新的索引视图都有一个问题。</span><span class="sxs-lookup"><span data-stu-id="7ead7-215">Our updated Index view has one problem.</span></span> <span data-ttu-id="7ead7-216">当单击联系人组时，不突出显示所选的组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-216">When you click a contact group, the selected group is not highlighted.</span></span> <span data-ttu-id="7ead7-217">由于在 Ajax 请求期间更新的区域之外显示的组的列表，不会不获取突出显示正确的组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-217">Because the list of groups is displayed outside of the region that is updated during an Ajax request, the right group does not get highlighted.</span></span> <span data-ttu-id="7ead7-218">我们将在下一节中修复此问题。</span><span class="sxs-lookup"><span data-stu-id="7ead7-218">We'll fix this issue in the next section.</span></span>


## <a name="adding-jquery-animation-effects"></a><span data-ttu-id="7ead7-219">添加 jQuery 动画效果</span><span class="sxs-lookup"><span data-stu-id="7ead7-219">Adding jQuery Animation Effects</span></span>

<span data-ttu-id="7ead7-220">通常情况下，当单击网页中的链接时，可以使用浏览器进度栏来检测在浏览器主动提取更新的内容。</span><span class="sxs-lookup"><span data-stu-id="7ead7-220">Normally, when you click a link in a web page, you can use the browser progress bar to detect whether or not the browser is actively fetching the updated content.</span></span> <span data-ttu-id="7ead7-221">在执行时 Ajax 请求，另一方面，浏览器进度栏不显示任何进度。</span><span class="sxs-lookup"><span data-stu-id="7ead7-221">When performing an Ajax request, on the other hand, the browser progress bar does not show any progress.</span></span> <span data-ttu-id="7ead7-222">这可以让用户紧张。</span><span class="sxs-lookup"><span data-stu-id="7ead7-222">This can make users nervous.</span></span> <span data-ttu-id="7ead7-223">如何知道是否已冻结在浏览器？</span><span class="sxs-lookup"><span data-stu-id="7ead7-223">How do you know whether the browser has frozen?</span></span>

<span data-ttu-id="7ead7-224">有几种方法，您可以指示用户正在执行的 Ajax 请求时执行工作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-224">There are several ways that you can indicate to a user that work is being performed while performing an Ajax request.</span></span> <span data-ttu-id="7ead7-225">一种方法是显示一个简单的动画。</span><span class="sxs-lookup"><span data-stu-id="7ead7-225">One approach is to display a simple animation.</span></span> <span data-ttu-id="7ead7-226">例如，您可以淡出区域时 Ajax 请求开始，并在请求完成时淡入的区域中。</span><span class="sxs-lookup"><span data-stu-id="7ead7-226">For example, you can fade out a region when an Ajax request begins and fade in the region when the request completes.</span></span>

<span data-ttu-id="7ead7-227">我们将使用 jQuery 库包含在 Microsoft ASP.NET MVC 框架，若要创建的动画效果。</span><span class="sxs-lookup"><span data-stu-id="7ead7-227">We'll use the jQuery library which is included with the Microsoft ASP.NET MVC framework, to create the animation effects.</span></span> <span data-ttu-id="7ead7-228">列表 4 中包含更新的索引视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-228">The updated Index view is contained in Listing 4.</span></span>

<span data-ttu-id="7ead7-229">**列表 4-Views\Contact\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="7ead7-229">**Listing 4 - Views\Contact\Index.aspx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample6.aspx)]

<span data-ttu-id="7ead7-230">请注意，更新的索引视图包含三个新的 JavaScript 函数。</span><span class="sxs-lookup"><span data-stu-id="7ead7-230">Notice that the updated Index view contains three new JavaScript functions.</span></span> <span data-ttu-id="7ead7-231">前两个函数使用 jQuery 淡出和淡入的联系人列表中，单击新联系人组时。</span><span class="sxs-lookup"><span data-stu-id="7ead7-231">The first two functions use jQuery to fade out and fade in the list of contacts when you click a new contact group.</span></span> <span data-ttu-id="7ead7-232">第三个函数中出现错误 （例如，网络超时） 显示一条错误消息时 Ajax 请求结果。</span><span class="sxs-lookup"><span data-stu-id="7ead7-232">The third function displays an error message when an Ajax request results in an error (for example, network timeout).</span></span>

<span data-ttu-id="7ead7-233">第一个函数还负责的突出显示所选的组。</span><span class="sxs-lookup"><span data-stu-id="7ead7-233">The first function also takes care of highlighting the selected group.</span></span> <span data-ttu-id="7ead7-234">一个类 = 所选的属性添加到单击的元素的父元素 （LI 元素）。</span><span class="sxs-lookup"><span data-stu-id="7ead7-234">A class= selected attribute is added to the parent element (the LI element) of the element clicked.</span></span> <span data-ttu-id="7ead7-235">同样，jQuery 使得可以轻松选择正确的元素和添加的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="7ead7-235">Again, jQuery makes it easy to select the right element and add the CSS class.</span></span>

<span data-ttu-id="7ead7-236">这些脚本已绑定到 Ajax.ActionLink() AjaxOptions 参数的帮助的组链接。</span><span class="sxs-lookup"><span data-stu-id="7ead7-236">These scripts are tied to the group links with the help of the Ajax.ActionLink() AjaxOptions parameter.</span></span> <span data-ttu-id="7ead7-237">更新的 Ajax.ActionLink() 方法调用如下所示：</span><span class="sxs-lookup"><span data-stu-id="7ead7-237">The updated Ajax.ActionLink() method call looks like this:</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a><span data-ttu-id="7ead7-238">添加浏览器历史记录支持</span><span class="sxs-lookup"><span data-stu-id="7ead7-238">Adding Browser History Support</span></span>

<span data-ttu-id="7ead7-239">通常情况下，单击更新页的链接，将更新你的浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-239">Normally, when you click a link to update a page, your browser history is updated.</span></span> <span data-ttu-id="7ead7-240">这样一来，可以单击浏览器后退按钮在时间中返回移动到页面的以前的状态。</span><span class="sxs-lookup"><span data-stu-id="7ead7-240">That way, you can click the browser Back button to move back in time to the previous state of the page.</span></span> <span data-ttu-id="7ead7-241">例如，如果您单击的好友联系人组，然后单击业务联系人组，可以单击浏览器后退按钮时要导航到页面的状态的好友联系人组选择。</span><span class="sxs-lookup"><span data-stu-id="7ead7-241">For example, if you click the Friends contact group and then click the Business contact group, you can click the browser Back button to navigate back to the state of the page when the Friends contact group was selected.</span></span>

<span data-ttu-id="7ead7-242">遗憾的是，执行 Ajax 请求不会更新浏览器历史记录自动。</span><span class="sxs-lookup"><span data-stu-id="7ead7-242">Unfortunately, performing an Ajax request does not update browser history automatically.</span></span> <span data-ttu-id="7ead7-243">如果单击联系人组，并使用 Ajax 请求检索匹配的联系人的列表，则不会更新浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-243">If you click a contact group, and the list of matching contacts is retrieved with an Ajax request, then the browser history is not updated.</span></span> <span data-ttu-id="7ead7-244">浏览器的后退按钮不能用于向后定位到联系人组选择新联系人组后。</span><span class="sxs-lookup"><span data-stu-id="7ead7-244">You cannot use the browser Back button to navigate back to a contact group after selecting a new contact group.</span></span>

<span data-ttu-id="7ead7-245">如果你希望用户能够使用浏览器返回按钮执行 Ajax 请求后，然后需要执行更多工作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-245">If you want users to be able to use the browser Back button after performing Ajax requests then you need to perform a little more work.</span></span> <span data-ttu-id="7ead7-246">您需要充分利用在 ASP.NET AJAX Framework 中构建的浏览器历史记录管理功能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-246">You need to take advantage of the browser history management functionality built in the ASP.NET AJAX Framework.</span></span>

<span data-ttu-id="7ead7-247">ASP.NET AJAX 浏览器历史记录，您需要做三件事：</span><span class="sxs-lookup"><span data-stu-id="7ead7-247">ASP.NET AJAX browser history, you need to do three things:</span></span>

1. <span data-ttu-id="7ead7-248">通过浏览器历史记录 enableBrowserHistory 属性设置为 true。</span><span class="sxs-lookup"><span data-stu-id="7ead7-248">Enable Browser History by setting the enableBrowserHistory property to true.</span></span>
2. <span data-ttu-id="7ead7-249">通过调用 addHistoryPoint() 方法的视图状态更改时，将保存历史时间点。</span><span class="sxs-lookup"><span data-stu-id="7ead7-249">Save history points when the state of a view changes by calling the addHistoryPoint() method.</span></span>
3. <span data-ttu-id="7ead7-250">引发导航事件时，重新构造的视图状态。</span><span class="sxs-lookup"><span data-stu-id="7ead7-250">Reconstruct the state of the view when the navigate event is raised.</span></span>

<span data-ttu-id="7ead7-251">列表 5 中包含更新的索引视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-251">The updated Index view is contained in Listing 5.</span></span>

<span data-ttu-id="7ead7-252">**列表 5-Views\Contact\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="7ead7-252">**Listing 5 - Views\Contact\Index.aspx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample8.aspx)]

<span data-ttu-id="7ead7-253">列表 5 中 pageInit() 函数中启用了浏览器历史记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-253">In Listing 5, Browser History is enabled in the pageInit() function.</span></span> <span data-ttu-id="7ead7-254">PageInit() 函数还用于设置导航事件的事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-254">The pageInit() function is also used to set up the event handler for the navigate event.</span></span> <span data-ttu-id="7ead7-255">浏览器前进或后退按钮会导致的页后，可以更改状态时，将引发导航事件。</span><span class="sxs-lookup"><span data-stu-id="7ead7-255">The navigate event is raised whenever the browser Forward or Back button causes the state of the page to change.</span></span>

<span data-ttu-id="7ead7-256">单击联系人组时，被调用 beginContactList() 方法。</span><span class="sxs-lookup"><span data-stu-id="7ead7-256">The beginContactList() method is called when you click a contact group.</span></span> <span data-ttu-id="7ead7-257">此方法通过调用 addHistoryPoint() 方法来创建新的历史时间点。</span><span class="sxs-lookup"><span data-stu-id="7ead7-257">This method creates a new history point by calling the addHistoryPoint() method.</span></span> <span data-ttu-id="7ead7-258">单击联系人组的 id 添加到历史记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-258">The id of the contact group clicked is added to history.</span></span>

<span data-ttu-id="7ead7-259">从联系人组链接的 expando 属性中检索组 id。</span><span class="sxs-lookup"><span data-stu-id="7ead7-259">The group id is retrieved from an expando attribute on the contact group link.</span></span> <span data-ttu-id="7ead7-260">使用以下调用 Ajax.ActionLink() 呈现链接。</span><span class="sxs-lookup"><span data-stu-id="7ead7-260">The link is rendered with the following call to Ajax.ActionLink().</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample9.aspx)]

<span data-ttu-id="7ead7-261">最后一个参数传递给 Ajax.ActionLink() 将添加一个名为 groupid （小写的 XHTML 兼容性） 链接到的 expando 属性。</span><span class="sxs-lookup"><span data-stu-id="7ead7-261">The last parameter passed to the Ajax.ActionLink() adds an expando attribute named groupid to the link (lowercase for XHTML compatibility).</span></span>

<span data-ttu-id="7ead7-262">当用户遇到回浏览器或前进按钮时，引发导航事件，并调用 navigate() 方法。</span><span class="sxs-lookup"><span data-stu-id="7ead7-262">When a user hits the browser Back or Forward button, the navigate event is raised and the navigate() method is called.</span></span> <span data-ttu-id="7ead7-263">此方法会更新以匹配到浏览器历史记录点传递给 navigate 方法相对应的页的状态在页中显示的联系人。</span><span class="sxs-lookup"><span data-stu-id="7ead7-263">This method updates the contacts displayed in the page to match the state of the page that corresponds to the browser history point passed to the navigate method.</span></span>

## <a name="performing-ajax-deletes"></a><span data-ttu-id="7ead7-264">执行 Ajax 删除</span><span class="sxs-lookup"><span data-stu-id="7ead7-264">Performing Ajax Deletes</span></span>

<span data-ttu-id="7ead7-265">目前，若要删除联系人，您需要单击删除链接上，然后单击删除确认页中显示删除按钮 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="7ead7-265">Currently, in order to delete a contact, you need to click on the Delete link and then click the Delete button displayed in the delete confirmation page (see Figure 2).</span></span> <span data-ttu-id="7ead7-266">这看起来好像很多的页请求来执行简单删除的数据库记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-266">This seems like a lot of page requests to do something simple like deleting a database record.</span></span>


<span data-ttu-id="7ead7-267">[![删除确认页](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="7ead7-267">[![The delete confirmation page](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)</span></span>

<span data-ttu-id="7ead7-268">**图 02**: 删除确认页 ([单击以查看实际尺寸的图像](iteration-7-add-ajax-functionality-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="7ead7-268">**Figure 02**: The delete confirmation page([Click to view full-size image](iteration-7-add-ajax-functionality-cs/_static/image4.png))</span></span>


<span data-ttu-id="7ead7-269">很容易就跳过删除确认页面并直接从索引视图中删除联系人。</span><span class="sxs-lookup"><span data-stu-id="7ead7-269">It is tempting to skip the delete confirmation page and delete a contact directly from the Index view.</span></span> <span data-ttu-id="7ead7-270">由于采用这种方法打开到安全漏洞的应用程序，应避免心。</span><span class="sxs-lookup"><span data-stu-id="7ead7-270">You should avoid this temptation because taking this approach opens your application to security holes.</span></span> <span data-ttu-id="7ead7-271">一般情况下，don t 想要调用的 web 应用程序状态修改操作时执行的 HTTP GET 操作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-271">In general, you don t want to perform an HTTP GET operation when invoking an action that modifies the state of your web application.</span></span> <span data-ttu-id="7ead7-272">在执行 delete 时，你想要执行 HTTP POST，或者更确切地说，HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-272">When performing a delete, you want to perform an HTTP POST, or better yet, an HTTP DELETE operation.</span></span>

<span data-ttu-id="7ead7-273">删除链接包含在部分联系人列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-273">The Delete link is contained in the ContactList partial.</span></span> <span data-ttu-id="7ead7-274">列表 6 中包含的部分 ContactList 更新的版本。</span><span class="sxs-lookup"><span data-stu-id="7ead7-274">An updated version of the ContactList partial is contained in Listing 6.</span></span>

<span data-ttu-id="7ead7-275">**代码清单 6-Views\Contact\ContactList.ascx**</span><span class="sxs-lookup"><span data-stu-id="7ead7-275">**Listing 6 - Views\Contact\ContactList.ascx**</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample10.aspx)]

<span data-ttu-id="7ead7-276">删除链接呈现并对 Ajax.ImageActionLink() 方法的以下调用：</span><span class="sxs-lookup"><span data-stu-id="7ead7-276">The Delete link is rendered with the following call to the Ajax.ImageActionLink() method:</span></span>

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample11.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="7ead7-277">Ajax.ImageActionLink() 不是 ASP.NET MVC 框架的标准组成部分。</span><span class="sxs-lookup"><span data-stu-id="7ead7-277">The Ajax.ImageActionLink() is not a standard part of the ASP.NET MVC framework.</span></span> <span data-ttu-id="7ead7-278">Ajax.ImageActionLink() 是 Contact Manager 项目中包含自定义帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="7ead7-278">The Ajax.ImageActionLink() is a custom helper methods included in the Contact Manager project.</span></span>


<span data-ttu-id="7ead7-279">AjaxOptions 参数具有两个属性。</span><span class="sxs-lookup"><span data-stu-id="7ead7-279">The AjaxOptions parameter has two properties.</span></span> <span data-ttu-id="7ead7-280">首先，确认属性用于显示一个弹出窗口 JavaScript 确认对话框。</span><span class="sxs-lookup"><span data-stu-id="7ead7-280">First, the Confirm property is used to display a popup JavaScript confirmation dialog.</span></span> <span data-ttu-id="7ead7-281">其次，HttpMethod 属性用于执行 HTTP DELETE 操作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-281">Second, the HttpMethod property is used to perform an HTTP DELETE operation.</span></span>

<span data-ttu-id="7ead7-282">列表 7 包含已添加到联系人控制器的新 AjaxDelete() 操作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-282">Listing 7 contains a new AjaxDelete() action that has been added to the Contact controller.</span></span>

<span data-ttu-id="7ead7-283">**列表 7-Controllers\ContactController.cs (AjaxDelete)**</span><span class="sxs-lookup"><span data-stu-id="7ead7-283">**Listing 7 - Controllers\ContactController.cs (AjaxDelete)**</span></span>

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample12.cs)]

<span data-ttu-id="7ead7-284">AjaxDelete() 操作是使用 AcceptVerbs 属性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="7ead7-284">The AjaxDelete() action is decorated with an AcceptVerbs attribute.</span></span> <span data-ttu-id="7ead7-285">此属性会阻止调用除了任何 HTTP 操作而不是 HTTP DELETE 操作的操作。</span><span class="sxs-lookup"><span data-stu-id="7ead7-285">This attribute prevents the action from being invoked except by any HTTP operation other than an HTTP DELETE operation.</span></span> <span data-ttu-id="7ead7-286">具体而言，不能调用此操作使用 HTTP GET。</span><span class="sxs-lookup"><span data-stu-id="7ead7-286">In particular, you cannot invoke this action with an HTTP GET.</span></span>

<span data-ttu-id="7ead7-287">删除数据库记录后，您需要显示更新的联系人列表不包含已删除的记录。</span><span class="sxs-lookup"><span data-stu-id="7ead7-287">After you delete database record, you need to display the updated list of contacts that does not contain the deleted record.</span></span> <span data-ttu-id="7ead7-288">AjaxDelete() 方法返回部分 ContactList 和更新的联系人列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-288">The AjaxDelete() method returns the ContactList partial and the updated list of contacts.</span></span>

## <a name="summary"></a><span data-ttu-id="7ead7-289">总结</span><span class="sxs-lookup"><span data-stu-id="7ead7-289">Summary</span></span>

<span data-ttu-id="7ead7-290">在此迭代中，我们添加 Ajax 功能到我们的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="7ead7-290">In this iteration, we added Ajax functionality to our Contact Manager application.</span></span> <span data-ttu-id="7ead7-291">我们使用 Ajax 来提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="7ead7-291">We used Ajax to improve the responsiveness and performance of our application.</span></span>

<span data-ttu-id="7ead7-292">首先，我们重构索引视图，以便单击联系人组不会更新整个视图。</span><span class="sxs-lookup"><span data-stu-id="7ead7-292">First, we refactored the Index view so that clicking a contact group does not update the entire view.</span></span> <span data-ttu-id="7ead7-293">相反，单击联系人组仅可更新联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-293">Instead, clicking a contact group only updates the list of contacts.</span></span>

<span data-ttu-id="7ead7-294">接下来，我们使用 jQuery 动画效果淡出和淡入的联系人列表。</span><span class="sxs-lookup"><span data-stu-id="7ead7-294">Next, we used jQuery animation effects to fade out and fade in the list of contacts.</span></span> <span data-ttu-id="7ead7-295">将动画添加到 Ajax 应用程序可以用于为浏览器进度栏的等效项的应用程序的用户提供。</span><span class="sxs-lookup"><span data-stu-id="7ead7-295">Adding animation to an Ajax application can be used to provide users of the application with the equivalent of a browser progress bar.</span></span>

<span data-ttu-id="7ead7-296">我们还添加到我们的 Ajax 应用程序的浏览器历史记录支持。</span><span class="sxs-lookup"><span data-stu-id="7ead7-296">We also added browser history support to our Ajax application.</span></span> <span data-ttu-id="7ead7-297">我们已启用的用户单击浏览器返回并转发按钮可以更改索引视图的状态。</span><span class="sxs-lookup"><span data-stu-id="7ead7-297">We enabled users to click the browser Back and Forward buttons to change the state of the Index view.</span></span>

<span data-ttu-id="7ead7-298">最后，我们创建支持 HTTP DELETE 操作的删除链接。</span><span class="sxs-lookup"><span data-stu-id="7ead7-298">Finally, we created a delete link that supports HTTP DELETE operations.</span></span> <span data-ttu-id="7ead7-299">通过执行 Ajax 删除，我们使用户能够删除数据库记录，而无需用户请求额外的删除确认页面。</span><span class="sxs-lookup"><span data-stu-id="7ead7-299">By performing Ajax deletes, we enable users to delete database records without requiring the user to request an additional delete confirmation page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7ead7-300">[上一页](iteration-6-use-test-driven-development-cs.md)
> [下一页](iteration-1-create-the-application-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7ead7-300">[Previous](iteration-6-use-test-driven-development-cs.md)
[Next](iteration-1-create-the-application-vb.md)</span></span>
