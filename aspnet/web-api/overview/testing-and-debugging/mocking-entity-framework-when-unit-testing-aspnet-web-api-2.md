---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 模拟 Entity Framework 时的单元测试 ASP.NET Web API 2 |Microsoft Docs
author: tfitzmac
description: 此指南和应用程序演示如何为 Web API 2 应用程序使用实体框架创建单元测试。 它演示了如何修改...
ms.author: aspnetcontent
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: dc50965a2757defb254d05f0b8a5fd46a90dc75f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804390"
---
<a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>模拟 Entity Framework 时的单元测试 ASP.NET Web API 2
====================
通过[Tom FitzMacken](https://github.com/tfitzmac)

[下载已完成的项目](http://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-e2867d4d)

> 此指南和应用程序演示如何为 Web API 2 应用程序使用实体框架创建单元测试。 它显示了如何修改已搭建基架的控制器，以启用传递上下文对象进行测试，以及如何创建使用实体框架的测试对象。
> 
> 使用 ASP.NET Web API 进行单元测试的简介，请参阅[Unit Testing 与 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)。
> 
> 本教程假定你熟悉的 ASP.NET Web API 的基本概念。 有关介绍性教程，请参阅[Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - [Visual Studio 2017](https://www.visualstudio.com/vs/)
> - Web API 2


## <a name="in-this-topic"></a>在本主题中

本主题包含以下各节：

- [先决条件](#prereqs)
- [下载代码](#download)
- [使用单元测试项目创建应用程序](#appwithunittest)
- [创建模型类](#modelclass)
- [添加控制器](#controller)
- [添加依赖关系注入](#dependency)
- [在测试项目中安装 NuGet 包](#testpackages)
- [创建测试上下文](#testcontext)
- [创建测试](#tests)
- [运行测试](#runtests)

如果你已完成中的步骤[Unit Testing 与 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)，则可以跳到部分[添加控制器](#controller)。

<a id="prereqs"></a>
## <a name="prerequisites"></a>系统必备

Visual Studio 2017 Community、 Professional 或 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>下载代码

下载[已完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。 可下载项目包含本主题以及单元测试代码[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主题。

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>使用单元测试项目创建应用程序

可以创建单元测试项目，创建你的应用程序时，也可以将单元测试项目添加到现有应用程序。 本教程演示创建应用程序时创建单元测试项目。

创建一个新的 ASP.NET Web 应用程序名为**StoreApp**。

在新建 ASP.NET 项目窗口中，选择**空**模板和添加文件夹和核心引用有关 Web API。 选择**添加单元测试**选项。 单元测试项目将自动命名**StoreApp.Tests**。 可以保留此名称。

![创建单元测试项目](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

创建程序后，会看到它包含两个项目- **StoreApp**并**StoreApp.Tests**。

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>创建模型类

在 StoreApp 项目中，将添加到一个类文件**模型**名为文件夹**Product.cs**。 将以下代码替换为该文件的内容。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

生成解决方案。

<a id="controller"></a>
## <a name="add-the-controller"></a>添加控制器

右键单击 Controllers 文件夹，然后选择**外**并**新基架项**。 选择 Web API 2 控制器操作使用 Entity Framework。

![添加新的控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

设置下列值：

- 控制器名称： **ProductController**
- 模型类：**产品**
- 数据上下文类: [选择**新建数据上下文**按钮填充如下所示的值的]

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

单击**添加**要创建自动生成的代码使用控制器。 代码包括用于创建、 检索、 更新和删除产品类的实例方法。 下面的代码显示了该方法用于将产品。 请注意，该方法返回的实例**IHttpActionResult**。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

IHttpActionResult 是一个 Web API 2 中的新功能，这样可以简化单元测试开发。

在下一步部分中，您将自定义生成的代码，以便将测试对象传递给控制器。

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>添加依赖关系注入

目前，ProductController 类是硬编码为使用 StoreAppContext 类的实例。 将使用称为依赖关系注入的模式来修改应用程序，并删除该硬编码的依赖关系。 通过打破这种依赖关系，您可以传入 mock 对象测试时。

右键单击**模型**文件夹，并添加名为的新界面**IStoreAppContext**。

将代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

打开 StoreAppContext.cs 文件并进行以下突出显示的更改。 需要注意的重要更改是：

- StoreAppContext 类实现 IStoreAppContext 接口
- 实现 MarkAsModified 方法


[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

打开 ProductController.cs 文件。 更改现有代码，以匹配突出显示的代码。 这些更改在 StoreAppContext 破坏依赖项，并启用要传递给不同对象中的上下文类的其他类。 此更改将可以在单元测试期间传递测试上下文中。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

没有一个详细的更改必须在 ProductController 中进行。 在中**PutProduct**方法中，将为实体状态设置为行修改为 MarkAsModified 方法的调用。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

生成解决方案。

你现已准备好设置测试项目。

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>在测试项目中安装 NuGet 包

当使用空模板创建的应用程序时，单元测试项目 (StoreApp.Tests) 不包括任何已安装的 NuGet 包。 其他模板，例如 Web API 模板中，单元测试项目中包括一些 NuGet 包。 对于本教程，必须包括实体框架包和 Microsoft ASP.NET Web API 2 核心包到测试项目。

右键单击 StoreApp.Tests 项目并选择**管理 NuGet 包**。 必须选择要将包添加到该项目的 StoreApp.Tests 项目。

![管理包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

从联机包中，查找并安装 EntityFramework 包 （版本 6.0 或更高版本）。 如果它出现 EntityFramework 包已安装，您可能选择 StoreApp 项目而不是 StoreApp.Tests 项目。

![添加实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

查找和安装 Microsoft ASP.NET Web API 2 核心包。

![安装 web api core 包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

关闭管理 NuGet 包窗口。

<a id="testcontext"></a>
## <a name="create-test-context"></a>创建测试上下文

添加名为的类**TestDbSet**到测试项目。 此类用作测试数据集类的基类。 将代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

添加名为的类**TestProductDbSet**到测试项目中包含以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

添加名为的类**TestStoreAppContext**和现有代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>创建测试

默认情况下，你的测试项目包括一个名为的空测试文件**UnitTest1.cs**。 此文件显示了用于创建测试方法的属性。 对于本教程，可以删除此文件，因为您将添加新的测试类。

添加名为的类**TestProductController**到测试项目。 将代码替换为以下代码。

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>运行测试

现在您就可以运行测试。 使用标记的方法的所有**TestMethod**属性进行测试。 从**测试**菜单项，运行测试。

![运行测试](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

打开**测试资源管理器**窗口中，并请注意，测试结果。

![测试结果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
