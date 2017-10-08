---
title: STELLA aaaRun-CCM + con HPC Pack nelle macchine virtuali Linux | Documenti Microsoft
description: "Distribuire un cluster Microsoft HPC Pack in Azure ed eseguire un processo STAR-CCM+ in più nodi di calcolo Linux su una rete RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Eseguire STAR-CCM+ con Microsoft HPC Pack in un cluster Linux RDMA in Azure
Questo articolo illustra come toodeploy Microsoft HPC Pack del cluster in Azure ed eseguire un [STELLA CD adapco-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) processo su più nodi di calcolo di Linux che sono collegate tra loro tramite InfiniBand.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Microsoft HPC Pack fornisce funzionalità toorun un'ampia gamma di HPC su larga scala e applicazioni parallele, incluse le applicazioni MPI, nei cluster di macchine virtuali di Microsoft Azure. HPC Pack supporta anche applicazioni HPC che eseguono Linux su VM di nodi di calcolo Linux distribuite in un cluster HPC Pack. Per un toousing introduzione Linux nodi con HPC Pack, vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md).

## <a name="set-up-an-hpc-pack-cluster"></a>Configurare un cluster HPC Pack
Scaricare gli script di distribuzione IaaS di HPC Pack hello da hello [area Download](https://www.microsoft.com/en-us/download/details.aspx?id=44949) ed estrarli in locale.

Azure PowerShell è un prerequisito. Se PowerShell non è configurato nel computer locale, consultare l'articolo articolo hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

In fase di hello di questo articolo, le immagini Linux hello da hello Azure Marketplace, che contiene i driver InfiniBand hello per Azure, sono per SLES 12, CentOS 6.5 e CentOS 7.1. Questo articolo si basa sull'utilizzo di hello SLES 12. nome di hello tooretrieve di tutte le immagini Linux che supportano HPC in hello Marketplace, è possibile eseguire hello comando PowerShell seguente:

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

output di Hello è indicato hello percorso in cui queste immagini sono disponibili e hello Nome immagine (**ImageName**) toobe utilizzato nel modello di distribuzione hello in seguito.

Prima distribuire i cluster di hello, è necessario toobuild un file di modello di distribuzione di HPC Pack. Poiché la destinazione è un piccolo cluster, nodo head hello verrà controller di dominio hello e ospitare un database SQL locale.

Hello modello seguente verrà distribuire un nodo head, creare un file XML denominato **MyCluster.xml**e sostituire i valori hello di **SubscriptionId**, **StorageAccount**,  **Percorso**, **VMName**, e **ServiceName** con quelle dell'utente.

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

Avviare la creazione del nodo head hello eseguendo hello comando di PowerShell in un prompt dei comandi con privilegi elevati:

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

Dopo 20 minuti too30, nodo head hello deve essere pronta. È possibile connettersi tooit dal portale di Azure hello facendo hello **Connetti** sull'icona della macchina virtuale hello.

Server di inoltro DNS hello toofix potrebbe essere alla fine. toodo in tal caso, avviare Gestore DNS.

1. Nome del server hello pulsante destro del mouse in Gestore DNS, selezionare **proprietà**, quindi fare clic su hello **server d'inoltro** scheda.
2. Fare clic su hello **modifica** pulsante tooremove qualsiasi server d'inoltro e quindi fare clic su **OK**.
3. Verificare che tale hello **utilizzare i parametri radice se non sono disponibili alcun server d'inoltro** casella di controllo è selezionata e quindi fare clic su **OK**.

## <a name="set-up-linux-compute-nodes"></a>Configurare nodi di calcolo Linux
Distribuire nodi di calcolo di hello Linux utilizzando hello utilizzato nodo head di hello toocreate stesso modello di distribuzione.

Copia file hello **MyCluster.xml** dal nodo head toohello di computer locale e aggiornamento hello **NodeCount** tag con il numero di hello di nodi che si desidera toodeploy (< = 20). Essere toohave attenzione core a sufficienza disponibili della quota di Azure, perché ogni istanza A9 utilizzerà 16 core nella sottoscrizione. È possibile utilizzare istanze A8 (8 core) anziché A9 se si desidera toouse più macchine virtuali in hello stesso budget.

Nel nodo head hello, copiare gli script di distribuzione IaaS di HPC Pack hello.

Eseguire i seguenti comandi di PowerShell di Azure in un prompt dei comandi con privilegi elevati hello:

1. Eseguire **Add-AzureAccount** tooconnect tooyour sottoscrizione di Azure.
2. Se si dispone di più sottoscrizioni, eseguire **Get-AzureSubscription** toolist li.
3. Impostare una sottoscrizione predefinita eseguendo hello **Select-AzureSubscription - SubscriptionName xxxx-predefinito** comando.
4. Eseguire **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart distribuzione dei nodi di calcolo di Linux.
   
   ![Distribuzione del nodo head][hndeploy]

Aprire lo strumento di gestione di Cluster HPC Pack hello. Dopo alcuni minuti, i nodi di calcolo Linux verranno visualizzati normalmente in un elenco di nodi di calcolo del cluster. Con la modalità di distribuzione classica hello, vengono create in modo sequenziale le macchine virtuali IaaS. Pertanto, se il numero di hello di nodi è importante, recupero tutti distribuito può richiedere una quantità significativa di tempo.

![Nodi Linux in HPC Pack Cluster Manager][clustermanager]

Ora che tutti i nodi siano in esecuzione nel cluster hello, esistono toomake le impostazioni di un'infrastruttura aggiuntiva.

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a>Configurare una condivisione file di Azure per nodi Windows e Linux
È possibile utilizzare script toostore del servizio File di Azure hello, pacchetti di applicazioni e i file di dati. File di Azure offre funzionalità CIFS su un'archivio BLOB di Azure come archivio permanente. Tenere presente che questo non è la soluzione più scalabile hello, ma è hello quello più semplice e non richiede le macchine virtuali dedicate.

Creare una condivisione di File di Azure seguendo le istruzioni di hello nell'articolo hello [Introduzione all'archiviazione di File di Azure in Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).

