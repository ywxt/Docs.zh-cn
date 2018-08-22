---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: 安全指南为 ASP.NET Web API 2 OData |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 02/06/2013
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 2a5b776a81cb3e3cf809dd3c4229448988086a32
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824228"
---
<a name="security-guidance-for-aspnet-web-api-2-odata"></a>安全指南为 ASP.NET Web API 2 OData
====================
通过[Mike Wasson](https://github.com/MikeWasson)

本主题介绍了一些公开通过 OData 数据集时应考虑的安全问题。

## <a name="edm-security"></a>EDM 安全

查询语义均基于实体数据模型 (EDM) 中，不是基础的模型类型。 可以从 EDM 排除某属性，它将看不到查询。 例如，假设您的模型包含具有薪金属性的员工类型。 你可能想要从 EDM 来隐藏客户端从排除此属性。

有两种方式可以排除从 EDM 属性。 可以设置 **[IgnoreDataMember]** 模型类中的属性上的属性：

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

还可以删除该属性从 EDM 以编程方式：

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>查询安全性

恶意或简单客户端可以采用很长时间执行的查询。 在最坏情况下这可能会中断服务的访问权限。

**[Queryable]** 属性是操作筛选器，用于分析、 验证，并将查询应用。 筛选器将 LINQ 表达式转换为查询选项。 当返回 OData 控制器**IQueryable**类型， **IQueryable** LINQ 提供程序将查询转换为 LINQ 表达式。 因此，性能取决于使用时，LINQ 提供程序和数据集或数据库架构的特定的特征。

有关在 ASP.NET Web API 中使用 OData 查询选项的详细信息，请参阅[支持 OData 查询选项](supporting-odata-query-options.md)。

如果您知道所有客户端信任 （例如，在企业环境中），或者如果你的数据集很小，查询性能可能不会出现问题。 否则，应考虑以下建议。

- 测试你的服务的各种查询和分析数据库。
- 启用服务器驱动的分页，以避免在一个查询中返回大型数据集。 有关详细信息，请参阅[Server-Driven 分页](supporting-odata-query-options.md#server-paging)。 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- 您是否需要 $filter 和 $orderby？ 某些应用程序可能会允许客户端分页、 使用 $top 和 $skip，但禁用其他查询选项。 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- 考虑将 $orderby 限制为聚集索引中的属性。 没有聚集索引的大型数据排序速度较慢。 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 最大节点计数： **MaxNodeCount**上的属性 **[Queryable]** 设置 $filter 语法树中允许的最大数字节点。 默认值为 100，但你可能想要设置较低的值，因为大量的节点可能会很慢进行编译。 这是如果您使用的 LINQ to Objects （即，在内存中，而不使用中间 LINQ 提供程序的集合上的 LINQ 查询） 尤其如此。 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- 请考虑禁用 any （） 和 all （） 函数中，因为这些可能会很慢。 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 如果任何字符串属性包含的大型字符串和 #8212for 示例、 产品说明或博客文章和 #8212consider 禁用字符串函数。 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- 请考虑不允许对导航属性筛选。 导航属性进行筛选，则可能导致在联接，它可能会很慢，具体取决于您的数据库架构。 下面的代码演示可防止对导航属性筛选的查询验证程序。 有关查询验证程序的详细信息，请参阅[查询验证](supporting-odata-query-options.md#query-validation)。 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- 考虑将 $filter 查询限制通过编写针对您的数据库自定义验证程序。 例如，考虑这两个查询： 

  - 与执行组件的最后一个名称以 A 开头的所有电影。
  - 1994 年发布的所有电影。

    除非电影已编入索引的执行组件，第一个查询可能需要扫描整个列表的电影数据库引擎。 第二个查询可能是可接受的而假定电影进行索引按版本年份。

    下面的代码演示允许上的"ReleaseYear"和"Title"属性但没有其他属性进行筛选的验证程序。

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 一般情况下，请考虑需要哪些 $filter 函数。 如果你的客户端不需要的完整表现力 $filter，可以限制允许的函数。
