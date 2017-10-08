---
title: aaaLinux macchine virtuali di calcolo in un cluster HPC Pack | Documenti Microsoft
description: Informazioni su come toocreate e utilizzare un pacchetto di HPC cluster in Azure per Linux ad alte prestazioni (HPC) carichi di lavoro
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure
Configurare un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) in Azure contenente un nodo head che esegue Windows Server e diversi nodi di calcolo che eseguono una distribuzione di Linux supportata. Esplorare i dati di opzioni toomove tra i nodi di Linux hello e nodo head di Windows hello del cluster di hello. Informazioni su come i processi di HPC Linux toosubmit toohello cluster.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

In generale, hello diagramma seguente mostra cluster HPC Pack hello è creare e utilizzare.

![Cluster HPC Pack con nodi Linux][scenario]

Per altre toorun opzioni HPC Linux carichi di lavoro in Azure, vedere [risorse tecniche per batch e high performance computing](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Distribuzione di un cluster HPC Pack con nodi di calcolo Linux
Questo articolo illustra due opzioni toodeploy di un cluster HPC Pack in Azure con nodi di calcolo di Linux. Entrambi i metodi di utilizzano un'immagine del Marketplace di Windows Server con nodo head di HPC Pack toocreate hello. 

* **Modello di Azure Resource Manager** -utilizzare un modello da hello Azure Marketplace o un modello di avvio rapido dalla community di hello, creazione di tooautomate di hello cluster nel modello di distribuzione di gestione risorse di hello. Ad esempio, hello [cluster HPC Pack per i carichi di lavoro di Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modello in hello Azure Marketplace consente di creare un'infrastruttura di cluster HPC Pack completa per HPC Linux carichi di lavoro.
* **Script di PowerShell** -hello utilizzare [script di distribuzione IaaS di Microsoft HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate una distribuzione completa del cluster nel modello di distribuzione classica hello. Questo script di PowerShell Azure utilizza un'immagine di macchina virtuale di HPC Pack in hello Azure Marketplace per la distribuzione rapida e fornisce un set completo di toodeploy parametri di configurazione di nodi di calcolo di Linux.

Per ulteriori informazioni sulle opzioni di distribuzione di cluster HPC Pack in Azure, vedere [opzioni toocreate e gestire un cluster ad alte prestazioni (HPC computing) in Azure con Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Prerequisiti
* **Sottoscrizione di Azure** -è possibile utilizzare una sottoscrizione in un servizio Azure globale o Azure China hello. Se non si ha un account, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi minuti.
* **Quota di core** -potrebbe essere necessario quota hello tooincrease di core, soprattutto se si sceglie toodeploy diversi nodi del cluster con dimensioni delle macchine Virtuali multicore. tooincrease una quota, aprire una richiesta di supporto clienti online senza alcun costo.
* **Distribuzioni Linux** -attualmente HPC Pack supporta hello seguendo le distribuzioni di Linux per nodi di calcolo. È possibile usare le versioni del Marketplace di queste distribuzioni, se disponibili, oppure fornire le proprie.
  
  * **Basate su CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 per HPC, SLES 12 per HPC (Premium)
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > toouse hello rete RDMA di Azure con una delle dimensioni delle macchine Virtuali hello con supporto per RDMA, specificare un'immagine di SUSE Linux Enterprise Server 12 HPC o basato su CentOS HPC da hello Azure Marketplace. Per altre informazioni, vedere [Dimensioni delle VM High Performance Computing (HPC)](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Cluster di hello ulteriori prerequisiti toodeploy tramite script di distribuzione IaaS di HPC Pack hello:

* **Computer client** -è necessario uno script di distribuzione basati su Windows client computer toorun hello cluster.
* **Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.
* **Script di distribuzione IaaS di HPC Pack** : scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). È possibile controllare la versione di hello dello script di hello eseguendo `.\New-HPCIaaSCluster.ps1 –Version`. In questo articolo si basa sulla versione 4.4.1 o successiva di script hello.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Opzione di distribuzione 1. Usare il modello di Resource Manager
1. Passare toohello [cluster HPC Pack per i carichi di lavoro di Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modello hello Azure Marketplace e fare clic su **Distribuisci**.
2. In hello portale di Azure, esaminare le informazioni di hello e quindi fare clic su **crea**.
   
    ![Creazione nel portale][portal]
3. In hello **nozioni di base** pannello, immettere un nome per il cluster hello, che anche i nomi di macchina virtuale del nodo head hello. È possibile scegliere un gruppo di risorse esistente o creare un gruppo per la distribuzione di hello in un percorso tooyou disponibili. Hello posizione influisce sulla disponibilità di hello di determinate dimensioni delle macchine Virtuali e altri servizi di Azure (vedere [i prodotti disponibili per area](https://azure.microsoft.com/regions/services/)).
4. In hello **impostazioni del nodo Head** pannello per una distribuzione iniziale, in genere è possibile accettare le impostazioni predefinite di hello. 
   
   > [!NOTE]
   > Hello **URL dello script di post-configurazione** è facoltativa impostazione toospecify uno script di Windows PowerShell disponibile pubblicamente che si desidera toorun nella macchina virtuale del nodo head hello dopo che è in esecuzione. 
   > 
   > 
5. In hello **impostazioni dei nodi di calcolo** pannello selezionare un modello di denominazione per i nodi di hello, numero hello e dimensioni dei nodi hello e hello toodeploy distribuzione Linux.
6. In hello **le impostazioni dell'infrastruttura** pannello, immettere un nome per la rete virtuale hello e Active Directory dominio, dominio e le credenziali di amministratore di macchina virtuale e un modello di denominazione per gli account di archiviazione hello.
   
   > [!NOTE]
   > HPC Pack Usa hello Active Directory dominio tooauthenticate cluster users. 
   > 
   > 
7. Dopo l'esecuzione dei test di convalida hello ed esaminare condizioni hello di utilizzo, fare clic su **acquisto**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Opzione di distribuzione 2. Utilizzare script di distribuzione IaaS di hello
Di seguito sono cluster hello di ulteriori prerequisiti toodeploy tramite script di distribuzione IaaS di HPC Pack hello:

* **Computer client** -è necessario uno script di distribuzione basati su Windows client computer toorun hello cluster.
* **Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.
* **Script di distribuzione IaaS di HPC Pack** : scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). È possibile controllare la versione di hello dello script di hello eseguendo `.\New-HPCIaaSCluster.ps1 –Version`. In questo articolo si basa sulla versione 4.4.1 o successiva di script hello.

**File di configurazione XML**

Hello script di distribuzione IaaS di HPC Pack utilizza un file di configurazione XML come un cluster HPC hello toodescribe input. Hello file di configurazione di esempio seguente specifica un piccolo cluster costituito da un nodo head di HPC Pack e due nodi di calcolo di dimensione A7 CentOS 7.0 Linux. 

Modificare il file hello in base alle esigenze per l'ambiente e la configurazione del cluster desiderato e salvarlo con un nome, ad esempio HPCDemoConfig.xml. Ad esempio, è necessario toosupply il nome della sottoscrizione e un nome di account di archiviazione univoci e il nome del servizio cloud. Inoltre, potrebbe essere toochoose un altro immagine Linux è supportata per i nodi di calcolo hello. Per ulteriori informazioni sugli elementi hello nel file di configurazione di hello, vedere il file Manual.rtf hello nella cartella script hello e [creare un cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**hello toorun script di distribuzione IaaS di HPC Pack**

1. Aprire Windows PowerShell nel computer client hello come amministratore.
2. Modifica cartella toohello directory in cui si script hello installato (E:\IaaSClusterScript in questo esempio).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Eseguire hello cluster HPC Pack hello toodeploy di comando seguente. In questo esempio si presuppone che si trova il file di configurazione hello in E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Poiché hello **AdminPassword** non è specificato in hello precedente comando, è richiesta tooenter password hello utente *MyAdminName*.
   
    b. script Hello avvia quindi i file di configurazione toovalidate hello. È possibile richiedere tooseveral minuti a seconda della connessione di rete hello.
   
    ![Convalida][validate]
   
    c. Dopo che hanno superato le convalide, script hello Elenca toocreate di risorse cluster hello. Immettere *Y* toocontinue.
   
    ![Risorse][resources]
   
    d. script Hello toodeploy hello HPC Pack cluster sarà avviato e completato configurazione hello senza ulteriori passaggi manuali. script Hello è possibile eseguire per alcuni minuti.
   
    ![Distribuire][deploy]
   
   > [!NOTE]
   > In questo esempio hello script genera un file di log automaticamente dall'hello **- file di registro** parametro non è specificato. Hello registri non vengono scritti in tempo reale, ma vengono raccolti alla fine di hello di convalida hello e hello della distribuzione. Se il processo di PowerShell hello viene arrestato durante l'esecuzione di script hello, alcuni log andranno persi.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Nodo head toohello connettersi
Dopo aver distribuito il cluster HPC Pack hello in Azure, [connessione Desktop remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo head VM utilizzando le credenziali di dominio fornito al momento della distribuzione cluster hello di hello (ad esempio, *hpc\\ clusteradmin*). Gestire i cluster di hello dal nodo head hello.

Nel nodo head hello, avviare HPC Cluster Manager toocheck lo stato di hello del cluster HPC Pack hello. È possibile gestire e monitorare i nodi di calcolo Linux hello allo stesso modo di utilizzare le finestre nodi di calcolo. Ad esempio, vengono mostrati i nodi di Linux hello elencati in **la gestione delle risorse** (questi nodi vengono distribuiti con hello **LinuxNode** modello).

![Gestione dei nodi][management]

È inoltre visualizzare i nodi di Linux hello hello **mappa termica** visualizzazione.

![Mappa termica][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Come toomove dati in un cluster con nodi di Linux
Si dispone di più dati di toomove scelte tra nodi di Linux e nodo head di Windows hello del cluster di hello. Di seguito sono tre metodi comuni, descritti in dettaglio nelle sezioni che seguono hello:

* **File di Azure** -espone dati di toostore condivisione di file SMB gestiti i file nell'archiviazione di Azure. Nodi di Windows e Linux possono montare una condivisione di File di Azure come un'unità o cartella hello stesso tempo, anche se vengano distribuite in reti virtuali diverse.
* **Nodo head SMB condividere** -Monta una cartella condivisa Windows standard del nodo head hello in nodi di Linux.
* **Server NFS del nodo head**: offre una soluzione di condivisione file per un ambiente misto Windows e Linux.

### <a name="azure-file-storage"></a>Archiviazione file di Azure
Hello [File di Azure](https://azure.microsoft.com/services/storage/files/) servizio espone condivisioni file usando il protocollo SMB 2.1 standard hello. Servizi cloud e macchine virtuali di Azure possono condividere i dati di file tra componenti delle applicazioni tramite condivisioni montate e applicazioni locali possono accedere dati in una condivisione di file tramite API di archiviazione di File hello. 

Per i passaggi dettagliati toocreate condividere e montarlo nel nodo head hello di un File di Azure, vedere [Introduzione all'archiviazione di File di Azure in Windows](../../../storage/files/storage-how-to-use-files-windows.md). condivisione di File di Azure toomount hello in nodi di Linux hello, vedere [come archiviazione di File di Azure con Linux toouse](../../../storage/files/storage-how-to-use-files-linux.md). tooset le connessioni persistenti, vedere [tooMicrosoft connessioni Persisting Azure file](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

Nell'esempio seguente di hello, creare una condivisione di File di Azure in un account di archiviazione. hello toomount condivisione nel nodo head hello, aprire un prompt dei comandi e immettere hello seguenti comandi:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

In questo esempio, allvhdsje è il nome di account di archiviazione, storageaccountkey è la chiave di account di archiviazione e rdma è hello nome della condivisione File di Azure. condivisione di File di Azure Hello viene montata come z nel nodo head hello.

condivisione di File di Azure toomount hello in nodi di Linux, eseguire una **clusrun** comando nel nodo head hello. **[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  è un utile toocarry strumento di HPC Pack operazioni amministrative su più nodi. Vedere anche [Clusrun per nodi Linux](#Clusrun-for-Linux-nodes) in questo articolo.

Aprire una finestra di Windows PowerShell e immettere hello seguenti comandi:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

Hello primo comando crea una cartella denominata /rdma in tutti i nodi nel gruppo LinuxNodes hello. comando secondo Hello Monta hello Azure File condivisione allvhdsjw.file.core.windows.net/rdma nella cartella /rdma hello con dir e file too777 di set di bit di modalità. Nel secondo comando hello, allvhdsje è il nome di account di archiviazione e storageaccountkey è la chiave di account di archiviazione.

> [!NOTE]
> Hello "\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell. "\`,"significa che hello"," (carattere virgola) è una parte del comando hello.
> 
> 

### <a name="head-node-share"></a>Condivisione del nodo head
In alternativa, è possibile montare una cartella condivisa del nodo head hello in nodi di Linux. Una condivisione vengono forniti i file tooshare modo più semplici hello ma nodo head hello e tutti i nodi di Linux devono essere distribuiti in hello stessa rete virtuale. Ecco i passaggi di hello.

1. Creare una cartella nel nodo head hello e condividerlo tooEveryone con autorizzazioni di lettura/scrittura. Ad esempio condividere D:\OpenFOAM nel nodo head di hello come \\CentOS7RDMA HN\OpenFOAM. Ecco hello nome host del nodo head hello CentOS7RDMA HN.
   
    ![Autorizzazioni di condivisione file][fileshareperms]
   
    ![Condivisione di file][filesharing]
2. Aprire una finestra di Windows PowerShell ed eseguire hello seguenti comandi:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Hello primo comando crea una cartella denominata /openfoam in tutti i nodi nel gruppo LinuxNodes hello. comando secondo Hello Monta //CentOS7RDMA-HN/OpenFOAM cartella hello condivise nella cartella hello con dir e file too777 di set di bit di modalità. Hello nome utente e password nel comando hello devono essere hello username e password di un utente del cluster nel nodo head hello. Vedere [Aggiungere o rimuovere utenti del cluster](https://technet.microsoft.com/library/ff919330.aspx).

> [!NOTE]
> Hello "\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell. "\`,"significa che hello"," (carattere virgola) è una parte del comando hello.
> 
> 

### <a name="nfs-server"></a>Server NFS
Hello servizio NFS consente tooshare ed eseguire la migrazione di file tra computer con sistema operativo Windows Server 2012 hello mediante protocollo SMB hello e i computer basati su Linux mediante protocollo NFS hello. Hello del server NFS e tutti gli altri nodi hanno distribuito in hello toobe stessa rete virtuale. Consente di migliorare la compatibilità con i nodi Linux rispetto a una condivisione SMB. Ad esempio, supporta il collegamento di file.

1. tooinstall e configurare un server NFS, seguire i passaggi hello [Server per il File System prima rete End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Ad esempio, creare una condivisione NFS denominata nfs con hello le proprietà seguenti:
   
    ![Autorizzazione NFS][nfsauth]
   
    ![Autorizzazioni di condivisione NFS][nfsshare]
   
    ![Autorizzazioni NFS NTFS][nfsperm]
   
    ![Proprietà di gestione di NFS][nfsmanage]
2. Aprire una finestra di Windows PowerShell ed eseguire hello seguenti comandi:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   Hello primo comando crea una cartella denominata /nfsshared in tutti i nodi nel gruppo LinuxNodes hello. secondo comando mount hello NFS Hello condividere CentOS7RDMA HN: / hello di nfs nella cartella. Qui CentOS7RDMA HN: nfs è percorso remoto di hello della condivisione NFS.

## <a name="how-toosubmit-jobs"></a>Come i processi toosubmit
Esistono diversi cluster con HPC Pack toohello modi toosubmit processi:

* Gestione cluster HPC o interfaccia grafica della Gestione cluster HPC
* Portale Web HPC
* API REST

Invio di processi toohello cluster in Azure tramite strumenti di HPC Pack GUI e portale web di HPC hello sono hello uguale a quello di nodi di calcolo di Windows. Vedere [il gestore di processi di HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [come toosubmit processi da un computer client locale](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

processi toosubmit tramite hello API REST, vedere troppo[creazione e invio di processi tramite hello API REST di Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). processi toosubmit da un client Linux, fare riferimento anche esempio Python toohello in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun per nodi Linux
Hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) strumento può essere utilizzato tooexecute comandi nei nodi Linux tramite un prompt dei comandi o HPC Cluster Manager. Di seguito sono riportati alcuni esempi di base.

* Mostra i nomi utente correnti in tutti i nodi del cluster di hello.
  
    ```command
    clusrun whoami
    ```
* Installare hello **gdb** dello strumento debugger con **yum** in tutti i nodi hello linuxnodes gruppo e quindi riavviare i nodi di hello dopo 10 minuti.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Creare uno script della shell visualizzazione ogni numero da 1 a 10 per un secondo in ogni nodo di Linux in cluster hello, eseguirlo e visualizzare immediatamente l'output dai nodi hello.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Potrebbe essere necessario toouse alcuni caratteri di escape nei **clusrun** comandi. Come illustrato in questo esempio, utilizzare ^ in hello di tooescape un prompt dei comandi ">" simbolo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Provare la scalabilità verticale hello cluster tooa maggior numero di nodi oppure provare a eseguire un carico di lavoro di Linux nel cluster hello. Per un esempio, vedere [Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-namd.md).
* Provare a un cluster con [macchine virtuali che supportano RDMA, con uso intensivo](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun carichi di lavoro MPI. Per un esempio, vedere [Eseguire OpenFOAM con Microsoft HPC Pack in un cluster Linux RDMA in Azure](hpcpack-cluster-openfoam.md).
* Se si desidera utilizzare con i nodi di Linux in un cluster HPC Pack locale, vedere hello [Guida TechNet](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
