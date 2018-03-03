---
title: "迁移配置"
author: ardalis
description: 
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: migration/configuration
ms.openlocfilehash: e1ee582072c88542565c5cb860e157afe137f9f0
ms.sourcegitcommit: 7ac15eaae20b6d70e65f3650af050a7880115cbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2018
---
# <a name="migrating-configuration"></a><span data-ttu-id="8c6ea-102">迁移配置</span><span class="sxs-lookup"><span data-stu-id="8c6ea-102">Migrating Configuration</span></span>

<span data-ttu-id="8c6ea-103">作者：[Steve Smith](https://ardalis.com/) 和 [Scott Addie](https://scottaddie.com)</span><span class="sxs-lookup"><span data-stu-id="8c6ea-103">By [Steve Smith](https://ardalis.com/) and [Scott Addie](https://scottaddie.com)</span></span>

<span data-ttu-id="8c6ea-104">在以前的文章中，我们就已着手[将 ASP.NET MVC 项目迁移到 ASP.NET 核心 MVC](mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-104">In the previous article, we began [migrating an ASP.NET MVC project to ASP.NET Core MVC](mvc.md).</span></span> <span data-ttu-id="8c6ea-105">在本文中，我们将迁移配置。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-105">In this article, we migrate configuration.</span></span>

<span data-ttu-id="8c6ea-106">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples)（[如何下载](xref:tutorials/index#how-to-download-a-sample)）</span><span class="sxs-lookup"><span data-stu-id="8c6ea-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/migration/configuration/samples) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="setup-configuration"></a><span data-ttu-id="8c6ea-107">安装程序配置</span><span class="sxs-lookup"><span data-stu-id="8c6ea-107">Setup Configuration</span></span>

<span data-ttu-id="8c6ea-108">ASP.NET 核心不再使用*Global.asax*和*web.config* ASP.NET 的早期版本使用的文件。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-108">ASP.NET Core no longer uses the *Global.asax* and *web.config* files that previous versions of ASP.NET utilized.</span></span> <span data-ttu-id="8c6ea-109">在 ASP.NET 的早期版本中，应用程序的启动逻辑放入`Application_StartUp`方法内的*Global.asax*。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-109">In earlier versions of ASP.NET, application startup logic was placed in an `Application_StartUp` method within *Global.asax*.</span></span> <span data-ttu-id="8c6ea-110">更高版本，在 ASP.NET MVC *Startup.cs*项目; 的根目录中包含文件和应用程序启动时调用它。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-110">Later, in ASP.NET MVC, a *Startup.cs* file was included in the root of the project; and, it was called when the application started.</span></span> <span data-ttu-id="8c6ea-111">ASP.NET 核心已完全采用这种方法，通过将中的所有启动逻辑*Startup.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-111">ASP.NET Core has adopted this approach completely by placing all startup logic in the *Startup.cs* file.</span></span>

<span data-ttu-id="8c6ea-112">*Web.config*还在 ASP.NET Core 替换文件。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-112">The *web.config* file has also been replaced in ASP.NET Core.</span></span> <span data-ttu-id="8c6ea-113">配置本身现在可以配置，作为应用程序启动过程中所述的一部分*Startup.cs*。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-113">Configuration itself can now be configured, as part of the application startup procedure described in *Startup.cs*.</span></span> <span data-ttu-id="8c6ea-114">配置仍然可以利用 XML 文件，但通常 ASP.NET 核心项目将置于配置值的 JSON 格式文件，如*appsettings.json*。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-114">Configuration can still utilize XML files, but typically ASP.NET Core projects will place configuration values in a JSON-formatted file, such as *appsettings.json*.</span></span> <span data-ttu-id="8c6ea-115">ASP.NET 核心配置系统可以方便地访问环境变量，可以提供[更安全、 极其可靠的位置](xref:security/app-secrets)特定于环境的值。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-115">ASP.NET Core's configuration system can also easily access environment variables, which can provide a [more secure and robust location](xref:security/app-secrets) for environment-specific values.</span></span> <span data-ttu-id="8c6ea-116">这是针对如连接字符串和不应签入源代码管理的 API 密钥的机密尤其如此。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-116">This is especially true for secrets like connection strings and API keys that shouldn't be checked into source control.</span></span> <span data-ttu-id="8c6ea-117">请参阅[配置](xref:fundamentals/configuration/index)若要了解有关 ASP.NET 核心中配置的详细信息。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-117">See [Configuration](xref:fundamentals/configuration/index) to learn more about configuration in ASP.NET Core.</span></span>

<span data-ttu-id="8c6ea-118">有关本文中，我们开始使用中的部分迁移 ASP.NET Core 项目[上一篇文章](mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-118">For this article, we are starting with the partially-migrated ASP.NET Core project from [the previous article](mvc.md).</span></span> <span data-ttu-id="8c6ea-119">要设置配置中添加以下构造函数和属性*Startup.cs*文件位于项目根目录中：</span><span class="sxs-lookup"><span data-stu-id="8c6ea-119">To setup configuration, add the following constructor and property to the *Startup.cs* file located in the root of the project:</span></span>

[!code-csharp[](configuration/samples/WebApp1/src/WebApp1/Startup.cs?range=11-21)]

<span data-ttu-id="8c6ea-120">请注意，此时， *Startup.cs*文件将无法编译，因为我们仍需要将以下内容添加`using`语句：</span><span class="sxs-lookup"><span data-stu-id="8c6ea-120">Note that at this point, the *Startup.cs* file won't compile, as we still need to add the following `using` statement:</span></span>

```csharp
using Microsoft.Extensions.Configuration;
```

<span data-ttu-id="8c6ea-121">添加*appsettings.json*使用合适的项目模板项目的根目录的文件：</span><span class="sxs-lookup"><span data-stu-id="8c6ea-121">Add an *appsettings.json* file to the root of the project using the appropriate item template:</span></span>

![添加 AppSettings JSON](configuration/_static/add-appsettings-json.png)

## <a name="migrate-configuration-settings-from-webconfig"></a><span data-ttu-id="8c6ea-123">将配置设置迁移从 web.config</span><span class="sxs-lookup"><span data-stu-id="8c6ea-123">Migrate Configuration Settings from web.config</span></span>

<span data-ttu-id="8c6ea-124">我们的 ASP.NET MVC 项目包含中的所需的数据库连接字符串*web.config*中`<connectionStrings>`元素。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-124">Our ASP.NET MVC project included the required database connection string in *web.config*, in the `<connectionStrings>` element.</span></span> <span data-ttu-id="8c6ea-125">在我们 ASP.NET Core 项目中，我们将存储此信息在*appsettings.json*文件。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-125">In our ASP.NET Core project, we are going to store this information in the *appsettings.json* file.</span></span> <span data-ttu-id="8c6ea-126">打开*appsettings.json*，并记下它已包含以下：</span><span class="sxs-lookup"><span data-stu-id="8c6ea-126">Open *appsettings.json*, and note that it already includes the following:</span></span>

[!code-json[](../migration/configuration/samples/WebApp1/src/WebApp1/appsettings.json?highlight=4)]


<span data-ttu-id="8c6ea-127">在突出显示的行将上面所示，将更改从数据库的名称**_CHANGE_ME**为你的数据库的名称。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-127">In the highlighted line depicted above, change the name of the database from **_CHANGE_ME** to the name of your database.</span></span>

## <a name="summary"></a><span data-ttu-id="8c6ea-128">摘要</span><span class="sxs-lookup"><span data-stu-id="8c6ea-128">Summary</span></span>

<span data-ttu-id="8c6ea-129">ASP.NET 核心将置于单个文件，在其中的必要的服务和依赖项可以定义和配置应用程序的所有启动逻辑。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-129">ASP.NET Core places all startup logic for the application in a single file, in which the necessary services and dependencies can be defined and configured.</span></span> <span data-ttu-id="8c6ea-130">它将替换*web.config*与一种灵活的配置功能，可以利用多种文件格式，例如 JSON，以及环境变量的文件。</span><span class="sxs-lookup"><span data-stu-id="8c6ea-130">It replaces the *web.config* file with a flexible configuration feature that can leverage a variety of file formats, such as JSON, as well as environment variables.</span></span>
