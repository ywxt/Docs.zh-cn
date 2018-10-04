---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 入门 |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2cc9364b815cae0207fc59784303c6a0906f1b94
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578440"
---
<a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="20829-102">ASP.NET MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="20829-102">Getting started with ASP.NET MVC 5</span></span>
====================
<span data-ttu-id="20829-103">通过[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="20829-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

<span data-ttu-id="20829-104">本教程讲解构建 ASP.NET MVC 5 web 应用程序使用的基础知识[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="20829-104">This tutorial teaches you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="20829-105">本教程的最后一个源代码位于[GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)。</span><span class="sxs-lookup"><span data-stu-id="20829-105">The final source code for the tutorial is located on [GitHub](https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).</span></span>

<span data-ttu-id="20829-106">本教程由编写[Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[ @scottgu ](https://twitter.com/scottgu) )， [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [ @shanselman ](https://twitter.com/shanselman) )并[Rick Anderson](https://twitter.com/RickAndMSFT) ( [ @RickAndMSFT ](https://twitter.com/#!/RickAndMSFT) )</span><span class="sxs-lookup"><span data-stu-id="20829-106">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

<span data-ttu-id="20829-107">需要一个 Azure 帐户才能将此应用程序部署到 Azure:</span><span class="sxs-lookup"><span data-stu-id="20829-107">You need an Azure account to deploy this app to Azure:</span></span>

- <span data-ttu-id="20829-108">你可以[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="20829-108">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="20829-109">你可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-MSDN 订阅提供信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="20829-109">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="get-started"></a><span data-ttu-id="20829-110">入门</span><span class="sxs-lookup"><span data-stu-id="20829-110">Get started</span></span>

<span data-ttu-id="20829-111">首先[安装 Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="20829-111">Start by [installing Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="20829-112">然后，打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="20829-112">Then, open Visual Studio.</span></span>

<span data-ttu-id="20829-113">Visual Studio 是一个 IDE 或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="20829-113">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="20829-114">就像使用 Microsoft Word 编写文档，将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="20829-114">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="20829-115">在 Visual Studio 中，没有向您显示各种可用选项，底部的列表。</span><span class="sxs-lookup"><span data-stu-id="20829-115">In Visual Studio, there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="20829-116">此外，还有一个菜单，其中提供了另一种方法在 IDE 中执行任务。</span><span class="sxs-lookup"><span data-stu-id="20829-116">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="20829-117">例如，而不是选择**新的项目**上**起始页**，可以使用菜单栏并选择**文件** > **的新项目**.</span><span class="sxs-lookup"><span data-stu-id="20829-117">For example, instead of selecting **New Project** on the **Start page**, you can use the menu bar and select **File** > **New Project**.</span></span>

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a><span data-ttu-id="20829-118">创建你的第一个应用</span><span class="sxs-lookup"><span data-stu-id="20829-118">Create your first app</span></span>

<span data-ttu-id="20829-119">上**起始页**，选择**新项目**。</span><span class="sxs-lookup"><span data-stu-id="20829-119">On the **Start page**, select **New Project**.</span></span> <span data-ttu-id="20829-120">在中**新的项目**对话框中，选择**Visual C#** 左侧类别，然后**Web**，然后选择**ASP.NET Web 应用程序 (.NET Framework)** 项目模板。</span><span class="sxs-lookup"><span data-stu-id="20829-120">In the **New project** dialog box, select the **Visual C#** category on the left, then **Web**, and then select the **ASP.NET Web Application (.NET Framework)** project template.</span></span> <span data-ttu-id="20829-121">"MvcMovie"将项目命名，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="20829-121">Name your project "MvcMovie" and then choose **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="20829-122">在中**新的 ASP.NET Web 应用程序**对话框中，选择**MVC** ，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="20829-122">In the **New ASP.NET Web Application** dialog, choose **MVC** and then choose **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="20829-123">Visual Studio 刚刚创建的 ASP.NET MVC 项目使用默认模板，因此您的工作应用程序现在具有而无需执行任何操作 ！</span><span class="sxs-lookup"><span data-stu-id="20829-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="20829-124">这是简单"Hello World ！"</span><span class="sxs-lookup"><span data-stu-id="20829-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="20829-125">项目和它的启动应用程序的好时机。</span><span class="sxs-lookup"><span data-stu-id="20829-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="20829-126">按 **F5** 启动调试。</span><span class="sxs-lookup"><span data-stu-id="20829-126">Press **F5** to start debugging.</span></span> <span data-ttu-id="20829-127">当您按下**F5**，启动 Visual Studio [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)并运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="20829-127">When you press **F5**, Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your web app.</span></span> <span data-ttu-id="20829-128">然后，visual Studio 启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="20829-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="20829-129">请注意，在浏览器地址栏将显示`localhost:port#`并不是类似于`example.com`。</span><span class="sxs-lookup"><span data-stu-id="20829-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="20829-130">这是因为`localhost`始终指向自己在这种情况下运行应用程序刚生成的本地计算机。</span><span class="sxs-lookup"><span data-stu-id="20829-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="20829-131">Visual Studio 运行时 web 项目，一个随机端口用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="20829-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="20829-132">下图中的端口号是 1234年。</span><span class="sxs-lookup"><span data-stu-id="20829-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="20829-133">当您运行该应用程序时，您将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="20829-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="20829-134">即时可用的此默认模板向您提供`Home`， `Contact`，和`About`页。</span><span class="sxs-lookup"><span data-stu-id="20829-134">Right out of the box this default template gives you `Home`, `Contact`, and `About` pages.</span></span> <span data-ttu-id="20829-135">上面的图像不会显示**主页**，**有关**，并**联系人**链接。</span><span class="sxs-lookup"><span data-stu-id="20829-135">The image above doesn't show the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="20829-136">具体取决于浏览器窗口的大小，可能需要单击导航图标可查看下面的链接。</span><span class="sxs-lookup"><span data-stu-id="20829-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="20829-137">应用程序还提供支持注册和登录。</span><span class="sxs-lookup"><span data-stu-id="20829-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="20829-138">下一步是要更改此应用程序的工作方式有点了解 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="20829-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="20829-139">关闭 ASP.NET MVC 应用程序，让我们将一些代码。</span><span class="sxs-lookup"><span data-stu-id="20829-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="20829-140">当前教程的列表，请参阅[MVC 建议文章](../mvc-learning-sequence.md)。</span><span class="sxs-lookup"><span data-stu-id="20829-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="20829-141">请参阅在 Azure 上运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="20829-141">See this app running on Azure</span></span>

<span data-ttu-id="20829-142">若要查看已完成的站点作为实时 web 应用运行吗？</span><span class="sxs-lookup"><span data-stu-id="20829-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="20829-143">只需单击下面的按钮，可以将完整版本的应用部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="20829-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/Docs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="20829-144">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="20829-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="20829-145">如果还没有帐户，则可使用以下选项之一来创建一个：</span><span class="sxs-lookup"><span data-stu-id="20829-145">If you don't already have an account, use one of the following options to create one:</span></span>

- <span data-ttu-id="20829-146">[免费建立一个 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取信用额度可用于试用付费版 Azure 服务，甚至在用之后最多可以保留帐户并使用免费的 Azure 服务。</span><span class="sxs-lookup"><span data-stu-id="20829-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="20829-147">[激活 Visual Studio 订户权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)-Visual Studio 订阅提供的信用额度可以用于付费版 Azure 服务的每个月。</span><span class="sxs-lookup"><span data-stu-id="20829-147">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="20829-148">下一篇</span><span class="sxs-lookup"><span data-stu-id="20829-148">Next</span></span>](adding-a-controller.md)
