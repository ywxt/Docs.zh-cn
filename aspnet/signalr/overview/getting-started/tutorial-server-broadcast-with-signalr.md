---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 教程： 使用 signalr 2 实现服务器的广播 |Microsoft Docs
author: tdykstra
description: 本教程演示如何创建使用 ASP.NET SignalR 2 来提供服务器广播的功能的 web 应用程序。 服务器广播意味着该 commun...
ms.author: aspnetcontent
ms.date: 10/13/2014
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 0e86fbea9c5668e20fce7a494c76c52f9c089c09
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37820692"
---
<a name="tutorial-server-broadcast-with-signalr-2"></a><span data-ttu-id="07000-104">教程： 使用 signalr 2 实现广播的服务器</span><span class="sxs-lookup"><span data-stu-id="07000-104">Tutorial: Server Broadcast with SignalR 2</span></span>
====================
<span data-ttu-id="07000-105">通过[Tom Dykstra](https://github.com/tdykstra)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="07000-105">by [Tom Dykstra](https://github.com/tdykstra), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="07000-106">本教程演示如何创建使用 ASP.NET SignalR 2 来提供服务器广播的功能的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="07000-106">This tutorial shows how to create a web application that uses ASP.NET SignalR 2 to provide server broadcast functionality.</span></span> <span data-ttu-id="07000-107">服务器广播意味着发送到客户端的通信由服务器启动。</span><span class="sxs-lookup"><span data-stu-id="07000-107">Server broadcast means that communications sent to clients are initiated by the server.</span></span> <span data-ttu-id="07000-108">这种情况要求不同的编程方式对等方案，例如聊天应用程序，在其中发送到客户端的通信都是由一个或多个客户端。</span><span class="sxs-lookup"><span data-stu-id="07000-108">This scenario requires a different programming approach than peer-to-peer scenarios such as chat applications, in which communications sent to clients are initiated by one or more of the clients.</span></span>
> 
> <span data-ttu-id="07000-109">你将在本教程中创建的应用程序模拟股票行情服务器广播功能的典型方案。</span><span class="sxs-lookup"><span data-stu-id="07000-109">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span>
> 
> <span data-ttu-id="07000-110">本主题是最初编写的 Patrick Fletcher。</span><span class="sxs-lookup"><span data-stu-id="07000-110">This topic was originally written by Patrick Fletcher.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="07000-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="07000-111">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="07000-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="07000-112">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="07000-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="07000-113">.NET 4.5</span></span>
> - <span data-ttu-id="07000-114">SignalR 版本 2</span><span class="sxs-lookup"><span data-stu-id="07000-114">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="07000-115">本教程使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="07000-115">Using Visual Studio 2012 with this tutorial</span></span>
> 
> 
> <span data-ttu-id="07000-116">若要学习本教程使用 Visual Studio 2012，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="07000-116">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
> 
> - <span data-ttu-id="07000-117">更新你[程序包管理器](http://docs.nuget.org/docs/start-here/installing-nuget)到最新版本。</span><span class="sxs-lookup"><span data-stu-id="07000-117">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="07000-118">安装[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="07000-118">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="07000-119">在 Web 平台安装程序中，搜索并安装**ASP.NET 和 Web 工具 2013.1 适用于 Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="07000-119">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="07000-120">这将安装 Visual Studio 模板的 SignalR 类，如**中心**。</span><span class="sxs-lookup"><span data-stu-id="07000-120">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="07000-121">某些模板 (如**OWIN 启动类**) 将不可用; 对于这些数据，改为使用的类文件。</span><span class="sxs-lookup"><span data-stu-id="07000-121">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="07000-122">教程版本</span><span class="sxs-lookup"><span data-stu-id="07000-122">Tutorial Versions</span></span>
> 
> <span data-ttu-id="07000-123">有关 SignalR 的早期版本的信息，请参阅[SignalR 较早版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="07000-123">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="07000-124">问题和提出的意见</span><span class="sxs-lookup"><span data-stu-id="07000-124">Questions and comments</span></span>
> 
> <span data-ttu-id="07000-125">请在你喜欢本教程的内容以及我们可以改进的页的底部的评论中留下反馈。</span><span class="sxs-lookup"><span data-stu-id="07000-125">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="07000-126">如果你有与本教程不直接相关的问题，你可以发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="07000-126">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>


## <a name="overview"></a><span data-ttu-id="07000-127">概述</span><span class="sxs-lookup"><span data-stu-id="07000-127">Overview</span></span>

<span data-ttu-id="07000-128">在本教程中，将创建的实时应用程序想要定期"推送"的具有代表性的股票行情自动收录器应用程序或广播到所有连接的客户端将通知从服务器。</span><span class="sxs-lookup"><span data-stu-id="07000-128">In this tutorial, you'll create a stock ticker application that is representative of real-time applications in which you want to periodically "push," or broadcast, notifications from the server to all connected clients.</span></span> <span data-ttu-id="07000-129">在本教程的第一部分，将从零开始创建该应用程序的简化的版本。</span><span class="sxs-lookup"><span data-stu-id="07000-129">In the first part of this tutorial, you'll create a simplified version of that application from scratch.</span></span> <span data-ttu-id="07000-130">在本教程的其余部分，将安装 NuGet 包，它包含其他功能，查看这些功能的代码。</span><span class="sxs-lookup"><span data-stu-id="07000-130">In the remainder of the tutorial, you'll install a NuGet package that contains additional features, and review the code for those features.</span></span>

<span data-ttu-id="07000-131">在本教程的第一部分中将生成的应用程序显示的网格有库存数据。</span><span class="sxs-lookup"><span data-stu-id="07000-131">The application that you'll build in the first part of this tutorial displays a grid with stock data.</span></span>

![StockTicker 初始版本](tutorial-server-broadcast-with-signalr/_static/image1.png)

<span data-ttu-id="07000-133">定期服务器随机更新股票价格，并将更新推送到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="07000-133">Periodically the server randomly updates stock prices and pushes the updates to all connected clients.</span></span> <span data-ttu-id="07000-134">在浏览器数字和中的符号**更改**并**%** 列动态更改以响应来自服务器的通知。</span><span class="sxs-lookup"><span data-stu-id="07000-134">In the browser the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="07000-135">如果您打开其他浏览器相同的 URL，它们都同时显示相同的数据和对数据的相同更改。</span><span class="sxs-lookup"><span data-stu-id="07000-135">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

<span data-ttu-id="07000-136">本教程包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="07000-136">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="07000-137">先决条件</span><span class="sxs-lookup"><span data-stu-id="07000-137">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="07000-138">创建项目</span><span class="sxs-lookup"><span data-stu-id="07000-138">Create the project</span></span>](#createproject)
- [<span data-ttu-id="07000-139">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="07000-139">Set up the server code</span></span>](#server)
- [<span data-ttu-id="07000-140">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="07000-140">Set up the client code</span></span>](#client)
- [<span data-ttu-id="07000-141">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="07000-141">Test the application</span></span>](#test)
- [<span data-ttu-id="07000-142">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="07000-142">Enable logging</span></span>](#enablelogging)
- [<span data-ttu-id="07000-143">安装和查看完整的 StockTicker 示例</span><span class="sxs-lookup"><span data-stu-id="07000-143">Install and review the full StockTicker sample</span></span>](#fullsample)
- [<span data-ttu-id="07000-144">后续步骤</span><span class="sxs-lookup"><span data-stu-id="07000-144">Next steps</span></span>](#nextsteps)

<span data-ttu-id="07000-145">[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 包安装 Visual Studio 项目中的示例模拟股票行情自动收录器应用程序。</span><span class="sxs-lookup"><span data-stu-id="07000-145">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package installs a sample simulated stock ticker application in a Visual Studio project.</span></span>

> [!NOTE]
> <span data-ttu-id="07000-146">如果不想要逐步完成构建应用程序的步骤，你可以在新的空的 ASP.NET Web 应用程序项目中安装 SignalR.Sample 包。</span><span class="sxs-lookup"><span data-stu-id="07000-146">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new Empty ASP.NET Web Application project.</span></span> <span data-ttu-id="07000-147">如果不执行本教程中的步骤安装 NuGet 包**必须遵循 readme.txt 文件中的说明**。</span><span class="sxs-lookup"><span data-stu-id="07000-147">If you install the NuGet package without performing the steps in this tutorial, **you must follow the instructions in the readme.txt file**.</span></span> <span data-ttu-id="07000-148">若要运行包需要添加 OWIN 启动类的调用中已安装的程序包 ConfigureSignalR 方法。</span><span class="sxs-lookup"><span data-stu-id="07000-148">To run the package you need to add an OWIN startup class which calls the ConfigureSignalR method in the installed package.</span></span> <span data-ttu-id="07000-149">如果不添加 OWIN 启动类，将收到错误。</span><span class="sxs-lookup"><span data-stu-id="07000-149">You will receive an error if you do not add the OWIN startup class.</span></span>


<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="07000-150">系统必备</span><span class="sxs-lookup"><span data-stu-id="07000-150">Prerequisites</span></span>

<span data-ttu-id="07000-151">在开始之前，请确保已在计算机上安装的 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="07000-151">Before you start, make sure that you have Visual Studio 2013 installed on your computer.</span></span> <span data-ttu-id="07000-152">如果未安装 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)若要获取免费的 Visual Studio 2013 Express。</span><span class="sxs-lookup"><span data-stu-id="07000-152">If you don't have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2013 Express.</span></span>

<a id="createproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="07000-153">创建项目</span><span class="sxs-lookup"><span data-stu-id="07000-153">Create the project</span></span>

1. <span data-ttu-id="07000-154">从**文件**菜单上，单击**新项目**。</span><span class="sxs-lookup"><span data-stu-id="07000-154">From the **File** menu, click **New Project**.</span></span>
2. <span data-ttu-id="07000-155">在中**新的项目**对话框框中，展开**C#** 下**模板**，然后选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="07000-155">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="07000-156">选择**ASP.NET 空 Web 应用程序**模板，将项目命名*SignalR.StockTicker*，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="07000-156">Select the **ASP.NET Empty Web Application** template, name the project *SignalR.StockTicker*, and click **OK**.</span></span>

    ![“新建项目”对话框](tutorial-server-broadcast-with-signalr/_static/image2.png)
4. <span data-ttu-id="07000-158">在中**新的 ASP.NET**项目窗口中，保留**空**选中然后单击**创建项目**。</span><span class="sxs-lookup"><span data-stu-id="07000-158">In the **New ASP.NET** Project window, leave **Empty** selected and click **Create Project**.</span></span>

    ![新建 ASP 项目对话框](tutorial-server-broadcast-with-signalr/_static/image3.png)

<a id="server"></a>

## <a name="set-up-the-server-code"></a><span data-ttu-id="07000-160">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="07000-160">Set up the server code</span></span>

<span data-ttu-id="07000-161">在本部分中，设置在服务器运行的代码。</span><span class="sxs-lookup"><span data-stu-id="07000-161">In this section you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="07000-162">创建 Stock 类</span><span class="sxs-lookup"><span data-stu-id="07000-162">Create the Stock class</span></span>

<span data-ttu-id="07000-163">首先创建将用于存储和传输有关股票的信息的股票模型类。</span><span class="sxs-lookup"><span data-stu-id="07000-163">You begin by creating the Stock model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="07000-164">在项目文件夹中创建一个新类文件，将其命名*Stock.cs*，然后使用以下代码替换模板代码：</span><span class="sxs-lookup"><span data-stu-id="07000-164">Create a new class file in the project folder, name it *Stock.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    <span data-ttu-id="07000-165">在创建股票时将设置的两个属性是符号 (例如，Microsoft 的 MSFT) 和价格。</span><span class="sxs-lookup"><span data-stu-id="07000-165">The two properties that you'll set when you create stocks are the Symbol (for example, MSFT for Microsoft) and the Price.</span></span> <span data-ttu-id="07000-166">其他属性取决于如何以及何时设置价格。</span><span class="sxs-lookup"><span data-stu-id="07000-166">The other properties depend on how and when you set Price.</span></span> <span data-ttu-id="07000-167">设置价格，第一次的值获取传播到 DayOpen。</span><span class="sxs-lookup"><span data-stu-id="07000-167">The first time you set Price, the value gets propagated to DayOpen.</span></span> <span data-ttu-id="07000-168">当设置价格，更改并且 PercentChange 属性值进行计算的后续时间基于价格和 DayOpen 之间的差异。</span><span class="sxs-lookup"><span data-stu-id="07000-168">Subsequent times when you set Price, the Change and PercentChange property values are calculated based on the difference between Price and DayOpen.</span></span>

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a><span data-ttu-id="07000-169">创建在 StockTicker 和 StockTickerHub 类</span><span class="sxs-lookup"><span data-stu-id="07000-169">Create the StockTicker and StockTickerHub classes</span></span>

<span data-ttu-id="07000-170">SignalR 中心 API 将用于处理服务器到客户端交互。</span><span class="sxs-lookup"><span data-stu-id="07000-170">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="07000-171">从 SignalR Hub 类派生的 StockTickerHub 类将处理来自客户端接收连接和方法调用。</span><span class="sxs-lookup"><span data-stu-id="07000-171">A StockTickerHub class that derives from the SignalR Hub class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="07000-172">此外需要维护股票数据并运行计时器对象，以定期触发价格更新，独立于客户端连接。</span><span class="sxs-lookup"><span data-stu-id="07000-172">You also need to maintain stock data and run a Timer object to periodically trigger price updates, independently of client connections.</span></span> <span data-ttu-id="07000-173">因为中心实例是瞬态的不能置于 Hub 类，这些函数。</span><span class="sxs-lookup"><span data-stu-id="07000-173">You can't put these functions in a Hub class, because Hub instances are transient.</span></span> <span data-ttu-id="07000-174">为每个操作的中心，例如连接和从客户端对服务器的调用创建的中心类实例。</span><span class="sxs-lookup"><span data-stu-id="07000-174">A Hub class instance is created for each operation on the hub, such as connections and calls from the client to the server.</span></span> <span data-ttu-id="07000-175">因此，必须运行在单独的类，您将命名为 StockTicker 的机制，可保护库存数据，更新价格，并会广播价格更新。</span><span class="sxs-lookup"><span data-stu-id="07000-175">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class, which you'll name StockTicker.</span></span>

![从 StockTicker 的广播](tutorial-server-broadcast-with-signalr/_static/image5.png)

<span data-ttu-id="07000-177">您只想要运行的服务器上，因此将需要的单个 StockTicker 实例中设置从每个 StockTickerHub 实例引用的 StockTicker 类的一个实例。</span><span class="sxs-lookup"><span data-stu-id="07000-177">You only want one instance of the StockTicker class to run on the server, so you'll need to set up a reference from each StockTickerHub instance to the singleton StockTicker instance.</span></span> <span data-ttu-id="07000-178">StockTicker 类必须可以广播到客户端，因为它具有股票数据并触发更新，但 StockTicker 不是 Hub 类。</span><span class="sxs-lookup"><span data-stu-id="07000-178">The StockTicker class has to be able to broadcast to clients because it has the stock data and triggers updates, but StockTicker is not a Hub class.</span></span> <span data-ttu-id="07000-179">因此，StockTicker 类必须获取对 SignalR Hub 连接上下文对象的引用。</span><span class="sxs-lookup"><span data-stu-id="07000-179">Therefore, the StockTicker class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="07000-180">然后，它可以使用 SignalR 连接上下文对象广播到客户端。</span><span class="sxs-lookup"><span data-stu-id="07000-180">It can then use the SignalR connection context object to broadcast to clients.</span></span>

1. <span data-ttu-id="07000-181">在中**解决方案资源管理器**，右键单击项目，然后单击**添加 |SignalR Hub 类 (v2)**。</span><span class="sxs-lookup"><span data-stu-id="07000-181">In **Solution Explorer**, right-click the project and click **Add | SignalR Hub Class (v2)**.</span></span>
2. <span data-ttu-id="07000-182">命名新集线器*StockTickerHub.cs*，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="07000-182">Name the new hub *StockTickerHub.cs*, and then click **Add**.</span></span> <span data-ttu-id="07000-183">SignalR NuGet 包将添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="07000-183">SignalR NuGet packages will be added to your project.</span></span>
3. <span data-ttu-id="07000-184">模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="07000-184">Replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

    <span data-ttu-id="07000-185">[中心](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)类用于定义客户端可以调用在服务器的方法。</span><span class="sxs-lookup"><span data-stu-id="07000-185">The [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class is used to define methods the clients can call on the server.</span></span> <span data-ttu-id="07000-186">要定义一种方法： `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="07000-186">You are defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="07000-187">当客户端最初连接到服务器时，它将调用此方法以获取所有其当前价格股票的列表。</span><span class="sxs-lookup"><span data-stu-id="07000-187">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="07000-188">该方法可以同步执行并返回`IEnumerable<Stock>`由于它会从内存中返回数据。</span><span class="sxs-lookup"><span data-stu-id="07000-188">The method can execute synchronously and return `IEnumerable<Stock>` because it is returning data from memory.</span></span> <span data-ttu-id="07000-189">如果该方法必须通过执行将涉及等待，如数据库查找或 web 服务调用，获取的数据则会指定`Task<IEnumerable<Stock>>`作为返回值以启用异步处理。</span><span class="sxs-lookup"><span data-stu-id="07000-189">If the method had to get the data by doing something that would involve waiting, such as a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="07000-190">有关详细信息，请参阅[ASP.NET SignalR 中心 API 指南-服务器-时要异步执行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。</span><span class="sxs-lookup"><span data-stu-id="07000-190">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).</span></span>

    <span data-ttu-id="07000-191">HubName 属性指定将如何在客户端上的 JavaScript 代码中引用该中心。</span><span class="sxs-lookup"><span data-stu-id="07000-191">The HubName attribute specifies how the Hub will be referenced in JavaScript code on the client.</span></span> <span data-ttu-id="07000-192">如果不使用此属性在客户端上的默认名称是类名称，在这种情况下是 stockTickerHub 驼峰式大小写版本。</span><span class="sxs-lookup"><span data-stu-id="07000-192">The default name on the client if you don't use this attribute is a camel-cased version of the class name, which in this case would be stockTickerHub.</span></span>

    <span data-ttu-id="07000-193">正如您将看到更高版本创建 StockTicker 类时，在其静态实例属性中创建该类的单一实例。</span><span class="sxs-lookup"><span data-stu-id="07000-193">As you'll see later when you create the StockTicker class, a singleton instance of that class is created in its static Instance property.</span></span> <span data-ttu-id="07000-194">StockTicker 的单一实例保持在多少个客户端连接或断开连接，无论内存中，该实例是 GetAllStocks 方法用于返回当前股票信息。</span><span class="sxs-lookup"><span data-stu-id="07000-194">That singleton instance of StockTicker remains in memory no matter how many clients connect or disconnect, and that instance is what the GetAllStocks method uses to return current stock information.</span></span>
4. <span data-ttu-id="07000-195">在项目文件夹中创建一个新类文件，将其命名*StockTicker.cs*，然后使用以下代码替换模板代码：</span><span class="sxs-lookup"><span data-stu-id="07000-195">Create a new class file in the project folder, name it *StockTicker.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

    <span data-ttu-id="07000-196">由于多个线程将运行 StockTicker 代码的同一个实例，StockTicker 类必须是 threadsafe。</span><span class="sxs-lookup"><span data-stu-id="07000-196">Since multiple threads will be running the same instance of StockTicker code, the StockTicker class has to be threadsafe.</span></span>

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="07000-197">在静态字段中存储的单一实例</span><span class="sxs-lookup"><span data-stu-id="07000-197">Storing the singleton instance in a static field</span></span>

    <span data-ttu-id="07000-198">此代码初始化静态\_支持的类，并且此实例的实例属性的实例字段是可以创建类的唯一实例，因为构造函数标记为私有。</span><span class="sxs-lookup"><span data-stu-id="07000-198">The code initializes the static \_instance field that backs the Instance property with an instance of the class, and this is the only instance of the class that can be created, because the constructor is marked as private.</span></span> <span data-ttu-id="07000-199">[迟缓初始化](https://msdn.microsoft.com/library/dd997286.aspx)用于\_实例字段，不出于性能原因，但若要确保创建的实例是 threadsafe。</span><span class="sxs-lookup"><span data-stu-id="07000-199">[Lazy initialization](https://msdn.microsoft.com/library/dd997286.aspx) is used for the \_instance field, not for performance reasons but to ensure that the instance creation is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

    <span data-ttu-id="07000-200">客户端连接到服务器，每次在一个单独的线程中运行的 StockTickerHub 类的新实例获取的 StockTicker 单一实例从 StockTicker.Instance 静态属性，如前面在 StockTickerHub 类中看到。</span><span class="sxs-lookup"><span data-stu-id="07000-200">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the StockTicker.Instance static property, as you saw earlier in the StockTickerHub class.</span></span>

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="07000-201">在 ConcurrentDictionary 中存储常用的数据</span><span class="sxs-lookup"><span data-stu-id="07000-201">Storing stock data in a ConcurrentDictionary</span></span>

    <span data-ttu-id="07000-202">构造函数初始化\_具有一些示例股票数据和 GetAllStocks 股票集合返回股票。</span><span class="sxs-lookup"><span data-stu-id="07000-202">The constructor initializes the \_stocks collection with some sample stock data, and GetAllStocks returns the stocks.</span></span> <span data-ttu-id="07000-203">如上文所，StockTickerHub.GetAllStocks 这是客户端可以调用的中心类中的服务器方法又会返回股票的此集合。</span><span class="sxs-lookup"><span data-stu-id="07000-203">As you saw earlier, this collection of stocks is in turn returned by StockTickerHub.GetAllStocks which is a server method in the Hub class that clients can call.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

    <span data-ttu-id="07000-204">股票集合指[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)线程安全的类型。</span><span class="sxs-lookup"><span data-stu-id="07000-204">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="07000-205">作为替代方法，您可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)对象，并显式锁定字典时对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="07000-205">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

    <span data-ttu-id="07000-206">对于此示例应用程序，它是确定在内存中存储应用程序数据并释放 StockTicker 实例时丢失数据。</span><span class="sxs-lookup"><span data-stu-id="07000-206">For this sample application, it's OK to store application data in memory and to lose the data when the StockTicker instance is disposed.</span></span> <span data-ttu-id="07000-207">在实际的应用程序将如何使用后端数据存储，如数据库。</span><span class="sxs-lookup"><span data-stu-id="07000-207">In a real application you would work with a back-end data store such as a database.</span></span>

    ### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="07000-208">定期更新股票价格</span><span class="sxs-lookup"><span data-stu-id="07000-208">Periodically updating stock prices</span></span>

    <span data-ttu-id="07000-209">构造函数启动定期调用的方法，更新基于随机的股票价格的计时器对象。</span><span class="sxs-lookup"><span data-stu-id="07000-209">The constructor starts up a Timer object that periodically calls methods that update stock prices on a random basis.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

    <span data-ttu-id="07000-210">UpdateStockPrices 由计时器，该参数中的 null 将传入调用。</span><span class="sxs-lookup"><span data-stu-id="07000-210">UpdateStockPrices is called by the Timer, which passes in null in the state parameter.</span></span> <span data-ttu-id="07000-211">在更新之前的价格，采用锁\_updateStockPricesLock 对象。</span><span class="sxs-lookup"><span data-stu-id="07000-211">Before updating prices, a lock is taken on the \_updateStockPricesLock object.</span></span> <span data-ttu-id="07000-212">如果另一个线程已更新的价格，，然后在列表中每个股票调用 TryUpdateStockPrice 会检查代码。</span><span class="sxs-lookup"><span data-stu-id="07000-212">The code checks if another thread is already updating prices, and then it calls TryUpdateStockPrice on each stock in the list.</span></span> <span data-ttu-id="07000-213">TryUpdateStockPrice 方法决定是否要更改的股票价格和要对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="07000-213">The TryUpdateStockPrice method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="07000-214">如果股票价格已更改，调用 BroadcastStockPrice 广播到所有连接的客户端进行的股票价格更改。</span><span class="sxs-lookup"><span data-stu-id="07000-214">If the stock price is changed, BroadcastStockPrice is called to broadcast the stock price change to all connected clients.</span></span>

    <span data-ttu-id="07000-215">\_UpdatingStockPrices 标志标记为[易失性](https://msdn.microsoft.com/library/x13ttww7.aspx)以确保进行 threadsafe 到它的访问。</span><span class="sxs-lookup"><span data-stu-id="07000-215">The \_updatingStockPrices flag is marked as [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to ensure that access to it is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

    <span data-ttu-id="07000-216">在实际的应用程序，TryUpdateStockPrice 方法需要调用 web 服务，以便查找价格上涨。它在此代码中使用的随机数生成器随机进行更改。</span><span class="sxs-lookup"><span data-stu-id="07000-216">In a real application, the TryUpdateStockPrice method would call a web service to look up the price; in this code it uses a random number generator to make changes randomly.</span></span>

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="07000-217">获取 SignalR 上下文，以便 StockTicker 类可以广播到客户端</span><span class="sxs-lookup"><span data-stu-id="07000-217">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

    <span data-ttu-id="07000-218">因为价格更改来自此处 StockTicker 对象，所以这是需要在所有连接的客户端上调用 updateStockPrice 方法的对象。</span><span class="sxs-lookup"><span data-stu-id="07000-218">Because the price changes originate here in the StockTicker object, this is the object that needs to call an updateStockPrice method on all connected clients.</span></span> <span data-ttu-id="07000-219">用于调用客户端的方法，Hub 类中有一个 API，但 StockTicker 不从 Hub 类派生，但尚未对任何集线器对象的引用。</span><span class="sxs-lookup"><span data-stu-id="07000-219">In a Hub class you have an API for calling client methods, but StockTicker does not derive from the Hub class and does not have a reference to any Hub object.</span></span> <span data-ttu-id="07000-220">因此，若要将广播到连接的客户端，StockTicker 类必须 StockTickerHub 类获取 SignalR 上下文实例并使用它来在客户端上调用方法。</span><span class="sxs-lookup"><span data-stu-id="07000-220">Therefore, in order to broadcast to connected clients, the StockTicker class has to get the SignalR context instance for the StockTickerHub class and use that to call methods on clients.</span></span>

    <span data-ttu-id="07000-221">该代码获取对 SignalR 上下文的引用时创建的单一类实例，将引用传递给构造函数中，并构造函数将其放入客户端属性。</span><span class="sxs-lookup"><span data-stu-id="07000-221">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the Clients property.</span></span>

    <span data-ttu-id="07000-222">有两个原因你希望只需一次获取上下文的理由： 获取上下文是代价高昂的操作，并一次获取将确保消息发送到客户端的预期的顺序得到保留。</span><span class="sxs-lookup"><span data-stu-id="07000-222">There are two reasons why you want to get the context just once: getting the context is an expensive operation, and getting it once ensures that the intended order of messages sent to clients is preserved.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

    <span data-ttu-id="07000-223">获取上下文的客户端属性并将其置于 StockTickerClient 属性中可编写代码来调用方法的客户端中的中心类一样外观相同。</span><span class="sxs-lookup"><span data-stu-id="07000-223">Getting the Clients property of the context and putting it in the StockTickerClient property lets you write code to call client methods that looks the same as it would in a Hub class.</span></span> <span data-ttu-id="07000-224">例如，若要将广播到所有客户端可以编写 Clients.All.updateStockPrice(stock)。</span><span class="sxs-lookup"><span data-stu-id="07000-224">For instance, to broadcast to all clients you can write Clients.All.updateStockPrice(stock).</span></span>

    <span data-ttu-id="07000-225">在调用 BroadcastStockPrice updateStockPrice 方法尚不存在;在编写客户端上运行的代码时，你将从更高版本添加它。</span><span class="sxs-lookup"><span data-stu-id="07000-225">The updateStockPrice method that you are calling in BroadcastStockPrice doesn't exist yet; you'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="07000-226">因为 Clients.All 是动态的这意味着将在运行时计算该表达式可以引用 updateStockPrice 此处。</span><span class="sxs-lookup"><span data-stu-id="07000-226">You can refer to updateStockPrice here because Clients.All is dynamic, which means the expression will be evaluated at runtime.</span></span> <span data-ttu-id="07000-227">当此方法调用执行时，SignalR 将发送方法名称和参数值到客户端，并在客户端有一个名为 updateStockPrice 方法，将调用该方法和参数值将传递给它。</span><span class="sxs-lookup"><span data-stu-id="07000-227">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named updateStockPrice, that method will be called and the parameter value will be passed to it.</span></span>

    <span data-ttu-id="07000-228">Clients.All 意味着将发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="07000-228">Clients.All means send to all clients.</span></span> <span data-ttu-id="07000-229">SignalR 提供其他选项来指定哪些客户端或客户端将发送到的组。</span><span class="sxs-lookup"><span data-stu-id="07000-229">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="07000-230">有关详细信息，请参阅[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="07000-230">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="07000-231">注册 SignalR 路由</span><span class="sxs-lookup"><span data-stu-id="07000-231">Register the SignalR route</span></span>

<span data-ttu-id="07000-232">服务器需要知道要截获并将定向到 SignalR 的 URL。</span><span class="sxs-lookup"><span data-stu-id="07000-232">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="07000-233">若要执行此操作，添加 OWIN 启动类：</span><span class="sxs-lookup"><span data-stu-id="07000-233">To do that, add an OWIN startup class:</span></span>

1. <span data-ttu-id="07000-234">在中**解决方案资源管理器**，右键单击该项目，然后单击**添加 |OWIN 启动类**。</span><span class="sxs-lookup"><span data-stu-id="07000-234">In **Solution Explorer**, right-click the project, and then click **Add | OWIN Startup Class**.</span></span> <span data-ttu-id="07000-235">将类命名**Startup.cs**。</span><span class="sxs-lookup"><span data-stu-id="07000-235">Name the class **Startup.cs**.</span></span>
2. <span data-ttu-id="07000-236">中的代码替换**Startup.cs**以下。</span><span class="sxs-lookup"><span data-stu-id="07000-236">Replace the code in **Startup.cs** with the following.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

<span data-ttu-id="07000-237">现在已经完成设置服务器代码。</span><span class="sxs-lookup"><span data-stu-id="07000-237">You have now completed setting up the server code.</span></span> <span data-ttu-id="07000-238">下一节中将设置客户端。</span><span class="sxs-lookup"><span data-stu-id="07000-238">In the next section you'll set up the client.</span></span>

<a id="client"></a>

## <a name="set-up-the-client-code"></a><span data-ttu-id="07000-239">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="07000-239">Set up the client code</span></span>

1. <span data-ttu-id="07000-240">在项目文件夹中，创建一个新的 HTML 文件并将其命名*StockTicker.html*。</span><span class="sxs-lookup"><span data-stu-id="07000-240">Create a new HTML file in the project folder, and name it *StockTicker.html*.</span></span>
2. <span data-ttu-id="07000-241">模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="07000-241">Replace the template code with the following code.</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html)]

    <span data-ttu-id="07000-242">HTML 5 列、 一个标题行，与具有一个单元格跨越所有 5 个列的数据行创建一个表。</span><span class="sxs-lookup"><span data-stu-id="07000-242">The HTML creates a table with 5 columns, a header row, and a data row with a single cell that spans all 5 columns.</span></span> <span data-ttu-id="07000-243">数据行显示"正在加载..."，并暂时不可用时在应用程序启动后，才会显示。</span><span class="sxs-lookup"><span data-stu-id="07000-243">The data row displays "loading..." and will only be shown momentarily when the application starts.</span></span> <span data-ttu-id="07000-244">JavaScript 代码将删除该行，并添加其位置的行中使用从服务器中检索的股票数据。</span><span class="sxs-lookup"><span data-stu-id="07000-244">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="07000-245">脚本标记指定的 jQuery 脚本文件、 SignalR 核心脚本文件、 SignalR 代理脚本文件和更高版本，您将创建一个 StockTicker 脚本文件。</span><span class="sxs-lookup"><span data-stu-id="07000-245">The script tags specify the jQuery script file, the SignalR core script file, the SignalR proxies script file, and a StockTicker script file that you'll create later.</span></span> <span data-ttu-id="07000-246">SignalR 代理脚本文件的说明进行操作，它指定"/ signalr/中心"URL，动态生成，并在这种情况下定义 StockTickerHub.GetAllStocks 的 Hub 类上的方法的代理方法。</span><span class="sxs-lookup"><span data-stu-id="07000-246">The SignalR proxies script file, which specifies the "/signalr/hubs" URL, is dynamically generated and defines proxy methods for the methods on the Hub class, in this case for StockTickerHub.GetAllStocks.</span></span> <span data-ttu-id="07000-247">如果您愿意，您可以通过使用手动生成此 JavaScript 文件[SignalR 实用程序](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)和禁用 MapHubs 方法调用中的动态文件创建。</span><span class="sxs-lookup"><span data-stu-id="07000-247">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) and disable dynamic file creation in the MapHubs method call.</span></span>
3. > [!IMPORTANT]
   > <span data-ttu-id="07000-248">请确保在 JavaScript 文件中引用*StockTicker.html*正确无误。</span><span class="sxs-lookup"><span data-stu-id="07000-248">Make sure that the JavaScript file references in *StockTicker.html* are correct.</span></span> <span data-ttu-id="07000-249">也就是说，确保你的脚本标记 (1.10.2 在示例中) 中的 jQuery 版本是在项目中的 jQuery 版本相同*脚本*文件夹，并确保你的脚本标记中的 SignalR 版本是 SignalR 相同在项目的版本*脚本*文件夹。</span><span class="sxs-lookup"><span data-stu-id="07000-249">That is, make sure that the jQuery version in your script tag (1.10.2 in the example) is the same as the jQuery version in your project's *Scripts* folder, and make sure that the SignalR version in your script tag is the same as the SignalR version in your project's *Scripts* folder.</span></span> <span data-ttu-id="07000-250">如有必要，请更改脚本标记中的文件名称。</span><span class="sxs-lookup"><span data-stu-id="07000-250">Change the file names in the script tags if necessary.</span></span>
4. <span data-ttu-id="07000-251">在中**解决方案资源管理器**，右键单击*StockTicker.html*，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="07000-251">In **Solution Explorer**, right-click *StockTicker.html*, and then click **Set as Start Page**.</span></span>
5. <span data-ttu-id="07000-252">在项目文件夹中创建的新 JavaScript 文件并将其命名*StockTicker.js*...</span><span class="sxs-lookup"><span data-stu-id="07000-252">Create a new JavaScript file in the project folder and name it *StockTicker.js*..</span></span>
6. <span data-ttu-id="07000-253">模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="07000-253">Replace the template code with the following code:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

    <span data-ttu-id="07000-254">$.connection 指 SignalR 代理。</span><span class="sxs-lookup"><span data-stu-id="07000-254">$.connection refers to the SignalR proxies.</span></span> <span data-ttu-id="07000-255">该代码获取 StockTickerHub 类对代理的引用，并将其放入行情自动收录器变量。</span><span class="sxs-lookup"><span data-stu-id="07000-255">The code gets a reference to the proxy for the StockTickerHub class and puts it in the ticker variable.</span></span> <span data-ttu-id="07000-256">代理名称是 [HubName] 属性已设置的名称：</span><span class="sxs-lookup"><span data-stu-id="07000-256">The proxy name is the name that was set by the [HubName] attribute:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

    <span data-ttu-id="07000-257">定义所有变量和函数后，文件中的代码的最后一行初始化 SignalR 连接通过调用 SignalR 启动函数。</span><span class="sxs-lookup"><span data-stu-id="07000-257">After all the variables and functions are defined, the last line of code in the file initializes the SignalR connection by calling the SignalR start function.</span></span> <span data-ttu-id="07000-258">启动函数以异步方式执行，并返回[jQuery 延迟对象](http://api.jquery.com/category/deferred-object/)，这意味着您可以调用 done 的函数可指定异步操作完成时要调用的函数...</span><span class="sxs-lookup"><span data-stu-id="07000-258">The start function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means you can call the done function to specify the function to call when the asynchronous operation is completed..</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

    <span data-ttu-id="07000-259">Init 函数 getAllStocks 函数调用服务器上，并使用服务器将返回以更新库存表的信息。</span><span class="sxs-lookup"><span data-stu-id="07000-259">The init function calls the getAllStocks function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="07000-260">请注意，默认情况下，您必须使用 camel 大小写格式的客户端上但方法名是 pascal 大小写的服务器上。</span><span class="sxs-lookup"><span data-stu-id="07000-260">Notice that by default, you have to use camel casing on the client although the method name is pascal-cased on the server.</span></span> <span data-ttu-id="07000-261">Camel 大小写规则仅适用于方法，而不是对象。</span><span class="sxs-lookup"><span data-stu-id="07000-261">The camel-casing rule only applies to methods, not objects.</span></span> <span data-ttu-id="07000-262">例如，指股票。符号和库存。价格、 不 stock.symbol 或 stock.price。</span><span class="sxs-lookup"><span data-stu-id="07000-262">For example, you refer to stock.Symbol and stock.Price, not stock.symbol or stock.price.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

    <span data-ttu-id="07000-263">如果你想要在客户端上使用 pascal 大小写，或者如果你想要使用完全不同的方法名称，无法修饰具有 HubMethodName 特性中心的方法相同的方式，修饰，Hub 类本身与 HubName 属性。</span><span class="sxs-lookup"><span data-stu-id="07000-263">If you wanted to use pascal casing on the client, or if you wanted to use a completely different method name, you could decorate the Hub method with the HubMethodName attribute the same way you decorated the Hub class itself with the HubName attribute.</span></span>

    <span data-ttu-id="07000-264">在 init 方法中，为从服务器收到通过调用 formatStock 格式属性的常用对象，每个股票对象创建 HTML 表行，然后通过调用取代 (顶部定义*StockTicker.js*) 将 rowTemplate 变量中的占位符替换为股票对象属性值。</span><span class="sxs-lookup"><span data-stu-id="07000-264">In the init method, HTML for a table row is created for each stock object received from the server by calling formatStock to format properties of the stock object, and then by calling supplant (which is defined at the top of *StockTicker.js*) to replace placeholders in the rowTemplate variable with the stock object property values.</span></span> <span data-ttu-id="07000-265">生成的 HTML 然后追加到常用的表。</span><span class="sxs-lookup"><span data-stu-id="07000-265">The resulting HTML is then appended to the stock table.</span></span>

    <span data-ttu-id="07000-266">通过将其作为执行异步启动函数完成后的回调函数传递调用 init。</span><span class="sxs-lookup"><span data-stu-id="07000-266">You call init by passing it in as a callback function that executes after the asynchronous start function completes.</span></span> <span data-ttu-id="07000-267">如果作为单独的 JavaScript 语句调用开始后调用 init，该函数会失败，因为立即会执行而不必等待启动函数以完成建立连接。</span><span class="sxs-lookup"><span data-stu-id="07000-267">If you called init as a separate JavaScript statement after calling start, the function would fail because it would execute immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="07000-268">在这种情况下，init 函数会尝试调用 getAllStocks 函数，才能建立服务器连接。</span><span class="sxs-lookup"><span data-stu-id="07000-268">In that case, the init function would try to call the getAllStocks function before the server connection is established.</span></span>

    <span data-ttu-id="07000-269">当服务器更改股票的价格时，它调用 updateStockPrice 上连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="07000-269">When the server changes a stock's price, it calls the updateStockPrice on connected clients.</span></span> <span data-ttu-id="07000-270">若要在服务器使其可供调用情况下，该函数添加到 stockTicker 代理的客户端属性。</span><span class="sxs-lookup"><span data-stu-id="07000-270">The function is added to the client property of the stockTicker proxy in order to make it available to calls from the server.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

    <span data-ttu-id="07000-271">UpdateStockPrice 函数设置从服务器接收到一个表行，如 init 函数中所示相同的方式的常用对象的格式。</span><span class="sxs-lookup"><span data-stu-id="07000-271">The updateStockPrice function formats a stock object received from the server into a table row the same way as in the init function.</span></span> <span data-ttu-id="07000-272">但是，而不是追加到表的行，它查找股票的当前行的表中并替换新行。</span><span class="sxs-lookup"><span data-stu-id="07000-272">However, instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

<a id="test"></a>

## <a name="test-the-application"></a><span data-ttu-id="07000-273">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="07000-273">Test the application</span></span>

1. <span data-ttu-id="07000-274">按 F5 在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="07000-274">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="07000-275">库存表最初会显示"正在加载..."行，然后显示初始的股票数据时，一小段延迟后，然后股票价格开始更改。</span><span class="sxs-lookup"><span data-stu-id="07000-275">The stock table initially displays the "loading..." line, then after a short delay the initial stock data is displayed, and then the stock prices start to change.</span></span>

    ![“加载”](tutorial-server-broadcast-with-signalr/_static/image6.png)

    ![初始库存表](tutorial-server-broadcast-with-signalr/_static/image7.png)

    ![从服务器接收更改的库存表](tutorial-server-broadcast-with-signalr/_static/image8.png)
2. <span data-ttu-id="07000-279">从浏览器地址栏复制 URL 并将其粘贴到一个或多个新的浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="07000-279">Copy the URL from the browser address bar and paste it into one or more new browser window(s).</span></span>

    <span data-ttu-id="07000-280">初始股票显示第一个浏览器相同，同时发生了更改。</span><span class="sxs-lookup"><span data-stu-id="07000-280">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>
3. <span data-ttu-id="07000-281">关闭所有浏览器并打开新浏览器，然后转到相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="07000-281">Close all browsers and open a new browser, then go to the same URL.</span></span>

    <span data-ttu-id="07000-282">在服务器中运行，因此库存表屏幕将显示在股票已继续更改逐渐 StockTicker 单一实例对象。</span><span class="sxs-lookup"><span data-stu-id="07000-282">The StockTicker singleton object has continued to run in the server, so the stock table display shows that the stocks have continued to change.</span></span> <span data-ttu-id="07000-283">（不到具有零更改图形的初始表。）</span><span class="sxs-lookup"><span data-stu-id="07000-283">(You don't see the initial table with zero change figures.)</span></span>
4. <span data-ttu-id="07000-284">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="07000-284">Close the browser.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="07000-285">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="07000-285">Enable logging</span></span>

<span data-ttu-id="07000-286">SignalR 有一个可以在客户端启用帮助解决疑难问题的内置日志记录函数。</span><span class="sxs-lookup"><span data-stu-id="07000-286">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="07000-287">在本部分中启用日志记录并演示如何日志识别您哪一台以下的传输方法使用 SignalR 的示例，请参阅：</span><span class="sxs-lookup"><span data-stu-id="07000-287">In this section you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

- <span data-ttu-id="07000-288">[Websocket](http://en.wikipedia.org/wiki/WebSocket)、 IIS 8 和当前浏览器中受支持。</span><span class="sxs-lookup"><span data-stu-id="07000-288">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>
- <span data-ttu-id="07000-289">[服务器发送事件](http://en.wikipedia.org/wiki/Server-sent_events)、 Internet Explorer 以外的浏览器中受支持。</span><span class="sxs-lookup"><span data-stu-id="07000-289">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>
- <span data-ttu-id="07000-290">[永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)、 Internet Explorer 中受支持。</span><span class="sxs-lookup"><span data-stu-id="07000-290">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>
- <span data-ttu-id="07000-291">[Ajax 长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)，所有浏览器中受支持。</span><span class="sxs-lookup"><span data-stu-id="07000-291">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="07000-292">对于任何给定的连接，SignalR 会选择最佳的传输方法在服务器和客户端支持。</span><span class="sxs-lookup"><span data-stu-id="07000-292">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="07000-293">打开*StockTicker.js*并添加代码以启用日志记录之前初始化连接文件末尾的代码行：</span><span class="sxs-lookup"><span data-stu-id="07000-293">Open *StockTicker.js* and add a line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js)]
2. <span data-ttu-id="07000-294">按 F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="07000-294">Press F5 to run the project.</span></span>
3. <span data-ttu-id="07000-295">打开浏览器的开发人员工具窗口，并选择控制台以查看的日志。</span><span class="sxs-lookup"><span data-stu-id="07000-295">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="07000-296">您可能需要刷新页面以查看 Signalr 协商新连接的传输方法的日志。</span><span class="sxs-lookup"><span data-stu-id="07000-296">You might have to refresh the page to see the logs of Signalr negotiating the transport method for a new connection.</span></span>

    <span data-ttu-id="07000-297">如果在 Windows 8 (IIS 8) 上运行 Internet Explorer 10，传输方法是 Websocket。</span><span class="sxs-lookup"><span data-stu-id="07000-297">If you are running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![IE 10 IIS 8 控制台](tutorial-server-broadcast-with-signalr/_static/image9.png)

    <span data-ttu-id="07000-299">如果在 Windows 7 (IIS 7.5) 上运行 Internet Explorer 10，传输方法是 iframe。</span><span class="sxs-lookup"><span data-stu-id="07000-299">If you are running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is iframe.</span></span>

    ![IE 10 控制台中，IIS 7.5](tutorial-server-broadcast-with-signalr/_static/image10.png)

    <span data-ttu-id="07000-301">在 Firefox 中安装的 Firebug 外接程序以获取控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="07000-301">In Firefox, install the Firebug add-in to get a Console window.</span></span> <span data-ttu-id="07000-302">如果在 Windows 8 (IIS 8) 上运行 Firefox 19，传输方法是 Websocket。</span><span class="sxs-lookup"><span data-stu-id="07000-302">If you are running Firefox 19 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-signalr/_static/image11.png)

    <span data-ttu-id="07000-304">如果在 Windows 7 (IIS 7.5) 上运行 Firefox 19，传输方法将是服务器发送事件。</span><span class="sxs-lookup"><span data-stu-id="07000-304">If you are running Firefox 19 on Windows 7 (IIS 7.5), the transport method is server-sent events.</span></span>

    ![Firefox 19 IIS 7.5 控制台](tutorial-server-broadcast-with-signalr/_static/image12.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a><span data-ttu-id="07000-306">安装和查看完整的 StockTicker 示例</span><span class="sxs-lookup"><span data-stu-id="07000-306">Install and review the full StockTicker sample</span></span>

<span data-ttu-id="07000-307">StockTicker 应用程序的情况下，安装[Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 包包含更多的功能比只是创建从零开始的简化版本。</span><span class="sxs-lookup"><span data-stu-id="07000-307">The StockTicker application that is installed by the [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package includes more features than the simplified version that you just created from scratch.</span></span> <span data-ttu-id="07000-308">在本教程的此部分中，安装 NuGet 包并查看新功能和实现它们的代码。</span><span class="sxs-lookup"><span data-stu-id="07000-308">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span> <span data-ttu-id="07000-309">如果无需执行本教程的前面的步骤安装包，您必须将 OWIN 启动类添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="07000-309">If you install the package without performing the earlier steps of this tutorial, you must add an OWIN startup class to your project.</span></span> <span data-ttu-id="07000-310">此步骤是在 NuGet 包的 readme.txt 文件中所述。</span><span class="sxs-lookup"><span data-stu-id="07000-310">This step is explained in the readme.txt file for the NuGet package.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="07000-311">安装 SignalR.Sample NuGet 包</span><span class="sxs-lookup"><span data-stu-id="07000-311">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="07000-312">在中**解决方案资源管理器**，右键单击项目，然后单击**管理 NuGet 包**。</span><span class="sxs-lookup"><span data-stu-id="07000-312">In **Solution Explorer**, right-click the project and click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="07000-313">在中**管理 NuGet 包**对话框中，单击**联机**，输入*SignalR.Sample*中**联机搜索**框，然后依次**安装**中**SignalR.Sample**包。</span><span class="sxs-lookup"><span data-stu-id="07000-313">In the **Manage NuGet Packages** dialog box, click **Online**, enter *SignalR.Sample* in the **Search Online** box, and then click **Install** in the **SignalR.Sample** package.</span></span>

    ![安装 SignalR.Sample 包](tutorial-server-broadcast-with-signalr/_static/image13.png)
3. <span data-ttu-id="07000-315">在中**解决方案资源管理器**，展开*SignalR.Sample*安装 SignalR.Sample 包创建的文件夹。</span><span class="sxs-lookup"><span data-stu-id="07000-315">In **Solution Explorer**, expand the *SignalR.Sample* folder which was created by installing the SignalR.Sample package.</span></span>
4. <span data-ttu-id="07000-316">在中*SignalR.Sample*文件夹中，右键单击*StockTicker.html*，然后单击**设为起始页**。</span><span class="sxs-lookup"><span data-stu-id="07000-316">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then click **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="07000-317">安装 SignalR.Sample NuGet 包可能会更改中有的 jQuery 版本你*脚本*文件夹。</span><span class="sxs-lookup"><span data-stu-id="07000-317">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="07000-318">新*StockTicker.html*包将安装中的文件*SignalR.Sample*文件夹将与包将安装，但如果你想要运行原始的jQuery版本同步*StockTicker.html*再次文件中，您可能必须先更新中的脚本标记的 jQuery 引用。</span><span class="sxs-lookup"><span data-stu-id="07000-318">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="07000-319">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="07000-319">Run the application</span></span>

1. <span data-ttu-id="07000-320">按 F5 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="07000-320">Press F5 to run the application.</span></span>

    <span data-ttu-id="07000-321">除了你此前看到的网格中，完整股票行情自动收录器应用程序显示一个水平滚动的窗口，显示相同的库存数据。</span><span class="sxs-lookup"><span data-stu-id="07000-321">In addition to the grid that you saw earlier, the full stock ticker application shows a horizontally scrolling window that displays the same stock data.</span></span> <span data-ttu-id="07000-322">第一次的应用程序运行时，"市场""已关闭"，你看到静态网格和不滚动的行情自动收录器窗口。</span><span class="sxs-lookup"><span data-stu-id="07000-322">When you run the application for the first time, the "market" is "closed" and you see a static grid and a ticker window that isn't scrolling.</span></span>

    ![StockTicker 屏幕开始](tutorial-server-broadcast-with-signalr/_static/image14.png)

    <span data-ttu-id="07000-324">当您单击**公开市场**，则**实时股票行情自动收录器**水平滚动框开始和在服务器开始定期广播在随机的基础上的股票价格发生变化。</span><span class="sxs-lookup"><span data-stu-id="07000-324">When you click **Open Market**, the **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span> <span data-ttu-id="07000-325">每次股票价格发生更改，同时**实时股票表格**网格并**实时股票行情自动收录器**框会更新。</span><span class="sxs-lookup"><span data-stu-id="07000-325">Each time a stock price changes, both the **Live Stock Table** grid and the **Live Stock Ticker** box are updated.</span></span> <span data-ttu-id="07000-326">当股票的价格更改为正时，股票会显示绿色背景; 以及并更改为负，包含一个红色背景显示股票。</span><span class="sxs-lookup"><span data-stu-id="07000-326">When a stock's price change is positive, the stock is shown with a green background, and when the change is negative, the stock is shown with a red background.</span></span>

    ![StockTicker 应用市场打开](tutorial-server-broadcast-with-signalr/_static/image15.png)

    <span data-ttu-id="07000-328">**关闭市场**按钮停止所做的更改并停止行情自动收录器滚动，并**重置**按钮可重置所有股票数据为初始状态价格更改启动之前。</span><span class="sxs-lookup"><span data-stu-id="07000-328">The **Close Market** button stops the changes and stops the ticker scrolling, and the **Reset** button resets all stock data to the initial state before price changes started.</span></span> <span data-ttu-id="07000-329">如果您打开更多的浏览器窗口并转到同一个 URL，您将看到相同的数据在同一时间在每个浏览器中动态更新。</span><span class="sxs-lookup"><span data-stu-id="07000-329">If you open more browser windows and go to the same URL, you see the same data dynamically updated at the same time in each browser.</span></span> <span data-ttu-id="07000-330">当您单击某个按钮时，所有浏览器都在同一时间具有相同的方式。</span><span class="sxs-lookup"><span data-stu-id="07000-330">When you click one of the buttons, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="07000-331">实时股票行情自动收录器显示</span><span class="sxs-lookup"><span data-stu-id="07000-331">Live Stock Ticker display</span></span>

<span data-ttu-id="07000-332">**实时股票行情自动收录器**显示为未排序的列表中的 CSS 样式格式设置为单个行的 div 元素。</span><span class="sxs-lookup"><span data-stu-id="07000-332">The **Live Stock Ticker** display is an unordered list in a div element that is formatted into a single line by CSS styles.</span></span> <span data-ttu-id="07000-333">行情自动收录器会被初始化并更新表一样： 通过替换中的占位符&lt;li&gt;模板字符串和动态添加&lt;l i&gt;元素&lt;u l&gt;元素。</span><span class="sxs-lookup"><span data-stu-id="07000-333">The ticker is initialized and updated the same way as the table: by replacing placeholders in a &lt;li&gt; template string and dynamically adding the &lt;li&gt; elements to the &lt;ul&gt; element.</span></span> <span data-ttu-id="07000-334">通过使用 jQuery 进行动画处理函数来改变该 div。 中的未排序列表距左侧执行滚动</span><span class="sxs-lookup"><span data-stu-id="07000-334">The scrolling is performed by using the jQuery animate function to vary the margin-left of the unordered list within the div.</span></span>

<span data-ttu-id="07000-335">股票行情 HTML:</span><span class="sxs-lookup"><span data-stu-id="07000-335">The stock ticker HTML:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

<span data-ttu-id="07000-336">股票行情 CSS:</span><span class="sxs-lookup"><span data-stu-id="07000-336">The stock ticker CSS:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

<span data-ttu-id="07000-337">使它的 jQuery 代码滚动：</span><span class="sxs-lookup"><span data-stu-id="07000-337">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="07000-338">客户端可以调用的服务器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="07000-338">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="07000-339">StockTickerHub 类定义了四个客户端可以调用的其他方法：</span><span class="sxs-lookup"><span data-stu-id="07000-339">The StockTickerHub class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

<span data-ttu-id="07000-340">在页面顶部的按钮响应称为 OpenMarket、 CloseMarket 和重置。</span><span class="sxs-lookup"><span data-stu-id="07000-340">OpenMarket, CloseMarket, and Reset are called in response to the buttons at the top of the page.</span></span> <span data-ttu-id="07000-341">它们演示了一个客户端触发立即传播到所有客户端的状态的更改的模式。</span><span class="sxs-lookup"><span data-stu-id="07000-341">They demonstrate the pattern of one client triggering a change in state that is immediately propagated to all clients.</span></span> <span data-ttu-id="07000-342">每个方法调用中的方法 StockTicker 类市场状态更改，然后再将广播新状态的效果。</span><span class="sxs-lookup"><span data-stu-id="07000-342">Each of these methods calls a method in the StockTicker class that effects the market state change and then broadcasts the new state.</span></span>

<span data-ttu-id="07000-343">在 StockTicker 类中，通过返回 MarketState 枚举值的 MarketState 属性的维护是市场的状态：</span><span class="sxs-lookup"><span data-stu-id="07000-343">In the StockTicker class, the state of the market is maintained by a MarketState property that returns a MarketState enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

<span data-ttu-id="07000-344">每个更改市场状态的方法都这样做，在锁块的内部因为 StockTicker 类必须是 threadsafe:</span><span class="sxs-lookup"><span data-stu-id="07000-344">Each of the methods that change the market state do so inside a lock block because the StockTicker class has to be threadsafe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

<span data-ttu-id="07000-345">若要确保此代码是 threadsafe， \_marketState 字段支持 MarketState 属性标记为易失性，</span><span class="sxs-lookup"><span data-stu-id="07000-345">To ensure that this code is threadsafe, the \_marketState field that backs the MarketState property is marked as volatile,</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

<span data-ttu-id="07000-346">BroadcastMarketStateChange 和 BroadcastMarketReset 方法是您已看到的 BroadcastStockPrice 方法相似，只不过它们调用在客户端定义的不同方法：</span><span class="sxs-lookup"><span data-stu-id="07000-346">The BroadcastMarketStateChange and BroadcastMarketReset methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="07000-347">服务器可以调用的客户端上的其他函数</span><span class="sxs-lookup"><span data-stu-id="07000-347">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="07000-348">UpdateStockPrice 函数现在可处理网格和行情自动收录器显示，并使用 jQuery.Color 闪烁红色和绿色的颜色。</span><span class="sxs-lookup"><span data-stu-id="07000-348">The updateStockPrice function now handles both the grid and the ticker display, and it uses jQuery.Color to flash red and green colors.</span></span>

<span data-ttu-id="07000-349">中的新函数*SignalR.StockTicker.js*启用和禁用按钮根据市场的状态，并在停止或启动行情自动收录器窗口水平滚动。</span><span class="sxs-lookup"><span data-stu-id="07000-349">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state, and they stop or start the ticker window horizontal scrolling.</span></span> <span data-ttu-id="07000-350">由于多个函数添加到 ticker.client，因此[jQuery 扩展函数](http://api.jquery.com/jQuery.extend/)用于添加它们。</span><span class="sxs-lookup"><span data-stu-id="07000-350">Since multiple functions are being added to ticker.client, the [jQuery extend function](http://api.jquery.com/jQuery.extend/) is used to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="07000-351">建立连接后的其他客户端安装程序</span><span class="sxs-lookup"><span data-stu-id="07000-351">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="07000-352">客户端会建立连接后，它具有一些附加工作以执行操作： 找出市场是否打开或关闭以便调用相应 marketOpened 或 marketClosed 函数，并附加到按钮的服务器方法调用。</span><span class="sxs-lookup"><span data-stu-id="07000-352">After the client establishes the connection, it has some additional work to do: find out if the market is open or closed in order to call the appropriate marketOpened or marketClosed function, and attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

<span data-ttu-id="07000-353">服务器方法不是绑定到之前的按钮之后建立的连接，从而使代码不能尝试之前，它们可调用服务器方法。</span><span class="sxs-lookup"><span data-stu-id="07000-353">The server methods are not wired up to the buttons until after the connection is established, so that the code can't try to call the server methods before they are available.</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="07000-354">后续步骤</span><span class="sxs-lookup"><span data-stu-id="07000-354">Next steps</span></span>

<span data-ttu-id="07000-355">在本教程中介绍了如何将消息从服务器广播到所有连接的客户端，定期更新，以响应来自任何客户端通知的 SignalR 应用程序进行编程。</span><span class="sxs-lookup"><span data-stu-id="07000-355">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients, both on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="07000-356">使用多线程的单一实例维护服务器状态模式也还可在多玩家联机游戏方案。</span><span class="sxs-lookup"><span data-stu-id="07000-356">The pattern of using a multi-threaded singleton instance to maintain server state can also be also used in multi-player online game scenarios.</span></span> <span data-ttu-id="07000-357">有关示例，请参阅[依赖于使用 SignalR ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="07000-357">For an example, see [the ShootR game that is based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="07000-358">显示对等通信方案的教程，请参阅[SignalR 入门](introduction-to-signalr.md)并[使用 SignalR 实时更新](tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="07000-358">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](introduction-to-signalr.md) and [Real-Time Updating with SignalR](tutorial-high-frequency-realtime-with-signalr.md).</span></span>

<span data-ttu-id="07000-359">若要了解更高级的 SignalR 开发概念，请访问以下站点 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="07000-359">To learn more advanced SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="07000-360">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="07000-360">ASP.NET SignalR</span></span>](../../index.md)
- [<span data-ttu-id="07000-361">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="07000-361">SignalR Project</span></span>](http://signalr.net/)
- [<span data-ttu-id="07000-362">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="07000-362">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="07000-363">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="07000-363">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

<span data-ttu-id="07000-364">有关如何部署到 Azure 的 SignalR 应用程序的演练，请参阅[Azure 应用服务中的 Web 应用使用 SignalR](../deployment/using-signalr-with-azure-web-sites.md)。</span><span class="sxs-lookup"><span data-stu-id="07000-364">For a walkthrough on how to deploy a SignalR application to Azure, see [Using SignalR with Web Apps in Azure App Service](../deployment/using-signalr-with-azure-web-sites.md).</span></span> <span data-ttu-id="07000-365">有关如何将 Visual Studio web 项目部署到 Windows Azure 网站的详细信息，请参阅[在 Azure 应用服务中创建 ASP.NET web 应用](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="07000-365">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
