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
# <a name="data-protection-in-aspnet-core"></a>ASP.NET Core 中的数据保护

* [数据保护简介](xref:security/data-protection/introduction)

* [数据保护 API 入门](xref:security/data-protection/using-data-protection)

* [使用者 API](xref:security/data-protection/consumer-apis/index)

  * [使用者 API 概述](xref:security/data-protection/consumer-apis/overview)

  * [目标字符串](xref:security/data-protection/consumer-apis/purpose-strings)

  * [目标层次结构和多租户](xref:security/data-protection/consumer-apis/purpose-strings-multitenancy)

  * [哈希密码](xref:security/data-protection/consumer-apis/password-hashing)

  * [限制受保护负载的生存期](xref:security/data-protection/consumer-apis/limited-lifetime-payloads)

  * [取消保护已撤消其密钥的负载](xref:security/data-protection/consumer-apis/dangerous-unprotect)

* [配置](xref:security/data-protection/configuration/index)

  * [配置 ASP.NET Core 数据保护](xref:security/data-protection/configuration/overview)

  * [默认设置](xref:security/data-protection/configuration/default-settings)

  * [计算机范围的策略](xref:security/data-protection/configuration/machine-wide-policy)

  * [非 DI 感知方案](xref:security/data-protection/configuration/non-di-scenarios)

* [扩展性 API](xref:security/data-protection/extensibility/index)

  * [核心加密扩展性](xref:security/data-protection/extensibility/core-crypto)

  * [密钥管理扩展性](xref:security/data-protection/extensibility/key-management)

  * [其他 API](xref:security/data-protection/extensibility/misc-apis)

* [实现](xref:security/data-protection/implementation/index)

  * [已验证的加密详细信息](xref:security/data-protection/implementation/authenticated-encryption-details)

  * [子项派生和已验证的加密](xref:security/data-protection/implementation/subkeyderivation)

  * [上下文标头](xref:security/data-protection/implementation/context-headers)

  * [密钥管理](xref:security/data-protection/implementation/key-management)

  * [密钥存储提供程序](xref:security/data-protection/implementation/key-storage-providers)

  * [静态密钥加密](xref:security/data-protection/implementation/key-encryption-at-rest)

  * [密钥永久性和设置](xref:security/data-protection/implementation/key-immutability)

  * [密钥存储格式](xref:security/data-protection/implementation/key-storage-format)

  * [短数据保护提供程序](xref:security/data-protection/implementation/key-storage-ephemeral)

* [兼容性](xref:security/data-protection/compatibility/index)

  * [在 ASP.NET Core 中替换 ASP.NET <machineKey>](xref:security/data-protection/compatibility/replacing-machinekey)
