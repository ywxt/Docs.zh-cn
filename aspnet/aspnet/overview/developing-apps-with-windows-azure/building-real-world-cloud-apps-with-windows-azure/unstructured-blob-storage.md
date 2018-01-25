---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: "非结构化的 Blob 存储 （使用 Azure 构建真实世界云应用） |Microsoft 文档"
author: MikeWasson
description: "构建真实世界云应用程序与 Azure 的电子书基于由 Scott Guthrie 的演示。 它还说明了 13 模式和实践，他可以..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/30/2015
ms.topic: article
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: 489769533a26c99404c6a5186d66f560385dcffd
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
<a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="f36cc-104">非结构化的 Blob 存储 （使用 Azure 构建真实世界云应用）</span><span class="sxs-lookup"><span data-stu-id="f36cc-104">Unstructured Blob Storage (Building Real-World Cloud Apps with Azure)</span></span>
====================
<span data-ttu-id="f36cc-105">通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://github.com/Rick-Anderson)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="f36cc-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="f36cc-106">[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="f36cc-106">[Download Fix It Project](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="f36cc-107">**构建真实世界云应用程序与 Azure**电子书基于由 Scott Guthrie 的演示。</span><span class="sxs-lookup"><span data-stu-id="f36cc-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="f36cc-108">它还说明了 13 模式和实践，从而帮助你为成功开发适用于云中的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="f36cc-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="f36cc-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="f36cc-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>


<span data-ttu-id="f36cc-110">在前一章中我们将查看分区方案，并且说明了如何修复它应用在 Azure 存储 Blob 服务和 Azure SQL 数据库中的其他任务数据中存储图像。</span><span class="sxs-lookup"><span data-stu-id="f36cc-110">In the previous chapter we looked at partitioning schemes and explained how the Fix It app stores images in the Azure Storage Blob service, and other task data in Azure SQL Database.</span></span> <span data-ttu-id="f36cc-111">本章我们将深入查看 Blob 服务，并显示如何解决它的项目代码中实现。</span><span class="sxs-lookup"><span data-stu-id="f36cc-111">In this chapter we go deeper into the Blob service and show how it's implemented in Fix It project code.</span></span>

## <a name="what-is-blob-storage"></a><span data-ttu-id="f36cc-112">什么是 Blob 存储？</span><span class="sxs-lookup"><span data-stu-id="f36cc-112">What is Blob storage?</span></span>

<span data-ttu-id="f36cc-113">Azure 存储 Blob 服务使您能够在云中存储文件。</span><span class="sxs-lookup"><span data-stu-id="f36cc-113">The Azure Storage Blob service provides a way to store files in the cloud.</span></span> <span data-ttu-id="f36cc-114">Blob 服务具有大量通过将文件存储在本地网络文件系统的优点：</span><span class="sxs-lookup"><span data-stu-id="f36cc-114">The Blob service has a number of advantages over storing files in a local network file system:</span></span>

