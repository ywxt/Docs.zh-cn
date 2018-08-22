---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第 2 部分： 数据访问层 |Microsoft Docs
author: JoeStagner
description: 本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。 第 2 部分介绍如何添加数据访问层。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 5b5ae08b157054bf0f3231782127ee3110f36d00
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830479"
---
<a name="part-2-data-access-layer"></a><span data-ttu-id="4e9f6-104">第 2 部分： 数据访问层</span><span class="sxs-lookup"><span data-stu-id="4e9f6-104">Part 2: Data Access Layer</span></span>
====================
<span data-ttu-id="4e9f6-105">通过[Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="4e9f6-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="4e9f6-106">Tailspin Spyworks 演示如何创建适用于.NET 平台的功能强大、 可扩展应用程序是如何非常简单。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="4e9f6-107">它展示如何在 ASP.NET 4 中使用强大的新功能来构建在线商店，包括购物、 签出和管理。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="4e9f6-108">本系列教程详细介绍所有生成 Tailspin Spyworks 示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="4e9f6-109">第 2 部分介绍如何添加数据访问层。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-109">Part 2 covers adding the data access layer.</span></span>


## <a id="_Toc260221668"></a>  <span data-ttu-id="4e9f6-110">添加数据访问层</span><span class="sxs-lookup"><span data-stu-id="4e9f6-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="4e9f6-111">我们的电子商务应用程序将依赖于两个数据库。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="4e9f6-112">对于客户信息，我们将使用标准 ASP.NET 成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="4e9f6-113">我们的购物车和产品目录，我们将按如下所示实现 SQL Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="4e9f6-114">在应用程序的应用程序中创建数据库 (Commerce.mdf)\_我们可以继续创建使用.NET Entity Framework 数据访问层的数据文件夹。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="4e9f6-115">我们将创建一个名为"数据\_访问"和它们在该文件夹上右键单击并选择"添加新项"。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="4e9f6-116">在"安装模板"项，然后选择"ADO.NET 实体数据模型"输入 EDM\_Commerce.edmx 作为名称，然后单击"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="4e9f6-117">选择"从数据库生成"。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="4e9f6-118">保存并生成。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-118">Save and build.</span></span>

<span data-ttu-id="4e9f6-119">现在我们已准备好添加我们第一项功能 – 产品类别菜单。</span><span class="sxs-lookup"><span data-stu-id="4e9f6-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4e9f6-120">[上一页](tailspin-spyworks-part-1.md)
> [下一页](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="4e9f6-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
