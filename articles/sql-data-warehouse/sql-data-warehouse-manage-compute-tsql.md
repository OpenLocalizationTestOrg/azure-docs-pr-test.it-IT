---
title: Sospendere, riprendere e ridimensionare con T-SQL in Azure SQL Data Warehouse | Documentazione Microsoft
description: "Attività di Transact-SQL (T-SQL) per scalare orizzontalmente le prestazioni cambiando il numero delle DWU. Risparmiare sui costi eseguendo una scalabilità orizzontale durante le ore non di punta."
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
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="5a570-104">Gestire la potenza di calcolo in Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="5a570-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a570-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5a570-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="5a570-106">Portale</span><span class="sxs-lookup"><span data-stu-id="5a570-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="5a570-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a570-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="5a570-108">REST</span><span class="sxs-lookup"><span data-stu-id="5a570-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="5a570-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="5a570-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="5a570-110">Visualizzare le impostazioni DWU correnti</span><span class="sxs-lookup"><span data-stu-id="5a570-110">View current DWU settings</span></span>
<span data-ttu-id="5a570-111">Per visualizzare le impostazioni DWU correnti per i database:</span><span class="sxs-lookup"><span data-stu-id="5a570-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="5a570-112">Aprire Esplora oggetti di SQL Server in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a570-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="5a570-113">Connettersi al database master associato al server di database SQL logico.</span><span class="sxs-lookup"><span data-stu-id="5a570-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="5a570-114">Effettuare una selezione nella vista a gestione dinamica sys.database_service_objectives.</span><span class="sxs-lookup"><span data-stu-id="5a570-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="5a570-115">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="5a570-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="5a570-116">Ridimensionare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="5a570-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="5a570-117">Per modificare le DWU:</span><span class="sxs-lookup"><span data-stu-id="5a570-117">To change the DWUs:</span></span>

1. <span data-ttu-id="5a570-118">Connettersi al database master associato al server di database SQL logico.</span><span class="sxs-lookup"><span data-stu-id="5a570-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="5a570-119">Usare l'istruzione T-SQL [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="5a570-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="5a570-120">L'esempio seguente imposta l'obiettivo del livello di servizio su DW1000 per il database MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="5a570-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="5a570-121">Controllare lo stato del database e l'avanzamento dell'operazione</span><span class="sxs-lookup"><span data-stu-id="5a570-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="5a570-122">Connettersi al database master associato al server di database SQL logico.</span><span class="sxs-lookup"><span data-stu-id="5a570-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="5a570-123">Inviare query per controllare lo stato del database</span><span class="sxs-lookup"><span data-stu-id="5a570-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="5a570-124">Inviare query per controllare lo stato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="5a570-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="5a570-125">Questa DMV restituisce informazioni sulle varie operazioni di gestione in SQL Data Warehouse, ad esempio l'operazione e lo stato dell'operazione, che può essere IN_PROGRESS o COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="5a570-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="5a570-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a570-126">Next steps</span></span>
<span data-ttu-id="5a570-127">Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="5a570-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
