---
title: ASP.NET Core 中的数据保护
author: rick-anderson
description: 此文档充当各 ASP.NET Core 数据保护主题的目录。
manager: wpickett
ms.author: riande
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: security/data-protection/index
ms.openlocfilehash: 83b5bb1e6a4942a4d3e5ec0d445fa6e5a21fb533
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="data-protection-in-aspnet-core"></a><span data-ttu-id="ad48c-103">ASP.NET Core 中的数据保护</span><span class="sxs-lookup"><span data-stu-id="ad48c-103">Data Protection in ASP.NET Core</span></span>

* [<span data-ttu-id="ad48c-104">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="ad48c-104">Introduction to data protection</span></span>](xref:security/data-protection/introduction)

* [<span data-ttu-id="ad48c-105">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="ad48c-105">Get started with the Data Protection APIs</span></span>](xref:security/data-protection/using-data-protection)

* [<span data-ttu-id="ad48c-106">使用者 API</span><span class="sxs-lookup"><span data-stu-id="ad48c-106">Consumer APIs</span></span>](xref:security/data-protection/consumer-apis/index)

  * [<span data-ttu-id="ad48c-107">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="ad48c-107">Consumer APIs overview</span></span>](xref:security/data-protection/consumer-apis/overview)

  * [<span data-ttu-id="ad48c-108">目标字符串</span><span class="sxs-lookup"><span data-stu-id="ad48c-108">Purpose strings</span></span>](xref:security/data-protection/consumer-apis/purpose-strings)

  * [<span data-ttu-id="ad48c-109">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="ad48c-109">Purpose hierarchy and multi-tenancy</span></span>](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)

  * [<span data-ttu-id="ad48c-110">哈希密码</span><span class="sxs-lookup"><span data-stu-id="ad48c-110">Hash passwords</span></span>](xref:security/data-protection/consumer-apis/password-hashing)

  * [<span data-ttu-id="ad48c-111">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="ad48c-111">Limit the lifetime of protected payloads</span></span>](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)

  * [<span data-ttu-id="ad48c-112">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="ad48c-112">Unprotect payloads whose keys have been revoked</span></span>](xref:security/data-protection/consumer-apis/dangerous-unprotect)

* [<span data-ttu-id="ad48c-113">配置</span><span class="sxs-lookup"><span data-stu-id="ad48c-113">Configuration</span></span>](xref:security/data-protection/configuration/index)

  * [<span data-ttu-id="ad48c-114">配置 ASP.NET Core 数据保护</span><span class="sxs-lookup"><span data-stu-id="ad48c-114">Configure ASP.NET Core Data Protection</span></span>](xref:security/data-protection/configuration/overview)

  * [<span data-ttu-id="ad48c-115">默认设置</span><span class="sxs-lookup"><span data-stu-id="ad48c-115">Default settings</span></span>](xref:security/data-protection/configuration/default-settings)

  * [<span data-ttu-id="ad48c-116">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="ad48c-116">Machine-wide policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)

  * [<span data-ttu-id="ad48c-117">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="ad48c-117">Non DI-aware scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)

* [<span data-ttu-id="ad48c-118">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="ad48c-118">Extensibility APIs</span></span>](xref:security/data-protection/extensibility/index)

  * [<span data-ttu-id="ad48c-119">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="ad48c-119">Core cryptography extensibility</span></span>](xref:security/data-protection/extensibility/core-crypto)

  * [<span data-ttu-id="ad48c-120">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="ad48c-120">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)

  * [<span data-ttu-id="ad48c-121">其他 API</span><span class="sxs-lookup"><span data-stu-id="ad48c-121">Miscellaneous APIs</span></span>](xref:security/data-protection/extensibility/misc-apis)

* [<span data-ttu-id="ad48c-122">实现</span><span class="sxs-lookup"><span data-stu-id="ad48c-122">Implementation</span></span>](xref:security/data-protection/implementation/index)

  * [<span data-ttu-id="ad48c-123">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="ad48c-123">Authenticated encryption details</span></span>](xref:security/data-protection/implementation/authenticated-encryption-details)

  * [<span data-ttu-id="ad48c-124">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="ad48c-124">Subkey derivation and authenticated encryption</span></span>](xref:security/data-protection/implementation/subkeyderivation)

  * [<span data-ttu-id="ad48c-125">上下文标头</span><span class="sxs-lookup"><span data-stu-id="ad48c-125">Context headers</span></span>](xref:security/data-protection/implementation/context-headers)

  * [<span data-ttu-id="ad48c-126">密钥管理</span><span class="sxs-lookup"><span data-stu-id="ad48c-126">Key management</span></span>](xref:security/data-protection/implementation/key-management)

  * [<span data-ttu-id="ad48c-127">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="ad48c-127">Key storage providers</span></span>](xref:security/data-protection/implementation/key-storage-providers)

  * [<span data-ttu-id="ad48c-128">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="ad48c-128">Key encryption at rest</span></span>](xref:security/data-protection/implementation/key-encryption-at-rest)

  * [<span data-ttu-id="ad48c-129">密钥永久性和设置</span><span class="sxs-lookup"><span data-stu-id="ad48c-129">Key immutability and settings</span></span>](xref:security/data-protection/implementation/key-immutability)

  * [<span data-ttu-id="ad48c-130">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="ad48c-130">Key storage format</span></span>](xref:security/data-protection/implementation/key-storage-format)

  * [<span data-ttu-id="ad48c-131">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="ad48c-131">Ephemeral data protection providers</span></span>](xref:security/data-protection/implementation/key-storage-ephemeral)

* [<span data-ttu-id="ad48c-132">兼容性</span><span class="sxs-lookup"><span data-stu-id="ad48c-132">Compatibility</span></span>](xref:security/data-protection/compatibility/index)

  * [<span data-ttu-id="ad48c-133">在 ASP.NET Core 中替换 ASP.NET <machineKey></span><span class="sxs-lookup"><span data-stu-id="ad48c-133">Replacing ASP.NET <machineKey> in ASP.NET Core</span></span>](xref:security/data-protection/compatibility/replacing-machinekey)
