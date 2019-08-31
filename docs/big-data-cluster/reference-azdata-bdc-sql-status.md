---
title: azdata bdc sql 状态引用
titleSuffix: SQL Server big data clusters
description: Azdata bdc sql 状态命令的参考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c5c2cdd924f266400125080d21d0461d5f599190
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158252"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql 状态

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的参考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc sql 状态显示](#azdata-bdc-sql-status-show) | Sql-服务器服务状态。
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc sql 状态显示
Sql-服务器服务状态。
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>示例
获取 sql 服务的状态。
```bash
azdata bdc sql status show
```
获取包含所有实例的 sql 服务的状态。
```bash
azdata bdc sql status show --all
```
获取 sql 服务中的主资源的状态。
```bash
azdata bdc sql status show --resource master
```
### <a name="optional-parameters"></a>可选参数
#### `--resource -r`
在此服务中获取此资源。
#### `--all -a`
显示服务中每个资源的所有实例。
### <a name="global-arguments"></a>全局参数
#### `--debug`
提高日志记录详细程度以显示所有调试日志。
#### `--help -h`
显示此帮助消息并退出。
#### `--output -o`
输出格式。  允许的值：json、jsonc、table、tsv。  默认值：json。
#### `--query -q`
JMESPath 查询字符串。 请参阅 [http://jmespath.org/](http://jmespath.org/])，获取详细信息和示例。
#### `--verbose`
提高日志记录详细程度。 使用 --debug 获取完整的调试日志。

## <a name="next-steps"></a>后续步骤

- 有关其他“azdata”命令的详细信息，请参阅 [azdata 参考](reference-azdata.md)。 

- 有关如何安装 **azdata** 工具的详细信息，请参阅[安装 azdata 以管理 SQL Server 2019 大数据群集](deploy-install-azdata.md)。