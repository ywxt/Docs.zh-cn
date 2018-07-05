---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: 在 Visual Studio 2005 中的改进 |Microsoft Docs
author: microsoft
description: Visual Studio 2005 提供了众多改进和增强功能的 Web 项目的 Web 应用程序开发人员。
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 35ebb6e94c3da105b802c843e36f193f81a45782
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397634"
---
<a name="improvements-in-visual-studio-2005"></a>在 Visual Studio 2005 中的改进
====================
by [Microsoft](https://github.com/microsoft)

> Visual Studio 2005 提供了众多改进和增强功能的 Web 项目的 Web 应用程序开发人员。


Visual Studio 2005 提供了众多改进和增强功能的 Web 项目的 Web 应用程序开发人员。 具有强大的功能 Visual Studio.NET 2002年和 2003年是，许多投诉中包括的 Web 项目已处理的方式。 Visual Studio 2005 为了解决这些抱怨添加大量新功能。 有关这些适用于喜欢 Visual Studio.NET 2003年处理的 Web 应用程序编译的方式，请参阅[Web 应用程序项目](https://go.microsoft.com/fwlink/?LinkId=57870)。

在此模块中，我们将介绍 Web 项目创建、 管理和开发中的改进。 在更高版本的模块中，我们将介绍生成 Web 项目并将其部署中的改进。

## <a name="frontpage-server-extensions"></a>FrontPage 服务器扩展

Visual Studio.NET 2002年和 2003年所需的框才能创建或构建 Web 项目的 FrontPage 服务器扩展。 开发人员有两种不同的访问模式 （FrontPage 服务器扩展或文件访问模式） 之间进行选择，同时使用 FrontPage 服务器扩展来执行任务，例如在 IIS 等设置的应用程序根目录。

Visual Studio 2005 中删除而言，对于本地项目依赖于 FrontPage 服务器扩展。 Visual Studio 2005 现在访问 IIS 元数据库直接而不是使用 FrontPage 服务器扩展。 Visual Studio 2005 还添加了对 FTP 允许进行远程项目访问而无需 FrontPage 服务器扩展支持。

对于这些开发人员想要在其项目中使用 FrontPage 服务器扩展，选项为仍然可用。 但是，根据从 ASP.NET 开发人员社区强有力的反馈，它不是一项要求。

> [!NOTE]
> 仍需要远程项目创建、 打开等 FrontPage 服务器扩展。


## <a name="aspnet-development-server"></a>ASP.NET Development Server

Visual Studio 2005 中附带了名为 ASP.NET 开发服务器的新 Web 服务器。 （此 Web 服务器是以前称为 Cassini。）

有几个优点的 ASP.NET 开发服务器。

- 就现在可以为非管理员开发和调试针对 Web 服务器。
- ASP.NET Development Server 会动态将映射的虚拟目录的任何位置允许灵活的项目位置的文件系统中。
- 已在使用 IIS 在 Windows XP Professional 用户现在可以创建不会影响文件或文件夹结构的其默认网站在 IIS 中的新 Web 应用程序。

充分利用 ASP.NET Development Server 不需要任何特殊配置。 当文件系统托管的 Web 项目是调试或浏览时，Visual Studio 2005 上随机端口，以请求提供服务将自动启动 ASP.NET Development Server 的实例。

将此模块中的更高版本的 ASP.NET 开发服务器上介绍的详细信息。

## <a name="improved-file-management"></a>改进了的文件管理

在 Visual Studio 2002 和 2003年中，项目文件 (.vbproj 对于 VB.NET) 和 C# 的 Web 应用程序中的所有文件存储信息。 解决方案资源管理器显示基于项目文件中的文件信息。 正因为如此，在解决方案资源管理器通常会在其中使用了外部编辑器的情况下显示不准确的信息。 Visual Studio 2002 和 2003年将通常覆盖文件的更改或不显示文件的最新版本。

Visual Studio 2005 会使用项目文件。 相反，它会直接从该磁盘，从而导致你的项目中的文件的准确显示读取的文件和文件夹信息。 在 Visual Studio 2002 和 2003年中的引用文件夹不表示在 Web 应用程序中的实际文件夹，因为 Visual Studio 2005 还会从解决方案资源管理器中删除引用文件夹。 若要访问 Visual Studio 2005 中的项目的引用，您应使用项目属性页。

## <a name="creating-web-projects"></a>创建 Web 项目

Web 开发人员在 Visual Studio 2005 中有许多新的选项可用于创建项目。 网站文件系统中现在在任何位置创建，然后可以进行调试或浏览使用新的 ASP.NET 开发服务器。 开发人员还可以创建新网站使用 FTP。

若要查看在 Visual Studio 2005 中创建 Web 项目的视频演练，请单击此处。


![](improvements-in-visual-studio-2005/_static/image1.png)


[打开的全屏视频](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)


### <a name="file-system-projects"></a>文件系统项目

正如您看到视频演练中，您可以选择在本地计算机上或远程位置通过文件共享上的文件系统上创建网站。 在文件系统创建的网站的浏览和调试使用 ASP.NET 开发服务器。

> [!NOTE]
> ASP.NET 开发服务器可能会导致一些混淆的客户。 如果 IISs 目录结构 (即 c: / inetpub/wwwroot) 中的文件系统上创建 Web 项目，则将仍可通过从 Visual Studio 2005 中启动的 ASP.NET 开发服务器浏览 Web 站点。 因此，任何 IIS 配置 （即身份验证方法） 不适用。


大量还会删除默认的 web 项目的开销通过仅包含 Default.aspx 页面、 default.cs 文件和应用/数据 （_d） 文件夹。 根据他们需要添加 web.config 和特殊文件夹 (即应用/_code)。 你的 web 项目仅包括的文件和所需的文件夹。

### <a name="http-projects"></a>HTTP 项目

HTTP 项目可以是本地 IIS Web 站点上或远程网站上创建的项目。 默认项目位置是`http://localhost`。 如果单击浏览按钮时，有两个 HTTP 选项： 本地 IIS 和远程站点。 在这两个选项中的主要区别是其 web 站点的信息显示在选择位置对话框和如何将文件复制到 Web 服务器的方法。

本地 IIS 选项从本地计算机上配置数据库读取站点信息和使用文件系统复制文件。 远程站点选项使用 FrontPage 服务器扩展和站点信息和文件将复制使用 HTTP，FrontPage 服务器扩展 RPC 调用。

> [!NOTE]
> Vs###/_tmp.htm 文件和 get/_aspx/_ver.aspx 不再用于确定版本信息。


默认 HTTP 选项是本地 IIS。 此选项读取 IIS 元数据库，若要确定哪些站点可用，并在其中创建内容的位置。 在树视图中选择它，可以选择不同的文件夹或虚拟目录。 您可以还创建一个新的虚拟目录、 将标记为应用程序的文件夹，以及从该对话框中删除现有的虚拟目录。


![选择位置对话框](improvements-in-visual-studio-2005/_static/image1.gif)

**图 1**: 选择位置对话框


不同于在早期版本的 Visual Studio 中，如果您检查**使用安全套接字层**复选框和 SSL 证书与您正浏览的 URL 不匹配，则将显示一个安全警报对话框，询问您是否像要继续操作。 使用 Visual Studio.NET 2003 中，如果证书不是一匹配，将无法创建项目。


![安全警报的有关 SSL 证书](improvements-in-visual-studio-2005/_static/image2.gif)

**图 2**： 有关 SSL 证书的安全警报


### <a name="note-on-host-headers"></a>请注意，在主机标头

如果要绑定到特定的 IP 在站点上创建 Web 应用程序，您需要确保配置了主机标头。 否则，Visual Studio 将创建以下站点`http://localhost`，但浏览或 IDE 中调试从该站点时，不会正确解析 IP 地址。

如果选择远程站点选项，该对话框更改为允许你输入新的 Web 站点的目标 URL。 此 URL 必须已启用 FrontPage 服务器扩展的服务器上。 如果你想要使用本地 Web 服务器使用 FrontPage 服务器扩展，可以使用远程站点选项并指定本地 URL。


![在远程服务器上创建网站](improvements-in-visual-studio-2005/_static/image1.jpg)

**图 3**： 远程服务器上创建网站


通过 SSL，远程站点上创建应用程序，如果 SSL 证书不匹配，确认对话框时，对话框中显示时使用本地 IIS 选项略有不同。


![远程站点安全警报](improvements-in-visual-studio-2005/_static/image3.gif)

**图 4**： 远程站点安全警报


<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005 引入了用于创建通过 FTP 的网站的选项。 时使用此选项，IDE 的用户临时文件夹中本地创建文件，并使用 FTP 将文件移到的 FTP 位置。

> [!NOTE]
> 临时文件夹位置是 c: / 文档和设置 /&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/_&lt;应用程序名称&gt;


使用 FTP 选项时，您将看到一个对话框，选择位置。 在此对话框，如下所示输入所需的 FTP 连接信息。


![选择 ftp 位置对话框](improvements-in-visual-studio-2005/_static/image2.jpg)

**图 5**: 选择的 FTP 位置对话框


## <a name="lab-setup-ftp-site-and-create-a-project"></a>实验室： 设置 FTP 站点并创建一个项目

以下步骤配置的 FTP 站点，使用户具有只有他们可以通过 FTP 上载到的位置。

### <a name="install-the-ftp-service"></a>安装 FTP 服务

1. 打开添加或删除程序，选择添加/删除 Windows 组件
2. 选择 Internet 信息服务 （在 Windows 2003 上的应用程序服务器），然后单击**详细信息**。
3. 检查**文件传输协议 (FTP) 服务**然后单击**确定**。
4. 单击**下一步**安装 FTP 服务。

### <a name="create-a-new-folder-for-content"></a>为内容创建新文件夹

1. 在 Windows 资源管理器，创建一个名为的新文件夹**User1** c: / inetpub/wwwroot 内。

#### <a name="configure-folders-and-permissions-on-folders"></a>在文件夹上配置文件夹和权限。

1. 从管理工具中打开 Internet Information Services 管理单元中。 现在将计算机名称节点下的 FTP 站点文件夹。
2. 展开**FTP 站点**。
3. 右键单击**默认 FTP 站点**，选择**新建**，然后**虚拟目录**，然后单击**下一步**。
4. 输入**User1**为虚拟目录名称，然后单击**下一步**。
5. 输入**c: / inetpub/wwwroot/User1**作为路径，然后单击**下一步**。
6. 单击**下一步**，然后**完成**以完成向导。
7. 右键单击**User1**在默认的 FTP 站点，然后选择下的虚拟目录**属性**。
8. 检查**编写**复选框，单击**确定**关闭对话框。
9. 右键单击**默认 FTP 站点**，然后选择**属性**。
10. 上**安全帐户**选项卡上，取消选中**允许匿名连接**。
11. 单击**是**中对话框，询问是否要继续。
12. 单击**确定**关闭对话框。
13. 展开**Default Web Site**下**网站**节点。
14. 右键单击**User1**目录，然后选择**属性**
15. 在中**应用程序设置**部分中，单击**创建**将标记为应用程序的文件夹。
16. 单击**确定**关闭对话框。
17. 关闭 Internet Information Services 管理单元中。

### <a name="create-web-project"></a>创建 web 项目

1. 打开 Visual Studio 2005。
2. 从**文件**菜单中，选择**新的 Web 站点**。
3. 在中**位置**下拉列表中，选择**FTP**。
4. 单击“浏览” 。
5. 输入**localhost**中**Server**文本框中。
6. 输入**User1**目录文本框中。
7. 单击**打开**。 FTP 位置将输入到新建网站对话框中。
8. 单击 **“确定”**。
9. 取消选中**匿名登录**中的 FTP 登录对话框中，输入你的凭据，然后单击**确定**。
10. 项目 URL 是什么？ （该项目的 URL 将显示在解决方案资源管理器。）
11. 从**构建**菜单中，选择**生成网站**或**生成解决方案**。
12. 在 Default.aspx 在解决方案资源管理器中右键单击并选择**在浏览器中的查看**。
13. 在要求提供网站 URL 对话框中，输入`http://localhost/user1`为 URL，然后单击**确定**。

> [!NOTE]
> 如果你收到错误，表示无法加载类型 /_Default，请确保你的网站并不是早期版本上运行 ASP.NET 2.0。 您可以从在 Internet 信息服务中的 ASP.NET 选项卡来实现。


## <a name="opening-web-projects"></a>打开 Web 项目

打开 Web 项目是类似于创建项目。 调用区域，以保持关注的 IDE 内工作时以下各节。 它还介绍如何使用 HTTP 和 FTP 的 Web 项目使用。

若要打开 Web 项目，请从文件菜单中选择打开网站。 将会覆盖以前相同的选择位置对话框有提示，并且具有相同的四个选项可供你： 文件系统、 本地 IIS、 FTP 和远程站点。

<a id="_Toc116100245"></a>

## <a name="file-system"></a>文件系统

如之前在此模块中所示，Visual Studio 将无法再使用项目文件。 因此，如果您选择从文件系统打开网站，您实际上可以选择你想，任何文件夹，即使您选择的文件夹不作为最初在 Visual Studio 中的 Web 项目创建。 例如，可以选择要打开我的文档文件夹作为网站和 Visual Studio 将值得庆幸的是将其打开并显示你的文件，如下所示。


![我作为网站打开的文档](improvements-in-visual-studio-2005/_static/image3.jpg)

**图 6**:*我的文档*作为网站打开


由于 Visual Studio 仅创建其他文件和文件夹在必要时，任何其他文件或文件夹添加到打开的位置。 此体系结构的副作用是，它会阻止您嵌套在文件系统上的网站。 例如，考虑以下目录结构。

C: / mywebsite web 项目

C: / MyWebSite/嵌套在另一个 web 项目

当打开 c: / mywebsite Web 站点时，嵌套文件夹将显示为该应用程序的子文件夹。

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

从 IIS 元数据库 (本地 IIS) 或使用 FrontPage 服务器扩展 （远程站点。） 时打开通过 HTTP 的网站，读取设置如果有嵌套的 web 应用程序，这些还显示与标识为应用程序的图标。 如果你熟悉使用 FrontPage web 应用程序，Visual Studio 2005 中的行为将类似。

即使 Visual Studio 将显示嵌套在 IDE 中当前打开的应用程序下面的应用程序的图标，它将允许您以展开其查看其内容。 但是，可以双击它们来打开它们。 执行操作时，您会看到一个对话框，提示您需要打开 web 应用程序 （并替换当前打开的解决方案），或添加到当前解决方案的 Web 应用程序。


![双击一个嵌套的应用程序图标将显示此对话框](improvements-in-visual-studio-2005/_static/image4.jpg)

**图 7**： 双击嵌套的应用程序图标将显示此对话框


<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 站点

当您打开通过 FTP 站点时，文件所有本地复制到临时文件夹。 在本地存储位置的完整路径为项目属性窗格中显示，并使用以下格式进行创建。

C: / 文档和设置 /&lt;用户&gt;/本地设置/Temp/VWDWebCache/&lt;服务器&gt;/_&lt;应用程序名称&gt;

使用 FTP 时，Visual Studio 将需要指定你的项目的基 URL，以便您可以浏览它，如下所示。 如果不指定基 URL，Visual Studio 会要求您为其第一次尝试浏览 Web 站点中的页。


![指定的 FTP 站点的基 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

**图 8**： 指定的 FTP 站点的基 URL


## <a name="improvements-in-compilation"></a>在编译中的改进

使用 Visual Studio 2005 中的 Web 应用程序速度明显比以前版本更快。 这是由于在没有小部分编译体系结构中的更改。

在 Visual Studio 2002 和 2003年中，Web 应用程序已编译到驻留在 /bin 文件夹中的一个主要程序集。 在 Visual Studio 2005 中，添加了一个应用程序/_Code 文件夹。 类和其他非 UI 代码添加到应用程序/_Code 文件夹中。 Visual Studio 生成项目以后，应用/_Code 文件夹中的所有文件都编译到单个 App/_Code.dll 文件。 此更改的结果是，后续生成速度比在早期版本中。

> [!NOTE]
> MSBuild 命令行实用程序还可以用于生成 ASP.NET Web 应用程序。 该工具将模块 9 中所覆盖。


另一个编译增强功能是生成菜单上的新生成页选项。 此功能允许开发人员可以重新生成仅在当前页 （连同、 课程和依赖项），这样可以更快地编译更改。 C# 不提供用于更新 IntelliSense 等的后台编译，因为它们将极大地从此功能受益因为这可以使 intellisense 只需重新生成单个页面快速更新。

项目生成的属性，可配置的启动页面执行之前发生的生成的类型。 开发人员可以选择仅生成当前页，以便 Visual Studio 可以开始在代码更改后更快地调试应用程序。


![生成页开始操作](improvements-in-visual-studio-2005/_static/image6.jpg)

**图 9**： 生成页开始操作


Visual Studio 和 ASP.NET 体系结构到另一个很好的增强功能是在区域中的编辑并继续。 在 Visual Studio 2005 中，开发人员可以开始调试项目和项目进行代码更改，而分离调试器。 事实上，您可以按原义开始调试项目、 添加新类，将代码添加到该类、 将代码添加到您创建该类的新实例的页面和执行方法的类，所有操作都无分离调试器。 执行新的代码是作为刷新浏览器按字面意思一样简单 ！

单击此处可查看视频演练的编辑并继续在 Visual Studio 2005 中的功能。


![](improvements-in-visual-studio-2005/_static/image2.png)


[打开的全屏视频](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)


稳定可靠的编辑并继续在 ASP.NET 2.0 中的功能和 Visual Studio 2005 是由于对于 ASP.NET 应用程序的体系结构更改。 在 ASP.NET 1.x 中，创建 Visual Studio 2002/2003 中的应用程序已编译到 /bin 文件夹中存储的主要程序集。 所有类，页面，等的应用程序已编译到一个 DLL。 然后在运行时，ASP.NET 会将所有控件、 标记和 ASP.NET 页内的代码编译并将这些 Dll 复制到 ASP.NET 临时文件夹。

在 Visual Studio 2005 中使用 ASP.NET 2.0 中，这两个编译模型概述上面 （一个用于 Visual Studio），另一个用于 ASP.NET 在运行时已合并为一个通用的编译模型。 这意味着所有编译问题现在都捕获，以便在开发阶段，而不是在运行时。 它还允许为设计器和对用户控件和母版页等功能的 IntelliSense 支持。

若要查看对用户控件的设计器支持的视频演练，请单击此处。


![](improvements-in-visual-studio-2005/_static/image3.png)


[打开的全屏视频](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)


> [!NOTE]
> 从页上，删除的用户控件时@Register指令保持在标记中，应手动删除以避免分析器错误，如果从 Web 站点中删除的用户控件。


Visual Studio 编译模型中的另一个改进是发布网站功能。 发布功能预编译 Web 站点，因为开发人员可以享受无需编译任何内容按需添加了的的性能。 它还预编译应用程序/_Code 文件夹中的所有源代码到 DLL，以便没有源代码必须进行部署。


![发布网站对话框](improvements-in-visual-studio-2005/_static/image7.jpg)

**图 10**: 发布网站对话框


> [!NOTE]
> Aspnet/_compile.exe 实用工具还可以用于预编译的 ASP.NET Web 应用程序。 该工具将模块 9 中所覆盖。


当您发布网站，预编译的文件存储在 Temporary ASP.NET Files 文件夹，如下所示。 文件的工具 *.compiled*文件扩展名是定义特定 Dll 的依赖项的 XML 文件。 任何 web 窗体或用户控件被编译为开头的随机 Dll*应用程序 /_Web /_*。

如果将保留*允许可更新此预编译的站点*选中复选框，Webforms 和用户控件内的标记不会预编译到 DLL 允许您在部署后进行更改。 如果您希望锁定标记，以便不允许对部署的内容的更改，请取消选中此框。

*使用固定命名和单页程序集*复选框，可禁用批处理编译，以便每个页面编译到程序集具有固定名称。 保留此框未选中状态，可充分利用批处理编译。

*启用强命名在预编译程序集*复选框可以强名称为您预编译的程序集。

> [!NOTE]
> 在 ASP.NET 1.x 中，强名称程序集必须安装到全局程序集缓存 (GAC) 中。 在 ASP.NET 2.0 中，您都不需要强名称的程序集安装到 gac。


![ASP.NET 应用程序预编译的文件](improvements-in-visual-studio-2005/_static/image8.jpg)

**图 11**: ASP.NET 应用程序预编译的文件


> [!NOTE]
> 在上述应用程序，没有 web.config 文件。 如果已经存在，它会调用了*PrecompiledApp.config*后发布 Web 站点过程。


## <a name="improvements-in-deployment"></a>部署中的改进

作为使用 Visual Studio 2002 和 2003 年，Visual Studio 2005 提供复制项目功能。 但是，此功能已得到增强 Visual Studio 2005 中，现在称为复制网站。

复制网站对话框中拆分为左的框架和右侧的框架。 左的框架中称为源网站上，正确的帧被称为远程网站。 可能会混淆一些开发人员的一件事是，在右侧的框架中显示的站点不一定是远程站点。 它可能是本地文件系统上或 IIS 的本地实例上的站点。 此外，在左框架中显示的站点不一定在源网站由于，对话框允许您从远程网站上发布*到*源网站。

如果要将复制到远程网站上的一个项目，该站点必须具有在其上安装的 FrontPage 服务器扩展。 如果未显示，您将需要使用 FTP 进行连接。 但是，如果要将复制到本地 IIS 实例的一个项目，则不需要 FrontPage 服务器扩展。

> [!NOTE]
> 如果尝试在本地 IIS 实例上创建新的 Web 站点和安装 FrontPage 2002 Server Extensions，你将获取错误消息，告诉你创建网站的 SharePoint 服务器上不支持的。 在这种情况下，您可以选择安装 FrontPage 2000 服务器扩展或删除 FrontPage 服务器扩展。


复制网站功能的视频演练，请单击此处。


![](improvements-in-visual-studio-2005/_static/image4.png)


[打开的全屏视频](improvements-in-visual-studio-2005/_static/copysite1.wmv)


## <a name="improvements-in-debugging"></a>在调试改进

有四个主要的改进，在 Visual Studio 2005 中调试。

- 以非管理员身份在本地调试有可能在初始状态。
- Compilation 元素的调试属性现在是默认值为 false。
- 远程调试安装和配置是比之前更容易。
- 现在可以调试通过 FTP 位置打开的网站。

## <a name="debugging-as-a-non-administrator"></a>以非管理员身份调试

新增的 ASP.NET 开发服务器使非管理员可以轻松地调试 ASP.NET 应用程序即时可用的。 如果调试在本地文件系统上运行的 ASP.NET 应用程序，Visual Studio 将启动 ASP.NET 开发服务器的登录的用户上下文。 然后，该用户可以调试该应用程序无需其他配置。

## <a name="debug-is-false-by-default"></a>调试是 False 默认情况下

在 ASP.NET 1.x 中，*调试*属性中*编译*web.config 文件的元素设置为*true*默认情况下。 它始终已建议开发人员将此属性设置为*false*之前应用程序部署到生产环境中，而是因为大多数开发人员没有完全理解保留调试属性设置为的后果为 true，它们只需从左作为它的是。

最严重的问题与调试属性设置为 true 是，它会禁用 ASP.NETs 批处理编译模式。 因此，每个页面编译到单独的 DLL。 如果 Web 应用程序包含数千个页面 （不前所未有的方式），这意味着该应用程序将创建若干个几千个小 Dll。 虽然这些 Dll 较小的它们不是加载到内存中的任何特定位置。 因此，它们碎片导致系统内存，可能会导致 OutOfMemoryException 匹配项。

在 ASP.NET 2.0 中，默认情况下调试属性设置为 false。 如您已经看到，当开发人员调试 ASP.NET 应用程序在 Visual Studio 2005 中，会提示他们来添加启用了调试的 web.config 文件。 这样做会导致在 ASP.NET 中存在的相同缺点 1.x 中，但现在，开发人员会清楚地收到警告，该属性应重置为 false 之前移动到生产环境的应用程序。

## <a name="remote-debugging-setup-and-configuration"></a>远程调试安装和配置

在 Visual Studio 2002/2003，远程调试依赖计算机调试管理器 (mdm.exe) 和 vs7jit.exe 过程。 正因为如此，远程调试的问题进行故障排除通常客户一个黑色框，它通常不是获得更好的 PSS。

Visual Studio 2005 中删除，依赖于 mdm.exe 和 vs7jit.exe 进程。 相反，它现在使用远程调试监视器服务 (msvsmon.exe)。

远程调试 Visual Studio 2005 中的要求是非常简单。 您需要在调试之前在远程服务器上运行 msvsmon.exe。 你可以从 Visual Studio CD 安装远程调试监视器或您可以只需运行 msvsmon.exe 从共享而无需在所有 Web 服务器上安装任何内容。

当您运行 msvsmon.exe 时，很可能会抱怨有关端口被阻止进行远程调试的信息。 幸运的是，您可以轻松地取消阻止直接在警告对话框中的端口，如下所示。


![通知 Windows 防火墙阻止远程调试](improvements-in-visual-studio-2005/_static/image9.jpg)

**图 12**： 通知该 Windows 防火墙，阻止远程调试


你已取消阻止后调试所需的端口，您将看到远程调试监视器，如下所示。 从该界面可以监视连接并更改轻松调试的权限。


![远程调试监视器](improvements-in-visual-studio-2005/_static/image10.jpg)

**图 13**： 远程调试监视器


还有可能要通过 FTP 打开一个 Web 应用程序进行远程调试。 步骤将与以前涵盖的那些相同。 但是，需要指定用于浏览 FTP 项目之前在此模块中所述的基 URL。

## <a name="lab-2"></a>实验室 2

## <a name="remote-debugging-with-visual-studio-2005"></a>使用 Visual Studio 2005 的远程调试

此实验室将引导你完成使用 Visual Studio 2005 进行远程调试。

有关此实验室的视频演练，请单击此处。


![](improvements-in-visual-studio-2005/_static/image5.png)


[打开的全屏视频](improvements-in-visual-studio-2005/_static/remdebug1.wmv)


此体验要求具备你拥有两台计算机，一个正在运行的 Visual Studio 2005 和其他正在运行 IIS 5 或更高版本。

1. 打开 Visual Studio 2005，并在远程服务器上创建新的 Web 站点。

> [!NOTE]
> 在远程 IIS 实例上或通过 FTP，可以创建网站。


1. 从远程 Web 服务器，使用 UNC 路径在开发计算机上找到 msvsmon.exe 并执行它。  
 Msvsmon.exe 的默认位置是 //server/c$/Program 文件/Microsoft Visual Studio 8/Common7/IDE/远程调试器/x86。
2. 如果系统提示您取消阻止端口进行远程调试，这样做。
3. 从开发计算机中，打开 Default.aspx 代码隐藏和页/加载 （_l） 方法中设置断点。
4. 从开发计算机开始调试。

您应按预期方式命中该断点。

## <a name="aspnet-development-server"></a>ASP.NET Development Server

如我们前面已经讨论过，Visual Studio 2005 附带了名为 ASP.NET 开发服务器的 Web 服务器。 （ASP.NET 开发服务器有时称为 Cassini。）此 Web 服务器是一种便利的方法来浏览和调试 Web 应用程序在文件系统上运行。

ASP.NET Development Server 是受限制的 Web 服务器。 不允许远程连接，它不会启动 Web 服务器的用户以外的任何用户从允许的任何请求。 它还没有为 ASP 页面提供服务的功能。 仅 ASP.NET 资源和 HTML 资源 （包括图像、 CSS 文件等） 会提供服务。

ASP.NET 开发服务器可以通过命令行启动运行 WebDev.WebServer.exe 文件位于 c:/Windows/Microsoft.NET/Framework/v2.0./*/* /  */*/*. 以下对话框显示可用的参数。


![](improvements-in-visual-studio-2005/_static/image11.jpg)

**图 14**


> [!NOTE]
> ASP.NET Development Server 不支持通过命令行显式启动时。
