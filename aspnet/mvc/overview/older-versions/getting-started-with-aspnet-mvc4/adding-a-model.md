---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: 注意： 本教程中的更新的版本提供了使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示...
ms.author: aspnetcontent
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e68b6d41c7880fb849bbefbedd4c4e25c6f47b0e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837754"
---
<a name="adding-a-model"></a>添加模型
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

> > [!NOTE]
> > 本教程中的更新的版本是可用[此处](../../getting-started/introduction/getting-started.md)，它使用 ASP.NET MVC 5 和 Visual Studio 2013。 它是更安全、 更易于遵循，并演示更多的功能。


在本部分中将添加用于管理数据库中的电影的一些类。 这些类将是&quot;模型&quot;ASP.NET MVC 应用程序的一部分。

将使用名为.NET Framework 数据访问技术[Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)来定义和使用这些模型的类。 实体框架 （通常称为 EF） 支持开发模式称为*Code First*。 代码首先允许你通过编写简单的类来创建模型对象。 (这些是也称为 POCO 类，从&quot;普通旧 CLR 对象。&quot;)然后，您可以实现很整洁且快速的开发工作流的类，从动态创建的数据库。

## <a name="adding-model-classes"></a>添加模型类

在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。

![](adding-a-model/_static/image1.png)

输入*类*名称&quot;电影&quot;。

添加到以下五个属性`Movie`类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用`Movie`类来表示数据库中的电影。 每个实例`Movie`对象将对应于数据库表中，并的每个属性内的行`Movie`类将映射到表中的列。

在同一文件中，添加以下`MovieDBContext`类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext`类表示处理提取、 存储和更新的实体框架电影数据库上下文`Movie`类在数据库中的实例。 `MovieDBContext`派生自`DbContext`实体框架提供的基类。

若要引用将`DbContext`并`DbSet`，你需要添加以下`using`在文件顶部的语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

完整*Movie.cs*文件如下所示。 (多个 using 语句不需要已被删除。)

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>创建的连接字符串和使用 SQL Server LocalDB

`MovieDBContext`创建的类处理连接到数据库以及映射任务`Movie`数据库记录的对象。 您可能会问的一个问题，是如何指定将连接到的数据库。 您将通过添加中的连接信息来实现*Web.config*应用程序文件。

打开应用程序根目录*Web.config*文件。 (未*Web.config*中的文件*视图*文件夹。)打开*Web.config*以红色标出的文件。

![](adding-a-model/_static/image2.png)

添加到以下连接字符串`<connectionStrings>`中的元素*Web.config*文件。

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

下面的示例显示了一部分*Web.config*文件添加的新连接字符串：

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

这种少量的代码和 XML 是为了表示，并将影片数据存储在数据库中编写所需的一切。

接下来，你将生成一个新`MoviesController`类，该类可以用于显示电影数据并允许用户创建新的影片列表。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)
