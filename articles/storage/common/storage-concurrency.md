---
title: aaaManaging concorrenza in archiviazione di Microsoft Azure
description: "Modalità concorrenza toomanage per hello servizi Blob, coda, tabella e File"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 5b8efbe0a9ebc881ded8f3abef5f138e0385f7c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Gestione della concorrenza nell'archiviazione di Microsoft Azure
## <a name="overview"></a>Panoramica
Le moderne applicazioni basate su Internet sono in genere caratterizzate dalla presenza simultanea di più utenti che visualizzano e aggiornano dati. Ciò richiede toothink agli sviluppatori dell'applicazione con attenzione sulla modalità tooprovide a stimabile esperienza tootheir utenti finali, in particolare per scenari in cui è possono aggiornare più utenti hello stessi dati. Gli sviluppatori in genere prendono in considerazione tre strategie principali di concorrenza dei dati:  

1. Concorrenza ottimistica: un'applicazione eseguendo che un aggiornamento come parte del relativo aggiornamento verificherà se i dati hello sono stato modificato dall'applicazione hello ultima di leggere i dati. Ad esempio, se due utenti che visualizzano una pagina wiki toohello un aggiornamento stessa pagina piattaforma wiki hello è necessario assicurarsi che gli aggiornamenti di secondo hello non implica la sovrascrittura primo aggiornamento hello: e che entrambi gli utenti di comprendere se l'aggiornamento è riuscita o meno. Questa strategia viene usata con maggiore frequenza nelle applicazioni Web.
2. Concorrenza pessimistica: un'applicazione di ricerca tooperform un aggiornamento richiederà un blocco su un oggetto impedisce l'aggiornamento dati hello fino a quando viene rilasciato il blocco di hello di altri utenti. Ad esempio, in uno scenario di replica dati master/slave, in cui solo master hello eseguirà aggiornamenti master hello in genere conterrà un blocco esclusivo per un lungo periodo di tempo in tooensure dati hello non possa possibile aggiornarla.
3. Ultimo writer wins: un approccio che consenta di qualsiasi tooproceed di operazioni di aggiornamento senza verificare se un'altra applicazione ha hello dati aggiornati dall'applicazione hello prima lettura dati hello. Questa strategia (o mancanza di una strategia formale) viene in genere usata in cui i dati vengono partizionati in modo che non vi è alcun rischio che più utenti accederanno hello stessi dati. Può inoltre essere utile per l'elaborazione di flussi dei dati di breve durata.  

In questo articolo viene fornita una panoramica di come piattaforma di archiviazione di Azure hello semplifica lo sviluppo fornendo supporto eccellente per tutte e tre queste strategie di concorrenza.  

## <a name="azure-storage--simplifies-cloud-development"></a>Archiviazione di Azure – Semplifica lo sviluppo cloud
Hello Servizio archiviazione di Azure supporta tutte e tre le strategie, sebbene sia distintivo in possibilità tooprovide supporto completo per la concorrenza ottimistica e pessimistica perché era tooembrace progettato un modello di coerenza assoluta garantisce che quando Hello commit servizio di archiviazione dati inserire o aggiornare tutti gli accessi toothat ulteriori dati verranno visualizzato hello aggiornamento più recente di operazione. Piattaforme di archiviazione che utilizzano un modello di coerenza finale hanno un ritardo tra quando un'operazione di scrittura viene eseguita da un utente e quando hello aggiornato i dati possono essere visualizzati da altri utenti della complessità pertanto lo sviluppo di applicazioni client incoerenze tooprevent ordine da che interessano gli utenti finali.  

Inoltre tooselecting gli sviluppatori di strategia di concorrenza appropriata devono anche tenere come una piattaforma di archiviazione isola cambia, in particolare i toohello modifiche stesso oggetti tra le transazioni. Hello Servizio archiviazione di Azure Usa tooallow di isolamento snapshot leggere toohappen operazioni contemporaneamente a operazioni di scrittura all'interno di una singola partizione. A differenza di altri livelli di isolamento, l'isolamento dello snapshot garantisce che tutte le letture visualizzare uno snapshot coerenza dei dati hello anche durante gli aggiornamenti si verificano – essenzialmente restituendo valori commit ultimo hello durante l'elaborazione di una transazione di aggiornamento.  

