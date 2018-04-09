---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第 3 部分： 布局和类别菜单 |Microsoft 文档
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 3 部分介绍如何添加布局和类别菜单。
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/21/2010
ms.topic: article
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: 27a493173b03f813ee3dcbbfafd8bc52fb0b9771
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="part-3-layout-and-category-menu"></a><span data-ttu-id="7fb07-104">第 3 部分: 布局和类别菜单</span><span class="sxs-lookup"><span data-stu-id="7fb07-104">Part 3: Layout and Category Menu</span></span>
====================
<span data-ttu-id="7fb07-105">通过[Joe stagner 将](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="7fb07-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="7fb07-106">Tailspin Spyworks 演示创建在.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="7fb07-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="7fb07-107">它演示如何使用 ASP.NET 4 中出色的新功能构建在线商店，包括购物、 结帐和管理关闭。</span><span class="sxs-lookup"><span data-stu-id="7fb07-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="7fb07-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="7fb07-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="7fb07-109">第 3 部分介绍如何添加布局和类别菜单。</span><span class="sxs-lookup"><span data-stu-id="7fb07-109">Part 3 covers adding layout and a category menu.</span></span>


## <a id="_Toc260221669"></a>  <span data-ttu-id="7fb07-110">添加一些布局和类别菜单</span><span class="sxs-lookup"><span data-stu-id="7fb07-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="7fb07-111">在我们站点的主页面中，我们将添加将包含我们的产品类别菜单的左侧列 div。</span><span class="sxs-lookup"><span data-stu-id="7fb07-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="7fb07-112">请注意，将由我们添加到我们的 Style.css 文件的 CSS 类提供所需对齐和其他格式。</span><span class="sxs-lookup"><span data-stu-id="7fb07-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="7fb07-113">产品类别菜单将动态创建在运行时通过查询商务数据库，对于现有产品类别以及创建菜单项和相应链接。</span><span class="sxs-lookup"><span data-stu-id="7fb07-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="7fb07-114">若要实现此目的我们将使用两个 ASP。NET 的功能强大的数据控件。</span><span class="sxs-lookup"><span data-stu-id="7fb07-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="7fb07-115">"实体数据源"控件和"ListView"控件。</span><span class="sxs-lookup"><span data-stu-id="7fb07-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="7fb07-116">让我们切换到"设计视图"，并使用以下帮助器来配置我们的控件。</span><span class="sxs-lookup"><span data-stu-id="7fb07-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="7fb07-117">让我们将 EntityDataSource ID 属性设置为费用分配表\_类别\_菜单，然后单击"配置数据源"。</span><span class="sxs-lookup"><span data-stu-id="7fb07-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="7fb07-118">选择已创建为我们为我们的商务数据库创建实体数据源模型时的 CommerceEntities 连接，然后单击"下一步"。</span><span class="sxs-lookup"><span data-stu-id="7fb07-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="7fb07-119">选择"类别"实体集名称，并将其余的选项为默认值。</span><span class="sxs-lookup"><span data-stu-id="7fb07-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="7fb07-120">单击"完成"。</span><span class="sxs-lookup"><span data-stu-id="7fb07-120">Click "Finish".</span></span>

<span data-ttu-id="7fb07-121">现在让我们设置我们将为 ListView 我们页面放置的 ListView 控件实例的 ID 属性\_ProductsMenu 并激活其帮助器。</span><span class="sxs-lookup"><span data-stu-id="7fb07-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="7fb07-122">但我们无法使用控件选项来设置数据的项显示的格式和格式设置，我们菜单创建将只需要简单标记因此我们将在源视图中输入的代码。</span><span class="sxs-lookup"><span data-stu-id="7fb07-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="7fb07-123">请注意"Eval"语句： &lt;%# Eval("CategoryName") %&gt;</span><span class="sxs-lookup"><span data-stu-id="7fb07-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="7fb07-124">ASP.NET 语法&lt;%# %&gt;是指示运行时执行任何包含在中，"行"中的将结果输出的速记约定。</span><span class="sxs-lookup"><span data-stu-id="7fb07-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="7fb07-125">语句 Eval("CategoryName") 指示，当前项的数据项时，绑定的集合中提取的实体模型项名称的值"CatagoryName"。</span><span class="sxs-lookup"><span data-stu-id="7fb07-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CatagoryName".</span></span> <span data-ttu-id="7fb07-126">这是简洁语法非常强大的功能。</span><span class="sxs-lookup"><span data-stu-id="7fb07-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="7fb07-127">我们来运行应用程序现在。</span><span class="sxs-lookup"><span data-stu-id="7fb07-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="7fb07-128">请注意，现在显示我们的产品类别菜单和时我们将鼠标悬停我们可以看到我们必须尚未实现的页的菜单项链接点的类别菜单项的通过一个名为 ProductsList.aspx 并且，我们已生成动态查询字符串自变量，包含 类别 id。</span><span class="sxs-lookup"><span data-stu-id="7fb07-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7fb07-129">[上一页](tailspin-spyworks-part-2.md)
> [下一页](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="7fb07-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
