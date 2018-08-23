---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第 6 部分： ASP.NET 成员资格 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 6 部分添加 ASP.NET 成员资格。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: c847db058bc03115210f12eeb0c3c76fecc8a31e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834524"
---
<a name="part-6-aspnet-membership"></a><span data-ttu-id="db097-104">第 6 部分： ASP.NET 成员资格</span><span class="sxs-lookup"><span data-stu-id="db097-104">Part 6: ASP.NET Membership</span></span>
====================
<span data-ttu-id="db097-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="db097-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="db097-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="db097-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="db097-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="db097-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="db097-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="db097-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="db097-109">第 6 部分添加 ASP.NET 成员资格。</span><span class="sxs-lookup"><span data-stu-id="db097-109">Part 6 adds ASP.NET Membership.</span></span>


## <a id="_Toc260221672"></a>  <span data-ttu-id="db097-110">使用 ASP.NET 成员资格</span><span class="sxs-lookup"><span data-stu-id="db097-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="db097-111">单击安全</span><span class="sxs-lookup"><span data-stu-id="db097-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="db097-112">请确保，我们将使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="db097-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="db097-113">使用"创建用户"链接创建几个用户。</span><span class="sxs-lookup"><span data-stu-id="db097-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="db097-114">完成后，请参阅解决方案资源管理器窗口并刷新视图。</span><span class="sxs-lookup"><span data-stu-id="db097-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="db097-115">请注意，ASPNETDB。已创建 MDF 没问题。</span><span class="sxs-lookup"><span data-stu-id="db097-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="db097-116">此文件包含表以支持核心 ASP.NET 服务，如成员身份。</span><span class="sxs-lookup"><span data-stu-id="db097-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="db097-117">现在我们可以开始实施签出过程。</span><span class="sxs-lookup"><span data-stu-id="db097-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="db097-118">首先，创建 CheckOut.aspx 页。</span><span class="sxs-lookup"><span data-stu-id="db097-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="db097-119">CheckOut.aspx 页应仅可供已登录，因此我们会限制对访问已登录用户未登录到登录页的重定向用户的用户。</span><span class="sxs-lookup"><span data-stu-id="db097-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="db097-120">为此我们将添加以下 web.config 文件的配置节。</span><span class="sxs-lookup"><span data-stu-id="db097-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="db097-121">ASP.NET Web 窗体应用程序模板自动添加到 web.config 文件的身份验证部分，并建立的默认登录页。</span><span class="sxs-lookup"><span data-stu-id="db097-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="db097-122">我们必须修改 Login.aspx 代码隐藏文件以在用户登录时，迁移匿名的购物车。</span><span class="sxs-lookup"><span data-stu-id="db097-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="db097-123">更改的页\_加载事件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="db097-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="db097-124">然后添加如下设置的会话名称将为新登录的用户并通过我们 MyShoppingCart 类中调用 MigrateCart 方法将在购物车中的临时会话 id 更改为的用户的"LoggedIn"事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="db097-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="db097-125">（在.cs 文件中实现）</span><span class="sxs-lookup"><span data-stu-id="db097-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="db097-126">实现 MigrateCart() 方法像这样。</span><span class="sxs-lookup"><span data-stu-id="db097-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="db097-127">Checkout.aspx 中我们将使用 EntityDataSource 和 GridView 中我们签出页几乎与我们在我们的购物车页中。</span><span class="sxs-lookup"><span data-stu-id="db097-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="db097-128">请注意，我们的 GridView 控件指定"ondatabound"事件处理程序名为 MyList\_RowDataBound 因此让我们来实现此类事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="db097-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="db097-129">此方法操作可使汇总的购物车随着每个行绑定和更新 GridView 的底部行。</span><span class="sxs-lookup"><span data-stu-id="db097-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="db097-130">在此阶段我们实现了要放置的顺序的"评论"演示文稿。</span><span class="sxs-lookup"><span data-stu-id="db097-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="db097-131">让我们通过将少量的代码行添加到我们的页面处理空车方案\_加载事件：</span><span class="sxs-lookup"><span data-stu-id="db097-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="db097-132">当用户单击"提交"按钮时我们将执行下面的代码中的提交按钮单击事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="db097-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="db097-133">"主要内容"的订单提交过程是在我们 MyShoppingCart 类的 SubmitOrder() 方法中实现。</span><span class="sxs-lookup"><span data-stu-id="db097-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="db097-134">SubmitOrder 将：</span><span class="sxs-lookup"><span data-stu-id="db097-134">SubmitOrder will:</span></span>

- <span data-ttu-id="db097-135">在购物车中采取的所有行项，并使用它们来创建新的订单记录和相关联的 OrderDetails 记录。</span><span class="sxs-lookup"><span data-stu-id="db097-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="db097-136">计算发货日期。</span><span class="sxs-lookup"><span data-stu-id="db097-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="db097-137">清除购物车。</span><span class="sxs-lookup"><span data-stu-id="db097-137">Clear the shopping cart.</span></span>


[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="db097-138">此示例应用程序供我们将只需将两天添加到当前日期来计算发货日期。</span><span class="sxs-lookup"><span data-stu-id="db097-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="db097-139">运行应用程序现在将允许我们要测试从开始到完成购物过程。</span><span class="sxs-lookup"><span data-stu-id="db097-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="db097-140">[上一页](tailspin-spyworks-part-5.md)
> [下一页](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="db097-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
