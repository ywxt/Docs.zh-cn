---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: '迭代 #5 – 创建单元测试 (C#) |Microsoft 文档'
author: microsoft
description: 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类，并生成单元测试 o...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: 7a61b5791a40088df9d27f7b1bd37df1831ef22b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="iteration-5--create-unit-tests-c"></a><span data-ttu-id="9745d-104">迭代 #5 – 创建单元测试 (C#)</span><span class="sxs-lookup"><span data-stu-id="9745d-104">Iteration #5 – Create unit tests (C#)</span></span>
====================
<span data-ttu-id="9745d-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9745d-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="9745d-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="9745d-106">Download Code</span></span>](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> <span data-ttu-id="9745d-107">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-107">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="9745d-108">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="9745d-108">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="9745d-109">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="9745d-109">Building a Contact Management ASP.NET MVC Application (C#)</span></span>

<span data-ttu-id="9745d-110">在这一系列的教程，我们生成整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="9745d-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="9745d-111">联系人管理器应用程序，可存储的名称，电话号码和电子邮件地址的联系人信息有关的人员列表。</span><span class="sxs-lookup"><span data-stu-id="9745d-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="9745d-112">我们在多次迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="9745d-113">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="9745d-114">此多个迭代方法旨在使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="9745d-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="9745d-115">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="9745d-116">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="9745d-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="9745d-117">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="9745d-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="9745d-118">迭代 #2-使应用程序，看上去很好。</span><span class="sxs-lookup"><span data-stu-id="9745d-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="9745d-119">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="9745d-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="9745d-120">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="9745d-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="9745d-121">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="9745d-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="9745d-122">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="9745d-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="9745d-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="9745d-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="9745d-124">迭代 #4-请松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="9745d-125">在此第三个迭代中，我们利用多个软件设计模式以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="9745d-126">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="9745d-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="9745d-127">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="9745d-128">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="9745d-129">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="9745d-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="9745d-130">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="9745d-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="9745d-131">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="9745d-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="9745d-132">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="9745d-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="9745d-133">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="9745d-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="9745d-134">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="9745d-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="9745d-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="9745d-135">This Iteration</span></span>

<span data-ttu-id="9745d-136">在联系人管理器应用程序前一次迭代，我们将重构要更为松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-136">In the previous iteration of the Contact Manager application, we refactored the application to be more loosely coupled.</span></span> <span data-ttu-id="9745d-137">我们分隔到不同的控制器、 服务和存储库层应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-137">We separated the application into distinct controller, service, and repository layers.</span></span> <span data-ttu-id="9745d-138">与通过接口它下面的层交互，每个图层。</span><span class="sxs-lookup"><span data-stu-id="9745d-138">Each layer interacts with the layer beneath it through interfaces.</span></span>

<span data-ttu-id="9745d-139">我们将重构应用程序，以便更轻松地监视和修改应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-139">We refactored the application to make the application easier to maintain and modify.</span></span> <span data-ttu-id="9745d-140">例如，如果我们需要使用新的数据访问技术，我们只需可以直接更改存储库层，而无需触摸控制器或服务层。</span><span class="sxs-lookup"><span data-stu-id="9745d-140">For example, if we need to use a new data access technology, we can simply change the repository layer without touching the controller or service layer.</span></span> <span data-ttu-id="9745d-141">通过进行松散耦合，Contact Manager 我们进行了应用程序更具弹性，若要更改。</span><span class="sxs-lookup"><span data-stu-id="9745d-141">By making the Contact Manager loosely coupled, we ve made the application more resilient to change.</span></span>

<span data-ttu-id="9745d-142">但是，当我们需要将一项新功能添加到联系人管理器应用程序时，会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="9745d-142">But, what happens when we need to add a new feature to the Contact Manager application?</span></span> <span data-ttu-id="9745d-143">或者，当我们修复 bug 时，会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="9745d-143">Or, what happens when we fix a bug?</span></span> <span data-ttu-id="9745d-144">编写代码的很遗憾，但也经过验证，事实是，每当你触摸创建引入新 bug 的风险的代码。</span><span class="sxs-lookup"><span data-stu-id="9745d-144">A sad, but well proven, truth of writing code is that whenever you touch code you create the risk of introducing new bugs.</span></span>

<span data-ttu-id="9745d-145">例如，一个好的一天，你的经理可能会要求你添加到联系人管理器中的一项新功能。</span><span class="sxs-lookup"><span data-stu-id="9745d-145">For example, one fine day, your manager might ask you to add a new feature to the Contact Manager.</span></span> <span data-ttu-id="9745d-146">她希望添加联系人组的支持。</span><span class="sxs-lookup"><span data-stu-id="9745d-146">She wants you to add support for Contact Groups.</span></span> <span data-ttu-id="9745d-147">她希望你以使用户能够将他们的联系人组织到组，例如友元，业务，依次类推。</span><span class="sxs-lookup"><span data-stu-id="9745d-147">She wants you to enable users to organize their contacts into groups such as Friends, Business, and so on.</span></span>

<span data-ttu-id="9745d-148">为了实现这一新功能，你将需要修改的联系人管理器应用程序的所有三个层。</span><span class="sxs-lookup"><span data-stu-id="9745d-148">In order to implement this new feature, you'll need to modify all three layers of the Contact Manager application.</span></span> <span data-ttu-id="9745d-149">你将需要将新功能添加到服务层，并存储库中的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="9745d-149">You'll need to add new functionality to the controllers, the service layer, and the repository.</span></span> <span data-ttu-id="9745d-150">只要你开始修改代码，则可能中断之前处理的功能。</span><span class="sxs-lookup"><span data-stu-id="9745d-150">As soon as you start modifying code, you risk breaking functionality that worked before.</span></span>

<span data-ttu-id="9745d-151">重构到单独的层，我们的应用程序，正如我们在前一次迭代，做了一件好事。</span><span class="sxs-lookup"><span data-stu-id="9745d-151">Refactoring our application into separate layers, as we did in the previous iteration, was a good thing.</span></span> <span data-ttu-id="9745d-152">它是一件好事，因为它使我们能够对整个层进行更改，而无需触摸应用程序的其余部分。</span><span class="sxs-lookup"><span data-stu-id="9745d-152">It was a good thing because it enables us to make changes to entire layers without touching the rest of the application.</span></span> <span data-ttu-id="9745d-153">但是，如果你想要轻松地监视和修改在层内的代码，你需要创建代码的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-153">However, if you want to make the code within a layer easier to maintain and modify, you need to create unit tests for the code.</span></span>

<span data-ttu-id="9745d-154">你使用单元测试来测试代码的单个单元。</span><span class="sxs-lookup"><span data-stu-id="9745d-154">You use a unit test to test an individual unit of code.</span></span> <span data-ttu-id="9745d-155">代码的这些单位为小于整个应用程序层。</span><span class="sxs-lookup"><span data-stu-id="9745d-155">These units of code are smaller than entire application layers.</span></span> <span data-ttu-id="9745d-156">通常，你可以使用单元测试以验证你的代码中的特定方法的行为是否你预期的方式。</span><span class="sxs-lookup"><span data-stu-id="9745d-156">Typically, you use a unit test to verify whether a particular method in your code behaves in the way that you expect.</span></span> <span data-ttu-id="9745d-157">例如，你将创建由 ContactManagerService 类公开的 CreateContact() 方法的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-157">For example, you would create a unit test for the CreateContact() method exposed by the ContactManagerService class.</span></span>

<span data-ttu-id="9745d-158">只是应用程序工作的单元测试，如网络安全。</span><span class="sxs-lookup"><span data-stu-id="9745d-158">The unit tests for an application work just like a safety net.</span></span> <span data-ttu-id="9745d-159">每当你修改应用程序中的代码，你可以运行单元测试以检查是否修改将断开现有功能的一组。</span><span class="sxs-lookup"><span data-stu-id="9745d-159">Whenever you modify code in an application, you can run a set of unit tests to check whether the modification breaks existing functionality.</span></span> <span data-ttu-id="9745d-160">单元测试，你的代码可以更安全地修改。</span><span class="sxs-lookup"><span data-stu-id="9745d-160">Unit tests make your code safe to modify.</span></span> <span data-ttu-id="9745d-161">单元测试进行的所有代码中你的应用程序更具弹性，若要更改。</span><span class="sxs-lookup"><span data-stu-id="9745d-161">Unit tests make all of the code in your application more resilient to change.</span></span>

<span data-ttu-id="9745d-162">在此迭代中，我们将单元测试添加到我们的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-162">In this iteration, we add unit tests to our Contact Manager application.</span></span> <span data-ttu-id="9745d-163">这样一来，在下一个迭代中，我们可以添加联系人组到我们的应用程序而无需担心破坏现有功能。</span><span class="sxs-lookup"><span data-stu-id="9745d-163">That way, in the next iteration, we can add Contact Groups to our application without worrying about breaking existing functionality.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9745d-164">有大量的单元测试框架，包括 NUnit、 xUnit.net 和 MbUnit。</span><span class="sxs-lookup"><span data-stu-id="9745d-164">There are a variety of unit testing frameworks including NUnit, xUnit.net, and MbUnit.</span></span> <span data-ttu-id="9745d-165">在本教程中，我们使用的单元测试框架随 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9745d-165">In this tutorial, we use the unit testing framework included with Visual Studio.</span></span> <span data-ttu-id="9745d-166">但是，你可以轻松地使用这些替代框架之一。</span><span class="sxs-lookup"><span data-stu-id="9745d-166">However, you could just as easily use one of these alternative frameworks.</span></span>


## <a name="what-gets-tested"></a><span data-ttu-id="9745d-167">什么获取测试</span><span class="sxs-lookup"><span data-stu-id="9745d-167">What Gets Tested</span></span>

<span data-ttu-id="9745d-168">在理想情况下，所有代码将被覆盖的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-168">In the perfect world, all of your code would be covered by unit tests.</span></span> <span data-ttu-id="9745d-169">在理想情况下，你将必须完美的网络安全。</span><span class="sxs-lookup"><span data-stu-id="9745d-169">In the perfect world, you would have the perfect safety net.</span></span> <span data-ttu-id="9745d-170">你将能够修改任意应用程序中的代码行，并且知道此时，通过执行单元测试，更改是否中断现有功能。</span><span class="sxs-lookup"><span data-stu-id="9745d-170">You would be able to modify any line of code in your application and know instantly, by executing your unit tests, whether the change broke existing functionality.</span></span>

<span data-ttu-id="9745d-171">但是，我们并不理想的环境中的实时 t。</span><span class="sxs-lookup"><span data-stu-id="9745d-171">However, we don t live in a perfect world.</span></span> <span data-ttu-id="9745d-172">在实践中，编写单元测试时，你专注于编写你的业务逻辑 （例如，验证逻辑） 的测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-172">In practice, when writing unit tests, you concentrate on writing tests for your business logic (for example, validation logic).</span></span> <span data-ttu-id="9745d-173">具体而言，你*不这样做*编写单元测试为你的数据访问逻辑或你的视图逻辑。</span><span class="sxs-lookup"><span data-stu-id="9745d-173">In particular, you *do not* write unit tests for your data access logic or your view logic.</span></span>

<span data-ttu-id="9745d-174">若要有一定用处，单元测试必须执行得非常快。</span><span class="sxs-lookup"><span data-stu-id="9745d-174">To be useful, unit tests must execute very quickly.</span></span> <span data-ttu-id="9745d-175">轻松，你可以累积数百 （或甚至数千） 的应用程序的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-175">You easily can accumulate hundreds (or even thousands) of unit tests for an application.</span></span> <span data-ttu-id="9745d-176">如果单元测试需要很长时间才能运行你可以避免执行它们。</span><span class="sxs-lookup"><span data-stu-id="9745d-176">If the unit tests take a long time to run then you'll avoid executing them.</span></span> <span data-ttu-id="9745d-177">换而言之，长时间运行的单元测试是对于每天编码用途没有用处。</span><span class="sxs-lookup"><span data-stu-id="9745d-177">In other words, long running unit tests are useless for day to day coding purposes.</span></span>

<span data-ttu-id="9745d-178">为此，你通常不要编写的数据库交互的代码的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-178">For this reason, you typically do not write unit tests for code that interacts with a database.</span></span> <span data-ttu-id="9745d-179">实时数据库运行数百个单元测试将太慢。</span><span class="sxs-lookup"><span data-stu-id="9745d-179">Running hundreds of unit tests against a live database would be too slow.</span></span> <span data-ttu-id="9745d-180">相反，模拟你的数据库，并编写与模拟 （我们讨论模拟以下数据库） 的数据库交互的代码。</span><span class="sxs-lookup"><span data-stu-id="9745d-180">Instead, you mock your database and write code that interacts with the mock database (we discuss mocking a database below).</span></span>

<span data-ttu-id="9745d-181">类似的原因，你通常不要编写视图的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-181">For a similar reason, you typically do not write unit tests for views.</span></span> <span data-ttu-id="9745d-182">若要测试的视图，你必须启动 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9745d-182">In order to test a view, you must spin up a web server.</span></span> <span data-ttu-id="9745d-183">由于运转的 web 服务器是一个相对较慢的过程，不建议为你的视图创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-183">Because spinning up a web server is a relatively slow process, creating unit tests for your views is not recommended.</span></span>

<span data-ttu-id="9745d-184">如果你的视图包含复杂的逻辑则应考虑将逻辑移到帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-184">If your view contains complicated logic then you should consider moving the logic into Helper methods.</span></span> <span data-ttu-id="9745d-185">你可以编写执行而不在运转的 web 服务器的帮助器方法的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-185">You can write unit tests for Helper methods that execute without spinning up a web server.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9745d-186">虽然编写测试数据访问逻辑或视图逻辑不是一个不错的主意编写单元测试时，这些测试可在构建功能或集成测试时非常有价值。</span><span class="sxs-lookup"><span data-stu-id="9745d-186">While writing tests for data access logic or view logic is not a good idea when writing unit tests, these tests can be very valuable when building functional or integration tests.</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="9745d-187">ASP.NET MVC 是 Web 窗体视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9745d-187">ASP.NET MVC is the Web Forms View Engine.</span></span> <span data-ttu-id="9745d-188">Web 窗体视图引擎依赖于 web 服务器时，可能不是其他视图引擎。</span><span class="sxs-lookup"><span data-stu-id="9745d-188">While the Web Forms View Engine is dependent on a web server, other view engines might not be.</span></span>


## <a name="using-a-mock-object-framework"></a><span data-ttu-id="9745d-189">使用模拟对象框架</span><span class="sxs-lookup"><span data-stu-id="9745d-189">Using a Mock Object Framework</span></span>

<span data-ttu-id="9745d-190">在生成单元测试时，你几乎总是需要利用模拟对象框架。</span><span class="sxs-lookup"><span data-stu-id="9745d-190">When building unit tests, you almost always need to take advantage of a Mock Object framework.</span></span> <span data-ttu-id="9745d-191">模拟对象框架，可在你的应用程序中创建 mock 和类的存根。</span><span class="sxs-lookup"><span data-stu-id="9745d-191">A Mock Object framework enables you to create mocks and stubs for the classes in your application.</span></span>

<span data-ttu-id="9745d-192">例如，可以使用模拟对象框架来生成你的存储库类的模型版本。</span><span class="sxs-lookup"><span data-stu-id="9745d-192">For example, you can use a Mock Object framework to generate a mock version of your repository class.</span></span> <span data-ttu-id="9745d-193">这样一来，你可以使用模拟的存储库类而不是实际的存储库类在单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-193">That way, you can use the mock repository class instead of the real repository class in your unit tests.</span></span> <span data-ttu-id="9745d-194">使用模拟的存储库，可避免执行单元测试时执行数据库的代码。</span><span class="sxs-lookup"><span data-stu-id="9745d-194">Using the mock repository enables you to avoid executing database code when executing a unit test.</span></span>

<span data-ttu-id="9745d-195">Visual Studio 不包括一个模拟对象框架。</span><span class="sxs-lookup"><span data-stu-id="9745d-195">Visual Studio does not include a Mock Object framework.</span></span> <span data-ttu-id="9745d-196">但是，有可用于.NET framework 的多个商业和开放源代码模拟对象框架：</span><span class="sxs-lookup"><span data-stu-id="9745d-196">However, there are several commercial and open source Mock Object frameworks available for the .NET framework:</span></span>

1. <span data-ttu-id="9745d-197">Moq-此框架，请参阅的开放源代码 BSD 许可。</span><span class="sxs-lookup"><span data-stu-id="9745d-197">Moq - This framework is available under the open source BSD license.</span></span> <span data-ttu-id="9745d-198">你可以下载从 Moq [ https://code.google.com/p/moq/ ](https://code.google.com/p/moq/)。</span><span class="sxs-lookup"><span data-stu-id="9745d-198">You can download Moq from [https://code.google.com/p/moq/](https://code.google.com/p/moq/).</span></span>
2. <span data-ttu-id="9745d-199">Rhino Mocks-此框架是开放源代码 BSD 许可下可用。</span><span class="sxs-lookup"><span data-stu-id="9745d-199">Rhino Mocks - This framework is available under the open source BSD license.</span></span> <span data-ttu-id="9745d-200">你可以下载 Rhino Mocks 从[ http://ayende.com/projects/rhino-mocks.aspx ](http://ayende.com/projects/rhino-mocks.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9745d-200">You can download Rhino Mocks from [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx).</span></span>
3. <span data-ttu-id="9745d-201">Typemock 隔离器-这是一个商业框架。</span><span class="sxs-lookup"><span data-stu-id="9745d-201">Typemock Isolator - This is a commercial framework.</span></span> <span data-ttu-id="9745d-202">你可以下载从试用版[ http://www.typemock.com/ ](http://www.typemock.com/)。</span><span class="sxs-lookup"><span data-stu-id="9745d-202">You can download a trial version from [http://www.typemock.com/](http://www.typemock.com/).</span></span>

<span data-ttu-id="9745d-203">在本教程中，我决定使用 Moq。</span><span class="sxs-lookup"><span data-stu-id="9745d-203">In this tutorial, I decided to use Moq.</span></span> <span data-ttu-id="9745d-204">但是，你可以轻松地使用 Rhino Mocks Typemock 隔离器创建模型的对象或联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-204">However, you could just as easily use Rhino Mocks or Typemock Isolator to create the Mock objects for the Contact Manager application.</span></span>

<span data-ttu-id="9745d-205">你可以使用 Moq 之前，你需要完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="9745d-205">Before you can use Moq, you need to complete the following steps:</span></span>

1. <span data-ttu-id="9745d-206">.</span><span class="sxs-lookup"><span data-stu-id="9745d-206">.</span></span>
2. <span data-ttu-id="9745d-207">解压缩下载之前，请确保你右键单击该文件，然后单击标记按钮**解除阻止**（请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="9745d-207">Before you unzip the download, make sure that you right-click the file and click the button labeled **Unblock** (see Figure 1).</span></span>
3. <span data-ttu-id="9745d-208">解压缩下载。</span><span class="sxs-lookup"><span data-stu-id="9745d-208">Unzip the download.</span></span>
4. <span data-ttu-id="9745d-209">通过右键单击 ContactManager.Tests 项目中的引用文件夹并选择添加 Moq 程序集的引用**添加引用**。</span><span class="sxs-lookup"><span data-stu-id="9745d-209">Add a reference to the Moq assembly by right-clicking the References folder in the ContactManager.Tests project and selecting **Add Reference**.</span></span> <span data-ttu-id="9745d-210">在浏览选项卡，浏览到您在其中解压缩 Moq 的文件夹并选择 Moq.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="9745d-210">Under the Browse tab, browse to the folder where you unzipped Moq and select the Moq.dll assembly.</span></span> <span data-ttu-id="9745d-211">单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="9745d-211">Click the **OK** button.</span></span>
5. <span data-ttu-id="9745d-212">完成这些步骤后，你的引用的文件夹应如下所示图 2。</span><span class="sxs-lookup"><span data-stu-id="9745d-212">After you complete these steps, your References folder should look like Figure 2.</span></span>


<span data-ttu-id="9745d-213">[![取消阻塞 Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9745d-213">[![Unblocking Moq](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)</span></span>

<span data-ttu-id="9745d-214">**图 01**： 取消阻塞 Moq ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9745d-214">**Figure 01**: Unblocking Moq([Click to view full-size image](iteration-5-create-unit-tests-cs/_static/image2.png))</span></span>


<span data-ttu-id="9745d-215">[![在添加 Moq 后的引用](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="9745d-215">[![References after adding Moq](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)</span></span>

<span data-ttu-id="9745d-216">**图 02**： 添加 Moq 后的引用 ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="9745d-216">**Figure 02**: References after adding Moq([Click to view full-size image](iteration-5-create-unit-tests-cs/_static/image4.png))</span></span>


## <a name="creating-unit-tests-for-the-service-layer"></a><span data-ttu-id="9745d-217">为服务层创建单元测试</span><span class="sxs-lookup"><span data-stu-id="9745d-217">Creating Unit Tests for the Service Layer</span></span>

<span data-ttu-id="9745d-218">让我们来首先创建一组我们联系人管理器应用程序 s 服务层的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-218">Let s start by creating a set of unit tests for our Contact Manager application s service layer.</span></span> <span data-ttu-id="9745d-219">我们将使用这些测试来验证我们验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="9745d-219">We'll use these tests to verify our validation logic.</span></span>

<span data-ttu-id="9745d-220">创建 ContactManager.Tests 项目中名为 Models 的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="9745d-220">Create a new folder named Models in the ContactManager.Tests project.</span></span> <span data-ttu-id="9745d-221">接下来，右键单击 Models 文件夹，然后选择**添加、 新的测试**。</span><span class="sxs-lookup"><span data-stu-id="9745d-221">Next, right-click the Models folder and select **Add, New Test**.</span></span> <span data-ttu-id="9745d-222">**添加新测试**此时将显示图 3 所示的对话框。</span><span class="sxs-lookup"><span data-stu-id="9745d-222">The **Add New Test** dialog shown in Figure 3 appears.</span></span> <span data-ttu-id="9745d-223">选择**单元测试**模板并命名为新的测试 ContactManagerServiceTest.cs。</span><span class="sxs-lookup"><span data-stu-id="9745d-223">Select the **Unit Test** template and name your new test ContactManagerServiceTest.cs.</span></span> <span data-ttu-id="9745d-224">单击**确定**按钮以向测试项目中添加新的测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-224">Click the **OK** button to add your new test to your Test Project.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9745d-225">一般情况下，你希望测试项目中以匹配你的 ASP.NET MVC 项目的文件夹结构的文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="9745d-225">In general, you want the folder structure of your Test Project to match the folder structure of your ASP.NET MVC project.</span></span> <span data-ttu-id="9745d-226">例如，你将控制器测试放在控制器文件夹中，模型测试中的模型文件夹中，依次类推。</span><span class="sxs-lookup"><span data-stu-id="9745d-226">For example, you place controller tests in a Controllers folder, model tests in a Models folder, and so on.</span></span>


<span data-ttu-id="9745d-227">[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="9745d-227">[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)</span></span>

<span data-ttu-id="9745d-228">**图 03**: Models\ContactManagerServiceTest.cs ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="9745d-228">**Figure 03**: Models\ContactManagerServiceTest.cs([Click to view full-size image](iteration-5-create-unit-tests-cs/_static/image6.png))</span></span>


<span data-ttu-id="9745d-229">最初，我们想要测试由 ContactManagerService 类公开的 CreateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-229">Initially, we want to test the CreateContact() method exposed by the ContactManagerService class.</span></span> <span data-ttu-id="9745d-230">我们将创建下列五项测试：</span><span class="sxs-lookup"><span data-stu-id="9745d-230">We'll create the following five tests:</span></span>

- <span data-ttu-id="9745d-231">CreateContact()-向方法传递有效联系人时，测试该 CreateContact() 返回值 true。</span><span class="sxs-lookup"><span data-stu-id="9745d-231">CreateContact() - Tests that CreateContact() returns the value true when a valid Contact is passed to the method.</span></span>
- <span data-ttu-id="9745d-232">CreateContactRequiredFirstName() 的测试，将一条错误消息添加到模型状态时与缺少的第一个名称传递给 CreateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-232">CreateContactRequiredFirstName() - Tests that an error message is added to model state when a Contact with a missing first name is passed to the CreateContact() method.</span></span>
- <span data-ttu-id="9745d-233">CreateContactRequredLastName() 的测试，将一条错误消息添加到模型时缺少姓氏的联系人的状态被传递给 CreateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-233">CreateContactRequredLastName() - Tests that an error message is added to model state when a Contact with a missing last name is passed to the CreateContact() method.</span></span>
- <span data-ttu-id="9745d-234">CreateContactInvalidPhone() 的测试，将一条错误消息添加到模型状态时具有电话号码无效的协定传递给 CreateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-234">CreateContactInvalidPhone() - Tests that an error message is added to model state when a Contact with an invalid phone number is passed to the CreateContact() method.</span></span>
- <span data-ttu-id="9745d-235">CreateContactInvalidEmail() 的测试，将一条错误消息添加到模型时使用无效的电子邮件地址的联系人的状态被传递给 CreateContact() 方法...</span><span class="sxs-lookup"><span data-stu-id="9745d-235">CreateContactInvalidEmail() - Tests that an error message is added to model state when a Contact with an invalid email address is passed to the CreateContact() method..</span></span>

<span data-ttu-id="9745d-236">第一个测试验证有效联系人不会生成验证错误。</span><span class="sxs-lookup"><span data-stu-id="9745d-236">The first test verifies that a valid Contact does not generate a validation error.</span></span> <span data-ttu-id="9745d-237">其余测试，检查每个验证规则。</span><span class="sxs-lookup"><span data-stu-id="9745d-237">The remaining tests check each of the validation rules.</span></span>

<span data-ttu-id="9745d-238">列表 1 中包含这些测试的代码。</span><span class="sxs-lookup"><span data-stu-id="9745d-238">The code for these tests is contained in Listing 1.</span></span>

<span data-ttu-id="9745d-239">**Listing 1 - Models\ContactManagerServiceTest.cs**</span><span class="sxs-lookup"><span data-stu-id="9745d-239">**Listing 1 - Models\ContactManagerServiceTest.cs**</span></span>

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]


<span data-ttu-id="9745d-240">由于我们在列出 1 中使用联系人类，因此我们需要我们的测试项目添加到 Microsoft 的实体框架的引用。</span><span class="sxs-lookup"><span data-stu-id="9745d-240">Because we use the Contact class in Listing 1, we need to add a reference to the Microsoft Entity Framework to our Test project.</span></span> <span data-ttu-id="9745d-241">添加对 System.Data.Entity 程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="9745d-241">Add a reference to the System.Data.Entity assembly.</span></span>


<span data-ttu-id="9745d-242">列表 1 包含一个名为使用 [TestInitialize] 特性修饰的 initialize （） 方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-242">Listing 1 contains a method named Initialize() that is decorated with the [TestInitialize] attribute.</span></span> <span data-ttu-id="9745d-243">每个单元测试运行之前自动调用此方法 （它每个单元测试前称为 5 次）。</span><span class="sxs-lookup"><span data-stu-id="9745d-243">This method is called automatically before each of the unit tests is run (it is called 5 times right before each of the unit tests).</span></span> <span data-ttu-id="9745d-244">Initialize （） 方法创建具有以下代码行的模拟的存储库：</span><span class="sxs-lookup"><span data-stu-id="9745d-244">The Initialize() method creates a mock repository with the following line of code:</span></span>

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

<span data-ttu-id="9745d-245">此代码行使用 Moq 框架从 IContactManagerRepository 接口生成的模拟的存储库。</span><span class="sxs-lookup"><span data-stu-id="9745d-245">This line of code uses the Moq framework to generate a mock repository from the IContactManagerRepository interface.</span></span> <span data-ttu-id="9745d-246">模拟的存储库而不是实际 EntityContactManagerRepository 用于避免每个单元测试运行时访问数据库。</span><span class="sxs-lookup"><span data-stu-id="9745d-246">The mock repository is used instead of the actual EntityContactManagerRepository to avoid accessing the database when each unit test is run.</span></span> <span data-ttu-id="9745d-247">模拟的存储库实现的方法 IContactManagerRepository 接口，但方法 don t 实际执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="9745d-247">The mock repository implements the methods of the IContactManagerRepository interface, but the methods don t actually do anything.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9745d-248">当使用 Moq 框架，没有区分\_mockRepository 和\_mockRepository.Object。</span><span class="sxs-lookup"><span data-stu-id="9745d-248">When using the Moq framework, there is a distinction between \_mockRepository and \_mockRepository.Object.</span></span> <span data-ttu-id="9745d-249">前者指 Mock&lt;IContactManagerRepository&gt;类，其中包含用于指定模拟的存储库的行为方式的方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-249">The former refers to the Mock&lt;IContactManagerRepository&gt; class that contains methods for specifying how the mock repository will behave.</span></span> <span data-ttu-id="9745d-250">后者是指实现 IContactManagerRepository 接口的实际模拟存储库。</span><span class="sxs-lookup"><span data-stu-id="9745d-250">The latter refers to the actual mock repository that implements the IContactManagerRepository interface.</span></span>


<span data-ttu-id="9745d-251">创建 ContactManagerService 类的实例时，将在 initialize （） 方法中使用模拟的存储库。</span><span class="sxs-lookup"><span data-stu-id="9745d-251">The mock repository is used in the Initialize() method when creating an instance of the ContactManagerService class.</span></span> <span data-ttu-id="9745d-252">单个单元测试的所有使用 ContactManagerService 类的此实例。</span><span class="sxs-lookup"><span data-stu-id="9745d-252">All of the individual unit tests use this instance of the ContactManagerService class.</span></span>

<span data-ttu-id="9745d-253">列表 1 包含五个方法对应于每个单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-253">Listing 1 contains five methods that correspond to each of the unit tests.</span></span> <span data-ttu-id="9745d-254">上述每种方法是使用 [TestMethod] 特性修饰。</span><span class="sxs-lookup"><span data-stu-id="9745d-254">Each of these methods is decorated with the [TestMethod] attribute.</span></span> <span data-ttu-id="9745d-255">运行单元测试时，调用任何具有此属性的方法。</span><span class="sxs-lookup"><span data-stu-id="9745d-255">When you run the unit tests, any method that has this attribute is called.</span></span> <span data-ttu-id="9745d-256">换而言之，任何使用 [TestMethod] 特性修饰的方法是单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-256">In other words, any method that is decorated with the [TestMethod] attribute is a unit test.</span></span>

<span data-ttu-id="9745d-257">名为 CreateContact()，第一个单元测试验证，请与类的有效实例传递给方法时，调用 CreateContact() 返回值 true。</span><span class="sxs-lookup"><span data-stu-id="9745d-257">The first unit test, named CreateContact(), verifies that calling CreateContact() returns the value true when a valid instance of the Contact class is passed to the method.</span></span> <span data-ttu-id="9745d-258">测试创建联系人类的实例、 调用 CreateContact() 方法，并验证 CreateContact() 返回值 true。</span><span class="sxs-lookup"><span data-stu-id="9745d-258">The test creates an instance of the Contact class, calls the CreateContact() method, and verifies that CreateContact() returns the value true.</span></span>

<span data-ttu-id="9745d-259">剩余的测试验证当 CreateContact() 方法被调用无效的联系人时然后该方法返回 false 并预期的验证错误消息添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="9745d-259">The remaining tests verify that when the CreateContact() method is called with an invalid Contact then the method returns false and the expected validation error message is added to model state.</span></span> <span data-ttu-id="9745d-260">例如，CreateContactRequiredFirstName() 测试使用空字符串作为其 FirstName 属性创建联系人类的实例。</span><span class="sxs-lookup"><span data-stu-id="9745d-260">For example, the CreateContactRequiredFirstName() test creates an instance of the Contact class with an empty string for its FirstName property.</span></span> <span data-ttu-id="9745d-261">接下来，CreateContact() 方法已调用无效的联系人。</span><span class="sxs-lookup"><span data-stu-id="9745d-261">Next, the CreateContact() method is called with the invalid Contact.</span></span> <span data-ttu-id="9745d-262">最后，此项测试确认 CreateContact() 返回 false，模型状态包含预期的验证错误消息"名字是必需的。"</span><span class="sxs-lookup"><span data-stu-id="9745d-262">Finally, the test verifies that CreateContact() returns false and that model state contains the expected validation error message "First name is required."</span></span>

<span data-ttu-id="9745d-263">你可以列出 1 中运行单元测试，通过选择菜单选项**测试，运行，解决方案 （CTRL + R、 A） 中的所有测试**。</span><span class="sxs-lookup"><span data-stu-id="9745d-263">You can run the unit tests in Listing 1 by selecting the menu option **Test, Run, All Tests in Solution (CTRL+R, A)**.</span></span> <span data-ttu-id="9745d-264">测试的结果将显示在测试结果窗口 （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="9745d-264">The results of the tests are displayed in the Test Results window (see Figure 4).</span></span>


<span data-ttu-id="9745d-265">[![测试结果](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9745d-265">[![Test Results](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)</span></span>

<span data-ttu-id="9745d-266">**图 04**： 测试结果 ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="9745d-266">**Figure 04**: Test Results ([Click to view full-size image](iteration-5-create-unit-tests-cs/_static/image8.png))</span></span>


## <a name="creating-unit-tests-for-controllers"></a><span data-ttu-id="9745d-267">为控制器创建单元测试</span><span class="sxs-lookup"><span data-stu-id="9745d-267">Creating Unit Tests for Controllers</span></span>

<span data-ttu-id="9745d-268">ASP.NETMVC 应用程序控制的用户交互的流。</span><span class="sxs-lookup"><span data-stu-id="9745d-268">ASP.NETMVC application control the flow of user interaction.</span></span> <span data-ttu-id="9745d-269">当测试控制器时，你想要测试是否则控制器将返回正确的操作结果和查看数据。</span><span class="sxs-lookup"><span data-stu-id="9745d-269">When testing a controller, you want to test whether the controller returns the right action result and view data.</span></span> <span data-ttu-id="9745d-270">你还可能想要测试是否与预期的方式的模型类的控制器交互。</span><span class="sxs-lookup"><span data-stu-id="9745d-270">You also might want to test whether a controller interacts with model classes in the manner expected.</span></span>

<span data-ttu-id="9745d-271">例如，清单 2 包含联系人控制器 create （） 方法的两个单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-271">For example, Listing 2 contains two unit tests for the Contact controller Create() method.</span></span> <span data-ttu-id="9745d-272">第一个单元测试验证有效联系人传递给 create （） 方法，则 create （） 方法将重定向到的索引操作时。</span><span class="sxs-lookup"><span data-stu-id="9745d-272">The first unit test verifies that when a valid Contact is passed to the Create() method then the Create() method redirects to the Index action.</span></span> <span data-ttu-id="9745d-273">换而言之，当传递有效的联系人，create （） 方法应返回表示索引操作 RedirectToRouteResult。</span><span class="sxs-lookup"><span data-stu-id="9745d-273">In other words, when passed a valid Contact, the Create() method should return a RedirectToRouteResult that represents the Index action.</span></span>

<span data-ttu-id="9745d-274">我们不想以测试我们正在测试的控制器层 ContactManager 服务层。</span><span class="sxs-lookup"><span data-stu-id="9745d-274">We don t want to test the ContactManager service layer when we are testing the controller layer.</span></span> <span data-ttu-id="9745d-275">因此，我们模拟替换为以下代码的 Initialize 方法中的服务层：</span><span class="sxs-lookup"><span data-stu-id="9745d-275">Therefore, we mock the service layer with the following code in the Initialize method:</span></span>

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

<span data-ttu-id="9745d-276">在 CreateValidContact() 单元测试中，我们可以模拟调用服务层具有以下代码行的 CreateContact() 方法的行为：</span><span class="sxs-lookup"><span data-stu-id="9745d-276">In the CreateValidContact() unit test, we mock the behavior of calling the service layer CreateContact() method with the following line of code:</span></span>

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

<span data-ttu-id="9745d-277">以下代码行将会导致模拟的 ContactManager 服务，以调用其 CreateContact() 方法时返回值 true。</span><span class="sxs-lookup"><span data-stu-id="9745d-277">This line of code causes the mock ContactManager service to return the value true when its CreateContact() method is called.</span></span> <span data-ttu-id="9745d-278">通过模拟的服务层，我们可以测试控制器的行为而无需在服务层中执行的任何代码。</span><span class="sxs-lookup"><span data-stu-id="9745d-278">By mocking the service layer, we can test the behavior of our controller without needing to execute any code in the service layer.</span></span>

<span data-ttu-id="9745d-279">第二个单元测试验证向方法传递无效的联系人时，create （） 操作，返回创建视图。</span><span class="sxs-lookup"><span data-stu-id="9745d-279">The second unit test verifies that the Create() action returns the Create view when an invalid contact is passed to the method.</span></span> <span data-ttu-id="9745d-280">我们会导致服务层 CreateContact() 方法来返回值 false 与以下代码行：</span><span class="sxs-lookup"><span data-stu-id="9745d-280">We cause the service layer CreateContact() method to return the value false with the following line of code:</span></span>

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

<span data-ttu-id="9745d-281">如果 create （） 方法的行为与我们的期望则应在服务层，则返回值 false 时返回创建视图。</span><span class="sxs-lookup"><span data-stu-id="9745d-281">If the Create() method behaves as we expect then it should return the Create view when the service layer returns the value false.</span></span> <span data-ttu-id="9745d-282">这样一来，控制器可以显示验证错误消息，在创建视图中，用户有可能更正该了无效的联系人属性。</span><span class="sxs-lookup"><span data-stu-id="9745d-282">That way, the controller can display the validation error messages in the Create view and the user has a chance to correct that invalid Contact properties.</span></span>


<span data-ttu-id="9745d-283">如果你打算生成你的控制器的单元测试然后你需要的控制器操作返回显式的视图名称。</span><span class="sxs-lookup"><span data-stu-id="9745d-283">If you plan to build unit tests for your controllers then you need to return explicit view names from your controller actions.</span></span> <span data-ttu-id="9745d-284">例如，不返回如下的视图：</span><span class="sxs-lookup"><span data-stu-id="9745d-284">For example, do not return a view like this:</span></span>

<span data-ttu-id="9745d-285">返回 View();</span><span class="sxs-lookup"><span data-stu-id="9745d-285">return View();</span></span>

<span data-ttu-id="9745d-286">相反，返回如下视图：</span><span class="sxs-lookup"><span data-stu-id="9745d-286">Instead, return the view like this:</span></span>

<span data-ttu-id="9745d-287">return View("Create");</span><span class="sxs-lookup"><span data-stu-id="9745d-287">return View("Create");</span></span>

<span data-ttu-id="9745d-288">如果不能显式返回视图时 ViewResult.ViewName 属性将返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="9745d-288">If you are not explicit when returning a view then the ViewResult.ViewName property returns an empty string.</span></span>


<span data-ttu-id="9745d-289">**Listing 2 - Controllers\ContactControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="9745d-289">**Listing 2 - Controllers\ContactControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a><span data-ttu-id="9745d-290">总结</span><span class="sxs-lookup"><span data-stu-id="9745d-290">Summary</span></span>

<span data-ttu-id="9745d-291">在此迭代中，我们为我们的联系人管理器应用程序创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-291">In this iteration, we created unit tests for our Contact Manager application.</span></span> <span data-ttu-id="9745d-292">我们可以在任何时间，以验证，我们的应用程序仍行为与我们的预期方式运行这些单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-292">We can run these unit tests at any time to verify that our application still behaves in the manner that we expect.</span></span> <span data-ttu-id="9745d-293">单元测试充当一个安全网络，使应用程序，使我们能够安全地修改在将来，我们的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9745d-293">The unit tests act as a safety net for our application enabling us to safely modify our application in the future.</span></span>

<span data-ttu-id="9745d-294">我们将创建两个集的单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-294">We created two sets of unit tests.</span></span> <span data-ttu-id="9745d-295">首先，为我们的服务层创建单元测试测试我们的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="9745d-295">First, we tested our validation logic by creating unit tests for our service layer.</span></span> <span data-ttu-id="9745d-296">接下来，我们测试我们的流控制逻辑为我们控制器层创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="9745d-296">Next, we tested our flow control logic by creating unit tests for our controller layer.</span></span> <span data-ttu-id="9745d-297">当测试我们的服务层，我们隔离的我们的测试我们的服务层从我们的存储库层通过模拟我们存储库层。</span><span class="sxs-lookup"><span data-stu-id="9745d-297">When testing our service layer, we isolated our tests for our service layer from our repository layer by mocking our repository layer.</span></span> <span data-ttu-id="9745d-298">当测试控制器层，我们隔离的我们的测试为我们控制器层通过模拟的服务层。</span><span class="sxs-lookup"><span data-stu-id="9745d-298">When testing the controller layer, we isolated our tests for our controller layer by mocking the service layer.</span></span>

<span data-ttu-id="9745d-299">在下一步的迭代中，我们将修改联系人管理器应用程序，以便它支持联系人组。</span><span class="sxs-lookup"><span data-stu-id="9745d-299">In the next iteration, we modify the Contact Manager application so that it supports Contact Groups.</span></span> <span data-ttu-id="9745d-300">我们将此新功能添加到我们的应用程序使用称为测试驱动开发的软件设计过程。</span><span class="sxs-lookup"><span data-stu-id="9745d-300">We'll add this new functionality to our application using a software design process called test-driven development.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9745d-301">[上一页](iteration-4-make-the-application-loosely-coupled-cs.md)
> [下一页](iteration-6-use-test-driven-development-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9745d-301">[Previous](iteration-4-make-the-application-loosely-coupled-cs.md)
[Next](iteration-6-use-test-driven-development-cs.md)</span></span>
