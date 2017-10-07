---
title: aaaDesigning applicazioni altamente disponibili, utilizzando l'archiviazione con ridondanza geografica di Azure e accesso in lettura (RA-GRS) | Documenti Microsoft
description: "Come tooarchitect di archiviazione Azure RA-GRS toouse applicazioni a disponibilità elevata flessibilità sufficiente interruzioni toohandle."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Progettazione di applicazioni a disponibilità elevata con RA-GRS

Una funzionalità comune delle infrastrutture basate su cloud è che offrono una piattaforma a disponibilità elevata per l'hosting di applicazioni. Gli sviluppatori di applicazioni basate su cloud è necessario considerare attentamente come tooleverage agli utenti di tootheir questa piattaforma toodeliver applicazioni a disponibilità elevata. Questo articolo illustra in modo specifico su come gli sviluppatori possono utilizzare hello Azure archiviazione l'accesso in lettura archiviazione con ridondanza geografica (RA-GRS) toomake le applicazioni non è più disponibile.

Sono disponibili quattro opzioni di ridondanza: archiviazione con ridondanza locale (LRS), archiviazione con ridondanza della zona (ZRS), archiviazione con ridondanza geografica (GRS) e archiviazione con ridondanza geografica e accesso in lettura (RA-GRS). Verrà toodiscuss GRS e RA-GRS in questo articolo. Con l'archiviazione con ridondanza geografica, vengono mantenute tre copie dei dati nell'area primaria di hello selezionato durante l'impostazione di account di archiviazione hello. Altre tre copie vengono mantenute in modo asincrono in un'area secondaria specificata da Azure. RA-GRS è hello equivale all'archiviazione con ridondanza geografica, ad eccezione del fatto che si dispone di accesso in lettura toohello secondario copia. Per ulteriori informazioni sulle opzioni di ridondanza di archiviazione di Azure diversi hello, vedere [replica di archiviazione Azure](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). Hello replica viene inoltre hello associazioni di aree di hello primario e secondario.

Sono disponibili i frammenti di codice inclusi in questo articolo e un esempio completo tooa di collegamento alla fine di hello che è possibile scaricare ed eseguire.

## <a name="key-features-of-ra-grs"></a>Funzionalità principali dell'archiviazione con ridondanza geografica e accesso in lettura

Prima di descrivere come toouse archiviazione RA-GRS, esaminiamo le proprietà e comportamento.

* Archiviazione di Azure mantiene una copia di sola lettura di dati hello memorizzati nell'area primaria in un'area secondaria; come indicato in precedenza, il servizio di archiviazione hello determina posizione hello di un'area secondaria hello.

