---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 依赖关系注入 |Microsoft Docs
author: rick-anderson
description: 注意： 此动手实验假定你具有的 ASP.NET MVC 和 ASP.NET MVC 4 的筛选器的基本知识。 如果您没有使用 ASP.NET MVC 4 筛选器之前，我们建议...
ms.author: aspnetcontent
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 44c8f2055fb62d589e874683cbf43eed87a8c447
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37812335"
---
# <a name="aspnet-mvc-4-dependency-injection"></a><span data-ttu-id="4c2d1-104">ASP.NET MVC 4 依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="4c2d1-104">ASP.NET MVC 4 Dependency Injection</span></span>

<span data-ttu-id="4c2d1-105">通过[Web 训练营团队](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="4c2d1-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="4c2d1-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="4c2d1-107">此动手实验假定你已了解的基础知识**ASP.NET MVC**并**ASP.NET MVC 4 筛选**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC** and **ASP.NET MVC 4 filters**.</span></span> <span data-ttu-id="4c2d1-108">如果您未使用过**ASP.NET MVC 4 筛选**之前，我们建议你超出**ASP.NET MVC 自定义操作筛选器**动手实验。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-108">If you have not used **ASP.NET MVC 4 filters** before, we recommend you to go over **ASP.NET MVC Custom Action Filters** Hands-on Lab.</span></span>

> [!NOTE]
> <span data-ttu-id="4c2d1-109">在 Web 训练营培训工具包中，在可从包含所有示例代码和代码段[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-109">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="4c2d1-110">特定于此实验室项目位于[ASP.NET MVC 4 依赖关系注入](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-110">The project specific to this lab is available at [ASP.NET MVC 4 Dependency Injection](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).</span></span>

<span data-ttu-id="4c2d1-111">在中**面向对象的编程**范例，对象协同工作的协作模型有 contributors （参与者） 和使用者。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-111">In **Object Oriented Programming** paradigm, objects work together in a collaboration model where there are contributors and consumers.</span></span> <span data-ttu-id="4c2d1-112">正常情况下，此通信模型生成对象和组件，变得难以管理复杂性的不断提高时之间的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-112">Naturally, this communication model generates dependencies between objects and components, becoming difficult to manage when complexity increases.</span></span>

<span data-ttu-id="4c2d1-113">![类的依赖项和模型的复杂性](aspnet-mvc-4-dependency-injection/_static/image1.png "类依赖项和模型的复杂性")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-113">![Class dependencies and model complexity](aspnet-mvc-4-dependency-injection/_static/image1.png "Class dependencies and model complexity")</span></span>

<span data-ttu-id="4c2d1-114">*类依赖项和模型的复杂性*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-114">*Class dependencies and model complexity*</span></span>

<span data-ttu-id="4c2d1-115">可能听说**工厂模式**和之间的接口和使用服务，这些客户端对象位于通常负责服务位置的实现分离。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-115">You have probably heard about the **Factory Pattern** and the separation between the interface and the implementation using services, where the client objects are often responsible for service location.</span></span>

<span data-ttu-id="4c2d1-116">依赖关系注入模式是控制反转的特定实现。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-116">The Dependency Injection pattern is a particular implementation of Inversion of Control.</span></span> <span data-ttu-id="4c2d1-117">**控制反转 (IoC)** 意味着对象不会创建它们依赖来完成其工作的其他对象。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-117">**Inversion of Control (IoC)** means that objects do not create other objects on which they rely to do their work.</span></span> <span data-ttu-id="4c2d1-118">相反，他们获得所需从外部源 （例如，xml 配置文件） 的对象。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-118">Instead, they get the objects that they need from an outside source (for example, an xml configuration file).</span></span>

<span data-ttu-id="4c2d1-119">**依赖关系注入 (DI)** 意味着这是通过对象干预，通常将构造函数参数传递的 framework 组件并设置属性。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-119">**Dependency Injection (DI)** means that this is done without the object intervention, usually by a framework component that passes constructor parameters and set properties.</span></span>

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a><span data-ttu-id="4c2d1-120">依赖关系注入 (DI) 设计模式</span><span class="sxs-lookup"><span data-stu-id="4c2d1-120">The Dependency Injection (DI) Design Pattern</span></span>

<span data-ttu-id="4c2d1-121">在高级别中，依赖关系注入的目标是，客户端类 (例如*选手*) 需要满足接口的某些内容 (例如*IClub*)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-121">At a high level, the goal of Dependency Injection is that a client class (e.g. *the golfer*) needs something that satisfies an interface (e.g. *IClub*).</span></span> <span data-ttu-id="4c2d1-122">它并不关心的具体类型是什么 (例如*WoodClub，IronClub，WedgeClub*或*PutterClub*)，它需要处理的其他人 (例如的合理*托盘*)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-122">It doesn't care what the concrete type is (e.g. *WoodClub, IronClub, WedgeClub* or *PutterClub*), it wants someone else to handle that (e.g. a good *caddy*).</span></span> <span data-ttu-id="4c2d1-123">ASP.NET MVC 中的依赖关系解析程序可以让你能够注册到其他位置您依赖关系的逻辑 (例如容器或*俱乐部包*)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-123">The Dependency Resolver in ASP.NET MVC can allow you to register your dependency logic somewhere else (e.g. a container or a *bag of clubs*).</span></span>

<span data-ttu-id="4c2d1-124">![依赖关系注入关系图](aspnet-mvc-4-dependency-injection/_static/image2.png "依赖关系注入图")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-124">![Dependency Injection diagram](aspnet-mvc-4-dependency-injection/_static/image2.png "Dependency Injection illustration")</span></span>

<span data-ttu-id="4c2d1-125">*依赖关系注入-高尔夫类比*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-125">*Dependency Injection - Golf analogy*</span></span>

<span data-ttu-id="4c2d1-126">使用依赖关系注入模式和控制反转的优势如下所示：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-126">The advantages of using Dependency Injection pattern and Inversion of Control are the following:</span></span>

- <span data-ttu-id="4c2d1-127">减少了类耦合度</span><span class="sxs-lookup"><span data-stu-id="4c2d1-127">Reduces class coupling</span></span>
- <span data-ttu-id="4c2d1-128">提高代码重用</span><span class="sxs-lookup"><span data-stu-id="4c2d1-128">Increases code reusing</span></span>
- <span data-ttu-id="4c2d1-129">改进了代码可维护性</span><span class="sxs-lookup"><span data-stu-id="4c2d1-129">Improves code maintainability</span></span>
- <span data-ttu-id="4c2d1-130">改进了应用程序测试</span><span class="sxs-lookup"><span data-stu-id="4c2d1-130">Improves application testing</span></span>

> [!NOTE]
> <span data-ttu-id="4c2d1-131">依赖关系注入有时与抽象工厂设计模式，但这两种方法之间的细微差异。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-131">Dependency Injection is sometimes compared with Abstract Factory Design Pattern, but there is a slight difference between both approaches.</span></span> <span data-ttu-id="4c2d1-132">DI 具有背后努力解决依赖项通过调用工厂和注册的服务的框架。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-132">DI has a Framework working behind to solve dependencies by calling the factories and the registered services.</span></span>


<span data-ttu-id="4c2d1-133">现在，你已了解依赖关系注入模式，您将学习在此实验室中如何将其应用在 ASP.NET MVC 4 中。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-133">Now that you understand the Dependency Injection Pattern, you will learn throughout this lab how to apply it in ASP.NET MVC 4.</span></span> <span data-ttu-id="4c2d1-134">首先，将使用中的依赖关系注入**控制器**包含数据库访问服务。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-134">You will start using Dependency Injection in the **Controllers** to include a database access service.</span></span> <span data-ttu-id="4c2d1-135">接下来，将应用到的依赖关系注入**视图**若要使用的服务，并显示信息。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-135">Next, you will apply Dependency Injection to the **Views** to consume a service and show information.</span></span> <span data-ttu-id="4c2d1-136">最后，您将为 ASP.NET MVC 4 筛选器，将注入解决方案中的自定义操作筛选器扩展 DI。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-136">Finally, you will extend the DI to ASP.NET MVC 4 Filters, injecting a custom action filter in the solution.</span></span>

<span data-ttu-id="4c2d1-137">在本动手实验中，你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-137">In this Hands-on Lab, you will learn how to:</span></span>

- <span data-ttu-id="4c2d1-138">将 ASP.NET MVC 4 与 Unity 集成实现使用 NuGet 包的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="4c2d1-138">Integrate ASP.NET MVC 4 with Unity for Dependency Injection using NuGet Packages</span></span>
- <span data-ttu-id="4c2d1-139">使用依赖关系注入在 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-139">Use Dependency Injection inside an ASP.NET MVC Controller</span></span>
- <span data-ttu-id="4c2d1-140">使用依赖关系注入在 ASP.NET MVC 视图</span><span class="sxs-lookup"><span data-stu-id="4c2d1-140">Use Dependency Injection inside an ASP.NET MVC View</span></span>
- <span data-ttu-id="4c2d1-141">使用依赖关系注入在 ASP.NET MVC 操作筛选器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-141">Use Dependency Injection inside an ASP.NET MVC Action Filter</span></span>

> [!NOTE]
> <span data-ttu-id="4c2d1-142">此实验室使用 Unity.Mvc3 NuGet 包依赖关系解析，但可以调整为使用 ASP.NET MVC 4 的任何依赖关系注入框架。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-142">This Lab is using Unity.Mvc3 NuGet Package for dependency resolution, but it is possible to adapt any Dependency Injection Framework to work with ASP.NET MVC 4.</span></span>


<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="4c2d1-143">系统必备</span><span class="sxs-lookup"><span data-stu-id="4c2d1-143">Prerequisites</span></span>

<span data-ttu-id="4c2d1-144">必须具有要完成本实验的以下项：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-144">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="4c2d1-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web)或更高 (读取[附录 A](#AppendixA)有关如何安装它的说明)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-145">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="4c2d1-146">安装</span><span class="sxs-lookup"><span data-stu-id="4c2d1-146">Setup</span></span>

<span data-ttu-id="4c2d1-147">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="4c2d1-147">**Installing Code Snippets**</span></span>

<span data-ttu-id="4c2d1-148">为方便起见，您将沿此实验室管理大部分是代码的可用作 Visual Studio 代码段。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-148">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="4c2d1-149">若要安装运行的代码段 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-149">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="4c2d1-150">如果您不熟悉 Visual Studio 代码段，并想要了解如何使用它们，您可以从本文档引用的附录&quot;[附录 b： 使用代码片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-150">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

* * *

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="4c2d1-151">练习</span><span class="sxs-lookup"><span data-stu-id="4c2d1-151">Exercises</span></span>

<span data-ttu-id="4c2d1-152">此动手实验包含由以下练习：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-152">This Hands-On Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="4c2d1-153">练习 1： 将注入控制器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-153">Exercise 1: Injecting a Controller</span></span>](#Exercise1)
2. [<span data-ttu-id="4c2d1-154">练习 2： 将注入视图</span><span class="sxs-lookup"><span data-stu-id="4c2d1-154">Exercise 2: Injecting a View</span></span>](#Exercise2)
3. [<span data-ttu-id="4c2d1-155">练习 3： 将注入筛选器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-155">Exercise 3: Injecting Filters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="4c2d1-156">每个练习均附带**最终**包含生成应完成练习后获得的解决方案文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-156">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="4c2d1-157">如果需要更多帮助，学习了几项练习，您可以使用此解决方案作为指南。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-157">You can use this solution as a guide if you need additional help working through the exercises.</span></span>


<span data-ttu-id="4c2d1-158">估计的时间才能完成此实验： **30 分钟**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-158">Estimated time to complete this lab: **30 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a><span data-ttu-id="4c2d1-159">练习 1： 将注入控制器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-159">Exercise 1: Injecting a Controller</span></span>

<span data-ttu-id="4c2d1-160">在此练习中，您将学习如何在 ASP.NET MVC 控制器中使用依赖关系注入，通过集成 Unity 使用 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-160">In this exercise, you will learn how to use Dependency Injection in ASP.NET MVC Controllers by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="4c2d1-161">出于此原因，将单独从数据访问的逻辑将 MvcMusicStore 控制器到包括服务。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-161">For that reason, you will include services into your MvcMusicStore controllers to separate the logic from the data access.</span></span> <span data-ttu-id="4c2d1-162">服务将在控制器构造函数，它将使用依赖关系注入的帮助解决中创建新的依赖项**Unity**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-162">The services will create a new dependency in the controller constructor, which will be resolved using Dependency Injection with the help of **Unity**.</span></span>

<span data-ttu-id="4c2d1-163">此方法将演示如何生成不太耦合应用程序，即更灵活、 更易于维护和测试。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-163">This approach will show you how to generate less coupled applications, which are more flexible and easier to maintain and test.</span></span> <span data-ttu-id="4c2d1-164">您将学习如何将 ASP.NET MVC 与 Unity 集成。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-164">You will also learn how to integrate ASP.NET MVC with Unity.</span></span>

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a><span data-ttu-id="4c2d1-165">有关 StoreManager 服务</span><span class="sxs-lookup"><span data-stu-id="4c2d1-165">About StoreManager Service</span></span>

<span data-ttu-id="4c2d1-166">MVC Music 商店现在提供开始解决方案中包括用于管理名为的存储控制器数据的服务**StoreService**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-166">The MVC Music Store provided in the begin solution now includes a service that manages the Store Controller data named **StoreService**.</span></span> <span data-ttu-id="4c2d1-167">下面介绍了存储区服务实现。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-167">Below you will find the Store Service implementation.</span></span> <span data-ttu-id="4c2d1-168">请注意，所有方法都返回模型的实体。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-168">Note that all the methods return Model entities.</span></span>

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

<span data-ttu-id="4c2d1-169">**StoreController**从开始新的解决方案现在消耗**StoreService**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-169">**StoreController** from the begin solution now consumes **StoreService**.</span></span> <span data-ttu-id="4c2d1-170">所有数据引用已都删除从**StoreController**，并修改当前的数据访问接口，而无需更改使用的任何方法现在可以**StoreService**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-170">All the data references were removed from **StoreController**, and now possible to modify the current data access provider without changing any method that consumes **StoreService**.</span></span>

<span data-ttu-id="4c2d1-171">将在下面查找**StoreController**实现具有的依赖项**StoreService**在类构造函数。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-171">You will find below that the **StoreController** implementation has a dependency with **StoreService** inside the class constructor.</span></span>

> [!NOTE]
> <span data-ttu-id="4c2d1-172">在此练习中引入的依赖项与相关**控制反转**(IoC)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-172">The dependency introduced in this exercise is related to **Inversion of Control** (IoC).</span></span>
> 
> <span data-ttu-id="4c2d1-173">**StoreController**类构造函数接收**IStoreService**至关重要，可执行从在类中的服务调用的类型参数。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-173">The **StoreController** class constructor receives an **IStoreService** type parameter, which is essential to perform service calls from inside the class.</span></span> <span data-ttu-id="4c2d1-174">但是， **StoreController**未实现默认构造函数 （不带任何参数） 的任何控制器必须能够使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-174">However, **StoreController** does not implement the default constructor (with no parameters) that any controller must have to work with ASP.NET MVC.</span></span>
> 
> <span data-ttu-id="4c2d1-175">若要解决依赖关系，控制器必须创建的一个抽象工厂 （返回指定任何的类型对象的类）。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-175">To resolve the dependency, the controller has to be created by an abstract factory (a class that returns any object of the specified type).</span></span>


[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="4c2d1-176">此类尝试创建 StoreController 而无需发送服务对象，如声明没有无参数构造函数时，将出现错误。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-176">You will get an error when the class tries to create the StoreController without sending the service object, as there is no parameterless constructor declared.</span></span>


<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a><span data-ttu-id="4c2d1-177">任务 1-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="4c2d1-177">Task 1 - Running the Application</span></span>

<span data-ttu-id="4c2d1-178">在本任务中，将运行 Begin 应用程序，包括服务插入应用程序逻辑分离开来数据访问的存储控制器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-178">In this task, you will run the Begin application, which includes the service into the Store Controller that separates the data access from the application logic.</span></span>

<span data-ttu-id="4c2d1-179">运行程序时，你将收到一个异常，为控制器服务不默认情况下通过作为参数：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-179">When running the application, you will receive an exception, as the controller service is not passed as a parameter by default:</span></span>

1. <span data-ttu-id="4c2d1-180">打开**开始**解决方案位于**Source\Ex01 注入 Controller\Begin**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-180">Open the **Begin** solution located in **Source\Ex01-Injecting Controller\Begin**.</span></span>

   1. <span data-ttu-id="4c2d1-181">需要先下载某些缺少的 NuGet 包然后再继续。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-181">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4c2d1-182">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-182">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4c2d1-183">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-183">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4c2d1-184">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-184">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4c2d1-185">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-185">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4c2d1-186">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-186">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4c2d1-187">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-187">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="4c2d1-188">按**Ctrl + F5**不进行调试直接运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-188">Press **Ctrl + F5** to run the application without debugging.</span></span> <span data-ttu-id="4c2d1-189">你将收到错误消息&quot;**没有为此对象定义的无参数构造函数**&quot;:</span><span class="sxs-lookup"><span data-stu-id="4c2d1-189">You will get the error message &quot;**No parameterless constructor defined for this object**&quot;:</span></span>

    <span data-ttu-id="4c2d1-190">![运行 ASP.NET MVC 开始应用程序时出错](aspnet-mvc-4-dependency-injection/_static/image3.png "运行 ASP.NET MVC 开始应用程序时出错")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-190">![Error while running ASP.NET MVC Begin Application](aspnet-mvc-4-dependency-injection/_static/image3.png "Error while running ASP.NET MVC Begin Application")</span></span>

    <span data-ttu-id="4c2d1-191">*运行 ASP.NET MVC 开始应用程序时出错*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-191">*Error while running ASP.NET MVC Begin Application*</span></span>
3. <span data-ttu-id="4c2d1-192">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-192">Close the browser.</span></span>

<span data-ttu-id="4c2d1-193">以下步骤中你将适用于音乐应用商店解决方案将注入此控制器所需的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-193">In the following steps you will work on the Music Store Solution to inject the dependency this controller needs.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a><span data-ttu-id="4c2d1-194">任务 2-到 MvcMusicStore 解决方案包括 Unity</span><span class="sxs-lookup"><span data-stu-id="4c2d1-194">Task 2 - Including Unity into MvcMusicStore Solution</span></span>

<span data-ttu-id="4c2d1-195">在本任务中，将包括**Unity.Mvc3**到解决方案的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-195">In this task, you will include **Unity.Mvc3** NuGet Package to the solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4c2d1-196">Unity.Mvc3 包专为 ASP.NET MVC 3，但与 ASP.NET MVC 4 完全兼容。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-196">Unity.Mvc3 package was designed for ASP.NET MVC 3, but it is fully compatible with ASP.NET MVC 4.</span></span>
> 
> <span data-ttu-id="4c2d1-197">Unity 是轻量级的可扩展依赖关系注入容器并且还可以支持实例和类型拦截。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-197">Unity is a lightweight, extensible dependency injection container with optional support for instance and type interception.</span></span> <span data-ttu-id="4c2d1-198">它是在任何类型的.NET 应用程序中使用的通用容器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-198">It is a general-purpose container for use in any type of .NET application.</span></span> <span data-ttu-id="4c2d1-199">它提供了在依赖项注入机制包括中找到的所有常见功能： 创建对象，通过指定依赖项在运行时和大的灵活性，通过推迟到容器的组件配置要求的抽象。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-199">It provides all the common features found in dependency injection mechanisms including: object creation, abstraction of requirements by specifying dependencies at runtime and flexibility, by deferring the component configuration to the container.</span></span>


1. <span data-ttu-id="4c2d1-200">安装**Unity.Mvc3**中的 NuGet 包**MvcMusicStore**项目。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-200">Install **Unity.Mvc3** NuGet Package in the **MvcMusicStore** project.</span></span> <span data-ttu-id="4c2d1-201">若要执行此操作，打开**程序包管理器控制台**从**视图** | **其他 Windows**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-201">To do this, open the **Package Manager Console** from **View** | **Other Windows**.</span></span>
2. <span data-ttu-id="4c2d1-202">运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-202">Run the following command.</span></span>

    <span data-ttu-id="4c2d1-203">PMC</span><span class="sxs-lookup"><span data-stu-id="4c2d1-203">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    <span data-ttu-id="4c2d1-204">![安装 Unity.Mvc3 NuGet 包](aspnet-mvc-4-dependency-injection/_static/image4.png "安装 Unity.Mvc3 NuGet 包")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-204">![Installing Unity.Mvc3 NuGet Package](aspnet-mvc-4-dependency-injection/_static/image4.png "Installing Unity.Mvc3 NuGet Package")</span></span>

    <span data-ttu-id="4c2d1-205">*安装 Unity.Mvc3 NuGet 包*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-205">*Installing Unity.Mvc3 NuGet Package*</span></span>
3. <span data-ttu-id="4c2d1-206">一次**Unity.Mvc3**安装包，请浏览的文件和文件夹会自动将其添加为了简化 Unity 配置。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-206">Once the **Unity.Mvc3** package is installed, explore the files and folders it automatically adds in order to simplify Unity configuration.</span></span>

    <span data-ttu-id="4c2d1-207">![已安装的包 Unity.Mvc3](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 包安装")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-207">![Unity.Mvc3 package installed](aspnet-mvc-4-dependency-injection/_static/image5.png "Unity.Mvc3 package installed")</span></span>

    <span data-ttu-id="4c2d1-208">*Unity.Mvc3 包安装*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-208">*Unity.Mvc3 package installed*</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-applicationstart"></a><span data-ttu-id="4c2d1-209">任务 3-在 Global.asax.cs 应用程序中注册 Unity\_开始</span><span class="sxs-lookup"><span data-stu-id="4c2d1-209">Task 3 - Registering Unity in Global.asax.cs Application\_Start</span></span>

<span data-ttu-id="4c2d1-210">在本任务中，你将更新**应用程序\_启动**方法位于**Global.asax.cs**调用 Unity 引导程序初始值设定项，然后，更新引导程序文件注册服务和将用于依赖关系注入的控制器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-210">In this task, you will update the **Application\_Start** method located in **Global.asax.cs** to call the Unity Bootstrapper initializer and then, update the Bootstrapper file registering the Service and Controller you will use for Dependency Injection.</span></span>

1. <span data-ttu-id="4c2d1-211">现在，你将将挂接到引导程序是初始化 Unity 容器的文件和依赖关系解析程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-211">Now, you will hook up the Bootstrapper which is the file that initializes the Unity container and Dependency Resolver.</span></span> <span data-ttu-id="4c2d1-212">若要执行此操作，打开**Global.asax.cs**并添加以下突出显示的代码内**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-212">To do this, open **Global.asax.cs** and add the following highlighted code within the **Application\_Start** method.</span></span>

    <span data-ttu-id="4c2d1-213">(代码段- *ASP.NET 依赖关系注入实验-Ex01-初始化 Unity*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-213">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Initialize Unity*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. <span data-ttu-id="4c2d1-214">打开**Bootstrapper.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-214">Open **Bootstrapper.cs** file.</span></span>
3. <span data-ttu-id="4c2d1-215">包括以下命名空间： **MvcMusicStore.Services**并**MusicStore.Controllers**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-215">Include the following namespaces: **MvcMusicStore.Services** and **MusicStore.Controllers**.</span></span>

    <span data-ttu-id="4c2d1-216">(代码段- *ASP.NET 依赖关系注入实验-Ex01 的引导程序添加命名空间*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-216">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. <span data-ttu-id="4c2d1-217">替换**BuildUnityContainer**方法的内容与注册存储控制器和存储服务的以下代码。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-217">Replace **BuildUnityContainer** method's content with the following code that registers Store Controller and Store Service.</span></span>

    <span data-ttu-id="4c2d1-218">(代码段- *ASP.NET 依赖关系注入实验-Ex01-注册存储控制器和服务*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-218">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex01 - Register Store Controller and Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4c2d1-219">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="4c2d1-219">Task 4 - Running the Application</span></span>

<span data-ttu-id="4c2d1-220">在本任务中，将运行应用程序以验证它现在加载包括 Unity 之后。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-220">In this task, you will run the application to verify that it can now be loaded after including Unity.</span></span>

1. <span data-ttu-id="4c2d1-221">按**F5**若要运行该应用程序，该应用程序应立即加载而不显示任何错误消息。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-221">Press **F5** to run the application, the application should now load without showing any error message.</span></span>

    <span data-ttu-id="4c2d1-222">![运行应用程序依赖关系注入](aspnet-mvc-4-dependency-injection/_static/image6.png "使用依赖关系注入运行应用程序")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-222">![Running Application with Dependency Injection](aspnet-mvc-4-dependency-injection/_static/image6.png "Running Application with Dependency Injection")</span></span>

    <span data-ttu-id="4c2d1-223">*使用依赖关系注入运行的应用程序*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-223">*Running Application with Dependency Injection*</span></span>
2. <span data-ttu-id="4c2d1-224">浏览到 **/存储**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-224">Browse to **/Store**.</span></span> <span data-ttu-id="4c2d1-225">这会调用**StoreController**，其现已创建使用**Unity**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-225">This will invoke **StoreController**, which is now created using **Unity**.</span></span>

    <span data-ttu-id="4c2d1-226">![MVC Music 商店](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music 商店")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-226">![MVC Music Store](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC Music Store")</span></span>

    <span data-ttu-id="4c2d1-227">*MVC Music 商店*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-227">*MVC Music Store*</span></span>
3. <span data-ttu-id="4c2d1-228">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-228">Close the browser.</span></span>

<span data-ttu-id="4c2d1-229">在以下练习中，您将学习如何扩展要在 ASP.NET MVC 视图和操作筛选器内部使用它的依赖关系注入作用域。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-229">In the following exercises you will learn how to extend the Dependency Injection scope to use it inside ASP.NET MVC Views and Action Filters.</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a><span data-ttu-id="4c2d1-230">练习 2： 将注入视图</span><span class="sxs-lookup"><span data-stu-id="4c2d1-230">Exercise 2: Injecting a View</span></span>

<span data-ttu-id="4c2d1-231">在此练习中，您将学习如何使用依赖关系注入在 ASP.NET MVC 4 的新功能视图中为 Unity 集成。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-231">In this exercise, you will learn how to use Dependency Injection in a view with the new features of ASP.NET MVC 4 for Unity integration.</span></span> <span data-ttu-id="4c2d1-232">为此，您将调用自定义服务应用商店浏览视图后，它将显示一条消息，如下图中。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-232">In order to do that, you will call a custom service inside the Store Browse View, which will show a message and an image below.</span></span>

<span data-ttu-id="4c2d1-233">然后，将与 Unity 集成项目并创建自定义依赖关系解析程序来注入依赖项。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-233">Then, you will integrate the project with Unity and create a custom dependency resolver to inject the dependencies.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a><span data-ttu-id="4c2d1-234">任务 1-创建一个视图，它需要使用的服务</span><span class="sxs-lookup"><span data-stu-id="4c2d1-234">Task 1 - Creating a View that Consumes a Service</span></span>

<span data-ttu-id="4c2d1-235">在本任务中，将创建一个视图，它执行服务调用，以生成新的依赖项。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-235">In this task, you will create a view that performs a service call to generate a new dependency.</span></span> <span data-ttu-id="4c2d1-236">该服务包含在此解决方案中包含的简单消息传送服务。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-236">The service consists in a simple messaging service included in this solution.</span></span>

1. <span data-ttu-id="4c2d1-237">打开**开始**解决方案位于**Source\Ex02 注入 View\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-237">Open the **Begin** solution located in the **Source\Ex02-Injecting View\Begin** folder.</span></span> <span data-ttu-id="4c2d1-238">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-238">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4c2d1-239">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-239">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4c2d1-240">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-240">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4c2d1-241">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-241">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4c2d1-242">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-242">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4c2d1-243">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-243">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4c2d1-244">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-244">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4c2d1-245">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-245">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="4c2d1-246">有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-246">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4c2d1-247">包括**MessageService.cs**并**IMessageService.cs**类位于**源 \Assets**中的文件夹 **/服务**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-247">Include the **MessageService.cs** and the **IMessageService.cs** classes located in the **Source \Assets** folder in **/Services**.</span></span> <span data-ttu-id="4c2d1-248">若要执行此操作，右键单击**Services**文件夹，然后选择**添加现有项**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-248">To do this, right-click **Services** folder and select **Add Existing Item**.</span></span> <span data-ttu-id="4c2d1-249">浏览到文件的位置，并将其包含。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-249">Browse to the files' location and include them.</span></span>

    <span data-ttu-id="4c2d1-250">![添加消息服务和服务接口](aspnet-mvc-4-dependency-injection/_static/image8.png "添加消息服务和服务接口")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-250">![Adding Message Service and Service Interface](aspnet-mvc-4-dependency-injection/_static/image8.png "Adding Message Service and Service Interface")</span></span>

    <span data-ttu-id="4c2d1-251">*添加消息服务和服务接口*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-251">*Adding Message Service and Service Interface*</span></span>

    > [!NOTE]
    > <span data-ttu-id="4c2d1-252">**IMessageService**接口定义两个属性由实现**MessageService**类。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-252">The **IMessageService** interface defines two properties implemented by the **MessageService** class.</span></span> <span data-ttu-id="4c2d1-253">这些属性-**消息**并**ImageUrl**-存储要显示的消息和图像的 URL。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-253">These properties -**Message** and **ImageUrl**- store the message and the URL of the image to be displayed.</span></span>
3. <span data-ttu-id="4c2d1-254">创建文件夹 **/pages**在项目的根文件夹，以及如何将现有类**MyBasePage.cs**从**Source\Assets**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-254">Create the folder **/Pages** in the project's root folder, and then add the existing class **MyBasePage.cs** from **Source\Assets**.</span></span> <span data-ttu-id="4c2d1-255">基本页将继承具有以下结构。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-255">The base page you will inherit from has the following structure.</span></span>

    <span data-ttu-id="4c2d1-256">![页面文件夹](aspnet-mvc-4-dependency-injection/_static/image9.png "页面文件夹")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-256">![Pages folder](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages folder")</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. <span data-ttu-id="4c2d1-257">打开**Browse.cshtml**从查看 **/视图/存储**文件夹，并使其继承**MyBasePage.cs**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-257">Open **Browse.cshtml** view from **/Views/Store** folder, and make it inherit from **MyBasePage.cs**.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. <span data-ttu-id="4c2d1-258">在中**浏览**视图中，添加对的调用**MessageService**要显示的映像和服务来检索一条消息。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-258">In the **Browse** view, add a call to **MessageService** to display an image and a message retrieved by the service.</span></span>
   <span data-ttu-id="4c2d1-259">(C#)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-259">(C#)</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a><span data-ttu-id="4c2d1-260">任务 2-包括自定义依赖关系解析程序和自定义视图页激活器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-260">Task 2 - Including a Custom Dependency Resolver and a Custom View Page Activator</span></span>

<span data-ttu-id="4c2d1-261">在上一任务中，您注入新的依赖项内执行其内部的服务调用的视图。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-261">In the previous task, you injected a new dependency inside a view to perform a service call inside it.</span></span> <span data-ttu-id="4c2d1-262">现在，将通过实现 ASP.NET MVC 依赖关系注入接口解析该依赖关系**IViewPageActivator**并**IDependencyResolver**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-262">Now, you will resolve that dependency by implementing the ASP.NET MVC Dependency Injection interfaces **IViewPageActivator** and **IDependencyResolver**.</span></span> <span data-ttu-id="4c2d1-263">你将在解决方案中包括的实现**IDependencyResolver** ，将使用 Unity 处理服务检索。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-263">You will include in the solution an implementation of **IDependencyResolver** that will deal with the service retrieval by using Unity.</span></span> <span data-ttu-id="4c2d1-264">然后，将包括的另一个自定义实现**IViewPageActivator**将解决创建视图的接口。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-264">Then, you will include another custom implementation of **IViewPageActivator** interface that will solve the creation of the views.</span></span>

> [!NOTE]
> <span data-ttu-id="4c2d1-265">自 ASP.NET MVC 3 依赖关系注入的实现已简化用于注册服务的接口。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-265">Since ASP.NET MVC 3, the implementation for Dependency Injection had simplified the interfaces to register services.</span></span> <span data-ttu-id="4c2d1-266">**IDependencyResolver**并**IViewPageActivator**依赖关系注入是 ASP.NET MVC 3 功能的一部分。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-266">**IDependencyResolver** and **IViewPageActivator** are part of ASP.NET MVC 3 features for Dependency Injection.</span></span>
> 
> <span data-ttu-id="4c2d1-267">**-IDependencyResolver**界面替代了以前 IMvcServiceLocator。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-267">**- IDependencyResolver** interface replaces the previous IMvcServiceLocator.</span></span> <span data-ttu-id="4c2d1-268">IDependencyResolver 的实施者必须返回服务或服务集合的实例。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-268">Implementers of IDependencyResolver must return an instance of the service or a service collection.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> <span data-ttu-id="4c2d1-269">**-IViewPageActivator**接口提供了更加精细地控制如何通过依赖关系注入实例化视图页。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-269">**- IViewPageActivator** interface provides more fine-grained control over how view pages are instantiated via dependency injection.</span></span> <span data-ttu-id="4c2d1-270">实现的类**IViewPageActivator**接口可以创建使用上下文信息的视图实例。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-270">The classes that implement **IViewPageActivator** interface can create view instances using context information.</span></span>
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]


1. <span data-ttu-id="4c2d1-271">创建 /**工厂**项目的根文件夹中的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-271">Create the /**Factories** folder in the project's root folder.</span></span>
2. <span data-ttu-id="4c2d1-272">包括**CustomViewPageActivator.cs**到你的解决方案从 **/源/资产/** 到**工厂**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-272">Include **CustomViewPageActivator.cs** to your solution from **/Sources/Assets/** to **Factories** folder.</span></span> <span data-ttu-id="4c2d1-273">为此，请右键单击 **/Factories**文件夹，选择**添加 |现有项**，然后选择**CustomViewPageActivator.cs**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-273">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **CustomViewPageActivator.cs**.</span></span> <span data-ttu-id="4c2d1-274">此类实现**IViewPageActivator**接口来保存 Unity 容器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-274">This class implements the **IViewPageActivator** interface to hold the Unity Container.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > <span data-ttu-id="4c2d1-275">**CustomViewPageActivator**负责管理通过使用 Unity 容器创建一个视图。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-275">**CustomViewPageActivator** is responsible for managing the creation of a view by using a Unity container.</span></span>
3. <span data-ttu-id="4c2d1-276">包括**UnityDependencyResolver.cs**文件从 **/源/资产**到 **/Factories**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-276">Include **UnityDependencyResolver.cs** file from **/Sources/Assets** to **/Factories** folder.</span></span> <span data-ttu-id="4c2d1-277">为此，请右键单击 **/Factories**文件夹，选择**添加 |现有项**，然后选择**UnityDependencyResolver.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-277">To do that, right-click the **/Factories** folder, select **Add | Existing Item** and then select **UnityDependencyResolver.cs** file.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > <span data-ttu-id="4c2d1-278">**UnityDependencyResolver**类是 Unity 自定义 DependencyResolver。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-278">**UnityDependencyResolver** class is a custom DependencyResolver for Unity.</span></span> <span data-ttu-id="4c2d1-279">当 Unity 容器中找不到服务时，被 invocated 基冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-279">When a service cannot be found inside the Unity container, the base resolver is invocated.</span></span>

<span data-ttu-id="4c2d1-280">在下面的任务将注册这两个实现以便了解服务和视图的位置的模型。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-280">In the following task both implementations will be registered to let the model know the location of the services and the views.</span></span>

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a><span data-ttu-id="4c2d1-281">任务 3-Unity 容器中注册的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="4c2d1-281">Task 3 - Registering for Dependency Injection within Unity container</span></span>

<span data-ttu-id="4c2d1-282">在此任务中，会将所有以前的内容在一起以进行工作的依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-282">In this task, you will put all the previous things together to make Dependency Injection work.</span></span>

<span data-ttu-id="4c2d1-283">到现在为止你的解决方案包含以下元素：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-283">Up to now your solution has the following elements:</span></span>

- <span data-ttu-id="4c2d1-284">一个**浏览**视图继承自**MyBaseClass** ，并使用**MessageService**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-284">A **Browse** View that inherits from **MyBaseClass** and consumes **MessageService**.</span></span>
- <span data-ttu-id="4c2d1-285">中间类-**MyBaseClass**-具有依赖关系注入的服务接口声明。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-285">An intermediate class -**MyBaseClass**- that has dependency injection declared for the service interface.</span></span>
- <span data-ttu-id="4c2d1-286">服务-a **MessageService** -及其界面**IMessageService**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-286">A service - **MessageService** - and its interface **IMessageService**.</span></span>
- <span data-ttu-id="4c2d1-287">Unity-自定义依赖关系解析程序**UnityDependencyResolver** -服务检索的处理。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-287">A custom dependency resolver for Unity - **UnityDependencyResolver** - that deals with service retrieval.</span></span>
- <span data-ttu-id="4c2d1-288">视图页激活器- **CustomViewPageActivator** -创建页。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-288">A View Page activator - **CustomViewPageActivator** - that creates the page.</span></span>

<span data-ttu-id="4c2d1-289">若要将注入**浏览**视图中，现在，您将注册的自定义依赖关系解析程序在 Unity 容器中。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-289">To inject **Browse** View, you will now register the custom dependency resolver in the Unity container.</span></span>

1. <span data-ttu-id="4c2d1-290">打开**Bootstrapper.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-290">Open **Bootstrapper.cs** file.</span></span>
2. <span data-ttu-id="4c2d1-291">注册的实例**MessageService**到 Unity 容器来初始化该服务：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-291">Register an instance of **MessageService** into the Unity container to initialize the service:</span></span>

    <span data-ttu-id="4c2d1-292">(代码段- *ASP.NET 依赖关系注入实验-Ex02-注册消息服务*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-292">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register Message Service*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. <span data-ttu-id="4c2d1-293">添加对的引用**MvcMusicStore.Factories**命名空间。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-293">Add a reference to **MvcMusicStore.Factories** namespace.</span></span>

    <span data-ttu-id="4c2d1-294">(代码段- *ASP.NET 依赖关系注入实验-Ex02-工厂 Namespace*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-294">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Factories Namespace*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. <span data-ttu-id="4c2d1-295">注册**CustomViewPageActivator**到 Unity 容器视图页激活器为：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-295">Register **CustomViewPageActivator** as a View Page activator into the Unity container:</span></span>

    <span data-ttu-id="4c2d1-296">(代码段- *ASP.NET 依赖关系注入实验-Ex02-注册 CustomViewPageActivator*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-296">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Register CustomViewPageActivator*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. <span data-ttu-id="4c2d1-297">ASP.NET MVC 4 默认依赖关系解析程序替换的实例**UnityDependencyResolver**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-297">Replace ASP.NET MVC 4 default dependency resolver with an instance of **UnityDependencyResolver**.</span></span> <span data-ttu-id="4c2d1-298">若要执行此操作，请替换**Initialise**方法内容与以下代码：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-298">To do this, replace **Initialise** method content with the following code:</span></span>

    <span data-ttu-id="4c2d1-299">(代码段- *ASP.NET 依赖关系注入实验-Ex02-更新依赖关系解析程序*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-299">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex02 - Update Dependency Resolver*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="4c2d1-300">ASP.NET MVC 提供了一个默认依赖关系解析程序类。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-300">ASP.NET MVC provides a default dependency resolver class.</span></span> <span data-ttu-id="4c2d1-301">若要与我们为 unity 创建的一个使用自定义依赖关系解析程序，此解析程序必须被替换。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-301">To work with custom dependency resolvers as the one we have created for unity, this resolver has to be replaced.</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="4c2d1-302">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="4c2d1-302">Task 4 - Running the Application</span></span>

<span data-ttu-id="4c2d1-303">在本任务中，你将运行应用程序以验证存储浏览器使用该服务，并显示图像和检索到的消息：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-303">In this task, you will run the application to verify that the Store Browser consumes the service and shows the image and the message retrieved:</span></span>

1. <span data-ttu-id="4c2d1-304">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-304">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4c2d1-305">单击**Rock**内流派菜单，请参阅如何**MessageService**被注入到视图和加载的欢迎消息和映像。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-305">Click **Rock** within the Genres Menu and see how the **MessageService** was injected to the view and loaded the welcome message and the image.</span></span> <span data-ttu-id="4c2d1-306">在此示例中，我们进入到&quot; **Rock**&quot;:</span><span class="sxs-lookup"><span data-stu-id="4c2d1-306">In this example, we are entering to &quot;**Rock**&quot;:</span></span>

    <span data-ttu-id="4c2d1-307">![MVC Music 商店的视图注入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music 商店的视图注入")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-307">![MVC Music Store - View Injection](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC Music Store - View Injection")</span></span>

    <span data-ttu-id="4c2d1-308">*MVC Music 商店的视图注入*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-308">*MVC Music Store - View Injection*</span></span>
3. <span data-ttu-id="4c2d1-309">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-309">Close the browser.</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a><span data-ttu-id="4c2d1-310">练习 3： 将注入操作筛选器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-310">Exercise 3: Injecting Action Filters</span></span>

<span data-ttu-id="4c2d1-311">在先前的动手**自定义操作筛选器**您曾经使用筛选器自定义和注入。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-311">In the previous Hands-On lab **Custom Action Filters** you have worked with filters customization and injection.</span></span> <span data-ttu-id="4c2d1-312">在此练习中，您将学习如何使用 Unity 容器使用依赖关系注入插入筛选器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-312">In this exercise, you will learn how to inject filters with Dependency Injection by using the Unity container.</span></span> <span data-ttu-id="4c2d1-313">为此，将向解决方案中添加音乐应用商店将描摹站点的活动的自定义操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-313">To do that, you will add to the Music Store solution a custom action filter that will trace the activity of the site.</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a><span data-ttu-id="4c2d1-314">任务 1-在解决方案中包括跟踪筛选器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-314">Task 1 - Including the Tracking Filter in the Solution</span></span>

<span data-ttu-id="4c2d1-315">在本任务中，您将包括在音乐应用商店中自定义操作筛选器与跟踪事件。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-315">In this task, you will include in the Music Store a custom action filter to trace events.</span></span> <span data-ttu-id="4c2d1-316">为自定义操作筛选器的概念已中处理的上一个实验室&quot;自定义操作筛选器&quot;，您将只包括此实验中，从资产文件夹的筛选器类，然后创建用于 Unity 的筛选器提供程序：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-316">As custom action filter concepts are already treated in the previous Lab &quot;Custom Action Filters&quot;, you will just include the filter class from the Assets folder of this lab, and then create a Filter Provider for Unity:</span></span>

1. <span data-ttu-id="4c2d1-317">打开**开始**解决方案位于**Source\Ex03-注入操作 Filter\Begin**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-317">Open the **Begin** solution located in the **Source\Ex03 - Injecting Action Filter\Begin** folder.</span></span> <span data-ttu-id="4c2d1-318">否则，可能会继续使用**最终**解决方案通过完成上一练习中获取。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-318">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="4c2d1-319">如果您打开提供**开始**需要下载某些缺少的 NuGet 包的解决方案，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-319">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="4c2d1-320">若要执行此操作，请单击**项目**菜单，然后选择**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-320">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="4c2d1-321">在中**管理 NuGet 包**对话框中，单击**还原**若要下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-321">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="4c2d1-322">最后，通过单击生成解决方案**构建** | **生成解决方案**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-322">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4c2d1-323">使用 NuGet 的优点之一是，您不必提供在项目中的所有库项目大小减少。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-323">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="4c2d1-324">使用 NuGet 增强工具，请通过在 Packages.config 文件中，指定包版本可以下载第一次运行该项目的所有所需的库。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-324">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="4c2d1-325">这就是原因需要将从本实验中打开现有解决方案后运行这些步骤。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-325">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
      > 
      > <span data-ttu-id="4c2d1-326">有关详细信息，请参阅此文章： [ http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages ](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-326">For more information, see this article: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).</span></span>
2. <span data-ttu-id="4c2d1-327">包括**TraceActionFilter.cs**文件从 **/源/资产**到 **/筛选**文件夹。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-327">Include **TraceActionFilter.cs** file from **/Sources/Assets** to **/Filters** folder.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > <span data-ttu-id="4c2d1-328">此自定义操作筛选器执行 ASP.NET 跟踪。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-328">This custom action filter performs ASP.NET tracing.</span></span> <span data-ttu-id="4c2d1-329">你可以检查&quot;ASP.NET MVC 4 本地和动态操作筛选器&quot;实验室进行更多参考。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-329">You can check &quot;ASP.NET MVC 4 local and Dynamic Action Filters&quot; Lab for more reference.</span></span>
3. <span data-ttu-id="4c2d1-330">添加空的类**FilterProvider.cs**文件夹中的项目到  **/筛选器。**</span><span class="sxs-lookup"><span data-stu-id="4c2d1-330">Add the empty class **FilterProvider.cs** to the project in the folder **/Filters.**</span></span>
4. <span data-ttu-id="4c2d1-331">添加**System.Web.Mvc**并**Microsoft.Practices.Unity**中的命名空间**FilterProvider.cs**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-331">Add the **System.Web.Mvc** and **Microsoft.Practices.Unity** namespaces in **FilterProvider.cs**.</span></span>

    <span data-ttu-id="4c2d1-332">(代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序添加命名空间*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-332">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. <span data-ttu-id="4c2d1-333">使类继承自**IFilterProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-333">Make the class inherit from **IFilterProvider** Interface.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. <span data-ttu-id="4c2d1-334">添加**IUnityContainer**属性中的**FilterProvider**类，然后创建一个类构造函数来分配容器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-334">Add a **IUnityContainer** property in the **FilterProvider** class, and then create a class constructor to assign the container.</span></span>

    <span data-ttu-id="4c2d1-335">(代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序构造函数*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-335">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider Constructor*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > <span data-ttu-id="4c2d1-336">不创建筛选器提供程序类构造函数**新**对象内。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-336">The filter provider class constructor is not creating a **new** object inside.</span></span> <span data-ttu-id="4c2d1-337">作为参数传递容器，并通过 Unity 解决依赖项。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-337">The container is passed as a parameter, and the dependency is solved by Unity.</span></span>
7. <span data-ttu-id="4c2d1-338">在中**FilterProvider**类中，实现方法**GetFilters**从**IFilterProvider**接口。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-338">In the **FilterProvider** class, implement the method **GetFilters** from **IFilterProvider** interface.</span></span>

    <span data-ttu-id="4c2d1-339">(代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序 GetFilters*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-339">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Filter Provider GetFilters*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a><span data-ttu-id="4c2d1-340">任务 2-注册和启用该筛选器</span><span class="sxs-lookup"><span data-stu-id="4c2d1-340">Task 2 - Registering and Enabling the Filter</span></span>

<span data-ttu-id="4c2d1-341">在本任务中，将启用站点跟踪。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-341">In this task, you will enable site tracking.</span></span> <span data-ttu-id="4c2d1-342">为此，请将注册中的筛选器**Bootstrapper.cs BuildUnityContainer**方法以启动跟踪：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-342">To do that, you will register the filter in **Bootstrapper.cs BuildUnityContainer** method to start tracing:</span></span>

1. <span data-ttu-id="4c2d1-343">打开**Web.config**位于项目根目录和 System.Web 组启用跟踪跟踪。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-343">Open **Web.config** located in the project root and enable trace tracking at System.Web group.</span></span>

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. <span data-ttu-id="4c2d1-344">打开**Bootstrapper.cs**项目根目录。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-344">Open **Bootstrapper.cs** at project root.</span></span>
3. <span data-ttu-id="4c2d1-345">添加对的引用**MvcMusicStore.Filters**命名空间。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-345">Add a reference to the **MvcMusicStore.Filters** namespace.</span></span>

    <span data-ttu-id="4c2d1-346">(代码段- *ASP.NET 依赖关系注入实验室-Ex03 的引导程序添加命名空间*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-346">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Bootstrapper Adding Namespaces*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. <span data-ttu-id="4c2d1-347">选择**BuildUnityContainer**方法，并注册 Unity 容器中的筛选器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-347">Select the **BuildUnityContainer** method and register the filter in the Unity Container.</span></span> <span data-ttu-id="4c2d1-348">你将需要注册筛选器提供程序，以及操作筛选器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-348">You will have to register the filter provider as well as the action filter.</span></span>

    <span data-ttu-id="4c2d1-349">(代码段- *ASP.NET 依赖关系注入实验室-Ex03-注册 FilterProvider 和 ActionFilter*)</span><span class="sxs-lookup"><span data-stu-id="4c2d1-349">(Code Snippet - *ASP.NET Dependency Injection Lab - Ex03 - Register FilterProvider and ActionFilter*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="4c2d1-350">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="4c2d1-350">Task 3 - Running the Application</span></span>

<span data-ttu-id="4c2d1-351">在此任务中，您将运行该应用程序和测试自定义操作筛选器跟踪活动：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-351">In this task, you will run the application and test that the custom action filter is tracing the activity:</span></span>

1. <span data-ttu-id="4c2d1-352">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-352">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="4c2d1-353">单击**Rock**流派菜单中。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-353">Click **Rock** within the Genres Menu.</span></span> <span data-ttu-id="4c2d1-354">如果需要，可以浏览到多个流派。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-354">You can browse to more genres if you want to.</span></span>

    <span data-ttu-id="4c2d1-355">![音乐应用商店](aspnet-mvc-4-dependency-injection/_static/image11.png "音乐应用商店")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-355">![Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Music Store")</span></span>

    <span data-ttu-id="4c2d1-356">*Music 商店*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-356">*Music Store*</span></span>
3. <span data-ttu-id="4c2d1-357">浏览到 **/Trace.axd**若要查看应用程序跟踪页上，然后依次**查看详细信息**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-357">Browse to **/Trace.axd** to see the Application Trace page, and then click **View Details**.</span></span>

    <span data-ttu-id="4c2d1-358">![应用程序跟踪日志](aspnet-mvc-4-dependency-injection/_static/image12.png "应用程序跟踪日志")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-358">![Application Trace Log](aspnet-mvc-4-dependency-injection/_static/image12.png "Application Trace Log")</span></span>

    <span data-ttu-id="4c2d1-359">*应用程序跟踪日志*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-359">*Application Trace Log*</span></span>

    <span data-ttu-id="4c2d1-360">![应用程序跟踪的请求详细信息](aspnet-mvc-4-dependency-injection/_static/image13.png "跟踪应用程序的请求的详细信息")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-360">![Application Trace - Request Details](aspnet-mvc-4-dependency-injection/_static/image13.png "Application Trace - Request Details")</span></span>

    <span data-ttu-id="4c2d1-361">*应用程序跟踪的请求详细信息*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-361">*Application Trace - Request Details*</span></span>
4. <span data-ttu-id="4c2d1-362">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-362">Close the browser.</span></span>

* * *

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="4c2d1-363">总结</span><span class="sxs-lookup"><span data-stu-id="4c2d1-363">Summary</span></span>

<span data-ttu-id="4c2d1-364">通过完成本动手实验介绍了如何在 ASP.NET MVC 4 中使用依赖关系注入，通过集成 Unity 使用 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-364">By completing this Hands-On Lab you have learned how to use Dependency Injection in ASP.NET MVC 4 by integrating Unity using a NuGet Package.</span></span> <span data-ttu-id="4c2d1-365">若要实现此目的，你已在控制器、 视图和操作筛选器内使用依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-365">To achieve that, you have used Dependency Injection inside controllers, views and action filters.</span></span>

<span data-ttu-id="4c2d1-366">介绍了以下概念：</span><span class="sxs-lookup"><span data-stu-id="4c2d1-366">The following concepts were covered:</span></span>

- <span data-ttu-id="4c2d1-367">ASP.NET MVC 4 依赖关系注入功能</span><span class="sxs-lookup"><span data-stu-id="4c2d1-367">ASP.NET MVC 4 Dependency Injection features</span></span>
- <span data-ttu-id="4c2d1-368">Unity 集成使用 Unity.Mvc3 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="4c2d1-368">Unity integration using Unity.Mvc3 NuGet Package</span></span>
- <span data-ttu-id="4c2d1-369">控制器中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="4c2d1-369">Dependency Injection in Controllers</span></span>
- <span data-ttu-id="4c2d1-370">在视图中的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="4c2d1-370">Dependency Injection in Views</span></span>
- <span data-ttu-id="4c2d1-371">操作筛选器的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="4c2d1-371">Dependency injection of Action Filters</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="4c2d1-372">附录 a： 安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="4c2d1-372">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="4c2d1-373">你可以安装**Microsoft Visual Studio Express 2012 for Web**或另一个&quot;Express&quot;使用版本 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4c2d1-373">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="4c2d1-374">以下说明将指导您完成安装所需的步骤*Visual studio Express 2012 for Web*使用*Microsoft Web 平台安装程序*。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-374">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="4c2d1-375">转到[ [ https://go.microsoft.com/? linkid = 9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-375">Go to [[https://go.microsoft.com/? linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="4c2d1-376">或者，如果你已安装 Web 平台安装程序，则可以打开它，并搜索产品&quot; <em>Visual Studio Express 2012 for Web 与 Windows Azure SDK</em>&quot;。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-376">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="4c2d1-377">单击**立即安装**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-377">Click on **Install Now**.</span></span> <span data-ttu-id="4c2d1-378">如果还没有**Web 平台安装程序**将重定向以下载并安装。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-378">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="4c2d1-379">一次**Web 平台安装程序**处于打开状态，单击**安装**以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-379">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="4c2d1-380">![安装 Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-380">![Install Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="4c2d1-381">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-381">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="4c2d1-382">阅读所有产品的许可证和条款，然后单击**我接受**以继续。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-382">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-dependency-injection/_static/image15.png)

    <span data-ttu-id="4c2d1-384">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-384">*Accepting the license terms*</span></span>
5. <span data-ttu-id="4c2d1-385">等待，直到下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-385">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-dependency-injection/_static/image16.png)

    <span data-ttu-id="4c2d1-387">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-387">*Installation progress*</span></span>
6. <span data-ttu-id="4c2d1-388">安装完成后，单击**完成**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-388">When the installation completes, click **Finish**.</span></span>

    ![安装已完成](aspnet-mvc-4-dependency-injection/_static/image17.png)

    <span data-ttu-id="4c2d1-390">*安装已完成*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-390">*Installation completed*</span></span>
7. <span data-ttu-id="4c2d1-391">单击**退出**以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-391">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="4c2d1-392">若要打开 Visual Studio Express for Web，请转到**启动**屏幕上即可开始编写&quot; **VS Express**&quot;，然后单击**VS Express for Web**磁贴。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-392">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-dependency-injection/_static/image18.png)

    <span data-ttu-id="4c2d1-394">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-394">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="4c2d1-395">附录 b： 使用代码片段</span><span class="sxs-lookup"><span data-stu-id="4c2d1-395">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="4c2d1-396">使用代码段，可以轻松获得相关所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-396">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="4c2d1-397">实验室文档将告诉您完全何时可以使用它们，如下图中所示。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-397">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="4c2d1-398">![使用 Visual Studio 代码段代码插入到你的项目](aspnet-mvc-4-dependency-injection/_static/image19.png "使用 Visual Studio 代码段代码插入到你的项目")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-398">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-dependency-injection/_static/image19.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="4c2d1-399">*使用 Visual Studio 代码段代码插入到你的项目*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-399">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="4c2d1-400">***若要添加代码段使用键盘 (仅限 C#)***</span><span class="sxs-lookup"><span data-stu-id="4c2d1-400">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="4c2d1-401">将光标置于要插入的代码。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-401">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="4c2d1-402">开始键入代码片段名称 （不带空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-402">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="4c2d1-403">观看作为 IntelliSense 显示匹配的代码段的名称。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-403">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="4c2d1-404">选择正确的代码段 （或继续键入直到整个代码段的名称处于选定状态）。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-404">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="4c2d1-405">按 Tab 键两次，以在光标位置插入代码段。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-405">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="4c2d1-406">![开始键入代码段名称](aspnet-mvc-4-dependency-injection/_static/image20.png "开始键入代码段名称")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-406">![Start typing the snippet name](aspnet-mvc-4-dependency-injection/_static/image20.png "Start typing the snippet name")</span></span>

<span data-ttu-id="4c2d1-407">*开始键入代码段名称*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-407">*Start typing the snippet name*</span></span>

<span data-ttu-id="4c2d1-408">![按 tab 键以选择突出显示代码段](aspnet-mvc-4-dependency-injection/_static/image21.png "按选项卡以选择突出显示代码段")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-408">![Press Tab to select the highlighted snippet](aspnet-mvc-4-dependency-injection/_static/image21.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="4c2d1-409">*按 tab 键以选择突出显示代码段*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-409">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="4c2d1-410">![再次按 Tab 和代码段将 expand](aspnet-mvc-4-dependency-injection/_static/image22.png "再次按 Tab 和代码段将扩展")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-410">![Press Tab again and the snippet will expand](aspnet-mvc-4-dependency-injection/_static/image22.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="4c2d1-411">*再次按 Tab 和代码段将扩展*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-411">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="4c2d1-412">***若要添加代码段使用鼠标 （C#、 Visual Basic 和 XML）*** 1。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-412">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="4c2d1-413">右键单击你想要插入的代码片段。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-413">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="4c2d1-414">选择**插入代码段**跟**我的代码片段**。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-414">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="4c2d1-415">通过单击选择列表中中的相关代码片段。</span><span class="sxs-lookup"><span data-stu-id="4c2d1-415">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="4c2d1-416">![右键单击你想要插入代码段和选择插入代码段](aspnet-mvc-4-dependency-injection/_static/image23.png "右键单击你想要插入代码段和选择插入代码段")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-416">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-dependency-injection/_static/image23.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="4c2d1-417">*右键单击你想要插入代码段和选择插入代码段*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-417">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="4c2d1-418">![通过单击选择列表中中的相关代码片段](aspnet-mvc-4-dependency-injection/_static/image24.png "通过单击选择列表中中的相关代码片段")</span><span class="sxs-lookup"><span data-stu-id="4c2d1-418">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-dependency-injection/_static/image24.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="4c2d1-419">*通过单击选择列表中中的相关代码片段*</span><span class="sxs-lookup"><span data-stu-id="4c2d1-419">*Pick the relevant snippet from the list, by clicking on it*</span></span>
