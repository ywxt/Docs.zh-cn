---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 第一种使用 ASP.NET MVC 的 EF 数据库： 生成视图 |Microsoft Docs
author: tfitzmac
description: 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 此教程系列...
ms.author: aspnetcontent
ms.date: 12/29/2014
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: 9c85b330ac415d8c73d58b31a5108197b754669f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37835323"
---
<a name="ef-database-first-with-aspnet-mvc-generating-views"></a>第一种使用 ASP.NET MVC 的 EF 数据库： 生成视图
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

> 使用 MVC、 Entity Framework 和 ASP.NET 基架，可以创建提供接口的现有数据库的 web 应用程序。 本系列教程演示了如何自动生成代码，使用户能够显示、 编辑、 创建和删除驻留在数据库表中的数据。 生成的代码对应于数据库表中的列。
> 
> 本系列的此部分重点介绍使用 ASP.NET 基架生成控制器和视图。


## <a name="add-scaffold"></a>添加基架

已准备好生成将提供标准数据操作，以便在 model 类的代码。 通过添加基架项添加代码。 有许多选项的类型的基架可以添加;在本教程中，基架将包括控制器和对应于上一节中创建的 Student 和注册模型的视图。

若要维护你的项目中的一致性，将添加新控制器到现有**控制器**文件夹。 右键单击**控制器**文件夹，然后选择**添加**–**新基架项**。

![添加基架](generating-views/_static/image1.png)

选择**包含的 MVC 5 控制器视图，使用实体框架**选项。 此选项将生成控制器和视图更新、 删除、 创建和显示模型中的数据。

![添加 mvc 控制器](generating-views/_static/image2.png)

选择**学生**模型类，然后选择**ContosoUniversityEntities**上下文类。 保留作为控制器名称**StudentsController**，

![指定控制器](generating-views/_static/image3.png)

单击 **添加**。

如果收到错误，则可能是因为未生成上一节中的项目。 如果是这样，请尝试生成项目，，然后再次添加基架的项。

代码生成过程完成后，您将在项目中看到新的控制器和视图。

![显示视图](generating-views/_static/image4.png)

同样，执行相同的步骤，但添加注册类的基本框架。 完成后，应拥有**EnrollmentsController.cs**文件和文件夹下的**视图**名为**注册**与创建、 删除、 详细信息、 编辑和索引视图。

![显示视图](generating-views/_static/image5.png)

## <a name="add-links-to-new-views"></a>将链接添加到新的视图

若要使你更轻松地导航到新视图，可以索引视图中添加几个超链接，面向学生和注册。 打开的文件**Views/Home/Index.cshtml**，这是你的站点的主页。 添加 jumbotron 下面的代码。

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

对于 ActionLink 方法中，第一个参数是要显示的链接中的文本。 第二个参数是操作，第三个参数是控制器的名称。 例如，第一个链接指向 StudentsController 中的索引操作。 实际的超链接，这些值从构造。 第一个链接最终用户可转到**Index.cshtml**文件内**视图/学生**文件夹。

## <a name="display-student-views"></a>显示学生视图

将验证正确添加到你的项目的代码显示学生列表，并使用户能够编辑、 创建或删除数据库中的学生记录。

右键单击**Views/Home/Index.cshtml**文件，并选择**用浏览器查看**。 在此页上，单击学生列表的链接。

![](generating-views/_static/image6.png)

在此页上，请注意，若要修改此数据的学生和链接的列表。

![学生列表](generating-views/_static/image7.png)

单击**创建新**链接并为新的学生提供一些值。

![创建新学生](generating-views/_static/image8.png)

单击**创建**，并请注意，新学生添加到列表。

![具有新学生列表](generating-views/_static/image9.png)

选择**编辑**链接，并更改值的一些学生。

![编辑学生](generating-views/_static/image10.png)

单击**保存**，您会发现已更改学生记录。

最后，选择**删除**链接，然后确认你想要通过单击删除的记录**删除**按钮。

![删除学生](generating-views/_static/image11.png)

无需编写任何代码，您已添加在 Student 表中执行常见操作的数据的视图。

您可能已经注意到一个字段的文本标签基于的数据库属性 (如**LastName**) 这不一定是你想要在网页上显示。 例如，可能想要进行的标签**姓氏**。 本教程的后面，则将修复此显示问题。

## <a name="display-enrollment-views"></a>显示注册视图

你的数据库包括一个对多关系学生和注册表中与 Course 和 Enrollment 表之间的一个对多关系之间。 为注册视图正确处理这些关系。 导航到站点并选择主页**注册列表**链接，然后**创建新**链接。 该视图显示用于创建新的注册记录的窗体。 具体而言，请注意该窗体包含两个相关表中的值填充的下拉列表。

![创建注册](generating-views/_static/image12.png)

此外，验证所提供的值将自动应用基于字段的数据类型。 等级需要一个数字，因此如果你尝试提供不兼容的值显示一条错误消息。

![验证消息](generating-views/_static/image13.png)

您已验证的自动生成的视图使用户能够处理在数据库中的数据。 在本系列中下一个教程中，将更新数据库，并在 web 应用程序中进行相应更改。

> [!div class="step-by-step"]
> [上一页](creating-the-web-application.md)
> [下一页](changing-the-database.md)
