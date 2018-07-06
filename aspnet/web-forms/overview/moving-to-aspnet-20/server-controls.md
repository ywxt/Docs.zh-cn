---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 服务器控件 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 增强了服务器控件在许多方面。 在此模块中，我们将介绍一些方法 ASP.NET 2.0 和 Visual Studio 200 体系结构的更改...
ms.author: aspnetcontent
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: da06429f3949a47a02fccef45666d1220781e473
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2018
ms.locfileid: "37837064"
---
<a name="server-controls"></a><span data-ttu-id="2f19d-104">服务器控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-104">Server Controls</span></span>
====================
<span data-ttu-id="2f19d-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2f19d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2f19d-106">ASP.NET 2.0 增强了服务器控件在许多方面。</span><span class="sxs-lookup"><span data-stu-id="2f19d-106">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="2f19d-107">在此模块中，我们将介绍一些 ASP.NET 2.0 的方式对体系结构更改，Visual Studio 2005 处理服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-107">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>


<span data-ttu-id="2f19d-108">ASP.NET 2.0 增强了服务器控件在许多方面。</span><span class="sxs-lookup"><span data-stu-id="2f19d-108">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="2f19d-109">在此模块中，我们将介绍一些 ASP.NET 2.0 的方式对体系结构更改，Visual Studio 2005 处理服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-109">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

## <a name="view-state"></a><span data-ttu-id="2f19d-110">视图状态</span><span class="sxs-lookup"><span data-stu-id="2f19d-110">View state</span></span>

<span data-ttu-id="2f19d-111">在视图状态在 ASP.NET 2.0 中的主要更改是大大缩短了大小。</span><span class="sxs-lookup"><span data-stu-id="2f19d-111">The primary change in view state in ASP.NET 2.0 is a dramatic reduction in size.</span></span> <span data-ttu-id="2f19d-112">请考虑仅在其上一个日历控件的页。</span><span class="sxs-lookup"><span data-stu-id="2f19d-112">Consider a page with only a Calendar control on it.</span></span> <span data-ttu-id="2f19d-113">下面是在 ASP.NET 1.1 中的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-113">Here is the view state in ASP.NET 1.1.</span></span>

[!code-css[Main](server-controls/samples/sample1.css)]

<span data-ttu-id="2f19d-114">现在这是视图状态在相同页上中 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="2f19d-114">Now here's the view state on an identical page in ASP.NET 2.0.</span></span>

[!code-css[Main](server-controls/samples/sample2.css)]

<span data-ttu-id="2f19d-115">这是相当明显的更改，并考虑在网络上来回传送视图状态，此更改可以为开发人员提供性能将显著提高。</span><span class="sxs-lookup"><span data-stu-id="2f19d-115">That's a pretty significant change, and considering that view state is carried back and forth over the wire, this change can give developers a significant performance increase.</span></span> <span data-ttu-id="2f19d-116">大小减少的视图状态是很大程度上因为我们在内部处理的方式。</span><span class="sxs-lookup"><span data-stu-id="2f19d-116">The reduction in size of view state is largely due to the way that we handle it internally.</span></span> <span data-ttu-id="2f19d-117">请记住，视图状态是 Base64 编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="2f19d-117">Remember that view state is a Base64 encoded string.</span></span> <span data-ttu-id="2f19d-118">若要更好地了解 ASP.NET 2.0 中在视图状态更改，让我们来看，在上面的示例中的已解码值。</span><span class="sxs-lookup"><span data-stu-id="2f19d-118">To better understand the change in view state in ASP.NET 2.0, let's have a look at the decoded values from the examples above.</span></span>

<span data-ttu-id="2f19d-119">以下是解码的 1.1 的视图状态：</span><span class="sxs-lookup"><span data-stu-id="2f19d-119">Here is the 1.1 view state decoded:</span></span>

[!code-css[Main](server-controls/samples/sample3.css)]

<span data-ttu-id="2f19d-120">这可能看上去有点像乱码，但此处的模式。</span><span class="sxs-lookup"><span data-stu-id="2f19d-120">This may look a bit like gibberish, but there is a pattern here.</span></span> <span data-ttu-id="2f19d-121">在 ASP.NET 1.x 中，我们使用的单个字符来标识数据类型和分隔的值使用&lt;&gt;字符。</span><span class="sxs-lookup"><span data-stu-id="2f19d-121">In ASP.NET 1.x, we used single characters to identify data-types and delimited values using the &lt;&gt; characters.</span></span> <span data-ttu-id="2f19d-122">上面的视图状态示例中的"t"表示三联数。</span><span class="sxs-lookup"><span data-stu-id="2f19d-122">The "t" in the view state sample above represents a Triplet.</span></span> <span data-ttu-id="2f19d-123">三元数组包含一对 Arraylist （"l"表示 ArrayList。）这些 ArrayLists 之一包含为 int32 类型 ("i")，值为 1，另一个包含另一个三联数。</span><span class="sxs-lookup"><span data-stu-id="2f19d-123">The Triplet contains a pair of ArrayLists (the "l" represents an ArrayList.) One of those ArrayLists contains an Int32 ("i") with a value of 1 and the other contains another Triplet.</span></span> <span data-ttu-id="2f19d-124">三元数组包含一对 Arraylist，等等。需要记住的重要一点是，我们使用三个一组包含对，我们确定的数据类型，通过以字母，我们使用&lt;和&gt;作为分隔符的字符。</span><span class="sxs-lookup"><span data-stu-id="2f19d-124">The Triplet contains a pair of ArrayLists, etc. The important thing to remember is that we use Triplets that contain pairs, we identify the data-types via a letter, and we use the &lt; and &gt; characters as delimiters.</span></span>

<span data-ttu-id="2f19d-125">在 ASP.NET 2.0 中，已解码的视图状态看起来有点不同。</span><span class="sxs-lookup"><span data-stu-id="2f19d-125">In ASP.NET 2.0, the decoded view state looks a bit different.</span></span>

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

<span data-ttu-id="2f19d-126">您应注意到出现的已解码的视图状态大的变化。</span><span class="sxs-lookup"><span data-stu-id="2f19d-126">You should notice a huge change in the appearance of the decoded view state.</span></span> <span data-ttu-id="2f19d-127">此更改有多个体系结构的基础。</span><span class="sxs-lookup"><span data-stu-id="2f19d-127">This change has several architectural underpinnings.</span></span> <span data-ttu-id="2f19d-128">视图状态在 ASP.NET 1.x 使用 losformatter 将其中的数据序列。</span><span class="sxs-lookup"><span data-stu-id="2f19d-128">View state in ASP.NET 1.x used the LosFormatter to serialize data.</span></span> <span data-ttu-id="2f19d-129">在 2.0 中，我们将使用新的 ObjectStateFormatter 类。</span><span class="sxs-lookup"><span data-stu-id="2f19d-129">In 2.0, we use the new ObjectStateFormatter class.</span></span> <span data-ttu-id="2f19d-130">此类被专门用于帮助进行序列化和反序列化的视图状态和控件状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-130">This class was specifically designed to aid in the serialization and deserialization of view state and control state.</span></span> <span data-ttu-id="2f19d-131">（控件状态中将会讨论下一节。）有很多更改的序列化和反序列化发生的方法所获得的好处。</span><span class="sxs-lookup"><span data-stu-id="2f19d-131">(Control state will be covered in the next section.) There are many benefits gained by changing the method by which serialization and deserialization take place.</span></span> <span data-ttu-id="2f19d-132">一个最显著的是与使用 TextWriter LosFormatter，不同 ObjectStateFormatter 使用 BinaryWriter 的事实。</span><span class="sxs-lookup"><span data-stu-id="2f19d-132">One of the most dramatic is the fact that unlike the LosFormatter which uses a TextWriter, the ObjectStateFormatter uses a BinaryWriter.</span></span> <span data-ttu-id="2f19d-133">这样，ASP.NET 2.0 存储视图状态一系列字节而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="2f19d-133">This allows ASP.NET 2.0 to store view state a series of bytes instead of strings.</span></span> <span data-ttu-id="2f19d-134">例如，采用一个整型。</span><span class="sxs-lookup"><span data-stu-id="2f19d-134">Take, for example, an integer.</span></span> <span data-ttu-id="2f19d-135">在 ASP.NET 1.1 中，整数所需的视图状态的 4 个字节。</span><span class="sxs-lookup"><span data-stu-id="2f19d-135">In ASP.NET 1.1, an integer required 4 bytes of view state.</span></span> <span data-ttu-id="2f19d-136">在 ASP.NET 2.0 中，该同一个整数只需要 1 个字节。</span><span class="sxs-lookup"><span data-stu-id="2f19d-136">In ASP.NET 2.0, that same integer only requires 1 byte.</span></span> <span data-ttu-id="2f19d-137">为了减少存储的视图状态的进行了其他增强功能。</span><span class="sxs-lookup"><span data-stu-id="2f19d-137">Other enhancements were made to decrease the amount of view state that is stored.</span></span> <span data-ttu-id="2f19d-138">日期时间值，例如，现在使用存储 TickCount 而不是一个字符串。</span><span class="sxs-lookup"><span data-stu-id="2f19d-138">DateTime values, for example, are now stored using a TickCount instead of a string.</span></span>

