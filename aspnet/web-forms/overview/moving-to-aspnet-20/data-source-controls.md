---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: "数据源控件 |Microsoft 文档"
author: microsoft
description: "DataGrid 控件在 ASP.NET 1.x 标记为 Web 应用程序中的数据访问中的重大改进。 但是，它不是因为它可能是用户友好..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: b1ac7fb62767d61c97fe00338bc0f5087f4863b5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2018
---
<a name="data-source-controls"></a><span data-ttu-id="74343-104">数据源控件</span><span class="sxs-lookup"><span data-stu-id="74343-104">Data Source Controls</span></span>
====================
<span data-ttu-id="74343-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="74343-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="74343-106">DataGrid 控件在 ASP.NET 1.x 标记为 Web 应用程序中的数据访问中的重大改进。</span><span class="sxs-lookup"><span data-stu-id="74343-106">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="74343-107">但是，它不是因为它可能是用户友好。</span><span class="sxs-lookup"><span data-stu-id="74343-107">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="74343-108">它仍然需要相当长的代码可以从中获得多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="74343-108">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="74343-109">在所有数据访问工作中中 1.x 模型就是这样。</span><span class="sxs-lookup"><span data-stu-id="74343-109">Such is the model in all data access endeavors in 1.x.</span></span>


<span data-ttu-id="74343-110">DataGrid 控件在 ASP.NET 1.x 标记为 Web 应用程序中的数据访问中的重大改进。</span><span class="sxs-lookup"><span data-stu-id="74343-110">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="74343-111">但是，它不是因为它可能是用户友好。</span><span class="sxs-lookup"><span data-stu-id="74343-111">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="74343-112">它仍然需要相当长的代码可以从中获得多有用的功能。</span><span class="sxs-lookup"><span data-stu-id="74343-112">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="74343-113">在所有数据访问工作中中 1.x 模型就是这样。</span><span class="sxs-lookup"><span data-stu-id="74343-113">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="74343-114">ASP.NET 2.0 解决此问题与部分与数据源控件。</span><span class="sxs-lookup"><span data-stu-id="74343-114">ASP.NET 2.0 addresses this with in part with data source controls.</span></span> <span data-ttu-id="74343-115">ASP.NET 2.0 中的数据源控件提供开发人员提供用于检索数据，显示数据，和编辑数据的声明性模型。</span><span class="sxs-lookup"><span data-stu-id="74343-115">The data source controls in ASP.NET 2.0 provide developers with a declarative model for retrieving data, displaying data, and editing data.</span></span> <span data-ttu-id="74343-116">数据源控件的用途是提供一致数据的表示形式而不考虑这些数据源的数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="74343-116">The purpose of data source controls is to provide a consistent representation of data to data-bound controls regardless of the source of those data.</span></span> <span data-ttu-id="74343-117">ASP.NET 2.0 中的数据源控件的核心是 DataSourceControl 抽象类。</span><span class="sxs-lookup"><span data-stu-id="74343-117">At the heart of the data source controls in ASP.NET 2.0 is the DataSourceControl abstract class.</span></span> <span data-ttu-id="74343-118">DataSourceControl 类提供基实现的 IDataSource 接口和 IListSource 接口，后者允许你要分配为数据绑定控件 （通过新的 DataSourceId 属性的数据源的数据源控件讨论更高版本） 和公开这样的其中作为列表的数据。</span><span class="sxs-lookup"><span data-stu-id="74343-118">The DataSourceControl class provides a base implementation of the IDataSource interface and the IListSource interface, the latter of which allows you to assign the data source control as the DataSource of a data-bound control (via the new DataSourceId property discussed later) and expose the data therein as a list.</span></span> <span data-ttu-id="74343-119">每个列表的数据从数据源控件公开为 DataSourceView 对象。</span><span class="sxs-lookup"><span data-stu-id="74343-119">Each list of data from a data source control is exposed as a DataSourceView object.</span></span> <span data-ttu-id="74343-120">由 IDataSource 接口提供对 DataSourceView 实例的访问。</span><span class="sxs-lookup"><span data-stu-id="74343-120">Access to the DataSourceView instances is provided by the IDataSource interface.</span></span> <span data-ttu-id="74343-121">例如，GetViewNames 方法返回与特定数据源控件，使您能够枚举 DataSourceViews ICollection 关联和 GetView 方法允许你按名称访问特定的 DataSourceView 实例。</span><span class="sxs-lookup"><span data-stu-id="74343-121">For example, the GetViewNames method returns an ICollection that allows you to enumerate the DataSourceViews associated with a particular data source control, and the GetView method allows you to access a particular DataSourceView instance by name.</span></span>

<span data-ttu-id="74343-122">数据源控件具有没有用户界面。</span><span class="sxs-lookup"><span data-stu-id="74343-122">Data source controls have no user-interface.</span></span> <span data-ttu-id="74343-123">作为服务器控件，以便它们可以支持声明性语法，并且它们到页面状态具有访问权限，如果需要实现它们。</span><span class="sxs-lookup"><span data-stu-id="74343-123">They are implemented as server controls so that they can support declarative syntax and so that they have access to page state if desired.</span></span> <span data-ttu-id="74343-124">数据源控件向客户端不呈现任何 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="74343-124">Data source controls do not render any HTML markup to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="74343-125">正如您将看到更高版本，那里还缓存通过使用数据源控件获得的好处。</span><span class="sxs-lookup"><span data-stu-id="74343-125">As you'll see later, there are also caching benefits obtained by using data source controls.</span></span>


## <a name="storing-connection-strings"></a><span data-ttu-id="74343-126">存储连接字符串</span><span class="sxs-lookup"><span data-stu-id="74343-126">Storing Connection Strings</span></span>

<span data-ttu-id="74343-127">我们深入探讨着眼于如何配置数据源控件之前，我们应涵盖有关连接字符串的 ASP.NET 2.0 中的新功能。</span><span class="sxs-lookup"><span data-stu-id="74343-127">Before we get into looking at how to configure data source controls, we should cover a new capability in ASP.NET 2.0 concerning connection strings.</span></span> <span data-ttu-id="74343-128">ASP.NET 2.0 引入了新的节，您可以轻松地存储连接字符串可在运行时动态读取配置文件中。</span><span class="sxs-lookup"><span data-stu-id="74343-128">ASP.NET 2.0 introduces a new section in the configuration file that allows you to easily store connection strings that can be read dynamically at runtime.</span></span> <span data-ttu-id="74343-129">&lt;ConnectionStrings&gt;部分可以轻松地存储连接字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-129">The &lt;connectionStrings&gt; section makes it easy to store connection strings.</span></span>

