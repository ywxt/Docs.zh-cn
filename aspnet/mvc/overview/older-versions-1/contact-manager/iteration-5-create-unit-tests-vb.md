---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: 迭代 5 — 创建单元测试 (VB) |Microsoft Docs
author: microsoft
description: 在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。 我们模拟我们数据模型类和构建 o 的单元测试...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: 302dfc2a26e3f357818570c673eafe44346330c4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389997"
---
<a name="iteration-5--create-unit-tests-vb"></a><span data-ttu-id="826c0-104">迭代 5 — 创建单元测试 (VB)</span><span class="sxs-lookup"><span data-stu-id="826c0-104">Iteration #5 – Create unit tests (VB)</span></span>
====================
<span data-ttu-id="826c0-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="826c0-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="826c0-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="826c0-106">Download Code</span></span>](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> <span data-ttu-id="826c0-107">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-107">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="826c0-108">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-108">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="826c0-109">构建联系人管理 ASP.NET MVC 应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="826c0-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="826c0-110">在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="826c0-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="826c0-111">联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。</span><span class="sxs-lookup"><span data-stu-id="826c0-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="826c0-112">我们通过多个迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="826c0-113">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="826c0-114">此多个迭代方法的目标是帮助你了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="826c0-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="826c0-115">迭代 1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="826c0-116">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="826c0-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="826c0-117">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="826c0-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="826c0-118">迭代 2 – 使应用程序看上去更美观。</span><span class="sxs-lookup"><span data-stu-id="826c0-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="826c0-119">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="826c0-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="826c0-120">迭代 3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="826c0-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="826c0-121">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="826c0-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="826c0-122">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="826c0-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="826c0-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="826c0-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="826c0-124">迭代 4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="826c0-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="826c0-125">在此第三个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="826c0-126">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="826c0-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="826c0-127">迭代 5 — 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="826c0-128">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="826c0-129">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="826c0-130">迭代 6-使用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="826c0-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="826c0-131">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="826c0-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="826c0-132">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="826c0-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="826c0-133">迭代 7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="826c0-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="826c0-134">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="826c0-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="826c0-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="826c0-135">This Iteration</span></span>

<span data-ttu-id="826c0-136">上一次迭代中的联系人管理器应用程序，我们可以重构要更为松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-136">In the previous iteration of the Contact Manager application, we refactored the application to be more loosely coupled.</span></span> <span data-ttu-id="826c0-137">我们分隔到不同的控制器、 服务和存储库层应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-137">We separated the application into distinct controller, service, and repository layers.</span></span> <span data-ttu-id="826c0-138">与通过接口在它下面的层交互，每个层。</span><span class="sxs-lookup"><span data-stu-id="826c0-138">Each layer interacts with the layer beneath it through interfaces.</span></span>

<span data-ttu-id="826c0-139">我们重构应用程序，以便更轻松地监视和修改应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-139">We refactored the application to make the application easier to maintain and modify.</span></span> <span data-ttu-id="826c0-140">例如，如果我们需要使用新的数据访问技术，我们只需可以直接更改存储库层，而无需涉及控制器或服务层。</span><span class="sxs-lookup"><span data-stu-id="826c0-140">For example, if we need to use a new data access technology, we can simply change the repository layer without touching the controller or service layer.</span></span> <span data-ttu-id="826c0-141">松散耦合，联系人管理器发出我们进行了应用程序更具弹性，若要更改。</span><span class="sxs-lookup"><span data-stu-id="826c0-141">By making the Contact Manager loosely coupled, we ve made the application more resilient to change.</span></span>

<span data-ttu-id="826c0-142">但是，当我们需要将一项新功能添加到联系人管理器应用程序时，会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="826c0-142">But, what happens when we need to add a new feature to the Contact Manager application?</span></span> <span data-ttu-id="826c0-143">或者，当我们修复 bug 时，会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="826c0-143">Or, what happens when we fix a bug?</span></span> <span data-ttu-id="826c0-144">编写代码的一个很遗憾，但也经实践证明的事实是，每当改动代码创建引入新 bug 的风险。</span><span class="sxs-lookup"><span data-stu-id="826c0-144">A sad, but well proven, truth of writing code is that whenever you touch code you create the risk of introducing new bugs.</span></span>

<span data-ttu-id="826c0-145">例如，一个的最好时期，你的经理可能会要求你添加到联系人管理器中的一项新功能。</span><span class="sxs-lookup"><span data-stu-id="826c0-145">For example, one fine day, your manager might ask you to add a new feature to the Contact Manager.</span></span> <span data-ttu-id="826c0-146">她希望您将添加对联系人组的支持。</span><span class="sxs-lookup"><span data-stu-id="826c0-146">She wants you to add support for Contact Groups.</span></span> <span data-ttu-id="826c0-147">她希望您为了使用户能够将其联系人组织成组如朋友、 业务和等等。</span><span class="sxs-lookup"><span data-stu-id="826c0-147">She wants you to enable users to organize their contacts into groups such as Friends, Business, and so on.</span></span>

<span data-ttu-id="826c0-148">为了实现这一新功能，您将需要修改的联系人管理器应用程序的所有三个层。</span><span class="sxs-lookup"><span data-stu-id="826c0-148">In order to implement this new feature, you'll need to modify all three layers of the Contact Manager application.</span></span> <span data-ttu-id="826c0-149">你将需要将新功能添加到服务层，并在存储库的所有控制器。</span><span class="sxs-lookup"><span data-stu-id="826c0-149">You'll need to add new functionality to the controllers, the service layer, and the repository.</span></span> <span data-ttu-id="826c0-150">一旦您开始修改代码，则可能会破坏正常运行过的功能。</span><span class="sxs-lookup"><span data-stu-id="826c0-150">As soon as you start modifying code, you risk breaking functionality that worked before.</span></span>