<span data-ttu-id="2f19d-139">像所有的不够，特别要注意是支付给 1.x 中的视图状态的最大使用者之一是数据网格和类似控件的这一事实。</span><span class="sxs-lookup"><span data-stu-id="2f19d-139">As if all of that weren't enough, special attention was paid to the fact that one of the greatest consumers of view state in 1.x was the DataGrid and similar controls.</span></span> <span data-ttu-id="2f19d-140">控件，如数据网格视图状态而言的主要缺点是信息的它通常包含大量重复。</span><span class="sxs-lookup"><span data-stu-id="2f19d-140">A major drawback of controls such as the DataGrid where view state is concerned is that it often contains large amounts of repeated information.</span></span> <span data-ttu-id="2f19d-141">在 ASP.NET 1.x 中，重复信息只需通过和重新生成了臃肿的视图状态存储。</span><span class="sxs-lookup"><span data-stu-id="2f19d-141">In ASP.NET 1.x, that repeated information was simply stored over and over again resulting in a bloated view state.</span></span> <span data-ttu-id="2f19d-142">在 ASP.NET 2.0 中，我们将使用新的 IndexedString 类来存储此类数据。</span><span class="sxs-lookup"><span data-stu-id="2f19d-142">In ASP.NET 2.0, we use the new IndexedString class to store such data.</span></span> <span data-ttu-id="2f19d-143">如果字符串重复发生，我们只需 IndexedString 和 IndexedString 对象的正在运行表中的索引存储令牌。</span><span class="sxs-lookup"><span data-stu-id="2f19d-143">If a string repeats, we just store the token for the IndexedString and the index within a running table of IndexedString objects.</span></span>

## <a name="control-state"></a><span data-ttu-id="2f19d-144">控件状态</span><span class="sxs-lookup"><span data-stu-id="2f19d-144">Control State</span></span>

<span data-ttu-id="2f19d-145">开发人员必须与视图状态的主要牢骚之一是将其添加到 HTTP 有效负载的大小。</span><span class="sxs-lookup"><span data-stu-id="2f19d-145">One of the major gripes that developers had with view state was the size that it added to the HTTP payload.</span></span> <span data-ttu-id="2f19d-146">如前所述，视图状态的最大使用者之一是数据网格控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-146">As previously mentioned, one of the greatest consumers of view state is the DataGrid control.</span></span> <span data-ttu-id="2f19d-147">若要避免生成的数据网格视图状态的数量庞大，许多开发人员只需禁用该控件的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-147">To avoid the huge amounts of view state generated by a DataGrid, many developers simply disabled view state for that control.</span></span> <span data-ttu-id="2f19d-148">遗憾的是，该解决方案不始终是一个较好。</span><span class="sxs-lookup"><span data-stu-id="2f19d-148">Unfortunately, that solution wasn't always a good one.</span></span> <span data-ttu-id="2f19d-149">视图状态在 ASP.NET 1.x 包含不仅为该控件的正确功能所需的数据。</span><span class="sxs-lookup"><span data-stu-id="2f19d-149">View state in ASP.NET 1.x contains not only data necessary for the correct functionality of the control.</span></span> <span data-ttu-id="2f19d-150">它还包含有关控件的用户界面的状态信息。</span><span class="sxs-lookup"><span data-stu-id="2f19d-150">It also contains information concerning the state of the control's UI.</span></span> <span data-ttu-id="2f19d-151">这意味着如果你想要允许分页上 DataGrid 中，必须启用视图状态，即使不需要的所有查看 UI 信息，包含状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-151">This means that if you want to allow for pagination on a DataGrid, you must enable view state even if you don't need all of the UI information that view state contains.</span></span> <span data-ttu-id="2f19d-152">它是一个要么方案。</span><span class="sxs-lookup"><span data-stu-id="2f19d-152">It's an all-or-nothing scenario.</span></span>

<span data-ttu-id="2f19d-153">在 ASP.NET 2.0 中，控件状态便可解决很好地通过引入控件状态的问题。</span><span class="sxs-lookup"><span data-stu-id="2f19d-153">In ASP.NET 2.0, control state solves that problem nicely via the introduction of control state.</span></span> <span data-ttu-id="2f19d-154">控件状态包含绝对有必要让的特有功能的控件的数据。</span><span class="sxs-lookup"><span data-stu-id="2f19d-154">Control state contains the data that is absolutely necessary for the proper functionality of a control.</span></span> <span data-ttu-id="2f19d-155">与不同的视图状态，无法禁用控件状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-155">Unlike view state, control state cannot be disabled.</span></span> <span data-ttu-id="2f19d-156">因此，务必严格控制在控件状态中存储的数据。</span><span class="sxs-lookup"><span data-stu-id="2f19d-156">Therefore, it is important that the data being stored in control state is carefully controlled.</span></span>

> [!NOTE]
> <span data-ttu-id="2f19d-157">控件状态保存视图状态以及\_ \_VIEWSTATE 的隐藏窗体字段。</span><span class="sxs-lookup"><span data-stu-id="2f19d-157">Control state is persisted along with the view state in the \_\_VIEWSTATE hidden form field.</span></span>


<span data-ttu-id="2f19d-158">本视频是演练的视图状态和控件状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-158">This video is a walkthrough of view state and control state.</span></span>


![](server-controls/_static/image1.png)


[<span data-ttu-id="2f19d-159">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="2f19d-159">Open Full-Screen Video</span></span>](server-controls/_static/state1.wmv)


<span data-ttu-id="2f19d-160">在读取和写入来控制状态的服务器控件的顺序，您必须执行三个步骤。</span><span class="sxs-lookup"><span data-stu-id="2f19d-160">In order for a server control to read and write to control state, you must take three steps.</span></span>

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a><span data-ttu-id="2f19d-161">步骤 1： 调用 RegisterRequiresControlState 方法</span><span class="sxs-lookup"><span data-stu-id="2f19d-161">Step 1: Call the RegisterRequiresControlState Method</span></span>

<span data-ttu-id="2f19d-162">RegisterRequiresControlState 方法将通知 ASP.NET 控件需要以保持控件状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-162">The RegisterRequiresControlState method informs ASP.NET that a control needs to persist control state.</span></span> <span data-ttu-id="2f19d-163">它采用一个参数的类型是要注册的控件的控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-163">It takes one argument of type Control which is the control that is being registered.</span></span>

