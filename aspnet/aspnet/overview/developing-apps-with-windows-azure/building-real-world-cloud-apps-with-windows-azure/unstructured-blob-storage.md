---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: 非结构化的 Blob 存储 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: 9ca599e023ac9b1cf8f00389048c8da6ef0e364f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41834975"
---
<a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>非结构化的 Blob 存储 （使用 Azure 构建实际云应用）
====================
通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。


在上一章中我们介绍了分区方案，并介绍了如何修复它应用在 Azure 存储 Blob 服务和 Azure SQL 数据库中的其他任务数据中存储图像。 这一章中我们 Blob 服务一起深入探讨并演示如何实现在 Fix It 项目代码中。

## <a name="what-is-blob-storage"></a>什么是 Blob 存储？

Azure 存储 Blob 服务提供在云中存储文件的方法。 Blob 服务有很多优点通过在本地网络文件系统中存储文件：

- 它是高度可缩放。 单个存储帐户可以存储[亿字节](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)，并且可以具有多个存储帐户。 最大的 Azure 客户的一些存储数百个千万亿字节。 Microsoft SkyDrive 使用 blob 存储。
- 它是持久的。 自动备份存储在 Blob 服务中的每个文件。
- 它提供高可用性。 [存储的 SLA](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)承诺 99.9%或 99.99%运行时间，具体取决于哪个异地冗余选项选择。
- 它是 Azure 中，这意味着您只需存储和检索文件，只支付实际使用时，存储量的一项平台即服务 (PaaS) 功能，Azure 会自动负责设置和管理的所有 Vm 和所需的磁盘驱动器服务。
- 通过使用 REST API 或通过使用编程语言 API，可以访问 Blob 服务。 Sdk 是适用于.NET、 Java、 Ruby 和其他人。
- 当您将文件存储在 Blob 服务中时，就可以轻松地它公开提供通过 Internet。
- 可以保护服务，以便他们可以访问只能由授权用户的 Blob 中的文件，也可以提供临时访问令牌，用于使其可用的某个人可以仅为有限的时间段。

只要您为 Azure 构建应用，并且你想要存储大量数据的本地环境中，将转中的文件，例如图像、 视频、 Pdf、 电子表格等-请考虑将 Blob 服务。

## <a name="creating-a-storage-account"></a>创建存储帐户

若要开始使用 Blob 服务在 Azure 中创建存储帐户。 在门户中，单击**新建** -- **Data Services** -- **存储** -- **快速创建**，然后输入一个 URL 和数据中心位置。 数据中心位置应与你的 web 应用相同。

![创建存储帐户](unstructured-blob-storage/_static/image1.png)

你想要存储的内容，并且如果你选择选择主要区域[异地复制](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)选项时，Azure 中的国家/地区的另一个区域中不同的数据中心创建的所有数据副本。 例如，如果您选择美国西部的数据中心，当您将它放到美国西部的数据中心，但在后台 Azure 还将文件存储时将其复制到其他美国数据中心之一。 如果在灾难发生在一个国家/地区的区域中，你的数据是仍保持安全。

Azure 不会跨地缘政治边界复制数据： 如果主位置位于美国，你的文件只会复制到美国的; 另一个区域如果您的主要位置是澳大利亚，你的文件会仅复制到另一个数据中心中澳大利亚。

当然，您还可以创建存储帐户通过从脚本中，执行命令象我们早先。 下面是创建存储帐户的 Windows PowerShell 命令：

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

存储帐户后，你可以立即开始在 Blob 服务中存储文件。

## <a name="using-blob-storage-in-the-fix-it-app"></a>修复其应用中使用 Blob 存储

Fix It 应用，可将照片上传。

![创建 Fix It 任务](unstructured-blob-storage/_static/image2.png)

当您单击**创建 fix It**，应用程序上传指定的图像文件并将其存储在 Blob 服务。

### <a name="set-up-the-blob-container"></a>设置 Blob 容器

为了在所需的 Blob 服务中存储文件*容器*以将其存储在。 Blob 服务容器对应于文件系统文件夹。 我们讨论了中的环境创建脚本[使一切自动化章](automate-everything.md)创建存储帐户，但是它们无需创建一个容器。 因此的目的`CreateAndConfigure`方法的`PhotoService`类是创建一个容器，如果它尚不存在。 从中调用此方法`Application_Start`中的方法*Global.asax*。

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

存储帐户名称和访问密钥存储在`appSettings`的集合*Web.config*文件，并在代码`StorageUtils.StorageAccount`方法使用这些值来生成连接字符串和建立连接：

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

