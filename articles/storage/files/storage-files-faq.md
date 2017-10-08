---
title: domande frequenti sull'archiviazione di File di Azure aaaFrequently | Documenti Microsoft
description: Risposte toofrequently domande frequenti sull'archiviazione di File di Azure.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: d8a94fdc77e928dbc6996e1e635cd3527e0c67d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Domande frequenti sul servizio di Archiviazione di Azure

## <a name="general"></a>Generale
* **D. Che cos'è l'archiviazione file di Azure?**  
   
    Archiviazione file di Azure è un file system distribuito in Azure. Fornisce un'interfaccia del protocollo SMB che consente l'archiviazione hello toomount di utenti come condivisione native sul computer locale o di macchine virtuali di Azure supportate.

* **D. Vantaggi offerti da Archiviazione file di Azure**  
   
    Archiviazione file di Azure fornisce accesso ai dati condivisi tra più macchine virtuali e piattaforme. Fare riferimento troppo[archiviazione perché i File di Azure è utile](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **D. Quando usare File di Azure e BLOB di Azure invece di Dischi di Azure**  
   
    Microsoft Azure offre diversi modi toostore e accedere ai dati nel cloud hello.  
   
    Archiviazione di File di Azure - fornisce un'interfaccia SMB, le librerie client e un'interfaccia REST che permette il facile accesso ovunque toostored file.  
   
    Azure BLOB - fornisce librerie client e un'interfaccia REST che consente di dati non strutturati toobe archiviate e accessibili su larga scala in BLOB in blocchi.  
   
    Dati di Azure dischi - fornisce librerie client e un'interfaccia REST che consente di toobe dati archiviati in modo permanente e accessibile da un disco rigido virtuale collegato.  
   
    Altre informazioni su [determinazione quando toouse BLOB di Azure, i file di Azure o i dischi dati di Azure](../common/storage-decide-blobs-files-disks.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)

* **D. Come iniziare a usare l'archiviazione file di Azure?**  
   
    Iniziare creando una condivisione di file di Azure. È possibile creare condivisioni File di Azure usando il portale di Azure, i cmdlet di PowerShell di archiviazione di Azure hello, librerie client di archiviazione di Azure hello o hello API REST di archiviazione di Azure. In questa esercitazione si apprenderà:

    * [Informazioni su come toocreate File di Azure condividono utilizzando hello portale](storage-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Informazioni su come toocreate File di Azure condividono l'utilizzo di Powershell](storage-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Informazioni su come toocreate File di Azure condividono utilizzando CLI](storage-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **D. Quali repliche sono supportate da Archiviazione file di Azure?**  
   
    Attualmente, Archiviazione file di Azure supporta solo l'archiviazione con ridondanza locale o con ridondanza geografica. Contiamo toosupport RA-GRS, ma non è ancora alcun tooshare sequenza temporale.

## <a name="security-authentication-and-access-control"></a>Sicurezza, autenticazione e controllo di accesso

* **D. Quali sono i file di tooaccess modi diversi in archiviazione di File di Azure?**
    
    È possibile montare hello condivisione di file nel computer locale utilizzando il protocollo SMB 3.0 o utilizzare strumenti come [Esplora archivi](http://storageexplorer.com/) tooaccess file nella condivisione di file. Dall'applicazione, è possibile utilizzare le librerie client di archiviazione, le API REST o Powershell tooaccess che condividono i file nel File di Azure.

* **D. Come è possibile fornire tooa specifico di Access utilizzando un web browser?**
    
    Le firme di accesso condiviso consentono di generare token con autorizzazioni specifiche che restano valide per un periodo di tempo definito. Ad esempio, è possibile generare un token con file di particolare tooa di accesso in sola lettura per un periodo di tempo specifico. Qualsiasi utente che possiede l'url hello file accessibile direttamente da qualsiasi web browser mentre è valido. È possibile generare facilmente le chiavi di firma di accesso condiviso dall'interfaccia utente, ad esempio con Storage Explorer.

* **D. Si tratta di autorizzazioni di sola lettura o sola scrittura toospecify possibili per le cartelle all'interno di condivisione hello?**
    
    Questo livello di controllo delle autorizzazioni non è necessario se si monta hello condivisione di file tramite SMB. Tuttavia, è possibile ottenere mediante la creazione di una firma di accesso condiviso (SAS) tramite l'API REST hello o le librerie client.  

* **D. Come abilitare la crittografia lato server per l'archiviazione file di Azure**

    La [crittografia lato server](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) per l'archiviazione file di Azure è in genere disponibile in tutte le aree e nei cloud pubblici e nazionali. Per abilitare la crittografia lato server per l'archiviazione file di Azure, è possibile usare il [portale di Azure](https://portal.azure.com/), l'[API del provider di risorse di Archiviazione di Microsoft Azure](/rest/api/storagerp/storageaccounts), [Azure Powershell](https://msdn.microsoft.com/library/azure/mt607151.aspx) o l'[interfaccia della riga di comando di Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).
    
    Dopo aver abilitato SSE sull'archiviazione di File di Azure, tutti i nuovi dati scritti toohello archiviazione di file in tale account di archiviazione verranno crittografati automaticamente. Questa funzionalità è disponibile per tutti i nuovi dati scritti tooexisting o nuove condivisioni in un account di archiviazione esistente o nuovo. Non sono previsti costi aggiuntivi per questa funzionalità. Altre informazioni su [come tooenable SSE sull'archiviazione di File di Azure](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

* **D. L'autenticazione basata su Active Directory è supportata da Archiviazione file di Azure?**
   
    Al momento non è supportata l'autenticazione basata su Active Directory o sugli elenchi di controllo di accesso (ACL), ma è inclusa nell'elenco delle richieste di funzionalità. Per il momento, chiavi dell'account di archiviazione di Azure hello sono condivisione di file toohello autenticazione tooprovide utilizzato. Offriamo una soluzione alternativa che usa le firme di accesso condiviso (SAS) tramite le librerie client API REST o hello di hello. Le firme di accesso condiviso consentono di generare token con autorizzazioni specifiche che restano valide per un periodo di tempo definito. Ad esempio, è possibile generare un token con accesso in sola lettura tooa file con scadenza di 10 minuti specificato. Qualsiasi utente che possiede questo token, sebbene sia valido ha file toothat accesso in sola lettura per i 10 minuti.
   
    Firma di accesso condiviso è supportata solo tramite le librerie di API REST o client hello. Quando si monta una condivisione di file hello tramite hello protocollo SMB, è possibile utilizzare un contenuto di tooits accesso toodelegate SAS. 
    
* **D. Quali sono i criteri di conformità hello dati supportati per l'archiviazione di File di Azure?**

   Archiviazione di File di Azure viene eseguito in hello stessa architettura di archiviazione, come altre risorse di archiviazione di servizi di archiviazione di Azure e applica hello stessi criteri di conformità dei dati. Altre informazioni sulla conformità dei dati di archiviazione di Azure, è possibile scaricare e consultare troppo[documento di Microsoft Azure Data Protection](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Accesso locale

* **Q.Do ho toouse Azure ExpressRoute tooconnect tooAzure archiviazione di File da una macchina virtuale locale?**
   
    No. Se non si dispone di ExpressRoute, è comunque possibile accedere hello condivisione di file locale, purché si porta 445 (TCP in uscita) aperto per l'accesso a Internet. È tuttavia possibile usare ExpressRoute con archiviazione file di Azure, se lo si desidera.

* **D. Come è possibile montare la condivisione file di Azure nel computer locale?** 
    
    È possibile montare hello condivisione di file tramite il protocollo SMB hello, purché la porta 445 (TCP in uscita) è aperta e il client supporta il protocollo SMB 3.0 hello (ad esempio, si usa Windows 10 o Windows Server 2012). Rivolgersi la porta hello toounblock di provider ISP locale. In hello provvisorio, è possibile visualizzare i file utilizzando [Esplora archivi](../../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Prezzi e fatturazione
* **D. Hello traffico di rete tra una macchina virtuale di Azure e un conteggio di condivisione file come larghezza di banda esterna viene addebitato toohello sottoscrizione?**
   
    Se la condivisione di file hello e VM hello stessa regione di Azure, hello il traffico tra di essi è disponibile. Se sono presenti in diverse aree geografiche, verrà addebitato il traffico tra esse hello come larghezza di banda esterna.

## <a name="backup"></a>Backup

* **D. Come eseguire il backup nella condivisione file di Azure**
    
    È possibile usare AzCopy, RoboCopy o uno strumento di backup di terze parti per eseguire il backup di una condivisione di file montati. Prevediamo toohave snapshot tootake possibilità di hello delle condivisioni File in hello prossimo futuro; sarà possibile toouse in grado di condividere il File di Azure toobackup questa funzionalità.

## <a name="performance"></a>Prestazioni

* **D. Quali sono i limiti di scalabilità hello archiviazione dei File di Azure?**
    Per informazioni sugli obiettivi di scalabilità e prestazioni di Archiviazione file, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#scalability-targets-for-blobs-queues-tables-and-files).

* **D. My prestazioni sono lenta durante il tentativo di toounzip file nell'archiviazione di File di Azure. Cosa devo fare?**
    
    tootransfer un numero elevato di file nell'archiviazione di File di Azure, è consigliabile usare AzCopy (Windows, l'anteprima per Linux/Unix) o Azure Powershell perché questi strumenti sono stati ottimizzati per il trasferimento di rete.

* **D. Quali patch è stato rilasciato il problema di prestazioni lente toofix con l'archiviazione di File di Azure?**
    
    Hello recente rilasciato un toofix patch un problema di prestazioni lente quando cliente hello accede all'archiviazione di File di Azure da Windows 8.1 o Windows Server 2012 R2. Per ulteriori informazioni,. estrazione hello associata articolo della Knowledge Base, [rallentare le prestazioni quando si accede di archiviazione di File di Azure da Windows 8.1 o Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Funzionalità e interoperabilità con altri servizi
* **D. È un "condivisione File di controllo" per un cluster di failover, uno di hello casi d'uso per l'archiviazione di File di Azure?**
   
    Questa opzione non è attualmente supportata.

* **D. È un'operazione di ridenominazione nell'API REST hello?**
   
    Attualmente non è possibile.

* **D. È possibile usare condivisioni annidate, ovvero una condivisione all'interno di un'altra condivisione?**
    
    No. condivisione di file Hello comporta hello virtuale che è possibile montare, in modo condivisioni annidate non sono supportate.

* **D. Uso dell'archivio file di Azure con IBM MQ**
    
    IBM ha rilasciato i clienti MQ tooguide IBM documento quando si configura l'archiviazione di File di Azure con il servizio. Per ulteriori informazioni, vedere [come toosetup IBM MQ più istanza gestore delle code con il servizio File di Microsoft Azure](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Risoluzione dei problemi
* **D. Risoluzione degli errori di archiviazione file di Azure**
    
    È possibile fare riferimento troppo[archiviazione di File di Azure articolo Troubleshooting](storage-troubleshoot-windows-file-connection-problems.md) per informazioni sulla risoluzione end-to-end. 


## <a name="see-also"></a>Vedere anche
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

### <a name="conceptual-articles-and-videos"></a>Articoli concettuali e video
* [Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Come toouse archiviazione di File di Azure con Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Supporto degli strumenti per Archiviazione file
* [Come toouse AzCopy con archiviazione di Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Con l'archiviazione di Azure hello CLI di Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Risoluzione dei problemi di archiviazione file di Azure](storage-troubleshoot-linux-file-connection-problems.md)

### <a name="blog-posts"></a>Post di BLOG
* [Archiviazione file di Azure è attualmente disponibile a livello generale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File storage (Analisi di Archiviazione file di Azure)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introduzione al servizio File di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [La migrazione dei dati tooAzure archiviazione File](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>riferimento
* [Informazioni di riferimento sulla libreria client di archiviazione per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Riferimento API REST del servizio File](http://msdn.microsoft.com/library/azure/dn167006.aspx)
