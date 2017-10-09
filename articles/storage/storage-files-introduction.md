---
title: aaaIntroduction tooAzure archiviazione File | Documenti Microsoft
description: Una panoramica dell'archiviazione di File di Azure, un servizio che consente di toocreate e utilizzare file di rete nelle condivisioni di hello Microsoft Cloud utilizzando hello standard di settore.
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
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Introduzione tooAzure archiviazione File
Archiviazione di File di Azure offre le condivisioni file di rete in un cloud di hello tramite standard di settore hello [protocollo Server Message Block (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) e [Common Internet File System (CIFS)](https://technet.microsoft.com/library/cc939973.aspx). Le condivisioni file di Azure possono essere montate contemporaneamente da client come distribuzioni locali di Windows, macOS o Linux o da Macchine virtuali di Azure. Consente di account di archiviazione generico accedere tooAzure archiviazione di File e altri servizi, ad esempio BLOB, i dischi di macchina virtuale di Azure, le code in un singolo account.



## <a name="videos"></a>Video
| Introduzione ad Archiviazione file di Azure (27 minuti) | Esercitazione su Archiviazione file di Azure (5 minuti)  |
|-|-|
| [![ScreenCap del video di archiviazione di introduzione a Azure File hello - fare clic su tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![ScreenCap hello Azure archiviazione dei File esercitazione, fare clic su tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Vantaggi offerti da Archiviazione file di Azure
Archiviazione di File di Azure consente tooreplace Server Windows, Linux, o file server basati su NAS ospitato in locale o nel cloud hello con un file di cloud del sistema operativo senza condividere. Questo approccio sono hello seguenti vantaggi:

* **Accesso condiviso**. Settore hello supporto protocollo SMB standard, ciò significa che è possibile sostituire facilmente le condivisioni di file locale con le condivisioni File di Azure senza doversi preoccupare di compatibilità delle applicazioni di condivisioni di File di Azure. Essere in grado di tooshare un file system tra più computer, applicazioni o le istanze è un vantaggio significativo di archiviazione di File di Azure per le applicazioni che necessitano di facilità di condivisione. 
* **Soluzione completamente gestita**. È possibile creare condivisioni di File di Azure senza hardware toomanage necessità di hello o un sistema operativo. Ciò significa che non si dispone di toodeal con l'applicazione di patch SO server hello con gli aggiornamenti critici della protezione o la sostituzione di dischi rigidi difettosi.
* **Script e strumenti**. I cmdlet di PowerShell e CLI di Azure possono essere utilizzati toocreate, montare e gestire le condivisioni File archiviazione come parte dell'amministrazione hello di applicazioni Azure. È possibile creare e gestire le condivisioni di file di Azure tramite il portale di Azure e Azure storage Explorer. 
* **Resilienza**. Archiviazione di File di Azure è stata compilata dalla hello messa a terra backup toobe sempre disponibile. Sostituendo le condivisioni di file locale con File di Azure storage significa che non è più necessario toowake backup toodeal con interruzioni dell'alimentazione locale o di problemi di rete. 
* **Programmabilità nota**. Le applicazioni in esecuzione in Azure possono accedere i dati nella condivisione di hello tramite file [sistema I/O APIs](https://msdn.microsoft.com/library/system.io.file.aspx). Gli sviluppatori possono pertanto sfruttare le applicazioni esistenti di competenze toomigrate codice esistente. Inoltre tooSystem le API dei / o, è possibile utilizzare [le librerie Client di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dn261237.aspx) o hello [API REST di archiviazione Azure](/rest/api/storageservices/file-service-rest-api).

Le condivisioni file di Azure possono essere usate per gli scopi seguenti:

* **Sostituire file server locali**  
    Archiviazione di File Azure può essere utilizzato toocompletely Sostituisci condivisioni di file locali tradizionali file server o i dispositivi NAS. Sistemi operativi, ad esempio Windows, macOS e Linux, è possibile montare facilmente una condivisione di File di Azure ovunque si trovino in HelloWorld.

* **Trasferire in modalità lift-and-shift le applicazioni**  
    Archiviazione di File di Azure semplifica troppo "sollevare e spostare" cloud toohello di applicazioni che utilizzano il file locale condivide dati tooshare tra le parti di un'applicazione hello. toomake succedere, ogni macchina virtuale si connette toohello condivisione di file e quindi è possibile leggere e scrivere file esattamente come rispetto a un file locale condividerebbero.

* **Semplificare lo sviluppo per il cloud**  
    Archiviazione di File Azure può essere utilizzata in molti modi diversi toosimplify nuovi cloud progetti di sviluppo.
    * **Impostazioni delle applicazioni condivise**  
        Un modello comune per le applicazioni distribuite è toohave i file di configurazione in una posizione centralizzata in cui è possibile accedervi da molte macchine virtuali diverse. Tali file di configurazione possono ora essere archiviati in una condivisione file di Azure ed essere letti da tutte le istanze delle applicazioni. Queste impostazioni possono essere gestite anche tramite l'interfaccia REST hello, che consente l'accesso in tutto il mondo toohello i file di configurazione.

    * **Condivisione di diagnostica**  
        Una condivisione di File di Azure può inoltre essere utilizzati toosave file diagnostici quali registri, metriche e dump di arresto anomalo. Con questi disponibile tramite SMB hello e interfaccia REST consente applicazioni toobuild o utilizzare un'ampia gamma di strumenti di analisi per l'elaborazione e analisi dei dati di diagnostica hello.

    * **Sviluppo/test/debug**  
        Quando gli sviluppatori o gli amministratori utilizzano in macchine virtuali nel cloud hello, devono spesso un set di strumenti o utilità. L'installazione e la distribuzione di queste utilità in ogni macchina virtuale in cui sono necessarie possono richiedere molto tempo. Con l'archiviazione di File di Azure, uno sviluppatore o un amministratore può archiviare gli strumenti preferiti in una condivisione file, che può essere facilmente connesso toofrom qualsiasi macchina virtuale.
        
## <a name="how-does-it-work"></a>Come funziona?
Gestire le condivisioni file di Azure è molto più semplice che gestire le condivisioni file in locale. Hello seguente diagramma illustra i costrutti di gestione archiviazione File di Azure hello:

![Struttura di Archiviazione file](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Account di archiviazione**: tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione. Per informazioni sulla capacità degli account di archiviazione, vedere gli obiettivi di scalabilità e prestazioni per Archiviazione di Azure.
* **Condivisione**: una condivisione di Archiviazione file è una condivisione file SMB in Azure. Tutte le directory e i file devono essere creati in una condivisione padre. Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, backup toohello 5 TB di capacità totale della condivisione file hello.
* **Directory**: una gerarchia di directory facoltativa.
* **File**: un file nella condivisione di hello. Un file può essere up too1 TB nella dimensione.
* **Formato URL**: i file sono indirizzabili mediante hello seguendo il formato di URL:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Passaggi successivi
* [Creare una condivisione file di Azure](storage-file-how-to-create-file-share.md)
* [Eseguire la connessione e il montaggio in Windows](storage-file-how-to-use-files-windows.md)
* [Eseguire la connessione e il montaggio in Linux](storage-how-to-use-files-linux.md)
* [Eseguire la connessione e il montaggio in macOS](storage-file-how-to-use-files-mac.md)
* [Domande frequenti](storage-files-faq.md)
* [Risoluzione dei problemi](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Articoli concettuali e video
* [Azure File storage: a frictionless cloud SMB file system for Windows and Linux (Archiviazione file di Azure: un file system SMB nel cloud senza conflitti per Windows e Linux)](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Supporto degli strumenti per Archiviazione file di Azure
* [Uso di Azure PowerShell con Archiviazione di Azure](storage-powershell-guide-full.md)
* [Come toouse AzCopy con archiviazione di Microsoft Azure](storage-use-azcopy.md)
* [Con l'archiviazione di Azure hello CLI di Azure](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Post di BLOG
* [Archiviazione file di Azure è attualmente disponibile a livello generale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File storage (Analisi di Archiviazione file di Azure)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introduzione al servizio File di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [La migrazione dei dati tooAzure File](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>riferimento
* [Informazioni di riferimento sulla libreria client di archiviazione per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Riferimento API REST del servizio File](http://msdn.microsoft.com/library/azure/dn167006.aspx)