<span data-ttu-id="74343-130">下面的代码段添加一个新的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-130">The snippet below adds a new connection string.</span></span>

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="74343-131">正如使用&lt;appSettings&gt;部分中， &lt;connectionStrings&gt;部分会出现之外&lt;system.web&gt;配置文件中的部分。</span><span class="sxs-lookup"><span data-stu-id="74343-131">Just as with the &lt;appSettings&gt; section, the &lt;connectionStrings&gt; section appears outside of the &lt;system.web&gt; section in the configuration file.</span></span>


<span data-ttu-id="74343-132">若要使用此连接字符串，可以使用以下语法设置服务器控件的 ConnectionString 属性时。</span><span class="sxs-lookup"><span data-stu-id="74343-132">To use this connection string, you can use the following syntax when setting the ConnectionString attribute of a server control.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

<span data-ttu-id="74343-133">&lt;ConnectionStrings&gt;部分也被加密，因此不公开敏感信息。</span><span class="sxs-lookup"><span data-stu-id="74343-133">The &lt;connectionStrings&gt; section can also be encrypted so that sensitive information is not exposed.</span></span> <span data-ttu-id="74343-134">这项功能将在更高版本的模块中。</span><span class="sxs-lookup"><span data-stu-id="74343-134">That ability will be covered in a later module.</span></span>

## <a name="caching-data-sources"></a><span data-ttu-id="74343-135">缓存的数据源</span><span class="sxs-lookup"><span data-stu-id="74343-135">Caching Data Sources</span></span>

<span data-ttu-id="74343-136">每个 DataSourceControl 提供四个属性用于配置缓存;EnableCaching、 CacheDuration、 CacheExpirationPolicy 和 CacheKeyDependency。</span><span class="sxs-lookup"><span data-stu-id="74343-136">Each DataSourceControl provides four properties for configuring caching; EnableCaching, CacheDuration, CacheExpirationPolicy, and CacheKeyDependency.</span></span>

## <a name="enablecaching"></a><span data-ttu-id="74343-137">EnableCaching</span><span class="sxs-lookup"><span data-stu-id="74343-137">EnableCaching</span></span>

<span data-ttu-id="74343-138">EnableCaching 是布尔值属性，它确定缓存启用数据源控件。</span><span class="sxs-lookup"><span data-stu-id="74343-138">EnableCaching is a Boolean property that determines whether or not caching is enabled for the data source control.</span></span>

## <a name="cacheduration-property"></a><span data-ttu-id="74343-139">CacheDuration 属性</span><span class="sxs-lookup"><span data-stu-id="74343-139">CacheDuration Property</span></span>

<span data-ttu-id="74343-140">CacheDuration 属性设置缓存就保持有效的秒的数。</span><span class="sxs-lookup"><span data-stu-id="74343-140">The CacheDuration property sets the number of seconds that the cache remains valid.</span></span> <span data-ttu-id="74343-141">此属性设置为**0**使得保持有效之前显式失效的缓存。</span><span class="sxs-lookup"><span data-stu-id="74343-141">Setting this property to **0** causes the cache to remain valid until explicitly invalidated.</span></span>

## <a name="cacheexpirationpolicy-property"></a><span data-ttu-id="74343-142">CacheExpirationPolicy 属性</span><span class="sxs-lookup"><span data-stu-id="74343-142">CacheExpirationPolicy Property</span></span>

<span data-ttu-id="74343-143">CacheExpirationPolicy 属性可以设置为**绝对**或**可调**。</span><span class="sxs-lookup"><span data-stu-id="74343-143">The CacheExpirationPolicy property can be set to either **Absolute** or **Sliding**.</span></span> <span data-ttu-id="74343-144">将其设置为绝对意味着，将缓存数据的时间的最大量是 CacheDuration 属性指定的秒数。</span><span class="sxs-lookup"><span data-stu-id="74343-144">Setting it to Absolute means that the maximum amount of time that the data will be cached is the number of seconds specified by the CacheDuration property.</span></span> <span data-ttu-id="74343-145">通过将它设置为可调，执行每个操作时重置的过期时间。</span><span class="sxs-lookup"><span data-stu-id="74343-145">By setting it to Sliding, the expiration time is reset when each operation is performed.</span></span>

## <a name="cachekeydependency-property"></a><span data-ttu-id="74343-146">CacheKeyDependency 属性</span><span class="sxs-lookup"><span data-stu-id="74343-146">CacheKeyDependency Property</span></span>

<span data-ttu-id="74343-147">如果为 CacheKeyDependency 属性指定的字符串值，ASP.NET 将设置该字符串上基于新的缓存依赖项。</span><span class="sxs-lookup"><span data-stu-id="74343-147">If a string value is specified for the CacheKeyDependency property, ASP.NET will set up a new cache dependency based on that string.</span></span> <span data-ttu-id="74343-148">这允许您显式使缓存失效的通过只需更改或删除 CacheKeyDependency。</span><span class="sxs-lookup"><span data-stu-id="74343-148">This allows you to explicitly invalidate the cache by simply changing or removing the CacheKeyDependency.</span></span>

<span data-ttu-id="74343-149">**重要**： 如果模拟已启用和访问数据源和/或数据的内容取决于客户端标识，则我们建议，缓存不可用将 EnableCaching 设置为 False。</span><span class="sxs-lookup"><span data-stu-id="74343-149">**Important**: If impersonation is enabled and access to the data source and/or content of data are based upon client identity, it is recommended that caching be disabled by setting EnableCaching to False.</span></span> <span data-ttu-id="74343-150">如果在此方案中启用了缓存，并最初请求数据的用户以外的用户发出的请求，授权与数据源不会强制执行。</span><span class="sxs-lookup"><span data-stu-id="74343-150">If caching is enabled in this scenario and a user other than the user who originally requested the data issues a request, authorization to the data source is not enforced.</span></span> <span data-ttu-id="74343-151">只需将从缓存中提供数据。</span><span class="sxs-lookup"><span data-stu-id="74343-151">The data will simply be served from cache.</span></span>

## <a name="the-sqldatasource-control"></a><span data-ttu-id="74343-152">SqlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="74343-152">The SqlDataSource Control</span></span>

<span data-ttu-id="74343-153">SqlDataSource 控件允许开发人员为访问存储在支持 ADO.NET 任何关系数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="74343-153">The SqlDataSource control allows a developer to access data stored in any relational database that supports ADO.NET.</span></span> <span data-ttu-id="74343-154">它可以使用 System.Data.SqlClient 提供程序访问 SQL Server 数据库、 System.Data.OleDb 提供程序、 System.Data.Odbc 提供程序或要访问 Oracle 的 System.Data.OracleClient 提供程序。</span><span class="sxs-lookup"><span data-stu-id="74343-154">It can use the System.Data.SqlClient provider to access a SQL Server database, the System.Data.OleDb provider, the System.Data.Odbc provider, or the System.Data.OracleClient provider to access Oracle.</span></span> <span data-ttu-id="74343-155">因此，SqlDataSource 肯定不仅用于访问 SQL Server 数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="74343-155">Therefore, the SqlDataSource is certainly not only used for accessing data in a SQL Server database.</span></span>