- <span data-ttu-id="f36cc-115">它是高度可伸缩的。</span><span class="sxs-lookup"><span data-stu-id="f36cc-115">It's highly scalable.</span></span> <span data-ttu-id="f36cc-116">单个存储帐户可以存储[数百个亿字节](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)，并且可有多个存储帐户。</span><span class="sxs-lookup"><span data-stu-id="f36cc-116">A single Storage account can store [hundreds of terabytes](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx), and you can have multiple Storage accounts.</span></span> <span data-ttu-id="f36cc-117">最大的 Azure 客户的一些存储数百个 petabytes。</span><span class="sxs-lookup"><span data-stu-id="f36cc-117">Some of the biggest Azure customers store hundreds of petabytes.</span></span> <span data-ttu-id="f36cc-118">Microsoft SkyDrive 使用 blob 存储。</span><span class="sxs-lookup"><span data-stu-id="f36cc-118">Microsoft SkyDrive uses blob storage.</span></span>
- <span data-ttu-id="f36cc-119">它是持久事务。</span><span class="sxs-lookup"><span data-stu-id="f36cc-119">It's durable.</span></span> <span data-ttu-id="f36cc-120">Blob 服务中存储每个文件自动备份。</span><span class="sxs-lookup"><span data-stu-id="f36cc-120">Every file you store in the Blob service is automatically backed up.</span></span>
- <span data-ttu-id="f36cc-121">它提供了高可用性。</span><span class="sxs-lookup"><span data-stu-id="f36cc-121">It provides high availability.</span></span> <span data-ttu-id="f36cc-122">[SLA for Storage](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409)承诺 99.9%或 99.99%的正常运行时间，根据所选的地域冗余选项。</span><span class="sxs-lookup"><span data-stu-id="f36cc-122">The [SLA for Storage](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) promises 99.9% or 99.99% uptime, depending on which geo-redundancy option you choose.</span></span>
- <span data-ttu-id="f36cc-123">它是 Azure 中，这意味着你只需存储和检索文件，仅为你使用的存储的实际数量付费的平台即服务 (PaaS) 功能和 Azure 会自动负责设置和管理的所有 Vm 和所需的磁盘驱动器服务。</span><span class="sxs-lookup"><span data-stu-id="f36cc-123">It's a platform-as-a-service (PaaS) feature of Azure, which means you just store and retrieve files, paying only for the actual amount of storage you use, and Azure automatically takes care of setting up and managing all of the VMs and disk drives required for the service.</span></span>
- <span data-ttu-id="f36cc-124">通过使用 REST API 或通过使用 API 的编程语言，你可以访问 Blob 服务。</span><span class="sxs-lookup"><span data-stu-id="f36cc-124">You can access the Blob service by using a REST API or by using a programming language API.</span></span> <span data-ttu-id="f36cc-125">Sdk 都适用于.NET、 Java、 Ruby 和其他人。</span><span class="sxs-lookup"><span data-stu-id="f36cc-125">SDKs are available for .NET, Java, Ruby, and others.</span></span>
- <span data-ttu-id="f36cc-126">文件存储在 Blob 服务中时，你可以轻松地使其公开可通过 Internet。</span><span class="sxs-lookup"><span data-stu-id="f36cc-126">When you store a file in the Blob service, you can easily make it publicly available over the Internet.</span></span>
- <span data-ttu-id="f36cc-127">你可以保护服务，以便他们可以访问只能由经过授权的用户，Blob 中的文件，或者可以提供使它们可向某人仅为有限的时间段的临时访问令牌。</span><span class="sxs-lookup"><span data-stu-id="f36cc-127">You can secure files in the Blob service so they can accessed only by authorized users, or you can provide temporary access tokens that makes them available to someone only for a limited period of time.</span></span>

<span data-ttu-id="f36cc-128">每当你正在 azure 中生成应用程序并且你想要存储大量数据，在本地环境中将转中文件-如图像、 视频、 Pdf、 电子表格等-请考虑 Blob 服务。</span><span class="sxs-lookup"><span data-stu-id="f36cc-128">Anytime you're building an app for Azure and you want to store a lot of data that in an on-premises environment would go in files -- such as images, videos, PDFs, spreadsheets, etc. -- consider the Blob service.</span></span>

## <a name="creating-a-storage-account"></a><span data-ttu-id="f36cc-129">创建存储帐户</span><span class="sxs-lookup"><span data-stu-id="f36cc-129">Creating a Storage account</span></span>

<span data-ttu-id="f36cc-130">若要开始使用 Blob 服务在 Azure 中创建存储帐户。</span><span class="sxs-lookup"><span data-stu-id="f36cc-130">To get started with the Blob service you create a Storage account in Azure.</span></span> <span data-ttu-id="f36cc-131">在门户中，单击**新建** -- **Data Services** -- **存储** -- **快速创建**，然后输入一个 URL，数据中心位置。</span><span class="sxs-lookup"><span data-stu-id="f36cc-131">In the portal, click **New** -- **Data Services** -- **Storage** -- **Quick Create**, and then enter a URL and a data center location.</span></span> <span data-ttu-id="f36cc-132">数据中心位置应与你的 web 应用相同。</span><span class="sxs-lookup"><span data-stu-id="f36cc-132">The data center location should be the same as your web app.</span></span>

