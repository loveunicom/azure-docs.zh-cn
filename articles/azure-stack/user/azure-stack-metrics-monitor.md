---
title: 使用 Azure Stack 中的监视数据 |Microsoft Docs
description: 了解有关使用 Azure Stack 中的监视数据的选项。
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/14/2018
ms.author: mabrigg
ms.openlocfilehash: b6196ec434d00a6fbc6714095fa4182ede98ce91
ms.sourcegitcommit: ab9514485569ce511f2a93260ef71c56d7633343
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2018
ms.locfileid: "45633429"
---
# <a name="how-to-consume-monitoring-data-from-azure-stack"></a>如何使用 Azure Stack 中的监视数据

*适用于：Azure Stack 集成系统和 Azure Stack 开发工具包*

您可以找到与 Azure Monitor 管道，只需在一个位置中的监视数据等全球 Azure 中的 Azure Monitor。 但不是所有监视数据在全球 Azure 中找到 Azure Stack 中提供。 在本文中，你可以找到你可以以编程方式引入该服务中的监视数据的各种方法的摘要。
 
## <a name="options-for-data-consumption"></a>数据使用选项

| 数据类型 | 类别 | 支持的服务 | 访问方法 |
|-------------------------------------------------------------|----------|------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| Azure Monitor 平台级指标 | 度量值 | [Azure Stack 上的 Azure Monitor 支持的指标](azure-stack-metrics-supported.md) | REST API |
| 计算来宾 OS 指标 （例如，性能计数） | 度量值 | Windows 和 Linux 虚拟机 | 存储表或 blob:<br>Windows 或 Linux Azure 诊断 <br>事件中心：<br>Windows Azure 诊断 |
| 存储度量值 | 度量值 | Azure 存储 | 存储表：<br>存储分析 |
| 活动日志 | 活动 | 所有 Azure 服务 | REST API：<br>Azure Monitor 事件 API |
| 计算来宾 OS 日志 (例如，IIS、 ETW、 syslog) | 活动 | Windows 和 Linux 虚拟机 | 存储表或 blob:<br>Windows 或 Linux Azure 诊断 <br>事件中心：<br>Windows Azure 诊断 |
| 存储日志 | 活动 | Azure 存储 | 存储表：<br>存储分析 |

## <a name="next-steps"></a>后续步骤

详细了解如何[监视 Azure Stack 上的 Azure](azure-stack-metrics-azure-data.md)。
