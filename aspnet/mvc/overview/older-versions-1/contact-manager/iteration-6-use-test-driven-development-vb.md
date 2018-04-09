---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
title: 迭代 6 – 使用测试驱动开发 (VB) |Microsoft 文档
author: microsoft
description: 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。 此迭代中...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2009
ms.topic: article
ms.assetid: e1fd226f-3f8e-4575-a179-5c75b240333d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-vb
msc.type: authoredcontent
ms.openlocfilehash: 71b3425c5ca8cbfc1b89493c7afb26681f8bdc9d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="iteration-6--use-test-driven-development-vb"></a><span data-ttu-id="5741e-104">迭代 6 – 使用测试驱动开发 (VB)</span><span class="sxs-lookup"><span data-stu-id="5741e-104">Iteration #6 – Use test-driven development (VB)</span></span>
====================
<span data-ttu-id="5741e-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5741e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="5741e-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="5741e-106">Download Code</span></span>](iteration-6-use-test-driven-development-vb/_static/contactmanager_6_vb1.zip)

> <span data-ttu-id="5741e-107">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="5741e-108">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-108">In this iteration, we add contact groups.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="5741e-109">生成联系人管理 ASP.NET MVC 应用程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="5741e-109">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="5741e-110">在这一系列的教程，我们生成整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="5741e-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="5741e-111">联系人管理器应用程序，可存储的名称，电话号码和电子邮件地址的联系人信息有关的人员列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="5741e-112">我们在多次迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="5741e-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="5741e-113">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="5741e-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="5741e-114">此多个迭代方法旨在使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="5741e-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="5741e-115">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="5741e-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="5741e-116">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="5741e-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="5741e-117">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="5741e-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="5741e-118">迭代 #2-使应用程序，看上去很好。</span><span class="sxs-lookup"><span data-stu-id="5741e-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="5741e-119">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表改进应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="5741e-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="5741e-120">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="5741e-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="5741e-121">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="5741e-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="5741e-122">我们可以防止人员提交窗体，但不完成需要的表单域。</span><span class="sxs-lookup"><span data-stu-id="5741e-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="5741e-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="5741e-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="5741e-124">迭代 #4-请松散耦合的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5741e-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="5741e-125">在此第三个迭代中，我们利用多个软件设计模式以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="5741e-125">In this third iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="5741e-126">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="5741e-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="5741e-127">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="5741e-128">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="5741e-129">我们模拟我们数据模型类，并生成单元测试控制器和验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="5741e-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="5741e-130">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="5741e-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="5741e-131">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试和针对单元测试编写代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="5741e-132">在此迭代中，我们添加联系人的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="5741e-133">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="5741e-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="5741e-134">在第七个迭代中，我们通过添加对 Ajax 的支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="5741e-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="5741e-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="5741e-135">This Iteration</span></span>

