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
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="dc2b0-103">Eseguire STAR-CCM+ con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="dc2b0-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="dc2b0-104">Questo articolo illustra come toodeploy Microsoft HPC Pack del cluster in Azure ed eseguire un [STELLA CD adapco-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) processo su più nodi di calcolo di Linux che sono collegate tra loro tramite InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="dc2b0-105">Microsoft HPC Pack fornisce funzionalità toorun un'ampia gamma di HPC su larga scala e applicazioni parallele, incluse le applicazioni MPI, nei cluster di macchine virtuali di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="dc2b0-106">HPC Pack supporta anche applicazioni HPC che eseguono Linux su VM di nodi di calcolo Linux distribuite in un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="dc2b0-107">Per un toousing introduzione Linux nodi con HPC Pack, vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="dc2b0-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="dc2b0-108">Configurare un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="dc2b0-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="dc2b0-109">Scaricare gli script di distribuzione IaaS di HPC Pack hello da hello [area Download](https://www.microsoft.com/en-us/download/details.aspx?id=44949) ed estrarli in locale.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="dc2b0-110">Azure PowerShell è un prerequisito.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="dc2b0-111">Se PowerShell non è configurato nel computer locale, consultare l'articolo articolo hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dc2b0-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="dc2b0-112">In fase di hello di questo articolo, le immagini Linux hello da hello Azure Marketplace, che contiene i driver InfiniBand hello per Azure, sono per SLES 12, CentOS 6.5 e CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="dc2b0-113">Questo articolo si basa sull'utilizzo di hello SLES 12.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="dc2b0-114">nome di hello tooretrieve di tutte le immagini Linux che supportano HPC in hello Marketplace, è possibile eseguire hello comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="dc2b0-115">output di Hello è indicato hello percorso in cui queste immagini sono disponibili e hello Nome immagine (**ImageName**) toobe utilizzato nel modello di distribuzione hello in seguito.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="dc2b0-116">Prima distribuire i cluster di hello, è necessario toobuild un file di modello di distribuzione di HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="dc2b0-117">Poiché la destinazione è un piccolo cluster, nodo head hello verrà controller di dominio hello e ospitare un database SQL locale.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="dc2b0-118">Hello modello seguente verrà distribuire un nodo head, creare un file XML denominato **MyCluster.xml**e sostituire i valori hello di **SubscriptionId**, **StorageAccount**,  **Percorso**, **VMName**, e **ServiceName** con quelle dell'utente.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

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

<span data-ttu-id="dc2b0-119">Avviare la creazione del nodo head hello eseguendo hello comando di PowerShell in un prompt dei comandi con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="dc2b0-120">Dopo 20 minuti too30, nodo head hello deve essere pronta.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="dc2b0-121">È possibile connettersi tooit dal portale di Azure hello facendo hello **Connetti** sull'icona della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="dc2b0-122">Server di inoltro DNS hello toofix potrebbe essere alla fine.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="dc2b0-123">toodo in tal caso, avviare Gestore DNS.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="dc2b0-124">Nome del server hello pulsante destro del mouse in Gestore DNS, selezionare **proprietà**, quindi fare clic su hello **server d'inoltro** scheda.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="dc2b0-125">Fare clic su hello **modifica** pulsante tooremove qualsiasi server d'inoltro e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="dc2b0-126">Verificare che tale hello **utilizzare i parametri radice se non sono disponibili alcun server d'inoltro** casella di controllo è selezionata e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="dc2b0-127">Configurare nodi di calcolo Linux</span><span class="sxs-lookup"><span data-stu-id="dc2b0-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="dc2b0-128">Distribuire nodi di calcolo di hello Linux utilizzando hello utilizzato nodo head di hello toocreate stesso modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="dc2b0-129">Copia file hello **MyCluster.xml** dal nodo head toohello di computer locale e aggiornamento hello **NodeCount** tag con il numero di hello di nodi che si desidera toodeploy (< = 20).</span><span class="sxs-lookup"><span data-stu-id="dc2b0-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="dc2b0-130">Essere toohave attenzione core a sufficienza disponibili della quota di Azure, perché ogni istanza A9 utilizzerà 16 core nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="dc2b0-131">È possibile utilizzare istanze A8 (8 core) anziché A9 se si desidera toouse più macchine virtuali in hello stesso budget.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="dc2b0-132">Nel nodo head hello, copiare gli script di distribuzione IaaS di HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="dc2b0-133">Eseguire i seguenti comandi di PowerShell di Azure in un prompt dei comandi con privilegi elevati hello:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="dc2b0-134">Eseguire **Add-AzureAccount** tooconnect tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="dc2b0-135">Se si dispone di più sottoscrizioni, eseguire **Get-AzureSubscription** toolist li.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="dc2b0-136">Impostare una sottoscrizione predefinita eseguendo hello **Select-AzureSubscription - SubscriptionName xxxx-predefinito** comando.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="dc2b0-137">Eseguire **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart distribuzione dei nodi di calcolo di Linux.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Distribuzione del nodo head][hndeploy]