<span data-ttu-id="74343-156">若要使用 SqlDataSource，你只需为 ConnectionString 属性提供值和指定的 SQL 命令或存储过程。</span><span class="sxs-lookup"><span data-stu-id="74343-156">In order to use the SqlDataSource, you simply provide a value for the ConnectionString property and specify a SQL command or stored procedure.</span></span> <span data-ttu-id="74343-157">SqlDataSource 控件负责使用的基础 ADO.NET 体系结构。</span><span class="sxs-lookup"><span data-stu-id="74343-157">The SqlDataSource control takes care of working with the underlying ADO.NET architecture.</span></span> <span data-ttu-id="74343-158">它将打开的连接、 查询数据源或执行存储的过程，返回的数据，然后关闭你的连接。</span><span class="sxs-lookup"><span data-stu-id="74343-158">It opens the connection, queries the data source or executes the stored procedure, returns the data, and then closes the connection for you.</span></span>

> [!NOTE]
> <span data-ttu-id="74343-159">因为 DataSourceControl 类会自动关闭你的连接，它应减少客户调用生成的泄露数据库连接数。</span><span class="sxs-lookup"><span data-stu-id="74343-159">Because the DataSourceControl class automatically closes the connection for you, it should reduce the number of customer calls generated by leaking database connections.</span></span>


<span data-ttu-id="74343-160">以下代码段将 DropDownList 控件绑定到 SqlDataSource 控件使用如上所示的配置文件中存储的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-160">The code snippet below binds a DropDownList control to a SqlDataSource control using the connection string that is stored in the configuration file as shown above.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

<span data-ttu-id="74343-161">如上图所示，SqlDataSource DataSourceMode 属性指定数据源的模式。</span><span class="sxs-lookup"><span data-stu-id="74343-161">As illustrated above, the DataSourceMode property of the SqlDataSource specifies the mode for the data source.</span></span> <span data-ttu-id="74343-162">在上面的示例中，DataSourceMode 设置为 DataReader。</span><span class="sxs-lookup"><span data-stu-id="74343-162">In the example above, the DataSourceMode is set to DataReader.</span></span> <span data-ttu-id="74343-163">在这种情况下，SqlDataSource 将返回使用和只进只读游标的 IDataReader 对象。</span><span class="sxs-lookup"><span data-stu-id="74343-163">In that case, the SqlDataSource will return an IDataReader object using a forward-only and read-only cursor.</span></span> <span data-ttu-id="74343-164">返回对象的指定的类型的提供程序使用由控制。</span><span class="sxs-lookup"><span data-stu-id="74343-164">The specified type of object that is returned is controlled by the provider that is used.</span></span> <span data-ttu-id="74343-165">在这种情况下，我正在使用 System.Data.SqlClient 提供程序中指定&lt;connectionStrings&gt; web.config 文件的部分。</span><span class="sxs-lookup"><span data-stu-id="74343-165">In this case, I'm using the System.Data.SqlClient provider as specified in the &lt;connectionStrings&gt; section of the web.config file.</span></span> <span data-ttu-id="74343-166">因此，返回的对象将是类型 SqlDataReader。</span><span class="sxs-lookup"><span data-stu-id="74343-166">Therefore, the object that is returned will be of type SqlDataReader.</span></span> <span data-ttu-id="74343-167">通过指定 DataSourceMode 值的数据集，数据可以存储在服务器上的数据集。</span><span class="sxs-lookup"><span data-stu-id="74343-167">By specifying a DataSourceMode value of DataSet, the data can be stored in a DataSet on the server.</span></span> <span data-ttu-id="74343-168">此模式可用于添加功能，例如排序、 分页，等等。如果我已经数据绑定到 GridView 控件 SqlDataSource，我将选择的数据集模式。</span><span class="sxs-lookup"><span data-stu-id="74343-168">This mode allows you to add features such as sorting, paging, etc. If I had been data-binding the SqlDataSource to a GridView control, I would have chosen the DataSet mode.</span></span> <span data-ttu-id="74343-169">但是，对于 DropDownList DataReader 模式是正确的选择。</span><span class="sxs-lookup"><span data-stu-id="74343-169">However, in the case of a DropDownList, the DataReader mode is the correct choice.</span></span>

> [!NOTE]
> <span data-ttu-id="74343-170">当缓存 SqlDataSource 或 AccessDataSource，DataSourceMode 属性必须设置为数据集。</span><span class="sxs-lookup"><span data-stu-id="74343-170">When caching a SqlDataSource or an AccessDataSource, the DataSourceMode property must be set to DataSet.</span></span> <span data-ttu-id="74343-171">如果你启用与 DataSourceMode DataReader 缓存，则会发生异常。</span><span class="sxs-lookup"><span data-stu-id="74343-171">An exception will occur if you enable caching with a DataSourceMode of DataReader.</span></span>


## <a name="sqldatasource-properties"></a><span data-ttu-id="74343-172">SqlDataSource 属性</span><span class="sxs-lookup"><span data-stu-id="74343-172">SqlDataSource Properties</span></span>

<span data-ttu-id="74343-173">以下是一些 SqlDataSource 控件的属性。</span><span class="sxs-lookup"><span data-stu-id="74343-173">The following are some of the properties of the SqlDataSource control.</span></span>

### <a name="cancelselectonnullparameter"></a><span data-ttu-id="74343-174">CancelSelectOnNullParameter</span><span class="sxs-lookup"><span data-stu-id="74343-174">CancelSelectOnNullParameter</span></span>

<span data-ttu-id="74343-175">一个布尔值，指定是否已取消选择命令，是否其中一个参数为 null。</span><span class="sxs-lookup"><span data-stu-id="74343-175">A Boolean value that specifies whether a select command is canceled if one of the parameters is null.</span></span> <span data-ttu-id="74343-176">默认情况下，则为 true。</span><span class="sxs-lookup"><span data-stu-id="74343-176">True by default.</span></span>

### <a name="conflictdetection"></a><span data-ttu-id="74343-177">ConflictDetection</span><span class="sxs-lookup"><span data-stu-id="74343-177">ConflictDetection</span></span>

