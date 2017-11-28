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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="8bfba-104">Gestire la potenza di calcolo in Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="8bfba-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bfba-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8bfba-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="8bfba-106">Portale</span><span class="sxs-lookup"><span data-stu-id="8bfba-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="8bfba-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bfba-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="8bfba-108">REST</span><span class="sxs-lookup"><span data-stu-id="8bfba-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="8bfba-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="8bfba-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="8bfba-110">Visualizzare le impostazioni DWU correnti</span><span class="sxs-lookup"><span data-stu-id="8bfba-110">View current DWU settings</span></span>
<span data-ttu-id="8bfba-111">tooview hello DWU impostazioni correnti per i database:</span><span class="sxs-lookup"><span data-stu-id="8bfba-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="8bfba-112">Aprire Esplora oggetti di SQL Server in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8bfba-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="8bfba-113">La connessione a database master di toohello associato hello logico del Database di SQL server.</span><span class="sxs-lookup"><span data-stu-id="8bfba-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="8bfba-114">Selezionare dalla vista a gestione dinamica sys.database_service_objectives hello.</span><span class="sxs-lookup"><span data-stu-id="8bfba-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="8bfba-115">Di seguito è fornito un esempio:</span><span class="sxs-lookup"><span data-stu-id="8bfba-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="8bfba-116">Ridimensionare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="8bfba-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="8bfba-117">hello toochange Dwu:</span><span class="sxs-lookup"><span data-stu-id="8bfba-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="8bfba-118">Connettersi a database master di toohello associato con il server logico di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="8bfba-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="8bfba-119">Hello utilizzare [ALTER DATABASE] [ ALTER DATABASE] istruzione TSQL.</span><span class="sxs-lookup"><span data-stu-id="8bfba-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="8bfba-120">Hello esempio imposta hello servizio livello obiettivo tooDW1000 per database hello MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="8bfba-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="8bfba-121">Controllare lo stato del database e l'avanzamento dell'operazione</span><span class="sxs-lookup"><span data-stu-id="8bfba-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="8bfba-122">Connettersi a database master di toohello associato con il server logico di Database SQL.</span><span class="sxs-lookup"><span data-stu-id="8bfba-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="8bfba-123">Inviare lo stato di database toocheck query</span><span class="sxs-lookup"><span data-stu-id="8bfba-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="8bfba-124">Inviare query toocheck sullo stato dell'operazione</span><span class="sxs-lookup"><span data-stu-id="8bfba-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="8bfba-125">Questa DMV restituisce informazioni sulle varie operazioni di gestione nel proprio SQL Data Warehouse, ad esempio lo stato di operazione e hello hello dell'operazione di hello, che sarà IN_PROGRESS o completato.</span><span class="sxs-lookup"><span data-stu-id="8bfba-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="8bfba-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8bfba-126">Next steps</span></span>
<span data-ttu-id="8bfba-127">Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="8bfba-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