<span data-ttu-id="2f19d-164">请务必注意注册不会保留请求。</span><span class="sxs-lookup"><span data-stu-id="2f19d-164">It is important to note that registration does not persist from request to request.</span></span> <span data-ttu-id="2f19d-165">因此，此方法必须对每个请求调用如果一个控件，以保持控件状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-165">Therefore, this method must be called on every request if a control is to persist control state.</span></span> <span data-ttu-id="2f19d-166">建议在 OnInit 调用该方法。</span><span class="sxs-lookup"><span data-stu-id="2f19d-166">It is recommended that the method be called in OnInit.</span></span>

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a><span data-ttu-id="2f19d-167">步骤 2： 重写 savecontrolstate 来</span><span class="sxs-lookup"><span data-stu-id="2f19d-167">Step 2: Override SaveControlState</span></span>

<span data-ttu-id="2f19d-168">Savecontrolstate 来方法保存自上次回发控件的控件的状态更改。</span><span class="sxs-lookup"><span data-stu-id="2f19d-168">The SaveControlState method saves control state changes for a control since the last post back.</span></span> <span data-ttu-id="2f19d-169">它返回一个表示控件的状态对象。</span><span class="sxs-lookup"><span data-stu-id="2f19d-169">It returns an object representing the control's state.</span></span>

## <a name="step-3-override-loadcontrolstate"></a><span data-ttu-id="2f19d-170">步骤 3： 重写 LoadControlState</span><span class="sxs-lookup"><span data-stu-id="2f19d-170">Step 3: Override LoadControlState</span></span>

<span data-ttu-id="2f19d-171">LoadControlState 方法加载到控件的已保存的状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-171">The LoadControlState method loads saved state into a control.</span></span> <span data-ttu-id="2f19d-172">该方法采用一个参数的类型对象，其中包含该控件的已保存的状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-172">The method takes one argument of type Object which holds the saved state for the control.</span></span>

## <a name="full-xhtml-compliance"></a><span data-ttu-id="2f19d-173">完整的 XHTML 符合性</span><span class="sxs-lookup"><span data-stu-id="2f19d-173">Full XHTML Compliance</span></span>

<span data-ttu-id="2f19d-174">任何 Web 开发人员知道 Web 应用程序中的标准的重要性。</span><span class="sxs-lookup"><span data-stu-id="2f19d-174">Any Web developer knows the importance of standards in Web applications.</span></span> <span data-ttu-id="2f19d-175">为了维护的基于标准的开发环境，ASP.NET 2.0 是完全符合 XHTML。</span><span class="sxs-lookup"><span data-stu-id="2f19d-175">In order to maintain a standards-based development environment, ASP.NET 2.0 is fully XHTML compliant.</span></span> <span data-ttu-id="2f19d-176">因此，所有标记都都根据 XHTML 标准中支持 HTML 4.0 的浏览器呈现或更高版本。</span><span class="sxs-lookup"><span data-stu-id="2f19d-176">Therefore, all tags are rendered according to XHTML standards in browsers that support HTML 4.0 or greater.</span></span>

<span data-ttu-id="2f19d-177">ASP.NET 1.1 中的文档类型定义如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f19d-177">The DOCTYPE definition in ASP.NET 1.1 was as follows:</span></span>

[!code-html[Main](server-controls/samples/sample6.html)]

<span data-ttu-id="2f19d-178">在 ASP.NET 2.0 中，默认文档类型定义如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f19d-178">In ASP.NET 2.0, the default DOCTYPE definition is as follows:</span></span>

[!code-html[Main](server-controls/samples/sample7.html)]

<span data-ttu-id="2f19d-179">如果愿意，您可以更改通过配置文件中的 xhtmlConformance 节点的默认 XHML 符合性。</span><span class="sxs-lookup"><span data-stu-id="2f19d-179">If you choose, you can alter the default XHML compliance via the xhtmlConformance node in the configuration file.</span></span> <span data-ttu-id="2f19d-180">例如，web.config 文件中的以下节点将更改为 XHTML 1.0 Strict 的 XHTML 符合性：</span><span class="sxs-lookup"><span data-stu-id="2f19d-180">For example, the following node in the web.config file will change XHTML compliance to XHTML 1.0 Strict:</span></span>

[!code-xml[Main](server-controls/samples/sample8.xml)]

<span data-ttu-id="2f19d-181">如果愿意，还可以配置 ASP.NET 用于在 ASP.NET 中使用的旧配置，如下所示的 1.x:</span><span class="sxs-lookup"><span data-stu-id="2f19d-181">If you choose, you can also configure ASP.NET to use the legacy configuration used in ASP.NET 1.x as follows:</span></span>

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a><span data-ttu-id="2f19d-182">自适应呈现使用适配器</span><span class="sxs-lookup"><span data-stu-id="2f19d-182">Adaptive Rendering Using Adapters</span></span>

<span data-ttu-id="2f19d-183">在 ASP.NET 1.x 中，包含的配置文件&lt;browserCaps&gt;填充 HttpBrowserCapabilities 对象的部分。</span><span class="sxs-lookup"><span data-stu-id="2f19d-183">In ASP.NET 1.x, the configuration file contained a &lt;browserCaps&gt; section that populated a HttpBrowserCapabilities object.</span></span> <span data-ttu-id="2f19d-184">此对象允许开发人员能够确定哪些设备正在发出特定请求，并相应地呈现代码。</span><span class="sxs-lookup"><span data-stu-id="2f19d-184">This object allowed a developer to determine what device is making a particular request and render code appropriately.</span></span> <span data-ttu-id="2f19d-185">在 ASP.NET 2.0 中，模型改进了，现在使用新的 ControlAdapter 类。</span><span class="sxs-lookup"><span data-stu-id="2f19d-185">In ASP.NET 2.0, the model has improved and now uses the new ControlAdapter class.</span></span> <span data-ttu-id="2f19d-186">ControlAdapter 类重写控件的生命周期中的事件，并控制在呈现控件基于用户代理的功能。</span><span class="sxs-lookup"><span data-stu-id="2f19d-186">The ControlAdapter class overrides events in the control's lifecycle and controls the rendering of controls based upon the user agent's capabilities.</span></span> <span data-ttu-id="2f19d-187">由浏览器定义文件 （.browser 文件扩展名的文件） 存储在 c:\windows\microsoft.net\framework\v2.0 中定义的特定用户代理的功能。\* \* \* \*\CONFIG\Browsers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="2f19d-187">The capabilities of a specific user agent are defined by a browser definition file (a file with a .browser file extension) stored in the c:\windows\microsoft.net\framework\v2.0.\*\*\*\*\CONFIG\Browsers folder.</span></span>

> [!NOTE]
> <span data-ttu-id="2f19d-188">ControlAdapter 类是一个抽象类。</span><span class="sxs-lookup"><span data-stu-id="2f19d-188">The ControlAdapter class is an abstract class.</span></span>


<span data-ttu-id="2f19d-189">更喜欢&lt;browserCaps&gt;部分 1.x 中，浏览器定义文件中的使用正则表达式来分析用户代理字符串以确定请求浏览器。</span><span class="sxs-lookup"><span data-stu-id="2f19d-189">Much like the &lt;browserCaps&gt; section in 1.x, the browser definition file uses a Regular Expression to parse the user agent string in order to identify the requesting browser.</span></span> <span data-ttu-id="2f19d-190">它它们定义为该用户代理的特定功能。</span><span class="sxs-lookup"><span data-stu-id="2f19d-190">It them defines particular capabilities for that user agent.</span></span> <span data-ttu-id="2f19d-191">ControlAdapter 呈现控件通过呈现方法。</span><span class="sxs-lookup"><span data-stu-id="2f19d-191">The ControlAdapter renders the control via the Render method.</span></span> <span data-ttu-id="2f19d-192">因此，如果重写的 Render 方法，您不应在基础类上调用呈现。</span><span class="sxs-lookup"><span data-stu-id="2f19d-192">Therefore, if you override the Render method, you should not call Render on the base class.</span></span> <span data-ttu-id="2f19d-193">执行此操作可能会导致呈现发生两次，一次针对适配器，一次控件本身。</span><span class="sxs-lookup"><span data-stu-id="2f19d-193">Doing so may cause rendering to occur twice, once for the adapter and once for the control itself.</span></span>

