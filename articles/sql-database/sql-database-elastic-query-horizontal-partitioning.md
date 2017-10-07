---
title: "aaaReporting tra i database di scalabilità orizzontale cloud | Documenti Microsoft"
description: come tooset elastico query su partizioni orizzontali
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Creazione di report tra database cloud con scalabilità orizzontale (anteprima)
![Eseguire una query tra partizioni][1]

I database partizionati distribuiscono righe su un livello di dati a scalabilità orizzontale. schema di Hello è identico in tutti i database partecipanti, noti anche come partizionamento orizzontale. Con una query elastica è possibile creare report che si estendono a tutti i database di un database partizionato.

Per l'avvio rapido, vedere [Creazione di report tra database cloud con scalabilità orizzontale](sql-database-elastic-query-getting-started.md).

Per i database non partizionati, vedere [Eseguire query in database cloud con schemi diversi](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Prerequisiti
* Creare una mappa partizioni utilizzando hello libreria client di database elastico. Vedere [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md). Oppure usare app di esempio hello in [Introduzione agli strumenti di database elastico](sql-database-elastic-scale-get-started.md).
* In alternativa, vedere [esistenti di eseguire la migrazione di database database tooscaled-out](sql-database-elastic-convert-to-use-elastic-tools.md).
* utente Hello deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE. Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello.
* Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.

## <a name="overview"></a>Panoramica
Queste istruzioni creano rappresentazione dei metadati hello del livello dati partizionati nel database di query elastico hello. 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 Creare la chiave master e le credenziali con ambito database
Hello credenziali vengono utilizzate dal database remoti tooyour tooconnect query elastico hello.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Verificare che tale hello *"\<username\>"* non include alcun *"@servername"* suffisso. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 Creare origini dati esterne
Sintassi:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Esempio
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Recuperare l'elenco di hello delle origini dati esterne corrente: 

    select * from sys.external_data_sources; 

origine dati esterna Hello fa riferimento la mappa partizioni. Una query elastica utilizza quindi origine dati esterna hello e hello partizioni tooenumerate hello database delle mappe che fanno parte di livello dati hello sottostante. stesse credenziali Hello sono mappa di partizioni utilizzate tooread hello e tooaccess hello dati su partizioni hello durante l'elaborazione di hello di una query elastica. 

## <a name="13-create-external-tables"></a>1.3 Creare tabelle esterne
Sintassi:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Esempio**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Recuperare l'elenco di hello delle tabelle esterne del database corrente hello: 

    SELECT * from sys.external_tables; 

tabelle esterne toodrop:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Osservazioni
Hello dati\_clausola origine definisce l'origine dati esterna hello (una mappa partizioni) che viene utilizzato per la tabella esterna hello.  

Hello SCHEMA\_nome e l'oggetto\_clausole nome mappa hello esterno definizione tooa tabella in uno schema diverso. Se omesso, schema hello dell'oggetto remoto hello si presuppone che toobe "dbo" e il nome è nome della tabella esterna identici toohello toobe da definire. Ciò è utile se hello nome della tabella remota è già in uso nel database di hello in cui si desidera toocreate tabella esterna di hello. Ad esempio, si desidera toodefine un tooget tabella esterna, una vista aggregata di viste del catalogo o del livello DMV sui dati di scalabilità. Poiché le viste del catalogo e DMV già esiste in locale, è possibile utilizzare i nomi per la definizione di tabella esterna hello. In alternativa, utilizzare un nome diverso e utilizzare della vista del catalogo hello o hello Nome DMV in hello SCHEMA\_nome e/o oggetto\_clausole di nome. (Vedere l'esempio hello riportato di seguito). 

clausola distribuzione Hello specifica distribuzione dei dati hello utilizzata per questa tabella. query processor di Hello utilizza informazioni hello disponibili in hello distribuzione clausola toobuild hello più efficace i piani di query.  

1. **PARTIZIONATO** significa dati partizionati orizzontalmente tra database hello. chiave di partizionamento per la distribuzione dei dati hello è hello Hello **< sharding_column_name >** parametro.
2. **REPLICATI** significa che copie identiche di tabella hello siano presenti in ogni database. È il tooensure responsabilità che le repliche hello siano identiche tra database hello.
3. **ARROTONDAMENTO\_ROBIN** significa che la tabella hello è partizionata orizzontalmente utilizzando un metodo di distribuzione dipendenti dall'applicazione. 

**Riferimento di livello dati**: tabella esterna hello DDL fa riferimento l'origine dati esterna tooan. origine dati esterna Hello specifica una mappa partizioni che fornisce la tabella esterna hello con hello informazioni necessarie toolocate tutti i database di hello nel livello dati. 

### <a name="security-considerations"></a>Considerazioni relative alla sicurezza
Gli utenti con una tabella esterna toohello di accesso accedere automaticamente toohello tabelle remote sottostanti in credenziali hello specificata nella definizione dell'origine dati esterna hello. Evitare indesiderati l'elevazione dei privilegi tramite credenziali hello dell'origine dati esterna hello. Usare GRANT o REVOKE per la tabella esterna, come se fosse una tabella comune.  

Dopo aver definito l'origine dati esterna e le tabelle esterne, è ora possibile usare la sintassi T-SQL completa sulle tabelle esterne.

## <a name="example-querying-horizontal-partitioned-databases"></a>Esempio: esecuzione di query su database partizionati orizzontalmente
Hello nella query seguente esegue un join a tre vie tra magazzini, ordini e le righe dell'ordine e utilizza più funzioni di aggregazione e un filtro selettivo. Si presuppone (1) partizionamento (partizionamento orizzontale) e (2) che data warehouse, ordini e le righe di ordine sono partizionate dalla colonna di id warehouse hello e query elastico hello può condividere il percorso dei join hello su partizioni hello ed elaborare hello costosa parte query hello su hello partizioni in parallelo. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Stored procedure per l'esecuzione remota di T-SQL: sp\_execute_remote
Query elastico introduce inoltre una stored procedure che fornisce accesso diretto toohello partizioni. Hello stored procedure viene chiamata [sp\_eseguire \_remoto](https://msdn.microsoft.com/library/mt703714) e può essere utilizzato tooexecute stored procedure remote o il codice T-SQL nel database remoto hello. Avrà hello seguenti parametri: 

* Nome dell'origine dati (nvarchar): nome hello dell'origine dati esterna hello di tipo RDBMS. 
* Query (nvarchar): toobe query hello T-SQL eseguito su ogni partizione. 
* Dichiarazione di parametro (nvarchar) - facoltativa: stringa con definizioni dei tipi di dati per i parametri di hello utilizzati nel parametro di Query hello (ad esempio sp_executesql). 
* Elenco di valori dei parametri (facoltativo): elenco delimitato da virgole di valori dei parametri, ad esempio sp_executesql.

sp Hello\_eseguire\_remoto utilizza hello origine dati esterna cui hello chiamata parametri tooexecute hello dato istruzione T-SQL nel database remoto hello. Usa credenziali hello del database di gestione di hello dati esterni origine tooconnect toohello shardmap e database remoti hello.  

Esempio: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Connettività per gli strumenti
Regolare tooconnect di stringhe di connessione SQL Server utilizzare l'applicazione, BI e dati integrazione strumenti toohello database con le definizioni di tabella esterna. Assicurarsi che SQL Server sia supportato come origine dati per lo strumento. Fare riferimento a database elastico query hello come qualsiasi altro strumento di toohello database connessi a SQL Server e usare tabelle esterne da strumento o l'applicazione come se fossero tabelle locali. 

## <a name="best-practices"></a>Procedure consigliate
* Assicurarsi di che database elastico query endpoint hello ha toohello shardmap database e tutte le partizioni tramite hello che firewall di database di SQL Server.  
* Convalidare o applicare la distribuzione dei dati hello definita tabella esterna hello. Se la distribuzione di dati effettivo è diversa dalla distribuzione hello specificata nella definizione di tabella, le query possono restituire risultati imprevisti. 
* Query elastico attualmente non esegue l'eliminazione di partizioni quando predicati sulla chiave di partizionamento orizzontale hello consentirne toosafely escludere determinate partizioni dall'elaborazione.
* Query elastico è ideale per le query in cui la maggior parte del calcolo hello può essere eseguita su partizioni hello. In genere si ottiene hello migliori prestazioni di query con predicati del filtro selettivo che può essere valutata in partizioni hello o join su hello chiavi che possono essere eseguite in modo allineate alle partizioni in tutte le partizioni di partizionamento. Altri modelli di query, potrebbe essere necessario grandi quantità di tooload dei dati dal nodo head di hello partizioni toohello e potrebbero essere scarse

## <a name="next-steps"></a>Passaggi successivi

* Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).
* Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).
* Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)
* Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).
* Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
