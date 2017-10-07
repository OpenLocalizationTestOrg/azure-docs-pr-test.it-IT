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
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Creare un cluster di calcolo a elevate prestazioni (HPC) di Windows con script di distribuzione IaaS di HPC Pack hello
Eseguire hello IaaS di HPC Pack distribuzione PowerShell script toodeploy completamento del cluster HPC Pack 2012 R2 per i carichi di lavoro di Windows in macchine virtuali di Azure. Hello cluster è costituito da un nodo head appartenenti a un Active Directory in esecuzione Windows Server e Microsoft HPC Pack e si specifica di risorse di calcolo di finestre aggiuntive. Se si desidera toodeploy un cluster HPC Pack in Azure per i carichi di lavoro di Linux, vedere [creare un cluster HPC Linux con script di distribuzione IaaS di HPC Pack hello](../../linux/classic/hpcpack-cluster-powershell-script.md). È inoltre possibile utilizzare un toodeploy modello di Azure Resource Manager un cluster HPC Pack. Per degli esempi, vedere [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) (Creare un cluster HPC) e [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/) (Creare un cluster HPC con un'immagine di nodo di calcolo personalizzata).

> [!IMPORTANT] 
> Hello script di PowerShell descritto in questo articolo viene creato un cluster di Microsoft HPC Pack 2012 R2 in Azure utilizzando il modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.
> Inoltre, script hello descritto in questo articolo non supporta HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>File di configurazione di esempio
In hello negli esempi seguenti, sostituire i propri valori per l'Id sottoscrizione o nome e i nomi di account e il servizio di hello.

### <a name="example-1"></a>Esempio 1
Hello file di configurazione seguente consente di distribuire un cluster HPC Pack dotato di un nodo head con database locali e sistema operativo Windows Server 2012 R2 di hello cinque nodi di calcolo. Tutti i servizi cloud hello vengono creati direttamente nel percorso di Stati Uniti occidentali hello. nodo head Hello funge da controller di dominio della foresta di domini hello.

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

### <a name="example-2"></a>Esempio 2
Hello seguenti il file di configurazione consente di distribuire un cluster HPC Pack in una foresta di domini esistente. cluster Hello include 1 nodo head con database locali e 12 nodi con estensione BGInfo VM applicata hello di calcolo.
L'installazione automatica degli aggiornamenti di Windows è disabilitata per hello tutte le macchine virtuali in una foresta di domini hello. Tutti i servizi cloud hello creati direttamente in Asia orientale. nodi di calcolo Hello vengono creati tre servizi cloud e tre gli account di archiviazione: *da MyHPCCN-0001* troppo*MyHPCCN-0005* in *MyHPCCNService01* e  *mycnstorage01*; *Da MyHPCCN-0006* troppo*MyHPCCN0010* in *MyHPCCNService02* e *mycnstorage02*; e  *MyHPCCN-0011* troppo*MyHPCCN-0012* in *MyHPCCNService03* e *mycnstorage03*). nodi di calcolo Hello vengono creati da un'immagine privata esistente acquisita da un nodo di calcolo. Hello automatica aumentare e ridurre le servizio è abilitato con predefinito aumentare e ridurre gli intervalli.

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

### <a name="example-3"></a>Esempio 3
Hello seguenti il file di configurazione consente di distribuire un cluster HPC Pack in una foresta di domini esistente. Hello cluster contiene un nodo head, un server di database con un disco dati a 500 GB, due nodi broker che eseguono hello del sistema operativo di Windows Server 2012 R2 e sistema operativo Windows Server 2012 R2 di hello cinque nodi di calcolo. il servizio cloud MyHPCCNService viene creato nel gruppo di affinità hello Hello *MyIBAffinityGroup*, e hello altri servizi cloud vengono creati nel gruppo di affinità hello *MyAffinityGroup*. API REST dell'utilità di pianificazione di processo HPC Hello e portale web di HPC sono abilitati nel nodo head hello.

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



### <a name="example-4"></a>Esempio 4
Hello seguenti il file di configurazione consente di distribuire un cluster HPC Pack in una foresta di domini esistente. Hello cluster dispone di due nodi head con database locali, vengono creati due modelli di nodo di Azure e vengono creati tre nodi di Azure di medie dimensioni per il modello di nodo di Azure *AzureTemplate1*. Un file di script viene eseguito sul nodo head hello dopo aver configurato il nodo head di hello.

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

## <a name="troubleshooting"></a>Risoluzione dei problemi
* **Errore "La rete virtuale non esiste"** -se si esegue hello script toodeploy più cluster in Azure contemporaneamente in una sottoscrizione, una o più distribuzioni potrebbero non riuscire con l'errore hello "reti virtuali *VNet\_nome* non esiste".
  Se si verifica questo errore, eseguire script hello nuovamente per la distribuzione di hello non riuscita.
* **Problema di accesso hello Internet dalla rete virtuale di Azure hello** : se si crea un cluster con un nuovo controller di dominio tramite script di distribuzione hello o manualmente alzare di livello un nodo head VM toodomain controller, potrebbero verificarsi problemi connessione hello macchine virtuali toohello Internet. Questo problema può verificarsi se un server DNS di inoltro viene configurato automaticamente nel controller di dominio hello e questo server DNS di inoltro non viene risolto correttamente.
  
    toowork questo problema, accedere al controller di dominio toohello e l'impostazione di configurazione server d'inoltro hello rimuovere o configurare un server DNS di inoltro valido. tooconfigure questa impostazione, in Server Manager fare clic su **strumenti** >
    **DNS** tooopen gestore DNS, quindi fare doppio clic su **server d'inoltro**.
* **Problema di accesso di rete RDMA da macchine virtuali complesse** : se si aggiunge il calcolo di Windows Server o le dimensioni di macchine virtuali con un supporto per RDMA nodo broker, ad esempio A8 o A9, potrebbero verificarsi problemi di connessione di rete di applicazioni a tali macchine virtuali toohello RDMA. Questo problema si verifica uno dei motivi è se hello estensione HpcVmDrivers non è installato correttamente quando le macchine virtuali hello vengono aggiunti toohello cluster. L'estensione, ad esempio, potrebbe essere bloccata in hello lo stato di installazione.
  
    toowork questo problema, al primo controllo hello stato estensione hello in macchine virtuali di hello. Se l'estensione hello non è installato correttamente, provare a rimuovere i nodi di hello da un cluster HPC hello e quindi aggiungere di nuovo i nodi di hello. Ad esempio, è possibile aggiungere le macchine virtuali del nodo di calcolo eseguendo script Add-hpciaasnode.ps1 hello nel nodo head hello.

## <a name="next-steps"></a>Passaggi successivi
* Provare a eseguire un test di carico nel cluster hello. Per un esempio, vedere hello HPC Pack [Guida introduttiva](https://technet.microsoft.com/library/jj884144).
* Per un hello tooscript esercitazione della distribuzione del cluster ed eseguire un carico di lavoro HPC, vedere [iniziare con un cluster HPC Pack in Azure toorun carichi di lavoro Excel e SOA](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Provare toostart strumenti HPC Pack, arrestare, aggiungere e rimuovere i nodi di calcolo da un cluster a cui che si crea. Vedere [Gestire il numero e la disponibilità dei nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster-node-manage.md).
* tooget configurare cluster di toohello toosubmit processi da un computer locale, vedere [processi HPC di inviare un tooan computer locale HPC Pack del cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