![创建存储帐户](unstructured-blob-storage/_static/image1.png)

<span data-ttu-id="f36cc-134">你想要存储的内容，并且如果你选择选取主区域[异地复制](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage)选项，Azure 在不同的数据中心在国家/地区的另一个区域中创建的所有数据的副本。</span><span class="sxs-lookup"><span data-stu-id="f36cc-134">You pick the primary region where you want to store the content, and if you choose the [geo-replication](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) option, Azure creates replicas of all your data in a different data center in another region of the country.</span></span> <span data-ttu-id="f36cc-135">例如，如果你选择西方美国数据中心，它还将到美国西部数据中心，但在后台 Azure 文件存储时将其复制到其他美国数据中心之一。</span><span class="sxs-lookup"><span data-stu-id="f36cc-135">For example, if you choose the Western US data center, when you store a file it goes to the Western US data center, but in the background Azure also copies it to one of the other US data centers.</span></span> <span data-ttu-id="f36cc-136">如果在一个国家 / 地区在发生灾难，你的数据是仍安全的。</span><span class="sxs-lookup"><span data-stu-id="f36cc-136">If a disaster happens in one region of the country, your data is still safe.</span></span>

<span data-ttu-id="f36cc-137">Azure 不会跨地缘政治边界复制数据： 如果你的主位置是在美国，你的文件将仅复制到美国; 内的另一个区域如果您的主要位置，澳大利亚你的文件将仅复制到在澳大利亚的另一个数据中心。</span><span class="sxs-lookup"><span data-stu-id="f36cc-137">Azure won't replicate data across geo-political boundaries: if your primary location is in the U.S., your files are only replicated to another region within the U.S.; if your primary location is Australia, your files are only replicated to another data center in Australia.</span></span>

<span data-ttu-id="f36cc-138">当然，你还可以创建存储帐户通过从脚本中执行命令如我们前面看到的。</span><span class="sxs-lookup"><span data-stu-id="f36cc-138">Of course, you can also create a Storage account by executing commands from a script, as we saw earlier.</span></span> <span data-ttu-id="f36cc-139">下面是 Windows PowerShell 命令以创建存储帐户：</span><span class="sxs-lookup"><span data-stu-id="f36cc-139">Here's a Windows PowerShell command to create a Storage account:</span></span>

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

<span data-ttu-id="f36cc-140">存储帐户之后，你可以立即开始将文件存储在 Blob 服务。</span><span class="sxs-lookup"><span data-stu-id="f36cc-140">Once you have a Storage account, you can immediately start storing files in the Blob service.</span></span>

## <a name="using-blob-storage-in-the-fix-it-app"></a><span data-ttu-id="f36cc-141">修复它应用中使用 Blob 存储</span><span class="sxs-lookup"><span data-stu-id="f36cc-141">Using Blob storage in the Fix It app</span></span>

<span data-ttu-id="f36cc-142">修复它应用允许你上载照片。</span><span class="sxs-lookup"><span data-stu-id="f36cc-142">The Fix It app enables you to upload photos.</span></span>

![创建修复它任务](unstructured-blob-storage/_static/image2.png)

<span data-ttu-id="f36cc-144">当你单击**创建 FixIt**，应用程序将指定的图像文件上载并将其存储在 Blob 服务。</span><span class="sxs-lookup"><span data-stu-id="f36cc-144">When you click **Create the FixIt**, the application uploads the specified image file and stores it in the Blob service.</span></span>

### <a name="set-up-the-blob-container"></a><span data-ttu-id="f36cc-145">设置 Blob 容器</span><span class="sxs-lookup"><span data-stu-id="f36cc-145">Set up the Blob container</span></span>

