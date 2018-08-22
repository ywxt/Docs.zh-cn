---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 调用 Web API 从 Windows Phone 8 应用程序 (C#) |Microsoft Docs
author: rmcmurray
description: 创建完整的端到端方案包含的 ASP.NET Web API 应用程序提供了一个 Windows Phone 8 应用程序的本书籍的目录。
ms.author: riande
ms.date: 10/09/2013
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: ca2b5f41f6c3bd38faacd1e15c4dee6f6210aff7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830450"
---
<a name="calling-web-api-from-a-windows-phone-8-application-c"></a>调用 Web API 从 Windows Phone 8 应用程序 (C#)
====================
通过[Robert McMurray](https://github.com/rmcmurray)

在本教程中，您将学习如何创建完整的端到端方案包含的 ASP.NET Web API 应用程序提供了一个 Windows Phone 8 应用程序的本书籍的目录。

### <a name="overview"></a>概述

如 ASP.NET Web API rESTful 服务通过抽象化为服务器端和客户端应用程序的体系结构简化面向开发人员的基于 HTTP 的应用程序的创建。 而不是创建一种专有的基于套接字协议进行通信，Web API 开发人员只需发布自己的应用程序的必需 HTTP 方法 (例如： GET、 POST、 PUT、 DELETE)，并且客户端应用程序开发人员只需要使用所其应用程序所需的 HTTP 方法。

在本端到端教程，您将学习如何使用 Web API 来创建以下项目：

- 在中[此教程的第一部分](#STEP1)，将创建支持所有创建、 读取、 更新和删除 (CRUD) 操作来管理书籍目录的 ASP.NET Web API 应用程序。 此应用程序将使用[示例 XML 文件 (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx)从 MSDN。
- 在中[在本教程的第二个](#STEP2)，将创建从 Web API 应用程序中检索数据的交互式 Windows Phone 8 应用程序。

#### <a name="prerequisites"></a>系统必备

- 已安装 Windows Phone 8 sdk 的 visual Studio 2013
- Windows 8 或更高版本上安装 HYPER-V 的 64 位系统
- 有关其他要求的列表，请参阅*系统要求*部分[Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下载页。

> [!NOTE]
> 如果要测试 Web API 和本地系统上的 Windows Phone 8 项目之间的连接，你将需要按照中的说明*[连接到本地的 Web API 应用程序的 Windows Phone 8 仿真程序计算机](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文，设置测试环境。


<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>步骤 1： 创建 Web API 书店项目

本端到端教程的第一步是创建的所有 CRUD 操作; 支持的 Web API 项目请注意，将向此解决方案中添加 Windows Phone 应用程序项目[步骤 2](#STEP2)本教程。

1. 打开**Visual Studio 2013**。
2. 单击**文件**，然后**新**，然后**项目**。
3. 当**新的项目**对话框中，展开**已安装**，然后**模板**，然后**Visual C#**，，然后**Web**。


   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                单击以展开的图像                                                                |


4. 突出显示**ASP.NET Web 应用程序**，输入**书店**以及该项目名称，然后单击**确定**。
5. 当**新建 ASP.NET 项目**对话框中，选择**Web API**模板，，然后单击**确定**。


   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                单击以展开的图像                                                                |


6. Web API 项目打开后，从项目中删除示例控制器：

    1. 展开**控制器**在解决方案资源管理器中的文件夹。
    2. 右键单击**ValuesController.cs**文件，，然后单击**删除**。
    3. 单击**确定**当系统提示你确认删除。
7. 将 XML 数据文件添加到 Web API 项目中;此文件包含书店目录的内容：

   1. 右键单击**应用程序\_数据**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**新项**。
   2. 当**添加新项**对话框中，突出显示**XML 文件**模板。
   3. 将文件命名**Books.xml**，然后单击**添加**。
   4. 当**Books.xml**打开文件，并替换的示例 XML 文件中的代码**books.xml** MSDN 上的文件： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. 保存并关闭 XML 文件。

8. 将书店模型添加到 Web API 项目中;此模型包含的书店应用程序的创建、 读取、 更新和删除 (CRUD) 逻辑：

   1. 右键单击**模型**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**类**。
   2. 当**添加新项**对话框中，将该类文件命名**BookDetails.cs**，然后单击**添加**。
   3. 当**BookDetails.cs**打开文件、 文件中的代码替换为以下： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. 保存并关闭**BookDetails.cs**文件。

9. 将书店控制器添加到 Web API 项目：

   1. 右键单击**控制器**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**控制器**。
   2. 当**添加基架**对话框中，突出显示**Web API 2 控制器-空**，然后单击**添加**。
   3. 当**添加控制器**对话框中，将控制器命名**BooksController**，然后单击**添加**。
   4. 当**BooksController.cs**打开文件、 文件中的代码替换为以下： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. 保存并关闭**BooksController.cs**文件。

10. 构建 Web API 应用程序，以检查有错误。

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>步骤 2： 添加 Windows Phone 8 书店目录项目

此端到端方案的下一步是创建 Windows Phone 8 目录应用程序。 此应用程序将使用*Windows Phone 数据绑定应用*模板的默认用户界面，并且它将使用你在中创建的 Web API 应用程序[第 1 步](#STEP1)的本教程中作为数据源。

1. 右键单击**书店**中的解决方案在解决方案资源管理器，然后单击**添加**，然后**新项目**。
2. 当**新项目**对话框中，展开**已安装**，然后**Visual C#**，然后**Windows Phone**。
3. 突出显示**Windows Phone 数据绑定应用**，输入**BookCatalog**作为名称，然后单击**确定**。
4. 添加到 Json.NET NuGet 包**BookCatalog**项目：

    1. 右键单击**引用**有关**BookCatalog**项目在解决方案资源管理器中，然后单击**管理 NuGet 包**。
    2. 当**管理 NuGet 包**对话框中，展开**联机**部分，并突出显示**nuget.org**。
    3. 输入**Json.NET**在搜索字段，然后单击搜索图标。
    4. 突出显示**Json.NET**在搜索结果中，然后单击**安装**。
    5. 安装完成后，单击**关闭**。
5. 添加**BookDetails**模型到**BookCatalog**项目; 这包含书店类的常规模型：

   1. 右键单击**BookCatalog**项目在解决方案资源管理器，然后单击**添加**，然后单击**新文件夹**。
   2. 将新文件夹命名**模型**。
   3. 右键单击**模型**文件夹中的解决方案资源管理器，然后单击**添加**，然后单击**类**。
   4. 当**添加新项**对话框中，将该类文件命名**BookDetails.cs**，然后单击**添加**。
   5. 当**BookDetails.cs**打开文件、 文件中的代码替换为以下： 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. 保存并关闭**BookDetails.cs**文件。

6. 更新**MainViewModel.cs**类，以包含与书店 Web API 应用程序进行通信的功能：

   1. 展开**Viewmodel**文件夹中的解决方案资源管理器，然后再双击**MainViewModel.cs**文件。
   2. 当**MainViewModel.cs**打开文件时，文件中的代码替换为以下; 请注意，你将需要更新的值`apiUrl`常量与您的 Web API 的实际 URL: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. 保存并关闭**MainViewModel.cs**文件。

7. 更新**MainPage.xaml**文件以自定义应用程序名称：

   1. 双击**MainPage.xaml**在解决方案资源管理器中的文件。
   2. 当**MainPage.xaml**打开文件，找到以下代码行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. 使用以下内容替换这些行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. 保存并关闭**MainPage.xaml**文件。

8. 更新**DetailsPage.xaml**文件以自定义显示的项：

   1. 双击**DetailsPage.xaml**在解决方案资源管理器中的文件。
   2. 当**DetailsPage.xaml**打开文件，找到以下代码行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. 使用以下内容替换这些行： 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. 保存并关闭**DetailsPage.xaml**文件。

9. 构建 Windows Phone 应用程序，以检查有错误。

### <a name="step-3-testing-the-end-to-end-solution"></a>步骤 3： 测试端到端解决方案

如中所述*先决条件*本教程中，在测试 Web API 和 Windows Phone 8 之间的连接时的部分项目在本地系统上，将需要按照中的说明 *[连接到本地计算机上的 Web API 应用程序的 Windows Phone 8 仿真程序](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文，设置测试环境。

配置测试环境后，需要将 Windows Phone 应用程序设置为启动项目。 若要执行此操作，突出显示**BookCatalog**应用程序在解决方案资源管理器，然后单击**设为启动项目**:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| 单击以展开的图像 |

按 F5 时，Visual Studio 将启动这两个 Windows Phone 仿真程序，将显示&quot;稍候&quot;消息而从 Web API 中检索应用程序数据：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| 单击以展开的图像 |

如果所有内容均成功，应看到显示的目录：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| 单击以展开的图像 |

如果点击任何书籍标题时，应用程序将显示书籍说明：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| 单击以展开的图像 |

如果应用程序不能使用的 Web API 进行通信，将显示一条错误消息：

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| 单击以展开的图像 |

如果点击错误消息时，将显示有关错误的任何其他详细信息：


| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 单击以展开的图像                                                                 |