<span data-ttu-id="826c0-151">正如我们在上一次迭代，做重构到不同的层，我们的应用程序是一件好事。</span><span class="sxs-lookup"><span data-stu-id="826c0-151">Refactoring our application into separate layers, as we did in the previous iteration, was a good thing.</span></span> <span data-ttu-id="826c0-152">它是一件好事，因为它使我们能够对整个层进行更改，无需接触应用程序的其余部分。</span><span class="sxs-lookup"><span data-stu-id="826c0-152">It was a good thing because it enables us to make changes to entire layers without touching the rest of the application.</span></span> <span data-ttu-id="826c0-153">但是，如果你想要使在层内的代码更易于维护和修改，则需要创建单元测试的代码。</span><span class="sxs-lookup"><span data-stu-id="826c0-153">However, if you want to make the code within a layer easier to maintain and modify, you need to create unit tests for the code.</span></span>

<span data-ttu-id="826c0-154">你使用单元测试来测试单个代码单元。</span><span class="sxs-lookup"><span data-stu-id="826c0-154">You use a unit test to test an individual unit of code.</span></span> <span data-ttu-id="826c0-155">这些单位代码是小于整个应用程序层。</span><span class="sxs-lookup"><span data-stu-id="826c0-155">These units of code are smaller than entire application layers.</span></span> <span data-ttu-id="826c0-156">通常情况下，您可以使用单元测试以验证你的代码中的特定方法的行为是否在预期的方式。</span><span class="sxs-lookup"><span data-stu-id="826c0-156">Typically, you use a unit test to verify whether a particular method in your code behaves in the way that you expect.</span></span> <span data-ttu-id="826c0-157">例如，将创建由 ContactManagerService 类公开的 CreateContact() 方法的单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-157">For example, you would create a unit test for the CreateContact() method exposed by the ContactManagerService class.</span></span>

<span data-ttu-id="826c0-158">只是应用程序工作的单元测试，如网络安全。</span><span class="sxs-lookup"><span data-stu-id="826c0-158">The unit tests for an application work just like a safety net.</span></span> <span data-ttu-id="826c0-159">每当修改代码的应用程序，可以运行单元测试，以检查是否修改中断现有功能的一组。</span><span class="sxs-lookup"><span data-stu-id="826c0-159">Whenever you modify code in an application, you can run a set of unit tests to check whether the modification breaks existing functionality.</span></span> <span data-ttu-id="826c0-160">单元测试使您的代码安全地修改。</span><span class="sxs-lookup"><span data-stu-id="826c0-160">Unit tests make your code safe to modify.</span></span> <span data-ttu-id="826c0-161">单元测试的所有代码中进行应用程序更具弹性，若要更改。</span><span class="sxs-lookup"><span data-stu-id="826c0-161">Unit tests make all of the code in your application more resilient to change.</span></span>

<span data-ttu-id="826c0-162">在此迭代中，我们将单元测试添加到我们的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-162">In this iteration, we add unit tests to our Contact Manager application.</span></span> <span data-ttu-id="826c0-163">这样一来，在下一个迭代中，我们可以添加联系人组对我们的应用程序而无需担心破坏现有功能。</span><span class="sxs-lookup"><span data-stu-id="826c0-163">That way, in the next iteration, we can add Contact Groups to our application without worrying about breaking existing functionality.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="826c0-164">多种测试框架，包括 NUnit 和 xUnit.net，MbUnit 的单元。</span><span class="sxs-lookup"><span data-stu-id="826c0-164">There are a variety of unit testing frameworks including NUnit, xUnit.net, and MbUnit.</span></span> <span data-ttu-id="826c0-165">在本教程中，我们使用的单元测试框架与 Visual Studio 附带。</span><span class="sxs-lookup"><span data-stu-id="826c0-165">In this tutorial, we use the unit testing framework included with Visual Studio.</span></span> <span data-ttu-id="826c0-166">但是，您可以轻松地使用其中一种替代框架。</span><span class="sxs-lookup"><span data-stu-id="826c0-166">However, you could just as easily use one of these alternative frameworks.</span></span>


## <a name="what-gets-tested"></a><span data-ttu-id="826c0-167">获取测试内容</span><span class="sxs-lookup"><span data-stu-id="826c0-167">What Gets Tested</span></span>

<span data-ttu-id="826c0-168">在理想情况下，所有代码将包含一些单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-168">In the perfect world, all of your code would be covered by unit tests.</span></span> <span data-ttu-id="826c0-169">在理想情况下，您必须完美的网络安全。</span><span class="sxs-lookup"><span data-stu-id="826c0-169">In the perfect world, you would have the perfect safety net.</span></span> <span data-ttu-id="826c0-170">您可以修改应用程序中代码的任何行，并就可马上知道，通过执行单元测试，是否更改中断了现有功能。</span><span class="sxs-lookup"><span data-stu-id="826c0-170">You would be able to modify any line of code in your application and know instantly, by executing your unit tests, whether the change broke existing functionality.</span></span>