<span data-ttu-id="5741e-136">在联系人管理器应用程序前一次迭代，我们创建单元测试以提供网络安全代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="5741e-137">用于创建单元测试的动机是使我们的代码更具弹性，若要更改。</span><span class="sxs-lookup"><span data-stu-id="5741e-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="5741e-138">使用就地的单元测试，我们可以不假思索地对代码进行任何更改，并立即知道是否但我们破坏了现有功能。</span><span class="sxs-lookup"><span data-stu-id="5741e-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="5741e-139">在此迭代中，我们使用单元测试完全不同目的。</span><span class="sxs-lookup"><span data-stu-id="5741e-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="5741e-140">在此迭代中，我们使用单元测试的调用应用程序设计理念一部分*测试驱动开发*。</span><span class="sxs-lookup"><span data-stu-id="5741e-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="5741e-141">当您练习测试驱动开发，首先编写测试，然后编写针对测试的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="5741e-142">更确切地说，当练习测试驱动开发，有三个步骤，在完成后创建代码 (红色 / 绿色/重构):</span><span class="sxs-lookup"><span data-stu-id="5741e-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="5741e-143">编写失败 （红色） 的单元测试</span><span class="sxs-lookup"><span data-stu-id="5741e-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="5741e-144">编写代码中通过单元测试 （绿色）</span><span class="sxs-lookup"><span data-stu-id="5741e-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="5741e-145">重构代码 （重构）</span><span class="sxs-lookup"><span data-stu-id="5741e-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="5741e-146">首先，你编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-146">First, you write the unit test.</span></span> <span data-ttu-id="5741e-147">单元测试应表达你打算为您的代码的预期行为。</span><span class="sxs-lookup"><span data-stu-id="5741e-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="5741e-148">当你首次创建单元测试时，单元测试应失败。</span><span class="sxs-lookup"><span data-stu-id="5741e-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="5741e-149">测试应失败，因为尚未编写满足测试任何应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="5741e-150">接下来，按顺序传递使单元测试编写刚好足够的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="5741e-151">目标是 laziest、 sloppiest 和速度最快可能方式编写的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="5741e-152">不应浪费时间思考一下你的应用程序的体系结构。</span><span class="sxs-lookup"><span data-stu-id="5741e-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="5741e-153">相反，你应专注于编写代码满足表示由单元测试的目的所需的最少工作量。</span><span class="sxs-lookup"><span data-stu-id="5741e-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="5741e-154">最后，在编写完足够的代码后，你可以一步并考虑你的应用程序的总体体系结构。</span><span class="sxs-lookup"><span data-stu-id="5741e-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="5741e-155">在此步骤中，重写 （重构） 你的代码通过利用软件设计模式-例如的存储库模式-以使代码更易于维护。</span><span class="sxs-lookup"><span data-stu-id="5741e-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="5741e-156">因为你的代码涵盖的单元测试，你便可以 fearlessly 重写此步骤中的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="5741e-157">有很多好处由测试驱动开发在其中完成练习导致的。</span><span class="sxs-lookup"><span data-stu-id="5741e-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="5741e-158">首先，测试驱动开发强制您可以专注于实际上需要以编写的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="5741e-159">因为你不断侧重于只编写足够的代码来传递特定测试，将阻止到杂草发散型和写入大量您不应使用的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="5741e-160">其次，"第一次测试"的设计方法将强制你编写代码，从如何将使用你代码的角度来看。</span><span class="sxs-lookup"><span data-stu-id="5741e-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="5741e-161">换而言之，如果测试驱动开发在其中完成练习，您不断地编写测试从用户角度来看。</span><span class="sxs-lookup"><span data-stu-id="5741e-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="5741e-162">因此，测试驱动开发会导致更简洁且更易于理解的 Api。</span><span class="sxs-lookup"><span data-stu-id="5741e-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="5741e-163">最后，测试驱动开发将强制你编写的应用程序的正常过程的一部分编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="5741e-164">随着项目截止时间的临近，通常多测试是窗口出现故障的第一个操作。</span><span class="sxs-lookup"><span data-stu-id="5741e-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="5741e-165">当测试驱动开发，在其中完成练习另一方面，你很有可能是良性有关编写单元测试，因为测试驱动开发使单元测试中央为构建一个应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="5741e-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5741e-166">若要了解有关测试驱动开发的详细信息，建议你阅读 Michael 羽化簿**工作有效地使用旧代码**。</span><span class="sxs-lookup"><span data-stu-id="5741e-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>


<span data-ttu-id="5741e-167">在此迭代中，我们将一项新功能添加到我们的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="5741e-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="5741e-168">我们将添加对联系人组的支持。</span><span class="sxs-lookup"><span data-stu-id="5741e-168">We add support for Contact Groups.</span></span> <span data-ttu-id="5741e-169">你可以使用联系人组将你的联系人组织为类别，如业务和友元组。</span><span class="sxs-lookup"><span data-stu-id="5741e-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="5741e-170">我们将此新功能添加到我们的应用程序，按照测试驱动开发的进程。</span><span class="sxs-lookup"><span data-stu-id="5741e-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="5741e-171">我们将首先编写单元测试，并且我们将编写所有我们针对这些测试的代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="5741e-172">什么获取测试</span><span class="sxs-lookup"><span data-stu-id="5741e-172">What Gets Tested</span></span>

<span data-ttu-id="5741e-173">如我们在前一次迭代中所述，您通常不要的数据访问逻辑编写单元测试或查看逻辑。</span><span class="sxs-lookup"><span data-stu-id="5741e-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="5741e-174">您不 t 写入单元测试的数据访问逻辑，因为访问数据库是一个相对较慢的操作。</span><span class="sxs-lookup"><span data-stu-id="5741e-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="5741e-175">您不 t 写入单元测试的视图逻辑，因为访问视图需要 web 服务器是一个相对较慢的操作的运转。</span><span class="sxs-lookup"><span data-stu-id="5741e-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="5741e-176">你不应 t 编写单元测试，除非测试可执行反复非常快</span><span class="sxs-lookup"><span data-stu-id="5741e-176">You shouldn t write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="5741e-177">因为测试驱动开发驱动的单元测试中，我们重点最初编写控制器和业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="5741e-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="5741e-178">我们避免触摸视图的数据库。</span><span class="sxs-lookup"><span data-stu-id="5741e-178">We avoid touching the database or views.</span></span> <span data-ttu-id="5741e-179">我们获胜 t 修改数据库或本教程的最后才创建我们的视图。</span><span class="sxs-lookup"><span data-stu-id="5741e-179">We won t modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="5741e-180">我们开始什么可以进行测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="5741e-181">创建用户情景</span><span class="sxs-lookup"><span data-stu-id="5741e-181">Creating User Stories</span></span>