## <a name="managing-concurrency-in-blob-storage"></a>Gestione della concorrenza nell'archiviazione BLOB
È possibile scegliere toouse sia modelli di concorrenza ottimistica o pessimistica toomanage accesso tooblobs e contenitori in hello servizio blob. Se non si specifica esplicitamente una strategia di ultima scritture wins predefinito hello.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Concorrenza ottimistica per BLOB e contenitori
Hello servizio di archiviazione assegna un oggetto tooevery identificatore archiviato. che viene aggiornato ogni volta che un'operazione di aggiornamento viene eseguita su un oggetto. Identificatore Hello è restituito toohello client come parte di una risposta HTTP GET con intestazione ETag (tag di entità) hello è definito nel protocollo hello HTTP. Un utente che esegue un aggiornamento in un oggetto di questo tipo può inviare in hello ETag originale insieme a un tooensure intestazione condizionale che verrà eseguito l'aggiornamento solo se è stata soddisfatta una determinata condizione: in questo caso la condizione hello è un'intestazione "If-Match", che richiede l'archiviazione hello Servizio tooensure hello valore ETag specificato nella richiesta di aggiornamento hello è hello identici a quelli archiviati nel servizio di archiviazione hello hello.  

struttura Hello di questo processo è indicato di seguito:  

1. Recuperare un blob dal servizio di archiviazione hello, risposta hello include un valore di intestazione ETag HTTP che identifica la versione corrente di hello dell'oggetto hello nel servizio di archiviazione hello.
2. Quando si aggiorna il blob hello, includere il valore di ETag hello ottenuto nel passaggio 1 in hello **If-Match** condizionale intestazione della richiesta di hello inviati toohello servizio.
3. servizio Hello Confronta valore ETag di hello nella richiesta di hello con valore ETag corrente hello del blob hello.
4. Se il valore ETag corrente hello del blob hello è una versione diversa di hello ETag in hello **If-Match** intestazione condizionale nella richiesta di hello, servizio hello restituisce un client di 412 errore toohello. Indica che un altro processo ha aggiornato blob hello poiché è stato recuperato client hello client di toohello.
5. Se hello corrente ETag del blob hello è hello stessa versione di hello ETag in hello **If-Match** intestazione condizionale nella richiesta di hello, servizio hello esegue hello ha richiesto l'operazione e gli aggiornamenti hello valore ETag corrente del blob hello tooshow che ha creato una nuova versione.  

Hello seguente frammento di codice c# (mediante la libreria Client di archiviazione 4.2.0 hello) viene illustrato un semplice esempio di tooconstruct un **AccessCondition If-Match** hello valore ETag che è accessibile dalla proprietà hello di un blob che è stato in base precedentemente recuperati o inserito. Viene quindi utilizzato hello **AccessCondition** oggetto quando viene aggiornata blob hello: hello **AccessCondition** oggetto aggiunge hello **If-Match** richiesta toohello intestazione. Se un altro processo ha aggiornato il blob hello, servizio blob hello restituisce un messaggio di stato HTTP 412 (Precondition Failed). È possibile scaricare qui completo esempio hello: [gestione della concorrenza utilizzando l'archiviazione di Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Servizio di archiviazione Hello include anche il supporto per le intestazioni condizionali aggiuntive, ad esempio **If-Modified-Since**, **If-Unmodified-Since** e **If-None-Match** nonché loro combinazioni. Per altre informazioni, vedere [Specifica di intestazioni condizionali per le operazioni del servizio BLOB](http://msdn.microsoft.com/library/azure/dd179371.aspx) su MSDN.  

Hello nella tabella seguente sono riepilogate le operazioni di contenitore hello che accettano come ad esempio le intestazioni condizionali **If-Match** richiesta hello e che restituiscono un valore ETag nella risposta hello.  

