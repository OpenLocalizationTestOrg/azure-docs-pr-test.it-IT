---
title: "aaaPause, riprendere, la scalabilità orizzontale con T-SQL in Azure SQL Data Warehouse | Documenti Microsoft"
description: "Prestazioni tooscale-out di Transact-SQL (T-SQL) attività regolando Dwu. Risparmiare sui costi eseguendo una scalabilità orizzontale durante le ore non di punta."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Gestire la potenza di calcolo in Azure SQL Data Warehouse (T-SQL)
> [!div class="op_single_selector"]
> * [Panoramica](sql-data-warehouse-manage-compute-overview.md)
> * [Portale](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>Visualizzare le impostazioni DWU correnti
tooview hello DWU impostazioni correnti per i database:

1. Aprire Esplora oggetti di SQL Server in Visual Studio.
2. La connessione a database master di toohello associato hello logico del Database di SQL server.
3. Selezionare dalla vista a gestione dinamica sys.database_service_objectives hello. Di seguito è fornito un esempio: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Ridimensionare le risorse di calcolo
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

hello toochange Dwu:

1. Connettersi a database master di toohello associato con il server logico di Database SQL.
2. Hello utilizzare [ALTER DATABASE] [ ALTER DATABASE] istruzione TSQL. Hello esempio imposta hello servizio livello obiettivo tooDW1000 per database hello MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Controllare lo stato del database e l'avanzamento dell'operazione

1. Connettersi a database master di toohello associato con il server logico di Database SQL.
2. Inviare lo stato di database toocheck query

```sql
SELECT *
FROM
sys.databases
```

3. Inviare query toocheck sullo stato dell'operazione

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Questa DMV restituisce informazioni sulle varie operazioni di gestione nel proprio SQL Data Warehouse, ad esempio lo stato di operazione e hello hello dell'operazione di hello, che sarà IN_PROGRESS o completato.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Passaggi successivi
Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
