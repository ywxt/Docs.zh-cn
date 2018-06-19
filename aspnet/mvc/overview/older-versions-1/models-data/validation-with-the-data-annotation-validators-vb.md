---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 验证与数据批注验证程序 (VB) |Microsoft 文档
author: microsoft
description: 利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。 了解如何使用不同类型的验证程序...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/29/2009
ms.topic: article
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: d1987182a44a0ad3f91f455342dc934d1dd50267
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
ms.locfileid: "30870162"
---
<a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="59305-104">验证与数据批注验证程序 (VB)</span><span class="sxs-lookup"><span data-stu-id="59305-104">Validation with the Data Annotation Validators (VB)</span></span>
====================
<span data-ttu-id="59305-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="59305-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="59305-106">利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="59305-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="59305-107">了解如何使用不同类型的验证程序属性和 Microsoft 实体框架中使用它们。</span><span class="sxs-lookup"><span data-stu-id="59305-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>


<span data-ttu-id="59305-108">在本教程中，您将学习如何使用数据注释验证程序在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="59305-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="59305-109">使用数据注释验证程序的优点是它们使你可以执行验证，只需通过添加一个或多个属性 – 例如必需或 StringLength 属性 – 到类属性。</span><span class="sxs-lookup"><span data-stu-id="59305-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="59305-110">你可以使用数据注释验证程序之前，你必须下载数据批注模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="59305-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="59305-111">你可以从 CodePlex 网站下载数据批注模型联编程序示例，通过单击[此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)。</span><span class="sxs-lookup"><span data-stu-id="59305-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>


<span data-ttu-id="59305-112">请务必了解数据批注模型联编程序不是官方 Microsoft ASP.NET MVC framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="59305-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="59305-113">尽管数据批注模型联编程序已由 Microsoft ASP.NET MVC 团队创建的但 Microsoft 不提供数据批注模型联编程序的官方产品支持所述，然后在本教程中使用。</span><span class="sxs-lookup"><span data-stu-id="59305-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>


## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="59305-114">使用数据批注模型联编程序</span><span class="sxs-lookup"><span data-stu-id="59305-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="59305-115">若要使用 ASP.NET MVC 应用程序中的数据批注模型联编程序，首先需要添加对 Microsoft.Web.Mvc.DataAnnotations.dll 程序集和 System.ComponentModel.DataAnnotations.dll 程序集的引用。</span><span class="sxs-lookup"><span data-stu-id="59305-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="59305-116">选择菜单选项**项目中，添加引用**。</span><span class="sxs-lookup"><span data-stu-id="59305-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="59305-117">接下来，单击**浏览**选项卡，浏览到下载 （并解压缩） 数据批注模型联编程序示例其中的位置 (请参阅**图 1**)。</span><span class="sxs-lookup"><span data-stu-id="59305-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="59305-118">**图 1**： 添加对数据批注模型联编程序的引用 ([单击以查看实际尺寸的图像](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="59305-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="59305-119">选择 Microsoft.Web.Mvc.DataAnnotations.dll 程序集和 System.ComponentModel.DataAnnotations.dll 程序集，然后单击**确定**按钮。</span><span class="sxs-lookup"><span data-stu-id="59305-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>


<span data-ttu-id="59305-120">不能使用与数据批注模型联编程序的.NET Framework Service Pack 1 中包含的 System.ComponentModel.DataAnnotations.dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="59305-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="59305-121">你必须使用包含数据批注模型联编程序示例下载 System.ComponentModel.DataAnnotations.dll 程序集的版本。</span><span class="sxs-lookup"><span data-stu-id="59305-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>


