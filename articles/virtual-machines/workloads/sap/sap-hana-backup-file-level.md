---
title: aaaSAP HANA Azure Backup a livello file | Documenti Microsoft
description: Esistono due opzioni principali per il backup di SAP HANA su macchine virtuali di Azure e questo articolo descrive il backup di SAP HANA di Azure a livello di file.
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>Backup di SAP HANA di Azure a livello di file

## <a name="introduction"></a>Introduzione

Questo articolo fa parte di una serie di tre articoli correlati dedicati al backup di SAP HANA. [Guida al backup per SAP HANA in macchine virtuali di Azure](./sap-hana-backup-guide.md) fornisce una panoramica e informazioni sulle attività iniziali e [SAP HANA backup basato su snapshot di archiviazione](./sap-hana-backup-storage-snapshots.md) copre hello opzione di archiviazione basato su snapshot backup.

Esaminando hello dimensioni di macchina virtuale di Azure, si può osservare che un GS5 consente 64 dischi dati collegati. Per sistemi SAP HANA di grandi dimensioni, un numero significativo di dischi potrebbe essere già usato per i file di log e di dati, possibilmente in combinazione con RAID software per la velocità effettiva IO ottimale dei dischi. quindi domanda Hello è dove toostore SAP HANA backup di file, che potrebbe riempirsi dati hello collegato dischi nel tempo? Vedere [dimensioni per le macchine virtuali Linux in Azure](../../linux/sizes.md) per le tabelle di dimensioni di hello macchina virtuale di Azure.

Al momento, non è disponibile alcuna integrazione del backup di SAP HANA con il servizio di Backup di Azure. modalità standard di Hello toomanage backup/ripristino a livello di file hello è con un backup basato su file SAP HANA Studio o mediante istruzioni SQL di SAP HANA. Per altre informazioni, vedere [SAP HANA SQL and System Views Reference](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf) (Riferimento alle visualizzazioni del sistema e di SQL SAP HANA).

![In questa figura Mostra finestra di dialogo di hello della voce di menu backup hello in Studio di SAP HANA](media/sap-hana-backup-file-level/image022.png)

In questa figura Mostra finestra di dialogo di hello della voce di menu backup hello in Studio di SAP HANA. Quando si sceglie di tipo &quot;file&quot; toospecify uno è un percorso nel sistema di file hello in SAP HANA scrive i file di backup hello. Funzionamento del ripristino hello allo stesso modo.

Sebbene questa scelta sia semplice e diretta, è opportuno presentare alcune considerazioni. Come accennato in precedenza, una macchina virtuale di Azure presenta una limitazione nel numero di dischi di dati che è possibile collegare. Potrebbe non essere capacità toostore SAP HANA i file di backup nei sistemi file hello hello macchina virtuale, a seconda delle dimensioni di hello di hello database e disco requisiti velocità effettiva, che potrebbe comportare software RAID con striping tra dati di più dischi. Più avanti in questo articolo vengono fornite varie opzioni per lo spostamento di questi file di backup e per la gestione delle limitazioni relative alle dimensioni dei file e delle prestazioni durante la gestione di terabyte di dati.

Un'altra opzione, che offre più libertà in relazione alla capacità totale, è l'Archiviazione BLOB di Azure. Mentre un singolo blob è inoltre limitati too1 TB, capacità totale di hello di un contenitore blob singolo è attualmente 500 TB. Inoltre, offre ai clienti hello scelte tooselect cosiddetti &quot;sporadico&quot; blob di archiviazione, che offre un vantaggio di costo. Vedere [Archivio BLOB di Azure: livelli di archiviazione ad accesso frequente e sporadico](../../../storage/blobs/storage-blob-storage-tiers.md) per altre informazioni sull'archiviazione BLOB ad accesso sporadico.

Per motivi di sicurezza aggiuntivi, utilizzare un backup di archiviazione replicata geograficamente account toostore hello SAP HANA. Per dettagli sulla replica dell'account di archiviazione, vedere [Replica di Archiviazione di Azure](../../../storage/common/storage-redundancy.md).

