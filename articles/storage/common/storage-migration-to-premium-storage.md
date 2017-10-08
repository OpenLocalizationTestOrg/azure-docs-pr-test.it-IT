---
title: macchine virtuali di aaaMigrating tooAzure archiviazione Premium | Documenti Microsoft
description: Eseguire la migrazione del tooAzure macchine virtuali esistenti, archiviazione Premium. Archiviazione Premium offre prestazioni elevate e supporto per dischi a bassa latenza per carichi di lavoro con I/O intensivo in esecuzione su Macchine virtuali di Azure.
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Migrazione tooAzure archiviazione Premium (dischi non gestite)

> [!NOTE]
> Questo articolo viene illustrato come una macchina virtuale che utilizza dischi standard non gestito tooa macchina virtuale che utilizza toomigrate non gestito i dischi premium. È consigliabile usare dischi gestiti di Azure per nuove macchine virtuali e convertire i dischi di toomanaged precedente dischi non gestito. Account archiviazione sottostante dei dischi handle hello gestiti in modo non è necessario. Per altre informazioni, vedere [Panoramica di Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).
>

Archiviazione Premium di Azure offre prestazioni elevate e supporto per dischi a bassa latenza per le macchine virtuali che eseguono carichi di lavoro con I/O intensivo. È possibile sfruttare la velocità di hello e le prestazioni di questi dischi eseguendo la migrazione tooAzure dischi di macchina virtuale dell'applicazione archiviazione Premium.

scopo di Hello di questa guida è toohelp nuovi utenti di archiviazione di Azure Premium migliori preparare toomake una transizione graduale da loro tooPremium sistema corrente di archiviazione. Guida di Hello indirizzi tre componenti principali di hello in questo processo:

