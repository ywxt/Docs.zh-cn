---
uid: signalr/overview/older-versions/dependency-injection
title: 在 SignalR 的依赖关系注入 1.x |Microsoft 文档
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/15/2013
ms.topic: article
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
ms.technology: dotnet-signalr
ms.prod: .net-framework
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 6fd155adc9a0aa71b66db7a51062a51fb0c1feca
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26505486"
---
<a name="dependency-injection-in-signalr-1x"></a><span data-ttu-id="03986-102">在 SignalR 的依赖关系注入 1.x</span><span class="sxs-lookup"><span data-stu-id="03986-102">Dependency Injection in SignalR 1.x</span></span>
====================
<span data-ttu-id="03986-103">通过[Mike Wasson](https://github.com/MikeWasson)， [Patrick Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="03986-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

<span data-ttu-id="03986-104">依赖关系注入是一种方法来删除硬编码对象，使其更方便，若要替换的对象的依赖项，为测试 （使用模拟对象） 或更改运行时行为之间的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="03986-104">Dependency injection is a way to remove hard-coded dependencies between objects, making it easier to replace an object's dependencies, either for testing (using mock objects) or to change run-time behavior.</span></span> <span data-ttu-id="03986-105">本教程演示如何在 SignalR 集线器上执行依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="03986-105">This tutorial shows how to perform dependency injection on SignalR hubs.</span></span> <span data-ttu-id="03986-106">它还演示如何使用 SignalR IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="03986-106">It also shows how to use IoC containers with SignalR.</span></span> <span data-ttu-id="03986-107">IoC 容器是一个常规用于依赖关系注入框架。</span><span class="sxs-lookup"><span data-stu-id="03986-107">An IoC container is a general framework for dependency injection.</span></span>

## <a name="what-is-dependency-injection"></a><span data-ttu-id="03986-108">什么是依赖关系注入？</span><span class="sxs-lookup"><span data-stu-id="03986-108">What is Dependency Injection?</span></span>

<span data-ttu-id="03986-109">如果你已熟悉依赖关系注入，跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="03986-109">Skip this section if you are already familiar with dependency injection.</span></span>

<span data-ttu-id="03986-110">*依赖关系注入*(DI) 是一种模式不负责创建其自己的依赖项对象。</span><span class="sxs-lookup"><span data-stu-id="03986-110">*Dependency injection* (DI) is a pattern where objects are not responsible for creating their own dependencies.</span></span> <span data-ttu-id="03986-111">下面是一个简单的示例，以促使 DI。</span><span class="sxs-lookup"><span data-stu-id="03986-111">Here is a simple example to motivate DI.</span></span> <span data-ttu-id="03986-112">假设你有需要记录消息的对象。</span><span class="sxs-lookup"><span data-stu-id="03986-112">Suppose you have an object that needs to log messages.</span></span> <span data-ttu-id="03986-113">你可以定义日志记录接口：</span><span class="sxs-lookup"><span data-stu-id="03986-113">You might define a logging interface:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

<span data-ttu-id="03986-114">在你的对象，你可以创建`ILogger`记录消息：</span><span class="sxs-lookup"><span data-stu-id="03986-114">In your object, you can create an `ILogger` to log messages:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

<span data-ttu-id="03986-115">此方法有效，但它不是最佳设计。</span><span class="sxs-lookup"><span data-stu-id="03986-115">This works, but it's not the best design.</span></span> <span data-ttu-id="03986-116">如果你想要替换`FileLogger`与另一个`ILogger`实现中，你将需要修改`SomeComponent`。</span><span class="sxs-lookup"><span data-stu-id="03986-116">If you want to replace `FileLogger` with another `ILogger` implementation, you will have to modify `SomeComponent`.</span></span> <span data-ttu-id="03986-117">Supposing 大量的其他对象使用`FileLogger`，你将需要更改所有这些。</span><span class="sxs-lookup"><span data-stu-id="03986-117">Supposing that a lot of other objects use `FileLogger`, you will need to change all of them.</span></span> <span data-ttu-id="03986-118">或如果你决定进行`FileLogger`单一实例，你还需要在整个应用程序更改。</span><span class="sxs-lookup"><span data-stu-id="03986-118">Or if you decide to make `FileLogger` a singleton, you'll also need to make changes throughout the application.</span></span>

<span data-ttu-id="03986-119">更好的方法是以"插入"`ILogger`到对象-例如，通过使用构造函数自变量：</span><span class="sxs-lookup"><span data-stu-id="03986-119">A better approach is to "inject" an `ILogger` into the object—for example, by using a constructor argument:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

<span data-ttu-id="03986-120">现在的对象不是负责选择其`ILogger`使用。</span><span class="sxs-lookup"><span data-stu-id="03986-120">Now the object is not responsible for selecting which `ILogger` to use.</span></span> <span data-ttu-id="03986-121">你可以从交换机`ILogger`而无需更改依赖于它的对象的实现。</span><span class="sxs-lookup"><span data-stu-id="03986-121">You can swich `ILogger` implementations without changing the objects that depend on it.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

<span data-ttu-id="03986-122">此模式称为[构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)。</span><span class="sxs-lookup"><span data-stu-id="03986-122">This pattern is called [constructor injection](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection).</span></span> <span data-ttu-id="03986-123">另一种模式是 setter 注入，你在其中设置通过 setter 方法或属性的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="03986-123">Another pattern is setter injection, where you set the dependency through a setter method or property.</span></span>

## <a name="simple-dependency-injection-in-signalr"></a><span data-ttu-id="03986-124">在 SignalR 的简单的依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="03986-124">Simple Dependency Injection in SignalR</span></span>

<span data-ttu-id="03986-125">本教程中的聊天应用程序，请考虑[Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="03986-125">Consider the Chat application from the tutorial [Getting Started with SignalR](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="03986-126">下面是从该应用程序的中心类：</span><span class="sxs-lookup"><span data-stu-id="03986-126">Here is the hub class from that application:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

<span data-ttu-id="03986-127">假设你想要向用户发送之前存储在服务器上的聊天消息。</span><span class="sxs-lookup"><span data-stu-id="03986-127">Suppose that you want to store chat messages on the server before sending them.</span></span> <span data-ttu-id="03986-128">你可以定义一个接口，提取此功能，并使用 DI 注入到接口`ChatHub`类。</span><span class="sxs-lookup"><span data-stu-id="03986-128">You might define an interface that abstracts this functionality, and use DI to inject the interface into the `ChatHub` class.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

<span data-ttu-id="03986-129">唯一的问题是 SignalR 应用程序不会直接创建中心;SignalR 为你创建它们。</span><span class="sxs-lookup"><span data-stu-id="03986-129">The only problem is that a SignalR application does not directly create hubs; SignalR creates them for you.</span></span> <span data-ttu-id="03986-130">默认情况下，SignalR 希望中心类，具有无参数构造函数。</span><span class="sxs-lookup"><span data-stu-id="03986-130">By default, SignalR expects a hub class to have a parameterless constructor.</span></span> <span data-ttu-id="03986-131">但是，你可以轻松地注册创建中心实例的函数和使用此函数来执行 DI。</span><span class="sxs-lookup"><span data-stu-id="03986-131">However, you can easily register a function to create hub instances, and use this function to perform DI.</span></span> <span data-ttu-id="03986-132">注册此函数通过调用**GlobalHost.DependencyResolver.Register**。</span><span class="sxs-lookup"><span data-stu-id="03986-132">Register the function by calling **GlobalHost.DependencyResolver.Register**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

<span data-ttu-id="03986-133">现在 SignalR 将调用此匿名函数，只要它需要创建`ChatHub`实例。</span><span class="sxs-lookup"><span data-stu-id="03986-133">Now SignalR will invoke this anonymous function whenever it needs to create a `ChatHub` instance.</span></span>

## <a name="ioc-containers"></a><span data-ttu-id="03986-134">IoC 容器</span><span class="sxs-lookup"><span data-stu-id="03986-134">IoC Containers</span></span>

<span data-ttu-id="03986-135">前面的代码是相当不错的简单的用例。</span><span class="sxs-lookup"><span data-stu-id="03986-135">The previous code is fine for simple cases.</span></span> <span data-ttu-id="03986-136">但你仍然必须编写此：</span><span class="sxs-lookup"><span data-stu-id="03986-136">But you still had to write this:</span></span>

[!code-css[Main](dependency-injection/samples/sample8.css)]

<span data-ttu-id="03986-137">在具有许多依赖关系的复杂应用程序，你可能需要编写大量的此"连结"代码。</span><span class="sxs-lookup"><span data-stu-id="03986-137">In a complex application with many dependencies, you might need to write a lot of this "wiring" code.</span></span> <span data-ttu-id="03986-138">此代码可能难以维护，尤其是在嵌套依赖关系。</span><span class="sxs-lookup"><span data-stu-id="03986-138">This code can be hard to maintain, especially if dependencies are nested.</span></span> <span data-ttu-id="03986-139">也很难进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="03986-139">It is also hard to unit test.</span></span>

<span data-ttu-id="03986-140">一种解决方案是使用 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="03986-140">One solution is to use an IoC container.</span></span> <span data-ttu-id="03986-141">IoC 容器是一个软件组件，负责管理依赖关系。你向容器中，注册类型，然后使用容器以创建对象。</span><span class="sxs-lookup"><span data-stu-id="03986-141">An IoC container is a software component that is responsible for managing dependencies.You register types with the container, and then use the container to create objects.</span></span> <span data-ttu-id="03986-142">容器自动计算出的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="03986-142">The container automatically figures out the dependency relations.</span></span> <span data-ttu-id="03986-143">多个 IoC 容器还可用于控制对象生存期和作用域等事务。</span><span class="sxs-lookup"><span data-stu-id="03986-143">Many IoC containers also allow you to control things like object lifetime and scope.</span></span>

> [!NOTE]
> <span data-ttu-id="03986-144">"IoC"代表"反向的控件"，它是常规的模式其中一个框架，调入应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="03986-144">"IoC" stands for "inversion of control", which is a general pattern where a framework calls into application code.</span></span> <span data-ttu-id="03986-145">IoC 容器构造对象，其中"反转"常用控制流。</span><span class="sxs-lookup"><span data-stu-id="03986-145">An IoC container constructs your objects for you, which "inverts" the usual flow of control.</span></span>


## <a name="using-ioc-containers-in-signalr"></a><span data-ttu-id="03986-146">使用 SignalR 在 IoC 容器</span><span class="sxs-lookup"><span data-stu-id="03986-146">Using IoC Containers in SignalR</span></span>

<span data-ttu-id="03986-147">聊天应用程序可能是太简单，能够受益于 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="03986-147">The Chat application is probably too simple to benefit from an IoC container.</span></span> <span data-ttu-id="03986-148">相反，让我们看一下[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)示例。</span><span class="sxs-lookup"><span data-stu-id="03986-148">Instead, let's look at the [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) sample.</span></span>

<span data-ttu-id="03986-149">StockTicker 示例定义两个主要类：</span><span class="sxs-lookup"><span data-stu-id="03986-149">The StockTicker sample defines two main classes:</span></span>

- <span data-ttu-id="03986-150">`StockTickerHub`： 管理客户端连接中心类。</span><span class="sxs-lookup"><span data-stu-id="03986-150">`StockTickerHub`: The hub class, which manages client connections.</span></span>
- <span data-ttu-id="03986-151">`StockTicker`： 包含股票价格并定期更新这些值单一实例。</span><span class="sxs-lookup"><span data-stu-id="03986-151">`StockTicker`: A singleton that holds stock prices and periodically updates them.</span></span>

<span data-ttu-id="03986-152">`StockTickerHub`保存对`StockTicker`转变成 singleton，虽然`StockTicker`保存到的引用**IHubConnectionContext**为`StockTickerHub`。</span><span class="sxs-lookup"><span data-stu-id="03986-152">`StockTickerHub` holds a reference to the `StockTicker` singleton, while `StockTicker` holds a reference to the **IHubConnectionContext** for the `StockTickerHub`.</span></span> <span data-ttu-id="03986-153">使用此接口与进行通信`StockTickerHub`实例。</span><span class="sxs-lookup"><span data-stu-id="03986-153">It uses this interface to communicate with `StockTickerHub` instances.</span></span> <span data-ttu-id="03986-154">(有关详细信息，请参阅[服务器广播使用 ASP.NET SignalR](index.md)。)</span><span class="sxs-lookup"><span data-stu-id="03986-154">(For more information, see [Server Broadcast with ASP.NET SignalR](index.md).)</span></span>

<span data-ttu-id="03986-155">我们可以使用 IoC 容器有点理清这些依赖关系。</span><span class="sxs-lookup"><span data-stu-id="03986-155">We can use an IoC container to untangle these dependencies a bit.</span></span> <span data-ttu-id="03986-156">首先，让我们简化`StockTickerHub`和`StockTicker`类。</span><span class="sxs-lookup"><span data-stu-id="03986-156">First, let's simplify the `StockTickerHub` and `StockTicker` classes.</span></span> <span data-ttu-id="03986-157">在下面的代码中，我已注释掉的部分，我们不需要。</span><span class="sxs-lookup"><span data-stu-id="03986-157">In the following code, I've commented out the parts that we don't need.</span></span>

<span data-ttu-id="03986-158">移除无参数构造函数从`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="03986-158">Remove the parameterless constructor from `StockTicker`.</span></span> <span data-ttu-id="03986-159">相反，我们将始终使用 DI 来创建中心。</span><span class="sxs-lookup"><span data-stu-id="03986-159">Instead, we will always use DI to create the hub.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

<span data-ttu-id="03986-160">对于 StockTicker，移除的单一实例。</span><span class="sxs-lookup"><span data-stu-id="03986-160">For StockTicker, remove the singleton instance.</span></span> <span data-ttu-id="03986-161">更高版本，我们将使用 IoC 容器来控制 StockTicker 生存期。</span><span class="sxs-lookup"><span data-stu-id="03986-161">Later, we'll use the IoC container to control the StockTicker lifetime.</span></span> <span data-ttu-id="03986-162">此外，请公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="03986-162">Also, make the constructor public.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

<span data-ttu-id="03986-163">接下来，我们可以通过创建一个接口，使重构代码`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="03986-163">Next, we can refactor the code by creating an interface for `StockTicker`.</span></span> <span data-ttu-id="03986-164">我们将使用此接口来分离`StockTickerHub`从`StockTicker`类。</span><span class="sxs-lookup"><span data-stu-id="03986-164">We'll use this interface to decouple the `StockTickerHub` from the `StockTicker` class.</span></span>

<span data-ttu-id="03986-165">Visual Studio 使此类型的重构变得简单。</span><span class="sxs-lookup"><span data-stu-id="03986-165">Visual Studio makes this kind of refactoring easy.</span></span> <span data-ttu-id="03986-166">打开文件 StockTicker.cs，右键单击`StockTicker`类声明，然后选择**重构**...**提取接口**。</span><span class="sxs-lookup"><span data-stu-id="03986-166">Open the file StockTicker.cs, right-click on the `StockTicker` class declaration, and select **Refactor** ... **Extract Interface**.</span></span>

![](dependency-injection/_static/image1.png)

<span data-ttu-id="03986-167">在**提取接口**对话框中，单击**选择所有**。</span><span class="sxs-lookup"><span data-stu-id="03986-167">In the **Extract Interface** dialog, click **Select All**.</span></span> <span data-ttu-id="03986-168">保留其他默认值。</span><span class="sxs-lookup"><span data-stu-id="03986-168">Leave the other defaults.</span></span> <span data-ttu-id="03986-169">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="03986-169">Click **OK**.</span></span>

![](dependency-injection/_static/image2.png)

<span data-ttu-id="03986-170">Visual Studio 将创建名为的新接口`IStockTicker`，也会更改和`StockTicker`为派生自`IStockTicker`。</span><span class="sxs-lookup"><span data-stu-id="03986-170">Visual Studio creates a new interface named `IStockTicker`, and also changes `StockTicker` to derive from `IStockTicker`.</span></span>

<span data-ttu-id="03986-171">打开文件 IStockTicker.cs 和更改的接口**公共**。</span><span class="sxs-lookup"><span data-stu-id="03986-171">Open the file IStockTicker.cs and change the interface to **public**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

<span data-ttu-id="03986-172">在`StockTickerHub`类中，更改的两个实例`StockTicker`到`IStockTicker`:</span><span class="sxs-lookup"><span data-stu-id="03986-172">In the `StockTickerHub` class, change the two instances of `StockTicker` to `IStockTicker`:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

<span data-ttu-id="03986-173">创建`IStockTicker`接口不是绝对必需的但我希望演示如何 DI 可帮助降低应用程序中的组件之间的耦合。</span><span class="sxs-lookup"><span data-stu-id="03986-173">Creating an `IStockTicker` interface isn't strictly necessary, but I wanted to show how DI can help to reduce coupling between components in your application.</span></span>

## <a name="add-the-ninject-library"></a><span data-ttu-id="03986-174">添加 Ninject 库</span><span class="sxs-lookup"><span data-stu-id="03986-174">Add the Ninject Library</span></span>

<span data-ttu-id="03986-175">有多个适用于.NET 的开源 IoC 容器。</span><span class="sxs-lookup"><span data-stu-id="03986-175">There are many open-source IoC containers for .NET.</span></span> <span data-ttu-id="03986-176">对于本教程中，我将使用[Ninject](http://www.ninject.org/)。</span><span class="sxs-lookup"><span data-stu-id="03986-176">For this tutorial, I'll use [Ninject](http://www.ninject.org/).</span></span> <span data-ttu-id="03986-177">(其他常用库包括[城堡 Windsor](http://www.castleproject.org/)， [Spring.Net](http://www.springframework.net/)， [Autofac](https://code.google.com/p/autofac/)， [Unity](https://github.com/unitycontainer/unity)，和[StructureMap](http://docs.structuremap.net).)</span><span class="sxs-lookup"><span data-stu-id="03986-177">(Other popular libraries include [Castle Windsor](http://www.castleproject.org/), [Spring.Net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity), and [StructureMap](http://docs.structuremap.net).)</span></span>

<span data-ttu-id="03986-178">使用 NuGet 包管理器安装[Ninject 库](https://nuget.org/packages/Ninject/3.0.1.10)。</span><span class="sxs-lookup"><span data-stu-id="03986-178">Use NuGet Package Manager to install the [Ninject library](https://nuget.org/packages/Ninject/3.0.1.10).</span></span> <span data-ttu-id="03986-179">在 Visual Studio 中，从**工具**菜单中选择**库程序包管理器** | **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="03986-179">In Visual Studio, from the **Tools** menu select **Library Package Manager** | **Package Manager Console**.</span></span> <span data-ttu-id="03986-180">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="03986-180">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a><span data-ttu-id="03986-181">替换 SignalR 依赖项解析程序</span><span class="sxs-lookup"><span data-stu-id="03986-181">Replace the SignalR Dependency Resolver</span></span>

<span data-ttu-id="03986-182">若要使用 Ninject SignalR 内的，创建派生自的类**DefaultDependencyResolver**。</span><span class="sxs-lookup"><span data-stu-id="03986-182">To use Ninject within SignalR, create a class that derives from **DefaultDependencyResolver**.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

<span data-ttu-id="03986-183">此类重写**GetService**和**GetServices**方法**DefaultDependencyResolver**。</span><span class="sxs-lookup"><span data-stu-id="03986-183">This class overrides the **GetService** and **GetServices** methods of **DefaultDependencyResolver**.</span></span> <span data-ttu-id="03986-184">SignalR 调用这些方法来创建在运行时，包括中心实例，以及供内部使用 SignalR 的各种服务的各种对象。</span><span class="sxs-lookup"><span data-stu-id="03986-184">SignalR calls these methods to create various objects at runtime, including hub instances, as well as various services used internally by SignalR.</span></span>

- <span data-ttu-id="03986-185">**GetService**方法创建一种类型的单个实例。</span><span class="sxs-lookup"><span data-stu-id="03986-185">The **GetService** method creates a single instance of a type.</span></span> <span data-ttu-id="03986-186">重写此方法以调用 Ninject 内核**TryGet**方法。</span><span class="sxs-lookup"><span data-stu-id="03986-186">Override this method to call the Ninject kernel's **TryGet** method.</span></span> <span data-ttu-id="03986-187">如果该方法将返回 null，回退到默认冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="03986-187">If that method returns null, fall back to the default resolver.</span></span>
- <span data-ttu-id="03986-188">**GetServices**方法创建指定类型的对象的集合。</span><span class="sxs-lookup"><span data-stu-id="03986-188">The **GetServices** method creates a collection of objects of a specified type.</span></span> <span data-ttu-id="03986-189">重写此方法以从 Ninject 的结果与默认冲突解决程序将结果串联起来。</span><span class="sxs-lookup"><span data-stu-id="03986-189">Override this method to concatenate the results from Ninject with the results from the default resolver.</span></span>

## <a name="configure-ninject-bindings"></a><span data-ttu-id="03986-190">配置 Ninject 绑定</span><span class="sxs-lookup"><span data-stu-id="03986-190">Configure Ninject Bindings</span></span>

<span data-ttu-id="03986-191">现在我们将使用 Ninject 声明类型绑定。</span><span class="sxs-lookup"><span data-stu-id="03986-191">Now we'll use Ninject to declare type bindings.</span></span>

<span data-ttu-id="03986-192">打开文件 RegisterHubs.cs。</span><span class="sxs-lookup"><span data-stu-id="03986-192">Open the file RegisterHubs.cs.</span></span> <span data-ttu-id="03986-193">在`RegisterHubs.Start`方法，创建 Ninject 容器，Ninject 调用*内核*。</span><span class="sxs-lookup"><span data-stu-id="03986-193">In the `RegisterHubs.Start` method, create the Ninject container, which Ninject calls the *kernel*.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

<span data-ttu-id="03986-194">创建我们自定义的依赖项解析程序的实例：</span><span class="sxs-lookup"><span data-stu-id="03986-194">Create an instance of our custom dependency resolver:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

<span data-ttu-id="03986-195">为创建绑定`IStockTicker`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="03986-195">Create a binding for `IStockTicker` as follows:</span></span>

[!code-html[Main](dependency-injection/samples/sample17.html)]

<span data-ttu-id="03986-196">此代码表示以下两项操作。</span><span class="sxs-lookup"><span data-stu-id="03986-196">This code is saying two things.</span></span> <span data-ttu-id="03986-197">首先，每当应用程序需要`IStockTicker`，内核应创建的实例`StockTicker`。</span><span class="sxs-lookup"><span data-stu-id="03986-197">First, whenever the application needs an `IStockTicker`, the kernel should create an instance of `StockTicker`.</span></span> <span data-ttu-id="03986-198">第二个，`StockTicker`类应创建为单一实例对象。</span><span class="sxs-lookup"><span data-stu-id="03986-198">Second, the `StockTicker` class should be a created as a singleton object.</span></span> <span data-ttu-id="03986-199">Ninject 将创建的对象的一个实例，并返回相同的实例为每个请求。</span><span class="sxs-lookup"><span data-stu-id="03986-199">Ninject will create one instance of the object, and return the same instance for each request.</span></span>

<span data-ttu-id="03986-200">为创建绑定**IHubConnectionContext** ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="03986-200">Create a binding for **IHubConnectionContext** as follows:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

<span data-ttu-id="03986-201">此代码 creatres 返回一个匿名函数**IHubConnection**。</span><span class="sxs-lookup"><span data-stu-id="03986-201">This code creatres an anonymous function that returns an **IHubConnection**.</span></span> <span data-ttu-id="03986-202">**WhenInjectedInto**方法告知 Ninject 若要使用此函数仅在创建时`IStockTicker`实例。</span><span class="sxs-lookup"><span data-stu-id="03986-202">The **WhenInjectedInto** method tells Ninject to use this function only when creating `IStockTicker` instances.</span></span> <span data-ttu-id="03986-203">原因是 SignalR 创建**IHubConnectionContext**内部，实例，但我们不希望重写 SignalR 如何创建它们。</span><span class="sxs-lookup"><span data-stu-id="03986-203">The reason is that SignalR creates **IHubConnectionContext** instances internally, and we don't want to override how SignalR creates them.</span></span> <span data-ttu-id="03986-204">此函数仅适用于我们`StockTicker`类。</span><span class="sxs-lookup"><span data-stu-id="03986-204">This function only applies to our `StockTicker` class.</span></span>

<span data-ttu-id="03986-205">传递到依赖项解析程序**MapHubs**方法：</span><span class="sxs-lookup"><span data-stu-id="03986-205">Pass the dependency resolver into the **MapHubs** method:</span></span>

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

<span data-ttu-id="03986-206">现在 SignalR 会使用中指定的冲突解决程序**MapHubs**，而不是默认冲突解决程序。</span><span class="sxs-lookup"><span data-stu-id="03986-206">Now SignalR will use the resolver specified in **MapHubs**, instead of the default resolver.</span></span>

<span data-ttu-id="03986-207">下面是完整代码清单`RegisterHubs.Start`。</span><span class="sxs-lookup"><span data-stu-id="03986-207">Here is the complete code listing for `RegisterHubs.Start`.</span></span>

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

<span data-ttu-id="03986-208">若要在 Visual Studio 中运行 StockTicker 应用程序，按 F5。</span><span class="sxs-lookup"><span data-stu-id="03986-208">To run the StockTicker application in Visual Studio, press F5.</span></span> <span data-ttu-id="03986-209">在浏览器窗口中，导航到`http://localhost:*port*/SignalR.Sample/StockTicker.html`。</span><span class="sxs-lookup"><span data-stu-id="03986-209">In the browser window, navigate to `http://localhost:*port*/SignalR.Sample/StockTicker.html`.</span></span>

![](dependency-injection/_static/image3.png)

<span data-ttu-id="03986-210">该应用程序功能和以前完全相同。</span><span class="sxs-lookup"><span data-stu-id="03986-210">The application has exactly the same functionality as before.</span></span> <span data-ttu-id="03986-211">(有关的说明，请参阅[服务器广播使用 ASP.NET SignalR](index.md)。)我们尚未更改的行为;刚才更轻松地测试、 维护和改进的代码。</span><span class="sxs-lookup"><span data-stu-id="03986-211">(For a description, see [Server Broadcast with ASP.NET SignalR](index.md).) We haven't changed the behavior; just made the code easier to test, maintain, and evolve.</span></span>