## <a name="developing-a-custom-adapter"></a><span data-ttu-id="2f19d-194">开发自定义适配器</span><span class="sxs-lookup"><span data-stu-id="2f19d-194">Developing a Custom Adapter</span></span>

<span data-ttu-id="2f19d-195">可以通过继承了 ControlAdapter 开发自定义适配器。</span><span class="sxs-lookup"><span data-stu-id="2f19d-195">You can develop your own custom adapter by inheriting from ControlAdapter.</span></span> <span data-ttu-id="2f19d-196">此外，可以继承的抽象类 PageAdapter 在其中进行页面需要适配器的情况下。</span><span class="sxs-lookup"><span data-stu-id="2f19d-196">Additionally, you can inherit from the abstract class PageAdapter in cases where an adapter is needed for a page.</span></span> <span data-ttu-id="2f19d-197">通过完成的控件，以便自定义适配器的映射&lt;controlAdapters&gt;浏览器定义文件中的元素。</span><span class="sxs-lookup"><span data-stu-id="2f19d-197">Mapping of controls to your custom adapter is accomplished via the &lt;controlAdapters&gt; element in the browser definition file.</span></span> <span data-ttu-id="2f19d-198">例如，浏览器定义文件中的以下 XML 将菜单控件映射到 MenuAdapter 类：</span><span class="sxs-lookup"><span data-stu-id="2f19d-198">For example, the following XML from a browser definition file maps the Menu control to the MenuAdapter class:</span></span>

[!code-html[Main](server-controls/samples/sample10.html)]

<span data-ttu-id="2f19d-199">使用此模型，它将成为控件开发人员若要针对某个特定设备或浏览器可以非常容易。</span><span class="sxs-lookup"><span data-stu-id="2f19d-199">Using this model, it becomes quite easy for a control developer to target a particular device or browser.</span></span> <span data-ttu-id="2f19d-200">它还是开发人员可以完全控制每个设备上呈现页的方式非常简单。</span><span class="sxs-lookup"><span data-stu-id="2f19d-200">It's also quite simple for a developer to have complete control over how pages render on every device.</span></span>

## <a name="per-device-rendering"></a><span data-ttu-id="2f19d-201">每个设备呈现</span><span class="sxs-lookup"><span data-stu-id="2f19d-201">Per-Device Rendering</span></span>

<span data-ttu-id="2f19d-202">在 ASP.NET 2.0 中的服务器控件属性可以指定每个设备使用特定于浏览器的前缀。</span><span class="sxs-lookup"><span data-stu-id="2f19d-202">Server control properties in ASP.NET 2.0 can be specified per-device using a browser-specific prefix.</span></span> <span data-ttu-id="2f19d-203">例如，下面的代码将更改取决于哪种设备用于浏览页面的标签的文本。</span><span class="sxs-lookup"><span data-stu-id="2f19d-203">For example, the code below will change the Text of a label depending upon which device is being used to browse the page.</span></span>

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

<span data-ttu-id="2f19d-204">当从 Internet Explorer 浏览网页包含此标签时，标签将显示文本说"您将浏览 Internet Explorer。"</span><span class="sxs-lookup"><span data-stu-id="2f19d-204">When the page containing this label is browsed from Internet Explorer, the label will display text saying "You are browsing from Internet Explorer."</span></span> <span data-ttu-id="2f19d-205">从 Firefox 浏览页面后，标签将显示文本"您将浏览 Firefox。"</span><span class="sxs-lookup"><span data-stu-id="2f19d-205">When the page is browsed from Firefox, the label will display the text "You are browsing from Firefox."</span></span> <span data-ttu-id="2f19d-206">当从其他设备浏览页面后时，它将显示"您将浏览未知设备。"</span><span class="sxs-lookup"><span data-stu-id="2f19d-206">When the page is browsed from any other device, it will display "You are browsing from an unknown device."</span></span> <span data-ttu-id="2f19d-207">可以使用此特殊语法指定任何属性。</span><span class="sxs-lookup"><span data-stu-id="2f19d-207">Any property can be specified using this special syntax.</span></span>

## <a name="setting-focus"></a><span data-ttu-id="2f19d-208">设置焦点</span><span class="sxs-lookup"><span data-stu-id="2f19d-208">Setting Focus</span></span>

<span data-ttu-id="2f19d-209">ASP.NET 1.x 开发人员经常询问如何在特定控件上设置初始焦点。</span><span class="sxs-lookup"><span data-stu-id="2f19d-209">ASP.NET 1.x developers frequently asked about how to set initial focus on a particular control.</span></span> <span data-ttu-id="2f19d-210">例如，在登录页上，为用户 ID 文本框中首次加载页面时获得焦点很有用。</span><span class="sxs-lookup"><span data-stu-id="2f19d-210">For example, on a login page, it's useful to have the User ID textbox get the focus when the page first loads.</span></span> <span data-ttu-id="2f19d-211">在 ASP.NET 1.x 中，执行此操作需要编写一些客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="2f19d-211">In ASP.NET 1.x, doing this required writing some client-side script.</span></span> <span data-ttu-id="2f19d-212">即使此类脚本是一个简单的任务，它不再需要在 ASP.NET 2.0 中由于 SetFocus 方法。</span><span class="sxs-lookup"><span data-stu-id="2f19d-212">Even though such a script is a trivial task, it's no longer necessary in ASP.NET 2.0 thanks to the SetFocus method.</span></span> <span data-ttu-id="2f19d-213">SetFocus 方法采用一个参数，该值指示应接收焦点的控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-213">The SetFocus method takes one argument indicating the control that should receive focus.</span></span> <span data-ttu-id="2f19d-214">此参数可以是控件的字符串形式表示的客户端 ID 或控件对象形式表示的服务器控件的名称。</span><span class="sxs-lookup"><span data-stu-id="2f19d-214">This argument can either be the client ID of the control as a string or the name of the Server control as a Control object.</span></span> <span data-ttu-id="2f19d-215">例如，若要将初始焦点设置到 TextBox 控件调用 txtUserID 首次加载页面时，以下代码添加到页\_负载：</span><span class="sxs-lookup"><span data-stu-id="2f19d-215">For example, to set the initial focus to a TextBox control called txtUserID when the page first loads, add the following code to Page\_Load:</span></span>

[!code-csharp[Main](server-controls/samples/sample12.cs)]

<span data-ttu-id="2f19d-216">-或</span><span class="sxs-lookup"><span data-stu-id="2f19d-216">-- or</span></span>

[!code-csharp[Main](server-controls/samples/sample13.cs)]

<span data-ttu-id="2f19d-217">ASP.NET 2.0 使用 Webresource.axd 处理程序 （前面讨论过） 来呈现一个设置焦点的客户端函数。</span><span class="sxs-lookup"><span data-stu-id="2f19d-217">ASP.NET 2.0 uses the Webresource.axd handler (discussed previously) to render a client-side function that sets the focus.</span></span> <span data-ttu-id="2f19d-218">客户端函数的名称是 web 窗体\_AutoFocus 如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f19d-218">The name of the client-side function is WebForm\_AutoFocus as shown here:</span></span>

[!code-html[Main](server-controls/samples/sample14.html)]

