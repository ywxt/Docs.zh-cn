---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[如何实现:]与 Excel 类似应用程序的数据导出到逗号分隔 (CSV) 文件 |Microsoft Docs'
author: rick-anderson
description: 在本视频中 Chris Pels 演示如何从数据库或其他源提取数据并将其导出到的以逗号分隔文件，可在应用程序 li...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/22/2009
ms.topic: article
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: 7c1f94118c64fee7f4198cd096ae2ef200981ba8
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402598"
---
<a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="7d50c-103">[如何实现:]将数据导出到 Excel 这样的应用程序的逗号分隔 (CSV) 文件</span><span class="sxs-lookup"><span data-stu-id="7d50c-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>
====================
<span data-ttu-id="7d50c-104">通过[Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="7d50c-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="7d50c-105">在本视频中 Chris Pels 演示如何从数据库或其他源提取数据并将其导出到的以逗号分隔文件，可以使用类似于 Excel 的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="7d50c-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="7d50c-106">首先，作为 DataTable 对象创建一组数据。</span><span class="sxs-lookup"><span data-stu-id="7d50c-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="7d50c-107">接下来，清除当前的 web 页请求的响应，并被配置为 csv 文件的标头和内容类型。</span><span class="sxs-lookup"><span data-stu-id="7d50c-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="7d50c-108">然后实际数据添加到响应流的第一个写入的数据值的 csv 文件的列标题。</span><span class="sxs-lookup"><span data-stu-id="7d50c-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="7d50c-109">当用户需要的数据的导出，因此可以在程序中与 Excel 类似本地操作时，此方法可能很有用。</span><span class="sxs-lookup"><span data-stu-id="7d50c-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="7d50c-110">&#9654;观看视频 （19 分钟）</span><span class="sxs-lookup"><span data-stu-id="7d50c-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)