* [Pianificare la migrazione di hello tooPremium archiviazione](#plan-the-migration-to-premium-storage)
* [Preparare e copia dischi rigidi virtuali (VHD) tooPremium archiviazione](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Creare una macchina virtuale di Azure usando Archiviazione Premium](#create-azure-virtual-machine-using-premium-storage)

È possibile eseguire la migrazione di macchine virtuali da altri tooAzure piattaforme archiviazione Premium o eseguire la migrazione di macchine virtuali di Azure esistente da archiviazione Standard tooPremium archiviazione. Questa guida illustra i passaggi per entrambi i due scenari. Seguire i passaggi di hello specificati nella sezione appropriata di hello a seconda dello scenario.

> [!NOTE]
> Una panoramica delle funzionalità e dei prezzi di Archiviazione Premium è disponibile in [Archiviazione Premium: archiviazione dalle prestazioni elevate per carichi di lavoro di macchine virtuali di Azure](storage-premium-storage.md). È consigliabile eseguire la migrazione di un disco di macchina virtuale che richiedono tooAzure IOPS elevata archiviazione Premium per ottenere prestazioni ottimali per l'applicazione hello. Se il disco non richiede un numero elevato di IOPS, è possibile limitare i costi mantenendolo in Archiviazione Standard, che archivia i dati dei dischi delle macchine virtuali in unità disco rigido (HDD) invece che in unità SSD.
>

Completare il processo di migrazione hello nella sua interezza richiedano azioni aggiuntive prima e dopo i passaggi di hello forniti in questa Guida. Ad esempio la configurazione di reti virtuali o gli endpoint o apportare modifiche al codice all'interno di un'applicazione hello stesso che potrebbero richiedere tempi di inattività dell'applicazione. Queste azioni sono univoci tooeach applicazione e si dovrebbero essere completate insieme ai passaggi hello forniti in questo tooPremium completo della transizione di hello toomake Guida archiviazione più semplice possibile.

## <a name="plan-the-migration-to-premium-storage"></a>Pianificare la migrazione di hello tooPremium archiviazione
In questa sezione garantisce che sono pronti toofollow passaggi della migrazione hello in questo articolo e consente di decisione migliore di hello toomake sui tipi di macchina virtuale e disco.

### <a name="prerequisites"></a>Prerequisiti
* È necessaria una sottoscrizione di Azure. Se non è disponibile, è possibile creare una sottoscrizione di [valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/) di un mese oppure visitare [Prezzi di Azure](https://azure.microsoft.com/pricing/) per altre opzioni.
* tooexecute i cmdlet di PowerShell, è necessario il modulo di Microsoft Azure PowerShell hello. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per hello installare istruzioni sull'installazione e punto.
* Quando si pianifica toouse macchine virtuali di Azure in esecuzione in archiviazione Premium, è necessario toouse hello macchine virtuali in grado di archiviazione Premium. Con le VM che supportano Archiviazione Premium è possibile usare dischi sia di Archiviazione Standard che di Archiviazione Premium. I dischi di archiviazione Premium saranno disponibili con più tipi di macchine Virtuali in hello future. Per altre informazioni su tutte le dimensioni e su tutti i tipi di dischi disponibili per le macchine virtuali di Azure, vedere [Dimensioni delle macchine virtuali](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [Dimensioni dei servizi cloud](../../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Considerazioni
Una macchina virtuale di Azure supporta collegamento di più dischi di archiviazione Premium in modo che le applicazioni possono esistere fino a too256 TB di spazio di archiviazione per ogni macchina virtuale. Con Archiviazione Premium le applicazioni possono raggiungere 80.000 IOPS (operazioni di input/output al secondo) per ogni macchina virtuale e 2000 MB al secondo di velocità effettiva dei dischi per ogni macchina virtuale, con una latenza estremamente bassa per le operazioni di lettura. Sono disponibili diverse opzioni in termini di macchine virtuali e dischi. In questa sezione è toohelp si toofind un'opzione più adatta al carico di lavoro.

#### <a name="vm-sizes"></a>Dimensioni delle macchine virtuali
sono elencate le specifiche sulle dimensioni di macchina virtuale di Azure Hello in [dimensioni per le macchine virtuali](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Verificare le caratteristiche di prestazioni hello delle macchine virtuali che funzionano con archiviazione Premium e scegliere le dimensioni di macchina virtuale più appropriata hello più adatta al carico di lavoro. Assicurarsi che vi sia sufficiente larghezza di banda disponibile nel traffico VM toodrive hello disco.

#### <a name="disk-sizes"></a>Dimensione disco
È possibile usare cinque tipi di dischi con la VM, ognuno con limiti di velocità effettiva e IOP specifici. Prendere in considerazione questi limiti quando scegliendo il tipo di disco hello per la macchina virtuale in base alle esigenze di hello dell'applicazione in termini di capacità, prestazioni, scalabilità e carichi di picco.

| Tipo di disco Premium  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Dimensioni disco           | 128 GB| 512 GB| 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| IOPS per disco       | 500   | 2300  | 5000           | 7500           | 7500           | 
| Velocità effettiva per disco | 100 MB al secondo | 150 MB al secondo | 200 MB al secondo | 250 MB al secondo | 250 MB al secondo |

A seconda del carico di lavoro, determinare se per la macchina virtuale in uso sono necessari dischi dati aggiuntivi. È possibile collegare più dati persistenti dischi tooyour macchina virtuale. Se necessario, è possibile eseguire lo striping tra hello dischi tooincrease hello capacità e prestazioni del volume hello. Per altre informazioni sullo striping del disco, vedere [qui](storage-premium-storage-performance.md#disk-striping). Se si esegue lo striping di dischi dati di Archiviazione Premium con [Spazi di archiviazione][4], è consigliabile configurare una colonna per ogni disco usato. In caso contrario, hello complessivo delle prestazioni del volume con striping hello potrebbero essere inferiore al previsto a causa di toouneven distribuzione del traffico tra dischi hello. Per le macchine virtuali Linux è possibile utilizzare hello *mdadm* tooachieve utilità hello stesso. Per informazioni dettagliate, vedere l'articolo sulla [configurazione del RAID software in Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .

#### <a name="storage-account-scalability-targets"></a>Obiettivi di scalabilità per gli account di archiviazione
Account di archiviazione Premium sono hello seguenti obiettivi di scalabilità in aggiunta toohello [Azure obiettivi di scalabilità e prestazioni](storage-scalability-targets.md). Se i requisiti dell'applicazione superano obiettivi di scalabilità hello di un singolo account di archiviazione, compilare l'applicazione toouse più account di archiviazione e partizionare i dati in tali account di archiviazione.

| Capacità account totale | Larghezza di banda totale per un account di archiviazione con ridondanza locale |
|:--- |:--- |
| Capacità disco : 35 TB<br />Capacità snapshot: 10 TB |Backup too50 Gigabit al secondo in entrata e in uscita |

Per ulteriori informazioni sulle specifiche di archiviazione Premium di hello, estrarre [obiettivi di scalabilità e prestazioni quando si utilizza l'archiviazione Premium](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Criteri di memorizzazione nella cache su disco
Per impostazione predefinita, la memorizzazione nella cache dei criteri di disco è *Read-Only* per tutti i dischi dati Premium, di hello e *lettura-scrittura* al disco del sistema operativo Premium hello associato toohello macchina virtuale. Questa impostazione di configurazione è consigliata tooachieve hello ottenere prestazioni ottimali per IOs dell'applicazione. Per i dischi di dati con un utilizzo elevato della scrittura o di sola scrittura (ad esempio i file di log di SQL Server), disabilitare la memorizzazione nella cache su disco in modo da migliorare le prestazioni delle applicazioni. le impostazioni della cache di Hello per i dischi di dati esistente possono essere aggiornate mediante [portale Azure](https://portal.azure.com) o hello *- HostCaching* parametro di hello *Set-AzureDataDisk* cmdlet.

#### <a name="location"></a>Percorso
Selezionare una posizione in cui è disponibile il servizio Archiviazione Premium di Azure. Per informazioni aggiornate sulle località disponibili, vedere [Prodotti in base all'area](https://azure.microsoft.com/regions/#services) . Le macchine virtuali presenti in hello stessa area, come account di archiviazione che archivi hello dischi per hello VM offrirà prestazioni migliori rispetto a se si trovano in aree separate hello.

#### <a name="other-azure-vm-configuration-settings"></a>Altre impostazioni di configurazione delle macchine virtuali di Azure
Quando si crea una macchina virtuale di Azure, sarà richiesto tooconfigure determinate impostazioni della macchina virtuale. Tenere presente che alcune impostazioni sono fisse per la durata di hello di hello macchina virtuale, mentre è possibile modificare o aggiungere altri utenti in un secondo momento. Esaminare queste impostazioni di configurazione della macchina virtuale di Azure e assicurarsi che questi siano configurati in modo appropriato toomatch i requisiti del carico di lavoro.

### <a name="optimization"></a>Ottimizzazione
L'articolo [Archiviazione Premium di Azure: progettata per prestazioni elevate](storage-premium-storage-performance.md) fornisce indicazioni per lo sviluppo di applicazioni a prestazioni elevate mediante l'Archiviazione Premium di Azure. È possibile seguire le linee guida hello combinate con prestazioni migliori procedure consigliate applicabile tootechnologies utilizzati dall'applicazione.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Preparare e copiare i dischi rigidi virtuali (VHD) tooPremium archiviazione
Hello seguente sezione vengono fornite linee guida per la preparazione di dischi rigidi virtuali dalla macchina virtuale e copia di dischi rigidi virtuali tooAzure archiviazione.

* [Scenario 1: "in corso la migrazione tooAzure macchine virtuali di Azure esistente archiviazione Premium."](#scenario1)
* [Scenario 2: "in corso la migrazione macchine virtuali da altri tooAzure piattaforme archiviazione Premium."](#scenario2)

### <a name="prerequisites"></a>Prerequisiti
hello tooprepare dischi rigidi virtuali per la migrazione, è necessario:

* Una sottoscrizione di Azure, un account di archiviazione e un contenitore di archiviazione account toowhich è possibile copiare il disco rigido virtuale. Si noti che l'account di archiviazione di destinazione hello può essere un account Standard o Premium archiviazione in base alle esigenze.
* Un hello toogeneralize strumento disco rigido virtuale se si prevede di toocreate più istanze di macchina virtuale da esso. Ad esempio, sysprep per Windows o virt-sysprep per Ubuntu.
* Un strumento tooupload hello VHD file toohello account di archiviazione. Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md) o utilizzare un [Esplora archivi Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Questa guida viene descritto come copiare il disco rigido virtuale utilizzando lo strumento AzCopy hello.

> [!NOTE]
> Se si sceglie l'opzione copia sincrono con AzCopy, per ottenere prestazioni ottimali, copiare il disco rigido virtuale eseguendo uno di questi strumenti da una macchina virtuale di Azure in hello stessa regione dell'account di archiviazione di destinazione hello. Se si copia un disco rigido virtuale da una macchina virtuale di Azure in un'area diversa, le prestazioni potrebbero essere più lente.
>
> Per copiare una grande quantità di dati in larghezza di banda limitata, prendere in considerazione [tramite servizio di importazione/esportazione di Azure hello, dati tootransfer tooBlob archiviazione](../storage-import-export-service.md); in questo modo si tootransfer i dati dal disco rigido shipping unità tooan Azure Data Center. È possibile utilizzare importazione/esportazione di Azure servizio toocopy dati tooa account di archiviazione standard solo hello. Una volta hello dati nell'account di archiviazione standard, è possibile utilizzare entrambi hello [API di copia Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) o account di archiviazione di AzCopy tootransfer hello dati tooyour premium.
>
> Notare che Microsoft Azure supporta solo file di disco rigido virtuale a dimensione fissa. I file VHDX o i dischi rigidi virtuali dinamici non sono supportati. Se si dispone di un disco rigido virtuale dinamico, è possibile convertirlo toofixed dimensioni utilizzando hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.
>
>

### <a name="scenario1"></a>Scenario 1: "in corso la migrazione tooAzure macchine virtuali di Azure esistente archiviazione Premium."
Se si esegue la migrazione di macchine virtuali di Azure, hello arresta macchina virtuale esistente preparare i dischi rigidi virtuali per ogni tipo di hello del disco rigido virtuale desiderata e quindi copiare hello VHD con AzCopy o PowerShell.

Hello VM deve toobe completamente verso il basso toomigrate uno stato pulito. Sarà presente un tempo di inattività fino al completamento della migrazione hello.

#### <a name="step-1-prepare-vhds-for-migration"></a>Passaggio 1. Preparare i dischi rigidi virtuali per la migrazione
Se si esegue la migrazione tooPremium macchine virtuali di Azure esistente archiviazione, potrebbe essere il disco rigido virtuale:

* Un'immagine del sistema operativo generalizzata
* Un disco di sistema operativo univoco
* Un disco dati

Di seguito vengono illustrati tre scenari per la preparazione dei dischi rigidi virtuali.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Utilizzare un toocreate disco rigido virtuale del sistema operativo generalizzato più istanze di macchina virtuale
Se si siano caricando un disco rigido virtuale che verrà utilizzato toocreate più istanze di macchina virtuale di Azure generiche, è innanzitutto necessario generalizzare VHD utilizzando un'utilità sysprep. Si applica tooa disco rigido virtuale che si trova in locale o nel cloud hello. Sysprep consente di rimuove le informazioni specifiche del computer hello disco rigido virtuale.

> [!IMPORTANT]
> Eseguire un'istantanea o il backup della macchina virtuale prima di generalizzarla. Interrompe e deallocare hello VM istanza in esecuzione sysprep. Attenersi alla procedura riportata di seguito toosysprep un disco rigido virtuale del sistema operativo Windows. Si noti che esegue il comando di Sysprep hello richiederà tooshut macchina virtuale hello verso il basso. Per altre informazioni su Sysprep, vedere la [panoramica di Sysprep](http://technet.microsoft.com/library/hh825209.aspx) oppure il [materiale di riferimento tecnico di Sysprep](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Aprire una finestra del Prompt dei comandi come amministratore.
2. Immettere hello seguente tooopen comando Sysprep:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Selezionare sistema immettere Out-of-Box configurazione guidata, casella di controllo selezionare hello Generalize hello System Preparation Tool, selezionare **arresto**, quindi fare clic su **OK**, come illustrato nell'immagine di hello riportata di seguito. Sysprep verrà generalizzare hello del sistema operativo e arresta il sistema hello.

    ![][1]

Per una VM Ubuntu, utilizzare virt sysprep tooachieve hello stesso. Vedere [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) per ulteriori informazioni. Vedere anche alcune open source di hello [il Provisioning di Server Linux software](http://www.cyberciti.biz/tips/server-provisioning-software.html) per altri sistemi operativi Linux.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Utilizzare un toocreate disco rigido virtuale del sistema operativo univoco di una singola istanza di macchina virtuale
Se si dispone di un'applicazione in esecuzione nella macchina virtuale che richiede dati specifici di hello macchina hello, non generalizzare hello disco rigido virtuale. Un disco rigido virtuale generalizzato non può essere utilizzato toocreate un'unica istanza di macchina virtuale di Azure. Ad esempio, se si dispone di Controller di dominio sul disco rigido virtuale, l'esecuzione di sysprep lo renderà inefficace come controller di dominio. Esaminare le applicazioni di hello nella macchina virtuale e hello impatto dell'esecuzione di sysprep su di essi prima della generalizzazione hello disco rigido virtuale.

##### <a name="register-data-disk-vhd"></a>Registrare un disco rigido virtuale di dischi dati
Se dispone di dischi di dati in Azure toobe eseguita la migrazione, è necessario assicurarsi che macchine virtuali di hello che utilizzano questi dati vengono arrestati i dischi.

Seguire i passaggi hello descritti di seguito toocopy VHD tooAzure archiviazione Premium e registrarlo come disco dati di provisioning.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Passaggio 2. Creare hello destinazione per il disco rigido virtuale
Creare un account di archiviazione per mantenere i dischi rigidi virtuali. Considerare i seguenti punti quando si pianifica dove hello toostore i dischi rigidi virtuali:

* destinazione Hello account di archiviazione Premium.
* posizione dell'account di archiviazione Hello deve essere uguale a archiviazione Premium macchine virtuali di Azure in grado di supportare verrà creato nella fase finale hello. È possibile copiare il nuovo account di archiviazione tooa o hello toouse piano stesso account di archiviazione in base alle proprie esigenze.
* Copiare e salvare una chiave di account di archiviazione hello hello destinazione dell'account di archiviazione per la fase successiva hello.

Per i dischi dati, è possibile scegliere tookeep alcuni dischi dati in un account di archiviazione standard (ad esempio, i dischi che dispongono di archiviazione di dispositivo di raffreddamento), ma è fortemente consigliabile spostare tutti i dati per l'archiviazione premium toouse del carico di lavoro di produzione.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>Passaggio 3. Copia del disco rigido virtuale con AzCopy o PowerShell
Il percorso del contenitore e l'account tooprocess chiave una di queste due opzioni di archiviazione, sarà necessario toofind. Il percorso del contenitore e la chiave dell'account di archiviazione sono reperibili in **Portale di Azure** > **Archiviazione**. URL del contenitore Hello sarà ad esempio "https://myaccount.blob.core.windows.net/mycontainer/".

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Opzione 1: copia di un disco rigido virtuale con AzCopy (copia asincrona)
Utilizza AzCopy, è possibile caricare hello VHD su hello Internet. A seconda delle dimensioni di hello di hello dischi rigidi virtuali, l'operazione potrebbe richiedere tempo. Quando si utilizza questa opzione, ricordare limiti di ingresso/uscita account di archiviazione di toocheck hello. Vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) per i dettagli.

1. Scaricare e installare AzCopy da qui: [versione più recente di AzCopy](http://aka.ms/downloadazcopy)
2. Aprire Azure PowerShell e passare toohello cartella in cui è installato AzCopy.
3. Comando che segue di hello utilizzare file di disco rigido virtuale toocopy hello "Origine" troppo "Destination".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Esempio:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Ecco le descrizioni dei parametri di hello utilizzati nel comando AzCopy hello:

   * **/ Origine:  *&lt;origine&gt;:***  percorso della cartella di hello o URL del contenitore dell'archiviazione che contiene hello disco rigido virtuale.
   * **/ SourceKey:  *&lt;chiave dell'account origine&gt;:***  chiave account di archiviazione dell'account di archiviazione di origine hello.
   * **/ Dest:  *&lt;destinazione&gt;:***  toocopy URL contenitore di archiviazione hello disco rigido virtuale.
   * **/ DestKey:  *&lt;chiave dell'account dest&gt;:***  chiave account di archiviazione dell'account di archiviazione di destinazione hello.
   * **/ Modello:  *&lt;nome file&gt;:***  specifica il nome di file di hello di hello toocopy di disco rigido virtuale.

Per informazioni dettagliate sull'uso di AzCopy strumento, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Opzione 2: copia di un disco rigido virtuale con PowerShell (copia sincronizzata)
È inoltre possibile copiare i file VHD hello utilizzando il cmdlet di PowerShell hello AzureStorageBlobCopy di inizio. Utilizzare hello comando seguente in Azure PowerShell toocopy disco rigido virtuale. Sostituire i valori hello in <> con valori corrispondenti dall'account di archiviazione di origine e di destinazione. toouse questo comando, è necessario disporre di un contenitore chiamato VHD nell'account di archiviazione di destinazione. Se il contenitore di hello non esiste, crearlo prima di eseguire il comando hello.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Esempio:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Scenario 2: "in corso la migrazione macchine virtuali da altri tooAzure piattaforme archiviazione Premium."
Se si esegue la migrazione di disco rigido virtuale da tooAzure di archiviazione Cloud non Azure, è prima necessario esportare directory locale tooa di hello disco rigido virtuale. Percorso di origine completo hello di disco rigido virtuale in cui è archiviato utile la directory locale hello e utilizzando quindi tooupload AzCopy è tooAzure archiviazione.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>Passaggio 1. Esportare la directory locale tooa di disco rigido virtuale
##### <a name="copy-a-vhd-from-aws"></a>Copia di un disco rigido virtuale da AWS
1. Se si utilizza AWS, esportare hello EC2 istanza tooa disco rigido virtuale in un bucket S3 Amazon. Seguire i passaggi di hello descritti nella documentazione di Amazon per lo strumento dell'interfaccia della riga di comando (CLI) di esportazione Amazon EC2 istanze tooinstall hello Amazon EC2 hello ed eseguire i file VHD hello comando create-istanza--attività di esportazione tooexport hello EC2 istanza tooa. Toouse assicurarsi di essere **VHD** per immagine disco hello &#95; &#95; Variabile formato quando si esegue hello **creare-istanza--attività di esportazione** comando. file disco rigido virtuale esportato Hello viene salvato nel bucket S3 Amazon hello che scelto durante il processo.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Scaricare i file VHD hello da bucket S3 hello. File VHD hello selezionare, quindi **azioni** > **scaricare**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Copia di un disco rigido virtuale da altri cloud non Azure
Se si esegue la migrazione di disco rigido virtuale da tooAzure di archiviazione Cloud non Azure, è prima necessario esportare directory locale tooa di hello disco rigido virtuale. Copiare hello percorso di origine completo della directory locale di hello in cui sono archiviati i file VHD.

##### <a name="copy-a-vhd-from-on-premises"></a>Copia di un disco rigido virtuale da locale
Se si esegue la migrazione di disco rigido virtuale da un ambiente locale, è necessario il percorso di origine completo hello in cui sono archiviati i file VHD. percorso di origine Hello potrebbe essere una condivisione di file o percorso del server.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Passaggio 2. Creare hello destinazione per il disco rigido virtuale
Creare un account di archiviazione per mantenere i dischi rigidi virtuali. Considerare i seguenti punti quando si pianifica dove hello toostore i dischi rigidi virtuali:

* account di archiviazione di destinazione Hello potrebbe essere archiviazione standard o premium in base alle esigenze dell'applicazione.
* area dell'account di archiviazione Hello deve corrispondere all'archiviazione Premium macchine virtuali di Azure in grado di supportare verrà creato in fase di hello finale. È possibile copiare il nuovo account di archiviazione tooa o hello toouse piano stesso account di archiviazione in base alle proprie esigenze.
* Copiare e salvare una chiave di account di archiviazione hello hello destinazione dell'account di archiviazione per la fase successiva hello.

È fortemente consigliabile spostare tutti i dati per l'archiviazione premium toouse del carico di lavoro di produzione.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>Passaggio 3. Caricare hello VHD tooAzure archiviazione
Dopo avere creato il disco rigido virtuale nella directory locale hello, è possibile utilizzare AzCopy o AzurePowerShell tooupload hello VHD file tooAzure archiviazione. Di seguito sono fornite entrambe le opzioni:

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Opzione 1: Utilizzo di file con estensione vhd di Azure PowerShell Add-AzureVhd tooupload hello

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Un esempio <Uri> potrebbe essere ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***. Un esempio <FileInfo> potrebbe essere ***"C:\path\to\upload.vhd"***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Opzione 2: Utilizzo di file con estensione vhd hello tooupload AzCopy
Utilizza AzCopy, è possibile caricare hello VHD su hello Internet. A seconda delle dimensioni di hello di hello dischi rigidi virtuali, l'operazione potrebbe richiedere tempo. Quando si utilizza questa opzione, ricordare limiti di ingresso/uscita account di archiviazione di toocheck hello. Vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md) per i dettagli.

1. Scaricare e installare AzCopy da qui: [versione più recente di AzCopy](http://aka.ms/downloadazcopy)
2. Aprire Azure PowerShell e passare toohello cartella in cui è installato AzCopy.
3. Comando che segue di hello utilizzare file di disco rigido virtuale toocopy hello "Origine" troppo "Destination".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Esempio:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Ecco le descrizioni dei parametri di hello utilizzati nel comando AzCopy hello:

   * **/ Origine:  *&lt;origine&gt;:***  percorso della cartella di hello o URL del contenitore dell'archiviazione che contiene hello disco rigido virtuale.
   * **/ SourceKey:  *&lt;chiave dell'account origine&gt;:***  chiave account di archiviazione dell'account di archiviazione di origine hello.
   * **/ Dest:  *&lt;destinazione&gt;:***  toocopy URL contenitore di archiviazione hello disco rigido virtuale.
   * **/ DestKey:  *&lt;chiave dell'account dest&gt;:***  chiave account di archiviazione dell'account di archiviazione di destinazione hello.
   * **/ BlobType: pagina:** specifica tale destinazione hello è un blob di pagine.
   * **/ Modello:  *&lt;nome file&gt;:***  specifica il nome di file di hello di hello toocopy di disco rigido virtuale.

Per informazioni dettagliate sull'uso di AzCopy strumento, vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Altre opzioni per il caricamento di un disco rigido virtuale
È inoltre possibile caricare un account di archiviazione tooyour disco rigido virtuale utilizzando uno dei hello seguente indica:

* [API Copy Blob di Archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Caricamento di BLOB in Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)
* [Materiale di riferimento dell'API REST del servizio di importazione/esportazione dell'archiviazione](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> È consigliabile usare il servizio di importazione/esportazione se il tempo di caricamento stimato è maggiore di 7 giorni. È possibile utilizzare [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) ora hello tooestimate dall'unità di dimensioni e il trasferimento di dati.
>
> Importazione/esportazione può essere utilizzato l'account di archiviazione standard tooa toocopy. Sarà necessario toocopy dall'account di archiviazione toopremium archiviazione standard usando uno strumento come AzCopy.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Creare macchine virtuali di Azure tramite Archiviazione Premium
Dopo aver hello VHD caricato o copiato toohello desiderato account di archiviazione, seguire le istruzioni hello questo hello tooregister sezione VHD come immagine del sistema operativo o il disco del sistema operativo a seconda dello scenario e quindi creare un'istanza di macchina virtuale da esso. disco dati Hello disco rigido virtuale può essere collegato toohello macchina virtuale dopo averla creata.
Un esempio di script di migrazione viene fornito alla fine di hello in questa sezione. Si tratta di uno script semplificato, che non corrisponde a tutti gli scenari. Potrebbe essere necessario tooupdate hello script toomatch con il proprio scenario specifico. toosee se questo script si applica tooyour scenario, vedere di seguito [Script di migrazione di un esempio](#a-sample-migration-script).

### <a name="checklist"></a>Elenco di controllo
1. Attendere fino a quando tutti i dischi rigidi Virtuali hello copia è stata completata.
2. Verificare che l'archiviazione Premium è disponibile nell'area di hello a che esegue la migrazione.
3. Decidere hello nuova serie di macchine Virtuali che verrà utilizzato. Deve essere uno spazio di archiviazione Premium in grado di supportare e hello dimensioni devono essere a seconda della disponibilità di hello in area hello e in base alle esigenze.
4. Decidere hello esatta dimensioni delle macchine Virtuali che si utilizzerà. Dimensioni della macchina virtuale devono numero di hello toobe toosupport sufficiente di dischi dati che si dispone. Ad esempio, Se si dispone di 4 dischi dati, hello macchina virtuale deve disporre di 2 o più core. Considerare anche la potenza di elaborazione, la memoria e la larghezza di banda di rete necessarie.
5. Creare un account di archiviazione Premium nell'area di destinazione hello. Si tratta di account hello che verrà utilizzato per hello nuova macchina virtuale.
6. Dispone di hello corrente VM informazioni utili, tra cui hello elenco di dischi e i BLOB VHD corrispondenti.

Preparare l'applicazione per il tempo di inattività. toodo una migrazione parziale, è necessario toostop tutta l'elaborazione di hello nel sistema corrente hello. Solo a questo punto è possibile ottenere lo stato di tooconsistent che è possibile eseguire la migrazione toohello nuova piattaforma. Durata inattività dipenderà hello quantità di dati in toomigrate dischi hello.

> [!NOTE]
> Se si sta creando una VM di Azure Resource Manager da un disco specializzato di disco rigido virtuale, fare riferimento troppo[questo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) per la distribuzione di VM Resource Manager utilizzando un disco esistente.
>
>

### <a name="register-your-vhd"></a>Registrazione del disco rigido virtuale
una macchina virtuale dal disco rigido virtuale del sistema operativo o un tooa disco dati tooattach toocreate nuova macchina virtuale, è necessario prima registrarli. Seguire la procedura riportata di seguito, a seconda dello scenario del disco rigido virtuale.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Generalizzato toocreate disco rigido virtuale del sistema operativo più istanze di macchina virtuale di Azure
Dopo aver generalizzato immagine del sistema operativo è di disco rigido virtuale caricato toohello account di archiviazione, registrarlo come un **immagine di macchina virtuale di Azure** in modo che è possibile creare uno o più istanze di macchina virtuale da esso. Utilizzare il disco rigido virtuale di hello tooregister i cmdlet di PowerShell seguente come un'immagine del sistema operativo VM di Azure. Specificare l'URL del contenitore completo hello in disco rigido virtuale è stato copiato.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Copiare e salvare il nome di hello di questa nuova immagine di macchina virtuale di Azure. Nell'esempio hello sopra, è *OSImageName*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Toocreate disco rigido virtuale del sistema operativo univoco una singola istanza di macchina virtuale di Azure
Dopo aver hello univoco disco rigido virtuale del sistema operativo è caricato toohello archiviazione conto, registrarlo come un **disco del sistema operativo Azure** in modo che è possibile creare un'istanza di macchina virtuale da esso. Utilizzare queste tooregister i cmdlet di PowerShell il disco rigido virtuale come disco del sistema operativo Azure. Specificare l'URL del contenitore completo hello in disco rigido virtuale è stato copiato.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Copiare e salvare il nome di hello del nuovo disco del sistema operativo Azure. Nell'esempio hello sopra, è *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Toobe di disco rigido virtuale del disco dati collegato toonew delle istanze di macchina virtuale di Azure
Una volta hello disco dati è di disco rigido virtuale caricato toostorage account, registrarlo come un disco dati di Azure in modo che possa essere allegato tooyour nuova serie DS, DSv2 serie o istanza di macchina virtuale di Azure serie GS.

Utilizzare queste tooregister i cmdlet di PowerShell il disco rigido virtuale come un disco dati di Azure. Specificare l'URL del contenitore completo hello in disco rigido virtuale è stato copiato.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Copiare e salvare il nome di hello di questo nuovo disco dati di Azure. Nell'esempio hello sopra, è *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Creare una macchina virtuale che supporti Archiviazione Premium
Una volta hello immagine del sistema operativo o disco del sistema operativo sono registrati, creare una nuova serie DS, DSv2-series o GS-series VM. Si utilizzerà immagine del sistema operativo hello o nome del disco del sistema operativo è stato registrato. Selezionare il tipo di macchina virtuale hello dal livello di archiviazione Premium hello. Nell'esempio seguente, usiamo hello *Standard_DS2* dimensioni della macchina virtuale.

> [!NOTE]
> Aggiornare hello disco dimensioni toomake verificarne che la corrispondenza, la capacità e requisiti di prestazioni e le dimensioni di hello disponibile su disco di Azure.
>
>

Cmdlet di PowerShell seguente hello dettagliate sotto toocreate hello nuova macchina virtuale. Innanzitutto, impostare i parametri comuni di hello:

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

Innanzitutto, creare un servizio cloud in cui verranno ospitate le nuove VM.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

Successivamente, a seconda dello scenario, creare hello macchina virtuale di Azure da hello immagine del sistema operativo o disco del sistema operativo che è stato registrato.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Generalizzato toocreate disco rigido virtuale del sistema operativo più istanze di macchina virtuale di Azure
Creare uno o più nuove macchine Virtuali di Azure serie DS istanze utilizzando hello di hello **immagine del sistema operativo Azure** registrato. Questo nome di immagine del sistema operativo specificato nella configurazione della macchina virtuale hello durante la creazione nuova macchina virtuale, come illustrato di seguito.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Toocreate disco rigido virtuale del sistema operativo univoco una singola istanza di macchina virtuale di Azure
Creare una nuova istanza VM Azure serie DS utilizzando hello **disco del sistema operativo Azure** registrato. Specificare il nome del disco del sistema operativo nella configurazione della macchina virtuale hello durante la creazione di hello nuova macchina virtuale, come illustrato di seguito.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Specificare altre informazioni di macchina virtuale di Azure, ad esempio, un servizio cloud, l’area, l’account di archiviazione, il set di disponibilità e i criteri di memorizzazione nella cache. Si noti che istanza hello della macchina virtuale deve essere condiviso con sistema operativo associato o dischi dati, pertanto l'account di servizio, area e di archiviazione cloud hello selezionato deve essere hello stesso percorso hello sottostante dischi rigidi virtuali di questi dischi.

### <a name="attach-data-disk"></a>Collegare il disco dati
Infine, se sono state registrate dati su disco di dischi rigidi virtuali, collegarli toohello nuova VM di Azure in grado di archiviazione Premium.

Utilizzare le seguenti PowerShell cmdlet tooattach dati disco toohello nuova macchina virtuale e specificare i criteri di memorizzazione nella cache di hello. Nell'esempio riportato di seguito hello criteri di memorizzazione nella cache è troppo*ReadOnly*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Potrebbero essere presenti ulteriori passaggi necessari toosupport l'applicazione che non rientrano in questa Guida.
>
>

### <a name="checking-and-plan-backup"></a>Controllo e pianificazione del backup
Una volta hello nuova macchina virtuale è in esecuzione, l'accesso tramite hello stesso id di accesso e password come hello macchina virtuale originale e verificare che tutto funzioni come previsto. Tutte le impostazioni di hello, inclusi i volumi con striping hello, può essere incluso in hello nuova macchina virtuale.

ultimo passaggio Hello è tooplan pianificazione di backup e manutenzione per la nuova macchina virtuale in base alle esigenze dell'applicazione hello hello.

### <a name="a-sample-migration-script"></a>Esempio di script di migrazione
Se si dispone di più macchine virtuali toomigrate, saranno utili automazione tramite gli script di PowerShell. Di seguito è uno script di esempio che consente di automatizzare la migrazione di hello di una macchina virtuale. Si noti che gli script seguente è solo un esempio e sono presenti alcuni presupposti presenti sui dischi di macchina virtuale correnti hello. Potrebbe essere necessario tooupdate hello script toomatch con il proprio scenario specifico.

presupposti Hello sono:

* Si stanno creando macchine virtuali di Azure classico.
* I dischi del sistema operativo e i dischi dati di origine si trovano nello stesso account di archiviazione e nello stesso contenitore. Se i dischi del sistema operativo e i dischi di dati non sono nello stesso hello inserito, è possibile usare AzCopy o Azure PowerShell toocopy dischi rigidi virtuali tramite gli account di archiviazione e i contenitori. Fare riferimento passaggio precedente toohello: [copia dei dischi rigidi Virtuali con PowerShell o di AzCopy](#copy-vhd-with-azcopy-or-powershell). Modifica questa toomeet script lo scenario è un'altra scelta, ma è consigliabile usare AzCopy o PowerShell in quanto è più facile e veloce.

script di automazione Hello di seguito. Sostituire il testo con le informazioni necessarie e aggiornare hello script toomatch con il proprio scenario specifico.

> [!NOTE]
> Utilizzando uno script esistente hello non mantiene la configurazione di rete hello dell'origine di macchina virtuale. È necessario toore-config le impostazioni di rete hello in macchine virtuali migrate.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>Ottimizzazione
Configurazione della macchina virtuale corrente può essere personalizzata in modo specifico toowork anche con dischi Standard. Ad esempio, tooincrease hello delle prestazioni con numero di dischi in un volume con striping. Anziché 4 dischi separatamente in archiviazione Premium, ad esempio, potrebbe essere il costo di hello toooptimize in grado di con un singolo disco. Le ottimizzazioni come questo toobe necessità gestito sul caso per caso e richiedono istruzioni personalizzate dopo la migrazione di hello. Inoltre, si noti che questo processo potrebbe non funzionare bene per i database e applicazioni che dipendono dal layout del disco hello definita nel programma di installazione hello.

##### <a name="preparation"></a>Operazioni preliminari
1. Hello completo migrazione semplice, come descritto in hello precedente sezione. Verranno eseguite le ottimizzazioni su hello nuova macchina virtuale dopo la migrazione di hello.
2. Definire dimensioni disco nuovo hello richiesto hello con ottimizzazione per la configurazione.
3. Determinare il mapping di hello dischi o volumi toohello nuovo disco specifiche correnti.

##### <a name="execution-steps"></a>Passaggi di esecuzione
1. Creare hello nuovi dischi con dimensioni corrette di hello in hello macchina virtuale di archiviazione Premium.
2. Account di accesso toohello macchina virtuale e copia hello i dati da hello corrente toohello nuovo disco del volume che esegue il mapping toothat volume. Questa operazione per tutti i volumi corrente hello necessarie toomap tooa nuovo disco.
3. Successivamente, modificare hello applicazione impostazioni tooswitch toohello nuovi dischi e volumi hello scollegare.

Per l'ottimizzazione di un'applicazione hello per migliorare le prestazioni del disco, fare riferimento troppo[ottimizzazione delle prestazioni dell'applicazione](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Migrazioni delle applicazioni
I database e altre applicazioni complesse potrebbero essere necessari passaggi speciali come definito dal provider dell'applicazione hello per la migrazione di hello. Consultare la documentazione dell'applicazione toorespective. Ad esempio, è possibile in genere eseguire la migrazione dei database con il backup e ripristino.

## <a name="next-steps"></a>Passaggi successivi
Vedere hello risorse per scenari specifici per la migrazione di macchine virtuale seguenti:

* [Eseguire la migrazione di macchine virtuali di Azure tra account di archiviazione](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Creare e caricare tooAzure un disco rigido virtuale di Windows Server.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Creazione e caricamento di un disco rigido virtuale contenente hello del sistema operativo Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migrazione di macchine virtuali da Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Vedere anche hello seguenti risorse toolearn ulteriori informazioni sull'archiviazione di Azure e macchine virtuali di Azure:

* [Archiviazione di Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Macchine virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
