---
title: Eseguire STAR-CCM+ con HPC Pack in VM Linux | Microsoft Docs
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
ms.openlocfilehash: b45fcfb981287035da02fda62eaf5f9436ec2379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="90493-103">Eseguire STAR-CCM+ con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="90493-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="90493-104">Questo articolo illustra come distribuire un cluster Microsoft HPC Pack in Azure ed eseguire un processo [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) su più nodi di calcolo Linux interconnessi con InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="90493-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="90493-105">Microsoft HPC Pack fornisce le funzionalità necessarie per eseguire svariate applicazioni HPC e parallele su larga scala, incluse le applicazioni MPI, in cluster di macchine virtuali di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90493-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="90493-106">HPC Pack supporta anche applicazioni HPC che eseguono Linux su VM di nodi di calcolo Linux distribuite in un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="90493-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="90493-107">Per informazioni introduttive sull'uso di nodi di calcolo Linux con HPC Pack, vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="90493-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="90493-108">Configurare un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="90493-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="90493-109">Scaricare gli script di distribuzione IaaS per HPC Pack dall'[Area download](https://www.microsoft.com/en-us/download/details.aspx?id=44949) ed estrarli localmente.</span><span class="sxs-lookup"><span data-stu-id="90493-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="90493-110">Azure PowerShell è un prerequisito.</span><span class="sxs-lookup"><span data-stu-id="90493-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="90493-111">Se non è configurato nel computer locale, leggere l'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="90493-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="90493-112">Al momento della stesura di questo documento, le immagini Linux da Azure Marketplace, che include i driver InfiniBand per Azure, sono specifiche per SLES 12, CentOS 6.5 e CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="90493-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="90493-113">Questo articolo è basato sull'uso di SLES 12.</span><span class="sxs-lookup"><span data-stu-id="90493-113">This article is based on the usage of SLES 12.</span></span> <span data-ttu-id="90493-114">Per recuperare il nome di tutte le immagini Linux che supportano HPC nel Marketplace, è possibile eseguire il comando di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="90493-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="90493-115">L'output elenca le posizioni in cui sono disponibili le immagini e il nome dell'immagine (**ImageName**) da usare in seguito nel modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="90493-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span></span>

<span data-ttu-id="90493-116">Prima di distribuire il cluster, è necessario creare un file di modello di distribuzione per HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="90493-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span></span> <span data-ttu-id="90493-117">Poiché si specifica come destinazione un cluster di piccole dimensioni, il nodo head sarà il controller di dominio e ospiterà un database SQL locale.</span><span class="sxs-lookup"><span data-stu-id="90493-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span></span>

<span data-ttu-id="90493-118">Il modello seguente distribuirà un nodo head di questo tipo, creerà un nome file XML **MyCluster.xml** e sostituirà i valori di **SubscriptionId**, **StorageAccount**, **Location**, **VMName** e **ServiceName** con i valori dell'utente.</span><span class="sxs-lookup"><span data-stu-id="90493-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

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

<span data-ttu-id="90493-119">Avviare la creazione del nodo head eseguendo il comando di PowerShell in una finestra di comando con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="90493-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="90493-120">Il nodo head sarà pronto dopo 20-30 minuti.</span><span class="sxs-lookup"><span data-stu-id="90493-120">After 20 to 30 minutes, the head node should be ready.</span></span> <span data-ttu-id="90493-121">È possibile connettersi al nodo dal portale di Azure facendo clic sull'icona **Connetti** della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="90493-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span></span>

<span data-ttu-id="90493-122">Sarà infine necessario risolvere i problemi del server d'inoltro DNS.</span><span class="sxs-lookup"><span data-stu-id="90493-122">You might eventually have to fix the DNS forwarder.</span></span> <span data-ttu-id="90493-123">A questo scopo, avviare il Gestore DNS.</span><span class="sxs-lookup"><span data-stu-id="90493-123">To do so, start DNS Manager.</span></span>

