---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web 窗体中使用 Web API |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 04/03/2012
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: c9da38d290a812e94ed9473386ba6b897447dac5
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37840883"
---
<a name="using-web-api-with-aspnet-web-forms"></a>ASP.NET Web 窗体中使用 Web API
====================
通过[Mike Wasson](https://github.com/MikeWasson)

尽管 ASP.NET Web API 与 ASP.NET MVC 一起打包，很容易地将 Web API 添加到传统的 ASP.NET Web 窗体应用程序。 本教程将指导你完成的步骤。

## <a name="overview"></a>概述

若要在 Web 窗体应用程序中使用 Web API，有两个主要步骤：

- 添加 Web API 控制器派生自**ApiController**类。
- 添加到路由表**应用程序\_启动**方法。

## <a name="create-a-web-forms-project"></a>创建 Web 窗体项目

启动 Visual Studio 并选择**新的项目**从**启动**页。 或者，从**文件**菜单中，选择**新建**，然后**项目**。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Web**。 在项目模板列表中选择**ASP.NET Web 窗体应用程序**。 输入项目的名称，然后单击**确定**。

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>创建模型和控制器

本教程使用相同的模型和控制器类[Getting Started](tutorial-your-first-web-api.md)教程。

首先，添加一个模型类。 在中**解决方案资源管理器**，右键单击该项目并选择**添加类**。 命名类产品，并添加以下实现：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

接下来，将 Web API 控制器添加到项目中。，一个*控制器*是针对 Web API 处理 HTTP 请求的对象。

在中**解决方案资源管理器**，右键单击该项目。 选择**添加新项**。

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

下**已安装的模板**，展开**Visual C#** ，然后选择**Web**。 然后，从模板列表中，选择**Web API 控制器类**。 将控制器命名为"ProductsController"，然后单击**添加**。

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

**添加新项**向导将创建一个名为 ProductsController.cs 文件。 删除向导包括的方法并添加以下方法：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

有关此控制器中的代码的详细信息，请参阅[Getting Started](tutorial-your-first-web-api.md)教程。

## <a name="add-routing-information"></a>添加路由信息

接下来，我们将因此添加 URI 路由该形式的 Uri &quot;/api/产品/&quot;路由到控制器。

在中**解决方案资源管理器**，双击 Global.asax 以打开代码隐藏文件 Global.asax.cs。 添加以下**使用**语句。

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

然后将以下代码添加到**应用程序\_启动**方法：

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

有关路由表的详细信息，请参阅[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

## <a name="add-client-side-ajax"></a>添加客户端 AJAX

这是您需要创建的 web 客户端可以访问的 API。 现在让我们添加使用 jQuery 来调用 API 的 HTML 页。

请确保主页面 (例如， *Site.Master*) 包括`ContentPlaceHolder`与`ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

打开 Default.aspx 文件。 替换为在主内容部分中，样板文本所示：

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

接下来，添加对 jQuery 源代码文件中的引用`HeaderContent`部分：

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

注意： 您可以轻松地添加脚本引用通过拖放文件从**解决方案资源管理器**的代码编辑器窗口中。

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

下面的 jQuery 脚本标记，添加以下脚本块：

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

当文档加载后时，此脚本进行到 AJAX 请求&quot;api/产品&quot;。 该请求以 JSON 格式返回的产品的列表。 该脚本将产品信息添加到 HTML 表。

当您运行该应用程序时，它应如下所示：

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
