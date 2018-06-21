---
title: ASP.NET Core 中的数据保护
author: rick-anderson
description: 此文档充当各 ASP.NET Core 数据保护主题的目录。
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/index
ms.openlocfilehash: 1c38c587956dd99078fa4386c2f4423d784abc60
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277119"
---
# <a name="data-protection-in-aspnet-core"></a><span data-ttu-id="a3991-103">ASP.NET Core 中的数据保护</span><span class="sxs-lookup"><span data-stu-id="a3991-103">Data Protection in ASP.NET Core</span></span>

* [<span data-ttu-id="a3991-104">数据保护简介</span><span class="sxs-lookup"><span data-stu-id="a3991-104">Introduction to data protection</span></span>](xref:security/data-protection/introduction)

* [<span data-ttu-id="a3991-105">数据保护 API 入门</span><span class="sxs-lookup"><span data-stu-id="a3991-105">Get started with the Data Protection APIs</span></span>](xref:security/data-protection/using-data-protection)

* [<span data-ttu-id="a3991-106">使用者 API</span><span class="sxs-lookup"><span data-stu-id="a3991-106">Consumer APIs</span></span>](xref:security/data-protection/consumer-apis/index)

  * [<span data-ttu-id="a3991-107">使用者 API 概述</span><span class="sxs-lookup"><span data-stu-id="a3991-107">Consumer APIs overview</span></span>](xref:security/data-protection/consumer-apis/overview)

  * [<span data-ttu-id="a3991-108">目标字符串</span><span class="sxs-lookup"><span data-stu-id="a3991-108">Purpose strings</span></span>](xref:security/data-protection/consumer-apis/purpose-strings)

  * [<span data-ttu-id="a3991-109">目标层次结构和多租户</span><span class="sxs-lookup"><span data-stu-id="a3991-109">Purpose hierarchy and multi-tenancy</span></span>](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)

  * [<span data-ttu-id="a3991-110">哈希密码</span><span class="sxs-lookup"><span data-stu-id="a3991-110">Hash passwords</span></span>](xref:security/data-protection/consumer-apis/password-hashing)

  * [<span data-ttu-id="a3991-111">限制受保护负载的生存期</span><span class="sxs-lookup"><span data-stu-id="a3991-111">Limit the lifetime of protected payloads</span></span>](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)

  * [<span data-ttu-id="a3991-112">取消保护已撤消其密钥的负载</span><span class="sxs-lookup"><span data-stu-id="a3991-112">Unprotect payloads whose keys have been revoked</span></span>](xref:security/data-protection/consumer-apis/dangerous-unprotect)

* [<span data-ttu-id="a3991-113">配置</span><span class="sxs-lookup"><span data-stu-id="a3991-113">Configuration</span></span>](xref:security/data-protection/configuration/index)

  * [<span data-ttu-id="a3991-114">配置 ASP.NET Core 数据保护</span><span class="sxs-lookup"><span data-stu-id="a3991-114">Configure ASP.NET Core Data Protection</span></span>](xref:security/data-protection/configuration/overview)

  * [<span data-ttu-id="a3991-115">默认设置</span><span class="sxs-lookup"><span data-stu-id="a3991-115">Default settings</span></span>](xref:security/data-protection/configuration/default-settings)

  * [<span data-ttu-id="a3991-116">计算机范围的策略</span><span class="sxs-lookup"><span data-stu-id="a3991-116">Machine-wide policy</span></span>](xref:security/data-protection/configuration/machine-wide-policy)

  * [<span data-ttu-id="a3991-117">非 DI 感知方案</span><span class="sxs-lookup"><span data-stu-id="a3991-117">Non DI-aware scenarios</span></span>](xref:security/data-protection/configuration/non-di-scenarios)

* [<span data-ttu-id="a3991-118">扩展性 API</span><span class="sxs-lookup"><span data-stu-id="a3991-118">Extensibility APIs</span></span>](xref:security/data-protection/extensibility/index)

  * [<span data-ttu-id="a3991-119">核心加密扩展性</span><span class="sxs-lookup"><span data-stu-id="a3991-119">Core cryptography extensibility</span></span>](xref:security/data-protection/extensibility/core-crypto)

  * [<span data-ttu-id="a3991-120">密钥管理扩展性</span><span class="sxs-lookup"><span data-stu-id="a3991-120">Key management extensibility</span></span>](xref:security/data-protection/extensibility/key-management)

  * [<span data-ttu-id="a3991-121">其他 API</span><span class="sxs-lookup"><span data-stu-id="a3991-121">Miscellaneous APIs</span></span>](xref:security/data-protection/extensibility/misc-apis)

* [<span data-ttu-id="a3991-122">实现</span><span class="sxs-lookup"><span data-stu-id="a3991-122">Implementation</span></span>](xref:security/data-protection/implementation/index)

  * [<span data-ttu-id="a3991-123">已验证的加密详细信息</span><span class="sxs-lookup"><span data-stu-id="a3991-123">Authenticated encryption details</span></span>](xref:security/data-protection/implementation/authenticated-encryption-details)

  * [<span data-ttu-id="a3991-124">子项派生和已验证的加密</span><span class="sxs-lookup"><span data-stu-id="a3991-124">Subkey derivation and authenticated encryption</span></span>](xref:security/data-protection/implementation/subkeyderivation)

  * [<span data-ttu-id="a3991-125">上下文标头</span><span class="sxs-lookup"><span data-stu-id="a3991-125">Context headers</span></span>](xref:security/data-protection/implementation/context-headers)

  * [<span data-ttu-id="a3991-126">密钥管理</span><span class="sxs-lookup"><span data-stu-id="a3991-126">Key management</span></span>](xref:security/data-protection/implementation/key-management)

  * [<span data-ttu-id="a3991-127">密钥存储提供程序</span><span class="sxs-lookup"><span data-stu-id="a3991-127">Key storage providers</span></span>](xref:security/data-protection/implementation/key-storage-providers)

  * [<span data-ttu-id="a3991-128">静态密钥加密</span><span class="sxs-lookup"><span data-stu-id="a3991-128">Key encryption at rest</span></span>](xref:security/data-protection/implementation/key-encryption-at-rest)

  * [<span data-ttu-id="a3991-129">密钥永久性和设置</span><span class="sxs-lookup"><span data-stu-id="a3991-129">Key immutability and settings</span></span>](xref:security/data-protection/implementation/key-immutability)

  * [<span data-ttu-id="a3991-130">密钥存储格式</span><span class="sxs-lookup"><span data-stu-id="a3991-130">Key storage format</span></span>](xref:security/data-protection/implementation/key-storage-format)

  * [<span data-ttu-id="a3991-131">短数据保护提供程序</span><span class="sxs-lookup"><span data-stu-id="a3991-131">Ephemeral data protection providers</span></span>](xref:security/data-protection/implementation/key-storage-ephemeral)

* [<span data-ttu-id="a3991-132">兼容性</span><span class="sxs-lookup"><span data-stu-id="a3991-132">Compatibility</span></span>](xref:security/data-protection/compatibility/index)

  * [<span data-ttu-id="a3991-133">在 ASP.NET Core 中替换 ASP.NET <machineKey></span><span class="sxs-lookup"><span data-stu-id="a3991-133">Replacing ASP.NET <machineKey> in ASP.NET Core</span></span>](xref:security/data-protection/compatibility/replacing-machinekey)
