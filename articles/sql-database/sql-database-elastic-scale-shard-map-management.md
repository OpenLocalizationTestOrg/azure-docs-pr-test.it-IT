---
title: aaaScale un database SQL di Azure | Documenti Microsoft
description: Come toouse hello ShardMapManager, libreria client di database elastico
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Scalabilità orizzontale di database con gestore mappe partizioni di hello
scalabilità orizzontale tooeasily database in SQL Azure, utilizzare un gestore mappe partizioni. gestore mappe partizioni di Hello è un database speciale che gestisce le informazioni di mapping globale su tutte le partizioni (database) in un set di partizioni. Hello metadati consentono a un database dell'applicazione tooconnect toohello corretto in base al valore di hello di hello **chiave di partizionamento orizzontale**. Inoltre, ogni partizione nel set di hello contiene le mappe che tengono traccia dei dati di partizione locale hello (noto come **shardlet**). 

![Gestione mappe partizioni](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Informazioni sulle modalità di costruzione queste mappe è Gestione mappa tooshard essenziali. Questa operazione viene eseguita utilizzando hello [ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), trovato in hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md) toomanage partizione viene mappata.  

## <a name="shard-maps-and-shard-mappings"></a>Mappe partizioni e mapping di partizioni
Per ogni partizione, è necessario selezionare il tipo di hello di toocreate mappa partizioni. scelta di Hello dipende dall'architettura di database hello: 

1. Singolo tenant per database  
2. Più tenant per database (due tipi):
   1. Mapping di tipo elenco
   2. Mapping di tipo intervallo

Per un modello a singolo tenant, creare una mappa partizioni con **mapping di tipo elenco** . modello single-tenant Hello assegna a un database per ogni tenant. Si tratta di un modello efficace per gli sviluppatori SaaS in quanto semplifica la gestione.

![Mapping di tipo elenco][1]

modello multi-tenant Hello assegna diversi tenant tooa singolo database ed è possibile distribuire i gruppi di tenant tra più database. Utilizzare questo modello quando si prevede che necessita di dati di dimensioni ridotte di toohave ogni tenant. In questo modello viene assegnato un intervallo di tenant tooa database utilizzando **mapping intervallo**. 

![Mapping di tipo intervallo][2]

Oppure è possibile implementare un modello di database multi-tenant utilizzando un *mapping elenco* tooassign più singolo database tooa tenant. Ad esempio, DB1 viene utilizzato toostore informazioni sull'id tenant 1 e 5 e DB2 archivia i dati di 10 di tenant e tenant 7. 

