---
title: Azure CLI 脚本示例 - 获取 Azure Redis 缓存的详细信息 | Microsoft Docs
description: Azure CLI 脚本示例 - 获取 Azure Redis 缓存的详细信息
services: redis-cache
documentationcenter: ''
author: wesmc7777
manager: cfowler
editor: ''
tags: azure-service-management
ms.assetid: 155924e6-00d5-4a8c-ba99-5189f300464a
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/30/2017
ms.author: wesmc
ms.openlocfilehash: 00ae8e00d456d4660cadf645d4521173d254bbd7
ms.sourcegitcommit: 8c3267c34fc46c681ea476fee87f5fb0bf858f9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2018
ms.locfileid: "29846241"
---
# <a name="get-details-of-an-azure-redis-cache"></a>获取 Azure Redis 缓存的详细信息

在此方案中，将了解如何检索 Azure Redis 缓存实例的详细信息，包括其预配状态。

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>示例脚本

[!code-azurecli[main](../../../cli_scripts/redis-cache/show-cache/show-cache.sh "Azure Redis Cache")]

## <a name="script-explanation"></a>脚本说明

此脚本使用以下命令检索 Azure Redis 缓存实例的详细信息。 表中的每条命令均链接到特定于命令的文档。

| 命令 | 说明 |
|---|---|
| [az redis show](https://docs.microsoft.com/cli/azure/redis#az_redis_show) | 检索 Azure Redis 缓存实例的详细信息。 |


## <a name="next-steps"></a>后续步骤

有关 Azure CLI 的详细信息，请参阅 [Azure CLI 文档](https://docs.microsoft.com/cli/azure)。

可以在 [Azure Redis 缓存文档](../cli-samples.md)中找到其他 Azure Redis 缓存 CLI 脚本示例。