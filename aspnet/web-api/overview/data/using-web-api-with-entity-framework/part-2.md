---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 添加模型和控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: f127f239bcc665f71976bb34f6d3387f8e0b72a7
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37393127"
---
<a name="add-models-and-controllers"></a>添加模型和控制器
====================
通过[Mike Wasson](https://github.com/MikeWasson)

[下载已完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，您将添加模型，这些类定义的数据库实体。 然后您将添加对这些实体执行 CRUD 操作的 Web API 控制器。

## <a name="add-model-classes"></a>添加模型类

在本教程中，我们将通过使用"代码优先"方法到 Entity Framework (EF) 创建数据库。 使用 Code First，C# 类相对应的写入数据库表和 EF 创建数据库。 (有关详细信息，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)。)

首先我们域对象定义为 Poco （普通旧 CLR 对象）。 我们将创建以下 Poco:

- 作者
- 通讯簿

在解决方案资源管理器，右键单击模型文件夹。 选择**外**，然后选择**类**。 将此类命名为 `Author`。

![](part-2/_static/image1.png)

使用以下代码将替换所有 Author.cs 中的样板代码。

[!code-csharp[Main](part-2/samples/sample1.cs)]

添加名为的另一个类`Book`，用下面的代码。

[!code-csharp[Main](part-2/samples/sample2.cs)]

实体框架将使用这些模型创建数据库表。 对于每个模型，`Id`属性将成为的数据库表的主键列。

在书籍类中，`AuthorId`定义的外键`Author`表。 （为简单起见，我假定每本书有一个作者。）Book 类还包含对相关的导航属性`Author`。 可以使用导航属性访问相关`Author`在代码中。 我说有关第 4，部分中的导航属性的详细信息[处理实体关系](part-4.md)。

## <a name="add-web-api-controllers"></a>添加 Web API 控制器

在本部分中，我们将添加 Web API 控制器支持 CRUD 操作 （创建、 读取、 更新和删除）。 控制器将使用 Entity Framework 与数据库层进行通信。

首先，您可以删除文件 Controllers/ValuesController.cs。 此文件包含一个示例 Web API 控制器，但对于本教程不需要它。

![](part-2/_static/image2.png)

接下来，生成项目。 Web API 基架使用反射来查找模型类，因此它需要编译的程序集。

在解决方案资源管理器，右键单击 Controllers 文件夹。 选择**外**，然后选择**控制器**。

![](part-2/_static/image3.png)

在中**添加基架**对话框中，选择"Web API 2 控制器的操作，使用实体框架"。 单击 **添加**。

![](part-2/_static/image4.png)

在中**添加控制器**对话框中，执行以下操作：

1. 在中**模型类**下拉列表中，选择`Author`类。 （如果没有看到它列在下拉列表中，请确保您生成项目。）
2. 检查"使用异步控制器操作"。
3. 将作为控制器名称&quot;AuthorsController&quot;。
4. 单击加号 （+） 按钮旁边**数据上下文类**。

![](part-2/_static/image5.png)

在中**新建数据上下文**对话框中，保留默认名称，然后单击**添加**。

![](part-2/_static/image6.png)

单击**外**若要完成**添加控制器**对话框。 该对话框向项目中添加两个类：

- `AuthorsController` 定义 Web API 控制器。 在控制器实现 REST API 客户端用来执行 CRUD 操作列表上的作者。
- `BookServiceContext` 在运行时，其中包括填充对象将数据从数据库、 更改跟踪和数据保存到数据库管理实体对象。 它继承自`DbContext`。

![](part-2/_static/image7.png)

在此情况下，重新生成项目。 现在，通过相同的步骤来添加的 API 控制器，转`Book`实体。 这次请选择`Book`作为模型类，并选择现有`BookServiceContext`数据上下文类的类。 （不创建新的数据上下文。）单击**添加**将控制器添加。

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [上一页](part-1.md)
> [下一页](part-3.md)
