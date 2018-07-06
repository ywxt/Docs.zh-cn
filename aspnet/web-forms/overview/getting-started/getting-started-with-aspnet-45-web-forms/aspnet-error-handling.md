---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 错误处理 |Microsoft Docs
author: Erikre
description: 本教程系列将指导您学习生成有关我们使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 的 ASP.NET Web 窗体应用程序的基础知识...
ms.author: aspnetcontent
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 8d6c19be7c77079b870261d1c4cf0ea62e0e2fd6
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37807585"
---
<a name="aspnet-error-handling"></a>ASP.NET 错误处理
====================
通过[Erik Reitan](https://github.com/Erikre)

[下载 Wingtip Toys 示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 此教程系列将介绍构建 ASP.NET Web 窗体应用程序使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 的基础知识。 Visual Studio 2013[包含 C# 源代码项目](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)可随附于本系列教程。


在本教程中，您将修改 Wingtip Toys 示例应用程序，包括错误处理和错误日志记录。 错误处理将允许应用程序适当地处理错误并相应地显示错误消息。 错误日志记录将允许您查找和修复已发生的错误。 本教程上一教程为基础"URL 路由"，并为 Wingtip Toys 教程系列的一部分。

## <a name="what-youll-learn"></a>你将学习：

- 如何添加全局错误处理的应用程序的配置。
- 如何添加错误处理在应用程序、 页面和代码级别。
- 如何记录供以后查看的错误。
- 如何显示错误消息，不会危及安全性。
- 如何实现错误记录模块和处理程序 (ELMAH) 错误日志记录。

## <a name="overview"></a>概述

ASP.NET 应用程序必须能够处理在一致的方式执行期间发生的错误。 ASP.NET 使用公共语言运行时 (CLR)，它提供一种方法向应用程序错误通知以统一的方式。 出现错误时，将引发异常。 例外情况是任何错误、 条件或应用程序遇到的意外的行为。

在 .NET Framework 中，异常是从 `System.Exception` 类继承的对象。 异常引发自发生问题的代码区域。 异常调用堆栈中向上传递给该应用程序提供代码来处理异常的其中一个位置。 如果应用程序不处理异常，强制浏览器显示的错误详细信息。

最佳做法是，处理中的代码级别中的错误`Try` / `Catch` / `Finally`内你的代码块中。 请尝试将这些块，以便用户可以更正出现的上下文中的问题。 如果错误处理块太远而从发生错误，变得更加困难，为用户提供所需来解决该问题的信息。

### <a name="exception-class"></a>异常类

异常类是异常从中继承的基类。 大多数异常对象是异常类的一些派生类的实例，如`SystemException`类，`IndexOutOfRangeException`类，或`ArgumentNullException`类。 异常类具有属性，如`StackTrace`属性，`InnerException`属性，并`Message`属性，提供有关已发生的错误的特定信息。

### <a name="exception-inheritance-hierarchy"></a>异常继承层次结构

运行时有一组基本的异常派生自`SystemException`时遇到异常，将引发运行时的类。 从异常类，如继承的类的大多数`IndexOutOfRangeException`类和`ArgumentNullException`类中，不实现其他成员。 因此，最重要的异常的信息可在层次结构的异常、 异常名称和异常所含的信息。

### <a name="exception-handling-hierarchy"></a>异常处理层次结构

在 ASP.NET Web 窗体应用程序，可以基于特定处理层次结构处理异常。 可以在以下级别上处理的异常：

- 应用程序级别
- 页级别
- 代码级别

当应用程序处理异常时，可以检索，向用户显示有关异常的异常类中继承的其他信息。 除了应用程序、 页面和代码级别，还可以处理在 HTTP 模块级别和通过使用 IIS 自定义处理程序的异常。

### <a name="application-level-error-handling"></a>应用程序级别错误处理

通过修改应用程序的配置或添加，您可以处理应用程序级别的默认错误`Application_Error`处理程序中的*Global.asax*在应用程序文件。

可以通过添加处理默认错误和 HTTP 错误`customErrors`部分*Web.config*文件。 `customErrors`部分允许您指定将重定向到用户，发生错误时的默认页。 它还允许您指定的特定状态代码错误的各个页面。

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

遗憾的是，当使用配置将用户重定向到其他页面时，您不具有所发生的错误的详细信息。

但是，您可以捕获任意位置出现的错误在应用程序中通过将代码添加到`Application_Error`处理程序中的*Global.asax*文件。

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>页面级别错误事件处理

页面级别处理程序使用户返回到页上出现错误，但由于没有维持控件的实例，将不再有任何内容页上。 若要向应用程序的用户提供错误详细信息，必须专门将写入错误详细信息页。

记录未处理的错误，或若要将用户转到可以显示有用信息的页面，通常会使用页级错误处理程序。

此代码示例演示在 ASP.NET Web 页中的错误事件的处理程序。 此处理程序捕获不能处理中的所有异常`try` / `catch`页中的块。

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

处理错误后，您必须清除它通过调用`ClearError`的服务器对象的方法 (`HttpServerUtility`类)，否则你将看到以前发生了错误。

### <a name="code-level-error-handling"></a>代码级别错误处理

Try-catch 语句由 try 块跟一个或多个 catch 子句，指定不同异常的处理程序。 时引发异常，公共语言运行时 (CLR) 查找处理此异常的 catch 语句。 如果当前正在执行的方法不包含 catch 块，则 CLR 会查看调用当前方法中，依次类推，在调用堆栈上的方法。 如果不找到任何 catch 块，则 CLR 向用户显示一条未处理的异常消息，并停止执行程序。

下面的代码示例演示常见的使用方法`try` / `catch` / `finally`来处理错误。

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

在上述代码中，try 块包含需要避免可能的异常的代码。 直到引发异常或已成功完成块将执行此块。 如果任一`FileNotFoundException`异常或`IOException`发生的异常，将执行转移到另一页。 然后，在包含的代码执行块最后，无论是否出错。

## <a name="adding-error-logging-support"></a>添加错误日志记录支持

添加错误处理 Wingtip Toys 示例应用程序之前, 中，您将添加错误日志记录支持通过添加`ExceptionUtility`类来*逻辑*文件夹。 通过执行此操作，请在每次应用程序处理错误，错误详细信息将添加到错误日志文件。

1. 右键单击*逻辑*文件夹，然后选择**添加** - &gt; **新项**。   
   随即出现“添加新项”对话框。
2. 选择**Visual C#**  - &gt; **代码**在左侧的模板组。 然后，选择**类**从中间列表并将其命名**ExceptionUtility.cs**。
3. 选择“添加”。 显示新类文件中。
4. 将现有代码替换为以下代码：  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

异常发生时，可以通过调用写入到的异常错误日志文件异常`LogException`方法。 此方法采用两个参数、 异常对象和一个包含有关异常的源的详细信息的字符串。 异常错误日志写入到*errorlog.txt 中*中的文件*应用\_数据*文件夹。

### <a name="adding-an-error-page"></a>添加一个错误页面

Wingtip Toys 示例应用程序，在一页将用于显示错误。 错误页用于向站点的用户显示一条安全错误消息。 但是，如果用户是发出 HTTP 请求的计算机上本地提供代码所在的开发人员，其他错误详细信息将显示在错误页。

1. 右键单击项目名称 (**Wingtip Toys**) 中**解决方案资源管理器**，然后选择**添加** - &gt; **新项**.   
   随即出现“添加新项”对话框。
2. 选择**Visual C#**  - &gt; **Web**在左侧的模板组。 从中间列表中选择**包含母版页的 Web 窗体**，并将其命名**ErrorPage.aspx**。
3. 单击 **添加**。
4. 选择*Site.Master*另存为母版页文件，然后选择**确定**。
5. 使用以下内容替换现有标记：   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 隐藏代码的现有代码替换为 (*ErrorPage.aspx.cs*) 以使其显示，如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

当显示错误页时，`Page_Load`执行事件处理程序。 在`Page_Load`处理程序，确定已先处理该错误的位置。 然后，发生的最后一个错误由调用`GetLastError`服务器对象的方法。 如果异常不再存在，则创建一般异常。 然后，如果本地发出 HTTP 请求，会显示所有错误详细信息。 在这种情况下，仅运行 web 应用程序的本地计算机将看到这些错误的详细信息。 已显示的错误信息后，错误将添加到日志文件，并从服务器中清除该错误。

### <a name="displaying-unhandled-error-messages-for-the-application"></a>应用程序显示未处理的错误消息

通过添加`customErrors`部分*Web.config*文件中，可以快速处理整个应用程序发生的简单错误。 此外可以指定如何处理错误基于其状态代码值，例如 404-找不到文件。

#### <a name="update-the-configuration"></a>更新配置

通过添加更新的配置`customErrors`部分*Web.config*文件。

1. 在中**解决方案资源管理器**，找到并打开*Web.config* Wingtip Toys 示例应用程序根目录的文件。
2. 添加`customErrors`部分*Web.config*文件内`<system.web>`节点，如下所示：   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. 保存*Web.config*文件。

`customErrors`部分指定的模式，它被设置为"开启"。 它还指定`defaultRedirect`，它将告诉哪一页时出错时要导航到应用程序。 此外，您添加了一个特定的错误元素，指定如何处理 404 错误，找不到页面时。 稍后在本教程中，你将添加额外的错误处理，将捕获的应用程序级别的错误详细信息。

#### <a name="running-the-application"></a>运行应用程序

可以运行应用程序现在以查看更新的路由。

1. 按**F5**运行 Wingtip Toys 示例应用程序。  
 在浏览器将打开并显示*Default.aspx*页。
2. 以下 URL 输入到浏览器 (请务必使用**你**端口号):  
    `https://localhost:44300/NoPage.aspx`
3. 审阅*ErrorPage.aspx*浏览器中显示。 

    ![ASP.NET 错误处理-找不到页面错误](aspnet-error-handling/_static/image1.png)

当请求*NoPage.aspx*页上，不存在，则错误页将显示简单的错误消息和详细的错误信息如果提供了更多详细信息。 但是，如果用户请求从远程位置不存在页，则错误页将只会以红色显示错误消息。

### <a name="including-an-exception-for-testing-purposes"></a>出于测试目的包括异常

若要验证你的应用程序的运行时出现错误的方式发生，在 ASP.NET 中特意创建错误条件。 在 Wingtip Toys 示例应用程序，将加载默认页面以查看会发生什么情况时引发测试异常。

1. 打开的代码隐藏*Default.aspx* Visual Studio 中的页。   
   *Default.aspx.cs* ，将显示代码隐藏页。
2. 在`Page_Load`处理程序中，添加代码，以便该处理程序出现，如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

就可以创建各种不同类型的异常。 在上述代码中，将创建`InvalidOperationException`时*Default.aspx*加载页面。

#### <a name="running-the-application"></a>运行应用程序

可以运行应用程序以查看应用程序如何处理异常。

1. 按**CTRL + F5**运行 Wingtip Toys 示例应用程序。  
 应用程序将引发 InvalidOperationException。 

    > [!NOTE] 
    > 
    > 必须按下**CTRL + F5**而不会中断到代码以在 Visual Studio 中查看该错误的源中显示的页。
2. 审阅*ErrorPage.aspx*浏览器中显示。 

    ![ASP.NET 错误处理的错误页](aspnet-error-handling/_static/image2.png)

正如您所看到错误详细信息中，已捕获异常`customError`主题中*Web.config*文件。

### <a name="adding-application-level-error-handling"></a>添加应用程序级别的错误处理

而不是异常使用陷阱`customErrors`主题中*Web.config*文件中，获得有关异常的一些信息，其中您可以捕获应用程序级别的错误并检索错误详细信息。

1. 在中**解决方案资源管理器**，找到并打开*Global.asax.cs*文件。
2. 添加**应用程序\_错误**处理程序，使其显示，如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

在应用程序中发生错误时`Application_Error`调用处理程序。 此处理程序中的最后一个异常检索并查看。 如果异常为未处理，并且该异常包含内部异常详细信息 (即，`InnerException`不为 null)，该应用程序来将执行转移到错误页并显示异常详细信息的位置。

#### <a name="running-the-application"></a>运行应用程序

可以运行应用程序以查看通过处理应用程序级别的异常提供的其他错误详细信息。

1. 按**CTRL + F5**运行 Wingtip Toys 示例应用程序。  
 应用程序将引发`InvalidOperationException`。
2. 审阅*ErrorPage.aspx*浏览器中显示。 

    ![ASP.NET 错误处理的应用程序级别错误](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>添加页面级别的错误处理

您可以添加页面级别的错误处理到一个页面是通过添加`ErrorPage`归于`@Page`指令的页上，或通过添加`Page_Error`到页面的代码隐藏的事件处理程序。 在本部分中，您将添加`Page_Error`事件处理程序会将传输到执行*ErrorPage.aspx*页。

1. 在中**解决方案资源管理器**，找到并打开*Default.aspx.cs*文件。
2. 添加`Page_Error`处理程序，以便代码隐藏显示为遵循：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

在页上，发生错误时`Page_Error`调用事件处理程序。 此处理程序中的最后一个异常检索并查看。 如果`InvalidOperationException`发生，`Page_Error`事件处理程序来将执行转移到错误页并显示异常详细信息的位置。

#### <a name="running-the-application"></a>运行应用程序

可以运行应用程序现在以查看更新的路由。

1. 按**CTRL + F5**运行 Wingtip Toys 示例应用程序。  
 应用程序将引发`InvalidOperationException`。
2. 审阅*ErrorPage.aspx*浏览器中显示。 

    ![ASP.NET 错误处理的页级别的错误](aspnet-error-handling/_static/image4.png)
3. 关闭浏览器窗口中。

### <a name="removing-the-exception-used-for-testing"></a>删除用于测试的异常

若要允许 Wingtip Toys 示例应用程序，而不引发的异常在本教程前面部分添加函数，请删除该异常。

1. 打开的代码隐藏*Default.aspx*页。
2. 在`Page_Load`处理程序中，删除引发异常，以便该处理程序出现，如下所示的代码：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>添加代码级别的错误日志记录

在本教程前面所述，可以添加 try/catch 语句，尝试运行一段代码并处理第一个出现的错误。 在此示例中，将仅写入错误详细信息的错误日志文件，以便可以稍后查看错误。

1. 在中**解决方案资源管理器**，在*逻辑*文件夹中，找到并打开*PayPalFunctions.cs*文件。
2. 更新`HttpCall`方法以便，代码显示为如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

上面的代码调用`LogException`方法中包含的`ExceptionUtility`类。 您添加*ExceptionUtility.cs*类的文件*逻辑*此前在本教程中的文件夹。 `LogException` 方法采用两个参数。 第一个参数是异常对象。 第二个参数是一个字符串，用来识别错误的源。

### <a name="inspecting-the-error-logging-information"></a>检查错误日志记录信息

正如前面提到的可以使用错误日志以确定应首先修复应用程序中的错误。 当然，将记录已捕获和写入错误日志的错误。

1. 在中**解决方案资源管理器**，找到并打开*errorlog.txt 中*文件中*应用\_数据*文件夹。   
 可能需要选择"**显示所有文件**"选项或"**刷新**"顶部的选项**解决方案资源管理器**以查看*errorlog.txt 中*文件。
2. 查看 Visual Studio 中显示的错误日志： 

    ![ASP.NET 错误处理-errorlog.txt 中](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>安全的错误消息

它是**值得注意**，当你的应用程序显示错误消息时，它不应该泄露恶意用户可能会有所攻击你的应用程序中的信息。 例如，如果你的应用程序未成功尝试写入数据库，它不应显示错误消息，包括它所使用的用户名。 出于此原因，以红色的一般性错误消息显示给用户。 向开发人员在本地计算机上仅显示所有其他错误详细信息。

## <a name="using-elmah"></a>使用 ELMAH

ELMAH （错误日志记录模块和处理程序） 是插入到作为 NuGet 包的 ASP.NET 应用程序错误日志记录功能。 ELMAH 提供以下功能：

- 未经处理的异常日志记录功能。
- 若要查看整个日志记录未处理异常的网页。
- 若要查看的每个完整的详细信息的网页记录异常。
- 它发生的时间在每个错误的电子邮件通知。
- 从日志的最后 15 个错误的 RSS 源。

可以在使用 ELMAH 之前，必须安装它。 这很容易使用*NuGet*程序包安装程序。 如本系列教程前面所述，NuGet 将是 Visual Studio 扩展，它可以更轻松地安装和更新的开放源代码库和 Visual Studio 中的工具。

1. Visual Studio 中，从**工具**菜单中，选择**库程序包管理器** - &gt; **为解决方案管理 NuGet 包**。 

    ![ASP.NET 错误处理的管理解决方案的 NuGet 包](aspnet-error-handling/_static/image6.png)
2. **管理 NuGet 包**Visual Studio 中将显示对话框。
3. 在中**管理 NuGet 包**对话框框中，展开**联机**在左侧，然后选择**nuget.org**。然后，找到并安装**ELMAH**包从联机可用包列表。 

    ![ASP.NET 错误处理-ELMA NuGet 包](aspnet-error-handling/_static/image7.png)
4. 需要具有 internet 连接才能下载包。
5. 在中**选择项目**对话框框中，请确保**WingtipToys**选择已选中，然后单击**确定**。 

    ![ASP.NET 错误处理的选择项目对话框](aspnet-error-handling/_static/image8.png)
6. 单击**关闭**中**管理 NuGet 包**必要的对话框。
7. 如果 Visual Studio 请求重新加载任何打开的文件，选择"**全是**"。
8. ELMAH 包本身中添加条目*Web.config*根目录下的项目文件。 如果 Visual Studio 会要求你如果你想要重新加载修改后*Web.config*文件中，单击**是**。

ELMAH 现已准备好存储出现的任何未处理的错误。

### <a name="viewing-the-elmah-log"></a>查看 ELMAH 日志

查看 ELMAH 日志非常容易，但首先您将创建将在 ELMAH 日志中记录的未处理的异常。

1. 按**CTRL + F5**运行 Wingtip Toys 示例应用程序。
2. 若要写入的 ELMAH 日志未处理的异常，请导航到以下 URL （使用端口号） 在浏览器中：  
    `https://localhost:44300/NoPage.aspx` 将显示错误页。
3. 若要显示的 ELMAH 日志，请导航到以下 URL （使用端口号） 在浏览器中：  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 错误处理-ELMAH 错误日志](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>总结

在本教程中，你已了解如何在应用程序级别、 页面级别中，而代码级别的错误处理。 您还学习了如何记录处理和未经处理的错误，供以后查看。 您添加了 ELMAH 实用工具提供异常日志记录和使用 NuGet 的应用程序的通知。 此外，你已了解如何安全错误消息的重要性。

## <a name="tutorial-series-conclusion"></a>系列教程结束

*感谢您的随笔。我希望本系列教程帮助您成为更熟悉 ASP.NET Web 窗体。如果你需要有关在 ASP.NET 4.5 和 Visual Studio 2013 中可用的 Web 窗体功能的详细信息，请参阅* [*ASP.NET 和 Web Tools for Visual Studio 2013 发行说明*](../../../../visual-studio/overview/2013/release-notes.md)*.此外，一定要看一看本教程中所述* ***后续步骤****部分和 defintely 试用* [*免费 Azure 试用版*](https://azure.microsoft.com/pricing/free-trial/)*.*

![谢谢-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>后续步骤

了解有关部署到 Microsoft Azure web 应用程序的详细信息，请参阅[将包含成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET Web 窗体应用部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)。

## <a name="free-trial"></a>免费试用版

[Microsoft Azure-免费试用版](https://azure.microsoft.com/pricing/free-trial/)  
 你的网站发布到 Microsoft Azure 将节省时间、 维护和支出。 它是一个到 web 应用部署到 Azure 的快速过程。 当你需要进行维护和监视你的 web 应用时，Azure 提供了各种各样的工具和服务。 管理数据、 通讯、 标识、 备份、 消息传递、 媒体和在 Azure 中的性能。 和所有这些都非常经济高效的方法中提供。

## <a name="additional-resources"></a>其他资源

[ASP.NET 运行状况监视的日志记录错误详细信息](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>致谢

我想要感谢下列人员进行本系列教程的内容的重要贡献的人：

- [Alberto Poblacion、 MVP &amp; MCT、 西班牙](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen，荷兰](http://blog.alexthissen.nl/)(twitter: [ @alexthissen ](http://twitter.com/alexthissen))
- [Andre Tournier，USA](http://andret503.wordpress.com/)
- Apurva Joshi Microsoft
- [Bojan Vrhovnik，斯洛文尼亚](http://twitter.com/bvrhovnik)
- [Bruno Sonnino，巴西](http://msmvps.com/blogs/bsonnino)(twitter: [ @bsonnino ](http://twitter.com/bsonnino))
- [Carlos dos Santos 巴西](http://www.carloscds.net/)
- [Dave Campbell，USA](http://www.wynapse.com/) (twitter: [ @windowsdevnews ](http://twitter.com/windowsdevnews))
- [Jon Galloway、 Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [ @jongalloway ](http://twitter.com/jongalloway))
- [Michael 音号，USA](http://www.930solutions.com/) (twitter: [ @mrsharps ](http://twitter.com/mrsharps))
- Mike 教皇
- [Mitchel 卖家，USA](http://www.mitchelsellers.com/) (twitter: [ @MitchelSellers ](http://twitter.com/MitchelSellers))
- [Paul Cociuba Microsoft](http://linqto.me/Links/pcociuba)
- [Paulo Morgado 葡萄牙](http://paulomorgado.net/)
- [Pranav rastogi 撰写 Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom Dykstra Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>社区贡献

- Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))  
  Visual Studio 2012 相关 MSDN 上的代码示例：[导航 Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
  Visual Studio 2012 相关 MSDN 上的代码示例：[在 Visual Basic 中的 ASP.NET 4.5 Web 窗体教程系列](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft 技术受众参与者 (twitter: @driazevedo)  
  Visual Studio 2012 翻译： [Iniciando com Visão Geral 的 ASP.NET Web 窗体 4.5-Parte 1-Introdução e](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [上一篇](url-routing.md)