Mantenere hello nome dell'account di archiviazione come **saname**, nome della condivisione file hello come **sharename**e una chiave di account di archiviazione hello come **sakey**.

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a>Condivisione di File di Azure hello montaggio nel nodo head hello
Aprire un prompt dei comandi con privilegi elevati ed eseguire hello seguendo le credenziali di hello toostore comando nell'insieme di credenziali di hello computer locale:

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

Quindi, toomount hello Azure condivisione File, eseguire:

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a>Montare in una condivisione hello Azure sui nodi di calcolo di Linux
Uno strumento utile che viene fornito con HPC Pack è lo strumento clusrun hello. È possibile utilizzare questo hello toorun strumento da riga di comando stesso comando contemporaneamente su un set di nodi di calcolo. In questo caso, è utilizzata una condivisione di File di Azure toomount hello e renderlo persistente toosurvive riavvii.
In un prompt con privilegi elevato nel nodo head hello, eseguire hello i comandi seguenti.

directory di montaggio toocreate hello:

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

hello toomount condivisione File di Azure:

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

condivisione di montaggio toopersist hello:

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a>Installare STAR-CCM+
Le istanze A8 e A9 delle VM di Azure forniscono il supporto per InfiniBand e le funzionalità RDMA. Hello kernel che consentono di tali funzionalità sono disponibili driver per Windows Server 2012 R2, SUSE 12, CentOS 6.5 e immagini CentOS 7.1 hello Azure Marketplace. Microsoft MPI e Intel MPI (versione 5. x) sono hello due MPI librerie che supportano i driver in Azure.

CD-adapco STAR-CCM+ 11.x e versioni successive è incluso in Intel MPI versione 5.x, quindi è incluso il supporto di InfiniBand per Azure.

