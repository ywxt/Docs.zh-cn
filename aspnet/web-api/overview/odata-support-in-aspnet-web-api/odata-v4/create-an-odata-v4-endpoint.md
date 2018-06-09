---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: 创建 OData v4 终结点使用 ASP.NET Web API 2.2 |Microsoft 文档
author: MikeWasson
description: 开放式数据协议 (OData) 是 web 数据访问协议。 OData 提供统一的方式来查询和操作通过 CRUD 操作的数据集...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/24/2014
ms.topic: article
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: a3f94818f9674b0e1e9a45b2a6cc9455edc79726
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2018
ms.locfileid: "26508046"
---
<a name="create-an-odata-v4-endpoint-using-aspnet-web-api-22"></a><span data-ttu-id="bdd71-104">创建 OData v4 终结点使用 ASP.NET Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="bdd71-104">Create an OData v4 Endpoint Using ASP.NET Web API 2.2</span></span>
====================
<span data-ttu-id="bdd71-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bdd71-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="bdd71-106">开放式数据协议 (OData) 是 web 数据访问协议。</span><span class="sxs-lookup"><span data-stu-id="bdd71-106">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="bdd71-107">OData 提供统一的方式来查询和操作数据集通过 CRUD 操作 （创建、 读取、 更新和删除）。</span><span class="sxs-lookup"><span data-stu-id="bdd71-107">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
> 
> <span data-ttu-id="bdd71-108">ASP.NET Web API 支持 v3 和 v4 协议。</span><span class="sxs-lookup"><span data-stu-id="bdd71-108">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="bdd71-109">你甚至可以有运行的并行 v4 终结点与 v3 终结点。</span><span class="sxs-lookup"><span data-stu-id="bdd71-109">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
> 
> <span data-ttu-id="bdd71-110">本教程演示如何创建支持的 CRUD 操作的 OData v4 终结点。</span><span class="sxs-lookup"><span data-stu-id="bdd71-110">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="bdd71-111">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="bdd71-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="bdd71-112">Web API 2.2</span><span class="sxs-lookup"><span data-stu-id="bdd71-112">Web API 2.2</span></span>
> - <span data-ttu-id="bdd71-113">OData v4</span><span class="sxs-lookup"><span data-stu-id="bdd71-113">OData v4</span></span>
> - [<span data-ttu-id="bdd71-114">Visual Studio 2013 Update 2</span><span class="sxs-lookup"><span data-stu-id="bdd71-114">Visual Studio 2013 Update 2</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - <span data-ttu-id="bdd71-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="bdd71-115">Entity Framework 6</span></span>
> - <span data-ttu-id="bdd71-116">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="bdd71-116">.NET 4.5</span></span>
> 
> 
> ## <a name="tutorial-versions"></a><span data-ttu-id="bdd71-117">教程版本</span><span class="sxs-lookup"><span data-stu-id="bdd71-117">Tutorial versions</span></span>
> 
> <span data-ttu-id="bdd71-118">有关 OData 版本 3，请参阅[创建 OData v3 终结点](../odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="bdd71-118">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>


## <a name="create-the-visual-studio-project"></a><span data-ttu-id="bdd71-119">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="bdd71-119">Create the Visual Studio Project</span></span>

<span data-ttu-id="bdd71-120">在 Visual Studio 中，从**文件**菜单上，选择**新建** &gt; **项目**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-120">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="bdd71-121">展开**已安装** &gt; **模板** &gt; **Visual C#** &gt; **Web**，然后选择**ASP.NET Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="bdd71-121">Expand **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="bdd71-122">将项目&quot;ProductService&quot;。</span><span class="sxs-lookup"><span data-stu-id="bdd71-122">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image2.png)](create-an-odata-v4-endpoint/_static/image1.png)

<span data-ttu-id="bdd71-123">在**新项目**对话框中，选择**空**模板。</span><span class="sxs-lookup"><span data-stu-id="bdd71-123">In the **New Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="bdd71-124">下&quot;将文件夹添加和核心引用...&quot;，单击**Web API**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-124">Under &quot;Add folders and core references...&quot;, click **Web API**.</span></span> <span data-ttu-id="bdd71-125">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-125">Click **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image4.png)](create-an-odata-v4-endpoint/_static/image3.png)

