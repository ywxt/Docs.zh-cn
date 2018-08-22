---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 增强数据验证 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: riande
ms.date: 12/29/2014
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: dbff33a1c4f47474adda82e796d9c292392142f2
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824448"
---
<a name="ef-database-first-with-aspnet-mvc-enhancing-data-validation"></a>第一种使用 ASP.NET MVC 的 EF 数据库： 增强数据验证
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。 生成的代码对应于数据库表中的列。
> 
> 本系列的此部分主要介绍在将数据批注添加到数据模型以指定验证要求和显示格式。 它改进了基于注释部分中的用户的反馈。


## <a name="add-data-annotations"></a>添加数据批注

正如您看到在之前主题中，一些数据的验证规则会自动应用到用户输入。 例如，可以仅级属性提供一个数字。 若要指定多个数据验证规则，可以向 model 类中添加数据批注。 这些批注将应用于整个 web 应用程序为指定的属性。 您还可以应用更改属性的显示方式; 的格式设置属性例如，更改使用的文本标签的值。

在本教程中，您将添加数据注释来限制为 FirstName、 LastName 和 MiddleName 属性提供的值的长度。 在数据库中，这些值是 50 个字符;但是，在 web 应用程序中的字符数限制为当前不强制执行。 如果用户提供超过 50 个字符，这些值之一，尝试将值保存到数据库时将崩溃页。 你还将为介于 0 和 4 之间的值限制级。

打开**Student.cs**中的文件**模型**文件夹。 向类添加以下突出显示的代码。

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

在 Enrollment.cs，添加以下突出显示的代码。

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

生成解决方案。

浏览到用于编辑或创建一个学生页。 如果尝试输入超过 50 个字符，显示一条错误消息。

![显示错误消息](enhancing-data-validation/_static/image1.png)

浏览到页以进行编辑注册，并尝试提供 4 级。

![级范围错误](enhancing-data-validation/_static/image2.png)

可以将应用于属性和类的数据验证注释的完整列表，请参阅[System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。

## <a name="add-metadata-classes"></a>添加元数据类

当不希望更改; 的数据库时，直接向 model 类添加验证特性有效但是，如果更改了数据库，并且需要重新生成模型类，您将丢失所有已应用于模型类的属性。 这种方法可以是非常低效，而且容易丢失重要的验证规则。

若要避免此问题，可以添加一个包含属性的元数据类。 当将关联到元数据类的模型类时，这些属性应用于该模型。 在此方法中，模型类可以重新生成而不会丢失所有已应用于元数据类的属性。

在中**模型**文件夹中，添加一个名为类**Metadata.cs**。

![添加元数据类](enhancing-data-validation/_static/image3.png)

将以下代码替换为 Metadata.cs 中的代码。

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

这些元数据类包含所有先前应用到模型类的验证特性。 **显示**特性用于更改使用的文本标签的值。

现在，必须将模型类关联的元数据类。

在中**模型**文件夹中，添加一个名为类**PartialClasses.cs**。

将以下代码替换为该文件的内容。

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

请注意，每个类标记为`partial`类，并且每个匹配的名称和命名空间为自动生成的类。 通过将元数据特性应用到分部类，可确保数据验证属性，将应用到自动生成类。 当你重新生成模型类，因为在不重新生成的分部类中应用的元数据特性，这些属性不会丢失。

若要重新生成会自动生成的类，请打开 ContosoModel.edmx 文件。 再次重申，右键单击设计图面，然后选择**从数据库更新模型**。 即使没有更改数据库，此过程将重新生成类。 在中**刷新**选项卡上，选择**表**并**完成**。

![刷新表](enhancing-data-validation/_static/image4.png)

保存 ContosoModel.edmx 文件以应用更改。

打开 Student.cs 文件或 Enrollment.cs 文件，并请注意，您先前应用的数据验证属性将不再在文件中。 但是，运行该应用程序，并请注意，当输入数据时仍应用验证规则。

> [!div class="step-by-step"]
> [上一页](customizing-a-view.md)
> [下一页](publish-to-azure.md)
