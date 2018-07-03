---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在使用 ASP.NET Web API OData v4 中打开类型 |Microsoft Docs
author: microsoft
description: OData v4 中开放类型是包含动态属性，除了在类型定义中声明的任何属性的 stuctured 类型。 打开...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/15/2014
ms.topic: article
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 0eae376830e70199a9692df5a154168646f99716
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37375520"
---
<a name="open-types-in-odata-v4-with-aspnet-web-api"></a>在使用 ASP.NET Web API OData v4 中打开类型
====================
by [Microsoft](https://github.com/microsoft)

> 在 OData v4*打开类型*是 stuctured 类型，其中包含动态属性，除了在类型定义中声明的任何属性。 开放类型，可以添加到数据模型的灵活性。 本教程演示如何在 ASP.NET Web API OData 中使用开放类型。
> 
> 本教程假定您已经知道如何在 ASP.NET Web API 中创建 OData 终结点。 如果不是，应首先阅读[创建 OData v4 终结点](create-an-odata-v4-endpoint.md)第一个。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Web API OData 5.3
> - OData v4


首先，OData 的一些术语：

- 实体类型： 具有一个键的结构化的类型。
- 复杂类型： 结构化的类型没有键。
- 打开类型： 具有动态属性的类型。 实体类型和复杂类型可以打开。

动态属性的值可以是基元类型、 复杂类型或枚举类型;或任何这些类型的集合。 有关开放类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。

## <a name="install-the-web-odata-libraries"></a>安装 Web OData 库

使用 NuGet 包管理器安装最新的 Web API OData 库。 从包管理器控制台窗口中：

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>定义 CLR 类型

首先，定义为 CLR 类型的 EDM 模型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

创建实体数据模型 (EDM) 时，

- `Category` 是枚举类型。
- `Address` 是一种复杂类型。 （它没有密钥，因此它不是实体类型。）
- `Customer` 是实体类型。 （它具有一个密钥）。
- `Press` 是打开的复杂类型。
- `Book` 为开放实体类型。

若要创建开放类型，CLR 类型必须具有一个类型的属性`IDictionary<string, object>`，用于保存动态属性。

## <a name="build-the-edm-model"></a>生成的 EDM 模型

如果您使用**ODataConventionModelBuilder**若要创建 EDM`Press`和`Book`自动添加为开放类型，根据是否存在的`IDictionary<string, object>`属性。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

您还可以构建 EDM 显式使用**ODataModelBuilder**。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>添加一个 OData 控制器

接下来，添加一个 OData 控制器。 对于本教程中，我们将使用简化的控制器仅支持获取，和 POST 请求，以及使用的内存中列表来存储实体。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

请注意，第一个`Book`实例都有任何动态属性。 第二个`Book`实例都有以下动态属性：

- "已发布": 基元类型
- "作者": 基元类型的集合
- "OtherCategories": 枚举类型的集合。

此外，`Press`属性的`Book`实例都有以下动态属性：

- "博客": 基元类型
- "Address": 复杂类型

## <a name="query-the-metadata"></a>查询的元数据

若要获取 OData 元数据文档，请将发送 GET 请求到`~/$metadata`。 响应正文应类似于以下所示：

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

从元数据文档中，您可以看到：

- 有关`Book`并`Press`类型的值`OpenType`属性为 true。 `Customer`和`Address`类型不具有此特性。
- `Book`实体类型具有三个声明的属性： ISBN、 标题，然后按。 OData 元数据不包括`Book.Properties`从 CLR 类的属性。
- 同样，`Press`复杂类型具有只有两个声明的属性： 名称和类别。 元数据不包括`Press.DynamicProperties`从 CLR 类的属性。

## <a name="query-an-entity"></a>查询的实体

若要获取对书籍 ISBN 等于"978-0-7356-7942-9"，将发送 GET 请求到`~/Books('978-0-7356-7942-9')`。 响应正文应类似于以下。 （缩进，以使其更具可读性。）

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

请注意，动态属性以内联形式包含声明的属性。

## <a name="post-an-entity"></a>POST 实体

若要添加的书实体，发送 POST 请求到`~/Books`。 客户端可以在请求负载中设置动态属性。

下面是示例请求。 请注意"Price"和"已发布"属性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

如果在控制器方法中设置断点，可以看到 Web API 添加到这些属性`Properties`字典。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>其他资源

[OData 开放类型示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