| Operazione | Restituisce il valore ETag del contenitore | Accetta intestazioni condizionali |
|:--- |:--- |:--- |
| Create Container |Sì |No |
| Get Container Properties |Sì |No |
| Get Container Metadata |Sì |No |
| Set Container Metadata |Sì |Sì |
| Get Container ACL |Sì |No |
| Set Container ACL |Sì |Sì (*) |
| Delete Container |No |Sì |
| Lease Container |Sì |Sì |
| List Blobs |No |No |

(*) hello le autorizzazioni definite da SetContainerACL vengono memorizzati nella cache e le autorizzazioni toothese aggiornamenti richiedere 30 secondi toopropagate durante il periodo in cui gli aggiornamenti non sono garantiti toobe coerente.  

Hello nella tabella seguente sono riepilogate le operazioni di blob hello che accettano come ad esempio le intestazioni condizionali **If-Match** richiesta hello e che restituiscono un valore ETag nella risposta hello.

| Operazione | Restituisce il valore ETag | Accetta intestazioni condizionali |
|:--- |:--- |:--- |
| Put Blob |Sì |Sì |
| Get Blob |Sì |Sì |
| Get Blob Properties |Sì |Sì |
| Set Blob Properties |Sì |Sì |
| Get Blob Metadata |Sì |Sì |
| Set Blob Metadata |Sì |Sì |
| Lease Blob (*) |Sì |Sì |
| Snapshot Blob |Sì |Sì |
| Copy Blob |Sì |Sì (per il BLOB di origine e destinazione) |
| Abort Copy Blob |No |No |
| Delete Blob |No |Sì |
| Put Block |No |No |
| Put Block List |Sì |Sì |
| Get Block List |Sì |No |
| Put Page |Sì |Sì |
| Get Page Ranges |Sì |Sì |

(*) Blob del lease non modifica hello ETag su un blob.  

### <a name="pessimistic-concurrency-for-blobs"></a>Concorrenza pessimistica per i BLOB
toolock un blob per l'uso esclusivo, è possibile acquisire un [lease](http://msdn.microsoft.com/library/azure/ee691972.aspx) su di esso. Quando si acquisisce un lease, è necessario specificare per quanto tempo è necessario hello lease: può trattarsi per compreso tra 15 secondi too60 o infinito, che gli importi tooan un blocco esclusivo. È possibile rinnovare un lease finito di tooextend ed è possibile rilasciare un lease dopo aver terminato con. servizio blob Hello rilascia automaticamente i lease finiti alla scadenza.  

Lease Abilita sincronizzazione diverse strategie toobe supportati, inclusi esclusivo in scrittura / scrittura esclusivo, lettura condivisa / esclusivo di lettura e scrittura condivisa / lettura esclusivo. Se esiste un lease del servizio di archiviazione hello applica esclusivo operazioni di scrittura (put e impostazione delle operazioni di eliminazione) garantendo tuttavia esclusiva per operazioni di lettura richiede hello developer tooensure che tutte le applicazioni client deve utilizzare un ID lease e che solo un client in un momento ha un ID lease valido. Le operazioni di lettura che non includono un ID lease determinano letture condivise.  

Hello c# frammento di codice seguente viene illustrato un esempio di acquisire un lease esclusivo per 30 secondi in un blob, l'aggiornamento del contenuto di hello del blob hello e quindi rilasciare il lease hello. Se è già presente un lease valido nel blob hello quando si tenta un nuovo lease tooacquire, servizio blob hello restituisce un risultato di stato di "HTTP (409) conflitto". Hello frammento seguente viene utilizzato un **AccessCondition** oggetto informazioni sul lease di hello tooencapsulate quando si rende un blob di hello tooupdate richiesta nel servizio di archiviazione hello.  È possibile scaricare qui completo esempio hello: [gestione della concorrenza utilizzando l'archiviazione di Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Se si tenta un'operazione di scrittura su un blob con lease senza passare l'ID lease hello, viene generato un errore 412 richiesta hello. Si noti che se hello lease scade prima di chiamare hello **UploadText** metodo ma si continua a superare ID lease hello, richiesta hello ha esito negativo anche con un **412** errore. Per ulteriori informazioni sulla gestione di ore di scadenza del lease e gli ID lease, vedere hello [Lease Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) documentazione REST.  

