---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自承载 ASP.NET Web API 1 (C#) |Microsoft Docs
author: MikeWasson
description: ASP.NET Web API 不需要 IIS。 您可以在自己的主机进程中自托管 web API。 本教程演示如何在托管 web API 应用的控制台内...
ms.author: aspnetcontent
ms.date: 01/26/2012
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 50681dcd89dfed480cf343f753371af384fd3e68
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811732"
---
<a name="self-host-aspnet-web-api-1-c"></a>自承载 ASP.NET Web API 1 (C#)
====================
通过[Mike Wasson](https://github.com/MikeWasson)

> ASP.NET Web API 不需要 IIS。 您可以在自己的主机进程中自托管 web API。 本教程演示如何承载在控制台应用程序的 web API。
> 
> **新的应用程序应使用 OWIN 自托管 Web API。** 请参阅[使用 OWIN 自托管 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>在本教程中使用的软件版本
> 
> 
> - Web API 1
> - Visual Studio 2012


## <a name="create-the-console-application-project"></a>创建控制台应用程序项目

启动 Visual Studio 并选择**新的项目**从**启动**页。 或者，从**文件**菜单中，选择**新建**，然后**项目**。

在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。 下**Visual C#**，选择**Windows**。 在项目模板列表中选择**控制台应用程序**。 将项目命名&quot;SelfHost&quot;然后单击**确定**。

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>设置目标框架 (Visual Studio 2010)

如果使用 Visual Studio 2010，更改目标框架为.NET Framework 4.0。 (默认情况下，项目模板面向[.Net Framework 客户端配置文件](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)。)

在解决方案资源管理器，右键单击该项目并选择**属性**。 在中**目标框架**下拉列表中，将目标框架更改为.NET Framework 4.0。 当系统提示以应用更改，单击**是**。

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>安装 NuGet 包管理器

NuGet 包管理器是 Web API 程序集添加到非 ASP.NET 项目的最简单方法。

若要检查是否已安装 NuGet 包管理器，请单击**工具**Visual Studio 菜单中的。 如果看到一个菜单项调用**库程序包管理器**，则具有 NuGet 包管理器。

若要安装 NuGet 包管理器：

1. 启动 Visual Studio。
2. 从**工具**菜单中，选择**扩展和更新**。
3. 在中**扩展和更新**对话框中，选择**联机**。
4. 如果看不到"NuGet 包管理器"，请在搜索框中键入"nuget 包管理器"。
5. 选择 NuGet 包管理器，然后单击**下载**。
6. 下载完成后，系统将提示安装。
7. 安装完成后，你可能会提示您重新启动 Visual Studio。

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>添加 Web API NuGet 包

安装 NuGet 包管理器后，将 Web API 自托管包添加到你的项目。

1. 从**工具**菜单中，选择**库程序包管理器**。 *请注意*： 如果你不会看到此菜单项，请确保已正确安装该 NuGet 包管理器。
2. 选择**管理解决方案的 NuGet 包...**
3. 在中**Manage NugGet Packages**对话框中，选择**联机**。
4. 在搜索框中，键入&quot;Microsoft.AspNet.WebApi.SelfHost&quot;。
5. 选择 ASP.NET Web API 自宿主包，然后单击**安装**。
6. 包将安装后，单击**关闭**关闭对话框。

> [!NOTE]
> 请确保安装名为 Microsoft.AspNet.WebApi.SelfHost，不 AspNetWebApi.SelfHost 的包。


![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>创建模型和控制器

本教程使用相同的模型和控制器类[Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。

添加一个名为的公共类`Product`。

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

添加一个名为的公共类`ProductsController`。 从该类派生**System.Web.Http.ApiController**。

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

有关此控制器中的代码的详细信息，请参阅[Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。 此控制器定义了三个 GET 操作：

| URI | 描述 |
| --- | --- |
| / api/产品 | 获取所有产品的列表。 |
| /api/产品/*id* | 获取产品的 id。 |
| /api/products/?category=*category* | 按类别获取的产品的列表。 |

## <a name="host-the-web-api"></a>承载 Web API

打开文件 Program.cs 并添加以下 using 语句：

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

将以下代码添加到**程序**类。

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>（可选）添加 HTTP URL Namespace 保留

此应用程序侦听`http://localhost:8080/`。 默认情况下，侦听特定的 HTTP 地址需要管理员权限。 当您运行本教程时，因此，可能会收到此错误:"HTTP 无法注册 URL http://+:8080/"有两种方法来避免此错误：

- 使用提升的管理员权限运行 Visual Studio 或
- 使用 Netsh.exe 让你的帐户权限以保留该 URL。

若要使用 Netsh.exe，使用管理员特权打开命令提示符并输入以下命令： 以下命令：

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

其中*按*是您的用户帐户。

完成之后自承载，请务必删除保留：

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>从客户端应用程序 (C#) 中调用 Web API

让我们来编写一个简单的控制台应用程序调用 web API。

将新的控制台应用程序项目添加到解决方案：

- 在解决方案资源管理器，右键单击解决方案并选择**添加新项目**。
- 创建名为的新控制台应用程序&quot;ClientApp&quot;。

![](self-host-a-web-api/_static/image5.png)

使用 NuGet 包管理器来添加 ASP.NET Web API 的核心库包：

- 从工具菜单中，选择**库程序包管理器**。
- 选择**管理解决方案的 NuGet 包...**
- 在中**管理 NuGet 包**对话框中，选择**联机**。
- 在搜索框中，键入&quot;Microsoft.AspNet.WebApi.Client&quot;。
- 选择 Microsoft ASP.NET Web API 客户端库包，然后单击**安装**。

到 SelfHost 项目 ClientApp 中添加的引用：

- 在解决方案资源管理器，右键单击 ClientApp 项目。
- 选择“添加引用”。
- 在中**引用管理器**对话框下**解决方案**，选择**项目**。
- 选择 SelfHost 项目。
- 单击 **“确定”**。

![](self-host-a-web-api/_static/image6.png)

打开 Client/Program.cs 文件。 添加以下**使用**语句：

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

添加静态**HttpClient**实例：

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

添加以下方法来按类别列出的所有产品，列表按 ID、 产品和产品列表。

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

每种方法如下所示相同的模式：

1. 调用**HttpClient.GetAsync**将 GET 请求发送到的相应 URI。
2. 调用**HttpResponseMessage.EnsureSuccessStatusCode**。 如果 HTTP 响应状态为错误代码，此方法将引发异常。
3. 调用**ReadAsAsync&lt;T&gt;** 要反序列化的 HTTP 响应中的 CLR 类型。 此方法是在定义的扩展方法**System.Net.Http.HttpContentExtensions**。

**GetAsync**并**ReadAsAsync**方法均异步。 它们将返回**任务**对象，后者表示异步操作。 获取**结果**属性阻止线程，直到操作完成。

有关使用 HttpClient，包括如何执行非阻止调用，请参阅[调用 Web API 从.NET 客户端](../advanced/calling-a-web-api-from-a-net-client.md)。

调用这些方法之前, 将 BaseAddress 属性设置到 HttpClient 实例上"`http://localhost:8080`"。 例如：

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

这应输出以下。 （请记住要首先运行 SelfHost 应用程序。）

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