<span data-ttu-id="f36cc-146">若要将文件存储在您需要的 Blob 服务*容器*以将其存储在。</span><span class="sxs-lookup"><span data-stu-id="f36cc-146">In order to store a file in the Blob service you need a *container* to store it in.</span></span> <span data-ttu-id="f36cc-147">Blob 服务容器对应于文件系统文件夹。</span><span class="sxs-lookup"><span data-stu-id="f36cc-147">A Blob service container corresponds to a file system folder.</span></span> <span data-ttu-id="f36cc-148">我们回顾了中的环境创建脚本[使一切自动化章](automate-everything.md)创建存储帐户中，但它们不创建容器。</span><span class="sxs-lookup"><span data-stu-id="f36cc-148">The environment creation scripts that we reviewed in the [Automate Everything chapter](automate-everything.md) create the Storage account, but they don't create a container.</span></span> <span data-ttu-id="f36cc-149">因此的用途`CreateAndConfigure`方法`PhotoService`类是创建一个容器，如果它尚不存在。</span><span class="sxs-lookup"><span data-stu-id="f36cc-149">So the purpose of the `CreateAndConfigure` method of the `PhotoService` class is to create a container if it doesn't already exist.</span></span> <span data-ttu-id="f36cc-150">此方法调用从`Application_Start`中的方法*Global.asax*。</span><span class="sxs-lookup"><span data-stu-id="f36cc-150">This method is called from the `Application_Start` method in *Global.asax*.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

<span data-ttu-id="f36cc-151">存储帐户名称和访问密钥存储在`appSettings`集合*Web.config*文件中，并在代码`StorageUtils.StorageAccount`方法使用这些值来生成连接字符串和建立连接：</span><span class="sxs-lookup"><span data-stu-id="f36cc-151">The storage account name and access key are stored in the `appSettings` collection of the *Web.config* file, and code in the `StorageUtils.StorageAccount` method uses those values to build a connection string and establish a connection:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

<span data-ttu-id="f36cc-152">`CreateAndConfigureAsync`方法会创建一个表示 Blob 服务中，对象和一个对象，表示容器 （文件夹） Blob 服务中名为"images":</span><span class="sxs-lookup"><span data-stu-id="f36cc-152">The `CreateAndConfigureAsync` method then creates an object that represents the Blob service, and an object that represents a container (folder) named "images" in the Blob service:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

<span data-ttu-id="f36cc-153">如果容器名为"images"尚不存在-这将是第一次针对新的存储帐户-运行应用程序代码创建的容器，并将设置设为公开的权限，则返回 true。</span><span class="sxs-lookup"><span data-stu-id="f36cc-153">If a container named "images" doesn't exist yet -- which will be true the first time you run the app against a new storage account -- the code creates the container and sets permissions to make it public.</span></span> <span data-ttu-id="f36cc-154">（默认情况下，新的 blob 容器是私有，可访问仅向用户有权访问你的存储帐户。）</span><span class="sxs-lookup"><span data-stu-id="f36cc-154">(By default, new blob containers are private and are accessible only to users who have permission to access your storage account.)</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a><span data-ttu-id="f36cc-155">在 Blob 存储中存储的已上载的照片</span><span class="sxs-lookup"><span data-stu-id="f36cc-155">Store the uploaded photo in Blob storage</span></span>

<span data-ttu-id="f36cc-156">上载和保存该图像文件，应用程序使用`IPhotoService`接口和一个实现中的接口`PhotoService`类。</span><span class="sxs-lookup"><span data-stu-id="f36cc-156">To upload and save the image file, the app uses an `IPhotoService` interface and an implementation of the interface in the `PhotoService` class.</span></span> <span data-ttu-id="f36cc-157">*PhotoService.cs*文件包含所有应用中的代码修复它与 Blob 服务进行通信。</span><span class="sxs-lookup"><span data-stu-id="f36cc-157">The *PhotoService.cs* file contains all of the code in the Fix It app that communicates with the Blob service.</span></span>

