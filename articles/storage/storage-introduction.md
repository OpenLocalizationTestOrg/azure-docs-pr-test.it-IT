---
title: aaaIntroduction tooAzure archiviazione | Documenti Microsoft
description: Panoramica dell'archiviazione di Azure, archiviazione dei dati online di Microsoft nel cloud hello. Informazioni su come toouse hello migliore soluzione di archiviazione cloud disponibili nelle applicazioni.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Introduzione tooMicrosoft di archiviazione di Azure

## <a name="overview"></a>Panoramica
Archiviazione di Azure è una soluzione di archiviazione cloud hello per le moderne applicazioni che si basano su esigenze di hello toomeet scalabilità dei clienti, disponibilità e durata. Questo articolo offre a sviluppatori, professionisti IT e decision maker aziendali informazioni su:

* Che cos'è Archiviazione di Azure e come è possibile usarlo nelle applicazioni cloud, mobili, server e desktop
* I tipi di dati è possibile archiviare con servizi di archiviazione Azure hello: blob di dati (oggetto), dati di tabella di database NoSQL, messaggi in coda e le condivisioni file.
* La modalità di gestione di accesso ai dati tooyour in archiviazione di Azure
* Come vengono resi durevoli i dati di Archiviazione di Azure grazie a ridondanza e replica
* Dove toobuild Avanti toogo la prima applicazione di archiviazione di Azure

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Per informazioni dettagliate su strumenti, librerie e altre risorse per l'utilizzo di Archiviazione di Azure, vedere la sezione [Passaggi successivi](#next-steps) di seguito.

## <a name="what-is-azure-storage"></a>Informazioni su Archiviazione di Azure
Il cloud computing consente di disporre di nuovi scenari per le applicazioni che richiedono un sistema di archiviazione scalabile, durevole e a disponibilità elevata per i propri dati. Questo è esattamente lo scopo per cui è stato sviluppato Archiviazione di Microsoft Azure. In aggiunta toomaking è possibile per gli sviluppatori toobuild applicazioni su larga scala toosupport nuovi scenari, archiviazione di Azure fornisce inoltre foundation archiviazione hello per macchine virtuali di Azure, un ulteriore affidabilità tooits la testimonianza.

Archiviazione di Azure è altamente scalabile, pertanto è possibile archiviare ed elaborare centinaia di terabyte di scenari di dati toosupport hello dati necessari per l'analisi di scientifici, finanziari e applicazioni multimediali. Oppure è possibile archiviare hello piccole quantità di dati necessari per un sito Web di piccole aziende. Ogni volta che sono comprese le proprie esigenze, si paga solo per i dati di hello che si desidera archiviare. In Archiviazione di Azure sono al momento archiviate decine di migliaia di miliardi di oggetti univoci dei clienti e sono gestiti in media milioni di richieste al secondo.

Archiviazione di Azure è elastico, pertanto è possibile progettare applicazioni per un pubblico globale di grandi dimensioni e scalare le applicazioni in base alle esigenze, sia in termini di quantità hello dei dati archiviati e hello numero di richieste eseguite su di essa. Il cliente paga solo per ciò che utilizza e solo quando lo utilizza.

Archiviazione di Azure utilizza un sistema di partizionamento automatico che applica automaticamente il bilanciamento del carico dei dati in base al traffico. Ciò significa che come hello richieste per l'aumento di applicazione, archiviazione di Azure alloca automaticamente hello delle risorse appropriate toomeet li.

Archiviazione di Azure è accessibile ovunque nel mondo hello, da qualsiasi tipo di applicazione, se è in esecuzione nel cloud hello, sul desktop di hello, in un server locale o di un mobile o un dispositivo tablet. È possibile utilizzare l'archiviazione di Azure negli scenari per dispositivi mobili in cui un'applicazione hello archivia un subset di dati nel dispositivo hello e Sincronizza con un set completo di dati archiviati nel cloud hello.

