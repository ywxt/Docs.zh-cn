---
title: 添加、 下载和删除标识到 ASP.NET Core项目中的自定义用户数据
author: rick-anderson
description: 了解如何在 ASP.NET Core 项目中添加到标识的自定义用户数据。 删除每个 GDPR 数据。
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 6/16/2018
uid: security/authentication/add-user-data
ms.openlocfilehash: ecd0e6d1c71b24309fab70fbb06af7731463bb0e
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36271952"
---
# <a name="add-download-and-delete-custom-user-data-to-identity-in-an-aspnet-core-project"></a>添加、 下载和删除标识到 ASP.NET Core项目中的自定义用户数据

作者：[Rick Anderson](https://twitter.com/RickAndMSFT)

这篇文章演示如何：

* 将自定义用户数据添加到 ASP.NET Core web 应用程序。
* 修饰具有自定义用户数据模型[PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1)属性，以便它自动下载和删除。 使能够下载和删除这些数据可帮助满足[GDPR](xref:security/gdpr)要求。

项目示例将创建从 Razor 页 web 应用，但了 ASP.NET Core MVC web 应用的类似的说明。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

## <a name="prerequisites"></a>系统必备

[!INCLUDE [](~/includes/2.1-SDK.md)]

## <a name="create-a-razor-web-app"></a>创建 Razor Web 应用

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 从 Visual Studio“文件”菜单中选择“新建” > “项目”。 将项目**WebApp1**如果您希望与其匹配的命名空间[下载示例](https://github.com/aspnet/Docs/tree/live/aspnetcore/security/authentication/add-user-data/sample)代码。
* 选择**ASP.NET Core Web 应用程序** > **确定**
* 选择**ASP.NET Core 2.1**下拉列表中
* 选择**Web 应用程序**  > **确定**
* 生成并运行该项目。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet new webapp -o WebApp1
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

## <a name="run-the-identity-scaffolder"></a>运行标识基架

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

* 从**解决方案资源管理器**，右键单击该项目 >**添加** > **新建基架项**。
* 从左窗格**添加基架**对话框中，选择**标识** > **添加**。
* 在**添加标识**对话框中，以下选项：
  * 选择现有的布局文件 *~/Pages/Shared/_Layout.cshtml*
  * 选择要重写的以下文件：
    * **帐户/注册**
    * **帐户/管理/索引**
  * 选择**+** 按钮以创建一个新**数据上下文类**。 接受类型 (**WebApp1.Models.WebApp1Context**如果名为项目**WebApp1**)。
  * 选择**+** 按钮以创建一个新**用户类**。 接受类型 (**WebApp1User**如果名为项目**WebApp1**) >**添加**。
* 选择**添加**。

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

如果以前尚未安装 ASP.NET 基架，请立即进行安装：

```cli
dotnet tool install -g dotnet-aspnet-codegenerator
```

添加对的包引用[Microsoft.VisualStudio.Web.CodeGeneration.Design](https://www.nuget.org/packages/Microsoft.VisualStudio.Web.CodeGeneration.Design/)项目 (.csproj) 文件。 在项目目录中运行以下命令：

```cli
dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design
dotnet restore
```

运行以下命令以列出标识基架选项：

```cli
dotnet aspnet-codegenerator identity -h
```

在项目文件夹中，运行标识基架：

```cli
dotnet aspnet-codegenerator identity -u WebApp1User -fi Account.Register;Account.Manage.Index
```

-------------

按照中的说明[迁移、 UseAuthentication 和布局](xref:security/authentication/scaffold-identity#efm)以执行以下步骤：

* 创建迁移并更新数据库。
* 将 `UseAuthentication` 添加到 `Startup.Configure`。
* 添加`<partial name="_LoginPartial" />`布局文件。
* 测试应用：
  * 注册用户
  * 选择新的用户名称 (旁边**注销**链接)。 你可能需要展开该窗口或选择要显示的用户名和其他链接的导航栏图标。
  * 选择**个人数据**选项卡。
  * 选择**下载**按钮，然后检查*PersonalData.json*文件。
  * 测试**删除**按钮，删除已登录用户。

## <a name="add-custom-user-data-to-the-identity-db"></a>将自定义用户数据添加到标识数据库

更新`IdentityUser`派生类与自定义属性。 如果名为你的项目 WebApp1 时，该文件名为*Areas/Identity/Data/WebApp1User.cs*。 替换为以下代码更新文件：

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Data/WebApp1User.cs)]

使用修饰属性， [PersonalData](/dotnet/api/microsoft.aspnetcore.identity.personaldataattribute?view=aspnetcore-2.1)属性：

* 删除时*Areas/Identity/Pages/Account/Manage/DeletePersonalData.cshtml* Razor 页调用`UserManager.Delete`。
* 包含在下载的数据通过*Areas/Identity/Pages/Account/Manage/DownloadPersonalData.cshtml* Razor 页。

### <a name="update-the-accountmanageindexcshtml-page"></a>更新 Account/Manage/Index.cshtml 页

更新`InputModel`中*Areas/Identity/Pages/Account/Manage/Index.cshtml.cs*替换为以下突出显示的代码：

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml.cs?name=snippet&highlight=28-36,63-64,87-95,120)]

更新*Areas/Identity/Pages/Account/Manage/Index.cshtml*替换为以下突出显示的标记：

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Manage/Index.cshtml?highlight=34-41)]

### <a name="update-the-accountregistercshtml-page"></a>更新 Account/Register.cshtml 页

更新`InputModel`中*Areas/Identity/Pages/Account/Register.cshtml.cs*替换为以下突出显示的代码：

[!code-csharp[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml.cs?name=snippet&highlight=8-16,43,44)]

更新*Areas/Identity/Pages/Account/Register.cshtml*替换为以下突出显示的标记：

[!code-html[Main](add-user-data/sample/Areas/Identity/Pages/Account/Register.cshtml?highlight=16-25)]

生成项目。

### <a name="add-a-migration-for-the-custom-user-data"></a>添加自定义用户数据的迁移

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio)

在 Visual Studio**程序包管理器控制台**:

```PMC
Add-Migration CustomUserData
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```cli
dotnet ef migrations add CustomUserData
dotnet ef database update
```

------

## <a name="test-create-view-download-delete-custom-user-data"></a>测试创建、 查看、 下载、 删除自定义用户数据

测试应用：

* 注册新的用户。
* 查看自定义用户数据`/Identity/Account/Manage`页。
* 下载并查看来自用户个人数据`/Identity/Account/Manage/PersonalData`页。
