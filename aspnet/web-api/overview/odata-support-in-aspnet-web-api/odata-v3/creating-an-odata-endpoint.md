---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: 创建具有 Web API 2 OData v3 终结点 |Microsoft Docs
author: MikeWasson
description: 开放数据协议 (OData) 是一种用于 web 的数据访问协议。 OData 提供统一的方法来构造数据、 查询的数据和操作的数据...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 654f697c8d095d45ba31e2808c52f9ad24b606c8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41833737"
---
<a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>创建具有 Web API 2 OData v3 终结点
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> [开放数据协议](http://www.odata.org/)(OData) 是用于 web 的数据访问协议。 OData 提供统一的方法来构造数据、 查询的数据和操作该数据集通过 CRUD 操作 （创建、 读取、 更新和删除）。 OData 支持 AtomPub (XML) 和 JSON 格式。 OData 还定义了一种方法来公开数据的元数据。 客户端可以使用元数据发现的类型信息和数据集的关系。
> 
> ASP.NET Web API 可以轻松地创建数据集的 OData 终结点。 您可以控制完全的 OData 操作的终结点支持。 你可以托管多个 OData 终结点，以及非 OData 终结点。 您可以完全控制数据模型、 后端业务逻辑和数据层。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - [Visual Studio 2013](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - Web API 2
> - OData 版本 3
> - Entity Framework 6
> - [Fiddler Web 调试代理 （可选）](http://www.fiddler2.com)
> 
> 中增加了 web API OData 支持[ASP.NET 和 Web Tools 2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。 但是，本教程使用 Visual Studio 2013 中已添加的基架。


在本教程中，将创建一个简单的 OData 终结点的客户端可以查询。 您还将创建终结点的 C# 客户端。 完成本教程后下, 一步的系列教程介绍如何添加更多的功能，包括实体关系操作，并展开的 $/ $选择。

- [创建 Visual Studio 项目](#create-project)
- [添加实体模型](#add-model)
- [添加一个 OData 控制器](#add-controller)
- [添加的 EDM 和路由](#edm)
- [（可选） 数据库中植入](#seed-db)
- [探索 OData 终结点](#explore)
- [OData 序列化格式](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

在本教程中，将创建支持基本的 CRUD 操作的 OData 终结点。 终结点将公开单个资源，产品列表。 后续教程将添加更多的功能。

启动 Visual Studio 并选择**新的项目**从起始页。 或者，从**文件**菜单中，选择**新建**，然后**项目**。

在中**模板**窗格中，选择**已安装的模板**并展开 Visual C# 节点。 下**Visual C#**，选择**Web**。 选择**ASP.NET Web 应用程序**模板。

![](creating-an-odata-endpoint/_static/image1.png)

在中**新建 ASP.NET 项目**对话框中，选择**空**模板。 下&quot;添加文件夹和核心引用...&quot;，检查**Web API**。 单击 **“确定”**。

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>添加实体模型

模型是表示应用程序中的数据的对象。 本教程中，我们需要表示产品的模型。 模型对应于我们的 OData 实体类型。

在解决方案资源管理器，右键单击模型文件夹。 从上下文菜单中，选择**外**然后选择**类**。

![](creating-an-odata-endpoint/_static/image3.png)

在中**新添**项对话框中，类命名&quot;产品&quot;。

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 按照约定，模型类位于 Models 文件夹中。 无需遵循此约定在您自己的项目，但我们将在本教程中使用它。


在 Product.cs 文件中，添加以下类定义：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID 属性将为实体键。 客户端可以查询产品的 id。 此字段也是后端数据库中的主键。

现在生成项目。 在下一步，我们将使用一些使用反射来查找产品类型的 Visual Studio 基架。

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>添加一个 OData 控制器

一个*控制器*是处理 HTTP 请求的类。 定义每个实体在你的 OData 服务中设置单独的控制器。 在本教程中，我们将创建一个控制器。

在解决方案资源管理器，右键单击 Controllers 文件夹。 选择**外**，然后选择**控制器**。

![](creating-an-odata-endpoint/_static/image5.png)

在中**添加基架**对话框中，选择&quot;包含 Web API 2 OData 控制器操作，使用实体框架&quot;。

![](creating-an-odata-endpoint/_static/image6.png)

在中**添加控制器**对话框中，将控制器"ProductsController"。 选择&quot;使用异步控制器操作&quot;复选框。 在中**模型**下拉列表中，选择 Product 类。

![](creating-an-odata-endpoint/_static/image7.png)

单击**新建数据上下文...** 按钮。 保留数据上下文类型的默认名称，然后单击**添加**。

![](creating-an-odata-endpoint/_static/image8.png)

在添加控制器对话框来添加控制器，单击添加。

![](creating-an-odata-endpoint/_static/image9.png)

注意： 是否你收到一条错误消息指出&quot;时出错，获取类型...&quot;，请确保添加 Product 类后生成 Visual Studio 项目。 基架使用反射来查找类。

![](creating-an-odata-endpoint/_static/image10.png)

基架添加到项目的两个代码文件：

- Products.cs 定义实现 OData 终结点的 Web API 控制器。
- ProductServiceContext.cs 提供方法来查询基础数据库中，使用实体框架。

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>添加的 EDM 和路由

在解决方案资源管理器，展开应用\_启动文件夹并打开名为 WebApiConfig.cs 文件。 此类包含对 Web API 配置代码。 此代码替换为以下：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

此代码执行两项操作：

- 创建 OData 终结点的实体数据模型 (EDM)。
- 将添加为终结点的路由。

EDM 是抽象的数据模型。 EDM 用于创建元数据文档，并定义服务的 Uri。 **ODataConventionModelBuilder**创建 EDM 使用一组默认命名约定 EDM。 此方法要求最少的代码。 如果你想更好地控制 EDM，则可以使用**ODataModelBuilder**类，以通过添加属性、 键和导航属性显式创建 EDM。

**EntitySet**方法将添加一个实体集到 EDM:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

"产品"的字符串定义的实体集的名称。 控制器的名称必须与实体集的名称匹配。 在本教程中，实体集被命名为"产品"和控制器被命名为`ProductsController`。 如果在名为的实体集"ProductSet"，则将命名为控制器`ProductSetController`。 请注意，终结点可以具有多个实体集。 调用**EntitySet&lt;T&gt;** 为每个实体集，，然后定义相应的控制器。

**MapODataRoute**方法将添加为 OData 终结点的路由。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

第一个参数是路由的友好名称。 你的服务的客户端不会看到此名称。 第二个参数是终结点的 URI 前缀。 给定此代码，Products 实体集的 URI 为 http://<em>主机名</em>  /odata/产品。 应用程序可以具有多个 OData 终结点。 对于每个终结点，调用<strong>MapODataRoute</strong>提供唯一的路由名称和唯一的 URI 前缀。

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>（可选） 数据库中植入

在此步骤中，将使用 Entity Framework 以设置一些测试数据与数据库的种子。 此步骤是可选的但它可以立即测试 OData 终结点。

从**工具**菜单中，选择**库程序包管理器**，然后选择**程序包管理器控制台**。 在包管理器控制台窗口中，输入以下命令：

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

这将添加名为迁移和名为 Configuration.cs 代码文件的文件夹。

![](creating-an-odata-endpoint/_static/image12.png)

打开此文件，并将以下代码添加到`Configuration.Seed`方法。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

在包管理器控制台窗口中，输入以下命令：

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

这些命令将生成创建数据库，然后执行该代码的代码。

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>探索 OData 终结点

在本部分中，我们将使用[Fiddler Web 调试代理](http://www.fiddler2.com)将请求发送到终结点并检查响应消息。 这将帮助您了解 OData 终结点的功能。

在 Visual Studio 中，按 F5 启动调试。 默认情况下，Visual Studio 将打开你的浏览器`http://localhost:*port*`，其中*端口*是在项目设置中配置的端口号。

你可以在项目设置中的端口号。 在解决方案资源管理器，右键单击该项目并选择**属性**。 在属性窗口中，选择**Web**。 输入下的端口号**项目 Url**。

### <a name="service-document"></a>服务文档

*服务文档*包含 OData 终结点的实体集的列表。 若要获取服务文档，请对根服务的 URI 发送 GET 请求。

使用 Fiddler，输入中的以下 URI **Composer**选项卡： `http://localhost:port/odata/`，其中*端口*是端口号。

![](creating-an-odata-endpoint/_static/image13.png)

单击**Execute**按钮。 Fiddler 将 HTTP GET 请求发送到你的应用程序。 应看到 Web 会话列表中的响应。 如果一切正常，则状态代码将为 200。

![](creating-an-odata-endpoint/_static/image14.png)

双击要查看检查器选项卡中的响应消息的详细信息的 Web 会话列表中的响应。

![](creating-an-odata-endpoint/_static/image15.png)

原始 HTTP 响应消息应类似于下面所示：

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

默认情况下，Web API 返回 AtomPub 格式的服务文档。 若要请求 JSON，将 HTTP 请求中添加以下标头：

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

现在的 HTTP 响应包含 JSON 有效负载：

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>服务元数据文档

*服务元数据文档*介绍了使用一种称为概念架构定义语言 (CSDL) 的 XML 语言的服务数据模型。 元数据文档在服务中，显示的数据结构，并可用于生成客户端代码。

若要获取的元数据文档，请将发送 GET 请求到`http://localhost:port/odata/$metadata`。 下面是本教程中所示的终结点的元数据。

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>实体集

若要获取的产品实体集，将发送 GET 请求到`http://localhost:port/odata/Products`。

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>实体

若要获取的各个产品，发送 GET 请求到`http://localhost:port/odata/Products(1)`，其中"1"是产品 id。

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData 序列化格式

OData 支持多种序列化格式：

- Atom Pub (XML)
- JSON"light"（在 OData v3 中引入）
- JSON"详细"(OData v2)

默认情况下，Web API 使用 AtomPubJSON"light"格式。 

若要获取 AtomPub 格式，请设置为"application/atom + xml"Accept 标头。 下面是响应正文示例：

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

您所见的 Atom 格式的一个明显缺点： 它是 JSON 精简模式的更详细。 但是，如果必须理解 AtomPub 的客户端，客户端可能更倾向于该格式通过 JSON。

下面是实体的相同的 JSON 轻型版本：

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

OData 协议版本 3 中引入了 JSON 轻型格式。 为了向后兼容性，客户端可以请求的较旧的"详细"JSON 格式。 若要请求详细 JSON，请将 Accept 标头设置为`application/json;odata=verbose`。 下面是详细的版本：

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

此格式会告知在响应正文中，可以极大地增加开销通过整个会话的多个元数据。 此外，它会通过包装在名为"d"的属性的对象添加一定程度的间接性。

## <a name="next-steps"></a>后续步骤

- [添加实体关系](working-with-entity-relations.md)
- [添加 OData 操作](odata-actions.md)
- [从.NET 客户端调用 OData 服务](calling-an-odata-service-from-a-net-client.md)