<span data-ttu-id="dc2b0-139">Aprire lo strumento di gestione di Cluster HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="dc2b0-140">Dopo alcuni minuti, i nodi di calcolo Linux verranno visualizzati normalmente in un elenco di nodi di calcolo del cluster.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="dc2b0-141">Con la modalità di distribuzione classica hello, vengono create in modo sequenziale le macchine virtuali IaaS.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="dc2b0-142">Pertanto, se il numero di hello di nodi è importante, recupero tutti distribuito può richiedere una quantità significativa di tempo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nodi Linux in HPC Pack Cluster Manager][clustermanager]

<span data-ttu-id="dc2b0-144">Ora che tutti i nodi siano in esecuzione nel cluster hello, esistono toomake le impostazioni di un'infrastruttura aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="dc2b0-145">Configurare una condivisione file di Azure per nodi Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="dc2b0-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="dc2b0-146">È possibile utilizzare script toostore del servizio File di Azure hello, pacchetti di applicazioni e i file di dati.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="dc2b0-147">File di Azure offre funzionalità CIFS su un'archivio BLOB di Azure come archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="dc2b0-148">Tenere presente che questo non è la soluzione più scalabile hello, ma è hello quello più semplice e non richiede le macchine virtuali dedicate.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="dc2b0-149">Creare una condivisione di File di Azure seguendo le istruzioni di hello nell'articolo hello [Introduzione all'archiviazione di File di Azure in Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="dc2b0-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="dc2b0-150">Mantenere hello nome dell'account di archiviazione come **saname**, nome della condivisione file hello come **sharename**e una chiave di account di archiviazione hello come **sakey**.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="dc2b0-151">Condivisione di File di Azure hello montaggio nel nodo head hello</span><span class="sxs-lookup"><span data-stu-id="dc2b0-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="dc2b0-152">Aprire un prompt dei comandi con privilegi elevati ed eseguire hello seguendo le credenziali di hello toostore comando nell'insieme di credenziali di hello computer locale:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="dc2b0-153">Quindi, toomount hello Azure condivisione File, eseguire:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="dc2b0-154">Montare in una condivisione hello Azure sui nodi di calcolo di Linux</span><span class="sxs-lookup"><span data-stu-id="dc2b0-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="dc2b0-155">Uno strumento utile che viene fornito con HPC Pack è lo strumento clusrun hello.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="dc2b0-156">È possibile utilizzare questo hello toorun strumento da riga di comando stesso comando contemporaneamente su un set di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="dc2b0-157">In questo caso, è utilizzata una condivisione di File di Azure toomount hello e renderlo persistente toosurvive riavvii.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="dc2b0-158">In un prompt con privilegi elevato nel nodo head hello, eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="dc2b0-159">directory di montaggio toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="dc2b0-160">hello toomount condivisione File di Azure:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="dc2b0-161">condivisione di montaggio toopersist hello:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="dc2b0-162">Installare STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="dc2b0-162">Install STAR-CCM+</span></span>
<span data-ttu-id="dc2b0-163">Le istanze A8 e A9 delle VM di Azure forniscono il supporto per InfiniBand e le funzionalità RDMA.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="dc2b0-164">Hello kernel che consentono di tali funzionalità sono disponibili driver per Windows Server 2012 R2, SUSE 12, CentOS 6.5 e immagini CentOS 7.1 hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="dc2b0-165">Microsoft MPI e Intel MPI (versione 5. x) sono hello due MPI librerie che supportano i driver in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="dc2b0-166">CD-adapco STAR-CCM+ 11.x e versioni successive è incluso in Intel MPI versione 5.x, quindi è incluso il supporto di InfiniBand per Azure.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="dc2b0-167">Ottenere hello Linux64 STELLA-CCM + pacchetto da hello [portale CD adapco](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="dc2b0-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="dc2b0-168">In questo caso, è stata usata la versione 11.02.010 con precisione mista.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="dc2b0-169">Nel nodo head hello in hello **/hpcdata** File di Azure condividono, creare uno script della shell denominato **setupstarccm.sh** con hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="dc2b0-170">Questo script deve essere eseguito su ogni tooset del nodo di calcolo di STELLA-CCM + localmente.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="dc2b0-171">Script setupstarcm.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="dc2b0-171">Sample setupstarcm.sh script</span></span>
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
<span data-ttu-id="dc2b0-172">A questo punto, tooset backup STELLA-CCM + in tutti i Linux nodi di calcolo, aprire un prompt dei comandi con privilegi elevati ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="dc2b0-173">Durante l'eseguono di comandi hello, è possibile monitorare l'utilizzo della CPU hello utilizzando la mappa di calore hello di gestione Cluster.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="dc2b0-174">La configurazione di tutti i nodi dovrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="dc2b0-175">Eseguire processi STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="dc2b0-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="dc2b0-176">HPC Pack viene utilizzato per le funzionalità di utilità di pianificazione di processo in ordine toorun STELLA-CCM + processi.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="dc2b0-177">toodo in tal caso, si base hello supporto di alcuni script processo hello toostart utilizzato ed eseguiti a STELLA-CCM +.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="dc2b0-178">dati di input Hello viene mantenuti nella condivisione di File di Azure hello primo per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="dc2b0-179">Hello lo script di PowerShell seguente viene utilizzato tooqueue una STELLA-CCM + processo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="dc2b0-180">Accetta tre argomenti:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-180">It takes three arguments:</span></span>

* <span data-ttu-id="dc2b0-181">nome del modello Hello</span><span class="sxs-lookup"><span data-stu-id="dc2b0-181">hello model name</span></span>
* <span data-ttu-id="dc2b0-182">numero di Hello di nodi toobe utilizzato</span><span class="sxs-lookup"><span data-stu-id="dc2b0-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="dc2b0-183">numero di Hello di core in ogni nodo di toobe utilizzato</span><span class="sxs-lookup"><span data-stu-id="dc2b0-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="dc2b0-184">Poiché a STELLA-CCM + può riempire la larghezza di banda di hello memoria, è in genere è preferibile toouse meno core per nodi di calcolo e aggiungere nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="dc2b0-185">numero esatto di Hello di core per nodo dipenderà dalla famiglia di processori hello e la velocità di interconnessione hello.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="dc2b0-186">i nodi di Hello vengono allocati esclusivamente per il processo di hello e non possono essere condivisa con altri processi.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="dc2b0-187">il processo di Hello non viene avviato direttamente come un processo MPI.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="dc2b0-188">Hello **runstarccm.sh** script della shell verranno avvio hello MPI.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="dc2b0-189">Hello input modello e hello **runstarccm.sh** script vengono archiviati in hello **/hpcdata** condivisione che era stati montati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="dc2b0-190">File di log denominati con ID processo hello e vengono archiviati in hello **/hpcdata condivisione**, insieme a STELLA hello-CCM + file di output.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="dc2b0-191">Script SubmitStarccmJob.ps1 di esempio</span><span class="sxs-lookup"><span data-stu-id="dc2b0-191">Sample SubmitStarccmJob.ps1 script</span></span>
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
<span data-ttu-id="dc2b0-192">Sostituire **runner.java** con il servizio di avvio preferito per il modello Java STAR-CCM+ e con il codice di registrazione.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="dc2b0-193">Script runstarccm.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="dc2b0-193">Sample runstarccm.sh script</span></span>
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

<span data-ttu-id="dc2b0-194">Nel test viene usato un token di licenza di tipo Power-One-Demand.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="dc2b0-195">Per tale token, è necessario hello tooset **$CDLMD_LICENSE_FILE** variabile di ambiente troppo **1999@flex.cd-adapco.com**  e la chiave di hello in hello **- podkey** opzione della riga di comando hello .</span><span class="sxs-lookup"><span data-stu-id="dc2b0-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="dc2b0-196">Dopo alcune operazioni di inizializzazione, estrae script hello - da hello **CCP_NODES_CORES $** hello di variabili di ambiente HPC Pack set - elenco di nodi toobuild utilizza un file di host che hello avvio MPI.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="dc2b0-197">Questo file host conterrà un elenco di hello di nomi di nodo di calcolo che vengono utilizzati per il processo di hello, un nome per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="dc2b0-198">formato Hello **CCP_NODES_CORES $** segue questo modello:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="dc2b0-199">Dove:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-199">Where:</span></span>

* <span data-ttu-id="dc2b0-200">`<Number of nodes>`è il numero di hello di nodi allocata toothis processo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="dc2b0-201">`<Name of node_n_...>`è il nome di hello di ogni nodo allocata toothis processo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="dc2b0-202">`<Cores of node_n_...>`è il numero di hello di core nel nodo hello allocata toothis processo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="dc2b0-203">numero di core Hello (**$NBCORES**) è anche calcolata hello in base a numero di nodi (**$NBNODES**) e il numero di core per nodo hello (fornito come parametro **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="dc2b0-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="dc2b0-204">Per le opzioni MPI hello, hello quelli che vengono utilizzati con Intel MPI in Azure sono:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="dc2b0-205">`-mpi intel`toospecify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="dc2b0-206">`-fabric UDAPL`toouse InfiniBand Azure verbi.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="dc2b0-207">`-cpubind bandwidth,v`larghezza di banda di toooptimize per MPI con STELLA-CCM +.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="dc2b0-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI utilizzare Azure InfiniBand e hello tooset obbligatorio per un numero di core per nodo.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="dc2b0-209">`-batch`STELLA toostart-CCM + in modalità batch senza interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="dc2b0-210">Infine, toostart un processo, assicurarsi che i nodi siano in esecuzione e che siano online in Gestione Cluster.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="dc2b0-211">Da un prompt dei comandi di PowerShell eseguire quindi questo comando:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="dc2b0-212">Arrestare i nodi</span><span class="sxs-lookup"><span data-stu-id="dc2b0-212">Stop nodes</span></span>
<span data-ttu-id="dc2b0-213">In un secondo momento al termine dei test, è possibile utilizzare hello toostop di HPC Pack PowerShell i comandi seguenti e avviare i nodi:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="dc2b0-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc2b0-214">Next steps</span></span>
<span data-ttu-id="dc2b0-215">Provare a eseguire altri carichi di lavoro di Linux.</span><span class="sxs-lookup"><span data-stu-id="dc2b0-215">Try running other Linux workloads.</span></span> <span data-ttu-id="dc2b0-216">Per esempi, vedere:</span><span class="sxs-lookup"><span data-stu-id="dc2b0-216">For example, see:</span></span>

* [<span data-ttu-id="dc2b0-217">Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="dc2b0-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="dc2b0-218">Eseguire OpenFoam con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="dc2b0-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
