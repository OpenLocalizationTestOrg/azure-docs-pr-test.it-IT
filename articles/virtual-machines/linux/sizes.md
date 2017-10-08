---
title: dimensioni aaaLinux VM in Azure | Documenti Microsoft
description: Elenca le diverse dimensioni hello disponibili per le macchine virtuali Linux in Azure.
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a>Dimensioni delle macchine virtuali Linux in Azure
In questo articolo descrive le dimensioni disponibili hello e le opzioni di hello macchine virtuali di Azure è possibile utilizzare toorun Linux App e i carichi di lavoro. Fornisce inoltre toobe considerazioni sulla distribuzione conoscere quando si pianifica toouse queste risorse. Questo articolo è disponibile anche per le [macchine virtuali Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


| Tipo                     | Dimensioni           |    Descrizione       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [Utilizzo generico](sizes-general.md)          | Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7  | Rapporto equilibrato tra CPU e memoria. Ideale per i test e sviluppo, i database di piccole dimensioni toomedium e toomedium bassa il traffico web server. |
| [Ottimizzate per il calcolo](sizes-compute.md)        | Fs, F             | Rapporto elevato tra CPU e memoria. Soluzione idonea per server Web con livelli medi di traffico, dispositivi di rete, processi batch e server applicazioni.        |
| [Ottimizzate per la memoria](sizes-memory.md)         | Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D   | Rapporto elevato tra memoria e CPU. Ideale per i server di database relazionale, cache toolarge medium e analitica in memoria.                 |
| [Ottimizzate per l'archiviazione](sizes-storage.md)        | Ls                | I/O e velocità effettiva del disco elevati. Ideale per Big Data, database SQL e NoSQL.                                                         |
| [GPU](sizes-gpu.md)            | NV, NC            | Macchine virtuali specializzate ottimizzate per livelli intensivi di rendering della grafica e modifica di video, disponibili con GPU singole o più GPU.       |
| [High Performance Computing (HPC)](sizes-hpc.md) | H, A8-11          | Le nostre macchine virtuali con CPU più veloci e potenti, con interfacce di rete ad alta velocità effettiva facoltative (RDMA). 

<br>

- Per informazioni sui prezzi di hello diverse dimensioni, vedere [macchine virtuali: prezzi](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux). 
- Per la disponibilità delle dimensioni di VM nelle aree di Azure, vedere [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services/).
- toosee limiti generali in macchine virtuali di Azure, vedere [sottoscrizione di Azure e limiti dei servizi, quote e vincoli](../../azure-subscription-service-limits.md).
- Altre informazioni su come le [unità di calcolo di Azure](../windows/acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.


## <a name="rest-api"></a>API REST

Per informazioni sull'utilizzo di hello tooquery di API REST per dimensioni di macchina virtuale, vedere l'esempio hello:

- [List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Elencare le dimensioni delle macchine virtuali disponibili per il ridimensionamento)
- [List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Elencare le dimensioni delle macchine virtuali disponibili per una sottoscrizione)
- [List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Elencare le dimensioni delle macchine virtuali disponibili in un set di disponibilità)

## <a name="acu"></a>Unità di calcolo di Azure

Altre informazioni su come le [unità di calcolo di Azure](acu.md) consentono di confrontare le prestazioni di calcolo negli SKU di Azure.

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sulle dimensioni della VM diverse hello disponibili:
- [Utilizzo generico](sizes-general.md)
- [Ottimizzate per il calcolo](sizes-compute.md)
- [Ottimizzate per la memoria](sizes-memory.md)
- [Ottimizzate per l'archiviazione](sizes-storage.md)
- [GPU](sizes-gpu.md)
- [High Performance Computing (HPC)](sizes-hpc.md)



