---
title: dimensioni delle macchine Virtuali di Windows di aaaAzure - HPC | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibile per Windows elaborazione a elevate prestazioni macchine virtuali in Azure.
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a>Dimensioni delle VM High Performance Computing (HPC)

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Istanze con supporto per RDMA
Un subset delle istanze con utilizzo intensivo di calcolo di hello (H16r, H16mr, A8 e A9) funzionalità di un'interfaccia di rete per la connettività diretto a memoria remota (RDMA) di accesso. Questa interfaccia viene inoltre dimensioni di macchina virtuale disponibile tooother interfaccia toohello rete di Azure standard. 
  
Questa interfaccia consente toocommunicate istanze che supportano RDMA hello in una rete InfiniBand, operando a tariffe FDR per le macchine virtuali H16r e H16mr e di tariffe QDR per le macchine virtuali A8 e A9. È possibile migliorare le funzionalità RDMA hello scalabilità e prestazioni delle applicazioni di interfaccia MPI (Message Passing).

Di seguito sono i requisiti per le macchine virtuali Windows con supporto per RDMA tooaccess hello rete RDMA di Azure: 

* **Sistema operativo**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Windows Server 2016 non supporta attualmente la connettività RDMA in Azure.
  >

* **Impostare la disponibilità o un servizio cloud** : le macchine virtuali che supportano RDMA hello Distribuisci in hello stesso set (quando si utilizza il modello di distribuzione del hello Azure Resource Manager) di disponibilità o hello nello stesso servizio cloud (quando si utilizza il modello di distribuzione classica hello). Se si utilizza Azure Batch, le macchine virtuali che supportano RDMA hello deve essere in hello stesso pool.

* **MPI** : Microsoft MPI (MS-MPI) 2012 R2 o versione successiva, Intel MPI Library 5.x

  Implementazioni MPI supportate utilizzano hello toocommunicate di interfaccia Microsoft Network Direct tra istanze. 

* **Spazio degli indirizzi di rete RDMA** -rete RDMA hello in Azure riserva hello indirizzo spazio 172.16.0.0/16. toorun di applicazioni MPI in istanze distribuite in una rete virtuale di Azure, assicurarsi che spazio degli indirizzi di rete virtuale hello non si sovrapponga rete RDMA hello.

* **Estensione HpcVmDrivers VM** -nelle macchine virtuali che supportano RDMA, è necessario aggiungere hello HpcVmDrivers estensione tooinstall rete driver di dispositivo Windows per la connettività RDMA. (In alcune distribuzioni di istanze A8 e A9, hello estensione HpcVmDrivers viene aggiunto automaticamente.) tooadd hello VM estensione tooa VM, è possibile utilizzare [Azure PowerShell](/powershell/azure/overview) cmdlet. 

  
  Hello comando Installa hello estensione HpcVMDrivers di versione 1.1 più recente in una macchina virtuale che supportano RDMA esistente denominata seguente *myVM* distribuito nel gruppo di risorse hello denominato *myResourceGroup* in hello  *Stati Uniti occidentali* area:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Per altre informazioni, vedere [Estensioni e funzionalità della macchina virtuale](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). È anche possibile operare con le estensioni per le macchine virtuali distribuite in hello [modello di distribuzione classica](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Utilizzo di HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuita HPC cluster e processi soluzione di gestione Microsoft, è una delle opzioni per si toocreate un cluster di calcolo in applicazioni MPI basati su Windows Azure toorun e altri carichi di lavoro HPC. HPC Pack 2012 R2 e versioni successive includono un ambiente di runtime per MS-MPI che utilizza hello rete RDMA di Azure quando distribuito in macchine virtuali che supportano RDMA.




## <a name="other-sizes"></a>Altre dimensioni
- [Utilizzo generico](sizes-general.md)
- [Ottimizzate per il calcolo](sizes-compute.md)
- [Ottimizzate per la memoria](../virtual-machines-windows-sizes-memory.md)
- [Ottimizzate per l'archiviazione](../virtual-machines-windows-sizes-storage.md)
- [Ottimizzate per la GPU](sizes-gpu.md)

## <a name="next-steps"></a>Passaggi successivi

- Per elenchi di controllo toouse hello complesse le istanze con HPC Pack in Windows Server, vedere [configurazione di un cluster di Windows RDMA con applicazioni MPI di HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- le istanze con utilizzo intensivo di calcolo di toouse durante l'esecuzione di applicazioni MPI con Azure Batch, vedere [multi-istanza usare attività toorun applicazioni di interfaccia MPI (Message Passing) in Azure Batch](../../batch/batch-mpi.md).

- Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.