Archiviazione di Azure supporta client che usano sistemi operativi di vario tipo (tra cui Windows e Linux) e numerosi linguaggi di programmazione (tra cui .NET, Java, Node.js, Python, Ruby, PHP, C++ e linguaggi di programmazione per dispositivi mobili) per facilitare le operazioni di sviluppo. Archiviazione di Azure espone anche le risorse di dati tramite le API REST semplice, sono disponibili tooany client in grado di inviare e ricevere dati tramite HTTP/HTTPS.

L'archiviazione premium di Azure offre prestazioni elevate, supporto disco a bassa latenza per carichi di lavoro con uso intensivo di I/O in esecuzione su Macchine virtuali di Azure. Con l'archiviazione Premium di Azure, è possibile collegare più macchina di virtuale tooa di dischi dati persistenti e configurarli toomeet requisiti di prestazioni. Ogni disco di dati è supportato da un disco SSD nell'archiviazione premium di Azure per le massime prestazioni di I/O. Per altre informazioni, vedere [Archiviazione premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md) .

## <a name="introducing-hello-azure-storage-services"></a>Introduzione a servizi di archiviazione Azure hello
Archiviazione di Azure fornisce i seguenti quattro servizi hello: Blob di archiviazione, archiviazione tabelle, l'archiviazione delle code e archiviazione di File.

* L'archiviazione BLOB archivia dati oggetto non strutturati. Un BLOB può essere qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche noto tooas archiviazione di oggetti.
* L'archiviazione tabelle archivia set di dati strutturati. Archiviazione tabelle è un archivio di dati degli attributi di chiave NoSQL, che consente lo sviluppo rapido e quantità toolarge l'accesso rapido di dati.
* L'archiviazione code offre un sistema di messaggistica affidabile per l'elaborazione del flusso di lavoro e per la comunicazione tra componenti dei servizi cloud.
* Archiviazione di file offre spazio di archiviazione condiviso per le applicazioni legacy utilizzando il protocollo SMB standard di hello. Macchine virtuali di Azure e servizi cloud possono condividere i dati di file tra i componenti delle applicazioni tramite condivisioni montate e applicazioni locali possono accedere ai dati dei file in una condivisione tramite l'API REST del servizio File hello.

Un account di archiviazione di Azure è un account sicuro che consente di accedere ai tooservices in archiviazione di Azure. L'account di archiviazione fornisce lo spazio dei nomi univoci di hello per le risorse di archiviazione. immagine di Hello seguente mostra le relazioni di hello tra le risorse di archiviazione di Azure hello in un account di archiviazione:

![Risorse di archiviazione di Azure](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Archiviazione BLOB
Per gli utenti con grandi quantità di oggetti non strutturati toostore di dati nel cloud hello, archiviazione Blob offre una soluzione economica e scalabile. È possibile utilizzare contenuto toostore di archiviazione Blob, ad esempio:

* Documenti
* Dati dei social network come foto, video, musica e blog
* Backup di file, computer, database e dispositivi
* Immagini e testo per applicazioni Web
* Dati di configurazione per applicazioni cloud
* Big Data, come log e altri set di dati di grandi dimensioni

Ogni BLOB è organizzato in un contenitore. I contenitori forniscono anche un toogroups di criteri protezione tooassign utile di oggetti. Un account di archiviazione può contenere qualsiasi numero di contenitori e un contenitore può contenere qualsiasi numero di BLOB, di limite di capacità di 500 TB toohello hello dell'account di archiviazione.

Gli archivi BLOB offrono tre tipi di BLOB: i BLOB in blocchi , i BLOB di accodamento e i BLOB di pagine (dischi).

* I BLOB in blocchi sono ottimizzati per lo streaming e l'archiviazione di oggetti cloud e sono una soluzione adatta per l'archiviazione di documenti, file multimediali, backup e così via.
* Aggiungere BLOB BLOB tooblock simile, ma sono ottimizzati per operazioni di aggiunta. È possibile aggiornare un blob di aggiunta solo aggiungendo un nuovo end toohello blocco. Aggiungere i BLOB sono una buona scelta per scenari quali la registrazione, in cui i nuovi dati devono toobe scritti solo toohello fine del blob hello.
* BLOB di pagine sono ottimizzati per che rappresentano i dischi di IaaS e supporto casuale scrive e può essere up too1 TB nella dimensione. Un disco IaaS collegato a una rete di macchine virtuali Azure è un disco rigido virtuale archiviato come BLOB di pagine.

Per grandi set di dati in cui i vincoli di rete assicurarsi di caricare o scaricare l'archiviazione dei dati tooBlob rete hello poco realistico, è possibile fornire un tooimport tooMicrosoft unità disco rigido o esportare i dati direttamente dal centro dati hello. Vedere [utilizzare hello servizio importazione/esportazione di Microsoft Azure tooTransfer dati tooBlob archiviazione](storage-import-export-service.md).

## <a name="table-storage"></a>Archiviazione tabelle

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Le applicazioni moderne spesso richiedono l'utilizzo di archivi dati con scalabilità e flessibilità maggiori di quelli delle versioni precedenti del software. Archiviazione tabelle offre l'archiviazione a disponibilità elevata, altamente scalabile, in modo che l'applicazione è possibile scalare automaticamente richiesta utente toomeet. Archiviazione tabelle è l'archivio di chiavi/attributi NoSQL di Microsoft. Ha una struttura senza schema ed è quindi diverso dai database relazionali tradizionali. Con un archivio dati schemaless, è facile tooadapt i dati come hello necessita di evolve l'applicazione. Archiviazione tabelle è facile toouse, pertanto gli sviluppatori possono creare applicazioni rapidamente. Accesso toodata è veloce e conveniente per tutti i tipi di applicazioni.  L'archiviazione tabelle presenta in genere costi decisamente più bassi rispetto alle soluzioni SQL tradizionali per volumi simili di dati.

Archiviazione tabelle è un archivio chiave-attributo, ovvero ogni valore di una tabella è archiviato con un nome di proprietà tipizzato nome della proprietà Hello è utilizzabile per l'impostazione di criteri di selezione e filtro. Una raccolta di proprietà con i rispettivi valori costituisce un'entità. Poiché l'archiviazione tabelle è schemaless, due entità in hello stessa tabella può contenere diverse raccolte di proprietà e tali proprietà possono essere di tipi diversi.

È possibile utilizzare una tabella archiviazione toostore flessibile set di dati, ad esempio i dati utente per applicazioni web, rubriche, informazioni sul dispositivo e qualsiasi altro tipo di metadati che richiede il servizio.  È possibile archiviare qualsiasi numero di entità in una tabella e un account di archiviazione può contenere qualsiasi numero di tabelle, di limite di capacità toohello hello dell'account di archiviazione.

Come BLOB e code, gli sviluppatori possono gestire e accedere all'archiviazione tabelle utilizzando i protocolli REST standard, tuttavia archivio tabelle anche supporta un sottoinsieme del protocollo OData hello, semplificando le operazioni avanzate funzionalità di query e l'abilitazione di JSON e AtomPub (basato su XML) formati.

Per le applicazioni basate su Internet oggi, nei database NoSQL come archiviazione tabella offrono un diffuso tootraditional alternativo database relazionali.

## <a name="queue-storage"></a>Archiviazione code
Durante la progettazione di applicazioni scalabili, i componenti dell'applicazione vengono spesso separati, per poter essere scalati in modo indipendente. L'archiviazione delle code fornisce una soluzione di messaggistica affidabile per la comunicazione asincrona tra componenti dell'applicazione, se sono in esecuzione nel cloud hello, sul desktop di hello, in un server locale o in un dispositivo mobile. Supporta inoltre la gestione di attività asincrone e la creazione di flussi di lavoro dei processi.

Un account di archiviazione può contenere il numero desiderato di code. Una coda può contenere qualsiasi numero di messaggi, il limite di capacità toohello hello dell'account di archiviazione. Singoli messaggi possono essere too64 KB di dimensioni.

## <a name="file-storage"></a>Archiviazione file
Hello servizio file di Azure consente tooset le condivisioni di file di rete a disponibilità elevata che è possibile accedere tramite il protocollo Server Message Block (SMB) standard di hello. Che indica che è possono condividere più macchine virtuali hello stesso file con accesso in lettura e scrittura. È inoltre possibile leggere i file di hello usando l'interfaccia REST hello o le librerie client di archiviazione hello.

Una cosa che distingue l'archiviazione di File di Azure dal file in una condivisione file aziendale è che è possibile accedere ai file di hello ovunque nel mondo hello tramite un URL che punta a file toohello e include un token di firma di accesso condiviso. È possibile generare token di firma di accesso condiviso; consentono asset privata tooa di accesso specifici per un periodo di tempo specifico.

Le condivisioni file possono essere usate per molti scenari comuni:

* Molte applicazioni locali usano condivisioni file. Questa funzionalità rende più semplice toomigrate le applicazioni che condividono dati tooAzure. Se si monta hello toohello condivisione file stessa lettera di hello di unità locale che utilizza, parte hello dell'applicazione che accede a una condivisione di hello dovrebbe funzionare con modifiche minime, se presente.

* È possibile archiviare i file di configurazione in una condivisione di file e accedervi da più macchine virtuali. Strumenti e utilità utilizzata da più sviluppatori in un gruppo possono essere archiviate in una condivisione di file, assicurando che tutti gli utenti possano trovarli, e che usano hello stessa versione.

* I log di diagnostica, metriche e i dump di arresto anomalo del sistema sono sufficienti tre esempi di dati che possono essere scritti in una condivisione tooa ed elaborati o analizzati in seguito.

In questa fase, l'autenticazione basata su Active Directory e l'accesso (ACL) di elenchi di controllo non sono supportati, ma saranno in un momento nel futuro hello. le credenziali dell'account di archiviazione Hello sono autenticazione tooprovide utilizzato per la condivisione di file toohello di accesso. Ciò significa che chiunque con condivisione hello montato avrà condivisione toohello di accesso in lettura/scrittura.

## <a name="access-tooblob-table-queue-and-file-resources"></a>Accesso tooBlob, tabella, di accodamento e File di risorse
Per impostazione predefinita, solo proprietario dell'account archiviazione hello possa accedere alle risorse nell'account di archiviazione hello. Per la protezione dei dati hello, ogni richiesta effettuata per le risorse nell'account deve essere autenticata. L'autenticazione si basa su un modello di chiave condivisa. BLOB possono anche essere toosupport configurata l'autenticazione anonima.

Durante la creazione dell'account di archiviazione, vengono assegnate due chiavi di accesso private utilizzate per l'autenticazione. La presenza di due chiavi assicura che l'applicazione rimanga disponibile quando si rigenerano regolarmente le chiavi di hello come procedura di gestione delle chiavi di protezione comuni.

Se è necessario tooallow controllato accesso tooyour archiviazione alle risorse, è possibile creare una firma di accesso condiviso. Una firma di accesso condiviso (SAS) è un token che può essere accodati tooa URL che abilita delega accesso tooa risorsa di archiviazione. Chiunque possieda token hello potrà accedere a risorse hello che punti autorizzazioni hello toowith che specifica, per il periodo di hello di tempo che non è valido. A partire dalla versione del 4/5/2015, Archiviazione di Azure supporta due tipi di firme di accesso condiviso: firma di accesso condiviso del servizio e firma di accesso condiviso dell'account.

accedono a delegati SAS del servizio Hello risorsa tooa solo uno dei servizi di archiviazione hello: hello servizio Blob, coda, tabella o File.

Un account sa delega accesso tooresources in uno o più dei servizi di archiviazione hello. È possibile delegare operazioni tooservice a livello di accesso che non sono disponibili con un servizio di firma di accesso condiviso. È inoltre possibile delegare accesso tooread, scrittura e le operazioni di eliminazione in contenitori blob, tabelle, code e le condivisioni di file che non sono consentite con un firma di accesso condiviso del servizio.

È infine possibile specificare che un contenitore e i relativi BLOB o che un BLOB specifico sia disponibile per l'accesso pubblico. Quando si indica che un contenitore o un BLOB è pubblico, qualsiasi utente lo potrà leggere in forma anonima, in quanto non è necessaria l'autenticazione.  I contenitori e i BLOB pubblici sono utili per esporre risorse come file multimediali e documenti ospitati in siti Web.  toodecrease latenza di rete per un pubblico globale, è possibile memorizzare nella cache di dati blob utilizzati dai siti Web con hello rete CDN di Azure.

Per altre informazioni sulle firme di accesso condiviso, vedere [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) (Uso di firme di accesso condiviso). Vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md) e [l'autenticazione per i servizi di archiviazione Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) per ulteriori informazioni sull'account di archiviazione tooyour proteggere l'accesso.

## <a name="replication-for-durability-and-high-availability"></a>Replica per la durabilità e la disponibilità elevata
dati Hello in di Microsoft Azure è sempre l'account di archiviazione replicata tooensure durabilità e disponibilità elevata. Copia la replica dei dati, all'interno hello stesso data center o tooa secondo data center, a seconda dell'opzione di replica scelto. Replica protegge i dati e mantiene l'applicazione tempo nell'evento hello di errori hardware temporanei. Se i dati vengono replicati tooa secondo data center, che protegge i dati rispetto a un errore grave nella posizione primaria hello.

La replica garantisce che l'account di archiviazione soddisfi hello [contratto a livello di servizio (SLA) per l'archiviazione](https://azure.microsoft.com/support/legal/sla/storage/) anche in faccia hello di errori. Vedere hello contratto di servizio per informazioni sull'archiviazione di Azure garantisce la durabilità e la disponibilità.

Quando si crea un account di archiviazione, è possibile selezionare una delle seguenti opzioni di replica hello:

* **Archiviazione con ridondanza locale (LRS).** Con l'archiviazione con ridondanza locale vengono conservate tre copie dei dati. Tale tipo di archiviazione viene replicato per tre volte all'interno di un unico data center di una singola area. Ridondanza locale consente di proteggere i dati dai normali errori hardware, ma non da un errore di hello di un singolo data center.

    L'archiviazione con ridondanza locale viene offerta a tariffe scontate. Per la massima durabilità, è consigliabile usare l'archiviazione con ridondanza geografica descritta di seguito.
* **Archiviazione con ridondanza della zona (ZRS).** Con l'archiviazione con ridondanza della zona vengono conservate tre copie dei dati. Ridondanza della zona verrà replicato tre volte in due strutture toothree all'interno di una singola area o in due aree, fornendo una durabilità maggiore rispetto a ridondanza locale. Questa opzione di replica assicura la durabilità dei dati all'interno di una singola area.

    L'archiviazione con ridondanza della zona fornisce un livello di durabilità maggiore rispetto all'archiviazione con ridondanza locale. Tuttavia, per la massima durabilità, è consigliabile usare l'archiviazione con ridondanza geografica descritta di seguito.

  > [!NOTE]
  > ZRS è attualmente disponibile solo per i BLOB in blocchi ed è supportata solo nelle versioni 2014-02-14 e versioni successive.
  >
  > Dopo aver creato l'account di archiviazione e selezionato ZRS, è possibile eseguire la conversione toouse tooany altri tipo di replica o viceversa.
  >
  >
* **Archiviazione con ridondanza geografica (GRS)**. Con tale tipo di archiviazione vengono conservate sei copie dei dati. Con l'archiviazione con ridondanza geografica, i dati vengono replicati tre volte all'interno di area primaria hello e vengono inoltre replicati tre volte in un'area secondaria a centinaia di miglia di distanza area primaria hello, fornendo hello di livello più alto di durabilità. In caso di hello di un errore in area primaria hello, archiviazione di Azure eseguirà area secondaria toohello di failover. L'archiviazione con ridondanza geografica assicura la durabilità dei dati in due aree distinte.

    Per informazioni sulle associazioni primarie e secondarie per area, vedere [Aree di Azure](https://azure.microsoft.com/regions/).
* **Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS)**. Archiviazione con ridondanza geografica e accesso in lettura replica i dati tooa secondario area geografica e fornisce inoltre l'accesso in lettura tooyour dati nella posizione secondaria hello. Archiviazione con ridondanza geografica e accesso in lettura consente tooaccess i dati da hello primario o posizione secondaria hello, in caso di hello che diventa disponibile un'unica posizione. Archiviazione con ridondanza geografica e accesso in lettura è hello predefinito per l'account di archiviazione per impostazione predefinita quando viene creato.

  > [!IMPORTANT]
  > È possibile modificare come i dati vengono replicati dopo aver creato l'account di archiviazione, a meno che non è specificato ZRS durante la creazione di account hello. Si noti tuttavia che si può incorrere in costi se si passa dall'archiviazione con ridondanza locale tooGRS o RA-GRS un trasferimento di dati occasionale aggiuntivi.
  >
  >

Per altri dettagli sulle opzioni di replica di archiviazione, vedere [Replica di Archiviazione di Azure](storage-redundancy.md) .

Per informazioni sui prezzi per la replica dell'account di archiviazione, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/). Per altre informazioni sui servizi disponibili in ogni area, vedere [Aree di Azure](https://azure.microsoft.com/regions/#services) .

Per i dettagli architetturali sulla durabilità con Archiviazione di Azure, vedere [Paper SOSP - Archiviazione di Microsoft Azure: Un servizio di archiviazione cloud a elevata disponibilità con coerenza assoluta](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).

## <a name="transferring-data-tooand-from-azure-storage"></a>Trasferimento dati tooand da archiviazione di Azure
È possibile utilizzare hello AzCopy utilità della riga di comando toocopy blob, file e dati della tabella all'interno dell'account di archiviazione o tra account di archiviazione. Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md) per ulteriori informazioni.