* copia di sola lettura Hello è [alla fine coerente](https://en.wikipedia.org/wiki/Eventual_consistency) con dati hello nell'area primaria hello.

* Per BLOB, tabelle e code, è possibile eseguire una query area secondaria di hello per un *ora dell'ultima sincronizzazione* valore che indica quando la replica ultimo hello dall'area secondaria di hello toohello primario si è verificato. Questa operazione non è supportata per Archiviazione file di Azure, che non ha attualmente l'archiviazione con ridondanza geografica e accesso in lettura.

* È possibile utilizzare hello libreria Client di archiviazione toointeract con dati hello in una regione di hello primario o secondario. È inoltre possibile reindirizzare lettura richiede automaticamente area secondaria toohello caso di timeout di un'area primaria toohello di richiesta di lettura.

* Se si verifica un problema importante avere effetto sull'accessibilità hello dei dati di hello nell'area primaria hello, hello team di Azure può attivare un failover geografico, a quel punto le voci DNS di hello verso l'area primaria toohello saranno modificate toopoint toohello secondario area.

* Se si verifica un failover geografico, Azure verrà selezionare un nuovo percorso secondario percorso toothat di hello dati di replica, quindi scegliere tooit di voci DNS secondario hello. endpoint secondario Hello sarà disponibile fino a quando l'account di archiviazione hello abbia terminato la replica. Per ulteriori informazioni, vedere [quali toodo se si verifica un'interruzione di servizio di archiviazione Azure](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>Considerazioni sulla progettazione di applicazioni quando si usa l'archiviazione con ridondanza geografica e accesso in lettura

scopo principale di Hello di questo articolo è tooshow è come un'applicazione che continuerà toofunction (anche se in una capacità limitata) anche in caso di hello di un errore grave nel file di dati primario hello toodesign center. Questo scopo è avente il temporaneo toohandle applicazione o problemi con esecuzione prolungata mentre si è verificato un problema di commutazione tooread dall'area secondaria hello e passa indietro quando l'area primaria hello sarà nuovamente disponibile.

### <a name="using-eventually-consistent-data"></a>Uso di dati con coerenza finale

Questa soluzione proposta presuppone che sia accettabile tooreturn ciò che potrebbe essere l'applicazione chiamante toohello di dati non aggiornati. Poiché dati secondari hello sono alla fine coerenti, è possibile che dati hello è stata scritta toohello primario ma hello aggiornamento toohello secondario del termine non replicare quando l'area primaria hello è diventato inaccessibile.

Ad esempio, il cliente è stato possibile inviare un aggiornamento che ha esito positivo e quindi hello primario può scendere prima aggiornamento hello viene propagato toohello secondario. In questo caso, se il cliente di hello chiede quindi backup dei dati hello tooread, ricevuti dati non aggiornati di hello anziché dati hello aggiornato. È necessario decidere se questa situazione è accettabile e in tal caso, come viene verrà messaggio cliente hello. Verrà visualizzato come toocheck hello ora dell'ultima sincronizzazione dati secondario di hello più avanti in questo articolo di toosee se hello secondario è aggiornato.

### <a name="handling-services-separately-or-all-together"></a>Gestione separata o collettiva dei servizi

Anche se probabilmente non è possibile che toobecome un servizio non disponibile mentre hello altri servizi sono ancora completamente funzionale. È possibile handle hello tentativi e modalità di sola lettura per ogni servizio separatamente (BLOB, code, tabelle) oppure è possibile gestire i tentativi in modo generico per tutti i servizi di archiviazione hello insieme.

Ad esempio, se si usa code e BLOB nell'applicazione, si può decidere tooput errori non irreversibile toohandle di codice separato per ognuno di essi. Quindi se viene ricevuto un nuovo tentativo dal servizio blob hello, ma il servizio di Accodamento di hello sta ancora lavorando, sarà interessata solo hello in parte l'applicazione che gestisce i BLOB. Se si decide di toohandle servizio di archiviazione di tutti i tentativi in modo generico e un servizio di chiamata toohello blob restituisce un errore non irreversibile, quindi ne risentirà richieste tooboth hello blob servizio e il servizio di Accodamento di hello.

Ciò dipende in definitiva, complessità hello dell'applicazione. È possibile decidere di non gli errori di hello toohandle dal servizio, ma invece di leggere le richieste per tutti i servizi toohello secondario area di archiviazione e di eseguire un'applicazione hello in modalità di sola lettura quando viene rilevato un problema con qualsiasi servizio di archiviazione nell'area primaria hello tooredirect.

### <a name="other-considerations"></a>Altre considerazioni

Questi sono hello altre considerazioni si parlerà in rest hello di questo articolo.

*   La gestione dei tentativi di richieste di lettura utilizzando il modello di interruttore hello

*   I dati alla fine coerente e hello ora dell'ultima sincronizzazione

*   Test

## <a name="running-your-application-in-read-only-mode"></a>Esecuzione dell'applicazione in modalità di sola lettura

toouse archiviazione RA-GRS, deve essere in grado di toohandle sia impossibile le richieste di lettura e non è stato possibile di richieste di aggiornamento (con aggiornamento in questo caso pertanto gli inserimenti, aggiornamenti ed eliminazioni). Se hello ha esito negativo centro dati principale, di lettura delle richieste può essere reindirizzato toohello data center secondario, ma le richieste di aggiornamento non è possibile perché hello secondario è di sola lettura. Per questo motivo, è necessario alcuni toorun modo l'applicazione in modalità di sola lettura.

Ad esempio, è possibile impostare un flag che verrà controllato prima dell'invio di qualsiasi servizio di archiviazione toohello le richieste di aggiornamento. Quando una delle richieste di aggiornamento hello, è possibile ignorarlo e restituire un cliente toohello risposta appropriata. È possibile anche desidera toodisable completamente determinate funzionalità finché non viene risolto il problema di hello e avvisare gli utenti che tali funzionalità sono temporaneamente non disponibile.

Se si decide di separatamente toohandle errori per ogni servizio, è necessario anche toohandle hello possibilità toorun l'applicazione in modalità di sola lettura dal servizio. È possibile che i flag di sola lettura per ogni servizio che può essere abilitato e disabilitato e handle hello flag appropriati nelle posizioni appropriate di hello nel codice.

Toorun in grado di corso l'applicazione in modalità di sola lettura con un altro vantaggio: consente di definire funzionalità limitate per hello possibilità tooensure durante un aggiornamento dell'applicazione principale. È possibile attivare toorun l'applicazione in sola lettura e la modalità e punto toohello data center secondario, assicurando che nessun utente è l'accesso ai dati di hello nell'area primaria hello mentre si apportano gli aggiornamenti.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Gestione degli aggiornamenti durante l'esecuzione in modalità di sola lettura

Esistono diversi modi toohandle aggiornamento richieste durante l'esecuzione in modalità di sola lettura. Questi modi non verranno illustrati nei dettagli, ma in linea generale vengono presi in considerazione due modelli.

1.  È possibile rispondere utente tooyour e segnalando che non attualmente implica l'accettazione degli aggiornamenti. Ad esempio, un sistema di gestione dei contatti potrebbe consentire ai clienti informazioni di contatto tooaccess ma non effettuare aggiornamenti.

2.  È possibile accodare gli aggiornamenti in un'altra area. In questo caso, sarebbe scrivere la coda tooa le richieste di aggiornamento in sospeso in un'area diversa e quindi di avere tali richieste tooprocess un modo dopo hello data center principale viene portato nuovamente online. In questo scenario, è necessario comunicare hello cliente che ha richiesto l'aggiornamento hello è in coda per l'elaborazione successiva.

3.  È possibile scrivere gli aggiornamenti tooa account di archiviazione in un'altra area. Quando hello data center principale torna online, è possibile eseguire un toomerge modo gli aggiornamenti dati hello primario, a seconda della struttura di hello dei dati di hello. Ad esempio, se si siano creando un file separato con un indicatore di data/ora nel nome hello, è possibile copiare tali area primaria toohello backup di file. Questa procedura funziona per alcuni carichi di lavoro, ad esempio dati di registrazione e iOT.

## <a name="handling-retries"></a>Gestione dei tentativi

Come si possono identificare gli errori non irreversibili? Viene determinato dalla libreria client di archiviazione hello. Ad esempio, un errore 404 (risorsa non trovata) non è non irreversibile nuovo tentativo in corso, non è probabilmente tooresult in caso di esito positivo. In hello invece un errore 500 è non irreversibile perché si tratta di un errore del server, e può essere semplicemente un problema temporaneo. Per ulteriori dettagli, consultare hello [aprire codice sorgente per la classe ExponentialRetry hello](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) nella libreria client di archiviazione .NET hello. (Cercare hello metodo ShouldRetry).

### <a name="read-requests"></a>Richieste di lettura

Se si è verificato un problema con l'archiviazione primaria, le richieste di lettura possono essere reindirizzato toosecondary archiviazione. Come indicato in precedenza in [utilizzando infine i dati coerenti](#using-eventually-consistent-data), deve essere accettabile per toopotentially l'applicazione di leggere i dati non aggiornati. Se si utilizza hello storage client library tooaccess dati RA-GRS, è possibile specificare il comportamento di ripetizione hello di una richiesta di lettura impostando un valore per hello **LocationMode** tooone delle proprietà seguenti hello:

*   **Localizzazione PrimaryOnly** (hello predefinito)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Quando si imposta hello **LocationMode** troppo**PrimaryThenSecondary**, se hello iniziale leggere endpoint primario toohello di richiesta ha esito negativo con un errore non irreversibile, il client di hello esegue automaticamente un'altra lettura endpoint secondario toohello della richiesta. Se l'errore hello è un timeout del server, client hello avrà toowait per hello timeout tooexpire prima di ricevere un errore non irreversibile dal servizio hello.

Sono disponibili essenzialmente due scenari tooconsider quando si decide come toorespond tooa: errore non irreversibile:

*   Si tratta di un problema di tipo isolato e l'endpoint primario di richieste successive toohello non restituirà un errore non irreversibile. Un esempio di questa situazione può verificarsi in caso di errore di rete temporaneo.

    In questo scenario, non ci sono controindicazioni significativo delle prestazioni in presenza di **LocationMode** impostare troppo**PrimaryThenSecondary** come questo errore si verifica raramente.

*   Si tratta di un problema con almeno uno dei servizi di archiviazione hello in area primaria hello e servizio di toothat tutte le successive richieste nell'area primaria hello sono errori non irreversibili tooreturn probabile per un periodo di tempo. Un esempio di questo oggetto è se l'area primaria hello è completamente accessibile.

    In questo scenario, è una riduzione delle prestazioni, poiché tutte le richieste di lettura verranno provare innanzitutto l'endpoint primario hello, attendere hello timeout tooexpire, quindi passare l'endpoint secondario toohello.

Per questi scenari, è necessario identificare che sia presente un problema con l'endpoint primario hello in corso e inviare tutte le richieste di lettura direttamente hello toohello endpoint secondario impostando **LocationMode** proprietà troppo **SecondaryOnly**. In questo momento, è necessario modificare anche toorun applicazione hello in modalità di sola lettura. Questo approccio è noto come hello [modello di interruttore](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Richieste di aggiornamento

modello di interruttore Hello può anche essere applicato tooupdate richieste. Tuttavia, le richieste di aggiornamento non possono essere reindirizzato toosecondary archiviazione, che è di sola lettura. Per queste richieste, è consigliabile lasciare hello **LocationMode** impostata troppo**localizzazione PrimaryOnly** (hello predefinito). toohandle questi errori, è possibile applicare un richiede toothese metrica –, ad esempio 10 errori in una riga e quando la soglia viene raggiunta, un'applicazione hello in modalità di sola lettura. È possibile utilizzare hello stessi metodi per la restituzione di modalità tooupdate come quelle descritte di seguito nella sezione successiva di hello sul modello di interruttore hello.

## <a name="circuit-breaker-pattern"></a>Modello a interruttore

Utilizzando il modello di interruttore hello nell'applicazione può impedirne Ritenta un'operazione che è probabile che toofail ripetutamente. Consente di hello applicazione toocontinue toorun piuttosto che occupano tempo durante l'operazione di hello viene ripetuta in modo esponenziale. Verifica inoltre rileva se l'errore hello è stato risolto, in cui un'applicazione hello ora possibile provare a ripetere l'operazione di hello.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>Come tooimplement hello modello di interruttore

tooidentify che si verifica un problema con un endpoint primario in corso, è possibile monitorare la frequenza con cui client hello rileva errori non irreversibili. Poiché ogni case è diversa, occorre toodecide soglia hello desiderate toouse per endpoint secondario toohello tooswitch decisione hello e l'esecuzione di un'applicazione hello in modalità di sola lettura. Ad esempio, è possibile decidere commutatore hello tooperform se sono presenti errori di 10 in una riga con operazioni non riuscite. Un altro esempio è tooswitch se hanno esito negativo 90% delle richieste di hello in un periodo di 2 minuti.

Per primo scenario hello, è semplicemente possibile mantenere un numero di errori di hello e nel caso di esito positivo prima di raggiungere hello toozero di back-conteggio massimo, impostare hello. Per secondo scenario hello, tooimplement unidirezionale è toouse hello MemoryCache oggetto (.NET). Per ogni richiesta, aggiungere una cache toohello CacheItem, hello valore toosuccess (1) o avere esito negativo (0) e too2 minuti di hello scadenza ora dall'ora (o qualunque sia il vincolo di tempo). Quando viene raggiunta l'ora di scadenza della voce, la voce hello viene rimosso automaticamente. Sarà così disponibile una finestra continua di 2 minuti. Ogni volta che si apportata un servizio di archiviazione toohello richiesta, utilizzare innanzitutto una query Linq in hello MemoryCache oggetto toocalculate hello percentuale di successo somma i valori hello e dividendo per il conteggio di hello. Quando la percentuale di successo hello scende sotto una determinata soglia (ad esempio il 10%), impostare hello **LocationMode** proprietà per richieste di lettura troppo**SecondaryOnly** e passa in modalità di sola lettura prima di un'applicazione hello continuare.

soglia di Hello degli errori utilizzata toodetermine quando l'opzione hello toomake può variare rispetto a tooservice servizio dell'applicazione, pertanto è consigliabile rendendoli parametri configurabili. Si tratta anche se si decide di separatamente gli errori non irreversibili toohandle da ogni servizio o come una sola, come descritto in precedenza.

Un'altra considerazione riguarda la modalità toohandle più istanze di un'applicazione e quali toodo quando si rilevano errori non irreversibili in ogni istanza. Ad esempio, è possibile 20 macchine virtuali in esecuzione con hello caricamento dell'applicazione stessa. Ogni istanza viene gestita separatamente? Se un'istanza avvia problemi, si desidera toolimit hello risposta toojust di un'istanza o si desidera tootry toohave tutte le istanze di rispondono in hello stesso quando un'istanza dispone di un problema? La gestione di istanze di hello separatamente è molto più semplice che sta tentando di risposta hello toocoordinate tra di loro, ma la procedura dipende dall'architettura dell'applicazione.

### <a name="options-for-monitoring-hello-error-frequency"></a>Opzioni per il monitoraggio frequenza di errore hello

Esistono tre opzioni per il monitoraggio frequenza hello di tentativi nell'area primaria di hello in ordine toodetermine quando tooswitch area secondaria toohello e modifica hello toorun applicazione in modalità di sola lettura.

*   Aggiungere un gestore per hello [ **nuovo tentativo in corso** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) evento hello [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) dell'oggetto il passaggio delle richieste di archiviazione tooyour: si tratta di hello metodo visualizzato in questo articolo e utilizzato nel hello che accompagna di esempio. Questi eventi vengono attivati ogni volta che il client hello Ritenta una richiesta, che consente la frequenza con cui tootrack client hello rileva errori non irreversibili in un endpoint primario.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   In hello [ **Evaluate** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) metodo in un criterio di ripetizione di tentativi personalizzati, è possibile eseguire codice personalizzato ogni volta che un nuovo tentativo viene eseguito. In aggiunta toorecording quando si verifica un nuovo tentativo, questo consente hello opportunità toomodify il comportamento del nuovo tentativo.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   terzo approccio Hello è un componente di monitoraggio personalizzato nell'applicazione che esegue il ping continuamente l'endpoint di archiviazione primaria fittizio tooimplement leggere le richieste (ad esempio leggendo un blob di piccole dimensioni) toodetermine relativa integrità. Questa operazione impiegherà alcune risorse, ma non molte. Quando viene rilevato un problema che raggiunge la soglia, quindi eseguire switch hello troppo**SecondaryOnly** e modalità di sola lettura.

A un certo punto, si desidererà endpoint primario di tooswitch toousing indietro hello e consentire gli aggiornamenti. Se si utilizza uno dei primi due metodi hello elencati in precedenza, è possibile passare l'endpoint primario toohello indietro e abilitare la modalità di aggiornamento dopo un periodo di tempo selezionato arbitrariamente o numero di operazioni è stata eseguita. È possibile quindi consentire torna tramite la logica di ripetizione hello. Se il problema hello è stato risolto, verrà continuare endpoint primario del toouse hello e consentire gli aggiornamenti. Se è ancora un problema, ancora una volta passa endpoint secondario toohello indietro e modalità di sola lettura dopo criteri hello che è stata impostata.

Per terzo scenario hello, quando endpoint di archiviazione primario hello ping nuovamente esito positivo, è possibile attivare torna hello troppo**localizzazione PrimaryOnly** e continuare a consentire gli aggiornamenti.

## <a name="handling-eventually-consistent-data"></a>Gestione di dati con coerenza finale

RA-GRS funziona mediante la replica di transazioni dall'area secondaria di hello toohello primario. Il processo di replica garantisce la hello dei dati nell'area secondaria hello *alla fine coerente*. Ciò significa che tutte le transazioni di hello nell'area primaria hello verranno infine visualizzate nell'area secondaria hello, ma che potrebbe verificarsi un ritardo prima che vengano visualizzati e che non vi è alcuna garanzia transazioni hello arrivare in area secondaria di hello in hello stesso ordine che in cui sono stati originariamente installati nell'area primaria hello. Se le transazioni arrivano in area secondaria di hello non in ordine, si *potrebbe* prendere in considerazione i dati in toobe area secondaria hello in uno stato incoerente finché il servizio hello è aggiornato.

Hello nella tabella seguente viene illustrato un esempio di cosa potrebbe accadere quando si aggiorna i dettagli di hello di toomake un dipendente un membro di hello *amministratori* ruolo. Per i migliori risultati hello di questo esempio, è necessario aggiornare hello **dipendente** entità e aggiornare un **ruolo di amministratore** entità con un conteggio del numero totale di hello degli amministratori. Si noti come hello applicati gli aggiornamenti sono disponibili nell'area secondaria hello.

| **Ora** | **Transazione**                                            | **Replica**                       | **Ora ultima sincronizzazione** | **Risultato** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | Transazione A: <br> Inserimento dell'entità <br> employee nell'area primaria |                                   |                    | La transazione A inserito tooprimary,<br> non ancora replicata. |
| T1       |                                                            | Transazione A <br> replicata<br> nell'area secondaria | T1 | La transazione replicata toosecondary. <br>Ora ultima sincronizzazione aggiornata.    |
| T2       | Transazione B:<br>Aggiornamento<br> dell'entità employee<br> nell'area primaria  |                                | T1                 | Transazione B scritte tooprimary,<br> non ancora replicata.  |
| T3       | Transazione C:<br> Aggiornamento <br>entità<br>administrator role nell'area<br>primaria |                    | T1                 | Transazione C scritta tooprimary,<br> non ancora replicata.  |
| *T4*     |                                                       | Transazione C <br>replicata<br> nell'area secondaria | T1         | Transazione C replicata toosecondary.<br>LastSyncTime non aggiornato perché <br>la transazione B non è stata ancora replicata.|
| *T5*     | Lettura delle entità <br>dall'area secondaria                           |                                  | T1                 | Si ottiene hello valore non aggiornato per dipendente <br> employee perché la transazione B <br> non è stata ancora replicata. Ottenere hello nuovo valore per<br> l'entità administrator role perché C è stata<br> replicata. Ora ultima sincronizzazione non ancora<br> aggiornata perché la transazione B<br> non è stata replicata. È possibile stabilire che<br>l'entità administrator role è incoerente <br>essendo hello entità data/ora dopo <br>Hello ora dell'ultima sincronizzazione. |
| *T6*     |                                                      | Transazione B<br> replicata<br> nell'area secondaria | T6                 | *T6*: tutte le transazioni fino alla C sono <br>state replicate, ora ultima sincronizzazione<br> aggiornata. |

In questo esempio, si supponga hello client commutatori tooreading dall'area secondaria di hello al T5. È possibile leggere correttamente hello **ruolo di amministratore** entità in questo momento, ma l'entità hello contiene un valore per il conteggio di hello degli amministratori che non è coerenza con il numero di hello di **dipendente** entità in questa fase, che sono contrassegnati come amministratori nell'area secondaria hello. Il client può visualizzare questo valore, con rischio di hello è costituito da informazioni incoerenti. In alternativa, hello client potrebbe tentare toodetermine tale hello **ruolo di amministratore** è in uno stato potenzialmente incoerente perché si sono verificati nell'ordine errato hello aggiornamenti e quindi comunicare utente hello del fact.

toorecognize che dispone di dati potenzialmente non coerenti, hello può utilizzare hello valori di hello *ora dell'ultima sincronizzazione* che è possibile ottenere in qualsiasi momento eseguendo una query su un servizio di archiviazione. In questo modo si hello ora dati hello nell'area secondaria hello ultimo coerente e quando è applicato servizio hello tutti hello transazioni toothat precedente punto nel tempo. Nell'esempio hello illustrato in precedenza, dopo che il servizio hello inserito hello **dipendente** entità nell'area secondaria hello, hello ora dell'ultima sincronizzazione è troppo*T1*. Rimane *T1* fino a quando il servizio di hello Aggiorna hello **dipendente** entità nell'area secondaria di hello quando si imposta troppo*T6*. Se il client di hello recupera hello quando legge entità hello all'ora dell'ultima sincronizzazione *T5*, è possibile confrontarlo con timestamp hello in entità hello. Se il timestamp di hello nell'entità hello è successiva a quella hello ultima sincronizzazione riuscita, quindi hello entità si trova in uno stato potenzialmente non coerente ed effettuare qualunque sia l'azione appropriata di hello per l'applicazione. L'utilizzo del campo, è necessario conoscere quando hello ultimo aggiornamento toohello primaria è stata completata.

## <a name="testing"></a>Test

È importante tootest che l'applicazione si comporta come previsto quando si verificano errori non irreversibili. Ad esempio, è necessario tootest che hello toohello Opzioni applicazione secondaria e in modalità di sola lettura quando viene rilevato un problema e torna quando area primaria hello diventa nuovamente disponibile. toodo, è necessario un toosimulate riproducibile gli errori e controllare la frequenza con cui si verificano.

È possibile utilizzare [Fiddler](http://www.telerik.com/fiddler) toointercept e modificare le risposte HTTP in uno script. Questo script è possibile identificare le risposte provenienti dall'endpoint primario e modificare tooone codice stato HTTP di hello che hello che libreria Client di archiviazione riconosce come un errore non irreversibile. Frammento di codice seguente illustra un semplice esempio di script Fiddler che intercetta le richieste di tooread risposte contro hello **employeedata** tooreturn tabella stato 502:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

È possibile estendere questo esempio toointercept una gamma più ampia di richieste e modificare solo hello **responseCode** alcuni di essi toobetter simulare uno scenario reale. Per ulteriori informazioni sulla personalizzazione script Fiddler, vedere [la modifica di una richiesta o risposta](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) in hello documentazione Fiddler.

Se sono state apportate le soglie di hello per l'applicazione tooread sola modalità configurabile di commutazione, sarà più facile tootest hello il comportamento con volumi di transazioni non di produzione.

## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni sull'accesso in lettura con ridondanza geografica, incluso un altro esempio di impostazione hello LastSyncTime, vedere [opzioni di ridondanza di archiviazione di Azure Windows e accesso in lettura l'archiviazione con ridondanza geografica](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Per un esempio completo che illustra come toomake hello commutatore avanti e indietro tra gli endpoint di hello primari e secondari, vedere [esempi di Azure-utilizzo hello modello di interruttore con archiviazione RA-GRS](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
