---
description: STNumGeometries（geometry 数据类型）
title: STNumGeometries（geometry 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f988829d747889feeca37a538c4a0cb565d9dea6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181770"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries（geometry 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

返回构成 **geometry** 实例的几何图形的数目。
  
## <a name="syntax"></a>语法  
  
```  
  
.STNumGeometries ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>返回类型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回类型：int  
  
 CLR 返回类型：SqlInt32  
  
## <a name="remarks"></a>备注  
 如果 geometry 实例不是 MultiPoint、MultiLineString、MultiPolygon 或 GeometryCollection 实例，则此方法返回 1；如果 geometry 实例为空，则返回 0。  
  
> [!NOTE]  
>  如果 GeometryCollection 嵌套了空元素，则 `STNumGeometries()` 不会返回 0。 虽然 GeometryCollection 实例中的元素为空，但该实例本身不是空集。  
  
  

