---
title: ASP.NET 核心的密钥管理可扩展性
author: rick-anderson
description: 了解有关 ASP.NET 核心数据保护密钥管理扩展性。
manager: wpickett
ms.author: riande
ms.date: 11/22/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/extensibility/key-management
ms.openlocfilehash: e3042b371cf7be8fa0218c1906042d2810b180e3
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
ms.locfileid: "30074159"
---
# <a name="key-management-extensibility-in-aspnet-core"></a><span data-ttu-id="8e822-103">ASP.NET 核心的密钥管理可扩展性</span><span class="sxs-lookup"><span data-stu-id="8e822-103">Key management extensibility in ASP.NET Core</span></span>

<a name="data-protection-extensibility-key-management"></a>

>[!TIP]
> <span data-ttu-id="8e822-104">读取[密钥管理](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)之前阅读此部分中，因为它介绍了这些 Api 的基本概念的某些部分。</span><span class="sxs-lookup"><span data-stu-id="8e822-104">Read the [key management](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) section before reading this section, as it explains some of the fundamental concepts behind these APIs.</span></span>

>[!WARNING]
> <span data-ttu-id="8e822-105">实现的任意以下接口的类型应该是线程安全的多个调用方。</span><span class="sxs-lookup"><span data-stu-id="8e822-105">Types that implement any of the following interfaces should be thread-safe for multiple callers.</span></span>

## <a name="key"></a><span data-ttu-id="8e822-106">键</span><span class="sxs-lookup"><span data-stu-id="8e822-106">Key</span></span>

<span data-ttu-id="8e822-107">`IKey`接口是加密系统中的键的基本表示。</span><span class="sxs-lookup"><span data-stu-id="8e822-107">The `IKey` interface is the basic representation of a key in cryptosystem.</span></span> <span data-ttu-id="8e822-108">在抽象的意义上，不在"加密密钥材料"字面意义上此处使用的术语密钥。</span><span class="sxs-lookup"><span data-stu-id="8e822-108">The term key is used here in the abstract sense, not in the literal sense of "cryptographic key material".</span></span> <span data-ttu-id="8e822-109">密钥具有以下属性：</span><span class="sxs-lookup"><span data-stu-id="8e822-109">A key has the following properties:</span></span>

* <span data-ttu-id="8e822-110">激活、 创建和到期日期</span><span class="sxs-lookup"><span data-stu-id="8e822-110">Activation, creation, and expiration dates</span></span>

* <span data-ttu-id="8e822-111">吊销状态</span><span class="sxs-lookup"><span data-stu-id="8e822-111">Revocation status</span></span>

* <span data-ttu-id="8e822-112">密钥标识符 (GUID)</span><span class="sxs-lookup"><span data-stu-id="8e822-112">Key identifier (a GUID)</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8e822-113">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8e822-113">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

<span data-ttu-id="8e822-114">此外，`IKey`公开`CreateEncryptor`方法用于创建[IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor)实例绑定到此密钥。</span><span class="sxs-lookup"><span data-stu-id="8e822-114">Additionally, `IKey` exposes a `CreateEncryptor` method which can be used to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance tied to this key.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8e822-115">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8e822-115">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

