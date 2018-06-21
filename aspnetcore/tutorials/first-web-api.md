---
title: 使用 ASP.NET Core 和 Visual Studio for Windows 创建 Web API
author: rick-anderson
description: 使用 ASP.NET Core MVC 和 Visual Studio for Windows 生成 Web API
ms.author: riande
ms.custom: mvc
ms.date: 05/17/2018
uid: tutorials/first-web-api
ms.openlocfilehash: 3da22cbbbe0db7771656997a13587521e182fb2a
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277395"
---
# <a name="create-a-web-api-with-aspnet-core-and-visual-studio-for-windows"></a>使用 ASP.NET Core 和 Visual Studio for Windows 创建 Web API

作者：[Rick Anderson](https://twitter.com/RickAndMSFT) 和 [Mike Wasson](https://github.com/mikewasson)

本教程构建了用于管理“待办事项”列表的 Web API。 未创建用户界面 (UI)。

本教程提供 3 个版本：

* Windows：使用 Visual Studio for Windows 创建 Web API（本教程）
* macOS：[使用 Visual Studio for Mac 创建 Web API](xref:tutorials/first-web-api-mac)
* macOS、Linux、Windows：[使用 Visual Studio Code 创建 Web API](xref:tutorials/web-api-vsc)

<!-- WARNING: The code AND images in this doc are used by uid: tutorials/web-api-vsc, tutorials/first-web-api-mac and tutorials/first-web-api. If you change any code/images in this tutorial, update uid: tutorials/web-api-vsc -->

[!INCLUDE[intro to web API](../includes/webApi/intro.md)]

## <a name="prerequisites"></a>系统必备

[!INCLUDE[](~/includes/net-core-prereqs-windows.md)]

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中执行以下步骤：

* 从“文件”菜单中选择“新建” > “项目”。
* 选择“ASP.NET Core Web 应用程序”模板。 将项目命名为 TodoApi，然后单击“确定”。
* 在“新建 ASP.NET Core Web 应用程序 - TodoApi”对话框中，选择 ASP.NET Core 版本。 选择“API”模板，然后单击“确定”。 请不要选择“启用 Docker 支持”。

### <a name="launch-the-app"></a>启动应用

在 Visual Studio 中，按 CTRL+F5 启动应用。 Visual Studio 启动浏览器并导航到 `http://localhost:<port>/api/values`，其中 `<port>` 是随机选择的端口号。 Chrome、Microsoft Edge 和 Firefox 将显示以下输出：

```json
["value1","value2"]
```

如果使用 Internet Explorer，系统将提示你保存 values.json 文件。

### <a name="add-a-model-class"></a>添加模型类

模型是表示应用中的数据的对象。 在此示例中，唯一的模型是待办事项。

在解决方案资源管理器中，右键单击项目。 选择“添加” > “新建文件夹”。 将文件夹命名为“Models”。

> [!NOTE]
> 模型类可以出现在项目的任意位置。 Models 文件夹按约定用于模型类。

在解决方案资源管理器中右键单击“模型”文件夹，然后选择“添加” > “类”。 将类命名为 TodoItem，然后单击“添加”。

使用以下代码更新 `TodoItem` 类：

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoItem.cs)]

创建 `TodoItem` 时，数据库将生成 `Id`。

### <a name="create-the-database-context"></a>创建数据库上下文

数据库上下文是为给定数据模型协调实体框架功能的主类。 此类由 `Microsoft.EntityFrameworkCore.DbContext` 类派生而来。

在解决方案资源管理器中右键单击“模型”文件夹，然后选择“添加” > “类”。 将类命名为 TodoContext，然后单击“添加”。

将该类替换为以下代码：

[!code-csharp[](first-web-api/samples/2.0/TodoApi/Models/TodoContext.cs)]

[!INCLUDE[Register the database context](../includes/webApi/register_dbContext.md)]

### <a name="add-a-controller"></a>添加控制器

在解决方案资源管理器中，右键单击“控制器”文件夹。 选择 **添加** > **新建项**。 在“添加新项”对话框中，选择“API 控制器类”模板。 将类命名为 TodoController，然后单击“添加”。

![“添加新项”对话框，“控制器”显示在搜索框中，并且“Web API 控制器”已选中](first-web-api/_static/new_controller.png)

将该类替换为以下代码：

[!INCLUDE[code and get todo items](../includes/webApi/getTodoItems.md)]

### <a name="launch-the-app"></a>启动应用

在 Visual Studio 中，按 CTRL+F5 启动应用。 Visual Studio 启动浏览器并导航到 `http://localhost:<port>/api/values`，其中 `<port>` 是随机选择的端口号。 导航到位于 `http://localhost:<port>/api/todo` 的 `Todo` 控制器。

[!INCLUDE[last part of web API](../includes/webApi/end.md)]

[!INCLUDE[jQuery](../includes/webApi/add-jquery.md)]

[!INCLUDE[next steps](../includes/webApi/next.md)]