<span data-ttu-id="f36cc-158">下面的 MVC 控制器方法调用当用户单击**创建 FixIt**。</span><span class="sxs-lookup"><span data-stu-id="f36cc-158">The following MVC controller method is called when the user clicks **Create the FixIt**.</span></span> <span data-ttu-id="f36cc-159">在此代码中，`photoService`的实例是指`PhotoService`类，和`fixittask`的实例是指`FixItTask`将新任务的数据存储的实体类。</span><span class="sxs-lookup"><span data-stu-id="f36cc-159">In this code, `photoService` refers to an instance of the `PhotoService` class, and `fixittask` refers to an instance of the `FixItTask` entity class that stores data for a new task.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

<span data-ttu-id="f36cc-160">`UploadPhotoAsync`中的方法`PhotoService`类将上载的文件存储在 Blob 服务，并返回指向新的 blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="f36cc-160">The `UploadPhotoAsync` method in the `PhotoService` class stores the uploaded file in the Blob service and returns a URL that points to the new blob.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

<span data-ttu-id="f36cc-161">作为 in`CreateAndConfigure`方法，代码连接到存储帐户，然后创建一个表示对象的"映像"blob 容器，但此处假定该容器已存在。</span><span class="sxs-lookup"><span data-stu-id="f36cc-161">As in the `CreateAndConfigure` method, the code connects to the storage account and creates an object that represents the "images" blob container, except here it assumes the container already exists.</span></span>

<span data-ttu-id="f36cc-162">然后它将创建要由新的 GUID 值与文件扩展名串联上载的图像的唯一标识符：</span><span class="sxs-lookup"><span data-stu-id="f36cc-162">Then it creates a unique identifier for the image about to be uploaded, by concatenating a new GUID value with the file extension:</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

<span data-ttu-id="f36cc-163">然后的代码使用 blob 容器对象和新的唯一标识符来创建 blob 对象，则在哪种文件它，，然后使用 blob 对象存储在 blob 存储中的文件，该值指示该对象上设置属性。</span><span class="sxs-lookup"><span data-stu-id="f36cc-163">The code then uses the blob container object and the new unique identifier to create a blob object, sets an attribute on that object indicating what kind of file it is, and then uses the blob object to store the file in blob storage.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

<span data-ttu-id="f36cc-164">最后，它获取引用 blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="f36cc-164">Finally, it gets a URL that references the blob.</span></span> <span data-ttu-id="f36cc-165">此 URL 将存储在数据库和可以用于解决它的网页中显示已上载的图像。</span><span class="sxs-lookup"><span data-stu-id="f36cc-165">This URL will be stored in the database and can be used in Fix It web pages to display the uploaded image.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

<span data-ttu-id="f36cc-166">此 URL 作为一个 FixItTask 表的列存储在数据库中。</span><span class="sxs-lookup"><span data-stu-id="f36cc-166">This URL is stored in the database as one of the columns of the FixItTask table.</span></span>

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

<span data-ttu-id="f36cc-167">使用仅在数据库中，URL 和 Blob 存储中的映像中，修复它应用以使数据库保持小、 可伸缩且成本较低时其中存储为比较便宜，能够处理兆兆字节乃至 petabytes 存储映像。</span><span class="sxs-lookup"><span data-stu-id="f36cc-167">With only the URL in the database, and images in Blob storage, the Fix It app keeps the database small, scalable, and inexpensive, while the images are stored where storage is cheap and capable of handling terabytes or petabytes.</span></span> <span data-ttu-id="f36cc-168">一个存储帐户可以存储数百万亿字节的修复它照片，而且你只需为你的使用付费。</span><span class="sxs-lookup"><span data-stu-id="f36cc-168">One storage account can store hundreds of terabytes of Fix It photos, and you only pay for what you use.</span></span> <span data-ttu-id="f36cc-169">因此你可以首先小付费的 9 美分的第一个千兆字节，并为其他 /gb 便士添加更多的图像。</span><span class="sxs-lookup"><span data-stu-id="f36cc-169">So you can start off small paying 9 cents for the first gigabyte, and add more images for pennies per additional gigabyte.</span></span>