Ottenere hello Linux64 STELLA-CCM + pacchetto da hello [portale CD adapco](https://steve.cd-adapco.com). In questo caso, è stata usata la versione 11.02.010 con precisione mista.

Nel nodo head hello in hello **/hpcdata** File di Azure condividono, creare uno script della shell denominato **setupstarccm.sh** con hello dopo contenuto. Questo script deve essere eseguito su ogni tooset del nodo di calcolo di STELLA-CCM + localmente.

#### <a name="sample-setupstarcmsh-script"></a>Script setupstarcm.sh di esempio
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
A questo punto, tooset backup STELLA-CCM + in tutti i Linux nodi di calcolo, aprire un prompt dei comandi con privilegi elevati ed eseguire hello comando seguente:

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

Durante l'eseguono di comandi hello, è possibile monitorare l'utilizzo della CPU hello utilizzando la mappa di calore hello di gestione Cluster. La configurazione di tutti i nodi dovrebbe richiedere qualche minuto.

## <a name="run-star-ccm-jobs"></a>Eseguire processi STAR-CCM+
HPC Pack viene utilizzato per le funzionalità di utilità di pianificazione di processo in ordine toorun STELLA-CCM + processi. toodo in tal caso, si base hello supporto di alcuni script processo hello toostart utilizzato ed eseguiti a STELLA-CCM +. dati di input Hello viene mantenuti nella condivisione di File di Azure hello primo per motivi di semplicità.

Hello lo script di PowerShell seguente viene utilizzato tooqueue una STELLA-CCM + processo. Accetta tre argomenti:

* nome del modello Hello
* numero di Hello di nodi toobe utilizzato
* numero di Hello di core in ogni nodo di toobe utilizzato

Poiché a STELLA-CCM + può riempire la larghezza di banda di hello memoria, è in genere è preferibile toouse meno core per nodi di calcolo e aggiungere nuovi nodi. numero esatto di Hello di core per nodo dipenderà dalla famiglia di processori hello e la velocità di interconnessione hello.

i nodi di Hello vengono allocati esclusivamente per il processo di hello e non possono essere condivisa con altri processi. il processo di Hello non viene avviato direttamente come un processo MPI. Hello **runstarccm.sh** script della shell verranno avvio hello MPI.

Hello input modello e hello **runstarccm.sh** script vengono archiviati in hello **/hpcdata** condivisione che era stati montati in precedenza.

File di log denominati con ID processo hello e vengono archiviati in hello **/hpcdata condivisione**, insieme a STELLA hello-CCM + file di output.

#### <a name="sample-submitstarccmjobps1-script"></a>Script SubmitStarccmJob.ps1 di esempio
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
Sostituire **runner.java** con il servizio di avvio preferito per il modello Java STAR-CCM+ e con il codice di registrazione.

#### <a name="sample-runstarccmsh-script"></a>Script runstarccm.sh di esempio
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

Nel test viene usato un token di licenza di tipo Power-One-Demand. Per tale token, è necessario hello tooset **$CDLMD_LICENSE_FILE** variabile di ambiente troppo **1999@flex.cd-adapco.com**  e la chiave di hello in hello **- podkey** opzione della riga di comando hello .

Dopo alcune operazioni di inizializzazione, estrae script hello - da hello **CCP_NODES_CORES $** hello di variabili di ambiente HPC Pack set - elenco di nodi toobuild utilizza un file di host che hello avvio MPI. Questo file host conterrà un elenco di hello di nomi di nodo di calcolo che vengono utilizzati per il processo di hello, un nome per ogni riga.

formato Hello **CCP_NODES_CORES $** segue questo modello:

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

Dove:

* `<Number of nodes>`è il numero di hello di nodi allocata toothis processo.
* `<Name of node_n_...>`è il nome di hello di ogni nodo allocata toothis processo.
* `<Cores of node_n_...>`è il numero di hello di core nel nodo hello allocata toothis processo.

numero di core Hello (**$NBCORES**) è anche calcolata hello in base a numero di nodi (**$NBNODES**) e il numero di core per nodo hello (fornito come parametro **$NBCORESPERNODE**).

Per le opzioni MPI hello, hello quelli che vengono utilizzati con Intel MPI in Azure sono:

* `-mpi intel`toospecify Intel MPI.
* `-fabric UDAPL`toouse InfiniBand Azure verbi.
* `-cpubind bandwidth,v`larghezza di banda di toooptimize per MPI con STELLA-CCM +.
* `-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI utilizzare Azure InfiniBand e hello tooset obbligatorio per un numero di core per nodo.
* `-batch`STELLA toostart-CCM + in modalità batch senza interfaccia utente.

Infine, toostart un processo, assicurarsi che i nodi siano in esecuzione e che siano online in Gestione Cluster. Da un prompt dei comandi di PowerShell eseguire quindi questo comando:

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a>Arrestare i nodi
In un secondo momento al termine dei test, è possibile utilizzare hello toostop di HPC Pack PowerShell i comandi seguenti e avviare i nodi:

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a>Passaggi successivi
Provare a eseguire altri carichi di lavoro di Linux. Per esempi, vedere:

* [Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-namd.md)
* [Eseguire OpenFoam con Microsoft HPC Pack in un cluster Linux RDMA in Azure](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