1. <span data-ttu-id="90493-124">Fare clic con il pulsante destro del mouse sul nome del server in Gestore DNS, scegliere **Proprietà** e selezionare la scheda **Server d'inoltro**.</span><span class="sxs-lookup"><span data-stu-id="90493-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span></span>
2. <span data-ttu-id="90493-125">Fare clic sul pulsante **Modifica**, rimuovere gli eventuali server d'inoltro e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90493-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="90493-126">Assicurarsi di selezionare la casella di controllo **Usa parametri radice se non sono disponibili server d'inoltro** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="90493-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="90493-127">Configurare nodi di calcolo Linux</span><span class="sxs-lookup"><span data-stu-id="90493-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="90493-128">Distribuire i nodi di calcolo Linux con lo stesso modello di distribuzione usato per creare il nodo head.</span><span class="sxs-lookup"><span data-stu-id="90493-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span></span>

<span data-ttu-id="90493-129">Copiare il file **MyCluster.xml** dal computer locale nel nodo head e aggiornare il tag **NodeCount** con il numero di nodi da distribuire (<=20).</span><span class="sxs-lookup"><span data-stu-id="90493-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span></span> <span data-ttu-id="90493-130">Assicurarsi di avere un numero sufficiente di core disponibili nella quota di Azure, perché ogni istanza A9 utilizzerà 16 core nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90493-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="90493-131">È possibile usare istanze A8 (8 core) invece di A9, se si vogliono usare più VM nello stesso budget.</span><span class="sxs-lookup"><span data-stu-id="90493-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span></span>

<span data-ttu-id="90493-132">Nel nodo head copiare gli script di distribuzione IaaS per HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="90493-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="90493-133">Eseguire i comandi di Azure PowerShell seguenti in un prompt dei comandi con privilegi elevati:</span><span class="sxs-lookup"><span data-stu-id="90493-133">Run the following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="90493-134">Eseguire **Add-AzureAccount** per connettersi alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="90493-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span></span>
2. <span data-ttu-id="90493-135">Se sono disponibili più sottoscrizioni, eseguire **Get-AzureSubscription** per elencarle.</span><span class="sxs-lookup"><span data-stu-id="90493-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span></span>
3. <span data-ttu-id="90493-136">Impostare una sottoscrizione predefinita eseguendo il comando **Select-AzureSubscription -SubscriptionName xxxx -Default** .</span><span class="sxs-lookup"><span data-stu-id="90493-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="90493-137">Eseguire **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** per avviare la distribuzione dei nodi di calcolo Linux. </span><span class="sxs-lookup"><span data-stu-id="90493-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span></span>
   
   ![Distribuzione del nodo head][hndeploy]

<span data-ttu-id="90493-139">Aprire lo strumento HPC Pack Cluster Manager</span><span class="sxs-lookup"><span data-stu-id="90493-139">Open the HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="90493-140">Dopo alcuni minuti, i nodi di calcolo Linux verranno visualizzati normalmente in un elenco di nodi di calcolo del cluster.</span><span class="sxs-lookup"><span data-stu-id="90493-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="90493-141">Con la modalità di distribuzione classica, le VM IaaS vengono create in modo sequenziale,</span><span class="sxs-lookup"><span data-stu-id="90493-141">With the classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="90493-142">quindi se il numero di nodi è importante, la distribuzione di tutte le VM potrebbe richiedere una quantità di tempo significativa.</span><span class="sxs-lookup"><span data-stu-id="90493-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Nodi Linux in HPC Pack Cluster Manager][clustermanager]

