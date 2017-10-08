---
title: aaaIntroduction tooAzure archiviazione | Documenti Microsoft
description: Introduzione tooAzure archiviazione, l'archiviazione dei dati di Microsoft nel cloud hello.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Introduzione tooMicrosoft di archiviazione di Azure

Archiviazione di Microsoft Azure è un servizio cloud gestito da Microsoft che offre risorse di archiviazione a disponibilità, sicurezza, durabilità, scalabilità e ridondanza elevate. Microsoft si occupa della manutenzione e gestisce i problemi critici per conto dell'utente. 

Archiviazione di Azure è costituito da tre servizi dati: archiviazione BLOB, archiviazione file e archiviazione code. Archiviazione BLOB supporta l'archiviazione standard e premium, con archiviazione premium utilizzando solo unità SSD i tempi delle prestazioni hello. Un'altra caratteristica è interessante spazio di archiviazione, consentendo toostorage grandi quantità di dati a cui si accede raramente per un costo inferiore.

In questo articolo viene illustrato come segue hello:
* servizi di archiviazione Azure Hello
* tipi di Hello di account di archiviazione
* Accesso a BLOB, code e file
* Crittografia
* Replica 
* Trasferimento di dati verso e dalle risorse di archiviazione
* Hello molti le librerie client di archiviazione disponibile. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Introduzione a servizi di archiviazione Azure hello

uno dei servizi hello fornito dal servizio di archiviazione Azure - archiviazione Blob di archiviazione di File e archiviazione delle code - toouse prima di creare un account di archiviazione e quindi è possibile trasferire dati da e verso un servizio specifico di tale account di archiviazione. 

## <a name="blob-storage"></a>Archiviazione BLOB

I BLOB sono essenzialmente file simili a quelli archiviati nel computer o nel tablet, nel dispositivo mobile e così via. Possono essere file di qualsiasi tipo, ad esempio immagini, file di Microsoft Excel, file HTML, dischi rigidi virtuali, Big Data come log, backup dei database. BLOB vengono archiviati in contenitori, che sono toofolders simile. 

Dopo l'archiviazione dei file nell'archiviazione Blob, è possibile accedervi ovunque nel mondo hello tramite URL, hello interfaccia REST o una delle librerie client di archiviazione Azure SDK hello. Le librerie client di archiviazione sono disponibili per molti linguaggi, tra cui Node.js, Java, PHP, Ruby, Python e .NET. 

Esistono tre tipi di BLOB, ovvero i BLOB in blocchi, i BLOB di aggiunta
e i BLOB di pagine (usati per i file VHD).

* BLOB in blocchi sono utilizzati toohold normali file di backup tooabout 4,7 TB. 
* BLOB di pagine sono file di accesso casuale toohold utilizzato backup too8 TB nella dimensione. Vengono utilizzati per i file VHD hello che eseguire il backup di macchine virtuali.
* Aggiungere i BLOB sono costituiti da blocchi come BLOB in blocchi hello, ma sono ottimizzati per operazioni di aggiunta. Vengono utilizzati per elementi quali la registrazione di informazioni toohello stesso blob da più macchine virtuali.

Per grandi set di dati in cui i vincoli di rete assicurarsi di caricare o scaricare l'archiviazione dei dati tooBlob rete hello poco realistico, è possibile fornire un set di dischi rigidi tooMicrosoft tooimport o esportare i dati direttamente dal centro dati hello. Vedere [utilizzare hello servizio importazione/esportazione di Microsoft Azure tooTransfer dati tooBlob archiviazione](../storage-import-export-service.md).

## <a name="file-storage"></a>Archiviazione file

Hello servizio file di Azure consente tooset le condivisioni di file di rete a disponibilità elevata che è possibile accedere tramite il protocollo Server Message Block (SMB) standard di hello. Che indica che è possono condividere più macchine virtuali hello stesso file con accesso in lettura e scrittura. È inoltre possibile leggere i file di hello usando l'interfaccia REST hello o le librerie client di archiviazione hello. 

