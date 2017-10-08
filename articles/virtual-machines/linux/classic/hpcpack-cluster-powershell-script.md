---
title: aaaPowerShell script toodeploy cluster HPC Linux | Documenti Microsoft
description: Eseguire un toodeploy di script di PowerShell di un cluster Linux HPC Pack 2012 R2 in macchine virtuali di Azure
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="67452-103">Creare un cluster di calcolo a elevate prestazioni (HPC) Linux con script di distribuzione IaaS di HPC Pack hello</span><span class="sxs-lookup"><span data-stu-id="67452-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="67452-104">Eseguire hello IaaS di HPC Pack distribuzione PowerShell script toodeploy completamento del cluster HPC Pack 2012 R2 per i carichi di lavoro di Linux in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="67452-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="67452-105">Hello cluster è costituito da un nodo head appartenenti a un Active Directory in esecuzione Windows Server e Microsoft HPC Pack e i nodi di calcolo che eseguono una delle hello distribuzioni Linux supportate da HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="67452-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="67452-106">Se si desidera toodeploy un cluster HPC Pack nei carichi di lavoro di Azure per Windows, vedere [creare un cluster Windows HPC con lo script di distribuzione IaaS di HPC Pack hello](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67452-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="67452-107">È inoltre possibile utilizzare un toodeploy modello di Azure Resource Manager un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="67452-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="67452-108">Per un esempio, vedere [Creare un cluster HPC con nodi di calcolo Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="67452-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="67452-109">Hello script di PowerShell descritto in questo articolo viene creato un cluster di Microsoft HPC Pack 2012 R2 in Azure utilizzando il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="67452-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="67452-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="67452-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="67452-111">Inoltre, script hello descritto in questo articolo non supporta HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="67452-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="67452-112">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="67452-112">Example configuration file</span></span>
<span data-ttu-id="67452-113">Hello file di configurazione seguente crea un controller di dominio e foresta di domini e distribuisce un cluster HPC Pack dotato di un nodo head con database locali e 10 nodi di calcolo di Linux.</span><span class="sxs-lookup"><span data-stu-id="67452-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="67452-114">Tutti i servizi cloud hello vengono creati direttamente nel percorso di hello Asia orientale.</span><span class="sxs-lookup"><span data-stu-id="67452-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="67452-115">Hello Linux nodi di calcolo vengono creati due servizi cloud e due account di archiviazione (vale a dire *MyLnxCN-0001* a *MyLnxCN-0005* in *MyLnxCNService01* e *mylnxstorage01*, e *MyLnxCN-0006* a *MyLnxCN 0010* in *MyLnxCNService02* e *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="67452-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="67452-116">nodi di calcolo Hello vengono creati da un'immagine di Linux CentOS OpenLogic versione 7.0.</span><span class="sxs-lookup"><span data-stu-id="67452-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="67452-117">Sostituire i valori per il nome della sottoscrizione e i nomi di account e il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="67452-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="67452-118">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="67452-118">Troubleshooting</span></span>
* <span data-ttu-id="67452-119">**Errore "La rete virtuale non esiste"**.</span><span class="sxs-lookup"><span data-stu-id="67452-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="67452-120">Se si esegue hello IaaS di HPC Pack distribuzione script toodeploy più cluster in Azure contemporaneamente in una sottoscrizione, una o più distribuzioni potrebbero non riuscire con l'errore hello "reti virtuali *VNet\_nome* non esiste".</span><span class="sxs-lookup"><span data-stu-id="67452-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="67452-121">Se si verifica questo errore, eseguire di nuovo script hello per la distribuzione di hello non riuscita.</span><span class="sxs-lookup"><span data-stu-id="67452-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="67452-122">**Problema di accesso hello Internet dalla rete virtuale di Azure hello**.</span><span class="sxs-lookup"><span data-stu-id="67452-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="67452-123">Se si crea un cluster HPC Pack con un nuovo controller di dominio utilizzando lo script di distribuzione hello o alzare manualmente di livello un nodo head controller toodomain VM, potrebbero verificarsi problemi di connessione hello macchine virtuali nella rete virtuale di Azure di hello toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="67452-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="67452-124">Ciò può verificarsi se un server DNS di inoltro viene configurato automaticamente nel controller di dominio hello e questo server DNS di inoltro non viene risolto correttamente.</span><span class="sxs-lookup"><span data-stu-id="67452-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="67452-125">toowork questo problema, accedere al controller di dominio toohello e l'impostazione di configurazione server d'inoltro hello rimuovere o configurare un server DNS di inoltro valido.</span><span class="sxs-lookup"><span data-stu-id="67452-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="67452-126">toodo, in Server Manager fare clic su **strumenti** > **DNS** tooopen gestore DNS, quindi fare doppio clic su **server d'inoltro**.</span><span class="sxs-lookup"><span data-stu-id="67452-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67452-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67452-127">Next steps</span></span>
* <span data-ttu-id="67452-128">Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per informazioni sulle distribuzioni Linux supportate, lo spostamento dei dati e l'invio di cluster di HPC Pack tooan processi con Linux nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="67452-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="67452-129">Per le esercitazioni che usare hello script toocreate un cluster ed eseguire un carico di lavoro HPC Linux, vedere:</span><span class="sxs-lookup"><span data-stu-id="67452-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="67452-130">Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="67452-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="67452-131">Eseguire OpenFoam con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="67452-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="67452-132">Eseguire STAR-CCM+ con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="67452-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

