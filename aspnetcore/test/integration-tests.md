---
title: 在 ASP.NET Core 的集成测试
author: guardrex
description: 了解如何集成测试确保应用程序的组件正常在基础结构级别，包括数据库、 文件系统和网络。
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 05/30/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: test/integration-tests
ms.openlocfilehash: a402c3f5f6a75917eba4058e6cc6926f25b214d4
ms.sourcegitcommit: 726ffab258070b4fe6cf950bf030ce10c0c07bb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "35217536"
---
# <a name="integration-tests-in-aspnet-core"></a>在 ASP.NET Core 的集成测试

通过[Luke Latham](https://github.com/guardrex)和[Steve Smith](https://ardalis.com/)

集成测试确保应用程序的组件正常工作，其中包含应用程序的支持的基础结构，例如数据库、 文件系统和网络级别。 ASP.NET 核心支持测试 web 宿主和内存中测试服务器中使用单元测试框架的集成测试。

本主题假定单元测试的一个基本的了解。 如果测试概念不太熟悉，请参阅[在.NET 核心和标准.NET 中的单元测试](/dotnet/core/testing/)主题和其链接的内容。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）

示例应用程序是 Razor 页应用，并假定 Razor 页的一个基本的了解。 如果熟悉 Razor 页，请参阅以下主题：

* [Razor 页面介绍](xref:mvc/razor-pages/index)
* [Razor 页面入门](xref:tutorials/razor-pages/razor-pages-start)
* [Razor 页单元测试](xref:test/razor-pages-tests)

## <a name="introduction-to-integration-tests"></a>集成测试的简介

集成测试评估比更广泛级别上的应用程序的组件[单元测试](/dotnet/core/testing/)。 单元测试用于测试独立的软件组件，例如单独的类的方法。 集成测试可确认，两个或多个应用程序组件配合工作来生成预期的结果，还可能包括完全处理某个请求所需的每个组件。

这些更广泛测试用于测试应用程序的基础结构和整个框架，通常包括以下组件：

* 数据库
* 文件系统
* 网络设备
* 请求-响应管道

单元测试使用制造的组件，称为*fakes*或*模拟对象*，替代基础结构组件。

与单元测试集成测试：

* 使用应用程序在生产中使用的实际组件。
* 需要更多代码和数据处理。
* 需要更长时间才能运行。

因此，限制到最重要的基础结构方案的集成测试使用。 使用单元测试或集成测试，可以测试行为，如果选择的单元测试。

> [!TIP]
> 不写入数据库和文件系统使用的数据和文件访问每个可能排列的集成测试。 而不考虑跨应用程序的多少位与数据库和文件系统、 集中的读取、 写入、 更新和删除集成测试通常能够充分测试数据库和文件系统组件进行交互。 使用单元测试的方法逻辑例程与这些组件进行交互的测试。 在单位测试中的基础结构使用 fakes/mock 中测试执行速度更快的结果。

> [!NOTE]
> 在讨论的集成测试，测试的项目经常称为*待测试系统*，或简称"SUT"。

## <a name="aspnet-core-integration-tests"></a>ASP.NET 核心集成测试

集成测试在 ASP.NET 核心中的有以下要求：

* 测试项目用于包含并执行测试。 测试项目具有对经过测试的 ASP.NET Core 项目中，调用的引用*待测试系统*(SUT)。 _在本主题使用"SUT"来指代经过测试的应用程序。_
* 测试项目创建 SUT 测试 web 主机，并使用测试服务器客户端以处理请求和响应 SUT。
* 测试运行程序用于执行的测试和报告测试结果。

集成测试遵循事件，其中包括常用序列*排列*， *Act*，和*断言*测试步骤：

1. SUT 的 web 主机配置。
1. 测试服务器客户端创建以将请求提交到应用程序。
1. *排列*执行测试步骤： 测试应用程序准备请求。
1. *Act*执行测试步骤： 客户端提交该请求并接收响应。
1. *断言*执行测试步骤：*实际*响应进行验证*传递*或*失败*基于*预期*响应。
1. 此过程将继续之前执行的所有测试。
1. 报告测试结果。

通常情况下，测试 web 主机配置以不同的方式不是测试应用程序的正常 web 主机都运行。 例如，不同的数据库或不同的应用程序设置可用于测试。

基础结构组件，例如测试 web 主机和内存中测试服务器 ([TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver))、 提供或由管理[Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing)包。 测试创建和执行，从而简化了使用此包。

`Microsoft.AspNetCore.Mvc.Testing`包处理以下任务：

* 将复制依赖项文件 (*\*.deps*) 从入测试项目的 SUT *bin*文件夹。
* 请设置为 SUT 的项目根目录内容的根，静态文件和页/视图位于测试执行的时间。
* 提供[WebApplicationFactory](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1)类来简化引导与 SUT `TestServer`。

[单元测试](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)文档介绍如何设置的测试项目和测试运行程序，以及如何运行测试和了解建议的名称测试和测试类的详细说明。

> [!NOTE]
> 在创建应用程序测试项目时，将单元测试集成测试与分开到不同的项目。 这有助于确保测试的基础结构组件不意外包括在单元测试。 单元和集成测试的分离还允许控制通过的测试运行。

几乎 Razor 页应用的测试的配置和 MVC 应用程序之间没有差异。 唯一的区别是在测试的命名方式。 在 Razor 页应用中，测试页终结点通常命名页模型类 (例如，`IndexPageTests`测试索引页的组件集成)。 在 MVC 应用程序，测试通常组织由控制器类和命名它们所测试的控制器 (例如，`HomeControllerTests`测试 Home 控制器的组件集成)。

## <a name="test-app-prerequisites"></a>测试应用程序的必备组件

测试项目必须：

* 有关包引用[Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App/)。
* 在项目文件中使用 Web SDK (`<Project Sdk="Microsoft.NET.Sdk.Web">`)。

可在中查看这些 prerequesities[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)。 检查*tests/RazorPagesProject.Tests/RazorPagesProject.Tests.csproj*文件。

## <a name="basic-tests-with-the-default-webapplicationfactory"></a>使用默认 WebApplicationFactory 的基本测试

[WebApplicationFactory&lt;TEntryPoint&gt; ](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1)用于创建[TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)集成测试。 `TEntryPoint` 通常是对 sut 的入口点类`Startup`类。

测试类实现*类配件*接口 (`IClassFixture`) 以指示类包含测试和跨类中的测试提供共享的对象实例。

### <a name="basic-test-of-app-endpoints"></a>基本应用程序终结点的测试

以下测试类， `BasicTests`，使用`WebApplicationFactory`引导 SUT 并提供[HttpClient](/dotnet/api/system.net.http.httpclient)到测试方法时， `Get_EndpointsReturnSuccessAndCorrectContentType`。 该方法检查是否成功的响应状态代码 （200 299 的范围中的状态代码） 和`Content-Type`标头是`text/html; charset=utf-8`为多个应用程序页面。

[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient)创建的实例`HttpClient`自动遵循重定向和处理 cookie。

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet1)]

