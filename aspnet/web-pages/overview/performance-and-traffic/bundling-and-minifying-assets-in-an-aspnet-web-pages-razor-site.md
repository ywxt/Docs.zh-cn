---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: 绑定和贴图层在 ASP.NET 网页中的资产页 (Razor) 站点 |Microsoft 文档
author: microsoft
description: 绑定和缩减是方式使您的网站更快。 绑定允许你组合多个 JavaScript (.js) 文件或多个级联样式表 （...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/21/2012
ms.topic: article
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: df00b5c9e741e429011143d04121df97c1930602
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2017
ms.locfileid: "26528546"
---
<a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="75ece-104">绑定和贴图层 ASP.NET Web 页 (Razor) 站点中的资产</span><span class="sxs-lookup"><span data-stu-id="75ece-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>
====================
<span data-ttu-id="75ece-105">通过[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="75ece-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="75ece-106">绑定和缩减是方式使您的网站更快。</span><span class="sxs-lookup"><span data-stu-id="75ece-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="75ece-107">绑定可以合并多个 JavaScript (*.js*) 文件或多个级联样式表 (*.css*) 文件，以便它们可以作为一个单元，而不是一次一个地下载。</span><span class="sxs-lookup"><span data-stu-id="75ece-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="75ece-108">缩减加大出空白，并执行其他类型的压缩可让尽可能小的下载的文件可能发生的。</span><span class="sxs-lookup"><span data-stu-id="75ece-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="75ece-109">ASP.NET 网页 2 RC 版本不支持绑定和缩减，因为包含所需的元素的包尚不可用 Microsoft WebMatrix 中。</span><span class="sxs-lookup"><span data-stu-id="75ece-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="75ece-110">对于此不便，我们深表歉意。</span><span class="sxs-lookup"><span data-stu-id="75ece-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="75ece-111">包预计会在 ASP.NET 网页 2 和 WebMatrix 2 的最终版本中可用。</span><span class="sxs-lookup"><span data-stu-id="75ece-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>
