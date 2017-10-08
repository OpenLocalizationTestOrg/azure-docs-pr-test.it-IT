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
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="27da4-103">Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure</span><span class="sxs-lookup"><span data-stu-id="27da4-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="27da4-104">Configurare un cluster [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) in Azure contenente un nodo head che esegue Windows Server e diversi nodi di calcolo che eseguono una distribuzione di Linux supportata.</span><span class="sxs-lookup"><span data-stu-id="27da4-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="27da4-105">Esplorare i dati di opzioni toomove tra i nodi di Linux hello e nodo head di Windows hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="27da4-106">Informazioni su come i processi di HPC Linux toosubmit toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="27da4-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="27da4-107">In generale, hello diagramma seguente mostra cluster HPC Pack hello è creare e utilizzare.</span><span class="sxs-lookup"><span data-stu-id="27da4-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Cluster HPC Pack con nodi Linux][scenario]

<span data-ttu-id="27da4-109">Per altre toorun opzioni HPC Linux carichi di lavoro in Azure, vedere [risorse tecniche per batch e high performance computing](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="27da4-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="27da4-110">Distribuzione di un cluster HPC Pack con nodi di calcolo Linux</span><span class="sxs-lookup"><span data-stu-id="27da4-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="27da4-111">Questo articolo illustra due opzioni toodeploy di un cluster HPC Pack in Azure con nodi di calcolo di Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="27da4-112">Entrambi i metodi di utilizzano un'immagine del Marketplace di Windows Server con nodo head di HPC Pack toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="27da4-113">**Modello di Azure Resource Manager** -utilizzare un modello da hello Azure Marketplace o un modello di avvio rapido dalla community di hello, creazione di tooautomate di hello cluster nel modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="27da4-114">Ad esempio, hello [cluster HPC Pack per i carichi di lavoro di Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modello in hello Azure Marketplace consente di creare un'infrastruttura di cluster HPC Pack completa per HPC Linux carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="27da4-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="27da4-115">**Script di PowerShell** -hello utilizzare [script di distribuzione IaaS di Microsoft HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-hpciaascluster.ps1**) tooautomate una distribuzione completa del cluster nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="27da4-116">Questo script di PowerShell Azure utilizza un'immagine di macchina virtuale di HPC Pack in hello Azure Marketplace per la distribuzione rapida e fornisce un set completo di toodeploy parametri di configurazione di nodi di calcolo di Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="27da4-117">Per ulteriori informazioni sulle opzioni di distribuzione di cluster HPC Pack in Azure, vedere [opzioni toocreate e gestire un cluster ad alte prestazioni (HPC computing) in Azure con Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27da4-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="27da4-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="27da4-118">Prerequisites</span></span>
* <span data-ttu-id="27da4-119">**Sottoscrizione di Azure** -è possibile utilizzare una sottoscrizione in un servizio Azure globale o Azure China hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="27da4-120">Se non si ha un account, è possibile creare un [account gratuito](https://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="27da4-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="27da4-121">**Quota di core** -potrebbe essere necessario quota hello tooincrease di core, soprattutto se si sceglie toodeploy diversi nodi del cluster con dimensioni delle macchine Virtuali multicore.</span><span class="sxs-lookup"><span data-stu-id="27da4-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="27da4-122">tooincrease una quota, aprire una richiesta di supporto clienti online senza alcun costo.</span><span class="sxs-lookup"><span data-stu-id="27da4-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="27da4-123">**Distribuzioni Linux** -attualmente HPC Pack supporta hello seguendo le distribuzioni di Linux per nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="27da4-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="27da4-124">È possibile usare le versioni del Marketplace di queste distribuzioni, se disponibili, oppure fornire le proprie.</span><span class="sxs-lookup"><span data-stu-id="27da4-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="27da4-125">**Basate su CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="27da4-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="27da4-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="27da4-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="27da4-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 per HPC, SLES 12 per HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="27da4-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="27da4-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="27da4-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="27da4-129">toouse hello rete RDMA di Azure con una delle dimensioni delle macchine Virtuali hello con supporto per RDMA, specificare un'immagine di SUSE Linux Enterprise Server 12 HPC o basato su CentOS HPC da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="27da4-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="27da4-130">Per altre informazioni, vedere [Dimensioni delle VM High Performance Computing (HPC)](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27da4-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="27da4-131">Cluster di hello ulteriori prerequisiti toodeploy tramite script di distribuzione IaaS di HPC Pack hello:</span><span class="sxs-lookup"><span data-stu-id="27da4-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="27da4-132">**Computer client** -è necessario uno script di distribuzione basati su Windows client computer toorun hello cluster.</span><span class="sxs-lookup"><span data-stu-id="27da4-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="27da4-133">**Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="27da4-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="27da4-134">**Script di distribuzione IaaS di HPC Pack** : scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="27da4-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="27da4-135">È possibile controllare la versione di hello dello script di hello eseguendo `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="27da4-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="27da4-136">In questo articolo si basa sulla versione 4.4.1 o successiva di script hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="27da4-137">Opzione di distribuzione 1.</span><span class="sxs-lookup"><span data-stu-id="27da4-137">Deployment option 1.</span></span> <span data-ttu-id="27da4-138">Usare il modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27da4-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="27da4-139">Passare toohello [cluster HPC Pack per i carichi di lavoro di Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modello hello Azure Marketplace e fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="27da4-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="27da4-140">In hello portale di Azure, esaminare le informazioni di hello e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="27da4-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Creazione nel portale][portal]
3. <span data-ttu-id="27da4-142">In hello **nozioni di base** pannello, immettere un nome per il cluster hello, che anche i nomi di macchina virtuale del nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="27da4-143">È possibile scegliere un gruppo di risorse esistente o creare un gruppo per la distribuzione di hello in un percorso tooyou disponibili.</span><span class="sxs-lookup"><span data-stu-id="27da4-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="27da4-144">Hello posizione influisce sulla disponibilità di hello di determinate dimensioni delle macchine Virtuali e altri servizi di Azure (vedere [i prodotti disponibili per area](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="27da4-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="27da4-145">In hello **impostazioni del nodo Head** pannello per una distribuzione iniziale, in genere è possibile accettare le impostazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="27da4-146">Hello **URL dello script di post-configurazione** è facoltativa impostazione toospecify uno script di Windows PowerShell disponibile pubblicamente che si desidera toorun nella macchina virtuale del nodo head hello dopo che è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="27da4-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="27da4-147">In hello **impostazioni dei nodi di calcolo** pannello selezionare un modello di denominazione per i nodi di hello, numero hello e dimensioni dei nodi hello e hello toodeploy distribuzione Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="27da4-148">In hello **le impostazioni dell'infrastruttura** pannello, immettere un nome per la rete virtuale hello e Active Directory dominio, dominio e le credenziali di amministratore di macchina virtuale e un modello di denominazione per gli account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27da4-149">HPC Pack Usa hello Active Directory dominio tooauthenticate cluster users.</span><span class="sxs-lookup"><span data-stu-id="27da4-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="27da4-150">Dopo l'esecuzione dei test di convalida hello ed esaminare condizioni hello di utilizzo, fare clic su **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="27da4-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="27da4-151">Opzione di distribuzione 2.</span><span class="sxs-lookup"><span data-stu-id="27da4-151">Deployment option 2.</span></span> <span data-ttu-id="27da4-152">Utilizzare script di distribuzione IaaS di hello</span><span class="sxs-lookup"><span data-stu-id="27da4-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="27da4-153">Di seguito sono cluster hello di ulteriori prerequisiti toodeploy tramite script di distribuzione IaaS di HPC Pack hello:</span><span class="sxs-lookup"><span data-stu-id="27da4-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="27da4-154">**Computer client** -è necessario uno script di distribuzione basati su Windows client computer toorun hello cluster.</span><span class="sxs-lookup"><span data-stu-id="27da4-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="27da4-155">**Azure PowerShell** - [installare e configurare Azure PowerShell](/powershell/azure/overview) (versione 0.8.10 o versione successiva) nel computer client.</span><span class="sxs-lookup"><span data-stu-id="27da4-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="27da4-156">**Script di distribuzione IaaS di HPC Pack** : scaricare e decomprimere hello versione dello script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="27da4-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="27da4-157">È possibile controllare la versione di hello dello script di hello eseguendo `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="27da4-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="27da4-158">In questo articolo si basa sulla versione 4.4.1 o successiva di script hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="27da4-159">**File di configurazione XML**</span><span class="sxs-lookup"><span data-stu-id="27da4-159">**XML configuration file**</span></span>

<span data-ttu-id="27da4-160">Hello script di distribuzione IaaS di HPC Pack utilizza un file di configurazione XML come un cluster HPC hello toodescribe input.</span><span class="sxs-lookup"><span data-stu-id="27da4-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="27da4-161">Hello file di configurazione di esempio seguente specifica un piccolo cluster costituito da un nodo head di HPC Pack e due nodi di calcolo di dimensione A7 CentOS 7.0 Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="27da4-162">Modificare il file hello in base alle esigenze per l'ambiente e la configurazione del cluster desiderato e salvarlo con un nome, ad esempio HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="27da4-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="27da4-163">Ad esempio, è necessario toosupply il nome della sottoscrizione e un nome di account di archiviazione univoci e il nome del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="27da4-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="27da4-164">Inoltre, potrebbe essere toochoose un altro immagine Linux è supportata per i nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="27da4-165">Per ulteriori informazioni sugli elementi hello nel file di configurazione di hello, vedere il file Manual.rtf hello nella cartella script hello e [creare un cluster HPC con lo script di distribuzione IaaS di HPC Pack hello](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27da4-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="27da4-166">**hello toorun script di distribuzione IaaS di HPC Pack**</span><span class="sxs-lookup"><span data-stu-id="27da4-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="27da4-167">Aprire Windows PowerShell nel computer client hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="27da4-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="27da4-168">Modifica cartella toohello directory in cui si script hello installato (E:\IaaSClusterScript in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="27da4-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="27da4-169">Eseguire hello cluster HPC Pack hello toodeploy di comando seguente.</span><span class="sxs-lookup"><span data-stu-id="27da4-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="27da4-170">In questo esempio si presuppone che si trova il file di configurazione hello in E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="27da4-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="27da4-171">a.</span><span class="sxs-lookup"><span data-stu-id="27da4-171">a.</span></span> <span data-ttu-id="27da4-172">Poiché hello **AdminPassword** non è specificato in hello precedente comando, è richiesta tooenter password hello utente *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="27da4-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="27da4-173">b.</span><span class="sxs-lookup"><span data-stu-id="27da4-173">b.</span></span> <span data-ttu-id="27da4-174">script Hello avvia quindi i file di configurazione toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="27da4-175">È possibile richiedere tooseveral minuti a seconda della connessione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Convalida][validate]
   
    <span data-ttu-id="27da4-177">c.</span><span class="sxs-lookup"><span data-stu-id="27da4-177">c.</span></span> <span data-ttu-id="27da4-178">Dopo che hanno superato le convalide, script hello Elenca toocreate di risorse cluster hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="27da4-179">Immettere *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="27da4-179">Enter *Y* toocontinue.</span></span>
   
    ![Risorse][resources]
   
    <span data-ttu-id="27da4-181">d.</span><span class="sxs-lookup"><span data-stu-id="27da4-181">d.</span></span> <span data-ttu-id="27da4-182">script Hello toodeploy hello HPC Pack cluster sarà avviato e completato configurazione hello senza ulteriori passaggi manuali.</span><span class="sxs-lookup"><span data-stu-id="27da4-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="27da4-183">script Hello è possibile eseguire per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="27da4-183">hello script can run for several minutes.</span></span>
   
    ![Distribuire][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="27da4-185">In questo esempio hello script genera un file di log automaticamente dall'hello **- file di registro** parametro non è specificato.</span><span class="sxs-lookup"><span data-stu-id="27da4-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="27da4-186">Hello registri non vengono scritti in tempo reale, ma vengono raccolti alla fine di hello di convalida hello e hello della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="27da4-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="27da4-187">Se il processo di PowerShell hello viene arrestato durante l'esecuzione di script hello, alcuni log andranno persi.</span><span class="sxs-lookup"><span data-stu-id="27da4-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="27da4-188">Nodo head toohello connettersi</span><span class="sxs-lookup"><span data-stu-id="27da4-188">Connect toohello head node</span></span>
<span data-ttu-id="27da4-189">Dopo aver distribuito il cluster HPC Pack hello in Azure, [connessione Desktop remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello nodo head VM utilizzando le credenziali di dominio fornito al momento della distribuzione cluster hello di hello (ad esempio, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="27da4-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="27da4-190">Gestire i cluster di hello dal nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="27da4-191">Nel nodo head hello, avviare HPC Cluster Manager toocheck lo stato di hello del cluster HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="27da4-192">È possibile gestire e monitorare i nodi di calcolo Linux hello allo stesso modo di utilizzare le finestre nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="27da4-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="27da4-193">Ad esempio, vengono mostrati i nodi di Linux hello elencati in **la gestione delle risorse** (questi nodi vengono distribuiti con hello **LinuxNode** modello).</span><span class="sxs-lookup"><span data-stu-id="27da4-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Gestione dei nodi][management]

<span data-ttu-id="27da4-195">È inoltre visualizzare i nodi di Linux hello hello **mappa termica** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="27da4-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Mappa termica][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="27da4-197">Come toomove dati in un cluster con nodi di Linux</span><span class="sxs-lookup"><span data-stu-id="27da4-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="27da4-198">Si dispone di più dati di toomove scelte tra nodi di Linux e nodo head di Windows hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="27da4-199">Di seguito sono tre metodi comuni, descritti in dettaglio nelle sezioni che seguono hello:</span><span class="sxs-lookup"><span data-stu-id="27da4-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="27da4-200">**File di Azure** -espone dati di toostore condivisione di file SMB gestiti i file nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="27da4-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="27da4-201">Nodi di Windows e Linux possono montare una condivisione di File di Azure come un'unità o cartella hello stesso tempo, anche se vengano distribuite in reti virtuali diverse.</span><span class="sxs-lookup"><span data-stu-id="27da4-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="27da4-202">**Nodo head SMB condividere** -Monta una cartella condivisa Windows standard del nodo head hello in nodi di Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="27da4-203">**Server NFS del nodo head**: offre una soluzione di condivisione file per un ambiente misto Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="27da4-204">Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="27da4-204">Azure File storage</span></span>
<span data-ttu-id="27da4-205">Hello [File di Azure](https://azure.microsoft.com/services/storage/files/) servizio espone condivisioni file usando il protocollo SMB 2.1 standard hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="27da4-206">Servizi cloud e macchine virtuali di Azure possono condividere i dati di file tra componenti delle applicazioni tramite condivisioni montate e applicazioni locali possono accedere dati in una condivisione di file tramite API di archiviazione di File hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="27da4-207">Per i passaggi dettagliati toocreate condividere e montarlo nel nodo head hello di un File di Azure, vedere [Introduzione all'archiviazione di File di Azure in Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="27da4-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="27da4-208">condivisione di File di Azure toomount hello in nodi di Linux hello, vedere [come archiviazione di File di Azure con Linux toouse](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="27da4-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="27da4-209">tooset le connessioni persistenti, vedere [tooMicrosoft connessioni Persisting Azure file](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="27da4-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="27da4-210">Nell'esempio seguente di hello, creare una condivisione di File di Azure in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="27da4-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="27da4-211">hello toomount condivisione nel nodo head hello, aprire un prompt dei comandi e immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="27da4-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="27da4-212">In questo esempio, allvhdsje è il nome di account di archiviazione, storageaccountkey è la chiave di account di archiviazione e rdma è hello nome della condivisione File di Azure.</span><span class="sxs-lookup"><span data-stu-id="27da4-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="27da4-213">condivisione di File di Azure Hello viene montata come z nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="27da4-214">condivisione di File di Azure toomount hello in nodi di Linux, eseguire una **clusrun** comando nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="27da4-215">**[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  è un utile toocarry strumento di HPC Pack operazioni amministrative su più nodi.</span><span class="sxs-lookup"><span data-stu-id="27da4-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="27da4-216">Vedere anche [Clusrun per nodi Linux](#Clusrun-for-Linux-nodes) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="27da4-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="27da4-217">Aprire una finestra di Windows PowerShell e immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="27da4-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="27da4-218">Hello primo comando crea una cartella denominata /rdma in tutti i nodi nel gruppo LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="27da4-219">comando secondo Hello Monta hello Azure File condivisione allvhdsjw.file.core.windows.net/rdma nella cartella /rdma hello con dir e file too777 di set di bit di modalità.</span><span class="sxs-lookup"><span data-stu-id="27da4-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="27da4-220">Nel secondo comando hello, allvhdsje è il nome di account di archiviazione e storageaccountkey è la chiave di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="27da4-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="27da4-221">Hello "\\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27da4-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="27da4-222">"\\`,"significa che hello"," (carattere virgola) è una parte del comando hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="27da4-223">Condivisione del nodo head</span><span class="sxs-lookup"><span data-stu-id="27da4-223">Head node share</span></span>
<span data-ttu-id="27da4-224">In alternativa, è possibile montare una cartella condivisa del nodo head hello in nodi di Linux.</span><span class="sxs-lookup"><span data-stu-id="27da4-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="27da4-225">Una condivisione vengono forniti i file tooshare modo più semplici hello ma nodo head hello e tutti i nodi di Linux devono essere distribuiti in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="27da4-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="27da4-226">Ecco i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-226">Here are hello steps.</span></span>

1. <span data-ttu-id="27da4-227">Creare una cartella nel nodo head hello e condividerlo tooEveryone con autorizzazioni di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="27da4-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="27da4-228">Ad esempio condividere D:\OpenFOAM nel nodo head di hello come \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="27da4-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="27da4-229">Ecco hello nome host del nodo head hello CentOS7RDMA HN.</span><span class="sxs-lookup"><span data-stu-id="27da4-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Autorizzazioni di condivisione file][fileshareperms]
   
    ![Condivisione di file][filesharing]
2. <span data-ttu-id="27da4-232">Aprire una finestra di Windows PowerShell ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="27da4-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="27da4-233">Hello primo comando crea una cartella denominata /openfoam in tutti i nodi nel gruppo LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="27da4-234">comando secondo Hello Monta //CentOS7RDMA-HN/OpenFOAM cartella hello condivise nella cartella hello con dir e file too777 di set di bit di modalità.</span><span class="sxs-lookup"><span data-stu-id="27da4-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="27da4-235">Hello nome utente e password nel comando hello devono essere hello username e password di un utente del cluster nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="27da4-236">Vedere [Aggiungere o rimuovere utenti del cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="27da4-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="27da4-237">Hello "\\`" simbolo nel secondo comando hello è un simbolo di escape per PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27da4-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="27da4-238">"\\`,"significa che hello"," (carattere virgola) è una parte del comando hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="27da4-239">Server NFS</span><span class="sxs-lookup"><span data-stu-id="27da4-239">NFS server</span></span>
<span data-ttu-id="27da4-240">Hello servizio NFS consente tooshare ed eseguire la migrazione di file tra computer con sistema operativo Windows Server 2012 hello mediante protocollo SMB hello e i computer basati su Linux mediante protocollo NFS hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="27da4-241">Hello del server NFS e tutti gli altri nodi hanno distribuito in hello toobe stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="27da4-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="27da4-242">Consente di migliorare la compatibilità con i nodi Linux rispetto a una condivisione SMB.</span><span class="sxs-lookup"><span data-stu-id="27da4-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="27da4-243">Ad esempio, supporta il collegamento di file.</span><span class="sxs-lookup"><span data-stu-id="27da4-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="27da4-244">tooinstall e configurare un server NFS, seguire i passaggi hello [Server per il File System prima rete End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="27da4-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="27da4-245">Ad esempio, creare una condivisione NFS denominata nfs con hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="27da4-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Autorizzazione NFS][nfsauth]
   
    ![Autorizzazioni di condivisione NFS][nfsshare]
   
    ![Autorizzazioni NFS NTFS][nfsperm]
   
    ![Proprietà di gestione di NFS][nfsmanage]
2. <span data-ttu-id="27da4-250">Aprire una finestra di Windows PowerShell ed eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="27da4-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="27da4-251">Hello primo comando crea una cartella denominata /nfsshared in tutti i nodi nel gruppo LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="27da4-252">secondo comando mount hello NFS Hello condividere CentOS7RDMA HN: / hello di nfs nella cartella.</span><span class="sxs-lookup"><span data-stu-id="27da4-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="27da4-253">Qui CentOS7RDMA HN: nfs è percorso remoto di hello della condivisione NFS.</span><span class="sxs-lookup"><span data-stu-id="27da4-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="27da4-254">Come i processi toosubmit</span><span class="sxs-lookup"><span data-stu-id="27da4-254">How toosubmit jobs</span></span>
<span data-ttu-id="27da4-255">Esistono diversi cluster con HPC Pack toohello modi toosubmit processi:</span><span class="sxs-lookup"><span data-stu-id="27da4-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="27da4-256">Gestione cluster HPC o interfaccia grafica della Gestione cluster HPC</span><span class="sxs-lookup"><span data-stu-id="27da4-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="27da4-257">Portale Web HPC</span><span class="sxs-lookup"><span data-stu-id="27da4-257">HPC web portal</span></span>
* <span data-ttu-id="27da4-258">API REST</span><span class="sxs-lookup"><span data-stu-id="27da4-258">REST API</span></span>

<span data-ttu-id="27da4-259">Invio di processi toohello cluster in Azure tramite strumenti di HPC Pack GUI e portale web di HPC hello sono hello uguale a quello di nodi di calcolo di Windows.</span><span class="sxs-lookup"><span data-stu-id="27da4-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="27da4-260">Vedere [il gestore di processi di HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [come toosubmit processi da un computer client locale](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="27da4-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="27da4-261">processi toosubmit tramite hello API REST, vedere troppo[creazione e invio di processi tramite hello API REST di Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="27da4-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="27da4-262">processi toosubmit da un client Linux, fare riferimento anche esempio Python toohello in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="27da4-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="27da4-263">Clusrun per nodi Linux</span><span class="sxs-lookup"><span data-stu-id="27da4-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="27da4-264">Hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) strumento può essere utilizzato tooexecute comandi nei nodi Linux tramite un prompt dei comandi o HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="27da4-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="27da4-265">Di seguito sono riportati alcuni esempi di base.</span><span class="sxs-lookup"><span data-stu-id="27da4-265">Following are some basic examples.</span></span>

* <span data-ttu-id="27da4-266">Mostra i nomi utente correnti in tutti i nodi del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="27da4-267">Installare hello **gdb** dello strumento debugger con **yum** in tutti i nodi hello linuxnodes gruppo e quindi riavviare i nodi di hello dopo 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="27da4-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="27da4-268">Creare uno script della shell visualizzazione ogni numero da 1 a 10 per un secondo in ogni nodo di Linux in cluster hello, eseguirlo e visualizzare immediatamente l'output dai nodi hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="27da4-269">Potrebbe essere necessario toouse alcuni caratteri di escape nei **clusrun** comandi.</span><span class="sxs-lookup"><span data-stu-id="27da4-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="27da4-270">Come illustrato in questo esempio, utilizzare ^ in hello di tooescape un prompt dei comandi ">" simbolo.</span><span class="sxs-lookup"><span data-stu-id="27da4-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="27da4-271">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27da4-271">Next steps</span></span>
* <span data-ttu-id="27da4-272">Provare la scalabilità verticale hello cluster tooa maggior numero di nodi oppure provare a eseguire un carico di lavoro di Linux nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="27da4-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="27da4-273">Per un esempio, vedere [Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="27da4-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="27da4-274">Provare a un cluster con [macchine virtuali che supportano RDMA, con uso intensivo](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun carichi di lavoro MPI.</span><span class="sxs-lookup"><span data-stu-id="27da4-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="27da4-275">Per un esempio, vedere [Eseguire OpenFOAM con Microsoft HPC Pack in un cluster Linux RDMA in Azure](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="27da4-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="27da4-276">Se si desidera utilizzare con i nodi di Linux in un cluster HPC Pack locale, vedere hello [Guida TechNet](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="27da4-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

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
