---
description: 更改跟踪函数 (Transact-SQL)
title: " (Transact-sql) 更改跟踪函数 |Microsoft Docs"
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], change tracking
- change tracking [SQL Server], functions
ms.assetid: 04eb53c4-8b69-414e-9696-185d227fea35
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 98713d32007aecb6eec05dc172fd57d3af08aba0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2021
ms.locfileid: "99196178"
---
# <a name="change-tracking-functions-transact-sql"></a>更改跟踪函数 (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  更改跟踪函数用于记录应用于被跟踪表的插入、更新和删除操作，同时采用易于使用的关系格式提供有关更改的详细信息。 下列函数返回有关更改的信息。  
  
|功能|说明|  
|--------------|-----------------|  
|[CHANGETABLE (更改) ](../../relational-databases/system-functions/changetable-transact-sql.md)|返回自指定版本起对表所做的所有更改的跟踪信息。|  
|[CHANGETABLE (版本) ](../../relational-databases/system-functions/changetable-transact-sql.md)|返回指定行的最新更改跟踪信息。|  
|[CHANGE_TRACKING_MIN_VALID_VERSION ( # B1 ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)|返回在使用 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) 函数时从指定表获取更改跟踪信息所使用的最小版本。|  
|[CHANGE_TRACKING_CURRENT_VERSION](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)|获取与上次提交事务关联的版本。 可以在下次使用 CHANGETABLE 枚举更改时使用此版本。|  
|[CHANGE_TRACKING_IS_COLUMN_IN_MASK](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)|解释 CHANGETABLE (CHANGES ... ) 函数返回的 SYS_CHANGE_COLUMNS 值。|  
|[WITH CHANGE_TRACKING_CONTEXT](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md)|用于在应用程序更改数据时指定更改上下文，例如发起方 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [跟踪数据更改 (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
