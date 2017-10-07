---
title: problemi di mapping aaaUsing toofix di gestione del ripristino di partizioni | Documenti Microsoft
description: Utilizzare hello RecoveryManager classe toosolve problemi mappe partizioni
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Utilizzando i problemi di mappa partizioni toofix classe RecoveryManager hello
Hello [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) fornisce applicazioni ADO.Net hello possibilità tooeasily rilevare e correggere eventuali incoerenze tra mappa di partizioni globale hello (GSM) e mappa di partizioni locali di hello (LSM) in un ambiente di database partizionato. 

Hello GSM e LSM traccia hello mapping di ogni database in un ambiente partizionato. In alcuni casi, si verifica un'interruzione tra hello GSM e hello LSM. In tal caso, utilizzare hello RecoveryManager classe toodetect e ripristinare interruzione hello.

Hello RecoveryManager classe fa parte di hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md). 

![Mappa partizioni][1]

Per le definizioni dei termini, vedere il [glossario degli strumenti del database elastico](sql-database-elastic-scale-glossary.md). hello come toounderstand **ShardMapManager** toomanage utilizzati dati in una soluzione partizionata, vedere [gestione mappa partizioni](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Perché utilizzare Gestione del ripristino di hello?
In un ambiente di database partizionato c'è un unico tenant per database e ci sono molti database per server. Può anche essere molti server nell'ambiente di hello. Ogni database viene eseguito il mapping nella mappa partizioni hello, pertanto possono essere chiamate di database e server corretto toohello indirizzato. I database vengono rilevati in base tooa **chiave di partizionamento orizzontale**, e ogni partizione viene assegnato un **intervallo di valori chiave**. Ad esempio, una chiave di partizionamento orizzontale può rappresentare i nomi dei clienti hello da "D" troppo "f" Hello mapping di tutte le partizioni (noto anche come database) e i relativi intervalli di mapping sono contenuti in hello **mappa partizioni globali (GSM)**. Ogni database contiene anche una mappa di intervalli di hello contenuti nella partizione hello noto come hello **mappa di partizioni locali (LSM)**. Quando un'applicazione si connette tooa partizioni, mapping hello viene memorizzato nella cache con hello app per il recupero rapido. Hello LSM è usato toovalidate memorizzati nella cache dei dati. 

Hello GSM e LSM potrebbe diventare non sincronizzata per hello seguenti motivi:

1. l'eliminazione di Hello di una partizione il cui intervallo sembrano toono più essere in uso o la ridenominazione di una partizione. Eliminazione dei risultati di una partizione in un **mapping di partizione orfana**. Analogamente, anche un database rinominato può causare un mapping di partizione orfana. A seconda della finalità hello Roc hello, partizioni hello potrebbe essere necessario toobe rimosso o percorso partizioni hello deve toobe aggiornato. toorecover un database eliminato, vedere [ripristinare un database eliminato](sql-database-recovery-using-backups.md).
2. Si verifica un evento di failover geografico. toocontinue, uno necessario aggiornare il nome di server hello e nome del database di gestore mappe partizioni in un'applicazione hello e quindi dettagli sul mapping di aggiornamento hello partizione per tutte le partizioni in una mappa partizioni. Se si verifica un failover geografico, tale logica di ripristino deve essere automatizzata all'interno del flusso di lavoro di hello failover. L'automazione delle azioni di ripristino rende possibile la gestibilità senza problemi dei database abilitati per la replica geografica, evitando interventi manuali. toolearn sulle opzioni toorecover un database, se si verifica un'interruzione del centro dati, vedere [la continuità aziendale](sql-database-business-continuity.md) e [il ripristino di emergenza](sql-database-disaster-recovery.md).
3. Database ShardMapManager hello o partizioni viene ripristinato tooan precedenti temporizzate. toolearn sul punto di recupero temporizzato tramite i backup, vedere [ripristino tramite backup](sql-database-recovery-using-backups.md).

Per ulteriori informazioni sugli strumenti di Database elastico del Database SQL di Azure, la replica geografica e ripristino, vedere l'esempio hello: 

* [Panoramica: Continuità aziendale del cloud e ripristino di emergenza del database con database SQL](sql-database-business-continuity.md) 
* [Iniziare a utilizzare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md)  
* [Gestione di mappe partizioni](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Ripristino di RecoveryManager da un oggetto ShardMapManager
primo passaggio Hello è un'istanza di RecoveryManager toocreate. Hello [GetRecoveryManager metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) restituisce hello recovery manager per hello corrente [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) istanza. eseguire il mapping di eventuali incoerenze nella partizione hello tooaddress, è innanzitutto necessario recuperare hello RecoveryManager per mappa di partizioni particolare hello. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

In questo esempio hello RecoveryManager viene inizializzato dai hello ShardMapManager. Hello ShardMapManager contenente un ShardMap anche già inizializzato. 

Poiché il codice dell'applicazione modifica mappa partizioni hello stesso, hello credenziali utilizzate nel metodo factory hello (nell'esempio sopra riportato, hello smmConnectionString) devono essere le credenziali che dispongono delle autorizzazioni di lettura e scrittura sul database GSM hello hello a cui fa riferimento stringa di connessione. Queste credenziali sono solitamente diverse da connessioni tooopen le credenziali utilizzate per il routing dipendente dai dati. Per ulteriori informazioni, vedere [utilizzando le credenziali nel client di database elastico hello](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Rimozione di una partizione da hello ShardMap dopo l'eliminazione di una partizione
Hello [DetachShard metodo](https://msdn.microsoft.com/library/azure/dn842083.aspx) Scollega hello dato partizione dalla mappa partizioni hello ed elimina i mapping associati hello partizione.  

* il parametro di percorso Hello è percorso partizioni hello, in particolare il nome di server e il nome database di partizione hello viene scollegato. 
* parametro shardMapName Hello è nome mappa partizioni di hello. Questo è solo necessario quando più mappe partizioni sono gestite da hello stesso gestore di mappe partizioni. Facoltativo. 


> [!IMPORTANT]
> Utilizzare questa tecnica solo se si è certi che l'intervallo di hello per il mapping di hello aggiornato è vuoto. dati per intervallo hello spostato non controllati da metodi Hello precedenti, è preferibile tooinclude verifica nel codice.
>

In questo esempio rimuove le partizioni dalla mappa partizioni hello. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

mappa partizioni Hello riflette posizione partizioni hello hello GSM prima dell'eliminazione di hello della partizione hello. Poiché è stato eliminato partizioni hello, si presuppone questo era intenzionale e intervalli di chiavi di partizionamento orizzontale hello non sono più in uso. Se non è questo il caso, è possibile eseguire un ripristino temporizzato. partizione di hello toorecover da un precedente punto nel tempo. (In questo caso, esaminare hello seguendo le incoerenze di partizioni toodetect sezione). toorecover, vedere [recupero temporizzato](sql-database-recovery-using-backups.md).

Poiché si presuppone l'eliminazione del database hello era intenzionale, hello Azione pulizia amministrativi finale è toodelete hello voce toohello partizione gestore mappe partizioni di hello. Questo impedisce l'applicazione hello intervallo tooa informazioni che non si prevede di scrivere inavvertitamente.

## <a name="toodetect-mapping-differences"></a>differenze di mapping toodetect
Hello [DetectMappingDifferences metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) Seleziona e restituisce una delle mappe di partizioni hello (locali o globali) come origine hello e riconcilia i mapping di entrambe le mappe partizioni (GSM e LSM).

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Hello *percorso* specifica il nome di server hello e il nome del database. 
* Hello *shardMapName* parametro è il nome della mappa partizioni hello. Questo è solo necessario se più mappe partizioni sono gestite da hello stesso gestore di mappe partizioni. Facoltativo. 

## <a name="tooresolve-mapping-differences"></a>differenze di mapping tooresolve
Hello [ResolveMappingDifferences metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) seleziona una delle mappe di partizioni hello (locali o globali) come origine hello e riconcilia i mapping di entrambe le mappe partizioni (GSM e LSM).

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Hello *RecoveryToken* parametro enumera hello differenze nei mapping hello hello GSM e hello LSM per partizioni specifiche di hello. 
* Hello [MappingDifferenceResolution enumerazione](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) metodo hello tooindicate utilizzato per risolvere hello differenza tra i mapping delle partizioni hello. 
* **MappingDifferenceResolution.KeepShardMapping** è consigliabile quando hello LSM contiene mapping accurato hello e pertanto mapping hello in partizioni hello devono essere utilizzate. Questo avviene in genere hello se si verifica un failover: partizioni hello si trovano ora in un nuovo server. Poiché la partizione hello deve essere rimossa prima dal hello GSM (RecoveryManager.DetachShard metodo hello), un mapping non esiste più sul hello GSM. Hello LSM deve pertanto essere utilizzato toore-stabilire il mapping di partizione hello.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Collegare un toohello partizioni ShardMap dopo il ripristino di una partizione
Hello [AttachShard metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) collega hello mappa partizioni toohello di partizioni specificato. Quindi, rileva eventuali incoerenze mappa partizioni e degli aggiornamenti delle partizioni di hello mapping toomatch hello al punto di ripristino di partizioni hello di hello. Si presuppone che il database hello anche tooreflect rinominato hello nome del database originale (prima partizione hello è stata ripristinata), poiché ripristino temporizzata di hello predefinite tooa nuovo database aggiunto con un timestamp hello. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Hello *percorso* parametro è il nome di server hello e nome del database, di partizioni hello da connettere. 
* Hello *shardMapName* parametro è il nome della mappa partizioni hello. Questo è solo necessario quando più mappe partizioni sono gestite da hello stesso gestore di mappe partizioni. Facoltativo. 

Questo esempio aggiunge una mappa partizioni toohello di partizioni che è stato recentemente ripristinata da un'ora di punto precedente. Poiché la partizione hello (vale a dire hello mapping per la partizione hello in hello LSM) è stata ripristinata, è potenzialmente non coerente con la voce di partizione hello in GSM hello. Di fuori di questo codice di esempio, partizioni hello è stato ripristinato e rinominato toohello nome originale del database hello. Dal momento che è stato ripristinato, si presuppone il mapping di hello in hello LSM mapping attendibile hello. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>L'aggiornamento dei percorsi partizioni dopo un failover geografico (ripristino) di partizioni hello
Se si verifica un failover geografico, database secondario hello verrà resi accessibili scrivere e diventa hello nuovo database primario. nome del server di hello e, potenzialmente, il database di hello (a seconda della configurazione) Hello, potrebbe essere diverso dalla replica primaria originale hello. Pertanto hello voci di mapping per la partizione hello in GSM hello e LSM devono essere corretti. Analogamente, se hello database è ripristinato tooa altro nome o percorso o tooan punto nel tempo precedente, ciò potrebbe causare incoerenze nelle mappe partizioni hello. Hello gestore mappe partizioni gestisce la distribuzione di hello di database corretto toohello di connessioni aperte. Distribuzione basata su dati hello nella mappa partizioni hello e il valore di hello della chiave di partizionamento orizzontale hello hello destinazione della richiesta di applicazioni hello. Dopo un failover geografico, è necessario aggiornare questo informazioni con il nome di server accurato hello, nome del database e il mapping delle partizioni del database ripristinato hello. 

## <a name="best-practices"></a>Procedure consigliate
Failover geo e il ripristino sono operazioni in genere gestiti da un amministratore del cloud di un'applicazione hello intenzionalmente utilizzando una delle funzionalità di continuità aziendale di database SQL di Azure. Pianificazione della continuità aziendale richiede i processi, procedure e misure tooensure che è possono continuare le operazioni aziendali senza interruzioni. Hello metodi disponibili come parte di hello RecoveryManager classe deve essere usato all'interno di questo hello tooensure del flusso di lavoro GSM e LSM vengono aggiornati in base a un'operazione di ripristino hello eseguita. Esistono cinque passaggi fondamentali tooproperly garantire hello GSM e LSM riflettono informazioni accurate di hello dopo un evento di failover. Hello tooexecute codice applicazione che questi passaggi possono essere integrati in flusso di lavoro e gli strumenti esistenti. 

1. Consente di recuperare hello RecoveryManager hello ShardMapManager. 
2. Scollegare partizione precedente di hello dalla mappa partizioni hello.
3. Collegare hello nuova partizione toohello mappa partizioni, compresa l'ubicazione di hello nuova partizione.
4. Il mapping tra hello GSM e LSM hello vengono rilevate incoerenze. 
5. Risolvere le differenze tra hello GSM e hello LSM, hello trusting LSM. 

In questo esempio esegue hello alla procedura seguente:

1. Rimuove le partizioni da hello mappa partizioni che riflettono i percorsi di partizione prima dell'evento di failover hello.
2. Collega partizioni toohello mappa partizioni riflettente hello nuove partizioni posizioni (parametro hello "Configuration.SecondaryServer" è nuovo nome del server hello ma hello stesso nome del database).
3. Recupera il token di ripristino hello rilevando le differenze di mapping tra hello GSM e hello LSM per ogni partizione. 
4. Risolve le incoerenze hello mappando hello trusting da hello LSM di ogni partizione. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

