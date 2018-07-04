---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 第 2 部分： 创建域模型 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2012
ms.topic: article
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9f379c92f7795c9fe10f7860b72188a8cfc1b6d2
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37379720"
---
<a name="part-2-creating-the-domain-models"></a>第 2 部分： 创建域模型
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>添加模型

有三种方式来实体框架的方法：

- 数据库优先： 对于数据库，启动和实体框架生成的代码。
- 实体数据模型： 开始从可视模型和实体框架生成的数据库和代码。
- 代码优先： 开头的代码中，并且实体框架生成数据库。

我们将使用代码优先方法中，因此我们首先定义我们的域对象为 Poco （普通旧 CLR 对象）。 使用代码优先方法时，域对象不需要任何额外的代码，以支持数据库层，例如事务或持久性。 (具体而言，它们不需要从继承[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)类。)仍然可以使用数据注释来控制如何 Entity Framework 创建数据库架构。

因为 Poco 不传送任何额外的属性描述[的数据库状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx)，他们可以轻松地序列化为 JSON 或 XML。 但是，这不表示您应始终公开实体框架模型直接向客户端，正如我们将看到在本教程后面。

我们将创建以下 Poco:

- 产品
- 顺序
- OrderDetail

若要创建的每个类，请右键单击解决方案资源管理器中的 Models 文件夹。 从上下文菜单中，选择**外**，然后选择**类。**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

添加`Product`类具有以下实现：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

按照约定，Entity Framework 使用`Id`为主键的属性并将其映射到数据库表中的标识列。 当您创建一个新`Product`实例中，不会设置一个值`Id`，因为该数据库生成值。

**ScaffoldColumn**特性告诉 ASP.NET MVC 跳过`Id`属性生成编辑器窗体时。 **所需**特性用于验证模型。 它指定`Name`属性必须为非空字符串。

添加`Order`类：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

添加`OrderDetail`类：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>外键关系

订单包含多个订单详细信息，以及每个订单详细信息是指一个产品。 来表示这些关系`OrderDetail`类定义了名为的属性`OrderId`和`ProductId`。 实体框架将推断这些属性表示外键，并将向数据库添加 foreign key 约束。

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

`Order`和`OrderDetail`类还包括"导航"属性，其中包含对相关对象的引用。 给定订单，您可以导航到的产品的顺序由以下导航属性。

现在来编译项目。 实体框架使用反射来发现模型的属性，因此它需要一个已编译的程序集，以创建数据库架构。

## <a name="configure-the-media-type-formatters"></a>配置媒体类型格式化程序

一个[媒体类型格式化程序](../../formats-and-model-binding/media-formatters.md)是当 Web API 将 HTTP 响应正文将你的数据序列化的对象。 内置格式化程序支持 JSON 和 XML 输出。 默认情况下，这两个这些格式化程序序列化的所有对象的值。

如果对象图包含循环引用，则按值序列化会产生问题。 这是完全与用例`Order`和`OrderDetail`类，因为每个保存到其他的引用。 格式化程序将按照值，通过编写每个对象引用，并在兜圈子转。 因此，我们需要更改默认行为。

在解决方案资源管理器，展开应用\_启动文件夹并打开名为 WebApiConfig.cs 文件。 将下面的代码添加到 `WebApiConfig` 类中:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

此代码设置 JSON 格式化程序来保留对象引用，并从管道中完全删除 XML 格式化程序。 （你可以配置要保留对象引用的 XML 格式化程序，但它是需要执行一些操作，和我们只需为此应用程序的 JSON。 有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。)

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-1.md)
> [下一页](using-web-api-with-entity-framework-part-3.md)
