---
description: sys.sysforeignkeys (Transact-SQL)
title: sys.sysforeignkeys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sysforeignkeys
- sys.sysforeignkeys
- sys.sysforeignkeys_TSQL
- sysforeignkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysforeignkeys system table
- sys.sysforeignkeys compatibility view
ms.assetid: 41544236-1c46-4501-be88-18c06963b6e8
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: edbb686df3d410b6049bca2799e0f10b2ff07db8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2021
ms.locfileid: "99158523"
---
# <a name="syssysforeignkeys-transact-sql"></a>sys.sysforeignkeys (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  包含有关数据库内的表定义中的 FOREIGN KEY 约束的信息。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 约束的 ID。|  
|**fkeyid**|**int**|具有 FOREIGN KEY 约束的表的对象 ID。|  
|**rkeyid**|**int**|在 FOREIGN KEY 约束中引用的表的对象 ID。|  
|**fkey**|**smallint**|引用列的 ID。|  
|**rkey**|**smallint**|被引用列的 ID。|  
|**keyno**|**smallint**|该列在引用列列表中的位置。|  
  
## <a name="see-also"></a>另请参阅  
 [将系统表映射到系统视图 &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [兼容性视图 (Transact SQL)](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
