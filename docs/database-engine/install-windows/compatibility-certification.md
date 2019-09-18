---
title: 兼容性认证 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
- Databases [SQL Server], upgrading
- Database Engine [SQL Server], upgrading
- compatibility [SQL Server], certification
- compatibility level [SQL Server], upgrades
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433856
author: pmasl
ms.author: pelopes
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 0c10566cca9c92dc54efdd4f0f4248b087b670ea
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70122973"
---
# <a name="compatibility-certification"></a>兼容性认证

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

兼容性认证使企业能够在本地、云中和边缘升级和现代化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，消除了应用程序兼容性风险。 

相同的 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 同时支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]（包括托管实例）。 此共享 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 意味着用户数据库可以在本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 之间顺畅移动，而在数据库中以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 执行的应用程序代码将继续像在源系统中那样工作。

对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的每个新版本，默认兼容性级别将设置为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的版本。 但会保留以前版本的兼容性级别，以持续兼容现有应用程序。 此兼容性矩阵可在[此处](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats)查看。
因此，经认证可与给定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本一起使用的应用程序实际上经过了认证，可在该版本的默认兼容性级别工作。

例如，数据库兼容性级别 130 是 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 的默认兼容性级别。 由于兼容性级别强制执行特定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能和查询优化行为，因此在数据库兼容性级别 130 上隐式认证了经认证可在 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 上工作的数据库。 只要数据库兼容性级别保持为 130，此数据库就可以像在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更新版本（如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 和 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]）中工作。 

这是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 持续集成操作模型的基本原则。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 在 Azure 中持续改进和升级，但由于现有数据库保持其当前兼容性级别，因此即使在升级到基础 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 数据库后，它们仍将继续按设计的形式工作。 

## <a name="managing-upgrade-risk-with-compatibility-certification"></a>利用兼容性认证管理升级风险
使用兼容性认证是数据库现代化的一种非常有用的方法。 通过基于兼容性级别进行认证，开发人员可以将应用程序的技术要求设置为在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 上受支持，但应用程序生命周期将从数据库平台生命周期分离出来。 这样，公司便可以根据生命周期策略的要求来升级 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、利用不依赖于代码的全新可伸缩性和性能增强，以及通过升级连接应用程序以保持其功能状态  。

对功能和性能产生负面影响的可能性是任何升级的主要风险因素。 通过兼容性认证，你可以放心地管理以下升级风险：