AzCopy è basato su hello [raccolta lo spostamento dei dati di Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), che è attualmente disponibile in anteprima.

Hello servizio importazione/esportazione di Azure fornisce un modo tooimport blob di dati in o esportare i dati blob dall'account di archiviazione tramite un disco rigido spedito toohello data center di Azure. Per ulteriori informazioni su hello servizio importazione/esportazione, vedere [utilizzare hello servizio importazione/esportazione di Microsoft Azure tooTransfer dati tooBlob archiviazione](storage-import-export-service.md).

## <a name="pricing"></a>Prezzi
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>API di archiviazione, librerie e strumenti
Le risorse di archiviazione di Azure sono accessibile da qualsiasi linguaggio in grado di eseguire richieste HTTP/HTTPS. In Archiviazione di Azure sono inoltre disponibili librerie di programmazione per diversi linguaggi comuni. Tali librerie semplificano molti aspetti dell'utilizzo di Archiviazione di Azure gestendo dettagli come la chiamata sincrona e asincrona, l'esecuzione delle operazioni in batch, la gestione delle eccezioni, la ripetizione automatica dei tentativi, il comportamento operativo e così via. Librerie sono attualmente disponibili per hello seguenti linguaggi e piattaforme, con altri utenti nella pipeline di hello:

### <a name="azure-storage-data-services"></a>Servizi dati di Archiviazione di Azure
* [API REST dei servizi di archiviazione](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Libreria client per .NET, Windows Phone e Windows Runtime](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Libreria client di archiviazione per C++](https://github.com/Azure/azure-storage-cpp)
* [Libreria client di archiviazione per Java/Android](https://azure.microsoft.com/develop/java/)
* [Libreria client di archiviazione per Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Libreria client di archiviazione per PHP](https://azure.microsoft.com/develop/php/)
* [Libreria client di archiviazione per Ruby](https://azure.microsoft.com/develop/ruby/)
* [Libreria client di archiviazione per Python](https://azure.microsoft.com/develop/python/)
* [Cmdlet di archiviazione per PowerShell 1.0](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Servizi di gestione di Archiviazione di Azure
* [Informazioni di riferimento sulle API REST del provider di risorse di archiviazione](/rest/api/storagerp/)
* [Libreria client del provider di risorse di archiviazione per .NET](/dotnet/api/microsoft.azure.management.storage)
* [Cmdlet del provider di risorse di archiviazione per PowerShell 1.0](/powershell/module/azure.storage)
* [API REST di gestione del servizio di archiviazione (classico)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Servizi di spostamento dei dati di Archiviazione di Azure
* [API REST del servizio di importazione/esportazione dell'archiviazione](storage-import-export-service.md)
* [Libreria client di spostamento dei dati di archiviazione per .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Strumenti e utilità
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* [Strumento client di Archiviazione di Azure](storage-explorers.md)
* [Azure SDK e strumenti](https://azure.microsoft.com/tools/)
* [Emulatore di archiviazione di Azure](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [Utilità da riga di comando di AzCopy](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'archiviazione di Azure, è esplorare queste risorse:

### <a name="documentation"></a>Documentazione
* [Documentazione di Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Creare un account di archiviazione](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Per amministratori
* [Uso di Azure PowerShell con Archiviazione di Azure](storage-powershell-guide-full.md)
* [Uso dell'interfaccia della riga di comando di Azure con Archiviazione di Azure](storage-azure-cli.md)

### <a name="for-net-developers"></a>Per sviluppatori .NET
* [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md)
* [Introduzione all'archiviazione tabelle di Azure con .NET](storage-dotnet-how-to-use-tables.md)
* [Introduzione all'archiviazione code di Azure con .NET](storage-dotnet-how-to-use-queues.md)
* [Introduzione ad Archiviazione file di Azure in Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Per sviluppatori Java/Android
* [Come toouse archiviazione Blob da Java](storage-java-how-to-use-blob-storage.md)
* [Come toouse archiviazione tabelle da Java](storage-java-how-to-use-table-storage.md)
* [Come toouse l'archiviazione delle code da Java](storage-java-how-to-use-queue-storage.md)
* [Come toouse archiviazione di File da Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Per sviluppatori Node.js
* [Come toouse archiviazione Blob da Node.js](storage-nodejs-how-to-use-blob-storage.md)
* [Come toouse archiviazione tabelle da Node.js](storage-nodejs-how-to-use-table-storage.md)
* [Come toouse archiviazione delle code da Node.js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Per sviluppatori PHP
* [Come toouse archiviazione Blob da PHP](storage-php-how-to-use-blobs.md)
* [Come toouse archiviazione tabelle da PHP](storage-php-how-to-use-table-storage.md)
* [Come toouse l'archiviazione delle code da PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Per sviluppatori Ruby
* [Come toouse archiviazione Blob da Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Come archiviazione tabella da Ruby toouse](storage-ruby-how-to-use-table-storage.md)
* [Come l'archiviazione delle code da Ruby toouse](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Per sviluppatori Python
* [Come toouse archiviazione Blob da Python](storage-python-how-to-use-blob-storage.md)
* [Come toouse archiviazione tabelle da Python](storage-python-how-to-use-table-storage.md)
* [Come toouse l'archiviazione delle code da Python](storage-python-how-to-use-queue-storage.md)
* [Come toouse archiviazione di File da Python](storage-python-how-to-use-file-storage.md)
