---
title: "图像标记帮助器 |Microsoft 文档"
author: pkellner
description: "演示如何使用图像标记帮助器"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/image-tag-helper
ms.openlocfilehash: d0857e1926c341b2357bc824fa379c4fc30affbc
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="imagetaghelper"></a><span data-ttu-id="0e7a4-103">ImageTagHelper</span><span class="sxs-lookup"><span data-stu-id="0e7a4-103">ImageTagHelper</span></span>

<span data-ttu-id="0e7a4-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="0e7a4-104">By [Peter Kellner](http://peterkellner.net)</span></span> 

<span data-ttu-id="0e7a4-105">图像标记帮助程序增强了`img`(`<img>`) 标记。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-105">The Image Tag Helper enhances the `img` (`<img>`) tag.</span></span> <span data-ttu-id="0e7a4-106">它需要`src`标记以及`boolean`属性`asp-append-version`。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-106">It requires a `src` tag as well as the `boolean` attribute `asp-append-version`.</span></span>

<span data-ttu-id="0e7a4-107">如果图像源 (`src`) 文件是静态文件在主机 web 服务器上，清除功能字符串的唯一缓存追加作为图像源的查询参数。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-107">If the image source (`src`) is a static file on the host web server, a unique cache busting string is appended as a query parameter to the image source.</span></span> <span data-ttu-id="0e7a4-108">这可确保，如果主机 web 服务器上的文件发生更改，将会生成唯一的请求 URL 包含更新的请求参数。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-108">This ensures that if the file on the host web server changes, a unique request URL is generated that includes the updated request parameter.</span></span> <span data-ttu-id="0e7a4-109">清除功能字符串缓存是表示静态图像文件的哈希的唯一值。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-109">The cache busting string is a unique value representing the hash of the static image file.</span></span>

<span data-ttu-id="0e7a4-110">如果图像源 (`src`) 不是静态文件 （例如远程 URL 或文件服务器不存在），`<img>`标记的`src`与清除功能查询字符串参数不缓存生成的属性。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-110">If the image source (`src`) isn't a static file (for example a remote URL or the file doesn't exist on the server), the `<img>` tag's `src` attribute is generated with no cache busting query string parameter.</span></span>

## <a name="image-tag-helper-attributes"></a><span data-ttu-id="0e7a4-111">图像标记帮助器属性</span><span class="sxs-lookup"><span data-stu-id="0e7a4-111">Image Tag Helper Attributes</span></span>


### <a name="asp-append-version"></a><span data-ttu-id="0e7a4-112">asp-append-version</span><span class="sxs-lookup"><span data-stu-id="0e7a4-112">asp-append-version</span></span>

<span data-ttu-id="0e7a4-113">指定与时`src`，都会调用特性，图像标记帮助器。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-113">When specified along with a `src` attribute, the Image Tag Helper is invoked.</span></span>

<span data-ttu-id="0e7a4-114">一个有效的示例`img`标记帮助程序是：</span><span class="sxs-lookup"><span data-stu-id="0e7a4-114">An example of a valid `img` tag helper is:</span></span>

```cshtml
<img src="~/images/asplogo.png" 
    asp-append-version="true"  />
```

<span data-ttu-id="0e7a4-115">如果静态文件存在于目录*...wwwroot/images/asplogo.png*生成的 html 是类似于以下 （哈希值将有所不同）：</span><span class="sxs-lookup"><span data-stu-id="0e7a4-115">If the static file exists in the directory *..wwwroot/images/asplogo.png* the generated html is similar to the following (the hash will be different):</span></span>

```html
<img 
    src="/images/asplogo.png?v=Kl_dqr9NVtnMdsM2MUg4qthUnWZm5T1fCEimBPWDNgM"/>
```

<span data-ttu-id="0e7a4-116">分配给该参数的值`v`是磁盘上的文件的哈希值。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-116">The value assigned to the parameter `v` is the hash value of the file on disk.</span></span> <span data-ttu-id="0e7a4-117">如果 web 服务器无法获取对读取访问权限的静态文件引用，否`v`参数添加到`src`属性。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-117">If the web server is unable to obtain read access to the static file referenced,  no `v` parameters is added to the `src` attribute.</span></span>

- - -

### <a name="src"></a><span data-ttu-id="0e7a4-118">src</span><span class="sxs-lookup"><span data-stu-id="0e7a4-118">src</span></span>

<span data-ttu-id="0e7a4-119">若要激活图像标记帮助器，src 属性都需要`<img>`元素。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-119">To activate the Image Tag Helper, the src attribute is required on the `<img>` element.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e7a4-120">使用图像标记帮助器`Cache`本地 web 服务器上的提供商联系，以存储计算`Sha512`给定文件。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-120">The Image Tag Helper uses the `Cache` provider on the local web server to store the calculated `Sha512` of a given file.</span></span> <span data-ttu-id="0e7a4-121">如果对文件请求再次`Sha512`不需要重新计算。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-121">If the file is requested again the `Sha512` doesn't need to be recalculated.</span></span> <span data-ttu-id="0e7a4-122">缓存失效的文件观察程序附加到的文件时该文件的`Sha512`计算。</span><span class="sxs-lookup"><span data-stu-id="0e7a4-122">The Cache is invalidated by a file watcher that's attached to the file when the file's `Sha512` is calculated.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e7a4-123">其他资源</span><span class="sxs-lookup"><span data-stu-id="0e7a4-123">Additional resources</span></span>

* <xref:performance/caching/memory>
