---
title: ASP.NET Core 中的图像标记帮助程序
author: pkellner
description: 演示如何使用图像标记帮助程序
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: 6aa9175f873c4ea62e0319c812e5312cd3331141
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="image-tag-helper-in-aspnet-core"></a><span data-ttu-id="70f18-103">ASP.NET Core 中的图像标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="70f18-103">Image Tag Helper in ASP.NET Core</span></span>

<span data-ttu-id="70f18-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="70f18-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="70f18-105">图像标记帮助程序可增强 `img` (`<img>`) 标记。</span><span class="sxs-lookup"><span data-stu-id="70f18-105">The Image Tag Helper enhances the `img` (`<img>`) tag.</span></span> <span data-ttu-id="70f18-106">它需要 `src` 标记以及 `boolean` 属性 `asp-append-version`。</span><span class="sxs-lookup"><span data-stu-id="70f18-106">It requires a `src` tag as well as the `boolean` attribute `asp-append-version`.</span></span>

<span data-ttu-id="70f18-107">如果图像源 (`src`) 是主机 Web 服务器上的静态文件，则会向图像源追加一个唯一缓存清除字符串作为查询参数。</span><span class="sxs-lookup"><span data-stu-id="70f18-107">If the image source (`src`) is a static file on the host web server, a unique cache busting string is appended as a query parameter to the image source.</span></span> <span data-ttu-id="70f18-108">这可确保，如果主机 Web 服务器上的文件发生更改，将生成包含已更新请求参数的唯一请求 URL。</span><span class="sxs-lookup"><span data-stu-id="70f18-108">This ensures that if the file on the host web server changes, a unique request URL is generated that includes the updated request parameter.</span></span> <span data-ttu-id="70f18-109">缓存清除字符串是一个唯一值，表示静态图像文件的哈希。</span><span class="sxs-lookup"><span data-stu-id="70f18-109">The cache busting string is a unique value representing the hash of the static image file.</span></span>

<span data-ttu-id="70f18-110">如果图像源 (`src`) 不是静态文件（例如远程 URL，或者服务器上不存在该文件），则生成的 `<img>` 标记的 `src` 属性不带缓存清除查询字符串参数。</span><span class="sxs-lookup"><span data-stu-id="70f18-110">If the image source (`src`) isn't a static file (for example a remote URL or the file doesn't exist on the server), the `<img>` tag's `src` attribute is generated with no cache busting query string parameter.</span></span>

## <a name="image-tag-helper-attributes"></a><span data-ttu-id="70f18-111">图像标记帮助程序属性</span><span class="sxs-lookup"><span data-stu-id="70f18-111">Image Tag Helper Attributes</span></span>


### <a name="asp-append-version"></a><span data-ttu-id="70f18-112">asp-append-version</span><span class="sxs-lookup"><span data-stu-id="70f18-112">asp-append-version</span></span>

<span data-ttu-id="70f18-113">与 `src` 属性一起指定时，会调用图像标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="70f18-113">When specified along with a `src` attribute, the Image Tag Helper is invoked.</span></span>

<span data-ttu-id="70f18-114">有效的 `img` 标记帮助程序示例为：</span><span class="sxs-lookup"><span data-stu-id="70f18-114">An example of a valid `img` tag helper is:</span></span>

```cshtml
<img src="~/images/asplogo.png" 
    asp-append-version="true"  />
```

<span data-ttu-id="70f18-115">如果目录 *..wwwroot/images/asplogo.png* 中存在静态文件，生成的 html 与下面类似（哈希有所不同）：</span><span class="sxs-lookup"><span data-stu-id="70f18-115">If the static file exists in the directory *..wwwroot/images/asplogo.png* the generated html is similar to the following (the hash will be different):</span></span>

```html
<img 
    src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM"/>
```

<span data-ttu-id="70f18-116">分配给参数 `v` 的值是磁盘上的文件的哈希值。</span><span class="sxs-lookup"><span data-stu-id="70f18-116">The value assigned to the parameter `v` is the hash value of the file on disk.</span></span> <span data-ttu-id="70f18-117">如果 Web 服务器无法获取对所引用的静态文件的读取访问权限，则不会向 `src` 属性添加 `v` 参数。</span><span class="sxs-lookup"><span data-stu-id="70f18-117">If the web server is unable to obtain read access to the static file referenced,  no `v` parameters is added to the `src` attribute.</span></span>

- - -

### <a name="src"></a><span data-ttu-id="70f18-118">src</span><span class="sxs-lookup"><span data-stu-id="70f18-118">src</span></span>

<span data-ttu-id="70f18-119">若要激活图像标记帮助程序，`<img>` 元素需要有 src 属性。</span><span class="sxs-lookup"><span data-stu-id="70f18-119">To activate the Image Tag Helper, the src attribute is required on the `<img>` element.</span></span> 

> [!NOTE]
> <span data-ttu-id="70f18-120">图像标记帮助程序使用本地 Web 服务器上的 `Cache` 提供程序来存储给定文件的已计算 `Sha512`。</span><span class="sxs-lookup"><span data-stu-id="70f18-120">The Image Tag Helper uses the `Cache` provider on the local web server to store the calculated `Sha512` of a given file.</span></span> <span data-ttu-id="70f18-121">如果再次请求该文件，则不需要重新计算 `Sha512`。</span><span class="sxs-lookup"><span data-stu-id="70f18-121">If the file is requested again the `Sha512` doesn't need to be recalculated.</span></span> <span data-ttu-id="70f18-122">当计算该文件的 `Sha512` 时，附加到该文件的文件观察程序会让 Cache 失效。</span><span class="sxs-lookup"><span data-stu-id="70f18-122">The Cache is invalidated by a file watcher that's attached to the file when the file's `Sha512` is calculated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="70f18-123">其他资源</span><span class="sxs-lookup"><span data-stu-id="70f18-123">Additional resources</span></span>

* <xref:performance/caching/memory>
