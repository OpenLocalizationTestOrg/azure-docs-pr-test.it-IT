---
title: aaaRestore un Azure data warehouse - locale e con ridondanza geografica | Documenti Microsoft
description: Panoramica delle opzioni di ripristino di database di hello per il ripristino di un database in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a>Ripristino di SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Panoramica][Overview]
> * [Portale][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

SQL Data Warehouse offre ripristini locali e geografici come parte delle sue funzionalità di ripristino di emergenza del data warehouse. Utilizzare dati warehouse backup toorestore il ripristino di data warehouse tooa punto nell'area primaria hello oppure utilizzare l'area geografica diversa tooa backup con ridondanza geografica toorestore. Questo articolo illustra le specifiche di hello del ripristino di un data warehouse.

## <a name="what-is-a-data-warehouse-restore"></a>Cos'è un ripristino del data warehouse?
Un ripristino del data warehouse consiste in un nuovo data warehouse creato da un backup di un data warehouse esistente o eliminato. warehouse di dati ripristinati Hello ricrea warehouse dati di backup hello in un momento specifico. Poiché SQL Data Warehouse è un sistema distribuito, il ripristino del data warehouse viene creato da molti file di backup archiviati nei blob di Azure. 

Il ripristino del database è un elemento essenziale di qualsiasi strategia di continuità aziendale e di ripristino di emergenza perché ricrea i dati dopo un caso di danneggiamento o eliminazione accidentale.

Per altre informazioni, vedere:

* [Backup di SQL Data Warehouse](sql-data-warehouse-backups.md)
* [Panoramica sulla continuità aziendale](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a>Punti di ripristino del data warehouse
Il vantaggio dell'utilizzo di archiviazione Premium di Azure SQL Data Warehouse utilizza il Blob di archiviazione di Azure degli snapshot toobackup hello primario del data warehouse. Ogni snapshot è un punto di ripristino che rappresenta il tempo di hello snapshot hello avviato. toorestore un data warehouse, scegliere un punto di ripristino e inviare un comando di ripristino.  

SQL Data Warehouse viene sempre ripristinato hello tooa backup nuovo data warehouse. È possibile mantenere hello ripristinato del data warehouse e hello corrente o eliminare uno di essi. Se si desidera tooreplace hello corrente del data warehouse con hello ripristino del data warehouse, è possibile rinominarlo.

Se è necessario toorestore eliminate o in pausa data warehouse, è possibile [creare un ticket di supporto](sql-data-warehouse-get-started-create-support-ticket.md). 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a>Ripristino con ridondanza geografica
È possibile ripristinare l'area tooany warehouse di dati che supporta Azure SQL Data Warehouse con il livello di prestazioni scelto. Si noti che DWU 9000 e 18000 non sono supportate in tutte le aree durante l'anteprima di hello.

> [!NOTE]
> ripristino di un con ridondanza geografica tooperform che è necessario non stata esplicitamente questa funzionalità.
> 
> 

## <a name="restore-timeline"></a>Sequenza temporale del ripristino
È possibile ripristinare un punto di ripristino disponibile tooany di database all'interno di hello negli ultimi sette giorni. Gli snapshot avviare ogni quattro ore tooeight e sono disponibili sette giorni. Quando uno snapshot supera i sette giorni di vita, scade e il relativo punto di ripristino non è più disponibile.

## <a name="restore-costs"></a>Costi di ripristino
costi di archiviazione Hello per hello ripristinato data warehouse viene fatturato alla tariffa di archiviazione di Azure Premium hello. 

Se si sospende un ripristinato data warehouse, viene addebitata per l'archiviazione con frequenza di archiviazione di Azure Premium hello. Il vantaggio di Hello della sospensione è che non vengono addebitate le risorse di elaborazione DWU hello.

Per altre informazioni sui prezzi di SQL Data Warehouse, vedere [Prezzi di SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).

## <a name="uses-for-restore"></a>Usi della funzionalità di ripristino
uso principale Hello ripristino dei dati del warehouse è toorecover dati dopo la perdita di dati accidentali.

Inoltre, è possibile utilizzare dati warehouse ripristino tooretain una copia di backup per più di sette giorni. Una volta ripristinato il backup di hello, in base a cui si dispone di data warehouse di hello online e possibile sospenderla indefinitamente toosave calcolo dei costi. database sospeso Hello comporta costi di archiviazione con frequenza di archiviazione di Azure Premium hello. 

## <a name="related-topics"></a>Argomenti correlati
### <a name="scenarios"></a>Scenari
* Per una panoramica sulla continuità aziendale, vedere [Panoramica sulla continuità aziendale](../sql-database/sql-database-business-continuity.md)

<!-- ### Tasks -->

tooperform un data warehouse di ripristino, eseguire il ripristino utilizzando:

* Azure portale, vedere [ripristino configurazione di un data warehouse utilizzando hello portale di Azure](sql-data-warehouse-restore-database-portal.md)
* Cmdlet di PowerShell )vedere [Ripristinare un data warehouse con i cmdlet di PowerShell](sql-data-warehouse-restore-database-powershell.md))
* API REST, vedere [ripristino configurazione di un data warehouse utilizzando le API REST hello](sql-data-warehouse-restore-database-rest-api.md)

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
