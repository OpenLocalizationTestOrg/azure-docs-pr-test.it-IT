---
title: aaaMigrate esistente database tooscale-out | Documenti Microsoft
description: Convertire gli strumenti di database elastico toouse database partizionati mediante la creazione di un gestore mappe partizioni
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Eseguire la migrazione di database esistente tooscale-out
Gestire facilmente i database partizionati esistenti di scalabilità orizzontale utilizzando gli strumenti di database di Database SQL di Azure (ad esempio hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md)). È prima necessario convertire un set esistente di hello toouse database [gestore mappe partizioni](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Panoramica
toomigrate un database partizionato esistente: 

1. Preparare hello [il database di gestione di partizioni mapping](sql-database-elastic-scale-shard-map-management.md).
2. Creare una mappa partizioni hello.
3. Preparare singole partizioni hello.  
4. Aggiungere una mappa partizioni toohello di mapping.

Queste tecniche possono essere implementate usando entrambi hello [libreria client .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), o gli script di PowerShell hello trovato in [database SQL di Azure - script di strumenti di Database elastico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). di seguito esempi di Hello utilizzano gli script di PowerShell hello.

Per ulteriori informazioni su hello ShardMapManager, vedere [gestione mappa partizioni](sql-database-elastic-scale-shard-map-management.md). Per una panoramica degli strumenti di database elastico hello, vedere [panoramica sulle funzionalità di Database elastico](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Preparare il database di gestione di hello partizioni mappa
gestore mappe partizioni di Hello è un database speciale che contiene i database di scalabilità orizzontale di hello dati toomanage. È possibile usare un database esistente o crearne un nuovo. Si noti che un database che funge da gestore mappe partizioni non deve essere hello stesso database come una partizione. Si noti inoltre che uno script di PowerShell hello non crea database hello automaticamente. 

## <a name="step-1-create-a-shard-map-manager"></a>Passaggio 1: Creare un gestore mappe partizioni
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>gestore mappe partizioni di hello tooretrieve
Dopo la creazione, è possibile recuperare gestore mappe partizioni di hello con questo cmdlet. Questo passaggio è necessario ogni volta che è necessario toouse hello ShardMapManager oggetto.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Passaggio 2: creare una mappa partizioni hello
È necessario selezionare il tipo di hello di toocreate mappa partizioni. scelta di Hello dipende dall'architettura di database hello: 

1. Single-tenant per ogni database (per i termini, vedere hello [glossario](sql-database-elastic-scale-glossary.md).) 
2. Più tenant per database (due tipi):
   1. Mapping di tipo elenco
   2. Mapping di tipo intervallo

Per un modello a singolo tenant, creare una mappa partizioni con **mapping di tipo elenco** . modello single-tenant Hello assegna a un database per ogni tenant. Si tratta di un modello efficace per gli sviluppatori SaaS in quanto semplifica la gestione.

![Mapping di tipo elenco][1]

modello multi-tenant Hello assegna diversi tenant tooa singolo database ed è possibile distribuire i gruppi di tenant tra più database. Utilizzare questo modello quando si prevede che necessita di dati di dimensioni ridotte di toohave ogni tenant. In questo modello viene assegnato un intervallo di tenant tooa database utilizzando **mapping intervallo**. 

![Mapping di tipo intervallo][2]

Oppure è possibile implementare un modello di database multi-tenant utilizzando un *mapping elenco* tooassign più singolo database tooa tenant. Ad esempio, DB1 viene utilizzato toostore informazioni sull'id tenant 1 e 5 e DB2 archivia i dati di 10 di tenant e tenant 7. 

![Tenant multipli su database singolo][3] 

**In base alla scelta effettuata, procedere con una delle opzioni seguenti:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Opzione 1: creare una mappa partizioni per un mapping di tipo elenco
Creare una mappa partizioni utilizzando hello ShardMapManager oggetto. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Opzione 2: creare una mappa partizioni per un mapping di tipo intervallo
Si noti che tooutilize questo schema di mapping, i valori di id tenant deve intervalli continui toobe e toohave accettabile gap negli intervalli hello è semplicemente ignorando intervallo hello quando si creano database hello.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Opzione 3: eseguire il mapping di tipo elenco in un database singolo
Per l'impostazione di questo modello è necessario anche creare una mappa di tipo elenco, come illustrato nel passaggio 2, opzione 1.

## <a name="step-3-prepare-individual-shards"></a>Passaggio 3: preparare le singole partizioni
Aggiungere ogni gestore mappe partizioni di partizioni (database) toohello. Questa funzione prepara i singoli database hello per archiviare le informazioni di mapping. Eseguire questo metodo su ogni partizione.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Passaggio 4: aggiungere mapping
aggiunta di Hello di mapping dipende dal tipo di hello di mappa partizioni che è stato creato. Se è stata creata una mappa di tipo elenco, aggiungere mapping di tipo elenco. Se è stata creata una mappa di tipo intervallo, aggiungere mapping di tipo intervallo.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Opzione 1: eseguire il mapping hello dati per il mapping di un elenco
Eseguire il mapping hello dati aggiungendo un mapping di elenco per ogni tenant.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Opzione 2: eseguire il mapping hello dati per il mapping di un intervallo
Aggiungere i mapping di intervallo hello per tutti i hello tenant intervallo per l'id, le associazioni di database:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Passaggio 4 opzione 3: eseguire il mapping hello dati a più tenant su un singolo database
Per ogni tenant, eseguire Add-ListMapping hello (opzione 1, sopra). 

## <a name="checking-hello-mappings"></a>Verifica mapping hello
Informazioni sulle partizioni esistenti hello e mapping hello associate possono eseguire una query utilizzando i seguenti comandi:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Riepilogo
Dopo aver completato l'installazione di hello, è possibile iniziare libreria client di Database elastico hello toouse. È anche possibile usare il [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) e le [query su più partizioni](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Passaggi successivi
Ottenere gli script di PowerShell hello da [Database elastica di database SQL di Azure strumenti sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

gli strumenti di Hello sono anche in GitHub: [/elastica-db-strumenti di Azure](https://github.com/Azure/elastic-db-tools).

Utilizzare hello dello strumento di merge di divisione toomove dati tooor da un modello di modello multi-tenant tooa single-tenant. Vedere la pagina relativa allo [strumento di divisione-unione](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Risorse aggiuntive
Per informazioni sugli schemi di architettura dati comuni delle applicazioni di database multi-tenant software come un servizio (SaaS), vedere [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Domande e richieste di funzionalità
Per domande, rivolgersi toous su hello [forum di Database SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e per le richieste di funzionalità, aggiungerli toohello [forum sul feedback su Database SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