<span data-ttu-id="5741e-182">当测试驱动开发在其中完成练习，你始终通过启动编写的测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="5741e-183">这将立即引发问题： 如何决定哪个测试将第一次？</span><span class="sxs-lookup"><span data-stu-id="5741e-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="5741e-184">若要回答这个问题，应编写一套[*用户情景*](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="5741e-184">To answer this question, you should write a set of [*user stories*](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="5741e-185">用户情景是非常短暂 （通常一个句子） 描述的软件要求。</span><span class="sxs-lookup"><span data-stu-id="5741e-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="5741e-186">它应从用户角度来看写入的要求的非技术说明。</span><span class="sxs-lookup"><span data-stu-id="5741e-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="5741e-187">此处 s 描述新的联系人组功能所需的功能的用户情景的集：</span><span class="sxs-lookup"><span data-stu-id="5741e-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="5741e-188">用户可以查看联系人的组的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="5741e-189">用户可以创建新联系人的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="5741e-190">用户可以删除现有联系人组。</span><span class="sxs-lookup"><span data-stu-id="5741e-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="5741e-191">创建新的联系人时，用户可以选择联系人的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="5741e-192">编辑现有联系人时，用户可以选择一个联系人的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="5741e-193">在索引视图中显示的联系人的组列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="5741e-194">当用户单击联系人的组时，显示匹配联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="5741e-195">请注意，此列表的用户情景客户完全理解。</span><span class="sxs-lookup"><span data-stu-id="5741e-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="5741e-196">并没有提及的技术实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="5741e-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="5741e-197">虽然过程中生成应用程序，组的用户情景可能会变得更完善。</span><span class="sxs-lookup"><span data-stu-id="5741e-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="5741e-198">为多个情景 （要求），可能会中断用户情景。</span><span class="sxs-lookup"><span data-stu-id="5741e-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="5741e-199">例如，你可能会决定创建一个新的联系人组应涉及验证。</span><span class="sxs-lookup"><span data-stu-id="5741e-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="5741e-200">提交联系人组没有名称应返回验证错误。</span><span class="sxs-lookup"><span data-stu-id="5741e-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="5741e-201">创建的用户情景的列表后，你就可以编写第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="5741e-202">我们首先创建一个单元测试用于查看的联系人的组的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="5741e-203">列出联系人的组</span><span class="sxs-lookup"><span data-stu-id="5741e-203">Listing Contact Groups</span></span>

<span data-ttu-id="5741e-204">我们第一个用户情景，用户应该是能够查看联系人的组的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="5741e-205">我们需要使用测试 express 这篇文章。</span><span class="sxs-lookup"><span data-stu-id="5741e-205">We need to express this story with a test.</span></span>

<span data-ttu-id="5741e-206">创建新的单元测试，请右键单击 Controllers 文件夹在 ContactManager.Tests 项目中，选择**添加、 新建测试**，并选择**单元测试**模板 （请参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="5741e-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="5741e-207">在新的单元测试 GroupControllerTest.vb 并单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="5741e-207">Name the new unit test GroupControllerTest.vb and click the **OK** button.</span></span>


<span data-ttu-id="5741e-208">[![添加 GroupControllerTest 单元测试](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-vb/_static/image1.jpg)](iteration-6-use-test-driven-development-vb/_static/image1.png)</span></span>

<span data-ttu-id="5741e-209">**图 01**： 添加 GroupControllerTest 单元测试 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image2.png))</span></span>


<span data-ttu-id="5741e-210">我们第一个单元测试包含在清单 1。</span><span class="sxs-lookup"><span data-stu-id="5741e-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="5741e-211">此测试验证组控制器的 index （） 方法返回一组的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="5741e-212">测试将验证的组的集合视图中返回数据。</span><span class="sxs-lookup"><span data-stu-id="5741e-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="5741e-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-213">**Listing 1 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample1.vb)]

<span data-ttu-id="5741e-214">当你第一次键入列出 Visual Studio 中的 1 中的代码时，你将获得大量的红色波浪线。</span><span class="sxs-lookup"><span data-stu-id="5741e-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="5741e-215">我们尚未创建 GroupController 或组类。</span><span class="sxs-lookup"><span data-stu-id="5741e-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="5741e-216">此时，我们可以 t 甚至生成我们的应用程序，以便我们可以 t 执行我们的第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="5741e-217">S 良好。</span><span class="sxs-lookup"><span data-stu-id="5741e-217">That s good.</span></span> <span data-ttu-id="5741e-218">将计为未通过的测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-218">That counts as a failing test.</span></span> <span data-ttu-id="5741e-219">因此，我们现在有权开始编写应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="5741e-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="5741e-220">我们需要编写足够的代码来执行我们的测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="5741e-221">列出 2 中的组控制器类包含需通过单元测试的代码的最低要求。</span><span class="sxs-lookup"><span data-stu-id="5741e-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="5741e-222">Index （） 操作返回组 （组类定义中列出的 3） 的静态编码的的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="5741e-223">**Listing 2 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-223">**Listing 2 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample2.vb)]

