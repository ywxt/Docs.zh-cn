---
title: "ASP.NET Core 中的数据保护"
author: rick-anderson
description: "此文档充当各 ASP.NET Core 数据保护主题的目录。"
keywords: "ASP.NET Core, 数据保护"
ms.author: riande
manager: wpickett
ms.date: 10/14/2016
ms.topic: article
ms.assetid: 1f402da8-1052-4970-9835-9f9f16a02dbc
ms.technology: aspnet
ms.prod: asp.net-core
uid: security/data-protection/index
ms.openlocfilehash: cbf18c6ec867fefec22980f3e3493562594ef72d
ms.sourcegitcommit: 12e5194936b7e820efc5505a2d5d4f84e88eb5ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2018
---
# <a name="data-protection-in-aspnet-core-consumer-apis-configuration-extensibility-apis-and-implementation"></a><span data-ttu-id="f4f03-104">ASP.NET Core 中的数据保护：使用者 API、配置、扩展性 API 和实现</span><span class="sxs-lookup"><span data-stu-id="f4f03-104">Data Protection in ASP.NET Core: Consumer APIs, configuration, extensibility APIs and implementation</span></span>

* [<span data-ttu-id="f4f03-105">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="f4f03-105">Introduction to data protection</span></span>](introduction.md)

* [<span data-ttu-id="f4f03-106">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="f4f03-106">Get started with the Data Protection APIs</span></span>](using-data-protection.md)

* [<span data-ttu-id="f4f03-107">使用者 API</span><span class="sxs-lookup"><span data-stu-id="f4f03-107">Consumer APIs</span></span>](consumer-apis/index.md)

  * [<span data-ttu-id="f4f03-108">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="f4f03-108">Consumer APIs overview</span></span>](consumer-apis/overview.md)

  * [<span data-ttu-id="f4f03-109">目标字符串</span><span class="sxs-lookup"><span data-stu-id="f4f03-109">Purpose strings</span></span>](consumer-apis/purpose-strings.md)

  * [<span data-ttu-id="f4f03-110">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="f4f03-110">Purpose hierarchy and multi-tenancy</span></span>](consumer-apis/purpose-strings-multitenancy.md)

  * [<span data-ttu-id="f4f03-111">密码哈希</span><span class="sxs-lookup"><span data-stu-id="f4f03-111">Password hashing</span></span>](consumer-apis/password-hashing.md)

  * [<span data-ttu-id="f4f03-112">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="f4f03-112">Limiting the lifetime of protected payloads</span></span>](consumer-apis/limited-lifetime-payloads.md)

  * [<span data-ttu-id="f4f03-113">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="f4f03-113">Unprotecting payloads whose keys have been revoked</span></span>](consumer-apis/dangerous-unprotect.md)

* [<span data-ttu-id="f4f03-114">配置</span><span class="sxs-lookup"><span data-stu-id="f4f03-114">Configuration</span></span>](configuration/index.md)

  * [<span data-ttu-id="f4f03-115">配置数据保护</span><span class="sxs-lookup"><span data-stu-id="f4f03-115">Configuring data protection</span></span>](configuration/overview.md)

  * [<span data-ttu-id="f4f03-116">默认设置</span><span class="sxs-lookup"><span data-stu-id="f4f03-116">Default settings</span></span>](configuration/default-settings.md)

  * [<span data-ttu-id="f4f03-117">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="f4f03-117">Machine-wide policy</span></span>](configuration/machine-wide-policy.md)

  * [<span data-ttu-id="f4f03-118">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="f4f03-118">Non DI-aware scenarios</span></span>](configuration/non-di-scenarios.md)

* [<span data-ttu-id="f4f03-119">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="f4f03-119">Extensibility APIs</span></span>](extensibility/index.md)

  * [<span data-ttu-id="f4f03-120">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="f4f03-120">Core cryptography extensibility</span></span>](extensibility/core-crypto.md)

  * [<span data-ttu-id="f4f03-121">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="f4f03-121">Key management extensibility</span></span>](extensibility/key-management.md)

  * [<span data-ttu-id="f4f03-122">其他 API</span><span class="sxs-lookup"><span data-stu-id="f4f03-122">Miscellaneous APIs</span></span>](extensibility/misc-apis.md)

* [<span data-ttu-id="f4f03-123">实现</span><span class="sxs-lookup"><span data-stu-id="f4f03-123">Implementation</span></span>](implementation/index.md)

  * [<span data-ttu-id="f4f03-124">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="f4f03-124">Authenticated encryption details</span></span>](implementation/authenticated-encryption-details.md)

  * [<span data-ttu-id="f4f03-125">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="f4f03-125">Subkey derivation and authenticated encryption</span></span>](implementation/subkeyderivation.md)

  * [<span data-ttu-id="f4f03-126">上下文标头</span><span class="sxs-lookup"><span data-stu-id="f4f03-126">Context headers</span></span>](implementation/context-headers.md)

  * [<span data-ttu-id="f4f03-127">密钥管理</span><span class="sxs-lookup"><span data-stu-id="f4f03-127">Key management</span></span>](implementation/key-management.md)

  * [<span data-ttu-id="f4f03-128">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="f4f03-128">Key storage providers</span></span>](implementation/key-storage-providers.md)

  * [<span data-ttu-id="f4f03-129">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="f4f03-129">Key encryption at rest</span></span>](implementation/key-encryption-at-rest.md)

  * [<span data-ttu-id="f4f03-130">密钥永久性和更改设置</span><span class="sxs-lookup"><span data-stu-id="f4f03-130">Key immutability and changing settings</span></span>](implementation/key-immutability.md)

  * [<span data-ttu-id="f4f03-131">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="f4f03-131">Key storage format</span></span>](implementation/key-storage-format.md)

  * [<span data-ttu-id="f4f03-132">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="f4f03-132">Ephemeral data protection providers</span></span>](implementation/key-storage-ephemeral.md)

* [<span data-ttu-id="f4f03-133">兼容性</span><span class="sxs-lookup"><span data-stu-id="f4f03-133">Compatibility</span></span>](compatibility/index.md)

  * [<span data-ttu-id="f4f03-134">在应用之间共享 cookie</span><span class="sxs-lookup"><span data-stu-id="f4f03-134">Sharing cookies between apps</span></span>](compatibility/cookie-sharing.md)

  * [<span data-ttu-id="f4f03-135">在 ASP.NET中替换 <machineKey></span><span class="sxs-lookup"><span data-stu-id="f4f03-135">Replacing <machineKey> in ASP.NET</span></span>](compatibility/replacing-machinekey.md)
