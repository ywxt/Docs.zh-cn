---
title: "ASP.NET Core 中的数据保护"
author: rick-anderson
description: "此文档充当各 ASP.NET Core 数据保护主题的目录。"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/index
ms.openlocfilehash: 7bbd203a67b32032ba2ab82448a5fc9a495b52aa
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a><span data-ttu-id="ab771-103">ASP.NET Core 中的数据保护：使用者 API、配置、扩展性 API 和实现</span><span class="sxs-lookup"><span data-stu-id="ab771-103">Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation</span></span>

* [<span data-ttu-id="ab771-104">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="ab771-104">Introduction to data protection</span></span>](introduction.md)

* [<span data-ttu-id="ab771-105">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="ab771-105">Get started with the Data Protection APIs</span></span>](using-data-protection.md)

* [<span data-ttu-id="ab771-106">使用者 API</span><span class="sxs-lookup"><span data-stu-id="ab771-106">Consumer APIs</span></span>](consumer-apis/index.md)

  * [<span data-ttu-id="ab771-107">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="ab771-107">Consumer APIs overview</span></span>](consumer-apis/overview.md)

  * [<span data-ttu-id="ab771-108">目标字符串</span><span class="sxs-lookup"><span data-stu-id="ab771-108">Purpose strings</span></span>](consumer-apis/purpose-strings.md)

  * [<span data-ttu-id="ab771-109">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="ab771-109">Purpose hierarchy and multi-tenancy</span></span>](consumer-apis/purpose-strings-multitenancy.md)

  * [<span data-ttu-id="ab771-110">密码哈希</span><span class="sxs-lookup"><span data-stu-id="ab771-110">Password hashing</span></span>](consumer-apis/password-hashing.md)

  * [<span data-ttu-id="ab771-111">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="ab771-111">Limiting the lifetime of protected payloads</span></span>](consumer-apis/limited-lifetime-payloads.md)

  * [<span data-ttu-id="ab771-112">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="ab771-112">Unprotecting payloads whose keys have been revoked</span></span>](consumer-apis/dangerous-unprotect.md)

* [<span data-ttu-id="ab771-113">配置</span><span class="sxs-lookup"><span data-stu-id="ab771-113">Configuration</span></span>](configuration/index.md)

  * [<span data-ttu-id="ab771-114">配置数据保护</span><span class="sxs-lookup"><span data-stu-id="ab771-114">Configuring data protection</span></span>](configuration/overview.md)

  * [<span data-ttu-id="ab771-115">默认设置</span><span class="sxs-lookup"><span data-stu-id="ab771-115">Default settings</span></span>](configuration/default-settings.md)

  * [<span data-ttu-id="ab771-116">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="ab771-116">Machine-wide policy</span></span>](configuration/machine-wide-policy.md)

  * [<span data-ttu-id="ab771-117">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="ab771-117">Non DI-aware scenarios</span></span>](configuration/non-di-scenarios.md)

* [<span data-ttu-id="ab771-118">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="ab771-118">Extensibility APIs</span></span>](extensibility/index.md)

  * [<span data-ttu-id="ab771-119">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="ab771-119">Core cryptography extensibility</span></span>](extensibility/core-crypto.md)

  * [<span data-ttu-id="ab771-120">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="ab771-120">Key management extensibility</span></span>](extensibility/key-management.md)

  * [<span data-ttu-id="ab771-121">其他 API</span><span class="sxs-lookup"><span data-stu-id="ab771-121">Miscellaneous APIs</span></span>](extensibility/misc-apis.md)

* [<span data-ttu-id="ab771-122">实现</span><span class="sxs-lookup"><span data-stu-id="ab771-122">Implementation</span></span>](implementation/index.md)

  * [<span data-ttu-id="ab771-123">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="ab771-123">Authenticated encryption details</span></span>](implementation/authenticated-encryption-details.md)

  * [<span data-ttu-id="ab771-124">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="ab771-124">Subkey derivation and authenticated encryption</span></span>](implementation/subkeyderivation.md)

  * [<span data-ttu-id="ab771-125">上下文标头</span><span class="sxs-lookup"><span data-stu-id="ab771-125">Context headers</span></span>](implementation/context-headers.md)

  * [<span data-ttu-id="ab771-126">密钥管理</span><span class="sxs-lookup"><span data-stu-id="ab771-126">Key management</span></span>](implementation/key-management.md)

  * [<span data-ttu-id="ab771-127">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="ab771-127">Key storage providers</span></span>](implementation/key-storage-providers.md)

  * [<span data-ttu-id="ab771-128">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="ab771-128">Key encryption at rest</span></span>](implementation/key-encryption-at-rest.md)

  * [<span data-ttu-id="ab771-129">密钥永久性和更改设置</span><span class="sxs-lookup"><span data-stu-id="ab771-129">Key immutability and changing settings</span></span>](implementation/key-immutability.md)

  * [<span data-ttu-id="ab771-130">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="ab771-130">Key storage format</span></span>](implementation/key-storage-format.md)

  * [<span data-ttu-id="ab771-131">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="ab771-131">Ephemeral data protection providers</span></span>](implementation/key-storage-ephemeral.md)

* [<span data-ttu-id="ab771-132">兼容性</span><span class="sxs-lookup"><span data-stu-id="ab771-132">Compatibility</span></span>](compatibility/index.md)

  * [<span data-ttu-id="ab771-133">在应用之间共享 cookie</span><span class="sxs-lookup"><span data-stu-id="ab771-133">Sharing cookies between apps</span></span>](compatibility/cookie-sharing.md)

  * [<span data-ttu-id="ab771-134">在 ASP.NET中替换 <machineKey></span><span class="sxs-lookup"><span data-stu-id="ab771-134">Replacing <machineKey> in ASP.NET</span></span>](compatibility/replacing-machinekey.md)