Hello operazioni blob seguenti è possono utilizzare la concorrenza pessimistica toomanage lease:  

* Put Blob
* Get Blob
* Get Blob Properties
* Set Blob Properties
* Get Blob Metadata
* Set Blob Metadata
* Delete Blob
* Put Block
* Put Block List
* Get Block List
* Put Page
* Get Page Ranges
* Snapshot Blob: ID lease facoltativo se esiste un lease
* Copia di Blob: lease ID obbligatorio se è presente un lease nel blob di destinazione hello
* Abort Copy Blob: lease ID obbligatorio se esiste un lease infinito sul blob di destinazione hello
* Lease Blob  

### <a name="pessimistic-concurrency-for-containers"></a>Concorrenza pessimistica per i contenitori
Lease sui contenitori abilitare hello stesso toobe strategie di sincronizzazione supportate come sui BLOB (esclusivo di scrittura / scrittura esclusivo, lettura condivisa / esclusivo di lettura e scrittura condivisa / lettura esclusiva) tuttavia a differenza dei blob del servizio di archiviazione hello impone solo esclusiva in operazioni di eliminazione. toodelete un contenitore con un lease attivo, un client deve includere l'ID lease attivo hello hello richiesta di eliminazione. Tutte le altre operazioni hanno esito positivo su un contenitore con lease senza includere l'ID lease hello in questo caso sono condivisi operazioni. Se è richiesta l'esclusività di un'operazione di aggiornamento (Put o Set) o di lettura, gli sviluppatori devono garantire che tutti i client usino un ID lease e che un solo client alla volta abbia un ID lease valido.  

Hello operazioni contenitore è possono utilizzare la concorrenza pessimistica toomanage lease:  

* Delete Container
* Get Container Properties
* Get Container Metadata
* Set Container Metadata
* Get Container ACL
* Set Container ACL
* Lease Container  

Per altre informazioni, vedere:  

