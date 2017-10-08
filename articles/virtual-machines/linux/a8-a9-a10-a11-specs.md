---
title: aaaAbout complesse le macchine virtuali con Linux | Documenti Microsoft
description: Ottenere informazioni generali e considerazioni per l'utilizzo delle dimensioni di hello H serie e A8, A9, A10 e A11 complesse per le macchine virtuali Linux
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Informazioni sulle macchine virtuali serie H e serie A a elevato utilizzo di calcolo per Linux
Ecco informazioni complementari e alcune considerazioni per l'utilizzo di hello serie H Azure più recente e hello precedenti dimensioni A8, A9, A10 e A11, noto anche come *complesse* istanze. Questo articolo illustra l'uso di queste dimensioni per macchine virtuali Linux. È possibile usarle anche per [macchine virtuali di Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Per conoscere le specifiche di base, le capacità di archiviazione e i dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Rete con RDMA toohello accesso
È possibile creare cluster di macchine virtuali di Linux che supportano RDMA che eseguono una delle seguenti distribuzioni Linux HPC supportate e un vantaggio di tootake implementazione MPI supportato di rete RDMA di Azure hello hello. Vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) per passaggi di configurazione di esempio e le opzioni di distribuzione.

* **Distribuzioni** : È necessario distribuire le macchine virtuali dal supporto per RDMA SUSE Linux Enterprise Server (SLES) o immagini Software Wave non autorizzato (in precedenza OpenLogic) basato su CentOS HPC in hello Azure Marketplace. Hello immagini Marketplace seguenti supportano la connettività RDMA:
  
    * SLES 12 SP1 per HPC, SLES 12 SP1 per HPC (Premium)
    
    * HPC 7.1 basata su CentOS, HPC 6.5 basata su CentOS  
 
        > [!NOTE]
        > Per le macchine virtuali serie H è consigliabile un'immagine SLES 12 SP1 per HPC o un'immagine HPC basata su CentOS 7.1.
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
    
    Configurazione di sistema aggiuntive non necessari toorun di processi MPI nel cluster macchine virtuali. Ad esempio, in un cluster di macchine virtuali, è necessario tooestablish trust tra hello nodi di calcolo. Per alcune impostazioni tipiche, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Considerazioni per HPC Pack e Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuita HPC cluster e processi soluzione di gestione Microsoft, fornisce un'opzione per consentire le istanze con utilizzo intensivo di calcolo di hello toouse con Linux. versioni più recenti di Hello di HPC Pack supportano diverse distribuzioni di Linux toorun nel calcolo nodi distribuiti nelle macchine virtuali di Azure, gestito da un nodo head di Windows Server. Con nodi di calcolo di Linux che supportano RDMA in esecuzione Intel MPI, HPC Pack può pianificare ed eseguire applicazioni MPI Linux rete con RDMA hello tale accesso. tooget introduzione, vedere [Introduzione a Linux nodi di calcolo in un cluster HPC Pack in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Considerazioni sulla topologia di rete
* Nelle macchine virtuali Linux con supporto per RDMA in Azure, Eth1 è riservato al traffico di rete RDMA. Non modificare le impostazioni della scheda Eth1 o tutte le informazioni nel file di configurazione hello che fa riferimento a rete toothis. Eth0 è riservato per il normale traffico di rete di Azure.
* In Azure, IP over InfiniBand (IB) non è supportato. Solo RDMA over IB è supportato.



## <a name="next-steps"></a>Passaggi successivi
* Per informazioni sulla disponibilità e prezzi di dimensioni elevate hello, vedere [prezzi-macchine virtuali](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Per informazioni sulle funzionalità di archiviazione e dettagli relativi ai dischi, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* tooget avviata la distribuzione e l'utilizzo di dimensioni elevate con RDMA su Linux, vedere [impostare un applicazioni MPI di Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