<span data-ttu-id="826c0-171">但是，我们并不完美的世界中的实时 t。</span><span class="sxs-lookup"><span data-stu-id="826c0-171">However, we don t live in a perfect world.</span></span> <span data-ttu-id="826c0-172">在实践中，编写单元测试时，您专注于编写您的业务逻辑 （例如，验证逻辑） 的测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-172">In practice, when writing unit tests, you concentrate on writing tests for your business logic (for example, validation logic).</span></span> <span data-ttu-id="826c0-173">具体而言，你*不这样做*编写单元测试为你的数据访问逻辑或视图逻辑。</span><span class="sxs-lookup"><span data-stu-id="826c0-173">In particular, you *do not* write unit tests for your data access logic or your view logic.</span></span>

<span data-ttu-id="826c0-174">若要很有用，单元测试必须执行非常快速地。</span><span class="sxs-lookup"><span data-stu-id="826c0-174">To be useful, unit tests must execute very quickly.</span></span> <span data-ttu-id="826c0-175">您轻松地可能会累积 （成百上千台） 的应用程序的单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-175">You easily can accumulate hundreds (or even thousands) of unit tests for an application.</span></span> <span data-ttu-id="826c0-176">如果单元测试可能需要很长时间才能运行您要防止执行它们。</span><span class="sxs-lookup"><span data-stu-id="826c0-176">If the unit tests take a long time to run then you'll avoid executing them.</span></span> <span data-ttu-id="826c0-177">换而言之，长时间运行的单元测试是无用的日常编码用途。</span><span class="sxs-lookup"><span data-stu-id="826c0-177">In other words, long running unit tests are useless for day to day coding purposes.</span></span>

<span data-ttu-id="826c0-178">出于此原因，您通常做不编写与数据库交互的代码的单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-178">For this reason, you typically do not write unit tests for code that interacts with a database.</span></span> <span data-ttu-id="826c0-179">针对实时数据库运行数百个单元测试会太慢。</span><span class="sxs-lookup"><span data-stu-id="826c0-179">Running hundreds of unit tests against a live database would be too slow.</span></span> <span data-ttu-id="826c0-180">不过，您可以模拟你的数据库，编写与 （我们讨论模拟以下数据库） 的模拟数据库交互的代码。</span><span class="sxs-lookup"><span data-stu-id="826c0-180">Instead, you mock your database and write code that interacts with the mock database (we discuss mocking a database below).</span></span>

<span data-ttu-id="826c0-181">出于类似原因，您通常不写入视图的单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-181">For a similar reason, you typically do not write unit tests for views.</span></span> <span data-ttu-id="826c0-182">若要测试一个视图，必须启动 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="826c0-182">In order to test a view, you must spin up a web server.</span></span> <span data-ttu-id="826c0-183">由于启动 web 服务器是一个相对较慢的过程，不建议创建单元测试您的视图。</span><span class="sxs-lookup"><span data-stu-id="826c0-183">Because spinning up a web server is a relatively slow process, creating unit tests for your views is not recommended.</span></span>

<span data-ttu-id="826c0-184">如果您的视图包含复杂的逻辑则应考虑将逻辑移到帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="826c0-184">If your view contains complicated logic then you should consider moving the logic into Helper methods.</span></span> <span data-ttu-id="826c0-185">您可以编写单元测试的执行而无需启动 web 服务器的帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="826c0-185">You can write unit tests for Helper methods that execute without spinning up a web server.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="826c0-186">虽然编写测试的数据访问逻辑或视图逻辑不是一个不错的主意，编写单元测试时，这些测试可能会非常有价值，构建功能或集成测试时。</span><span class="sxs-lookup"><span data-stu-id="826c0-186">While writing tests for data access logic or view logic is not a good idea when writing unit tests, these tests can be very valuable when building functional or integration tests.</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="826c0-187">ASP.NET MVC 是 Web 窗体视图引擎。</span><span class="sxs-lookup"><span data-stu-id="826c0-187">ASP.NET MVC is the Web Forms View Engine.</span></span> <span data-ttu-id="826c0-188">Web 窗体视图引擎依赖于 web 服务器时，可能不是其他视图引擎。</span><span class="sxs-lookup"><span data-stu-id="826c0-188">While the Web Forms View Engine is dependent on a web server, other view engines might not be.</span></span>


## <a name="using-a-mock-object-framework"></a><span data-ttu-id="826c0-189">使用模拟对象框架</span><span class="sxs-lookup"><span data-stu-id="826c0-189">Using a Mock Object Framework</span></span>

<span data-ttu-id="826c0-190">在生成单元测试时，几乎总是需要利用的模拟对象框架。</span><span class="sxs-lookup"><span data-stu-id="826c0-190">When building unit tests, you almost always need to take advantage of a Mock Object framework.</span></span> <span data-ttu-id="826c0-191">模拟对象框架，可在应用程序中创建模拟和存根 （stub） 的类。</span><span class="sxs-lookup"><span data-stu-id="826c0-191">A Mock Object framework enables you to create mocks and stubs for the classes in your application.</span></span>

<span data-ttu-id="826c0-192">例如，可以使用模拟对象框架来生成你的存储库类的模型版本。</span><span class="sxs-lookup"><span data-stu-id="826c0-192">For example, you can use a Mock Object framework to generate a mock version of your repository class.</span></span> <span data-ttu-id="826c0-193">这样一来，您可以使用模拟存储库类而不是实际的存储库类在单元测试中。</span><span class="sxs-lookup"><span data-stu-id="826c0-193">That way, you can use the mock repository class instead of the real repository class in your unit tests.</span></span> <span data-ttu-id="826c0-194">使用模拟的存储库，可避免执行数据库的代码执行单元测试时。</span><span class="sxs-lookup"><span data-stu-id="826c0-194">Using the mock repository enables you to avoid executing database code when executing a unit test.</span></span>