<span data-ttu-id="90493-144">Quando tutti i nodi sono attivi e in esecuzione nel cluster, si dovranno configurare altri elementi dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="90493-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="90493-145">Configurare una condivisione file di Azure per nodi Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="90493-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="90493-146">È possibile usare il servizio File di Azure per archiviare script, pacchetti delle applicazioni e file di dati.</span><span class="sxs-lookup"><span data-stu-id="90493-146">You can use the Azure File service to store scripts, application packages, and data files.</span></span> <span data-ttu-id="90493-147">File di Azure offre funzionalità CIFS su un'archivio BLOB di Azure come archivio permanente.</span><span class="sxs-lookup"><span data-stu-id="90493-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="90493-148">Si noti che questa non è la soluzione più ridimensionabile, ma si tratta della soluzione più semplice e non richiede macchine virtuali dedicate.</span><span class="sxs-lookup"><span data-stu-id="90493-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="90493-149">Creare una condivisione file di Azure seguendo le istruzioni disponibili nell'articolo [Introduzione ad Archiviazione file di Azure in Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="90493-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="90493-150">Mantenere il nome dell'account di archiviazione **saname**, il nome della condivisione file **sharename** e la chiave dell'account di archiviazione **sakey**.</span><span class="sxs-lookup"><span data-stu-id="90493-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span></span>

### <a name="mount-the-azure-file-share-on-the-head-node"></a><span data-ttu-id="90493-151">Montare la condivisione file di Azure nel nodo head</span><span class="sxs-lookup"><span data-stu-id="90493-151">Mount the Azure File share on the head node</span></span>
<span data-ttu-id="90493-152">Aprire un prompt dei comandi con privilegi elevati ed eseguire il comando seguente per archiviare le credenziali nell'insieme di credenziali del computer locale.</span><span class="sxs-lookup"><span data-stu-id="90493-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="90493-153">Per montare quindi la condivisione file di Azure eseguire:</span><span class="sxs-lookup"><span data-stu-id="90493-153">Then, to mount the Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-the-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="90493-154">Montare la condivisione file di Azure nei nodi di calcolo Linux</span><span class="sxs-lookup"><span data-stu-id="90493-154">Mount the Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="90493-155">Uno strumento utile disponibile in HPC Pack è l'utilità clusrun.</span><span class="sxs-lookup"><span data-stu-id="90493-155">One useful tool that comes with HPC Pack is the clusrun tool.</span></span> <span data-ttu-id="90493-156">Questa riga di comando consente di eseguire lo stesso comando simultaneamente su un set di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="90493-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="90493-157">In questo caso viene usato per montare la condivisione file di Azure e renderla permanente, anche dopo eventuali riavvii.</span><span class="sxs-lookup"><span data-stu-id="90493-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span></span>
<span data-ttu-id="90493-158">In un prompt dei comandi con privilegi elevati sul nodo head eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="90493-158">In an elevated command prompt on the head node, run the following commands.</span></span>

<span data-ttu-id="90493-159">Per creare la directory di montaggio:</span><span class="sxs-lookup"><span data-stu-id="90493-159">To create the mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="90493-160">Per montare la condivisione file di Azure:</span><span class="sxs-lookup"><span data-stu-id="90493-160">To mount the Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="90493-161">Per rendere permanente la condivisione di montaggio:</span><span class="sxs-lookup"><span data-stu-id="90493-161">To persist the mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="90493-162">Installare STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="90493-162">Install STAR-CCM+</span></span>
<span data-ttu-id="90493-163">Le istanze A8 e A9 delle VM di Azure forniscono il supporto per InfiniBand e le funzionalità RDMA.</span><span class="sxs-lookup"><span data-stu-id="90493-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="90493-164">I driver del kernel che abilitano tali funzionalità sono disponibili in Azure Marketplace per le immagini Windows Server 2012 R2, SUSE 12, CentOS 6.5 e CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="90493-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span></span> <span data-ttu-id="90493-165">Microsoft MPI e Intel MPI (versione 5.x) sono le due librerie MPI che supportano questi driver in Azure.</span><span class="sxs-lookup"><span data-stu-id="90493-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="90493-166">CD-adapco STAR-CCM+ 11.x e versioni successive è incluso in Intel MPI versione 5.x, quindi è incluso il supporto di InfiniBand per Azure.</span><span class="sxs-lookup"><span data-stu-id="90493-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="90493-167">Ottenere il pacchetto Linux64 STAR-CCM+ dal [portale di CD-adapco](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="90493-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="90493-168">In questo caso, è stata usata la versione 11.02.010 con precisione mista.</span><span class="sxs-lookup"><span data-stu-id="90493-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="90493-169">Nel nodo head della condivisione file di Azure **/hpcdata** creare uno script della shell denominato **setupstarccm.sh** con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="90493-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span></span> <span data-ttu-id="90493-170">Questo script verrà eseguito in ogni nodo di calcolo per configurare STAR-CCM+ localmente.</span><span class="sxs-lookup"><span data-stu-id="90493-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="90493-171">Script setupstarcm.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="90493-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh to set up STAR-CCM+ locally

    # Create the CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy the STAR-CCM package from the file share to the local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract the package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without the FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="90493-172">Per configurare STAR-CCM+ in tutti i nodi di calcolo Linux, aprire un prompt dei comandi con privilegi elevati ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="90493-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="90493-173">Durante l'esecuzione del comando, è possibile monitorare l'utilizzo della CPU con la mappa termica di Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="90493-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span></span> <span data-ttu-id="90493-174">La configurazione di tutti i nodi dovrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="90493-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="90493-175">Eseguire processi STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="90493-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="90493-176">HPC Pack viene usato per le relative funzionalità di pianificazione di processi per l'esecuzione di processi STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="90493-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span></span> <span data-ttu-id="90493-177">A questo scopo, è necessario il supporto di alcuni script usati per attivare il processo ed eseguire STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="90493-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span></span> <span data-ttu-id="90493-178">I dati di input vengono mantenuti nella condivisione file di Azure prima di tutto per semplicità.</span><span class="sxs-lookup"><span data-stu-id="90493-178">The input data is kept on the Azure File share first for simplicity.</span></span>

<span data-ttu-id="90493-179">Lo script di Powershell seguente viene usato per accodare un processo STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="90493-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span></span> <span data-ttu-id="90493-180">Accetta tre argomenti:</span><span class="sxs-lookup"><span data-stu-id="90493-180">It takes three arguments:</span></span>

* <span data-ttu-id="90493-181">Nome del modello</span><span class="sxs-lookup"><span data-stu-id="90493-181">The model name</span></span>
* <span data-ttu-id="90493-182">Numero di nodi da usare</span><span class="sxs-lookup"><span data-stu-id="90493-182">The number of nodes to be used</span></span>
* <span data-ttu-id="90493-183">Numero di core in ogni nodo da usare</span><span class="sxs-lookup"><span data-stu-id="90493-183">The number of cores on each node to be used</span></span>

<span data-ttu-id="90493-184">Poiché STAR-CCM+ può consumare tutta la larghezza di banda della memoria, è in genere consigliabile usare un numero minore di core per ogni nodo di calcolo e aggiungere nuovi nodi.</span><span class="sxs-lookup"><span data-stu-id="90493-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="90493-185">Il rapporto esatto tra core e nodi dipende dalla famiglia del processore e dalla velocità di interconnessione.</span><span class="sxs-lookup"><span data-stu-id="90493-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span></span>

<span data-ttu-id="90493-186">I nodi vengono allocati esclusivamente per il processo e non possono essere condivisi con altri processi.</span><span class="sxs-lookup"><span data-stu-id="90493-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span></span> <span data-ttu-id="90493-187">Il processo non viene avviato direttamente come un processo MPI.</span><span class="sxs-lookup"><span data-stu-id="90493-187">The job is not started as an MPI job directly.</span></span> <span data-ttu-id="90493-188">Lo script della shell **runstarccm.sh** avvierà il servizio di avvio MPI.</span><span class="sxs-lookup"><span data-stu-id="90493-188">The **runstarccm.sh** shell script will start the MPI launcher.</span></span>

<span data-ttu-id="90493-189">Il modello di input e lo script **runstarccm.sh** vengono archiviati nella condivisione **/hpcdata** montata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="90493-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="90493-190">Ai file di log viene assegnato l'ID del processo come nome e i file vengono archiviati nella **condivisione /hpcdata**, insieme ai file di output di STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="90493-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="90493-191">Script SubmitStarccmJob.ps1 di esempio</span><span class="sxs-lookup"><span data-stu-id="90493-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us the job ID that's used to identify the name of the uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit the job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="90493-192">Sostituire **runner.java** con il servizio di avvio preferito per il modello Java STAR-CCM+ e con il codice di registrazione.</span><span class="sxs-lookup"><span data-stu-id="90493-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="90493-193">Script runstarccm.sh di esempio</span><span class="sxs-lookup"><span data-stu-id="90493-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # The path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set the mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into the hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with the hostfile argument
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

<span data-ttu-id="90493-194">Nel test viene usato un token di licenza di tipo Power-One-Demand.</span><span class="sxs-lookup"><span data-stu-id="90493-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="90493-195">Per questo token è necessario impostare la variabile di ambiente **$CDLMD_LICENSE_FILE** su **1999@flex.cd-adapco.com** e la chiave nell'opzione **-podkey** della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="90493-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span></span>

<span data-ttu-id="90493-196">Dopo alcune operazioni di inizializzazione, lo script estrae l'elenco di nodi per la compilazione di un file host usato dal servizio di avvio MPI dalle variabili di ambiente **$CCP_NODES_CORES** impostate da HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="90493-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span></span> <span data-ttu-id="90493-197">Il file host conterrà l'elenco di nomi di nodi di calcolo usati per il processo, un nome per ogni riga.</span><span class="sxs-lookup"><span data-stu-id="90493-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span></span>

<span data-ttu-id="90493-198">Il formato della variabile **$CCP_NODES_CORES** segue questo modello:</span><span class="sxs-lookup"><span data-stu-id="90493-198">The format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="90493-199">Dove:</span><span class="sxs-lookup"><span data-stu-id="90493-199">Where:</span></span>

* <span data-ttu-id="90493-200">`<Number of nodes>` è il numero di nodi allocati a questo processo.</span><span class="sxs-lookup"><span data-stu-id="90493-200">`<Number of nodes>` is the number of nodes allocated to this job.</span></span>
* <span data-ttu-id="90493-201">`<Name of node_n_...>` è il nome di ogni nodo allocato a questo processo.</span><span class="sxs-lookup"><span data-stu-id="90493-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span></span>
* <span data-ttu-id="90493-202">`<Cores of node_n_...>` è il numero di core nel nodo allocato a questo processo.</span><span class="sxs-lookup"><span data-stu-id="90493-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span></span>

<span data-ttu-id="90493-203">Il numero di core **$NBCORES** viene calcolato anche in base al numero di nodi **$NBNODES** e al numero di core per nodo specificato come parametro **$NBCORESPERNODE**.</span><span class="sxs-lookup"><span data-stu-id="90493-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="90493-204">Ecco le opzioni MPI usate con Intel MPI in Azure:</span><span class="sxs-lookup"><span data-stu-id="90493-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="90493-205">`-mpi intel` per specificare Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="90493-205">`-mpi intel` to specify Intel MPI.</span></span>
* <span data-ttu-id="90493-206">`-fabric UDAPL` per usare verbi InfiniBand Azure.</span><span class="sxs-lookup"><span data-stu-id="90493-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="90493-207">`-cpubind bandwidth,v` per ottimizzare la larghezza di banda per MPI con STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="90493-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="90493-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` per consentire il funzionamento di Intel MPI con InfiniBand Azure e impostare il numero di core per nodo necessario.</span><span class="sxs-lookup"><span data-stu-id="90493-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span></span>
* <span data-ttu-id="90493-209">`-batch` per avviare STAR-CCM+ in modalità batch senza interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="90493-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="90493-210">Per avviare un processo, assicurarsi infine che i nodi siano attivi, in esecuzione e online in Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="90493-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="90493-211">Da un prompt dei comandi di PowerShell eseguire quindi questo comando:</span><span class="sxs-lookup"><span data-stu-id="90493-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="90493-212">Arrestare i nodi</span><span class="sxs-lookup"><span data-stu-id="90493-212">Stop nodes</span></span>
<span data-ttu-id="90493-213">Al termine dei test, per arrestare e avviare i nodi è possibile usare i comandi di PowerShell seguenti per HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="90493-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="90493-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90493-214">Next steps</span></span>
<span data-ttu-id="90493-215">Provare a eseguire altri carichi di lavoro di Linux.</span><span class="sxs-lookup"><span data-stu-id="90493-215">Try running other Linux workloads.</span></span> <span data-ttu-id="90493-216">Per esempi, vedere:</span><span class="sxs-lookup"><span data-stu-id="90493-216">For example, see:</span></span>

* [<span data-ttu-id="90493-217">Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="90493-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="90493-218">Eseguire OpenFoam con Microsoft HPC Pack in un cluster Linux RDMA in Azure</span><span class="sxs-lookup"><span data-stu-id="90493-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
