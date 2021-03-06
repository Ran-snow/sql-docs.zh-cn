---
description: sp_change_log_shipping_secondary_primary (Transact-SQL)
title: sp_change_log_shipping_secondary_primary (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_change_log_shipping_secondary_primary
- sp_change_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_primary
ms.assetid: 5bcb4df7-6df3-4f2b-9207-b97b5addf2a6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8352706512e71a5cba3a0b22befe2b7416d276bc
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2021
ms.locfileid: "99209345"
---
# <a name="sp_change_log_shipping_secondary_primary-transact-sql"></a>sp_change_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  更改辅助数据库设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_change_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server',  
[ @primary_database = ] 'primary_database',  
[, [ @backup_source_directory = ] 'backup_source_directory']  
[, [ @backup_destination_directory = ] 'backup_destination_directory']  
[, [ @file_retention_period = ] file_retention_period]  
[, [ @monitor_server_security_mode = ] monitor_server_security_mode]  
[, [ @monitor_server_login = ] 'monitor_server_login']  
[, [ @monitor_server_password = ] 'monitor_server_password']  
```  
  
## <a name="arguments"></a>参数  
`[ @primary_server = ] 'primary_server'`[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 日志传送配置中的主实例的名称。 *primary_server* 为 **sysname** ，且不能为 NULL。  
  
`[ @primary_database = ] 'primary_database'` 主服务器上的数据库的名称。 *primary_database* **sysname**，无默认值。  
  
`[ @backup_source_directory = ] 'backup_source_directory'` 存储主服务器中的事务日志备份文件的目录。 *backup_source_directory* 为 **nvarchar (500)** ，且不能为 NULL。  
  
`[ @backup_destination_directory = ] 'backup_destination_directory'` 辅助服务器上将备份文件复制到的目录。 *backup_destination_directory* 为 **nvarchar (500)** ，且不能为 NULL。  
  
`[ @file_retention_period = ] 'file_retention_period'` 将保留历史记录的时间长度（分钟）。 *history_retention_period* 的值为 **int**，默认值为 NULL。 如果未指定值，则使用值 14420。  
  
`[ @monitor_server_security_mode = ] 'monitor_server_security_mode'` 用于连接到监视服务器的安全模式。  
  
 1 = Windows 身份验证；  
  
 0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 *monitor_server_security_mode* 是 **bit** ，并且不能为 NULL。  
  
`[ @monitor_server_login = ] 'monitor_server_login'` 用于访问监视服务器的帐户的用户名。  
  
`[ @monitor_server_password = ] 'monitor_server_password'` 用于访问监视服务器的帐户的密码。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 必须从辅助服务器上的 **master** 数据库运行 **sp_change_log_shipping_secondary_primary** 。 此存储过程执行以下操作：  
  
1.  根据需要更改 **log_shipping_secondary** 记录中的设置。  
  
2.  如果监视服务器不同于辅助服务器，则会根据需要使用提供的参数更改监视服务器上 **log_shipping_monitor_secondary** 中的监视记录。  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员才能运行此过程。  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
