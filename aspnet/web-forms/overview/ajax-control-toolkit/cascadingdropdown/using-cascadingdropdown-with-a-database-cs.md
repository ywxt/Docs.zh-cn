---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: 使用数据库 (C#) CascadingDropDown |Microsoft 文档
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 1991c26d408e593999288ea6df0467cea0369457
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
<a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="550e9-103">CascadingDropDown 使用数据库 (C#)</span><span class="sxs-lookup"><span data-stu-id="550e9-103">Using CascadingDropDown with a Database (C#)</span></span>
====================
<span data-ttu-id="550e9-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="550e9-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="550e9-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="550e9-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="550e9-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 值。</span><span class="sxs-lookup"><span data-stu-id="550e9-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="550e9-107">为了使这种方式生效，必须创建特殊的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="550e9-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="550e9-108">概述</span><span class="sxs-lookup"><span data-stu-id="550e9-108">Overview</span></span>

<span data-ttu-id="550e9-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展的 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 值。</span><span class="sxs-lookup"><span data-stu-id="550e9-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="550e9-110">（例如，一个列表提供了一份我们状态，并且用处于该状态的主要城市然后填充下一个列表。）为了使这种方式生效，必须创建特殊的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="550e9-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="550e9-111">步骤</span><span class="sxs-lookup"><span data-stu-id="550e9-111">Steps</span></span>

<span data-ttu-id="550e9-112">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="550e9-112">First of all, a data source is required.</span></span> <span data-ttu-id="550e9-113">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="550e9-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="550e9-114">数据库是 （包括速成版） 的 Visual Studio 安装的可选部分，还可用作下单独下载[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="550e9-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="550e9-115">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="550e9-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="550e9-116">设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;-4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 和附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="550e9-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="550e9-117">对于此示例中，我们假定的 SQL Server 2005 Express Edition 实例称为`SQLEXPRESS`和驻留在与 web 服务器; 相同的计算机上也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="550e9-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="550e9-118">如果你的设置不同，你必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="550e9-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="550e9-119">为了激活 ASP.NET AJAX 和控件工具包中的功能`ScriptManager`必须在页面上任意位置放置控件 (但内&lt; `form` &gt;元素):</span><span class="sxs-lookup"><span data-stu-id="550e9-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="550e9-120">在下一步的步骤中，两个 DropDownList 控件是必需的。</span><span class="sxs-lookup"><span data-stu-id="550e9-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="550e9-121">在此示例中，我们使用从 AdventureWorks 的供应商和联系人信息，因此我们创建一个列表用于可用供应商，一个用于可用联系人：</span><span class="sxs-lookup"><span data-stu-id="550e9-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="550e9-122">然后，两个 CascadingDropDown 扩展程序必须添加到页面。</span><span class="sxs-lookup"><span data-stu-id="550e9-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="550e9-123">一个填充第一个 （供应商） 列表中，并且另一填充第二个 （联系人） 列表。</span><span class="sxs-lookup"><span data-stu-id="550e9-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="550e9-124">必须设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="550e9-124">The following attributes must be set:</span></span>

- <span data-ttu-id="550e9-125">`ServicePath`: 提供的列表项 web 服务的 URL</span><span class="sxs-lookup"><span data-stu-id="550e9-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="550e9-126">`ServiceMethod`: Web 方法提供的列表项</span><span class="sxs-lookup"><span data-stu-id="550e9-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="550e9-127">`TargetControlID`: ID 的下拉列表</span><span class="sxs-lookup"><span data-stu-id="550e9-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="550e9-128">`Category`： 提交给 web 方法调用时的类别信息</span><span class="sxs-lookup"><span data-stu-id="550e9-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="550e9-129">`PromptText`： 当以异步方式从服务器加载列表数据时显示的文本</span><span class="sxs-lookup"><span data-stu-id="550e9-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="550e9-130">`ParentControlID`: (可选) 父下拉列表中的当前列表，触发器加载</span><span class="sxs-lookup"><span data-stu-id="550e9-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="550e9-131">具体取决于所用的编程语言，web 服务的名称会更改，但所有其他属性值是相同的。</span><span class="sxs-lookup"><span data-stu-id="550e9-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="550e9-132">此处是第一个下拉列表中的 CascadingDropDown 元素：</span><span class="sxs-lookup"><span data-stu-id="550e9-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="550e9-133">第二个列表控件的扩展器需要设置`ParentControlID`属性，以便加载供应商列表触发器中选择某一项关联的联系人列表中的元素。</span><span class="sxs-lookup"><span data-stu-id="550e9-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="550e9-134">在 web 服务中，按以下方式设置，然后完成实际工作。</span><span class="sxs-lookup"><span data-stu-id="550e9-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="550e9-135">请注意，`[ScriptService]`使用属性，否则 ASP.NET AJAX 无法创建要从客户端脚本代码访问的 web 方法的 JavaScript 代理。</span><span class="sxs-lookup"><span data-stu-id="550e9-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="550e9-136">由 CascadingDropDown 调用 web 方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="550e9-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="550e9-137">因此返回的值必须为类型的数组`CascadingDropDownNameValue`其定义了控件工具包。</span><span class="sxs-lookup"><span data-stu-id="550e9-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="550e9-138">`GetVendors()`方法可以很容易地实现： 代码连接到 AdventureWorks 数据库，并查询前 25 个供应商。</span><span class="sxs-lookup"><span data-stu-id="550e9-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="550e9-139">中的第一个参数`CascadingDropDownNameValue`构造函数的列表项第二个的默认标题是其值 (以 HTML 的 value 属性&lt; `option` &gt;元素)。</span><span class="sxs-lookup"><span data-stu-id="550e9-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="550e9-140">以下是代码：</span><span class="sxs-lookup"><span data-stu-id="550e9-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="550e9-141">获取供应商相关联的联系人 (方法名称： `GetContactsForVendor()`) 棘手。</span><span class="sxs-lookup"><span data-stu-id="550e9-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="550e9-142">首先，必须确定这已在第一个下拉列表中选择的供应商。</span><span class="sxs-lookup"><span data-stu-id="550e9-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="550e9-143">该控件工具包定义为该任务的帮助器方法：`ParseKnownCategoryValuesString()`方法返回`StringDictionary`与下拉列表中的数据的元素：</span><span class="sxs-lookup"><span data-stu-id="550e9-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="550e9-144">出于安全原因，必须首先验证此数据。</span><span class="sxs-lookup"><span data-stu-id="550e9-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="550e9-145">因此，如果供应商条目 (因为`Category`的第一个 CascadingDropDown 元素的属性设置为`"Vendor"`)，可能会检索所选供应商 ID:</span><span class="sxs-lookup"><span data-stu-id="550e9-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="550e9-146">该方法的其余部分是相当简单，然后所示。</span><span class="sxs-lookup"><span data-stu-id="550e9-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="550e9-147">供应商的 ID 用作可检索为该供应商的所有相关联的联系人的 SQL 查询参数。</span><span class="sxs-lookup"><span data-stu-id="550e9-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="550e9-148">同样，该方法返回类型的数组`CascadingDropDownNameValue`。</span><span class="sxs-lookup"><span data-stu-id="550e9-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="550e9-149">加载 ASP.NET 页中，并在很短的时间后供应商列表填充包含 25 个条目。</span><span class="sxs-lookup"><span data-stu-id="550e9-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="550e9-150">选择一个条目，并注意如何填充数据的第二个下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="550e9-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="550e9-151">[![第一个列表中自动填充](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="550e9-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="550e9-152">第一个列表中自动填充 ([单击以查看实际尺寸的图像](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="550e9-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>


<span data-ttu-id="550e9-153">[![第二个列表填充根据第一个列表中选择](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="550e9-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="550e9-154">第二个列表填充根据第一个列表中选择 ([单击以查看实际尺寸的图像](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="550e9-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="550e9-155">[上一页](filling-a-list-using-cascadingdropdown-cs.md)
> [下一页](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="550e9-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
