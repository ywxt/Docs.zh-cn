---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 处理实体关系 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: 5d05a2e5d4380a15078317545325bd20fde3f83c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831700"
---
<a name="handling-entity-relations"></a>处理实体关系
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

本部分介绍 EF 加载相关的实体的方式以及如何处理循环的导航属性在模型类中的一些详细信息。 （本部分提供了背景知识，并不需要完成本教程。 如果您愿意，请跳到[第 5 部分。](part-5.md)。)

## <a name="eager-loading-versus-lazy-loading"></a>预先加载与延迟加载

当使用 EF 关系数据库时，务必了解 EF 加载相关的数据的方式。

也很有用，若要查看 EF 生成的 SQL 查询。 若要跟踪 SQL，请添加以下代码行`BookServiceContext`构造函数：

[!code-csharp[Main](part-4/samples/sample1.cs)]

如果向 /api/books 发送 GET 请求，它将返回 JSON，如下所示：

[!code-console[Main](part-4/samples/sample2.cmd)]

您可以看到 Author 属性是 null，即使该指南包含有效的作者 Id。 这是因为 EF 不加载相关的作者实体。 SQL 查询的跟踪日志对此进行确认：

[!code-console[Main](part-4/samples/sample3.sql)]

SELECT 语句从书表中获取并不引用作者表。

有关参考，下面是在方法`BooksController`返回书籍列表的类。

[!code-csharp[Main](part-4/samples/sample4.cs)]

我们来看作为 JSON 数据的一部分，我们就可以返回作者。 有三种方法来加载相关的实体框架中的数据： 预先加载、 延迟加载和显式加载。 有权衡与每种技术，因此务必要了解它们如何工作。

### <a name="eager-loading"></a>预先加载

与*预先加载*，EF 加载相关的实体作为初始数据库查询的一部分。 若要执行预先加载，请使用**System.Data.Entity.Include**扩展方法。

[!code-csharp[Main](part-4/samples/sample5.cs)]

这将告知 EF 在查询中包括创作数据。 如果你进行此更改，并运行应用，现在的 JSON 数据如下所示：

[!code-console[Main](part-4/samples/sample6.cmd)]

跟踪日志显示了 EF 的书籍和作者表执行联接。

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>延迟加载

使用延迟加载，EF 会自动加载相关的实体时取消引用该实体的导航属性。 若要启用延迟加载，使导航属性虚拟方法。 例如，在 Book 类中：

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

现在请考虑以下代码：

[!code-csharp[Main](part-4/samples/sample9.cs)]

启用延迟加载后，访问`Author`属性上的`books[0]`促使 EF 查询作者的数据库。

延迟加载需要多个数据库访问，原因是 EF 将发送每次它检索相关的实体的查询。 通常，您希望序列化的对象禁用延迟加载。 序列化程序具有读取所有模型，这将触发加载相关的实体的属性。 例如，下面是出现 EF 将启用延迟加载序列化的书籍列表的 SQL 查询。 您可以看到 EF 的三个作者可以三个单独的查询。

[!code-console[Main](part-4/samples/sample10.sql)]

仍有可能的希望使用延迟加载。 预先加载可能会导致 EF 生成非常复杂的联接。 或您可能需要相关的实体的少量数据，并延迟加载会更高效。

若要避免序列化问题的一种方法是序列化而不是实体对象的数据传输对象 (Dto)。 在本文的后面，我将介绍这种方法。

### <a name="explicit-loading"></a>显式加载

显式加载是类似于延迟加载，只是显式代码; 中有相关的数据它不会自动发生时您访问导航属性。 显式加载可提供更好地控制何时加载相关的数据，但需要额外的代码。 有关显式加载的详细信息，请参阅[加载相关实体](https://msdn.microsoft.com/data/jj574232#explicit)。

## <a name="navigation-properties-and-circular-references"></a>导航属性和循环引用

当我定义的书籍和作者模型时，我定义一个导航属性上`Book`类书籍作者关系，但我没有在另一个方向定义导航属性。

如果您将添加到相应的导航属性，会发生什么情况`Author`类？

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

遗憾的是，这会产生问题时序列化模型。 如果在加载相关的数据，它将创建循环对象图。

![](part-4/_static/image1.png)

当 JSON 或 XML 格式化程序尝试序列化关系图时，它将引发异常。 两个格式化程序会引发其他异常消息。 下面是 JSON 格式化程序的示例：

[!code-console[Main](part-4/samples/sample12.cmd)]

下面是 XML 格式化程序：

[!code-xml[Main](part-4/samples/sample13.xml)]

一种解决方案是使用 Dto，我在下一节中介绍。 或者，可以配置 JSON 和 XML 格式化程序用于处理关系图周期。 有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。

对于本教程中，不需要`Author.Book`导航属性，因此可以省略。

> [!div class="step-by-step"]
> [上一页](part-3.md)
> [下一页](part-5.md)
