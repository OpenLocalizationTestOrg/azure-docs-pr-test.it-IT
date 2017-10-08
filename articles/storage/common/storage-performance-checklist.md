---
title: "elenco di prestazioni e scalabilità di archiviazione aaaAzure | Documenti Microsoft"
description: Un elenco di controllo delle procedure consolidate per l'utilizzo dell'archiviazione di Azure nello sviluppo di applicazioni ad elevate prestazioni.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2970c055d460070288d1810e4a77a7f056a4137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure
## <a name="overview"></a>Panoramica
Dopo il rilascio hello dei servizi di archiviazione di Microsoft Azure hello, Microsoft ha sviluppato una serie di procedure comprovate per l'utilizzo di questi servizi in modo efficiente, e questo articolo serve hello tooconsolidate più importanti di esse in un elenco di controllo elenco. intenzione di Hello di questo articolo è agli sviluppatori di applicazioni toohelp verificare che utilizzano procedure comprovate con archiviazione di Azure e li identificare altre procedure consolidate, di che è opportuno valutare l'adozione toohelp. In questo articolo non toocover ogni possibile ottimizzazione delle prestazioni e scalabilità, ovvero sono esclusi quelli che sono un impatto limitato o non è applicabile su vasta scala. extent toohello hello comportamento dell'applicazione può essere previsto durante la progettazione, è utile tookeep nel presente nella fase iniziale le progettazioni tooavoid verificano dei problemi di prestazioni.  

Ogni sviluppatore di applicazioni utilizzando l'archiviazione di Azure deve richiedere tooread ora hello in questo articolo e controllare che la propria applicazione segue ognuna delle procedure elencate di seguito consolidate hello.  

## <a name="checklist"></a>Elenco di controllo
In questo articolo organizza le procedure consigliate di hello rivelato in hello seguenti gruppi. Procedure comprovate applicabili a:  

* Tutti i servizi di archiviazione di Azure (BLOB, tabelle, code e file)
* Blobs
* Tabelle
* Queues  

