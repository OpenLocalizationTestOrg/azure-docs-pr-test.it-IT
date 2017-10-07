---
title: dimensioni aaaAzure VM Linux - HPC | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibile per Linux elaborazione a elevate prestazioni macchine virtuali in Azure.
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a>Dimensioni delle macchine virtuali High Performance Computing (HPC) Linux

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Istanze con supporto per RDMA
Un subset delle istanze con utilizzo intensivo di calcolo di hello (H16r, H16mr, A8 e A9) funzionalità di un'interfaccia di rete per la connettività diretto a memoria remota (RDMA) di accesso. Questa interfaccia viene inoltre dimensioni di macchina virtuale disponibile tooother interfaccia toohello rete di Azure standard. 
  
Questa interfaccia consente toocommunicate istanze che supportano RDMA hello in una rete InfiniBand, operando a tariffe FDR per le macchine virtuali H16r e H16mr e di tariffe QDR per le macchine virtuali A8 e A9. È possibile migliorare le funzionalità RDMA hello scalabilità e prestazioni delle applicazioni di interfaccia MPI (Message Passing).

Di seguito sono i requisiti per le macchine virtuali Linux che supportano RDMA tooaccess hello rete RDMA di Azure:
 
* **Distribuzioni** : È necessario distribuire le macchine virtuali dal supporto per RDMA SUSE Linux Enterprise Server (SLES) o immagini Software Wave non autorizzato (in precedenza OpenLogic) basato su CentOS HPC in hello Azure Marketplace. Hello immagini Marketplace seguenti supportano la connettività RDMA:
  
    * SLES 12 SP1 per HPC o SLES 12 SP1 per HPC (Premium)
    
    * HPC basata su CentOS 7.3, HPC basata su CentOS 7.1, HPC basata su CentOS 6.8 o HPC basata su CentOS 6.5  
 
        > [!NOTE]
        > Per le macchine virtuali serie H è consigliabile un'immagine SLES 12 SP1 per HPC o un'immagine HPC basata su CentOS 7.1 o versione successiva.
        >
        > Le immagini basate su CentOS HPC hello, gli aggiornamenti kernel sono disabilitati in hello **yum** file di configurazione. In questo modo hello driver Linux RDMA vengono distribuiti come un pacchetto RPM e gli aggiornamenti dei driver potrebbero non funzionare se kernel hello viene aggiornato.
        > 
        > 
* **MPI** : Intel MPI Library 5.x.
  
    A seconda di un'immagine del Marketplace hello prescelto, installazione di gestione delle licenze, separata, o configurazione di Intel MPI potrebbe essere necessarie, come indicato di seguito: 
  
  * **SLES 12 SP1 per l'immagine HPC** -Intel MPI pacchetti vengono distribuiti in hello macchina virtuale. Installare eseguendo hello comando seguente:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Immagini HPC basate su CentOS** : Intel MPI 5.1 è già installato.  
    
    Configurazione di sistema aggiuntive non necessari toorun di processi MPI nel cluster macchine virtuali. Ad esempio, in un cluster di macchine virtuali, è necessario tooestablish trust tra hello nodi di calcolo. Per alcune impostazioni tipiche, vedere [impostare una di applicazioni MPI cluster toorun Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Considerazioni sulla topologia di rete
* Nelle macchine virtuali Linux con supporto per RDMA in Azure, Eth1 è riservato al traffico di rete RDMA. Non modificare le impostazioni della scheda Eth1 o tutte le informazioni nel file di configurazione hello che fa riferimento a rete toothis. Eth0 è riservato per il normale traffico di rete di Azure.

* In Azure, IP over InfiniBand (IB) non è supportato. Solo RDMA over IB è supportato.

## <a name="using-hpc-pack"></a>Utilizzo di HPC Pack
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuita HPC cluster e processi soluzione di gestione Microsoft, è un'opzione per consentire le istanze con utilizzo intensivo di calcolo di hello toouse con Linux. versioni più recenti di Hello di HPC Pack supportano diverse distribuzioni di Linux toorun nel calcolo nodi distribuiti nelle macchine virtuali di Azure, gestito da un nodo head di Windows Server. Con nodi di calcolo di Linux che supportano RDMA in esecuzione Intel MPI, HPC Pack può pianificare ed eseguire applicazioni MPI Linux rete con RDMA hello tale accesso. Vedere l'articolo di [introduzione ai nodi di calcolo Linux in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Altre dimensioni
- [Utilizzo generico](sizes-general.md)
- [Ottimizzate per il calcolo](sizes-compute.md)
- [Ottimizzate per la memoria](sizes-memory.md)
- [Ottimizzate per l'archiviazione](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Passaggi successivi

- tooget avviata la distribuzione e l'utilizzo di dimensioni elevate con RDMA su Linux, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.




