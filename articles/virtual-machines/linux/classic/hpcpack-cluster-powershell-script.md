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
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Creare un cluster di calcolo a elevate prestazioni (HPC) Linux con script di distribuzione IaaS di HPC Pack hello
Eseguire hello IaaS di HPC Pack distribuzione PowerShell script toodeploy completamento del cluster HPC Pack 2012 R2 per i carichi di lavoro di Linux in macchine virtuali di Azure. Hello cluster è costituito da un nodo head appartenenti a un Active Directory in esecuzione Windows Server e Microsoft HPC Pack e i nodi di calcolo che eseguono una delle hello distribuzioni Linux supportate da HPC Pack. Se si desidera toodeploy un cluster HPC Pack nei carichi di lavoro di Azure per Windows, vedere [creare un cluster Windows HPC con lo script di distribuzione IaaS di HPC Pack hello](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). È inoltre possibile utilizzare un toodeploy modello di Azure Resource Manager un cluster HPC Pack. Per un esempio, vedere [Creare un cluster HPC con nodi di calcolo Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Hello script di PowerShell descritto in questo articolo viene creato un cluster di Microsoft HPC Pack 2012 R2 in Azure utilizzando il modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.
> Inoltre, script hello descritto in questo articolo non supporta HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>File di configurazione di esempio
Hello file di configurazione seguente crea un controller di dominio e foresta di domini e distribuisce un cluster HPC Pack dotato di un nodo head con database locali e 10 nodi di calcolo di Linux. Tutti i servizi cloud hello vengono creati direttamente nel percorso di hello Asia orientale. Hello Linux nodi di calcolo vengono creati due servizi cloud e due account di archiviazione (vale a dire *MyLnxCN-0001* a *MyLnxCN-0005* in *MyLnxCNService01* e *mylnxstorage01*, e *MyLnxCN-0006* a *MyLnxCN 0010* in *MyLnxCNService02* e *mylnxstorage02* ). nodi di calcolo Hello vengono creati da un'immagine di Linux CentOS OpenLogic versione 7.0. 

Sostituire i valori per il nome della sottoscrizione e i nomi di account e il servizio di hello.

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
## <a name="troubleshooting"></a>Risoluzione dei problemi
* **Errore "La rete virtuale non esiste"**. Se si esegue hello IaaS di HPC Pack distribuzione script toodeploy più cluster in Azure contemporaneamente in una sottoscrizione, una o più distribuzioni potrebbero non riuscire con l'errore hello "reti virtuali *VNet\_nome* non esiste".
  Se si verifica questo errore, eseguire di nuovo script hello per la distribuzione di hello non riuscita.
* **Problema di accesso hello Internet dalla rete virtuale di Azure hello**. Se si crea un cluster HPC Pack con un nuovo controller di dominio utilizzando lo script di distribuzione hello o alzare manualmente di livello un nodo head controller toodomain VM, potrebbero verificarsi problemi di connessione hello macchine virtuali nella rete virtuale di Azure di hello toohello Internet. Ciò può verificarsi se un server DNS di inoltro viene configurato automaticamente nel controller di dominio hello e questo server DNS di inoltro non viene risolto correttamente.
  
    toowork questo problema, accedere al controller di dominio toohello e l'impostazione di configurazione server d'inoltro hello rimuovere o configurare un server DNS di inoltro valido. toodo, in Server Manager fare clic su **strumenti** > **DNS** tooopen gestore DNS, quindi fare doppio clic su **server d'inoltro**.

## <a name="next-steps"></a>Passaggi successivi
* Vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](hpcpack-cluster.md) per informazioni sulle distribuzioni Linux supportate, lo spostamento dei dati e l'invio di cluster di HPC Pack tooan processi con Linux nodi di calcolo.
* Per le esercitazioni che usare hello script toocreate un cluster ed eseguire un carico di lavoro HPC Linux, vedere:
  * [Eseguire NAMD con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-namd.md)
  * [Eseguire OpenFoam con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-openfoam.md)
  * [Eseguire STAR-CCM+ con Microsoft HPC Pack su nodi di calcolo Linux in Azure](hpcpack-cluster-starccm.md)

