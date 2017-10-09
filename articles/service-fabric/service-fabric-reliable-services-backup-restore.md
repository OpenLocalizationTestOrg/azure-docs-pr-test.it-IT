---
title: aaaService infrastruttura Backup e ripristino | Documenti Microsoft
description: Documentazione concettuale per il backup e ripristino di Service Fabric
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Eseguire il backup e il ripristino di Reliable Services e Reliable Actors
Azure Service Fabric è una piattaforma a disponibilità elevata che replica stato hello in più nodi toomaintain la disponibilità elevata.  Di conseguenza, anche se un nodo cluster hello non riesce, servizi hello continuano toobe disponibili. Sebbene questa ridondanza integrata fornita dalla piattaforma hello potrebbe essere sufficiente per alcuni, in alcuni casi è consigliabile che hello servizio tooback dei dati (archivio esterno tooan).

> [!NOTE]
> È toobackup critici e il ripristino dei dati (e i test che funziona come previsto) in modo è possibile ripristinare da scenari di perdita dei dati.
> 
> 

Ad esempio, un servizio necessario tooback dei dati in ordine tooprotect da hello seguenti scenari:

- Nell'evento hello di perdita definitiva di hello di un intero cluster di Service Fabric.
- Perdita definitiva di una maggioranza delle repliche hello di una partizione di servizio
- Errori amministrativi, in base al quale hello stato accidentalmente Ottiene eliminato o danneggiato. Questo problema può verificarsi, ad esempio, se un amministratore con privilegi sufficienti elimina erroneamente servizio hello.
- Bug nel servizio hello che provocano il danneggiamento dei dati. Ad esempio, ciò può verificarsi quando un aggiornamento del codice del servizio inizia la scrittura di dati difettoso tooa insieme affidabile. In tal caso, entrambi hello codice e dati di hello possono avere toobe ripristinato tooan stato in precedenza.
- Elaborazione dati offline. Potrebbe essere toohave pratico l'elaborazione offline dei dati per la business intelligence che si verifica separatamente dal servizio hello che genera dati hello.

funzionalità di Backup/ripristino Hello consente servizi basati su backup toocreate e il ripristino di API per servizi affidabili hello. Hello API backup fornite dalla piattaforma hello consentono il/i backup dello stato di una partizione servizio, senza blocco lettura o di operazioni di scrittura. ripristino di Hello API consente toobe di una partizione servizio stato ripristinato da un backup scelto.

## <a name="types-of-backup"></a>Tipi di backup
Sono disponibili due opzioni di backup: completo e incrementale.
Un backup completo è una copia di backup che contiene tutti hello dati necessari toorecreate hello lo stato della replica hello: Checkpoint e tutti i record di log.
Poiché dispone di checkpoint hello e log di hello, un backup completo può essere ripristinato da solo.

Quando i checkpoint hello sono di grandi dimensioni, si verifica il problema di Hello con backup completi.
Ad esempio, una replica che dispone di 16 GB di stato i checkpoint saranno che costituiscono circa too16 GB.
Se si dispone di un obiettivo del punto di ripristino di cinque minuti, hello replica sono necessari toobe backup ogni cinque minuti.
Ogni volta che viene eseguito il backup deve toocopy 16 GB di checkpoint inoltre too50 MB (configurabile utilizzando `CheckpointThresholdInMB`) relativi registri.