### <a name="test-a-secure-endpoint"></a>测试安全的终结点

中的另一个测试`BasicTests`类将检查安全的终结点到应用程序的登录页将未经身份验证的用户重定向。

在 SUT，`/SecurePage`页上使用[AuthorizePage](/dotnet/api/microsoft.extensions.dependencyinjection.pageconventioncollectionextensions.authorizepage)约定将[AuthorizeFilter](/dotnet/api/microsoft.aspnetcore.mvc.authorization.authorizefilter)到页。 有关详细信息，请参阅[Razor 页授权约定](xref:security/authorization/razor-pages-authorization#require-authorization-to-access-a-page)。

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/src/RazorPagesProject/Startup.cs?name=snippet1)]

在`Get_SecurePageRequiresAnAuthenticatedUser`测试， [WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions)设置为禁止重定向设置[AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect)到`false`:

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/BasicTests.cs?name=snippet2)]

通过禁止客户端遵循重定向，可以进行以下检查：

* 可以检查 SUT 返回的状态代码针对预期[HttpStatusCode.Redirect](/dotnet/api/system.net.httpstatuscode)不重定向到登录页上，将是之后的最终状态代码、 结果[HttpStatusCode.OK](/dotnet/api/system.net.httpstatuscode).
* `Location`响应标头中的标头值进行检查以确认它开头`http://localhost/Identity/Account/Login`，不将最终的登录页响应，其中`Location`标头不会存在。