<span data-ttu-id="74343-178">其中多个用户可能正在更新数据源在同一时间的情况下，ConflictDetection 属性确定 SqlDataSource 控件的行为。</span><span class="sxs-lookup"><span data-stu-id="74343-178">In a situation where multiple users may be updating a data source at the same time, the ConflictDetection property determines the behavior of the SqlDataSource control.</span></span> <span data-ttu-id="74343-179">此属性的计算结果为 ConflictOptions 枚举值之一。</span><span class="sxs-lookup"><span data-stu-id="74343-179">This property evaluates to one of the values of the ConflictOptions enumeration.</span></span> <span data-ttu-id="74343-180">这些值为**CompareAllValues**和**OverwriteChanges**。</span><span class="sxs-lookup"><span data-stu-id="74343-180">Those values are **CompareAllValues** and **OverwriteChanges**.</span></span> <span data-ttu-id="74343-181">如果设置为 OverwriteChanges，若要将数据写入到数据源的最后一个人将覆盖任何以前的更改。</span><span class="sxs-lookup"><span data-stu-id="74343-181">If set to OverwriteChanges, the last person to write data to the data source overwrites any previous changes.</span></span> <span data-ttu-id="74343-182">但是，如果 ConflictDetection 属性设置为 CompareAllValues，SelectCommand 返回的列创建参数，参数还会创建以每个允许到 SqlDataSource 这些列中保存的原始值确定由于 SelectCommand 已执行，因此，发生了变化的值。</span><span class="sxs-lookup"><span data-stu-id="74343-182">However, if the ConflictDetection property is set to CompareAllValues, parameters get created for the columns returned by the SelectCommand and parameters are also created to hold the original values in each of those columns allowing the SqlDataSource to determine whether or not the values have changed since the SelectCommand was executed.</span></span>

### <a name="deletecommand"></a><span data-ttu-id="74343-183">DeleteCommand</span><span class="sxs-lookup"><span data-stu-id="74343-183">DeleteCommand</span></span>

<span data-ttu-id="74343-184">设置或获取从数据库中删除行时使用的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-184">Sets or gets the SQL string used when deleting rows from the database.</span></span> <span data-ttu-id="74343-185">这可以是 SQL 查询或存储的过程名称。</span><span class="sxs-lookup"><span data-stu-id="74343-185">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="deletecommandtype"></a><span data-ttu-id="74343-186">DeleteCommandType</span><span class="sxs-lookup"><span data-stu-id="74343-186">DeleteCommandType</span></span>

<span data-ttu-id="74343-187">设置或 SQL 查询 （文本） 或存储的过程 (StoredProcedure) 或者获取 delete 命令的类型。</span><span class="sxs-lookup"><span data-stu-id="74343-187">Sets or gets the type of delete command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="deleteparameters"></a><span data-ttu-id="74343-188">DeleteParameters</span><span class="sxs-lookup"><span data-stu-id="74343-188">DeleteParameters</span></span>

<span data-ttu-id="74343-189">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象 DeleteCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="74343-189">Returns the parameters that are used by the DeleteCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="oldvaluesparameterformatstring"></a><span data-ttu-id="74343-190">OldValuesParameterFormatString</span><span class="sxs-lookup"><span data-stu-id="74343-190">OldValuesParameterFormatString</span></span>

<span data-ttu-id="74343-191">此属性用于指定在其中 ConflictDetection 属性设置为 CompareAllValues 的情况下的原始值参数的格式。</span><span class="sxs-lookup"><span data-stu-id="74343-191">This property is used to specify the format of the original value parameters in cases where the ConflictDetection property is set to CompareAllValues.</span></span> <span data-ttu-id="74343-192">默认值为 {0} 这意味着原始值参数将采用与原始参数同名。</span><span class="sxs-lookup"><span data-stu-id="74343-192">The default is {0} which means that original value parameters will take the same name as the original parameter.</span></span> <span data-ttu-id="74343-193">换而言之，如果字段名称为雇员 id，原始值参数将为@EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="74343-193">In other words, if the field name is EmployeeID, the original value parameter would be @EmployeeID.</span></span>

### <a name="selectcommand"></a><span data-ttu-id="74343-194">SelectCommand</span><span class="sxs-lookup"><span data-stu-id="74343-194">SelectCommand</span></span>

<span data-ttu-id="74343-195">设置或获取用于从数据库检索数据的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-195">Sets or gets the SQL string that is used to retrieve data from the database.</span></span> <span data-ttu-id="74343-196">这可以是 SQL 查询或存储的过程名称。</span><span class="sxs-lookup"><span data-stu-id="74343-196">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="selectcommandtype"></a><span data-ttu-id="74343-197">SelectCommandType</span><span class="sxs-lookup"><span data-stu-id="74343-197">SelectCommandType</span></span>

<span data-ttu-id="74343-198">设置或 SQL 查询 （文本） 或存储的过程 (StoredProcedure) 或者获取 select 命令的类型。</span><span class="sxs-lookup"><span data-stu-id="74343-198">Sets or gets the type of select command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="selectparameters"></a><span data-ttu-id="74343-199">SelectParameters</span><span class="sxs-lookup"><span data-stu-id="74343-199">SelectParameters</span></span>

<span data-ttu-id="74343-200">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象 SelectCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="74343-200">Returns the parameters that are used by the SelectCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="sortparametername"></a><span data-ttu-id="74343-201">SortParameterName</span><span class="sxs-lookup"><span data-stu-id="74343-201">SortParameterName</span></span>

<span data-ttu-id="74343-202">获取或设置当使用时会使用对数据进行排序检索数据源控件存储的过程参数的名称。</span><span class="sxs-lookup"><span data-stu-id="74343-202">Gets or sets the name of a stored procedure parameter that is used when sorting data retrieved by the data source control.</span></span> <span data-ttu-id="74343-203">仅在 SelectCommandType 设置为 StoredProcedure 有效。</span><span class="sxs-lookup"><span data-stu-id="74343-203">Valid only when SelectCommandType is set to StoredProcedure.</span></span>

### <a name="sqlcachedependency"></a><span data-ttu-id="74343-204">SqlCacheDependency</span><span class="sxs-lookup"><span data-stu-id="74343-204">SqlCacheDependency</span></span>

<span data-ttu-id="74343-205">指定的数据库和表中的 SQL Server 缓存依赖项使用的以分号分隔字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-205">A semi-colon delimited string specifying the databases and tables used in a SQL Server cache dependency.</span></span> <span data-ttu-id="74343-206">（SQL 缓存依赖项将讨论在更高版本的模块中。）</span><span class="sxs-lookup"><span data-stu-id="74343-206">(SQL cache dependencies will be discussed in a later module.)</span></span>

### <a name="updatecommand"></a><span data-ttu-id="74343-207">UpdateCommand</span><span class="sxs-lookup"><span data-stu-id="74343-207">UpdateCommand</span></span>

<span data-ttu-id="74343-208">设置或获取在更新数据库中的数据时使用的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-208">Sets or gets the SQL string that is used when updating data in the database.</span></span> <span data-ttu-id="74343-209">这可以是 SQL 查询或存储的过程名称。</span><span class="sxs-lookup"><span data-stu-id="74343-209">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="updatecommandtype"></a><span data-ttu-id="74343-210">UpdateCommandType</span><span class="sxs-lookup"><span data-stu-id="74343-210">UpdateCommandType</span></span>

