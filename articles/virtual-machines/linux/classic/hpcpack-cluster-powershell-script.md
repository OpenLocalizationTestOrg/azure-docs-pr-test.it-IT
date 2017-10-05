---
title: Script PowerShell per distribuire cluster HPC Linux | Documentazione Microsoft
description: Eseguire uno script PowerShell per distribuire un cluster HPC Pack 2012 R2 Linux in macchine virtuali di Azure
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
ms.openlocfilehash: c15dc66718a855e22f8109448cb8c8a23787b9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="6d004-103">Creare un cluster HPC (High Performance Computing) Linux con lo script di distribuzione IaaS di HPC Pack</span><span class="sxs-lookup"><span data-stu-id="6d004-103">Create a Linux high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="6d004-104">Eseguire lo script PowerShell di distribuzione IaaS di HPC Pack per distribuire un cluster HPC Pack 2012 R2 completo per carichi di lavoro Linux in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d004-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="6d004-105">Il cluster è costituito da un nodo head aggiunto ad Active Directory che esegue Windows Server e Microsoft HPC Pack e da nodi di calcolo che eseguono una delle distribuzioni di Linux supportate da HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6d004-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of the Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="6d004-106">Se si desidera distribuire un cluster HPC Pack in Azure per i carichi di lavoro di Windows, vedere [Creare un cluster Windows HPC con lo script di distribuzione IaaS di HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d004-106">If you want to deploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="6d004-107">Per distribuire un cluster HPC Pack è anche possibile usare un modello di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d004-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="6d004-108">Per un esempio, vedere [Creare un cluster HPC con nodi di calcolo Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="6d004-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="6d004-109">Lo script PowerShell descritto in questo articolo crea un cluster Microsoft HPC Pack 2012 R2 in Azure usando il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="6d004-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="6d004-110">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="6d004-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="6d004-111">Lo script descritto in questo articolo inoltre non supporta HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="6d004-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="6d004-112">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="6d004-112">Example configuration file</span></span>
<span data-ttu-id="6d004-113">Il file di configurazione seguente crea una foresta di domini e di controller di dominio e distribuisce un cluster HPC Pack con un nodo head con database locali e 10 nodi di calcolo Linux.</span><span class="sxs-lookup"><span data-stu-id="6d004-113">The following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="6d004-114">Tutti i servizi cloud vengono creati direttamente nell'area Asia orientale.</span><span class="sxs-lookup"><span data-stu-id="6d004-114">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="6d004-115">I nodi di calcolo Linux vengono creati in due servizi cloud e due account di archiviazione (vale a dire *MyLnxCN-0001* a *MyLnxCN-0005* in *MyLnxCNService01* e *mylnxstorage01* e *MyLnxCN-0006* a *MyLnxCN-0010* in *MyLnxCNService02* e *mylnxstorage02*).</span><span class="sxs-lookup"><span data-stu-id="6d004-115">The Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="6d004-116">I nodi di calcolo sono creati da un'immagine OpenLogic CentOS versione 7.0.</span><span class="sxs-lookup"><span data-stu-id="6d004-116">The compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="6d004-117">Sostituire con i propri valori il nome della sottoscrizione e i nomi degli account e dei servizi.</span><span class="sxs-lookup"><span data-stu-id="6d004-117">Substitute your own values for your subscription name and the account and service names.</span></span>

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
## <a name="troubleshooting"></a><span data-ttu-id="6d004-118">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6d004-118">Troubleshooting</span></span>
* <span data-ttu-id="6d004-119">**Errore "La rete virtuale non esiste"**.</span><span class="sxs-lookup"><span data-stu-id="6d004-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="6d004-120">Se si esegue lo script di distribuzione IaaS di HPC Pack per distribuire istantaneamente più cluster in Azure in una sottoscrizione, è possibile che una o più distribuzioni generi l'errore "La rete virtuale *Nome\_Retevirtuale* non esiste".</span><span class="sxs-lookup"><span data-stu-id="6d004-120">If you run the HPC Pack IaaS deployment script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="6d004-121">In questo caso, eseguire nuovamente lo script per la distribuzione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="6d004-121">If this error occurs, rerun the script for the failed deployment.</span></span>
* <span data-ttu-id="6d004-122">**Problemi di accesso a Internet dalla rete virtuale di Azure**.</span><span class="sxs-lookup"><span data-stu-id="6d004-122">**Problem accessing the Internet from the Azure virtual network**.</span></span> <span data-ttu-id="6d004-123">Se si crea un cluster HPC Pack con un nuovo controller di dominio usando lo script di distribuzione oppure se si alza manualmente di livello la VM di un nodo head trasformandola in controller di dominio, è possibile che si verifichino problemi di connessione a Internet delle VM nella rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6d004-123">If you create an HPC Pack cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs in the Azure virtual network to the Internet.</span></span> <span data-ttu-id="6d004-124">Ciò si può verificare se un server DNS di inoltro viene configurato automaticamente nel controller di dominio e tale server non viene risolto correttamente.</span><span class="sxs-lookup"><span data-stu-id="6d004-124">This can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="6d004-125">Per risolvere il problema, accedere al controller di dominio e rimuovere l'impostazione di configurazione di inoltro oppure configurare un server DNS di inoltro valido.</span><span class="sxs-lookup"><span data-stu-id="6d004-125">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="6d004-126">A tale scopo, in Server Manager fare clic su **Strumenti** > **DNS** per aprire il Gestore DNS, quindi fare doppio clic su **Server d'inoltro**.</span><span class="sxs-lookup"><span data-stu-id="6d004-126">To do this, in Server Manager click **Tools** > **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d004-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6d004-127">Next steps</span></span>
* <span data-ttu-id="6d004-128">Vedere [Introduzione all'uso di nodi di calcolo Linux in un cluster HPC Pack in Azure](hpcpack-cluster.md) per informazioni sulle distribuzioni Linux supportate, lo spostamento dei dati e inviare processi a un cluster HPC Pack con Linux nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="6d004-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs to an HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="6d004-129">Per esercitazioni in cui si usa lo script per creare un cluster ed eseguire un carico di lavoro HPC Linux, vedere:</span><span class="sxs-lookup"><span data-stu-id="6d004-129">For tutorials that use the script to create a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="6d004-130">Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="6d004-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="6d004-131">Eseguire OpenFoam con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="6d004-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="6d004-132">Eseguire STAR-CCM+ con Microsoft HPC Pack su nodi di calcolo Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="6d004-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

