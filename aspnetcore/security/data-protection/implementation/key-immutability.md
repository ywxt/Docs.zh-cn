---
title: 密钥不可变性和 ASP.NET Core 中的密钥设置
author: rick-anderson
description: 了解可变性 ASP.NET Core 数据保护 Api 的实现详细信息。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-immutability
ms.openlocfilehash: 45460e0bdf6ad0a978f984d55b64f562c13fb575
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36279449"
---
# <a name="key-immutability-and-key-settings-in-aspnet-core"></a><span data-ttu-id="86515-103">密钥不可变性和 ASP.NET Core 中的密钥设置</span><span class="sxs-lookup"><span data-stu-id="86515-103">Key immutability and key settings in ASP.NET Core</span></span>

<span data-ttu-id="86515-104">一旦对象持久保留到后备存储，其表示形式是永久固定的。</span><span class="sxs-lookup"><span data-stu-id="86515-104">Once an object is persisted to the backing store, its representation is forever fixed.</span></span> <span data-ttu-id="86515-105">新的数据可以添加到后备存储，但可以永远不会更改现有数据。</span><span class="sxs-lookup"><span data-stu-id="86515-105">New data can be added to the backing store, but existing data can never be mutated.</span></span> <span data-ttu-id="86515-106">此行为的主要目的是为了防止数据损坏。</span><span class="sxs-lookup"><span data-stu-id="86515-106">The primary purpose of this behavior is to prevent data corruption.</span></span>

<span data-ttu-id="86515-107">此行为的一个后果是，一旦给后备存储编写了一个键，不可变。</span><span class="sxs-lookup"><span data-stu-id="86515-107">One consequence of this behavior is that once a key is written to the backing store, it's immutable.</span></span> <span data-ttu-id="86515-108">其创建、 激活和到期日期可以永远不会更改，但它可以通过使用吊销`IKeyManager`。</span><span class="sxs-lookup"><span data-stu-id="86515-108">Its creation, activation, and expiration dates can never be changed, though it can revoked by using `IKeyManager`.</span></span> <span data-ttu-id="86515-109">此外，其基础的算法信息、 主密钥材料和加密 rest 属性也是不可变。</span><span class="sxs-lookup"><span data-stu-id="86515-109">Additionally, its underlying algorithmic information, master keying material, and encryption at rest properties are also immutable.</span></span>

<span data-ttu-id="86515-110">如果开发人员更改会影响密钥保持任何设置，这些更改不会生效只有在下次时都会生成一个密钥，是指在通过显式调用`IKeyManager.CreateNewKey`或通过数据保护系统的自己[自动密钥生成](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)行为。</span><span class="sxs-lookup"><span data-stu-id="86515-110">If the developer changes any setting that affects key persistence, those changes won't go into effect until the next time a key is generated, either via an explicit call to `IKeyManager.CreateNewKey` or via the data protection system's own [automatic key generation](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management) behavior.</span></span> <span data-ttu-id="86515-111">影响密钥持久性的设置如下所示：</span><span class="sxs-lookup"><span data-stu-id="86515-111">The settings that affect key persistence are as follows:</span></span>

* [<span data-ttu-id="86515-112">默认密钥生存时间</span><span class="sxs-lookup"><span data-stu-id="86515-112">The default key lifetime</span></span>](xref:security/data-protection/implementation/key-management#data-protection-implementation-key-management)

* [<span data-ttu-id="86515-113">在 rest 机制密钥加密</span><span class="sxs-lookup"><span data-stu-id="86515-113">The key encryption at rest mechanism</span></span>](xref:security/data-protection/implementation/key-encryption-at-rest#data-protection-implementation-key-encryption-at-rest)

* [<span data-ttu-id="86515-114">在项包含的算法信息</span><span class="sxs-lookup"><span data-stu-id="86515-114">The algorithmic information contained within the key</span></span>](xref:security/data-protection/configuration/overview#changing-algorithms-with-usecryptographicalgorithms)

<span data-ttu-id="86515-115">如果你需要这些设置，以便早于下一步的自动密钥滚动时间启动，请考虑使显式调用`IKeyManager.CreateNewKey`强制创建新的密钥。</span><span class="sxs-lookup"><span data-stu-id="86515-115">If you need these settings to kick in earlier than the next automatic key rolling time, consider making an explicit call to `IKeyManager.CreateNewKey` to force the creation of a new key.</span></span> <span data-ttu-id="86515-116">请记得提供显式激活日期 （{现在 + 2 天} 是一个很好的经验法则以允许更改传播的时间） 和调用中的到期日期。</span><span class="sxs-lookup"><span data-stu-id="86515-116">Remember to provide an explicit activation date ({ now + 2 days } is a good rule of thumb to allow time for the change to propagate) and expiration date in the call.</span></span>

>[!TIP]
> <span data-ttu-id="86515-117">点击存储库中的所有应用程序应指定要用的相同设置`IDataProtectionBuilder`扩展方法。</span><span class="sxs-lookup"><span data-stu-id="86515-117">All applications touching the repository should specify the same settings with the `IDataProtectionBuilder` extension methods.</span></span> <span data-ttu-id="86515-118">否则，保存的密钥的属性将取决于调用的密钥生成例程的特定应用程序。</span><span class="sxs-lookup"><span data-stu-id="86515-118">Otherwise, the properties of the persisted key will be dependent on the particular application that invoked the key generation routines.</span></span>