![Esempio di backup completo.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

problema di toothis soluzione hello è backup incrementali, in cui backup contiene solo i record del log hello modificato dall'ultimo backup hello.

![Esempio di backup incrementale.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Poiché i backup incrementali sono solo le modifiche apportate dall'ultimo backup hello (non include i checkpoint hello), toobe sono in genere più veloce, ma non possono essere ripristinati in modo autonomo.
toorestore un backup incrementale, hello intera catena di backup è obbligatorio.
Una catena di backup inizia con un backup completo e prosegue con diversi backup incrementali contigui.

## <a name="backup-reliable-services"></a>Eseguire il backup di Reliable Services
Hello autore servizio abbia il pieno controllo sul momento in backup toomake e in cui verranno archiviati i backup.

toostart una copia di backup, il servizio di hello deve tooinvoke hello ereditata membro funzione `BackupAsync`.  
I backup possono essere composto solo da repliche primarie e richiedono toobe di scrittura stato concesso.

Come illustrato di seguito, `BackupAsync` accetta un `BackupDescription` oggetto, uno in cui è possibile specificare un backup completo o incrementale, nonché una funzione di callback, `Func<< BackupInfo, CancellationToken, Task<bool>>>` che è richiamato quando la cartella di backup hello è stato creato in locale ed è pronto toobe spostati toosome archiviazione esterna.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Richiesta tootake un backup incrementale può non riuscire con `FabricMissingFullBackupException`. Questa eccezione indica che uno dei seguenti aspetti hello è in corso:

- replica Hello non è mai eseguito un backup completo, poiché è stato contrassegnato come primario,
- alcune delle hello i record di log dall'ultimo backup hello è stato troncato o
- replica passato hello `MaxAccumulatedBackupLogSizeInMB` limite.

Gli utenti possono aumentare la probabilità hello di essere in grado di toodo i backup incrementali configurando `MinLogSizeInMB` o `TruncationThresholdFactor`.
Si noti che l'aumento di questi valori aumenta hello in base all'utilizzo del disco di replica.
Per altre informazioni, vedere [Configurazione di Reliable Services](service-fabric-reliable-services-configuration.md)

`BackupInfo`vengono fornite informazioni sui backup di hello, incluso il percorso di hello hello cartella in cui il runtime hello backup hello (`BackupInfo.Directory`). funzione di callback Hello è possibile spostare hello `BackupInfo.Directory` tooan archivio esterno o in un'altra posizione.  Questa funzione restituisce anche valore booleano che indica se è il percorso di destinazione tooits toosuccessfully in grado di spostare hello cartella di backup.

Hello codice seguente viene illustrato come hello `BackupCallbackAsync` metodo può essere utilizzato tooupload hello backup tooAzure archiviazione:

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

Nell'esempio precedente hello `ExternalBackupStore` è una classe di esempio hello toointerface utilizzato con l'archiviazione Blob di Azure, e `UploadBackupFolderAsync` metodo hello che comprime cartella hello e lo inserisce nell'archivio Blob di Azure hello.

Si noti che:

  - In un dato momento può essere in corso una sola operazione di backup per replica. Più `BackupAsync` chiamata alla volta genererà `FabricBackupInProgressException` toolimit in-Flight backup tooone.
  - Se una replica viene eseguito il failover mentre è in corso un backup, backup hello non sia stato completato. Pertanto, al termine del failover hello, si tratta responsabilità toorestart hello backup del servizio hello richiamando `BackupAsync` in base alle esigenze.

## <a name="restore-reliable-services"></a>Ripristinare Reliable Services
In generale, hello casi potrebbe essere necessario tooperform un'operazione di ripristino rientrano in una di queste categorie:

  - servizio Hello partizionare i dati persi. Ad esempio, disco hello per due dei tre repliche per una partizione (inclusa la replica primaria di hello) Ottiene danneggiato o cancellato. nuovo database primario di Hello potrebbe essere necessario toorestore dati da un backup.
  - intero servizio Hello viene persa. Ad esempio, un amministratore rimuove intero servizio hello e devono toobe ripristinato hello servizio e dati di hello.
  - servizio Hello replicati i dati di applicazione danneggiata (ad esempio, a causa di un bug dell'applicazione). In questo caso, il servizio di hello ha toobe aggiornato o ripristinato tooremove hello causa del danneggiamento hello e non danneggiare i dati ha ripristinato toobe.

Anche se molti approcci sono possibili, si offrono alcuni esempi sull'utilizzo di `RestoreAsync` toorecover da hello sopra gli scenari.

## <a name="partition-data-loss-in-reliable-services"></a>Perdita di dati della partizione in Reliable Services
In questo caso, hello runtime verrà automaticamente rilevare perdite di dati hello e richiamare hello `OnDataLossAsync` API.

autore servizio Hello deve hello tooperform toorecover seguenti:

  - Eseguire l'override di metodo della classe base virtuale hello `OnDataLossAsync`.
  - Trovare hello più recente backup nel percorso esterno hello che contiene il backup del servizio hello.
  - Scaricare l'ultimo backup hello (e decomprimere i backup hello nella cartella di backup hello se compresso).
  - Hello `OnDataLossAsync` metodo fornisce un `RestoreContext`. Chiamare hello `RestoreAsync` API in hello fornito `RestoreContext`.
  - Restituisce true se il ripristino di hello riuscita.

Ecco un esempio di implementazione di hello `OnDataLossAsync` metodo:

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`passato toohello `RestoreContext.RestoreAsync` chiamata contiene un membro denominato `BackupFolderPath`.
Quando si ripristina un backup completo, questo `BackupFolderPath` deve essere impostato toohello percorso locale della cartella hello che contiene il backup completo.
Quando si ripristina un backup completo e un numero di backup incrementali, `BackupFolderPath` deve essere impostato toohello percorso locale della cartella hello che contiene non solo backup completi di hello, ma anche tutti i hello backup incrementali.
`RestoreAsync`chiamata può generare `FabricMissingFullBackupException` se hello `BackupFolderPath` fornito non contiene un backup completo.
Può anche generare `ArgumentException` se `BackupFolderPath` contiene una catena interrotta di backup incrementali,
Ad esempio, se contiene hello backup completo, innanzitutto hello incrementale e hello terzo backup incrementale, ma nessun backup incrementale secondo hello.

> [!NOTE]
> Hello RestorePolicy è tooSafe per impostazione predefinita.  Ciò significa che hello `RestoreAsync` API avrà esito negativo con ArgumentException se rileva tale cartella di backup hello contiene uno stato che è stato più vecchi di o uguale toohello contenuto in questa replica.  `RestorePolicy.Force`può essere utilizzato tooskip il controllo di sicurezza. Viene specificato come parte di `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Servizio eliminato o perso
Se viene rimosso un servizio, è necessario innanzitutto creare nuovamente servizio hello prima di ripristinare i dati di hello.  È importante toocreate hello servizio con hello stessa configurazione, ad esempio, il partizionamento di schema, in modo che hello dati può essere ripristinata senza problemi.  Una volta servizio hello è attivo, hello dati toorestore API (`OnDataLossAsync` sopra) ha toobe richiamata per ogni partizione del servizio. A tal fine, è possibile usare `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` su ogni partizione.  

A questo punto, implementazione è hello come hello sopra scenario. Ogni partizione deve toorestore hello ultimo rilevanti backup dall'archivio esterno hello. Uno svantaggio è tale partizione hello che ID sia stato ora modificato, poiché hello runtime crea gli ID di partizione in modo dinamico. Di conseguenza, il servizio di hello necessita di informazioni di partizione appropriato toostore hello e servizio nome tooidentify hello corretto più recente backup toorestore da per ogni partizione.

> [!NOTE]
> Non è consigliabile toouse `FabricClient.ServiceManager.InvokeDataLossAsync` in ogni partizione toorestore hello intero servizio, dal momento che potrebbe danneggiare lo stato del cluster.
> 

## <a name="replication-of-corrupt-application-data"></a>Replica di dati dell'applicazione danneggiati
Se l'aggiornamento dell'applicazione hello appena distribuito dispone di un bug, che può causare il danneggiamento dei dati. Ad esempio, un aggiornamento dell'applicazione può avviare tooupdate ogni record al numero di telefono in un dizionario affidabile con un prefisso non valido.  In questo caso, i numeri di telefono non valido di hello verranno replicati poiché Service Fabric non è a conoscenza di natura hello dei dati di hello che viene archiviati.

Hello in primo luogo toodo dopo è rilevare tali un bug che causa il danneggiamento dei dati egregious è toofreeze hello servizio a livello di applicazione hello e, se possibile, aggiornare la versione toohello hello codice dell'applicazione che non dispone di bug hello.  Tuttavia, anche dopo il codice di servizio hello è fissa, dati hello ancora potrebbero essere danneggiati e pertanto dati potrebbe essere necessario toobe ripristinato.  In questi casi, potrebbe non essere sufficiente toorestore hello backup più recente, poiché i backup più recenti di hello inoltre potrebbero essere danneggiati.  Pertanto, si è toofind hello ultimo backup eseguito prima dati hello sono danneggiati.

Se non sei sicuro che i backup sono danneggiati, è possibile distribuire un nuovo cluster di Service Fabric e ripristinare i backup hello di partizioni interessate come hello sopra "Deleted o perdita di servizio" scenario.  Per ogni partizione, avviare minimo per il ripristino dei backup hello da toohello più recente di hello. Dopo aver trovato una copia di backup che non dispone di danneggiamento hello, spostamento o eliminazione della partizione di tutti i backup che erano più recenti (backup). Ripetere questo processo per ogni partizione. A questo punto, quando `OnDataLossAsync` viene chiamato nella partizione hello in cluster in produzione hello, hello ultimo backup disponibile in hello esterno archivio sarà hello uno prelevati da hello di sopra di processo.

A questo punto, i passaggi in hello, "Deleted o perdita di servizio" hello sezione può essere utilizzato lo stato di hello toorestore dello stato di toohello hello del servizio prima codice anomalo hello hello danneggiato.

Si noti che:

  - Quando si ripristina, esiste la possibilità che hello backup viene ripristinato è precedente rispetto allo stato della partizione hello hello prima hello dati sono andati persi. Per questo motivo, è necessario ripristinare solo come un ultimo toorecover risorsa quanti più dati possibile.
  - stringa che rappresenta il percorso di cartella di backup hello Hello e hello percorsi dei file nella cartella di backup hello possono essere maggiori di 255 caratteri, in base al percorso FabricDataRoot hello e lunghezza del nome del tipo di applicazione. Ciò può causare alcuni metodi di .NET, ad esempio `Directory.Move`, hello toothrow `PathTooLongException` eccezione. Una soluzione alternativa consiste toodirectly chiamare le API kernel32, ad esempio `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Eseguire il backup e il ripristino di Reliable Actors


Reliable Actors Framework si basa su Reliable Services. Hello ActorService che ospita actor(s) hello è un servizio affidabile con stato. Di conseguenza, tutti i backup di hello e funzionalità di ripristino disponibili in servizi affidabili anche attori tooReliable disponibili (eccetto i comportamenti specifico del provider di stato). Poiché i backup verranno eseguiti per partizione, verrà eseguito il backup degli stati per tutti gli attori in quella partizione (il ripristino è simile e verrà eseguito anch'esso per partizione). tooperform backup/ripristino, il proprietario del servizio hello deve creare una classe di servizio actor personalizzata che deriva dalla classe ActorService e quindi backup/ripristino simile tooReliable Services come descritto in precedenza nella sezione precedente.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Quando si crea una classe del servizio actor personalizzato, è necessario che anche tooregister durante la registrazione attore hello.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

provider di stato predefinito Hello per Reliable Actors `KvsActorStateProvider`. Per impostazione predefinita, il backup incrementale non è abilitato per `KvsActorStateProvider`. È possibile abilitare il backup incrementale creando `KvsActorStateProvider` con hello appropriato impostando nel relativo costruttore e passando quindi tooActorService costruttore come illustrato nel frammento di codice seguente:

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Dopo il backup incrementale è stato abilitato, eseguire un backup incrementale può non riuscire con FabricMissingFullBackupException per uno dei seguenti motivi e sarà necessario tootake un backup completo prima di portare il/i backup incrementali:

  - replica Hello non è mai eseguito un backup completo perché era primario.
  - Alcuni dei record di log hello è stati troncati perché è stato eseguito l'ultimo backup.

Quando è abilitato il backup incrementale, `KvsActorStateProvider` non utilizza toomanage circolare del buffer relativo log registra e lo tronca periodicamente. Se viene eseguito alcun backup dall'utente per un periodo di 45 minuti, il sistema hello tronca automaticamente i record del log hello. Questo intervallo può essere configurato specificando `logTrunctationIntervalInMinutes` in `KvsActorStateProvider` costruttore (analoga toowhen Abilita il backup incrementale). i record del log Hello possono inoltre ottenere troncati se la replica primaria necessario toobuild un'altra replica mediante l'invio di tutti i relativi dati.

Quando si esegue il ripristino da una catena di backup, servizi tooReliable analoghi, hello BackupFolderPath deve contenere sottodirectory con una sottodirectory contenente backup completo e altri sottodirectory che includono il/i backup incrementali. Se si verifica un errore di convalida della catena di backup di hello, Hello ripristino API genererà FabricException con messaggio di errore appropriato. 

> [!NOTE]
> `KvsActorStateProvider`Ignora attualmente opzione hello RestorePolicy.Safe. Il supporto per questa funzionalità è pianificato per una versione futura.
> 

## <a name="testing-backup-and-restore"></a>Test del backup e del ripristino
È importante tooensure che i dati critici durante il backup e possono essere ripristinati da. Questa operazione può essere eseguita richiamando hello `Start-ServiceFabricPartitionDataLoss` cmdlet di PowerShell che possono provocare la perdita di dati in una partizione specifica di tootest se dati hello backup e ripristino delle funzionalità per il servizio funzioni come previsto.  È inoltre possibile tooprogrammatically richiamare la perdita di dati e il ripristino da anche tale evento.

> [!NOTE]
> È possibile trovare un'implementazione di esempio di backup e ripristino delle funzionalità in hello App riferimento Web in GitHub. Consultare hello `Inventory.Service` servizio per altri dettagli.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Quinte hello: ulteriori dettagli su backup e ripristino
Ecco altri dettagli sul backup e ripristino.

### <a name="backup"></a>Backup
Hello affidabile di gestione dello stato fornisce backup coerenti hello possibilità toocreate senza il blocco di lettura o le operazioni di scrittura. toodo in tal caso, utilizza un meccanismo di persistenza di checkpoint e di log.  Hello affidabile di gestione dello stato accetta fuzzy checkpoint (lightweight) determinati pressione toorelieve punti dal log delle transazioni hello e migliorare i tempi di ripristino.  Quando `BackupAsync` viene chiamato, hello affidabile di gestione dello stato indica tutti gli oggetti affidabile toocopy loro più recente del punto di controllo file tooa backup cartella locale.  Quindi, hello affidabile di gestione dello stato copia tutti i record di log, a partire da hello "start puntatore" toohello ultimo record di log nella cartella di backup hello.  Poiché tutti i record di log hello dei record del log più recente toohello siano incluse nel backup hello e affidabile di gestione dello stato di hello mantiene registrazione write-ahead, hello gestore degli stati affidabile garantisce che tutte le transazioni che viene eseguito il commit (`CommitAsync` ha restituito correttamente) sono inclusi nel backup hello.

Qualsiasi transazione di cui viene eseguito il commit dopo `BackupAsync` è stato chiamato maggio o potrebbe non essere in backup di hello.  Una volta che la cartella di backup locale di hello è stata popolata dalla piattaforma hello (ad esempio, backup locale viene completato tramite il runtime hello), del servizio hello backup richiamata.  Il callback è responsabile dello spostamento hello backup tooan esterno percorso della cartella, ad esempio l'archiviazione di Azure.

### <a name="restore"></a>Ripristino
Hello affidabile di gestione dello stato fornisce hello possibilità toorestore da un backup utilizzando hello `RestoreAsync` API.  
Hello `RestoreAsync` metodo `RestoreContext` può essere chiamato solo all'interno di hello `OnDataLossAsync` metodo.
Hello restituito da bool `OnDataLossAsync` indica se il servizio di hello ripristinato lo stato da un'origine esterna.
Se hello `OnDataLossAsync` restituisce true, tutte le altre repliche da questo primario causerà la ricostruzione Service Fabric. Service Fabric garantisce che le repliche che riceveranno `OnDataLossAsync` chiamare primo ruolo primario di transizione toohello ma stato non vengono concesse lettura o scrittura dello stato.
Per i responsabili dell'implementazione di StatefulService significa che `RunAsync` viene chiamato solo dopo il completamento corretto di `OnDataLossAsync`.
Quindi, `OnDataLossAsync` verrà richiamato nel nuovo database primario di hello.
Fino a quando un servizio consente di completare questa API correttamente (restituisce true o false) e termina la riconfigurazione rilevanti hello, hello API verrà mantenere viene chiamato uno alla volta.

`RestoreAsync`prima Elimina tutti gli stati esistenti nella replica primaria hello che è stata chiamata su.  
Hello affidabile stato Manager crea quindi tutti gli oggetti affidabile hello che esistono nella cartella di backup hello.  
Successivamente, gli oggetti affidabile di hello sono istruzioni riportate toorestore dai loro checkpoint nella cartella di backup hello.  
Infine, hello affidabile di gestione dello stato consente di recuperare il proprio stato da record del log nella cartella di backup hello hello ed esegue il ripristino.  
Come parte del processo di ripristino hello, a partire da hello "punto di partenza" le operazioni che include i record di commit del log nella cartella di backup di hello sono oggetti affidabile toohello riprodotto.  
Questo passaggio garantisce che hello ripristinato lo stato è coerente.

## <a name="next-steps"></a>Passaggi successivi
  - [Reliable Collections](service-fabric-work-with-reliable-collections.md)
  - [Guida introduttiva a Reliable Services di Microsoft Azure Service Fabric](service-fabric-reliable-services-quick-start.md)
  - [Notifiche di Reliable Services](service-fabric-reliable-services-notifications.md)
  - [Configurazione di Reliable Services](service-fabric-reliable-services-configuration.md)
  - [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

