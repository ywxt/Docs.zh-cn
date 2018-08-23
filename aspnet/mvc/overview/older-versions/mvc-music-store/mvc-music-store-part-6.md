---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: 第 6 部分： 使用数据批注的模型验证 |Microsoft Docs
author: jongalloway
description: 本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。 第 6 部分介绍如何为模型 V 使用数据注释...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: b666c3cef0b09c6d68cee581a3c27c08e3357cca
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830873"
---
<a name="part-6-using-data-annotations-for-model-validation"></a><span data-ttu-id="0c82b-104">第 6 部分： 使用数据注释进行模型验证</span><span class="sxs-lookup"><span data-stu-id="0c82b-104">Part 6: Using Data Annotations for Model Validation</span></span>
====================
<span data-ttu-id="0c82b-105">通过[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0c82b-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0c82b-106">MVC Music 商店是介绍，并说明如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发分步教程应用程序。</span><span class="sxs-lookup"><span data-stu-id="0c82b-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0c82b-107">MVC Music 商店是该类销售音乐 album 联机，并实现基本的站点管理、 用户登录，和购物车功能存储区实现轻量的示例。</span><span class="sxs-lookup"><span data-stu-id="0c82b-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="0c82b-108">本系列教程详细介绍所有构建 ASP.NET MVC Music 商店示例应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="0c82b-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0c82b-109">第 6 部分介绍如何为模型验证中使用数据注释。</span><span class="sxs-lookup"><span data-stu-id="0c82b-109">Part 6 covers Using Data Annotations for Model Validation.</span></span>


<span data-ttu-id="0c82b-110">我们使用我们创建和编辑窗体具有一个主要问题： 未做任何验证。</span><span class="sxs-lookup"><span data-stu-id="0c82b-110">We have a major issue with our Create and Edit forms: they're not doing any validation.</span></span> <span data-ttu-id="0c82b-111">我们可以执行某些操作，如在价格字段中，保留空白的必填的字段或键入字母，我们将看到的第一个错误来自数据库。</span><span class="sxs-lookup"><span data-stu-id="0c82b-111">We can do things like leave required fields blank or type letters in the Price field, and the first error we'll see is from the database.</span></span>

<span data-ttu-id="0c82b-112">我们可以轻松添加验证到我们的应用程序，这需要通过将数据批注添加到我们的模型类来实现。</span><span class="sxs-lookup"><span data-stu-id="0c82b-112">We can easily add validation to our application by adding Data Annotations to our model classes.</span></span> <span data-ttu-id="0c82b-113">数据批注，我们可以描述应用于模型属性，我们想要的规则和 ASP.NET MVC 将负责强制执行它们并向我们的用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="0c82b-113">Data Annotations allow us to describe the rules we want applied to our model properties, and ASP.NET MVC will take care of enforcing them and displaying appropriate messages to our users.</span></span>

## <a name="adding-validation-to-our-album-forms"></a><span data-ttu-id="0c82b-114">向我们唱片集窗体中添加验证</span><span class="sxs-lookup"><span data-stu-id="0c82b-114">Adding Validation to our Album Forms</span></span>

<span data-ttu-id="0c82b-115">我们将使用以下数据注释属性：</span><span class="sxs-lookup"><span data-stu-id="0c82b-115">We'll use the following Data Annotation attributes:</span></span>

- <span data-ttu-id="0c82b-116">**所需**– 指示该属性是必填的字段</span><span class="sxs-lookup"><span data-stu-id="0c82b-116">**Required** – Indicates that the property is a required field</span></span>
- <span data-ttu-id="0c82b-117">**DisplayName** – 定义要我们在窗体字段和验证消息使用的文本</span><span class="sxs-lookup"><span data-stu-id="0c82b-117">**DisplayName** – Defines the text we want used on form fields and validation messages</span></span>
- <span data-ttu-id="0c82b-118">**StringLength** – 定义字符串字段的最大长度</span><span class="sxs-lookup"><span data-stu-id="0c82b-118">**StringLength** – Defines a maximum length for a string field</span></span>
- <span data-ttu-id="0c82b-119">**范围**– 为数字字段提供最大和最小值</span><span class="sxs-lookup"><span data-stu-id="0c82b-119">**Range** – Gives a maximum and minimum value for a numeric field</span></span>
- <span data-ttu-id="0c82b-120">**将绑定**– 列出要排除或包括当参数或窗体值绑定到模型属性的字段</span><span class="sxs-lookup"><span data-stu-id="0c82b-120">**Bind** – Lists fields to exclude or include when binding parameter or form values to model properties</span></span>
- <span data-ttu-id="0c82b-121">**ScaffoldColumn** – 允许隐藏编辑器窗体中的字段</span><span class="sxs-lookup"><span data-stu-id="0c82b-121">**ScaffoldColumn** – Allows hiding fields from editor forms</span></span>

<span data-ttu-id="0c82b-122">*注意： 有关使用数据注释属性的模型验证的详细信息，请参阅上的 MSDN 文档*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span><span class="sxs-lookup"><span data-stu-id="0c82b-122">*Note: For more information on Model Validation using Data Annotation attributes, see the MSDN documentation at*[`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)</span></span>

<span data-ttu-id="0c82b-123">打开唱片集类并添加以下*使用*到顶部的语句。</span><span class="sxs-lookup"><span data-stu-id="0c82b-123">Open the Album class and add the following *using* statements to the top.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

<span data-ttu-id="0c82b-124">接下来，更新以添加显示和验证属性，如下所示的属性。</span><span class="sxs-lookup"><span data-stu-id="0c82b-124">Next, update the properties to add display and validation attributes as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

<span data-ttu-id="0c82b-125">我们可以在那里，我们已更改为虚拟属性的流派和艺术家。</span><span class="sxs-lookup"><span data-stu-id="0c82b-125">While we're there, we've also changed the Genre and Artist to virtual properties.</span></span> <span data-ttu-id="0c82b-126">这样，若要延迟加载它们根据需要的实体框架。</span><span class="sxs-lookup"><span data-stu-id="0c82b-126">This allows Entity Framework to lazy-load them as necessary.</span></span>

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

<span data-ttu-id="0c82b-127">后具有这些属性添加到我们唱片集的模型，我们创建和编辑屏幕立即开始验证字段，并使用显示名称，我们已选择 (例如唱片集画面 Url 而不是 AlbumArtUrl)。</span><span class="sxs-lookup"><span data-stu-id="0c82b-127">After having added these attributes to our Album model, our Create and Edit screen immediately begin validating fields and using the Display Names we've chosen (e.g. Album Art Url instead of AlbumArtUrl).</span></span> <span data-ttu-id="0c82b-128">运行应用程序并浏览到 /StoreManager/Create。</span><span class="sxs-lookup"><span data-stu-id="0c82b-128">Run the application and browse to /StoreManager/Create.</span></span>

![](mvc-music-store-part-6/_static/image1.png)

<span data-ttu-id="0c82b-129">接下来，我们将分一些验证规则。</span><span class="sxs-lookup"><span data-stu-id="0c82b-129">Next, we'll break some validation rules.</span></span> <span data-ttu-id="0c82b-130">输入 0 的价格，然后将标题留空。</span><span class="sxs-lookup"><span data-stu-id="0c82b-130">Enter a price of 0 and leave the Title blank.</span></span> <span data-ttu-id="0c82b-131">当我们单击创建按钮时，我们将看到显示验证错误消息显示哪些字段不符合验证规则我们已定义的窗体。</span><span class="sxs-lookup"><span data-stu-id="0c82b-131">When we click on the Create button, we will see the form displayed with validation error messages showing which fields did not meet the validation rules we have defined.</span></span>

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a><span data-ttu-id="0c82b-132">测试客户端验证</span><span class="sxs-lookup"><span data-stu-id="0c82b-132">Testing the Client-Side Validation</span></span>

<span data-ttu-id="0c82b-133">服务器端验证是从应用程序的角度看，非常重要，因为用户可以绕过客户端验证。</span><span class="sxs-lookup"><span data-stu-id="0c82b-133">Server-side validation is very important from an application perspective, because users can circumvent client-side validation.</span></span> <span data-ttu-id="0c82b-134">但是，仅实现服务器端验证网页窗体表现出三个严重问题。</span><span class="sxs-lookup"><span data-stu-id="0c82b-134">However, webpage forms which only implement server-side validation exhibit three significant problems.</span></span>

1. <span data-ttu-id="0c82b-135">用户必须等待要发布，在服务器上，验证的窗体，并且要发送到其浏览器的响应。</span><span class="sxs-lookup"><span data-stu-id="0c82b-135">The user has to wait for the form to be posted, validated on the server, and for the response to be sent to their browser.</span></span>
2. <span data-ttu-id="0c82b-136">他们会校正字段，以便它现在通过验证规则时，用户不会获得即时反馈。</span><span class="sxs-lookup"><span data-stu-id="0c82b-136">The user doesn't get immediate feedback when they correct a field so that it now passes the validation rules.</span></span>
3. <span data-ttu-id="0c82b-137">我们都浪费服务器资源来执行验证逻辑，而不是利用用户的浏览器。</span><span class="sxs-lookup"><span data-stu-id="0c82b-137">We are wasting server resources to perform validation logic instead of leveraging the user's browser.</span></span>

<span data-ttu-id="0c82b-138">幸运的是，ASP.NET MVC 3 基架模板具有客户端验证内置的需要说明，否则任何额外工作。</span><span class="sxs-lookup"><span data-stu-id="0c82b-138">Fortunately, the ASP.NET MVC 3 scaffold templates have client-side validation built in, requiring no additional work whatsoever.</span></span>

<span data-ttu-id="0c82b-139">在标题字段中键入单个字母满足验证要求，以便验证消息将立即删除。</span><span class="sxs-lookup"><span data-stu-id="0c82b-139">Typing a single letter in the Title field satisfies the validation requirements, so the validation message is immediately removed.</span></span>

![](mvc-music-store-part-6/_static/image3.png)


> [!div class="step-by-step"]
> <span data-ttu-id="0c82b-140">[上一页](mvc-music-store-part-5.md)
> [下一页](mvc-music-store-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="0c82b-140">[Previous](mvc-music-store-part-5.md)
[Next](mvc-music-store-part-7.md)</span></span>