`CreateAndConfigureAsync`方法然后创建一个对象，表示 Blob 服务和一个对象，表示容器 （文件夹） Blob 服务中名为"images":

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

如果容器名为"images"尚不存在-这将是第一次针对新的存储帐户-运行应用程序代码创建容器并设置权限以将其公开，则返回 true。 （默认情况下，新的 blob 容器是专用的和仅有权访问你的存储帐户的用户可以访问。）

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>存储在 Blob 存储中上传的照片

若要上传和保存图像文件，该应用使用`IPhotoService`接口和接口中的一个实现`PhotoService`类。 *PhotoService.cs*文件包含所有应用中的代码修复它与 Blob 服务进行通信。

当用户单击调用以下 MVC 控制器方法**创建 fix It**。 在此代码中，`photoService`的实例是指`PhotoService`类，并`fixittask`的实例是指`FixItTask`实体类，用于存储数据的新任务。

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

`UploadPhotoAsync`中的方法`PhotoService`类将上传的文件存储在 Blob 服务，并返回指向新的 blob 的 URL。

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

如`CreateAndConfigure`方法，该代码连接到存储帐户并创建一个对象，表示"映像"blob 容器，但此处假定该容器已存在。

然后创建要上载的文件扩展名的新 GUID 值连接在一起的图像的唯一标识符：

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

然后该代码使用 blob 容器对象和新的唯一标识符创建一个 blob 对象，哪种文件它，，然后使用 blob 对象存储在 blob 存储中的文件，该值指示该对象上设置属性。

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

最后，它获取 blob 引用的 URL。 此 URL 将存储在数据库中，并可用于修复它网页中显示上传的图像。

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

此 URL 是在数据库中存储为一个 FixItTask 表的列。

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

使用仅在数据库中，URL 和 Blob 存储中的映像，修复其应用以使数据库保持小、 可缩放且成本较低时的映像存储比较便宜，能够处理千吉字节或千万亿字节存储所在。 一个存储帐户可以存储亿字节的 Fix It 照片，您只需为所使用的内容付费。 因此可以开始小付费的 9 美分的第一个千兆字节，并为每个其他千兆字节便士添加更多映像。

### <a name="display-the-uploaded-file"></a>显示上传的文件

显示任务的详细信息时，修复其应用程序将显示上传的图像文件。

![修复与照片任务详细信息](unstructured-blob-storage/_static/image3.png)

若要显示图像，MVC 视图只需是包括`PhotoUrl`HTML 发送到浏览器中的值。 Web 服务器和数据库不使用周期来显示图像，它们仅向图像 URL 提供了几个字节。 在以下 Razor 代码中，`Model`的实例是指`FixItTask`实体类。

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

如果您看一下，显示的页面的 HTML，你会看到直接指向 blob 存储，如下所示中的图像的 URL:

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>总结

您已了解如何修复其应用将映像存储在 Blob 服务和 SQL 数据库中的图像 Url。 使用 Blob 服务使 SQL 数据库不是它否则为可纵向扩展到几乎无限数量的任务，而可以完成而无需编写大量代码要小得多。

中的存储帐户，可以有数百兆兆字节，比 SQL 数据库存储空间，开始每十亿字节 / 月加上较小的事务费用大约 3 个美分价格更便宜的存储成本。 并请记住，您不特别的最大容量，但仅对你实际存储，因此您的应用程序已准备好缩放，但您不特别的所有额外的容量量。

在中[接下来的章节](design-to-survive-failures.md)我们将讨论的云应用程序能够正常处理失败的重要性。

## <a name="resources"></a>资源

有关详细信息，请参阅以下资源：

- [Azure BLOB 存储简介](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。 由 Mike Wood 博客。
- [如何在.NET 中使用 Azure Blob 存储服务](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。 MicrosoftAzure.com 站点上的官方文档。 简要介绍到 blob 存储代码示例显示如何连接到 blob 存储后, 跟创建容器、 上传和下载 blob，等等。
- [防故障： 构建可缩放、 可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 包含 9 个部分由 Ulrich Homann、 Marc Mercuri 和 Mark Simms 的视频系列。 提供高级概念和体系结构原则非常可访问且有趣的方式，来自 Microsoft 客户咨询团队 (CAT) 实际客户体验的情景。 Azure 存储服务和 blob 的讨论，请参阅第 5 开始 35:13。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅附属密钥模式。

> [!div class="step-by-step"]
> [上一页](data-partitioning-strategies.md)
> [下一页](design-to-survive-failures.md)