<span data-ttu-id="2f19d-219">或者，可以使用控件的焦点方法初始焦点设置到该控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-219">Alternatively, you can use the Focus method for a control to set the initial focus to that control.</span></span> <span data-ttu-id="2f19d-220">Focus 方法派生控件类，可供所有 ASP.NET 2.0 控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-220">The Focus method derives from the Control class and is available to all ASP.NET 2.0 controls.</span></span> <span data-ttu-id="2f19d-221">还有可能发生验证错误时，将焦点设置到特定控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-221">It is also possible to set focus to a particular control when a validation error occurs.</span></span> <span data-ttu-id="2f19d-222">在更高版本的模块，将介绍的。</span><span class="sxs-lookup"><span data-stu-id="2f19d-222">That will be covered in a later module.</span></span>

## <a name="new-server-controls-in-aspnet-20"></a><span data-ttu-id="2f19d-223">ASP.NET 2.0 中的新服务器控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-223">New Server Controls in ASP.NET 2.0</span></span>

<span data-ttu-id="2f19d-224">以下是在 ASP.NET 2.0 中的新服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-224">The following are new server controls in ASP.NET 2.0.</span></span> <span data-ttu-id="2f19d-225">我们将介绍更高版本的模块中的其中一些更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="2f19d-225">We will go into more detail on some of them in later modules.</span></span>

## <a name="imagemap-control"></a><span data-ttu-id="2f19d-226">ImageMap 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-226">ImageMap Control</span></span>

<span data-ttu-id="2f19d-227">ImageMap 控件，可通过添加热点可以启动回发或导航到的 URL 的图像。</span><span class="sxs-lookup"><span data-stu-id="2f19d-227">The ImageMap control allows you to add hotspots to an image that can initiate a post back or navigate to a URL.</span></span> <span data-ttu-id="2f19d-228">有三种类型的热点;CircleHotSpot、 RectangleHotSpot 和 PolygonHotSpot。</span><span class="sxs-lookup"><span data-stu-id="2f19d-228">There are three types of hotspots available; CircleHotSpot, RectangleHotSpot, and PolygonHotSpot.</span></span> <span data-ttu-id="2f19d-229">在 Visual Studio 中或以编程方式在代码中的集合编辑器通过添加热点。</span><span class="sxs-lookup"><span data-stu-id="2f19d-229">Hotspots are added via a collection editor in Visual Studio or programmatically in code.</span></span> <span data-ttu-id="2f19d-230">可用于在图像上绘制热点是没有用户界面。</span><span class="sxs-lookup"><span data-stu-id="2f19d-230">There is no user-interface available for drawing hotspots on an image.</span></span> <span data-ttu-id="2f19d-231">必须以声明方式指定坐标和大小或 radius 的热点。</span><span class="sxs-lookup"><span data-stu-id="2f19d-231">The coordinates and size or radius of the hotspot must be specified declaratively.</span></span> <span data-ttu-id="2f19d-232">此外，还有在设计器中的一个热点没有可视化表示形式。</span><span class="sxs-lookup"><span data-stu-id="2f19d-232">There is also no visual representation of a hotspot in the designer.</span></span> <span data-ttu-id="2f19d-233">热点配置为导航到的 URL，如果是通过热点的 NavigateUrl 属性指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="2f19d-233">If a hotspot is configured to navigate to a URL, the URL is specified via the NavigateUrl property of the hotspot.</span></span> <span data-ttu-id="2f19d-234">对于 post 回热点，PostBackValue 属性可用于在服务器端代码中传递回发中可检索的字符串。</span><span class="sxs-lookup"><span data-stu-id="2f19d-234">In the case of a post back hotspot, the PostBackValue property allows you to pass a string in the post back that can be retrieved in server-side code.</span></span>


![在 Visual Studio 中的作用点集合编辑器](server-controls/_static/image1.jpg)

<span data-ttu-id="2f19d-236">**图 1**： 在 Visual Studio 中的作用点集合编辑器</span><span class="sxs-lookup"><span data-stu-id="2f19d-236">**Figure 1**: HotSpot Collection Editor in Visual Studio</span></span>


## <a name="bulletedlist-control"></a><span data-ttu-id="2f19d-237">BulletedList 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-237">BulletedList Control</span></span>

<span data-ttu-id="2f19d-238">BulletedList 控件是可以轻松地进行数据绑定的项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="2f19d-238">The BulletedList control is a bulleted list that can easily be data bound.</span></span> <span data-ttu-id="2f19d-239">可排序列表 （编号） 或未通过 BulletStyle 属性排序。</span><span class="sxs-lookup"><span data-stu-id="2f19d-239">The list can be ordered (numbered) or unordered via the BulletStyle property.</span></span> <span data-ttu-id="2f19d-240">列表中的每个项由 ListItem 对象表示。</span><span class="sxs-lookup"><span data-stu-id="2f19d-240">Each item in the list is represented by a ListItem object.</span></span>


![Visual Studio 中的 BulletedList 控件](server-controls/_static/image1.gif)

<span data-ttu-id="2f19d-242">**图 2**： 在 Visual Studio 中的 BulletedList 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-242">**Figure 2**: BulletedList Control in Visual Studio</span></span>


## <a name="hiddenfield-control"></a><span data-ttu-id="2f19d-243">HiddenField 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-243">HiddenField Control</span></span>

<span data-ttu-id="2f19d-244">HiddenField 控件将隐藏窗体字段添加到您的页面，其值是服务器端代码中提供。</span><span class="sxs-lookup"><span data-stu-id="2f19d-244">The HiddenField control adds a hidden form field to your page, the value of which is available in server-side code.</span></span> <span data-ttu-id="2f19d-245">隐藏的窗体字段的值通常需要回发之间保持不变。</span><span class="sxs-lookup"><span data-stu-id="2f19d-245">The value of a hidden form field is generally expected to remain unchanged between post backs.</span></span> <span data-ttu-id="2f19d-246">但是，它是恶意的用户可以更改回发值之前。</span><span class="sxs-lookup"><span data-stu-id="2f19d-246">However, it is possible for a malicious user to change the value prior to post back.</span></span> <span data-ttu-id="2f19d-247">如果发生这种情况，HiddenField 控件将引发 ValueChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-247">If this happens, the HiddenField control will raise the ValueChanged event.</span></span> <span data-ttu-id="2f19d-248">如果 HiddenField 控件中有敏感的信息和你想要确保其保持不变，则应在代码中处理 ValueChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-248">If you have sensitive information in the HiddenField control and you want to ensure that it remains unchanged, you should handle the ValueChanged event in your code.</span></span>

## <a name="fileupload-control"></a><span data-ttu-id="2f19d-249">FileUpload 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-249">FileUpload Control</span></span>

<span data-ttu-id="2f19d-250">ASP.NET 2.0 中的 FileUpload 控件使可能将文件上传到 Web 服务器通过 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="2f19d-250">The FileUpload control in ASP.NET 2.0 makes it possible to upload files to a Web server via an ASP.NET page.</span></span> <span data-ttu-id="2f19d-251">此控件是非常类似于 ASP.NET 1.x HtmlInputFile 类有少数例外。</span><span class="sxs-lookup"><span data-stu-id="2f19d-251">This control is quite similar to the ASP.NET 1.x HtmlInputFile class with a few exceptions.</span></span> <span data-ttu-id="2f19d-252">在 ASP.NET 1.x 中，会建议 PostedFile 属性，将检查是否为 null 以确定是否有一个很好的文件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-252">In ASP.NET 1.x, it was recommended that the PostedFile property be checked for null in order to determine if you had a good file.</span></span> <span data-ttu-id="2f19d-253">ASP.NET 2.0 中的 FileUpload 控件添加新的 HasFile 属性可用于同一目的和更高效。</span><span class="sxs-lookup"><span data-stu-id="2f19d-253">The FileUpload control in ASP.NET 2.0 adds a new HasFile property that you can use for the same purpose and it's a bit more efficient.</span></span>