<span data-ttu-id="8e822-116">此外，`IKey`公开`CreateEncryptorInstance`方法用于创建[IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor)实例绑定到此密钥。</span><span class="sxs-lookup"><span data-stu-id="8e822-116">Additionally, `IKey` exposes a `CreateEncryptorInstance` method which can be used to create an [IAuthenticatedEncryptor](xref:security/data-protection/extensibility/core-crypto#data-protection-extensibility-core-crypto-iauthenticatedencryptor) instance tied to this key.</span></span>

---

> [!NOTE]
> <span data-ttu-id="8e822-117">没有 API 检索从原始的加密材料`IKey`实例。</span><span class="sxs-lookup"><span data-stu-id="8e822-117">There's no API to retrieve the raw cryptographic material from an `IKey` instance.</span></span>

## <a name="ikeymanager"></a><span data-ttu-id="8e822-118">IKeyManager</span><span class="sxs-lookup"><span data-stu-id="8e822-118">IKeyManager</span></span>

<span data-ttu-id="8e822-119">`IKeyManager`接口表示负责常规的密钥存储、 检索和操作的对象。</span><span class="sxs-lookup"><span data-stu-id="8e822-119">The `IKeyManager` interface represents an object responsible for general key storage, retrieval, and manipulation.</span></span> <span data-ttu-id="8e822-120">它公开三个高级操作：</span><span class="sxs-lookup"><span data-stu-id="8e822-120">It exposes three high-level operations:</span></span>

* <span data-ttu-id="8e822-121">创建新密钥并将其保存在存储。</span><span class="sxs-lookup"><span data-stu-id="8e822-121">Create a new key and persist it to storage.</span></span>

* <span data-ttu-id="8e822-122">从存储中获取所有键。</span><span class="sxs-lookup"><span data-stu-id="8e822-122">Get all keys from storage.</span></span>

* <span data-ttu-id="8e822-123">撤消一个或多个密钥，而且将保留到存储的吊销信息。</span><span class="sxs-lookup"><span data-stu-id="8e822-123">Revoke one or more keys and persist the revocation information to storage.</span></span>

>[!WARNING]
> <span data-ttu-id="8e822-124">编写`IKeyManager`是一个非常高级的任务，和大多数开发人员不应尝试。</span><span class="sxs-lookup"><span data-stu-id="8e822-124">Writing an `IKeyManager` is a very advanced task, and the majority of developers shouldn't attempt it.</span></span> <span data-ttu-id="8e822-125">相反，大多数开发人员应充分利用所提供的功能[XmlKeyManager](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-xmlkeymanager)类。</span><span class="sxs-lookup"><span data-stu-id="8e822-125">Instead, most developers should take advantage of the facilities offered by the [XmlKeyManager](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-xmlkeymanager) class.</span></span>

<a name="data-protection-extensibility-key-management-xmlkeymanager"></a>

## <a name="xmlkeymanager"></a><span data-ttu-id="8e822-126">XmlKeyManager</span><span class="sxs-lookup"><span data-stu-id="8e822-126">XmlKeyManager</span></span>

<span data-ttu-id="8e822-127">`XmlKeyManager`类型是内置的具体实现`IKeyManager`。</span><span class="sxs-lookup"><span data-stu-id="8e822-127">The `XmlKeyManager` type is the in-box concrete implementation of `IKeyManager`.</span></span> <span data-ttu-id="8e822-128">它提供了几个有用的功能，包括密钥证书和加密对静止的密钥。</span><span class="sxs-lookup"><span data-stu-id="8e822-128">It provides several useful facilities, including key escrow and encryption of keys at rest.</span></span> <span data-ttu-id="8e822-129">在此系统的密钥将呈现为 XML 元素 (具体而言， [XElement](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/xelement-class-overview))。</span><span class="sxs-lookup"><span data-stu-id="8e822-129">Keys in this system are represented as XML elements (specifically, [XElement](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/xelement-class-overview)).</span></span>

<span data-ttu-id="8e822-130">`XmlKeyManager` 依赖于在完成其任务的过程中的其他几个组件：</span><span class="sxs-lookup"><span data-stu-id="8e822-130">`XmlKeyManager` depends on several other components in the course of fulfilling its tasks:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8e822-131">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8e822-131">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

* <span data-ttu-id="8e822-132">`AlgorithmConfiguration`这决定使用新密钥的算法。</span><span class="sxs-lookup"><span data-stu-id="8e822-132">`AlgorithmConfiguration`, which dictates the algorithms used by new keys.</span></span>

* <span data-ttu-id="8e822-133">`IXmlRepository`其中键将保留在存储中的控件。</span><span class="sxs-lookup"><span data-stu-id="8e822-133">`IXmlRepository`, which controls where keys are persisted in storage.</span></span>

* <span data-ttu-id="8e822-134">`IXmlEncryptor` [可选]，这允许加密对静止的密钥。</span><span class="sxs-lookup"><span data-stu-id="8e822-134">`IXmlEncryptor` [optional], which allows encrypting keys at rest.</span></span>

* <span data-ttu-id="8e822-135">`IKeyEscrowSink` [可选]，其提供密钥托管服务。</span><span class="sxs-lookup"><span data-stu-id="8e822-135">`IKeyEscrowSink` [optional], which provides key escrow services.</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8e822-136">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8e822-136">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

* <span data-ttu-id="8e822-137">`IXmlRepository`其中键将保留在存储中的控件。</span><span class="sxs-lookup"><span data-stu-id="8e822-137">`IXmlRepository`, which controls where keys are persisted in storage.</span></span>

* <span data-ttu-id="8e822-138">`IXmlEncryptor` [可选]，这允许加密对静止的密钥。</span><span class="sxs-lookup"><span data-stu-id="8e822-138">`IXmlEncryptor` [optional], which allows encrypting keys at rest.</span></span>

* <span data-ttu-id="8e822-139">`IKeyEscrowSink` [可选]，其提供密钥托管服务。</span><span class="sxs-lookup"><span data-stu-id="8e822-139">`IKeyEscrowSink` [optional], which provides key escrow services.</span></span>

---

<span data-ttu-id="8e822-140">以下是高级关系图，表明如何这些组件连接在一起内`XmlKeyManager`。</span><span class="sxs-lookup"><span data-stu-id="8e822-140">Below are high-level diagrams which indicate how these components are wired together within `XmlKeyManager`.</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8e822-141">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8e822-141">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ![密钥创建](key-management/_static/keycreation2.png)

   <span data-ttu-id="8e822-143">*密钥创建 / CreateNewKey*</span><span class="sxs-lookup"><span data-stu-id="8e822-143">*Key Creation / CreateNewKey*</span></span>

<span data-ttu-id="8e822-144">实现中`CreateNewKey`、`AlgorithmConfiguration`组件用于创建唯一`IAuthenticatedEncryptorDescriptor`，其中然后序列化为 XML。</span><span class="sxs-lookup"><span data-stu-id="8e822-144">In the implementation of `CreateNewKey`, the `AlgorithmConfiguration` component is used to create a unique `IAuthenticatedEncryptorDescriptor`, which is then serialized as XML.</span></span> <span data-ttu-id="8e822-145">如果存在密钥托管接收器，则原始 （未加密） 的 XML 到接收器提供适用于长期存储。</span><span class="sxs-lookup"><span data-stu-id="8e822-145">If a key escrow sink is present, the raw (unencrypted) XML is provided to the sink for long-term storage.</span></span> <span data-ttu-id="8e822-146">然后通过运行的未加密的 XML `IXmlEncryptor` （如果需要） 来生成加密的 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="8e822-146">The unencrypted XML is then run through an `IXmlEncryptor` (if required) to generate the encrypted XML document.</span></span> <span data-ttu-id="8e822-147">此加密的文档保存到长期存储通过`IXmlRepository`。</span><span class="sxs-lookup"><span data-stu-id="8e822-147">This encrypted document is persisted to long-term storage via the `IXmlRepository`.</span></span> <span data-ttu-id="8e822-148">(如果没有`IXmlEncryptor`是配置，未加密的文档保存在`IXmlRepository`。)</span><span class="sxs-lookup"><span data-stu-id="8e822-148">(If no `IXmlEncryptor` is configured, the unencrypted document is persisted in the `IXmlRepository`.)</span></span>

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8e822-149">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8e822-149">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ![密钥创建](key-management/_static/keycreation1.png)

   <span data-ttu-id="8e822-151">*密钥创建 / CreateNewKey*</span><span class="sxs-lookup"><span data-stu-id="8e822-151">*Key Creation / CreateNewKey*</span></span>

<span data-ttu-id="8e822-152">实现中`CreateNewKey`、`IAuthenticatedEncryptorConfiguration`组件用于创建唯一`IAuthenticatedEncryptorDescriptor`，其中然后序列化为 XML。</span><span class="sxs-lookup"><span data-stu-id="8e822-152">In the implementation of `CreateNewKey`, the `IAuthenticatedEncryptorConfiguration` component is used to create a unique `IAuthenticatedEncryptorDescriptor`, which is then serialized as XML.</span></span> <span data-ttu-id="8e822-153">如果存在密钥托管接收器，则原始 （未加密） 的 XML 到接收器提供适用于长期存储。</span><span class="sxs-lookup"><span data-stu-id="8e822-153">If a key escrow sink is present, the raw (unencrypted) XML is provided to the sink for long-term storage.</span></span> <span data-ttu-id="8e822-154">然后通过运行的未加密的 XML `IXmlEncryptor` （如果需要） 来生成加密的 XML 文档。</span><span class="sxs-lookup"><span data-stu-id="8e822-154">The unencrypted XML is then run through an `IXmlEncryptor` (if required) to generate the encrypted XML document.</span></span> <span data-ttu-id="8e822-155">此加密的文档保存到长期存储通过`IXmlRepository`。</span><span class="sxs-lookup"><span data-stu-id="8e822-155">This encrypted document is persisted to long-term storage via the `IXmlRepository`.</span></span> <span data-ttu-id="8e822-156">(如果没有`IXmlEncryptor`是配置，未加密的文档保存在`IXmlRepository`。)</span><span class="sxs-lookup"><span data-stu-id="8e822-156">(If no `IXmlEncryptor` is configured, the unencrypted document is persisted in the `IXmlRepository`.)</span></span>

---

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8e822-157">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8e822-157">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ![密钥检索](key-management/_static/keyretrieval2.png)
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8e822-159">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8e822-159">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ![密钥检索](key-management/_static/keyretrieval1.png)

---

   <span data-ttu-id="8e822-161">*密钥检索 / GetAllKeys*</span><span class="sxs-lookup"><span data-stu-id="8e822-161">*Key Retrieval / GetAllKeys*</span></span>

<span data-ttu-id="8e822-162">实现中`GetAllKeys`、 XML 文档表示键和从基础读取吊销`IXmlRepository`。</span><span class="sxs-lookup"><span data-stu-id="8e822-162">In the implementation of `GetAllKeys`, the XML documents representing keys and revocations are read from the underlying `IXmlRepository`.</span></span> <span data-ttu-id="8e822-163">如果这些文档进行加密，系统将自动解密。</span><span class="sxs-lookup"><span data-stu-id="8e822-163">If these documents are encrypted, the system will automatically decrypt them.</span></span> <span data-ttu-id="8e822-164">`XmlKeyManager` 创建适当`IAuthenticatedEncryptorDescriptorDeserializer`实例进行反序列化文档回`IAuthenticatedEncryptorDescriptor`实例，然后将封装在单个`IKey`实例。</span><span class="sxs-lookup"><span data-stu-id="8e822-164">`XmlKeyManager` creates the appropriate `IAuthenticatedEncryptorDescriptorDeserializer` instances to deserialize the documents back into `IAuthenticatedEncryptorDescriptor` instances, which are then wrapped in individual `IKey` instances.</span></span> <span data-ttu-id="8e822-165">此集合`IKey`实例返回给调用方。</span><span class="sxs-lookup"><span data-stu-id="8e822-165">This collection of `IKey` instances is returned to the caller.</span></span>

<span data-ttu-id="8e822-166">在找不到在特定的 XML 元素上的进一步信息[密钥存储格式文档](xref:security/data-protection/implementation/key-storage-format#data-protection-implementation-key-storage-format)。</span><span class="sxs-lookup"><span data-stu-id="8e822-166">Further information on the particular XML elements can be found in the [key storage format document](xref:security/data-protection/implementation/key-storage-format#data-protection-implementation-key-storage-format).</span></span>

## <a name="ixmlrepository"></a><span data-ttu-id="8e822-167">IXmlRepository</span><span class="sxs-lookup"><span data-stu-id="8e822-167">IXmlRepository</span></span>

<span data-ttu-id="8e822-168">`IXmlRepository`接口表示可保留 XML 到和从一个后备存储检索 XML 的类型。</span><span class="sxs-lookup"><span data-stu-id="8e822-168">The `IXmlRepository` interface represents a type that can persist XML to and retrieve XML from a backing store.</span></span> <span data-ttu-id="8e822-169">它公开两个 Api:</span><span class="sxs-lookup"><span data-stu-id="8e822-169">It exposes two APIs:</span></span>

* <span data-ttu-id="8e822-170">GetAllElements(): IReadOnlyCollection<XElement></span><span class="sxs-lookup"><span data-stu-id="8e822-170">GetAllElements() : IReadOnlyCollection<XElement></span></span>

* <span data-ttu-id="8e822-171">StoreElement （XElement 元素，字符串 friendlyName）</span><span class="sxs-lookup"><span data-stu-id="8e822-171">StoreElement(XElement element, string friendlyName)</span></span>

<span data-ttu-id="8e822-172">实现`IXmlRepository`不需要通过其传递对 XML 进行分析。</span><span class="sxs-lookup"><span data-stu-id="8e822-172">Implementations of `IXmlRepository` don't need to parse the XML passing through them.</span></span> <span data-ttu-id="8e822-173">它们应视为不透明 XML 文档，让较高层担心生成和分析文档。</span><span class="sxs-lookup"><span data-stu-id="8e822-173">They should treat the XML documents as opaque and let higher layers worry about generating and parsing the documents.</span></span>

<span data-ttu-id="8e822-174">有两个内置的具体类型实现`IXmlRepository`:`FileSystemXmlRepository`和`RegistryXmlRepository`。</span><span class="sxs-lookup"><span data-stu-id="8e822-174">There are two built-in concrete types which implement `IXmlRepository`: `FileSystemXmlRepository` and `RegistryXmlRepository`.</span></span> <span data-ttu-id="8e822-175">请参阅[密钥存储提供程序文档](xref:security/data-protection/implementation/key-storage-providers#data-protection-implementation-key-storage-providers)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="8e822-175">See the [key storage providers document](xref:security/data-protection/implementation/key-storage-providers#data-protection-implementation-key-storage-providers) for more information.</span></span> <span data-ttu-id="8e822-176">注册的自定义`IXmlRepository`将适当的方式为使用不同的后备存储，例如，Azure Blob 存储。</span><span class="sxs-lookup"><span data-stu-id="8e822-176">Registering a custom `IXmlRepository` would be the appropriate manner to use a different backing store, e.g., Azure Blob Storage.</span></span>

<span data-ttu-id="8e822-177">若要更改默认存储库应用程序级，注册一个自定义`IXmlRepository`实例：</span><span class="sxs-lookup"><span data-stu-id="8e822-177">To change the default repository application-wide, register a custom `IXmlRepository` instance:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8e822-178">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8e822-178">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ```csharp
   services.Configure<KeyManagementOptions>(options => options.XmlRepository = new MyCustomXmlRepository());
   ```
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8e822-179">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8e822-179">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ```csharp
   services.AddSingleton<IXmlRepository>(new MyCustomXmlRepository());
   ```

---

<a name="data-protection-extensibility-key-management-ixmlencryptor"></a>

## <a name="ixmlencryptor"></a><span data-ttu-id="8e822-180">IXmlEncryptor</span><span class="sxs-lookup"><span data-stu-id="8e822-180">IXmlEncryptor</span></span>

<span data-ttu-id="8e822-181">`IXmlEncryptor`接口表示可以加密纯文本 XML 元素的类型。</span><span class="sxs-lookup"><span data-stu-id="8e822-181">The `IXmlEncryptor` interface represents a type that can encrypt a plaintext XML element.</span></span> <span data-ttu-id="8e822-182">它公开单个 API:</span><span class="sxs-lookup"><span data-stu-id="8e822-182">It exposes a single API:</span></span>

* <span data-ttu-id="8e822-183">加密 (XElement plaintextElement): EncryptedXmlInfo</span><span class="sxs-lookup"><span data-stu-id="8e822-183">Encrypt(XElement plaintextElement) : EncryptedXmlInfo</span></span>

<span data-ttu-id="8e822-184">如果一个序列化`IAuthenticatedEncryptorDescriptor`包含任何元素标记为"需要加密"，然后`XmlKeyManager`将通过配置运行这些元素`IXmlEncryptor`的`Encrypt`方法，和它将保留 enciphered 的元素而不是为纯文本元素`IXmlRepository`。</span><span class="sxs-lookup"><span data-stu-id="8e822-184">If a serialized `IAuthenticatedEncryptorDescriptor` contains any elements marked as "requires encryption", then `XmlKeyManager` will run those elements through the configured `IXmlEncryptor`'s `Encrypt` method, and it will persist the enciphered element rather than the plaintext element to the `IXmlRepository`.</span></span> <span data-ttu-id="8e822-185">输出`Encrypt`方法是`EncryptedXmlInfo`对象。</span><span class="sxs-lookup"><span data-stu-id="8e822-185">The output of the `Encrypt` method is an `EncryptedXmlInfo` object.</span></span> <span data-ttu-id="8e822-186">此对象是包装器，其中包含两个所产生的 enciphered`XElement`和表示类型`IXmlDecryptor`可用于解密的相应元素。</span><span class="sxs-lookup"><span data-stu-id="8e822-186">This object is a wrapper which contains both the resultant enciphered `XElement` and the Type which represents an `IXmlDecryptor` which can be used to decipher the corresponding element.</span></span>

<span data-ttu-id="8e822-187">有四个内置的具体类型实现`IXmlEncryptor`:</span><span class="sxs-lookup"><span data-stu-id="8e822-187">There are four built-in concrete types which implement `IXmlEncryptor`:</span></span>
* `CertificateXmlEncryptor`
* `DpapiNGXmlEncryptor`
* `DpapiXmlEncryptor`
* `NullXmlEncryptor`

<span data-ttu-id="8e822-188">请参阅[rest 文档的密钥加密](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest)有关详细信息。</span><span class="sxs-lookup"><span data-stu-id="8e822-188">See the [key encryption at rest document](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest) for more information.</span></span>

<span data-ttu-id="8e822-189">若要更改默认密钥加密在 rest 机制整个应用程序范围，注册一个自定义`IXmlEncryptor`实例：</span><span class="sxs-lookup"><span data-stu-id="8e822-189">To change the default key-encryption-at-rest mechanism application-wide, register a custom `IXmlEncryptor` instance:</span></span>

# <a name="aspnet-core-2xtabaspnetcore2x"></a>[<span data-ttu-id="8e822-190">ASP.NET Core 2.x</span><span class="sxs-lookup"><span data-stu-id="8e822-190">ASP.NET Core 2.x</span></span>](#tab/aspnetcore2x)

   ```csharp
   services.Configure<KeyManagementOptions>(options => options.XmlEncryptor = new MyCustomXmlEncryptor());
   ```
   
# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="8e822-191">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="8e822-191">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x)

   ```csharp
   services.AddSingleton<IXmlEncryptor>(new MyCustomXmlEncryptor());
   ```

---

## <a name="ixmldecryptor"></a><span data-ttu-id="8e822-192">IXmlDecryptor</span><span class="sxs-lookup"><span data-stu-id="8e822-192">IXmlDecryptor</span></span>

<span data-ttu-id="8e822-193">`IXmlDecryptor`接口表示一种类型，知道如何解密`XElement`，已通过 enciphered `IXmlEncryptor`。</span><span class="sxs-lookup"><span data-stu-id="8e822-193">The `IXmlDecryptor` interface represents a type that knows how to decrypt an `XElement` that was enciphered via an `IXmlEncryptor`.</span></span> <span data-ttu-id="8e822-194">它公开单个 API:</span><span class="sxs-lookup"><span data-stu-id="8e822-194">It exposes a single API:</span></span>

* <span data-ttu-id="8e822-195">解密 (XElement encryptedElement): XElement</span><span class="sxs-lookup"><span data-stu-id="8e822-195">Decrypt(XElement encryptedElement) : XElement</span></span>

<span data-ttu-id="8e822-196">`Decrypt`方法撤消由执行加密`IXmlEncryptor.Encrypt`。</span><span class="sxs-lookup"><span data-stu-id="8e822-196">The `Decrypt` method undoes the encryption performed by `IXmlEncryptor.Encrypt`.</span></span> <span data-ttu-id="8e822-197">通常情况下，每个具体`IXmlEncryptor`实现将具有相应的具体`IXmlDecryptor`实现。</span><span class="sxs-lookup"><span data-stu-id="8e822-197">Generally, each concrete `IXmlEncryptor` implementation will have a corresponding concrete `IXmlDecryptor` implementation.</span></span>

<span data-ttu-id="8e822-198">类型可实现`IXmlDecryptor`应该具有以下两个公共构造函数之一：</span><span class="sxs-lookup"><span data-stu-id="8e822-198">Types which implement `IXmlDecryptor` should have one of the following two public constructors:</span></span>

* <span data-ttu-id="8e822-199">.ctor(IServiceProvider)</span><span class="sxs-lookup"><span data-stu-id="8e822-199">.ctor(IServiceProvider)</span></span>
* <span data-ttu-id="8e822-200">.ctor()</span><span class="sxs-lookup"><span data-stu-id="8e822-200">.ctor()</span></span>

> [!NOTE]
> <span data-ttu-id="8e822-201">`IServiceProvider`传递给构造函数可能为 null。</span><span class="sxs-lookup"><span data-stu-id="8e822-201">The `IServiceProvider` passed to the constructor may be null.</span></span>

## <a name="ikeyescrowsink"></a><span data-ttu-id="8e822-202">IKeyEscrowSink</span><span class="sxs-lookup"><span data-stu-id="8e822-202">IKeyEscrowSink</span></span>

<span data-ttu-id="8e822-203">`IKeyEscrowSink`接口表示可以执行托管的敏感信息的类型。</span><span class="sxs-lookup"><span data-stu-id="8e822-203">The `IKeyEscrowSink` interface represents a type that can perform escrow of sensitive information.</span></span> <span data-ttu-id="8e822-204">回想一下，序列化的描述符可能包含敏感信息 （如加密材料），这是什么导致了引入[IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor)键入第一个位置。</span><span class="sxs-lookup"><span data-stu-id="8e822-204">Recall that serialized descriptors might contain sensitive information (such as cryptographic material), and this is what led to the introduction of the [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor) type in the first place.</span></span> <span data-ttu-id="8e822-205">但是，意外的发生，并且密钥环可以删除或损坏。</span><span class="sxs-lookup"><span data-stu-id="8e822-205">However, accidents happen, and key rings can be deleted or become corrupted.</span></span>

<span data-ttu-id="8e822-206">托管接口提供了允许访问原始序列化的 XML 转换由任何配置前紧急转义阴影[IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor)。</span><span class="sxs-lookup"><span data-stu-id="8e822-206">The escrow interface provides an emergency escape hatch, allowing access to the raw serialized XML before it's transformed by any configured [IXmlEncryptor](xref:security/data-protection/extensibility/key-management#data-protection-extensibility-key-management-ixmlencryptor).</span></span> <span data-ttu-id="8e822-207">接口公开单个 API:</span><span class="sxs-lookup"><span data-stu-id="8e822-207">The interface exposes a single API:</span></span>

* <span data-ttu-id="8e822-208">应用商店 （Guid keyId、 XElement 元素）</span><span class="sxs-lookup"><span data-stu-id="8e822-208">Store(Guid keyId, XElement element)</span></span>

<span data-ttu-id="8e822-209">这就需要通过`IKeyEscrowSink`实现，以安全的方式与业务策略一致处理提供的元素。</span><span class="sxs-lookup"><span data-stu-id="8e822-209">It's up to the `IKeyEscrowSink` implementation to handle the provided element in a secure manner consistent with business policy.</span></span> <span data-ttu-id="8e822-210">一个可能的实现可能是为托管接收器使用已知的企业 X.509 证书的 XML 元素进行加密其中已托管证书的私钥;`CertificateXmlEncryptor`类型可以对此有帮助。</span><span class="sxs-lookup"><span data-stu-id="8e822-210">One possible implementation could be for the escrow sink to encrypt the XML element using a known corporate X.509 certificate where the certificate's private key has been escrowed; the `CertificateXmlEncryptor` type can assist with this.</span></span> <span data-ttu-id="8e822-211">`IKeyEscrowSink`实现程序还负责适当地保留提供的元素。</span><span class="sxs-lookup"><span data-stu-id="8e822-211">The `IKeyEscrowSink` implementation is also responsible for persisting the provided element appropriately.</span></span>

<span data-ttu-id="8e822-212">默认情况下没有托管机制启用，但服务器管理员可以[全局配置此](xref:security/data-protection/configuration/machine-wide-policy)。</span><span class="sxs-lookup"><span data-stu-id="8e822-212">By default no escrow mechanism is enabled, though server administrators can [configure this globally](xref:security/data-protection/configuration/machine-wide-policy).</span></span> <span data-ttu-id="8e822-213">它还可以配置以编程方式通过`IDataProtectionBuilder.AddKeyEscrowSink`方法，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="8e822-213">It can also be configured programmatically via the `IDataProtectionBuilder.AddKeyEscrowSink` method as shown in the sample below.</span></span> <span data-ttu-id="8e822-214">`AddKeyEscrowSink`方法重载镜像`IServiceCollection.AddSingleton`和`IServiceCollection.AddInstance`重载，为`IKeyEscrowSink`实例都应是单一实例。</span><span class="sxs-lookup"><span data-stu-id="8e822-214">The `AddKeyEscrowSink` method overloads mirror the `IServiceCollection.AddSingleton` and `IServiceCollection.AddInstance` overloads, as `IKeyEscrowSink` instances are intended to be singletons.</span></span> <span data-ttu-id="8e822-215">如果选择多个`IKeyEscrowSink`注册实例，每个过程中将调用密钥生成，因此键可以同时托管多个机制。</span><span class="sxs-lookup"><span data-stu-id="8e822-215">If multiple `IKeyEscrowSink` instances are registered, each one will be called during key generation, so keys can be escrowed to multiple mechanisms simultaneously.</span></span>

<span data-ttu-id="8e822-216">没有任何 API 来读取中的材料`IKeyEscrowSink`实例。</span><span class="sxs-lookup"><span data-stu-id="8e822-216">There's no API to read material from an `IKeyEscrowSink` instance.</span></span> <span data-ttu-id="8e822-217">这是与托管机制的设计理论一致： 它具有用于受信任的颁发机构，方便密钥材料，并且应用程序本身不是受信任颁发机构，因为它不应具有访问自己保管材料。</span><span class="sxs-lookup"><span data-stu-id="8e822-217">This is consistent with the design theory of the escrow mechanism: it's intended to make the key material accessible to a trusted authority, and since the application is itself not a trusted authority, it shouldn't have access to its own escrowed material.</span></span>

<span data-ttu-id="8e822-218">下面的示例代码演示如何创建和注册`IKeyEscrowSink`其中托管密钥，以便只有"CONTOSODomain 管理员"的成员可以恢复它们。</span><span class="sxs-lookup"><span data-stu-id="8e822-218">The following sample code demonstrates creating and registering an `IKeyEscrowSink` where keys are escrowed such that only members of "CONTOSODomain Admins" can recover them.</span></span>

> [!NOTE]
> <span data-ttu-id="8e822-219">若要运行此示例，你必须是在已加入域的 Windows 8 / Windows Server 2012 计算机和域控制器必须是 Windows Server 2012 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="8e822-219">To run this sample, you must be on a domain-joined Windows 8 / Windows Server 2012 machine, and the domain controller must be Windows Server 2012 or later.</span></span>

[!code-csharp[](key-management/samples/key-management-extensibility.cs)]