Una cosa che distingue l'archiviazione di File di Azure dal file in una condivisione file aziendale è che è possibile accedere ai file di hello ovunque nel mondo hello tramite un URL che punta a file toohello e include un token di firma di accesso condiviso. È possibile generare token di firma di accesso condiviso; consentono asset privata tooa di accesso specifici per un periodo di tempo specifico. 

Le condivisioni file possono essere usate per molti scenari comuni: 

* Molte applicazioni locali usano condivisioni file. Questa funzionalità rende più semplice toomigrate le applicazioni che condividono dati tooAzure. Se si monta hello toohello condivisione file stessa lettera di hello di unità locale che utilizza, parte hello dell'applicazione che accede a una condivisione di hello dovrebbe funzionare con modifiche minime, se presente.

* È possibile archiviare i file di configurazione in una condivisione di file e accedervi da più macchine virtuali. Strumenti e utilità utilizzata da più sviluppatori in un gruppo possono essere archiviate in una condivisione di file, assicurando che tutti gli utenti possano trovarli, e che usano hello stessa versione.

* I log di diagnostica, metriche e i dump di arresto anomalo del sistema sono sufficienti tre esempi di dati che possono essere scritti in una condivisione tooa ed elaborati o analizzati in seguito.

In questa fase, l'autenticazione basata su Active Directory e l'accesso (ACL) di elenchi di controllo non sono supportati, ma saranno in un momento nel futuro hello. le credenziali dell'account di archiviazione Hello sono autenticazione tooprovide utilizzato per la condivisione di file toohello di accesso. Ciò significa che chiunque con condivisione hello montato avrà condivisione toohello di accesso in lettura/scrittura.

## <a name="queue-storage"></a>Archiviazione code

servizio di Accodamento Azure Hello è utilizzato toostore e recuperare i messaggi. Messaggi in coda possono essere too64 KB di dimensioni e una coda può contenere milioni di messaggi. Le code sono elenchi toostore utilizzato in genere di toobe i messaggi elaborati in modo asincrono. 

