---
title: "aaaPause, riprendere, la scalabilità orizzontale con REST in Azure SQL Data Warehouse | Documenti Microsoft"
description: Gestire la potenza di calcolo in SQL Data Warehouse con REST, T-SQL e PowerShell.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a>Gestire la potenza di calcolo in Azure SQL Data Warehouse (REST)
> [!div class="op_single_selector"]
> * [Panoramica](sql-data-warehouse-manage-compute-overview.md)
> * [Portale](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Ridimensionare la potenza di calcolo
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

hello toochange Dwu, utilizzare hello [crea o aggiorna Database] [ Create or Update Database] API REST. Hello esempio imposta hello servizio livello obiettivo tooDW1000 per database hello MySQLDW che è ospitato nel server MyServer. server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure.

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Sospendere le risorse di calcolo
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause un database, utilizzare hello [Database pausa] [ Pause Database] API REST. Hello esempio seguente viene sospeso un database denominato Database02 ospitato in un server denominato Server01. server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure.

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Riavviare le risorse di calcolo
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart un database, utilizzare hello [Database Resume] [ Resume Database] API REST. Hello esempio seguente viene avviato un database denominato Database02 ospitato in un server denominato Server01. server Hello è denominato ResourceGroup1 in un gruppo di risorse di Azure. 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a>Controllare lo stato del database

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Passaggi successivi
Per altre attività di gestione, vedere [Panoramica della gestione][Management overview].

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