![Tenant multipli su database singolo][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Tipi .NET supportati per le chiavi di partizionamento orizzontale
Hello di supporto scala elastica seguenti di .net Framework i tipi come chiavi di partizionamento orizzontale:

* numero intero
* long
* guid
* byte[]  
* datetime
* timespan
* datetimeoffset

### <a name="list-and-range-shard-maps"></a>Mappe partizioni di tipo elenco e intervallo
Le mappe partizioni possono essere create usando **elenchi di singoli valori di chiavi di partizionamento orizzontale** oppure tramite **intervalli di valori di chiavi di partizionamento orizzontale**. 

### <a name="list-shard-maps"></a>Mappe partizioni di tipo elenco
**Partizioni** contengono **shardlet** e mapping hello di shardlet tooshards è gestito da una mappa partizioni. Oggetto **mappa partizioni elenco** è un'associazione tra hello singoli valori di chiave che identificano gli shardlet hello e database hello che fungono da partizioni.  **Elenca i mapping** , esplicite e diversi valori di chiave possono essere mappato toohello dello stesso database. Ad esempio, viene eseguito il mapping A tooDatabase chiave 1 e B. Database fanno riferimento a valori di chiave, 3 e 6

| Chiave | Percorso della partizione |
| --- | --- |
| 1 |Database_A |
| 3 |Database_B |
| 4 |Database_C |
| 6 |Database_B |
| ... |... |

### <a name="range-shard-maps"></a>Mappa partizioni di tipo intervallo
In un **mappa partizioni intervallo**, intervalli di chiavi hello sono descritto da una coppia **[valore ridotto, valore massimo)** dove hello *valore ridotto* hello chiave minimo nell'intervallo hello e hello *Valore elevato* hello primo valore più elevato intervallo hello. 

Ad esempio, **[0, 100)** include tutti i numeri interi superiori o uguali a 0 e inferiori a 100. Si noti che sono supportati più intervalli può punto toohello stesso database e non contiguo di intervalli (ad esempio, [100,200) e [400,600) entrambi C punto tooDatabase nel seguente esempio hello.)

| Chiave | Percorso della partizione |
| --- | --- |
| [1, 50) |Database_A |
| [50, 100) |Database_B |
| [100, 200) |Database_C |
| [400, 600) |Database_C |
| ... |... |

Ognuna delle tabelle di hello illustrate sopra è riportato un esempio concettuale di un **ShardMap** oggetto. Ogni riga è un esempio semplificato dell'individuo **PointMapping** (per la mappa di partizioni elenco hello) o **RangeMapping** (per la mappa di partizioni intervallo hello) oggetto.

## <a name="shard-map-manager"></a>Gestore mappe partizioni
Nella libreria client hello, gestore mappe partizioni di hello è una raccolta di mappe partizioni. Hello dati gestiti da un **ShardMapManager** istanza viene mantenuta in tre posizioni: 

1. **Mappa di partizioni globali (GSM)**: specificare un tooserve database come repository hello per tutte le mappe partizioni e i mapping. Stored procedure e tabelle speciali vengono create automaticamente le informazioni di hello toomanage. Questo è in genere un database di piccole dimensioni e leggermente accessibili e non deve essere usato per altre esigenze di un'applicazione hello. salve le tabelle sono in uno schema speciale denominato **__ShardManagement**. 
2. **Mappa di partizioni locali (LSM)**: ogni database che si specifica una partizione è toobe modificato toocontain diverse tabelle di piccole dimensioni e stored procedure speciale che contengono e gestire partizioni di toothat specifiche informazioni mappa partizioni. Queste informazioni sono ridondanti con informazioni hello in GSM hello e consente le informazioni sulla mappa partizioni hello applicazione toovalidate memorizzati nella cache senza porre alcun carico sul hello GSM; un'applicazione Hello utilizza hello LSM toodetermine se un mapping memorizzati nella cache è ancora valido. Hello tabelle corrispondente toohello LSM in ogni partizione sono anche nello schema hello **__ShardManagement**.
3. **Cache dell'applicazione**: ogni istanza di applicazione che accede a un oggetto **ShardMapManager** gestisce una cache in memoria locale dei rispettivi mapping, in cui vengono archiviate le informazioni di routing appena recuperate. 

## <a name="constructing-a-shardmapmanager"></a>Creazione di un oggetto ShardMapManager
Un oggetto **ShardMapManager** viene creato con un modello [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) . Hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  accetta le credenziali (nome del server hello e nome del database contenente hello GSM inclusi) in formato hello un  **ConnectionString** e restituisce un'istanza di un **ShardMapManager**.  

**Nota:** hello **ShardMapManager** deve essere creata un'istanza solo una volta per ogni dominio applicazione, all'interno di codice di inizializzazione hello per un'applicazione. Creazione di istanze aggiuntive di ShardMapManager in hello stesso appdomain, comporterà un aumento della memoria e di utilizzo della CPU di un'applicazione hello. Un oggetto **ShardMapManager** può includere un numero qualsiasi di mappe partizioni. Anche se è possibile che una singola mappa partizioni sia sufficiente per molte applicazioni, in alcune situazioni vengono usati diversi set di database per schemi diversi o per finalità specifiche. In questi casi è preferibile usare più mappe partizioni. 

In questo codice, un'applicazione prova tooopen esistente **ShardMapManager** con hello [TryGetSqlShardMapManager metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Se gli oggetti che rappresentano un Global **ShardMapManager** (GSM) non sono ancora presenti all'interno del database di hello, libreria client hello vengono create sono utilizzando hello [CreateSqlShardMapManager metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

In alternativa, è possibile utilizzare Powershell toocreate un nuovo gestore mappe partizioni. Un esempio è disponibile [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Ottenere una mappa RangeShardMap o ListShardMap
Dopo aver creato una partizione gestore mappe, è possibile ottenere hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) utilizzando hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), o hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) metodo.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Credenziali di amministrazione delle mappe partizioni
Le applicazioni che amministrano e modificare mappe partizioni sono diverse da quelli che utilizzano connessioni di tooroute mappe partizioni hello. 

esegue il mapping di partizione tooadminister (aggiungere o modificare partizioni, mappe partizioni, i mapping delle partizioni, e così via) è necessario creare un'istanza di hello **ShardMapManager** utilizzando **le credenziali che dispongono di lettura/scrittura privilegi entrambi database GSM hello e in ogni database che funge da una partizione**. le credenziali di Hello devono consentire di scritture su tabelle di hello entrambi hello GSM e LSM come informazioni relative alla mappa partizioni è inseriti o modificati, nonché per la creazione di tabelle LSM in nuove partizioni.  