Ad esempio si desidera le immagini in grado di tooupload toobe di clienti e si desidera toocreate anteprime di ogni immagine. È possibile che il cliente si anteprime hello toocreate attendere durante il caricamento di immagini hello. In alternativa sarebbe toouse una coda. Al termine del suo caricamento cliente hello, scrivere una coda di messaggi toohello. Recuperare il messaggio hello dalla coda hello e creare miniature hello che quindi sia una funzione di Azure. Ciascuna delle parti di hello di questo tipo di elaborazione può essere scalato separatamente, fornendo un controllo maggiore durante l'ottimizzazione, per l'utilizzo.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Archiviazione tabelle
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
L'archiviazione tabelle di Azure Standard è ora inclusa in Cosmos DB. Sono anche disponibili tabelle Premium per l'archiviazione tabelle di Azure, che offrono tabelle ottimizzate per la velocità effettiva, distribuzione globale e indici secondari automatici. ulteriori toolearn e provare hello nuova esperienza, il check-out [DB Cosmos Azure: tabella API](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Archiviazione su disco

il team di archiviazione di Azure Hello possiede anche i dischi, che include tutti hello gestito e le funzionalità disco non gestite utilizzate da macchine virtuali. Per ulteriori informazioni su queste funzionalità, vedere hello [documentazione del servizio di calcolo](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Tipi di account di archiviazione 

Questa tabella mostra hello vari tipi di account di archiviazione e gli oggetti che possono essere utilizzati con ognuno.

|**Tipo di account di archiviazione**|**Utilizzo generico Standard**|**Utilizzo generico Premium**|**Archiviazione BLOB, livelli ad accesso frequente e ad accesso sporadico**|
|-----|-----|-----|-----|
|**Servizi supportati**| Servizi BLOB, file, code | Servizio BLOB | Servizio BLOB|
|**Tipi di BLOB supportati**|BLOB in blocchi, BLOB di pagine e BLOB di aggiunta | BLOB di pagine | BLOB in blocchi e BLOB di aggiunta|

### <a name="general-purpose-storage-accounts"></a>Account di archiviazione per utilizzo generico

Sono disponibili due tipi di account di archiviazione per utilizzo generico. 

#### <a name="standard-storage"></a>Archiviazione standard 

gli account di archiviazione Hello più diffuse sono gli account di archiviazione standard, che possono essere utilizzati per tutti i tipi di dati. Gli account di archiviazione standard utilizzano dati di supporto magnetico toostore.

#### <a name="premium-storage"></a>Archiviazione Premium

L'Archiviazione Premium fornisce risorse di archiviazione a prestazioni elevate per i BLOB di pagine, usati principalmente per i file VHD. Account di archiviazione Premium utilizzare dati toostore unità SSD. Microsoft consiglia di usare l'Archiviazione Premium per tutte le VM.

### <a name="blob-storage-accounts"></a>Account di archiviazione BLOB

account di archiviazione Blob Hello è un account di archiviazione specializzata utilizzata toostore BLOB in blocchi e BLOB di aggiunta. Non è possibile archiviare i BLOB di pagine in questi account e quindi non è possibile archiviare file VHD. Questi account consentono di tooset tooHot di livello un accesso o Cool; livello di Hello può essere modificato in qualsiasi momento. 

livello di accesso frequente Hello viene utilizzato per i file che si accede di frequente - si paga un costo superiore per l'archiviazione, ma il costo di hello di accedere agli oggetti BLOB hello è molto inferiore. Per i BLOB archiviati nel livello di accesso sporadico hello, si paga un costo superiore per l'accesso ai BLOB hello, ma costo hello dell'archiviazione è molto inferiore.

## <a name="accessing-your-blobs-files-and-queues"></a>Accesso a BLOB, file e code

Ogni account di archiviazione include due chiavi di autenticazione, che possono essere usate per qualsiasi operazione. Esistono due chiavi in modo è possibile eseguire il rollback su hello chiavi occasionalmente tooenhance sicurezza. È fondamentale che queste chiavi occorre mantenere la sicurezza perché possesso, insieme al nome account hello, consente di accesso illimitato tooall dati nell'account di archiviazione hello. 

Questa sezione vengono illustrati due account di archiviazione hello di toosecure modi e i relativi dati. Per informazioni dettagliate sulla sicurezza dell'account di archiviazione e i dati, vedere hello [Guida alla protezione di archiviazione di Azure](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Protezione dell'accesso account toostorage mediante Azure AD

Dati di archiviazione tooyour accesso toosecure unidirezionale sono mediante il controllo di accesso toohello chiavi account di archiviazione. Con Gestione risorse di controllo di accesso basato sui ruoli (RBAC), è possibile assegnare ruoli toousers, gruppi o applicazioni. Questi ruoli sono collegati tooa set specifico di azioni che sono consentiti o non consentiti. RBAC tramite account di archiviazione tooa toogrant accesso gestisce solo le operazioni di gestione per tale account di archiviazione, ad esempio la modifica a livello di accesso hello hello. È possibile usare RBAC toogrant accesso toodata gli oggetti come una condivisione di file o contenitore specifico. Tuttavia, è possibile utilizzare RBAC toogrant accesso toohello chiavi account di archiviazione, che possono essere utilizzati tooread hello dati oggetti. 

### <a name="securing-access-using-shared-access-signatures"></a>Protezione dell'accesso tramite le firme di accesso condiviso 

È possibile utilizzare le firme di accesso condiviso e archiviati gli oggetti di data di toosecure di criteri di accesso. Una firma di accesso condiviso (SAS) è una stringa contenente un token di sicurezza che può essere collegati toohello URI per un asset che consente di oggetti di archiviazione toospecific toodelegate accesso e i vincoli di toospecify, ad esempio le autorizzazioni e l'intervallo di data/ora hello di accesso. Questa funzionalità offre capacità estese. Per informazioni dettagliate, vedere troppo[tramite firme di accesso condiviso (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Accesso pubblico tooblobs

Servizio Blob Hello consente tooprovide accesso pubblico tooa contenitore e i relativi BLOB o un blob specifico. Quando si indica che un contenitore o un BLOB è pubblico, qualsiasi utente lo potrà leggere in forma anonima, in quanto non è necessaria l'autenticazione. Un esempio di cui vuoi toodo è quando si dispone di un sito Web che utilizza immagini, video o documenti dall'archiviazione Blob. Per ulteriori informazioni, vedere [gestire l'accesso in lettura anonimo toocontainers e BLOB](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Crittografia

Sono disponibili due tipi di base di crittografia per i servizi di archiviazione hello. 

### <a name="encryption-at-rest"></a>Crittografia di dati inattivi 

È possibile abilitare la crittografia del servizio di archiviazione (SSE) su dei servizi file hello (anteprima) o hello servizio Blob per un account di archiviazione di Azure. Se abilitata, tutti i dati scritti toohello di servizio specifico viene crittografato prima della scrittura. Quando si leggono dati hello, questo viene decrittografato prima restituito. 

### <a name="client-side-encryption"></a>Crittografia lato client

salve le librerie client di archiviazione dispongono di metodi è possibile chiamare tooprogrammatically crittografare i dati prima di inviarlo in transito hello da hello client tooAzure. I dati vengono archiviati crittografati, ovvero sono crittografati anche quando inattivi. Durante la lettura di backup dei dati hello, decrittografare le informazioni di hello dopo averlo ricevuto. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Crittografia in transito con le condivisioni file di Azure

Per altre informazioni sulle firme di accesso condiviso, vedere [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) (Uso di firme di accesso condiviso). Vedere [gestire BLOB e accesso in lettura anonimo toocontainers](../blobs/storage-manage-access-to-resources.md) e [l'autenticazione per i servizi di archiviazione Azure hello](https://msdn.microsoft.com/library/azure/dd179428.aspx) per ulteriori informazioni sull'account di archiviazione tooyour proteggere l'accesso.

Per ulteriori informazioni sulla protezione dell'account di archiviazione e la crittografia, vedere hello [Guida alla protezione di archiviazione di Azure](storage-security-guide.md).

## <a name="replication"></a>Replica

In ordine tooensure che i dati siano durevoli, archiviazione di Azure è hello possibilità tookeep (e gestire) più copie dei dati. Questo approccio viene definito replica o ridondanza. Quando si configura l'account di archiviazione, si seleziona il tipo di replica. Nella maggior parte dei casi, questa impostazione può essere modificata dopo l'impostazione di account di archiviazione hello. 

Tutti gli account di archiviazione hanno l'**archiviazione con ridondanza locale**. Ciò significa tre copie dei dati gestite da archiviazione di Azure nel data center di hello specificato quando è stato impostato hello account di archiviazione. Quando le modifiche sono tooone commit copiare, hello altri due copie vengono aggiornate prima di restituire l'esito positivo. Ciò significa che le tre repliche di hello sono sempre sincronizzate. Inoltre, hello tre copie si trovano in domini di errore e domini di aggiornamento, ovvero che i dati sono disponibili anche se ha esito negativo di un nodo di archiviazione che contiene i dati o è uscito toobe offline aggiornato. 

**Archiviazione con ridondanza locale (LRS)**

Come illustrato in precedenza, l'archiviazione con ridondanza locale fornisce tre copie dei dati in un singolo data center. In grado di gestire il problema di hello dei dati non sono più disponibili se un nodo di archiviazione ha esito negativo o viene portato non in linea toobe aggiornato, ma non hello caso di un intero Data Center diventi non disponibile.

**Archiviazione con ridondanza della zona**

Archiviazione con ridondanza della zona (ZRS) gestisce hello tre copie dei dati oltre a un altro set di tre copie dei dati. Hello secondo set di tre copie vengono replicati in modo asincrono in Data Center all'interno di uno o due aree. Si noti che l'archiviazione con ridondanza della zona è disponibile solo per i BLOB in blocchi negli account di archiviazione per utilizzo generico. Inoltre, dopo aver creato l'account di archiviazione e selezionato ZRS, è possibile convertirlo toouse tooany altri tipo di replica o viceversa.

L'archiviazione con ridondanza della zona fornisce una durabilità superiore rispetto all'archiviazione con ridondanza locale, ma gli account di archiviazione con ridondanza della zona non includono metriche o funzionalità di registrazione. 

**Archiviazione con ridondanza geografica (GRS)**

Archiviazione con ridondanza geografica (GRS) gestisce hello tre copie dei dati in un'area primaria oltre a un altro set di tre copie dei dati in un'area secondaria a centinaia di miglia di distanza area primaria hello. In caso di hello di un errore in area primaria hello, archiviazione di Azure eseguirà il failover area secondaria toohello. 

**Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS).** 

Archiviazione con ridondanza geografica e accesso in lettura è identico a quello di archiviazione con ridondanza geografica, ad eccezione del fatto che sia possibile ottenere l'accesso in lettura toohello dati nella posizione secondaria hello. Se hello data center primario diventa temporaneamente non disponibile, è possibile continuare dati hello tooread dal percorso secondario hello. Questo approccio può risultare molto utile. Ad esempio, potrebbe avere un'applicazione web che viene modificato in modalità di sola lettura e copia secondaria toohello, consentendo l'accesso, anche se non sono disponibili aggiornamenti. 

> [!IMPORTANT]
> È possibile modificare come i dati vengono replicati dopo aver creato l'account di archiviazione, a meno che non è specificato ZRS durante la creazione di account hello. Si noti tuttavia che si può incorrere in costi se si passa dall'archiviazione con ridondanza locale tooGRS o RA-GRS un trasferimento di dati occasionale aggiuntivi.
>

Per altre informazioni sulla replica, vedere [Replica di Archiviazione di Azure](storage-redundancy.md).

Per informazioni di ripristino di emergenza, vedere [quali toodo se si verifica un'interruzione di servizio di archiviazione Azure](storage-disaster-recovery-guidance.md).

Per un esempio di come tooleverage RA-GRS archiviazione tooensure la disponibilità elevata, vedere [progettazione altamente disponibile di applicazioni utilizzando RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Trasferimento dati tooand da archiviazione di Azure

È possibile utilizzare hello AzCopy utilità della riga di comando toocopy blob e i dati di file all'interno dell'account di archiviazione o tra account di archiviazione. Uno dei seguenti hello articoli per la Guida, vedere:

* [Transfer data with AzCopy for Windows](storage-use-azcopy.md) (Trasferire dati con AzCopy per Windows)
* [Transfer data with AzCopy for Linux](storage-use-azcopy-linux.md) (Trasferire dati con AzCopy per Linux)

AzCopy è basato su hello [raccolta lo spostamento dei dati di Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), che è attualmente disponibile in anteprima.

Hello servizio importazione/esportazione di Azure può essere utilizzato tooimport o l'esportazione di grandi tooor dati blob dall'account di archiviazione. Preparare e di posta elettronica più unità disco rigido tooan data center di Azure, in cui verranno trasferiti dati hello in/da dischi rigidi hello e inviare nuovamente i dischi rigidi hello tooyou. Per ulteriori informazioni su hello servizio importazione/esportazione, vedere [utilizzare hello servizio importazione/esportazione di Microsoft Azure tooTransfer dati tooBlob archiviazione](../storage-import-export-service.md).

## <a name="pricing"></a>Prezzi

Per informazioni dettagliate sui prezzi di archiviazione di Azure, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>API di archiviazione, librerie e strumenti
Le risorse di archiviazione di Azure sono accessibile da qualsiasi linguaggio in grado di eseguire richieste HTTP/HTTPS. In Archiviazione di Azure sono inoltre disponibili librerie di programmazione per diversi linguaggi comuni. Tali librerie semplificano molti aspetti dell'utilizzo di Archiviazione di Azure gestendo dettagli come la chiamata sincrona e asincrona, l'esecuzione delle operazioni in batch, la gestione delle eccezioni, la ripetizione automatica dei tentativi, il comportamento operativo e così via. Librerie sono attualmente disponibili per hello seguenti linguaggi e piattaforme, con altri utenti nella pipeline di hello:

### <a name="azure-storage-data-services"></a>Servizi dati di Archiviazione di Azure
* [API REST dei servizi di archiviazione](/rest/api/storageservices/)
* [Libreria client di archiviazione per .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Libreria client di archiviazione per C++](https://github.com/Azure/azure-storage-cpp)
* [Libreria client di archiviazione per Java/Android](https://azure.microsoft.com/develop/java/)
* [Libreria client di archiviazione per Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Libreria client di archiviazione per PHP](https://azure.microsoft.com/develop/php/)
* [Libreria client di archiviazione per Python](https://azure.microsoft.com/develop/python/)
* [Libreria client di archiviazione per Ruby](https://azure.microsoft.com/develop/ruby/)
* [Cmdlet di archiviazione per PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Storage Commands for CLI 2.0](/cli/azure/storage) (Comandi di archiviazione per l'interfaccia della riga di comando 2.0)

## <a name="next-steps"></a>Passaggi successivi

* [Learn more about Blob storage (Altre informazioni sull'archiviazione BLOB)](../blobs/storage-blobs-introduction.md)
* [Learn more about Blob storage (Altre informazioni sull'archiviazione file)](../storage-files-introduction.md)
* [Learn more about Blob storage (Altre informazioni sull'archiviazione code)](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Per amministratori
* [Uso di Azure PowerShell con Archiviazione di Azure](storage-powershell-guide-full.md)
* [Uso dell'interfaccia della riga di comando di Azure con Archiviazione di Azure](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Per sviluppatori .NET
* [Introduzione all'archiviazione BLOB di Azure con .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Introduzione all'archiviazione tabelle di Azure con .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Introduzione all'archiviazione code di Azure con .NET](../storage-dotnet-how-to-use-queues.md)
* [Introduzione ad Archiviazione file di Azure in Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Per sviluppatori Java/Android
* [Come toouse archiviazione Blob da Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Come toouse archiviazione tabelle da Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Come toouse l'archiviazione delle code da Java](../storage-java-how-to-use-queue-storage.md)
* [Come toouse archiviazione di File da Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Per sviluppatori Node.js
* [Come toouse archiviazione Blob da Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Come toouse archiviazione tabelle da Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Come toouse archiviazione delle code da Node.js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Per sviluppatori PHP
* [Come toouse archiviazione Blob da PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Come toouse archiviazione tabelle da PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Come toouse l'archiviazione delle code da PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Per sviluppatori Ruby
* [Come toouse archiviazione Blob da Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Come archiviazione tabella da Ruby toouse](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Come l'archiviazione delle code da Ruby toouse](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Per sviluppatori Python
* [Come toouse archiviazione Blob da Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Come toouse archiviazione tabelle da Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Come toouse l'archiviazione delle code da Python](../storage-python-how-to-use-queue-storage.md)   
* [Come toouse archiviazione di File da Python](../storage-python-how-to-use-file-storage.md) 
-->