<span data-ttu-id="59305-122">最后，你需要在 Global.asax 文件中注册 DataAnnotations 模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="59305-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="59305-123">将以下代码行添加到应用程序\_start （） 事件处理程序，以便应用程序\_start （） 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="59305-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="59305-124">此代码行将 DataAnnotationsModelBinder 注册为整个 ASP.NET MVC 应用程序的默认模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="59305-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="59305-125">使用数据批注验证程序属性</span><span class="sxs-lookup"><span data-stu-id="59305-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="59305-126">当使用数据批注模型联编程序时，您将使用验证程序属性执行验证。</span><span class="sxs-lookup"><span data-stu-id="59305-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="59305-127">System.ComponentModel.DataAnnotations 命名空间包括以下的验证程序属性：</span><span class="sxs-lookup"><span data-stu-id="59305-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="59305-128">范围 – 使你可以验证是否属性的值介于之间指定的值范围。</span><span class="sxs-lookup"><span data-stu-id="59305-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="59305-129">ReqularExpression – 使你可以验证是否与指定正则表达式模式匹配的属性的值。</span><span class="sxs-lookup"><span data-stu-id="59305-129">ReqularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="59305-130">所需 – 使您能够将根据需要属性标记。</span><span class="sxs-lookup"><span data-stu-id="59305-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="59305-131">StringLength –，可指定的字符串属性的最大长度。</span><span class="sxs-lookup"><span data-stu-id="59305-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="59305-132">验证 – 所有验证程序属性的基类。</span><span class="sxs-lookup"><span data-stu-id="59305-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="59305-133">如果任何标准的验证程序不能满足你的验证需求然后你始终可以通过从基本的验证属性继承新的验证程序属性创建自定义验证程序属性的选项。</span><span class="sxs-lookup"><span data-stu-id="59305-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>


