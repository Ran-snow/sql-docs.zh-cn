---
description: sp_remoteoption (Transact-SQL)
title: sp_remoteoption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_remoteoption_TSQL
- sp_remoteoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_remoteoption
ms.assetid: c9a7309b-eab7-4192-a414-e282581af4e5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aff4a43e54c6bbb8e6c406d6b48452fc84915e9f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2021
ms.locfileid: "99185640"
---
# <a name="sp_remoteoption-transact-sql"></a>sp_remoteoption (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  显示或更改在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地服务器中定义的远程登录的选项。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]sp_remoteoption 将不更改任何选项并返回一条错误消息。 仅用于支持向后兼容性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_remoteoption [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @loginame = ] 'loginame' ]   
     [ , [ @remotename = ] 'remotename' ]   
     [ , [ @optname = ] 'optname' ]   
     [ , [ @optvalue = ] 'optvalue' ]  
```  
  
## <a name="remarks"></a>备注  
 此存储过程返回以下错误消息：  
  
 `The trusted option in remote login mapping is no longer supported.`  
  
## <a name="see-also"></a>另请参阅  
 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
  
