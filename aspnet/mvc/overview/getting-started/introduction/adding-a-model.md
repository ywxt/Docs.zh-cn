---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/28/2015
ms.topic: article
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
ms.technology: dotnet-mvc
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 98b6693b07e4da318a649494649d9da83fe8a7d3
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365131"
---
<a name="adding-a-model"></a>添加模型
====================
通过[Rick Anderson](https://github.com/Rick-Anderson)

[!INCLUDE [Tutorial Note](sample/code-location.md)]

在本部分中将添加用于管理数据库中的电影的一些类。 这些类将是&quot;模型&quot;ASP.NET MVC 应用程序的一部分。

将使用名为.NET Framework 数据访问技术[Entity Framework](https://docs.microsoft.com/ef/)来定义和使用这些模型的类。 实体框架 （通常称为 EF） 支持开发模式称为*Code First*。 代码首先允许你通过编写简单的类来创建模型对象。 (这些是也称为 POCO 类，从&quot;普通旧 CLR 对象。&quot;)然后，您可以实现很整洁且快速的开发工作流的类，从动态创建的数据库。 如果您需要首先创建数据库，您仍可遵循此教程，了解有关 MVC 和 EF 应用程序开发。 然后可以按照 Tom Fizmakens [ASP.NET 基架](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)教程，介绍了数据库第一种方法。

## <a name="adding-model-classes"></a>添加模型类

在中**解决方案资源管理器**，右键单击*模型*文件夹，选择**添加**，然后选择**类**。

![](adding-a-model/_static/image1.png)

输入*类*名称&quot;电影&quot;。

添加到以下五个属性`Movie`类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用`Movie`类来表示数据库中的电影。 每个实例`Movie`对象将对应于数据库表中，并的每个属性内的行`Movie`类将映射到表中的列。

注意： 若要使用 system.data.entity 的引用和相关的类，您需要安装[实体框架 NuGet 包](https://www.nuget.org/packages/EntityFramework/)。 请访问有关进一步说明链接。

在同一文件中，添加以下`MovieDBContext`类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext`类表示处理提取、 存储和更新的实体框架电影数据库上下文`Movie`类在数据库中的实例。 `MovieDBContext`派生自`DbContext`实体框架提供的基类。

若要引用将`DbContext`并`DbSet`，你需要添加以下`using`在文件顶部的语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

您可以执行此操作通过手动添加 using 语句，也可以悬停在红色的波浪线，再单击`Show potential fixes`单击 `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

注意： 多个未使用`using`语句已被删除。 Visual Studio 将显示为灰色的未使用的依赖项。 可以通过将鼠标悬停的灰色的依赖项上删除未使用的依赖项，再单击`Show potential fixes`单击**删除未使用的 Using。**

![](adding-a-model/_static/image3.png)

最后，我们已添加模型 (在 MVC 中的 M)。 下一节中将使用数据库连接字符串。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](creating-a-connection-string.md)
