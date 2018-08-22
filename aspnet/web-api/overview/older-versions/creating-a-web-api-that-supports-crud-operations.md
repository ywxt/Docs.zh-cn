---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: 启用 ASP.NET Web API 1 中的 CRUD 操作 |Microsoft Docs
author: MikeWasson
description: 本教程演示如何使用 ASP.NET Web API 的 HTTP 服务中支持的 CRUD 操作。 在教程的 Visual Studio 2012 Web AP 中使用的软件版本...
ms.author: riande
ms.date: 01/28/2012
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: ba061b26b8527e447f25f6046057542a54f989a8
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823540"
---
<a name="enabling-crud-operations-in-aspnet-web-api-1"></a>启用 ASP.NET Web API 1 中的 CRUD 操作
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> 本教程演示如何使用 ASP.NET Web API 的 HTTP 服务中支持的 CRUD 操作。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Visual Studio 2012
> - Web API 1 （也适用于 Web API 2）


代表 CRUD&quot;创建、 读取、 更新和删除，&quot;这是四个基本数据库操作。 许多 HTTP 服务还能模拟通过 REST 或类似于 REST 的 Api 的 CRUD 操作。

在本教程中，将生成非常简单的 web API 可以管理的产品列表。 每个产品将包含名称、 价格和类别 (如&quot;toys&quot;或&quot;硬件&quot;)，以及产品 id。

产品 API 将公开以下方法。

