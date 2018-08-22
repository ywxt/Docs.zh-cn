---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: 迭代 6 – 使用测试驱动开发 (C#) |Microsoft Docs
author: microsoft
description: 在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。 此小版本中...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: 3c4358a1b979ab95d8ac25551e21ee95d75e5eae
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834954"
---
<a name="iteration-6--use-test-driven-development-c"></a><span data-ttu-id="1c2fd-104">迭代 6 – 使用测试驱动开发 (C#)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-104">Iteration #6 – Use test-driven development (C#)</span></span>
====================
<span data-ttu-id="1c2fd-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="1c2fd-106">下载代码</span><span class="sxs-lookup"><span data-stu-id="1c2fd-106">Download Code</span></span>](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> <span data-ttu-id="1c2fd-107">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-107">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="1c2fd-108">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-108">In this iteration, we add contact groups.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-c"></a><span data-ttu-id="1c2fd-109">生成联系人管理 ASP.NET MVC 应用程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-109">Building a Contact Management ASP.NET MVC Application (C#)</span></span>
  

<span data-ttu-id="1c2fd-110">在本系列教程，我们构建整个联系人管理应用程序从头到尾完成。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-110">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="1c2fd-111">联系人管理器应用程序，可存储联系人信息的名称，电话号码和电子邮件地址的人的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-111">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="1c2fd-112">我们通过多个迭代中生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-112">We build the application over multiple iterations.</span></span> <span data-ttu-id="1c2fd-113">每次迭代时，我们逐渐提高应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-113">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="1c2fd-114">此多个迭代方法的目标是帮助你了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-114">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="1c2fd-115">迭代 1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-115">Iteration #1 - Create the application.</span></span> <span data-ttu-id="1c2fd-116">在第一次迭代中，我们创建联系人管理器中的最简单方法可能。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-116">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="1c2fd-117">我们将添加对基本数据库操作的支持： 创建、 读取、 更新和删除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-117">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="1c2fd-118">迭代 2 – 使应用程序看上去更美观。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-118">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="1c2fd-119">在此迭代中，我们通过修改默认 ASP.NET MVC 视图母版页和级联样式表提高应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-119">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="1c2fd-120">迭代 3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-120">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="1c2fd-121">在第三个迭代中，我们将添加基本窗体验证。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-121">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="1c2fd-122">我们阻止用户提交窗体而无法完成所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-122">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="1c2fd-123">我们还验证电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-123">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="1c2fd-124">迭代 4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-124">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="1c2fd-125">在此第四个迭代中，我们将充分利用多个软件设计模式，以使其更轻松地监视和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-125">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="1c2fd-126">例如，我们将重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-126">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="1c2fd-127">迭代 5 — 创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-127">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="1c2fd-128">在第五个迭代中，我们使我们的应用程序更轻松地监视和修改通过添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-128">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="1c2fd-129">我们模拟我们数据模型类，并生成为控制器和验证逻辑单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-129">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="1c2fd-130">迭代 6-使用测试驱动的开发。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-130">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="1c2fd-131">在此第六个迭代中，我们将添加新功能到我们的应用程序通过首先编写单元测试并针对单元测试编写的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-131">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="1c2fd-132">在此迭代中，我们将添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-132">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="1c2fd-133">迭代 7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-133">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="1c2fd-134">在第七个迭代中，我们通过添加对 Ajax 支持提高响应能力和我们的应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-134">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="1c2fd-135">此迭代</span><span class="sxs-lookup"><span data-stu-id="1c2fd-135">This Iteration</span></span>

<span data-ttu-id="1c2fd-136">在联系人管理器应用程序上一次迭代，我们创建单元测试，以提供网络安全代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-136">In the previous iteration of the Contact Manager application, we created unit tests to provide a safety net for our code.</span></span> <span data-ttu-id="1c2fd-137">用于创建单元测试的动机是使我们的代码更具弹性，若要更改。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-137">The motivation for creating the unit tests was to make our code more resilient to change.</span></span> <span data-ttu-id="1c2fd-138">使用中的位置的单元测试，我们可以值得庆幸的是对我们的代码进行任何更改，并立即知道是否我们破坏现有功能。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-138">With unit tests in place, we can happily make any change to our code and immediately know whether we have broken existing functionality.</span></span>

<span data-ttu-id="1c2fd-139">在此迭代中，我们使用单元测试进行完全不同的用途。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-139">In this iteration, we use unit tests for an entirely different purpose.</span></span> <span data-ttu-id="1c2fd-140">在此迭代中，我们使用单元测试作为一部分调用应用程序设计理念*测试驱动开发，*。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-140">In this iteration, we use unit tests as part of an application design philosophy called *test-driven development*.</span></span> <span data-ttu-id="1c2fd-141">当您练习测试驱动开发，首先编写测试，然后编写针对测试的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-141">When you practice test-driven development, you write tests first and then write code against the tests.</span></span>

<span data-ttu-id="1c2fd-142">更确切地说，实践测试驱动开发，有三个步骤，在完成后创建的代码 (红 / 绿/重构):</span><span class="sxs-lookup"><span data-stu-id="1c2fd-142">More precisely, when practicing test-driven development, there are three steps that you complete when creating code (Red/ Green/Refactor):</span></span>

1. <span data-ttu-id="1c2fd-143">编写的单元测试失败 （红色）</span><span class="sxs-lookup"><span data-stu-id="1c2fd-143">Write a unit test that fails (Red)</span></span>
2. <span data-ttu-id="1c2fd-144">编写代码，通过的单元测试 （绿色）</span><span class="sxs-lookup"><span data-stu-id="1c2fd-144">Write code that passes the unit test (Green)</span></span>
3. <span data-ttu-id="1c2fd-145">重构代码 （重构）</span><span class="sxs-lookup"><span data-stu-id="1c2fd-145">Refactor your code (Refactor)</span></span>

<span data-ttu-id="1c2fd-146">首先，您编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-146">First, you write the unit test.</span></span> <span data-ttu-id="1c2fd-147">单元测试应表达你打算为您的代码的预期行为。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-147">The unit test should express your intention for how you expect your code to behave.</span></span> <span data-ttu-id="1c2fd-148">当你首次创建单元测试时，单元测试应失败。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-148">When you first create the unit test, the unit test should fail.</span></span> <span data-ttu-id="1c2fd-149">测试应失败，因为尚未编写满足测试任何应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-149">The test should fail because you have not yet written any application code that satisfies the test.</span></span>

<span data-ttu-id="1c2fd-150">接下来，为了使单元测试通过编写刚好足够的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-150">Next, you write just enough code in order for the unit test to pass.</span></span> <span data-ttu-id="1c2fd-151">目标是 laziest、 sloppiest 和可能最快的方式编写的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-151">The goal is to write the code in the laziest, sloppiest and fastest possible way.</span></span> <span data-ttu-id="1c2fd-152">你不应浪费时间考虑您的应用程序的体系结构。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-152">You should not waste time thinking about the architecture of your application.</span></span> <span data-ttu-id="1c2fd-153">相反，您应集中精力编写单元测试所表达的意图满足所需代码的最少工作量。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-153">Instead, you should focus on writing the minimal amount of code necessary to satisfy the intention expressed by the unit test.</span></span>

<span data-ttu-id="1c2fd-154">最后，编写足够的代码后，你可以回过头想想您的应用程序的整体体系结构。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-154">Finally, after you have written enough code, you can step back and consider the overall architecture of your application.</span></span> <span data-ttu-id="1c2fd-155">在此步骤中，重写 （重构） 你的代码通过利用的软件设计模式-存储库模式-例如，使代码更易于维护。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-155">In this step, you rewrite (refactor) your code by taking advantage of software design patterns -- such as the repository pattern -- so that your code is more maintainable.</span></span> <span data-ttu-id="1c2fd-156">支持下大胆可以请你在此步骤中的代码重写原因由单元测试纳入您的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-156">You can fearlessly rewrite your code in this step because your code is covered by unit tests.</span></span>

<span data-ttu-id="1c2fd-157">有很多好处所产生的测试驱动开发，在其中完成练习。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-157">There are many benefits that result from practicing test-driven development.</span></span> <span data-ttu-id="1c2fd-158">首先，测试驱动开发强制您专注于实际需要编写的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-158">First, test-driven development forces you to focus on code that actually needs to be written.</span></span> <span data-ttu-id="1c2fd-159">因为你不断地关注只需编写足够的代码来传递特定的测试，请您不能进入的这个井水和写入大量永远不会将使用的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-159">Because you are constantly focused on just writing enough code to pass a particular test, you are prevented from wandering into the weeds and writing massive amounts of code that you will never use.</span></span>

<span data-ttu-id="1c2fd-160">其次，"首先测试"的设计方法会强制您从将如何使用你的代码的角度来看编写代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-160">Second, a "test first" design methodology forces you to write code from the perspective of how your code will be used.</span></span> <span data-ttu-id="1c2fd-161">换而言之，实践测试驱动开发，您会不断地编写你的测试从用户角度来看。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-161">In other words, when practicing test-driven development, you are constantly writing your tests from a user perspective.</span></span> <span data-ttu-id="1c2fd-162">因此，测试驱动开发，可能导致更干净且更易于理解的 Api。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-162">Therefore, test-driven development can result in cleaner and more understandable APIs.</span></span>

<span data-ttu-id="1c2fd-163">最后，测试驱动开发，会强制你编写单元测试编写的应用程序的正常过程的一部分。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-163">Finally, test-driven development forces you to write unit tests as part of the normal process of writing an application.</span></span> <span data-ttu-id="1c2fd-164">项目截止时间的临近，测试是通常超出窗口第一件事。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-164">As a project deadline approaches, testing is typically the first thing that goes out the window.</span></span> <span data-ttu-id="1c2fd-165">实践测试驱动开发，但是，则更有可能是良性有关编写单元测试，因为测试驱动开发，使单元测试中央为构建应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-165">When practicing test-driven development, on the other hand, you are more likely to be virtuous about writing unit tests because test-driven development makes unit tests central to the process of building an application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1c2fd-166">若要了解有关测试驱动开发的详细信息，建议您阅读 Michael Feathers 书籍**处理有效地使用旧代码**。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-166">To learn more about test-driven development, I recommend that you read Michael Feathers book **Working Effectively with Legacy Code**.</span></span>


<span data-ttu-id="1c2fd-167">在此迭代中，我们将一项新功能添加到我们的联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-167">In this iteration, we add a new feature to our Contact Manager application.</span></span> <span data-ttu-id="1c2fd-168">我们将添加对联系人组的支持。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-168">We add support for Contact Groups.</span></span> <span data-ttu-id="1c2fd-169">可以使用联系人组来组织你的联系人为如业务的类别和友元组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-169">You can use Contact Groups to organize your contacts into categories such as Business and Friend groups.</span></span>

<span data-ttu-id="1c2fd-170">我们将这一新功能添加到我们的应用程序，通过的测试驱动的开发过程。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-170">We'll add this new functionality to our application by following a process of test-driven development.</span></span> <span data-ttu-id="1c2fd-171">我们将首先编写单元测试，我们将编写所有这些测试针对我们的代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-171">We'll write our unit tests first and we'll write all of our code against these tests.</span></span>

## <a name="what-gets-tested"></a><span data-ttu-id="1c2fd-172">获取测试内容</span><span class="sxs-lookup"><span data-stu-id="1c2fd-172">What Gets Tested</span></span>

<span data-ttu-id="1c2fd-173">如我们在上一次迭代中所述，通常没有为数据访问逻辑编写单元测试或查看逻辑。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-173">As we discussed in the previous iteration, you typically do not write unit tests for data access logic or view logic.</span></span> <span data-ttu-id="1c2fd-174">您不 t 写入的数据访问逻辑的单元测试，因为访问数据库是一个相对较慢的操作。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-174">You don t write unit tests for data access logic because accessing a database is a relatively slow operation.</span></span> <span data-ttu-id="1c2fd-175">您不视图逻辑的 t 写入单元测试，因为访问视图需要快速启动的 web 服务器，这是一个相对较慢的操作。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-175">You don t write unit tests for view logic because accessing a view requires spinning up a web server which is a relatively slow operation.</span></span> <span data-ttu-id="1c2fd-176">长度应不 t 编写单元测试，除非可以执行测试，非常快</span><span class="sxs-lookup"><span data-stu-id="1c2fd-176">You shouldn t write a unit test unless the test can be executed over and over again very fast</span></span>

<span data-ttu-id="1c2fd-177">由于测试驱动开发，由单元测试，我们专注于最初编写控制器和业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-177">Because test-driven development is driven by unit tests, we focus initially on writing controller and business logic.</span></span> <span data-ttu-id="1c2fd-178">我们避免触及视图的数据库。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-178">We avoid touching the database or views.</span></span> <span data-ttu-id="1c2fd-179">我们获得了 t 修改数据库或本教程的最后才创建我们的视图。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-179">We won t modify the database or create our views until the very end of this tutorial.</span></span> <span data-ttu-id="1c2fd-180">我们开始可以测试内容。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-180">We start with what can be tested.</span></span>

## <a name="creating-user-stories"></a><span data-ttu-id="1c2fd-181">创建用户情景</span><span class="sxs-lookup"><span data-stu-id="1c2fd-181">Creating User Stories</span></span>

<span data-ttu-id="1c2fd-182">实践测试驱动开发，始终首先编写测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-182">When practicing test-driven development, you always start by writing a test.</span></span> <span data-ttu-id="1c2fd-183">这将立即引发问题： 如何确定哪些测试，以首先编写？</span><span class="sxs-lookup"><span data-stu-id="1c2fd-183">This immediately raises the question: How do you decide what test to write first?</span></span> <span data-ttu-id="1c2fd-184">若要回答此问题，应编写一套[**用户情景**](http://en.wikipedia.org/wiki/User_stories)。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-184">To answer this question, you should write a set of [**user stories**](http://en.wikipedia.org/wiki/User_stories).</span></span>

<span data-ttu-id="1c2fd-185">用户情景是很短的软件要求 （通常一个句子） 说明。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-185">A user story is a very brief (usually one sentence) description of a software requirement.</span></span> <span data-ttu-id="1c2fd-186">它应该是从用户角度编写需求的非技术说明。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-186">It should be a non-technical description of a requirement written from a user perspective.</span></span>

<span data-ttu-id="1c2fd-187">下面提供的一组描述新的联系人组功能所需的功能的用户情景：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-187">Here s the set of user stories that describe the features required by the new Contact Group functionality:</span></span>

1. <span data-ttu-id="1c2fd-188">用户可以查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-188">User can view a list of contact groups.</span></span>
2. <span data-ttu-id="1c2fd-189">用户可以创建新的联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-189">User can create a new contact group.</span></span>
3. <span data-ttu-id="1c2fd-190">用户可以删除现有的联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-190">User can delete an existing contact group.</span></span>
4. <span data-ttu-id="1c2fd-191">创建一个新的联系人时，用户可以选择联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-191">User can select a contact group when creating a new contact.</span></span>
5. <span data-ttu-id="1c2fd-192">编辑现有联系人时，用户可以选择联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-192">User can select a contact group when editing an existing contact.</span></span>
6. <span data-ttu-id="1c2fd-193">在索引视图中显示的联系人组列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-193">A list of contact groups is displayed in the Index view.</span></span>
7. <span data-ttu-id="1c2fd-194">当用户单击联系人组时，显示的匹配的联系人列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-194">When a user clicks a contact group, a list of matching contacts is displayed.</span></span>

<span data-ttu-id="1c2fd-195">请注意，此列表的用户情景的客户完全可以理解。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-195">Notice that this list of user stories is completely understandable by a customer.</span></span> <span data-ttu-id="1c2fd-196">并没有提及的技术实现详细信息。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-196">There is no mention of technical implementation details.</span></span>

<span data-ttu-id="1c2fd-197">虽然在构建过程中你的应用程序，一组用户情景可能会变得更完善。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-197">While in the process of building your application, the set of user stories can become more refined.</span></span> <span data-ttu-id="1c2fd-198">为多个情景 （要求），则可能会中断用户情景。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-198">You might break a user story into multiple stories (requirements).</span></span> <span data-ttu-id="1c2fd-199">例如，可能会决定创建新的联系人组应涉及验证。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-199">For example, you might decide that creating a new contact group should involve validation.</span></span> <span data-ttu-id="1c2fd-200">提交联系人组没有名称应返回验证错误。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-200">Submitting a contact group without a name should return a validation error.</span></span>

<span data-ttu-id="1c2fd-201">创建用户情景的列表后，已准备好编写第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-201">After you create a list of user stories, you are ready to write your first unit test.</span></span> <span data-ttu-id="1c2fd-202">我们将首先创建单元测试用于查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-202">We'll start by creating a unit test for viewing the list of contact groups.</span></span>

## <a name="listing-contact-groups"></a><span data-ttu-id="1c2fd-203">列表联系人组</span><span class="sxs-lookup"><span data-stu-id="1c2fd-203">Listing Contact Groups</span></span>

<span data-ttu-id="1c2fd-204">我们第一个用户情景是用户应该能够查看联系人组的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-204">Our first user story is that a user should be able to view a list of contact groups.</span></span> <span data-ttu-id="1c2fd-205">我们需要使用测试 express 这篇文章。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-205">We need to express this story with a test.</span></span>

<span data-ttu-id="1c2fd-206">创建新的单元测试，请右键单击 Controllers 文件夹在 ContactManager.Tests 项目中，选择**添加、 新测试**，并选择**单元测试**模板 （参见图 1）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-206">Create a new unit test by right-clicking the Controllers folder in the ContactManager.Tests project, selecting **Add, New Test**, and selecting the **Unit Test** template (see Figure 1).</span></span> <span data-ttu-id="1c2fd-207">名称在新的单元测试 GroupControllerTest.cs，然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-207">Name the new unit test GroupControllerTest.cs and click the **OK** button.</span></span>


<span data-ttu-id="1c2fd-208">[![添加 GroupControllerTest 单元测试](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-208">[![Adding the GroupControllerTest unit test](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)</span></span>

<span data-ttu-id="1c2fd-209">**图 01**： 添加 GroupControllerTest 单元测试 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-209">**Figure 01**: Adding the GroupControllerTest unit test([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image2.png))</span></span>


<span data-ttu-id="1c2fd-210">在列表 1 中包含了第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-210">Our first unit test is contained in Listing 1.</span></span> <span data-ttu-id="1c2fd-211">此测试验证组控制器的 index （） 方法返回一系列组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-211">This test verifies that the Index() method of the Group controller returns a set of Groups.</span></span> <span data-ttu-id="1c2fd-212">此测试将验证组的集合视图中返回数据。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-212">The test verifies that a collection of Groups is returned in view data.</span></span>

<span data-ttu-id="1c2fd-213">**代码清单 1-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-213">**Listing 1 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

<span data-ttu-id="1c2fd-214">当你首次在列表 1 中在 Visual Studio 中键入代码时，您将获得大量的红色波浪线。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-214">When you first type the code in Listing 1 in Visual Studio, you'll get a lot of red squiggly lines.</span></span> <span data-ttu-id="1c2fd-215">我们尚未创建 GroupController 或组类。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-215">We have not created the GroupController or Group classes.</span></span>

<span data-ttu-id="1c2fd-216">此时，我们可以 t 甚至生成我们的应用程序，以便我们可以 t 执行了第一个单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-216">At this point, we can t even build our application so we can t execute our first unit test.</span></span> <span data-ttu-id="1c2fd-217">很好的 s。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-217">That s good.</span></span> <span data-ttu-id="1c2fd-218">作为失败测试计数。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-218">That counts as a failing test.</span></span> <span data-ttu-id="1c2fd-219">因此，我们现在必须开始编写应用程序代码的权限。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-219">Therefore, we now have permission to start writing application code.</span></span> <span data-ttu-id="1c2fd-220">我们需要编写足够的代码来执行我们的测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-220">We need to write enough code to execute our test.</span></span>

<span data-ttu-id="1c2fd-221">代码清单 2 中的组控制器类包含通过单元测试所需代码的最低。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-221">The Group controller class in Listing 2 contains the bare minimum of code required to pass the unit test.</span></span> <span data-ttu-id="1c2fd-222">Index （） 操作返回组 （组类定义中清单 3） 以静态方式编码的的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-222">The Index() action returns a statically coded list of Groups (the Group class is defined in Listing 3).</span></span>

<span data-ttu-id="1c2fd-223">**代码清单 2-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-223">**Listing 2 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

<span data-ttu-id="1c2fd-224">**代码清单 3-Models\Group.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-224">**Listing 3 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

<span data-ttu-id="1c2fd-225">我们将在 GroupController 和组类添加到我们的项目后，我们的第一个单元测试成功完成 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-225">After we add the GroupController and Group classes to our project, our first unit test completes successfully (see Figure 2).</span></span> <span data-ttu-id="1c2fd-226">我们已经通过该测试所需的最小工作。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-226">We have done the minimum work required to pass the test.</span></span> <span data-ttu-id="1c2fd-227">为了庆祝就。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-227">It is time to celebrate.</span></span>


<span data-ttu-id="1c2fd-228">[![成功 ！](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-228">[![Success!](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)</span></span>

<span data-ttu-id="1c2fd-229">**图 02**： 成功 ！ ([单击此项可查看原尺寸图像](iteration-6-use-test-driven-development-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-229">**Figure 02**: Success!([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image4.png))</span></span>


## <a name="creating-contact-groups"></a><span data-ttu-id="1c2fd-230">创建联系人组</span><span class="sxs-lookup"><span data-stu-id="1c2fd-230">Creating Contact Groups</span></span>

<span data-ttu-id="1c2fd-231">现在，我们可以转到第二个用户情景。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-231">Now we can move on to the second user story.</span></span> <span data-ttu-id="1c2fd-232">我们需要能够创建新联系人组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-232">We need to be able to create new contact groups.</span></span> <span data-ttu-id="1c2fd-233">我们需要与测试 express 此目的。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-233">We need to express this intention with a test.</span></span>

<span data-ttu-id="1c2fd-234">列表 4 中的测试验证调用 create （） 方法，通过新组将组添加到组 index （） 方法返回的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-234">The test in Listing 4 verifies that calling the Create() method with a new Group adds the Group to the list of Groups returned by the Index() method.</span></span> <span data-ttu-id="1c2fd-235">换而言之，如果我创建一个新组然后我应该能够收到新的组的 index （） 方法返回的组的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-235">In other words, if I create a new group then I should be able to get the new Group back from the list of Groups returned by the Index() method.</span></span>

<span data-ttu-id="1c2fd-236">**列表 4-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-236">**Listing 4 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

<span data-ttu-id="1c2fd-237">列表 4 中的测试会调用组控制器与新联系人组 create （） 方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-237">The test in Listing 4 calls the Group controller Create() method with a new contact Group.</span></span> <span data-ttu-id="1c2fd-238">接下来，测试将验证，调用组控制器 index （） 方法返回新的组中查看数据。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-238">Next, the test verifies that calling the Group controller Index() method returns the new Group in view data.</span></span>

<span data-ttu-id="1c2fd-239">列表 5 中已修改的组控制器包含的更改通过新的测试所需的最低要求。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-239">The modified Group controller in Listing 5 contains the bare minimum of changes required to pass the new test.</span></span>

<span data-ttu-id="1c2fd-240">**列表 5-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-240">**Listing 5 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a><span data-ttu-id="1c2fd-241">列表 5 中的组控制器具有一个新的 create （） 操作。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-241">The Group controller in Listing 5 has a new Create() action.</span></span> <span data-ttu-id="1c2fd-242">此操作将一组添加到组的集合。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-242">This action adds a Group to a collection of Groups.</span></span> <span data-ttu-id="1c2fd-243">请注意，index （） 操作已被修改以返回组的集合的内容。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-243">Notice that the Index() action has been modified to return the contents of the collection of Groups.</span></span>

<span data-ttu-id="1c2fd-244">再次重申，我们已执行利用最少量的通过单元测试所需的工作。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-244">Once again, we have performed the bare minimum amount of work required to pass the unit test.</span></span> <span data-ttu-id="1c2fd-245">我们对组控制器进行这些更改后，我们单位的所有测试都通过。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-245">After we make these changes to the Group controller, all of our unit tests pass.</span></span>

## <a name="adding-validation"></a><span data-ttu-id="1c2fd-246">添加验证</span><span class="sxs-lookup"><span data-stu-id="1c2fd-246">Adding Validation</span></span>

<span data-ttu-id="1c2fd-247">显式用户情景中，未规定此要求。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-247">This requirement was not stated explicitly in the user story.</span></span> <span data-ttu-id="1c2fd-248">但是，有理由需要一个组具有一个名称。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-248">However, it is reasonable to require that a Group have a name.</span></span> <span data-ttu-id="1c2fd-249">否则，将联系人组织到组将不会非常有用。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-249">Otherwise, organizing contacts into Groups would not be very useful.</span></span>

<span data-ttu-id="1c2fd-250">代码清单 6 包含新的测试表明此目的。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-250">Listing 6 contains a new test that expresses this intention.</span></span> <span data-ttu-id="1c2fd-251">此测试验证尝试无需提供在模型状态中的验证错误消息中的名称结果中创建组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-251">This test verifies that attempting to create a Group without supplying a name results in a validation error message in model state.</span></span>

<span data-ttu-id="1c2fd-252">**代码清单 6-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-252">**Listing 6 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

<span data-ttu-id="1c2fd-253">为了满足此测试，我们需要添加到组类 （请参阅列表 7） 的 Name 属性。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-253">In order to satisfy this test, we need to add a Name property to our Group class (see Listing 7).</span></span> <span data-ttu-id="1c2fd-254">此外，我们需要将小小的验证逻辑添加到组控制器 s create （） 操作 （请参阅代码清单 8）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-254">Furthermore, we need to add a tiny bit of validation logic to our Group controller s Create() action (see Listing 8).</span></span>

<span data-ttu-id="1c2fd-255">**列表 7-Models\Group.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-255">**Listing 7 - Models\Group.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

<span data-ttu-id="1c2fd-256">**代码清单 8-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-256">**Listing 8 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

<span data-ttu-id="1c2fd-257">请注意组控制器 create （） 操作现在包含验证和数据库的逻辑。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-257">Notice that the Group controller Create() action now contains both validation and database logic.</span></span> <span data-ttu-id="1c2fd-258">当前，组控制器使用的数据库所包含的没有什么比内存中集合。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-258">Currently, the database used by the Group controller consists of nothing more than an in-memory collection.</span></span>

## <a name="time-to-refactor"></a><span data-ttu-id="1c2fd-259">重构的时间</span><span class="sxs-lookup"><span data-stu-id="1c2fd-259">Time to Refactor</span></span>

<span data-ttu-id="1c2fd-260">红/绿/重构的第三步是重构部分。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-260">The third step in Red/Green/Refactor is the Refactor part.</span></span> <span data-ttu-id="1c2fd-261">此时，我们需要我们的代码中，并考虑如何，我们可以重构应用程序以提高它的设计。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-261">At this point, we need to step back from our code and consider how we can refactor our application to improve its design.</span></span> <span data-ttu-id="1c2fd-262">重构阶段是的我们认真考虑的最佳方法的实现软件设计原则和模式的阶段。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-262">The Refactor stage is the stage at which we think hard about the best way of implementing software design principles and patterns.</span></span>

<span data-ttu-id="1c2fd-263">我们可以随意修改我们的代码以任何方式，我们选择以提高代码的设计。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-263">We are free to modify our code in any way that we choose to improve the design of the code.</span></span> <span data-ttu-id="1c2fd-264">我们有单元测试，使我们无法破坏现有功能的安全网。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-264">We have a safety net of unit tests that prevent us from breaking existing functionality.</span></span>

<span data-ttu-id="1c2fd-265">现在，我们组控制器是从优秀的软件设计的角度来看乱。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-265">Right now, our Group controller is a mess from the perspective of good software design.</span></span> <span data-ttu-id="1c2fd-266">组控制器包含纷繁混乱现象验证和数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-266">The Group controller contains a tangled mess of validation and data access code.</span></span> <span data-ttu-id="1c2fd-267">为了避免违反单一责任原则，我们需要将这些问题分离到不同的类。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-267">To avoid violating the Single Responsibility Principle, we need to separate these concerns into different classes.</span></span>

<span data-ttu-id="1c2fd-268">我们重构的组控制器类都包含在程序列表 9。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-268">Our refactored Group controller class is contained in Listing 9.</span></span> <span data-ttu-id="1c2fd-269">控制器已被修改为使用 ContactManager 服务层。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-269">The controller has been modified to use the ContactManager service layer.</span></span> <span data-ttu-id="1c2fd-270">这是我们向联系人控制器使用的相同服务层。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-270">This is the same service layer that we use with the Contact controller.</span></span>

<span data-ttu-id="1c2fd-271">代码清单 10 包含添加到 ContactManager 服务层以支持验证、 列出和创建组的新方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-271">Listing 10 contains the new methods added to the ContactManager service layer to support validating, listing, and creating groups.</span></span> <span data-ttu-id="1c2fd-272">IContactManagerService 界面已更新为包括新的方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-272">The IContactManagerService interface was updated to include the new methods.</span></span>

<span data-ttu-id="1c2fd-273">代码清单 11 包含实现 IContactManagerRepository 接口的新 FakeContactManagerRepository 类。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-273">Listing 11 contains a new FakeContactManagerRepository class that implements the IContactManagerRepository interface.</span></span> <span data-ttu-id="1c2fd-274">与 EntityContactManagerRepository 类还实现 IContactManagerRepository 接口，不同新 FakeContactManagerRepository 类不与数据库通信。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-274">Unlike the EntityContactManagerRepository class that also implements the IContactManagerRepository interface, our new FakeContactManagerRepository class does not communicate with the database.</span></span> <span data-ttu-id="1c2fd-275">FakeContactManagerRepository 类使用的内存中集合的代理的数据库。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-275">The FakeContactManagerRepository class uses an in-memory collection as a proxy for the database.</span></span> <span data-ttu-id="1c2fd-276">我们将在我们的单元测试中使用此类，作为一个虚设储存库层。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-276">We'll use this class in our unit tests as a fake repository layer.</span></span>

<span data-ttu-id="1c2fd-277">**列表 9-Controllers\GroupController.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-277">**Listing 9 - Controllers\GroupController.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

<span data-ttu-id="1c2fd-278">**代码清单 10-Controllers\ContactManagerService.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-278">**Listing 10 - Controllers\ContactManagerService.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

<span data-ttu-id="1c2fd-279">**代码清单 11-Controllers\FakeContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-279">**Listing 11 - Controllers\FakeContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

<span data-ttu-id="1c2fd-280">修改接口需要的 IContactManagerRepository 使用 EntityContactManagerRepository 类中实现的 CreateGroup() 和 ListGroups() 方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-280">Modifying the IContactManagerRepository interface requires use to implement the CreateGroup() and ListGroups() methods in the EntityContactManagerRepository class.</span></span> <span data-ttu-id="1c2fd-281">执行此操作的 laziest 和最快方法是添加存根 （stub） 的方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-281">The laziest and fastest way to do this is to add stub methods that look like this:</span></span>   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]


<span data-ttu-id="1c2fd-282">最后，我们的应用程序设计这些更改需要我们对我们的单元测试中进行一些修改。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-282">Finally, these changes to the design of our application require us to make some modifications to our unit tests.</span></span> <span data-ttu-id="1c2fd-283">我们现在需要执行单元测试时使用 FakeContactManagerRepository。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-283">We now need to use the FakeContactManagerRepository when performing the unit tests.</span></span> <span data-ttu-id="1c2fd-284">更新后的 GroupControllerTest 类都包含在列表 12。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-284">The updated GroupControllerTest class is contained in Listing 12.</span></span>

<span data-ttu-id="1c2fd-285">**列表 12-Controllers\GroupControllerTest.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-285">**Listing 12 - Controllers\GroupControllerTest.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

<span data-ttu-id="1c2fd-286">建立所有这些后，再次重申，所有更改的我们通过单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-286">After we make all of these changes, once again, all of our unit tests pass.</span></span> <span data-ttu-id="1c2fd-287">我们已经完成红/绿/重构整个周期。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-287">We have completed the entire cycle of Red/Green/Refactor.</span></span> <span data-ttu-id="1c2fd-288">我们已实现的第一个的两个用户情景。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-288">We have implemented the first two user stories.</span></span> <span data-ttu-id="1c2fd-289">现在，我们具有支持单元测试的用户情景以表示的要求。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-289">We now have supporting unit tests for the requirements expressed in the user stories.</span></span> <span data-ttu-id="1c2fd-290">实现用户情景的剩余部分包括重复红/绿/重构的同一个周期。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-290">Implementing the remainder of the user stories involves repeating the same cycle of Red/Green/Refactor.</span></span>

## <a name="modifying-our-database"></a><span data-ttu-id="1c2fd-291">修改我们的数据库</span><span class="sxs-lookup"><span data-stu-id="1c2fd-291">Modifying our Database</span></span>

<span data-ttu-id="1c2fd-292">遗憾的是，尽管我们已经满足所有要求通过我们的单元测试来表示，我们的工作不会进行。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-292">Unfortunately, even though we have satisfied all of the requirements expressed by our unit tests, our work is not done.</span></span> <span data-ttu-id="1c2fd-293">我们仍需要修改我们的数据库。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-293">We still need to modify our database.</span></span>

<span data-ttu-id="1c2fd-294">我们需要创建一个新的组数据库表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-294">We need to create a new Group database table.</span></span> <span data-ttu-id="1c2fd-295">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-295">Follow these steps:</span></span>

1. <span data-ttu-id="1c2fd-296">在服务器资源管理器窗口中，右键单击表文件夹，然后选择菜单选项**添加新表**。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-296">In the Server Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span>
2. <span data-ttu-id="1c2fd-297">输入在表设计器中，如下所述的两个列。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-297">Enter the two columns described below in the Table Designer.</span></span>
3. <span data-ttu-id="1c2fd-298">将标记 Id 列作为主键和标识列。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-298">Mark the Id column as a primary key and Identity column.</span></span>
4. <span data-ttu-id="1c2fd-299">通过单击的软盘图标与命名组保存的新表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-299">Save the new table with the name Groups by clicking the icon of the floppy.</span></span>

<a id="0.11_table01"></a>


| <span data-ttu-id="1c2fd-300">**列名称**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-300">**Column Name**</span></span> | <span data-ttu-id="1c2fd-301">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-301">**Data Type**</span></span> | <span data-ttu-id="1c2fd-302">**允许 null 值**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-302">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1c2fd-303">Id</span><span class="sxs-lookup"><span data-stu-id="1c2fd-303">Id</span></span> | <span data-ttu-id="1c2fd-304">int</span><span class="sxs-lookup"><span data-stu-id="1c2fd-304">int</span></span> | <span data-ttu-id="1c2fd-305">False</span><span class="sxs-lookup"><span data-stu-id="1c2fd-305">False</span></span> |
| <span data-ttu-id="1c2fd-306">name</span><span class="sxs-lookup"><span data-stu-id="1c2fd-306">Name</span></span> | <span data-ttu-id="1c2fd-307">nvarchar （50)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-307">nvarchar(50)</span></span> | <span data-ttu-id="1c2fd-308">False</span><span class="sxs-lookup"><span data-stu-id="1c2fd-308">False</span></span> |


<span data-ttu-id="1c2fd-309">接下来，我们需要从联系人表中删除的所有数据 (否则，我们获得了能够创建联系人和组表之间的关系)。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-309">Next, we need to delete all of the data from the Contacts table (otherwise, we won t be able to create a relationship between the Contacts and Groups tables).</span></span> <span data-ttu-id="1c2fd-310">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-310">Follow these steps:</span></span>

1. <span data-ttu-id="1c2fd-311">右键单击联系人表，然后选择菜单选项**显示表数据**。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-311">Right-click the Contacts table and select the menu option **Show Table Data**.</span></span>
2. <span data-ttu-id="1c2fd-312">删除的所有行。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-312">Delete all of the rows.</span></span>

<span data-ttu-id="1c2fd-313">接下来，我们需要定义组数据库表和现有的联系人数据库表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-313">Next, we need to define a relationship between the Groups database table and the existing Contacts database table.</span></span> <span data-ttu-id="1c2fd-314">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-314">Follow these steps:</span></span>

1. <span data-ttu-id="1c2fd-315">双击服务器资源管理器窗口打开表设计器中的联系人表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-315">Double-click the Contacts table in the Server Explorer window to open the Table Designer.</span></span>
2. <span data-ttu-id="1c2fd-316">将新的整数列添加到名为 GroupId 联系人表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-316">Add a new integer column to the Contacts table named GroupId.</span></span>
3. <span data-ttu-id="1c2fd-317">单击关系按钮以打开外键关系对话框 （参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-317">Click the Relationship button to open the Foreign Key Relationships dialog (see Figure 3).</span></span>
4. <span data-ttu-id="1c2fd-318">单击添加按钮。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-318">Click the Add button.</span></span>
5. <span data-ttu-id="1c2fd-319">单击显示表和列规范按钮旁边的省略号按钮。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-319">Click the ellipsis button that appears next to the Table and Columns Specification button.</span></span>
6. <span data-ttu-id="1c2fd-320">在表和列对话框中，选择作为主键表和作为主键列的 Id 的组。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-320">In the Tables and Columns dialog, select Groups as the primary key table and Id as the primary key column.</span></span> <span data-ttu-id="1c2fd-321">选择联系人作为外键表和外键列作为 GroupId （请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-321">Select Contacts as the foreign key table and GroupId as the foreign key column (see Figure 4).</span></span> <span data-ttu-id="1c2fd-322">单击确定按钮。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-322">Click the OK button.</span></span>
7. <span data-ttu-id="1c2fd-323">下**INSERT 和 UPDATE 规范**，选择的值**Cascade**有关**删除规则**。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-323">Under **INSERT and UPDATE Specification**, select the value **Cascade** for **Delete Rule**.</span></span>
8. <span data-ttu-id="1c2fd-324">单击关闭按钮以关闭外键关系对话框。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-324">Click the Close button to close the Foreign Key Relationships dialog.</span></span>
9. <span data-ttu-id="1c2fd-325">单击保存按钮以将所做的更改保存到 Contacts 表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-325">Click the Save button to save the changes to the Contacts table.</span></span>


<span data-ttu-id="1c2fd-326">[![创建数据库表关系](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-326">[![Creating a database table relationship](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)</span></span>

<span data-ttu-id="1c2fd-327">**图 03**： 创建数据库表关系 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-327">**Figure 03**: Creating a database table relationship ([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image6.png))</span></span>


<span data-ttu-id="1c2fd-328">[![指定表关系](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-328">[![Specifying table relationships](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)</span></span>

<span data-ttu-id="1c2fd-329">**图 04**： 指定表关系 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-329">**Figure 04**: Specifying table relationships([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image8.png))</span></span>


### <a name="updating-our-data-model"></a><span data-ttu-id="1c2fd-330">更新数据模型</span><span class="sxs-lookup"><span data-stu-id="1c2fd-330">Updating our Data Model</span></span>

<span data-ttu-id="1c2fd-331">接下来，我们需要更新数据模型以表示新的数据库表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-331">Next, we need to update our data model to represent the new database table.</span></span> <span data-ttu-id="1c2fd-332">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-332">Follow these steps:</span></span>

1. <span data-ttu-id="1c2fd-333">双击 ContactManagerModel.edmx 文件在 Models 文件夹中打开实体设计器。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-333">Double-click the ContactManagerModel.edmx file in the Models folder to open the Entity Designer.</span></span>
2. <span data-ttu-id="1c2fd-334">右键单击设计器图面，然后选择菜单选项**从数据库更新模型**。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-334">Right-click the Designer surface and select the menu option **Update Model from Database**.</span></span>
3. <span data-ttu-id="1c2fd-335">在更新向导中，选择组表，然后单击完成按钮 （请参见图 5）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-335">In the Update Wizard, select the Groups table and click the Finish button (see Figure 5).</span></span>
4. <span data-ttu-id="1c2fd-336">右键单击组实体，然后选择菜单选项**重命名**。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-336">Right-click the Groups entity and select the menu option **Rename**.</span></span> <span data-ttu-id="1c2fd-337">更改的名称*组*实体与*组*（单数）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-337">Change the name of the *Groups* entity to *Group* (singular).</span></span>
5. <span data-ttu-id="1c2fd-338">右键单击联系人实体的底部将显示的组导航属性。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-338">Right-click the Groups navigation property that appears at the bottom of the Contact entity.</span></span> <span data-ttu-id="1c2fd-339">更改的名称*组*导航属性设置为*组*（单数）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-339">Change the name of the *Groups* navigation property to *Group* (singular).</span></span>


<span data-ttu-id="1c2fd-340">[![更新数据库中的实体框架模型](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-340">[![Updating an Entity Framework model from the database](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)</span></span>

<span data-ttu-id="1c2fd-341">**图 05**： 更新数据库中的实体框架模型 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-341">**Figure 05**: Updating an Entity Framework model from the database([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image10.png))</span></span>


<span data-ttu-id="1c2fd-342">完成这些步骤后，你的数据模型将表示的联系人和组的表。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-342">After you complete these steps, your data model will represent both the Contacts and Groups tables.</span></span> <span data-ttu-id="1c2fd-343">在实体设计器应显示这两个实体 （请参阅图 6）。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-343">The Entity Designer should show both entities (see Figure 6).</span></span>


<span data-ttu-id="1c2fd-344">[![实体设计器显示组和联系人](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-344">[![Entity Designer displaying Group and Contact](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)</span></span>

<span data-ttu-id="1c2fd-345">**图 06**： 显示组和联系人实体设计器 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-345">**Figure 06**: Entity Designer displaying Group and Contact([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image12.png))</span></span>


### <a name="creating-our-repository-classes"></a><span data-ttu-id="1c2fd-346">创建存储库类</span><span class="sxs-lookup"><span data-stu-id="1c2fd-346">Creating our Repository Classes</span></span>

<span data-ttu-id="1c2fd-347">接下来，我们需要实现我们的存储库类。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-347">Next, we need to implement our repository class.</span></span> <span data-ttu-id="1c2fd-348">此迭代的过程中，我们添加了几个新方法到 IContactManagerRepository 接口编写代码以满足我们的单元测试时。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-348">Over the course of this iteration, we added several new methods to the IContactManagerRepository interface while writing code to satisfy our unit tests.</span></span> <span data-ttu-id="1c2fd-349">IContactManagerRepository 接口的最终版本包含在列表 14。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-349">The final version of the IContactManagerRepository interface is contained in Listing 14.</span></span>

<span data-ttu-id="1c2fd-350">**代码清单 14-Models\IContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-350">**Listing 14 - Models\IContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

<span data-ttu-id="1c2fd-351">我们还没有真正实现任何与使用联系人组相关的方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-351">We haven t actually implemented any of the methods related to working with contact groups.</span></span> <span data-ttu-id="1c2fd-352">目前，EntityContactManagerRepository 类 IContactManagerRepository 界面中列出的联系人组方法的每个具有存根 （stub） 方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-352">Currently, the EntityContactManagerRepository class has stub methods for each of the contact group methods listed in the IContactManagerRepository interface.</span></span> <span data-ttu-id="1c2fd-353">例如，ListGroups() 方法当前如下所示：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-353">For example, the ListGroups() method currently looks like this:</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

<span data-ttu-id="1c2fd-354">存根 （stub） 方法使我们能够编译我们的应用程序并通过单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-354">The stub methods enabled us to compile our application and pass the unit tests.</span></span> <span data-ttu-id="1c2fd-355">但是，现在就来实施这些方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-355">However, now it is time to actually implement these methods.</span></span> <span data-ttu-id="1c2fd-356">EntityContactManagerRepository 类的最终版本包含在列表 13。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-356">The final version of the EntityContactManagerRepository class is contained in Listing 13.</span></span>

<span data-ttu-id="1c2fd-357">**代码清单 13-Models\EntityContactManagerRepository.cs**</span><span class="sxs-lookup"><span data-stu-id="1c2fd-357">**Listing 13 - Models\EntityContactManagerRepository.cs**</span></span>

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a><span data-ttu-id="1c2fd-358">创建视图</span><span class="sxs-lookup"><span data-stu-id="1c2fd-358">Creating the Views</span></span>

<span data-ttu-id="1c2fd-359">ASP.NET MVC 应用程序时使用的默认 ASP.NET 视图引擎。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-359">ASP.NET MVC application when you use the default ASP.NET view engine.</span></span> <span data-ttu-id="1c2fd-360">因此，don t 创建视图以响应特定的单元测试。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-360">So, you don t create views in response to a particular unit test.</span></span> <span data-ttu-id="1c2fd-361">但是，因为应用程序都是毫无用处，除非视图，我们可以 t 完成此迭代而无需创建和修改联系人管理器应用程序中包含的视图。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-361">However, because an application would be useless without views, we can t complete this iteration without creating and modifying the views contained in the Contact Manager application.</span></span>

<span data-ttu-id="1c2fd-362">我们需要创建以下新视图，用于管理联系人组 （请参阅图 7）：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-362">We need to create the following new views for managing contact groups (see Figure 7):</span></span>

- <span data-ttu-id="1c2fd-363">Views\Group\Index.aspx-联系人组的显示列表</span><span class="sxs-lookup"><span data-stu-id="1c2fd-363">Views\Group\Index.aspx - Displays list of contact groups</span></span>
- <span data-ttu-id="1c2fd-364">Views\Group\Delete.aspx-用于删除联系人组显示确认窗体</span><span class="sxs-lookup"><span data-stu-id="1c2fd-364">Views\Group\Delete.aspx - Displays confirmation form for deleting a contact group</span></span>


<span data-ttu-id="1c2fd-365">[![组索引视图](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-365">[![The Group Index view](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)</span></span>

<span data-ttu-id="1c2fd-366">**图 07**: 组索引视图 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-366">**Figure 07**: The Group Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image14.png))</span></span>


<span data-ttu-id="1c2fd-367">我们需要修改以下现有视图，使其包含联系人组：</span><span class="sxs-lookup"><span data-stu-id="1c2fd-367">We need to modify the following existing views so that they include contact groups:</span></span>

- <span data-ttu-id="1c2fd-368">Views\Home\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="1c2fd-368">Views\Home\Create.aspx</span></span>
- <span data-ttu-id="1c2fd-369">Views\Home\Edit.aspx</span><span class="sxs-lookup"><span data-stu-id="1c2fd-369">Views\Home\Edit.aspx</span></span>
- <span data-ttu-id="1c2fd-370">Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="1c2fd-370">Views\Home\Index.aspx</span></span>

<span data-ttu-id="1c2fd-371">通过查看此教程中随附的 Visual Studio 应用程序，可以看到修改后的视图。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-371">You can see the modified views by looking at the Visual Studio application that accompanies this tutorial.</span></span> <span data-ttu-id="1c2fd-372">例如，图 8 显示了联系人索引视图。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-372">For example, Figure 8 illustrates the Contact Index view.</span></span>


<span data-ttu-id="1c2fd-373">[![请联系索引视图](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-373">[![The Contact Index view](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)</span></span>

<span data-ttu-id="1c2fd-374">**图 08**: 请联系索引视图 ([单击以查看实际尺寸的图像](iteration-6-use-test-driven-development-cs/_static/image16.png))</span><span class="sxs-lookup"><span data-stu-id="1c2fd-374">**Figure 08**: The Contact Index view([Click to view full-size image](iteration-6-use-test-driven-development-cs/_static/image16.png))</span></span>


## <a name="summary"></a><span data-ttu-id="1c2fd-375">总结</span><span class="sxs-lookup"><span data-stu-id="1c2fd-375">Summary</span></span>

<span data-ttu-id="1c2fd-376">在此迭代中，我们添加新功能到我们的联系人管理器应用程序按照测试驱动开发应用程序设计方法。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-376">In this iteration, we added new functionality to our Contact Manager application by following a test-driven development application design methodology.</span></span> <span data-ttu-id="1c2fd-377">我们首先创建了一组用户情景。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-377">We started by creating a set of user stories.</span></span> <span data-ttu-id="1c2fd-378">我们创建了一组单元测试用户情景所表达的要求相对应。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-378">We created a set of unit tests that corresponds to the requirements expressed by the user stories.</span></span> <span data-ttu-id="1c2fd-379">最后，我们编写了刚好足够的代码以满足表示的单元测试的要求。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-379">Finally, we wrote just enough code to satisfy the requirements expressed by the unit tests.</span></span>

<span data-ttu-id="1c2fd-380">我们完成编写足够的代码以满足表示的单元测试的要求后，我们将更新我们的数据库和视图。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-380">After we finished writing enough code to satisfy the requirements expressed by the unit tests, we updated our database and views.</span></span> <span data-ttu-id="1c2fd-381">我们对我们的数据库添加新组表，并更新我们实体框架数据模型。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-381">We added a new Groups table to our database and updated our Entity Framework Data Model.</span></span> <span data-ttu-id="1c2fd-382">我们还创建和修改的一组视图。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-382">We also created and modified a set of views.</span></span>

<span data-ttu-id="1c2fd-383">在下一次迭代-最后一个迭代-我们重写应用程序以充分利用 Ajax。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-383">In the next iteration -- the final iteration -- we rewrite our application to take advantage of Ajax.</span></span> <span data-ttu-id="1c2fd-384">通过利用 Ajax，我们将提高响应能力和联系人管理器应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="1c2fd-384">By taking advantage of Ajax, we'll improve the responsiveness and performance of the Contact Manager application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1c2fd-385">[上一页](iteration-5-create-unit-tests-cs.md)
> [下一页](iteration-7-add-ajax-functionality-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1c2fd-385">[Previous](iteration-5-create-unit-tests-cs.md)
[Next](iteration-7-add-ajax-functionality-cs.md)</span></span>