<span data-ttu-id="826c0-195">Visual Studio 不会包含模拟对象框架。</span><span class="sxs-lookup"><span data-stu-id="826c0-195">Visual Studio does not include a Mock Object framework.</span></span> <span data-ttu-id="826c0-196">但是，有可用于.NET framework 的多个商业和开源模拟对象框架：</span><span class="sxs-lookup"><span data-stu-id="826c0-196">However, there are several commercial and open source Mock Object frameworks available for the .NET framework:</span></span>

1. <span data-ttu-id="826c0-197">Moq-此框架是开放源 BSD 许可下提供。</span><span class="sxs-lookup"><span data-stu-id="826c0-197">Moq - This framework is available under the open source BSD license.</span></span> <span data-ttu-id="826c0-198">您可以下载从 Moq [ https://code.google.com/p/moq/ ](https://code.google.com/p/moq/)。</span><span class="sxs-lookup"><span data-stu-id="826c0-198">You can download Moq from [https://code.google.com/p/moq/](https://code.google.com/p/moq/).</span></span>
2. <span data-ttu-id="826c0-199">Rhino Mocks-此框架是开放源 BSD 许可下提供。</span><span class="sxs-lookup"><span data-stu-id="826c0-199">Rhino Mocks - This framework is available under the open source BSD license.</span></span> <span data-ttu-id="826c0-200">您可以下载从 Rhino Mocks [ http://ayende.com/projects/rhino-mocks.aspx ](http://ayende.com/projects/rhino-mocks.aspx)。</span><span class="sxs-lookup"><span data-stu-id="826c0-200">You can download Rhino Mocks from [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx).</span></span>
3. <span data-ttu-id="826c0-201">Typemock Isolator-这是一个商业的框架。</span><span class="sxs-lookup"><span data-stu-id="826c0-201">Typemock Isolator - This is a commercial framework.</span></span> <span data-ttu-id="826c0-202">您可以下载从试用版[ http://www.typemock.com/ ](http://www.typemock.com/)。</span><span class="sxs-lookup"><span data-stu-id="826c0-202">You can download a trial version from [http://www.typemock.com/](http://www.typemock.com/).</span></span>

<span data-ttu-id="826c0-203">在本教程中，我决定使用 Moq。</span><span class="sxs-lookup"><span data-stu-id="826c0-203">In this tutorial, I decided to use Moq.</span></span> <span data-ttu-id="826c0-204">但是，您可以轻松地使用 Rhino Mocks 或 Typemock Isolator 创建 Mock 对象为联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="826c0-204">However, you could just as easily use Rhino Mocks or Typemock Isolator to create the Mock objects for the Contact Manager application.</span></span>

<span data-ttu-id="826c0-205">可以使用 Moq 之前，需要完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="826c0-205">Before you can use Moq, you need to complete the following steps:</span></span>

1. <span data-ttu-id="826c0-206">.</span><span class="sxs-lookup"><span data-stu-id="826c0-206">.</span></span>
2. <span data-ttu-id="826c0-207">解压缩下载之前，请确保右键单击该文件，并单击标记的按钮**解除阻止**（参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="826c0-207">Before you unzip the download, make sure that you right-click the file and click the button labeled **Unblock** (see Figure 1).</span></span>
3. <span data-ttu-id="826c0-208">解压缩下载。</span><span class="sxs-lookup"><span data-stu-id="826c0-208">Unzip the download.</span></span>
4. <span data-ttu-id="826c0-209">通过选择菜单选项将 Moq 程序集的引用添加到你的测试项目**项目中，添加引用**以打开**添加引用**对话框。</span><span class="sxs-lookup"><span data-stu-id="826c0-209">Add a reference to the Moq assembly to your Test project by selecting the menu option **Project, Add Reference** to open the **Add Reference** dialog.</span></span> <span data-ttu-id="826c0-210">在浏览选项卡，浏览到你在其中解压缩 Moq 文件夹并选择 Moq.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="826c0-210">Under the Browse tab, browse to the folder where you unzipped Moq and select the Moq.dll assembly.</span></span> <span data-ttu-id="826c0-211">单击**确定**按钮 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="826c0-211">Click the **OK** button (see Figure 2).</span></span>


<span data-ttu-id="826c0-212">[![取消阻塞 Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="826c0-212">[![Unblocking Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)</span></span>

<span data-ttu-id="826c0-213">**图 01**： 取消阻塞 Moq ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="826c0-213">**Figure 01**: Unblocking Moq([Click to view full-size image](iteration-5-create-unit-tests-vb/_static/image2.png))</span></span>


<span data-ttu-id="826c0-214">[![添加 Moq 后引用](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="826c0-214">[![References after adding Moq](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)</span></span>

<span data-ttu-id="826c0-215">**图 02**： 添加 Moq 后的引用 ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="826c0-215">**Figure 02**: References after adding Moq([Click to view full-size image](iteration-5-create-unit-tests-vb/_static/image4.png))</span></span>


## <a name="creating-unit-tests-for-the-service-layer"></a><span data-ttu-id="826c0-216">为服务层创建单元测试</span><span class="sxs-lookup"><span data-stu-id="826c0-216">Creating Unit Tests for the Service Layer</span></span>

<span data-ttu-id="826c0-217">让我们来首先创建一组我们联系人管理器应用程序 s 的服务层的单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-217">Let s start by creating a set of unit tests for our Contact Manager application s service layer.</span></span> <span data-ttu-id="826c0-218">我们将使用这些测试来验证我们的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="826c0-218">We'll use these tests to verify our validation logic.</span></span>

<span data-ttu-id="826c0-219">创建 ContactManager.Tests 项目中名为 Models 的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="826c0-219">Create a new folder named Models in the ContactManager.Tests project.</span></span> <span data-ttu-id="826c0-220">接下来，右键单击模型文件夹并选择**添加、 新测试**。</span><span class="sxs-lookup"><span data-stu-id="826c0-220">Next, right-click the Models folder and select **Add, New Test**.</span></span> <span data-ttu-id="826c0-221">**添加新测试**此时将显示图 3 所示的对话框。</span><span class="sxs-lookup"><span data-stu-id="826c0-221">The **Add New Test** dialog shown in Figure 3 appears.</span></span> <span data-ttu-id="826c0-222">选择**单元测试**模板并命名新测试 ContactManagerServiceTest.vb。</span><span class="sxs-lookup"><span data-stu-id="826c0-222">Select the **Unit Test** template and name your new test ContactManagerServiceTest.vb.</span></span> <span data-ttu-id="826c0-223">单击**确定**按钮将新测试添加到测试项目。</span><span class="sxs-lookup"><span data-stu-id="826c0-223">Click the **OK** button to add your new test to your Test Project.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="826c0-224">一般情况下，所需测试项目以匹配你的 ASP.NET MVC 项目的文件夹结构的文件夹的结构。</span><span class="sxs-lookup"><span data-stu-id="826c0-224">In general, you want the folder structure of your Test Project to match the folder structure of your ASP.NET MVC project.</span></span> <span data-ttu-id="826c0-225">例如，您将测试控制器放置在控制器文件夹中，在模型文件夹中，模型测试等。</span><span class="sxs-lookup"><span data-stu-id="826c0-225">For example, you place controller tests in a Controllers folder, model tests in a Models folder, and so on.</span></span>


<span data-ttu-id="826c0-226">[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="826c0-226">[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)</span></span>

<span data-ttu-id="826c0-227">**图 03**: Models\ContactManagerServiceTest.cs ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="826c0-227">**Figure 03**: Models\ContactManagerServiceTest.cs([Click to view full-size image](iteration-5-create-unit-tests-vb/_static/image6.png))</span></span>


<span data-ttu-id="826c0-228">最初，我们想要测试由 ContactManagerService 类公开的 CreateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="826c0-228">Initially, we want to test the CreateContact() method exposed by the ContactManagerService class.</span></span> <span data-ttu-id="826c0-229">我们将创建以下五个测试：</span><span class="sxs-lookup"><span data-stu-id="826c0-229">We'll create the following five tests:</span></span>

- <span data-ttu-id="826c0-230">CreateContact()-向方法传递了有效的联系人时，测试该 CreateContact() 返回值 true。</span><span class="sxs-lookup"><span data-stu-id="826c0-230">CreateContact() - Tests that CreateContact() returns the value true when a valid Contact is passed to the method.</span></span>
- <span data-ttu-id="826c0-231">CreateContactRequiredFirstName()-CreateContact() 方法被通过的测试，将一条错误消息添加到模型状态时缺少的名字的联系人。</span><span class="sxs-lookup"><span data-stu-id="826c0-231">CreateContactRequiredFirstName() - Tests that an error message is added to model state when a Contact with a missing first name is passed to the CreateContact() method.</span></span>
- <span data-ttu-id="826c0-232">CreateContactRequredLastName()-CreateContact() 方法被通过的测试，将一条错误消息添加到模型状态时缺少姓氏的联系人。</span><span class="sxs-lookup"><span data-stu-id="826c0-232">CreateContactRequredLastName() - Tests that an error message is added to model state when a Contact with a missing last name is passed to the CreateContact() method.</span></span>
- <span data-ttu-id="826c0-233">CreateContactInvalidPhone()-CreateContact() 方法被通过的测试，将一条错误消息添加到模型状态时的联系人电话号码无效。</span><span class="sxs-lookup"><span data-stu-id="826c0-233">CreateContactInvalidPhone() - Tests that an error message is added to model state when a Contact with an invalid phone number is passed to the CreateContact() method.</span></span>
- <span data-ttu-id="826c0-234">CreateContactInvalidEmail()-测试，将一条错误消息添加到模型状态无效的电子邮件地址的联系人时传递给 CreateContact() 方法...</span><span class="sxs-lookup"><span data-stu-id="826c0-234">CreateContactInvalidEmail() - Tests that an error message is added to model state when a Contact with an invalid email address is passed to the CreateContact() method..</span></span>

<span data-ttu-id="826c0-235">第一个测试验证了有效的联系人不会生成验证错误。</span><span class="sxs-lookup"><span data-stu-id="826c0-235">The first test verifies that a valid Contact does not generate a validation error.</span></span> <span data-ttu-id="826c0-236">剩余测试检查每个验证规则。</span><span class="sxs-lookup"><span data-stu-id="826c0-236">The remaining tests check each of the validation rules.</span></span>

<span data-ttu-id="826c0-237">对于这些测试的代码包含在列表 1 中。</span><span class="sxs-lookup"><span data-stu-id="826c0-237">The code for these tests is contained in Listing 1.</span></span>

<span data-ttu-id="826c0-238">**Listing 1 - Models\ContactManagerServiceTest.vb**</span><span class="sxs-lookup"><span data-stu-id="826c0-238">**Listing 1 - Models\ContactManagerServiceTest.vb**</span></span>

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]


<span data-ttu-id="826c0-239">由于我们在列表 1 中使用 Contact 类，我们需要将对 Microsoft 实体框架的引用添加到我们的测试项目。</span><span class="sxs-lookup"><span data-stu-id="826c0-239">Because we use the Contact class in Listing 1, we need to add a reference to the Microsoft Entity Framework to our Test project.</span></span> <span data-ttu-id="826c0-240">添加对 system.data.entity 的引用程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="826c0-240">Add a reference to the System.Data.Entity assembly.</span></span>


<span data-ttu-id="826c0-241">代码清单 1 包含一个名为使用 [TestInitialize] 特性修饰的 initialize （） 方法。</span><span class="sxs-lookup"><span data-stu-id="826c0-241">Listing 1 contains a method named Initialize() that is decorated with the [TestInitialize] attribute.</span></span> <span data-ttu-id="826c0-242">每个单元测试运行之前自动调用此方法 （它每个单元测试前调用 5 次）。</span><span class="sxs-lookup"><span data-stu-id="826c0-242">This method is called automatically before each of the unit tests is run (it is called 5 times right before each of the unit tests).</span></span> <span data-ttu-id="826c0-243">使用以下代码行，initialize （） 方法创建 mock 存储库：</span><span class="sxs-lookup"><span data-stu-id="826c0-243">The Initialize() method creates a mock repository with the following line of code:</span></span>

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

<span data-ttu-id="826c0-244">这行代码使用 Moq 框架来生成从 IContactManagerRepository 接口的 mock 存储库。</span><span class="sxs-lookup"><span data-stu-id="826c0-244">This line of code uses the Moq framework to generate a mock repository from the IContactManagerRepository interface.</span></span> <span data-ttu-id="826c0-245">Mock 存储库而不是实际 EntityContactManagerRepository 用于避免在每个单元测试运行时访问数据库。</span><span class="sxs-lookup"><span data-stu-id="826c0-245">The mock repository is used instead of the actual EntityContactManagerRepository to avoid accessing the database when each unit test is run.</span></span> <span data-ttu-id="826c0-246">Mock 存储库实现 IContactManagerRepository 接口的方法，但方法 don t 实际执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="826c0-246">The mock repository implements the methods of the IContactManagerRepository interface, but the methods don t actually do anything.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="826c0-247">使用 Moq 框架时，会区分\_mockRepository 和\_mockRepository.Object。</span><span class="sxs-lookup"><span data-stu-id="826c0-247">When using the Moq framework, there is a distinction between \_mockRepository and \_mockRepository.Object.</span></span> <span data-ttu-id="826c0-248">前者是指包含用于指定模拟存储库的行为方式的方法的模拟 (的 IContactManagerRepository) 类。</span><span class="sxs-lookup"><span data-stu-id="826c0-248">The former refers to the Mock(Of IContactManagerRepository) class that contains methods for specifying how the mock repository will behave.</span></span> <span data-ttu-id="826c0-249">后者是指实际的 mock 存储库，实现 IContactManagerRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="826c0-249">The latter refers to the actual mock repository that implements the IContactManagerRepository interface.</span></span>


<span data-ttu-id="826c0-250">创建 ContactManagerService 类的实例时，将在 initialize （） 方法中使用模拟的存储库。</span><span class="sxs-lookup"><span data-stu-id="826c0-250">The mock repository is used in the Initialize() method when creating an instance of the ContactManagerService class.</span></span> <span data-ttu-id="826c0-251">所有的各个单元测试使用 ContactManagerService 类的此实例。</span><span class="sxs-lookup"><span data-stu-id="826c0-251">All of the individual unit tests use this instance of the ContactManagerService class.</span></span>

<span data-ttu-id="826c0-252">代码清单 1 包含五个方法对应于每个单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-252">Listing 1 contains five methods that correspond to each of the unit tests.</span></span> <span data-ttu-id="826c0-253">每种方法是使用 [TestMethod] 特性修饰。</span><span class="sxs-lookup"><span data-stu-id="826c0-253">Each of these methods is decorated with the [TestMethod] attribute.</span></span> <span data-ttu-id="826c0-254">当您运行单元测试时，被调用具有此属性的任何方法。</span><span class="sxs-lookup"><span data-stu-id="826c0-254">When you run the unit tests, any method that has this attribute is called.</span></span> <span data-ttu-id="826c0-255">换而言之，任何使用 [TestMethod] 特性修饰的方法是单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-255">In other words, any method that is decorated with the [TestMethod] attribute is a unit test.</span></span>

<span data-ttu-id="826c0-256">第一个单元测试，名为 CreateContact()，验证，有效 Contact 类的实例传递给方法时，调用 CreateContact() 返回值 true。</span><span class="sxs-lookup"><span data-stu-id="826c0-256">The first unit test, named CreateContact(), verifies that calling CreateContact() returns the value true when a valid instance of the Contact class is passed to the method.</span></span> <span data-ttu-id="826c0-257">测试创建 Contact 类的实例，调用 CreateContact() 方法，并验证 CreateContact() 返回值 true。</span><span class="sxs-lookup"><span data-stu-id="826c0-257">The test creates an instance of the Contact class, calls the CreateContact() method, and verifies that CreateContact() returns the value true.</span></span>

<span data-ttu-id="826c0-258">剩余测试验证，当使用无效的联系人调用 CreateContact() 方法然后方法返回 false，预期的验证错误消息添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="826c0-258">The remaining tests verify that when the CreateContact() method is called with an invalid Contact then the method returns false and the expected validation error message is added to model state.</span></span> <span data-ttu-id="826c0-259">例如，CreateContactRequiredFirstName() 测试与空字符串作为其 FirstName 属性创建联系人类的实例。</span><span class="sxs-lookup"><span data-stu-id="826c0-259">For example, the CreateContactRequiredFirstName() test creates an instance of the Contact class with an empty string for its FirstName property.</span></span> <span data-ttu-id="826c0-260">接下来，使用无效的联系人调用 CreateContact() 方法。</span><span class="sxs-lookup"><span data-stu-id="826c0-260">Next, the CreateContact() method is called with the invalid Contact.</span></span> <span data-ttu-id="826c0-261">最后，此测试将验证 CreateContact() 返回 false，并且模型状态包含预期的验证错误消息"名字是必填。"</span><span class="sxs-lookup"><span data-stu-id="826c0-261">Finally, the test verifies that CreateContact() returns false and that model state contains the expected validation error message "First name is required."</span></span>

<span data-ttu-id="826c0-262">可以通过选择菜单选项在列表 1 中运行单元测试**测试，运行，解决方案 （CTRL + R、 A） 中的所有测试**。</span><span class="sxs-lookup"><span data-stu-id="826c0-262">You can run the unit tests in Listing 1 by selecting the menu option **Test, Run, All Tests in Solution (CTRL+R, A)**.</span></span> <span data-ttu-id="826c0-263">在测试结果窗口中显示测试结果 （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="826c0-263">The results of the tests are displayed in the Test Results window (see Figure 4).</span></span>


<span data-ttu-id="826c0-264">[![测试结果](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="826c0-264">[![Test Results](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)</span></span>

<span data-ttu-id="826c0-265">**图 04**： 测试结果 ([单击以查看实际尺寸的图像](iteration-5-create-unit-tests-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="826c0-265">**Figure 04**: Test Results ([Click to view full-size image](iteration-5-create-unit-tests-vb/_static/image8.png))</span></span>


## <a name="creating-unit-tests-for-controllers"></a><span data-ttu-id="826c0-266">为控制器创建单元测试</span><span class="sxs-lookup"><span data-stu-id="826c0-266">Creating Unit Tests for Controllers</span></span>

<span data-ttu-id="826c0-267">ASP.NET MVC 应用程序控制流的用户交互。</span><span class="sxs-lookup"><span data-stu-id="826c0-267">ASP.NET MVC application control the flow of user interaction.</span></span> <span data-ttu-id="826c0-268">当测试控制器时，你想要测试是否将控制器返回正确的操作结果和查看数据。</span><span class="sxs-lookup"><span data-stu-id="826c0-268">When testing a controller, you want to test whether the controller returns the right action result and view data.</span></span> <span data-ttu-id="826c0-269">此外可能想要测试是否与预期的方式中的模型类交互，一个控制器。</span><span class="sxs-lookup"><span data-stu-id="826c0-269">You also might want to test whether a controller interacts with model classes in the manner expected.</span></span>

<span data-ttu-id="826c0-270">例如，代码清单 2 包含联系人控制器 create （） 方法的两个单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-270">For example, Listing 2 contains two unit tests for the Contact controller Create() method.</span></span> <span data-ttu-id="826c0-271">第一个单元测试验证了有效的联系人传递给 create （） 方法，则 create （） 方法将重定向到的索引操作时。</span><span class="sxs-lookup"><span data-stu-id="826c0-271">The first unit test verifies that when a valid Contact is passed to the Create() method then the Create() method redirects to the Index action.</span></span> <span data-ttu-id="826c0-272">换而言之，当传递了有效的联系人，create （） 方法应返回表示索引操作 RedirectToRouteResult。</span><span class="sxs-lookup"><span data-stu-id="826c0-272">In other words, when passed a valid Contact, the Create() method should return a RedirectToRouteResult that represents the Index action.</span></span>

<span data-ttu-id="826c0-273">我们不想测试 ContactManager 服务层，我们将测试控制器层时。</span><span class="sxs-lookup"><span data-stu-id="826c0-273">We don t want to test the ContactManager service layer when we are testing the controller layer.</span></span> <span data-ttu-id="826c0-274">因此，我们模拟服务层提供的 Initialize 方法中的以下代码：</span><span class="sxs-lookup"><span data-stu-id="826c0-274">Therefore, we mock the service layer with the following code in the Initialize method:</span></span>

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

<span data-ttu-id="826c0-275">在 CreateValidContact() 单元测试中，我们模拟调用服务层具有以下代码行 CreateContact() 方法的行为：</span><span class="sxs-lookup"><span data-stu-id="826c0-275">In the CreateValidContact() unit test, we mock the behavior of calling the service layer CreateContact() method with the following line of code:</span></span>

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

<span data-ttu-id="826c0-276">这行代码会导致模拟的 ContactManager 服务，以调用其 CreateContact() 方法返回的值为 true。</span><span class="sxs-lookup"><span data-stu-id="826c0-276">This line of code causes the mock ContactManager service to return the value true when its CreateContact() method is called.</span></span> <span data-ttu-id="826c0-277">由模拟服务层，我们可以测试控制器的行为而无需执行的服务层中的任何代码。</span><span class="sxs-lookup"><span data-stu-id="826c0-277">By mocking the service layer, we can test the behavior of our controller without needing to execute any code in the service layer.</span></span>

<span data-ttu-id="826c0-278">第二个单元测试验证无效联系人传递给方法时，create （） 操作，返回创建视图。</span><span class="sxs-lookup"><span data-stu-id="826c0-278">The second unit test verifies that the Create() action returns the Create view when an invalid contact is passed to the method.</span></span> <span data-ttu-id="826c0-279">我们会导致服务层 CreateContact() 方法返回值 false，使用以下代码行：</span><span class="sxs-lookup"><span data-stu-id="826c0-279">We cause the service layer CreateContact() method to return the value false with the following line of code:</span></span>

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

<span data-ttu-id="826c0-280">如果 create （） 方法的行为我们预期它应在服务层，则返回值 false 时返回创建视图。</span><span class="sxs-lookup"><span data-stu-id="826c0-280">If the Create() method behaves as we expect then it should return the Create view when the service layer returns the value false.</span></span> <span data-ttu-id="826c0-281">这样一来，控制器可以显示验证错误消息，在创建视图和用户有机会更正该无效联系人属性。</span><span class="sxs-lookup"><span data-stu-id="826c0-281">That way, the controller can display the validation error messages in the Create view and the user has a chance to correct that invalid Contact properties.</span></span>


<span data-ttu-id="826c0-282">如果您计划生成你的控制器的单元测试然后您需要的控制器操作返回显式视图名称。</span><span class="sxs-lookup"><span data-stu-id="826c0-282">If you plan to build unit tests for your controllers then you need to return explicit view names from your controller actions.</span></span> <span data-ttu-id="826c0-283">例如，不返回此类的视图：</span><span class="sxs-lookup"><span data-stu-id="826c0-283">For example, do not return a view like this:</span></span>

<span data-ttu-id="826c0-284">返回 View()</span><span class="sxs-lookup"><span data-stu-id="826c0-284">Return View()</span></span>

<span data-ttu-id="826c0-285">改为返回的视图如下：</span><span class="sxs-lookup"><span data-stu-id="826c0-285">Instead, return the view like this:</span></span>

<span data-ttu-id="826c0-286">返回 View("Create")</span><span class="sxs-lookup"><span data-stu-id="826c0-286">Return View("Create")</span></span>

<span data-ttu-id="826c0-287">如果不能显式返回视图时 ViewResult.ViewName 属性将返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="826c0-287">If you are not explicit when returning a view then the ViewResult.ViewName property returns an empty string.</span></span>


<span data-ttu-id="826c0-288">**Listing 2 - Controllers\ContactControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="826c0-288">**Listing 2 - Controllers\ContactControllerTest.vb**</span></span>

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a><span data-ttu-id="826c0-289">总结</span><span class="sxs-lookup"><span data-stu-id="826c0-289">Summary</span></span>

<span data-ttu-id="826c0-290">在此迭代中，我们为我们的联系人管理器应用程序创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-290">In this iteration, we created unit tests for our Contact Manager application.</span></span> <span data-ttu-id="826c0-291">若要验证我们的应用程序仍行为我们预期的方式在任何时候，我们可以运行这些单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-291">We can run these unit tests at any time to verify that our application still behaves in the manner that we expect.</span></span> <span data-ttu-id="826c0-292">单元测试作为使应用程序，使我们能够安全地修改我们的应用程序在将来的安全网。</span><span class="sxs-lookup"><span data-stu-id="826c0-292">The unit tests act as a safety net for our application enabling us to safely modify our application in the future.</span></span>

<span data-ttu-id="826c0-293">我们创建了两个集的单元测试。</span><span class="sxs-lookup"><span data-stu-id="826c0-293">We created two sets of unit tests.</span></span> <span data-ttu-id="826c0-294">首先，我们通过创建我们的服务层的单元测试来测试我们的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="826c0-294">First, we tested our validation logic by creating unit tests for our service layer.</span></span> <span data-ttu-id="826c0-295">接下来，我们通过创建我们的控制器层的单元测试来测试我们的流控制逻辑。</span><span class="sxs-lookup"><span data-stu-id="826c0-295">Next, we tested our flow control logic by creating unit tests for our controller layer.</span></span> <span data-ttu-id="826c0-296">当测试我们的服务层，我们独立的我们的测试为我们的服务层从我们的存储库层通过模拟我们存储库层。</span><span class="sxs-lookup"><span data-stu-id="826c0-296">When testing our service layer, we isolated our tests for our service layer from our repository layer by mocking our repository layer.</span></span> <span data-ttu-id="826c0-297">当测试控制器层，我们独立的我们的测试我们控制器层由模拟服务层。</span><span class="sxs-lookup"><span data-stu-id="826c0-297">When testing the controller layer, we isolated our tests for our controller layer by mocking the service layer.</span></span>

<span data-ttu-id="826c0-298">在下一个迭代中，我们将修改联系人管理器应用程序，以便它支持联系人组。</span><span class="sxs-lookup"><span data-stu-id="826c0-298">In the next iteration, we modify the Contact Manager application so that it supports Contact Groups.</span></span> <span data-ttu-id="826c0-299">我们将此新功能添加到我们的应用程序使用名为测试驱动开发的软件设计过程。</span><span class="sxs-lookup"><span data-stu-id="826c0-299">We'll add this new functionality to our application using a software design process called test-driven development.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="826c0-300">[上一页](iteration-4-make-the-application-loosely-coupled-vb.md)
> [下一页](iteration-6-use-test-driven-development-vb.md)</span><span class="sxs-lookup"><span data-stu-id="826c0-300">[Previous](iteration-4-make-the-application-loosely-coupled-vb.md)
[Next](iteration-6-use-test-driven-development-vb.md)</span></span>