| 操作 | HTTP 方法 | 相对 URI |
| --- | --- | --- |
| 获取所有产品的列表 | GET | / api/产品 |
| 获取按 ID 的产品 | GET | /api/产品/*id* |
| 按类别获取产品 | GET | /api/products?category=*category* |
| 创建一个新的产品 | 发布 | / api/产品 |
| 将产品更新 | PUT | /api/产品/*id* |
| 删除产品 | DELETE | /api/产品/*id* |

注意到一些 Uri 路径中包括的产品 ID。 例如，若要获取其 ID 为 28 的产品，客户端发送 GET 请求`http://hostname/api/products/28`。

### <a name="resources"></a>资源

API 的产品定义为两种资源类型的 Uri:

| 资源 | URI |
| --- | --- |
| 所有产品的列表。 | / api/产品 |
| 单独的产品。 | /api/产品/*id* |

### <a name="methods"></a>方法

四个主要 HTTP 方法 （GET、 PUT、 POST 和 DELETE） 可以按如下所示映射到 CRUD 操作：

- GET 操作将检索指定 URI 处的资源的表示形式。 获取应在服务器上具有任何副作用。
- PUT 更新资源时指定的 URI。 PUT 还可用来创建新的资源在指定的 URI，如果服务器允许客户端指定的新 Uri。 对于本教程，该 API 将不支持通过 PUT 创建。
- POST 创建新的资源。 服务器分配新对象的 URI，并返回此 URI 的响应消息的一部分。
- 删除： 删除指定 URI 处的资源。

注意： 该 PUT 方法将替换整个产品实体。 也就是说，客户端应发送更新的产品的完整表示形式。 如果你想要支持部分更新，修补程序方法是首选。 本教程不实现修补程序。

## <a name="create-a-new-web-api-project"></a>创建新的 Web API 项目

首先运行 Visual Studio，然后选择**新的项目**从**启动**页。 或者，从**文件**菜单中，选择**新建**，然后**项目**。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET MVC 4 Web 应用程序**。 将项目命名&quot;ProductStore&quot;然后单击**确定**。

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

在中**新的 ASP.NET MVC 4 项目**对话框中，选择**Web API**然后单击**确定**。

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>添加模型

模型是表示应用程序中的数据的对象。 在 ASP.NET Web API 中，可以为模型中，使用强类型的 CLR 对象和它们会自动串行化为 XML 或 JSON 为客户端。

对于 ProductStore API 中，我们的数据中包含产品，因此我们将创建一个名为的新类`Product`。

如果解决方案资源管理器尚不可见，请单击**视图**菜单，然后选择**解决方案资源管理器**。 在解决方案资源管理器中右键单击**模型**文件夹。 从上下文排队中，选择**外**，然后选择**类**。 将类命名&quot;产品&quot;。

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

添加以下属性来`Product`类。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>添加存储库

我们需要存储的产品的集合。 它是单独的集合从我们的服务实现一个好办法。 这样一来，我们可以更改的后备存储，无需重写服务类。 这种设计称为*存储库*模式。 首先，定义存储库中的泛型接口。

在解决方案资源管理器中右键单击**模型**文件夹。 选择**外**，然后选择**新项**。

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

在中**模板**窗格中，选择**已安装的模板**展开 C# 节点。 在 C# 中，选择**代码**。 在代码模板列表中，选择**接口**。 命名接口&quot;IProductRepository&quot;。

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

添加以下实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

现在将另一个类添加到模型文件夹，名为&quot;化 ProductRepository。&quot;此类将实现 `IProductRespository` 接口。 添加以下实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

存储库在本地内存中保留列表。 这是正常的教程，但在实际的应用程序，您应将数据从外部看，这两个数据库存储或云存储中。 存储库模式将使其更轻松地更改实现更高版本。

## <a name="adding-a-web-api-controller"></a>添加 Web API 控制器

如果您曾经使用 ASP.NET MVC，然后您已熟悉控制器。 在 ASP.NET Web API 中，*控制器*是处理来自客户端的 HTTP 请求的类。 创建项目时，新项目向导将创建两个控制器。 若要查看它们，请展开解决方案资源管理器中的 Controllers 文件夹。

- HomeController 是传统的 ASP.NET MVC 控制器。 它负责处理 HTML 页面的站点，并与我们的 web API 不直接相关。
- ValuesController 是示例 WebAPI 控制器。

继续操作并右键单击解决方案资源管理器中的文件并选择删除 ValuesController，**删除。** 现在，如下所示添加新控制器：

在中**解决方案资源管理器**，右键单击 Controllers 文件夹。 选择**外**，然后选择**控制器**。

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

在中**添加控制器**向导中，将控制器命名&quot;ProductsController&quot;。 在中**模板**下拉列表中，选择**空 API 控制器**。 然后单击 **“添加”**。

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> 不需要将你的控制器放入名为控制器的文件夹。 文件夹名称并不重要;它是只是组织的源文件的简便方法。


**添加控制器**向导将创建名为 ProductsController.cs 控制器文件夹中的文件。 如果没有打开此文件，则双击文件将其打开。 添加以下**使用**语句：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

添加保存的字段**IProductRepository**实例。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> 调用`new ProductRepository()`控制器中不是最佳设计，因为它绑定到的特定实现控制器`IProductRepository`。 更好的方法，请参阅[使用 Web API 依赖关系解析程序](../advanced/dependency-injection.md)。


## <a name="getting-a-resource"></a>获取资源

ProductStore API 会公开多个&quot;读取&quot;作为 HTTP GET 方法的操作。 每个操作将对应于中的方法`ProductsController`类。

| 操作 | HTTP 方法 | 相对 URI |
| --- | --- | --- |
| 获取所有产品的列表 | GET | / api/产品 |
| 获取按 ID 的产品 | GET | /api/产品/*id* |
| 按类别获取产品 | GET | /api/products?category=*category* |

若要获取的所有产品的列表，请将以下方法添加到`ProductsController`类：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

方法名称开头&quot;获取&quot;，因此，它映射到 GET 请求的约定。 此外，由于该方法不具有任何参数，它映射到 URI 不包含*&quot;id&quot;* 路径中的段。

若要获取产品的 ID，将以下方法添加到`ProductsController`类：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

此方法名称还以开头&quot;获取&quot;，但方法具有一个名为参数*id*。此参数映射到&quot;id&quot; URI 路径段。 ASP.NET Web API 框架会自动将 ID 转换为正确的数据类型 (**int**) 的参数。

为 getproduct 方法将引发类型的异常**HttpResponseException**如果*id*无效。 此异常将由框架转换为 404 （未找到） 错误。

最后，添加一个方法来按类别查找产品：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

如果在请求 URI 查询字符串，Web API 会尝试匹配控制器方法的参数的查询参数。 因此，在窗体的 URI"api/产品？ 类别 =*类别*"将映射到此方法。

## <a name="creating-a-resource"></a>创建资源

接下来，我们将添加到方法`ProductsController`类，以创建一个新的产品。 下面是该方法的简单实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

请注意有关此方法的两项操作：

- 方法名称开头&quot;文章...&quot;. 若要创建一个新的产品，客户端发送的 HTTP POST 请求。
- 该方法采用产品类型的参数。 在 Web API 中，复杂类型的参数是从反序列化请求正文。 因此，我们期望客户端以 XML 或 JSON 格式发送产品对象的序列化表示形式。

此实现将起作用，但并不十分完整。 理想情况下，我们想要包括以下各项的 HTTP 响应：

- **响应代码：** 默认情况下，Web API 框架将响应状态代码设置为 200 （正常）。 但是，根据 HTTP/1.1 协议中，在创建的资源，导致 POST 请求时服务器应答复状态 201 （已创建）。
- **位置：** 时服务器创建了资源，它应在响应的 Location 标头中包含新资源的 URI。

ASP.NET Web API，使易于操作的 HTTP 响应消息。 以下是改进了的实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

请注意，方法返回类型是现在**HttpResponseMessage**。 通过返回**HttpResponseMessage**而不是一种产品，我们可以控制 HTTP 响应消息，包括状态代码和 Location 标头的详细信息。

**CreateResponse**方法创建**HttpResponseMessage**并自动将产品对象的序列化表示形式写入到正文 fo 响应消息。

> [!NOTE]
> 此示例不会验证`Product`。 有关模型验证的信息，请参阅[ASP.NET Web API 中的模型验证](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。


## <a name="updating-a-resource"></a>更新资源

使用 PUT 更新产品非常简单：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

方法名称开头&quot;放...&quot;，因此，Web API 的 PUT 请求匹配它。 该方法采用两个参数，产品 ID 和已更新的产品。 *Id*参数来自 URI 路径，并*产品*从请求正文反序列化参数。 默认情况下，ASP.NET Web API 框架会采用来自路由的简单的参数类型和请求正文中的复杂类型。

## <a name="deleting-a-resource"></a>删除资源

若要删除 resourse，定义的"删除..."方法。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

如果 DELETE 请求成功，它可以使用描述的状态; 实体正文中返回状态 200 （正常）状态 202 （已接受） 如果删除仍然挂起;或状态 204 （无内容） 没有实体正文。 在这种情况下，`DeleteProduct`方法具有`void`返回类型，因此 ASP.NET Web API 会自动将其转变成状态代码 204 （无内容）。