## <a name="install-the-odata-packages"></a><span data-ttu-id="bdd71-126">安装 OData 包</span><span class="sxs-lookup"><span data-stu-id="bdd71-126">Install the OData Packages</span></span>

<span data-ttu-id="bdd71-127">从**工具**菜单上，选择**NuGet 包管理器** &gt; **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="bdd71-128">在 Package Manager Console 窗口中，键入：</span><span class="sxs-lookup"><span data-stu-id="bdd71-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="bdd71-129">此命令将安装最新的 OData NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="bdd71-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="bdd71-130">将一个模型类添加</span><span class="sxs-lookup"><span data-stu-id="bdd71-130">Add a Model Class</span></span>

<span data-ttu-id="bdd71-131">A*模型*是一个对象，表示你的应用程序中的数据实体。</span><span class="sxs-lookup"><span data-stu-id="bdd71-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="bdd71-132">在解决方案资源管理器，右键单击模型文件夹。</span><span class="sxs-lookup"><span data-stu-id="bdd71-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="bdd71-133">从上下文菜单中，选择**添加** &gt; **类**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="bdd71-134">按照约定，模型类都放在 Models 文件夹中，但你不需要遵循此约定中您自己的项目。</span><span class="sxs-lookup"><span data-stu-id="bdd71-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>


<span data-ttu-id="bdd71-135">将此类命名为 `Product`。</span><span class="sxs-lookup"><span data-stu-id="bdd71-135">Name the class `Product`.</span></span> <span data-ttu-id="bdd71-136">在 Product.cs 文件中，将替换为以下内容的样板文件代码：</span><span class="sxs-lookup"><span data-stu-id="bdd71-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="bdd71-137">`Id`属性是实体键。</span><span class="sxs-lookup"><span data-stu-id="bdd71-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="bdd71-138">客户端可以查询按的键的实体。</span><span class="sxs-lookup"><span data-stu-id="bdd71-138">Clients can query entities by key.</span></span> <span data-ttu-id="bdd71-139">例如，若要获取的产品与 ID 为 5，URI 是`/Products(5)`。</span><span class="sxs-lookup"><span data-stu-id="bdd71-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="bdd71-140">`Id`属性也将后端数据库中的主键。</span><span class="sxs-lookup"><span data-stu-id="bdd71-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="bdd71-141">启用实体框架</span><span class="sxs-lookup"><span data-stu-id="bdd71-141">Enable Entity Framework</span></span>

<span data-ttu-id="bdd71-142">对于本教程，我们将使用 Entity Framework (EF) Code First 创建后端数据库。</span><span class="sxs-lookup"><span data-stu-id="bdd71-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd71-143">Web API OData 不需要 EF。</span><span class="sxs-lookup"><span data-stu-id="bdd71-143">Web API OData does not require EF.</span></span> <span data-ttu-id="bdd71-144">使用任何数据访问层上可以转换模型数据库实体。</span><span class="sxs-lookup"><span data-stu-id="bdd71-144">Use any data-access layer that can translate database entities into models.</span></span>


<span data-ttu-id="bdd71-145">首先，为 EF 安装 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="bdd71-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="bdd71-146">从**工具**菜单上，选择**NuGet 包管理器** &gt; **程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="bdd71-147">在 Package Manager Console 窗口中，键入：</span><span class="sxs-lookup"><span data-stu-id="bdd71-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="bdd71-148">打开 Web.config 文件中，并添加以下节内的**配置**元素后面**configSections**元素。</span><span class="sxs-lookup"><span data-stu-id="bdd71-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="bdd71-149">此设置将添加 LocalDB 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bdd71-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="bdd71-150">本地运行应用时，将使用此数据库。</span><span class="sxs-lookup"><span data-stu-id="bdd71-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="bdd71-151">接下来，添加一个名为类`ProductsContext`到 Models 文件夹：</span><span class="sxs-lookup"><span data-stu-id="bdd71-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="bdd71-152">在构造函数中，`"name=ProductsContext"`提供的连接字符串名称。</span><span class="sxs-lookup"><span data-stu-id="bdd71-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="bdd71-153">配置 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="bdd71-153">Configure the OData Endpoint</span></span>

