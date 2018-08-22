---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 重大更改 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了针对.NET Framework 版本可能会影响使用创建的应用程序的月 4 日版本的更改...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 112483abdd920649fb530959a538b1d5ed6064d7
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41830045"
---
<a name="aspnet-4-breaking-changes"></a>ASP.NET 4 重大更改
====================
> 本文档介绍了针对.NET Framework 版本可能会影响使用早期版本中，其中包括 ASP.NET 4 Beta 1 和 Beta 2 版本创建的应用程序的月 4 日版本的更改。
> 
> [下载此白皮书](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)


<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>内容

[Web.config 文件中的 ControlRenderingCompatibilityVersion 设置](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode 更改](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode 和 UrlEncode 现在编码单引号](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET 页面 (.aspx) 分析器是 Stricter](#0.1__Toc256770144 "_Toc256770144")  
[更新的浏览器定义文件](#0.1__Toc256770145 "_Toc256770145")  
[从根 Web 配置文件中删除 System.Web.Mobile.dll](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET 请求验证](#0.1__Toc256770147 "_Toc256770147")  
[哈希算法的默认值现在为 HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[与新的 ASP.NET 4 根配置相关的配置错误](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 子应用程序启动失败的时在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序](#0.1__Toc256770150 "_Toc256770150")  
[ASP.NET 4 网站不能在安装 SharePoint 计算机上启动](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest.FilePath 属性不再包括 PathInfo 值](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2.0 应用程序可能会生成引用 eurl.axd 的 HttpException 错误](#0.1__Toc256770153 "_Toc256770153")  
[事件处理程序可能不会不引发在 IIS 7 或 IIS 7.5 中的默认文档集成模式下](#0.1__Toc256770154 "_Toc256770154")  
[将更改为 ASP.NET 代码访问安全性 (CAS) 实现](#0.1__Toc256770155 "_Toc256770155")  
[在移动 MembershipUser 中和其他类型 System.Web.Security Namespace](#0.1__Toc256770156 "_Toc256770156")  
[输出缓存发生更改以改变\*HTTP 标头](#0.1__Toc256770157 "_Toc256770157")  
[Passport System.Web.Security 类型可以是已过时](#0.1__Toc256770158 "_Toc256770158")  
[MenuItem.PopOutImageUrl 属性将无法呈现 ASP.NET 4 中的映像](#0.1__Toc256770159 "_Toc256770159")  
[Menu.StaticPopOutImageUrl 但 Menu.DynamicPopOutImageUrl 无法呈现图像时路径包含反斜杠](#0.1__Toc256770160 "_Toc256770160")  
[Disclaimer](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web.config 文件中的 ControlRenderingCompatibilityVersion 设置

ASP.NET 控件中修改了.NET Framework 版本 4 以便让您可以指定更准确地说及其呈现标记。 在以前版本的.NET Framework 中，某些控件发出了无法禁用的标记。 默认情况下，不能再生成 ASP.NET 4 此类型的标记。

如果使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，该工具会自动添加到的设置`Web.config`保留旧式呈现的文件。 但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的呈现模式。 若要禁用新的呈现模式，添加以下设置中的`Web.config`文件：

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

主要呈现更改的新行为将如下所示：

- **图像**并**ImageButton**控件不再呈现`border="0"`属性。
- **BaseValidator**从其派生的类和验证控件不再呈现红色文本默认情况下。
- **HtmlForm**控件不呈现**名称**属性。
- **表**控件不再呈现`border="0"`属性。
- 不设计用于用户输入的控件 (例如，**标签**控件) 不再呈现`disabled="disabled"`特性及其**已启用**属性设置为**false**（或如果它们从容器控件继承此设置）。

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode 的更改

**ClientIDMode** ASP.NET 4 中的设置允许您指定 ASP.NET 如何生成**id** HTML 元素的属性。 在以前版本的 ASP.NET，默认行为是等效于**AutoID**设置为**ClientIDMode**。 但是，默认设置是现在**可预测**。

如果使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，该工具会自动添加到的设置`Web.config`保留早期版本的.NET Framework 的行为的文件。 但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的模式。 若要禁用新的客户端 ID 模式，添加以下设置中的`Web.config`文件：

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode 和 UrlEncode 现在对单引号进行编码

在 ASP.NET 4 中， **HtmlEncode**并**UrlEncode**方法**HttpUtility**并**HttpServerUtility**类已更新到按如下所示进行编码的单引号字符 （'）：

- **HtmlEncode**方法将单引号的实例编码为。
- **UrlEncode**方法将单引号的实例编码为 %27。

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET 页面 (.aspx) 分析器是 Stricter

ASP.NET 页的页分析器 (`.aspx`文件) 和用户控件 (`.ascx`文件) 是在 ASP.NET 4 中更严格，则将拒绝无效标记的更多实例。 例如，以下两个代码片段会将已成功分析在早期版本的 ASP.NET，但现在将引发在 ASP.NET 4 中的分析器错误。

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

请注意，末尾处的无效分号**HiddenField**标记。

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

请注意，未闭合**样式**属性，在遇到**CssClass**属性。

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>更新的浏览器定义文件

浏览器定义文件已更新，以包括有关新的和已更新的浏览器和设备的信息。 旧式浏览器和设备（如 Netscape Navigator）已被删除，并且已添加更新的浏览器和设备（如 Google Chrome 和 Apple iPhone）。

如果应用程序包含的自定义浏览器定义继承自一个已删除的浏览器定义，将会出现错误。 例如，如果`App_Browsers`文件夹包含从 IE2 浏览器定义继承的浏览器定义，您将收到以下配置错误消息：

- 找不到 id 为 IE2 的浏览器或网关元素。

> [!NOTE]
> **HttpBrowserCapabilities**对象 (这由页面的公开**Request.Browser**属性) 由浏览器定义文件驱动。 因此，通过访问该对象在 ASP.NET 4 中的属性返回的信息可能不同于 ASP.NET 的早期版本中返回的信息。


您可以通过从以下文件夹复制浏览器定义文件还原到旧的浏览器定义文件：

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

将文件复制到相应`\CONFIG\Browsers`为 ASP.NET 4 的文件夹。 复制文件后，运行 Aspnet\_regbrowsers.exe 命令行工具。

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>System.Web.Mobile.dll 从根 Web 配置文件中删除

在以前版本的 ASP.NET，对 System.Web.Mobile.dll 程序集的引用已包含在根`Web.config`文件中**程序集**部分下。 为了提高性能，已删除对此程序集的引用。

System.Web.Mobile.dll 程序集包含在 ASP.NET 4 中，但不推荐使用。 如果你想要使用从 System.Web.Mobile.dll 程序集的类型，将对此程序集的引用添加到根`Web.config`文件或某个应用程序`Web.config`文件。 例如，如果你想要使用的任何 （已弃用） 的 ASP.NET 移动控件，您必须添加对 System.Web.Mobile.dll 程序集的引用`Web.config`文件。

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET 请求验证

在 ASP.NET 请求验证功能提供了一定的默认保护免受跨站点脚本 (XSS) 攻击。 在以前版本的 ASP.NET 中，默认情况下已启用请求验证。 但是，它仅应用于 ASP.NET 页面 (`.aspx`文件和其类文件) 和仅当这些页面执行。

在 ASP.NET 4 中，默认情况下启用请求验证的所有请求，因为它启用之前**BeginRequest**阶段的 HTTP 请求。 因此，请求验证适用于所有 ASP.NET 资源，而不仅仅是.aspx 页请求的请求。 这包括如 Web 服务调用和自定义 HTTP 处理程序的请求。 请求验证也处于活动状态的自定义 HTTP 模块将读取的 HTTP 请求内容时。

因此，以前未触发错误的请求可能现在会出现请求验证错误。 若要还原到 ASP.NET 2.0 请求验证功能的行为，添加以下设置中的`Web.config`文件：

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

但是，我们建议你分析任何请求验证错误，以确定是否存在的处理程序、 模块或其他自定义代码访问可能不安全 HTTP 输入的可能是 XSS 攻击途径。

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>哈希算法的默认值现在为 HMACSHA256

ASP.NET 使用加密算法和哈希算法来帮助保护数据（如窗体身份验证 Cookie 和视图状态）。 默认情况下，ASP.NET 4 现在使用 HMACSHA256 算法对 cookie 和视图状态哈希操作。 早期版本的 ASP.NET 使用较旧的 HMACSHA1 算法。

如果运行混合的 ASP.NET 2.0/ASP.NET 4，可能会影响你的应用程序数据，例如窗体身份验证 cookie 一定 across.NET Framework 版本的环境。 若要配置 ASP.NET 4 Web 应用程序使用较旧的 HMACSHA1 算法，添加以下设置中的`Web.config`文件：

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>与新的 ASP.NET 4 根配置相关的配置错误

根配置文件 (`machine.config`文件和根`Web.config`文件) 的已更新.NET Framework 4 （以及因此 ASP.NET 4） 若要包括的大多数样本配置信息中找到 ASP.NET 3.5 中的应用程序`Web.config`文件。 由于托管 IIS 7 和 IIS 7.5 配置系统的复杂性，运行 ASP.NET 4 下以及在 IIS 7 和 IIS 7.5 的 ASP.NET 3.5 应用程序可以导致 ASP.NET 或 IIS 配置错误。

我们建议如果可行，通过在 Visual Studio 2010 中，使用的项目升级工具升级到 ASP.NET 4 的 ASP.NET 3.5 应用程序。 Visual Studio 2010 自动修改 ASP.NET 3.5 应用程序的`Web.config`文件以包含为 ASP.NET 4 的相应设置。

但是，它是受支持的方案运行使用.NET Framework 4 中无需重新编译的 ASP.NET 3.5 应用程序。 在这种情况下，您可能必须手动修改应用程序的`Web.config`文件之前运行的应用程序在.NET Framework 4 和 IIS 7 或 IIS 7.5 下。

接下来的两部分介绍可能需要的软件的不同组合进行的更改。

**Windows Vista SP1 或 Windows Server 2008 SP1 中，既不 KB958854 修补程序，也不 SP2 的安装位置。** 在此配置中，IIS 7 配置系统错误地将应用程序的受管理的配置合并通过比较应用程序级`Web.config`文件到 ASP.NET 2.0`machine.config`文件。 由于此，应用程序级`Web.config`从.NET Framework 3.5 或更高版本的文件必须具有**system.web.extensions**为了不会导致 IIS 7 验证失败的配置节定义 （元素）。

但是，手动修改应用程序级`Web.config`不精确匹配引入了 Visual Studio 2008 的原始样本配置部分中定义的文件条目将导致 ASP.NET 配置错误。 （生成的 Visual Studio 2008 的默认配置项正常工作。）一个常见问题是手动修改`Web.config`文件省略**allowDefinition**并**requirePermission**在各种配置部分中找到的配置属性定义。 这会导致应用程序级别中的缩写的配置部分之间不匹配`Web.config`文件和 ASP.NET 4 中的完整定义`machine.config`文件。 因此，在运行时，ASP.NET 4 配置系统引发配置错误。

**Windows Vista SP2、 Windows Server 2008 SP2、 Windows 7、 Windows Server 2008 R2，并且还使用 Windows Vista SP1 和 Windows Server 2008 SP1 安装了修补程序 KB958854。**

在此方案中，IIS 7 和 IIS 7.5 本机配置系统将返回配置错误因为它对执行文本比较**类型**为受管理的配置节处理程序定义的属性。 因为所有`Web.config`生成的 Visual Studio 2008 和 Visual Studio 2008 SP1 的文件具有"3.5"中的类型字符串**system.web.extensions** （和相关） 配置节处理程序，因为 ASP.NET4`machine.config`文件中具有"4.0"**类型**属性 (attribute) 同一个配置节处理程序，始终在 Visual Studio 2008 或 Visual Studio 2008 SP1 中生成的应用程序无法通过在 IIS 7 中的配置验证和IIS 7.5。

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>解决这些问题

第一个方案的解决方法是更新应用程序级`Web.config`文件将从样板配置文本包含`Web.config`由 Visual Studio 2008 会自动生成的文件。

备用解决方法的第一个方案是在计算机上安装的 Vista 或 Windows Server 2008 Service Pack 2 或安装修补程序 KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)) 若要修复的不正确的配置合并行为IIS 配置系统。 但是，执行上述任一操作后，你的应用程序可能遇到的第二个方案所述的问题由于配置错误。

第二个方案的解决方法是删除或注释掉所有**system.web.extensions**配置节定义和配置节组的应用程序级定义`Web.config`文件。 这些定义通常位于应用程序级别顶部`Web.config`文件，并可以由标识**configSections**元素及其子项。

对于这两种方案，建议手动删除**system.codedom**部分中，虽然这不是必需。

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 子应用程序启动失败的时在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序

由于配置或编译错误，配置为运行 ASP.NET 早期版本的应用程序子级的 ASP.NET 4 应用程序可能无法启动。 下面的示例显示了受影响的应用程序的目录结构。

`/parentwebapp` （配置为使用 ASP.NET 2.0 或 ASP.NET 3.5）  
`/childwebapp` （配置为使用 ASP.NET 4）

中的应用程序`childwebapp`文件夹将无法启动在 IIS 7 或 IIS 7.5 上并将报表配置错误。 错误文本将包含一条类似于以下消息：

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`
  

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

在 IIS 6 中的应用程序上`childwebapp`文件夹也将无法启动，但它将会报告其他错误。 例如，错误文本可能状态如下：

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

因为，会出现这些情况中的父应用程序中的配置信息`parentwebapp`文件夹是确定使用的子站点的最后一个合并的配置设置的配置信息的层次结构的一部分应用程序中`childwebapp`文件夹。 具体取决于 ASP.NET 4 Web 应用程序是否在 IIS 7 （或 IIS 7.5） 上或在 IIS 6 上运行，IIS 配置系统或 ASP.NET 4 编译系统会返回错误。

若要解决此问题并获取子 ASP.NET 4 应用程序工作必须遵循的步骤取决于 ASP.NET 4 应用程序是否在 IIS 7 （或 IIS 7.5） 上运行了 IIS 6 或。

### <a name="step-1-iis-7-or-iis-75-only"></a>步骤 1 （IIS 7 或 IIS 7.5 仅）

此步骤是必需仅在运行 IIS 7 的操作系统或 IIS 7.5，其中包括 Windows Vista、 Windows Server 2008、 Windows 7 和 Windows Server 2008 R2 上。

移动**configSections**中的定义`Web.config`文件的父应用程序 （运行 ASP.NET 2.0 或 ASP.NET 3.5 的应用程序） 到根目录`Web.config`.net Framework 2.0 的文件。 IIS 7 和 IIS 7.5 native 配置系统扫描**configSections**元素时合并配置文件的层次结构。 移动**configSections**从父 Web 应用程序的定义`Web.config`根文件`Web.config`文件实际上就隐藏了所发生的子 ASP.NET 4 的配置合并过程中的元素应用程序。

在 32 位操作系统上或 32 位应用程序池，根的`Web.config`ASP.NET 2.0 和 ASP.NET 3.5 中的文件通常位于以下文件夹中：

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

在 64 位操作系统上或 64 位应用程序池，根的`Web.config`ASP.NET 2.0 和 ASP.NET 3.5 中的文件通常位于以下文件夹中：

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

如果在 64 位计算机上运行 32 位和 64 位 Web 应用程序，则必须移动**configSections**根元素向上`Web.config`32 位和 64 位系统文件。

当将**configSections**根目录中的元素`Web.config`文件中，粘贴部分后立即**配置**元素。 下面的示例演示根哪些的上半部分`Web.config`文件应如下所示完成移动元素。

> [!NOTE]
> 在以下示例中，以提高可读性已换行。


[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>步骤 2 （所有版本的 IIS）

此步骤是必需的 ASP.NET 4 子 Web 应用程序是否正在运行 IIS 6 上或在 IIS 7 （或 IIS 7.5） 上。

在中`Web.config`文件中的父 Web 应用程序运行的 ASP.NET 2 或 ASP.NET 3.5 中，添加**位置**显式指定 （对于 IIS 和 ASP.NET 配置系统） 的标记的配置条目仅将应用于父 Web 应用程序。 下面的示例演示的语法**位置**要添加元素：

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

下面的示例演示如何**位置**标记用于包装开头的所有配置节**appSettings**部分，并以结尾**system.webServer**部分。

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

完成步骤 1 和 2 后，子 ASP.NET 4 Web 应用程序将启动且未出错。

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>ASP.NET 4 网站不能在安装 SharePoint 计算机上启动

运行 SharePoint 的 web 服务器具有`Web.config`部署的 SharePoint 网站根目录的文件 (例如，`c:\inetpub\wwwroot\web.config`的默认 Web 站点)。 在此`Web.config`文件中，SharePoint 自定义部分信任级别设置名为 WSS\_最小。

如果尝试为此类型的 SharePoint Web 站点的子级运行部署的 ASP.NET 4 Web 站点，您将看到以下错误：

`Could not find permission set named 'ASP.NET'.`

此错误是因为 ASP.NET 4 代码访问安全性 (CAS) 基础结构会查找名为 ASP.NET 的权限集。 但是，部分信任配置文件引用的 WSS\_最小不包含具有该名称的任何权限集。

目前还没有 SharePoint 可与 ASP.NET 兼容的版本。 因此，您不应尝试作为子站点下 SharePoint Web 站点运行的 ASP.NET 4 网站。

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest.FilePath 属性不再包括 PathInfo 值

包含 ASP.NET 的早期版本**PathInfo**各种文件路径相关的属性，包括从返回的值中的值**HttpRequest.FilePath**， **HttpRequest.AppRelativeCurrentExecutionFilePath**，并**HttpRequest.CurrentExecutionFilePath**。 ASP.NET 4 不再包括**PathInfo**从这些属性的返回值中的值。 相反， **PathInfo**中提供了信息**HttpRequest.PathInfo**。 例如，假定以下 URL 片段：

`/testapp/Action.mvc/SomeAction`

在早期版本的 ASP.NET 中， **HttpRequest**属性具有以下值：

**HttpRequest.FilePath**: `/testapp/Action.mvc/SomeAction`

**HttpRequest.PathInfo**: （空）

在 ASP.NET 4 中， **HttpRequest**属性改为具有以下值：

**HttpRequest.FilePath**: `/testapp/Action.mvc`

**HttpRequest.PathInfo**: `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2.0 应用程序可能会生成引用 eurl.axd 的 HttpException 错误

ASP.NET 4 启用 IIS 6 上之后，（在 Windows Server 2003 或 Windows Server 2003 R2） 的 IIS 6 运行的 ASP.NET 2.0 应用程序可能会产生如下所示的错误：

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

当 ASP.NET 检测到配置的网站以使用 ASP.NET 4，ASP.NET 4 的本机组件无扩展名将 URL 传递到 ASP.NET 的托管部分进行进一步的处理会发生此错误。 但是，如果 ASP.NET 4 Web 站点下的虚拟目录配置为使用 ASP.NET 2.0，则处理此方法会导致修改后的 URL，其中包含字符串"eurl.axd"中的无扩展名 URL。 然后，此修改后的 URL 被发送到 ASP.NET 2.0 应用程序。 ASP.NET 2.0 无法识别"eurl.axd"格式。 因此，ASP.NET 2.0 将尝试查找名为的文件`eurl.axd`并执行它。 因为没有这样的文件存在，则请求会失败**HttpException**异常。

您可以解决此问题，使用以下选项之一。

### <a name="option-1"></a>选项 1

如果 ASP.NET 4 不需要为了运行网站，重新映射该网站以改为使用 ASP.NET 2.0。

### <a name="option-2"></a>选项 2

如果 ASP.NET 4 才能运行网站，移动到另一个网站映射到 ASP.NET 2.0 的所有子 ASP.NET 2.0 虚拟目录。

### <a name="option-3"></a>选项 3

如果不可行，若要重新映射到 ASP.NET 2.0 网站，或若要更改虚拟目录的位置，显式禁用在 ASP.NET 4 中处理无扩展名 URL。 使用以下过程：

1. 在 Windows 注册表中，打开以下节点：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. 创建一个新**DWORD**名为值**EnableExtensionlessUrls**。
2. 设置**EnableExtensionlessUrls**为 0。 这将禁用无扩展名 URL 行为。
3. 保存注册表值并关闭注册表编辑器。
4. 运行**iisreset**命令行工具，这会导致 IIS 读取新的注册表值。

> [!NOTE]
> 设置**EnableExtensionlessUrls**为 1 可启用无扩展名 URL 行为。 这是默认设置，如果未不指定任何值。


<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>事件处理程序可能不会不引发在 IIS 7 或 IIS 7.5 中的默认文档集成模式下

ASP.NET 4 中包含的更改的修改如何**操作**特性的 html**窗体**元素呈现时无扩展名 URL 解析为默认文档。 无扩展名 URL 解析为默认文档的示例将[ http://contoso.com/ ](http://contoso.com/)，从而导致对请求[ http://contoso.com/Default.aspx ](http://contoso.com/Default.aspx)。

现在 ASP.NET 4 的 HTML 呈现**窗体**元素的**操作**属性值为空字符串，当请求时，有一个默认文档映射到它的无扩展名 URL。 例如，在早期版本的 ASP.NET 中，对请求[ http://contoso.com ](http://contoso.com)会导致对请求`Default.aspx`。 在该文档中，打开**窗体**标记的呈现如以下示例所示：

`<form action="Default.aspx" />`

在 ASP.NET 4 中，对请求[ http://contoso.com ](http://contoso.com)也会导致对请求`Default.aspx`。 但是，ASP.NET 现在也可以呈现 HTML 开始**窗体**标记如以下示例所示：

`<form action="" />`

如何在这种差异**操作**呈现属性可能会导致细微的更改通过 IIS 和 ASP.NET 窗体发布请求的处理方式。 当**操作**属性为空字符串，IIS **DefaultDocumentModule**对象将创建对的子请求`Default.aspx`。 大多数情况下，此子请求是透明的应用程序代码和`Default.aspx`页会正常运行。

但托管代码和 IIS 7 或 IIS 7.5 集成模式之间可能的交互会导致托管 .aspx 页在子请求期间停止正常工作。 如果发生以下情况时，对子请求`Default.aspx`文档将导致错误或意外行为：

1. 使用浏览器发送一个.aspx 页面**窗体**元素的**操作**属性设置为""。
2. 在窗体回发到 ASP.NET。
3. 托管的 HTTP 模块读取实体正文的某些部分。 例如，模块将读取**Request.Form**或**Request.Params**。 这会使 POST 请求的实体正文读入托管内存中。 因此，实体正文不再对在 IIS 7 或 IIS 7.5 集成模式中运行的任何本机代码模块可用。
4. IIS **DefaultDocumentModule**对象最终运行并创建到的子请求`Default.aspx`文档。 但由于一段托管代码已读取实体正文，因此没有可发送给子请求的实体正文。
5. HTTP 管道子请求的处理程序的运行时`.aspx`对子阶段运行文件。
6. 没有实体正文，因为有任何窗体变量和视图状态，并因此没有信息是可供.aspx 页处理程序，以确定应引发哪个事件 （如果有）。 因此，不会运行针对受影响 .aspx 页的任何回发事件处理程序。

您可以按以下方式来解决此行为：

- 标识在默认文档的请求期间访问请求的实体正文的 HTTP 模块，并确定是否可以将它配置为仅针对托管请求运行。 在 IIS 7 和 IIS 7.5 集成模式下，HTTP 模块可以将标记为仅针对托管请求通过将以下属性添加到模块的运行**system.webServer/modules**条目：

- `precondition="managedHandler"`

- 在模块中的搜索请求 IIS 7 和 IIS 7.5 确定为不符合此设置禁用管理请求。 默认文档的请求，对于第一个请求都是无扩展名 URL。 因此，IIS 不运行标记为任何托管的模块与托管处理程序的前置条件在初始请求处理过程。 因此，托管的模块将不会意外地读取实体正文，因此实体正文仍可用，并传递给子请求和默认文档。

- 如果有问题的 HTTP 模块必须运行的所有请求 (静态文件，针对无扩展名 Url 解析为的**DefaultDocumentModule**对象，用于托管的请求，等等)，显式修改按受影响的.aspx 页设置**操作**页面的属性**System.Web.UI.HtmlControls.HtmlForm**控件为非空字符串。 例如，如果默认文档是`Default.aspx`，修改页面的代码以显式设置**HtmlForm**控件的**操作**属性设置为"Default.aspx"。

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>对 ASP.NET 代码访问安全性 (CAS) 实现的更改

ASP.NET 2.0 中，并通过扩展在 3.5 中，已添加的 ASP.NET 功能使用.NET Framework 1.1 和 2.0 代码访问安全性 (CAS) 模型。 但是，实质上已对 ASP.NET 4 中的 CAS 实现进行了检查。 因此，依赖于受信任的代码在全局程序集缓存 (GAC) 中运行的部分信任 ASP.NET 应用程序可能会因各种安全异常。 依赖于进行计算机 CAS 策略的大量修改的部分信任应用程序也可能会失败，且安全异常。

可以还原部分信任 ASP.NET 4 应用程序的行为的 ASP.NET 1.1 和 2.0 版使用新**legacyCasModel**属性中**信任**配置元素，如下面的示例中所示:

`<trust level= "Medium" legacyCasModel="true" />`

时还原到旧的 CAS 模型时，会启用以下旧 CA 行为：

- 遵循计算机 CAS 策略。
- 允许在单个应用程序域中的多个不同的权限集。
- 显式权限断言不需要的 GAC 中程序集，只有 ASP.NET 或其他.NET Framework 代码位于堆栈上时调用。

不能在.NET Framework 4 中还原一个方案： 非 Web 部分信任应用程序可以不再调用 System.Web.dll 和 System.Web.Extensions.dll 中的某些 Api。 在以前版本的.NET Framework 中，有可能使非 Web 部分信任应用程序要对其显式授予<strong>AspNetHostingPermission</strong>权限。 然后可以使用这些应用程序<strong>System.Web.HttpUtility</strong>，键入<strong>System.Web.ClientServices。\</ s > * 命名空间和类型与成员资格、 角色和配置文件。 在.NET Framework 4 中不再支持从非 Web 部分信任应用程序中调用这些类型。

> [!NOTE]
> **HtmlEncode**并**HtmlDecode**的功能**System.Web.HttpUtility**类已移至新的.NET Framework 4 **System.Net.WebUtility**类。 如果这是唯一使用的 ASP.NET 功能，应用程序的代码修改为使用新**WebUtility**类。


下面是对 ASP.NET 4 中的默认 CAS 实现的更改的高级摘要：

- ASP.NET 应用程序域现在是同构应用程序域。 应用程序域中提供了仅部分信任和完全信任的授予集。
- ASP.NET 部分信任的授予集是独立于任何企业级、 计算机级别或用户级 CAS 策略。
- ASP.NET 3.5 和 3.5 SP1 中提供的程序集已转换为使用.NET Framework 4 的透明度模型。
- 使用 ASP.NET **AspNetHostingPermission**大大减少了属性。 已从公共 ASP.NET Api 中删除此属性的大多数实例。
- 动态编译的程序集创建的 ASP.NET 生成提供程序已更新，以显式标记为透明的程序集。
- ASP.NET 的所有程序集现已标记 APTCA 特性可仅在 Web 托管环境的方式。 ClickOnce 等部分受信任的非 Web 宿主环境不能以调入 ASP.NET 程序集。

有关新的 ASP.NET 4 代码访问安全性模型的详细信息，请参阅[在 ASP.NET 应用程序中使用代码访问安全性](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)MSDN 网站上。

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>在移动 MembershipUser 和 System.Web.Security Namespace 中的其他类型

在 ASP.NET 成员资格中使用某些类型已从`System.Web.dll`对新 System.Web.ApplicationServices.dll 程序集。 移动这些类型是为了解析客户端中的类型与扩展的 .NET Framework SKU 中的类型之间的体系结构层依赖关系。

网站项目没有因移动这些类型，而问题，因为 System.Web.ApplicationServices.dll 由 ASP.NET 编译系统添加到默认情况下使用的引用的程序集列表。 如果升级通过在 Visual Studio 2010 中打开使用早期版本的 ASP.NET 到 ASP.NET 4 创建的网站项目，项目将编译错误。

同样，如果升级已在早期版本的 ASP.NET 到 ASP.NET 4 中通过在 Visual Studio 2010 中打开一个 Web 应用程序项目，升级过程将向项目添加对 System.Web.ApplicationServices.dll 的引用。 因此，升级的 Web 应用程序项目也将编译未出现错误。

使用 ASP.NET 的早期版本创建的已编译 （二进制） 文件也将不包含错误在运行 ASP.NET 4 中，即使成员身份类型移到不同的程序集。 类型转发的信息已添加到 ASP.NET 4 版的`System.Web.dll`，会自动将这些类型的运行时引用路由到新位置的类型。

但是，使用特定的成员身份类型和已从早期版本的 ASP.NET 中升级的类库将无法进行编译时在 ASP.NET 4 项目中使用。 例如，一个类库项目可能无法编译并报告错误如下所示：

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
  

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

可以通过添加引用你的类库项目中对 System.Web.ApplicationServices.dll 来解决此问题。

以下列表显示*System.Web.Security*类型已从移动`System.Web.dll`对 System.Web.ApplicationServices.dll:

- *System.Web.Security.MembershipCreateStatus*
- *System.Web.Security.Membership.CreateUserException*
- *System.Web.Security.MembershipPasswordException*
- *System.Web.Security.MembershipPasswordFormat*
- *System.Web.Security.MembershipProvider*
- *System.Web.Security.MembershipProviderCollection*
- *System.Web.Security.MembershipUser*
- *System.Web.Security.MembershipUserCollection*
- *System.Web.Security.MembershipValidatePasswordEventHandler*
- *System.Web.Security.ValidatePasswordEventArgs*
- *System.Web.Security.RoleProvider*
- <a id="0.1_a"></a>*System.Web.Configuration.MembershipPasswordCompatibilityMode*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>输出缓存发生更改以改变\*HTTP 标头

在 ASP.NET 1.0 中，bug 会导致缓存指定的页面`Location="ServerAndClient"`作为输出 – 缓存设置，以便发出`Vary:*`在响应中的 HTTP 标头。 这还能起到告知客户端浏览器绝不要本地对页进行缓存的作用。

在 ASP.NET 1.1 **System.Web.HttpCachePolicy.SetOmitVaryStar**方法的调用，禁止显示时无法调用`Vary:*`标头。 选择此方法是因为更改发出的 HTTP 标头被视为可能影响重大的更改。 但是，开发人员感到困惑的行为在 ASP.NET 中，并且 bug 报告表明开发人员不了解现有**SetOmitVaryStar**行为。

在 ASP.NET 4 中，已做出的决定修复根本问题。 `Vary:*` HTTP 标头，将不再发出从指定以下指令的响应：

`<%@OutputCache Location="ServerAndClient" %>`

因此， **SetOmitVaryStar**不再需要即可禁止显示`Vary:*`标头。

在指定的应用程序中`Location="ServerAndClient"`中 **@ OutputCache**指令在页面上，则你将看到的名称所暗示的行为**位置**属性的值-即，对页进行缓存可调用而无需在浏览器中缓存**SetOmitVaryStar**方法。

如果你的应用程序中的页必须发出`Vary:*`，调用**AppendHeader**方法，如以下示例所示：

`HttpResponse.AppendHeader("Vary","*");`

或者，可以更改输出缓存的值**位置**属性为"Server"。

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport System.Web.Security 类型可以是已过时

ASP.NET 2.0 中内置的 Passport 支持已过时和不支持几年由于 Passport (现在 LiveID) 中进行了更改。 五种类型中与 Passport 相关的结果， **System.Web.Security**现在被标记为与**ObsoleteAttribute**属性。

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>MenuItem.PopOutImageUrl 属性将无法呈现在 ASP.NET 4 中的图像

在 ASP.NET 3.5 中， *MenuItem.PopOutImageUrl*属性，可以指定用于指示菜单项具有动态子菜单的菜单项中显示的图像的 URL。 下面的示例演示如何在 ASP.NET 3.5 中的标记中指定此属性。

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

由于 ASP.NET 4 中的设计更改，而不输出为呈现*PopOutImageUrl*如果属性设置为*MenuItem*类。 相反，您必须指定图像 URL 中直接*菜单*控制使用*StaticPopOutImageUrl*属性或*DynamicPopOutImageUrl*属性。 在静态菜单中，使用时*Menu.StaticPopOutImageUrl*属性指定显示，以便指示静态菜单项包含子菜单，如下面的示例中所示的图像的 URL:

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

如果您正在使用动态菜单，则使用*Menu.DynamicPopOutImageUrl*属性来指定，该值指示动态菜单项包含子菜单的图像的 URL。 下面的示例类似于前一个，但演示了如何设置*DynamicPopOutImageUrl*动态菜单的属性。

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

如果*Menu.DynamicPopOutImageUrl*未设置属性和*Menu.DynamicEnableDefaultPopOutImage*属性设置为*false*，不显示任何图像。 同样，如果*StaticPopOutImageUrl*未设置属性和*StaticEnableDefaultPopOutImage*属性设置为*false*，不显示任何图像。

当设置这些属性的路径时，使用正斜杠 （/） 而不是反斜杠 (\)。 有关详细信息，请参阅[Menu.StaticPopOutImageUrl 和 Menu.DynamicPopOutImageUrl 故障到呈现图像时路径包含反斜杠](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu.StaticPopOutImageUrl_and_Menu。") 其他位置在本文档中。

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>Menu.StaticPopOutImageUrl 和 Menu.DynamicPopOutImageUrl 无法呈现图像时路径包含反斜杠

在 ASP.NET 4 中，使用指定的映像*Menu.StaticPopOutImageUrl*并*Menu.DynamicPopOutImageUrl*属性将不会呈现如果路径包含 backlashes (\)。 这是从 ASP.NET 的早期版本的更改。

下面的示例对*菜单*控件的标记演示*StaticPopOutImageUrl*属性设置使用的路径包含反斜杠。 在 ASP.NET 4 中，将不会呈现在属性中指定的图像。

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

若要更正此问题，请更改中指定的路径值*StaticPopOutImageUrl*并*DynamicPopOutImageUrl*属性，以使用正斜杠 （/）。 下面的示例显示了此更改：

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

请注意从早期版本的 ASP.NET 到 ASP.NET 4 已迁移的应用程序可能还会受到影响，因为*MenuItem.PopOutImageUrl*属性已更改。 有关详细信息，请参阅[MenuItem.PopOutImageUrl 属性将无法呈现 ASP.NET 4 中的映像](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem.PopOutImageUrl_Propert")本文档中的其他位置。

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。 由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

遵守所有适用的著作权法是用户的责任。 未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。

对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。

除非另有说明，示例公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人物、 地点和事件属虚构的并且无意与任何真实的公司、 组织、 产品、 域名、 电子邮件地址、 徽标、 人员、 地点或事件无关，也应进行这方面的推断。

© 2010 Microsoft Corporation. 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。