<span data-ttu-id="5741e-224">**Listing 3 - Models\Group.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-224">**Listing 3 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample3.vb)]

<span data-ttu-id="5741e-225">我们将 GroupController 和组类添加到我们的项目之后，我们第一个单元测试成功完成 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="5741e-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="5741e-226">我们已完成通过的测试所需的最小工作量。</span><span class="sxs-lookup"><span data-stu-id="5741e-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="5741e-227">是时候纸婚。</span><span class="sxs-lookup"><span data-stu-id="5741e-227">It is time to celebrate.</span></span>


<span data-ttu-id="5741e-228">[![Success!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-228">[![Success!](iteration-6-use-test-driven-development-vb/_static/image2.jpg)](iteration-6-use-test-driven-development-vb/_static/image3.png)</span></span>

<span data-ttu-id="5741e-229">**图 02**： 成功 ！ ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image4.png))</span></span>


## <a name="creating-contact-groups"></a><span data-ttu-id="5741e-230">创建联系人的组</span><span class="sxs-lookup"><span data-stu-id="5741e-230">Creating Contact Groups</span></span>

<span data-ttu-id="5741e-231">现在我们可以转到第二个用户情景。</span><span class="sxs-lookup"><span data-stu-id="5741e-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="5741e-232">我们需要能够创建新联系人的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="5741e-233">我们需要使用测试 express 此目的。</span><span class="sxs-lookup"><span data-stu-id="5741e-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="5741e-234">列出 4 中的测试验证调用 create （） 方法与新的组将组添加到组 index （） 方法返回的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="5741e-235">换而言之，如果我创建一个新组然后我应能够新组取回从 index （） 方法返回的组的列表。</span><span class="sxs-lookup"><span data-stu-id="5741e-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="5741e-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-236">**Listing 4 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample4.vb)]

<span data-ttu-id="5741e-237">在测试中列出 4 调用组控制器与新联系人组的 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="5741e-238">接下来，测试验证，调用组控制器 index （） 方法返回新的组中查看数据。</span><span class="sxs-lookup"><span data-stu-id="5741e-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="5741e-239">列出 5 中的已修改的组控制器包含更改通过新的测试所需的最低。</span><span class="sxs-lookup"><span data-stu-id="5741e-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="5741e-240">**Listing 5 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-240">**Listing 5 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample5.vb)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="5741e-241">列出 5 中的组控制器具有新的 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="5741e-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="5741e-242">此操作将组添加到组的集合。</span><span class="sxs-lookup"><span data-stu-id="5741e-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="5741e-243">请注意 index （） 操作修改为返回的组的集合的内容。</span><span class="sxs-lookup"><span data-stu-id="5741e-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="5741e-244">同样，我们进行裸机最少量的工作来进行传递的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="5741e-245">我们对组控制器进行这些更改后，我们单元的所有测试都通过。</span><span class="sxs-lookup"><span data-stu-id="5741e-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="5741e-246">添加验证</span><span class="sxs-lookup"><span data-stu-id="5741e-246">Adding Validation</span></span>

<span data-ttu-id="5741e-247">显式用户情景中，未指定此要求。</span><span class="sxs-lookup"><span data-stu-id="5741e-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="5741e-248">但是，它是合理要求一组有一个名称。</span><span class="sxs-lookup"><span data-stu-id="5741e-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="5741e-249">否则，组织联系人为组，将不会非常有用。</span><span class="sxs-lookup"><span data-stu-id="5741e-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="5741e-250">列出 6 包含新的测试表明此目的。</span><span class="sxs-lookup"><span data-stu-id="5741e-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="5741e-251">此测试验证尝试未提供的验证错误消息模型状态中的名称结果情况下创建组。</span><span class="sxs-lookup"><span data-stu-id="5741e-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="5741e-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-252">**Listing 6 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample6.vb)]

<span data-ttu-id="5741e-253">为了满足此测试，我们需要添加到组类 （请参阅列出 7） 的名称属性。</span><span class="sxs-lookup"><span data-stu-id="5741e-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="5741e-254">此外，我们需要将一小段验证逻辑添加到我们组控制器 s create （） 操作 （请参阅列出 8）。</span><span class="sxs-lookup"><span data-stu-id="5741e-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="5741e-255">**Listing 7 - Models\Group.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-255">**Listing 7 - Models\Group.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample7.vb)]

<span data-ttu-id="5741e-256">**Listing 8 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-256">**Listing 8 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample8.vb)]