<span data-ttu-id="74343-211">设置或 SQL 查询 （文本） 或存储的过程 (StoredProcedure) 或者获取的更新命令的类型。</span><span class="sxs-lookup"><span data-stu-id="74343-211">Sets or gets the type of update command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="updateparameters"></a><span data-ttu-id="74343-212">UpdateParameters</span><span class="sxs-lookup"><span data-stu-id="74343-212">UpdateParameters</span></span>

<span data-ttu-id="74343-213">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象 UpdateCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="74343-213">Returns the parameters that are used by the UpdateCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

## <a name="the-accessdatasource-control"></a><span data-ttu-id="74343-214">AccessDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="74343-214">The AccessDataSource Control</span></span>

<span data-ttu-id="74343-215">AccessDataSource 控件派生自 SqlDataSource 类，用于数据绑定到 Microsoft Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="74343-215">The AccessDataSource control derives from the SqlDataSource class and is used to data-bind to a Microsoft Access database.</span></span> <span data-ttu-id="74343-216">AccessDataSource 控件的 ConnectionString 属性是只读的属性。</span><span class="sxs-lookup"><span data-stu-id="74343-216">The ConnectionString property for the AccessDataSource control is a read-only property.</span></span> <span data-ttu-id="74343-217">而不是使用 ConnectionString 属性，用于指向 Access 数据库，如下所示的数据文件属性。</span><span class="sxs-lookup"><span data-stu-id="74343-217">Instead of using the ConnectionString property, the DataFile property is used to point to the Access Database as shown below.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

<span data-ttu-id="74343-218">AccessDataSource 将始终设置为 System.Data.OleDb 基 SqlDataSource ProviderName 并连接到使用 Microsoft.Jet.OLEDB.4.0 OLE DB 提供程序的数据库。</span><span class="sxs-lookup"><span data-stu-id="74343-218">The AccessDataSource will always set the ProviderName of the base SqlDataSource to System.Data.OleDb and connects to the database using the Microsoft.Jet.OLEDB.4.0 OLE DB provider.</span></span> <span data-ttu-id="74343-219">AccessDataSource 控件不能用于连接到受密码保护的 Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="74343-219">You cannot use the AccessDataSource control to connect to a password-protected Access database.</span></span> <span data-ttu-id="74343-220">如果你必须连接到受密码保护数据库，则应使用 SqlDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="74343-220">If you have to connect to a password protected database, you should use the SqlDataSource control.</span></span>

> [!NOTE]
> <span data-ttu-id="74343-221">在网站内存储的 access 数据库应放置在应用程序\_数据目录。</span><span class="sxs-lookup"><span data-stu-id="74343-221">Access databases stored within the Web site should be placed in the App\_Data directory.</span></span> <span data-ttu-id="74343-222">ASP.NET 不允许在要浏览此目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="74343-222">ASP.NET does not allow files in this directory to be browsed.</span></span> <span data-ttu-id="74343-223">你将需要授予对应用程序的读取和写入权限的进程帐户\_数据目录时使用 Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="74343-223">You will need to grant the process account Read and Write permissions to the App\_Data directory when using Access databases.</span></span>


## <a name="the-xmldatasource-control"></a><span data-ttu-id="74343-224">XmlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="74343-224">The XmlDataSource Control</span></span>

<span data-ttu-id="74343-225">XmlDataSource 用于数据绑定 XML 数据，数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="74343-225">The XmlDataSource is used to data-bind XML data to data-bound controls.</span></span> <span data-ttu-id="74343-226">你可以将它们绑定到 XML 文件使用数据文件属性或可以绑定到使用数据属性的 XML 字符串。</span><span class="sxs-lookup"><span data-stu-id="74343-226">You can bind to an XML file using the DataFile property or you can bind to an XML string using the Data property.</span></span> <span data-ttu-id="74343-227">XmlDataSource 作为可绑定字段公开 XML 特性。</span><span class="sxs-lookup"><span data-stu-id="74343-227">The XmlDataSource exposes XML attributes as bindable fields.</span></span> <span data-ttu-id="74343-228">在你需要将绑定到不表示为属性的值的情况下，你将需要使用 XSL 转换。</span><span class="sxs-lookup"><span data-stu-id="74343-228">In cases where you need to bind to values that are not represented as attributes, you will need to use an XSL transform.</span></span> <span data-ttu-id="74343-229">你还可以使用筛选 XML 数据的 XPath 表达式。</span><span class="sxs-lookup"><span data-stu-id="74343-229">You can also use XPath expressions to filter XML data.</span></span>

<span data-ttu-id="74343-230">请考虑下面的 XML 文件：</span><span class="sxs-lookup"><span data-stu-id="74343-230">Consider the following XML file:</span></span>

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

<span data-ttu-id="74343-231">请注意，XmlDataSource 使用的 XPath 属性*人员/人员*以便筛选仅&lt;人员&gt;节点。</span><span class="sxs-lookup"><span data-stu-id="74343-231">Notice that the XmlDataSource uses an XPath property of *People/Person* in order to filter on just the &lt;Person&gt; nodes.</span></span> <span data-ttu-id="74343-232">DropDownList 然后数据-将绑定到 LastName 属性使用 DataTextField 属性。</span><span class="sxs-lookup"><span data-stu-id="74343-232">The DropDownList then data-binds to the LastName attribute using the DataTextField property.</span></span>

<span data-ttu-id="74343-233">虽然 XmlDataSource 控件主要用于数据绑定到只读的 XML 数据，则可以编辑 XML 数据文件。</span><span class="sxs-lookup"><span data-stu-id="74343-233">While the XmlDataSource control is primarily used to data-bind to read-only XML data, it is possible to edit the XML data file.</span></span> <span data-ttu-id="74343-234">请注意，在这种情况下，自动插入、 更新和删除的 XML 文件中的信息不会自动与其他数据源控件一样。</span><span class="sxs-lookup"><span data-stu-id="74343-234">Note that in such cases, automatic insertion, updating, and deletion of information in the XML file does not happen automatically as it does with other data source controls.</span></span> <span data-ttu-id="74343-235">相反，你将需要编写代码来手动编辑使用下列方法之一 XmlDataSource 控件的数据。</span><span class="sxs-lookup"><span data-stu-id="74343-235">Instead, you will have to write code to manually edit the data using the following methods of the XmlDataSource control.</span></span>

### <a name="getxmldocument"></a><span data-ttu-id="74343-236">GetXmlDocument</span><span class="sxs-lookup"><span data-stu-id="74343-236">GetXmlDocument</span></span>