### <a name="display-the-uploaded-file"></a><span data-ttu-id="f36cc-170">显示已上载的文件</span><span class="sxs-lookup"><span data-stu-id="f36cc-170">Display the uploaded file</span></span>

<span data-ttu-id="f36cc-171">显示的任务的详细信息时，修复它应用程序将显示已上载的图像文件。</span><span class="sxs-lookup"><span data-stu-id="f36cc-171">The Fix It application displays the uploaded image file when it displays details for a task.</span></span>

![修复它的照片的任务详细信息](unstructured-blob-storage/_static/image3.png)

<span data-ttu-id="f36cc-173">若要显示图像，所有的 MVC 视图都只需是包括`PhotoUrl`HTML 发送到浏览器中的值。</span><span class="sxs-lookup"><span data-stu-id="f36cc-173">To display the image, all the MVC view has to do is include the `PhotoUrl` value in the HTML sent to the browser.</span></span> <span data-ttu-id="f36cc-174">Web 服务器和数据库不会使用循环显示图像，它们仅向图像 URL 提供了几个字节。</span><span class="sxs-lookup"><span data-stu-id="f36cc-174">The web server and the database are not using cycles to display the image, they are only serving up a few bytes to the image URL.</span></span> <span data-ttu-id="f36cc-175">在以下 Razor 代码中，`Model`的实例是指`FixItTask`实体类。</span><span class="sxs-lookup"><span data-stu-id="f36cc-175">In the following Razor code, `Model` refers to an instance of the `FixItTask` entity class.</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

<span data-ttu-id="f36cc-176">如果你查看上显示的页的 HTML，你将看到直接指向中 blob 存储，如下所示的图像的 URL:</span><span class="sxs-lookup"><span data-stu-id="f36cc-176">If you look at the HTML of the page that displays, you see the URL pointing directly to the image in blob storage, something like this:</span></span>

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a><span data-ttu-id="f36cc-177">摘要</span><span class="sxs-lookup"><span data-stu-id="f36cc-177">Summary</span></span>

<span data-ttu-id="f36cc-178">你已了解如何解决它应用将映像存储在 Blob 服务和映像 Url 仅在 SQL 数据库中。</span><span class="sxs-lookup"><span data-stu-id="f36cc-178">You've seen how the Fix It app stores images in the Blob service and only image URLs in the SQL database.</span></span> <span data-ttu-id="f36cc-179">使用 Blob 服务使 SQL 数据库不是它否则为有可能增加到几乎无限数量的任务，而可以完成而无需编写大量的代码要小得多。</span><span class="sxs-lookup"><span data-stu-id="f36cc-179">Using the Blob service keeps the SQL database much smaller than it otherwise would be, makes it possible to scale up to an almost unlimited number of tasks, and can be done without writing a lot of code.</span></span>

<span data-ttu-id="f36cc-180">你可以在存储帐户，有数百个亿字节而存储成本是价格比 SQL 数据库存储，开始大约 3 美分 /gb 情况下，每个月加上较小的事务的费用更便宜。</span><span class="sxs-lookup"><span data-stu-id="f36cc-180">You can have hundreds of terabytes in a storage account, and the storage cost is much less expensive than SQL Database storage, starting at about 3 cents per gigabyte per month plus a small transaction charge.</span></span> <span data-ttu-id="f36cc-181">和，请记住，您不特别的最大容量，但仅针对你实际上存储，因此你的应用已准备好缩放但您不特别所有这些额外的容量的量。</span><span class="sxs-lookup"><span data-stu-id="f36cc-181">And keep in mind that you're not paying for the maximum capacity but only for the amount you actually store, so your app is ready to scale but you're not paying for all that extra capacity.</span></span>

