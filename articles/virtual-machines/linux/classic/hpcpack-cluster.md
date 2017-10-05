---
title: Macchine virtuali di calcolo Linux in un cluster HPC Pack | Microsoft Docs
description: Informazioni su come creare e usare un cluster HPC Pack in Azure per carichi di lavoro HPC (High Performance Computing) Linux
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
ms.openlocfilehash: 809d3944311badf265117d353b65642e044d900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="d18f1-103">Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="d18f1-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="d18f1-104">Configurare un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) in Azure contenente un nodo head che esegue Windows Server e diversi nodi di calcolo che eseguono una distribuzione di Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="d18f1-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="d18f1-105">Sono disponibili varie opzioni per spostare dati tra i nodi Linux e il nodo head Windows del cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-105">Explore options to move data among the Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="d18f1-106">Leggere le informazioni su come inviare processi HPC Linux al cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-106">Learn how to submit Linux HPC jobs to the cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d18f1-107">Il diagramma seguente illustra a livello generale il cluster HPC Pack creato e usato.</span><span class="sxs-lookup"><span data-stu-id="d18f1-107">At a high level, the following diagram shows the HPC Pack cluster you create and work with.</span></span>

![Cluster HPC Pack con nodi Linux][scenario]

<span data-ttu-id="d18f1-109">Per altre opzioni relative all'esecuzione di carichi di lavoro HPC in Linux e in Azure, vedere [Risorse tecniche per batch e high performance computing](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d18f1-109">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="d18f1-110">Distribuzione di un cluster HPC Pack con nodi di calcolo Linux</span><span class="sxs-lookup"><span data-stu-id="d18f1-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="d18f1-111">Questo articolo illustra due opzioni per distribuire un cluster HPC Pack in Azure con nodi di calcolo Linux.</span><span class="sxs-lookup"><span data-stu-id="d18f1-111">This article shows you two options to deploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="d18f1-112">Entrambi i metodi usano un'immagine del Marketplace di Windows Server con HPC Pack per creare il nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-112">Both methods use a Marketplace image of Windows Server with HPC Pack to create the head node.</span></span> 

* <span data-ttu-id="d18f1-113">**Modello di Azure Resource Manager** : usare un modello di Azure Marketplace o un modello di avvio rapido fornito dalla community per automatizzare la creazione del cluster nel modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d18f1-113">**Azure Resource Manager template** - Use a template from the Azure Marketplace, or a quickstart template from the community, to automate creation of the cluster in the Resource Manager deployment model.</span></span> <span data-ttu-id="d18f1-114">Ad esempio, il modello [Cluster HPC Pack per carichi di lavoro Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) in Azure Marketplace consente di creare un'infrastruttura di cluster HPC Pack per carichi di lavoro HPC Linux.</span><span class="sxs-lookup"><span data-stu-id="d18f1-114">For example, the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="d18f1-115">**Script PowerShell**: usare lo [script di distribuzione IaaS di Microsoft HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) per automatizzare la distribuzione completa di cluster nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="d18f1-115">**PowerShell script** - Use the [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) to automate a complete cluster deployment in the classic deployment model.</span></span> <span data-ttu-id="d18f1-116">Questo script di Azure PowerShell usa un'immagine di macchina virtuale di HPC Pack in Azure Marketplace per accelerare la distribuzione e fornisce un set completo di parametri di configurazione per distribuire nodi di calcolo Linux.</span><span class="sxs-lookup"><span data-stu-id="d18f1-116">This Azure PowerShell script uses an HPC Pack VM image in the Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters to deploy Linux compute nodes.</span></span>