<span data-ttu-id="74343-237">检索一个 XmlDocument 对象，包含由 XmlDataSource 检索的 XML 代码。</span><span class="sxs-lookup"><span data-stu-id="74343-237">Retrieves an XmlDocument object containing the XML code retrieved by the XmlDataSource.</span></span>

### <a name="save"></a><span data-ttu-id="74343-238">保存</span><span class="sxs-lookup"><span data-stu-id="74343-238">Save</span></span>

<span data-ttu-id="74343-239">将内存中 XmlDocument 保存回数据源。</span><span class="sxs-lookup"><span data-stu-id="74343-239">Saves the in-memory XmlDocument back to the data source.</span></span>

<span data-ttu-id="74343-240">请务必认识到 Save 方法满足以下两个条件时才会起作用：</span><span class="sxs-lookup"><span data-stu-id="74343-240">It's important to realize that the Save method will only work when the following two conditions are met:</span></span>

1. <span data-ttu-id="74343-241">XmlDataSource 使用数据文件属性绑定到 XML 文件而不是数据属性以将绑定到内存中 XML 数据。</span><span class="sxs-lookup"><span data-stu-id="74343-241">The XmlDataSource is using the DataFile property to bind to an XML file instead of the Data property to bind to in-memory XML data.</span></span>
2. <span data-ttu-id="74343-242">通过转换或 TransformFile 属性不指定任何转换。</span><span class="sxs-lookup"><span data-stu-id="74343-242">No transformation is specified via the Transform or TransformFile property.</span></span>

<span data-ttu-id="74343-243">另请注意 Save 方法可以产生意外的结果时并行调用多个用户。</span><span class="sxs-lookup"><span data-stu-id="74343-243">Note also that the Save method can yield unexpected results when called by multiple users concurrently.</span></span>

## <a name="the-objectdatasource-control"></a><span data-ttu-id="74343-244">ObjectDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="74343-244">The ObjectDataSource Control</span></span>

<span data-ttu-id="74343-245">我们已介绍到目前为止的数据源控件是两个层应用程序的极佳选择数据源控件直接与数据存储通信的位置。</span><span class="sxs-lookup"><span data-stu-id="74343-245">The data source controls that we have covered up to this point are excellent choices for two-tier applications where the data source control communicates directly to the data store.</span></span> <span data-ttu-id="74343-246">但是，许多实际应用程序是多层应用程序可能需要告知这，反过来，与数据层进行通信的业务对象数据源控件。</span><span class="sxs-lookup"><span data-stu-id="74343-246">However, many real-world applications are multi-tier applications where a data source control might need to communicate to a business object which, in turn, communicates with the data layer.</span></span> <span data-ttu-id="74343-247">在这些情况下，ObjectDataSource 精美填充帐单。</span><span class="sxs-lookup"><span data-stu-id="74343-247">In these situations, the ObjectDataSource fills the bill nicely.</span></span> <span data-ttu-id="74343-248">ObjectDataSource 结合使用与源对象。</span><span class="sxs-lookup"><span data-stu-id="74343-248">The ObjectDataSource works in conjunction with a source object.</span></span> <span data-ttu-id="74343-249">ObjectDataSource 控件将创建的源对象，调用指定方法，单个请求的范围内的所有对象实例的释放的实例，如果你的对象已而不是静态方法 （在 Visual Basic 中为共享） 的实例方法。</span><span class="sxs-lookup"><span data-stu-id="74343-249">The ObjectDataSource control will create an instance of the source object, call the specified method, and dispose of the object instance all within the scope of a single request, if your object has instance methods instead of static methods (Shared in Visual Basic).</span></span> <span data-ttu-id="74343-250">因此，你的对象必须是无状态。</span><span class="sxs-lookup"><span data-stu-id="74343-250">Therefore, your object must be stateless.</span></span> <span data-ttu-id="74343-251">也就是说，你的对象应获取和发布在单个请求的范围内的所有所需的资源。</span><span class="sxs-lookup"><span data-stu-id="74343-251">That is, your object should acquire and release all required resources within the span of a single request.</span></span> <span data-ttu-id="74343-252">你可以控制如何通过处理 ObjectDataSource 控件 ObjectCreating 事件创建的源对象。</span><span class="sxs-lookup"><span data-stu-id="74343-252">You can control how the source object is created by handling the ObjectCreating event of the ObjectDataSource control.</span></span> <span data-ttu-id="74343-253">你可以创建的源对象实例和将 ObjectDataSourceEventArgs 类的 ObjectInstance 属性设置为该实例。</span><span class="sxs-lookup"><span data-stu-id="74343-253">You can create an instance of the source object, and then set the ObjectInstance property of the ObjectDataSourceEventArgs class to that instance.</span></span> <span data-ttu-id="74343-254">ObjectDataSource 控件将使用而不是自行创建实例的 ObjectCreating 事件中创建的实例。</span><span class="sxs-lookup"><span data-stu-id="74343-254">The ObjectDataSource control will use the instance that is created in the ObjectCreating event instead of creating an instance on its own.</span></span>

<span data-ttu-id="74343-255">如果 ObjectDataSource 控件源对象公开的公共静态方法 （在 Visual Basic 中为共享） 可以调用来检索和修改数据，ObjectDataSource 控件将直接调用这些方法。</span><span class="sxs-lookup"><span data-stu-id="74343-255">If the source object for an ObjectDataSource control exposes public static methods (Shared in Visual Basic) that can be called to retrieve and modify data, an ObjectDataSource control will call those methods directly.</span></span> <span data-ttu-id="74343-256">如果 ObjectDataSource 控件必须创建源对象的实例，以便进行方法调用，该对象必须包含不带参数的公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="74343-256">If an ObjectDataSource control must create an instance of the source object in order to make method calls, the object must include a public constructor that takes no parameters.</span></span> <span data-ttu-id="74343-257">创建源对象的新实例时，ObjectDataSource 控件将调用此构造函数。</span><span class="sxs-lookup"><span data-stu-id="74343-257">The ObjectDataSource control will call this constructor when it creates a new instance of the source object.</span></span>

<span data-ttu-id="74343-258">如果源对象不包含不带参数的公共构造函数，你可以创建将由 ObjectCreating 事件中的 ObjectDataSource 控件源对象的实例。</span><span class="sxs-lookup"><span data-stu-id="74343-258">If the source object does not contain a public constructor without parameters, you can create an instance of the source object that will be used by the ObjectDataSource control in the ObjectCreating event.</span></span>

## <a name="specifying-object-methods"></a><span data-ttu-id="74343-259">指定对象的方法</span><span class="sxs-lookup"><span data-stu-id="74343-259">Specifying Object Methods</span></span>