<span data-ttu-id="f36cc-182">在[下一章](design-to-survive-failures.md)我们将讨论使云应用程序能够正常处理失败的重要性。</span><span class="sxs-lookup"><span data-stu-id="f36cc-182">In the [next chapter](design-to-survive-failures.md) we'll talk about the importance of making a cloud app capable of gracefully handling failures.</span></span>

## <a name="resources"></a><span data-ttu-id="f36cc-183">资源</span><span class="sxs-lookup"><span data-stu-id="f36cc-183">Resources</span></span>

<span data-ttu-id="f36cc-184">有关详细信息请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="f36cc-184">For more information see the following resources:</span></span>

- <span data-ttu-id="f36cc-185">[Azure BLOB 存储空间简介](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/)。</span><span class="sxs-lookup"><span data-stu-id="f36cc-185">[An Introduction to Azure BLOB Storage](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/).</span></span> <span data-ttu-id="f36cc-186">Mike 木材的博客。</span><span class="sxs-lookup"><span data-stu-id="f36cc-186">Blog by Mike Wood.</span></span>
- <span data-ttu-id="f36cc-187">[如何在.NET 中使用 Azure Blob 存储服务](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)。</span><span class="sxs-lookup"><span data-stu-id="f36cc-187">[How to use the Azure Blob Storage Service in .NET](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs).</span></span> <span data-ttu-id="f36cc-188">MicrosoftAzure.com 网站上的正式文档。</span><span class="sxs-lookup"><span data-stu-id="f36cc-188">Official documentation on the MicrosoftAzure.com site.</span></span> <span data-ttu-id="f36cc-189">简要介绍到 blob 存储跟代码示例演示如何连接到 blob 存储创建容器、 上载和下载 blob，等等。</span><span class="sxs-lookup"><span data-stu-id="f36cc-189">A brief introduction to blob storage followed by code examples showing how to connect to blob storage, create containers, upload and download blobs, etc.</span></span>
- <span data-ttu-id="f36cc-190">[防故障： 构建可扩展、 有弹性的云服务](https://channel9.msdn.com/Series/FailSafe)。</span><span class="sxs-lookup"><span data-stu-id="f36cc-190">[FailSafe: Building Scalable, Resilient Cloud Services](https://channel9.msdn.com/Series/FailSafe).</span></span> <span data-ttu-id="f36cc-191">通过 Ulrich Homann、 Marc Mercuri 和 Mark Simms 九一部分视频系列。</span><span class="sxs-lookup"><span data-stu-id="f36cc-191">Nine-part video series by Ulrich Homann, Marc Mercuri, and Mark Simms.</span></span> <span data-ttu-id="f36cc-192">高级概念和体系结构原理以非常可访问且有趣方式，提供与 Microsoft 客户咨询团队 (CAT) 体验与实际客户从绘制的情景。</span><span class="sxs-lookup"><span data-stu-id="f36cc-192">Presents high-level concepts and architectural principles in a very accessible and interesting way, with stories drawn from Microsoft Customer Advisory Team (CAT) experience with actual customers.</span></span> <span data-ttu-id="f36cc-193">有关 Azure 存储服务和 blob 的讨论，请参阅段 5 开始 35:13。</span><span class="sxs-lookup"><span data-stu-id="f36cc-193">For a discussion of Azure Storage service and blobs, see episode 5 starting at 35:13.</span></span>
- <span data-ttu-id="f36cc-194">[Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f36cc-194">[Microsoft Patterns and Practices - Azure Guidance](https://msdn.microsoft.com/library/dn568099.aspx).</span></span> <span data-ttu-id="f36cc-195">请参阅 Valet 密钥模式。</span><span class="sxs-lookup"><span data-stu-id="f36cc-195">See Valet Key pattern.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="f36cc-196">[上一页](data-partitioning-strategies.md)
[下一页](design-to-survive-failures.md)</span><span class="sxs-lookup"><span data-stu-id="f36cc-196">[Previous](data-partitioning-strategies.md)
[Next](design-to-survive-failures.md)</span></span>