<span data-ttu-id="5741e-257">请注意，组控制器 create （） 操作现在包含同时验证和数据库的逻辑。</span><span class="sxs-lookup"><span data-stu-id="5741e-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="5741e-258">当前，使用组控制器的数据库所包含的只是内存中的集合。</span><span class="sxs-lookup"><span data-stu-id="5741e-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="5741e-259">重构的时间</span><span class="sxs-lookup"><span data-stu-id="5741e-259">Time to Refactor</span></span>

<span data-ttu-id="5741e-260">红色/绿色/重构的第三步是重构一部分。</span><span class="sxs-lookup"><span data-stu-id="5741e-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="5741e-261">此时，我们需要从我们的代码返回步骤并考虑如何我们可以重构应用程序以提高其设计。</span><span class="sxs-lookup"><span data-stu-id="5741e-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="5741e-262">重构阶段是从该处我们认真考虑实施软件设计原则和模式的最佳方式的阶段。</span><span class="sxs-lookup"><span data-stu-id="5741e-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="5741e-263">我们可以随意修改我们代码中我们选择以改进代码的设计以任何方式。</span><span class="sxs-lookup"><span data-stu-id="5741e-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="5741e-264">我们有安全网我们阻止在出现中断现有功能的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="5741e-265">现在，我们组控制器是优秀的软件设计角度混乱。</span><span class="sxs-lookup"><span data-stu-id="5741e-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="5741e-266">组控制器包含验证和数据访问代码 tangled 的的混乱。</span><span class="sxs-lookup"><span data-stu-id="5741e-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="5741e-267">若要避免违反单个责任原则，我们需要将这些问题分离到不同的类。</span><span class="sxs-lookup"><span data-stu-id="5741e-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="5741e-268">我们重构的组控制器类包含在列出 9。</span><span class="sxs-lookup"><span data-stu-id="5741e-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="5741e-269">控制器已修改为使用 ContactManager 服务层。</span><span class="sxs-lookup"><span data-stu-id="5741e-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="5741e-270">这是我们的联系人控制器使用的相同服务层。</span><span class="sxs-lookup"><span data-stu-id="5741e-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="5741e-271">列出 10 包含添加到 ContactManager 服务层，以支持验证、 列出和创建组的新方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="5741e-272">IContactManagerService 接口已更新为包括新方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="5741e-273">列出 11 包含一个新的 FakeContactManagerRepository 类实现 IContactManagerRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="5741e-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="5741e-274">与不同的是还实现 IContactManagerRepository 接口 EntityContactManagerRepository 类，我们新 FakeContactManagerRepository 类不与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="5741e-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="5741e-275">FakeContactManagerRepository 类使用的内存中集合作为代理的数据库。</span><span class="sxs-lookup"><span data-stu-id="5741e-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="5741e-276">作为假存储库层，我们将在我们的单元测试中使用此类。</span><span class="sxs-lookup"><span data-stu-id="5741e-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="5741e-277">**Listing 9 - Controllers\GroupController.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-277">**Listing 9 - Controllers\GroupController.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample9.vb)]

<span data-ttu-id="5741e-278">**Listing 10 - Controllers\ContactManagerService.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-278">**Listing 10 - Controllers\ContactManagerService.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample10.vb)]

<span data-ttu-id="5741e-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-279">**Listing 11 - Controllers\FakeContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample11.vb)]


<span data-ttu-id="5741e-280">修改接口需要 IContactManagerRepository 用于 EntityContactManagerRepository 类中实现的 CreateGroup() 和 ListGroups() 方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="5741e-281">执行此操作的 laziest 和最快方法是添加存根 （stub） 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5741e-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample12.vb)]


<span data-ttu-id="5741e-282">最后，我们的应用程序的设计这些更改要求我们使到我们的单元测试中的一些修改。</span><span class="sxs-lookup"><span data-stu-id="5741e-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="5741e-283">现在，我们需要执行单元测试时使用 FakeContactManagerRepository。</span><span class="sxs-lookup"><span data-stu-id="5741e-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="5741e-284">更新后的 GroupControllerTest 类包含在列出 12。</span><span class="sxs-lookup"><span data-stu-id="5741e-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="5741e-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-285">**Listing 12 - Controllers\GroupControllerTest.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample13.vb)]

<span data-ttu-id="5741e-286">我们进行所有这些后更改，同样，所有我们通过单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="5741e-287">我们已经完成红色/绿色/重构的整个周期。</span><span class="sxs-lookup"><span data-stu-id="5741e-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="5741e-288">我们已实施的第一个的两个用户情景。</span><span class="sxs-lookup"><span data-stu-id="5741e-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="5741e-289">我们现在有支持要求表示在用户情景中的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="5741e-290">实现用户情景的其余部分包括重复的红色/绿色/重构此相同循环。</span><span class="sxs-lookup"><span data-stu-id="5741e-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="5741e-291">修改我们的数据库</span><span class="sxs-lookup"><span data-stu-id="5741e-291">Modifying our Database</span></span>