<span data-ttu-id="74343-260">ObjectDataSource 控件源对象可以包含任意数量的方法，用于选择、 插入、 更新或删除数据。</span><span class="sxs-lookup"><span data-stu-id="74343-260">The source object for an ObjectDataSource control can contain any number of methods that are used to select, insert, update, or delete data.</span></span> <span data-ttu-id="74343-261">由 ObjectDataSource 控件基于名称的方法，调用这些方法，如通过 ObjectDataSource 控件 SelectMethod、 InsertMethod、 UpdateMethod 或 delete 方法属性标识。</span><span class="sxs-lookup"><span data-stu-id="74343-261">These methods are called by the ObjectDataSource control based on the name of the method, as identified by using either the SelectMethod, InsertMethod, UpdateMethod, or DeleteMethod property of the ObjectDataSource control.</span></span> <span data-ttu-id="74343-262">源对象还可以包括可选的 SelectCount 方法，由使用的 SelectCountMethod 属性，返回的数据源中的对象总数的计数的 ObjectDataSource 控件标识。</span><span class="sxs-lookup"><span data-stu-id="74343-262">The source object can also include an optional SelectCount method, which is identified by the ObjectDataSource control using the SelectCountMethod property, that returns the count of the total number of objects at the data source.</span></span> <span data-ttu-id="74343-263">ObjectDataSource 控件将调用 SelectCount 方法之后调用选择方法以当分页时检索的使用数据源处的记录总数。</span><span class="sxs-lookup"><span data-stu-id="74343-263">The ObjectDataSource control will call the SelectCount method after a Select method has been called to retrieve the total number of records at the data source for use when paging.</span></span>

## <a name="lab-using-data-source-controls"></a><span data-ttu-id="74343-264">实验室中使用数据源控件</span><span class="sxs-lookup"><span data-stu-id="74343-264">Lab Using Data Source Controls</span></span>

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a><span data-ttu-id="74343-265">练习 1-SqlDataSource 控件与显示数据</span><span class="sxs-lookup"><span data-stu-id="74343-265">Exercise 1 - Displaying Data with the SqlDataSource Control</span></span>

<span data-ttu-id="74343-266">下面的练习使用 SqlDataSource 控件来连接到 Northwind 数据库。</span><span class="sxs-lookup"><span data-stu-id="74343-266">The following exercise uses the SqlDataSource control to connect to the Northwind database.</span></span> <span data-ttu-id="74343-267">它假定您的 SQL Server 2000 实例上有包含到 Northwind 数据库的访问。</span><span class="sxs-lookup"><span data-stu-id="74343-267">It assumes that you have access to the Northwind database on a SQL Server 2000 instance.</span></span>

1. <span data-ttu-id="74343-268">创建一个新的 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="74343-268">Create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="74343-269">添加新的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="74343-269">Add a new web.config file.</span></span>

    1. <span data-ttu-id="74343-270">右键单击解决方案资源管理器中的项目，然后单击添加新项。</span><span class="sxs-lookup"><span data-stu-id="74343-270">Right-click on the project in Solution Explorer and click Add New Item.</span></span>
    2. <span data-ttu-id="74343-271">从模板列表中选择 Web 配置文件并单击添加。</span><span class="sxs-lookup"><span data-stu-id="74343-271">Choose Web Configuration File from the list of templates and click Add.</span></span>
3. <span data-ttu-id="74343-272">编辑&lt;connectionStrings&gt;部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74343-272">Edit the &lt;connectionStrings&gt; section as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. <span data-ttu-id="74343-273">切换到代码视图，并添加 ConnectionString 属性和 SelectCommand 属性与&lt;asp: SqlDataSource&gt;控制，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74343-273">Switch to Code view and add a ConnectionString attribute and a SelectCommand attribute to the &lt;asp:SqlDataSource&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. <span data-ttu-id="74343-274">从设计视图中，添加一个新的 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="74343-274">From Design view, add a new GridView control.</span></span>
6. <span data-ttu-id="74343-275">从 GridView 任务菜单的选择数据源下拉列表中，选择 SqlDataSource1。</span><span class="sxs-lookup"><span data-stu-id="74343-275">From the Choose Data Source dropdown in the GridView Tasks menu, choose SqlDataSource1.</span></span>
7. <span data-ttu-id="74343-276">右键单击 Default.aspx，然后在浏览器中从菜单中选择视图。</span><span class="sxs-lookup"><span data-stu-id="74343-276">Right-click on Default.aspx and choose View in Browser from the menu.</span></span> <span data-ttu-id="74343-277">当系统提示保存，请单击是。</span><span class="sxs-lookup"><span data-stu-id="74343-277">Click Yes when prompted to save.</span></span>
8. <span data-ttu-id="74343-278">GridView 显示从 Products 表的数据。</span><span class="sxs-lookup"><span data-stu-id="74343-278">The GridView displays the data from the Products table.</span></span>

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a><span data-ttu-id="74343-279">练习 2-编辑数据与 SqlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="74343-279">Exercise 2 - Editing Data with the SqlDataSource Control</span></span>

<span data-ttu-id="74343-280">下面的练习演示如何将数据绑定的 DropDownList 控制是通过使用声明性语法和允许你编辑的 DropDownList 控件中显示的数据。</span><span class="sxs-lookup"><span data-stu-id="74343-280">The following exercise demonstrates how to data bind a DropDownList control using the declarative syntax and allows you to edit the data presented in the DropDownList control.</span></span>

1. <span data-ttu-id="74343-281">在设计视图中，从 Default.aspx 中删除 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="74343-281">In Design view, delete the GridView control from Default.aspx.</span></span> 

    <span data-ttu-id="74343-282">**重要**： 离开页面上的 SqlDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="74343-282">**Important**: Leave the SqlDataSource control on the page.</span></span>