* [Specifica di intestazioni condizionali per le operazioni del servizio BLOB](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Lease Container](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Lease Blob ](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Gestione della concorrenza in hello del servizio tabelle
servizio tabelle Hello Usa controlli di concorrenza ottimistica come comportamento predefinito di hello quando si lavora con entità, a differenza dei servizi blob hello in cui è necessario scegliere in modo esplicito i controlli di concorrenza ottimistica tooperform. Hello altra differenza tra i servizi blob e tabella di hello è che è possibile gestire solo il comportamento della concorrenza hello delle entità mentre con il servizio blob hello è possibile gestire la concorrenza hello di contenitori e BLOB.  

concorrenza ottimistica toouse e toocheck se un altro processo modificato un'entità perché è stato recuperato dal servizio di archiviazione tabelle hello, è possibile utilizzare il valore di ETag hello che viene visualizzato quando il servizio tabelle hello restituisce un'entità. struttura Hello di questo processo è indicato di seguito:  

1. Recuperare un'entità dal servizio di archiviazione tabella hello, risposta hello include un valore ETag che identifica l'identificatore attuale di hello associati all'entità nel servizio di archiviazione hello.
2. Quando si aggiorna entità hello, includere il valore di ETag hello ottenuto nel passaggio 1 in hello obbligatorio **If-Match** intestazione della richiesta di hello inviati toohello servizio.
3. servizio Hello Confronta valore ETag di hello nella richiesta di hello con valore ETag corrente hello dell'entità hello.
4. Se è diverso da quello Ciao ETag hello obbligatorio valore ETag corrente hello dell'entità hello **If-Match** intestazione nella richiesta di hello, servizio hello restituisce un client di 412 errore toohello. Indica che un altro processo ha aggiornato entità hello poiché è stato recuperato client hello client di toohello.
5. Se il valore ETag corrente hello dell'entità hello è hello stesso hello ETag in hello obbligatorio **If-Match** intestazione nella richiesta di hello o hello **If-Match** intestazione contiene caratteri jolly hello (*), servizio hello esegue hello ha richiesto l'operazione e gli aggiornamenti hello valore ETag corrente di hello tooshow di entità che è stato aggiornato.  

Si noti che, a differenza dei servizi blob hello, del servizio tabelle hello richiede hello client tooinclude un **If-Match** intestazione in richieste di aggiornamento. Tuttavia, è possibile tooforce un non condizionale (ultimo writer wins strategia) di aggiornamento e ignorare i controlli di concorrenza se i client di hello imposta hello **If-Match** carattere jolly toohello di intestazione (*) nella richiesta di hello.  

Hello frammento di codice c# seguente viene illustrata un'entità customer che in precedenza è stata creata o recuperata con indirizzo di posta elettronica aggiornato. Inserisce Hello iniziale o recuperare il valore ETag di operazione archivi hello oggetto customer hello e poiché viene utilizzato l'esempio hello hello stessa istanza dell'oggetto durante l'esecuzione di hello operazione di sostituzione, invia automaticamente il servizio tabelle toohello indietro di valore ETag di hello, abilitazione toocheck servizio hello per le violazioni di concorrenza. Se un altro processo ha aggiornato l'entità hello nell'archiviazione tabelle, il servizio di hello restituisce un messaggio di stato HTTP 412 (Precondition Failed).  È possibile scaricare qui completo esempio hello: [gestione della concorrenza utilizzando l'archiviazione di Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

disabilitare il controllo della concorrenza hello tooexplicitly, è consigliabile impostare hello **ETag** proprietà di hello **dipendente** oggetto troppo "*" prima di eseguire l'operazione di sostituzione hello.  

```csharp
customer.ETag = "*";  
```

Hello nella tabella seguente sono riepilogati come operazioni di entità tabella hello usare valori ETag:

| Operazione | Restituisce il valore ETag | Richiede l'intestazione della richiesta If-Match |
|:--- |:--- |:--- |
| Query Entities |Sì |No |
| Insert Entity |Sì |No |
| Update Entity |Sì |Sì |
| Merge Entity |Sì |Sì |
| Delete Entity |No |Sì |
| Insert or Replace Entity |Sì |No |
| Insert or Merge Entity |Sì |No |

Si noti che hello **Insert o sostituire entità** e **Insert o Merge entità** operazioni *non* esegue alcun controllo della concorrenza, poiché non inviano un toohello valore ETag servizio tabelle.  

In generale gli sviluppatori che usano tabelle devono fare affidamento sulla concorrenza ottimistica quando sviluppano applicazioni scalabili. Se il blocco pessimistico è necessaria, gli sviluppatori di un approccio possono intraprendere quando l'accesso alle tabelle viene tooassign un blob designato per ogni tabella e provare un lease nel blob hello tootake prima di operare sulla tabella hello. Questo approccio richiede tooensure applicazione hello accesso ai dati di tutti i percorsi ottenere hello lease toooperating precedente tabella hello. Si noti che una durata del lease minimo hello è 15 secondi che richiede un'attenta valutazione per la scalabilità.  

Per altre informazioni, vedere:  

* [Operazioni sulle entità](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Gestione della concorrenza in hello servizio di Accodamento
Uno scenario che in cui la concorrenza è un problema nel servizio di Accodamento messaggi hello è in cui più client recuperano messaggi da una coda. Quando un messaggio viene recuperato dalla coda di hello, risposta hello include messaggio hello e un valore di ricezione pop, ovvero messaggio hello toodelete obbligatorio. messaggio non viene eliminato automaticamente dalla coda di hello, ma dopo che sono stati recuperati, non è visibile tooother client per l'intervallo di tempo hello specificato dal parametro visibilitytimeout hello. client Hello che recupera il messaggio hello è messaggio hello toodelete previsto dopo che è stata elaborata e prima di hello ora specificata da hello elemento TimeNextVisible di hello risposta, che viene calcolato in base al valore hello hello visibilitytimeout parametro. il valore di Hello del visibilitytimeout viene aggiunto toohello ora in cui hello messaggio recuperato TimeNextVisible valore hello toodetermine.  

il servizio di Accodamento di Hello non dispone del supporto per la concorrenza ottimistica o pessimistica e per questo client motivo l'elaborazione dei messaggi recuperati da una coda devono verificare i messaggi vengono elaborati in modo idempotente. Una strategia in cui prevale l'ultima scrittura viene usata per aggiornare operazioni quali SetQueueServiceProperties, SetQueueMetaData, SetQueueACL e UpdateMessage.  

Per altre informazioni, vedere:  

* [API REST del servizio di accodamento](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Get Messages](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Gestione della concorrenza in hello servizio File
servizio file Hello è possibile accedere tramite due endpoint di protocollo diversi: SMB e REST. Hello servizio REST non dispone di supporto per il blocco ottimistico o pessimistico blocco e tutti gli aggiornamenti seguiranno una strategia di wins ultimo writer. I client SMB che montate condivisioni file possono utilizzare file blocco meccanismi toomanage accesso tooshared del file system-tra cui hello possibilità tooperform il blocco pessimistico. Quando un client SMB apre un file, specifica l'accesso al file hello sia condivisione modalità. Se un'opzione di accesso ai File di "Scrittura" o "Lettura/scrittura" insieme a una modalità di condivisione File "None", verrà restituita nel file hello è bloccato da un client SMB fino alla chiusura di file hello. Se l'operazione di resto viene tentata in un file in cui un client SMB ha bloccato file hello hello servizio REST restituirà il codice di stato 409 (conflitto) con codice errore SharingViolation.  

Quando un client SMB apre un file per l'eliminazione, contrassegna il file hello come in attesa di eliminazione fino a quando tutti gli altri client SMB vengono chiusi gli handle aperti sul file selezionato. Quando un file viene contrassegnato come in attesa di eliminazione, qualsiasi operazione REST su tale file restituirà il codice di stato 409 (Conflitto) con codice errore SMBDeletePending. Poiché è possibile per hello di hello SMB client tooremove file hello tooclosing precedente flag di eliminazione in sospeso, non viene restituito il codice di stato 404 (non trovato). In altre parole, codice di stato 404 (non trovato) è previsto solo quando è stato rimosso il file hello. Si noti che mentre un file è un protocollo SMB in sospeso lo stato di eliminazione, non essere incluso in hello che elencati i file di risultati. Si noti inoltre che le operazioni REST Elimina tutti i File e Directory eliminare REST hello vengono eseguito il commit in modo atomico e non vengano inseriti in uno stato di eliminazione in sospeso.  

Per altre informazioni, vedere:  

* [Managing File Locks](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Riepilogo e passaggi successivi
Hello archiviazione di Microsoft Azure, servizio è stato progettato esigenze hello toomeet delle applicazioni in linea più complesse hello senza imporre agli sviluppatori toocompromise o riflettere sulla chiave presupposti di progettazione, ad esempio concorrenza e consistenza dei dati che provengono tootake Per concedere.  

Per hello completare l'applicazione di esempio a cui fa riferimento in questo blog:  

* [Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Per altre informazioni sull'archiviazione di Azure, vedere:  

* [Home page di Archiviazione di Microsoft Azure](https://azure.microsoft.com/services/storage/)
* [Introduzione tooAzure archiviazione](storage-introduction.md)
* Introduzione all'archiviazione per [BLOB](../blobs/storage-dotnet-how-to-use-blobs.md), [tabelle](../../cosmos-db/table-storage-how-to-use-dotnet.md), [code](../storage-dotnet-how-to-use-queues.md) e [file](../storage-dotnet-how-to-use-files.md)
* Architettura di archiviazione - [Archiviazione di Azure: un servizio di archiviazione cloud a elevata disponibilità con coerenza assoluta](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