<span data-ttu-id="d18f1-117">Per altre informazioni sulle opzioni di distribuzione del cluster HPC Pack in Azure, vedere le [opzioni per creare e gestire un cluster HPC in Azure con Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d18f1-117">For more information about HPC Pack cluster deployment options in Azure, see [Options to create and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d18f1-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d18f1-118">Prerequisites</span></span>
* <span data-ttu-id="d18f1-119">**Sottoscrizione di Azure** : è possibile usare una sottoscrizione nel servizio Azure globale o Azure Cina.</span><span class="sxs-lookup"><span data-stu-id="d18f1-119">**Azure subscription** - You can use a subscription in either the Azure Global or Azure China service.</span></span> <span data-ttu-id="d18f1-120">Se non si ha un account, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d18f1-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="d18f1-121">**Quota di core** : potrebbe essere necessario aumentare la quota di core, soprattutto se si sceglie di distribuire più nodi del cluster con dimensioni delle macchine virtuali multicore.</span><span class="sxs-lookup"><span data-stu-id="d18f1-121">**Cores quota** - You might need to increase the quota of cores, especially if you choose to deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="d18f1-122">Per aumentare una quota, aprire una richiesta di assistenza clienti online gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="d18f1-122">To increase a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="d18f1-123">**Distribuzioni Linux:** attualmente HPC Pack supporta le seguenti distribuzioni Linux per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="d18f1-123">**Linux distributions** - Currently HPC Pack supports the following Linux distributions for compute nodes.</span></span> <span data-ttu-id="d18f1-124">È possibile usare le versioni del Marketplace di queste distribuzioni, se disponibili, oppure fornire le proprie.</span><span class="sxs-lookup"><span data-stu-id="d18f1-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="d18f1-125">**Basate su CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="d18f1-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="d18f1-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="d18f1-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="d18f1-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 per HPC, SLES 12 per HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="d18f1-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="d18f1-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="d18f1-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="d18f1-129">Per usare una rete RDMA di Azure con una delle dimensioni di macchina virtuale con supporto per RDMA, specificare un'immagine HPC SUSE Linux Enterprise Server 12 o un'immagine HPC basata su CentOS da Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d18f1-129">To use the Azure RDMA network with one of the RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from the Azure Marketplace.</span></span> <span data-ttu-id="d18f1-130">Per altre informazioni, vedere [Dimensioni delle VM High Performance Computing (HPC)](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d18f1-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="d18f1-131">Prerequisiti aggiuntivi per distribuire il cluster usando lo script di distribuzione di HPC Pack IaaS:</span><span class="sxs-lookup"><span data-stu-id="d18f1-131">Additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="d18f1-132">**Computer client** : è necessario un computer client basato su Windows per eseguire lo script di distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-132">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="d18f1-133">**Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="d18f1-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="d18f1-134">**Script di distribuzione di HPC Pack IaaS** : scaricare e decomprimere la versione più recente dello script dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="d18f1-134">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="d18f1-135">È possibile controllare la versione dello script eseguendo `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="d18f1-135">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="d18f1-136">Questo articolo si basa sulla versione dello script 4.4.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d18f1-136">This article is based on version 4.4.1 or later of the script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="d18f1-137">Opzione di distribuzione 1.</span><span class="sxs-lookup"><span data-stu-id="d18f1-137">Deployment option 1.</span></span> <span data-ttu-id="d18f1-138">Usare il modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d18f1-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="d18f1-139">Andare al modello di [cluster HPC Pack per carichi di lavoro Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) in Azure Marketplace e fare clic su **Distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="d18f1-139">Go to the [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in the Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="d18f1-140">Nel portale di Azure verificare le informazioni e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d18f1-140">In the Azure portal, review the information and then click **Create**.</span></span>
   
    ![Creazione nel portale][portal]
3. <span data-ttu-id="d18f1-142">Nel pannello **Informazioni di base** immettere un nome per il cluster, che è anche il nome della macchina virtuale del nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-142">On the **Basics** blade, enter a name for the cluster, which also names the head node VM.</span></span> <span data-ttu-id="d18f1-143">È possibile scegliere un gruppo di risorse esistente o creare un gruppo per la distribuzione in un percorso disponibile.</span><span class="sxs-lookup"><span data-stu-id="d18f1-143">You can choose an existing resource group or create a group for the deployment in a location that's available to you.</span></span> <span data-ttu-id="d18f1-144">La disponibilità delle dimensioni di alcune macchine virtuali e di altri servizi di Azure può variare a seconda dell'area. Vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="d18f1-144">The location affects the availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="d18f1-145">Nel pannello **Impostazioni modo head** , per una prima distribuzione, in genere è possibile accettare le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="d18f1-145">On the **Head node settings** blade, for a first deployment, you can generally accept the default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="d18f1-146">**URL script di post-configurazione** è un'impostazione facoltativa per specificare uno script di Windows PowerShell disponibile pubblicamente che si vuole eseguire nella VM del nodo head una volta che questa sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d18f1-146">The **Post-configuration script URL** is an optional setting to specify a publicly available Windows PowerShell script that you want to run on the head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="d18f1-147">Nel pannello **Impostazioni nodo di calcolo** selezionare un pattern di nome per i nodi, il numero e le dimensioni dei nodi e la distribuzione Linux da distribuire.</span><span class="sxs-lookup"><span data-stu-id="d18f1-147">On the **Compute node settings** blade, select a naming pattern for the nodes, the number and size of the nodes, and the Linux distribution to deploy.</span></span>
6. <span data-ttu-id="d18f1-148">Nel pannello **Impostazioni infrastruttura** immettere i nomi per la rete virtuale e il dominio di Active Directory, le credenziali amministratore del dominio e della macchina virtuale e un pattern di nome per gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d18f1-148">On the **Infrastructure settings** blade, enter names for the virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for the storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d18f1-149">HPC Pack usa il dominio di Active Directory per autenticare gli utenti del cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-149">HPC Pack uses the Active Directory domain to authenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="d18f1-150">Dopo l'esecuzione dei test di convalida e l'analisi delle condizioni per l'uso, fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="d18f1-150">After the validation tests run and you review the terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-the-iaas-deployment-script"></a><span data-ttu-id="d18f1-151">Opzione di distribuzione 2.</span><span class="sxs-lookup"><span data-stu-id="d18f1-151">Deployment option 2.</span></span> <span data-ttu-id="d18f1-152">Uso dello script di distribuzione IaaS</span><span class="sxs-lookup"><span data-stu-id="d18f1-152">Use the IaaS deployment script</span></span>
<span data-ttu-id="d18f1-153">Prerequisiti aggiuntivi per distribuire il cluster usando lo script di distribuzione IaaS di HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="d18f1-153">Following are additional prerequisites to deploy the cluster by using the HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="d18f1-154">**Computer client** : è necessario un computer client basato su Windows per eseguire lo script di distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-154">**Client computer** - You need a Windows-based client computer to run the cluster deployment script.</span></span>
* <span data-ttu-id="d18f1-155">**Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="d18f1-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="d18f1-156">**Script di distribuzione di HPC Pack IaaS** : scaricare e decomprimere la versione più recente dello script dall' [Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="d18f1-156">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="d18f1-157">È possibile controllare la versione dello script eseguendo `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="d18f1-157">You can check the version of the script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="d18f1-158">Questo articolo si basa sulla versione dello script 4.4.1 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d18f1-158">This article is based on version 4.4.1 or later of the script.</span></span>

<span data-ttu-id="d18f1-159">**File di configurazione XML**</span><span class="sxs-lookup"><span data-stu-id="d18f1-159">**XML configuration file**</span></span>

<span data-ttu-id="d18f1-160">Lo script di distribuzione IaaS di HPC Pack usa come input un file di configurazione XML per descrivere il cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="d18f1-160">The HPC Pack IaaS deployment script uses an XML configuration file as input to describe the  HPC cluster.</span></span> <span data-ttu-id="d18f1-161">Il file di configurazione di esempio seguente definisce un cluster di dimensioni ridotte costituito da un nodo head di HPC Pack e due nodi di calcolo CentOS 7.0 di Linux di dimensioni A7.</span><span class="sxs-lookup"><span data-stu-id="d18f1-161">The following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="d18f1-162">Modificare il file in base alle necessità dell'ambiente e della configurazione cluster desiderata e salvarlo con un nome come HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="d18f1-162">Modify the file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="d18f1-163">Ad esempio, è necessario specificare il nome della sottoscrizione, un nome di account di archiviazione univoco e un nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="d18f1-163">For example, you need to supply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="d18f1-164">È inoltre consigliabile scegliere una diversa immagine Linux supportata per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="d18f1-164">Additionally, you might want to choose a different supported Linux image for the compute nodes.</span></span> <span data-ttu-id="d18f1-165">Per altre informazioni sugli elementi del file di configurazione, vedere il file Manual.rtf nella cartella dello script e l'articolo [Creare un cluster HPC con lo script di distribuzione di HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d18f1-165">For more information about the elements in the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="d18f1-166">**Per eseguire lo script di distribuzione di HPC Pack IaaS**</span><span class="sxs-lookup"><span data-stu-id="d18f1-166">**To run the HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="d18f1-167">Aprire PowerShell nel computer client come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d18f1-167">Open Windows PowerShell on the client computer as an administrator.</span></span>
2. <span data-ttu-id="d18f1-168">Sostituire la directory con la cartella in cui è installato lo script (E:\IaaSClusterScript in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="d18f1-168">Change directory to the folder where the script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="d18f1-169">Eseguire il comando seguente per distribuire il cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d18f1-169">Run the following command to deploy the HPC Pack cluster.</span></span> <span data-ttu-id="d18f1-170">In questo esempio si presuppone che il file di configurazione si trovi in E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="d18f1-170">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="d18f1-171">a.</span><span class="sxs-lookup"><span data-stu-id="d18f1-171">a.</span></span> <span data-ttu-id="d18f1-172">Poiché **AdminPassword** non è specificata nel comando precedente, viene chiesto di immettere la password per l'utente *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="d18f1-172">Because the **AdminPassword** is not specified in the preceding command, you are prompted to enter the password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="d18f1-173">b.</span><span class="sxs-lookup"><span data-stu-id="d18f1-173">b.</span></span> <span data-ttu-id="d18f1-174">Lo script avvia quindi la convalida del file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d18f1-174">The script then starts to validate the configuration file.</span></span> <span data-ttu-id="d18f1-175">Questa operazione richiede alcuni minuti a seconda della connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="d18f1-175">It can take up to several minutes depending on the network connection.</span></span>
   
    ![Convalida][validate]
   
    <span data-ttu-id="d18f1-177">c.</span><span class="sxs-lookup"><span data-stu-id="d18f1-177">c.</span></span> <span data-ttu-id="d18f1-178">Una volta superate le convalide, lo script elenca le risorse cluster da creare.</span><span class="sxs-lookup"><span data-stu-id="d18f1-178">After validations pass, the script lists the cluster resources to create.</span></span> <span data-ttu-id="d18f1-179">Immettere *Y* per continuare.</span><span class="sxs-lookup"><span data-stu-id="d18f1-179">Enter *Y* to continue.</span></span>
   
    ![Risorse][resources]
   
    <span data-ttu-id="d18f1-181">d.</span><span class="sxs-lookup"><span data-stu-id="d18f1-181">d.</span></span> <span data-ttu-id="d18f1-182">Lo script inizia a distribuire il cluster HPC Pack e completa la configurazione senza ulteriori passaggi manuali.</span><span class="sxs-lookup"><span data-stu-id="d18f1-182">The script starts to deploy the HPC Pack cluster and completes the configuration without further manual steps.</span></span> <span data-ttu-id="d18f1-183">L'esecuzione dello script può richiedere diversi minuti.</span><span class="sxs-lookup"><span data-stu-id="d18f1-183">The script can run for several minutes.</span></span>
   
    ![Distribuisci][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="d18f1-185">In questo esempio lo script genera automaticamente un file di log in quanto il parametro **-LogFile** non è specificato.</span><span class="sxs-lookup"><span data-stu-id="d18f1-185">In this example, the script generates a log file automatically since the **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="d18f1-186">I log non vengono scritti in tempo reale, ma vengono raccolti alla fine della convalida e della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d18f1-186">The logs aren't written in real time, but are collected at the end of the validation and the deployment.</span></span> <span data-ttu-id="d18f1-187">Se il processo di PowerShell viene arrestato mentre lo script è in esecuzione, alcuni log vengono persi.</span><span class="sxs-lookup"><span data-stu-id="d18f1-187">If the PowerShell process is stopped while the script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-to-the-head-node"></a><span data-ttu-id="d18f1-188">Connettersi al nodo head</span><span class="sxs-lookup"><span data-stu-id="d18f1-188">Connect to the head node</span></span>
<span data-ttu-id="d18f1-189">Dopo aver distribuito il cluster HPC Pack in Azure, [connettersi con Desktop remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) alla macchina virtuale del nodo head usando le credenziali del dominio specificate durante la distribuzione del cluster, ad esempio, *hpc\\clusteradmin*.</span><span class="sxs-lookup"><span data-stu-id="d18f1-189">After you deploy the HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="d18f1-190">Il cluster viene gestito dal nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-190">You manage the cluster from the head node.</span></span>

<span data-ttu-id="d18f1-191">Nel nodo head avviare Gestione cluster HPC per controllare lo stato del cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="d18f1-191">On the head node, start HPC Cluster Manager to check the status of the HPC Pack cluster.</span></span> <span data-ttu-id="d18f1-192">È possibile gestire e monitorare i nodi di calcolo di Linux nello stesso modo dei nodi di calcolo di Windows.</span><span class="sxs-lookup"><span data-stu-id="d18f1-192">You can manage and monitor Linux compute nodes the same way you work with Windows compute nodes.</span></span> <span data-ttu-id="d18f1-193">Ad esempio, vengono visualizzati i nodi Linux elencati in **Gestione risorse**. Questi nodi vengono distribuiti con il modello **LinuxNode**.</span><span class="sxs-lookup"><span data-stu-id="d18f1-193">For example, you see the Linux nodes listed in **Resource Management** (these nodes are deployed with the **LinuxNode** template).</span></span>

![Gestione dei nodi][management]

<span data-ttu-id="d18f1-195">I nodi Linux vengono visualizzati anche in **Mappa termica** .</span><span class="sxs-lookup"><span data-stu-id="d18f1-195">You also see the Linux nodes in the **Heat Map** view.</span></span>

![Mappa termica][heatmap]

## <a name="how-to-move-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="d18f1-197">Spostamento dei dati in un cluster con nodi Linux</span><span class="sxs-lookup"><span data-stu-id="d18f1-197">How to move data in a cluster with Linux nodes</span></span>
<span data-ttu-id="d18f1-198">Sono disponibili varie opzioni per spostare dati tra i nodi Linux e il nodo head Windows del cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-198">You have several choices to move data among Linux nodes and the Windows head node of the cluster.</span></span> <span data-ttu-id="d18f1-199">Nelle sezioni seguenti sono descritti nel dettaglio tre metodi comuni:</span><span class="sxs-lookup"><span data-stu-id="d18f1-199">Here are three common methods, described in more detail in the following sections:</span></span>

* <span data-ttu-id="d18f1-200">**File di Azure** : espone una condivisione file SMB gestita per archiviare i file di dati nella risorsa di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d18f1-200">**Azure File** - Exposes a managed SMB file share to store data files in Azure storage.</span></span> <span data-ttu-id="d18f1-201">I nodi di Windows e Linux possono montare contemporaneamente una condivisione di file Azure come un'unità o una cartella anche se vengono distribuiti in reti virtuali differenti.</span><span class="sxs-lookup"><span data-stu-id="d18f1-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at the same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="d18f1-202">**Condivisione SMB del nodo head** : monta una cartella condivisa Windows standard del nodo head in nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="d18f1-202">**Head node SMB share** - Mounts a standard Windows shared folder of the head node on Linux nodes.</span></span>
* <span data-ttu-id="d18f1-203">**Server NFS del nodo head**: offre una soluzione di condivisione file per un ambiente misto Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="d18f1-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="d18f1-204">Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="d18f1-204">Azure File storage</span></span>
<span data-ttu-id="d18f1-205">Il servizio [File di Azure](https://azure.microsoft.com/services/storage/files/) espone condivisioni di file usando il protocollo SMB 2.1 standard.</span><span class="sxs-lookup"><span data-stu-id="d18f1-205">The [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using the standard SMB 2.1 protocol.</span></span> <span data-ttu-id="d18f1-206">Le VM e i servizi cloud di Azure possono condividere i dati dei file tra componenti delle applicazioni tramite le condivisioni montate e le applicazioni locali possono accedere ai dati dei file in una condivisione tramite l'API della risorsa di archiviazione File.</span><span class="sxs-lookup"><span data-stu-id="d18f1-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through the File storage API.</span></span> 

<span data-ttu-id="d18f1-207">Per la procedura dettagliata per creare una condivisione file di Azure e per montarla nel nodo head, vedere [Introduzione all'archivio file di Azure in Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d18f1-207">For detailed steps to create an Azure File share and mount it on the head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="d18f1-208">Per montare la condivisione file di Azure nei nodi Linux, vedere [Come usare l'archiviazione file di Azure con Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d18f1-208">To mount the Azure File share on the Linux nodes, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="d18f1-209">Per configurare connessioni persistenti, vedere la pagina relativa alle [connessioni persistenti a file di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="d18f1-209">To set up persisting connections, see [Persisting connections to Microsoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="d18f1-210">Nell'esempio seguente creare una condivisione file di Azure in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d18f1-210">In the following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="d18f1-211">Per il montaggio della condivisione nel nodo head, aprire un prompt dei comandi e immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d18f1-211">To mount the share on the head node, open a Command Prompt and enter the following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="d18f1-212">In questo esempio, allvhdsje è il nome dell'account di archiviazione, storageaccountkey è la chiave dell'account di archiviazione e rdma è il nome della condivisione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="d18f1-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is the Azure File share name.</span></span> <span data-ttu-id="d18f1-213">La condivisione file di Azure viene montata come Z: nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-213">The Azure File share is mounted as Z: on the head node.</span></span>

<span data-ttu-id="d18f1-214">Per il montaggio della condivisione di File di Azure in nodi Linux, eseguire un comando **clusrun** sul nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-214">To mount the Azure File share on Linux nodes, run a **clusrun** command on the head node.</span></span> <span data-ttu-id="d18f1-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** è uno strumento di HPC Pack utile per eseguire attività amministrative su più nodi.</span><span class="sxs-lookup"><span data-stu-id="d18f1-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool to carry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="d18f1-216">Vedere anche [Clusrun per nodi Linux](#Clusrun-for-Linux-nodes) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d18f1-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="d18f1-217">Aprire una finestra di Windows PowerShell e immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d18f1-217">Open a Windows PowerShell window and enter the following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="d18f1-218">Il primo comando crea una cartella denominata /rdma su tutti i nodi del gruppo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="d18f1-218">The first command creates a folder named /rdma on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="d18f1-219">Il secondo comando consente di montare la condivisione di File di Azure allvhdsjw.file.core.windows.net/rdma nella cartella /rdma con dir e bit di modalità file impostati su 777.</span><span class="sxs-lookup"><span data-stu-id="d18f1-219">The second command mounts the Azure File share allvhdsjw.file.core.windows.net/rdma onto the /rdma folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="d18f1-220">Nel secondo comando, allvhdsje è il nome dell'account di archiviazione e storageaccountkey è la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d18f1-220">In the second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="d18f1-221">Il simbolo "\\`" nel secondo comando è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d18f1-221">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="d18f1-222">"\\`" significa che ",", ossia una virgola, è una parte del comando.</span><span class="sxs-lookup"><span data-stu-id="d18f1-222">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="d18f1-223">Condivisione del nodo head</span><span class="sxs-lookup"><span data-stu-id="d18f1-223">Head node share</span></span>
<span data-ttu-id="d18f1-224">In alternativa, montare una cartella condivisa del nodo head nei nodi Linux.</span><span class="sxs-lookup"><span data-stu-id="d18f1-224">Alternatively, mount a shared folder of the head node on Linux nodes.</span></span> <span data-ttu-id="d18f1-225">Una condivisione rappresenta il modo più semplice per condividere file, ma il nodo head e tutti i nodi Linux devono essere distribuiti nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d18f1-225">A share provides the simplest way to share files, but the head node and all Linux nodes must be deployed in the same virtual network.</span></span> <span data-ttu-id="d18f1-226">Di seguito sono riportati i passaggi necessari.</span><span class="sxs-lookup"><span data-stu-id="d18f1-226">Here are the steps.</span></span>

1. <span data-ttu-id="d18f1-227">Creare una cartella nel nodo head e condividerla per tutti gli utenti con autorizzazioni di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="d18f1-227">Create a folder on the head node and share it to Everyone with Read/Write permissions.</span></span> <span data-ttu-id="d18f1-228">Ad esempio, condividere D:\OpenFOAM nel nodo head come \\CentOS7RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="d18f1-228">For example, share D:\OpenFOAM on the head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="d18f1-229">CentOS7RDMA-HN è il nome host del nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-229">Here CentOS7RDMA-HN is the hostname of the head node.</span></span>
   
    ![Autorizzazioni di condivisione file][fileshareperms]
   
    ![Condivisione di file][filesharing]
2. <span data-ttu-id="d18f1-232">Aprire una finestra di Windows PowerShell ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d18f1-232">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="d18f1-233">Il primo comando crea una cartella denominata /openfoam in tutti i nodi del gruppo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="d18f1-233">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="d18f1-234">Il secondo comando monta la cartella condivisa //CentOS7RDMA-HN/OpenFOAM nella cartella con dir e bit di modalità file impostati su 777.</span><span class="sxs-lookup"><span data-stu-id="d18f1-234">The second command mounts the shared folder //CentOS7RDMA-HN/OpenFOAM onto the folder with dir and file mode bits set to 777.</span></span> <span data-ttu-id="d18f1-235">Il nome utente e la password nel comando devono corrispondere al nome utente e alla password di un utente del nodo head.</span><span class="sxs-lookup"><span data-stu-id="d18f1-235">The username and password in the command should be the username and password of a cluster user on the head node.</span></span> <span data-ttu-id="d18f1-236">Vedere [Aggiungere o rimuovere utenti del cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="d18f1-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="d18f1-237">Il simbolo "\\`" nel secondo comando è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d18f1-237">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="d18f1-238">"\\`" significa che ",", ossia una virgola, è una parte del comando.</span><span class="sxs-lookup"><span data-stu-id="d18f1-238">“\\`,” means that the “,” (comma character) is a part of the command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="d18f1-239">Server NFS</span><span class="sxs-lookup"><span data-stu-id="d18f1-239">NFS server</span></span>
<span data-ttu-id="d18f1-240">Il servizio NFS consente di condividere e migrare i file tra computer che eseguono il sistema operativo Windows Server 2012 usando il protocollo SMB e i computer basati su Linux mediante il protocollo NFS.</span><span class="sxs-lookup"><span data-stu-id="d18f1-240">The NFS service enables you to share and migrate files between computers running the Windows Server 2012 operating system using the SMB protocol and Linux-based computers using the NFS protocol.</span></span> <span data-ttu-id="d18f1-241">Il server NFS e tutti gli altri nodi devono essere distribuiti nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d18f1-241">The NFS server and all other nodes have to be deployed in the same virtual network.</span></span> <span data-ttu-id="d18f1-242">Consente di migliorare la compatibilità con i nodi Linux rispetto a una condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="d18f1-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="d18f1-243">Ad esempio, supporta il collegamento di file.</span><span class="sxs-lookup"><span data-stu-id="d18f1-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="d18f1-244">Per installare e configurare un server NFS, seguire la procedura riportata in [Server per condivisione primo Network File System end-to-end](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="d18f1-244">To install and set up an NFS server, follow the steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="d18f1-245">Ad esempio, creare una condivisione NFS denominata nfs con le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="d18f1-245">For example, create an NFS share named nfs with the following properties:</span></span>
   
    ![Autorizzazione NFS][nfsauth]
   
    ![Autorizzazioni di condivisione NFS][nfsshare]
   
    ![Autorizzazioni NFS NTFS][nfsperm]
   
    ![Proprietà di gestione di NFS][nfsmanage]
2. <span data-ttu-id="d18f1-250">Aprire una finestra di Windows PowerShell ed eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d18f1-250">Open a Windows PowerShell window and run the following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="d18f1-251">Il primo comando crea una cartella denominata /nfsshared su tutti i nodi del gruppo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="d18f1-251">The first command creates a folder named /nfsshared on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="d18f1-252">Il secondo comando consente di montare la condivisione CentOS7RDMA-HN:/nfs nella cartella.</span><span class="sxs-lookup"><span data-stu-id="d18f1-252">The second command mounts the NFS share CentOS7RDMA-HN:/nfs onto the folder.</span></span> <span data-ttu-id="d18f1-253">Qui CentOS7RDMA-HN:/nfs è il percorso remoto della condivisione NFS.</span><span class="sxs-lookup"><span data-stu-id="d18f1-253">Here CentOS7RDMA-HN:/nfs is the remote path of your NFS share.</span></span>

## <a name="how-to-submit-jobs"></a><span data-ttu-id="d18f1-254">Invio di processi</span><span class="sxs-lookup"><span data-stu-id="d18f1-254">How to submit jobs</span></span>
<span data-ttu-id="d18f1-255">Esistono vari metodi per inviare i processi al cluster HPC Pack:</span><span class="sxs-lookup"><span data-stu-id="d18f1-255">There are several ways to submit jobs to the HPC Pack cluster:</span></span>

* <span data-ttu-id="d18f1-256">Gestione cluster HPC o interfaccia grafica della Gestione cluster HPC</span><span class="sxs-lookup"><span data-stu-id="d18f1-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="d18f1-257">Portale Web HPC</span><span class="sxs-lookup"><span data-stu-id="d18f1-257">HPC web portal</span></span>
* <span data-ttu-id="d18f1-258">API REST</span><span class="sxs-lookup"><span data-stu-id="d18f1-258">REST API</span></span>

<span data-ttu-id="d18f1-259">La procedura di invio di processi al cluster in Azure tramite gli strumenti dell'interfaccia utente grafica di HPC Pack e il portale Web HPC è uguale a quella usata per i nodi di calcolo di Windows.</span><span class="sxs-lookup"><span data-stu-id="d18f1-259">Job submission to the cluster in Azure via HPC Pack GUI tools and the HPC web portal are the same as for Windows compute nodes.</span></span> <span data-ttu-id="d18f1-260">Vedere [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) (Gestore dei processi HPC Pack) e la [procedura per inviare i processi da un computer client locale](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d18f1-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How to submit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d18f1-261">Per inviare processi tramite l'API REST, vedere l'articolo relativo a [creazione e invio di processi tramite uso dell'API REST in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="d18f1-261">To submit jobs via the REST API, refer to [Creating and Submitting Jobs by Using the REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="d18f1-262">Per inviare processi a un client Linux, fare riferimento anche all'esempio Python in [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="d18f1-262">To submit jobs from a Linux client, also refer to the Python sample in the [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="d18f1-263">Clusrun per nodi Linux</span><span class="sxs-lookup"><span data-stu-id="d18f1-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="d18f1-264">Lo strumento [clusrun](https://technet.microsoft.com/library/cc947685.aspx) di HPC Pack può essere usato per eseguire comandi su nodi Linux tramite un prompt dei comandi o Gestione cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="d18f1-264">The HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used to execute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="d18f1-265">Di seguito sono riportati alcuni esempi di base.</span><span class="sxs-lookup"><span data-stu-id="d18f1-265">Following are some basic examples.</span></span>

* <span data-ttu-id="d18f1-266">Visualizzare i nomi utente correnti di tutti i nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-266">Show current user names on all nodes in the cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="d18f1-267">Installare lo strumento di debugger **gdb** con **yum** su tutti i nodi nel gruppo linuxnodes e riavviare i nodi dopo 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="d18f1-267">Install the **gdb** debugger tool with **yum** on all nodes in the linuxnodes group and then restart the nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="d18f1-268">Creare uno script shell che visualizza tutti i numeri da 1 e 10 per un secondo in ogni nodo Linux del cluster, eseguirlo e visualizzare immediatamente l'output dei nodi.</span><span class="sxs-lookup"><span data-stu-id="d18f1-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in the cluster, run it, and show output from the nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="d18f1-269">Potrebbe essere necessario usare determinati caratteri di escape nei comandi **clusrun** .</span><span class="sxs-lookup"><span data-stu-id="d18f1-269">You might need to use certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="d18f1-270">Come illustrato in questo esempio, usare ^ in un prompt dei comandi per eseguire l'escape del simbolo ">".</span><span class="sxs-lookup"><span data-stu-id="d18f1-270">As shown in this example, use ^ in a Command Prompt to escape the ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d18f1-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d18f1-271">Next steps</span></span>
* <span data-ttu-id="d18f1-272">Provare ad aumentare il numero di nodi del cluster o a eseguire un carico di lavoro Linux nel cluster.</span><span class="sxs-lookup"><span data-stu-id="d18f1-272">Try scaling up the cluster to a larger number of nodes, or try running a Linux workload on the cluster.</span></span> <span data-ttu-id="d18f1-273">Per un esempio, vedere [Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="d18f1-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="d18f1-274">Provare un cluster con [macchine virtuali a elevato utilizzo di calcolo e con supporto di RDMA](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) per eseguire carichi di lavoro MPI.</span><span class="sxs-lookup"><span data-stu-id="d18f1-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to run MPI workloads.</span></span> <span data-ttu-id="d18f1-275">Per un esempio, vedere [Eseguire OpenFOAM con Microsoft HPC Pack in un cluster Linux RDMA in Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="d18f1-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="d18f1-276">Se si è interessati a usare i nodi Linux in un cluster di HPC Pack locale, vedere le [linee guida di TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="d18f1-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see the [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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