È possibile posizionare dischi rigidi virtuali dedicati per i backup di SAP HANA in un account di archiviazione di backup apposito con replica geografica. In caso contrario uno è stato possibile copiare i dischi rigidi virtuali hello che conserva i backup di SAP HANA hello account di archiviazione replicata geograficamente tooa o account di archiviazione tooa in un'area diversa.

## <a name="azure-backup-agent"></a>Agente di Backup di Azure

Azure backup offre hello opzione toonot solo eseguire il backup completo le macchine virtuali, ma anche file e directory tramite l'agente backup hello, che ha installato nel sistema operativo guest hello toobe. Ma a partire dal 2016 dicembre, l'agente è supportato solo in Windows (vedere [backup tooAzure un client o Server Windows con modello di distribuzione di gestione risorse di hello](../../../backup/backup-configure-vault.md)).

Una soluzione alternativa è toofirst copia i file di backup di SAP HANA tooa macchina virtuale Windows in Azure (ad esempio, tramite la condivisione SAMBA) e quindi utilizzare hello agente Azure backup da qui. Sebbene sia tecnicamente possibile, potrebbe aggiungere complessità e rallentare backup hello o ripristinare processo abbastanza a causa di copia toohello tra hello Linux e macchina virtuale di Windows hello. Non è consigliabile toofollow questo approccio.

## <a name="azure-blobxfer-utility-details"></a>Dettagli sull'utilità di blobxfer di Azure

