---
title: cluster HPC Windows toodeploy di script aaaPowerShell | Documenti Microsoft
description: Eseguire un toodeploy di script di PowerShell di un cluster Windows HPC Pack 2012 R2 in macchine virtuali di Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="034f8-103">Creare un cluster di calcolo a elevate prestazioni (HPC) di Windows con script di distribuzione IaaS di HPC Pack hello</span><span class="sxs-lookup"><span data-stu-id="034f8-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="034f8-104">Eseguire hello IaaS di HPC Pack distribuzione PowerShell script toodeploy completamento del cluster HPC Pack 2012 R2 per i carichi di lavoro di Windows in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="034f8-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="034f8-105">Hello cluster è costituito da un nodo head appartenenti a un Active Directory in esecuzione Windows Server e Microsoft HPC Pack e si specifica di risorse di calcolo di finestre aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="034f8-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="034f8-106">Se si desidera toodeploy un cluster HPC Pack in Azure per i carichi di lavoro di Linux, vedere [creare un cluster HPC Linux con script di distribuzione IaaS di HPC Pack hello](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="034f8-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="034f8-107">È inoltre possibile utilizzare un toodeploy modello di Azure Resource Manager un cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="034f8-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="034f8-108">Per degli esempi, vedere [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) (Creare un cluster HPC) e [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/) (Creare un cluster HPC con un'immagine di nodo di calcolo personalizzata).</span><span class="sxs-lookup"><span data-stu-id="034f8-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="034f8-109">Hello script di PowerShell descritto in questo articolo viene creato un cluster di Microsoft HPC Pack 2012 R2 in Azure utilizzando il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="034f8-110">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="034f8-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="034f8-111">Inoltre, script hello descritto in questo articolo non supporta HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="034f8-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="034f8-112">File di configurazione di esempio</span><span class="sxs-lookup"><span data-stu-id="034f8-112">Example configuration files</span></span>
<span data-ttu-id="034f8-113">In hello negli esempi seguenti, sostituire i propri valori per l'Id sottoscrizione o nome e i nomi di account e il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="034f8-114">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="034f8-114">Example 1</span></span>
<span data-ttu-id="034f8-115">Hello file di configurazione seguente consente di distribuire un cluster HPC Pack dotato di un nodo head con database locali e sistema operativo Windows Server 2012 R2 di hello cinque nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="034f8-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="034f8-116">Tutti i servizi cloud hello vengono creati direttamente nel percorso di Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="034f8-117">nodo head Hello funge da controller di dominio della foresta di domini hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-117">hello head node acts as domain controller of hello domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="034f8-118">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="034f8-118">Example 2</span></span>
<span data-ttu-id="034f8-119">Hello seguenti il file di configurazione consente di distribuire un cluster HPC Pack in una foresta di domini esistente.</span><span class="sxs-lookup"><span data-stu-id="034f8-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="034f8-120">cluster Hello include 1 nodo head con database locali e 12 nodi con estensione BGInfo VM applicata hello di calcolo.</span><span class="sxs-lookup"><span data-stu-id="034f8-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="034f8-121">L'installazione automatica degli aggiornamenti di Windows è disabilitata per hello tutte le macchine virtuali in una foresta di domini hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="034f8-122">Tutti i servizi cloud hello creati direttamente in Asia orientale.</span><span class="sxs-lookup"><span data-stu-id="034f8-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="034f8-123">nodi di calcolo Hello vengono creati tre servizi cloud e tre gli account di archiviazione: *da MyHPCCN-0001* troppo*MyHPCCN-0005* in *MyHPCCNService01* e  *mycnstorage01*; *Da MyHPCCN-0006* troppo*MyHPCCN0010* in *MyHPCCNService02* e *mycnstorage02*; e  *MyHPCCN-0011* troppo*MyHPCCN-0012* in *MyHPCCNService03* e *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="034f8-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="034f8-124">nodi di calcolo Hello vengono creati da un'immagine privata esistente acquisita da un nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="034f8-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="034f8-125">Hello automatica aumentare e ridurre le servizio è abilitato con predefinito aumentare e ridurre gli intervalli.</span><span class="sxs-lookup"><span data-stu-id="034f8-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="034f8-126">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="034f8-126">Example 3</span></span>
<span data-ttu-id="034f8-127">Hello seguenti il file di configurazione consente di distribuire un cluster HPC Pack in una foresta di domini esistente.</span><span class="sxs-lookup"><span data-stu-id="034f8-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="034f8-128">Hello cluster contiene un nodo head, un server di database con un disco dati a 500 GB, due nodi broker che eseguono hello del sistema operativo di Windows Server 2012 R2 e sistema operativo Windows Server 2012 R2 di hello cinque nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="034f8-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="034f8-129">il servizio cloud MyHPCCNService viene creato nel gruppo di affinità hello Hello *MyIBAffinityGroup*, e hello altri servizi cloud vengono creati nel gruppo di affinità hello *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="034f8-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="034f8-130">API REST dell'utilità di pianificazione di processo HPC Hello e portale web di HPC sono abilitati nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="034f8-131">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="034f8-131">Example 4</span></span>
<span data-ttu-id="034f8-132">Hello seguenti il file di configurazione consente di distribuire un cluster HPC Pack in una foresta di domini esistente.</span><span class="sxs-lookup"><span data-stu-id="034f8-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="034f8-133">Hello cluster dispone di due nodi head con database locali, vengono creati due modelli di nodo di Azure e vengono creati tre nodi di Azure di medie dimensioni per il modello di nodo di Azure *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="034f8-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="034f8-134">Un file di script viene eseguito sul nodo head hello dopo aver configurato il nodo head di hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-134">A script file runs on hello head node after hello head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="034f8-135">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="034f8-135">Troubleshooting</span></span>
* <span data-ttu-id="034f8-136">**Errore "La rete virtuale non esiste"** -se si esegue hello script toodeploy più cluster in Azure contemporaneamente in una sottoscrizione, una o più distribuzioni potrebbero non riuscire con l'errore hello "reti virtuali *VNet\_nome* non esiste".</span><span class="sxs-lookup"><span data-stu-id="034f8-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="034f8-137">Se si verifica questo errore, eseguire script hello nuovamente per la distribuzione di hello non riuscita.</span><span class="sxs-lookup"><span data-stu-id="034f8-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="034f8-138">**Problema di accesso hello Internet dalla rete virtuale di Azure hello** : se si crea un cluster con un nuovo controller di dominio tramite script di distribuzione hello o manualmente alzare di livello un nodo head VM toodomain controller, potrebbero verificarsi problemi connessione hello macchine virtuali toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="034f8-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="034f8-139">Questo problema può verificarsi se un server DNS di inoltro viene configurato automaticamente nel controller di dominio hello e questo server DNS di inoltro non viene risolto correttamente.</span><span class="sxs-lookup"><span data-stu-id="034f8-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="034f8-140">toowork questo problema, accedere al controller di dominio toohello e l'impostazione di configurazione server d'inoltro hello rimuovere o configurare un server DNS di inoltro valido.</span><span class="sxs-lookup"><span data-stu-id="034f8-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="034f8-141">tooconfigure questa impostazione, in Server Manager fare clic su **strumenti** >
    **DNS** tooopen gestore DNS, quindi fare doppio clic su **server d'inoltro**.</span><span class="sxs-lookup"><span data-stu-id="034f8-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="034f8-142">**Problema di accesso di rete RDMA da macchine virtuali complesse** : se si aggiunge il calcolo di Windows Server o le dimensioni di macchine virtuali con un supporto per RDMA nodo broker, ad esempio A8 o A9, potrebbero verificarsi problemi di connessione di rete di applicazioni a tali macchine virtuali toohello RDMA.</span><span class="sxs-lookup"><span data-stu-id="034f8-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="034f8-143">Questo problema si verifica uno dei motivi è se hello estensione HpcVmDrivers non è installato correttamente quando le macchine virtuali hello vengono aggiunti toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="034f8-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="034f8-144">L'estensione, ad esempio, potrebbe essere bloccata in hello lo stato di installazione.</span><span class="sxs-lookup"><span data-stu-id="034f8-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="034f8-145">toowork questo problema, al primo controllo hello stato estensione hello in macchine virtuali di hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="034f8-146">Se l'estensione hello non è installato correttamente, provare a rimuovere i nodi di hello da un cluster HPC hello e quindi aggiungere di nuovo i nodi di hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="034f8-147">Ad esempio, è possibile aggiungere le macchine virtuali del nodo di calcolo eseguendo script Add-hpciaasnode.ps1 hello nel nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="034f8-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="034f8-148">Next steps</span></span>
* <span data-ttu-id="034f8-149">Provare a eseguire un test di carico nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="034f8-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="034f8-150">Per un esempio, vedere hello HPC Pack [Guida introduttiva](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="034f8-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="034f8-151">Per un hello tooscript esercitazione della distribuzione del cluster ed eseguire un carico di lavoro HPC, vedere [iniziare con un cluster HPC Pack in Azure toorun carichi di lavoro Excel e SOA](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="034f8-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="034f8-152">Provare toostart strumenti HPC Pack, arrestare, aggiungere e rimuovere i nodi di calcolo da un cluster a cui che si crea.</span><span class="sxs-lookup"><span data-stu-id="034f8-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="034f8-153">Vedere [Gestire il numero e la disponibilità dei nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="034f8-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="034f8-154">tooget configurare cluster di toohello toosubmit processi da un computer locale, vedere [processi HPC di inviare un tooan computer locale HPC Pack del cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="034f8-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

