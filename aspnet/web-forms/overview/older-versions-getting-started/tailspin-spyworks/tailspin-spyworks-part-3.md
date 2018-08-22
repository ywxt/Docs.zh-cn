---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第 3 部分： 布局和类别菜单 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 3 部分介绍如何添加布局和类别菜单。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: f55b29a271dbdb72d3e2249ed74517b77d78cf5e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825048"
---
<a name="part-3-layout-and-category-menu"></a><span data-ttu-id="c20d4-104">第 3 部分： 布局和类别菜单</span><span class="sxs-lookup"><span data-stu-id="c20d4-104">Part 3: Layout and Category Menu</span></span>
====================
<span data-ttu-id="c20d4-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="c20d4-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="c20d4-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="c20d4-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="c20d4-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="c20d4-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="c20d4-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="c20d4-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="c20d4-109">第 3 部分介绍如何添加布局和类别菜单。</span><span class="sxs-lookup"><span data-stu-id="c20d4-109">Part 3 covers adding layout and a category menu.</span></span>


## <a id="_Toc260221669"></a>  <span data-ttu-id="c20d4-110">添加一些布局和类别菜单</span><span class="sxs-lookup"><span data-stu-id="c20d4-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="c20d4-111">在我们站点的主页面中，我们将添加将包含我们的产品类别菜单的左侧和右侧列的 div。</span><span class="sxs-lookup"><span data-stu-id="c20d4-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="c20d4-112">请注意，将由我们添加到我们 Style.css 文件的 CSS 类提供所需的对齐和其他格式设置。</span><span class="sxs-lookup"><span data-stu-id="c20d4-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="c20d4-113">产品类别菜单将动态创建在运行时通过查询商务数据库的现有产品类别以及创建菜单项和相应的链接。</span><span class="sxs-lookup"><span data-stu-id="c20d4-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="c20d4-114">若要完成此我们将使用两个 ASP。NET 的功能强大的数据控件。</span><span class="sxs-lookup"><span data-stu-id="c20d4-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="c20d4-115">"实体数据源"控件和"ListView"控件。</span><span class="sxs-lookup"><span data-stu-id="c20d4-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="c20d4-116">让我们切换到"设计视图"和帮助程序用于配置我们的控件。</span><span class="sxs-lookup"><span data-stu-id="c20d4-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="c20d4-117">让我们将 EntityDataSource ID 属性设置为 EDS\_类别\_菜单，并单击"配置数据源"。</span><span class="sxs-lookup"><span data-stu-id="c20d4-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="c20d4-118">选择我们为我们的商务数据库创建实体数据源模型时为我们创建的 CommerceEntities 连接，然后单击"下一步"。</span><span class="sxs-lookup"><span data-stu-id="c20d4-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="c20d4-119">选择"类别"实体集名称，并将其余选项为默认值。</span><span class="sxs-lookup"><span data-stu-id="c20d4-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="c20d4-120">单击"完成"。</span><span class="sxs-lookup"><span data-stu-id="c20d4-120">Click "Finish".</span></span>

<span data-ttu-id="c20d4-121">现在让我们在我们对 ListView 的页面放置的 ListView 控件实例的 ID 属性设置\_ProductsMenu 并激活其帮助程序。</span><span class="sxs-lookup"><span data-stu-id="c20d4-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="c20d4-122">不过我们可以使用控制选项设置数据的项显示的格式和格式设置，我们创建了菜单将只需要简单的标记以便将源视图中输入代码。</span><span class="sxs-lookup"><span data-stu-id="c20d4-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="c20d4-123">请注意"Eval"语句： &lt;%# Eval("CategoryName") %&gt;</span><span class="sxs-lookup"><span data-stu-id="c20d4-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="c20d4-124">ASP.NET 语法&lt;%# %&gt;是指示运行时执行任何包含在中，输出结果"行"的速记约定。</span><span class="sxs-lookup"><span data-stu-id="c20d4-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="c20d4-125">语句 Eval("CategoryName") 指示，当前项的数据项时，绑定集合中提取实体模型项名称的值"CatagoryName"。</span><span class="sxs-lookup"><span data-stu-id="c20d4-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CatagoryName".</span></span> <span data-ttu-id="c20d4-126">这是一个非常强大的功能的简洁语法。</span><span class="sxs-lookup"><span data-stu-id="c20d4-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="c20d4-127">让我们运行应用程序现在。</span><span class="sxs-lookup"><span data-stu-id="c20d4-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="c20d4-128">请注意，现在显示我们的产品类别菜单和时我们将鼠标悬停在通过一个我们可以看到我们必须尚未实现的页的菜单项链接点的类别菜单项名为 ProductsList.aspx 并且，我们已经构建了一个动态查询字符串参数，包含 类别 id。</span><span class="sxs-lookup"><span data-stu-id="c20d4-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c20d4-129">[上一页](tailspin-spyworks-part-2.md)
> [下一页](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="c20d4-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
