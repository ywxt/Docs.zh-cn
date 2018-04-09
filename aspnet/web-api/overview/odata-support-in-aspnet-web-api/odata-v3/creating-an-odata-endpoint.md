---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: 创建与 Web API 2 OData v3 终结点 |Microsoft 文档
author: MikeWasson
description: 开放式数据协议 (OData) 是 web 数据访问协议。 OData 提供统一的方式来构造数据、 查询的数据，以及处理数据...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/25/2014
ms.topic: article
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 227faacd3f42731e08a4cd2b71075776309961b6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a><span data-ttu-id="97a4a-104">创建与 Web API 2 OData v3 终结点</span><span class="sxs-lookup"><span data-stu-id="97a4a-104">Creating an OData v3 Endpoint with Web API 2</span></span>
====================
<span data-ttu-id="97a4a-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="97a4a-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="97a4a-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="97a4a-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="97a4a-107">[开放数据协议](http://www.odata.org/)(OData) 是用于 web 的数据访问协议。</span><span class="sxs-lookup"><span data-stu-id="97a4a-107">The [Open Data Protocol](http://www.odata.org/) (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="97a4a-108">OData 提供统一的方式来结构数据、 查询的数据和操作数据集通过 CRUD 操作 （创建、 读取、 更新和删除）。</span><span class="sxs-lookup"><span data-stu-id="97a4a-108">OData provides a uniform way to structure data, query the data, and manipulate the data set through CRUD operations (create, read, update, and delete).</span></span> <span data-ttu-id="97a4a-109">OData 支持 AtomPub (XML) 和 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="97a4a-109">OData supports both AtomPub (XML) and JSON formats.</span></span> <span data-ttu-id="97a4a-110">OData 还定义了如何公开数据的元数据。</span><span class="sxs-lookup"><span data-stu-id="97a4a-110">OData also defines a way to expose metadata about the data.</span></span> <span data-ttu-id="97a4a-111">客户端可以使用元数据发现的类型信息和数据集的关系。</span><span class="sxs-lookup"><span data-stu-id="97a4a-111">Clients can use the metadata to discover the type information and relationships for the data set.</span></span>
> 
> <span data-ttu-id="97a4a-112">ASP.NET Web API 可以轻松创建数据集的 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-112">ASP.NET Web API makes it easy to create an OData endpoint for a data set.</span></span> <span data-ttu-id="97a4a-113">你可以控制完全的 OData 操作终结点支持。</span><span class="sxs-lookup"><span data-stu-id="97a4a-113">You can control exactly which OData operations the endpoint supports.</span></span> <span data-ttu-id="97a4a-114">你可以托管多个 OData 终结点，以及非 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-114">You can host multiple OData endpoints, alongside non-OData endpoints.</span></span> <span data-ttu-id="97a4a-115">必须对数据模型、 后端业务逻辑和数据层的完全控制。</span><span class="sxs-lookup"><span data-stu-id="97a4a-115">You have full control over your data model, back-end business logic, and data layer.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="97a4a-116">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="97a4a-116">Software versions used in the tutorial</span></span>
> 
> 
> - [<span data-ttu-id="97a4a-117">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="97a4a-117">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="97a4a-118">Web API 2</span><span class="sxs-lookup"><span data-stu-id="97a4a-118">Web API 2</span></span>
> - <span data-ttu-id="97a4a-119">OData 版本 3</span><span class="sxs-lookup"><span data-stu-id="97a4a-119">OData Version 3</span></span>
> - <span data-ttu-id="97a4a-120">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="97a4a-120">Entity Framework 6</span></span>
> - [<span data-ttu-id="97a4a-121">Fiddler Web 调试代理 （可选）</span><span class="sxs-lookup"><span data-stu-id="97a4a-121">Fiddler Web Debugging Proxy (Optional)</span></span>](http://www.fiddler2.com)
> 
> <span data-ttu-id="97a4a-122">在添加了 web API OData 支持[ASP.NET 和 Web Tools 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。</span><span class="sxs-lookup"><span data-stu-id="97a4a-122">Web API OData support was added in [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=282650).</span></span> <span data-ttu-id="97a4a-123">但是，本教程使用已添加到 Visual Studio 2013 中的基架。</span><span class="sxs-lookup"><span data-stu-id="97a4a-123">However, this tutorial uses scaffolding that was added in Visual Studio 2013.</span></span>


<span data-ttu-id="97a4a-124">在本教程中，你将创建一个简单的 OData 终结点的客户端可以查询。</span><span class="sxs-lookup"><span data-stu-id="97a4a-124">In this tutorial, you will create a simple OData endpoint that clients can query.</span></span> <span data-ttu-id="97a4a-125">你还将创建的 C# 客户端终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-125">You will also create a C# client for the endpoint.</span></span> <span data-ttu-id="97a4a-126">完成本教程后，接下来的教程演示如何添加更多的功能，包括实体关系，操作，然后展开的 $/ $选择。</span><span class="sxs-lookup"><span data-stu-id="97a4a-126">After you complete this tutorial, the next set of tutorials show how to add more functionality, including entity relations, actions, and $expand/$select.</span></span>

- [<span data-ttu-id="97a4a-127">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="97a4a-127">Create the Visual Studio Project</span></span>](#create-project)
- [<span data-ttu-id="97a4a-128">添加实体模型</span><span class="sxs-lookup"><span data-stu-id="97a4a-128">Add an Entity Model</span></span>](#add-model)
- [<span data-ttu-id="97a4a-129">添加一个 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="97a4a-129">Add an OData Controller</span></span>](#add-controller)
- [<span data-ttu-id="97a4a-130">添加的 EDM 和路由</span><span class="sxs-lookup"><span data-stu-id="97a4a-130">Add the EDM and Route</span></span>](#edm)
- [<span data-ttu-id="97a4a-131">种子数据库 （可选）</span><span class="sxs-lookup"><span data-stu-id="97a4a-131">Seed the Database (Optional)</span></span>](#seed-db)
- [<span data-ttu-id="97a4a-132">浏览 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="97a4a-132">Exploring the OData Endpoint</span></span>](#explore)
- [<span data-ttu-id="97a4a-133">OData 序列化格式</span><span class="sxs-lookup"><span data-stu-id="97a4a-133">OData Serialization Formats</span></span>](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a><span data-ttu-id="97a4a-134">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="97a4a-134">Create the Visual Studio Project</span></span>

<span data-ttu-id="97a4a-135">在本教程中，你将创建一个支持基本的 CRUD 操作的 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-135">In this tutorial, you will create an OData endpoint that supports basic CRUD operations.</span></span> <span data-ttu-id="97a4a-136">终结点将公开单个资源，产品的列表。</span><span class="sxs-lookup"><span data-stu-id="97a4a-136">The endpoint will expose a single resource, a list of products.</span></span> <span data-ttu-id="97a4a-137">更高版本的教程将添加更多的功能。</span><span class="sxs-lookup"><span data-stu-id="97a4a-137">Later tutorials will add more features.</span></span>

<span data-ttu-id="97a4a-138">启动 Visual Studio 并选择**新项目**从开始页。</span><span class="sxs-lookup"><span data-stu-id="97a4a-138">Start Visual Studio and select **New Project** from the Start page.</span></span> <span data-ttu-id="97a4a-139">或从**文件**菜单上，选择**新建**然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-139">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="97a4a-140">在**模板**窗格中，选择**已安装的模板**和展开 Visual C# 节点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-140">In the **Templates** pane, select **Installed Templates** and expand the Visual C# node.</span></span> <span data-ttu-id="97a4a-141">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-141">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="97a4a-142">选择**ASP.NET Web 应用程序**模板。</span><span class="sxs-lookup"><span data-stu-id="97a4a-142">Select **the ASP.NET Web Application** template.</span></span>

![](creating-an-odata-endpoint/_static/image1.png)

<span data-ttu-id="97a4a-143">在**新建 ASP.NET 项目**对话框中，选择**空**模板。</span><span class="sxs-lookup"><span data-stu-id="97a4a-143">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="97a4a-144">下&quot;将文件夹添加和核心引用...&quot;，检查**Web API**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-144">Under &quot;Add folders and core references for...&quot;, check **Web API**.</span></span> <span data-ttu-id="97a4a-145">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-145">Click **OK**.</span></span>

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a><span data-ttu-id="97a4a-146">添加实体模型</span><span class="sxs-lookup"><span data-stu-id="97a4a-146">Add an Entity Model</span></span>

<span data-ttu-id="97a4a-147">模型是表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="97a4a-147">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="97a4a-148">对于本教程，我们需要表示产品的模型。</span><span class="sxs-lookup"><span data-stu-id="97a4a-148">For this tutorial, we need a model that represents a product.</span></span> <span data-ttu-id="97a4a-149">模型对应于我们 OData 实体类型。</span><span class="sxs-lookup"><span data-stu-id="97a4a-149">The model corresponds to our OData entity type.</span></span>

<span data-ttu-id="97a4a-150">在解决方案资源管理器，右键单击模型文件夹。</span><span class="sxs-lookup"><span data-stu-id="97a4a-150">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="97a4a-151">从上下文菜单中，选择**添加**然后选择**类**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-151">From the context menu, select **Add** then select **Class**.</span></span>

![](creating-an-odata-endpoint/_static/image3.png)

<span data-ttu-id="97a4a-152">在**添加新**项对话框，将类&quot;产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="97a4a-152">In the **Add New** Item dialog, name the class &quot;Product&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="97a4a-153">按照约定，模型类放置在模型文件夹中。</span><span class="sxs-lookup"><span data-stu-id="97a4a-153">By convention, model classes are placed in the Models folder.</span></span> <span data-ttu-id="97a4a-154">无需遵循此约定在你自己的项目中，但我们将在本教程中使用它。</span><span class="sxs-lookup"><span data-stu-id="97a4a-154">You don't have to follow this convention in your own projects, but we'll use it for this tutorial.</span></span>


<span data-ttu-id="97a4a-155">在 Product.cs 文件中，添加以下类定义：</span><span class="sxs-lookup"><span data-stu-id="97a4a-155">In the Product.cs file, add the following class definition:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

<span data-ttu-id="97a4a-156">ID 属性将为实体键。</span><span class="sxs-lookup"><span data-stu-id="97a4a-156">The ID property will be the entity key.</span></span> <span data-ttu-id="97a4a-157">客户端可以查询 id 的产品</span><span class="sxs-lookup"><span data-stu-id="97a4a-157">Clients can query products by ID.</span></span> <span data-ttu-id="97a4a-158">此字段还将后端数据库中的主键。</span><span class="sxs-lookup"><span data-stu-id="97a4a-158">This field would also be the primary key in the back-end database.</span></span>

<span data-ttu-id="97a4a-159">现在生成项目。</span><span class="sxs-lookup"><span data-stu-id="97a4a-159">Build the project now.</span></span> <span data-ttu-id="97a4a-160">在下一步的步骤中，我们将使用某些 Visual Studio 基架使用反射来找到的产品类型。</span><span class="sxs-lookup"><span data-stu-id="97a4a-160">In the next step, we'll use some Visual Studio scaffolding that uses reflection to find the Product type.</span></span>

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a><span data-ttu-id="97a4a-161">添加一个 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="97a4a-161">Add an OData Controller</span></span>

<span data-ttu-id="97a4a-162">A*控制器*是处理 HTTP 请求的类。</span><span class="sxs-lookup"><span data-stu-id="97a4a-162">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="97a4a-163">定义每个实体集在你的 OData 服务的单独控制器。</span><span class="sxs-lookup"><span data-stu-id="97a4a-163">You define a separate controller for each entity set in you OData service.</span></span> <span data-ttu-id="97a4a-164">在本教程中，我们将创建一个控制器。</span><span class="sxs-lookup"><span data-stu-id="97a4a-164">In this tutorial, we'll create a single controller.</span></span>

<span data-ttu-id="97a4a-165">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="97a4a-165">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="97a4a-166">选择**添加**，然后选择**控制器**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-166">Select **Add** and then select **Controller**.</span></span>

![](creating-an-odata-endpoint/_static/image5.png)

<span data-ttu-id="97a4a-167">在**添加基架**对话框中，选择&quot;Web API 2 OData 控制器其操作使用 Entity Framework&quot;。</span><span class="sxs-lookup"><span data-stu-id="97a4a-167">In the **Add Scaffold** dialog, select &quot;Web API 2 OData Controller with actions, using Entity Framework&quot;.</span></span>

![](creating-an-odata-endpoint/_static/image6.png)

<span data-ttu-id="97a4a-168">在**添加控制器**对话框中，控制器"ProductsController"。</span><span class="sxs-lookup"><span data-stu-id="97a4a-168">In the **Add Controller** dialog, name the controller "ProductsController".</span></span> <span data-ttu-id="97a4a-169">选择&quot;使用异步控制器操作&quot;复选框。</span><span class="sxs-lookup"><span data-stu-id="97a4a-169">Select the &quot;Use async controller actions&quot; checkbox.</span></span> <span data-ttu-id="97a4a-170">在**模型**下拉列表中，选择产品类别。</span><span class="sxs-lookup"><span data-stu-id="97a4a-170">In the **Model** drop-down list, select the Product class.</span></span>

![](creating-an-odata-endpoint/_static/image7.png)

<span data-ttu-id="97a4a-171">单击**新建数据上下文...**按钮。</span><span class="sxs-lookup"><span data-stu-id="97a4a-171">Click the **New data context...** button.</span></span> <span data-ttu-id="97a4a-172">保留的数据上下文类型的默认名称，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-172">Leave the default name for the data context type, and click **Add**.</span></span>

![](creating-an-odata-endpoint/_static/image8.png)

<span data-ttu-id="97a4a-173">在添加控制器对话框添加控制器中，单击添加。</span><span class="sxs-lookup"><span data-stu-id="97a4a-173">Click Add in the Add Controller dialog to add the controller.</span></span>

![](creating-an-odata-endpoint/_static/image9.png)

<span data-ttu-id="97a4a-174">注意： 是否你收到一条错误消息，指出&quot;时出错，获取类型...&quot;，请确保添加产品类后生成 Visual Studio 项目。</span><span class="sxs-lookup"><span data-stu-id="97a4a-174">Note: If you get an error message that says &quot;There was an error getting the type...&quot;, make sure that you built the Visual Studio project after you added the Product class.</span></span> <span data-ttu-id="97a4a-175">基架使用反射来查找类。</span><span class="sxs-lookup"><span data-stu-id="97a4a-175">The scaffolding uses reflection to find the class.</span></span>

![](creating-an-odata-endpoint/_static/image10.png)

<span data-ttu-id="97a4a-176">基架添加到项目的两个代码文件：</span><span class="sxs-lookup"><span data-stu-id="97a4a-176">The scaffolding adds two code files to the project:</span></span>

- <span data-ttu-id="97a4a-177">Products.cs 定义实现 OData 终结点的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="97a4a-177">Products.cs defines the Web API controller that implements the OData endpoint.</span></span>
- <span data-ttu-id="97a4a-178">ProductServiceContext.cs 提供方法来查询使用实体框架的基础数据库。</span><span class="sxs-lookup"><span data-stu-id="97a4a-178">ProductServiceContext.cs provides methods to query the underlying database, using Entity Framework.</span></span>

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a><span data-ttu-id="97a4a-179">添加的 EDM 和路由</span><span class="sxs-lookup"><span data-stu-id="97a4a-179">Add the EDM and Route</span></span>

<span data-ttu-id="97a4a-180">在解决方案资源管理器，展开应用程序\_启动文件夹并打开名为 WebApiConfig.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="97a4a-180">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="97a4a-181">此类包含 Web API 的配置代码。</span><span class="sxs-lookup"><span data-stu-id="97a4a-181">This class holds configuration code for Web API.</span></span> <span data-ttu-id="97a4a-182">将替换为以下这段代码：</span><span class="sxs-lookup"><span data-stu-id="97a4a-182">Replace this code with the following:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

<span data-ttu-id="97a4a-183">此代码执行两项操作：</span><span class="sxs-lookup"><span data-stu-id="97a4a-183">This code does two things:</span></span>

- <span data-ttu-id="97a4a-184">创建实体数据模型 (EDM) 的 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-184">Creates an Entity Data Model (EDM) for the OData endpoint.</span></span>
- <span data-ttu-id="97a4a-185">添加终结点的路由。</span><span class="sxs-lookup"><span data-stu-id="97a4a-185">Adds a route for the endpoint.</span></span>

<span data-ttu-id="97a4a-186">EDM 是一个抽象模型的数据。</span><span class="sxs-lookup"><span data-stu-id="97a4a-186">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="97a4a-187">EDM 用于创建元数据文档并定义服务的 Uri。</span><span class="sxs-lookup"><span data-stu-id="97a4a-187">The EDM is used to create the metadata document and define the URIs for the service.</span></span> <span data-ttu-id="97a4a-188">**ODataConventionModelBuilder**使用一组默认的命名约定 EDM 创建 EDM 的实体。</span><span class="sxs-lookup"><span data-stu-id="97a4a-188">The **ODataConventionModelBuilder** creates an EDM by using a set of default naming conventions EDM.</span></span> <span data-ttu-id="97a4a-189">此方法要求最少的代码。</span><span class="sxs-lookup"><span data-stu-id="97a4a-189">This approach requires the least code.</span></span> <span data-ttu-id="97a4a-190">如果你想 EDM 的更好地控制，则可以使用**ODataModelBuilder**类以创建 EDM 显式添加属性、 密钥和导航属性。</span><span class="sxs-lookup"><span data-stu-id="97a4a-190">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="97a4a-191">**EntitySet**方法将添加的实体集 EDM 到：</span><span class="sxs-lookup"><span data-stu-id="97a4a-191">The **EntitySet** method adds an entity set to the EDM:</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

<span data-ttu-id="97a4a-192">字符串"Products"定义的实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="97a4a-192">The string "Products" defines the name of the entity set.</span></span> <span data-ttu-id="97a4a-193">控制器的名称必须匹配的实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="97a4a-193">The name of the controller must match the name of the entity set.</span></span> <span data-ttu-id="97a4a-194">在本教程中，实体集的名称为"Products"和控制器命名为`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="97a4a-194">In this tutorial, the entity set is named "Products" and the controller is named `ProductsController`.</span></span> <span data-ttu-id="97a4a-195">如果你名为的实体集"ProductSet"，你需要命名控制器`ProductSetController`。</span><span class="sxs-lookup"><span data-stu-id="97a4a-195">If you named the entity set "ProductSet", you would name the controller `ProductSetController`.</span></span> <span data-ttu-id="97a4a-196">请注意，终结点可以有多个实体集。</span><span class="sxs-lookup"><span data-stu-id="97a4a-196">Note that an endpoint can have multiple entity sets.</span></span> <span data-ttu-id="97a4a-197">调用**EntitySet&lt;T&gt;** 有关每个实体，以及然后定义一个相应的控制器。</span><span class="sxs-lookup"><span data-stu-id="97a4a-197">Call **EntitySet&lt;T&gt;** for each entity set, and then define a corresponding controller.</span></span>

<span data-ttu-id="97a4a-198">**MapODataRoute**方法将添加 OData 终结点的路由。</span><span class="sxs-lookup"><span data-stu-id="97a4a-198">The **MapODataRoute** method adds a route for the OData endpoint.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

<span data-ttu-id="97a4a-199">第一个参数是路由的友好名称。</span><span class="sxs-lookup"><span data-stu-id="97a4a-199">The first parameter is a friendly name for the route.</span></span> <span data-ttu-id="97a4a-200">你的服务的客户端不会看到此名称。</span><span class="sxs-lookup"><span data-stu-id="97a4a-200">Clients of your service do not see this name.</span></span> <span data-ttu-id="97a4a-201">第二个参数是终结点的 URI 前缀。</span><span class="sxs-lookup"><span data-stu-id="97a4a-201">The second parameter is the URI prefix for the endpoint.</span></span> <span data-ttu-id="97a4a-202">给定此代码，Products 实体集的 URI 是 http://<em>主机名</em>  /odata/产品。</span><span class="sxs-lookup"><span data-stu-id="97a4a-202">Given this code, the URI for the Products entity set is http://<em>hostname</em>/odata/Products.</span></span> <span data-ttu-id="97a4a-203">你的应用程序可以具有多个 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-203">Your application can have more than one OData endpoint.</span></span> <span data-ttu-id="97a4a-204">对于每个终结点，调用<strong>MapODataRoute</strong>提供唯一的路由名称和唯一的 URI 前缀。</span><span class="sxs-lookup"><span data-stu-id="97a4a-204">For each endpoint, call <strong>MapODataRoute</strong> and provide a unique route name and a unique URI prefix.</span></span>

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a><span data-ttu-id="97a4a-205">种子数据库 （可选）</span><span class="sxs-lookup"><span data-stu-id="97a4a-205">Seed the Database (Optional)</span></span>

<span data-ttu-id="97a4a-206">在此步骤中，你将使用实体框架植入到数据库的某些测试数据。</span><span class="sxs-lookup"><span data-stu-id="97a4a-206">In this step, you will use Entity Framework to seed the database with some test data.</span></span> <span data-ttu-id="97a4a-207">此步骤是可选的但它可让你立即测试 OData 终结点。</span><span class="sxs-lookup"><span data-stu-id="97a4a-207">This step is optional, but it lets you test out your OData endpoint right away.</span></span>

<span data-ttu-id="97a4a-208">从**工具**菜单上，选择**库程序包管理器**，然后选择**程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-208">From the **Tools** menu, select **Library Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="97a4a-209">在 Package Manager Console 窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="97a4a-209">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

<span data-ttu-id="97a4a-210">这将添加名为迁移和名为 Configuration.cs 代码文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="97a4a-210">This adds a folder named Migrations and a code file named Configuration.cs.</span></span>

![](creating-an-odata-endpoint/_static/image12.png)

<span data-ttu-id="97a4a-211">打开此文件并添加以下代码`Configuration.Seed`方法。</span><span class="sxs-lookup"><span data-stu-id="97a4a-211">Open this file and add the following code to the `Configuration.Seed` method.</span></span>

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

<span data-ttu-id="97a4a-212">在程序包管理器控制台窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="97a4a-212">In the Package Manager Console Window, enter the following commands:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

<span data-ttu-id="97a4a-213">这些命令生成创建数据库，并将执行该代码的代码。</span><span class="sxs-lookup"><span data-stu-id="97a4a-213">These commands generate code that creates the database, and then executes that code.</span></span>

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a><span data-ttu-id="97a4a-214">浏览 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="97a4a-214">Exploring the OData Endpoint</span></span>

<span data-ttu-id="97a4a-215">在本部分中，我们将使用[Fiddler Web 调试代理](http://www.fiddler2.com)将请求发送到终结点并检查响应消息。</span><span class="sxs-lookup"><span data-stu-id="97a4a-215">In this section, we'll use the [Fiddler Web Debugging Proxy](http://www.fiddler2.com) to send requests to the endpoint and examine the response messages.</span></span> <span data-ttu-id="97a4a-216">这将帮助你了解 OData 终结点的功能。</span><span class="sxs-lookup"><span data-stu-id="97a4a-216">This will help you to understand the capabilities of an OData endpoint.</span></span>

<span data-ttu-id="97a4a-217">在 Visual Studio 中，按 F5 启动调试。</span><span class="sxs-lookup"><span data-stu-id="97a4a-217">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="97a4a-218">默认情况下，Visual Studio 将打开浏览器指向`http://localhost:*port*`，其中*端口*是在项目设置中配置的端口号。</span><span class="sxs-lookup"><span data-stu-id="97a4a-218">By default, Visual Studio opens your browser to `http://localhost:*port*`, where *port* is the port number configured in the project settings.</span></span>

<span data-ttu-id="97a4a-219">你可以更改项目设置中的端口号。</span><span class="sxs-lookup"><span data-stu-id="97a4a-219">You can change the port number in the project settings.</span></span> <span data-ttu-id="97a4a-220">在解决方案资源管理器，右键单击该项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-220">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="97a4a-221">在属性窗口中，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-221">In the properties window, select **Web**.</span></span> <span data-ttu-id="97a4a-222">输入下的端口号**项目 Url**。</span><span class="sxs-lookup"><span data-stu-id="97a4a-222">Enter the port number under **Project Url**.</span></span>

### <a name="service-document"></a><span data-ttu-id="97a4a-223">服务文档</span><span class="sxs-lookup"><span data-stu-id="97a4a-223">Service Document</span></span>

<span data-ttu-id="97a4a-224">*服务文档*包含 OData 终结点的实体集的列表。</span><span class="sxs-lookup"><span data-stu-id="97a4a-224">The *service document* contains a list of the entity sets for the OData endpoint.</span></span> <span data-ttu-id="97a4a-225">若要获取服务文档，请对根 URI 的服务发送 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="97a4a-225">To get the service document, send a GET request to the root URI of the service.</span></span>

<span data-ttu-id="97a4a-226">使用 Fiddler，输入以下 URI 中的**Composer**选项卡： `http://localhost:port/odata/`，其中*端口*是端口号。</span><span class="sxs-lookup"><span data-stu-id="97a4a-226">Using Fiddler, enter the following URI in the **Composer** tab: `http://localhost:port/odata/`, where *port* is the port number.</span></span>

![](creating-an-odata-endpoint/_static/image13.png)

<span data-ttu-id="97a4a-227">单击**执行**按钮。</span><span class="sxs-lookup"><span data-stu-id="97a4a-227">Click the **Execute** button.</span></span> <span data-ttu-id="97a4a-228">Fiddler 将 HTTP GET 请求发送到你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="97a4a-228">Fiddler sends an HTTP GET request to your application.</span></span> <span data-ttu-id="97a4a-229">你应看到 Web 会话列表中的响应。</span><span class="sxs-lookup"><span data-stu-id="97a4a-229">You should see the response in the Web Sessions list.</span></span> <span data-ttu-id="97a4a-230">如果一切正常，则状态代码将为 200。</span><span class="sxs-lookup"><span data-stu-id="97a4a-230">If everything is working, the status code will be 200.</span></span>

![](creating-an-odata-endpoint/_static/image14.png)

<span data-ttu-id="97a4a-231">双击 Web 会话列表以查看检查器选项卡中的响应消息的详细信息中的响应。</span><span class="sxs-lookup"><span data-stu-id="97a4a-231">Double-click the response in the Web Sessions list to see the details of the response message in the Inspectors tab.</span></span>

![](creating-an-odata-endpoint/_static/image15.png)

<span data-ttu-id="97a4a-232">原始 HTTP 响应消息应类似于以下形式：</span><span class="sxs-lookup"><span data-stu-id="97a4a-232">The raw HTTP response message should look similar to the following:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

<span data-ttu-id="97a4a-233">默认情况下，Web API AtomPub 格式返回服务文档。</span><span class="sxs-lookup"><span data-stu-id="97a4a-233">By default, Web API returns the service document in AtomPub format.</span></span> <span data-ttu-id="97a4a-234">若要请求 JSON，请对 HTTP 请求中添加以下标头：</span><span class="sxs-lookup"><span data-stu-id="97a4a-234">To request JSON, add the following header to the HTTP request:</span></span>

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

<span data-ttu-id="97a4a-235">现在 HTTP 响应包含 JSON 负载：</span><span class="sxs-lookup"><span data-stu-id="97a4a-235">Now the HTTP response contains a JSON payload:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a><span data-ttu-id="97a4a-236">服务元数据文档</span><span class="sxs-lookup"><span data-stu-id="97a4a-236">Service Metadata Document</span></span>

<span data-ttu-id="97a4a-237">*服务元数据文档*描述服务中，使用一种称为概念架构定义语言 (CSDL) 的 XML 语言的数据模型。</span><span class="sxs-lookup"><span data-stu-id="97a4a-237">The *service metadata document* describes the data model of the service, using an XML language called the Conceptual Schema Definition Language (CSDL).</span></span> <span data-ttu-id="97a4a-238">元数据文档在服务中，显示的数据的结构，可以用于生成客户端代码。</span><span class="sxs-lookup"><span data-stu-id="97a4a-238">The metadata document shows the structure of the data in the service, and can be used to generate client code.</span></span>

<span data-ttu-id="97a4a-239">若要获取的元数据文档，发送 GET 请求到`http://localhost:port/odata/$metadata`。</span><span class="sxs-lookup"><span data-stu-id="97a4a-239">To get the metadata document, send a GET request to `http://localhost:port/odata/$metadata`.</span></span> <span data-ttu-id="97a4a-240">下面是本教程中所示的终结点的元数据。</span><span class="sxs-lookup"><span data-stu-id="97a4a-240">Here is the metadata for the endpoint shown in this tutorial.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a><span data-ttu-id="97a4a-241">实体集</span><span class="sxs-lookup"><span data-stu-id="97a4a-241">Entity Set</span></span>

<span data-ttu-id="97a4a-242">若要获取的产品实体集，发送 GET 请求到`http://localhost:port/odata/Products`。</span><span class="sxs-lookup"><span data-stu-id="97a4a-242">To get the Products entity set, send a GET request to `http://localhost:port/odata/Products`.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a><span data-ttu-id="97a4a-243">实体</span><span class="sxs-lookup"><span data-stu-id="97a4a-243">Entity</span></span>

<span data-ttu-id="97a4a-244">若要获取各个产品，发送 GET 请求到`http://localhost:port/odata/Products(1)`，其中"1"是产品 id。</span><span class="sxs-lookup"><span data-stu-id="97a4a-244">To get an individual product, send a GET request to `http://localhost:port/odata/Products(1)`, where "1" is the product ID.</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a><span data-ttu-id="97a4a-245">OData 序列化格式</span><span class="sxs-lookup"><span data-stu-id="97a4a-245">OData Serialization Formats</span></span>

<span data-ttu-id="97a4a-246">OData 支持几种序列化格式：</span><span class="sxs-lookup"><span data-stu-id="97a4a-246">OData supports several serialization formats:</span></span>

- <span data-ttu-id="97a4a-247">Atom 发布 (XML)</span><span class="sxs-lookup"><span data-stu-id="97a4a-247">Atom Pub (XML)</span></span>
- <span data-ttu-id="97a4a-248">JSON"light"（在 OData v3 中引入）</span><span class="sxs-lookup"><span data-stu-id="97a4a-248">JSON "light" (introduced in OData v3)</span></span>
- <span data-ttu-id="97a4a-249">JSON"详细"(OData v2)</span><span class="sxs-lookup"><span data-stu-id="97a4a-249">JSON "verbose" (OData v2)</span></span>

<span data-ttu-id="97a4a-250">默认情况下，Web API 使用 AtomPubJSON"light"格式。</span><span class="sxs-lookup"><span data-stu-id="97a4a-250">By default, Web API uses AtomPubJSON "light" format.</span></span> 

<span data-ttu-id="97a4a-251">若要获取 AtomPub 格式，请设置为"application/atom + xml"Accept 标头。</span><span class="sxs-lookup"><span data-stu-id="97a4a-251">To get AtomPub format, set the Accept header to "application/atom+xml".</span></span> <span data-ttu-id="97a4a-252">下面是一个示例响应正文：</span><span class="sxs-lookup"><span data-stu-id="97a4a-252">Here is an example response body:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

<span data-ttu-id="97a4a-253">你可以看到的 Atom 格式的一个明显缺点： 它是大量比详细 JSON light。</span><span class="sxs-lookup"><span data-stu-id="97a4a-253">You can see one obvious disadvantage of the Atom format: It's a lot more verbose than the JSON light.</span></span> <span data-ttu-id="97a4a-254">但是，如果必须理解 AtomPub 的客户端，则客户端可能通过 JSON 希望该格式。</span><span class="sxs-lookup"><span data-stu-id="97a4a-254">However, if you have a client that understands AtomPub, the client might prefer that format over JSON.</span></span>

<span data-ttu-id="97a4a-255">下面是实体的 JSON 轻量版本的相同:</span><span class="sxs-lookup"><span data-stu-id="97a4a-255">Here is the JSON light version of the same entity:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

<span data-ttu-id="97a4a-256">OData 协议版本 3 中引入了 JSON 浅色格式。</span><span class="sxs-lookup"><span data-stu-id="97a4a-256">The JSON light format was introduced in version 3 of the OData protocol.</span></span> <span data-ttu-id="97a4a-257">为了向后兼容性，客户端可以请求的较旧的"详细"JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="97a4a-257">For backward compatibility, a client can request the older "verbose" JSON format.</span></span> <span data-ttu-id="97a4a-258">若要请求详细 JSON，请将 Accept 标头设置为`application/json;odata=verbose`。</span><span class="sxs-lookup"><span data-stu-id="97a4a-258">To request verbose JSON, set the Accept header to `application/json;odata=verbose`.</span></span> <span data-ttu-id="97a4a-259">以下是详细的版本：</span><span class="sxs-lookup"><span data-stu-id="97a4a-259">Here is the verbose version:</span></span>

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

<span data-ttu-id="97a4a-260">此格式可传达在响应正文中，可以将其添加增加大量开销 over 整个会话的多个元数据。</span><span class="sxs-lookup"><span data-stu-id="97a4a-260">This format conveys more metadata in the response body, which can add considerable overhead over an entire session.</span></span> <span data-ttu-id="97a4a-261">此外，它将添加一定程度的间接性包装在名为"d"的属性的对象。</span><span class="sxs-lookup"><span data-stu-id="97a4a-261">Also, it adds a level of indirection by wrapping the object in a property named "d".</span></span>

## <a name="next-steps"></a><span data-ttu-id="97a4a-262">后续步骤</span><span class="sxs-lookup"><span data-stu-id="97a4a-262">Next Steps</span></span>

- [<span data-ttu-id="97a4a-263">添加实体关系</span><span class="sxs-lookup"><span data-stu-id="97a4a-263">Add Entity Relations</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="97a4a-264">添加 OData 操作</span><span class="sxs-lookup"><span data-stu-id="97a4a-264">Add OData Actions</span></span>](odata-actions.md)
- [<span data-ttu-id="97a4a-265">从.NET 客户端调用 OData 服务</span><span class="sxs-lookup"><span data-stu-id="97a4a-265">Call the OData Service From a .NET Client</span></span>](calling-an-odata-service-from-a-net-client.md)