<span data-ttu-id="bdd71-154">打开文件应用\_Start/WebApiConfig.cs。</span><span class="sxs-lookup"><span data-stu-id="bdd71-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="bdd71-155">添加以下**使用**语句：</span><span class="sxs-lookup"><span data-stu-id="bdd71-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="bdd71-156">然后添加以下代码到**注册**方法：</span><span class="sxs-lookup"><span data-stu-id="bdd71-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="bdd71-157">此代码执行两项操作：</span><span class="sxs-lookup"><span data-stu-id="bdd71-157">This code does two things:</span></span>

- <span data-ttu-id="bdd71-158">创建实体数据模型 (EDM)。</span><span class="sxs-lookup"><span data-stu-id="bdd71-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="bdd71-159">添加一个路由。</span><span class="sxs-lookup"><span data-stu-id="bdd71-159">Adds a route.</span></span>

<span data-ttu-id="bdd71-160">EDM 是一个抽象模型的数据。</span><span class="sxs-lookup"><span data-stu-id="bdd71-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="bdd71-161">EDM 用于创建服务元数据文档。</span><span class="sxs-lookup"><span data-stu-id="bdd71-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="bdd71-162">**ODataConventionModelBuilder**类创建 EDM 通过使用默认的命名约定。</span><span class="sxs-lookup"><span data-stu-id="bdd71-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="bdd71-163">此方法要求最少的代码。</span><span class="sxs-lookup"><span data-stu-id="bdd71-163">This approach requires the least code.</span></span> <span data-ttu-id="bdd71-164">如果你想 EDM 的更好地控制，则可以使用**ODataModelBuilder**类以创建 EDM 显式添加属性、 密钥和导航属性。</span><span class="sxs-lookup"><span data-stu-id="bdd71-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="bdd71-165">A*路由*告知如何将 HTTP 请求路由到终结点的 Web API。</span><span class="sxs-lookup"><span data-stu-id="bdd71-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="bdd71-166">若要创建 OData v4 路由的步骤，请调用**MapODataServiceRoute**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="bdd71-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="bdd71-167">如果你的应用程序具有多个 OData 终结点，每个创建单独的路由。</span><span class="sxs-lookup"><span data-stu-id="bdd71-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="bdd71-168">为每个路由，指定唯一的路由名称和前缀。</span><span class="sxs-lookup"><span data-stu-id="bdd71-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="bdd71-169">添加 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="bdd71-169">Add the OData Controller</span></span>

<span data-ttu-id="bdd71-170">A*控制器*是处理 HTTP 请求的类。</span><span class="sxs-lookup"><span data-stu-id="bdd71-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="bdd71-171">你创建的每个实体在你的 OData 服务中设置单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="bdd71-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="bdd71-172">在本教程中，将为创建一个控制器，`Product`实体。</span><span class="sxs-lookup"><span data-stu-id="bdd71-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="bdd71-173">在解决方案资源管理器，右键单击 Controllers 文件夹，然后选择**添加** &gt; **类**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="bdd71-174">将此类命名为 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="bdd71-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="bdd71-175">本教程针对 OData v3 使用的版本**添加控制器**基架。</span><span class="sxs-lookup"><span data-stu-id="bdd71-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="bdd71-176">目前，OData v4 没有基架。</span><span class="sxs-lookup"><span data-stu-id="bdd71-176">Currently, there is no scaffolding for OData v4.</span></span>


