---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
title: 预编译网站 (VB) |Microsoft Docs
author: rick-anderson
description: Visual Studio 将 ASP.NET 开发人员提供了两种类型的项目： Web 应用程序项目 (Wap) 和网站项目 (Wsp)。 其中一个主要区别 betwe...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: c285dc6f-a1c6-46e6-ac03-3830947f57e3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/precompiling-your-website-vb
msc.type: authoredcontent
ms.openlocfilehash: d952a949552f5ec1a0241fd8467431cbec0758e9
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41831850"
---
<a name="precompiling-your-website-vb"></a>预编译网站 (VB)
====================
通过[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](http://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_15_VB.zip)或[下载 PDF](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial15_Precompiling_vb.pdf)

> Visual Studio 将 ASP.NET 开发人员提供了两种类型的项目： Web 应用程序项目 (Wap) 和网站项目 (Wsp)。 两种项目类型之间的主要差异之一是 Wap 必须具有而 WSP 中的代码自动编译 web 服务器上，在部署之前显式编译的代码。 但是，就可以在部署之前 WSP 预编译。 本教程探讨了预编译的优势，并演示如何预编译网站从 Visual Studio 中和从命令行。


## <a name="introduction"></a>介绍

Visual Studio 将 ASP.NET 开发人员提供了两种不同的项目类型： Web 应用程序项目 (WAP) 和网站项目 (WSP)。 这些项目类型之间的主要区别之一是，需要 Wap*显式编译*而使用 Wsp*自动编译*，默认情况下。 使用 Wap，web 应用程序的代码编译为单个程序集，在网站中创建`Bin`文件夹。 部署需要复制标记内容 ( `.aspx.ascx`，并`.master`文件) 在项目中的程序集以及`Bin`文件夹; 代码隐藏类文件本身不需要部署。 但是，通过将标记页面和其相应的代码隐藏类复制到生产环境部署 Wsp。 Web 服务器上按需编译的代码隐藏类。

> [!NOTE]
> 引用的"显式编译与自动编译"一节中[*确定哪些文件需要将部署到*教程](determining-what-files-need-to-be-deployed-vb.md)的更多背景上项目之间的差异模型、 显式和自动编译和编译模型如何影响部署。


自动编译选项是易于使用。 没有任何显式编译步骤，并且文件已修改需要部署，而显式编译要求部署已更改的标记页和只是编译的程序集。 但是，自动部署具有两个潜在的缺点：

- 因为第一次访问时，必须自动编译页面，所以时，可能会短暂而明显的延迟为在部署后首次请求 ASP.NET 页。
- 自动编译需要这两种声明性标记和源代码代码在 web 服务器上存在。 如果计划销售给客户将在其 web 服务器安装的 web 应用程序，这可以是来说毫无吸引力。

如果两个以上不足之处是交易断路器，你可以转到 WAP 模型或*预编译*在部署之前 WSP。 本教程中检查预编译选项最适合用于托管网站，并演示了如何预编译过程并预编译网站的部署。

## <a name="an-overview-of-aspnet-code-generation-and-compilation"></a>ASP.NET 代码生成和编译的概述

我们查看可用的预编译选项之前，让我们首先谈一谈的代码生成和编译的 ASP.NET 页面请求第一次，因为创建或上次更新时间时发生。 如您所知，ASP.NET 页面组成两个部分： 中的声明性标记`.aspx`文件; 以及源的代码部分，通常在单独的代码隐藏类文件 (`.aspx.vb`)。 当请求 ASP.NET 页时由运行时执行的步骤取决于应用程序的编译模式。

使用 Wap，页的源代码必须显式编译到单个程序集，然后部署。 在部署期间，此程序集和各种标记页面都复制到生产环境。 当请求到达时到 ASP.NET 页面的 web 服务器时，运行时创建页面的代码隐藏类的实例并调用其`ProcessRequest`方法，用于启动页面生命周期，并从根本上讲，生成页面的内容，返回到请求者。 因为代码隐藏类已编译到程序集在部署之前，运行时可使用 ASP.NET 页面的代码隐藏类。

使用 Wsp 和自动编译，则在部署之前没有显式编译步骤。 相反，部署涉及到将声明性和源代码内容复制到生产环境。 请求到达时到 ASP.NET 页面的 web 服务器第一次由于页面已创建或上次更新时间，则运行时必须先编译为程序集的代码隐藏类。 此编译的程序集保存在文件夹`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`，但可以通过自定义此文件夹的位置`<pages>`中的元素`Web.config`。 由于程序集保存到磁盘，它不需要的后续请求同一页进行重新编译。

> [!NOTE]
> 在使用自动编译，因为它需要一段时间来编译页面的代码并将保存到生成的程序集的服务器的站点中的第一次 （或第一次由于它被更改） 请求页时如您所料，是连接期间的轻微延迟磁盘。


简单地说，与显式编译需要编译网站的源代码，然后再进行部署，无需执行该步骤中保存运行时。 与自动编译运行时处理页面第一次访问编译的页的源代码，但稍有初始化成本，其创建后或上次更新时间。

但 ASP.NET 页的声明性部分 (`.aspx`文件)？ 很明显，没有之间的关系`.aspx`文件和其代码隐藏类，作为在声明性标记中定义的 Web 控件中的代码均可在代码中访问。 它也是很明显，中的内容`.aspx`文件可能严重影响呈现的标记生成的页面。 如何在运行时的工作原理与文本、 HTML 和 Web 控件的语法中定义`.aspx`文件生成请求的页面的呈现内容？

我不想获取太多低级别实施详细信息，Wap 和 Wsp 之间的不同，但在简单地说，运行时自动生成作为受保护的成员和方法包含各种 Web 控件的类文件。 此生成的文件作为*分部类*到相应的代码隐藏类。 ([分部类](http://www.dotnet-guide.com/partialclasses.html)允许单个类的内容分布在多个文件。)因此，在两个位置定义的代码隐藏类： 在`.aspx.vb`创建，并由运行时创建此自动生成的类中的文件。 此自动生成的类存储在`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`文件夹。

其中重要一点此处是 ASP.NET 页以呈现由运行时，这两个其声明性和源的代码部分必须编译到程序集。 使用 Wap，源代码显式编译到程序集之前部署，但声明性标记仍必须转换为代码和 web 服务器上运行时编译。 使用自动编译的 Wsp，使用的源代码和声明性标记都需要编译的 web 服务器。

可以使用 WSP 模型使用显式编译它。 可以显式等源的代码部分中，编译使用 WAP 模型。 更重要的是，您还可以编译声明性标记。

## <a name="precompilation-options"></a>预编译选项

.NET Framework 附带[ASP.NET 编译工具 (`aspnet_compiler.exe`)](https://msdn.microsoft.com/library/ms229863.aspx) ，可用于编译 ASP.NET 应用程序使用 WSP 模型生成的源代码 （和甚至内容）。 此工具随.NET Framework 2.0 版一起发布，它位于`%WINDIR%\Microsoft.NET\Framework\v2.0.50727`文件夹; 它可以从命令行使用或启动 Visual Studio 中通过生成菜单的发布网站选项。

编译工具提供了两种常规形式的编译： 就地预编译和部署的预编译。 运行就地预编译`aspnet_compiler.exe`从命令行工具，然后在计算机上指定的虚拟目录或驻留的网站物理路径的路径。 编译工具然后会将每个 ASP.NET 页面在项目中，存储中的已编译的版本`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\Temporary ASP.NET Files`一样如果页面具有每个已访问过第一次从浏览器的文件夹。 就地预编译可以加快对你的站点上的新部署 ASP.NET 页面，因为它减少了无需执行此步骤运行时的第一个请求。 但是，因为它要求您将能够运行程序从 web 服务器的命令行的就地预编译不适用于大多数托管网站。 在共享宿主环境中不允许此访问级别。

> [!NOTE]
> 有关就地预编译的详细信息，请参阅[How To： 预编译 ASP.NET Web Sites](https://msdn.microsoft.com/library/ms227972.aspx)和[ASP.NET 2.0 中的预编译](http://www.odetocode.com/Articles/417.aspx)。


而不是编译到的网站中的页`Temporary ASP.NET Files`文件夹中，为部署的预编译会编译到所选的和一种格式，可以部署到生产环境中的目录页面。

有两种类型的预编译为我们在本教程中探讨的部署： 预编译使用的可更新用户界面，并利用非可更新用户界面的预编译。 使用的可更新用户界面的预编译离开中的声明性标记`.aspx`， `.ascx`，和`.master`文件，从而允许开发人员能够查看，如有需要，修改生产服务器上的声明性标记。 使用非可更新用户界面的预编译生成`.aspx`页的任何内容并删除 void`.ascx`和`.master`文件，从而隐藏在声明性标记和禁止开发人员从其进行更改生产环境。

### <a name="precompiling-for-deployment-with-an-updatable-user-interface"></a>预编译为部署使用的可更新用户界面

若要了解有关部署的预编译的最佳方式是查看示例的操作。 让我们重新编译使用的可更新用户界面部署通讯簿评审 WSP。 从 Visual Studio 的生成菜单或从命令行中，可以调用 ASP.NET 编译工具。 本部分将检查中使用工具从 Visual Studio;"预编译命令行中的"部分介绍从命令行运行的编译器工具。

在 Visual Studio 中打开通讯簿评审 WSP，转到生成菜单并选择发布网站菜单选项。 这将启动发布网站对话框中 (请参阅**图 1**) 时，可以指定目标位置、 是否预编译的站点的用户界面对其进行更新和其他编译器工具选项。 目标位置可以是远程 web 服务器或 FTP 服务器，但现在选择您的计算机的硬盘驱动器上的文件夹。 因为我们想要重新编译站点使用的可更新用户界面，保留选中"允许更新此预编译的站点"复选框，然后单击确定。

[![](precompiling-your-website-vb/_static/image2.png)](precompiling-your-website-vb/_static/image1.png)

**图 1**: ASP.NET 编译工具将预编译你的网站到指定的目标位置  
 ([单击此项可查看原尺寸图像](precompiling-your-website-vb/_static/image3.png))

> [!NOTE]
> 生成菜单中的发布网站选项不可用在 Visual Web Developer。 如果您使用的 Visual Web Developer 需要使用 ASP.NET 编译工具，它在"预编译命令行中的"部分中介绍的命令行版本。


在预编译网站后, 导航到在发布网站对话框中输入的目标位置。 请花费片刻时间进行比较的你的网站的内容与此文件夹的内容。 **图 2**显示书评网站文件夹。 请注意它同时包含`.aspx`和`.aspx.cs`文件。 另请注意，`Bin`目录中只有一个文件，包括`Elmah.dll`，我们在添加[前面的教程](logging-error-details-with-elmah-vb.md)

[![](precompiling-your-website-vb/_static/image5.png)](precompiling-your-website-vb/_static/image4.png)

**图 2**： 在项目目录包含`.aspx`并`.aspx.cs`文件;`Bin`文件夹只包含 `Elmah.dll`  
 ([单击此项可查看原尺寸图像](precompiling-your-website-vb/_static/image6.png))

**图 3**显示其内容创建的 ASP.NET 编译工具的目标位置文件夹。 此文件夹不包含任何代码隐藏文件。 此外，此文件夹`Bin`目录中包括几个程序集和第二个`.compiled`除了文件`Elmah.dll`程序集。

[![](precompiling-your-website-vb/_static/image8.png)](precompiling-your-website-vb/_static/image7.png)

**图 3**： 目标位置文件夹包括有关部署的文件  
 ([单击此项可查看原尺寸图像](precompiling-your-website-vb/_static/image9.png))

与 Wap 中的显式编译，不同的部署过程预编译不会创建一个程序集的整个站点。 相反，它的批一起几页每个程序集。 它还会将`Global.asax`到自己的程序集，以及中的任何类文件 （如果存在）`App_Code`文件夹。 为 ASP.NET 保存声明性标记的文件的 web 页面、 用户控件和母版页 (`.aspx`， `.ascx`，和`.master`文件，分别) 作为复制-是到目标位置目录。 同样，`Web.config`文件将直接通过复制以及任何静态文件，例如图像、 CSS 类和 PDF 文件。 有关更正式的编译工具如何处理各种说明文件类型，请参阅[ASP.NET 预编译期间文件处理](https://msdn.microsoft.com/library/e22s60h9.aspx)。

> [!NOTE]
> 您可以指示编译工具来创建每个 ASP.NET 页、 用户控件或母版页的一个程序集从发布网站对话框中的"使用固定命名和单页程序集"复选框。 使每个 ASP.NET 页面编译到自己的程序集可以更加精细地控制部署。 例如，如果你已更新单个 ASP.NET 网页，且需要来部署所做的更改，你需要仅部署该页面的`.aspx`文件和关联的程序集到生产环境。 请查阅[如何： 使用 ASP.NET 编译工具生成固定名称](https://msdn.microsoft.com/library/ms228040.aspx)有关详细信息。


目标位置目录还包含一个文件，即未预编译的 web 项目的一部分`PrecompiledApp.config`。 此文件告知应用程序进行预编译的 ASP.NET 运行时且是否它进行预编译可更新或中午可更新 ui。

最后，请花费片刻时间来打开其中一个`.aspx`中使用 Visual Studio 或所选文本编辑器的目标位置的文件。 时使用的可更新用户界面的部署，预编译，目标位置目录中的 ASP.NET 页面将包含在网站中的相应文件完全相同的标记。

### <a name="precompiling-for-deployment-with-a-non-updatable-user-interface"></a>预编译为具有非可更新用户界面部署

ASP.NET 编译器工具还可以使用预编译站点部署中使用非可更新 UI。 预编译站点具有非可更新 UI 工作方式非常类似原因 ASP.NET 页、 用户控件和母版页的目标目录中去除它们的标记的可更新 UI，主要区别的预编译。 若要预编译的网站部署中使用非可更新 UI，从生成菜单中选择发布 Web 站点选项，但取消选中"允许更新此预编译的站点"选项 (请参阅**图 4**)。

[![](precompiling-your-website-vb/_static/image11.png)](precompiling-your-website-vb/_static/image10.png)

**图 4**： 取消选中"允许更新此预编译的站点"选项向预编译与非可更新 UI  
 ([单击此项可查看原尺寸图像](precompiling-your-website-vb/_static/image12.png))

**图 5**预编译的非可更新用户界面后显示的目标位置文件夹。

[![](precompiling-your-website-vb/_static/image14.png)](precompiling-your-website-vb/_static/image13.png)

**图 5**： 非可更新 Ui 的部署的目标位置文件夹  
 ([单击此项可查看原尺寸图像](precompiling-your-website-vb/_static/image15.png))

比较**图 3**到**图 5**。 虽然两个文件夹可能看起来完全相同，但请注意不可更新的 UI 文件夹缺少母版页， `Site.master`。 和，而**图 5**包括各种 ASP.NET 页中，如果您查看您将看到它们已被其声明性标记去掉并包含占位符文本替换为这些文件的内容:"这是由生成的标记文件预编译工具，并且不应删除 ！"

[![](precompiling-your-website-vb/_static/image17.png)](precompiling-your-website-vb/_static/image16.png)

**图 5**： 已从 ASP.NET 页中删除的声明性标记

`Bin`中的文件夹**图 3**并**5**更大不相同。 程序集，除了`Bin`文件夹中的**图 5**包括`.compiled`每个 ASP.NET 页、 用户控件和母版页文件。

预编译站点具有非可更新的 UI 可在你不想要修改的个人或公司，他们会安装或管理在生产环境中的网站的 ASP.NET 页的内容。 如果生成销售给客户在其自己的 web 服务器上安装的 ASP.NET web 应用程序，您可能希望确保他们不要通过直接编辑修改您的网站的外观`.aspx`将其寄送的页面。 通过预编译你的网站使用非可更新 UI，寄送占位符`.aspx`页作为安装过程中，从而防止你的客户从检查或修改其内容的一部分。

### <a name="precompiling-from-the-command-line"></a>从命令行预编译

在后台，Visual Studio 的发布网站对话框调用 ASP.NET 编译工具 (`aspnet_compiler.exe`) 预编译网站。 或者，可以调用此工具从命令行。 事实上，如果使用 Visual Web Developer 然后需要编译器工具从命令行运行，因为 Visual Web Developer 的生成菜单不包括发布 Web 站点选项。

若要使用命令行中的编译器工具，启动到命令行删除，然后导航到 framework 目录中，通过`%WINDIR%\Microsoft.NET\Framework\v2.0.50727`。 接下来，在命令行中输入以下语句：

`aspnet_compiler -p "physical_path_to_app" -v / -f -u "target_location_folder"`

上述命令将启动 ASP.NET 编译器工具 (`aspnet_compiler.exe`) 并通过`-p`开关，指示它预编译网站以根*物理\_路径\_到\_应用*;此值将类似于`C:\MySites\BookReviews`，并应由双引号分隔。

`-v`开关指定站点的虚拟目录。 如果你的站点注册为 IIS 元数据库中的默认网站，则可以省略`-p`切换，只需指定应用程序的虚拟目录。 如果您使用`-p`切换值继续`-v`开关指示网站的根目录，用于解决应用程序根目录的引用。 例如，如果指定的值`-v /MySite`然后于应用程序中引用`~/path/file`将解析为`~/MySite/path/file`。 因为书评站点位于在我的 web 托管公司的根目录处我已使用交换机`-v /`。

`-f`开关，如果存在，指示编译工具，以覆盖*目标\_位置\_文件夹*目录已存在。 如果省略`-f`开关和目标位置文件夹已存在，则编译工具将退出并显示错误:"错误 ASPRUNTIME： 目标目录不为空。 请手动删除或选择不同的目标。"

`-u`开关，如果存在，会通知该工具以创建可更新用户界面。 省略此预编译站点有一个非可更新用户界面的开关。

最后，*目标\_位置\_文件夹*是目标位置目录; 的物理路径此值将类似于`C:\MySites\Output\BookReviews`，并应由双引号分隔。

## <a name="deploying-the-precompiled-website"></a>部署预编译的网站

现在我们已了解如何使用 ASP.NET 编译工具预编译网站使用的可更新而非可更新的用户界面选项。 但是，我们的示例到目前为止已预编译网站到本地文件夹，而不适用于生产环境。 好消息是预编译的网站部署变得轻而易举，并可通过 Visual Studio 或通过某些其他文件复制机制，如从独立的 FTP 客户端。

发布网站对话框 (第一次所示**图 1**) 具有的目标位置选项，指示预编译的网站文件复制到的位置。 此位置可以是远程 web 服务器或 FTP 服务器。 此文本框中输入远程服务器预编译，并将该网站部署到在一个步骤中指定的服务器。 或者，可以预编译到本地文件夹的网站，然后手动将该文件夹的内容复制到生产环境中通过 FTP 或某些其他方法。

通过 Visual Studio 的发布网站对话框会自动部署的预编译的网站是有用的简单的站点在开发和生产环境之间没有配置差异。 但是，如中所述[*常见配置差异之间开发和生产*教程](common-configuration-differences-between-development-and-production-vb.md)并不少见的存在此类差异。 例如，书评 web 应用程序开发环境中比在生产环境中使用不同的数据库。 当 Visual Studio 将网站发布到远程服务器，它会盲目地将复制设置开发环境中的配置文件信息。

为站点配置开发和生产环境之间的差异可能是最好预编译站点到本地目录中，复制的特定于生产环境的配置文件，然后将复制到的预编译输出的内容生产环境。

有关在开发环境中的文件复制到生产环境使用刷新程序参考[*部署在网站中使用 FTP 客户端*](deploying-your-site-using-an-ftp-client-vb.md)并[ *部署您的网站使用 Visual Studio* ](determining-what-files-need-to-be-deployed-vb.md)教程。

## <a name="summary"></a>总结

ASP.NET 支持的编译两种模式： 自动和显式。 如前面的教程中所述，Web 应用程序项目 (Wap) 将使用显式编译，而网站项目 (Wsp) 默认情况下使用自动编译。 但是，就可以进行显式使用 ASP.NET 编译工具编译在部署之前 WSP。

本教程着重介绍有关部署支持的编译工具的预编译。 当部署的预编译，编译工具创建的目标位置文件夹、 编译指定的 web 应用程序的源代码，并复制这些编译到目标位置文件夹的程序集和内容文件。 编译工具可以配置为创建可更新或非可更新用户界面。 使用非可更新用户界面选项预编译，会删除内容文件中的声明性标记。 简单地说，预编译允许在部署基于网站项目的应用程序，而不包括任何源代码文件和使用声明性标记删除，如果所需的。

快乐编程 ！

### <a name="further-reading"></a>其他阅读材料

在本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 网站预编译](https://msdn.microsoft.com/library/ms228015.aspx)
- [代码隐藏文件和 ASP.NET 2.0 中的编译](https://msdn.microsoft.com/magazine/cc163675.aspx)
- [在 ASP.NET 中的预编译](http://www.odetocode.com/Articles/417.aspx)
- [在 ASP.NET 中的预编译的站点选项](http://www.dotnetperls.com/precompiled)

> [!div class="step-by-step"]
> [上一页](logging-error-details-with-elmah-vb.md)
> [下一页](users-and-roles-on-the-production-website-vb.md)
