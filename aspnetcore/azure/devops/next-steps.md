---
title: 使用 ASP.NET Core 和 Azure DevOps |后续步骤
author: CamSoper
description: 提供有关为托管在 Azure 中的 ASP.NET Core 应用构建 DevOps 管道的端到端指导的指南。
ms.author: casoper
ms.date: 08/07/2018
uid: azure/devops/next-steps
ms.openlocfilehash: 7a0f1b1b56a33b1870e0657d8ba465adb84f5a02
ms.sourcegitcommit: d53e0cc71542b92de867bcce51575b054886f529
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "42909900"
---
# <a name="next-steps"></a>后续步骤

在本指南中，您将创建 ASP.NET Core 示例应用的 DevOps 管道。 祝贺你！ 我们希望您喜欢学习来将 ASP.NET Core web 应用发布到 Azure 应用服务，并自动执行更改的持续集成。

Web 宿主和 DevOps，超出 Azure 有广泛的平台-作为-服务 (PaaS) 服务适用于 ASP.NET Core 开发人员。 本部分提供的一些最常使用的服务的简要概述。

## <a name="storage-and-databases"></a>存储和数据库

[Redis 缓存](https://docs.microsoft.com/azure/redis-cache/)是缓存可作为服务的高吞吐量、 低延迟数据。 它可以用于缓存页面输出、 减少数据库请求和 ASP.NET Core 会话状态提供应用的多个实例。

[Azure 存储](https://docs.microsoft.com/azure/storage/)是 Azure 的大规模可缩放的云存储。 开发人员可以利用[队列存储](https://docs.microsoft.com/azure/storage/queues/storage-queues-introduction)可靠的消息队列，并[表存储](https://docs.microsoft.com/azure/storage/tables/table-storage-overview)是设计用于快速开发使用大规模、 半结构化数据集的 NoSQL 键-值存储。

[Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/)提供的熟悉的关系数据库功能与使用 Microsoft SQL Server 引擎的服务。

[Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)全球分布的多模型 NoSQL 数据库服务。 多个 Api 都可用，包括 SQL API （以前称为 DocumentDB）、 Cassandra 和 MongoDB。

## <a name="identity"></a>标识

[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)并[Azure Active Directory B2C](https://docs.microsoft.com/azure/active-directory-b2c/)是这两个标识服务。 Azure Active Directory 专为企业方案和时在 Azure Active Directory B2C 是预期的业务客户方案，包括社交网络单一登录启用 Azure AD B2B （企业到企业） 协作。

## <a name="mobile"></a>移动电话

[通知中心](https://docs.microsoft.com/azure/notification-hubs/)是一种多平台且可扩展的推送通知引擎快速发送数百万条消息到各种类型的设备上运行的应用。

## <a name="web-infrastructure"></a>Web 基础结构

[Azure 容器服务](https://docs.microsoft.com/azure/aks/)管理托管的 Kubernetes 环境，使它快速、 轻松地部署和管理容器化的应用而无需容器业务流程专业知识。

[Azure 搜索](https://docs.microsoft.com/azure/search/)用于基于专用异类内容创建一种企业搜索解决方案。

[Service Fabric](https://docs.microsoft.com/azure/service-fabric/)是一个分布式的系统平台，轻松地打包、 部署和管理可缩放和可靠的微服务和容器。