有关详细信息`WebApplicationFactoryClientOptions`，请参阅[客户端选项](#client-options)部分。

## <a name="customize-webapplicationfactory"></a>自定义 WebApplicationFactory

可以通过从继承独立于测试类创建 web 主机配置`WebApplicationFactory`创建一个或多个自定义工厂：

1. 继承自`WebApplicationFactory`，并重写[ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost)。 [IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder)允许具有的服务集合的配置[ConfigureServices](/dotnet/api/microsoft.aspnetcore.hosting.istartup.configureservices):

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/CustomWebApplicationFactory.cs?name=snippet1)]

   数据库在种子设定[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)由执行`InitializeDbForTests`方法。 该方法所述[集成测试的示例： 测试应用程序组织](#test-app-organization)部分。

2. 使用自定义`CustomWebApplicationFactory`测试类中。 下面的示例使用中的工厂`IndexPageTests`类：

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet1)]

   示例应用程序的客户端配置为阻止`HttpClient`从以下重定向。 中所述[测试安全的终结点](#test-a-secure-endpoint)部分中，这就允许测试以检查应用程序的第一个响应的结果。 第一个响应是在很多与这些测试的重定向`Location`标头。

3. 典型测试使用`HttpClient`和帮助器方法来处理请求和响应：

   [!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet2)]

向 SUT 任何 POST 请求必须满足 antiforgery 检查自动是由应用程序的开发[数据保护 antiforgery 系统](xref:security/data-protection/introduction)。 若要安排某个测试的 POST 请求，测试应用程序必须：

1. 请对页的请求。
1. 分析 antiforgery cookie 和响应的请求验证令牌。
1. 到位，请使用 antiforgery 的 cookie 与请求验证的 POST 请求令牌。