| Operazione completata | Area | Categoria | Domanda |
| --- | --- | --- | --- |
| &nbsp; | Tutti i servizi |Obiettivi di scalabilità |[È il tooavoid applicazione progettata per raggiungere obiettivi di scalabilità hello?](#subheading1) |
| &nbsp; | Tutti i servizi |Obiettivi di scalabilità |[È la denominazione tooenable convenzione progettata meglio il bilanciamento del carico?](#subheading47) |
| &nbsp; | Tutti i servizi |Rete |[Dispositivi sul lato client dispone della larghezza di banda sufficientemente elevato e delle prestazioni di hello tooachieve a bassa latenza necessarie?](#subheading2) |
| &nbsp; | Tutti i servizi |Rete |[I dispositivi sul lato client hanno un collegamento di qualità adeguata?](#subheading3) |
| &nbsp; | Tutti i servizi |Rete |[Un'applicazione hello client si trova "near" account di archiviazione hello?](#subheading4) |
| &nbsp; | Tutti i servizi |Distribuzione del contenuto |[Viene usata una rete CDN per la distribuzione del contenuto?](#subheading5) |
| &nbsp; | Tutti i servizi |Accesso client diretto |[Si sta utilizzando unità SAS e CORS toostorage accesso diretto tooallow anziché proxy?](#subheading6) |
| &nbsp; | Tutti i servizi |Memorizzazione nella cache |[L'applicazione sta memorizzando nella cache i dati usati di frequente e modificati raramente?](#subheading7) |
| &nbsp; | Tutti i servizi |Memorizzazione nella cache |[L'applicazione sta creando batch di aggiornamenti (memorizzandoli nella cache sul lato client e caricandoli in set più grandi)?](#subheading8) |
| &nbsp; | Tutti i servizi |Configurazione .NET |[È stato configurato il toouse client un numero sufficiente di connessioni simultanee?](#subheading9) |
| &nbsp; | Tutti i servizi |Configurazione .NET |[Sono state configurate toouse .NET un numero sufficiente di thread?](#subheading10) |
| &nbsp; | Tutti i servizi |Configurazione .NET |[Si sta usando .NET 4.5 o versione successiva, che dispone di una funzionalità migliorata di Garbage Collection?](#subheading11) |
| &nbsp; | Tutti i servizi |Parallelismo |[È stato accertato che è limitato in modo appropriato il parallelismo in modo che non sovraccaricare la funzionalità del client oppure obiettivi di scalabilità hello?](#subheading12) |
| &nbsp; | Tutti i servizi |Strumenti |[Si usa la versione più recente di hello di Microsoft sono disponibili strumenti e librerie client?](#subheading13) |
| &nbsp; | Tutti i servizi |Tentativi |[Si sta usando un criterio per l'esecuzione di nuovi tentativi per il backoff esponenziale per gli errori di limitazione e i timeout?](#subheading14) |
| &nbsp; | Tutti i servizi |Tentativi |[L'applicazione sta evitando nuovi tentativi in caso di errori irreversibili?](#subheading15) |
| &nbsp; | Blobs |Obiettivi di scalabilità |[È presente un numero elevato di client che accedono contemporaneamente a un singolo oggetto?](#subheading46) |
| &nbsp; | Blobs |Obiettivi di scalabilità |[L'applicazione è sempre all'interno di obiettivo di scalabilità di larghezza di banda o operazioni hello per un singolo blob?](#subheading16) |
| &nbsp; | Blobs |Copia dei BLOB |[La copia dei BLOB sta avvenendo in modo efficace?](#subheading17) |
| &nbsp; | Blobs |Copia dei BLOB |[Si sta usando AzCopy per le copie bulk dei BLOB?](#subheading18) |
| &nbsp; | Blobs |Copia dei BLOB |[Si siano utilizzando Importazione/esportazione di Azure tootransfer molto grandi volumi di dati?](#subheading19) |
| &nbsp; | Blobs |Usare i metadati |[Si stanno archiviando i metadati usati di frequente relativi ai BLOB nei rispettivi metadati?](#subheading20) |
| &nbsp; | Blobs |Caricamento rapido |[Quando si tenta di un blob tooupload rapidamente, si siano caricando blocchi in parallelo?](#subheading21) |
| &nbsp; | Blobs |Caricamento rapido |[Durante il tentativo tooupload molti BLOB rapidamente, si sta caricando in parallelo BLOB?](#subheading22) |
| &nbsp; | Blobs |Tipo di BLOB corretto |[Si stanno usando BLOB di pagine o in blocchi quando appropriato?](#subheading23) |
| &nbsp; | Tabelle |Obiettivi di scalabilità |[Sono è imminente hello obiettivi di scalabilità per l'entità al secondo?](#subheading24) |
| &nbsp; | Tabelle |Configurazione |[Si sta usando JSON per le richieste della tabella?](#subheading25) |
| &nbsp; | Tabelle |Configurazione |[È stato attivato Nagle prestazioni hello tooimprove di piccole dimensioni richieste?](#subheading26) |
| &nbsp; | Tabelle |Tabelle e partizioni |[I dati sono stati partizionati correttamente?](#subheading27) |
| &nbsp; | Tabelle |Partizioni critiche |[Si stanno evitando i modelli Solo accodamenti e Solo anteposizioni?](#subheading28) |
| &nbsp; | Tabelle |Partizioni critiche |[Gli inserimenti/aggiornamenti sono distribuiti in più partizioni?](#subheading29) |
| &nbsp; | Tabelle |Ambito delle query |[È stato progettato il tooallow dello schema per punto query toobe utilizzata per la maggior parte dei casi e toobe query di tabella utilizzato solo se necessario?](#subheading30) |
| &nbsp; | Tabelle |Densità delle query |[Le query in genere analizzano e restituiscono solo le righe usate dall'applicazione?](#subheading31) |
| &nbsp; | Tabelle |Limitazione dei dati restituiti |[Si sta utilizzando entità restituzione tooavoid filtro non sono necessari?](#subheading32) |
| &nbsp; | Tabelle |Limitazione dei dati restituiti |[Si sta utilizzando tooavoid proiezione restituzione di proprietà che non sono necessari?](#subheading33) |
| &nbsp; | Tabelle |Denormalizzazione |[Si hanno denormalizzato i dati in modo da evitare query inefficiente o più richieste di lettura durante il tentativo di tooget dati?](#subheading34) |
| &nbsp; | Tabelle |Inserimento/aggiornamento/eliminazione |[Si sono batch richieste necessario toobe transazionale o possono essere eseguite alla hello stesso tempo di round trip tooreduce?](#subheading35) |
| &nbsp; | Tabelle |Inserimento/aggiornamento/eliminazione |[Sono evitare il recupero di un toodetermine solo entità se toocall inserire o aggiornare?](#subheading36) |
| &nbsp; | Tabelle |Inserimento/aggiornamento/eliminazione |[È stata considerata l'archiviazione di serie di dati che vengono spesso recuperate insieme in una singola entità sotto forma di proprietà invece che in più entità?](#subheading37) |
| &nbsp; | Tabelle |Inserimento/aggiornamento/eliminazione |[Per le entità recuperate sempre insieme e che possono essere scritte in batch (ad esempio, dati di serie temporali) è stato valutato l'uso di BLOB invece che di tabelle?](#subheading38) |
| &nbsp; | Queues |Obiettivi di scalabilità |[Si è imminente hello obiettivi di scalabilità per i messaggi al secondo?](#subheading39) |
| &nbsp; | Code |Configurazione |[È stato attivato Nagle prestazioni hello tooimprove di piccole dimensioni richieste?](#subheading40) |
| &nbsp; | Code |Dimensioni del messaggio |[Sono i messaggi di compact tooimprove hello prestazioni della coda di hello?](#subheading41) |
| &nbsp; | Code |Recupero bulk |[Si stanno recuperando più messaggi con un'unica operazione "Get"?](#subheading42) |
| &nbsp; | Queues |Frequenza di polling |[Eseguono il polling spesso sufficiente hello tooreduce percepita latenza dell'applicazione?](#subheading43) |
| &nbsp; | Code |Aggiornamento del messaggio |[Si sta utilizzando lo stato di avanzamento di UpdateMessage toostore nell'elaborazione dei messaggi, evitare tooreprocess intero messaggio, se si verifica un errore?](#subheading44) |
| &nbsp; | Code |Architettura |[Si sta utilizzando code toomake l'intera applicazione più scalabile, mantenendo i carichi di lavoro a esecuzione prolungata fuori percorso critico hello e scala quindi in modo indipendente?](#subheading45) |

## <a name="allservices"></a>Tutti i servizi
Questa sezione vengono elencate procedure comprovate che utilizzano toohello applicabile di hello Azure servizi di archiviazione (BLOB, tabelle, code o file).  

### <a name="subheading1"></a>Obiettivi di scalabilità
Ciascuno dei servizi di archiviazione di Azure hello obiettivi di scalabilità per capacità (GB), la frequenza delle transazioni e larghezza di banda. Se l'applicazione si avvicina o supera i obiettivi di scalabilità di hello, potrebbe verificarsi la latenza delle transazioni o la limitazione delle richieste. Quando un servizio di archiviazione limita l'applicazione, il servizio hello inizia tooreturn "503 Server occupato" o "timeout dell'operazione 500" codici di errore per alcune transazioni di archiviazione. Questa sezione illustra in particolare entrambi toodealing approccio generale hello con obiettivi di scalabilità e obiettivi di scalabilità della larghezza di banda. Nelle sezioni successive che gestiscono i servizi di archiviazione singolo discutere obiettivi di scalabilità nel contesto di hello di tale servizio specifico:  

* [Larghezza di banda BLOB e richieste al secondo](#subheading16)
* [Entità di tabella al secondo](#subheading24)
* [Messaggi della coda al secondo](#subheading39)  

#### <a name="sub1bandwidth"></a>Obiettivo di scalabilità della larghezza di banda per tutti i servizi
Al momento della scrittura hello destinazioni di larghezza di banda hello nell'account hello US per un'archiviazione con ridondanza geografica (GRS) sono 10 Gigabit al secondo (Gbps) in ingresso (account di archiviazione toohello inviati dati) e 20 GB/s in uscita (dati inviati dall'account di archiviazione hello). Per un account di archiviazione localmente ridondante (LRS), i limiti di hello sono più elevati – 20 GB/s per in ingresso e 30 GB/s in uscita.  I limiti di larghezza di banda internazionali possono essere inferiori e possono essere visualizzati nella [pagina degli obiettivi di scalabilità](http://msdn.microsoft.com/library/azure/dn249410.aspx).  Per ulteriori informazioni sulle opzioni di ridondanza di archiviazione hello, vedere i collegamenti di hello in [risorse utili](#sub1useful) sotto.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>Quali toodo quando per raggiungere un obiettivo di scalabilità
Se l'applicazione sta per raggiungere obiettivi di scalabilità hello per un singolo account di archiviazione, è opportuno adottare uno degli approcci seguenti hello:  

* Riconsiderare hello del carico di lavoro fa sì che l'applicazione tooapproach o superare l'obiettivo di scalabilità hello. Possibile fase di progettazione in modo diverso toouse meno larghezza di banda o capacità o meno transazioni?
* Se un'applicazione può essere uno degli obiettivi di scalabilità di hello, è consigliabile creare più account di archiviazione e partizione i dati delle applicazioni tra le più account di archiviazione. Se si utilizza questo modello, quindi essere toodesign che l'applicazione in modo che è possibile aggiungere più account di archiviazione in futuro per il bilanciamento del carico hello. Al momento della stesura, ogni sottoscrizione di Azure può essere composto too100 gli account di archiviazione.  Gli account di archiviazione, inoltre, non hanno costi aggiuntivi rispetto a quelli per l'uso, ossia associati ai dati archiviati, alle transazioni effettuate o ai dati trasferiti.
* Se l'applicazione raggiunge le destinazioni di larghezza di banda hello, prendere in considerazione la compressione dei dati hello client tooreduce hello larghezza di banda richiesta toosend hello dati toohello del servizio di archiviazione.  Questa operazione, che consente di risparmiare la larghezza di banda e migliorare le prestazioni di rete, può avere anche degli effettivi negativi.  È consigliabile valutare l'impatto sulle prestazioni di hello scadenza toohello ulteriori requisiti di elaborazione per la compressione e decompressione dei dati nel client hello di questo oggetto. Inoltre, l'archiviazione dei dati compressi può rendere più difficile tootroubleshoot problemi perché potrebbe essere più difficile tooview archiviati dati, utilizzando strumenti standard.
* Se l'applicazione raggiunge obiettivi di scalabilità di hello, assicurarsi che si utilizza un backoff esponenziale per i tentativi (vedere [tentativi](#subheading14)).  La migliore toomake che non si avvicinano mai obiettivi di scalabilità di hello (utilizzando uno dei hello sopra metodi), ma in questo modo l'applicazione non appena ritentare rapidamente, rendendo hello limitazione peggiorando.  

#### <a name="useful-resources"></a>Risorse utili
Hello seguenti collegamenti fornisce dettagli aggiuntivi sulla obiettivi di scalabilità:

* Per informazioni sugli obiettivi di scalabilità, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) .
* Vedere [replica di archiviazione Azure](storage-redundancy.md) e post di blog hello [opzioni di ridondanza di archiviazione di Azure e archiviazione con ridondanza geografica di accesso in lettura](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) per informazioni sulle opzioni di ridondanza di archiviazione.
* Per informazioni aggiornate sui prezzi dei servizi Azure, vedere [Prezzi di Azure](https://azure.microsoft.com/pricing/overview/).  

### <a name="subheading47"></a>Convenzione di denominazione delle partizioni
Archiviazione di Azure Usa un basata sull'intervallo partizionamento schema tooscale e carico saldo hello system. chiave di partizione Hello è toopartition utilizzati dati in intervalli e questi intervalli sono con bilanciamento del carico tra sistema hello. Ciò significa che le convenzioni di denominazione, ad esempio lessicale ordinamento (ad esempio msftpayroll msftperformance, msftemployees, e così via) o con timestamp (log20160101 log20160102, log20160102, e così via) verranno si presta partizioni toohello potenzialmente condivise si trovano sulla hello server di partizione stessa, fino a quando l'operazione di bilanciamento del carico loro divide in intervalli più piccoli. Ad esempio, tutti i BLOB in un contenitore possono essere utilizzati da un singolo server fino a quando non hello carico sul BLOB richiede ulteriore ribilanciamento di intervalli di partizione hello. Analogamente, un gruppo di carico ridotto account con i relativi nomi disposti in ordine lessicale può essere servito da un singolo server fino a quando hello caricare uno o tutti questi account richiedono toobe divisa in più server di partizioni. Ogni operazione di bilanciamento del carico può influire sul latenza hello delle chiamate di archiviazione durante l'operazione di hello. toohandle di capacità del sistema Hello che un burst improvviso della partizione tooa traffico è limitato dalla scalabilità hello di un singolo server partizione fino a quando l'operazione di bilanciamento del carico di hello viene attivato in ingresso ed eseguito il ribilanciamento intervalli di chiavi di partizione hello.  

È possibile seguire alcune procedura frequenza di hello tooreduce consigliate di tali operazioni.  

* Esaminare una convenzione di denominazione hello che utilizzare per l'account, contenitori, BLOB, tabelle e code, strettamente. Considerare l'aggiunta di un prefisso ai nomi di account con un hash di 3 cifre, mediante la funzione di hashing più adatta alle esigenze.  
* Se si organizzano i dati utilizzando i timestamp o identificatori numerici, è necessario tooensure non si utilizza un traffico append-only (o solo anteposizioni). Questi modelli non sono adatti per un intervallo di-basato su partizionamento sistema e potrebbe lead tooall hello traffico corso tooa singola partizione e sistema hello limitazione da in modo efficace il bilanciamento del carico. Ad esempio, se si dispone di ogni giorno le operazioni che utilizzano un oggetto blob con un timestamp, ad esempio aaaammgg, quindi tutto hello il traffico per che quotidiana viene indirizzato tooa singolo oggetto cui viene gestita da un singolo server partizione. Controllare se hello per ogni blob limita e per ogni partizione limiti alle proprie esigenze e provare a suddividere l'operazione in più BLOB, se necessario. Analogamente, se si archiviano i dati della serie temporale nelle tabelle, tutto il traffico hello potrebbe essere indirizzate toohello ultima parte dello spazio dei nomi chiave hello. Se è necessario utilizzare l'ID numerico o timestamp, prefisso id hello con un hash di 3 cifre, o nel caso di hello di timestamp prefisso hello parte relativa ai secondi di tempo hello, ad esempio ssyyyymmdd. Se vengono eseguite regolarmente operazioni di query e creazione elenchi, scegliere una funzione di hashing che limiti il numero di query. In altri casi può essere sufficiente un prefisso casuale.  
* Per ulteriori informazioni su hello partizionamento schema utilizzato nell'archiviazione di Azure, leggere il documento Sosp su hello [qui](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf).

### <a name="networking"></a>Rete
Mentre hello API chiama in materia, spesso hello fisico i vincoli di rete di un'applicazione hello avere un impatto significativo sulle prestazioni. esempio Hello vengono descritte alcune delle limitazioni per gli utenti possono verificarsi.  

#### <a name="client-network-capability"></a>Capacità della rete client
##### <a name="subheading2"></a>Velocità effettiva.
Per la larghezza di banda, problema hello è spesso funzionalità hello del client hello. Ad esempio, mentre un singolo account di archiviazione è possibile gestire più di 10 Gbps di ingresso (vedere [obiettivi di scalabilità della larghezza di banda](#sub1bandwidth)), velocità di rete hello in un'istanza del ruolo di lavoro di Azure "Small" è in grado di circa 100 Mbps. Le istanze di Azure più grandi possono avere schede di interfaccia di rete con capacità più elevate ed è quindi opportuno prendere in considerazione l'uso di un'istanza più grande o di più macchine virtuali se è necessario che un singolo computer abbia limiti di rete più elevati. Se si accede da un'applicazione locale in un servizio di archiviazione, quindi hello stessa regola si applica: comprendere la funzionalità di rete hello del dispositivo client hello e toohello di connettività di rete hello percorso di archiviazione di Azure e di migliorare le esigenze o progettare il toowork applicazione entro le relative funzionalità.  

##### <a name="subheading3"></a>Qualità del collegamento
Come accade in ogni rete, tenere presente che le condizioni di rete che generano errori e perdita di pacchetti riducono la velocità effettiva.  L'uso di WireShark o NetMon può contribuire a diagnosticare il problema.  

##### <a name="useful-resources"></a>Risorse utili
Per altre informazioni sulle dimensioni della macchina virtuale e sulla larghezza di banda allocata, vedere [Dimensioni delle macchine virtuali di Windows](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Dimensioni delle macchine virtuali di Linux](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

#### <a name="subheading4"></a>Posizione
In qualsiasi ambiente distribuito, l'inserimento di client hello vicino toohello server offre prestazioni migliori hello. Per l'accesso all'archiviazione di Azure con latenza più bassa hello, hello migliore per il client si trova all'interno di hello stessa area di Azure. Ad esempio, se si ha un sito Web di Azure che usa l'archiviazione di Azure, posizionare entrambi in un'unica area (ad esempio, Stati Uniti occidentali o Asia sudorientale). Questo riduce la latenza di hello e hello costo, in fase di hello di scrittura, utilizzo della larghezza di banda in una singola regione è disponibile.  

Se il client di applicazioni non sono ospitate all'interno di Azure (ad esempio di App per dispositivi mobili o in servizi aziendali locali), quindi ripetere l'inserimento di account di archiviazione hello in un'area in prossimità di dispositivi toohello che avrà accesso, verrà in genere riducono la latenza. Se i client sono distribuiti in un'area ampia (ad esempio, alcuni in America del Nord e altri in Europa), è opportuno usare più account di archiviazione: uno nell'area nordamericana e uno in quella europea. Ciò consentirà di latenza tooreduce per gli utenti in entrambe le aree. Questo approccio è tooimplement in genere più semplice se hello hello applicazione archivi dati è tooindividual specifici utenti e non richiede la replica dei dati tra gli account di archiviazione.  Ampia distribuzione del contenuto, è consigliabile una rete CDN: vedere hello sezione successiva per ulteriori dettagli.  

### <a name="subheading5"></a>Distribuzione di contenuti
In alcuni casi, un hello tooserve esigenze di applicazione stessi utenti toomany contenuto (ad esempio, un prodotto demo video usato nella home page di un sito Web di hello), si trova in uno hello stesso o in più aree. In questo scenario, è consigliabile utilizzare una rete CDN (Content Delivery), ad esempio rete CDN di Azure e hello CDN utilizzerà l'archiviazione di Azure come origine hello dei dati di hello. A differenza di un account di archiviazione di Azure presenti in una singola area e che non è possibile distribuire contenuto con una latenza bassa tooother aree della rete CDN di Azure vengono utilizzati server in più data center in tutto il mondo hello. Inoltre, una rete CDN in genere supporta limiti in uscita molto più elevati rispetto a un singolo account di archiviazione.  

Per altre informazioni sulla rete CDN di Azure, vedere [rete CDN di Azure](https://azure.microsoft.com/services/cdn/).  

### <a name="subheading6"></a>Uso delle firme di accesso condiviso (SAS) e della condivisione risorse tra le origini (CORS)
Quando è necessario codice tooauthorize come JavaScript nel browser web dell'utente o di cellulare app tooaccess dati in archiviazione di Azure, un approccio consiste toouse un'applicazione nel ruolo web come proxy: dispositivo dell'utente hello autentica con ruolo web hello, che a sua volta esegue l'autenticazione con il servizio di archiviazione hello. In questo modo si evita di esporre le chiavi dell'account di archiviazione in dispositivi non sicuri. Tuttavia, ciò comporta un sovraccarico importante per ruolo web hello perché tutti i dati di hello trasferiti tra il dispositivo dell'utente hello e hello servizio di archiviazione deve passare tramite ruolo web hello. È possibile evitare usando un ruolo web come un proxy per il servizio di archiviazione hello con accesso condiviso firme (SAS), talvolta in combinazione con le intestazioni di condivisione delle risorse Multiorigine (CORS). L'utilizzo di SAS, è possibile consentire che toomake dispositivo dell'utente richieste direttamente tooa archiviazione del servizio tramite un token di accesso limitato. Ad esempio, se un utente richiede un'applicazione tooyour foto tooupload, il ruolo web può generare e inviare dispositivo dell'utente toohello un token di firma di accesso condiviso che concede l'autorizzazione toowrite tooa specifico blob o contenitore per hello Avanti 30 minuti (dopo il quale hello token SAS scade).

In genere, un browser non sarà possibile JavaScript in una pagina ospitata da un sito Web in un dominio tooperform specifica le operazioni, ad esempio un dominio di tooanother "PUT". Ad esempio, se si ospita un ruolo web "contosomarketing.cloudapp.net" e si desidera toouse client side JavaScript tooupload un account di archiviazione blob tooyour "contosoproducts.blob.core.windows.net", hello del browser "stesso criterio di origine", questo non consentite operazione. Condivisione CORS è una funzionalità del browser che consente di hello dominio (in questo account di archiviazione hello case) toocommunicate toohello browser di destinazione che considera attendibili provenienti da richieste nel dominio di origine hello (in questo ruolo web hello case).  

Entrambe le tecnologie possono aiutare a evitare carichi o colli di bottiglia non necessari nell'applicazione Web.  

#### <a name="useful-resources"></a>Risorse utili
Per ulteriori informazioni sulla firma di accesso condiviso, vedere [firme di accesso condiviso, parte 1: hello comprensione del modello di firma di accesso condiviso](../storage-dotnet-shared-access-signature-part-1.md).  

Per ulteriori informazioni su CORS, vedere [il supporto di condivisione delle risorse Multiorigine (CORS) per servizi di archiviazione Azure hello](http://msdn.microsoft.com/library/azure/dn535601.aspx).  

### <a name="caching"></a>Memorizzazione nella cache
#### <a name="subheading7"></a>Recupero dei dati
In generale è meglio recuperare i dati da un servizio una sola volta e non ripetutamente. Considerare l'esempio hello di un'applicazione web MVC in esecuzione in un ruolo web che ha già recuperato un blob di 50MB da tooserve servizio di archiviazione hello come utente tooa contenuto. un'applicazione Hello potrebbe recuperare tale blob stesso ogni volta che un utente lo richiede o è possibile memorizzare nella cache, localmente toodisk e riutilizzo hello versione memorizzata nella cache per le richieste utente successive. Inoltre, ogni volta che un utente richiede dati hello, hello applicazione potrebbe eseguire GET con un'intestazione condizionale per l'ora di modifica, che potrebbe evitare di ottenere l'intero blob hello se non è stato modificato. È possibile applicare questo stesso tooworking modello con entità di tabella.  

In alcuni casi, si potrebbe decidere che l'applicazione può presupporre che blob hello rimane valido per un breve periodo dopo il recupero e durante questo periodo hello applicazione non è necessario che toocheck se blob hello è stata modificata.

Configurazione, ricerca e altri dati che vengono sempre utilizzati da un'applicazione hello sono ottimi candidati per la memorizzazione nella cache.  

Per un esempio di come tooget hello toodiscover le proprietà di un blob data dell'ultima modifica con .NET, vedere [Set e recuperare proprietà e i metadati](../blobs/storage-properties-metadata.md). Per altre informazioni sui download condizionali, vedere [Aggiornare una copia locale di un Blob in modo condizionale](http://msdn.microsoft.com/library/azure/dd179371.aspx).  

#### <a name="subheading8"></a>Caricamento dei dati in batch
In alcuni scenari dell'applicazione è possibile aggregare i dati localmente e caricarli periodicamente in un batch invece di caricare subito i singoli dati. Ad esempio, un'applicazione web può mantenere un file di log di attività: hello applicazione sia stato possibile caricare i dettagli di ogni attività di cui si verifica come un'entità di tabella (che richiede molte operazioni di archiviazione) o è stato possibile salvare i dettagli tooa locale file di log attività, quindi caricare periodicamente tutti i dettagli attività come un blob tooa file delimitato da virgole. Se ogni voce di log è di 1KB di dimensioni, è possibile caricare migliaia di una singola transazione "Put Blob" (è possibile caricare un blob di backup too64MB dimensioni in un'unica transazione). Naturalmente, se il computer locale hello arresti anomali caricamento toohello precedente, potenzialmente dati andranno persi alcuni log: sviluppatore dell'applicazione hello necessario progettare il possibilità hello del dispositivo client o caricare gli errori.  Se i dati di attività hello toobe scaricati per gli intervalli di tempo (attività non unico), sono consigliati BLOB su tabelle.

### <a name="net-configuration"></a>Configurazione .NET
Se tramite hello .NET Framework, in questa sezione sono elencate diverse impostazioni di configurazione rapida, che è possibile utilizzare i miglioramenti significativi delle prestazioni toomake.  In altri linguaggi, controllare toosee se applicano concetti simili nella lingua scelta.  

#### <a name="subheading9"></a>Aumento del limite di connessione predefinito
In .NET, hello seguente codice aumenta limite di connessione predefinito hello (che è in genere 2 in un ambiente client o in un ambiente server 10) too100. In genere, è necessario impostare hello valore tooapproximately hello il numero di thread utilizzati dall'applicazione.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

È necessario impostare il limite di connessioni hello prima di aprire tutte le connessioni.  

Per altri linguaggi di programmazione, vedere toodetermine documentazione del linguaggio che come connessione hello tooset limitare.  

Per ulteriori informazioni, vedere hello post di blog [servizi Web: connessioni simultanee](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx).  

#### <a name="subheading10"></a>Aumentare il numero minimo di thread di ThreadPool se si usa codice sincrono con attività asincrone
Questo codice aumenterà hello min thread del pool:  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

Per altre informazioni, vedere [Metodo ThreadPool.SetMinThreads](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx).  

#### <a name="subheading11"></a>Vantaggi della funzionalità Garbage Collection di .NET 4.5
Utilizzare .NET 4.5 o versioni successive per hello client applicazione tootake sfruttare i miglioramenti delle prestazioni in garbage collection per server.

Per ulteriori informazioni, vedere l'articolo hello [una panoramica dei miglioramenti delle prestazioni in .NET 4.5](http://msdn.microsoft.com/magazine/hh882452.aspx).  

### <a name="subheading12"></a>Parallelismo non associato
Parallelismo può essere la soluzione ideale per le prestazioni, prestare attenzione nell'utilizzare dati di tooupload o download parallelismo illimitata (nessun limite hello numero di thread e/o richieste in parallelo), utilizzando più thread di lavoro tooaccess più partizioni (contenitori, le code, o le partizioni di tabella) in hello stesso account di archiviazione o tooaccess più elementi in hello stessa partizione. Se il parallelismo di hello è illimitato, l'applicazione può superare la capacità del dispositivo client hello o hello obiettivi di scalabilità dell'account di archiviazione risulta latenze più lunghe e la limitazione delle richieste.  

### <a name="subheading13"></a>Librerie e strumenti client dell'archiviazione
Usare sempre strumenti e librerie client fornite da Microsoft più recenti di hello. Al momento della scrittura hello esistono le librerie client disponibili per .NET, Windows Phone, Windows Runtime, Java e C++, nonché librerie di anteprima per altri linguaggi. Inoltre, Microsoft ha rilasciato i cmdlet di PowerShell e i comandi CLI Azure da usare con l'archiviazione di Azure. Microsoft attivamente sviluppa questi strumenti nell'ottica delle prestazioni, li mantiene backup toodate con versioni più recenti del servizio hello e assicura che gestiscono molti dei hello rivelato internamente ottimali di prestazioni.  

### <a name="retries"></a>Tentativi
#### <a name="subheading14"></a>Limitazione/ServerBusy
In alcuni casi, hello servizio di archiviazione può limitare l'applicazione o potrebbe semplicemente tooserve Impossibile hello richiesta a causa di condizione temporanea toosome e restituire un messaggio "503 Server occupato" o "Timeout 500".  Questa situazione può verificarsi se l'applicazione sta per raggiungere uno degli obiettivi di scalabilità hello o sistema hello è ribilanciamento tooallow i dati partizionati per una velocità effettiva.  un'applicazione client Hello in genere deve ritentare l'operazione hello che causa questo errore: il tentativo di hello stessa richiesta in un secondo momento può avere esito positivo. Tuttavia, se il servizio di archiviazione hello è la limitazione delle richieste dell'applicazione perché è superiore a obiettivi di scalabilità o anche se il servizio hello richiesta hello tooserve riuscito per altri motivi, tentativi aggressive in genere eseguono peggiorare il problema hello. Per questo motivo, è consigliabile utilizzare un valore esponenziale Backoff (comportamento toothis predefinito di librerie client hello). Ad esempio, l'applicazione può riprovare l'operazione dopo 2 secondi, 4 secondi, 10 secondi, 30 secondi, dopo di che non effettua altri tentativi. Ciò comporta l'applicazione in modo significativo ridurre il carico del servizio hello anziché accrescere eventuali problemi.  

Si noti che gli errori di connettività possono ritentare immediatamente, perché non sono il risultato di hello della limitazione delle richieste e sono previsti toobe temporanei.  

#### <a name="subheading15"></a>Errori irreversibili
librerie client Hello siano gli errori sono in grado di ripetizione e non quelli attendibili. Se si scrive codice personalizzato nel servizio di archiviazione hello API REST, ciononostante, sono presenti alcuni errori che non devono ripetere: ad esempio, un 400 (Bad Request) risposta indica che un'applicazione hello client ha inviato una richiesta che non è stato possibile elaborare poiché è non è nel formato previsto. Inviare di nuovo la richiesta verrà generato hello stessa risposta ogni volta, pertanto non c'è alcun nuovo tentativo in corso il punto. Se si scrive codice personalizzato nel servizio di archiviazione hello API REST, tenere presente l'errore hello codici tooretry migliore Media e hello (o non) per ognuno di essi.  

#### <a name="useful-resources"></a>Risorse utili
Per ulteriori informazioni sui codici di errore di archiviazione, vedere [lo stato e codici di errore](http://msdn.microsoft.com/library/azure/dd179382.aspx) sul sito web di Microsoft Azure hello.  

## <a name="blobs"></a>Blobs
In aggiunta toohello procedure per consolidate [tutti i servizi](#allservices) descritto in precedenza, seguito hello procedure consolidate si applica in modo specifico il servizio di blob toohello.  

### <a name="blob-specific-scalability-targets"></a>Obiettivi di scalabilità specifici per BLOB
#### <a name="subheading46"></a>Accesso simultaneo di più client a un singolo oggetto
Se si dispone di un numero elevato di client che accedono contemporaneamente a un singolo oggetto, è necessario tooconsider per obiettivi di scalabilità di account di archiviazione e l'oggetto. numero esatto di Hello del client che possono accedere a un singolo oggetto verrà variano a seconda di fattori, ad esempio il numero di hello del client che richiedono contemporaneamente, l'oggetto hello dimensioni hello dell'oggetto di hello, le condizioni e così via della rete.

Se l'oggetto hello può essere distribuito tramite una rete CDN, ad esempio immagini o video servito da un sito Web, è consigliabile utilizzare una rete CDN. Vedere [qui](#subheading5).

In altri scenari, ad esempio le simulazioni di scientifiche in cui i dati hello sono riservati sono disponibili due opzioni. Hello viene innanzitutto toostagger accesso del carico di lavoro tali hello oggetto avviene in un periodo di tempo vs avviene contemporaneamente. In alternativa, è possibile copiare temporaneamente hello oggetto toomultiple gli account di archiviazione, aumentando quindi hello totale di IOPS per ogni oggetto e gli account di archiviazione. Nei test limitato è stato rilevato che le macchine virtuali circa 25 è stato possibile scaricare contemporaneamente un blob di 100GB in parallelo (ogni macchina virtuale è stata parallelizzazione download hello utilizzando 32 thread). Se si dispone di 100 client che richiedono oggetto hello tooaccess innanzitutto copiarlo tooa secondo account di archiviazione e quindi hanno hello primi 50 macchine virtuali accesso hello primo blob e hello secondo 50 macchine virtuali blob secondo hello accesso. I risultati variano a seconda del comportamento delle applicazioni. È quindi opportuno eseguire dei test in fase di progettazione. 

#### <a name="subheading16"></a>Larghezza di banda e operazioni per BLOB
È possibile leggere o scrivere singolo blob tooa al backup tooa massimo a 60 MB al secondo (si tratta di circa 480 Mbps che supera la capacità hello di molte reti di lato client (inclusi hello NIC fisica nel dispositivo client hello). Inoltre, un singolo blob supporta backup too500 richieste al secondo. Se si dispone di più client che richiedono tooread hello stesso blob e si potrebbero superare tali limiti, è consigliabile utilizzare una rete CDN per la distribuzione di blob hello.  

Per altre informazioni sulla velocità effettiva da raggiungere per i BLOB, vedere [Obiettivi di scalabilità e prestazioni di archiviazione di Azure](storage-scalability-targets.md).  

### <a name="copying-and-moving-blobs"></a>Copia e spostamento dei BLOB
#### <a name="subheading17"></a>Copia Blob
archiviazione Hello API REST versione 2012-02-12 introdotto BLOB toocopy possibilità utile di hello tra account: un'applicazione client può indicare toocopy servizio di archiviazione hello un blob da un'altra origine (possibilmente in un altro account di archiviazione) e quindi consentire hello servizio di eseguire la copia di hello in modo asincrono. Ciò può ridurre notevolmente la larghezza di banda hello necessario per un'applicazione hello quando si è la migrazione dei dati da altri account di archiviazione perché non è necessario toodownload e caricare i dati di hello.  

Una delle considerazioni, tuttavia, è che, durante la copia tra account di archiviazione, non è garantito tempo nel momento in cui si completerà copia hello. Se l'applicazione deve toocomplete un blob copiare rapidamente sotto controllo, potrebbe essere migliore blob di hello toocopy scaricarlo tooa macchina virtuale e quindi caricarli toohello destinazione.  Per la prevedibilità completa in questa situazione, verificare che copia hello viene eseguita da una macchina virtuale in esecuzione in hello stessa area di Azure, altrimenti le condizioni della rete può (e probabilmente verranno) interessano le prestazioni di copia.  Inoltre, è possibile monitorare lo stato di avanzamento hello di una copia asincrona a livello di codice.  

Si noti che copia all'interno di hello stesso account di archiviazione stessa vengono in genere completate rapidamente.  

Per altre informazioni, vedere [Copy Blob](http://msdn.microsoft.com/library/azure/dd894037.aspx).  

#### <a name="subheading18"></a>Usare AzCopy
il team di archiviazione di Azure Hello ha rilasciato uno strumento da riga di comando "AzCopy" ovvero ha significato toohelp con trasferimento molti BLOB to, from e tra account di archiviazione di massa.  Questo strumento è ottimizzato per questo scenario e può raggiungere elevate velocità di trasferimento.  Se ne consiglia l'uso negli scenari di caricamento, download e copia bulk. toolearn ulteriori informazioni e download, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).  

#### <a name="subheading19"></a>Servizio di importazione/esportazione di Azure
Per grandi volumi di dati (più di 1TB), hello archiviazione di Azure offre hello servizio importazione/esportazione, che consente di caricare e scaricare dall'archiviazione blob dalle unità disco rigida per la spedizione.  È possibile inserire i dati su un disco rigido e inviarlo tooMicrosoft per il caricamento o inviare dati di toodownload tooMicrosoft un disco rigido vuoto.  Per ulteriori informazioni, vedere [utilizzare hello servizio importazione/esportazione di Microsoft Azure tooTransfer dati tooBlob archiviazione](../storage-import-export-service.md).  Può essere molto più efficiente il caricamento e il download di questo volume di dati in rete hello.  

### <a name="subheading20"></a>Usare i metadati
servizio blob Hello supporta le richieste head, che possono includere i metadati relativi blob hello. Ad esempio, se l'applicazione è necessario dati EXIF hello fuori una foto, Impossibile recuperare la foto hello e decomprimerlo. toosave della larghezza di banda e migliorare le prestazioni, l'applicazione potrebbe archiviare i dati EXIF hello nei metadati del blob hello quando un'applicazione hello caricato foto hello: è quindi possibile recuperare dati EXIF hello nei metadati usando solo una richiesta HEAD, risparmiando larghezza di banda significativo e il tempo di elaborazione hello necessarie tooextract hello dati EXIF è di lettura blob di hello ogni ora. Questo potrebbe essere utile negli scenari in cui è necessario solo metadati hello e non hello contenuto completo di un blob.  Si noti che possono essere archiviati solo 8 KB di metadati per ogni blob (servizio hello non accetterà un toostore richiesta maggiore), pertanto se i dati di hello non rientrano in tale dimensione, potrebbe non essere in grado di toouse questo approccio.  

Per un esempio di come tooget metadati di un blob utilizzando .NET, vedere [Set e recuperare proprietà e i metadati](../blobs/storage-properties-metadata.md).  

### <a name="uploading-fast"></a>Caricamento rapido
BLOB tooupload veloce, hello prima domanda tooanswer è: si caricamento uno blob o molti?  Utilizzare hello seguito indicazioni toodetermine hello metodo corretto toouse a seconda dello scenario.  

#### <a name="subheading21"></a>Caricamento rapido di un BLOB di grandi dimensioni
tooupload un unico grande blob rapidamente, l'applicazione client deve caricare relativi blocchi o pagine in parallelo (da attenzione di obiettivi di scalabilità hello per ogni BLOB e account di archiviazione hello nel suo complesso).  Si noti che hello ufficiale fornita da Microsoft RTM archiviazione librerie Client (.NET, Java) hello possibilità toodo questo.  Per ognuna delle librerie di hello, usare hello sotto livello hello tooset di oggetto specificato o la proprietà di concorrenza:  

* .NET: Set ParallelOperationThreadCount su un toobe oggetto BlobRequestOptions utilizzato.
* Java/Android: Usare BlobRequestOptions.setConcurrentRequestCount()
* Node.js: Utilizzare parallelOperationThreadCount in entrambe le opzioni di richiesta hello o nel servizio blob hello.
* C++: Metodo blob_request_options:: set_parallelism_factor utilizzare hello.

#### <a name="subheading22"></a>Caricamento rapido di più BLOB
tooupload molti BLOB rapidamente, caricare i BLOB in parallelo. Questo è più veloce rispetto al caricamento BLOB singolo in una fase di operazioni di caricamento parallelo di blocco perché distribuisce hello caricamento tra più partizioni hello del servizio di archiviazione. Un singolo BLOB supporta una velocità effettiva di soli 60 MB/secondo (circa 480 Mbps). In fase di hello di scrittura, un account LRS basata negli Stati Uniti supporta fino a too20 in ingresso Gbps che è molto più di velocità effettiva di hello è supportata da un singolo blob.  [AzCopy](#subheading18) esegue i caricamenti in parallelo per impostazione predefinita ed è consigliato per questo scenario.  

### <a name="subheading23"></a>Scelta del tipo corretto di hello di blob
Archiviazione di Azure supporta due tipi di BLOB: BLOB di *pagine* e BLOB in *blocchi*. Per uno scenario di utilizzo specifico, la scelta del tipo di blob influirà hello prestazioni e scalabilità della soluzione. BLOB in blocchi sono appropriati quando si desidera grandi quantità di tooupload di dati in modo efficiente: ad esempio, un'applicazione client potrebbe essere necessario foto tooupload o archiviazione tooblob video. BLOB di pagine sono appropriati se un'applicazione hello deve tooperform scritture casuali sui dati hello: ad esempio, dischi rigidi virtuali di Azure vengono archiviati come BLOB di pagine.  

Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).  

## <a name="tables"></a>Tabelle
In aggiunta toohello procedure per consolidate [tutti i servizi](#allservices) descritto in precedenza, seguente hello procedure consolidate si applicano specificatamente toohello servizio di tabella.  

### <a name="subheading24"></a>Obiettivi di scalabilità specifici per tabelle
Limitazioni della larghezza di banda di toohello aggiunta di un account di archiviazione intera, tabelle disporre hello seguente limite di scalabilità specifici.  Si noti che il sistema hello sarà il bilanciamento del carico man mano che aumenta il traffico, ma se il traffico è improvvisi, potrebbe non essere in grado di tooget il volume di velocità effettiva immediatamente.  Se il modello è picchi, è necessario prevedere la limitazione delle richieste di toosee e/o timeout durante hello burst come servizio di archiviazione hello automaticamente la tabella bilancia il carico.  Aumentando lentamente in genere è migliori risultati quanto consente di bilanciare tooload ora sistema di hello in modo appropriato.  

#### <a name="entities-per-second-account"></a>Entità al secondo (account)
limite di scalabilità Hello per accedere alle tabelle sia attivo too20, 000 entità (1KB ogni) al secondo per un account.  In generale ogni entità inserita, aggiornata, eliminata o analizzata viene presa in considerazione ai fini del calcolo per l'obiettivo.  Quindi, un inserimento batch che contiene 100 entità conta come 100 entità.  Una query che analizza 1000 entità e ne restituisce 5 conta come 1000 entità.  

#### <a name="entities-per-second-partition"></a>Entità al secondo (partizione)
All'interno di una singola partizione, hello obiettivo di scalabilità per l'accesso alle tabelle è 2.000 entità (1KB ogni) al secondo, utilizzando hello conteggio stesso come descritto nella sezione precedente hello.  

### <a name="configuration"></a>Configurazione
In questa sezione sono elencate diverse impostazioni di configurazione rapida, che è possibile utilizzare i miglioramenti significativi delle prestazioni toomake nel servizio tabelle hello:  

#### <a name="subheading25"></a>Usare JSON
A partire dalla versione del servizio di archiviazione 2013-08-15, del servizio tabelle hello supporta l'utilizzo di JSON anziché formato basato su XML AtomPub hello per il trasferimento di dati della tabella. Questo può ridurre le dimensioni del payload al 75% e può migliorare significativamente le prestazioni di hello dell'applicazione.

Per ulteriori informazioni, vedere hello post [le tabelle di Microsoft Azure: Introduzione a JSON](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) e [formato di Payload per operazioni del servizio tabelle](http://msdn.microsoft.com/library/azure/dn535600.aspx).

#### <a name="subheading26"></a>Disattivazione di Nagle
Algoritmo Nagle viene ampiamente implementato nelle reti TCP/IP come prestazioni della rete tooimprove un mezzo. Tuttavia, non è la soluzione ottimale in tutti gli scenari (ad esempio, gli ambienti ad alta interazione). Per l'archiviazione di Azure, algoritmo Nagle ha un impatto negativo sulle prestazioni di hello dei servizi di tabella e coda toohello le richieste ed è consigliabile disabilitarla se possibile.  

Per ulteriori informazioni, vedere il post di blog [l'algoritmo Nagle non è descrittivo verso le richieste di piccole dimensioni](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), che spiega perché algoritmo Nagle interagisce con la tabella e coda delle richieste e viene illustrato come toodisable nel client applicazione.  

### <a name="schema"></a>Schema
Modalità di eseguire query sui dati e rappresentano è hello principali un fattore che influisce sulle prestazioni di hello del servizio tabelle hello. Ogni applicazione è diversa, ma in questa sezione vengono descritte alcune procedure comprovate generali relative a:  

* Progettazione della tabella
* Query efficaci
* Aggiornamenti dei dati efficaci  

#### <a name="subheading27"></a>Tabelle e partizioni
Le tabella sono divise in partizioni. Ogni entità archiviate in una partizione condivisioni hello stessa chiave di partizione e ha un tooidentify chiave di riga univoco in tale partizione. Le partizioni offrono dei vantaggi ma introducono anche dei limiti di scalabilità.  

* Vantaggi: È possibile aggiornare le entità in hello stessa partizione in una transazione atomica singola, batch che contiene le operazioni di archiviazione separata too100 (limite di dimensione totale di 4MB). Supponendo che hello stesso numero di entità toobe recuperati, è anche possibile eseguire query dei dati all'interno di una singola partizione in modo più efficiente rispetto ai dati che si estende su partizioni (lettura tuttavia in per ulteriori informazioni sull'esecuzione di query dei dati di tabella).
* Limite di scalabilità: tooentities di accesso archiviati in una singola partizione non può essere con bilanciamento del carico perché le partizioni supportano le transazioni batch atomiche. Per questo motivo, obiettivo di scalabilità hello per una partizione singola tabella è minore rispetto al livello del servizio tabelle hello nel suo complesso.  

A causa di queste caratteristiche di tabelle e partizioni, è necessario adottare hello seguenti principi di progettazione:  

* Dati che l'applicazione client spesso aggiornati o eseguire una query nella stessa unità logica di lavoro deve essere collocato nello hello hello stessa partizione.  Può trattarsi di perché l'applicazione sta aggregando scritture o perché si vuole usare tootake operazioni batch atomiche.  Inoltre, le query sui dati in una singola partizione possono essere eseguite in modo più efficace con un'unica query rispetto a quelle sui dati in più partizioni.
* I dati dell'applicazione client non inserimento/aggiornamento o eseguire una query nella stessa unità logica di lavoro (singola query o aggiornamento batch) deve essere collocato nello hello partizioni diverse.  Una nota importante non è che sono toohello alcuna limitazione del numero di chiavi di partizione in una singola tabella, in modo da disporre di milioni di chiavi di partizione non è un problema e non avrà impatto sulle prestazioni.  Ad esempio, se l'applicazione è un sito Web comuni con account di accesso utente, utilizzando hello Id utente come chiave di partizione hello potrebbe essere una buona scelta.  

#### <a name="hot-partitions"></a>Partizioni critiche
Una partizione a caldo è una che riceve una percentuale sproporzionata dell'account di tooan traffico hello e non può essere con carico bilanciato perché è una singola partizione.  In generale, le partizioni critiche vengono create in uno di questi due modi:  

##### <a name="subheading28"></a>Modelli Solo accodamenti e Solo anteposizioni
modello "Solo aggiungere" Hello è uno in cui tutte o quasi sempre di hello traffico tooa dato PK aumenta, mentre diminuisce toohello secondo ora corrente.  Un esempio è se l'applicazione utilizzata hello data corrente come chiave di partizione per i dati di log.  Di conseguenza, tutti gli inserimenti hello passare toohello ultima partizione nella tabella e il sistema di hello non è possibile bilanciare il carico perché sono tutti di scritture hello corso toohello fine della tabella.  Se il volume di hello della partizione toothat traffico supera la destinazione di hello scalabilità a livello di partizione, quindi comporterà la limitazione delle richieste.  È meglio tooensure che il traffico viene inviato toomultiple partizioni, hello bilanciamento carico di tooenable delle richieste tra la tabella.  

##### <a name="subheading29"></a>Dati con traffico elevato
Se i risultati di schema di partizionamento in una singola partizione che include solo i dati molto più utilizzati rispetto alle altre partizioni, è possibile vedere anche la limitazione delle richieste poiché tale partizione si avvicina alla destinazione di hello scalabilità per una singola partizione.  È meglio toomake assicurarsi che i risultati di schema di partizione in nessuna singola partizione vicine obiettivi di scalabilità di hello.  

#### <a name="querying"></a>Query
Questa sezione descrive procedure comprovate per l'esecuzione di query del servizio tabelle hello.  

##### <a name="subheading30"></a>Ambito delle query
Esistono diversi modi toospecify hello gamma tooquery di entità.  di seguito Hello è una descrizione degli utilizzi di hello di ognuno.  

In generale, evitare di analisi (maggiore di una singola entità di query), ma se è necessario eseguire l'analisi, provare a tooorganize i dati in modo che l'analisi di recuperano dati hello che necessario senza restituzione di entità che non è necessario ingenti o di analisi.  

###### <a name="point-queries"></a>Query di tipo punto
Una query di tipo punto recupera esattamente un'entità. Ciò avviene specificando la chiave di partizione hello e chiave di riga del tooretrieve entità hello. Queste query sono molto efficaci e vanno usate quando possibile.  

###### <a name="partition-queries"></a>Query sulle partizioni
Una query sulle partizioni recupera un set di dati che condivide una chiave di partizione comune. Query hello in genere, specifica un intervallo di valori di chiave di riga o un intervallo di valori per alcune proprietà dell'entità nella chiave di partizione tooa aggiunta. Queste query sono meno efficaci delle query di tipo punto e devono essere usate in casi limitati.  

###### <a name="table-queries"></a>Query sulle tabelle
Una query sulle tabelle recupera un set di entità che non condivide una chiave di partizione comune. Queste query non sono efficaci e, se possibile, vanno evitate.  

##### <a name="subheading31"></a>Densità delle query
Un altro fattore chiave per l'efficienza di query è il numero di hello di entità restituito come numero toohello confrontati di entità restituita imposta hello toofind sottoposte ad analisi. Se l'applicazione esegue una query di tabella con un filtro per un valore della proprietà che solo 1% di hello dati condivisioni, hello query analizza 100 entità per ogni uno entità che restituisce. Hello obiettivi di scalabilità di tabella descritti in precedenza tutti riferimento toohello numero di entità analizzate e non hello numero di entità restituite: una densità bassa query può causare facilmente hello tabella servizio toothrottle l'applicazione perché è necessario eseguire l'analisi moltissimi si sta cercando entità hello tooretrieve di entità.  Vedere di seguito la sezione hello in [denormalizzazione](#subheading34) per ulteriori informazioni su come tooavoid questo.  

##### <a name="limiting-hello-amount-of-data-returned"></a>Limitazione della quantità di dati restituito hello
###### <a name="subheading32"></a>Filtri
Se si sa che una query verrà restituite le entità che non è necessario nell'applicazione client hello, considerare l'utilizzo di una dimensione di hello tooreduce di filtro di hello restituito set. Durante le entità hello restituito non toohello client ancora conteggiati per hello limiti di scalabilità, le prestazioni dell'applicazione verranno migliorare a causa delle dimensioni del payload rete hello ridotto e un numero ridotto di entità che l'applicazione client deve elaborare hello .  Vedere in precedenza nota in [Query densità](#subheading31), tuttavia: obiettivi di scalabilità hello correlare toohello numero di entità analizzate, pertanto una query che filtra molte entità ancora potrebbe verificarsi di limitazione, anche se vengono restituite alcune entità.  

###### <a name="subheading33"></a>Proiezione
Se l'applicazione client deve solo un set limitato di proprietà di entità hello nella tabella, è possibile utilizzare una dimensione di hello toolimit proiezione di hello ha restituito il set di dati. Come con l'applicazione di filtri, in questo modo il carico di rete tooreduce e l'elaborazione dei client.  

##### <a name="subheading34"></a>Denormalizzazione
A differenza di lavorare con i database relazionali, hello procedure comprovate per le query in modo efficiente i dati della tabella causare toodenormalizing i dati. Vale a dire la duplicazione di hello stessi dati in più entità (uno per ogni chiave è possibile utilizzare dati hello toofind) numero hello toominimize di entità che una query è necessario eseguirne la scansione toofind hello dati hello client esigenze, anziché un numero elevato di entità toofind tooscan l'applicazione necessita di dati Hello.  Ad esempio, in un sito Web di e-commerce, si consiglia un ordine sia all'ID cliente hello toofind (trarne gli ordini del cliente) e data hello (trarne gli ordini in una data).  Nell'archiviazione tabelle, è migliore entità di hello toostore (o un tooit riferimento) due volte, una volta con il nome di tabella, PK e RK ricerca toofacilitate dall'ID cliente, una volta toofacilitate rilevarlo data hello.  

#### <a name="insertupdatedelete"></a>Inserimento/aggiornamento/eliminazione
Questa sezione descrive procedure comprovate per la modifica di entità archiviata nel servizio tabelle hello.  

##### <a name="subheading35"></a>Creazione di batch
Le transazioni batch sono noti come entità gruppo di transazioni (ETG) in archiviazione di Azure; tutte le operazioni all'interno di un ETG hello devono trovarsi in una singola partizione in una singola tabella. Dove possibile, utilizzare ETGs tooperform inserimenti, aggiornamenti ed eliminazioni in batch. Questo riduce il numero di hello di round trip tra il server di toohello applicazioni client, riduce il numero di hello di transazione fatturabile (un ETG viene considerato come una singola transazione ai fini della fatturazione e può contenere un massimo di operazioni di archiviazione too100) e l'esecuzione atomico aggiornamenti (tutte le operazioni di esito positivo o tutte esito negativo all'interno di un ETG). Gli ambienti con latenze elevate come i dispositivi mobili possono trarre grandi vantaggi dall'uso delle ETG.  

##### <a name="subheading36"></a>Upsert
Usare le operazioni della tabella **Upsert** quando possibile. Esistono due tipi di **Upsert**, entrambi più efficaci di una tradizionale operazione di **inserimento** e **aggiornamento**:  

* **InsertOrMerge**: usare questa opzione quando si desidera un subset di proprietà dell'entità hello tooupload, ma non si è certi di fatto entità hello esiste già. Se hello entità esiste, questa chiamata Aggiorna proprietà hello incluse in hello **Upsert** operazione e lascia tutte le proprietà esistenti, così come sono, se hello entità non esiste, inserisce una nuova entità hello. Si tratta di proiezione toousing simili in una query, in quanto è necessario solo proprietà hello tooupload che sta modificando.
* **InsertOrReplace**: usare questa opzione quando si desidera tooupload un'entità completamente nuova, ma non si è certi se esiste già. È necessario utilizzare questa operazione solo quando si conosce tale hello appena caricato entità sia completamente corretto perché sovrascrive completamente entità precedente hello. Ad esempio, si desidera entità hello tooupdate che archivia la posizione corrente dell'utente indipendentemente dal fatto che un'applicazione hello è archiviati in precedenza dati sulla località per utente hello. nuova entità di percorso Hello è stata completata e le informazioni di qualsiasi entità precedente non è necessaria.

##### <a name="subheading37"></a>Archiviazione di serie di dati in una singola entità
In alcuni casi, un'applicazione archivia una serie di dati che è spesso necessario tooretrieve in un'unica: ad esempio, un'applicazione potrebbe tenere traccia dell'utilizzo della CPU nel tempo in ordine tooplot un grafico di dati hello in sequenza da hello ultime 24 ore. Un approccio è l'entità di una tabella toohave all'ora, con ogni entità che rappresenta un'ora specifica e l'archiviazione di utilizzo della CPU hello per quell'ora. tooplot questi dati, un'applicazione hello devono entità hello tooretrieve contenente dati hello hello 24 ore più recente.  

In alternativa, l'applicazione potrebbe archiviare utilizzo hello della CPU per ogni ora come una proprietà di una singola entità separata: tooupdate ogni ora, l'applicazione può utilizzare una sola **InsertOrMerge Upsert** chiamare valore hello tooupdate per hello ora più recente. dati hello tooplot, un'applicazione hello sufficiente tooretrieve una singola entità anziché 24, rendendo per una query molto efficiente (vedere sopra discussione su [ambito query](#subheading30)).

##### <a name="subheading38"></a>Archiviazione di dati strutturati in BLOB
A volte sembra che i dati strutturati debbano essere inseriti nelle tabelle, tuttavia gli intervalli delle entità vengono sempre recuperati insieme e possono essere inseriti in batch.  Per spiegarlo efficacemente, si prenda l'esempio di un file di log.  In questo caso è possibile creare in batch e inserire diversi minuti di log. Questi minuti di log vengono anche recuperati tutti in una volta.  In questo caso, per le prestazioni, è preferibile BLOB toouse anziché le tabelle, poiché è possibile ridurre significativamente il numero di hello di scritto e restituiti gli oggetti, nonché in genere hello numero di richieste che devono.  

## <a name="queues"></a>Code
In aggiunta toohello procedure per consolidate [tutti i servizi](#allservices) descritto in precedenza, seguito hello procedure consolidate si applica specificatamente toohello servizio di Accodamento.  

### <a name="subheading39"></a>Limiti di scalabilità
Una singola coda può elaborare circa 2000 messaggi (da 1 KB ciascuno) al secondo (in questo caso, i metodi AddMessage, GetMessage e DeleteMessage vengono considerati come singoli messaggi). Se è insufficiente per l'applicazione, è necessario utilizzare più code e distribuire messaggi hello su di essi.  

È possibile visualizzare gli obiettivi di scalabilità correnti nella pagina [Obiettivi di scalabilità e prestazioni di archiviazione Azure](storage-scalability-targets.md).  

### <a name="subheading40"></a>Disattivazione di Nagle
Vedere la sezione hello nella configurazione della tabella che descrive l'algoritmo Nagle di hello, l'algoritmo Nagle hello è in genere non valida per le prestazioni di hello delle richieste di coda e, è consigliabile disabilitarla.  

### <a name="subheading41"></a>Dimensioni del messaggio
Le prestazioni e la scalabilità della coda diminuiscono con l'aumentare delle dimensioni del messaggio. È consigliabile inserire solo hello hello ricevitore esigenze in un messaggio.  

### <a name="subheading42"></a>Recupero in batch
È possibile recuperare i messaggi too32 da una coda in un'unica operazione. Questo può ridurre il numero di hello di round trip dall'applicazione client hello, che risulta particolarmente utile per gli ambienti, ad esempio dispositivi mobili, ad alta latenza.  

### <a name="subheading43"></a>Intervallo di polling della coda
La maggior parte delle applicazioni il polling per i messaggi da una coda, che può essere una delle origini più grande di hello delle transazioni per l'applicazione. Selezionare l'intervallo di polling in modo appropriato: esecuzione troppo frequente del polling potrebbe causare l'applicazione tooapproach obiettivi di scalabilità hello per coda hello. Tuttavia, 200.000 transazioni per $0,01 (in fase di hello di scrittura), un singolo processore il polling di una volta al secondo per un mese sarebbe costo inferiore a 15 centesimi così costi non è in genere un fattore che influisce sulla scelta dell'intervallo di polling.  

Per informazioni aggiornate sui costi, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).  

### <a name="subheading44"></a>UpdateMessage
È possibile utilizzare **UpdateMessage** tooincrease hello invisibilità timeout tooupdate informazioni sullo stato o di un messaggio. Durante questa operazione è utile, tenere presente che ogni **UpdateMessage** operazione viene conteggiato obiettivo di scalabilità hello. Tuttavia, può trattarsi di un approccio molto più efficiente rispetto a un flusso di lavoro che passa un processo da una coda toohello successivamente, quando viene completato ogni passaggio del processo di hello. Utilizzo di hello **UpdateMessage** operazione consente il messaggio toohello stato processo di applicazione toosave hello e quindi continuare a utilizzare, anziché nuovamente Accodamento messaggio hello del passaggio successivo di hello del processo di hello ogni volta che viene completata una fase.  

Per ulteriori informazioni, vedere l'articolo hello [procedura: modificare hello contenuto di un messaggio in coda](../queues/storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message).  

### <a name="subheading45"></a>Architettura dell'applicazione
È consigliabile utilizzare le code toomake l'architettura dell'applicazione scalabile. esempio Hello sono elencati alcuni possibili utilizzi toomake code dell'applicazione più scalabile:  

* È possibile usare i backlog di toocreate code di lavoro per l'elaborazione e uniformare i carichi di lavoro nell'applicazione. Ad esempio, è Impossibile mettere in coda le richieste di lavoro con utilizzo intensivo del processore tooperform di utenti, ad esempio il ridimensionamento delle immagini caricate.
* È possibile utilizzare parti toodecouple code dell'applicazione in modo da poter ridimensionare in modo indipendente. Ad esempio, un front-end Web può inserire i risultati di un sondaggio degli utenti in una coda per l'analisi e l'archiviazione successive. È possibile aggiungere che ulteriori tooprocess di istanze di ruolo worker hello dati della coda in base alle esigenze.  

## <a name="conclusion"></a>Conclusioni
In questo articolo illustrate alcune delle più comune, hello rivelati procedure consigliate per ottimizzare le prestazioni quando si utilizza l'archiviazione di Azure. Abbiamo incoraggiare la propria applicazione in ognuno degli hello sopra consigliate ogni tooassess sviluppatore dell'applicazione e considerare agisce di hello indicazioni tooget ottime prestazioni per le applicazioni che utilizzano l'archiviazione di Azure.