<span data-ttu-id="5741e-292">遗憾的是，即使我们已经满足所有要求表示我们单元测试，我们的工作不会执行。</span><span class="sxs-lookup"><span data-stu-id="5741e-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="5741e-293">我们仍需要修改我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="5741e-293">We still need to modify our database.</span></span>

<span data-ttu-id="5741e-294">我们需要创建一个新的组数据库表。</span><span class="sxs-lookup"><span data-stu-id="5741e-294">We need to create a new Group database table.</span></span> <span data-ttu-id="5741e-295">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="5741e-295">Follow these steps:</span></span>

1. <span data-ttu-id="5741e-296">在服务器资源管理器窗口中，右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="5741e-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="5741e-297">输入在表设计器中，如下所述的两个列。</span><span class="sxs-lookup"><span data-stu-id="5741e-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="5741e-298">将标记作为 primary key 和标识列的 Id 列。</span><span class="sxs-lookup"><span data-stu-id="5741e-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="5741e-299">通过单击软盘图标保存命名组的新表。</span><span class="sxs-lookup"><span data-stu-id="5741e-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.12_table01"></a>


| <span data-ttu-id="5741e-300">**列名称**</span><span class="sxs-lookup"><span data-stu-id="5741e-300">**Column Name**</span></span> | <span data-ttu-id="5741e-301">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="5741e-301">**Data Type**</span></span> | <span data-ttu-id="5741e-302">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="5741e-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5741e-303">Id</span><span class="sxs-lookup"><span data-stu-id="5741e-303">Id</span></span> | <span data-ttu-id="5741e-304">int</span><span class="sxs-lookup"><span data-stu-id="5741e-304">int</span></span> | <span data-ttu-id="5741e-305">False</span><span class="sxs-lookup"><span data-stu-id="5741e-305">False</span></span> |
| <span data-ttu-id="5741e-306">名称</span><span class="sxs-lookup"><span data-stu-id="5741e-306">Name</span></span> | <span data-ttu-id="5741e-307">nvarchar(50)</span><span class="sxs-lookup"><span data-stu-id="5741e-307">nvarchar(50)</span></span> | <span data-ttu-id="5741e-308">False</span><span class="sxs-lookup"><span data-stu-id="5741e-308">False</span></span> |


<span data-ttu-id="5741e-309">接下来，我们需要从联系人表中删除的所有数据 (否则，我们获胜 t 能够创建联系人和组表之间的关系)。</span><span class="sxs-lookup"><span data-stu-id="5741e-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won t be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="5741e-310">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="5741e-310">Follow these steps:</span></span>

1. <span data-ttu-id="5741e-311">右键单击联系人表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="5741e-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="5741e-312">删除的所有行。</span><span class="sxs-lookup"><span data-stu-id="5741e-312">Delete all of the rows.</span></span>

<span data-ttu-id="5741e-313">接下来，我们需要定义组数据库表和现有的联系人数据库表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="5741e-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="5741e-314">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="5741e-314">Follow these steps:</span></span>

1. <span data-ttu-id="5741e-315">双击服务器资源管理器窗口以打开表设计器中的联系人表。</span><span class="sxs-lookup"><span data-stu-id="5741e-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="5741e-316">将新的整数列添加到 Contacts 表名为 GroupId。</span><span class="sxs-lookup"><span data-stu-id="5741e-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="5741e-317">单击关系按钮以打开外键关系对话框 （请参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="5741e-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="5741e-318">单击添加按钮。</span><span class="sxs-lookup"><span data-stu-id="5741e-318">Click the Add button.</span></span>
5. <span data-ttu-id="5741e-319">单击表和列规范按钮旁边显示的省略号按钮。</span><span class="sxs-lookup"><span data-stu-id="5741e-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="5741e-320">在表和列对话框中，选择作为主键表和作为主键列的 Id 的组。</span><span class="sxs-lookup"><span data-stu-id="5741e-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="5741e-321">选择联系人作为外键表和作为外键列的 GroupId （请参见图 4）。</span><span class="sxs-lookup"><span data-stu-id="5741e-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="5741e-322">单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="5741e-322">Click the OK button.</span></span>
7. <span data-ttu-id="5741e-323">下**INSERT 和 UPDATE 规范**，选择值**Cascade**为**删除规则**。</span><span class="sxs-lookup"><span data-stu-id="5741e-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="5741e-324">单击关闭按钮以关闭外键关系对话框。</span><span class="sxs-lookup"><span data-stu-id="5741e-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="5741e-325">单击保存按钮以保存对联系人表的更改。</span><span class="sxs-lookup"><span data-stu-id="5741e-325">Click the Save button to save the changes to the Contacts table.</span></span>