<span data-ttu-id="2f19d-254">PostedFile 属性仍可用于访问 HttpPostedFile 对象，但一些 HttpPostedFile 功能现已推出本质上与 FileUpload 控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-254">The PostedFile property is still available for access to an HttpPostedFile object, but some of the functionality of the HttpPostedFile is now available intrinsically with the FileUpload control.</span></span> <span data-ttu-id="2f19d-255">例如，若要将上传的文件保存在 ASP.NET 1.x 中，调用 SaveAs 方法 HttpPostedFile 对象上。</span><span class="sxs-lookup"><span data-stu-id="2f19d-255">For example, to save an uploaded file in ASP.NET 1.x, you call the SaveAs method on the HttpPostedFile object.</span></span> <span data-ttu-id="2f19d-256">使用 FileUpload 控件在 ASP.NET 2.0 中，将在 FileUpload 控件自身上调用 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="2f19d-256">Using the FileUpload control in ASP.NET 2.0, you would call the SaveAs method on the FileUpload control itself.</span></span>

<span data-ttu-id="2f19d-257">2.0 的行为 （和可能的最重要的更改） 中的另一个重大变化是，它不再需要之前将其保存到内存中加载整个上传的文件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-257">Another significant change in the 2.0 behavior (and likely the most significant change) is that it is no longer necessary to load an entire uploaded file into memory before saving it.</span></span> <span data-ttu-id="2f19d-258">在 1.x 中，任何已上传的文件保存整个读入内存之前写入到磁盘。</span><span class="sxs-lookup"><span data-stu-id="2f19d-258">In 1.x, any file that was uploaded is saved entirely into memory prior to being written to disk.</span></span> <span data-ttu-id="2f19d-259">此体系结构可防止大型文件上的传。</span><span class="sxs-lookup"><span data-stu-id="2f19d-259">This architecture prevents the upload of large files.</span></span>

<span data-ttu-id="2f19d-260">在 ASP.NET 2.0 中，httpRuntime 元素的 requestLengthDiskThreshold 属性，可配置多少千字节为单位保存在内存之前写入的缓冲区中到磁盘。</span><span class="sxs-lookup"><span data-stu-id="2f19d-260">In ASP.NET 2.0, the requestLengthDiskThreshold attribute of the httpRuntime element allows you to configure how many Kilobytes are held in a buffer in memory prior to being written to disk.</span></span>

<span data-ttu-id="2f19d-261">**重要**: MSDN 文档 （和其他位置的文档） 指定此值是以字节为单位 （而不是千字节），默认值为 256。</span><span class="sxs-lookup"><span data-stu-id="2f19d-261">**IMPORTANT**: MSDN documentation (and documentation elsewhere) specifies that this value is in bytes (not Kilobytes) and that the default is 256.</span></span> <span data-ttu-id="2f19d-262">实际上在千字节为单位指定的值和默认值为 80。</span><span class="sxs-lookup"><span data-stu-id="2f19d-262">The value is actually specified in Kilobytes and the default value is 80.</span></span> <span data-ttu-id="2f19d-263">通过默认值为 80 K，我们确保缓冲区不会不结束大型对象堆上。</span><span class="sxs-lookup"><span data-stu-id="2f19d-263">By having a default value of 80K, we ensure that the buffer does not end up on the large object heap.</span></span>

## <a name="wizard-control"></a><span data-ttu-id="2f19d-264">向导控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-264">Wizard Control</span></span>

<span data-ttu-id="2f19d-265">它是相当常见，会遇到 ASP.NET 开发人员尝试收集序列中的信息的使用面板"页"或通过将传输的页面所困扰。</span><span class="sxs-lookup"><span data-stu-id="2f19d-265">It is fairly common to encounter ASP.NET developers struggling with attempting to gather information in a series of "pages" using panels or by transferring from page to page.</span></span> <span data-ttu-id="2f19d-266">在大多数情况，这项工作是一个令人沮丧，并且是较长时间。</span><span class="sxs-lookup"><span data-stu-id="2f19d-266">More often than not, the endeavor is a frustrating one and is time consuming.</span></span> <span data-ttu-id="2f19d-267">新的向导控件允许用户熟悉的向导界面中的线性和非线性步骤，从而解决了问题。</span><span class="sxs-lookup"><span data-stu-id="2f19d-267">The new Wizard control solves the problems by allowing for linear and non-linear steps in a wizard interface that users are familiar with.</span></span> <span data-ttu-id="2f19d-268">向导控件显示输入窗体中的一系列步骤。</span><span class="sxs-lookup"><span data-stu-id="2f19d-268">The Wizard control presents input forms in a series of steps.</span></span> <span data-ttu-id="2f19d-269">每个步骤是控件的特定类型 StepType 属性指定。</span><span class="sxs-lookup"><span data-stu-id="2f19d-269">Each step is of a particular type specified by the StepType property of the control.</span></span> <span data-ttu-id="2f19d-270">可用的步骤类型如下所示：</span><span class="sxs-lookup"><span data-stu-id="2f19d-270">The available step types are as follows:</span></span>

| <span data-ttu-id="2f19d-271">**步骤类型**</span><span class="sxs-lookup"><span data-stu-id="2f19d-271">**Step Type**</span></span> | <span data-ttu-id="2f19d-272">**说明**</span><span class="sxs-lookup"><span data-stu-id="2f19d-272">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="2f19d-273">自动</span><span class="sxs-lookup"><span data-stu-id="2f19d-273">Auto</span></span> | <span data-ttu-id="2f19d-274">该向导会自动确定基于步骤层次结构中其位置的步骤的类型。</span><span class="sxs-lookup"><span data-stu-id="2f19d-274">The wizard automatically determines the type of step based upon its position within the step hierarchy.</span></span> |
| <span data-ttu-id="2f19d-275">Start</span><span class="sxs-lookup"><span data-stu-id="2f19d-275">Start</span></span> | <span data-ttu-id="2f19d-276">第一步，通常用于提供介绍性语句。</span><span class="sxs-lookup"><span data-stu-id="2f19d-276">The first step, often used to present an introductory statement.</span></span> |
| <span data-ttu-id="2f19d-277">步骤</span><span class="sxs-lookup"><span data-stu-id="2f19d-277">Step</span></span> | <span data-ttu-id="2f19d-278">正常的步骤。</span><span class="sxs-lookup"><span data-stu-id="2f19d-278">A normal step.</span></span> |
| <span data-ttu-id="2f19d-279">完成</span><span class="sxs-lookup"><span data-stu-id="2f19d-279">Finish</span></span> | <span data-ttu-id="2f19d-280">最后一步，通常用于呈现按钮以完成向导。</span><span class="sxs-lookup"><span data-stu-id="2f19d-280">The final step, usually used to present a button to finish the wizard.</span></span> |
| <span data-ttu-id="2f19d-281">完成</span><span class="sxs-lookup"><span data-stu-id="2f19d-281">Complete</span></span> | <span data-ttu-id="2f19d-282">提供了通信成功或失败的消息。</span><span class="sxs-lookup"><span data-stu-id="2f19d-282">Presents a message communicating success or failure.</span></span> |

> [!NOTE]
> <span data-ttu-id="2f19d-283">跟踪其状态使用 ASP.NET 控件状态的向导控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-283">The Wizard control keeps track of its state using ASP.NET control state.</span></span> <span data-ttu-id="2f19d-284">因此，EnableViewState 属性可以设置为 false，而无需任何从而不利。</span><span class="sxs-lookup"><span data-stu-id="2f19d-284">Therefore, the EnableViewState property can be set to false without any detriment.</span></span>


<span data-ttu-id="2f19d-285">此视频是向导控件的演练。</span><span class="sxs-lookup"><span data-stu-id="2f19d-285">This video is a walkthrough of the Wizard control.</span></span>


![](server-controls/_static/image2.png)


[<span data-ttu-id="2f19d-286">打开的全屏视频</span><span class="sxs-lookup"><span data-stu-id="2f19d-286">Open Full-Screen Video</span></span>](server-controls/_static/wizard1.wmv)