toostore directory e file in archiviazione di Azure, è possibile utilizzare CLI o PowerShell, o sviluppare uno strumento utilizzando uno dei hello [Azure SDK](https://azure.microsoft.com/downloads/). È inoltre disponibile un'utilità, pronto all'uso di AzCopy, per la copia di archiviazione dei dati tooAzure, ma è solo Windows (vedere [trasferire i dati con l'utilità della riga di comando AzCopy hello](../../../storage/common/storage-use-azcopy.md)).

Blobxfer è stato pertanto usato per la copia dei file di backup di SAP HANA. Si tratta di una risorsa open source, usata da molti clienti negli ambienti di produzione e disponibile su [GitHub](https://github.com/Azure/blobxfer). Questo strumento consente dati toocopy direttamente tooeither Azure blob storage o una condivisione di file di Azure. Offre anche una gamma di funzionalità utili, ad esempio hash md5 o parallelismo automatico durante la copia di una directory con più file.

## <a name="sap-hana-backup-performance"></a>Prestazioni del backup SAP HANA

![Questa schermata è della console backup di SAP HANA hello in Studio di SAP HANA](media/sap-hana-backup-file-level/image023.png)

Questa schermata è della console backup di SAP HANA hello in Studio di SAP HANA. Backup di circa 42 minuti toodo hello impiegato di hello 230 GB su un disco di archiviazione standard Azure singolo associata toohello HANA VM utilizzando XFS file system.

![Questa schermata è di YaST nella macchina virtuale di test di hello SAP HANA](media/sap-hana-backup-file-level/image024.png)

Questa schermata è YaST nella macchina virtuale di test SAP HANA hello. Come indicato in precedenza, si può osservare disco singolo hello di 1 TB per il backup di SAP HANA. Impiegato circa 42 minuti toobackup 230 GB. Sono stati anche associati cinque dischi da 200 GB ed è stato creato il RAID software md0 RAID, con striping su questi cinque dischi di dati di Azure.

![Ripetizione hello stesso backup RAID software con striping in cinque collegati dischi di dati standard di archiviazione Azure](media/sap-hana-backup-file-level/image025.png)

Hello ripetuta stesso backup RAID software con striping in cinque associata ora backup hello portati dischi dati di archiviazione di Azure standard da 42 minuti verso il basso too10 minuti. sono stati collegati dischi di Hello senza memorizzazione nella cache toohello macchina virtuale. Pertanto è evidente l'importanza produttività di scrittura su disco per l'ora del backup hello. Uno può quindi commutatore tooAzure premium archiviazione toofurther accelerare il processo di hello per ottenere prestazioni ottimali. In generale, l'Archiviazione Premium di Azure deve essere usata per i sistemi di produzione.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Copiare l'archiviazione blob tooAzure i file di backup di SAP HANA

Come di dicembre 2016, hello meglio i file di backup opzione tooquickly archivio SAP HANA è archiviazione blob di Azure. Un contenitore blob singolo ha un limite di 500 TB, è sufficiente per la maggior parte dei sistemi SAP HANA, in esecuzione in una macchina virtuale GS5 in Azure, i backup di SAP HANA sufficienti tookeep. I clienti hanno scelto di hello tra &quot;frequente&quot; e &quot;freddo&quot; nell'archiviazione blob (vedere [archiviazione Blob di Azure: a caldo e interessanti livelli di archiviazione](../../../storage/blobs/storage-blob-storage-tiers.md)).

Con lo strumento blobxfer hello, è facile toocopy file di backup SAP HANA hello direttamente tooAzure nell'archiviazione blob.

![Qui si possono osservare file hello di un backup completo del file SAP HANA](media/sap-hana-backup-file-level/image026.png)

Qui si possono osservare file hello di un backup completo del file SAP HANA. Esistono quattro file uno più grande hello è approssimativamente di 230 GB.

![Impiegato circa 3.000 secondi toocopy hello 230 GB tooan standard account blob contenitore di archiviazione Azure](media/sap-hana-backup-file-level/image027.png)

Nel test iniziale hello non usa l'hash md5, impiegato circa 3.000 secondi toocopy hello 230 GB tooan standard account blob contenitore di archiviazione Azure.

![In questa schermata, uno può vedere come appare nel portale di Azure hello](media/sap-hana-backup-file-level/image028.png)

In questa schermata, si può osservare come appare nel portale di Azure hello. Un contenitore blob denominato &quot;sap hana-i-backup&quot; è stato creato e include i quattro hello, che rappresentano i file di backup di hello SAP HANA. Uno di essi ha una dimensione di circa 230 GB.

console di backup HANA Studio Hello consente una dimensione massima del file di hello toorestrict HANA dei file di backup. Nell'ambiente di esempio hello, prestazioni migliorate, rendendo possibili toohave file più i backup più piccoli, anziché un file di 230 GB di grandi dimensioni.

![L'impostazione del limite di dimensioni file di backup di hello hello HANA lato &#39; t migliorare i tempi di backup hello](media/sap-hana-backup-file-level/image029.png)

L'impostazione del limite di dimensioni file di backup di hello hello HANA lato &#39; t tempi hello backup, perché i file hello vengono scritti in modo sequenziale, come illustrato nella figura seguente. limite delle dimensioni file Hello è stato impostato too60 GB, in modo backup hello creati quattro file di dati di grandi dimensioni anziché hello 230 GB file singolo.

![parallelismo tootest dello strumento blobxfer hello, hello dimensione massima del file per i backup HANA impostato quindi too15 GB](media/sap-hana-backup-file-level/image030.png)

parallelismo tootest dello strumento blobxfer hello, hello dimensione massima del file per i backup HANA impostato quindi too15 GB, che hanno comportato 19 file di backup. Questa configurazione attivata la modalità tempo hello per l'archiviazione blob di blobxfer toocopy hello 230 GB tooAzure da 3.000 secondi verso il basso too875 secondi.

Il risultato è dovuto toohello il limite di 60 MB/sec per la scrittura di un blob di Azure. Il parallelismo tramite più BLOB risolve collo di bottiglia hello, ma non esiste un svantaggio: miglioramento delle prestazioni di hello blobxfer strumento toocopy tutti questi tooAzure HANA con i file di backup nell'archiviazione blob inserisce carico hello HANA VM e rete hello. Ne è interessato il funzionamento del sistema HANA.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Copia di BLOB dei dischi di dati di Azure dedicati nel RAID software di backup

A differenza di hello manuale VM disco backup dei dati, con questo approccio uno non eseguire il backup di tutti i dischi dati hello in una macchina virtuale toosave hello intero SAP installazione, inclusi i dati HANA HANA registra i file e i file di configurazione. Al contrario, hello idea è RAID software toohave dedicato con striping tra più dischi rigidi virtuali dati Azure per archiviare un backup completo del file SAP HANA. Una copia solo i dischi che dispone di backup di SAP HANA hello. Può facilmente essere conservate in un account di archiviazione di backup HANA dedicato o collegato tooa dedicato &quot;backup Gestione VM&quot; per un'ulteriore elaborazione.

![Sono stati copiati tutti i dischi rigidi virtuali interessati utilizzando hello * * start-azurestorageblobcopy * * il comando di PowerShell](media/sap-hana-backup-file-level/image031.png)

Dopo il RAID software toohello backup locale hello è stato completato, tutti i dischi rigidi virtuali interessati sono stati copiati utilizzando hello **inizio azurestorageblobcopy** comando di PowerShell (vedere [inizio AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Poiché influisce solo sul sistema file hello dedicato per mantenere i file di backup hello, non esistono alcun problemi relativi a SAP HANA dati o log della coerenza del file su disco hello. Un vantaggio di questo comando è che funziona mentre hello VM rimane online. toobe determinati che nessun processo scrive un set di backup di striping toohello, essere toounmount assicurarsi prima hello copia del blob e crearla nuovamente in seguito. O è Impossibile utilizzare un appropriato troppo&quot;bloccare&quot; sistema file hello. Ad esempio, tramite xfs\_bloccare per hello XFS del file system.

![Questa schermata Mostra elenco hello di BLOB nel contenitore di dischi rigidi virtuali hello sul hello portale di Azure](media/sap-hana-backup-file-level/image032.png)

Questa schermata Mostra elenco hello di BLOB in hello &quot;dischi rigidi virtuali&quot; contenitore nel portale di Azure hello. schermata Hello Mostra hello cinque dischi rigidi virtuali, che sono stati collegati toohello SAP HANA server VM tooserve come hello software RAID tookeep SAP HANA i file di backup. Viene inoltre cinque copie, che sono state eseguite tramite comando di copia blob hello hello.

![A scopo di test, le copie di dischi RAID software di backup di SAP HANA hello hello sono stati macchina virtuale del server collegato toohello app](media/sap-hana-backup-file-level/image033.png)

A scopo di test, copie hello di dischi RAID software di backup di SAP HANA hello sono macchina virtuale del server collegato toohello app.

![il server di app Hello VM è stato arrestato copie del disco di hello tooattach](media/sap-hana-backup-file-level/image034.png)

il server di app Hello VM è stato arrestato tooattach hello disco copie. Dopo l'avvio hello macchine Virtuali, dischi hello e hello RAID, sono stati rilevati correttamente (montato tramite UUID). Solo il punto di montaggio hello è manca, cui è stato creato tramite partitioner YaST hello. In seguito le copie dei file di backup SAP HANA hello è diventata visibile sul livello del sistema operativo.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Copiare i file di backup di SAP HANA tooNFS condividere

toolessen hello potenziale impatto sulle hello sistema SAP HANA da un punto di vista dello spazio su disco o di prestazioni, è potrà considerare l'archiviazione dei file di backup SAP HANA hello in una condivisione NFS. Tecnicamente funziona, ma significa utilizzando una seconda macchina virtuale di Azure come host di hello di hello che condivisioni NFS. Non deve essere di piccole dimensioni di macchina virtuale, a causa di larghezza di banda della rete VM toohello. Sarebbe più utile quindi tooshut verso il basso questo &quot;backup VM&quot; e portarlo solo per l'esecuzione di backup di SAP HANA hello. La scrittura in una condivisione NFS condivisione inserita carico sulla rete di hello e impatto hello sistema SAP HANA, ma semplicemente la gestione di file di backup in un secondo momento nel hello hello &quot;backup VM&quot; non influirebbe sistema SAP HANA hello affatto.

![Una condivisione NFS da un'altra macchina virtuale di Azure è stato montato toohello macchina virtuale del server SAP HANA](media/sap-hana-backup-file-level/image035.png)

caso d'uso tooverify hello NFS, una condivisione NFS da un'altra macchina virtuale di Azure è stato montato toohello macchina virtuale del server SAP HANA. Non è stata applicata alcuna ottimizzazione NFS particolare.

![Backup di 1 ora e 46 minuti toodo hello impiegato direttamente](media/sap-hana-backup-file-level/image036.png)

condivisione NFS Hello è un set di striping veloce, ad esempio hello nel server SAP HANA hello. Tuttavia, sono stati impiegati 1 ora e hello toodo 46 minuti backup direttamente in una condivisione NFS hello invece di 10 minuti, durante la scrittura di un set di striping locale tooa.

![In alternativa Hello non è stata molto più rapidamente in 1 ora e 43 minuti](media/sap-hana-backup-file-level/image037.png)

condivisioni NFS alternativa Hello di eseguire un set di striping locale tooa backup e copia toohello sul livello del sistema operativo (una semplice **cp - avr** comando) non è stata molto più rapidamente. Ha impiegato 1 ora e 43 minuti.

In modo funziona, ma le prestazioni non è stata utile per test di backup di hello 230 GB. La situazione dovrebbe essere ancora più grave per più terabyte.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Servizio file tooAzure di SAP HANA i file di backup di copia

È possibile toomount condividere un file di Azure all'interno di una macchina virtuale Linux di Azure. articolo Hello [come archiviazione di File di Azure con Linux toouse](../../../storage/files/storage-how-to-use-files-linux.md) fornisce informazioni dettagliate su come toodo è. Tenere presente che esiste attualmente un limite di quota di 5 TB di una condivisione di file di Azure e un limite di dimensione del file di 1 TB per ogni file. Per altre informazioni sui limiti di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](../../../storage/common/storage-scalability-targets.md).

I test hanno dimostrato, tuttavia, che il backup di SAP HANA non funziona direttamente con questo tipo di montaggio CIFS. Nella [Nota SAP 1820529](https://launchpad.support.sap.com/#/notes/1820529) si dichiara anche che il CIFS non è consigliato.

![In questa figura mostra un errore nella finestra di dialogo backup hello in Studio di SAP HANA](media/sap-hana-backup-file-level/image038.png)

In questa figura mostra un errore nella finestra di dialogo backup hello in Studio di SAP HANA, durante il tentativo di tooback direttamente tooa condivisione di file di Azure montato CIFS. In modo che uno è toodo un backup standard di SAP HANA in un file system di macchina virtuale prima e quindi di file di backup di copia hello da tooAzure sono servizio file.

![Questa figura mostra che richiedeva 929 secondi toocopy 19 SAP HANA file di backup](media/sap-hana-backup-file-level/image039.png)

Questa figura mostra impiegato sui 929 secondi toocopy 19 SAP HANA i file di backup con una dimensione totale di circa condivisione di file di Azure toohello 230 GB.

![struttura di directory di origine Hello nella macchina virtuale di SAP HANA hello è stato copiato toohello condivisione di file di Azure](media/sap-hana-backup-file-level/image040.png)

In questa schermata, si può osservare che hello origine struttura di directory hello SAP HANA VM è stato copiato toohello condivisione di file di Azure: una directory (hana\_backup\_fsl\_15 gb) e 19 singoli file di backup.

Archiviare i file di backup di SAP HANA nel file di Azure potrebbe essere un'opzione interessano in futuro hello durante i backup dei file di SAP HANA supporta direttamente. Quando non è più possibile toomount i file di Azure tramite NFS e limite massimo di quota hello è notevolmente superiore a 5 TB.

## <a name="next-steps"></a>Passaggi successivi
* La [Guida del backup di SAP HANA in Macchine virtuali di Azure](sap-hana-backup-guide.md) offre una panoramica e informazioni introduttive.
* [Backup di SAP HANA in base agli snapshot di archiviazione](sap-hana-backup-storage-snapshots.md) descrive hello archiviazione basata su snapshot opzione di backup.
* toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md).
