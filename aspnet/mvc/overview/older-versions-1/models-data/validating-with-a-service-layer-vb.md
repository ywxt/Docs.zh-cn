---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 验证与服务层 (VB) |Microsoft 文档
author: StephenWalther
description: 了解如何移动你的验证逻辑控制器操作出来放入单独的服务层。 在本教程中，Stephen Walther 解释了如何你...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/02/2009
ms.topic: article
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: bb1191b663f863bf881def620efab4f2f03edc56
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="3374d-104">验证与服务层 (VB)</span><span class="sxs-lookup"><span data-stu-id="3374d-104">Validating with a Service Layer (VB)</span></span>
====================
<span data-ttu-id="3374d-105">通过[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="3374d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="3374d-106">了解如何移动你的验证逻辑控制器操作出来放入单独的服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="3374d-107">在本教程中，Stephen Walther 解释了如何通过隔离接受你的服务层，从控制器层维护尖锐分离问题。</span><span class="sxs-lookup"><span data-stu-id="3374d-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>


<span data-ttu-id="3374d-108">本教程的目的是为了说明的 ASP.NET MVC 应用程序中执行验证的一种方法。</span><span class="sxs-lookup"><span data-stu-id="3374d-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="3374d-109">在本教程中，您将学习如何移动你的验证逻辑你的控制器出来放入单独的服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="3374d-110">分隔问题</span><span class="sxs-lookup"><span data-stu-id="3374d-110">Separating Concerns</span></span>

<span data-ttu-id="3374d-111">生成 ASP.NET MVC 应用程序时，不应在你的控制器操作内将你数据库的逻辑。</span><span class="sxs-lookup"><span data-stu-id="3374d-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="3374d-112">混合使用你的数据库和控制器逻辑让你应用程序随着时间的推移维护更加困难。</span><span class="sxs-lookup"><span data-stu-id="3374d-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="3374d-113">推荐方法是你将所有数据库逻辑放在单独的存储库层。</span><span class="sxs-lookup"><span data-stu-id="3374d-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="3374d-114">例如，清单 1 包含名为化 ProductRepository 简单存储库。</span><span class="sxs-lookup"><span data-stu-id="3374d-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="3374d-115">产品储存库包含的所有应用程序的数据访问代码。</span><span class="sxs-lookup"><span data-stu-id="3374d-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="3374d-116">该列表还包括产品存储库实现的 IProductRepository 接口。</span><span class="sxs-lookup"><span data-stu-id="3374d-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="3374d-117">**Listing 1 - Models\ProductRepository.vb**</span><span class="sxs-lookup"><span data-stu-id="3374d-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="3374d-118">列出 2 中的控制器其 index （） 和 create （） 操作中使用存储库层。</span><span class="sxs-lookup"><span data-stu-id="3374d-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="3374d-119">请注意，此控制器不包含任何数据库逻辑。</span><span class="sxs-lookup"><span data-stu-id="3374d-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="3374d-120">创建存储库层使您能够维护完全分离关注点。</span><span class="sxs-lookup"><span data-stu-id="3374d-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="3374d-121">控制器负责应用程序流控制逻辑和存储库负责数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="3374d-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="3374d-122">**Listing 2 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="3374d-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="3374d-123">创建服务层</span><span class="sxs-lookup"><span data-stu-id="3374d-123">Creating a Service Layer</span></span>

<span data-ttu-id="3374d-124">因此，应用程序流控制逻辑所属控制器中，并且在存储库所属的数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="3374d-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="3374d-125">在这种情况下，不要放置您的验证逻辑？</span><span class="sxs-lookup"><span data-stu-id="3374d-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="3374d-126">一种选择是将放置在您验证逻辑*服务层*。</span><span class="sxs-lookup"><span data-stu-id="3374d-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="3374d-127">服务层是在 ASP.NET MVC 应用程序进行调解控制器和存储库层之间的通信的附加层。</span><span class="sxs-lookup"><span data-stu-id="3374d-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="3374d-128">服务层包含业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="3374d-128">The service layer contains business logic.</span></span> <span data-ttu-id="3374d-129">具体而言，它包含验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="3374d-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="3374d-130">例如，清单 3 的产品服务层具有 CreateProduct() 方法。</span><span class="sxs-lookup"><span data-stu-id="3374d-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="3374d-131">CreateProduct() 方法调用 ValidateProduct() 方法以将产品传递给产品存储库之前验证新产品。</span><span class="sxs-lookup"><span data-stu-id="3374d-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="3374d-132">**Listing 3 - Models\ProductService.vb**</span><span class="sxs-lookup"><span data-stu-id="3374d-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="3374d-133">产品控制器已更新列出 4 而不是存储库层使用的服务层中。</span><span class="sxs-lookup"><span data-stu-id="3374d-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="3374d-134">控制器层介绍对服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="3374d-135">服务层与存储库层通信。</span><span class="sxs-lookup"><span data-stu-id="3374d-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="3374d-136">每个层都有单独的责任。</span><span class="sxs-lookup"><span data-stu-id="3374d-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="3374d-137">**Listing 4 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="3374d-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="3374d-138">请注意，在产品控制器构造函数创建产品服务。</span><span class="sxs-lookup"><span data-stu-id="3374d-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="3374d-139">创建产品服务后，模型状态字典将传递到服务。</span><span class="sxs-lookup"><span data-stu-id="3374d-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="3374d-140">产品服务使用模型状态将验证错误消息传递回控制器。</span><span class="sxs-lookup"><span data-stu-id="3374d-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="3374d-141">分离的服务层</span><span class="sxs-lookup"><span data-stu-id="3374d-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="3374d-142">我们无法隔离控制器和一个方面中的服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="3374d-143">控制器和服务层通过模型状态进行通信。</span><span class="sxs-lookup"><span data-stu-id="3374d-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="3374d-144">换而言之，服务层具有特定功能的 ASP.NET MVC framework 的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="3374d-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="3374d-145">我们想要隔离从尽可能多地我们控制器层的服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="3374d-146">从理论上讲，我们应能够使用任何类型的应用程序和不只一个 ASP.NET MVC 应用程序使用的服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="3374d-147">例如，在将来，我们可能想要生成 WPF 前端我们为应用程序。</span><span class="sxs-lookup"><span data-stu-id="3374d-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="3374d-148">我们应从我们的服务层提供了如何删除对 ASP.NET MVC 依赖关系模型状态。</span><span class="sxs-lookup"><span data-stu-id="3374d-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="3374d-149">在列出 5 中，服务层具有已更新，以使其不再使用模型状态。</span><span class="sxs-lookup"><span data-stu-id="3374d-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="3374d-150">相反，它使用的任何类都实现 IValidationDictionary 接口。</span><span class="sxs-lookup"><span data-stu-id="3374d-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="3374d-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span><span class="sxs-lookup"><span data-stu-id="3374d-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="3374d-152">在列出 6 定义 IValidationDictionary 接口。</span><span class="sxs-lookup"><span data-stu-id="3374d-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="3374d-153">此简单的界面都具有单个方法和单个属性。</span><span class="sxs-lookup"><span data-stu-id="3374d-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="3374d-154">**列出 6-Models\IValidationDictionary.cs**</span><span class="sxs-lookup"><span data-stu-id="3374d-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="3374d-155">在列出 7 中，名为 ModelStateWrapper 类，类实现 IValidationDictionary 接口。</span><span class="sxs-lookup"><span data-stu-id="3374d-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="3374d-156">可以通过将模型状态字典传递给构造函数来实例化 ModelStateWrapper 类。</span><span class="sxs-lookup"><span data-stu-id="3374d-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="3374d-157">**Listing 7 - Models\ModelStateWrapper.vb**</span><span class="sxs-lookup"><span data-stu-id="3374d-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="3374d-158">最后，列出 8 中的更新的控制器使用 ModelStateWrapper 在其构造函数中创建服务层时。</span><span class="sxs-lookup"><span data-stu-id="3374d-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="3374d-159">**Listing 8 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="3374d-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="3374d-160">使用 IValidationDictionary 接口和 ModelStateWrapper 类使我们能够将从我们控制器层我们服务层完全隔离。</span><span class="sxs-lookup"><span data-stu-id="3374d-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="3374d-161">服务层不再依赖于模型状态。</span><span class="sxs-lookup"><span data-stu-id="3374d-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="3374d-162">可以传递任何实现的服务层的 IValidationDictionary 接口的类。</span><span class="sxs-lookup"><span data-stu-id="3374d-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="3374d-163">例如，一个 WPF 应用程序可能实现一个简单的集合类 IValidationDictionary 的接口。</span><span class="sxs-lookup"><span data-stu-id="3374d-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="3374d-164">总结</span><span class="sxs-lookup"><span data-stu-id="3374d-164">Summary</span></span>

<span data-ttu-id="3374d-165">本教程的目的是讨论在 ASP.NET MVC 应用程序中执行验证的一种方法。</span><span class="sxs-lookup"><span data-stu-id="3374d-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="3374d-166">在本教程中，您学习了如何将您的验证逻辑你的控制器出来放入单独的服务层的所有移动。</span><span class="sxs-lookup"><span data-stu-id="3374d-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="3374d-167">你还了解了如何通过创建 ModelStateWrapper 类隔离你从控制器层的服务层。</span><span class="sxs-lookup"><span data-stu-id="3374d-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3374d-168">[上一页](validating-with-the-idataerrorinfo-interface-vb.md)
> [下一页](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3374d-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>