## <a name="localize-control"></a><span data-ttu-id="2f19d-287">本地化控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-287">Localize Control</span></span>

<span data-ttu-id="2f19d-288">Localize 控件是类似于文字控件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-288">The Localize control is similar to a Literal control.</span></span> <span data-ttu-id="2f19d-289">但是，Localize 控件有**模式下**控件添加到它的标记的呈现方式的属性。</span><span class="sxs-lookup"><span data-stu-id="2f19d-289">However, the Localize control has a **Mode** property that controls how markup that is added to it is rendered.</span></span> <span data-ttu-id="2f19d-290">模式属性支持以下值：</span><span class="sxs-lookup"><span data-stu-id="2f19d-290">The Mode property supports the following values:</span></span>

| <span data-ttu-id="2f19d-291">**模式**</span><span class="sxs-lookup"><span data-stu-id="2f19d-291">**Mode**</span></span> | <span data-ttu-id="2f19d-292">**说明**</span><span class="sxs-lookup"><span data-stu-id="2f19d-292">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="2f19d-293">Transform</span><span class="sxs-lookup"><span data-stu-id="2f19d-293">Transform</span></span> | <span data-ttu-id="2f19d-294">根据浏览器发出请求的协议转换标记。</span><span class="sxs-lookup"><span data-stu-id="2f19d-294">Markup is transformed according to the protocol of the browser making the request.</span></span> |
| <span data-ttu-id="2f19d-295">传递</span><span class="sxs-lookup"><span data-stu-id="2f19d-295">PassThrough</span></span> | <span data-ttu-id="2f19d-296">标记呈现为的是。</span><span class="sxs-lookup"><span data-stu-id="2f19d-296">Markup is rendered as-is.</span></span> |
| <span data-ttu-id="2f19d-297">编码</span><span class="sxs-lookup"><span data-stu-id="2f19d-297">Encode</span></span> | <span data-ttu-id="2f19d-298">使用 HtmlEncode 编码添加到控件的标记。</span><span class="sxs-lookup"><span data-stu-id="2f19d-298">Markup that is added to the control is encoded using HtmlEncode.</span></span> |

## <a name="multiview-and-view-controls"></a><span data-ttu-id="2f19d-299">多视图和视图控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-299">MultiView and View Controls</span></span>

<span data-ttu-id="2f19d-300">多视图控件可用作视图控件的容器，并查看控件充当其他控件 （类似于在面板控件） 的容器。</span><span class="sxs-lookup"><span data-stu-id="2f19d-300">The MultiView control acts as a container for View controls, and the View control acts as a container (much like a Panel control) for other controls.</span></span> <span data-ttu-id="2f19d-301">多视图控件中的每个视图均由单个视图控件表示。</span><span class="sxs-lookup"><span data-stu-id="2f19d-301">Each view in a MultiView control is represented by a single View control.</span></span> <span data-ttu-id="2f19d-302">多视图中的第一个视图控件是视图，0，第二个是 1，视图等。可以通过指定的多视图控件 ActiveViewIndex 切换视图。</span><span class="sxs-lookup"><span data-stu-id="2f19d-302">The first View control in the MultiView is view 0, the second is view 1, etc. You can switch views by specifying the ActiveViewIndex of the MultiView control.</span></span>

## <a name="substitution-control"></a><span data-ttu-id="2f19d-303">Substitution 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-303">Substitution Control</span></span>

<span data-ttu-id="2f19d-304">Substitution 控件结合使用 ASP.NET 缓存。</span><span class="sxs-lookup"><span data-stu-id="2f19d-304">The Substitution control is used in conjunction with ASP.NET caching.</span></span> <span data-ttu-id="2f19d-305">在其中你想要充分利用缓存，但具有必须在每个请求 （换句话说，页面列出了部分受缓存限制） 更新的页的部分的情况下，替换组件提供了很好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="2f19d-305">In cases where you want to take advantage of caching, but you have portions of a page that must be updated on each request (in other words, portions of a page that are exempt from caching), the Substitution component provides a great solution.</span></span> <span data-ttu-id="2f19d-306">该控件实际上不会呈现在其自己的任何输出。</span><span class="sxs-lookup"><span data-stu-id="2f19d-306">The control doesn't actually render any output on its own.</span></span> <span data-ttu-id="2f19d-307">相反，它绑定到服务器端代码中的方法。</span><span class="sxs-lookup"><span data-stu-id="2f19d-307">Instead, it is bound to a method in server-side code.</span></span> <span data-ttu-id="2f19d-308">当请求页面时，调用该方法并返回的标记呈现替换控件的位置。</span><span class="sxs-lookup"><span data-stu-id="2f19d-308">When the page is requested, the method is called and the returned markup is rendered in place of the substitution control.</span></span>

<span data-ttu-id="2f19d-309">通过指定 Substitution 控件绑定到的方法**MethodName**属性。</span><span class="sxs-lookup"><span data-stu-id="2f19d-309">The method to which the Substitution control is bound is specified via the **MethodName** property.</span></span> <span data-ttu-id="2f19d-310">该方法必须满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="2f19d-310">That method must meet the following criteria:</span></span>

- <span data-ttu-id="2f19d-311">它必须是静态 (在中共享 VB) 方法。</span><span class="sxs-lookup"><span data-stu-id="2f19d-311">It must be a static (shared in VB) method.</span></span>
- <span data-ttu-id="2f19d-312">它接受一个类型参数的 HttpContext。</span><span class="sxs-lookup"><span data-stu-id="2f19d-312">It accepts one parameter of type HttpContext.</span></span>
- <span data-ttu-id="2f19d-313">它返回一个字符串，表示应将为页面上的控件的标记。</span><span class="sxs-lookup"><span data-stu-id="2f19d-313">It returns a string representing the markup that should replace the control on the page.</span></span>

<span data-ttu-id="2f19d-314">替换控件不具有修改的页上，任何其他控件的功能，但它确实有权访问的当前 HttpContext 中，通过其参数。</span><span class="sxs-lookup"><span data-stu-id="2f19d-314">The Substitution control does not have the ability to modify any other control on the page, but it does have access to the current HttpContext via its parameter.</span></span>

## <a name="gridview-control"></a><span data-ttu-id="2f19d-315">GridView 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-315">GridView Control</span></span>

<span data-ttu-id="2f19d-316">GridView 控件是 DataGrid 控件的替代。</span><span class="sxs-lookup"><span data-stu-id="2f19d-316">The GridView control is the replacement for the DataGrid control.</span></span> <span data-ttu-id="2f19d-317">此控件将在更高版本的模块中的更详细地介绍。</span><span class="sxs-lookup"><span data-stu-id="2f19d-317">This control will be covered in more detail in a later module.</span></span>

## <a name="detailsview-control"></a><span data-ttu-id="2f19d-318">在 DetailsView 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-318">DetailsView Control</span></span>

<span data-ttu-id="2f19d-319">在 DetailsView 控件可以显示来自数据源的单个记录，还可以编辑或删除它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-319">The DetailsView control allows you to display a single record from a data source and to edit or delete it.</span></span> <span data-ttu-id="2f19d-320">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-320">It is covered in more detail in a later module.</span></span>

## <a name="formview-control"></a><span data-ttu-id="2f19d-321">FormView 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-321">FormView Control</span></span>

<span data-ttu-id="2f19d-322">使用 FormView 控件在可配置界面中显示来自数据源的单个记录。</span><span class="sxs-lookup"><span data-stu-id="2f19d-322">The FormView control is used to display a single record from a datasource in a configurable interface.</span></span> <span data-ttu-id="2f19d-323">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-323">It is covered in more detail in a later module.</span></span>

## <a name="accessdatasource-control"></a><span data-ttu-id="2f19d-324">AccessDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-324">AccessDataSource Control</span></span>