2. <span data-ttu-id="74343-283">向 Default.aspx 中添加的 DropDownList 控件。</span><span class="sxs-lookup"><span data-stu-id="74343-283">Add a DropDownList control to Default.aspx.</span></span>
3. <span data-ttu-id="74343-284">切换到源视图。</span><span class="sxs-lookup"><span data-stu-id="74343-284">Switch to Source view.</span></span>
4. <span data-ttu-id="74343-285">添加到的 DataSourceId、 DataTextField 和 DataValueField 特性&lt;asp: DropDownList&gt;控制，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74343-285">Add a DataSourceId, DataTextField, and DataValueField attribute to the &lt;asp:DropDownList&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. <span data-ttu-id="74343-286">保存 Default.aspx，并在浏览器中查看它。</span><span class="sxs-lookup"><span data-stu-id="74343-286">Save Default.aspx and view it in the browser.</span></span> <span data-ttu-id="74343-287">请注意，下拉列表包含所有来自 Northwind 数据库的产品。</span><span class="sxs-lookup"><span data-stu-id="74343-287">Note that the DropDownList contains all of the products from the Northwind database.</span></span>
6. <span data-ttu-id="74343-288">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="74343-288">Close the browser.</span></span>
7. <span data-ttu-id="74343-289">在源视图中的 Default.aspx，添加一个新的文本框中控件的 DropDownList 控件下方。</span><span class="sxs-lookup"><span data-stu-id="74343-289">In Source view of Default.aspx, add a new TextBox control below the DropDownList control.</span></span> <span data-ttu-id="74343-290">将文本框中的 ID 属性更改为 txtProductName。</span><span class="sxs-lookup"><span data-stu-id="74343-290">Change the ID property of the TextBox to txtProductName.</span></span>
8. <span data-ttu-id="74343-291">在文本框控件中，添加一个新的按钮控件。</span><span class="sxs-lookup"><span data-stu-id="74343-291">Under the TextBox control, add a new Button control.</span></span> <span data-ttu-id="74343-292">将按钮的 ID 属性更改为 btnUpdate 和将文本属性设为**更新产品名称**。</span><span class="sxs-lookup"><span data-stu-id="74343-292">Change the ID property of the Button to btnUpdate and the Text property to **Update Product Name**.</span></span>
9. <span data-ttu-id="74343-293">在 Default.aspx 的源视图中，将添加 UpdateCommand 属性和两个新 UpdateParameters 到 SqlDataSource 标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="74343-293">In Source view of Default.aspx, add an UpdateCommand property and two new UpdateParameters to the SqlDataSource tag as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > <span data-ttu-id="74343-294">请注意，有两个更新此代码中添加的参数 （ProductName 和 ProductID）。</span><span class="sxs-lookup"><span data-stu-id="74343-294">Note that there are two update parameters (ProductName and ProductID) added in this code.</span></span> <span data-ttu-id="74343-295">这些参数映射到 txtProductName 文本框中的文本属性和 ddlProducts DropDownList SelectedValue 属性。</span><span class="sxs-lookup"><span data-stu-id="74343-295">These parameters are mapped to the Text property of the txtProductName TextBox and the SelectedValue property of the ddlProducts DropDownList.</span></span>
10. <span data-ttu-id="74343-296">切换到设计视图，并双击该按钮控件添加事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="74343-296">Switch to Design view and double-click on the Button control to add an event handler.</span></span>
11. <span data-ttu-id="74343-297">将以下代码添加到 btnUpdate\_单击代码：</span><span class="sxs-lookup"><span data-stu-id="74343-297">Add the following code to the btnUpdate\_Click code:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. <span data-ttu-id="74343-298">在 Default.aspx 上右键单击并选择在浏览器中查看它。</span><span class="sxs-lookup"><span data-stu-id="74343-298">Right-click on Default.aspx and choose to view it in the browser.</span></span> <span data-ttu-id="74343-299">当系统提示保存所有更改，请单击是。</span><span class="sxs-lookup"><span data-stu-id="74343-299">Click Yes when prompted to save all changes.</span></span>
13. <span data-ttu-id="74343-300">ASP.NET 2.0 分部类允许在运行时编译。</span><span class="sxs-lookup"><span data-stu-id="74343-300">ASP.NET 2.0 partial classes allow for compilation at runtime.</span></span> <span data-ttu-id="74343-301">不需要生成应用程序，以便查看代码更改生效。</span><span class="sxs-lookup"><span data-stu-id="74343-301">It is not necessary to build an application in order to see code changes take effect.</span></span>
14. <span data-ttu-id="74343-302">从下拉列表中选择一个产品。</span><span class="sxs-lookup"><span data-stu-id="74343-302">Select a product from the DropDownList.</span></span>
15. <span data-ttu-id="74343-303">在文本框中输入所选产品的新名称，然后单击更新按钮。</span><span class="sxs-lookup"><span data-stu-id="74343-303">Enter a new name for the selected product in the TextBox and then click the Update button.</span></span>
16. <span data-ttu-id="74343-304">在数据库中更新的产品名称。</span><span class="sxs-lookup"><span data-stu-id="74343-304">The product name is updated in the database.</span></span>

## <a name="exercise-3-using-the-objectdatasource-control"></a><span data-ttu-id="74343-305">练习 3 使用 ObjectDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="74343-305">Exercise 3 Using the ObjectDataSource Control</span></span>

<span data-ttu-id="74343-306">本练习将演示如何使用 ObjectDataSource 控件和源对象进行交互与 Northwind 数据库。</span><span class="sxs-lookup"><span data-stu-id="74343-306">This exercise will demonstrate how to use the ObjectDataSource control and a source object to interact with the Northwind database.</span></span>

1. <span data-ttu-id="74343-307">右键单击解决方案资源管理器中的项目，然后单击添加新项。</span><span class="sxs-lookup"><span data-stu-id="74343-307">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
2. <span data-ttu-id="74343-308">在模板列表中选择 Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="74343-308">Select Web Form in the templates list.</span></span> <span data-ttu-id="74343-309">将名称更改为 object.aspx 并单击添加。</span><span class="sxs-lookup"><span data-stu-id="74343-309">Change the name to object.aspx and click Add.</span></span>
3. <span data-ttu-id="74343-310">右键单击解决方案资源管理器中的项目，然后单击添加新项。</span><span class="sxs-lookup"><span data-stu-id="74343-310">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
4. <span data-ttu-id="74343-311">在模板列表中选择类。</span><span class="sxs-lookup"><span data-stu-id="74343-311">Select Class in the templates list.</span></span> <span data-ttu-id="74343-312">将类的名称更改为 NorthwindData.cs 并单击添加。</span><span class="sxs-lookup"><span data-stu-id="74343-312">Change the name of the class to NorthwindData.cs and click Add.</span></span>
5. <span data-ttu-id="74343-313">单击是将类添加到应用程序出现提示时\_代码文件夹。</span><span class="sxs-lookup"><span data-stu-id="74343-313">Click Yes when prompted to add the class to the App\_Code folder.</span></span>
6. <span data-ttu-id="74343-314">将以下代码添加到 NorthwindData.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="74343-314">Add the following code to the NorthwindData.cs file:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. <span data-ttu-id="74343-315">将以下代码添加到 object.aspx 的源视图：</span><span class="sxs-lookup"><span data-stu-id="74343-315">Add the following code to the Source view of object.aspx:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. <span data-ttu-id="74343-316">保存所有文件，并浏览 object.aspx。</span><span class="sxs-lookup"><span data-stu-id="74343-316">Save all files and browse object.aspx.</span></span>
9. <span data-ttu-id="74343-317">通过查看详细信息、 编辑员工、 添加员工，和删除员工与界面进行交互。</span><span class="sxs-lookup"><span data-stu-id="74343-317">Interact with the interface by viewing details, editing employees, adding employees, and deleting employees.</span></span>
