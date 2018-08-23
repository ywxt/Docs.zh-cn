---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: 通过数据库 (C#) 使用 CascadingDropDown |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中 anoth 值...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: ed5057ee942ce57503b038cbd856fefaa3d287ce
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825292"
---
<a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="795e6-103">使用 CascadingDropDown 与数据库 (C#)</span><span class="sxs-lookup"><span data-stu-id="795e6-103">Using CascadingDropDown with a Database (C#)</span></span>
====================
<span data-ttu-id="795e6-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="795e6-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="795e6-105">[下载代码](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip)或[下载 PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="795e6-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="795e6-106">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="795e6-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="795e6-107">为了使此功能，必须创建一个特殊 web 服务。</span><span class="sxs-lookup"><span data-stu-id="795e6-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="795e6-108">概述</span><span class="sxs-lookup"><span data-stu-id="795e6-108">Overview</span></span>

<span data-ttu-id="795e6-109">AJAX 控件工具包中的 CascadingDropDown 控件扩展 DropDownList 控件，使得一个 DropDownList 负载中的更改关联中另一个 DropDownList 的值。</span><span class="sxs-lookup"><span data-stu-id="795e6-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="795e6-110">（例如，一个列表提供了一系列我们状态，和与该状态中的主要城市然后填充下一个列表。）为了使此功能，必须创建一个特殊 web 服务。</span><span class="sxs-lookup"><span data-stu-id="795e6-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="795e6-111">步骤</span><span class="sxs-lookup"><span data-stu-id="795e6-111">Steps</span></span>

<span data-ttu-id="795e6-112">首先，数据源是必需的。</span><span class="sxs-lookup"><span data-stu-id="795e6-112">First of all, a data source is required.</span></span> <span data-ttu-id="795e6-113">此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。</span><span class="sxs-lookup"><span data-stu-id="795e6-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="795e6-114">数据库是可选的组成部分 （包括速成版） 的 Visual Studio 安装，并且仍可单独下载下[ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)。</span><span class="sxs-lookup"><span data-stu-id="795e6-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="795e6-115">AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库的一部分 (在下载[ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en))。</span><span class="sxs-lookup"><span data-stu-id="795e6-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="795e6-116">若要设置数据库的最简单方法是使用 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))，并将附加`AdventureWorks.mdf`数据库文件。</span><span class="sxs-lookup"><span data-stu-id="795e6-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="795e6-117">对于此示例中，我们假定 SQL Server 2005 Express Edition 的实例称为`SQLEXPRESS`和驻留在与 web 服务器; 在同一台计算机上这也是默认设置。</span><span class="sxs-lookup"><span data-stu-id="795e6-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="795e6-118">如果你的设置不同，您必须调整数据库的连接信息。</span><span class="sxs-lookup"><span data-stu-id="795e6-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="795e6-119">若要激活 ASP.NET AJAX 控件工具包的功能`ScriptManager`控件必须添加到任何位置的页上 (之内&lt; `form` &gt;元素):</span><span class="sxs-lookup"><span data-stu-id="795e6-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="795e6-120">在下一步中，两个 DropDownList 控件是必需的。</span><span class="sxs-lookup"><span data-stu-id="795e6-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="795e6-121">在此示例中，我们使用来自 AdventureWorks 的供应商和联系人信息，因此我们为可用的供应商，另一个可用的联系人用于创建一个列表：</span><span class="sxs-lookup"><span data-stu-id="795e6-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="795e6-122">然后，必须将两个 CascadingDropDown 扩展器添加到页面。</span><span class="sxs-lookup"><span data-stu-id="795e6-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="795e6-123">一个填充第一个 （供应商） 列表，并将另一个填充第二个 （联系人） 列表。</span><span class="sxs-lookup"><span data-stu-id="795e6-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="795e6-124">必须设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="795e6-124">The following attributes must be set:</span></span>

- <span data-ttu-id="795e6-125">`ServicePath`: Web 服务提供的列表项的 URL</span><span class="sxs-lookup"><span data-stu-id="795e6-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="795e6-126">`ServiceMethod`: Web 方法提供的列表项</span><span class="sxs-lookup"><span data-stu-id="795e6-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="795e6-127">`TargetControlID`: 下拉列表的 ID</span><span class="sxs-lookup"><span data-stu-id="795e6-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="795e6-128">`Category`： 提交到 web 方法调用时类别信息</span><span class="sxs-lookup"><span data-stu-id="795e6-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="795e6-129">`PromptText`： 以异步方式从服务器加载列表数据时显示的文本</span><span class="sxs-lookup"><span data-stu-id="795e6-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="795e6-130">`ParentControlID`: (可选) 父下拉列表中列出的当前列表，触发器加载</span><span class="sxs-lookup"><span data-stu-id="795e6-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="795e6-131">具体取决于使用的编程语言，有问题的 web 服务的名称更改，但所有其他属性值是相同的。</span><span class="sxs-lookup"><span data-stu-id="795e6-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="795e6-132">下面是第一个下拉列表中的 CascadingDropDown 元素：</span><span class="sxs-lookup"><span data-stu-id="795e6-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="795e6-133">第二个列表的控件扩展程序需要设置`ParentControlID`属性，以便在加载供应商列表触发器中选择某一项关联的联系人列表中的元素。</span><span class="sxs-lookup"><span data-stu-id="795e6-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="795e6-134">在 web 服务中，按如下所示设置然后完成实际工作。</span><span class="sxs-lookup"><span data-stu-id="795e6-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="795e6-135">请注意，`[ScriptService]`使用属性，否则 ASP.NET AJAX 不能创建要从客户端脚本代码访问的 web 方法的 JavaScript 代理。</span><span class="sxs-lookup"><span data-stu-id="795e6-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="795e6-136">通过 CascadingDropDown 调用的 web 方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="795e6-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="795e6-137">因此，返回值必须是类型的数组`CascadingDropDownNameValue`其定义了控件工具包。</span><span class="sxs-lookup"><span data-stu-id="795e6-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="795e6-138">`GetVendors()`方法可以很容易地实现： 代码连接到 AdventureWorks 数据库并查询前 25 个供应商。</span><span class="sxs-lookup"><span data-stu-id="795e6-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="795e6-139">中的第一个参数`CascadingDropDownNameValue`构造函数是其值的列表项，第二个的标题 (以 html 格式的值特性&lt; `option` &gt;元素)。</span><span class="sxs-lookup"><span data-stu-id="795e6-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="795e6-140">下面是代码：</span><span class="sxs-lookup"><span data-stu-id="795e6-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="795e6-141">获取关联的联系人的供应商 (方法名称： `GetContactsForVendor()`) 则有点棘手。</span><span class="sxs-lookup"><span data-stu-id="795e6-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="795e6-142">首先，必须确定供应商的第一个下拉列表中选择。</span><span class="sxs-lookup"><span data-stu-id="795e6-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="795e6-143">控件工具包定义该任务的帮助器方法：`ParseKnownCategoryValuesString()`方法将返回`StringDictionary`具有下拉列表中数据元素：</span><span class="sxs-lookup"><span data-stu-id="795e6-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="795e6-144">出于安全原因，必须首先验证此数据。</span><span class="sxs-lookup"><span data-stu-id="795e6-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="795e6-145">因此，如果供应商条目 (因为`Category`的第一个 CascadingDropDown 元素的属性设置为`"Vendor"`)，可能会检索所选的供应商的 ID:</span><span class="sxs-lookup"><span data-stu-id="795e6-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="795e6-146">方法的剩余部分就相当简单直接。</span><span class="sxs-lookup"><span data-stu-id="795e6-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="795e6-147">供应商的 ID 用作可检索有关该供应商相关联的所有联系人的 SQL 查询参数。</span><span class="sxs-lookup"><span data-stu-id="795e6-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="795e6-148">再次重申，该方法返回类型的数组`CascadingDropDownNameValue`。</span><span class="sxs-lookup"><span data-stu-id="795e6-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="795e6-149">加载 ASP.NET 页上，并且之后不久, 供应商列表填充包含 25 个条目。</span><span class="sxs-lookup"><span data-stu-id="795e6-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="795e6-150">选择一个条目，并请注意如何使用数据填充第二个下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="795e6-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="795e6-151">[![自动填充第一个列表](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="795e6-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="795e6-152">自动填充第一个列表 ([单击此项可查看原尺寸图像](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="795e6-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>


<span data-ttu-id="795e6-153">[![第二个列表填充根据第一个列表中选择](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="795e6-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="795e6-154">第二个列表填充根据第一个列表中选择 ([单击此项可查看原尺寸图像](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="795e6-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="795e6-155">[上一页](filling-a-list-using-cascadingdropdown-cs.md)
> [下一页](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="795e6-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>