<span data-ttu-id="59305-134">中的产品类**列出 1**演示了如何使用这些验证程序属性。</span><span class="sxs-lookup"><span data-stu-id="59305-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="59305-135">名称、 说明和单价属性标记所需的方式。</span><span class="sxs-lookup"><span data-stu-id="59305-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="59305-136">Name 属性必须是少于 10 个字符的字符串长度。</span><span class="sxs-lookup"><span data-stu-id="59305-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="59305-137">最后，单价属性必须与表示货币金额的正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="59305-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="59305-138">**列表 1**: Models\Product.vb</span><span class="sxs-lookup"><span data-stu-id="59305-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="59305-139">产品类演示了如何使用一个附加的属性： DisplayName 属性。</span><span class="sxs-lookup"><span data-stu-id="59305-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="59305-140">DisplayName 属性，可在一条错误消息中显示属性时修改属性的名称。</span><span class="sxs-lookup"><span data-stu-id="59305-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="59305-141">而不是显示错误消息"UnitPrice 字段必填"你可以显示错误消息"价格字段是必填"。</span><span class="sxs-lookup"><span data-stu-id="59305-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="59305-142">如果你想要完全自定义验证程序显示的错误消息可以将自定义错误消息分配给此类的验证程序的 ErrorMessage 属性： `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="59305-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>


<span data-ttu-id="59305-143">你可以使用中的产品类**列出 1**与中的 create （） 控制器操作**列出 2**。</span><span class="sxs-lookup"><span data-stu-id="59305-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="59305-144">当模型状态中包含任何错误，则此控制器操作重新显示创建视图。</span><span class="sxs-lookup"><span data-stu-id="59305-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="59305-145">**列出 2**: Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="59305-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="59305-146">最后，你可以在其中创建中的视图**列出 3**右键单击 create （） 操作并选择菜单选项**添加视图**。</span><span class="sxs-lookup"><span data-stu-id="59305-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="59305-147">作为模型类使用的产品类来创建强类型视图。</span><span class="sxs-lookup"><span data-stu-id="59305-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="59305-148">选择**创建**视图内容的下拉列表中 (请参阅**图 2**)。</span><span class="sxs-lookup"><span data-stu-id="59305-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="59305-149">**图 2**： 添加 Create 视图</span><span class="sxs-lookup"><span data-stu-id="59305-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="59305-150">**列出 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="59305-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="59305-151">从生成的创建表单中删除 Id 字段**添加视图**菜单选项。</span><span class="sxs-lookup"><span data-stu-id="59305-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="59305-152">Id 字段对应于标识列，因为你不想要允许用户输入此字段的值。</span><span class="sxs-lookup"><span data-stu-id="59305-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>


<span data-ttu-id="59305-153">如果提交的窗体创建产品并且不要为必填的字段中，输入值，则验证错误消息中**图 3**显示。</span><span class="sxs-lookup"><span data-stu-id="59305-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="59305-154">**图 3**： 缺少必填的字段</span><span class="sxs-lookup"><span data-stu-id="59305-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="59305-155">如果输入无效的货币金额，然后中的错误消息**图 4**显示。</span><span class="sxs-lookup"><span data-stu-id="59305-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="59305-156">**图 4**： 无效的货币金额</span><span class="sxs-lookup"><span data-stu-id="59305-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="59305-157">使用随实体框架数据批注验证程序</span><span class="sxs-lookup"><span data-stu-id="59305-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="59305-158">如果你使用 Microsoft 实体框架来生成你的数据模型类不能将验证程序属性应用直接向你的类。</span><span class="sxs-lookup"><span data-stu-id="59305-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="59305-159">因为实体框架设计器生成的模型类下, 一步时在设计器中进行任何更改将覆盖您对模型类进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="59305-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="59305-160">如果你想要使用实体框架生成的类中使用验证程序然后你需要创建元数据类。</span><span class="sxs-lookup"><span data-stu-id="59305-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="59305-161">你将验证程序应用于元数据类，而不是将验证程序应用到实际类。</span><span class="sxs-lookup"><span data-stu-id="59305-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="59305-162">例如，想象一下这样，你已创建了使用实体框架的电影类 (请参阅**图 5**)。</span><span class="sxs-lookup"><span data-stu-id="59305-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="59305-163">此外，假设你想要使影片标题和控制器属性所需的属性。</span><span class="sxs-lookup"><span data-stu-id="59305-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="59305-164">在这种情况下，你可以在其中创建分部类和中的元数据类**列出 4**。</span><span class="sxs-lookup"><span data-stu-id="59305-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="59305-165">**图 5**： 生成的实体框架的电影类</span><span class="sxs-lookup"><span data-stu-id="59305-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="59305-166">**列出 4**: Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="59305-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="59305-167">中的文件**列出 4**包含名为电影和 MovieMetaData 的两个类。</span><span class="sxs-lookup"><span data-stu-id="59305-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="59305-168">电影类是分部类。</span><span class="sxs-lookup"><span data-stu-id="59305-168">The Movie class is a partial class.</span></span> <span data-ttu-id="59305-169">它对应于 DataModel.Designer.vb 文件中包含的实体框架生成的分部类。</span><span class="sxs-lookup"><span data-stu-id="59305-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="59305-170">目前，.NET framework 不支持部分属性。</span><span class="sxs-lookup"><span data-stu-id="59305-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="59305-171">因此，没有方法将验证程序特性应用于电影类将验证程序特性应用到的属性内的文件中定义的电影类 DataModel.Designer.vb 文件中定义的属性**列出 4**.</span><span class="sxs-lookup"><span data-stu-id="59305-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="59305-172">请注意，具有指向 MovieMetaData 类 MetadataType 属性修饰电影分部类。</span><span class="sxs-lookup"><span data-stu-id="59305-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="59305-173">MovieMetaData 类包含属性的电影类的代理属性。</span><span class="sxs-lookup"><span data-stu-id="59305-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="59305-174">验证程序特性应用到 MovieMetaData 类的属性。</span><span class="sxs-lookup"><span data-stu-id="59305-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="59305-175">标题、 控制器和 DateReleased 属性所有被标记为必需属性。</span><span class="sxs-lookup"><span data-stu-id="59305-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="59305-176">必须将控制器属性分配包含小于 5 个字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="59305-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="59305-177">最后，DisplayName 属性应用于要显示一条错误消息，如"日期发布字段是必需的。"的 DateReleased 属性</span><span class="sxs-lookup"><span data-stu-id="59305-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="59305-178">而不是错误"DateReleased 字段是必需的。"</span><span class="sxs-lookup"><span data-stu-id="59305-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="59305-179">请注意，不需要 MovieMetaData 类中的代理属性来表示电影类中的相应属性相同的类型。</span><span class="sxs-lookup"><span data-stu-id="59305-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="59305-180">例如，目录属性是电影类中的字符串属性和 MovieMetaData 类中的对象属性。</span><span class="sxs-lookup"><span data-stu-id="59305-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>


<span data-ttu-id="59305-181">中的页**图 6**演示当电影属性中输入无效值时，返回的错误消息。</span><span class="sxs-lookup"><span data-stu-id="59305-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="59305-182">**图 6**： 使用实体框架的验证程序 ([单击以查看实际尺寸的图像](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="59305-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="59305-183">总结</span><span class="sxs-lookup"><span data-stu-id="59305-183">Summary</span></span>

<span data-ttu-id="59305-184">在本教程中，您学习了如何充分利用数据批注模型联编程序来执行验证的 ASP.NET MVC 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="59305-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="59305-185">您学习了如何使用不同类型的如所需的验证程序属性和 StringLength 属性。</span><span class="sxs-lookup"><span data-stu-id="59305-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="59305-186">你还了解了如何使用 Microsoft 实体框架时使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="59305-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="59305-187">上一篇</span><span class="sxs-lookup"><span data-stu-id="59305-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