`SendAsync` Helper 扩展方法 (*Helpers/HttpClientExtensions.cs*) 和`GetDocumentAsync`帮助器方法 (*Helpers/HtmlHelpers.cs*) 中[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples/)使用[AngleSharp](https://anglesharp.github.io/)分析器以使用下列方法处理 antiforgery 检查：

* `GetDocumentAsync` &ndash; 接收[HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage)并返回`IHtmlDocument`。 `GetDocumentAsync` 使用一个工厂，它准备*虚拟响应*基于原始`HttpResponseMessage`。 有关详细信息，请参阅[AngleSharp 文档](https://github.com/AngleSharp/AngleSharp#documentation)。
* `SendAsync` 扩展方法`HttpClient`撰写[HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage)并调用[SendAsync(HttpRequestMessage)](/dotnet/api/system.net.http.httpclient.sendasync#System_Net_Http_HttpClient_SendAsync_System_Net_Http_HttpRequestMessage_)将向 SUT 提交请求。 有关重载`SendAsync`接受 HTML 窗体 (`IHtmlFormElement`) 及以下：
  - 提交该窗体按钮 (`IHtmlElement`)
  - 窗体值集合 (`IEnumerable<KeyValuePair<string, string>>`)
  - 提交按钮 (`IHtmlElement`) 和窗体值 (`IEnumerable<KeyValuePair<string, string>>`)

> [!NOTE]
> [AngleSharp](https://anglesharp.github.io/)第三方分析用于演示目的，本主题和示例应用程序中的库。 AngleSharp 不受支持或所需的集成测试的 ASP.NET Core 应用。 其他分析程序可以使用，如[Html 灵活性包 (HAP)](http://html-agility-pack.net/)。 另一种方法是编写代码来直接处理 antiforgery 系统请求验证令牌和 antiforgery cookie。

## <a name="customize-the-client-with-withwebhostbuilder"></a>自定义客户端与 WithWebHostBuilder

在测试方法中，需要其他配置时[WithWebHostBuilder](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.withwebhostbuilder)创建一个新`WebApplicationFactory`与[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder) ，通过配置进一步自定义。

`Post_DeleteMessageHandler_ReturnsRedirectToRoot`测试方法的[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)演示如何使用`WithWebHostBuilder`。 此测试执行将记录删除触发窗体提交数据封闭在 SUT 数据库中。

因为在另一个测试`IndexPageTests`类执行的操作将删除所有数据库中的记录和之前可能会运行`Post_DeleteMessageHandler_ReturnsRedirectToRoot`方法，该数据库设置在此测试方法，以确保记录存在 SUT 若要删除的种子值。 选择`deleteBtn1`按钮`messages`窗体中 SUT 模拟 SUT 到请求中：

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/IntegrationTests/IndexPageTests.cs?name=snippet3)]

## <a name="client-options"></a>客户端选项

下表显示的默认[WebApplicationFactoryClientOptions](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions)时创建可用`HttpClient`实例。

| 选项 | 描述 | 默认 |
| ------ | ----------- | ------- |
| [AllowAutoRedirect](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.allowautoredirect) | 获取或设置是否`HttpClient`实例应自动遵循重定向响应。 | `true` |
| [BaseAddress](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.baseaddress) | 获取或设置的基址`HttpClient`实例。 | `http://localhost` |
| [HandleCookies](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.handlecookies) | 获取或设置是否`HttpClient`实例应处理 cookie。 | `true` |
| [MaxAutomaticRedirections](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactoryclientoptions.maxautomaticredirections) | 获取或设置的重定向响应的最大数目`HttpClient`实例应遵循。 | 7 |

创建`WebApplicationFactoryClientOptions`类并将其传递到[CreateClient](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.createclient)方法 （默认值代码示例所示）：

```csharp
// Default client option values are shown
var clientOptions = new WebApplicationFactoryClientOptions();
clientOptions.AllowAutoRedirect = true;
clientOptions.BaseAddress = new Uri("http://localhost");
clientOptions.HandleCookies = true;
clientOptions.MaxAutomaticRedirections = 7;

_client = _factory.CreateClient(clientOptions);
```

## <a name="how-the-test-infrastructure-infers-the-app-content-root-path"></a>如何测试基础结构推断的应用程序内容的根路径

`WebApplicationFactory`构造函数通过搜索推断的应用程序内容的根路径[WebApplicationFactoryContentRootAttribute](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactorycontentrootattribute)包含具有键等于集成测试的程序集上`TEntryPoint`程序集`System.Reflection.Assembly.FullName`. 如果找不到具有正确的注册表项的属性，`WebApplicationFactory`回退到搜索解决方案文件 (*\*.sln*)，并追加`TEntryPoint`到解决方案目录的程序集名称。 （内容的根路径） 的应用程序根目录用于发现视图和内容文件。

在大多数情况下，无需显式设置的应用程序内容根目录位置，如搜索逻辑通常在运行时查找正确的内容根。 在未找到的内容的根的特殊情况下使用内置的搜索算法，应用程序内容显式或通过使用自定义逻辑，可以指定根。 若要将应用程序内容根目录设置在这些情况下，调用`UseSolutionRelativeContentRoot`扩展方法从[Microsoft.AspNetCore.TestHost](https://www.nuget.org/packages/Microsoft.AspNetCore.TestHost)包。 提供解决方案的相对路径和可选的解决方案文件的名称或 glob 模式 (默认 = `*.sln`)。

调用[UseSolutionRelativeContentRoot](/dotnet/api/microsoft.aspnetcore.testhost.webhostbuilderextensions.usesolutionrelativecontentroot)扩展方法使用*一个*下列方法之一：

* 配置使用的测试类时`WebApplicationFactory`，提供的自定义配置[IWebHostBuilder](/dotnet/api/microsoft.aspnetcore.hosting.iwebhostbuilder):

   ```csharp
   public IndexPageTests(
       WebApplicationFactory<RazorPagesProject.Startup> factory)
   {
       var _factory = factory.WithWebHostBuilder(builder =>
       {
           builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

           ...
       });
   }
   ```

* 使用自定义配置的测试类时`WebApplicationFactory`，继承自`WebApplicationFactory`，并重写[ConfigureWebHost](/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1.configurewebhost):

   ```csharp
   public class CustomWebApplicationFactory<TStartup>
       : WebApplicationFactory<RazorPagesProject.Startup>
   {
       protected override void ConfigureWebHost(IWebHostBuilder builder)
       {
           builder.ConfigureServices(services =>
           {
               builder.UseSolutionRelativeContentRoot("<SOLUTION-RELATIVE-PATH>");

               ...
           });
       }
   }
   ```

## <a name="disable-shadow-copying"></a>禁用卷影复制

卷影复制会导致要在不同的文件夹的输出文件夹中执行的测试。 对于测试正常工作，卷影复制必须禁用。 [示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)使用 xUnit，同时禁用卷影复制 xUnit 通过包括*xunit.runner.json*具有正确的配置设置文件。 有关详细信息，请参阅[使用 JSON 配置 xUnit.net](https://xunit.github.io/docs/configuring-with-json.html)。

添加*xunit.runner.json*到具有以下内容的测试项目的根目录的文件：

```json
{
  "shadowCopy": false
}
```

## <a name="integration-tests-sample"></a>集成测试示例

[示例应用程序](https://github.com/aspnet/Docs/tree/master/aspnetcore/test/integration-tests/samples)由两个应用程序组成：

| 应用 | 项目文件夹 | 描述 |
| --- | -------------- | ----------- |
| 消息应用程序 (SUT) | *src/RazorPagesProject* | 允许用户添加、 删除其中一个，删除所有，和分析消息。 |
| 测试应用程序 | *tests/RazorPagesProject.Tests* | 用于集成测试 SUT。 |

可以使用一个 IDE 的内置测试功能，如运行测试[Visual Studio](https://www.visualstudio.com/vs/)。 如果使用[Visual Studio Code](https://code.visualstudio.com/)或命令行中，执行以下命令在命令提示符中*tests/RazorPagesProject.Tests*文件夹：

```console
dotnet test
```

### <a name="message-app-sut-organization"></a>消息应用程序 (SUT) 组织

SUT 是 Razor 页消息系统具有以下特征：

* 应用程序的索引页 (*Pages/Index.cshtml*和*Pages/Index.cshtml.cs*) 提供一个用户界面和网页模型方法，用于控制添加、 删除和分析消息 （每个消息的平均词）.
* 一条消息都由描述`Message`类 (*Data/Message.cs*) 具有两个属性： `Id` （密钥） 和`Text`（消息）。 `Text`属性是必需的限制为 200 个字符。
* 消息存储使用[实体框架的内存中数据库](/ef/core/providers/in-memory/)&#8224;。
* 此应用程序包含在其数据库上下文类中，数据访问层 (DAL) `AppDbContext` (*Data/AppDbContext.cs*)。
* 如果数据库为空应用程序启动时，消息存储区初始化与三条消息。
* 应用程序包括`/SecurePage`仅可由已经过身份验证的用户访问。

&#8224;EF 主题，[测试以及 InMemory](/ef/core/miscellaneous/testing/in-memory)，说明如何使用内存中数据库来使用 MSTest 测试。 本主题使用[xUnit](https://xunit.github.io/)测试框架。 测试概念和测试跨不同的测试框架的实现是类似，但不是完全相同。

尽管应用程序不使用[存储库模式](http://martinfowler.com/eaaCatalog/repository.html)并不是有效的示例[工作单元 (UoW) 模式](https://martinfowler.com/eaaCatalog/unitOfWork.html)，Razor 页中支持的开发模式。 有关详细信息，请参阅[设计基础结构持久性层](/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design)，[在 ASP.NET MVC 应用程序中实现的存储库和单元的工作模式](/aspnet/mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application)，和[测试控制器逻辑](/aspnet/core/mvc/controllers/testing)（此示例实现的存储库模式）。

### <a name="test-app-organization"></a>测试应用程序的组织

测试应用程序是在一个控制台应用*tests/RazorPagesProject.Tests*文件夹。

| 测试应用程序文件夹 | 描述 |
| --------------- | ----------- |
| *BasicTests* | *BasicTests.cs*包含路由、 访问未经身份验证的用户，通过安全页面和获取 GitHub 用户配置文件和检查配置文件的用户登录名的测试方法。 |
| *IntegrationTests* | *IndexPageTests.cs*包含使用自定义索引页的集成测试`WebApplicationFactory`类。 |
| *帮助器/实用程序* | <ul><li>*Utilities.cs*包含`InitializeDbForTests`方法用于设定使用测试数据的数据库的种子。</li><li>*HtmlHelpers.cs*一种方法可以返回 AngleSharp`IHtmlDocument`以供测试方法。</li><li>*HttpClientExtensions.cs*提供的重载`SendAsync`将向 SUT 提交请求。</li></ul> |

测试框架为[xUnit](https://xunit.github.io/)。 集成测试使用执行[Microsoft.AspNetCore.TestHost](/dotnet/api/microsoft.aspnetcore.testhost)，其中包括[TestServer](/dotnet/api/microsoft.aspnetcore.testhost.testserver)。 因为[Microsoft.AspNetCore.Mvc.Testing](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Testing)包用来配置测试主机和测试服务器，`TestHost`和`TestServer`包不需要测试应用的项目文件中直接包引用或测试应用程序中的开发人员配置。

**用于测试数据库进行种子设定**

集成测试通常需要在测试执行之前的数据库中的小型数据集。 例如，删除测试数据库记录删除的调用，因此数据库必须具有至少一个记录删除请求才能成功。

示例应用程序设定种子的数据库中的三个消息*Utilities.cs*时它们将执行测试，可以使用：

[!code-csharp[](integration-tests/samples/2.x/IntegrationTestsSample/tests/RazorPagesProject.Tests/Helpers/Utilities.cs?name=snippet1)]

## <a name="additional-resources"></a>其他资源

* [单元测试](/dotnet/articles/core/testing/unit-testing-with-dotnet-test)
* [Razor 页单元测试](xref:test/razor-pages-tests)
* [中间件](xref:fundamentals/middleware/index)
* [测试控制器](xref:mvc/controllers/testing)