Vedere [utilizzate le credenziali della libreria client di Database elastico hello tooaccess](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Impatto solo sui metadati
Metodi usati per la compilazione o la modifica di hello **ShardMapManager** dati non si modificano i dati utente hello archiviati in partizioni hello autonomamente. Ad esempio, i metodi, ad esempio **CreateShard**, **DeleteShard**, **UpdateMapping**e così via interessano solo metadati di mappa partizioni hello. Non rimuovere, aggiungere o modificare i dati utente contenuti nelle partizioni hello. Questi metodi sono invece progettato toobe utilizzato in combinazione con operazioni separate eseguire toocreate o rimuovere un database effettivo, o che lo spostamento di righe da una partizione tooanother toorebalance un ambiente partizionato.  (hello **suddivisione unione** strumento incluso in strumenti di database elastico utilizza queste API con lo spostamento dei dati effettivi tra le partizioni di orchestrazione.) Vedere [scala utilizzando lo strumento di unione di Database elastico split hello](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Esempio di popolamento di una mappa partizioni
Di seguito è riportata una sequenza di operazioni toopopulate una mappa partizioni specifiche di esempio. codice Hello esegue queste operazioni: 

1. Creazione di una nuova mappa partizioni in un gestore delle mappe partizioni. 
2. mappa partizioni toohello vengono aggiunti metadati di Hello per due partizioni diverse. 
3. Un'ampia gamma di mapping di intervalli di chiavi vengono aggiunti e hello contenuto globale della mappa partizioni hello viene visualizzati. 

codice Hello viene scritto in modo che sia possibile eseguire nuovamente il metodo hello se si verifica un errore. Ogni richiesta di verifica se una partizione o mapping esiste già, prima di tentare di toocreate è. Hello codice si presuppone che i database **sample_shard_0**, **sample_shard_1** e **sample_shard_2** sono già stati creati nel server di hello stringaacuifariferimento**shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Come alternativa è possibile utilizzare PowerShell script hello tooachieve stesso risultato. Alcuni degli esempi di PowerShell di esempio hello sono disponibili [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

Una volta mappe partizioni sono state popolate, applicazioni di accesso ai dati possono essere create o adattato toowork con mappe hello. La compilazione o la modifica delle mappe di hello non devono necessariamente verificarsi finché **layout mappa** deve toochange.  

## <a name="data-dependent-routing"></a>Routing dipendente dei dati
gestore mappe partizioni di Hello più utilizzato in applicazioni che richiedono operazioni di database connessioni tooperform hello dati specifici dell'applicazione. Tali connessioni devono essere associate al database corretto hello. Questa procedura è nota come **routing dipendente dai dati**. Per queste applicazioni, creare un'istanza di un oggetto di gestione di partizioni della mappa da factory hello utilizzando le credenziali che dispongono dell'accesso di sola lettura sul database GSM hello. Le singole richieste per le connessioni successive forniscono le credenziali necessarie per la connessione di database di partizione appropriato toohello.

Si noti che queste applicazioni (utilizzando **ShardMapManager** aperta con le credenziali di sola lettura) non è possibile apportare modifiche toohello mappe o i mapping. A questo scopo è possibile creare applicazioni specifiche per l'amministrazione o script di PowerShell che forniscono credenziali con privilegi elevati, come illustrato in precedenza. Vedere [utilizzate le credenziali della libreria client di Database elastico hello tooaccess](sql-database-elastic-scale-manage-credentials.md).

Per informazioni dettagliate, vedere [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Modifica di una mappa partizioni
È possibile modificare una mappa partizioni in molti modi diversi. Tutti i seguenti metodi hello modificare hello metadati che descrivono le partizioni hello e i relativi mapping, ma fisicamente non modificano i dati all'interno di partizioni hello, né eseguire e creare o eliminare database effettivo hello.  Alcune delle operazioni di hello nella mappa partizioni hello descritto di seguito potrebbe essere necessario toobe coordinati azioni amministrative che spostare fisicamente i dati o di aggiungere e rimuovere i database che funge da partizioni.

Questi metodi funzionano insieme come blocchi predefiniti di hello disponibili per la modifica di hello distribuzione complessiva dei dati nell'ambiente di database partizionato.  

* tooadd o Rimuovi partizioni: utilizzare  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  e  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  di hello [Shardmap classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Hello server e database che rappresenta il partizionamento di destinazione hello deve esistere per tooexecute queste operazioni. Questi metodi non hanno alcun impatto su hello database, solo nei metadati nella mappa partizioni hello.
* toocreate o rimuovere punti o gli intervalli che sono mappati partizioni toohello: utilizzare  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  di hello [RangeShardMapping classe](https://msdn.microsoft.com/library/azure/dn807318.aspx), e  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  di hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Molti punti diversi o gli intervalli possono essere mappata toohello stesso partizione. Questi metodi influiscono solo sui metadati, non sui dati eventualmente già presenti nelle partizioni. Se è necessario toobe rimosso dal database di hello in ordine toobe coerente con dati **DeleteMapping** operazioni, sarà necessario tooperform queste operazioni separatamente, ma in combinazione con i metodi seguenti.  
* toosplit intervalli esistenti in due o unione intervalli adiacenti in un unico: utilizzare  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  e  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Si noti che suddividere e le operazioni di unione **non cambiano chiave toowhich di hello partizione vengono eseguito il mapping di valori**. Una divisione suddivide un intervallo esistente in due parti, ma non entrambi come toohello mappato stesso partizione. Un'operazione di unione opera su due intervalli adiacenti che sono già mappato toohello partizione stessa, li unione in un singolo intervallo.  spostamento dei punti o gli stessi intervalli tra le partizioni Hello deve toobe coordinate mediante l'utilizzo **UpdateMapping** in combinazione con lo spostamento dei dati effettivi.  È possibile utilizzare hello **suddivisione/unione** strumenti del servizio che fa parte di database elastico toocoordinate modifiche alla mappa di partizioni con lo spostamento dei dati, quando è necessario lo spostamento. 
* mappa toore (o spostamento) partizioni toodifferent singoli punti o intervalli: utilizzare  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Poiché i dati potrebbero essere spostato da una partizione tooanother in ordine toobe coerente con toobe **UpdateMapping** operazioni, sarà necessario tooperform tale spostamento separatamente, ma in combinazione con i metodi seguenti.
* mapping tootake online e offline: utilizzare  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  e  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello online dello stato di un mapping. 
  
    Alcune operazioni sui mapping di partizioni, incluse le operazioni **UpdateMapping** e **DeleteMapping**, sono consentite solo se lo stato del mapping è "offline". Quando un mapping è offline, una richiesta dipendente dai dati e basata su una chiave inclusa nel mapping restituirà un errore. Inoltre, quando un intervallo prima di tutto è offline, tutte le partizioni di toohello interessata le connessioni vengono terminate automaticamente nei risultati ordine tooprevent incomplete o per le query nei confronti di intervalli da modificare. 

I mapping sono oggetti non modificabili in .NET.  Tutti i metodi hello precedenti che modificare i mapping di invalidare anche qualsiasi toothem riferimenti nel codice. toomake it sequenze tooperform più semplice di operazioni che modificano lo stato del mapping, tutti i metodi di hello che modifica un mapping di restituiscono un nuovo mapping di riferimento, pertanto le operazioni possono essere concatenate. Ad esempio, toodelete un mapping in sm shardmap che contiene la chiave hello 25 esistente, è possibile eseguire hello seguenti: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Aggiunta di una partizione
Le applicazioni spesso necessario toosimply aggiungere nuovi dati toohandle partizioni che si prevedono di nuove chiavi o intervalli di chiavi per una mappa partizioni è già esistente. Ad esempio, un'applicazione partizionata in base l'ID Tenant potrebbe essere necessario tooprovision una nuova partizione per un nuovo tenant o mensile partizionati dati potrebbe essere una nuova partizione provisioning prima dell'inizio hello di ogni nuovo mese. 

Se il nuovo intervallo di hello dei valori di chiave non è già parte di un mapping esistente e non lo spostamento dei dati è necessario, è una nuova partizione di hello tooadd molto semplice e associare una nuova chiave hello o partizioni toothat intervallo. Per informazioni dettagliate sull'aggiunta di nuove partizioni, vedere [Aggiunta di una nuova partizione](sql-database-elastic-scale-add-a-shard.md).

Per gli scenari che richiedono lo spostamento dei dati, tuttavia, lo strumento di unione di menu combinato hello è lo spostamento dei dati di hello tooorchestrate necessarie tra le partizioni in combinazione con gli aggiornamenti delle mappe partizioni necessari hello. Per informazioni dettagliate sull'utilizzo hello yool unione di menu combinato, vedere [Panoramica di unione di menu combinato](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