-  在与 [!INCLUDE[tsql](../../includes/tsql-md.md)] 行为相关的方面，任何更改都意味着需要重新认证应用程序的正确性。 然而，[数据库兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)设置提供与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 早期版本的后向兼容性，但后向兼容性仅适用于指定的数据库，而不适用于整个服务器。 保持数据库兼容性级别不变可确保现有应用程序查询在 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 升级之前和之后继续显示相同的行为。 有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] 行为和兼容性级别的详细信息，请参阅[使用兼容性级别实现后向兼容性](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#using-compatibility-level-for-backward-compatibility)。

-  在与性能相关的方面，由于每个版本都会引入查询优化器改进，因此，可能会遇到不同 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 版本之间的查询计划差异。 如果某些更改可能会对给定的查询或工作负载产生负面影响，则升级范围内的查询计划差异通常会转换为风险。 这种风险会促使进行重新认证，进而延迟升级并带来生命周期和支持挑战。 
   由于需要降低升级风险，因此查询优化器改进被限制为新版本的默认兼容性级别。 兼容性认证包括查询计划形状保护。查询计划形状保护是指在 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 升级后立即将数据库兼容性级别保持原样的概念，这意味着用于在新版本中创建查询计划的查询优化模型与升级之前相同  。 有关查询计划形状保护的详细信息，请参阅[使用兼容性级别实现后向兼容性](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#using-compatibility-level-for-backward-compatibility)。
   
只要应用程序不需要使用仅在更高数据库兼容性级别中可用的增强功能，它就是升级 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和维护之前的数据库兼容性级别的有效方法，而无需重新认证应用程序。 有关详细信息，请参阅本文后面部分的[兼容性级别和数据库引擎升级](#compatibility-levels-and-database-engine-upgrades)。

对于新的开发工作，或当现有应用程序需要使用新功能（如[智能查询处理](../../relational-databases/performance/intelligent-query-processing.md)）以及一些新的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 时，请计划将数据库兼容性级别升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的最新级别，并认证应用程序可与该兼容性级别一起使用。 有关升级数据库兼容性级别的更多详细信息，请参阅[升级数据库兼容性级别的最佳做法](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)。

## <a name="compatibility-certification-benefits"></a>兼容性认证的好处
数据库认证作为基于兼容性的方法而不是命名版本方法有几个直接好处：

-  将应用程序认证从平台分离出来  。 由于其共享的 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]，因此对于只需执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询的应用程序，无需为 Azure 和本地维护单独的认证过程。
-  降低升级风险，由于在数据库平台现代化期间，可以分离应用程序与数据库平台层升级周期，因此减少了中断，改进了变更管理  。
-  升级而不更改代码  。 升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 的新版本可以保持与源系统相同的兼容性级别，而无需对代码进行更改，并且不需要立即重新认证，直到应用程序需要使用仅在更高的数据库兼容性级别中可用的增强功能。
- 提高可管理性和可伸缩性，无需更改应用程序并可使用不受数据库兼容性级别限制的增强功能  。 例如，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这些功能包括： 
  - 丰富的监控和故障排除改进，并提供新的[系统动态管理视图](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)、[扩展事件](../../relational-databases/extended-events/extended-events.md)和[自动优化](../../relational-databases/automatic-tuning/automatic-tuning.md)。 
  - 更高的可伸缩性，例如，提供[自动 Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa)。

新数据库仍设置为 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 版本的默认兼容性级别。 但在将数据库从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的任何早期版本迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 的新版本时，数据库将保留其现有的兼容性级别。 

> [!IMPORTANT]
> 将数据库迁移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 的新版本之前，请验证该数据库兼容性级别是否仍受支持。 数据库兼容性级别支持矩阵可在[此处](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#arguments)查看。 
>
> 升级兼容性级别低于允许级别（例如，[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中的默认级别 90）的数据库会将数据库设置为允许的最低兼容性级别 (100)。
>
> 若要确定当前兼容级别，请查询 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 的 compatibility_level  列。

## <a name="compatibility-levels-and-database-engine-upgrades"></a>兼容性级别和数据库引擎升级
若要将 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]升级到最新版本，同时维持升级前的数据库兼容性级别及其可支持性状态，建议在数据库（存储过程、函数、触发器等可编程对象）和应用程序（使用捕获应用程序发送的动态代码的工作负荷跟踪）中，使用 [Microsoft 数据迁移助手](https://www.microsoft.com/download/details.aspx?id=53595)工具 (DMA) 对应用程序代码执行静态函数外围应用验证。 DMA 工具输出中没有关于缺失或不兼容功能的错误，可保护应用程序免受新目标版本上的任何功能回归影响。 有关详细信息，请参阅[数据迁移助手概述](../../dma/dma-overview.md)。

> [!NOTE]
> DMA 支持数据库兼容性级别 100 及更高级别。 排除 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 作为源版本。   

> [!IMPORTANT]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建议执行一些最小测试来验证升级是否成功，同时维持之前的数据库兼容性级别。 应该确定适用于自己的应用程序和场景的最小测试。   

> [!NOTE]
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 在下列情况下提供查询计划形状保护：
>
> - 新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（目标）在相当于之前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本（源）运行的硬件上运行。
> - 目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 均使用同一[支持的数据库兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats)。
>
> 上述情况下发生的任何查询计划形状回归（与源 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相比）将得到解决。 如果出现这种情况，请与 Microsoft 客户支持服务部门联系。
  
## <a name="see-also"></a>另请参阅 
[修改数据库兼容性级别](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)       
[查看或更改数据库的兼容级别](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)       
[升级数据库兼容性级别的最佳做法](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#best-practices-for-upgrading-database-compatibility-level)      