---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第 6 部分： ASP.NET 成员资格 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 6 部分添加 ASP.NET 成员资格。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: 83e9bc780ea8face3e0f55fdf8c00e13b60f80a7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886805"
---
<a name="part-6-aspnet-membership"></a><span data-ttu-id="39bda-104">第 6 部分： ASP.NET 成员资格</span><span class="sxs-lookup"><span data-stu-id="39bda-104">Part 6: ASP.NET Membership</span></span>
====================
<span data-ttu-id="39bda-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="39bda-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="39bda-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="39bda-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="39bda-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="39bda-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="39bda-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="39bda-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="39bda-109">第 6 部分添加 ASP.NET 成员资格。</span><span class="sxs-lookup"><span data-stu-id="39bda-109">Part 6 adds ASP.NET Membership.</span></span>


## <a id="_Toc260221672"></a>  <span data-ttu-id="39bda-110">使用 ASP.NET 成员资格</span><span class="sxs-lookup"><span data-stu-id="39bda-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="39bda-111">单击安全</span><span class="sxs-lookup"><span data-stu-id="39bda-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="39bda-112">请确保，我们将使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="39bda-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="39bda-113">使用"创建用户"链接创建几个用户。</span><span class="sxs-lookup"><span data-stu-id="39bda-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="39bda-114">完成后，请参阅解决方案资源管理器窗口，刷新视图。</span><span class="sxs-lookup"><span data-stu-id="39bda-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="39bda-115">请注意，ASPNETDB。已创建 MDF 正常。</span><span class="sxs-lookup"><span data-stu-id="39bda-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="39bda-116">此文件包含的表，以支持类似成员身份的核心 ASP.NET 服务。</span><span class="sxs-lookup"><span data-stu-id="39bda-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="39bda-117">现在我们可以开始实现在结帐过程。</span><span class="sxs-lookup"><span data-stu-id="39bda-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="39bda-118">首先创建 CheckOut.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="39bda-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="39bda-119">CheckOut.aspx 页应仅可供用户已登录，因此我们将限制对访问登录用户和重定向用户未登录到登录页。</span><span class="sxs-lookup"><span data-stu-id="39bda-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="39bda-120">若要这样做我们将添加以下内容到我们的 web.config 文件的配置节。</span><span class="sxs-lookup"><span data-stu-id="39bda-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="39bda-121">ASP.NET Web 窗体应用程序的模板自动添加到我们的 web.config 文件的身份验证部分，并建立的默认登录页。</span><span class="sxs-lookup"><span data-stu-id="39bda-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="39bda-122">我们必须修改 Login.aspx 代码隐藏文件在用户登录时，将迁移匿名的购物车。</span><span class="sxs-lookup"><span data-stu-id="39bda-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="39bda-123">更改页\_加载事件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="39bda-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="39bda-124">然后添加一个"LoggedIn"事件处理程序类似设置为新登录用户的会话名称，并通过在我们 MyShoppingCart 类中调用 MigrateCart 方法更改为的用户的购物车中的临时会话 id。</span><span class="sxs-lookup"><span data-stu-id="39bda-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="39bda-125">（在.cs 文件中实现）</span><span class="sxs-lookup"><span data-stu-id="39bda-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="39bda-126">实现 MigrateCart() 方法如下所示。</span><span class="sxs-lookup"><span data-stu-id="39bda-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="39bda-127">在 checkout.aspx 我们将使用 EntityDataSource 和 GridView 我们签出页中一样使用我们未在我们购物车页。</span><span class="sxs-lookup"><span data-stu-id="39bda-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="39bda-128">请注意，我们 GridView 控件指定"ondatabound"事件处理程序名为 MyList\_RowDataBound 因此让我们实现如下该事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="39bda-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="39bda-129">此方法使每个行绑定以及更新 GridView 的最后一行，购物车的购物运行总计。</span><span class="sxs-lookup"><span data-stu-id="39bda-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="39bda-130">在此阶段中，我们已实施顺序，以便放置"评论"演示的文稿。</span><span class="sxs-lookup"><span data-stu-id="39bda-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="39bda-131">让我们通过将几行代码添加到我们的页面中处理空购物车方案\_负载事件：</span><span class="sxs-lookup"><span data-stu-id="39bda-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="39bda-132">当用户单击"提交"按钮时我们将在提交按钮单击事件处理程序中执行下面的代码。</span><span class="sxs-lookup"><span data-stu-id="39bda-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="39bda-133">订单提交过程"肉"是在我们 MyShoppingCart 类的 SubmitOrder() 方法中实现。</span><span class="sxs-lookup"><span data-stu-id="39bda-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="39bda-134">将订单将：</span><span class="sxs-lookup"><span data-stu-id="39bda-134">SubmitOrder will:</span></span>

- <span data-ttu-id="39bda-135">采用所有行项购物车中并使用它们来创建新的顺序记录和相关联的 OrderDetails 记录。</span><span class="sxs-lookup"><span data-stu-id="39bda-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="39bda-136">计算传送日期。</span><span class="sxs-lookup"><span data-stu-id="39bda-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="39bda-137">清除购物车。</span><span class="sxs-lookup"><span data-stu-id="39bda-137">Clear the shopping cart.</span></span>


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="39bda-138">此示例应用程序供我们将通过只需将两天添加到当前日期计算发货日期。</span><span class="sxs-lookup"><span data-stu-id="39bda-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="39bda-139">运行应用程序现在将允许我们测试从开始到完成购物过程。</span><span class="sxs-lookup"><span data-stu-id="39bda-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="39bda-140">[上一页](tailspin-spyworks-part-5.md)
> [下一页](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="39bda-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
