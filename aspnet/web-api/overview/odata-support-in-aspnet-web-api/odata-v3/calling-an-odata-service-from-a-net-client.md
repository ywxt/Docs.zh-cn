---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: 从.NET 客户端 (C#) 调用 OData 服务 |Microsoft Docs
author: MikeWasson
description: 本教程演示如何从 C# 客户端应用程序调用 OData 服务。 在教程的 Visual Studio 2013 （适用于 Visual S...中使用的软件版本
ms.author: aspnetcontent
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 72dca7dc2ec27f15c9f0526621a713267f5835f8
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819550"
---
<a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="f707d-104">从.NET 客户端 (C#) 调用 OData 服务</span><span class="sxs-lookup"><span data-stu-id="f707d-104">Calling an OData Service From a .NET Client (C#)</span></span>
====================
<span data-ttu-id="f707d-105">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="f707d-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="f707d-106">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="f707d-106">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="f707d-107">本教程演示如何从 C# 客户端应用程序调用 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="f707d-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f707d-108">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="f707d-108">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f707d-109">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) （适用于 Visual Studio 2012）</span><span class="sxs-lookup"><span data-stu-id="f707d-109">[Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="f707d-110">WCF Data Services 客户端库</span><span class="sxs-lookup"><span data-stu-id="f707d-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="f707d-111">Web API 2。</span><span class="sxs-lookup"><span data-stu-id="f707d-111">Web API 2.</span></span> <span data-ttu-id="f707d-112">（使用 Web API 2，生成 OData 服务的示例，但客户端应用程序不依赖于 Web API）。</span><span class="sxs-lookup"><span data-stu-id="f707d-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>


<span data-ttu-id="f707d-113">在本教程中，我将逐步创建调用 OData 服务的客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="f707d-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="f707d-114">OData 服务公开以下实体：</span><span class="sxs-lookup"><span data-stu-id="f707d-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="f707d-115">以下文章介绍了如何在 Web API 中实现 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="f707d-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="f707d-116">（不需要读取它们能够了解本教程中，但是工作。）</span><span class="sxs-lookup"><span data-stu-id="f707d-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="f707d-117">在 Web API 2 中创建 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="f707d-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="f707d-118">Web API 2 中的 OData 实体关系</span><span class="sxs-lookup"><span data-stu-id="f707d-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="f707d-119">Web API 2 中的 OData 操作</span><span class="sxs-lookup"><span data-stu-id="f707d-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="f707d-120">生成服务代理</span><span class="sxs-lookup"><span data-stu-id="f707d-120">Generate the Service Proxy</span></span>

<span data-ttu-id="f707d-121">第一步是生成服务代理。</span><span class="sxs-lookup"><span data-stu-id="f707d-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="f707d-122">服务代理是一个.NET 类定义用于访问 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="f707d-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="f707d-123">代理将转换为 HTTP 请求的方法调用。</span><span class="sxs-lookup"><span data-stu-id="f707d-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="f707d-124">首先在 Visual Studio 中打开 OData 服务项目。</span><span class="sxs-lookup"><span data-stu-id="f707d-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="f707d-125">按 CTRL + F5 以在 IIS Express 中本地运行服务。</span><span class="sxs-lookup"><span data-stu-id="f707d-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="f707d-126">请注意本地地址，包括 Visual Studio 将分配的端口号。</span><span class="sxs-lookup"><span data-stu-id="f707d-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="f707d-127">在创建代理时，你将需要此地址。</span><span class="sxs-lookup"><span data-stu-id="f707d-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="f707d-128">接下来，打开 Visual Studio 的另一个实例并创建一个控制台应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="f707d-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="f707d-129">控制台应用程序将是我们的 OData 客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="f707d-129">The console application will be our OData client application.</span></span> <span data-ttu-id="f707d-130">（您还可以添加项目到与服务相同的解决方案。）</span><span class="sxs-lookup"><span data-stu-id="f707d-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="f707d-131">剩余的步骤，请参阅控制台项目。</span><span class="sxs-lookup"><span data-stu-id="f707d-131">The remaining steps refer the console project.</span></span>


<span data-ttu-id="f707d-132">在解决方案资源管理器中右键单击**引用**，然后选择**添加服务引用**。</span><span class="sxs-lookup"><span data-stu-id="f707d-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="f707d-133">在中**添加服务引用**对话框中，键入 OData 服务的地址：</span><span class="sxs-lookup"><span data-stu-id="f707d-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="f707d-134">其中*端口*是端口号。</span><span class="sxs-lookup"><span data-stu-id="f707d-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="f707d-135">有关**Namespace**，键入"ProductService"。</span><span class="sxs-lookup"><span data-stu-id="f707d-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="f707d-136">此选项定义的代理类的命名空间。</span><span class="sxs-lookup"><span data-stu-id="f707d-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="f707d-137">单击 **“转到”**。</span><span class="sxs-lookup"><span data-stu-id="f707d-137">Click **Go**.</span></span> <span data-ttu-id="f707d-138">Visual Studio 读取 OData 元数据文档来发现服务中的实体。</span><span class="sxs-lookup"><span data-stu-id="f707d-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="f707d-139">单击**确定**将代理类添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="f707d-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="f707d-140">创建服务代理类的实例</span><span class="sxs-lookup"><span data-stu-id="f707d-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="f707d-141">在你`Main`方法中，创建代理类的新实例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f707d-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="f707d-142">同样，使用运行你的服务的实际端口号。</span><span class="sxs-lookup"><span data-stu-id="f707d-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="f707d-143">在部署你的服务时，将使用实时服务的 URI。</span><span class="sxs-lookup"><span data-stu-id="f707d-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="f707d-144">不需要更新该代理。</span><span class="sxs-lookup"><span data-stu-id="f707d-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="f707d-145">以下代码添加事件处理程序将打印到控制台窗口的请求 Uri。</span><span class="sxs-lookup"><span data-stu-id="f707d-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="f707d-146">此步骤并不是必需的但很高兴地发现每个查询的 Uri。</span><span class="sxs-lookup"><span data-stu-id="f707d-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="f707d-147">查询服务</span><span class="sxs-lookup"><span data-stu-id="f707d-147">Query the Service</span></span>

<span data-ttu-id="f707d-148">下面的代码从 OData 服务获取产品的列表。</span><span class="sxs-lookup"><span data-stu-id="f707d-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="f707d-149">请注意，无需编写任何代码来发送 HTTP 请求或分析的响应。</span><span class="sxs-lookup"><span data-stu-id="f707d-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="f707d-150">代理类会自动在枚举`Container.Products`中的集合**foreach**循环。</span><span class="sxs-lookup"><span data-stu-id="f707d-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="f707d-151">当您运行该应用程序时，输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="f707d-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="f707d-152">若要获取 ID 对实体，请使用`where`子句。</span><span class="sxs-lookup"><span data-stu-id="f707d-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="f707d-153">本主题的其余部分，我不会显示整个`Main`函数，只需调用该服务所需的代码。</span><span class="sxs-lookup"><span data-stu-id="f707d-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="f707d-154">应用查询选项</span><span class="sxs-lookup"><span data-stu-id="f707d-154">Apply Query Options</span></span>

<span data-ttu-id="f707d-155">OData 定义[查询选项](../supporting-odata-query-options.md)，可用于筛选器、 排序、 页面数据等。</span><span class="sxs-lookup"><span data-stu-id="f707d-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="f707d-156">在服务代理，可以使用各种 LINQ 表达式来应用这些选项。</span><span class="sxs-lookup"><span data-stu-id="f707d-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="f707d-157">在本部分中，我将介绍简短示例。</span><span class="sxs-lookup"><span data-stu-id="f707d-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="f707d-158">有关更多详细信息，请参阅主题[LINQ 注意事项 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) MSDN 上。</span><span class="sxs-lookup"><span data-stu-id="f707d-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="f707d-159">筛选 ($filter)</span><span class="sxs-lookup"><span data-stu-id="f707d-159">Filtering ($filter)</span></span>

<span data-ttu-id="f707d-160">若要筛选，请使用`where`子句。</span><span class="sxs-lookup"><span data-stu-id="f707d-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="f707d-161">以下示例筛选按产品类别。</span><span class="sxs-lookup"><span data-stu-id="f707d-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="f707d-162">此代码对应于以下 OData 查询。</span><span class="sxs-lookup"><span data-stu-id="f707d-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="f707d-163">请注意，代理将转换`where`OData 子句`$filter`表达式。</span><span class="sxs-lookup"><span data-stu-id="f707d-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="f707d-164">排序 ($orderby)</span><span class="sxs-lookup"><span data-stu-id="f707d-164">Sorting ($orderby)</span></span>

<span data-ttu-id="f707d-165">若要进行排序，请使用`orderby`子句。</span><span class="sxs-lookup"><span data-stu-id="f707d-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="f707d-166">下面的示例按定价从高到低进行排序。</span><span class="sxs-lookup"><span data-stu-id="f707d-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="f707d-167">下面是相应的 OData 请求。</span><span class="sxs-lookup"><span data-stu-id="f707d-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="f707d-168">客户端的分页 （$skip 和 $top）</span><span class="sxs-lookup"><span data-stu-id="f707d-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="f707d-169">大型实体集的客户端可能会想要限制结果数。</span><span class="sxs-lookup"><span data-stu-id="f707d-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="f707d-170">例如，客户端可能会一次显示 10 个条目。</span><span class="sxs-lookup"><span data-stu-id="f707d-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="f707d-171">这称为*客户端分页*。</span><span class="sxs-lookup"><span data-stu-id="f707d-171">This is called *client-side paging*.</span></span> <span data-ttu-id="f707d-172">(此外，还有[服务器端分页](../supporting-odata-query-options.md#server-paging)，其中服务器会限制结果数。)若要执行客户端分页，使用 LINQ**跳过**并**采取**方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="f707d-173">以下示例将跳过前 40 结果，并采用 10 的下一步。</span><span class="sxs-lookup"><span data-stu-id="f707d-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="f707d-174">下面是相应的 OData 请求：</span><span class="sxs-lookup"><span data-stu-id="f707d-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="f707d-175">选择 ($select) 和展开 ($expand)</span><span class="sxs-lookup"><span data-stu-id="f707d-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="f707d-176">若要包括相关的实体，请使用`DataServiceQuery<t>.Expand`方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="f707d-177">例如，若要包括`Supplier`为每个`Product`:</span><span class="sxs-lookup"><span data-stu-id="f707d-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="f707d-178">下面是相应的 OData 请求：</span><span class="sxs-lookup"><span data-stu-id="f707d-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="f707d-179">若要更改的响应的形状，请使用 LINQ**选择**子句。</span><span class="sxs-lookup"><span data-stu-id="f707d-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="f707d-180">下面的示例获取只是每个产品，与任何其他属性的名称。</span><span class="sxs-lookup"><span data-stu-id="f707d-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="f707d-181">下面是相应的 OData 请求：</span><span class="sxs-lookup"><span data-stu-id="f707d-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="f707d-182">Select 子句可以包括相关的实体。</span><span class="sxs-lookup"><span data-stu-id="f707d-182">A select clause can include related entities.</span></span> <span data-ttu-id="f707d-183">在这种情况下，不要调用**展开**; 代理会自动在这种情况下包括的扩展。</span><span class="sxs-lookup"><span data-stu-id="f707d-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="f707d-184">下面的示例获取的名称和每个产品的供应商。</span><span class="sxs-lookup"><span data-stu-id="f707d-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="f707d-185">下面是相应的 OData 请求。</span><span class="sxs-lookup"><span data-stu-id="f707d-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="f707d-186">请注意，它包含 **$expand**选项。</span><span class="sxs-lookup"><span data-stu-id="f707d-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="f707d-187">详细了解 $select 和 $展开，请参阅[使用 $select，$expand、 和 Web API 2 中的 $value](../using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="f707d-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="f707d-188">添加新实体</span><span class="sxs-lookup"><span data-stu-id="f707d-188">Add a New Entity</span></span>

<span data-ttu-id="f707d-189">若要将新实体添加到实体集，调用`AddToEntitySet`，其中*EntitySet*是实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="f707d-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="f707d-190">例如，`AddToProducts`添加一个新`Product`到`Products`实体集。</span><span class="sxs-lookup"><span data-stu-id="f707d-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="f707d-191">在生成代理时，WCF 数据服务会自动创建这些强类型化**AddTo**方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="f707d-192">若要添加两个实体之间的链接，请使用**AddLink**并**SetLink**方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="f707d-193">下面的代码将添加一个新的供应商和一个新产品，然后创建它们之间的链接。</span><span class="sxs-lookup"><span data-stu-id="f707d-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="f707d-194">使用**AddLink**时的导航属性是集合。</span><span class="sxs-lookup"><span data-stu-id="f707d-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="f707d-195">在此示例中，我们将添加到产品`Products`供应商上的集合。</span><span class="sxs-lookup"><span data-stu-id="f707d-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="f707d-196">使用**SetLink**时的导航属性是一个单一实体。</span><span class="sxs-lookup"><span data-stu-id="f707d-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="f707d-197">在此示例中，我们将设置`Supplier`产品上的属性。</span><span class="sxs-lookup"><span data-stu-id="f707d-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="f707d-198">更新/修补程序</span><span class="sxs-lookup"><span data-stu-id="f707d-198">Update / Patch</span></span>

<span data-ttu-id="f707d-199">若要更新实体，请调用**UpdateObject**方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="f707d-200">在调用时执行更新，则**SaveChanges**。</span><span class="sxs-lookup"><span data-stu-id="f707d-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="f707d-201">默认情况下，WCF 发送 HTTP MERGE 请求。</span><span class="sxs-lookup"><span data-stu-id="f707d-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="f707d-202">**PatchOnUpdate**选项告知 WCF 改为发送 HTTP PATCH。</span><span class="sxs-lookup"><span data-stu-id="f707d-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="f707d-203">为什么修补与合并？</span><span class="sxs-lookup"><span data-stu-id="f707d-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="f707d-204">原始 HTTP 1.1 规范 ([RCF 2616](http://tools.ietf.org/html/rfc2616)) 未定义"部分更新"语义与任何 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="f707d-205">若要支持部分更新，OData 规范定义的合并方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="f707d-206">在 2010 中， [RFC 5789](http://tools.ietf.org/html/rfc5789)定义部分更新的修补程序方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="f707d-207">你可以阅读一些的历史记录中这[博客文章](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx)有关 WCF Data Services 博客文章。</span><span class="sxs-lookup"><span data-stu-id="f707d-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="f707d-208">目前，修补程序通过合并是首选。</span><span class="sxs-lookup"><span data-stu-id="f707d-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="f707d-209">Web API 基架创建的 OData 控制器支持这两种方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>


<span data-ttu-id="f707d-210">如果你想要替换整个实体 （PUT 语义），指定**ReplaceOnUpdate**选项。</span><span class="sxs-lookup"><span data-stu-id="f707d-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="f707d-211">这会导致 WCF 发送 HTTP PUT 请求。</span><span class="sxs-lookup"><span data-stu-id="f707d-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="f707d-212">删除实体</span><span class="sxs-lookup"><span data-stu-id="f707d-212">Delete an Entity</span></span>

<span data-ttu-id="f707d-213">若要删除实体，请调用**DeleteObject**。</span><span class="sxs-lookup"><span data-stu-id="f707d-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="f707d-214">调用 OData 操作</span><span class="sxs-lookup"><span data-stu-id="f707d-214">Invoke an OData Action</span></span>

<span data-ttu-id="f707d-215">在 OData 中，[操作](odata-actions.md)是一种方法来添加未轻松地定义为对实体的 CRUD 操作的服务器端行为。</span><span class="sxs-lookup"><span data-stu-id="f707d-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="f707d-216">尽管 OData 元数据文档描述的操作，但代理类不为其创建任何强类型化的方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="f707d-217">还可调用 OData 操作通过使用泛型**Execute**方法。</span><span class="sxs-lookup"><span data-stu-id="f707d-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="f707d-218">但是，需要知道的参数和返回值的数据类型。</span><span class="sxs-lookup"><span data-stu-id="f707d-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="f707d-219">例如，`RateProduct`操作采用名为"Rating"类型的参数`Int32`，并返回`double`。</span><span class="sxs-lookup"><span data-stu-id="f707d-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="f707d-220">下面的代码演示如何调用此操作。</span><span class="sxs-lookup"><span data-stu-id="f707d-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="f707d-221">有关详细信息，请参阅[调用服务操作和动作](https://msdn.microsoft.com/library/hh230677.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f707d-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="f707d-222">一种方法是扩展**容器**类以提供强类型化调用的方法，该操作：</span><span class="sxs-lookup"><span data-stu-id="f707d-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
