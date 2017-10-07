---
title: aaaPerformance i contatori per il gestore mappe partizioni
description: La classe ShardMapManager e i contatori delle prestazioni con routing dipendente dai dati
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Contatori delle prestazioni per Gestore mappe partizioni
È possibile acquisire le prestazioni di hello di un [gestore mappe partizioni](sql-database-elastic-scale-shard-map-management.md), soprattutto quando si utilizza [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md). I contatori vengono creati con i metodi della classe Microsoft.Azure.SqlDatabase.ElasticScale.Client hello.  

I contatori sono utilizzati tootrack hello prestazioni di [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) operazioni. Questi contatori sono accessibili in hello Performance Monitor, nella categoria "Gestione di partizioni: Database elastico" hello.

**Per la versione più recente di hello:** andare troppo[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Vedere anche [aggiornare un'app toouse hello più recente database elastico libreria client](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Prerequisiti
* categoria di prestazioni toocreate hello e contatori, hello utente deve far parte di hello locale **amministratori** gruppo computer hello che ospita un'applicazione hello.  
* toocreate delle prestazioni istanza di contatore e aggiornare i contatori di hello, hello utente deve essere un membro di entrambi hello **amministratori** o **Performance Monitor Users** gruppo. 

## <a name="create-performance-category-and-counters"></a>Creare una categoria e contatori delle prestazioni
contatori di hello toocreate, chiamare il metodo CreatePeformanceCategoryAndCounters hello di hello [ShardMapManagmentFactory classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Solo un amministratore può eseguire il metodo di hello: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

È inoltre possibile utilizzare [questo](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) metodo hello tooexecute script di PowerShell. metodo Hello crea hello i contatori delle prestazioni seguenti:  

* **Memorizzato nella cache i mapping**: numero di mapping memorizzati nella cache per la mappa partizioni hello.
* **DDR operazioni/sec**: frequenza delle operazioni di routing dipendente dati per la mappa partizioni hello. Questo contatore viene aggiornato quando una chiamata troppo[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) risultati in una partizione di destinazione toohello connessione ha esito positivo. 
* **Mapping di riscontri nella cache di ricerca/sec**: frequenza delle operazioni di ricerca ha esito positivo della cache per i mapping nella mappa partizioni hello. 
* **Mapping di mancati riscontri nella cache di ricerca al secondo**: frequenza delle operazioni di ricerca della cache non riuscito per i mapping nella mappa partizioni hello.
* **Mapping di aggiunte o aggiornate in cache/sec**: frequenza il mapping vengono aggiunti o aggiornati nella cache per mappa partizioni hello. 
* **Mapping rimossi dalla cache/sec**: frequenza con cui i mapping vengono rimossi dalla cache per la mappa partizioni hello. 

Vengono creati contatori delle prestazioni per ciascuna mappa partizioni memorizzata nella cache in modalità per processo.  

## <a name="notes"></a>Note
Hello eventi seguenti attivano la creazione di hello hello dei contatori delle prestazioni:  

* Inizializzazione di hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) con [caricamento eager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx)se hello ShardMapManager contiene le mappe partizioni. Questi includono hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) hello e [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) metodi.
* Ricerca con esito positivo di una mappa partizioni (mediante [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) o [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Creazione di una mappa partizioni mediante CreateShardMap().

i contatori delle prestazioni di Hello verranno aggiornati da tutte le operazioni eseguite su mapping e mappa partizioni hello cache. Completata la rimozione della mappa partizioni hello utilizzando DeleteShardMap () reults l'eliminazione di istanze di contatori delle prestazioni di hello.  

## <a name="best-practices"></a>Procedure consigliate
* Creazione di una categoria di prestazioni hello e contatori deve essere eseguita solo una volta prima della creazione di hello dell'oggetto ShardMapManager. Ogni esecuzione del comando hello CreatePerformanceCategoryAndCounters() Cancella i contatori precedenti hello (perdita di dati restituiti da tutte le istanze) e crea nuovi.  
* Le istanze dei contatori delle prestazioni vengono create in modalità per processo. Un arresto anomalo dell'applicazione o la rimozione di una mappa partizioni dalla cache di hello comporterà l'eliminazione di istanze dei contatori delle prestazioni hello.  

### <a name="see-also"></a>Vedere anche
[Panoramica sulle funzionalità di database elastico](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