<span data-ttu-id="bdd71-177">将替换为以下 ProductsController.cs 中的样板文件代码。</span><span class="sxs-lookup"><span data-stu-id="bdd71-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="bdd71-178">控制器使用`ProductsContext`类来访问使用 EF 的数据库。</span><span class="sxs-lookup"><span data-stu-id="bdd71-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="bdd71-179">请注意，控制器将重写**释放**方法来释放**ProductsContext**。</span><span class="sxs-lookup"><span data-stu-id="bdd71-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="bdd71-180">这是控制器的起始点。</span><span class="sxs-lookup"><span data-stu-id="bdd71-180">This is the starting point for the controller.</span></span> <span data-ttu-id="bdd71-181">接下来，我们将添加所有的 CRUD 操作的方法。</span><span class="sxs-lookup"><span data-stu-id="bdd71-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="querying-the-entity-set"></a><span data-ttu-id="bdd71-182">查询实体集</span><span class="sxs-lookup"><span data-stu-id="bdd71-182">Querying the Entity Set</span></span>

<span data-ttu-id="bdd71-183">添加以下方法`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="bdd71-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="bdd71-184">无参数版本`Get`方法将返回整个产品集合。</span><span class="sxs-lookup"><span data-stu-id="bdd71-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="bdd71-185">`Get`方法替换*密钥*参数按照键查找产品 (在这种情况下，`Id`属性)。</span><span class="sxs-lookup"><span data-stu-id="bdd71-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="bdd71-186">**[EnableQuery]** 属性使客户端能够修改查询，通过使用如 $filter、 $sort 和 $page 的查询选项。</span><span class="sxs-lookup"><span data-stu-id="bdd71-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="bdd71-187">有关详细信息，请参阅[支持 OData 查询选项](../supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="bdd71-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="adding-an-entity-to-the-entity-set"></a><span data-ttu-id="bdd71-188">将实体添加到实体集</span><span class="sxs-lookup"><span data-stu-id="bdd71-188">Adding an Entity to the Entity Set</span></span>

<span data-ttu-id="bdd71-189">若要启用客户端向数据库添加新的产品，添加以下方法`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="bdd71-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="updating-an-entity"></a><span data-ttu-id="bdd71-190">更新实体</span><span class="sxs-lookup"><span data-stu-id="bdd71-190">Updating an Entity</span></span>

<span data-ttu-id="bdd71-191">OData 支持用于更新实体，修补程序和 PUT 的两个不同的语义。</span><span class="sxs-lookup"><span data-stu-id="bdd71-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="bdd71-192">修补程序执行部分更新。</span><span class="sxs-lookup"><span data-stu-id="bdd71-192">PATCH performs a partial update.</span></span> <span data-ttu-id="bdd71-193">客户端指定只是要更新的属性。</span><span class="sxs-lookup"><span data-stu-id="bdd71-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="bdd71-194">PUT 会替换整个实体。</span><span class="sxs-lookup"><span data-stu-id="bdd71-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="bdd71-195">PUT 的缺点是客户端必须发送实体，包括未更改的值中的所有属性的值。</span><span class="sxs-lookup"><span data-stu-id="bdd71-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="bdd71-196">[OData 规范](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)规定修补程序是首选。</span><span class="sxs-lookup"><span data-stu-id="bdd71-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="bdd71-197">在任何情况下，以下是针对修补程序和 PUT 方法的代码：</span><span class="sxs-lookup"><span data-stu-id="bdd71-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="bdd71-198">对于 PATCH 的控制器使用**增量&lt;T&gt;** 类型以跟踪所做的更改。</span><span class="sxs-lookup"><span data-stu-id="bdd71-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="deleting-an-entity"></a><span data-ttu-id="bdd71-199">删除实体</span><span class="sxs-lookup"><span data-stu-id="bdd71-199">Deleting an Entity</span></span>

<span data-ttu-id="bdd71-200">若要启用客户端以从数据库中删除产品，添加以下方法`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="bdd71-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