<span data-ttu-id="5741e-326">[![创建数据库表关系](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-vb/_static/image3.jpg)](iteration-6-use-test-driven-development-vb/_static/image5.png)</span></span>

<span data-ttu-id="5741e-327">**图 03**： 创建数据库表关系 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image6.png))</span></span>


<span data-ttu-id="5741e-328">[![指定表关系](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-328">[![Specifying table relationships](iteration-6-use-test-driven-development-vb/_static/image4.jpg)](iteration-6-use-test-driven-development-vb/_static/image7.png)</span></span>

<span data-ttu-id="5741e-329">**图 04**： 指定表关系 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image8.png))</span></span>


### <a name="updating-our-data-model"></a><span data-ttu-id="5741e-330">更新我们的数据模型</span><span class="sxs-lookup"><span data-stu-id="5741e-330">Updating our Data Model</span></span>

<span data-ttu-id="5741e-331">接下来，我们需要更新我们的数据模型来表示新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="5741e-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="5741e-332">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="5741e-332">Follow these steps:</span></span>

1. <span data-ttu-id="5741e-333">双击模型文件夹，打开实体设计器中的 ContactManagerModel.edmx 文件。</span><span class="sxs-lookup"><span data-stu-id="5741e-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="5741e-334">右键单击设计器图面，然后选择菜单选项**从数据库更新模型**。</span><span class="sxs-lookup"><span data-stu-id="5741e-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="5741e-335">在更新向导中，选择组表，然后单击完成按钮 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="5741e-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="5741e-336">右键单击组实体，然后选择菜单选项**重命名**。</span><span class="sxs-lookup"><span data-stu-id="5741e-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="5741e-337">更改的名称*组*实体到*组*（采用单数形式）。</span><span class="sxs-lookup"><span data-stu-id="5741e-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="5741e-338">右键单击联系人实体的底部将显示的组导航属性。</span><span class="sxs-lookup"><span data-stu-id="5741e-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="5741e-339">更改的名称*组*导航属性*组*（采用单数形式）。</span><span class="sxs-lookup"><span data-stu-id="5741e-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>


<span data-ttu-id="5741e-340">[![更新数据库中的实体框架模型](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-vb/_static/image5.jpg)](iteration-6-use-test-driven-development-vb/_static/image9.png)</span></span>

<span data-ttu-id="5741e-341">**图 05**： 更新从数据库的实体框架模型 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image10.png))</span></span>


<span data-ttu-id="5741e-342">完成这些步骤后，你的数据模型将表示的联系人和组的表。</span><span class="sxs-lookup"><span data-stu-id="5741e-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="5741e-343">实体设计器应显示这两个实体 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="5741e-343">The Entity Designer should show both entities (see Figure 6).</span></span>


<span data-ttu-id="5741e-344">[![实体设计器中显示组和联系人](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-vb/_static/image6.jpg)](iteration-6-use-test-driven-development-vb/_static/image11.png)</span></span>

<span data-ttu-id="5741e-345">**图 06**： 实体设计器中显示组和联系人 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image12.png))</span></span>


### <a name="creating-our-repository-classes"></a><span data-ttu-id="5741e-346">创建我们存储库类</span><span class="sxs-lookup"><span data-stu-id="5741e-346">Creating our Repository Classes</span></span>

<span data-ttu-id="5741e-347">接下来，我们需要实现我们存储库类。</span><span class="sxs-lookup"><span data-stu-id="5741e-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="5741e-348">在此迭代过程中，我们添加几个新方法到 IContactManagerRepository 界面在编写代码以满足我们的单元测试时。</span><span class="sxs-lookup"><span data-stu-id="5741e-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="5741e-349">在列出 14 包含 IContactManagerRepository 接口的最终版本。</span><span class="sxs-lookup"><span data-stu-id="5741e-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="5741e-350">**列出 14-Models\IContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-350">**Listing 14 - Models\IContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample14.vb)]

<span data-ttu-id="5741e-351">我们还没有实际实现任何与使用我们的实际 EntityContactManagerRepository 类中的联系人组相关的方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-351">We haven t actually implemented any of the methods related to working with contact groups in our real EntityContactManagerRepository class.</span></span> <span data-ttu-id="5741e-352">目前，EntityContactManagerRepository 类具有存根 （stub） 方法的每个 IContactManagerRepository 界面中列出联系人组方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="5741e-353">例如，ListGroups() 方法当前类似如下所示：</span><span class="sxs-lookup"><span data-stu-id="5741e-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample15.vb)]