<span data-ttu-id="2f19d-325">AccessDataSource 控件是用于将数据绑定的 Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="2f19d-325">The AccessDataSource control is used to data bind an Access database.</span></span> <span data-ttu-id="2f19d-326">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-326">It is covered in more detail in a later module.</span></span>

## <a name="objectdatasource-control"></a><span data-ttu-id="2f19d-327">ObjectDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-327">ObjectDataSource Control</span></span>

<span data-ttu-id="2f19d-328">ObjectDataSource 控件用于支持三层体系结构，以便控件可以进行数据绑定到中间层业务对象而不是一个两层模型其中控件直接绑定到数据源。</span><span class="sxs-lookup"><span data-stu-id="2f19d-328">The ObjectDataSource control is used to support a three-tier architecture so that controls can be data-bound to a middle-tier business object as opposed to a two-tiered model where controls are bound directly to the data source.</span></span> <span data-ttu-id="2f19d-329">它将在更高版本的模块中的更详细地讨论。</span><span class="sxs-lookup"><span data-stu-id="2f19d-329">It will be discussed in more detail in a later module.</span></span>

## <a name="xmldatasource-control"></a><span data-ttu-id="2f19d-330">XmlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-330">XmlDataSource Control</span></span>

<span data-ttu-id="2f19d-331">XmlDataSource 控件用于将数据绑定到 XML 数据源。</span><span class="sxs-lookup"><span data-stu-id="2f19d-331">The XmlDataSource control is used to data bind to an XML data source.</span></span> <span data-ttu-id="2f19d-332">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-332">It is covered in more detail in a later module.</span></span>

## <a name="sitemapdatasource-control"></a><span data-ttu-id="2f19d-333">SiteMapDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-333">SiteMapDataSource Control</span></span>

<span data-ttu-id="2f19d-334">SiteMapDataSource 控件提供了基于站点图站点导航控件的数据绑定。</span><span class="sxs-lookup"><span data-stu-id="2f19d-334">The SiteMapDataSource control provides data binding for site navigation controls based on a site map.</span></span> <span data-ttu-id="2f19d-335">它将在更高版本的模块中的更详细地讨论。</span><span class="sxs-lookup"><span data-stu-id="2f19d-335">It will be discussed in more detail in a later module.</span></span>

## <a name="sitemappath-control"></a><span data-ttu-id="2f19d-336">SiteMapPath 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-336">SiteMapPath Control</span></span>

<span data-ttu-id="2f19d-337">SiteMapPath 控件显示一的系列通常称为痕迹导航链接。</span><span class="sxs-lookup"><span data-stu-id="2f19d-337">The SiteMapPath control displays a series of navigation links commonly referred to as breadcrumbs.</span></span> <span data-ttu-id="2f19d-338">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-338">It is covered in more detail in a later module.</span></span>

## <a name="menu-control"></a><span data-ttu-id="2f19d-339">Menu 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-339">Menu Control</span></span>

<span data-ttu-id="2f19d-340">菜单控件将显示使用 DHTML 的动态菜单。</span><span class="sxs-lookup"><span data-stu-id="2f19d-340">The Menu control displays dynamic menus using DHTML.</span></span> <span data-ttu-id="2f19d-341">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-341">It is covered in more detail in a later module.</span></span>

## <a name="treeview-control"></a><span data-ttu-id="2f19d-342">TreeView 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-342">TreeView Control</span></span>

<span data-ttu-id="2f19d-343">TreeView 控件用于显示数据的层次结构树视图。</span><span class="sxs-lookup"><span data-stu-id="2f19d-343">The TreeView control is used to display a hierarchical tree view of data.</span></span> <span data-ttu-id="2f19d-344">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-344">It is covered in more detail in a later module.</span></span>

## <a name="login-control"></a><span data-ttu-id="2f19d-345">Login 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-345">Login Control</span></span>

<span data-ttu-id="2f19d-346">Login 控件提供一种机制来登录到网站。</span><span class="sxs-lookup"><span data-stu-id="2f19d-346">The Login control provides for a mechanism to log into a Web site.</span></span> <span data-ttu-id="2f19d-347">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-347">It is covered in more detail in a later module.</span></span>

## <a name="loginview-control"></a><span data-ttu-id="2f19d-348">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-348">LoginView Control</span></span>

<span data-ttu-id="2f19d-349">LoginView 控件可让不同的模板根据用户的登录状态的显示器。</span><span class="sxs-lookup"><span data-stu-id="2f19d-349">The LoginView control allows for the display of different templates based upon a user's login status.</span></span> <span data-ttu-id="2f19d-350">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-350">It is covered in more detail in a later module.</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="2f19d-351">PasswordRecovery 控件</span><span class="sxs-lookup"><span data-stu-id="2f19d-351">PasswordRecovery Control</span></span>

<span data-ttu-id="2f19d-352">PasswordRecovery 控件用于 ASP.NET 应用程序的用户检索忘记的密码。</span><span class="sxs-lookup"><span data-stu-id="2f19d-352">The PasswordRecovery control is used to retrieve forgotten passwords by users of an ASP.NET application.</span></span> <span data-ttu-id="2f19d-353">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-353">It is covered in more detail in a later module.</span></span>

## <a name="loginstatus"></a><span data-ttu-id="2f19d-354">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="2f19d-354">LoginStatus</span></span>

<span data-ttu-id="2f19d-355">LoginStatus 控件显示用户的登录状态。</span><span class="sxs-lookup"><span data-stu-id="2f19d-355">The LoginStatus control displays a user's login status.</span></span> <span data-ttu-id="2f19d-356">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-356">It is covered in more detail in a later module.</span></span>

## <a name="loginname"></a><span data-ttu-id="2f19d-357">LoginName</span><span class="sxs-lookup"><span data-stu-id="2f19d-357">LoginName</span></span>

<span data-ttu-id="2f19d-358">登录到 ASP.NET 应用程序后，LoginName 控件显示用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="2f19d-358">The LoginName control displays a user's username after being logged into an ASP.NET application.</span></span> <span data-ttu-id="2f19d-359">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-359">It is covered in more detail in a later module.</span></span>

## <a name="createuserwizard"></a><span data-ttu-id="2f19d-360">CreateUserWizard</span><span class="sxs-lookup"><span data-stu-id="2f19d-360">CreateUserWizard</span></span>

<span data-ttu-id="2f19d-361">CreateUserWizard 是一个可配置向导，使用户能够创建 ASP.NET 应用程序中使用的 ASP.NET 成员资格帐户。</span><span class="sxs-lookup"><span data-stu-id="2f19d-361">The CreateUserWizard is a configurable wizard which gives users the ability to create an ASP.NET Membership account for use in an ASP.NET application.</span></span> <span data-ttu-id="2f19d-362">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-362">It is covered in more detail in a later module.</span></span>

## <a name="changepassword"></a><span data-ttu-id="2f19d-363">ChangePassword</span><span class="sxs-lookup"><span data-stu-id="2f19d-363">ChangePassword</span></span>

<span data-ttu-id="2f19d-364">ChangePassword 控件允许用户更改其密码为 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2f19d-364">The ChangePassword control allows users to change their password for an ASP.NET application.</span></span> <span data-ttu-id="2f19d-365">更高版本的模块中的更详细地介绍了它。</span><span class="sxs-lookup"><span data-stu-id="2f19d-365">It is covered in more detail in a later module.</span></span>

## <a name="various-webparts"></a><span data-ttu-id="2f19d-366">各种 web 部件</span><span class="sxs-lookup"><span data-stu-id="2f19d-366">Various WebParts</span></span>

<span data-ttu-id="2f19d-367">ASP.NET 2.0 随附了各种 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="2f19d-367">ASP.NET 2.0 ships with various Web Parts.</span></span> <span data-ttu-id="2f19d-368">这些将在更高版本的模块中的详细介绍。</span><span class="sxs-lookup"><span data-stu-id="2f19d-368">These will be covered in detail in a later module.</span></span>