<span data-ttu-id="5741e-354">存根 （stub） 方法使我们能够编译我们的应用程序和通过的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="5741e-355">但是，现在它是时间实际实现这些方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="5741e-356">EntityContactManagerRepository 类的最终版本包含在列出 13。</span><span class="sxs-lookup"><span data-stu-id="5741e-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="5741e-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="5741e-357">**Listing 13 - Models\EntityContactManagerRepository.vb**</span></span>

[!code-vb[Main](iteration-6-use-test-driven-development-vb/samples/sample16.vb)]

### <a name="creating-the-views"></a><span data-ttu-id="5741e-358">创建视图</span><span class="sxs-lookup"><span data-stu-id="5741e-358">Creating the Views</span></span>

<span data-ttu-id="5741e-359">ASP.NET MVC 应用程序时使用的默认 ASP.NET 视图引擎。</span><span class="sxs-lookup"><span data-stu-id="5741e-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="5741e-360">因此，don t 创建视图，以响应特定的单元测试。</span><span class="sxs-lookup"><span data-stu-id="5741e-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="5741e-361">但是，因为应用程序将毫无用处，除非视图，我们可以 t 完成此迭代，而创建和修改联系人管理器应用程序中包含的视图。</span><span class="sxs-lookup"><span data-stu-id="5741e-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="5741e-362">我们需要创建以下新视图用于管理联系人的组 （请参阅图 7）：</span><span class="sxs-lookup"><span data-stu-id="5741e-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="5741e-363">Views\Group\Index.aspx 的联系人的组的显示列表</span><span class="sxs-lookup"><span data-stu-id="5741e-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="5741e-364">Views\Group\Delete.aspx-用于删除联系人的组的显示确认窗体</span><span class="sxs-lookup"><span data-stu-id="5741e-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>


<span data-ttu-id="5741e-365">[![组索引视图](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-365">[![The Group Index view](iteration-6-use-test-driven-development-vb/_static/image7.jpg)](iteration-6-use-test-driven-development-vb/_static/image13.png)</span></span>

<span data-ttu-id="5741e-366">**图 07**: 组索引视图 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image14.png))</span></span>


<span data-ttu-id="5741e-367">我们需要修改以下现有视图，使其包含联系人的组：</span><span class="sxs-lookup"><span data-stu-id="5741e-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="5741e-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="5741e-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="5741e-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="5741e-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="5741e-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="5741e-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="5741e-371">你可以通过查看此教程中随附的 Visual Studio 应用程序看到修改后的视图。</span><span class="sxs-lookup"><span data-stu-id="5741e-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="5741e-372">例如，图 8 显示了联系人索引视图。</span><span class="sxs-lookup"><span data-stu-id="5741e-372">For example, Figure 8 illustrates the Contact Index view.</span></span>


<span data-ttu-id="5741e-373">[![请与索引视图](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="5741e-373">[![The Contact Index view](iteration-6-use-test-driven-development-vb/_static/image8.jpg)](iteration-6-use-test-driven-development-vb/_static/image15.png)</span></span>

<span data-ttu-id="5741e-374">**图 08**: 联系人索引视图 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-vb/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="5741e-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-vb/_static/image16.png))</span></span>


## <a name="summary"></a><span data-ttu-id="5741e-375">总结</span><span class="sxs-lookup"><span data-stu-id="5741e-375">Summary</span></span>

<span data-ttu-id="5741e-376">在此迭代中，我们添加新功能到我们的联系人管理器应用程序按照测试驱动开发应用程序设计方法。</span><span class="sxs-lookup"><span data-stu-id="5741e-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="5741e-377">通过创建一组用户情景，我们已开始。</span><span class="sxs-lookup"><span data-stu-id="5741e-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="5741e-378">我们创建一组单元测试，对应于表达用户情景的需求。</span><span class="sxs-lookup"><span data-stu-id="5741e-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="5741e-379">最后，我们已写入刚好足够的代码，以满足要求的单元测试来表示。</span><span class="sxs-lookup"><span data-stu-id="5741e-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="5741e-380">我们完成编写足够的代码来满足表示单元测试的要求后，我们更新我们的数据库和视图。</span><span class="sxs-lookup"><span data-stu-id="5741e-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="5741e-381">我们向我们的数据库添加新的组表，并更新我们实体框架数据模型。</span><span class="sxs-lookup"><span data-stu-id="5741e-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="5741e-382">我们还创建和修改一组视图。</span><span class="sxs-lookup"><span data-stu-id="5741e-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="5741e-383">在下一次迭代-最后一个迭代-我们重写应用程序以充分利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="5741e-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="5741e-384">通过利用 Ajax，我们将提高响应能力和联系人管理器应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="5741e-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5741e-385">[上一页](iteration-5-create-unit-tests-vb.md)
> [下一页](iteration-7-add-ajax-functionality-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5741e-385">[Previous](iteration-5-create-unit-tests-vb.md)
[Next](iteration-7-add-ajax-functionality-vb.md)</span></span>
